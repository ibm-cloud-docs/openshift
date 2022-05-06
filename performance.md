---

copyright: 
  years: 2014, 2022
lastupdated: "2022-05-06"

keywords: openshift, kernel

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Tuning performance
{: #kernel}

If you have specific performance optimization requirements, you can change the default settings for some cluster components in {{site.data.keyword.openshiftlong}}.
{: shortdesc}

If you choose to change the default settings, you are doing so at your own risk. You are responsible for running tests against any changed settings and for any potential disruptions caused by the changed settings in your environment.
{: important}

## Default worker node settings
{: #worker-default}

By default, your worker nodes have the operating system and compute hardware of the [worker node flavor](/docs/containers?topic=containers-planning_worker_nodes) that you choose when you create the worker pool.
{: shortdesc}

### Customizing the operating system
{: #worker-default-os}

The following operating systems are available for worker nodes: **RHEL 7**. Your cluster can't mix operating systems or use different operating systems.
{: shortdesc}

To optimize your worker nodes, consider the following information.
* **Image and version updates**: Worker node updates, such as security patches to the image or {{site.data.keyword.redhat_openshift_notm}} versions, are provided by IBM for you. However, you choose when to apply the updates to the worker nodes. For more information, see [Updating clusters, worker nodes, and cluster components](/docs/containers?topic=containers-update).
* **Temporary modifications**: If you log in to a pod or use some other process to modify a worker node setting, the modifications are temporary. Worker node lifecycle operations, such as autorecovery, reloading, updating, or replacing a worker node, change any modifications back to the default settings.
* **Persistent modifications**: For modifications to persist across worker node lifecycle operations, create a daemon set that uses an init container. For more information, see [Modifying default worker node settings to optimize performance](#worker).

    Modifications to the operating system are not supported. If you modify the default settings, you are responsible for debugging and resolving the issues that might occur.
    {: important}

### Hardware changes
{: #worker-default-hw}

To change the compute hardware, such as the CPU and memory per worker node, choose among the following options.
* [Create a worker pool](/docs/containers?topic=containers-add_workers). The instructions vary depending on the type of infrastructure for the cluster, such as classic, VPC, {{site.data.keyword.satelliteshort}}, or gateway clusters.
* [Update the flavor](/docs/containers?topic=containers-update#machine_type) in your cluster by creating a worker pool and removing the previous worker pool.

## Modifying default worker node settings to optimize performance
{: #worker}

If you have specific performance optimization requirements, you can change the default settings for the Linux kernel `sysctl` parameters on worker nodes.
{: shortdesc}

Worker nodes are automatically provisioned with optimized kernel performance, but you can change the default settings by applying a custom [Kubernetes `DaemonSet`](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/){: external} with an [`initContainer`](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/){: external} to your cluster. The daemon set modifies the settings for all existing worker nodes and applies the settings to any new worker nodes that are provisioned in the cluster. The init container makes sure that these modifications occur before other pods are scheduled on the worker node. No pods are affected.

You must have the [**Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/openshift?topic=openshift-users#checking-perms) for all namespaces to run the sample privileged `initContainer`. After the containers for the deployments are initialized, the privileges are dropped.
{: note}

Before you begin: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Save the following daemon set in a file named `worker-node-kernel-settings.yaml`. In the `spec.template.spec.initContainers` section, add the fields and values for the `sysctl` parameters that you want to tune. This example daemon set changes the default maximum number of connections that are allowed in the environment via the `net.core.somaxconn` setting and the ephemeral port range via the `net.ipv4.ip_local_port_range` setting.

    Depending on the `systctl` settings that you try to change, you might want to configure the security context. For more information, see the [{{site.data.keyword.redhat_openshift_notm}} documentation](https://docs.openshift.com/container-platform/4.9/nodes/containers/nodes-containers-sysctls.html){: external}.
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

2. Apply the daemon set to your worker nodes. The changes are applied immediately.
    ```sh
    oc apply -f worker-node-kernel-settings.yaml
    ```
    {: pre}



To revert your worker nodes' `sysctl` parameters to the default values set by {{site.data.keyword.containerlong_notm}}:

1. Delete the daemon set. The `initContainers` that applied the custom settings are removed.
    ```sh
    oc delete ds kernel-optimization
    ```
    {: pre}

2. [Reboot all worker nodes in the cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot). The worker nodes come back online with the default values applied.





## Changing the Calico maximum transmission unit (MTU)
{: #calico-mtu}

Increase or decrease the Calico plug-in maximum transmission unit (MTU) to meet the network throughput requirements of your environment.
{: shortdesc}

By default, the Calico network plug-in in your {{site.data.keyword.openshiftlong_notm}} cluster has an MTU of 1480 bytes. For most cases, this default MTU value provides sufficient throughput for packets that are sent and received in your network workloads. Review the following cases in which you might need to modify the default Calico MTU:

* If your cluster uses bare metal worker nodes, and you use jumbo frames on the bare metal worker nodes, the jumbo frames have an MTU value in the range of 1500 to 9000. To ensure that your cluster's pod network can use this higher MTU value, you can increase the Calico MTU to 20 bytes lower than the jumbo frame MTU. This 20 byte difference allows space for packet header on encapsulated packets. For example, if your worker nodes' jumbo frames are set to 9000, you can set the Calico MTU to 8980. Note that all worker nodes in the cluster must use the same Calico MTU, so to increase the Calico MTU, all worker nodes in the cluster must be bare metal and use jumbo frames.
* If you have a VPN connection set up for your cluster, some VPN connections require a smaller Calico MTU than the default. Check with the VPN service provider to determine whether a smaller Calico MTU is required.
* If your cluster's worker nodes exist on different subnets, increasing the MTU value for the worker nodes and for the Calico MTU can allow pods to use the full bandwidth capability of the worker nodes.

**Before you begin**: If your bare metal worker nodes still run the default MTU value, increase the MTU value for your worker nodes first before you increase the MTU value for the Calico plug-in. For example, you can apply the following daemon set to change the MTU for your worker nodes's jumbo frames to 9000 bytes.

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
            - ip link set dev bond0 mtu 9000;ip link set dev bond1 mtu 9000;
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



To run your {{site.data.keyword.redhat_openshift_notm}} cluster, make sure that the MTU is equal to or greater than 1450 bytes.
{: important}

### Changing the Calico MTU for version 4 clusters
{: #calico-mtu-43}

Increase the Calico plug-in MTU to meet the network throughput requirements of your environment in an {{site.data.keyword.redhat_openshift_notm}} version 4 cluster.
{: shortdesc}

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

### Changing the Calico MTU for 3.11 clusters
{: #calico-mtu-311}

Increase the Calico plug-in MTU to meet the network throughput requirements of your environment in an {{site.data.keyword.redhat_openshift_notm}} version 3.11 cluster.
{: shortdesc}



1. Edit the `calico-config` configmap resource.
    ```sh
    oc edit cm calico-config -n kube-system
    ```
    {: pre}

2. In the `data` section, add a `calico_mtu_override: "<new_MTU>"` field and specify the new MTU value for Calico. Note that the quotation marks (`"`) around the new MTU value are required.

    Do not change the values of `mtu` or `veth_mtu`. Changing any other settings besides the `calico_mtu_override` field for the Calico plug-in in this configmap is not supported.
    {: important}

    ```yaml
    apiVersion: v1
    data:
      calico_backend: bird
      calico_mtu_override: "8980"
      cni_network_config: |-
        {
          "name": "k8s-pod-network",
          "cniVersion": "0.3.1",
          "plugins": [
            {
              "type": "calico",
              "log_level": "info",
              "etcd_endpoints": "__ETCD_ENDPOINTS__",
              "etcd_key_file": "__ETCD_KEY_FILE__",
              "etcd_cert_file": "__ETCD_CERT_FILE__",
              "etcd_ca_cert_file": "__ETCD_CA_CERT_FILE__",
              "mtu": __CNI_MTU__,
              "ipam": {
                  "type": "calico-ipam"
              },
              "container_settings": {
                  "allow_ip_forwarding": true
              },
              "policy": {
                  "type": "k8s"
              },
              "kubernetes": {
                  "kubeconfig": "__KUBECONFIG_FILEPATH__"
              }
            },
            {
              "type": "portmap",
              "snat": true,
              "capabilities": {"portMappings": true}
            }
          ]
        }
      etcd_ca: /calico-secrets/etcd-ca
      etcd_cert: /calico-secrets/etcd-cert
      etcd_endpoints: https://172.20.0.1:2041
      etcd_key: /calico-secrets/etcd-key
      typha_service_name: none
      veth_mtu: "1480"
    kind: ConfigMap
    ...
    ```
    {: codeblock}

    To run your {{site.data.keyword.redhat_openshift_notm}} cluster, make sure that the MTU is equal to or greater than 1450 bytes.
    {: important} 

3. Apply the MTU changes to your cluster master by refreshing the master API server. It might take several minutes for the master to refresh.
    ```sh
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

4. Verify that the master refresh is completed. When the refresh is complete, the **Master Status** changes to `Ready`.
    ```sh
    ibmcloud oc cluster get --cluster <cluster_name_or_ID>
    ```
    {: pre}

5. In the `data` section of the output, verify that the `veth_mtu` field shows the new MTU value for Calico that you specified in step 2.
    ```sh
    oc get cm -n kube-system calico-config -o yaml
    ```
    {: pre}

    Example output

    ```yaml
    apiVersion: v1
    data:
      ...
      etcd_ca: /calico-secrets/etcd-ca
      etcd_cert: /calico-secrets/etcd-cert
      etcd_endpoints: https://172.20.0.1:2041
      etcd_key: /calico-secrets/etcd-key
      typha_service_name: none
      veth_mtu: "8980"
      kind: ConfigMap
      ...
    ```
    {: screen}

6. Apply the MTU changes to your worker nodes by [rebooting all worker nodes in your cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot).



## Disabling the port map plug-in
{: #calico-portmap}

The `portmap` plug-in for the Calico container network interface (CNI) enables you to use a `hostPort` to expose your app pods on a specific port on the worker node. Prevent iptables performance issues by removing the port map plug-in from your cluster's Calico CNI configuration.
{: shortdesc}

When you have many services in your cluster, such as more than 500 services, or many ports on services, such as more than 50 ports per service for 10 or more services, many iptables rules are generated for the Calico and Kubernetes network policies for these services. A large number of iptables rules can lead to performance issues for the port map plug-in, and might prevent future updates of iptables rules or cause the `calico-node` container to restart when no lock is received to make iptables rules updates within a specified time. To prevent these performance issues, you can disable the port map plug-in by removing it from your cluster's Calico CNI configuration.

If you must use `hostPorts`, don't disable the port map plug-in.
{: note}



### Disabling the port map plug-in for version 4 clusters
{: #calico-portmap-43}

Disable the port map plug-in by disabling `hostPorts` for Calico in an {{site.data.keyword.redhat_openshift_notm}} version 4 cluster.
{: shortdesc}

1. Edit the `default` Calico installation resource.
    ```sh
    oc edit installation default -n calico-system
    ```
    {: pre}

2. In the `spec.calicoNetwork` section, change the value of `hostPorts` to `Disabled`.
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

3. Save and close the file. Your changes are automatically applied.

### Disabling the port map plug-in for 3.11 clusters
{: #calico-portmap-311}

Disable the port map plug-in by disabling `hostPorts` for Calico in an {{site.data.keyword.redhat_openshift_notm}} version 3.11 cluster.
{: shortdesc}



1. Edit the `calico-config` configmap resource.
    ```sh
    oc edit cm calico-config -n kube-system
    ```
    {: pre}

2. In the `data.cni_network_config.plugins` section after the `kubernetes` plug-in, remove the `portmap` plug-in section. After you remove the `portmap` section, the configuration looks like the following:
    ```yaml
    apiVersion: v1
    data:
      calico_backend: bird
      cni_network_config: |-
        {
          "name": "k8s-pod-network",
          "cniVersion": "0.3.1",
          "plugins": [
            {
              "type": "calico",
              "log_level": "info",
              "etcd_endpoints": "__ETCD_ENDPOINTS__",
              "etcd_key_file": "__ETCD_KEY_FILE__",
              "etcd_cert_file": "__ETCD_CERT_FILE__",
              "etcd_ca_cert_file": "__ETCD_CA_CERT_FILE__",
              "mtu": __CNI_MTU__,
              "ipam": {
                  "type": "calico-ipam"
              },
              "container_settings": {
                  "allow_ip_forwarding": true
              },
              "policy": {
                  "type": "k8s"
              },
              "kubernetes": {
                  "kubeconfig": "__KUBECONFIG_FILEPATH__"
              }
            }
          ]
        }
      etcd_ca: /calico-secrets/etcd-ca
      ...
    ```
    {: codeblock}

    Changing any other settings for the Calico plug-in in this configmap is not supported.
    {: important}

3. Apply the change to your cluster by restarting all `calico-node` pods.

    1. Get the names of the `calico-node` pods in your cluster.
        ```sh
        oc get pods -n kube-system | grep calico-node
        ```
        {: pre}

    2. Restart all `calico-node` pods by manually deleting them. Separate each pod name with one space.
        ```sh
        oc delete pods -n kube-system <pod1> <pod2> ...
        ```
        {: pre}
