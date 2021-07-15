---

copyright:
  years: 2014, 2021
lastupdated: "2021-07-15"

keywords: openshift, openshift data foundation, openshift container storage, ocs, roks

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
{:terraform: .ph data-hd-interface='terraform'}
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
  

# Deploying OpenShift Data Foundation on VPC clusters
{: #deploy-odf-vpc}

OpenShift Data Foundation is a highly available storage solution that you can use to manage persistent storage for your containerized workloads in {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

The OpenShift Data Foundation add-on is available as a technology preview and might change without prior notice. Don't use this add-on for production workloads.
{: preview}

**Supported infrastructure provider**:
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

**Minimum required permissions**: **Administrator** platform access role and the **Manager** service access role for the cluster in {{site.data.keyword.containerlong_notm}}.

## Quick start for VPC clusters
{: #odf-quickstart}
You can deploy ODF on VPC clusters with the default configuration settings by running the `addon enable` command and specifying the `"ocsDeploy=true"` flag. Before enabling the add-on make sure that you have a [VPC cluster](/docs/openshift?topic=openshift-clusters) with at least three worker nodes. For high availability, create a cluster with at least one worker node per zone across three zones. Each worker node must have a minimum of 16 CPUs and 64 GB RAM.
{: shortdesc}

If you want to override the default parameters when deploying the add-on, you can use the `--param "key=value"` format. For more information, see [Deploying ODF](#odf-custom-install).
{: tip}
  
1. Enable the ODF and specify the `ocsDeploy=True` parameter to deploy ODF with the default configuration parameters. To see the default parameters, run `ibmcloud oc cluster addon options --addon openshift-container-storage`. To list the versions and find the current default, run `ibmcloud oc cluster addon versions`. If you have a cluster version other than the default, specify the `--version` flag. The add-on supports `n+1` cluster versions. 
  ```sh
  ibmcloud oc cluster addon enable openshift-container-storage -c <cluster_name> --version <version> --param "ocsDeploy=true"
  ```
  {: pre}

**Next steps**: [Deploy an app that uses ODF](/docs/openshift?topic=openshift-ocs-deploy-app)

<br />

## Creating a VPC cluster for OpenShift Data Foundation
{: #ocs-storage-prep}

Review the following steps to deploy ODF on your VPC cluster.
{: shortdesc}

1. [Install the `oc` CLI](/docs/openshift?topic=openshift-openshift-cli#cli_oc).
1. Create a [VPC cluster](/docs/openshift?topic=openshift-clusters) with at least three worker nodes. For high availability, create a cluster with at least one worker node per zone across three zones. Each worker node must have a minimum of 16 CPUs and 64 GB RAM.
1. **Optional** [Set up a {{site.data.keyword.cos_full_notm}} service instance](#odf-create-cos) as your default backing store. If you don't want to use {{site.data.keyword.cos_full_notm}} or if you want to configure backing stores later, see [Installing the add-on from the CLI](#install-odf-cli).


### Optional: Setting up an {{site.data.keyword.cos_full_notm}} service instance
{: #odf-create-cos}

If you want to set up {{site.data.keyword.cos_full_notm}} as the default backing store in your storage cluster, create an instance of {{site.data.keyword.cos_full_notm}}. Then, create a set of HMAC credentials and a Kubernetes secret that uses your {{site.data.keyword.cos_short}} HMAC credentials. If you don't specify {{site.data.keyword.cos_full_notm}} credentials during installation, then the default backing store in your storage cluster is created by using the PVs in your cluster. You can set up additional backing stores after deploying ODF, but you cannot change the default backing store.
{: shortdesc}

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

## Installing the add-on from the CLI
{: #install-odf-cli-vpc}

You can install the add-on by using the [`ibmcloud oc cluster addon enable` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable).
{: shortdesc}

1. Review the [VPC parameter reference](#odf-vpc-param-ref). When you enable the add-on, you can override the default values by specifying the `--param "key=value"` flag for each parameter that you want to override.
1. Before you enable the add-on, review the [changelog](/docs/openshift?topic=openshift-odf_addon_changelog) for the latest version information. Note that the add-on supports `n+1` cluster versions. For example, you can deploy version 4.7.0 of the add-on to an OCP 4.7 or 4.8 cluster. If you have a cluster version other than the default, you must specify the `--version` flag when you enable the add-on.
1. Review the add-on options.
  ```sh
  ibmcloud oc cluster addon options --addon openshift-container-storage
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
  ```
  {: screen}

1. Enable the `openshift-container-storage` add-on. If you also want to deploy ODF and create your storage cluster from the CLI, you can specify the `"ocsDeploy=true"` flag. If you want to override any of the default parameters, specify the `--param "key=value"` flag for each parameter you want to override. If you don't want to create your storage cluster when you enable the add-on, you can enable the add-on first, then create your storage cluster later by creating a CRD.

  ```sh
  ibmcloud oc cluster addon enable openshift-container-storage -c <cluster_name> --version <version> --param "ocsDeploy=true"
  ```
  {: pre}

  **Example command for overriding the `osdSize` parameter**:
  ```sh
  ibmcloud oc cluster addon enable openshift-container-storage -c <cluster_name> --version <version> --param "ocsDeploy=true" --param "osdSize=500Gi"
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

## Installing the OpenShift Data Foundation add-on from the console
{: #install-odf-console-vpc}

To install ODF in your cluster, complete the following steps.
{: shortdesc}

1. Before you enable the add-on, review the [changelog](/docs/openshift?topic=openshift-odf_addon_changelog) for the latest version information. Note that the add-on supports `n+1` cluster versions. For example, you can deploy version 4.7.0 of the add-on to an OCP 4.7 or 4.8 cluster. If you have a cluster version other than the default, you must install the add-on from the CLI and specify the `--version` flag.
1. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster for which you want to install the add-on.
2. On the cluster **Overview** page, click **Add-ons**.
3. On the OpenShift Data Foundation card, click **Install**.

## Creating your ODF storage cluster
{: #ocs-vpc-deploy-crd}

To create an ODF storage cluster in your VPC cluster or your {{site.data.keyword.satelliteshort}} cluster by using dynamic provisioning for your storage volumes, you can create a custom resource that is used to specify storage device details.
{: shortdesc}

If you want to use an {{site.data.keyword.cos_full_notm}} service instance as your default backing store, make sure that you [created the service instance](#odf-create-cos), and created the Kubernetes secret in your cluster. When you create the ODF CRD in your cluster, ODF looks for a secret named `ibm-cloud-cos-creds` to set up the default backing store that uses your {{site.data.keyword.cos_short}} HMAC credentials.
{: note}

1. Create a custom resource definition (CRD) called `OcsCluster`. Save one of the following custom resource definition files on your local machine and edit it to include the name of the custom storage class that you created earlier as the `monStorageClassName` and `osdStorageClassName` parameters. For more information about the `OcsCluster` parameters, see the [parameter reference](#ocs-vpc-param-ref).

  **Example custom resource definition (CRD) for installing ODF on all worker nodes in a {{site.data.keyword.satelliteshort}} cluster**
  ```yaml
  apiVersion: ocs.ibm.io/v1
  kind: OcsCluster
  metadata:
    name: ocscluster-vpc
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

  **Example custom resource definition (CRD) for installing ODF only on specified worker nodes in a {{site.data.keyword.satelliteshort}} cluster**
  ```yaml
  apiVersion: ocs.ibm.io/v1
  kind: OcsCluster
  metadata:
    name: ocscluster-sat
  spec:
    monStorageClassName: <monStorageClassName> # For multizone clusters, specify a storage class with a waitForFirstConsumer volume binding mode
    monSize: <monSize>
    osdStorageClassName: <osdStorageClassName> # For multizone clusters, specify a storage class with a waitForFirstConsumer volume binding mode
    osdSize: <osdSize> # The OSD size is the total storage capacity of your OCS storage cluster
    numOfOsd: 1
    billingType: advanced
    ocsUpgrade: false
    workerNodes: # Specify the private IP addresses of the worker nodes where you want to install OCS.
      - <worker-IP> # To get a list worker nodes, run `oc get nodes`.
      - <worker-IP>
      - <worker-IP>
  ```
  {: codeblock}

3. Save the file and create the `OcsCluster` custom resource to your cluster.
  ```sh
  oc create -f <ocs-cluster-filename>.yaml
  ```
  {: pre}

4. Verify that your `OcsCluster` is running.
  ```sh
  oc describe ocscluster ocscluster-vpc
  ```
  {: pre}

  **Example output**
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
<br />

**Next steps**: [Deploy an app that uses ODF](/docs/openshift?topic=openshift-ocs-deploy-app)

## Expanding ODF in VPC clusters
{: odf-vpc-expand-storage-cluster}

To expand your storage cluster, you can [add worker nodes](#ocs-vpc-add-worker-nodes) to your cluster, or you can scale by [increasing the `numOfOsd`](#ocs-vpc-scaling-osd).
{: shortdesc}

### Scaling by increasing the `numOfOsd` in your CRD
{: #odf-vpc-scaling-osd}

You can scale your ODF configuration by increasing the `numOfOsd` setting. When you increase the number of OSDs, ODF provisions that number of disks of the same `osdSize` capacity in GB in each of the worker nodes in your ODF cluster. However, the total storage that is available to your applications is equal to the number of worker nodes that are multiplied by the `osdSize` multiplied by the `numOfOsd`, and then divided by the replication factor, which is a constant of 3.
{: shortdesc}

For example, if your ODF cluster has three worker nodes, you specify an `osdSize` of `150Gi`, and you set the `numOfOsd` to 4, then your storage totals are as follows.
  * **Total storage that is available for application use**: `osdSize` multiplied by `numOfOsd` and the number of worker nodes in the cluster, and divided by the replication factor of 3, or `(3 x 150Gi x 4) / 3 = 600Gi`.
  * **Total storage that is provisioned as disks in the cluster**: `osdSize` multiplied by `numOfOsd` and the number of worker nodes in the cluster, or `150Gi x 4 x 3 = 1800Gi`.


| Number of worker nodes | Initial `osdSize` | `numOfOsd` per worker node | Storage capacity available to applications | Total storage of provisioned disks |
| --- | --- | --- | --- | --- |
| 3 | 150Gi | 1 | 150Gi | 450Gi |
| 3 | 150Gi | 2 | 300Gi | 900Gi |
| 3 | 150Gi | 3 | 450Gi | 1350Gi |
| 3 | 150Gi | 4 | 600Gi | 1800Gi |
| 6 | 150Gi | 1 | 300Gi | 900Gi |
| 6 | 150Gi | 2 | 600Gi | 1800Gi |
| 6 | 150Gi | 3 | 900Gi | 2700Gi |
| 6 | 150Gi | 4 | 1200Gi | 3600Gi |
{: caption="Table 1. OpenShift Data Foundation scaling." caption-side="top"}
{: summary="The rows are read from left to right. The first column is the number of worker nodes. The second column is the initial OSD size. The third column is the number of OSDs. The fourth column is the total storage capacity that is available to applications in the cluster. The fifth column is the total storage capacity of the provisioned disks."}

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

<br />

### Expanding ODF by adding worker nodes to your VPC cluster
{: #odf-vpc-add-worker-nodes}

To increase the storage capacity in your storage cluster, add compatible worker nodes to your cluster.
{: shortdesc}

1. Expand the worker pool of the cluster that is used for OCS by [adding worker nodes](/docs/openshift?topic=openshift-add_workers). Ensure that your worker nodes meet the [requirements for ODF](/docs/openshift?topic=openshift-ocs-storage-prep#ocs-classic-plan). If you deployed ODF on all of the worker nodes in your cluster, the ODF drivers are installed on the new worker nodes when they are added to your cluster.
2. If you deployed ODF on a subset of worker nodes in your cluster by specifying the private `<worker-IP>` parameters in your `OcsCluster` custom resource, you can add the IP addresses of the new worker nodes to your ODF deployment by editing the custom resource definition.
  ```sh
  oc edit ocscluster ocscluster-vpc
  ```
  {: pre}
3. Save the `OcsCluster` custom resource file to reapply it to your cluster.

<br />

## Limitations
{: #ocs-limitations}

Review the following limitations for deploying ODF.

**Kubernetes resource ID character limit:** Kubernetes PVC names must be fewer than 63 characters. If you deploy ODF in a multizone VPC cluster and create your ODF storage cluster by using a metro `retain` storage class such as `ibmc-vpc-block-metro-retain-10iops-tier`, the corresponding ODF device set that is created by using this storage class fails. For more information see [ODF device set creation fails because of the Kubernetes character limitation](/docs/openshift?topic=openshift-ts-ocs-roks-debug).

## Storage class reference
{: #ocs-reference-section}

[ODF storage class reference](/docs/openshift?topic=openshift-ocs-sc-ref)

<br />

## VPC: OpenShift Data Foundation parameter reference
{: #ocs-vpc-param-ref}

Refer to the following parameters when you use the add-on or operator in VPC clusters.
{: shortdesc}


| Parameter | Description | Default value |
| --- | --- | --- |
| `monStorageClassName` | Enter the name of the storage class that you want to use for your MON devices. For VPC clusters you must specify the `ibm-vpc-block` storage class that you want to use to provision storage for Monitor pods. For **multizone clusters**, specify the metro storage class that you want to use. If you want to use a metro `retain` storage class, [create a custom `WaitForFirstConsumer` storage class](/docs/openshift?topic=openshift-vpc-block#vpc-customize-storage-class) that's based off the tiered metro `retain` storage class that you want to use. Metro storage classes have the volume binding mode `WaitForFirstConsumer`, which is required for multizone ODF deployments. For **single zone clusters**, enter the name of the tiered storage class that you want to use. Example: `ibmc-vpc-block-10iops-tier`. For more information about VPC tiered storage classes, see the [{{site.data.keyword.block_storage_is_short}} Storage class reference](/docs/openshift?topic=openshift-vpc-block#vpc-block-reference).| N/A |
| `monSize` | Enter a size for the storage devices that you want to provision for the monitor pods. The devices that you provision must be at least 20Gi each.  Example: `20Gi` | N/A |
| `osdStorageClassName` | Enter the name of the storage class that you want to use for your OSD devices. For **multizone clusters**, specify the metro storage class that you want to use. If you want to use a metro `retain` storage class, [create a custom `WaitForFirstConsumer` storage class](/docs/openshift?topic=openshift-vpc-block#vpc-customize-storage-class) that's based off the tiered metro `retain` storage class that you want to use. Metro storage classes have the volume binding mode `WaitForFirstConsumer`, which is required for multizone ODF deployments. For **single zone clusters**, enter the name of the tiered storage class that you want to use. Example: `ibmc-vpc-block-10iops-tier`. For more information about VPC tiered storage classes, see the [{{site.data.keyword.block_storage_is_short}} Storage class reference](/docs/openshift?topic=openshift-vpc-block#vpc-block-reference).| N/A |
| `osdSize` | Enter a size for your storage devices. Example: `100Gi`. The total storage capacity of your ODF cluster is equivalent to the `osdSize` x 3 divided by the `numOfOsd`. | N/A |
| `numOfOsd` | Enter the number object storage daemons (OSDs) that you want to create. ODF creates three times the `numOfOsd` value. For example, if you enter `1`, ODF provisions 3 disks of the size and storage class that you specify in the `osdStorageClassName` field. | `1` |
| `billingType` | Enter a `billingType` of either `essentials` or `advanced` for your ODF deployment. | `advanced` |
| `ocsUpgrade` | Enter `true` or `false` to upgrade the major version of your ODF deployment. | `false` |
| `worker-IP` | **Optional**: Enter the private IP addresses for the worker nodes that you want to use for your ODF deployment. Don't specify this parameter if you want to use all of the worker nodes in your cluster. | N/A |
{: caption="ODF parameter reference" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the parameter. The second column is a brief description of the parameter. The third column is the default value of the parameter."}

<br />

