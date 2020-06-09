---

copyright:
  years: 2014, 2020
lastupdated: "2020-06-09"

keywords: openshift, rhoks, roks, rhos, kernel

subcollection: openshift

---

{:beta: .beta}
{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}



# Tuning performance
{: #kernel}

If you have specific performance optimization requirements, you can change the default settings for some cluster components in {{site.data.keyword.openshiftlong}}.
{: shortdesc}

If you choose to change the default settings, you are doing so at your own risk. You are responsible for running tests against any changed settings and for any potential disruptions caused by the changed settings in your environment.
{: important}

## Changing the Calico maximum transmission unit (MTU)
{: #calico-mtu}

Increase or decrease the Calico plug-in maximum transmission unit (MTU) to meet the network throughput requirements of your environment.
{: shortdesc}

By default, the Calico network plug-in in your Red Hat OpenShift on IBM Cloud cluster has an MTU of 1480 bytes. For most cases, this default MTU value provides sufficient throughput for packets that are sent and received in your network workloads. Review the following cases in which you might need to modify the default Calico MTU:

* If your cluster uses bare metal worker nodes, and you use jumbo frames on the bare metal worker nodes, the jumbo frames have an MTU value in the range of 1500 to 9000. To ensure that Calico can handle this throughput, you can increase the Calico MTU to match the MTU of the jumbo frames. Note that all worker nodes in the cluster must use the same Calico MTU, so to increase the Calico MTU, all worker nodes in the cluster must be bare metal and use jumbo frames.
* If you have a VPN connection set up for your cluster, some VPN connections require a smaller Calico MTU than the default. Check with the VPN service to determine whether a smaller Calico MTU is required.

You can change the MTU on the tunnel interface `tunl0`, which is used for pod to pod communication, and the MTU on the `caliXXXXXXXX` `veth` interface of each worker node.



### Changing the Calico MTU for 4.3 or later clusters
{: #calico-mtu-43}

Increase the Calico plug-in MTU to meet the network throughput requirements of your environment in an OpenShift version 4.3 or later cluster.
{: shortdesc}

1. Edit the `default` Calico installation resource.
  ```
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
       mtu: 1500
       nodeAddressAutodetectionV4:
         interface: (^bond0$|^eth0$|^ens6$|^ens3$)
     kubernetesProvider: OpenShift
     registry: registry.ng.bluemix.net/armada-master/
     variant: Calico
   status:
     variant: Calico
   ```
   {: screen}

3. Save and close the file.

4. Apply the MTU changes to your worker nodes by [rebooting all worker nodes in your cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot).

### Changing the Calico MTU for 3.11 clusters
{: #calico-mtu-311}

Increase the Calico plug-in MTU to meet the network throughput requirements of your environment in an OpenShift version 3.11 cluster.
{: shortdesc}


1. Edit the `calico-config` configmap resource.
  ```
  oc edit cm calico-config -n kube-system
  ```
  {: pre}

2. In the `data` section, add a `calico_mtu_override: "<new_MTU>"` field and specify the new MTU value for Calico. Note that the quotation marks (`"`) around the new MTU value are required.

    Do not change the values of `mtu` or `veth_mtu`.
    {: important}

    ```yaml
    apiVersion: v1
    data:
      calico_backend: bird
      calico_mtu_override: "1600"
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

3. Apply the MTU changes to your cluster master by refreshing the master API server. It might take several minutes for the master to refresh.
  ```
  ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
  ```
  {: pre}

4. Verify that the master refresh is completed. When the refresh is complete, the **Master Status** changes to `Ready`.
  ```
  ibmcloud oc cluster get --cluster <cluster_name_or_ID>
  ```
  {: pre}

5. In the `data` section of the output, verify that the `veth_mtu` field shows the new MTU value for Calico that you specified in step 2.
  ```
  oc get cm -n kube-system calico-config -o yaml
  ```
  {: pre}

  Example output:
  ```yaml
  apiVersion: v1
  data:
    ...
    etcd_ca: /calico-secrets/etcd-ca
    etcd_cert: /calico-secrets/etcd-cert
    etcd_endpoints: https://172.20.0.1:2041
    etcd_key: /calico-secrets/etcd-key
    typha_service_name: none
    veth_mtu: "1600"
  kind: ConfigMap
  ...
  ```
  {: screen}

6. Apply the MTU changes to your worker nodes by [rebooting all worker nodes in your cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot).

<br />


## Disabling the portmap plug-in
{: #calico-portmap}

The `portmap` plug-in for the Calico container network interface (CNI) enables you to use a `hostPort` to expose your app pods on a specific port on the worker node. Prevent iptables performance issues by removing the portmap plug-in from your cluster's Calico CNI configuration.
{: shortdesc}

When you have a large number of services in your cluster, such as more than 500 services, or a large number of ports on services, such as more than 50 ports per service for 10 or more services, a large number of iptables rules are generated for the Calico and Kubernetes network policies for these services. A large number of iptables rules can lead to performance issues for the portmap plug-in, and might prevent future updates of iptables rules or cause the `calico-node` container to restart when no lock is received to make iptables rules updates within a specified time. To prevent these performance issues, you can disable the portmap plug-in by removing it from your cluster's Calico CNI configuration.

If you must use `hostPorts`, do not disable the portmap plug-in.
{: note}

### Disabling the portmap plug-in for 4.3 or later clusters
{: #calico-portmap-43}

Disable the portmap plug-in by disabling `hostPorts` for Calico in an OpenShift version 4.3 or later cluster.
{: shortdesc}

1. Edit the `default` Calico installation resource.
  ```
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

### Disabling the portmap plug-in for 3.11 clusters
{: #calico-portmap-311}

Disable the portmap plug-in by disabling `hostPorts` for Calico in an OpenShift version 3.11 cluster.
{: shortdesc}


1. Edit the `calico-config` configmap resource.
  ```
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

3. Apply the change to your cluster by restarting all `calico-node` pods.
    1. Get the names of the `calico-node` pods in your cluster.
      ```
      oc get pods -n kube-system | grep calico-node
      ```
      {: pre}
    2. Restart all `calico-node` pods by manually deleting them. Separate each pod name with one space.
      ```
      oc delete pods -n kube-system <pod1> <pod2> ...
      ```
      {: pre}

