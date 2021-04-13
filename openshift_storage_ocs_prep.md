---

copyright:
  years: 2014, 2021
lastupdated: "2021-04-13"

keywords: openshift, openshift container storage, ocs, roks

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}
 


# Preparing your cluster for OpenShift Container Storage
{: #ocs-storage-prep}
OpenShift Container Storage is a highly available storage solution that you can use to manage persistent storage for your containerized databases and other stateful apps in {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

**Supported infrastructure provider**:
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

**Minimum required permissions**: **Administrator** platform access role and the **Manager** service access role for the cluster in {{site.data.keyword.containerlong_notm}}.

The OpenShift Container Storage add-on is available as a Technical Preview feature and might change without prior notice. Do not use this feature for production workloads. 
{: preview}

<br />

## VPC: Planning your OpenShift Container Storage set up
{: #ocs-vpc-plan}
Before you install OCS in your VPC Gen 2 cluster, you must make sure that the following prerequisite conditions are met:

1. [Install the `oc` CLI](/docs/openshift?topic=openshift-openshift-cli#cli_oc).
1. Create a [VPC Gen 2 cluster](/docs/containers?topic=containers-clusters) with at least 3 worker nodes. For high availability, create a cluster with at least 1 worker node per zone across 3 zones. Each worker node must have a minimum of 16 CPUs and 64GB RAM.

**Next steps**: [Install OCS in your cluster](/docs/openshift?topic=openshift-ocs-storage-install).

<br />

## Classic: Planning your OpenShift Container Storage set up
{: #ocs-classic-plan}
Before you install OCS in your cluster, you must make sure that the following prerequisite conditions are met:

1. [Install the `oc` CLI](/docs/openshift?topic=openshift-openshift-cli#cli_oc).
1. [Review the SDS worker node flavors](/docs/openshift?topic=openshift-planning_worker_nodes#sds-table).
1. Create a [classic cluster](/docs/containers?topic=containers-clusters) with a minimum of 1 worker node per zone across 3 zones. Create a cluster with worker nodes of flavor type `mb4c.32x384.3.8tb.ssd` or `mb4c.20x64.2x1.9tb.ssd` which have the required local disks for OCS.
1. [Prepare your classic cluster](#ocs-cluster-prepare-classic).

### Classic: Preparing your cluster for an OpenShift Container Storage installation.
{: #ocs-cluster-prepare-classic}
Before you install OpenShift Container Storage in a classic cluster, review the following steps to prepare your cluster for an OCS installation.
{: shortdesc}

[Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Log in to each worker node in your cluster by using the `oc debug` command and complete the following steps.
    * Log in to the worker node. Replace `<worker_node_IP>` with the private IP address of your worker node. To get the private IP addresses of your worker nodes, run the `oc get nodes` command.
      ```sh
      oc debug node/<node name> -- chroot /host rm -rvf /var/lib/rook /mnt/local-storage
      ```
      {: pre}

    * For each disk partition, clear the `xfs` file system that was created with the worker node. If you do not clear the file system, the OSD is not created.
      ```sh
      file -sL /dev/<partition>
      wipefs -a /dev/<partition>
      ```
      {: pre}

    * Log out of the worker node
      ```sh
      exit
      ```
    
1. Repeat step 3 for each worker node that you want use in your OCS deployment.

1. Update the `clusterRole` and `ClusterRoleBindings` for each worker node in your cluster. Edit the `system:node` cluster role to have `get, create, update, delete, list` access for the `volumeattachments.storage.k8s.io` resource.
  ```sh
  oc edit clusterrole system:node
  ```
  {: pre}

  **Example updated `system:node` cluster role configuration file**
  ```yaml
  apiVersion: rbac.authorization.k8s.io/v1
  kind: ClusterRole
  metadata:
    annotations:
      rbac.authorization.kubernetes.io/autoupdate: "true"
    creationTimestamp: "2020-07-20T18:52:59Z"
    labels:
      kubernetes.io/bootstrapping: rbac-defaults
    name: system:node
    resourceVersion: "60"
    selfLink: /apis/rbac.authorization.k8s.io/v1/clusterroles/system%3Anode
    uid: 1111111a-aa11-1111-1aa1-11a111111a1a
  rules:
  - apiGroups:
    - storage.k8s.io
    resources:
    - volumeattachments
    verbs:
    - get
    - create
    - update
    - delete
    - list
  ```
  {: codeblock}

1. Save and close the file to apply your changes.

1. Edit the cluster role binding `system:node` to add `subjects`.
  ```sh
  oc edit clusterrolebinding system:node
  ```
  {: pre}

  **Example updated `system:node` ClusterRoleBinding configuration file with `subjects`**
  ```yaml
  apiVersion: rbac.authorization.k8s.io/v1
  kind: ClusterRoleBinding
  metadata:
    annotations:
      rbac.authorization.kubernetes.io/autoupdate: "true"
    creationTimestamp: "2020-07-20T18:53:00Z"
    labels:
      kubernetes.io/bootstrapping: rbac-defaults
    name: system:node
    resourceVersion: "5202"
    selfLink: /apis/rbac.authorization.k8s.io/v1/clusterrolebindings/system%3Anode
    uid: aaaa1a11-1111-1111-1111-a1a11a111a11
  roleRef:
    apiGroup: rbac.authorization.k8s.io
    kind: ClusterRole
    name: system:node
  subjects:
  - apiGroup: rbac.authorization.k8s.io
    kind: Group
    name: system:nodes
  ```
  {: codeblock}

1. Save and close the file to apply your changes.

1. [Get your local device details](#ocs-classic-get-devices).

<br />

### Classic: Getting your device details
{: #ocs-classic-get-devices}

Before you install OCS, get the details of the local disks on your worker nodes.
{: shortdesc}

1. Log in to your cluster and get a list of available worker nodes. Make a note of the worker nodes that you want to use in your OCS deployment.
    ```sh
    oc get nodes
    ```
    {: pre}

2. Log in to each worker node that you want to use for your OCS. 
    ```sh
    oc debug node/<node-name>
    ```
    {: pre}
    
3. When the debug pod is deployed on the worker node, run the following command to allow host binaries.
    ```sh
    chroot /host
    ```
    {: pre}

4. List the available disks on the worker node.
    ```sh
    lsblk
    ```
    {: pre}

5. Review the command output for available disks. You can use only unmounted disks for OCS deployments, such as `sdc` disks in the following example. Note that the initial storage capacity of your OCS deployment is equal to the size of the disk that you specify as the `osd-device-path`. In this example, the `sdc` disk is unmounted and has two availabe partitions: `sdc1` and `sdc2`.
    ```sh
    NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
    sda      8:0    0   931G  0 disk
    |-sda1   8:1    0   256M  0 part /boot
    |-sda2   8:2    0     1G  0 part
    `-sda3   8:3    0 929.8G  0 part /
    sdb      8:16   0 744.7G  0 disk
    `-sdb1   8:17   0 744.7G  0 part /disk1
    sdc      8:32   0 744.7G  0 disk
    |-sdc1   8:33   0  18.6G  0 part
    `-sdc2   8:34   0 260.8G  0 part
    ```
    {: pre}

6. For each unmounted disk that you want to use in your deployment, find the disk ID. In the following example, the ID for the `sdc1` partition is `scsi-3600605b00d87b43027b3bc310a64c6c9-part1` and the ID for the `sdc2` partition is `scsi-3600605b00d87b43027b3bc310a64c6c9-part2`.

    ```sh
    ls -l /dev/disk/by-id/
    ```
    {: pre}

    **Example output:**
    ```sh
    total 0
    lrwxrwxrwx. 1 root root  9 Feb  9 04:15 scsi-3600605b00d87b43027b3bbb603150cc6 -> ../../sda
    lrwxrwxrwx. 1 root root 10 Feb  9 04:15 scsi-3600605b00d87b43027b3bbb603150cc6-part1 -> ../../sda1
    lrwxrwxrwx. 1 root root 10 Feb  9 04:15 scsi-3600605b00d87b43027b3bbb603150cc6-part2 -> ../../sda2
    lrwxrwxrwx. 1 root root 10 Feb  9 04:15 scsi-3600605b00d87b43027b3bbb603150cc6-part3 -> ../../sda3
    lrwxrwxrwx. 1 root root  9 Feb  9 04:15 scsi-3600605b00d87b43027b3bbf306bc28a7 -> ../../sdb
    lrwxrwxrwx. 1 root root 10 Feb  9 04:15 scsi-3600605b00d87b43027b3bbf306bc28a7-part1 -> ../../sdb1
    lrwxrwxrwx. 1 root root  9 Feb  9 04:17 scsi-3600605b00d87b43027b3bc310a64c6c9 -> ../../sdc
    lrwxrwxrwx. 1 root root 10 Feb 11 03:14 scsi-3600605b00d87b43027b3bc310a64c6c9-part1 -> ../../sdc1
    lrwxrwxrwx. 1 root root 10 Feb 11 03:15 scsi-3600605b00d87b43027b3bc310a64c6c9-part2 -> ../../sdc2
    ```
    {: pre}

7. Repeat the previous steps for each worker node that you want to use for your OpenShift Container Storage deployment.

8. Finishing installing OCS for your cluster type:
  * **Multizone clusters**: [Create a `waitForFirstConsumer` storage class](#classic-ocs-sc-wffc).
  * **Single zone clusters**: [Install OCS in your cluster](/docs/openshift?topic=openshift-ocs-storage-install).

<br />

### Classic: Creating a `waitForFirstConsumer` storage class
{: #classic-ocs-sc-wffc}
If you have a multizone cluster on classic infrastructure, you must create a custom storage class and set the `volumeBindingMode` to `waitForFirstConsumer`. You can use a tiered storage class as a template to create a storage class. For more information about {{site.data.keyword.blockstorageshort}} classes, see the [storage class reference](/docs/containers?topic=containers-block_storage#block_storageclass_reference).
{: shortdesc}

The following steps apply to multizone clusters only.
{: note}

1. Save the following `StorageClass` YAML to a file on your local machine.

  ```yaml
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: <name> # Enter a name for your storage class. Example: ocs-storage-class
    labels:
      app: ibmcloud-block-storage-plugin
  provisioner: ibm.io/ibmc-block
  parameters:
    type: "Endurance"
    iopsPerGB: "10"
    sizeRange: '[20-4000]Gi'
    fsType: "ext4"
    billingType: "hourly"
    classVersion: "2"
  reclaimPolicy: "Delete"
  allowVolumeExpansion: true
  volumeBindingMode: WaitForFirstConsumer # Important: For multizone clusters, set the volumeBidingMode to WaitForFirstConsumer.
  ```
  {: codeblock}

2. Save the file and create the storage class in your cluster.
  ```sh
  oc create -f <storageclass-filename>
  ```
  {: pre}

3. Verify that your storage class is deployed.
  ```
  oc get sc
  ```
  {: pre}

**Next steps**: [Install OCS in your cluster](/docs/openshift?topic=openshift-ocs-storage-install).



