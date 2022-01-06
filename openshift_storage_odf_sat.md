---

copyright:
  years: 2014, 2022
lastupdated: "2022-01-06"

keywords: openshift, openshift data foundation, openshift container storage, ocs, satellite

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}

 


# Deploying OpenShift Data Foundation on {{site.data.keyword.satelliteshort}} clusters
{: #deploy-odf-sat}

OpenShift Data Foundation is a highly available storage solution that you can use to manage persistent storage for your containerized workloads in {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

Installing OpenShift Data Foundation from OperatorHub is not supported on {{site.data.keyword.satelliteshort}} clusters. To install ODF, complete the following steps to deploy the cluster add-on or the {{site.data.keyword.satelliteshort}} configuration template.
{: important}


## Planning your setup
{: #odf-sat-plan}

Before you install ODF in your {{site.data.keyword.satelliteshort}} cluster, each cluster must meet the following prerequisite conditions.
{: shortdesc}

1. [Install](/docs/openshift?topic=openshift-openshift-cli#cli_oc) or [update the `oc` CLI](/docs/openshift?topic=openshift-openshift-cli#cs_cli_upgrade).
1. [Set up a {{site.data.keyword.satelliteshort}} location](/docs/satellite?topic=satellite-locations).
1. [Attach at least 3 hosts](/docs/satellite?topic=satellite-hosts#attach-hosts) that meet the [minimum host requirements](/docs/satellite?topic=satellite-host-reqs). Additionally, each host must have a minimum of 16 CPUs and 64 GB RAM.
1. [Create a cluster](/docs/openshift?topic=openshift-clusters) with the hosts that you previously attached to the location.

You can also deploy ODF to your {{site.data.keyword.satelliteshort}} cluster by using the {{site.data.keyword.satelliteshort}} storage templates. Templates allow you to automate your deployment across multiple {{site.data.keyword.satelliteshort}} clusters. For more information, see [ODF with remote disks](/docs/satellite?topic=satellite-config-storage-ocs-remote) or [ODF with local disks](/docs/satellite?topic=satellite-config-storage-ocs-local) depending on your cluster setup.
{: tip}

### Optional: Setting up an {{site.data.keyword.cos_full_notm}} service instance
{: #odf-create-cos-sat}

If you want to set up {{site.data.keyword.cos_full_notm}} as the default backing store in your storage cluster, create an instance of {{site.data.keyword.cos_full_notm}}. Then, create a set of HMAC credentials and a Kubernetes secret that uses your {{site.data.keyword.cos_short}} HMAC credentials. If you don't specify {{site.data.keyword.cos_full_notm}} credentials during installation, then the default backing store in your storage cluster is created by using the PVs in your cluster. You can set up additional backing stores after deploying ODF, but you can't change the default backing store.


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


## Creating a Kubernetes secret that contains your {{site.data.keyword.satelliteshort}} link credentials
{: #odf-sat-secret-create}

After you [create a link endpoint](/docs/satellite?topic=satellite-link-location-cloud#link-about) and before you install ODF, create a Kubernetes secret with your link credentials.
{: shortdesc}

1. List the secrets in the `kube-system` namespace of your cluster and look for the `storage-secret-store`.

    ```sh
    oc get secrets -n kube-system | grep storage-secret-store
    ```
    {: pre}

1. If the `storage-secret-store` secret doesn't exist, create it.

    1. Create a `secret.yaml` file that has your IAM API key.

        ```yaml
        apiVersion: v1
        kind: Secret
        metadata:
          name: storage-secret-store
          namespace: kube-system
        type: Opaque
        stringData:
          iam_api_key: "<iam_api_key>" # Enter your IAM API key
        ```
        {: codeblock}

    1. Create the secret in your cluster. 

        ```sh
        oc create -f secret.yaml -n kube-system
        ```
        {: pre}

1. If the `storage-secret-store` secret exists, update it.

    1. Edit the `storage-secret-store` secret.

        ```sh
        oc edit secret storage-secret-store -n kube-system
        ```
        {: pre}

        ```yaml
        apiVersion: v1
        kind: Secret
        metadata:
          name: storage-secret-store
          namespace: kube-system
        type: Opaque
        stringData:
          iam_api_key: "<iam_api_key>" # Enter your IAM API key
        ```
        {: codeblock}

    1. Save and close the file to apply the secret to your cluster.

1. Install OpenShift Data Foundation by using the [CLI](#install-odf-cli-sat).


## Installing the add-on from the CLI
{: #install-odf-cli-sat}

You can install the add-on by using the [`ibmcloud oc cluster addon enable` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable).
{: shortdesc}

If you want to use an {{site.data.keyword.cos_full_notm}} service instance as your default backing store, make sure that you [created the service instance](#odf-create-cos-sat), and created the Kubernetes secret in your cluster. When you create the ODF CRD in your cluster, ODF looks for a secret named `ibm-cloud-cos-creds` to set up the default backing store that uses your {{site.data.keyword.cos_short}} HMAC credentials.
{: note}

1. Review the [parameter reference](#odf-sat-param-ref). When you enable the add-on, you can override the default values by specifying the `--param "key=value"` flag for each parameter that you want to override.

1. Before you enable the add-on, review the [changelog](/docs/openshift?topic=openshift-odf_addon_changelog) for the latest version information. Note that the add-on supports `n+1` cluster versions. For example, you can deploy version `4.7.0` of the add-on to an OCP 4.7 or 4.8 cluster. If you have a cluster version other than the default, you must specify the `--version` flag when you enable the add-on.

1. Review the add-on options. Note that the default storage classes for `monStorageClassName` and `osdStorageClassName` are {{site.data.keyword.block_storage_is_short}} storage classes. For {{site.data.keyword.satelliteshort}}, you must override these values and specify a storage class that supports dynamic provisioning based on the block storage storage driver in your cluster. If you want to use local volumes on worker nodes instead of dynamically provisioned volumes, you must first [gather your local device information](#odf-sat-gather), then when you enable the add-on, specify `localfile` for `monStorageClassName` and `localblock` for `osdStorageClassName`.

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
    odfDeploy             true   
    monSize               20Gi   
    numOfOsd              1   
    monDevicePaths        invalid   
    osdStorageClassName   ibmc-vpc-block-metro-10iops-tier
    clusterEncryption     false
    ```
    {: screen}

1. Enable the `openshift-data-foundation` add-on. Then, create your storage cluster by creating a CRD.

    ```sh
    ibmcloud oc cluster addon enable openshift-data-foundation -c <cluster_name> --version 4.7.0 --param "odfDeploy=false"
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

1. [Create an ODF custom resource](#odf-sat-deploy-crd).



## Gathering your local block storage device details
{: #odf-sat-gather}

If you want to deploy ODF on a {{site.data.keyword.satelliteshort}} with local block storage devices, you must first gather the device paths to the disks on your worker nodes.
{: shortdesc}

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

5. Review the command output for available disks. You can use only unmounted disks for ODF deployments, such as `sdc` disks in the following example. Note the initial storage capacity of your ODF deployment is equal to the size of the disk that you specify as the `osd-device-path`. In this example, the `sdc` disk is unmounted and has two available partitions: `sdc1` and `sdc2`.
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

    Example output
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

**Next steps** Install ODF by [using the CLI](#install-odf-cli-sat).

## Creating your storage cluster
{: #odf-sat-deploy-crd}

To create an ODF storage cluster in your {{site.data.keyword.satelliteshort}} cluster by using dynamic provisioning for your storage volumes, you can create a custom resource to specify storage device details.
{: shortdesc}

If you want to use an {{site.data.keyword.cos_full_notm}} service instance as your default backing store, make sure that you [created the service instance](#odf-create-cos-sat), and created the Kubernetes secret in your cluster. When you create the ODF CRD in your cluster, ODF looks for a secret named `ibm-cloud-cos-creds` to set up the default backing store that uses your {{site.data.keyword.cos_short}} HMAC credentials.
{: note}

If you enabled the add-on from the CLI and set the `odfDeploy=false` parameter, complete the following steps to create a storage cluster CRD to deploy ODF. If you enabled the add-on from the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} or from the CLI and did not set `odfDeploy=false`, you don't need to create a CRD.

1. Create a custom resource called `OcsCluster`. Save one of the following custom resource definition files on your local machine and edit it to include the name of the custom storage class that you created earlier as the `monStorageClassName` and `osdStorageClassName` parameters. For more information about the `OcsCluster` parameters, see the [parameter reference](/docs/openshift?topic=openshift-deploy-odf-vpc#odf-vpc-param-ref).

    Example custom resource definition for installing ODF on all worker nodes.
    
    ```yaml
    apiVersion: ocs.ibm.io/v1
    kind: OcsCluster
    metadata:
        name: ocscluster # Kubernetes resource names can't contain capital letters or special characters. Enter a name for your resource that uses only lowercase letters, numbers, `-` or `.`
    spec:
      monStorageClassName: <monStorageClassName> # For multizone clusters, specify a storage class with a waitForFirstConsumer volume binding mode
      monSize: <monSize>
      osdStorageClassName: <osdStorageClassName> # For multizone clusters, specify a storage class with a waitForFirstConsumer volume binding mode
      osdSize: <osdSize> # The OSD size is the total storage capacity of your storage cluster
      numOfOsd: 1
      billingType: advanced
      ocsUpgrade: false
    ```
    {: codeblock}

    Example custom resource definition for installing ODF only on specified worker nodes.
    
    ```yaml
    apiVersion: ocs.ibm.io/v1
    kind: OcsCluster
    metadata:
        name: ocscluster-sat
    spec:
      monStorageClassName: <monStorageClassName> # For multizone clusters, specify a storage class with a waitForFirstConsumer volume binding mode
      monSize: <monSize>
      osdStorageClassName: <osdStorageClassName> # For multizone clusters, specify a storage class with a waitForFirstConsumer volume binding mode
      osdSize: <osdSize> # The OSD size is the total storage capacity of your storage cluster
      numOfOsd: 1
      billingType: advanced
      ocsUpgrade: false
      workerNodes: # Specify the private IP addresses of the worker nodes that you want to use.
        - <workerNodes> # To get a list worker nodes, run `oc get nodes`.
        - <workerNodes>
        - <workerNodes>
    ```
    {: codeblock}


    Example custom resource for installing ODF on all worker nodes.
    
    ```yaml
    apiVersion: ocs.ibm.io/v1
    kind: OcsCluster
    metadata:
        name: ocscluster # Kubernetes resource names can't contain capital letters or special characters. Enter a name for your resource that uses only lowercase letters, numbers, `-` or `.`
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

    Example custom resource for installing ODF only on certain worker nodes.
    

    ```yaml
    apiVersion: ocs.ibm.io/v1
    kind: OcsCluster
    metadata:
        name: ocscluster # Kubernetes resource names can't contain capital letters or special characters. Enter a name for your resource that uses only lowercase letters, numbers, `-` or `.`
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
    oc create -f <ocs-cluster-filename>.yaml
    ```
    {: pre}

1. Verify that your `OcsCluster` is running.

    ```sh
    oc describe ocscluster ocscluster
    ```
    {: pre}

## {{site.data.keyword.satelliteshort}}: OpenShift Data Foundation parameter reference
{: #odf-sat-param-ref}

Refer to the following parameters when you use the add-on or operator in {{site.data.keyword.satelliteshort}} clusters.
{: shortdesc}

| Parameter | Description | Default value |
| --- | --- | --- |
| `name` | Note that Kubernetes resource names can't contain capital letters or special characters. Enter a name for your resource that uses only lowercase letters, numbers, `-` or `.` | N/A |
| `monStorageClassName` | Enter the name of the storage class that you want to use for the monitor pod storage devices. To use the local disks on your worker nodes, enter `localfile`. To dynamically provision disks, enter the name of the storage class that you want to use. For **Multizone clusters**, make sure that you specify a storage class that has the `waitForFirstConsumer` binding mode. For **Single zone clusters**, enter the name of the storage class that you want to use. | N/A |
| `monDevicePaths` | **Local disks only** If you want to use dynamically provisioned disks in your storage cluster, don't specify the device path parameter. Enter a comma separated list of the disk-by-id paths for the storage devices that you want to use for the monitor (MON) pods. The devices that you specify must have at least `20GiB` of space and must not be formatted or mounted. The parameter format is `/dev/disk/by-id/<device-id>`. Example device path value for a partitioned device: `/dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part1`. If you specify more than one device path, be sure there are no spaces between each path. For example: `/dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part1`,`/dev/disk/by-id/scsi-1111111a11a11a11111a1aa111a11a1a1-part1`. | N/A |
| `monSize` | Enter a size for your monitoring storage devices. Example: `20Gi`. | N/A |
| `osdStorageClassName` | To use the local disks on your worker nodes, enter `localblock`. To dynamically provision volumes for your storage cluster, enter the name of the storage class that you want to use. For **Multizone clusters**, make sure that you specify a storage class that has the `waitForFirstConsumer` binding mode. For **Single zone clusters**, enter the name of the storage class that you want to use. | N/A |
| `osdSize` | Enter a size for your OSD block storage devices. Example: `100Gi`. | N/A |
| `osdDevicePath` | **Local disks only** If you want to use dynamically provisioned disks in your storage cluster, don't specify the device path parameter. Enter a comma separated list of the device paths for the devices that you want to use for the OSD devices. The devices that you specify are used as your application storage in your configuration. Each device must have at least `100GiB` of space and must not be formatted or mounted. The parameter format is `/dev/disk/by-id/<device-id>`. Example device path value for a partitioned device: `/dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part2`. If you specify more than one device path, be sure there are no spaces between each path. For example: `/dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part2`,`/dev/disk/by-id/scsi-1111111a11a11a11111a1aa111a11a1a1-part2`. |
| `numOfOsd` | Enter the number object storage daemons (OSDs) that you want to create. ODF creates three times the specified number. For example, if you enter `1`, ODF creates 3 OSDs. | `1` |
| `billingType` | Enter a `billingType` of either `essentials` or `advanced` for your OCS deployment. | `advanced` |
| `ocsUpgrade` | Enter a `true` or `false` to upgrade the major version of your ODF deployment. | `false` |
| `workerNodes` | **Optional**: Enter the private IP addresses for the worker nodes that you want to use for your ODF deployment. Don't specify this parameter if you want to use all the worker nodes in your cluster. To retrieve your worker node IP addresses, run `oc get nodes`. | N/A |
| `clusterEncryption` | Available for add-on version 4.7.0 and later. Enter `true` or `false` to enable encryption. |
{: caption="Parameter reference" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the custom resource parameter. The second column is a brief description of the parameter. The third column is the default value of the parameter."}






