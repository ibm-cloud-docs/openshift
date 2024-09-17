---

copyright:
  years: 2014, 2024
lastupdated: "2024-09-17"


keywords: openshift, openshift data foundation, openshift container storage, ocs, classic

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}




 

# Deploying OpenShift Data Foundation on Classic clusters
{: #deploy-odf-classic}

OpenShift Data Foundation is a highly available storage solution that you can use to manage persistent storage for your containerized workloads in {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

Installing OpenShift Data Foundation from OperatorHub is not supported on {{site.data.keyword.Bluemix_notm}} clusters. To install ODF, complete the following steps to deploy the cluster add-on.
{: important}

## Planning your setup
{: #odf-classic-plan}

Before you install ODF in your cluster, you must make sure that the following prerequisite conditions are met:

To install OpenShift Data Foundation on classic clusters, you must enable [VRF](/docs/account?topic=account-vrf-service-endpoint&interface=ui) in your account.
{: important}


1. [Install](/docs/openshift?topic=openshift-cli-install) or update the `oc` CLI
1. If you don't have virtual route forwarding (VRF) enabled in your account, enable [VRF](/docs/account?topic=account-vrf-service-endpoint&interface=ui).
    1. After you have enabled VRF, enable [Service endpoints](/docs/account?topic=account-vrf-service-endpoint&interface=ui#service-endpoint). 
1. [Review the SDS worker node flavors](/docs/openshift?topic=openshift-classic-flavors). In the tables for each metro area section, SDS flavors are in the **Bare Metal** tabs and end with `.ssd`.
1. Create a [classic cluster](/docs/openshift?topic=openshift-clusters) with a minimum of one worker node per zone across three zones. Choose worker nodes of flavor type `mb4c.32x384.3.8tb.ssd` or `mb4c.20x64.2x1.9tb.ssd` that have the required local disks for ODF.
1. [Prepare your classic cluster](#odf-cluster-prepare-classic).

### Optional: Setting up an {{site.data.keyword.cos_full_notm}} service instance
{: #odf-create-cos-classic}

If you want to set up {{site.data.keyword.cos_full_notm}} as the default backing store in your storage cluster, create an instance of {{site.data.keyword.cos_full_notm}}. Then, create a set of HMAC credentials and a Kubernetes secret that uses your {{site.data.keyword.cos_short}} HMAC credentials. If you don't specify {{site.data.keyword.cos_full_notm}} credentials during installation, then the default backing store in your storage cluster is created by using the PVs in your cluster. You can set up additional backing stores after deploying ODF, but you can't change the default backing store.


[Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

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

### Optional: Setting up encryption by using {{site.data.keyword.hscrypto}}
{: #odf-create-hscrypto-classic}

If you want to set up encryption, create an instance of {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}}. Then, create a root key, and a Kubernetes secret that uses your {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} credentials.

Your API key for {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} must have the following minimum required permissions:
:   `Reader`
:   `Reader Plus`

If you are using cluster wide encryption and storage class encryption, your API key must have the following required permissions:
:   `Reader`
:   `Reader Plus`
:   `Writer` 

1. Create an [{{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-provision&interface=ui) or [{{site.data.keyword.keymanagementserviceshort}}](/docs/key-protect?topic=key-protect-provision) service instance.

1. Create root key
    - [{{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-create-root-keys&interface=ui).
    - [{{site.data.keyword.keymanagementserviceshort}}](/docs/key-protect?topic=key-protect-create-root-keys&interface=ui).

1. After creating your instance and root key, make a note of your {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} instance name, instance ID, root key ID, and public endpoint.

1. Create a [service ID](/docs/account?topic=account-serviceids), [API key](/docs/account?topic=account-serviceidapikeys), and [access policy](/docs/account?topic=account-assign-access-resources) that allows access to either {{site.data.keyword.hscrypto}} and {{site.data.keyword.openshiftshort}} or {{site.data.keyword.keymanagementserviceshort}} and {{site.data.keyword.openshiftshort}}. Make a note of the API that you create. 

[Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. List your namespaces to determine whether you have an `openshift-storage` namespace. If you don't have an `openshift-storage` namespace, create it.
    ```sh
    oc get namespaces | grep openshift-storage
    ```
    {: pre}

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
        
1. Encode both the ID of your root key and the API key of the service ID that you created to base64.
    ```sh
    printf "ROOT-KEY-ID" | base64
    ```
    {: pre}
    
    ```sh
    printf "SERVICE-ID-API-KEY" | base64
    ```
    {: pre}

1. Create the Kubernetes secret in the `openshift-storage` namespace that uses your {{site.data.keyword.hscrypto}} credentials. 
    1. Save the following secret as a YAML file called `ibm-hpcs-secret.yaml`.
        ```yaml
        apiVersion: v1
        data:
          IBM_KP_CUSTOMER_ROOT_KEY: AaAAAaZAAAAy11AAAyAAkaAaQtAAk0AAA2AzY5AjYaaa67aa # your base64 encoded root key ID
          IBM_KP_SERVICE_API_KEY: AAAaaajAAAAAncmAAaaaaAAAAdAAId1AtVjBJRU1aAAaAeTh1aEw=AaaaA # your base64 encoded API
        kind: Secret
        metadata:
          name: ibm-hpcs-secret
          namespace: openshift-storage
        type: Opaque
        ```
        {: codeblock}
    
    1. Create the secret in your cluster.
        ```sh
        oc apply -f ibm-hpcs-secret.yaml
        ```
        {: pre}

1. Verify that your secret is created.
    ```sh
    oc get secrets -A | grep ibm-hpcs-secret
    ```
    {: pre}

### Preparing your cluster for an OpenShift Data Foundation installation
{: #odf-cluster-prepare-classic}

Before you install OpenShift Data Foundation, prepare your cluster.
{: shortdesc}


[Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).


1. Log in to each worker node in your cluster by using the `oc debug` command and complete the following steps.
    - Log in to the worker node. Replace `<worker_node_IP>` with the name of your worker node. To get the names of your worker nodes, run the **`oc get nodes`** command.
        ```sh
        oc debug node/<node name> -- chroot /host rm -rvf /var/lib/rook /mnt/local-storage
        ```
        {: pre}

    - For each disk partition, clear the `xfs` file system on the worker node. If you don't clear the file system, the OSD is not created.
        ```sh
        file -sL /dev/<partition>
        wipefs -a /dev/<partition>
        ```
        {: pre}
        
    - Edit the `/etc/kubernetes/kubelet.conf` file and change the value of the `EnableControllerAttachDetach` parameter to `true`.
        ```sh
        nano /etc/kubernetes/kubelet.conf
        ```
        {: pre}
    
    - Save and exit by using `ctrl + X`.
    
    - Restart the kubelet.
        ```sh
        systemctl restart kubelet
        ```
        {: pre}

    - Log out of the worker node.
        ```sh
        exit
        ```

1. Repeat the previous steps to wipe the file system for each worker node that you want to use in your ODF deployment.
    

### Getting your device details
{: #odf-classic-get-devices}

You can use automatic disk discovery to find available devices for ODF. However, if you want to manually specify storage devices for ODF, complete the following steps to retrieve your storage device details.
{: tip}

Before you install ODF, get the details of the local disks on your worker nodes.
{: shortdesc}

1. Log in to your cluster and get a list of available worker nodes. Make a note of the worker nodes that you want to use in your OCS deployment.
    ```sh
    oc get nodes
    ```
    {: pre}

1. Log in to each worker node that you want to use for your ODF.
    ```sh
    oc debug node/<node-name>
    ```
    {: pre}

1. After you deploy the debug pod on the worker node, run the following command to allow host binaries.
    ```sh
    chroot /host
    ```
    {: pre}

1. List the available disks on the worker node.
    ```sh
    lsblk
    ```
    {: pre}

1. Review the command output for available disks. You can use only unmounted disks for ODF deployments, such as `sdc` disks in the following example. Note the initial storage capacity of your ODF deployment is equal to the size of the disk that you specify as the `osd-device-path`. In this example, the `sdc` disk is unmounted and has two available partitions: `sdc1` and `sdc2`.
    ```sh
    NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
    sda      8:0    0   931G  0 disk
    |-sda1   8:1    0   256M  0 part /boot
    |-sda2   8:2    0     1G  0 part
     -sda3   8:3    0 929.8G  0 part /
    sdb      8:16   0 744.7G  0 disk
     -sdb1   8:17   0 744.7G  0 part /disk1
    sdc      8:32   0 744.7G  0 disk
    |-sdc1   8:33   0  18.6G  0 part
     -sdc2   8:34   0 260.8G  0 part
    ```
    {: screen}

1. For each unmounted disk that you want to use in your deployment, find the disk ID. In the following example, the ID for the `sdc1` partition is `scsi-3600605b00d87b43027b3bc310a64c6c9-part1` and the ID for the `sdc2` partition is `scsi-3600605b00d87b43027b3bc310a64c6c9-part2`.

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

1. Repeat the previous steps for each worker node that you want to use for your OpenShift Data Foundation deployment.

1. [Install ODF in your cluster](/docs/openshift?topic=openshift-deploy-odf-classic&interface=cli#install-odf-cli-classic).


## Installing the add-on from the CLI
{: #install-odf-cli-classic}
{: cli}

You can install the add-on by using the [`ibmcloud oc cluster addon enable` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable).
{: shortdesc}

If you want to use an {{site.data.keyword.cos_full_notm}} service instance as your default backing store, make sure that you [created the service instance](#odf-create-cos-classic), and created the Kubernetes secret in your cluster. When you create the ODF CRD in your cluster, ODF looks for a secret named `ibm-cloud-cos-creds` to set up the default backing store that uses your {{site.data.keyword.cos_short}} HMAC credentials.
{: note}

1. Review the [parameter reference](/docs/openshift?topic=openshift-openshift_storage_parameters). When you enable the add-on, you can override the default values by specifying the `--param "key=value"` option for each parameter that you want to override.

1. Before you enable the add-on, review the [change log](/docs/openshift?topic=openshift-odf_addon_changelog) for the latest version information. Note that the add-on supports `n+1` cluster versions. For example, you can deploy version `4.10.0` of the add-on to an OCP 4.9 or 4.11 cluster. If you have a cluster version other than the default, you must specify the `--version` option when you enable the add-on.

1. Review the add-on options for the version of the add-on that you want to deploy.
    ```sh
    ibmcloud oc cluster addon options --addon ADDON [--version VERSION]
    ```
    {: pre}

    Note that the default storage classes for `monStorageClassName` and `osdStorageClassName` are {{site.data.keyword.block_storage_is_short}} storage classes.
    {: note}

1. Enable the `openshift-data-foundation` add-on. If you want to deploy the ODF add-on only, you can specify the `"odfDeploy=false"` option. If you want to override any of the default parameters, specify the `--param "key=value"` option for each parameter you want to override. If you don't want to create your storage cluster when you enable the add-on, you can enable the add-on first, then create your storage cluster later by creating a CRD.

    Example command for enabling the add-on and automatically discovering local volumes, and enabling encryption with {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}}.
    ```sh
    ibmcloud oc cluster addon enable openshift-data-foundation -c <cluster-name> --version VERSION --param "odfDeploy=true"  --param "osdSize=250" --param "autoDiscoverDevices=true" --param "hpcsTokenUrl=https://iam.cloud.ibm.com/identity/token" --param "hpcsEncryption=true" --param "hpcsBaseUrl=<hpcs-instance-public-endpoint>" --param "hpcsInstanceId=<hpcs-instance-id>" --param "hpcsServiceName=<hpcs-instance-name>" --param "hpcsSecretName=<hpcs-secret-name>"
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

1. If you enabled the add-on and set the `odfDeploy=false` option, follow the steps to [create an ODF custom resource](/docs/openshift?topic=openshift-deploy-odf-classic&interface=cli#ocs-classic-deploy-crd).


## Installing the OpenShift Data Foundation add-on from the console
{: #install-odf-console-classic}
{: ui}

To install ODF in your cluster, complete the following steps.
{: shortdesc}

Version 4.11 is currently available for new clusters only. You can't upgrade a 4.10 deployment to 4.11. However, you can continue using ODF version 4.10.
{: note}

1. Before you enable the add-on, review the [change log](/docs/openshift?topic=openshift-odf_addon_changelog) for the latest version information. Note that the add-on supports `n+1` cluster versions.
1. [Review the parameter reference](/docs/openshift?topic=openshift-openshift_storage_parameters).
1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster where you want to install the add-on.
1. On the cluster **Overview** page, on the OpenShift Data Foundation card, click **Install**. The **Install ODF** panel opens.
1. In the **Install ODF** panel, enter the configuration parameters that you want to use for your ODF deployment.
1. Select either **Essentials** or **Advanced** as your billing plan.
1. For classic clusters, select **Local storage** to use local volumes on the worker nodes.
1. If you want to automatically discover the available storage devices on your worker nodes and use them in ODF, select **Local disk discovery**.
1. If you want to manually specify the storage devices on your worker nodes that you want to use in ODF, enter a comma-separated list of the disk IDs that you want to use. To find these disk IDs, see [Gathering your device details](#odf-classic-get-devices).
1. In the **Worker nodes** field, enter the node names of the worker nodes where you want to deploy ODF. You must enter at least 3 worker node names. To find you node names, run the `oc get nodes` command in your cluster. Leave this field blank to deploy ODF on all worker nodes. Node names must be comma-separated with no spaces between names. For example: `10.240.0.24,10.240.0.26,10.240.0.25`.
1. In the **Number of OSD disks required** field, enter the number of OSD disks (app storage) to provision on each worker node.
1. If you are re-enabling the add-on to upgrade the add-on version, select the **Upgrade ODF** option.
1. If you want to encrypt the volumes used by the ODF system pods, select **Enable cluster encryption**.
1. If you want to enable encryption on the OSD volumes (app storage), select **Enable volume encryption**.
    1. In the **Instance name** field, enter the name of your {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} instance. For example: `Hyper-Protect-Crypto-Services-eugb`.
    1. In the **Instance ID** field, enter your {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} instance ID. For example: `d11a1a43-aa0a-40a3-aaa9-5aaa63147aaa`.
    1. In the **Secret name** field, enter the name of the secret that you created using your {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} credentials. For example: `ibm-hpcs-secret`.
    1. In the **Base URL** field, enter the public endpoint of your {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} instance. For example: `https://api.eu-gb.hs-crypto.cloud.ibm.com:8389`.
    1. In the **Token URL** field, enter `https://iam.cloud.ibm.com/identity/token`.

## Creating your storage cluster
{: #ocs-classic-deploy-crd}
{: cli}

To deploy ODF in your classic cluster, you can create a custom resource definition to specify your storage device details.
{: shortdesc}

If you want to use an {{site.data.keyword.cos_full_notm}} service instance as your default backing store, make sure that you [created the service instance](#odf-create-cos-classic), and created the Kubernetes secret in your cluster. When you create the ODF CRD in your cluster, ODF looks for a secret named `ibm-cloud-cos-creds` to set up the default backing store by using your {{site.data.keyword.cos_short}} HMAC credentials.
{: note}

1. Create a custom resource called `OcsCluster`. Save and edit the following custom resource definition to include the device paths for the local disks [that you retrieved earlier](#odf-classic-get-devices). If you don't specify the optional `workerNodes` parameter, then all worker nodes in your cluster are used for the ODF deployment. Be sure to include the `/dev/disk/by-id/` path when you specify your storage devices. 
    - If your worker node has raw disks with partitions, you need one partition for the OSD and one partition for the MON per worker node. As a best practice, and to maximize storage capacity on partitioned disks, you can specify the smaller partition or disk for the MON, and the larger partition or disk for the OSD. Note that the initial storage capacity of your ODF configuration is equal to the size of the disk that you specify as the `osd-device-path` when you create your configuration. 
    - If you devices aren't partitioned, you  must specify one raw disk for the MON and one for the OSD for each worker node that you want to use.
    
    Example custom resource for installing ODF on all worker nodes in a version 4.8 cluster by using automatic disk discovery.
    ```yaml
    apiVersion: ocs.ibm.io/v1
    kind: OcsCluster
    metadata:
      name: ocscluster-classic
    spec:
      osdStorageClassName: localblock
      osdSize: "1"
      autoDiscoverDevices: true
    ```
    {: pre}
    
    Example custom resource for installing ODF on all worker nodes in a version 4.8 cluster with partitioned disks.
    ```yaml
    apiVersion: ocs.ibm.io/v1
    kind: OcsCluster
    metadata:
      name: ocscluster # Kubernetes resource names can't contain capital letters or special characters. Specify a name for your resource that uses only lowercase letters, numbers, `-` or `.`
    spec:
      osdStorageClassName: localblock
      osdSize: "1"
      numOfOsd: 1
      billingType: advanced
      ocsUpgrade: false
      osdDevicePaths:
        - <device-by-id> # Example: /dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part2
        - <device-by-id> # Example: /dev/disk/by-id/scsi-1111111a11a11a11111a1aa111a11a1a1-part2
        - <device-by-id> # Example: dev/disk/by-id/scsi-2222222a22a22a22222a2aa222a22a2a2-part2
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

1. [Deploy an app that uses ODF](/docs/openshift?topic=openshift-odf-deploy-app)




## Limitations
{: #odf-limitations-classic}


You can't use both the `ibmcloud-block-storage-plugin` and the ODF add-on at the same time. To install ODF, you must first edit the `/etc/kubernetes/kubelet.conf` file and change the value of the `EnableControllerAttachDetach` parameter to `true` which changes the default volume attachment behavior for the cluster. This means you can't dynamically provision volumes by using the `ibmc-block-*` storage classes. Instead, you must create volumes by using the [ODF storage classes](/docs/openshift?topic=openshift-ocs-sc-ref).
