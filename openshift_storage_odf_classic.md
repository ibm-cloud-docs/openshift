---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-25"

keywords: openshift, openshift data foundation, openshift container storage, ocs, classic, roks

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
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
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
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
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
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
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
 

# Deploying OpenShift Data Foundation on Classic clusters
{: #deploy-odf-classic}

OpenShift Data Foundation is a highly available storage solution that you can use to manage persistent storage for your containerized workloads in {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

The OpenShift Data Foundation add-on is available as a technology preview and might change without prior notice. Don't use this add-on for production workloads.
{: preview}

## Planning your setup
{: #odf-classic-plan}
Before you install ODF in your cluster, you must make sure that the following prerequisite conditions are met:

1. [Install the `oc` CLI](/docs/openshift?topic=openshift-openshift-cli#cli_oc).
1. [Review the SDS worker node flavors](/docs/openshift?topic=openshift-planning_worker_nodes#sds-table).
1. Create a [classic cluster](/docs/openshift?topic=openshift-clusters) with a minimum of one worker node per zone across three zones. Choose worker nodes of flavor type `mb4c.32x384.3.8tb.ssd` or `mb4c.20x64.2x1.9tb.ssd` that have the required local disks for ODF.
1. [Prepare your classic cluster](#odf-cluster-prepare-classic).

### Optional: Setting up an {{site.data.keyword.cos_full_notm}} service instance
{: #odf-create-cos}

If you want to set up {{site.data.keyword.cos_full_notm}} as the default backing store in your storage cluster, create an instance of {{site.data.keyword.cos_full_notm}}. Then, create a set of HMAC credentials and a Kubernetes secret that uses your {{site.data.keyword.cos_short}} HMAC credentials. If you don't specify {{site.data.keyword.cos_full_notm}} credentials during installation, then the default backing store in your storage cluster is created by using the PVs in your cluster. You can set up additional backing stores after deploying ODF, but you cannot change the default backing store.


[Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Create an `openshift-storage` namespace in your cluster. The driver pods are deployed to this namespace. Copy the following YAML and save it as `os-namespace.yaml` on your local machine.
    ```yaml
    apiVersion: v1
    kind: Namespace
    metadata:
      labels:
        openshift.io/cluster-monitoring: "true"
      name: openshift-storage
    ```
    {: codeblock}

1. Create the `openshift-storage` namespace by using the YAML file that you saved.
    ```sh
    oc create -f os-namespace.yaml
    ```
    {: pre}

1. Verify that the namespace is created.
    ```sh
    oc get namespaces | grep storage
    ```
    {: pre}

1. Create an {{site.data.keyword.cos_full_notm}} service instance.
    ```sh
    ibmcloud resource service-instance-create noobaa-store cloud-object-storage standard global
    ```
    {: pre}

1. Create HMAC credentials. Make a note of your credentials.
    ```sh
    ibmcloud resource service-key-create cos-cred-rw Writer --instance-name noobaa-store --parameters '{"HMAC": true}'
    ```
    {: pre}

1. Create the Kubernetes secret named `ibm-cloud-cos-creds` in the `openshift-storage` namespace that uses your {{site.data.keyword.cos_short}} HMAC credentials. When you run the command, specify your {{site.data.keyword.cos_short}} HMAC access key ID and secret access key. Note that your secret must be named `ibm-cloud-cos-creds`.
    ```sh
    oc -n 'openshift-storage' create secret generic 'ibm-cloud-cos-creds' --type=Opaque --from-literal=IBM_COS_ACCESS_KEY_ID=<access_key_id> --from-literal=IBM_COS_SECRET_ACCESS_KEY=<secret_access_key>
    ```
    {: pre}

1. Verify that your secret is created.
    ```sh
    oc get secrets -A | grep cos
    ```
    {: pre}

### Preparing your cluster for an OpenShift Data Foundation installation
{: #odf-cluster-prepare-classic}
Before you install OpenShift Data Foundation in a classic cluster, review the following steps to prepare your cluster for an ODF installation.
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

1. Repeat step 3 for each worker node that you want to use in your ODF deployment.

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

1. [Get your local device details](#odf-classic-get-devices).

<br />

### Getting your device details
{: #odf-classic-get-devices}

Before you install ODF, get the details of the local disks on your worker nodes.
{: shortdesc}

1. Log in to your cluster and get a list of available worker nodes. Make a note of the worker nodes that you want to use in your OCS deployment.
    ```sh
    oc get nodes
    ```
    {: pre}

2. Log in to each worker node that you want to use for your ODF.
    ```sh
    oc debug node/<node-name>
    ```
    {: pre}

3. After you deploy the debug pod on the worker node, run the following command to allow host binaries.
    ```sh
    chroot /host
    ```
    {: pre}

4. List the available disks on the worker node.
    ```sh
    lsblk
    ```
    {: pre}

5. Review the command output for available disks. You can use only unmounted disks for ODF deployments, such as `sdc` disks in the following example. Note the initial storage capacity of your ODF deployment is equal to the size of the disk that you specify as the `osd-device-path`. In this example, the `sdc` disk is unmounted and has two availabe partitions: `sdc1` and `sdc2`.
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
    {: screen}

6. For each unmounted disk that you want to use in your deployment, find the disk ID. In the following example, the ID for the `sdc1` partition is `scsi-3600605b00d87b43027b3bc310a64c6c9-part1` and the ID for the `sdc2` partition is `scsi-3600605b00d87b43027b3bc310a64c6c9-part2`.

    ```sh
    ls -l /dev/disk/by-id/
    ```
    {: pre}

    **Example output**
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
    {: screen}

7. Repeat the previous steps for each worker node that you want to use for your OpenShift Data Foundation deployment.

8. [Install ODF in your cluster](#install-odf-cli-classic).

<br />

## Installing the add-on from the CLI
{: #install-odf-cli-classic}

You can install the add-on by using the [`ibmcloud oc cluster addon enable` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable).
{: shortdesc}

If you want to use an {{site.data.keyword.cos_full_notm}} service instance as your default backing store, make sure that you [created the service instance](#odf-create-cos), and created the Kubernetes secret in your cluster. When you create the ODF CRD in your cluster, ODF looks for a secret named `ibm-cloud-cos-creds` to set up the default backing store by using your {{site.data.keyword.cos_short}} HMAC credentials.
{: note}

1. Review the [parameter reference](#odf-classic-param-ref). When you enable the add-on, you can override the default values by specifying the `--param "key=value"` flag for each parameter that you want to override. Note that for Classic clusters, you must provide the device paths to the local disks that you want to use.
1. Before you enable the add-on, review the [changelog](/docs/openshift?topic=openshift-odf_addon_changelog) for the latest version information. Note that the add-on supports `n+1` cluster versions. For example, you can deploy version `4.7.0` of the add-on to an OCP 4.7 or 4.8 cluster. If you have a cluster version other than the default, you must specify the `--version` flag when you enable the add-on.
1. Review the add-on options. Note that add-on options are only available for version `4.7.0` and later.
    ```sh
    ibmcloud oc cluster addon options --addon openshift-data-foundation
    ```
    {: pre}

    ```sh
    Add-on Options
    Option                Default Value   
    monStorageClassName   ibmc-vpc-block-metro-10iops-tier   
    osdSize               250Gi   
    osdDevicePaths        invalid   
    workerNodes           all   
    ocsUpgrade            false   
    ocsDeploy             false   
    monSize               20Gi   
    numOfOsd              1   
    monDevicePaths        invalid   
    osdStorageClassName   ibmc-vpc-block-metro-10iops-tier
    clusterEncryption     false
    ```
    {: screen}

1. Enable the `openshift-data-foundation` add-on. If you also want to deploy ODF and create your storage cluster from the CLI, you can specify the `"ocsDeploy=true"` flag. If you want to override any of the default parameters, specify the `--param "key=value"` flag for each parameter you want to override. If you don't want to create your storage cluster when you enable the add-on, you can enable the add-on first, then create your storage cluster later by creating a CRD.

    ```sh
    ibmcloud oc cluster addon enable openshift-data-foundation -c <cluster_name> --version <version> --param "ocsDeploy=true"
    ```
    {: pre}

    **Example command for overriding the `osdSize` parameter**:
    ```sh
    ibmcloud oc cluster addon enable openshift-data-foundation -c <cluster_name> --version <version> --param "ocsDeploy=true" --param "osdSize=500Gi"
    ```
    {: pre}

1. Verify the add-on is in a `Ready` state.
    ```sh
    ibmcloud oc cluster addon ls -c <cluster_name>
    ```
    {: pre}

1. Verify that the `ibm-ocs-operator-controller-manager-*****` pod is running in the `kube-system` namespace.
    ```sh
    oc get pods -A | grep ibm-ocs-operator-controller-manager
    ```
    {: pre}

<br />

## Installing the OpenShift Data Foundation add-on from the console
{: #install-odf-console-classic}

To install ODF in your cluster, complete the following steps.
{: shortdesc}

1. Before you enable the add-on, review the [changelog](/docs/openshift?topic=openshift-odf_addon_changelog) for the latest version information. Note that the add-on supports `n+1` cluster versions. For example, you can deploy version 4.7.0 of the add-on to an OCP 4.7 or 4.8 cluster. If you have a cluster version other than the default, you must install the add-on from the CLI and specify the `--version` flag.
1. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster where you want to install the add-on.
2. On the cluster **Overview** page, click **Add-ons**.
3. On the OpenShift Data Foundation card, click **Install**.

**Next steps** [Create your storage cluster](#ocs-classic-deploy-crd).

## Creating your storage cluster
{: #ocs-classic-deploy-crd}

To deploy ODF in your classic cluster, you can create a custom resource definition to specify your storage device details.
{: shortdesc}

If you want to use an {{site.data.keyword.cos_full_notm}} service instance as your default backing store, make sure that you [created the service instance](#odf-create-cos), and created the Kubernetes secret in your cluster. When you create the ODF CRD in your cluster, ODF looks for a secret named `ibm-cloud-cos-creds` to set up the default backing store by using your {{site.data.keyword.cos_short}} HMAC credentials.
{: note}

1. Create a custom resource called `OcsCluster`. Save and edit the following custom resource definition to include the device paths for the local disks [that you retrieved earlier](#odf-classic-get-devices). If you don't specify the optional `workerNodes` parameter, then all worker nodes in your cluster are used for the ODF deployment. Be sure to include the `/dev/disk/by-id/` path when you specify your storage devices. 
    - If your worker node has raw disks with partitions, you need one partition for the OSD and one partition for the MON per worker node. As a best practice, and to maximize storage capacity on partitioned disks, you can specify the smaller partition or disk for the MON, and the larger partition or disk for the OSD. Note that the initial storage capacity of your ODF configuration is equal to the size of the disk that you specify as the `osd-device-path` when you create your configuration. 
    - If you devices aren't partitioned, you  must specify one raw disk for the MON and one for the OSD for each worker node that you want to use.

    **Example custom resource for installing ODF on all worker nodes in a classic cluster with partitioned disks**
    ```yaml
    apiVersion: ocs.ibm.io/v1
    kind: OcsCluster
    metadata:
        name: ocscluster
      spec:
        monStorageClassName: localfile
        monSize: 20Gi
        osdStorageClassName: localblock
        osdSize: "1"
        numOfOsd: 1
        billingType: advanced
        ocsUpgrade: false
        monDevicePaths:
          - <device-by-id> # Example: /dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part1
          - <device-by-id> # Example: /dev/disk/by-id/scsi-1111111a11a11a11111a1aa111a11a1a1-part1
          - <device-by-id> # Example: /dev/disk/by-id/scsi-2222222a22a22a22222a2aa222a22a2a2-part1
        osdDevicePaths:
          - <device-by-id> # Example: /dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part2
          - <device-by-id> # Example: /dev/disk/by-id/scsi-1111111a11a11a11111a1aa111a11a1a1-part2
          - <device-by-id> # Example: dev/disk/by-id/scsi-2222222a22a22a22222a2aa222a22a2a2-part2
    ```
    {: codeblock}

    **Example custom resource for installing ODF only on certain worker nodes in a classic cluster with partitioned disks**
    ```yaml
    apiVersion: ocs.ibm.io/v1
    kind: OcsCluster
    metadata:
        name: ocscluster
      spec:
        monStorageClassName: localfile
        monSize: 20Gi
        osdStorageClassName: localblock
        osdSize: "1"
        numOfOsd: 1
        billingType: advanced
        ocsUpgrade: false
        monDevicePaths:
          - <device-by-id> # Example: /dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0
          - <device-by-id> # Example: /dev/disk/by-id/scsi-1111111a11a11a11111a1aa111a11a1a1
          - <device-by-id> # Example: /dev/disk/by-id/scsi-2222222a22a22a22222a2aa222a22a2a2
        osdDevicePaths:
          - <device-by-id> # Example: /dev/disk/by-id/scsi-3333333a33a33a33333a3aa333a33a3a3
          - <device-by-id> # Example: /dev/disk/by-id/scsi-4444444a44a44a44444a4aa444a44a4a4
          - <device-by-id> # Example: dev/disk/by-id/scsi-5555555a55a55a55555a5aa555a55a5a5
        workerNodes: # Specify the private IP addresses of each worker node where you want to install OCS.
          - <workerNodes> # To get a list worker nodes, run `oc get nodes`.
          - <workerNodes>
          - <workerNodes>
    ```
    {: codeblock}

    **Example custom resource for installing ODF on all worker nodes in a classic cluster with non-partitioned disks**
    ```yaml
    apiVersion: ocs.ibm.io/v1
    kind: OcsCluster
    metadata:
        name: ocscluster
      spec:
        monStorageClassName: localfile
        monSize: 20Gi
        osdStorageClassName: localblock
        osdSize: "1"
        numOfOsd: 1
        billingType: advanced
        ocsUpgrade: false
        monDevicePaths: 
          - <device-by-id> # Example: /dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0
          - <device-by-id> # Example: /dev/disk/by-id/scsi-1111111a11a11a11111a1aa111a11a1a1
          - <device-by-id> # Example: /dev/disk/by-id/scsi-2222222a22a22a22222a2aa222a22a2a2
        osdDevicePaths:
          - <device-by-id> # Example: /dev/disk/by-id/scsi-3333333a33a33a33333a3aa333a33a3a3
          - <device-by-id> # Example: /dev/disk/by-id/scsi-4444444a44a44a44444a4aa444a44a4a4
          - <device-by-id> # Example: dev/disk/by-id/scsi-5555555a55a55a55555a5aa555a55a5a5
    ```
    {: codeblock}

    **Example custom resource for installing ODF only on certain worker nodes in a classic cluster with non-partitioned disks**
    ```yaml
    apiVersion: ocs.ibm.io/v1
    kind: OcsCluster
    metadata:
        name: ocscluster
      spec:
        monStorageClassName: localfile
        monSize: 20Gi
        osdStorageClassName: localblock
        osdSize: "1"
        numOfOsd: 1
        billingType: advanced
        ocsUpgrade: false
        monDevicePaths:
          - <device-by-id> # Example: /dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part1
          - <device-by-id> # Example: /dev/disk/by-id/scsi-1111111a11a11a11111a1aa111a11a1a1-part1
          - <device-by-id> # Example: /dev/disk/by-id/scsi-2222222a22a22a22222a2aa222a22a2a2-part1
        osdDevicePaths:
          - <device-by-id> # Example: /dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part2
          - <device-by-id> # Example: /dev/disk/by-id/scsi-1111111a11a11a11111a1aa111a11a1a1-part2
          - <device-by-id> # Example: dev/disk/by-id/scsi-2222222a22a22a22222a2aa222a22a2a2-part2
        workerNodes: # Specify the private IP addresses of each worker node where you want to install OCS.
          - <workerNodes> # To get a list worker nodes, run `oc get nodes`.
          - <workerNodes>
          - <workerNodes>
    ```
    {: codeblock}

1. Save the file and create the `OcsCluster` custom resource to your cluster.
    ```sh
    oc create -f <ocs_cluster_filename>
    ```
    {: pre}

1. Verify that your `OcsCluster` custom resource is running.
    ```sh
    oc describe OcsCluster ocscluster
    ```
    {: pre}

**Next steps**: [Deploy an app that uses ODF](/docs/openshift?topic=openshift-odf-deploy-app)


## Parameter reference
{: #odf-classic-param-ref}

Refer to the following OpenShift Data Foundation parameters when you use the add-on or operator in classic clusters.
{: shortdesc}


| Parameter | Description | Default value |
| --- | --- | --- |
| `monStorageClassName` | Enter the name of the storage class that you want to use for your MON devices. For baremetal worker nodes, enter `localfile`. | N/A |
| `monDevicePaths` | Enter a comma separated list of the disk-by-id paths for the storage devices that you want to use for the monitor (MON) pods. The devices that you specify must have at least `20GiB` of space and must be unformatted and unmounted. The parameter format is `/dev/disk/by-id/<device-id>`. Example device path value for a partitioned device: `/dev/disk/by-id/scsi-3600605b00d87b43027b3bc310a64c6c9-part1`. If you specify more than one device path, be sure there are no spaces between each path. For example: `/dev/disk/by-id/scsi-3600605b00d87b43027b3bc310a64c6c9-part1`,`/dev/disk/by-id/scsi-3600605b00d87b43027b3bc310a64c6c9-part2`. | N/A |
| `monSize` | Enter a size for your monitoring storage devices. Example: `20Gi`. | N/A |
| `osdStorageClassName` | Enter the name of the storage class that you want to use for your OSD devices. For baremetal worker nodes, enter `localblock`. | N/A |
| `osdSize` | Enter a size for your OSD block storage devices. Example: `100Gi`. | N/A |
| `osdDevicePath` | Enter a comma separated list of the device paths for the devices that you want to use for the OSD devices. The devices that you specify are used as your application storage in your configuration. Each device must have at least `100GiB` of space and must be unformatted and unmounted. The parameter format is `/dev/disk/by-id/<device-id>`. Example device path value for a partitioned device: `/dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part2`. If you specify more than one device path, be sure there are no spaces between each path. For example: `/dev/disk/by-id/scsi-1111111a11a11a11111a1aa111a11a1a1-part2`,`/dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part2`. |
| `numOfOsd` | Enter the number object storage daemons (OSDs) that you want to create. ODF creates three times the specified number. For example, if you enter `1`, ODF creates 3 OSDs. | `1` |
| `billingType` | Enter a `billingType` of either `essentials` or `advanced` for your OCS deployment. | `hourly` |
| `ocsUpgrade` | Enter a `true` or `false` to upgrade the major version of your ODF deployment. | `false` |
| `workerNodes` | **Optional**: Enter the private IP addresses for the worker nodes that you want to use for your ODF deployment. Do not specify this parameter if you want to use all of the worker nodes in your cluster. To retrieve your worker node IP addresses, run `oc get nodes`. | N/A |
| `clusterEncryption` | Available for add-on version 4.7.0 and later. Enter `true` or `false` to enable encryption. |
{: caption="Classic OpenShift Data Foundation parameter reference" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the custom resource parameter. The second column is a brief description of the parameter. The third column is the default value of the parameter."}


