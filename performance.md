---

copyright: 
  years: 2014, 2024
lastupdated: "2024-11-11"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, kernel, performance

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

By default, your worker nodes have the operating system and compute hardware of the worker node flavor that you choose when you create the worker pool.
{: shortdesc}

### Customizing the operating system
{: #worker-default-os}

You can find a list of supported operating systems by cluster version in the [{{site.data.keyword.openshiftshort}} version information](/docs/openshift?topic=openshift-openshift_versions). Your cluster can't mix operating systems or use different operating systems.
{: shortdesc}

To optimize your worker nodes, consider the following information.
* **Image and version updates**: Worker node updates, such as security patches to the image or {{site.data.keyword.redhat_openshift_notm}} versions, are provided by IBM for you. However, you choose when to apply the updates to the worker nodes. For more information, see [Updating clusters, worker nodes, and cluster components](/docs/openshift?topic=openshift-update).
* **Temporary modifications**: If you log in to a pod or use some other process to modify a worker node setting, the modifications are temporary. Worker node lifecycle operations, such as autorecovery, reloading, updating, or replacing a worker node, change any modifications back to the default settings.
* **Persistent modifications**: For modifications to persist across worker node lifecycle operations, create a daemon set that uses an `init` container. For more information, see [Modifying default worker node settings to optimize performance](#worker-kernel-ds).

Modifications to the operating system are not supported. If you modify the default settings, you are responsible for debugging and resolving the issues that might occur.
{: important}

### Hardware changes
{: #worker-default-hw}

To change the compute hardware, such as the CPU and memory per worker node, choose among the following options.
* Create a worker pool. The instructions vary depending on the type of infrastructure for the cluster, such as classic, VPC, or {{site.data.keyword.satelliteshort}}. For more information, see [Adding worker nodes to Classic clusters](/docs/openshift?topic=openshift-add-workers-classic) or [Adding worker nodes to VPC clusters](/docs/openshift?topic=openshift-add-workers-vpc). 
* [Update the flavor](/docs/openshift?topic=openshift-update#machine_type) in your cluster by creating a worker pool and removing the previous worker pool.




## Modifying worker node kernel settings to optimize performance
{: #worker-kernel-ds}

Cluster worker nodes are configured for a level of stability, optimization, and performance that is expected to meet the needs of most workloads. Usually, it is not recommended to change your worker node kernel settings, as such changes can create unusual and unintended issues. However, if your workload has highly unique performance optimization requirements that necessitate changes to your kernel settings, a custom Kubernetes daemonset can be applied to change the kernel configuration. Understand that these changes can have significant negative consequences and that you implement changes to the kernel settings configuration **at your own risk**. 

If you change the configuration of your kernel settings, make sure you document and save the exact changes that you make. If you open a support ticket for any issues related to the cluster, you must specify these changes. These configuration changes might be responsible for the issue, and you might be asked to revert the changes as part of the issue investigation. In this case, you are responsible for reverting any kernel configuration changes you implement. 
{: important}

Changing the default kernel settings can have negative effects on your cluster. Make these changes at your own risk. 
{: important}

You can change the default kernel settings by applying a custom [Kubernetes `DaemonSet`](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/){: external} with an [`init` Container](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/){: external} to your cluster. The daemon set modifies the settings for all existing worker nodes and applies the settings to any new worker nodes that are provisioned in the cluster. The `init` container makes sure that these modifications occur before other pods are scheduled on the worker node. No pods are affected.

You must have the [**Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/openshift?topic=openshift-iam-platform-access-roles) for all namespaces to run the sample privileged `initContainer`. After the containers for the deployments are initialized, the privileges are dropped.
{: note}

Before you begin: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Save the following daemon set in a file named `worker-node-kernel-settings.yaml`. In the `spec.template.spec.initContainers` section, add the fields and values for the `sysctl` parameters that you want to tune. This example daemon set changes the default maximum number of connections that are allowed in the environment via the `net.core.somaxconn` setting and the ephemeral port range via the `net.ipv4.ip_local_port_range` setting.

    Depending on the `systctl` settings that you try to change, you might want to configure the security context. For more information, see the [{{site.data.keyword.redhat_openshift_notm}} documentation](https://docs.openshift.com/container-platform/4.16/nodes/containers/nodes-containers-sysctls.html){: external}.
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
                - sysctl -w net.ipv4.tcp_syn_retries="5"; sysctl -w net.ipv4.tcp_fin_timeout="15";
              image: us.icr.io/armada-master/network-alpine:latest
              imagePullPolicy: Always 
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
              image: us.icr.io/armada-master/network-alpine:latest
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



There currently isn't a way to set these `sysctl` keepalive settings on all pods by default in a cluster. The best way to modify the settings on all pods is to use a privileged `initContainer`. Review the following example of how to set up an `initContainer` for a deployment in a `test-ns` namespace.



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




All VPC worker nodes support jumbo frames, but classic infrastructure only supports jumbo frames on bare metal workers. 
{: note}


Changing maximum transmission unit (MTU) values can have unexpected results, especially in complex networking environments. To avoid disruption to your workflow, it is highly recommended that you test these changes on a development cluster before you make any changes to your production clusters. 
{: important}

By default, the Calico network plug-in in your {{site.data.keyword.openshiftlong_notm}} cluster has an MTU of 1450 bytes for Satellite clusters and 1480 bytes for non-Satellite clusters. For most cases, this default Calico MTU value is sufficient for preventing packet drops and fragmentation. Because most hosts use an MTU value of 1500, these default values provide Satellite clusters with 50 extra bytes for vxlan headers and provide non-Satellite clusters with 20 extra bytes for the IP headers used in some pod-to-pod cluster network traffic. Note that all worker nodes in the cluster must use the same Calico MTU value.

Review the following cases in which you might need to modify the default Calico MTU:

* If you need to improve your pod-to-pod network throughput and your cluster nodes are able to use a higher host MTU, then you can increase both the host and Calico MTU. This is called using "jumbo frames". The typical jumbo frame MTU is 9000. In this case, you can set the host private network interface to an MTU value of 9000 and the Calico MTU to a slightly lower value -- 8950 for Satellite clusters and 8980 for non-Satellite clusters. Note that some cloud provider hardware or resources, [such as Azure virtual machines](https://learn.microsoft.com/en-us/azure/virtual-network/how-to-virtual-machine-mtu?tabs=linux){: external}, might not support jumbo frames or might only support an MTU value of up to 4000. 
* If you have a VPN connection set up for your cluster, some VPN connections require a smaller Calico MTU than the default. Check with the VPN service provider to determine whether a smaller Calico MTU is required.


Before you begin
:   If your worker nodes still run the default MTU value, increase the MTU value for your worker nodes first before you increase the MTU value for the Calico plug-in. For example, you can apply the following daemon set to change the MTU for your worker nodes to 9000 bytes. Note the interface names that are used in the **`ip link`** command vary depending on the type of your worker nodes.
    - Example command for Bare Metal worker nodes: `ip link set dev bond0 mtu 9000;ip link set dev bond1 mtu 9000;`
    - Example command VPC Gen 2 worker nodes: `ip link set dev ens3 mtu 9000;`

1. Run the following commands to log into a cluster worker node and ping from one node to another. Because your node MTU is only set to 1500 or 1480, **this attempt is expected to fail**. In the following steps, you can run these commands again to verify that changes are successful.
    1. List the nodes in your cluster. Save the names and IP addresses of two healthy nodes. 
        ```sh
        oc get nodes -o wide
        ```
        {: pre}
    1. Log into one of the nodes. Specify the name of the node.

        
        ```sh
        oc debug node/<NODE_NAME>
        ```
        {: pre}
        
        


    1. Run the command to ping from one node to the other. Specify the IP address of the node that you did not reference in the previous step.
        ```sh
        ping -c1 -Mdo -s 8972 <OTHER_HOST_IP>
        ```
        {: pre}

2. Change the node MTU with the following example daemonset. This MTU value applies to node-to-node traffic. Modify the `- ip link set dev ens3 mtu <MTU_VALUE>` line to include your desired MTU value (the example uses a MTU value of 9000). Note that you might also need to change the `ens3` interface name if ens3 is not appropriate for your nodes.
    ```yaml
    apiVersion: apps/v1
    kind: DaemonSet
    metadata:
      labels:
        app: set-host-mtu
      name: set-host-mtu
      namespace: kube-system
    spec:
      selector:
        matchLabels:
          name: set-host-mtu
      template:
        metadata:
          labels:
            name: set-host-mtu
        spec:
          containers:
          - args:
            - |
              while true; do
                sleep 100000;
              done
            command:
            - /bin/sh
            - -c
            image: us.icr.io/armada-master/network-alpine:latest
            imagePullPolicy: IfNotPresent
            name: sleepforever
            resources:
              requests:
                cpu: 10m
          hostNetwork: true
          initContainers:
          - command:
            - sh
            - -c
            - ip link set dev ens3 mtu 9000
            image: us.icr.io/armada-master/network-alpine:latest
            imagePullPolicy: IfNotPresent
            name: set-host-mtu
            securityContext:
              capabilities:
                add:
                - NET_ADMIN
              privileged: true
            volumeMounts:
            - mountPath: /sys
              name: modifysys
          restartPolicy: Always
          terminationGracePeriodSeconds: 2
          tolerations:
          - operator: Exists
          volumes:
          - hostPath:
              path: /sys
              type: ""
            name: modifysys
      updateStrategy:
        rollingUpdate:
          maxSurge: 0
          maxUnavailable: 1
        type: RollingUpdate
    ```
    {: codeblock}

3. Apply the daemonset to change the node MTU value. 
    ```sh
      oc apply -f <file_name>
    ```
    {: pre}

4. Re-run the commands to log in to a node and ping from one host to another, using a large packet size. Now that you have increased the node MTU value, the `ping` command is expected to succeed. 
    
    ```sh
    oc debug node/<NODE_NAME>
    ```
    {: pre}
    
    

    ```sh
    ping -c1 -Mdo -s 8972 <OTHER_HOST_IP>
    ```
    {: pre}

5. Take time to test your cluster with the new node MTU value. Before you continue with changing the Calico MTU value, it is recommended that you check to make sure your applications still function as expected. 

6. Run the command to update the Calico MTU values so that pod-to-pod traffic can also use the larger MTU. For Satellite Core OS clusters, the Calico MTU value should be 50 bytes less than the node MTU value. For all other clusters, the Calico MTU value should be 20 bytes less. For example, if you specified 9000 for the node MTU, your Calico MTU should be 8950 for Satellite Core OS clusters or 8980 for all other clusters. 

      ```sh
      oc patch installation.operator.tigera.io default --type='merge' -p '{"spec":{"calicoNetwork":{"mtu":<MTU_VALUE>}}}'
      ```
      {: pre}

      You can also edit the resource directly by running `oc edit installation.operator.tigera.io default`.
      {: tip}

7. Apply these changes to all of your nodes by carefully rebooting all nodes. Make sure you have tested this process on a development cluster before you continue with this step, as these changes could cause disruptions to your workload. To reboot your nodes, it is recommended that you [cordon, drain, and reboot](/docs/containers?topic=containers-host-maintenance#worker-maintenance-classic) your nodes one by one. 

If you are completing these steps on a production cluster, you should use the same process you use for updating or replacing production nodes. It is highly recommended that you test this entire process on a test cluster before you complete these steps on a production cluster. 
{: important}

During the reboot process, some pods use the new larger MTU and some pods still have the original, smaller MTU. Typically, this scenario does not cause issues because both sides negotiate the correct max packet size. However, if you block ICMP packets, the negotiation might not work and your cluster might experience pod connection issues untill all reboots have completed. It is critical that this process is first tested on a development cluster. 
{: important}

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
