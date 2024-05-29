---

copyright:
  years: 2024, 2024
lastupdated: "2024-05-29"


keywords: pods, pod connectvity, networking, pod networking, pod trouble shooting, pod debug

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Debugging network connections between pods
{: #debug_pods}

Review the options and strategies for debugging connection issues between pods.

## Check the health of your cluster components and networking pods
{: #debug_pods_health}

Follow these steps to check the health of your components. Networking issues might occur if your cluster components are not up to date or are not in a healthy state.

1. Check that your cluster master and worker nodes run on a supported version and are in a healthy state. If the cluster master or workers do not run a supported version, [make any necessary updates](/docs/containers?topic=containers-update) so that they run a supported version. If the status of any components is not `Normal` or `Ready`, review the [cluster master health states](/docs/containers?topic=containers-debug_master), [cluster states](https://cloud.ibm.com/docs/containers?topic=containers-cluster-states-reference), or [worker node states](/docs/containers?topic=containers-worker-node-state-reference) for more information. Make sure any related issues are resolved before continuing. 

    To check the cluster master version and health:
    ```sh
    ibmcloud oc cluster get -c <cluster-id>
    ```
    {: pre}

    To check worker node versions and health:
    ```sh
    ibmcloud oc workers -c <cluster-id>
    ```
    {: pre}

2. For each worker node, verify that the Calico and cluster DNS pods are present and running in a healthy state. 
    1. Run the command to get the details of your cluster's pods. 

        ```sh
        oc get pods -A -o wide | grep calico
        ```
        {: pre}

    2. In the output, make sure that your cluster includes the following pods. Make sure that each pod's status is `Running`, and that the pods do not have too many restarts.
        - Exactly one `calico-node` pod per worker node. 
        - At least one `calico-typha` pod per cluster. Larger clusters may have more than one. 
        - Exactly one `calico-kube-controllers` pod per cluster. 
        - At least one `dns-default` pod per cluster. Larger clusters may have more than one. 

        Example output. 

        ```sh
        NAMESPACE       NAME                                       READY   STATUS     RESTARTS    AGE   IP              NODE           NOMINATED NODE   READINESS GATES
        calico-system   calico-kube-controllers-7dbc745664-vp7kh   1/1     Running    0           34h   172.17.24.75    192.168.0.22   <none>           <none>
        calico-system   calico-node-h9gpz                          1/1     Running    1           34h   192.168.0.22    192.168.0.22   <none>           <none>
        calico-system   calico-node-z8tb9                          1/1     Running    0           34h   192.168.0.21    192.168.0.21   <none>           <none>
        calico-system   calico-typha-5bdc4ddb57-h7jfd              1/1     Running    0           34h   192.168.0.22    192.168.0.22   <none>           <none>
        ```
        {: screen}

    3. If any of the listed pods are not present or are in an unhealthy state, go through the cluster and worker node trouble shooting documentation included in the previous steps. Make sure any issues with the pods in this step are resolved before moving on.


## Debug with test pods 
{: #debug_pods_test}

To determine the cause of networking issues on your pods, you can create a test pod on each of your worker nodes. Then, you can run tests and observe networking activity within the pod, which might reveal the source of the problem. 

### Setting up the pods
{: #debug_pods_test_setup}

1. Create a new privileged namespace for your test pods. Creating a new namespace prevents any custom policies or configurations in existing namespaces from affecting your test pods. In this example, the new namespace is called `pod-network-test`.

    Create the namespace. 

    ```sh
    oc create ns pod-network-test
    ```
    {: pre}

    Add labels to the namespace. 

    ```sh
    oc label namespace pod-network-test --overwrite=true \
                pod-security.kubernetes.io/enforce=privileged \
                pod-security.kubernetes.io/enforce-version=latest \
                pod-security.kubernetes.io/audit=privileged \
                pod-security.kubernetes.io/audit-version=latest \
                pod-security.kubernetes.io/warn=privileged \
                pod-security.kubernetes.io/warn-version=latest \
                security.openshift.io/scc.podSecurityLabelSync="false"
    ```
    {: pre}

1. Run the command to allow the namespace to run pods with a privileged security context.

```sh
oc adm policy add-scc-to-group privileged system:serviceaccounts:pod-network-test 
```
{: pre}


1. Create and apply a daemonset that creates a test pod on each node. Choose the correct daemonset based on your cluster connectivity (public, private, or none). You can make additional customizations to the daemonset as needed. 

    **For clusters with public connectivity.** This daemonset uses an image from Docker.

    ```yaml
    apiVersion: apps/v1
    kind: DaemonSet
    metadata:
      labels:
        name: nginx-test
        app: nginx-test
      name: nginx-test
    spec:
      selector:
        matchLabels:
          name: nginx-test
      template:
        metadata:
          labels:
            name: nginx-test
            app: nginx-test
        spec:
          tolerations:
          - operator: "Exists"
          containers:
          - name: nginx
            securityContext:
              privileged: true
            image: docker.io/nginx:latest
            ports:
            - containerPort: 80
    ```
    {: codeblock}

    **For clusters with private connectivity.** This daemonset uses the `us.icr.io/armada-master/network-alpine:latest` image from IBM Container Registry. 

    ```yaml
    apiVersion: apps/v1
    kind: DaemonSet
    metadata:
      labels:
        name: nginx-test
        app: nginx-test
      name: nginx-test
    spec:
      selector:
        matchLabels:
          name: nginx-test
      template:
        metadata:
          labels:
            name: nginx-test
            app: nginx-test
        spec:
          nodeSelector:
            kubernetes.io/hostname: 10.1.1.1
          tolerations:
          - operator: "Exists"
          containers:
          - name: nginx
            securityContext:
              privileged: true
            image: us.icr.io/armada-master/network-alpine:latest
            command: ["/bin/sh"]
            args: ["-c", "echo Hello from ${POD_NAME} > /root/index.html && while true; do { echo -ne \"HTTP/1.0 200 OK\r\nContent-Length: $(wc -c </root/index.html)\r\n\r\n\"; cat /root/index.html; } | nc -l -p 80; done"]
            env:
              - name: POD_NAME
                valueFrom:
                  fieldRef:
                    fieldPath: metadata.name
            ports:
            - containerPort: 80
    ```
    {: codeblock}

    **For clusters with no outbound connectivity at all.** This daemonset allows you to use the `ping`, `dig`, and `nc` commands without requiring outbound connectivity. 

    ```yaml
    apiVersion: apps/v1
    kind: DaemonSet
    metadata:
      labels:
        name: test-client
        app: test-client
      name: test-client
    spec:
      selector:
        matchLabels:
          name: test-client
      template:
        metadata:
          labels:
            name: test-client
            app: test-client
        spec:
          tolerations:
          - operator: "Exists"
          nodeSelector:
            kubernetes.io/hostname: 10.1.1.1
        containers:
        - name: test-client
          securityContext:
            privileged: true
          image: us.icr.io/armada-master/network-alpine:latest
          command: ["/bin/sh"]
          args: ["-c", "echo Hi && while true; do sleep 86400; done"]
    ```
    {: codeblock}

1. Apply the daemonset to deploy test pods on your worker nodes. 

```sh
oc apply --namespace pod-network-test -f <daemonset-file>
```
{: pre}

1. Verify that the pods start up successfully by listing all pods in the namespace. 
    ```sh
    oc get pods --namespace pod-network-test -o wide
    ```
    {: pre}

If you are using an image from your private container registry and you see pull errors due to not having the proper authority, try deploying the daemonset in the `default` namespace instead.
{: tip}

### Running tests within the pods
{: #debug_pods_test_run}

Run `curl`, `ping`, and `nc` commands to test each pod's network connection and the `dig` command to test the cluster DNS. Review each output, then see [Identifying issues](#debug_pods_test_id) to find what the outcomes might mean. 


1. List your test pods and note the name and IP of each pod. 

    ```sh
    oc get pods --namespace pod-network-test -o wide
    ```
    {: pre}

    Example output. 

    ```sh
    NAME               READY   STATUS    RESTARTS   AGE   IP               NODE             NOMINATED NODE   READINESS GATES
    nginx-test-dgbkz   1/1     Running   0          18s   172.30.208.211   10.188.102.116   <none>           <none>
    nginx-test-v8lvz   1/1     Running   0          18s   172.30.248.201   10.188.102.120   <none>           <none>
    ```
    {: screen}

1. Run the `exec` command to log into one pod. 

    ```sh
    kubectl exec -it --namespace pod-network-test <pod_name> -- sh
    ```
    {: pre}

1. Run the `curl` command on the pod and note the output. Specify the IP of the pod that you did **not** log into. This tests the network connection between pods on different nodes. 

    ```sh
    curl <pod_ip>
    ```
    {: pre}

    Example successful output. 

    ```sh
    Welcome to nginx!
    If you see this page, the nginx web server is successfully installed and
    working. Further configuration is required.
    ```
    {: screen}

1. Run the `ping` command on the pod and note the output. Specify the IP of the pod that you did **not** log into with the `exec` command. This tests the network connection between pods on different nodes. 

    ```sh
    ping -c 5 <pod_ip>
    ```
    {: pre}

    Example successful output. 

    ```sh
    PING 172.30.248.201 (172.30.248.201) 56(84) bytes of data.
    64 bytes from 172.30.248.201: icmp_seq=1 ttl=62 time=0.473 ms
    64 bytes from 172.30.248.201: icmp_seq=2 ttl=62 time=0.449 ms
    64 bytes from 172.30.248.201: icmp_seq=3 ttl=62 time=0.381 ms
    64 bytes from 172.30.248.201: icmp_seq=4 ttl=62 time=0.438 ms
    64 bytes from 172.30.248.201: icmp_seq=5 ttl=62 time=0.348 ms

    --- 172.30.248.201 ping statistics ---
    5 packets transmitted, 5 received, 0% packet loss, time 4086ms
    rtt min/avg/max/mdev = 0.348/0.417/0.473/0.046 ms
    ```
    {: screen}

1. Run the `nc` command on the pod and note the output. Specify the IP of the pod that you did **not** log into with the `exec` command. This tests the network connection between pods on different nodes. 

    ```sh
    nc -vzw 5 <pod_ip> 80
    ```
    {: pre}

    Example successful output. 

    ```sh
    Ncat: Version 7.93 ( https://nmap.org/ncat )
    Ncat: Connected to 172.30.248.201:80.
    Ncat: 0 bytes sent, 0 bytes received in 0.12 seconds.
    ```
    {: screen}

1. Run the `dig` commands to test the DNS. 

    ```sh
    dig +short kubernetes.default.svc.cluster.local
    ```
    {: pre}

    Example output. 

    ```sh
    172.21.0.1
    ```
    {: screen}

    ```sh
    dig +short ibm.com
    ```
    {: pre}

    Example output. 

    ```sh
    23.50.74.64
    ```
    {: screen}

1. Run `curl` commands to test a full TCP or HTTPS connection to the service. This example tests the connection between the pod and the cluster master by retrieving the cluster's version information. Successfully retrieving the cluster version indicates a healthy connection. 

    ```sh
    curl -k https://kubernetes.default.svc.cluster.local/version
    ```
    {: pre}

    Example output.

    ```sh
    {
    "major": "1",
    "minor": "25",
    "gitVersion": "v1.25.14+bcb9a60",
    "gitCommit": "3bdfba0be09da2bfdef3b63e421e6a023bbb08e6",
    "gitTreeState": "clean",
    "buildDate": "2023-10-30T21:33:07Z",
    "goVersion": "go1.19.13 X:strictfipsruntime",
    "compiler": "gc",
    "platform": "linux/amd64"
    }
    ```
    {: screen}

1. Log out of the pod. 

    ```sh
    exit
    ```
    {: pre}

1. Repeat the earlier steps with the remaining pods.

### Identifying issues
{: #debug_pods_test_id}

Review the outputs from the earlier section to help find the cause of your pod networking issues. This section lists some common causes that can be identified from the earlier section. 

- If the commands functioned normally on the test pods, but you still have networking issues in your application pods in your default namespace, there might be issues related specifically to your application. 
    - You might have Calico or Kubernetes network security policies in place that restrict your networking traffic. If a networking policy is applied to a pod, *all traffic that is not specifically allowed by that policy is dropped*. For more information on networking policies, see the [Kubernetes documentation](https://kubernetes.io/docs/concepts/services-networking/network-policies/){: external}. 
    - If you are using Istio or Red Hat OpenShift Service Mesh, there may be service configuration issues that drop or block traffic between pods. For more information, see the troubleshooting documentation for [Istio](https://istio.io/latest/docs/ops/diagnostic-tools/){: external} and [Red Hat OpenShift Service Mesh](https://docs.openshift.com/container-platform/4.14/service_mesh/v2x/ossm-troubleshooting-istio.html){: external}. 
    - The issue might be related to bugs in the application rather than your cluster, and might require your own independent trouble shooting. 

- If the `curl`, `ping`, or `nc` commands failed for certain pods, identify which worker nodes those pods are on. If the issue exists on only some of your worker nodes, [replace those worker nodes](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_replace) or see additional information on [worker node trouble shooting](/docs/openshift?topic=openshift-ts-critical-notready). 

- If the DNS lookups from the `dig` commands failed,  See the [Red Hat DNS troubleshooting information](https://access.redhat.com/solutions/3804501){: external}. 

If you are still unable to resolve your pod networking issue, [open a support case](/docs/get-support?topic=get-support-open-case) and include a detailed description of the problem, how you have tried to solve it, what kinds of tests you ran, and [relevant logs](/docs/containers?topic=containers-debug_clusters&interface=ui#ts-5) for your pods and worker nodes. For more information on opening a support case and what information to include, see the [general debugging guide](/docs/containers?topic=containers-debug_clusters&interface=ui#ts-3).



