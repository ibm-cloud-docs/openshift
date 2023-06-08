---

copyright:
  years: 2014, 2023
lastupdated: "2023-06-08"

keywords: openshift, openshift data foundation, openshift container storage, ocs

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}




# Deploying OpenShift Data Foundation on VPC clusters
{: #deploy-odf-vpc}

OpenShift Data Foundation is a highly available storage solution that you can use to manage persistent storage for your containerized workloads in {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

Installing OpenShift Data Foundation from OperatorHub is not supported on {{site.data.keyword.Bluemix_notm}} clusters. To install ODF, complete the following steps to deploy the cluster add-on.
{: important}

Minimum required permissions
:   `Administrator` platform access role
:   `Manager` service access role for the cluster in {{site.data.keyword.containerlong_notm}}.


## Prerequisites
{: #ocs-storage-vpc}

Review the following prerequisites.
{: shortdesc}

1. [Install](/docs/openshift?topic=openshift-openshift-cli) or update the `oc` CLI.
1. Create a [VPC cluster](/docs/openshift?topic=openshift-clusters) with at least 3 worker nodes. For high availability, create a cluster with at least one worker node per zone across three zones. Each worker node must have a minimum of 16 CPUs and 64 GB RAM.

    You can deploy OpenShift Data Foundation on 3 worker nodes of 16 CPUs and 32 GB RAM, but you must taint your worker nodes to run only ODF pods. You can't run any additional app workloads or system pods on your ODF nodes when you use this setup.
    {: important}

### Optional: Setting up an {{site.data.keyword.cos_full_notm}} service instance
{: #odf-create-cos}

Complete the following steps to create an {{site.data.keyword.cos_full_notm}} instance which you can use as the default backing store in your ODF deployment. If you don't want to set up {{site.data.keyword.cos_full_notm}}, you can skip this step and [install the add-on](#install-odf-cli-vpc).
{: shortdesc}

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
{: #odf-create-hscrypto-vpc}

If you want to set up encryption by using {{site.data.keyword.hscrypto}}, create an instance of {{site.data.keyword.hscrypto}}. Then, create a root key, and a Kubernetes secret that uses your {{site.data.keyword.hscrypto}} credentials.

Storage class encryption is available only for versions `4.10.0` and later of OpenShift Data Foundation.
{: note}

1. Create an [{{site.data.keyword.hscrypto}} service instance](/docs/hs-crypto?topic=hs-crypto-provision&interface=ui).

1. Create [root key](/docs/hs-crypto?topic=hs-crypto-create-root-keys&interface=ui).

1. After creating your instance and root key, make a note of your {{site.data.keyword.hscrypto}} instance name, instance ID, root key ID, and public endpoint.

1. Create a [service ID](/docs/account?topic=account-serviceids), [API key](/docs/account?topic=account-serviceidapikeys), and [access policy](/docs/account?topic=account-assign-access-resources) that allows access to {{site.data.keyword.hscrypto}} and {{site.data.keyword.openshiftshort}}. Make a note of the API that you create. 

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
        {: pre}
    
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

## Installing the OpenShift Data Foundation add-on from the console
{: #install-odf-console-vpc}
{: ui}

To install ODF in your cluster, complete the following steps.
{: shortdesc}


1. Before you enable the add-on, review the [change log](/docs/openshift?topic=openshift-odf_addon_changelog) for the latest version information. 
1. [Review the parameter reference](#odf-vpc-param-ref).
1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster where you want to install the add-on.
1. On the cluster **Overview** page, on the OpenShift Data Foundation card, click **Install**. The **Install ODF** panel opens.
1. In the **Install ODF** panel, enter the configuration parameters that you want to use for your ODF deployment.
1. Select either **Essentials** or **Advanced** as your billing plan.
1. For VPC clusters, select **Remote provisioning** to dynamically provision volumes for ODF by using the {{site.data.keyword.block_storage_is_short}}.
1. In the **OSD storage class name** field, enter the name of the {{site.data.keyword.block_storage_is_short}} ODF storage class that you want to use to provision storage volumes. For multizone clusters, use a storage class with the `VolumeBindingMode` of `WaitForFirstConsumer`. See the [Storage Class Reference](/docs/openshift?topic=openshift-vpc-block#vpc-block-reference) for more information.
1. In the **OSD pod size** field, enter the size of the volume that you want to provision.
1. In the **Worker nodes** field, enter the node names of the worker nodes where you want to deploy ODF. You must enter at least 3 worker node names. To find your node names, run the **`oc get nodes`** command in your cluster. Leave this field blank to deploy ODF on all worker nodes.
1. In the **Number of OSD disks required** field, enter the number of OSD disks (app storage) to provision on each worker node.
1. If you want to encrypt the OSD volumes (cluster wide encryption) used by the ODF system pods, select **Enable cluster encryption**.
1. If you want to enable encryption for the application volumes (app storage), select **Enable volume encryption**.
    1. In the **Instance name** field, enter a unique name for your {{site.data.keyword.hscrypto}} instance. 
    1. In the **Instance type** field, enter the type of encryption instance. 
    1. In the **Instance ID** field, enter your {{site.data.keyword.hscrypto}} instance ID. For example: `d11a1a43-aa0a-40a3-aaa9-5aaa63147aaa`.
    1. In the **Secret name** field, enter the name of the secret that you created using your {{site.data.keyword.hscrypto}} credentials. For example: `ibm-hpcs-secret`.
    1. In the **Base URL** field, enter the public endpoint of your {{site.data.keyword.hscrypto}} instance. For example: `https://api.eu-gb.hs-crypto.cloud.ibm.com:8389`.
    1. In the **Token URL** field, enter `https://iam.cloud.ibm.com/identity/token`.


1. After you enter the parameters that you want to use, click **Install**

1. Wait a few minutes for the add-on deployment to complete. When the deployment is complete, the add-on status is `Normal - Addon Ready`.

1. Verify your installation. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Run the following command to verify the ODF pods are running.

    ```sh
    oc get pods -n openshift-storage
    ```
    {: pre}

Next steps
:   [Deploy an app that uses ODF](/docs/openshift?topic=openshift-odf-deploy-app).
    

## Installing the add-on from the CLI
{: #install-odf-cli-vpc}
{: cli}


You can install the add-on by using the [`ibmcloud oc cluster addon enable` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable).
{: shortdesc}

1. Review the [VPC parameter reference](#odf-vpc-param-ref). When you enable the add-on, you can override the default values by specifying the `--param "key=value"` option for each parameter that you want to override.

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. List the `openshift-data-foundation` add-on versions. Make a note of the default version and determine the version that you want to install.
    ```sh
    ibmcloud ks cluster addon versions
    ```
    {: pre}

1. Before you enable the add-on, review the [change log](/docs/openshift?topic=openshift-odf_addon_changelog) for the latest version information. Note that the add-on supports `n+1` cluster versions. For example, you can deploy version `4.10.0` of the add-on to an OCP `4.9` or `4.11` cluster. If you have a cluster version other than the default, you must specify the `--version` option when you enable the add-on.

1. Review the add-on options.

    ```sh
    ibmcloud oc cluster addon options --addon openshift-data-foundation --version 4.10.0
    ```
    {: pre}
    
    Add-on options for version 4.10.0.
    
    ```sh
    Option                Default Value   
    osdSize               250Gi   
    numOfOsd              1   
    clusterEncryption     false   
    hpcsTokenUrl          <Please provide HPCS token URL>   
    workerNodes           all   
    hpcsEncryption        false   
    hpcsBaseUrl           <Please provide HPCS Base URL>   
    osdStorageClassName   ibmc-vpc-block-metro-10iops-tier   
    hpcsInstanceId        <Please provide HPCS Service ID>   
    autoDiscoverDevices   false   
    hpcsServiceName       <Please provide HPCS service name>   
    hpcsSecretName        <Please provide the HPCS secret name>   
    odfDeploy             true   
    osdDevicePaths        <Please provide IDs of the disks to be used for OSD pods if using local disks or standard classic cluster>   
    ocsUpgrade            false   
    billingType           advanced 
    ```
    {: screen}

1. Enable the `openshift-data-foundation` add-on. If you want to override any of the default parameters, specify the `--param "key=value"` option for each parameter you want to override. If you don't want to create your storage cluster when you enable the add-on, you can enable the add-on first, then create your storage cluster later by creating a CRD.

    Example command to deploy add-on version 4.10 with the default storage cluster settings and encryption with {{site.data.keyword.hscrypto}} enabled.
    ```sh
    ibmcloud oc cluster addon enable openshift-data-foundation -c <cluster-name> --version 4.10.0 --param "odfDeploy=true" --param "hpcsTokenUrl=https://iam.cloud.ibm.com/identity/token" --param "hpcsEncryption=true" --param "hpcsBaseUrl=<hpcs-instance-public-endpoint>" --param "hpcsInstanceId=<hpcs-instance-id>" --param "hpcsServiceName=<hpcs-instance-name>" --param "hpcsSecretName=<hpcs-secret-name>"
    ```
    {: pre}

    Example command for deploying the ODF add-on only.
    
    ```sh
    ibmcloud oc cluster addon enable openshift-data-foundation -c <cluster_name> --version <version> --param "odfDeploy=false"
    ```
    {: pre}

    Example command for deploying the ODF and creating a storage cluster with the default configuration parameters.
    
    ```sh
    ibmcloud oc cluster addon enable openshift-data-foundation -c <cluster_name> --version <version> 
    ```
    {: pre}

    Example command for deploying the ODF and creating a storage cluster while overriding the `osdSize` parameter.
    
    ```sh
    ibmcloud oc cluster addon enable openshift-data-foundation -c <cluster_name> --version <version> --param "osdSize=500Gi"
    ```
    {: pre}

1. Verify the add-on is in a `Ready` state.

    ```sh
    oc get storagecluster -n openshift-storage
    ```
    {: pre}

    Example output:

    ```sh
    NAME                 AGE   PHASE   EXTERNAL   CREATED AT             VERSION
    ocs-storagecluster   53m   Ready              2023-03-10T12:20:52Z   4.11.0
    ```
    {: screen}


1. Verify that the `ibm-ocs-operator-controller-manager-*****` pod is running in the `kube-system` namespace.

    ```sh
    oc get pods -A | grep ibm-ocs-operator-controller-manager
    ```
    {: pre}

1. If you enabled the add-on with `odfDeploy` set to `false`, follow the steps to [create an ODF custom resource](#ocs-vpc-deploy-crd).

## Creating your ODF custom resource
{: #ocs-vpc-deploy-crd}
{: cli}

To create an ODF storage cluster in your VPC cluster by using dynamic provisioning for your storage volumes, you can create a custom resource to specify storage device details.
{: shortdesc}

If you want to use an {{site.data.keyword.cos_full_notm}} service instance as your default backing store, make sure that you [created the service instance](#odf-create-cos), and created the Kubernetes secret in your cluster. When you create the ODF CRD in your cluster, ODF looks for a secret named `ibm-cloud-cos-creds` to set up the default backing store that uses your {{site.data.keyword.cos_short}} HMAC credentials.
{: note}

1. Create a custom resource definition called `OcsCluster`. Save one of the following custom resource definition files on your local machine and edit it to include the name of the custom storage class that you created earlier as the `monStorageClassName` and `osdStorageClassName` parameters. For more information about the `OcsCluster` parameters, see the [parameter reference](#odf-vpc-param-ref).

    Example custom resource definition for installing ODF on all worker nodes on a 4.8 cluster.

    ```yaml
    apiVersion: ocs.ibm.io/v1
    kind: OcsCluster
    metadata:
      name: ocscluster-vpc # Kubernetes resource names can't contain capital letters or special characters. Enter a name for your resource that uses only lowercase letters, numbers, `-` or `.`
    spec:
      osdStorageClassName: <osdStorageClassName> # For multizone clusters, specify a storage class with a waitForFirstConsumer volume binding mode
      osdSize: <osdSize> # The OSD size is the total storage capacity of your OCS storage cluster
      numOfOsd: 1
      billingType: advanced
      ocsUpgrade: false
    ```
    {: codeblock}

    Example custom resource definition for installing ODF only on specified worker nodes on a 4.8 cluster.

    ```yaml
    apiVersion: ocs.ibm.io/v1
    kind: OcsCluster
    metadata:
      name: ocscluster-vpc # Kubernetes resource names can't contain capital letters or special characters. Enter a name for your resource that uses only lowercase letters, numbers, `-` or `.`
    spec:
      osdStorageClassName: <osdStorageClassName> # For multizone clusters, specify a storage class with a waitForFirstConsumer volume binding mode
      osdSize: <osdSize> # The OSD size is the total storage capacity of your OCS storage cluster
      numOfOsd: 1
      billingType: advanced
      ocsUpgrade: false
      workerNodes: # Specify the private IP addresses of the worker nodes where you want to install OCS.
        - <workerNodes> # To get a list worker nodes, run `oc get nodes`.
        - <workerNodes>
        - <workerNodes>
    ```
    {: codeblock}


2. Save the file and create the `OcsCluster` custom resource to your cluster.

    ```sh
    oc create -f <ocs-cluster-filename>.yaml
    ```
    {: pre}

3. Verify that your `OcsCluster` is running.

    ```sh
    oc describe ocscluster ocscluster-vpc
    ```
    {: pre}

    Example output.

    ```yaml
    Name:         ocscluster-vpc
    Namespace:    
    Labels:       <none>
    Annotations:  <none>
    API Version:  ocs.ibm.io/v1
    Kind:         OcsCluster
    Metadata:
        Creation Timestamp:  2021-03-23T20:56:51Z
    Finalizers:
      finalizer.ocs.ibm.io
    Generation:  1
    Managed Fields:
      API Version:  ocs.ibm.io/v1
      Fields Type:  FieldsV1
      fieldsV1:
        f:spec:
          .:
          f:billingType:
          f:monSize:
          f:monStorageClassName:
          f:numOfOsd:
          f:ocsUpgrade:
          f:osdSize:
          f:osdStorageClassName:
      Manager:      oc
      Operation:    Update
      Time:         2021-03-23T20:56:51Z
      API Version:  ocs.ibm.io/v1
      Fields Type:  FieldsV1
      fieldsV1:
        f:metadata:
          f:finalizers:
            .:
            v:"finalizer.ocs.ibm.io":
        f:status:
          .:
          f:storageClusterStatus:
      Manager:         manager
      Operation:       Update
      Time:            2021-04-09T23:12:02Z
    Resource Version:  11372332
    Self Link:         /apis/ocs.ibm.io/v1/ocsclusters/ocscluster-vpc
    UID:               aa11a1a1-111f-aace-afac-1fa1afe1111a
    Spec:
      Billing Type:            hourly
      Mon Size:                20Gi
      Mon Storage Class Name:  ibmc-vpc-block-10iops-tier
      Num Of Osd:              1
      Ocs Upgrade:             false
      Osd Size:                100Gi
      Osd Storage Class Name:  ibmc-vpc-block-10iops-tier
    Status:
      Storage Cluster Status:  
    Events:                    <none>
    ```
    {: codeblock}



4. [Deploy an app that uses ODF](/docs/openshift?topic=openshift-odf-deploy-app).

### Scaling ODF
{: #odf-scaling}

You can scale your ODF configuration by increasing the `numOfOsd` setting. When you increase the number of OSDs, ODF provisions that number of disks of the same `osdSize` capacity in GB in each of the worker nodes in your ODF cluster. However, the total storage that is available to your applications is equal to the `osdSize` multiplied by the `numOfOsd`.
{: shortdesc}


| Number of worker nodes | Initial `osdSize` | `numOfOsd` | Storage capacity available to applications | Total storage of provisioned disks |
| --- | --- | --- | --- | --- |
| 3 | 150Gi | 1 | 150Gi | 450Gi |
| 3 | 150Gi | 2 | 300Gi | 900Gi |
| 3 | 150Gi | 3 | 450Gi | 1350Gi |
| 3 | 150Gi | 4 | 600Gi | 1800Gi |
{: caption="Table 1. OpenShift Data Foundation scaling." caption-side="bottom"}


### Scaling by increasing the `numOfOsd`
{: #odf-vpc-scaling-osd}

[Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Get the name of your `OcsCluster` custom resource.

    ```sh
    oc get ocscluster
    ```
    {: pre}

1. Save your `OcsCluster` custom resource YAML file to your local machine as `ocscluster.yaml`.

    ```sh
    oc get ocscluster ocscluster-vpc -o yaml
    ```
    {: pre}

1. Increase the `numOfOsd` parameter and reapply the `ocscluster` CRD to your cluster.

    ```sh
    oc apply -f ocscluster.yaml
    ```
    {: pre}

1. Verify that the additional OSDs are created.

    ```sh
    oc get pv
    ```
    {: pre}



### Expanding ODF by adding worker nodes to your VPC cluster
{: #odf-vpc-add-worker-nodes}

To increase the storage capacity in your storage cluster, add compatible worker nodes to your cluster.
{: shortdesc}

1. Expand the worker pool of the cluster that is used for OCS by [adding worker nodes](/docs/openshift?topic=openshift-add_workers). Ensure that your worker nodes meet the [requirements for ODF](/docs/openshift?topic=openshift-ocs-storage-prep). If you deployed ODF on all the worker nodes in your cluster, the ODF drivers are installed on the new worker nodes when they are added to your cluster.
2. If you deployed ODF on a subset of worker nodes in your cluster by specifying the private `<workerNodes>` parameters in your `OcsCluster` custom resource, you can add the node name of the new worker nodes to your ODF deployment by editing the custom resource definition.

    ```sh
    oc edit ocscluster ocscluster-vpc
    ```
    {: pre}

3. Save the `OcsCluster` custom resource file to reapply it to your cluster.


## Limitations
{: #ocs-limitations}

Review the following limitations for deploying ODF.

**Kubernetes resource ID character limit:** Kubernetes PVC names must be fewer than 63 characters. If you deploy ODF in a multizone VPC cluster and create your ODF storage cluster by using a metro `retain` storage class such as `ibmc-vpc-block-metro-retain-10iops-tier`, the corresponding ODF device set that is created by using this storage class fails. For more information see [ODF device set creation fails because of the Kubernetes character limitation](/docs/openshift?topic=openshift-ts-ocs-roks-debug).

## Storage class reference
{: #ocs-reference-section}

[ODF storage class reference](/docs/openshift?topic=openshift-ocs-sc-ref)



## Parameter reference
{: #odf-vpc-param-ref}

Refer to the following parameters when you use the add-on or operator in VPC clusters.
{: shortdesc}

### Version 4.12 clusters
{: #odf-vpc-params-412}

| Parameter | Description | Default value |
| --- | --- | --- |
| `name` | Note that Kubernetes resource names can't contain capital letters or special characters. Enter a name for your resource that uses only lowercase letters, numbers, `-` or `.` | N/A |
| `osdStorageClassName` | Enter `localblock`. | N/A |
| `osdSize` | Enter a size for your storage devices. Example: `100Gi`. The total storage capacity of your ODF cluster is equivalent to the `osdSize`  multiplied by the `numOfOsd`. | N/A |
| `osdDevicePaths` | Enter a comma separated list of the device paths for the devices that you want to use for the OSD devices. The devices that you specify are used as your application storage in your configuration. Each device must have at least `100GiB` of space and must be unformatted and unmounted. The parameter format is `/dev/disk/by-id/<device-id>`. Example device path value for a partitioned device: `/dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part2`. If you specify more than one device path, be sure there are no spaces between each path. For example: `/dev/disk/by-id/scsi-1111111a11a11a11111a1aa111a11a1a1-part2`,`/dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part2`. |
| `numOfOsd` | Enter the number object storage daemons (OSDs) that you want to create. ODF creates three times the specified number. For example, if you enter `1`, ODF creates 3 OSDs. | `1` |
| `billingType` | Enter a `billingType` of either `essentials` or `advanced` for your OCS deployment. | `advanced` |
| `ocsUpgrade` | Enter a `true` or `false` to upgrade the major version of your ODF deployment. | `false` |
| `workerNodes` | **Optional**: Enter the names of the worker nodes that you want to use for your ODF deployment. Don't specify this parameter if you want to use all the worker nodes in your cluster. To retrieve your worker node name, run the **`oc get nodes`** command. | N/A |
| `clusterEncryption` | Available for add-on version 4.7.0 and later. Enter `true` or `false` to enable encryption. |
| `autoDiscoverDevices` | **Optional**: Automatically discover the available disks on your worker nodes. Enter `true` or `false`. |
| `hpcsServiceName` | Enter the name of your {{site.data.keyword.hscrypto}} instance. For example: `Hyper-Protect-Crypto-Services-eugb`. | `false` |
| `hpcsInstanceId` | Enter your {{site.data.keyword.hscrypto}} instance ID. For example: `d11a1a43-aa0a-40a3-aaa9-5aaa63147aaa`. | `false` |
| `hpcsSecretName` | Enter the name of the secret that you created by using your {{site.data.keyword.hscrypto}} credentials. For example: `ibm-hpcs-secret`. | `false` |
| `hpcsBaseUrl` | Enter the public or private endpoint of your {{site.data.keyword.hscrypto}} instance. For example: `https://api.eu-gb.hs-crypto.cloud.ibm.com:8389`. | `false` |
| `hpcsTokenUrl` | Enter `https://iam.cloud.ibm.com/identity/token`. | `false` |
| `ignore-noobaa` | Enter `true` if you do not want to deploy MultiCloud Object Gateway. | `false` |
{: caption="VPC parameter reference" caption-side="bottom"}

### Version 4.10 and 4.11 clusters
{: #odf-vpc-params-410}

| Parameter | Description | Default value |
| --- | --- | --- |
| `osdStorageClassName` | Enter the name of the storage class that you want to use for your OSD devices. For **multizone clusters**, specify the metro storage class that you want to use. If you want to use a metro `retain` storage class, [create a custom `WaitForFirstConsumer` storage class](/docs/openshift?topic=openshift-vpc-block#vpc-customize-storage-class) that's based off the tiered metro `retain` storage class that you want to use. Metro storage classes have the volume binding mode `WaitForFirstConsumer`, which is required for multizone ODF deployments. For **single zone clusters**, enter the name of the tiered storage class that you want to use. Example: `ibmc-vpc-block-10iops-tier`. For more information about VPC tiered storage classes, see the [{{site.data.keyword.block_storage_is_short}} Storage class reference](/docs/openshift?topic=openshift-vpc-block#vpc-block-reference).| N/A |
| `osdSize` | Enter a size for your storage devices. Example: `100Gi`. The total storage capacity of your ODF cluster is equivalent to the `osdSize` multiplied by the `numOfOsd`. | N/A |
| `numOfOsd` | Enter the number object storage daemons (OSDs) that you want to create. ODF creates three times the `numOfOsd` value. For example, if you enter `1`, ODF provisions 3 disks of the size and storage class that you specify in the `osdStorageClassName` field. | `1` |
| `billingType` | Enter a `billingType` of either `essentials` or `advanced` for your ODF deployment. | `advanced` |
| `ocsUpgrade` | Enter `true` or `false` to upgrade the major version of your ODF deployment. | `false` |
| `workerNodes` | **Optional**: Enter the node names for the worker nodes that you want to use for your ODF deployment. Don't specify this parameter if you want to use all the worker nodes in your cluster. | N/A |
| `clusterEncryption` | Enter `true` or `false` to enable cluster wide encryption. |
| `hpcsServiceName` | Enter the name of your {{site.data.keyword.hscrypto}} instance. For example: `Hyper-Protect-Crypto-Services-eugb`. | `false` |
| `hpcsInstanceId` | Enter your {{site.data.keyword.hscrypto}} instance ID. For example: `d11a1a43-aa0a-40a3-aaa9-5aaa63147aaa`. | `false` |
| `hpcsSecretName` | Enter the name of the secret that you created by using your {{site.data.keyword.hscrypto}} credentials. For example: `ibm-hpcs-secret`. | `false` |
| `hpcsBaseUrl` | Enter the public or private endpoint of your {{site.data.keyword.hscrypto}} instance. For example: `https://api.eu-gb.hs-crypto.cloud.ibm.com:8389`. | `false` |
| `hpcsTokenUrl` | Enter `https://iam.cloud.ibm.com/identity/token`. | `false` |
{: caption="VPC parameter reference" caption-side="bottom"}


### Version 4.9 clusters
{: #odf-vpc-params-48}

| Parameter | Description | Default value |
| --- | --- | --- |
| `osdStorageClassName` | Enter the name of the storage class that you want to use for your OSD devices. For **multizone clusters**, specify the metro storage class that you want to use. If you want to use a metro `retain` storage class, [create a custom `WaitForFirstConsumer` storage class](/docs/openshift?topic=openshift-vpc-block#vpc-customize-storage-class) that's based off the tiered metro `retain` storage class that you want to use. Metro storage classes have the volume binding mode `WaitForFirstConsumer`, which is required for multizone ODF deployments. For **single zone clusters**, enter the name of the tiered storage class that you want to use. Example: `ibmc-vpc-block-10iops-tier`. For more information about VPC tiered storage classes, see the [{{site.data.keyword.block_storage_is_short}} Storage class reference](/docs/openshift?topic=openshift-vpc-block#vpc-block-reference).| N/A |
| `osdSize` | Enter a size for your storage devices. Example: `100Gi`. The total storage capacity of your ODF cluster is equivalent to the `osdSize` multiplied by the `numOfOsd`. | N/A |
| `numOfOsd` | Enter the number object storage daemons (OSDs) that you want to create. ODF creates three times the `numOfOsd` value. For example, if you enter `1`, ODF provisions 3 disks of the size and storage class that you specify in the `osdStorageClassName` field. | `1` |
| `billingType` | Enter a `billingType` of either `essentials` or `advanced` for your ODF deployment. | `advanced` |
| `ocsUpgrade` | Enter `true` or `false` to upgrade the major version of your ODF deployment. | `false` |
| `workerNodes` | **Optional**: Enter the node names for the worker nodes that you want to use for your ODF deployment. Don't specify this parameter if you want to use all the worker nodes in your cluster. | N/A |
| `clusterEncryption` | Enter `true` or `false` to enable cluster wide encryption. |
{: caption="ODF parameter reference" caption-side="bottom"}








