---

copyright:
  years: 2014, 2022
lastupdated: "2022-02-18"

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

**Minimum required permissions**: **Administrator** platform access role and the **Manager** service access role for the cluster in {{site.data.keyword.containerlong_notm}}.

## Quick start for VPC clusters
{: #odf-quickstart}

The following steps walk you through deploying ODF with the default settings. Before enabling the add-on make sure that you have a [VPC cluster](/docs/openshift?topic=openshift-clusters) with at least three worker nodes. For high availability, create a cluster with at least one worker node per zone across three zones. Each worker node must have a minimum of 16 CPUs and 64 GB RAM.
{: shortdesc}

To list the versions and find the current default, run `ibmcloud oc cluster addon versions`. If you have a cluster version other than the default, specify the `--version` flag. The add-on supports `n+1` cluster versions. Enable the add-on by running the following command.

```sh
ibmcloud oc cluster addon enable openshift-data-foundation -c <cluster_name> --version 4.7.0
```
{: pre}

**Next steps**: [Deploy an app that uses ODF](/docs/openshift?topic=openshift-odf-deploy-app)

If you want to override the default parameters when deploying the add-on, you can use the `--param "key=value"` format. For more information, see [Installing the add-on from the CLI](#install-odf-cli-vpc).
{: tip}

## Creating a VPC cluster for OpenShift Data Foundation
{: #ocs-storage-vpc}

Review the following steps to deploy ODF on your VPC cluster.
{: shortdesc}

For high availability, make sure that your VPC cluster has at least 3 worker nodes, with one worker node per zone.
{: important}


1. [Install](/docs/openshift?topic=openshift-openshift-cli#cli_oc) or [update the `oc` CLI](/docs/openshift?topic=openshift-openshift-cli#cs_cli_upgrade).
1. Create a [VPC cluster](/docs/openshift?topic=openshift-clusters) with at least 3 worker nodes. For high availability, create a cluster with at least one worker node per zone across three zones. Each worker node must have a minimum of 16 CPUs and 64 GB RAM.
1. **Optional** [Set up an {{site.data.keyword.cos_full_notm}} service instance](#odf-create-cos) as your default backing store. You can skip this step if you don't want to use {{site.data.keyword.cos_full_notm}}. You can also set up backing stores later. 

### Optional: Setting up an {{site.data.keyword.cos_full_notm}} service instance
{: #odf-create-cos}

Complete the following steps to create an {{site.data.keyword.cos_full_notm}} instance which you can use as the default backing store in your ODF deployment. If you don't want to set up {{site.data.keyword.cos_full_notm}}, you can skip this step and [install the add-on](#install-odf-cli-vpc).
{: shortdesc}

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

## Installing the OpenShift Data Foundation add-on from the console
{: #install-odf-console-vpc}

To install ODF in your cluster, complete the following steps.
{: shortdesc}

1. Before you enable the add-on, review the [changelog](/docs/openshift?topic=openshift-odf_addon_changelog) for the latest version information. Note that the add-on supports `n+1` cluster versions. For example, you can deploy version 4.7.0 of the add-on to an OCP 4.7 or 4.8 cluster. If you have a cluster version other than the default, you must install the add-on from the CLI and specify the `--version` flag.
1. [Review the parameter reference](#odf-vpc-param-ref).
1. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster where you want to install the add-on.
1. On the cluster **Overview** page, on the OpenShift Data Foundation card, click **Install**. The **Install ODF** panel opens.
1. In the **Install ODF** panel, enter the configuration parameters that you want to use for your ODF deployment.
    - `odfDeploy`: Enter `true` to enable the add-on and deploy the ODF resources to your cluster. Enter `false` to only enable the add-on. If you enter `false`, you must create a [CRD to deploy ODF](#ocs-vpc-deploy-crd) later.
    - `monSize`: Enter the size of the {{site.data.keyword.block_storage_is_short}} devices that you want to provision for the ODF [monitor pods](/docs/openshift?topic=openshift-ocs-storage-prep). The default setting `20Gi`.
    - `monStorageClassName`: Enter the {{site.data.keyword.block_storage_is_short}} [storage class](/docs/openshift?topic=openshift-vpc-block#vpc-block-reference) that you want to use to dynamically provision storage for the [monitor pods](/docs/openshift?topic=openshift-ocs-storage-prep). The default storage class is `ibmc-vpc-block-metro-10iops-tier`.
    - `monDevicePaths`: `invalid` for VPC clusters. Leave this parameter as-is.
    - `osdSize`: Enter the size of the {{site.data.keyword.block_storage_is_short}} devices that you want to provision for the [OSD pods](/docs/openshift?topic=openshift-ocs-storage-prep). The default size is `250Gi`.
     `osdStorageClassName`: Enter the {{site.data.keyword.block_storage_is_short}} [storage class](/docs/openshift?topic=openshift-vpc-block#vpc-block-reference) that you want to use to dynamically provision storage for the [OSD pods](/docs/openshift?topic=openshift-ocs-storage-prep). The default storage class is `ibmc-vpc-block-metro-10iops-tier`.
    - `osdDevicePaths`: `invalid` for VPC clusters. Leave this parameter as-is.
    - `numOfOsd`: Enter the number of block storage device sets that you want to provision for ODF. A `numOfOsd` value of 1 provisions 1 device set which includes 3 block storage devices. The devices are provisioned evenly across your worker nodes. For more information, see [Understanding ODF](/docs/openshift?topic=openshift-ocs-storage-prep).
    - `workerNodes`: Enter the worker nodes where you want to deploy ODF. You must have at least 3 worker nodes. The default setting is `all`. If you want to deploy ODF only on certain nodes, enter the IP addresses of the worker nodes in a comma-separated list without spaces, for example: `XX.XXX.X.X,XX.XXX.X.X,XX.XXX.X.X`.
    - `ocsUpgrade`: Enter `true` or `false` to upgrade the ODF operators. For initial deployment, leave this setting as `false`. The default setting is `false`.
    - `clusterEncryption`: Enter `true` or `false` to enable cluster encryption. The default setting is `false`.

1. After you enter the parameters that you want to use, click **Install**

1. Wait a few minutes for the add-on deployment to complete. When the deployment is complete, the add-on status is `Normal - Addon Ready`.

1. Verify your installation. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Run the following command to verify the ODF pods are running.

    ```sh
    oc get pods -n openshift-storage
    ```
    {: pre}

Example output

```sh
NAME                                                              READY   STATUS      RESTARTS   AGE
csi-cephfsplugin-bl4rx                                            3/3     Running     0          172m
csi-cephfsplugin-lsd8z                                            3/3     Running     0          172m
csi-cephfsplugin-provisioner-5b9b669659-5ktts                     6/6     Running     0          172m
csi-cephfsplugin-provisioner-5b9b669659-65zbk                     6/6     Running     0          172m
csi-cephfsplugin-xlkc2                                            3/3     Running     0          172m
csi-rbdplugin-c7tbj                                               3/3     Running     0          172m
csi-rbdplugin-fj7q7                                               3/3     Running     0          172m
csi-rbdplugin-provisioner-6f87685d6b-fxrpk                        6/6     Running     0          172m
csi-rbdplugin-provisioner-6f87685d6b-vb47x                        6/6     Running     0          172m
csi-rbdplugin-tc8hp                                               3/3     Running     0          172m
noobaa-core-0                                                     1/1     Running     0          163m
noobaa-db-pg-0                                                    1/1     Running     0          163m
noobaa-default-backing-store-noobaa-pod-c83e2ade                  1/1     Running     0          161m
noobaa-endpoint-5b97994bf7-fxknh                                  1/1     Running     0          161m
noobaa-operator-556b5db575-f9zbf                                  1/1     Running     0          172m
ocs-metrics-exporter-574784d58b-4mbgr                             1/1     Running     0          172m
ocs-operator-789c6d7f95-l7682                                     1/1     Running     0          173m
rook-ceph-crashcollector-10.241.0.6-676f9548b7-k44tk              1/1     Running     0          170m
rook-ceph-crashcollector-10.241.128.5-55565c8679-hf8h4            1/1     Running     0          167m
rook-ceph-crashcollector-10.241.64.9-767bc5776d-42njb             1/1     Running     0          169m
rook-ceph-mds-ocs-storagecluster-cephfilesystem-a-85dc5665rfdrh   2/2     Running     0          162m
rook-ceph-mds-ocs-storagecluster-cephfilesystem-b-68c779dcfknbp   2/2     Running     0          162m
rook-ceph-mgr-a-bc7f4cb94-tzrxx                                   2/2     Running     0          165m
rook-ceph-mon-a-6f47c4dd55-7mzbp                                  2/2     Running     0          170m
rook-ceph-mon-b-cdf99bf6f-b2pg9                                   2/2     Running     0          169m
rook-ceph-mon-c-59994fdd9f-b6t5c                                  2/2     Running     0          167m
rook-ceph-operator-bdf98d48b-b5rm6                                1/1     Running     0          173m
rook-ceph-osd-0-7659d76ff7-fnftm                                  2/2     Running     0          163m
rook-ceph-osd-1-b4c7c9487-kngtr                                   2/2     Running     0          163m
rook-ceph-osd-2-6c79647d6c-b5kng                                  2/2     Running     0          163m
rook-ceph-osd-prepare-ocs-deviceset-0-data-0tjmb9-r5mkj           0/1     Completed   0          165m
rook-ceph-osd-prepare-ocs-deviceset-1-data-0kphrw-jgx86           0/1     Completed   0          165m
rook-ceph-osd-prepare-ocs-deviceset-2-data-05d74g-6gvpn           0/1     Completed   0          165m
rook-ceph-rgw-ocs-storagecluster-cephobjectstore-a-784c848c8qrp   2/2     Running     0          162m
```
{: screen}

**Next steps**: [Deploy an app that uses ODF](/docs/openshift?topic=openshift-odf-deploy-app).
    

## Installing the add-on from the CLI
{: #install-odf-cli-vpc}

You can install the add-on by using the [`ibmcloud oc cluster addon enable` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable).
{: shortdesc}

1. Review the [VPC parameter reference](#odf-vpc-param-ref). When you enable the add-on, you can override the default values by specifying the `--param "key=value"` flag for each parameter that you want to override.

1. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Before you enable the add-on, review the [changelog](/docs/openshift?topic=openshift-odf_addon_changelog) for the latest version information. Note that the add-on supports `n+1` cluster versions. For example, you can deploy version `4.7.0` of the add-on to an OCP 4.7 or 4.8 cluster. If you have a cluster version other than the default, you must specify the `--version` flag when you enable the add-on.

1. Review the add-on options. Note that add-on options are only available for version `4.7.0` and later.

    ```sh
    ibmcloud oc cluster addon options --addon openshift-data-foundation --version 4.7.0
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

1. Enable the `openshift-data-foundation` add-on. If you want to override any of the default parameters, specify the `--param "key=value"` flag for each parameter you want to override. If you don't want to create your storage cluster when you enable the add-on, you can enable the add-on first, then create your storage cluster later by creating a CRD.

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
    ibmcloud oc cluster addon ls -c <cluster_name>
    ```
    {: pre}

1. Verify that the `ibm-ocs-operator-controller-manager-*****` pod is running in the `kube-system` namespace.

    ```sh
    oc get pods -A | grep ibm-ocs-operator-controller-manager
    ```
    {: pre}

1. If you enabled the add-on and didn't create a storage cluster, follow the steps to [create an ODF custom resource](#ocs-vpc-deploy-crd).

## Creating your ODF custom resource
{: #ocs-vpc-deploy-crd}

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

    Example custom resource definition for installing ODF on all worker nodes on a 4.7 cluster.

    ```yaml
    apiVersion: ocs.ibm.io/v1
    kind: OcsCluster
    metadata:
      name: ocscluster-vpc # Kubernetes resource names can't contain capital letters or special characters. Enter a name for your resource that uses only lowercase letters, numbers, `-` or `.`
    spec:
      monStorageClassName: <monStorageClassName> # For multizone clusters, specify a storage class with a waitForFirstConsumer volume binding mode
      monSize: <monSize>
      osdStorageClassName: <osdStorageClassName> # For multizone clusters, specify a storage class with a waitForFirstConsumer volume binding mode
      osdSize: <osdSize> # The OSD size is the total storage capacity of your OCS storage cluster
      numOfOsd: 1
      billingType: advanced
      ocsUpgrade: false
    ```
    {: codeblock}

    Example custom resource definition for installing ODF only on specified worker nodes on a 4.7 cluster.

    ```yaml
    apiVersion: ocs.ibm.io/v1
    kind: OcsCluster
    metadata:
      name: ocscluster-vpc # Kubernetes resource names can't contain capital letters or special characters. Enter a name for your resource that uses only lowercase letters, numbers, `-` or `.`
    spec:
      monStorageClassName: <monStorageClassName> # For multizone clusters, specify a storage class with a waitForFirstConsumer volume binding mode
      monSize: <monSize>
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
{: caption="Table 1. OpenShift Data Foundation scaling." caption-side="top"}
{: summary="The rows are read from left to right. The first column is the number of worker nodes. The second column is the initial OSD size. The third column is the number of OSDs. The fourth column is the total storage capacity that is available to applications in the cluster. The fifth column is the total storage capacity of the provisioned disks."}

### Scaling by increasing the `numOfOsd`
{: #odf-vpc-scaling-osd}

[Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

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
2. If you deployed ODF on a subset of worker nodes in your cluster by specifying the private `<workerNodes>` parameters in your `OcsCluster` custom resource, you can add the IP addresses of the new worker nodes to your ODF deployment by editing the custom resource definition.

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

### Version 4.8 clusters
{: #odf-vpc-params-48}

| Parameter | Description | Default value |
| --- | --- | --- |
| `name` | Note that Kubernetes resource names can't contain capital letters or special characters. Enter a name for your resource that uses only lowercase letters, numbers, `-` or `.` | N/A |
| `osdStorageClassName` | Enter the name of the storage class that you want to use for your OSD devices. For **multizone clusters**, specify the metro storage class that you want to use. If you want to use a metro `retain` storage class, [create a custom `WaitForFirstConsumer` storage class](/docs/openshift?topic=openshift-vpc-block#vpc-customize-storage-class) that's based off the tiered metro `retain` storage class that you want to use. Metro storage classes have the volume binding mode `WaitForFirstConsumer`, which is required for multizone ODF deployments. For **single zone clusters**, enter the name of the tiered storage class that you want to use. Example: `ibmc-vpc-block-10iops-tier`. For more information about VPC tiered storage classes, see the [{{site.data.keyword.block_storage_is_short}} Storage class reference](/docs/openshift?topic=openshift-vpc-block#vpc-block-reference).| N/A |
| `osdSize` | Enter a size for your storage devices. Example: `100Gi`. The total storage capacity of your ODF cluster is equivalent to the `osdSize` x 3 divided by the `numOfOsd`. | N/A |
| `numOfOsd` | Enter the number object storage daemons (OSDs) that you want to create. ODF creates three times the `numOfOsd` value. For example, if you enter `1`, ODF provisions 3 disks of the size and storage class that you specify in the `osdStorageClassName` field. | `1` |
| `billingType` | Enter a `billingType` of either `essentials` or `advanced` for your ODF deployment. | `advanced` |
| `ocsUpgrade` | Enter `true` or `false` to upgrade the major version of your ODF deployment. | `false` |
| `workerNodes` | **Optional**: Enter the private IP addresses for the worker nodes that you want to use for your ODF deployment. Don't specify this parameter if you want to use all the worker nodes in your cluster. | N/A |
| `clusterEncryption` | Enter `true` or `false` to enable encryption. |
{: caption="ODF parameter reference" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the parameter. The second column is a brief description of the parameter. The third column is the default value of the parameter."}


### Version 4.7 clusters
{: #odf-vpc-params-47}

| Parameter | Description | Default value |
| --- | --- | --- |
| `name` | Note that Kubernetes resource names can't contain capital letters or special characters. Enter a name for your resource that uses only lowercase letters, numbers, `-` or `.` | N/A |
| `monStorageClassName` | Enter the name of the storage class that you want to use for your MON devices. For VPC clusters you must specify the `ibm-vpc-block` storage class that you want to use to provision storage for Monitor pods. For **multizone clusters**, specify the metro storage class that you want to use. If you want to use a metro `retain` storage class, [create a custom `WaitForFirstConsumer` storage class](/docs/openshift?topic=openshift-vpc-block#vpc-customize-storage-class) that's based off the tiered metro `retain` storage class that you want to use. Metro storage classes have the volume binding mode `WaitForFirstConsumer`, which is required for multizone ODF deployments. For **single zone clusters**, enter the name of the tiered storage class that you want to use. Example: `ibmc-vpc-block-10iops-tier`. For more information about VPC tiered storage classes, see the [{{site.data.keyword.block_storage_is_short}} Storage class reference](/docs/openshift?topic=openshift-vpc-block#vpc-block-reference).| N/A |
| `monSize` | Enter a size for the storage devices that you want to provision for the monitor pods. The devices that you provision must be at least 20Gi each. Example: `20Gi` | N/A |
| `osdStorageClassName` | Enter the name of the storage class that you want to use for your OSD devices. For **multizone clusters**, specify the metro storage class that you want to use. If you want to use a metro `retain` storage class, [create a custom `WaitForFirstConsumer` storage class](/docs/openshift?topic=openshift-vpc-block#vpc-customize-storage-class) that's based off the tiered metro `retain` storage class that you want to use. Metro storage classes have the volume binding mode `WaitForFirstConsumer`, which is required for multizone ODF deployments. For **single zone clusters**, enter the name of the tiered storage class that you want to use. Example: `ibmc-vpc-block-10iops-tier`. For more information about VPC tiered storage classes, see the [{{site.data.keyword.block_storage_is_short}} Storage class reference](/docs/openshift?topic=openshift-vpc-block#vpc-block-reference).| N/A |
| `osdSize` | Enter a size for your storage devices. Example: `100Gi`. The total storage capacity of your ODF cluster is equivalent to the `osdSize` x 3 divided by the `numOfOsd`. | N/A |
| `numOfOsd` | Enter the number object storage daemons (OSDs) that you want to create. ODF creates three times the `numOfOsd` value. For example, if you enter `1`, ODF provisions 3 disks of the size and storage class that you specify in the `osdStorageClassName` field. | `1` |
| `billingType` | Enter a `billingType` of either `essentials` or `advanced` for your ODF deployment. | `advanced` |
| `ocsUpgrade` | Enter `true` or `false` to upgrade the major version of your ODF deployment. | `false` |
| `workerNodes` | **Optional**: Enter the private IP addresses for the worker nodes that you want to use for your ODF deployment. Don't specify this parameter if you want to use all the worker nodes in your cluster. | N/A |
| `clusterEncryption` | Enter `true` or `false` to enable encryption. |
{: caption="ODF parameter reference" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the parameter. The second column is a brief description of the parameter. The third column is the default value of the parameter."}









