---

copyright:
  years: 2014, 2021
lastupdated: "2021-06-07"

keywords: openshift, openshift container storage, ocs, vpc, roks

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
  
 


# Setting up your storage cluster
{: #ocs-storage-cluster-setup}

After you [prepare your cluster for OCS](/docs/openshift?topic=openshift-ocs-storage-prep) and [install OCS in your cluster](/docs/openshift?topic=openshift-ocs-storage-install), you must configure a storage cluster.

* If you installed OCS by using the managed cluster add-on, you must create a CRD for your storage cluster. In your CRD, you specify the details of the storage cluster that you create.

  * [VPC: Creating your OCS storage cluster by using a CRD](#ocs-vpc-deploy-crd).
  * [Classic: Creating your OCS storage cluster by using a CRD](#ocs-classic-deploy-crd).

* If you installed OCS by using OperatorHub, you must create your storage cluster by using the {{site.data.keyword.openshiftshort}} web console.

  * [VPC: Creating a storage cluster in the web console](#ocs-vpc-deploy-console).
  * [Classic: Creating a storage cluster in the web console](#ocs-classic-deploy-console).

## Add-on for VPC clusters: Creating your OCS storage cluster CRD
{: #ocs-vpc-deploy-crd}

To create an OCS storage cluster in your VPC cluster, you can create a custom resource that is used to specify storage device details.
{: shortdesc}

If you want to use an {{site.data.keyword.cos_full_notm}} service instance as your default backing store, make sure that you [created the service instance](/docs/openshift?topic=openshift-ocs-storage-install#ocs-create-cos), and created the Kubernetes secret in your cluster. When you create the OCS CRD in your cluster, OCS looks for a secret named `ibm-cloud-cos-creds` to set up the default backing store that uses your {{site.data.keyword.cos_short}} HMAC credentials.
{: note}

1. Create a custom resource called `OcsCluster`. Save one of the following custom resource definition files on your local machine and edit it to include the name of the custom storage class that you created earlier as the `monStorageClassName` and `osdStorageClassName` parameters. For more information about the `OcsCluster` parameters, see the [parameter reference](#ocs-vpc-param-ref).

  **Multizone clusters** To use a metro `retain` storage class like `ibmc-vpc-block-metro-retain-10iops-tier` to create your OCS storage cluster, you must [create a custom storage class](/docs/openshift?topic=openshift-vpc-block#vpc-customize-storage-class) with the same specifications as the metro `retain` class that you want to use. For more information, see the [Limitations](/docs/openshift?topic=openshift-ocs-storage-cluster-setup#ocs-limitations).
  {: important}

  **Example custom resource definition for installing OCS on all worker nodes in a VPC cluster**
  ```yaml
  apiVersion: ocs.ibm.io/v1
  kind: OcsCluster
  metadata:
    name: ocscluster-vpc
  spec:
    monStorageClassName: <monStorageClassName> # For multizone clusters, specify a 'metro' storage class
    monSize: <monSize>
    osdStorageClassName: <osdStorageClassName> # For multizone clusters, specify a 'metro' storage class
    osdSize: <osdSize> # The OSD size is the total storage capacity of your OCS storage cluster
    numOfOsd: 1
    billingType: hourly
    ocsUpgrade: false
  ```
  {: codeblock}

  **Example custom resource definition for installing OCS only on specified worker nodes in a VPC cluster**
  ```yaml
  apiVersion: ocs.ibm.io/v1
  kind: OcsCluster
  metadata:
    name: ocscluster-vpc
  spec:
    monStorageClassName: <monStorageClassName> # Example: ibmc-vpc-block-10iops-tier. For multizone clusters, specify a 'metro' storage class
    monSize: <monSize>
    osdStorageClassName: <osdStorageClassName> # Example: ibmc-vpc-block-10iops-tier. For multizone clusters, specify a 'metro' storage class
    osdSize: <osdSize> # The OSD size is the total storage capacity of your OCS storage cluster
    numOfOsd: 1
    billingType: hourly
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


**Next steps**: [Deploy an app that uses OCS](/docs/openshift?topic=openshift-ocs-deploy-app)

<br />


## Add-on for classic clusters: Creating your OCS storage cluster CRD
{: #ocs-classic-deploy-crd}

To deploy OCS in your classic cluster, you can create a custom resource definition that is used to specify your storage device details.
{: shortdesc}

If you want to use an {{site.data.keyword.cos_full_notm}} service instance as your default backing store, make sure that you [created the service instance](/docs/openshift?topic=openshift-ocs-storage-install#ocs-create-cos), and created the Kubernetes secret in your cluster. When you create the OCS CRD in your cluster, OCS looks for a secret named `ibm-cloud-cos-creds` to set up the default backing store by using your {{site.data.keyword.cos_short}} HMAC credentials.
{: note}

1. Create a custom resource called `OcsCluster`. Save and edit the following custom resource definition to include the device paths for the local disks [that you retrieved earlier](/docs/openshift?topic=openshift-ocs-storage-prep#ocs-classic-get-devices). If you do not provide the optional `workerNodes` parameter, then all of the worker nodes in your cluster are used for the OCS deployment. Be sure to include the `/dev/disk/by-id/` path when you specify your storage devices.

  **Example custom resource for installing OCS on all worker nodes in a classic cluster**
  ```yaml
  apiVersion: ocs.ibm.io/v1
  kind: OcsCluster
  metadata:
    name: ocscluster-classic
  spec:
    monStorageClassName: localfile
    monSize: 20Gi
    osdStorageClassName: localblock
    osdSize: "1"
    numOfOsd: 1
    billingType: hourly
    ocsUpgrade: false
    monDevicePaths:
      - <device-by-id> # Example: /dev/disk/by-id/scsi-3600605b00d87b43027b3bc310a64c6c9-part1
      - <device-by-id> # Example: /dev/disk/by-id/scsi-3600605b00d87b43027b3bc310a64c6c9-part2
      - <device-by-id> # Example: /dev/disk/by-id/scsi-3600605b00d87b43027b3bc310a64c6c9-part2
    osdDevicePaths:
      - <device-by-id> # Example: /dev/disk/by-id/scsi-3600605b00d87b43027b3bc310a64c6c9-part1
      - <device-by-id> # Example: /dev/disk/by-id/scsi-3600605b00d87b43027b3bc310a64c6c9-part2
      - <device-by-id> # Example: /dev/disk/by-id/scsi-3600605b00d87b43027b3bc310a64c6c9-part2
  ```
  {: codeblock}

  **Example custom resource for installing OCS only on certain worker nodes in a classic cluster**
  ```yaml
  apiVersion: ocs.ibm.io/v1
  kind: OcsCluster
  metadata:
    name: ocscluster-classic
  spec:
    monStorageClassName: localfile
    monSize: 20Gi
    osdStorageClassName: localblock
    osdSize: "1"
    numOfOsd: 1
    billingType: hourly
    ocsUpgrade: false
    monDevicePaths:
      - <device-by-id> # Example: /dev/disk/by-id/scsi-3600605b00d87b43027b3bc310a64c6c9-part1
      - <device-by-id> # Example: /dev/disk/by-id/scsi-3600605b00d87b43027b3bc310a64c6c9-part2
      - <device-by-id> # Example: /dev/disk/by-id/scsi-3600605b00d87b43027b3bc310a64c6c9-part2
    osdDevicePaths:
      - <device-by-id> # Example: /dev/disk/by-id/scsi-3600605b00d87b43027b3bc310a64c6c9-part1
      - <device-by-id> # Example: /dev/disk/by-id/scsi-3600605b00d87b43027b3bc310a64c6c9-part2
      - <device-by-id> # Example: /dev/disk/by-id/scsi-3600605b00d87b43027b3bc310a64c6c9-part2
    workerNodes: # Specify the private IP addresses of each worker node where you want to install OCS.
      - <worker-IP> # To get a list worker nodes, run `oc get nodes`.
      - <worker-IP>
      - <worker-IP>
  ```
  {: codeblock}

1. Save the file and create the `OcsCluster` custom resource to your cluster.
  ```sh
  oc create -f <ocs_cluster_filename>
  ```
  {: pre}

1. Verify that your `OcsCluster` custom resource is running.
  ```sh
  oc describe OcsCluster ocscluster-classic
  ```
  {: pre}


**Next steps**: [Deploy an app that uses OCS](/docs/openshift?topic=openshift-ocs-deploy-app).

## Operator: Creating an OCS storage cluster in the web console
{: #ocs-create-storagecluster-console}

If you installed the OCS operator from OperatorHub, you can use the web console to create a storage cluster.

### VPC: Creating a storage cluster in the web console
{: #ocs-vpc-deploy-console}

Complete the following steps to create an OCS storage cluster by using the {{site.data.keyword.openshiftshort}} web console.
{: shortdesc}

Complete the following steps only if you installed the OCS Operator from OperatorHub. If you installed the OCS add-on in your cluster, see [creating a storage cluster by using a CRD](#ocs-vpc-deploy-crd)
{: note}

1. From the {{site.data.keyword.openshiftshort}} web console, click **Operators** > **Installed Operators**.
1. Click the **OpenShift Container Storage operator**, then click the **Storage Cluster** tab and **Create Storage Cluster**
1. On the **Create Storage Cluster** page, make sure that the **Internal** tab is selected.
1. In the **Storage Class** menu, select the {{site.data.keyword.block_storage_is_short}} that you want to use for your OCS volumes. For multizone clusters, you must specify a metro storage class. Metro storage classes have the volume binding mode `WaitForFirstConsumer`, which is required for multizone OCS deployments. **Note**: To use a metro `retain` storage class like `ibmc-vpc-block-metro-retain-10iops-tier` to create your OCS storage cluster, you must [create a custom storage class](/docs/openshift?topic=openshift-vpc-block#vpc-customize-storage-class) with the same specifications as the metro `retain` class that you want to use. For more information, see the [Limitations](/docs/openshift?topic=openshift-ocs-storage-cluster-setup#ocs-limitations).
1. In the **OCS Service Capacity** menu, select the size of the OCS storage cluster that you want to create.
1. Enable or disable encrytion.
1. In the **Nodes** section, select the worker nodes where you want to provision the volumes for your OCS storage cluster.
1. Click **Create** to create your storage cluster.
1. Verify that your storage cluster is created and `Ready`.
  1. From the {{site.data.keyword.openshiftshort}} web console, click **Operators** > **Installed Operators**.
  1. Click the **OpenShift Container Storage operator**, then click the **Storage Cluster** tab.
  1. Verify that the storage cluster status is `Ready`. Creating the storage cluster takes approximately 15 minutes.


**Next steps**: [Deploy an app that uses OCS](/docs/openshift?topic=openshift-ocs-deploy-app)

### Classic: Creating a storage cluster in the web console
{: #ocs-classic-deploy-console}

Complete the following steps to create an OCS storage cluster by using the {{site.data.keyword.openshiftshort}} web console.
{: shortdesc}

Complete the following steps only if you installed the OCS Operator from OperatorHub. If you installed the OCS add-on in your cluster, see [creating a storage cluster by using a CRD](#ocs-classic-deploy-crd)
{: note}

1. From the {{site.data.keyword.openshiftshort}} web console, click **Operators** > **Installed Operators**.
1. Click the **OpenShift Container Storage operator**, then click the **Storage Cluster** tab and **Create Storage Cluster**
1. On the **Create Storage Cluster** page, make sure that the **Internal - Attached Devices** tab is selected.
1. In **1: Detect Disks**, on the **Auto Detect Volume** page, select the worker nodes where you want to detect local storage volumes.
1. In **2: Create Storage Class**, on the **Local Volume Set** page, enter a name for your volume set and specify the **Disk type**.
1. In **3: Create Storage Cluster**, specify the capacity and encryption setting that you want to use.
1. Click **Create** to create your storage cluster.
1. Verify that your storage cluster is created and `Ready`.
  1. From the {{site.data.keyword.openshiftshort}} web console, click **Operators** > **Installed Operators**.
  1. Click the **OpenShift Container Storage operator**, then click the **Storage Cluster** tab.
  1. Verify that the storage cluster status is `Ready`. Creating the storage cluster takes approximately 15 minutes.


**Next steps**: [Deploy an app that uses OCS](/docs/openshift?topic=openshift-ocs-deploy-app)

## VPC: OpenShift Container Storage parameter reference
{: #ocs-vpc-param-ref}

Refer to the following OpenShift Container Storage parameters when you use the add-on or operator in VPC clusters.
{: shortdesc}


| Parameter | Description | Default value |
| --- | --- | --- |
| `monStorageClassName` | Enter the name of the storage class that you want to use for your MON devices. For **multizone clusters**, specify the metro storage class that you want to use. If you want to use a metro `retain` storage class, [create a custom `WaitForFirstConsumer` storage class](/docs/openshift?topic=openshift-vpc-block#vpc-customize-storage-class) that is based off the tiered metro `retain` storage class that you want to use. Metro storage classes have the volume binding mode `WaitForFirstConsumer`, which is required for multizone OCS deployments. For **single zone clusters**, enter the name of the tiered storage class that you want to use. Example: `ibmc-vpc-block-10iops-tier`. For more information about VPC tiered storage classes, see the [{{site.data.keyword.block_storage_is_short}} Storage class reference](/docs/openshift?topic=openshift-vpc-block#vpc-block-reference).| N/A |
| `monSize` | Enter a size for your monitoring storage devices. Example: `20Gi` | N/A |
| `osdStorageClassName` | Enter the name of the storage class that you want to use for your OSD devices. For **multizone clusters**, specify the metro storage class that you want to use. If you want to use a metro `retain` storage class, [create a custom `WaitForFirstConsumer` storage class](/docs/openshift?topic=openshift-vpc-block#vpc-customize-storage-class) that is based off the tiered metro `retain` storage class that you want to use. Metro storage classes have the volume binding mode `WaitForFirstConsumer`, which is required for multizone OCS deployments. For **single zone clusters**, enter the name of the tiered storage class that you want to use. Example: `ibmc-vpc-block-10iops-tier`. For more information about VPC tiered storage classes, see the [{{site.data.keyword.block_storage_is_short}} Storage class reference](/docs/openshift?topic=openshift-vpc-block#vpc-block-reference).| N/A |
| `osdSize` | Enter a size for your storage devices. Example: `100Gi`. The total storage capacity of your OCS cluster is equivalent to the `osdSize` x 3 divided by the `numOfOsd`. | N/A |
| `numOfOsd` | Enter the number object storage daemons (OSDs) that you want to create. OCS creates three times the `numOfOsd` value. For example, if you enter `1`, OCS provisions 3 disks of the size and storage class that you specify in the `osdStorageClassName` field. | `1` |
| `billingType` | Enter a `billingType` of either `hourly` or `monthly` for your OCS deployment. | `hourly` |
| `ocsUpgrade` | Enter a `true` or `false` to upgrade the major version of your OCS deployment. | `false` |
| `worker-IP` | **Optional**: Enter the private IP addresses for the worker nodes that you want to use for your OCS deployment. Do not specify this parameter if you want to use all of the worker nodes in your cluster. | N/A |
{: caption="OCS parameter reference" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the custom resource parameter. The second column is a brief description of the parameter. The third column is the default value of the parameter."}

## Classic: OpenShift Container Storage parameter reference
{: #ocs-classic-param-ref}


Refer to the following OpenShift Container Storage parameters when you use the add-on or operator in classic clusters.
{: shortdesc}


| Parameter | Description | Default value |
| --- | --- | --- |
| `monStorageClassName` | Enter the name of the storage class that you want to use for your MON devices. For baremetal worker nodes, enter `localfile`. | N/A |
| `monSize` | Enter a size for your monitoring storage pods. Example: `20Gi`. | N/A |
| `osdStorageClassName` | Enter the name of the storage class that you want to use for your OSD devices. For baremetal worker nodes, enter `localblock`. | N/A |
| `osdSize` | Enter a size for your monitoring storage devices. Example: `100Gi`. | N/A |
| `numOfOsd` | Enter the number object storage daemons (OSDs) that you want to create. OCS creates three times the specified number. For example, if you enter `1`, OCS creates 3 OSDs. | `1` |
| `billingType` | Enter a `billingType` of either `hourly` or `monthly` for your OCS deployment. | `hourly` |
| `ocsUpgrade` | Enter a `true` or `false` to upgrade the major version of your OCS deployment. | `false` |
| `worker-IP` | **Optional**: Enter the private IP addresses for the worker nodes that you want to use for your OCS deployment. Do not specify this parameter if you want to use all of the worker nodes in your cluster. To retrieve your worker node IP addresses, run `oc get nodes`. | N/A |
{: caption="OpenShift Container Storage parameter reference" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the custom resource parameter. The second column is a brief description of the parameter. The third column is the default value of the parameter."}

<br />

## Limitations
{: #ocs-limitations}

Review the following limitations for deploying OCS.

**Kubernetes resource ID character limit:** Kubernetes PVC names must be fewer than 63 characters. If you deploy OCS in a multizone VPC cluster and create your OCS storage cluster by using a metro `retain` storage class such as `ibmc-vpc-block-metro-retain-10iops-tier`, the corresponding OCS device set that is created by using this storage class fails. For more information see [OCS device set creation fails due to Kubernetes character limitation](/docs/openshift?topic=openshift-ocs-manage-deployment#ocs-ts-sc-name-limit).

## Storage class reference
{: #ocs-reference-section}

[OCS storage class reference](/docs/openshift?topic=openshift-ocs-sc-ref)
