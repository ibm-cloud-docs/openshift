---

copyright:
  years: 2022, 2022
lastupdated: "2022-09-26"

keywords: satellite, hybrid, multicloud, sriov, nic, network

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Setting up Single Root I/O Virtualization (SR-IOV) in {{site.data.keyword.satellitelong_notm}} clusters
{: #satellite-sriov}

Single Root I/O Virtualization (SR-IOV) allows you to share a single, supported network device with multiple pods in your {{site.data.keyword.satelliteshort}} cluster. You can enable SR-IOV in your cluster by installing and configuring the SR-IOV network operator. For more information about SR-IOV, see [About Single Root I/O Virtualization (SR-IOV) hardware networks](https://docs.openshift.com/container-platform/4.6/networking/hardware_networks/about-sriov.html){: external}.
{: shortdesc}

Supported infrastructure providers
:   {{site.data.keyword.satelliteshort}}

Supported network interface controllers
:   The SR-IOV Network Operator can be used with supported network interface controllers (NICs) only. For more information, see [Supported NICs](https://docs.openshift.com/container-platform/4.6/networking/hardware_networks/installing-sriov-operator.html).

## Prerequisites for using SR-IOV
{: #sriov-prereqs}

1. [Create a {{site.data.keyword.satelliteshort}} location](/docs/satellite?topic=satellite-locations).
1. [Set up your location control plane](/docs/satellite?topic=satellite-locations#setup-control-plane).
1. [Attach more hosts to your location](/docs/satellite?topic=satellite-attach-hosts) to use as worker nodes in your cluster. The hosts that you want to use as worker nodes must have a [Supported NIC](https://docs.openshift.com/container-platform/4.6/networking/hardware_networks/installing-sriov-operator.html){: exteral}.

## Installing the SR-IOV network operator
{: #sriov-install-operator}

[Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Follow the steps to [Install the operator in your cluster](https://docs.openshift.com/container-platform/4.9/networking/hardware_networks/installing-sriov-operator.html#installing-sr-iov-operator_installing-sriov-operator){: external}. Make sure to set the **Update Approval** policy to **Manual**. 

1. After the operator is installed and running, run the following command to edit the `sriov-network-operator` deployment in the `openshift-sriov-network-operator` namespace.

   ```sh
   oc edit deployments.apps -n openshift-sriov-network-operator sriov-network-operator
   ```
   {: pre}
   
1. In the container specification section, add an environment variable with the name `CLUSTER_TYPE` and value `kubernetes`. 

   ```yaml
    - name: RESOURCE_PREFIX
      value: openshift.io
    - name: ENABLE_ADMISSION_CONTROLLER
      value: "true"
    - name: CLUSTER_TYPE
      value: kubernetes
   ```
   {: codeblock}
   
1. Save and close the deployment.

1. Run the following command to edit the `sriov-network-config-daemon` DaemonSet in the `openshift-sriov-network-operator` namespace.

   ```sh
   oc edit daemonsets.apps -n openshift-sriov-network-operator sriov-network-config-daemon
   ```
   {: pre}

1. Change the value of `CLUSTER_TYPE` from `openshift` to `kubernetes`.

   ```yaml
     - name: NAMESPACE
       valueFrom:
         fieldRef:
           apiVersion: v1
           fieldPath: metadata.namespace
     - name: CLUSTER_TYPE
       value: kubernetes
   ```
   {: codeblock}
   
1. Save and close the DaemonSet.

1. You can now begin [configuring your SRIOV-enabled network device](https://docs.openshift.com/container-platform/4.6/networking/hardware_networks/configuring-sriov-device.html){: external}.


