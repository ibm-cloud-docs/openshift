---

copyright: 
  years: 2014, 2024
lastupdated: "2024-03-15"


keywords: openshift, kubernetes, kernel, performance

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Tuning performance
{: #kernel}

If you have specific performance optimization requirements, you can change the default settings for some cluster components in {{site.data.keyword.openshiftlong}}.
{: shortdesc}

If you choose to change the default settings, you are doing so at your own risk. You are responsible for running tests against any changed settings and for any potential disruptions caused by the changed settings in your environment.
{: important}


Instead of tuning worker node performance with `MachineConfig` files in {{site.data.keyword.redhat_openshift_notm}}, you can modify the host with a `daemonset` file. For more information, see [Changing the Calico MTU](/docs/openshift?topic=openshift-kernel#calico-mtu) or [Tuning performance for Red Hat CoreOS worker nodes](/docs/openshift?topic=openshift-rhcos-performance).
{: note}



## Default worker node settings
{: #worker-default}

By default, your worker nodes have the operating system and compute hardware of the [worker node flavor](/docs/openshift?topic=openshift-planning_worker_nodes) that you choose when you create the worker pool.
{: shortdesc}

### Customizing the operating system
{: #worker-default-os}

You can find a list of supported operating systems by cluster version in the [{{site.data.keyword.openshiftshort}} version information](/docs/openshift?topic=openshift-openshift_versions). Your cluster can't mix operating systems or use different operating systems.
{: shortdesc}

To optimize your worker nodes, consider the following information.
* **Image and version updates**: Worker node updates, such as security patches to the image or {{site.data.keyword.redhat_openshift_notm}} versions, are provided by IBM for you. However, you choose when to apply the updates to the worker nodes. For more information, see [Updating clusters, worker nodes, and cluster components](/docs/openshift?topic=openshift-update).
* **Temporary modifications**: If you log in to a pod or use some other process to modify a worker node setting, the modifications are temporary. Worker node lifecycle operations, such as autorecovery, reloading, updating, or replacing a worker node, change any modifications back to the default settings.
* **Persistent modifications**: For modifications to persist across worker node lifecycle operations, create a daemon set that uses an `init` container. For more information, see [Modifying default worker node settings to optimize performance](#worker).

Modifications to the operating system are not supported. If you modify the default settings, you are responsible for debugging and resolving the issues that might occur.
{: important}

### Hardware changes
{: #worker-default-hw}

To change the compute hardware, such as the CPU and memory per worker node, choose among the following options.
* Create a worker pool. The instructions vary depending on the type of infrastructure for the cluster, such as classic, VPC, or {{site.data.keyword.satelliteshort}}. For more information, see [Adding worker nodes to Classic clusters](/docs/openshift?topic=openshift-add-workers-classic) or [Adding worker nodes to VPC clusters](/docs/openshift?topic=openshift-add-workers-vpc). 
* [Update the flavor](/docs/openshift?topic=openshift-update#machine_type) in your cluster by creating a worker pool and removing the previous worker pool.

## Modifying worker node settings to optimize performance
{: #worker}




### Modifying worker node settings by using the Node Tuning Operator
{: #worker-nto}

You can use the node tuning operator to tune worker node performance by creating custom profiles. For more information, see the {{site.data.keyword.redhat_notm}} [Node Tuning Operator](https://docs.openshift.com/container-platform/4.7/scalability_and_performance/using-node-tuning-operator.html){: external} docs.

{{site.data.keyword.redhat_notm}} SRE is not responsible for the tuning and performance management of nodes that are customized with the Node Tuning Operator (NTO). If changes made by the NTO cause the worker nodes to be unavailable for scheduling or unresponsive, then revert the changes made by using the NTO.
{: important}
    
1. Save the following example `Tuned` resource to a file called `tuned-node.yaml` and include the specifications you want to use for your worker nodes. Note that you can use the `recommend` method to apply the settings to your worker nodes by using node labels. In this example, the profile is called `tuned-node` and applies to worker nodes with the label `label: node-role.kubernetes.io/master` label.

    If you have custom labels on your worker nodes, or if you want to tune only certain workers in your cluster, you can [label your worker nodes](/docs/openshift?topic=openshift-worker-tag-label), then use those labels in your tuning configuration.
    {: tip}

    Example custom `Tuned` profile. For more information about customizing your `Tuned` profile, see [Node Tuning Operator](https://docs.openshift.com/container-platform/4.7/scalability_and_performance/using-node-tuning-operator.html){: external} docs.
    
    ```yaml
    apiVersion: tuned.openshift.io/v1
    kind: Tuned
    metadata:
      name: tuned-node
      namespace: openshift-cluster-node-tuning-operator
    spec:
      profile:
      - data: |
          [main]
          summary=Custom OpenShift node profile for my workloads
          include=openshift-control-plane
          [sysctl]
          kernel.sem="250 1024000 200 32768"
          kernel.msgmax="65536"
          kernel.shmmni="32768"
        name: openshift-node-parms
      recommend:
      - match:
        - label: node-role.kubernetes.io/master
        priority: 10
        profile: openshift-node-parms
    ```
    {: codeblock}

1. Create the custom `tuned-node` profile in your cluster.
    ```sh
    oc apply -f tuned-node.yaml
    ```
    {: pre}
    
The `oc debug` pods do not have access to retrieve worker node tuned profile settings. To retrieve or verify the updated worker node settings, you must be logged into a pod that has `hostIPC: true`.
{: note}





### Modifying worker node kernel settings
{: #worker-kernel-ds}

If you have specific performance optimization requirements, you can change the default settings for the Linux kernel `sysctl` parameters on worker nodes.
{: shortdesc}

Worker nodes are automatically provisioned with optimized kernel performance, but you can change the default settings by applying a custom [Kubernetes `DaemonSet`](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/){: external} with an [`init` Container](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/){: external} to your cluster. The daemon set modifies the settings for all existing worker nodes and applies the settings to any new worker nodes that are provisioned in the cluster. The `init` container makes sure that these modifications occur before other pods are scheduled on the worker node. No pods are affected.

You must have the [**Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/openshift?topic=openshift-iam-platform-access-roles) for all namespaces to run the sample privileged `initContainer`. After the containers for the deployments are initialized, the privileges are dropped.
{: note}

Before you begin: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Save the following daemon set in a file named `worker-node-kernel-settings.yaml`. In the `spec.template.spec.initContainers` section, add the fields and values for the `sysctl` parameters that you want to tune. This example daemon set changes the default maximum number of connections that are allowed in the environment via the `net.core.somaxconn` setting and the ephemeral port range via the `net.ipv4.ip_local_port_range` setting.

    Depending on the `systctl` settings that you try to change, you might want to configure the security context. For more information, see the [{{site.data.keyword.redhat_openshift_notm}} documentation](https://docs.openshift.com/container-platform/4.14/nodes/containers/nodes-containers-sysctls.html){: external}.
    {: note}

    
    ```yaml
    apiVersion: apps/v1
    kind: DaemonSet
    metadata:
      name: kernel-optimization
      namespace: kube-system
      labels:
        tier: management
        app: kernel-optimization
    spec:
      selector:
        matchLabels:
          name: kernel-optimization
      template:
        metadata:
          labels:
            name: kernel-optimization
        spec:
          hostNetwork: true
          hostPID: true
          hostIPC: true
          initContainers:
            - command:
                - sh
                - -c
                - sysctl -w net.ipv4.ip_local_port_range="1025 65535"; sysctl -w net.core.somaxconn=32768;
              image: alpine:3.6
              imagePullPolicy: IfNotPresent
              name: sysctl
              resources: {}
              securityContext:
                privileged: true
                capabilities:
                  add:
                    - NET_ADMIN
              volumeMounts:
                - name: modifysys
                  mountPath: /sys
          containers:
            - resources:
                requests:
                  cpu: 0.01
              image: alpine:3.6
              name: sleepforever
              command: ["/bin/sh", "-c"]
              args:
                - >
                  while true; do
                    sleep 100000;
                  done
          volumes:
            - name: modifysys
              hostPath:
                path: /sys
    ```
    {: codeblock}

1. Apply the daemon set to your worker nodes. The changes are applied immediately.
    ```sh
    oc apply -f worker-node-kernel-settings.yaml
    ```
    {: pre}

To revert your worker nodes `sysctl` parameters to the default values, follow these steps.

1. Delete the daemon set. The `initContainers` that applied the custom settings are removed.
    ```sh
    oc delete ds kernel-optimization
    ```
    {: pre}

1. [Reboot all worker nodes in the cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot). The worker nodes come back online with the default values applied.





## Optimizing network keepalive `sysctl` settings
{: #keepalive-iks}

If a pod has long running TCP connections that are occasionally disconnected when they are idle for a period of time, it might help to change the `sysctl` keepalive settings for the pod. 
{: shortdesc}

These scenarios and suggested settings are also described in the [Troubleshooting Outgoing Connection Issues with IBM VPC Public and Service Gateways](https://www.ibm.com/blog/troubleshooting-outgoing-connection-issues-with-ibm-vpc-public-and-service-gateways/){: external} blog.
{: tip}

The following `sysctl` network values can be set on all worker nodes in a cluster by using the daemonset described in the [Modifying worker node kernel settings](#worker-kernel-ds) section. However, there currently isn't a way to set these `sysctl` keepalive settings on all pods by default in a cluster. The best way to modify the settings on all pods is to use a privileged `initContainer`. Review the following example of how to set up an `initContainer` for a deployment in a `test-ns` namespace.



Allow privileged `initContainers` in the `test-ns` namespace: 

    ```sh
    oc adm policy add-scc-to-groupl privileged system:serviceaccounts:test-ns
    ```
    {: pre}



Deploy the following example `initContainer`. Remember to change the `containers:` section to your own application containers. The `initContainer` then sets the `sysctl` settings for all the regular containers in the pod because they all share the same network namespace.

    ```sh
    kubectl apply -f - << EOF
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: test-sysctl
      namespace: test-ns
      labels:
        run: test-sysctl
    spec:
      replicas: 2
      selector:
        matchLabels:
          run: test-sysctl
      template:
        metadata:
          labels:
            run: test-sysctl
        spec:
          initContainers:
          - command:
            - sh
            - -c
            - sysctl -e -w net.ipv4.tcp_keepalive_time=40; sysctl -e -w net.ipv4.tcp_keepalive_intvl=15; sysctl -e -w net.ipv4.tcp_keepalive_probes=6;
            image: us.icr.io/armada-master/alpine:latest
            imagePullPolicy: IfNotPresent
            name: sysctl-init
            resources: {}
            securityContext:
              privileged: true
          containers:
          - name: test-sysctl
            image: us.icr.io/armada-master/alpine:latest
            command: ["sleep", "2592000"]
      EOF
    ```
    {: pre}
      


## Changing the Calico maximum transmission unit (MTU)
{: #calico-mtu}

Increase or decrease the Calico plug-in maximum transmission unit (MTU) to meet the network throughput requirements of your environment.
{: shortdesc}

All VPC workers nodes support jumbo frames. However, on classic infrastructure, only bare metal workers support jumbo frames.
{: important}

By default, the Calico network plug-in in your {{site.data.keyword.openshiftlong_notm}} cluster has an MTU of 1480 bytes. For most cases, this default MTU value provides sufficient throughput for packets that are sent and received in your network workloads. Review the following cases in which you might need to modify the default Calico MTU:

* Jumbo frames have an MTU value in the range of 1500 to 9000. To ensure that your cluster's pod network can use this higher MTU value, you can increase the Calico MTU to 20 bytes less than the jumbo frame MTU. This 20 byte difference allows space for packet header on encapsulated packets. For example, if your worker nodes' jumbo frames are set to 9000, you can set the Calico MTU to 8980. Note that all worker nodes in the cluster must use the same Calico MTU, so to increase the Calico MTU, all worker nodes in the cluster must be bare metal and use jumbo frames.
* If you have a VPN connection set up for your cluster, some VPN connections require a smaller Calico MTU than the default. Check with the VPN service provider to determine whether a smaller Calico MTU is required.
* If your cluster's worker nodes exist on different subnets, increasing the MTU value for the worker nodes and for the Calico MTU can allow pods to use the full bandwidth capability of the worker nodes.


Before you begin
:   If your worker nodes still run the default MTU value, increase the MTU value for your worker nodes first before you increase the MTU value for the Calico plug-in. For example, you can apply the following daemon set to change the MTU for your worker nodes jumbo frames to 9000 bytes. Note the interface names that are used in the **`ip link`** command vary depending on the type of your worker nodes.
    - Example command for Bare Metal worker nodes: `ip link set dev bond0 mtu 9000;ip link set dev bond1 mtu 9000;`
    - Example command VPC Gen 2 worker nodes: `ip link set dev ens3 mtu 9000;`

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: jumbo-apply
  namespace: kube-system
  labels:
    tier: management
    app: jumbo-apply
spec:
  selector:
    matchLabels:
      name: jumbo-apply
  template:
    metadata:
      labels:
        name: jumbo-apply
    spec:
      hostNetwork: true
      hostPID: true
      hostIPC: true
      tolerations:
      - operator: Exists
      initContainers:
        - command:
            - sh
            - -c
            - ip link set dev bond0 mtu 9000;ip link set dev bond1 mtu 9000; # Update this command based on your worker node type.
          image: alpine:3.6
          imagePullPolicy: IfNotPresent
          name: iplink
          resources: {}
          securityContext:
            privileged: true
            capabilities:
              add:
                - NET_ADMIN
          volumeMounts:
            - name: modifysys
              mountPath: /sys
      containers:
        - resources:
            requests:
              cpu: 0.01
          image: alpine:3.6
          name: sleepforever
          command: ["/bin/sh", "-c"]
          args:
            - >
              while true; do
                sleep 100000;
              done
      volumes:
        - name: modifysys
          hostPath:
             path: /sys
```
{: codeblock}





### Updating the Calico installation 
{: #calico-mtu-43}

After [applying the DaemonSet to increase the Calico plug-in MTU](#calico-mtu), complete the following steps to update the Calico installation.


To run your {{site.data.keyword.redhat_openshift_notm}} cluster, make sure that the MTU is equal to or greater than 1450 bytes.
{: important}

1. Edit the `default` Calico installation resource.
    ```sh
    oc edit installation default -n calico-system
    ```
    {: pre}

2. In the `spec.calicoNetwork` section, change the value of the `mtu` field.
    ```yaml
    ...
    spec:
      calicoNetwork:
        ipPools:
        - cidr: 172.30.0.0/16
          encapsulation: IPIPCrossSubnet
          natOutgoing: Enabled
          nodeSelector: all()
        mtu: 8980
        nodeAddressAutodetectionV4:
          interface: (^bond0$|^eth0$|^ens6$|^ens3$)
      kubernetesProvider: OpenShift
      registry: registry.ng.bluemix.net/armada-master/
      variant: Calico
    status:
      variant: Calico
    ```
    {: screen}

    To run your {{site.data.keyword.redhat_openshift_notm}} cluster, make sure that the MTU is equal to or greater than 1450 bytes.
    {: important}

3. Save and close the file.

4. Apply the MTU changes to your worker nodes by [rebooting all worker nodes in your cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot).



## Disabling the port map plug-in
{: #calico-portmap}

The `portmap` plug-in for the Calico container network interface (CNI) enables you to use a `hostPort` to expose your app pods on a specific port on the worker node. Prevent iptables performance issues by removing the port map plug-in from your cluster's Calico CNI configuration.
{: shortdesc}

When you have many services in your cluster, such as more than 500 services, or many ports on services, such as more than 50 ports per service for 10 or more services, many iptables rules are generated for the Calico and Kubernetes network policies for these services. Using many iptables rules can lead to performance issues for the port map plug-in, and might prevent future updates of iptables rules or cause the `calico-node` container to restart when no lock is received to make iptables rules updates within a specified time. To prevent these performance issues, you can disable the port map plug-in by removing it from your cluster's Calico CNI configuration.

If you must use `hostPorts`, don't disable the port map plug-in.
{: note}


1. Edit the `default` Calico installation resource.
    ```sh
    oc edit installation default -n calico-system
    ```
    {: pre}

1. In the `spec.calicoNetwork` section, change the value of `hostPorts` to `Disabled`.
    ```yaml
    ...
    spec:
      calicoNetwork:
        hostPorts: Disabled
        ipPools:
        - cidr: 172.30.0.0/16
          encapsulation: IPIPCrossSubnet
          natOutgoing: Enabled
          nodeSelector: all()
        mtu: 1480
        nodeAddressAutodetectionV4:
          interface: (^bond0$|^eth0$|^ens6$|^ens3$)
      kubernetesProvider: OpenShift
      registry: registry.ng.bluemix.net/armada-master/
      variant: Calico
    status:
      variant: Calico
    ```
    {: screen}

1. Save and close the file. Your changes are automatically applied.


