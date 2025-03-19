---

copyright:
  years: 2014, 2025
lastupdated: "2025-03-19"


keywords: openshift, openshift data foundation, openshift container storage
subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}




# Understanding OpenShift Data Foundation
{: #ocs-storage-prep}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}


[OpenShift Data Foundation](https://www.redhat.com/en/technologies/cloud-computing/openshift-data-foundation){: external} is a highly available storage solution that you can use to manage persistent storage for your containerized apps.
{: shortdesc}

What is OpenShift Data Foundation?
:   OpenShift Data Foundation is a highly available storage solution that consists of several open source operators and technologies like [Ceph](https://docs.ceph.com/en/latest/dev/developer_guide/intro/){: external}, [NooBaa](https://www.noobaa.io/){: external}, and [Rook](https://rook.io/){: external}. These operators allow you to provision and manage File, Block, and Object storage for your containerized workloads in {{site.data.keyword.openshiftlong}} clusters. Unlike other storage solutions where you might need to configure separate drivers and operators for each type of storage, ODF is a unified solution capable of adapting or scaling to your storage needs. You can also deploy ODF on any OCP cluster.

How does OpenShift Data Foundation work?
:   ODF uses these devices to create a virtualized storage layer, where your app data is replicated for high availability. Because ODF abstracts your underlying storage, you can use ODF to create File, Block, or Object storage claims from the same underlying raw block storage.
:   ODF uses storage volumes in multiples of 3 and replicates your app data across these volumes. The underlying storage volumes that you use for ODF depends on your cluster type.
    - For **VPC clusters**, the storage volumes are {{site.data.keyword.block_storage_is_short}} storage volumes. 
    - For bare metal **Classic clusters**, the storage volumes are local disks on your bare metal worker nodes.
    - For **{{site.data.keyword.satelliteshort}} clusters**, the storage volumes are either local disks on your worker nodes, or you can dynamically provision disks by using a compatible block storage driver.

Can I install OpenShift Data Foundation on private-only VPC clusters?
:   Yes, you can install ODF on private-only VPC clusters beginning with cluster version `4.16.23_1546_openshift` for CoreOS workers and `4.16.21_1544_openshift` for RHEL workers.

Can I install the OpenShift Data Foundation add-on in {{site.data.keyword.satelliteshort}} clusters?
:   No. The cluster add-on is available only for Classic and VPC clusters. 


How do install OpenShift Data Foundation on {{site.data.keyword.satelliteshort}}?
:   You can install ODF on {{site.data.keyword.satelliteshort}} by using one of the {{site.data.keyword.satelliteshort}} storage templates. For more information, see the [{{site.data.keyword.satelliteshort}} storage docs](/docs/satellite?topic=satellite-storage-template-ov&interface=ui).
    - [`odf-local`](/docs/satellite?topic=satellite-storage-odf-local): Choose this template when you have local storage available to your worker nodes. If your storage volumes are visible when running `lsblk`, you can use these disks when deploying ODF if they are raw and unformatted.
    - [`odf-remote`](/docs/satellite?topic=satellite-storage-odf-remote): Choose this template if you have a CSI driver installed in your cluster. For example, the `azuredisk-csi-driver` driver. You can use the CSI driver to dynamically provision storage volumes when deploying ODF.



For a full overview of the features and benefits, see [OpenShift Data Foundation](https://www.redhat.com/en/technologies/cloud-computing/openshift-data-foundation){: external}.


## Architecture overview
{: #odf-ov}


Review the following diagram and table to learn more about OpenShift Data Foundation.
{: shortdesc}

![ODF architecture](images/ODF_components.svg "ODF architecture"){: caption="ODF architecture" caption-side="bottom"}


| Number | ODF component | Description |
| --- | --- | --- |
| 1 | OpenShift Data Foundation storage classes | When you deploy ODF, the ODF operator creates File, Block, and Object storage classes in your cluster. Reference these storage classes in your PVCs and to claim storage for your apps. |
| 2 | OSD Block Storage  | These devices provide application storage in your cluster. Each OSD is a raw block storage device that can be a local disk on your worker node or dynamically provisioned when you deploy ODF. In VPC clusters, your OSD block storage devices are dynamically provisioned by using the {{site.data.keyword.block_storage_is_short}} driver. In {{site.data.keyword.satelliteshort}} clusters, you can use local volumes on your worker nodes, or dynamically provision block storage devices by using a block storage driver that supports dynamic provisioning. In Classic clusters, the OSD block devices are local disks on your worker nodes. When you deploy ODF, each device is mounted by an OSD pod. The total storage that is available to your applications is equal to the `osdSize` multiplied by the `numOfOsd`. |
| 3 | Object Storage Daemon (OSD) pods | The OSD pods manage data placement and replication across your storage devices. |
| 4 | Monitor (Mon) pods | The Monitor pods keep a map of your OpenShift Data Foundation storage cluster and monitor storage cluster health. |
| 5 | Monitor (Mon) block storage device | The monitor storage devices are the underlying storage devices for the monitor pods. Each monitor device is a raw block storage device that can be a local disk on your worker node or dynamically provisioned when you deploy ODF. Each device provides storage to a monitor pod. |
{: caption="ODF architecture overview" caption-side="bottom"}



## Multicloud Object Gateway overview
{: #understanding-noobaa}

The Multicloud Object Gateway consists of the open source tool [NooBaa](https://www.noobaa.io/){: external} and is a component of OpenShift Data Foundation. With the Multicloud Object Gateway, you can manage objects and buckets across cloud providers.
{: shortdesc}

![Multicloud Object Gateway overview](images/noobaa.svg "NooBaa overview"){: caption="Multicloud Object Gateway overview" caption-side="bottom"}

| Number | Multicloud Object Gateway component | Description |
| --- | --- | --- |
| 1 | Backing store | Backing stores are s3 compatible object storage buckets. In the Multicloud Object Gateway, your backing stores can be in any cloud environment, regardless of provider. You can connect several backing stores to the Multicloud Object Gateway. When you deploy ODF, the default backing store uses the raw block storage devices that you specify for your ODF storage cluster. However, you can optionally set up {{site.data.keyword.cos_full_notm}} as your default backing store. |
| 2 | Bucket class | A bucket class consists of one or more backing stores (buckets) and a placement policy. You can configure backing stores and placement policies to manage your objects across locations and clouds. |
| 3 | Storage class | A storage class in the Multicloud Object Gateway is similar to any other Kubernetes storage class in that it defines storage resource parameters. However, in the Multicloud Object Gateway, when you create a storage class, you specify the bucket class that you want to use. By creating a storage class from your bucket class, you can make your Multicloud Object Gateway resources available across namespaces. |
| 4 | Object bucket claim (OBC) | An object bucket claim (OBC) is similar to a Kubernetes persistent volume claim (PVC) in that developers or storage admins can create OBCs to claim storage resources. When you create an OBC, you specify the storage class that you want to use and optionally provide a name for the dynamically created object bucket. | 
| 5 | Secret | When you create an Object Bucket Claim, a Kubernetes secret is also created in your cluster. |
| 6 | ConfigMap | When you create an Object Bucket Claim, a ConfigMap is also created in your cluster. |
| 7 | Object bucket | An object bucket is a dynamically provisioned when you create an Object bucket claim. The object bucket abstracts one or more backing stores to a single resource. |
| 8 | s3 app | An app that uses object storage. |
| 9 | Secret ref | A secret ref is a reference to a Kubernetes secret in your cluster. When you create an Object Bucket Claim, NooBaa creates a corresponding secret and config map. Then, you can reference the secret and config map in your apps without needing to directly include the credentials in your apps. |
| 10 | ConfigMap ref | A config map ref is a reference to a Kubernetes config map in your cluster. When you create an Object Bucket Claim, NooBaa dynamically creates a corresponding secret and config map. You can reference the secret and config map in your apps without needing to include these credentials in your applications. |
| 11 | Namespace resource | A namespace resource is an s3 compatible bucket. After you add namespace resources (buckets) to your Multicloud Object Gateway, you can reference those buckets by creating a Namespace bucket which can be used to read and write from one or more namespace resource. |
| 12 | Namespace bucket | A namespace bucket abstracts one or more namespace resources in the NooBaa namespace. When you create a namespace bucket, you can specify read or write policies to the namespace resources that you have configured in your Multicloud Object Gateway. For example, you can read from two buckets across different cloud providers and write to a third bucket in another, separate cloud environment. |
| 13 | Namespace bucket access key | The access key is used to access your namespace bucket. Namespace buckets can include multiple namespace resources from different cloud providers or on-prem buckets. The namespace bucket access key and secret key are used in your s3 apps to configure access to your namespace bucket which then defines read and write policies to namespace resources that you configure. |
| 14 | Namespace bucket secret key | The secret key is used to access your namespace bucket. Namespace buckets can include multiple namespace resources from different cloud providers or on-prem buckets. The namespace bucket access key and secret key are used in your s3 apps to configure access to your namespace bucket which then defines read and write policies to namespace resources that you configure. |
| 15 | Placement policy | When you create a bucket class, you must specify a placement policy. Placement policies define how your data is written to your backing stores. A **Mirror** placement policy mirrors objects across the backing stores in your bucket class and a **Spread** placement policy distributes the objects across the backing stores in your bucket class.  |
{: caption="NooBaa overview" caption-side="bottom"}



## Feature support by billing type
{: #odf-essentials-vs-advanced}

| Feature support | Essentials | Advanced |
| --- | --- | --- |
| Block storage | Yes | Yes |
| File storage | Yes | Yes |
| Object storage | Yes | Yes |
| Node and disk resiliency | Yes | Yes | 
| Operator based automation | Yes | Yes | 
| Compression | Yes | Yes |
| Local snapshots and cloning | Yes | Yes |
| Basic Cluster-wide encryption | Yes | Yes | 
| Advanced encryption with KMS | No | Yes |
| Regional disaster recovery with replication | No | Yes | 
| Stretched Clusters - Metro high availability and disaster recover | No | Yes |
| Multi-cluster - Metro high availability and disaster recover | No | Yes |
{: caption="Billing plan overview"}



## Best practices
{: #odf-best-practices}

Review the following sections for best practices when installing and managing ODF.

### Planning
{: #planning-odf}

Plan your worker node distribution
:   To ensure high availability, spread the ODF cluster across failure domains. This distribution helps minimize the impact of node failures and maintain the overall stability of the cluster.

Meet the minimum worker node specifications
:   Worker nodes that use ODF should have 16 vCPUs and 64GB of RAM or higher. For IBM Classic clusters, the recommended flavor is `mb4c.32x384.3.8tb.ssd` or higher.

Keep a standby host for high-availability
:   To ensure high-availability and minimize downtime in the event of a host failure, it is advisable to always keep a standby host.

Meet the storage device count per node recommendations
:   Plan to have fewer than nine storage devices per node. This helps prevent potential bottlenecks and enhances the efficiency of data access and retrieval.

Use the recommended storage device sizes and counts
:   When deploying local storage, use disk sizes of 4 TiB or smaller. It is important to ensure that all disks within the cluster, across all storage nodes, are of the same size and type for optimal use of storage. Use OSDs of at least 512Gi.

Scale up by using default replication factor and storage node configuration
:   In OpenShift Data Foundation (ODF), the replication factor is set to 3 by default. When you add capacity, plan to add storage nodes in multiples of 3.

Choose the right set up for your needs: Remote storage vs local storage
:   If you have lower storage needs or are using Virtual Server instances, remote storage can be a convenient and cost-effective option. On the other hand, if you have large storage requirements, a bare metal cluster, or high-performance storage with low network latency, that uses local storage would be more suitable.

Simplify your deployment by using auto discovery feature
:   In [Classic clusters]{: tag-classic-inf} or environments with local storage, leverage the auto discovery feature to automatically identify and configure the available storage disks in your cluster for ODF. This option eliminates the need for manual disk selection. Unless there are specific disk requirements for ODF provisioning, utilizing the auto discovery feature streamlines the deployment process and reduces the potential for configuration errors.

Use metro storage classes for ODF installations on remote storage
:   When performing an ODF installation that uses remote storage, make sure you use a storage class that has a `VolumeBindingMode` of `WaitForFirstConsumer` which delays the creation of the Block Storage until the first pod that uses this storage is ready to be scheduled.

Size your deployment
:   For a detailed analysis of storage requirements, the [Sizing Tool](https://sizer.ocs.ninja/index.html) to determine your storage capacity needed. You can also use the official [Red Hat sizing tool](https://access.redhat.com/labsinfo/ocsst){: external}

Set up periodic backups
:   Taking periodic backups for the ODF cluster is essential to ensure data protection and facilitate data recovery in the event of a disaster. Without regular backups, recovering data from a catastrophic event becomes significantly more challenging and may lead to permanent data loss.

### Deployment
{: #odf-deploy}

Plan to use dedicated storage nodes
:   In scenarios with heavy workloads, use dedicated storage nodes for ODF. By separating the operations of storage nodes, you can achieve better performance and scalability for your storage infrastructure.

Set up regular monitoring of the Red Hat console
:   The RedHat console provides valuable insights into the health and performance of your ODF environment. It is recommended to regularly monitor the console to stay informed about any potential issues. The console triggers alerts whenever there are problems detected with ODF, enabling you to take proactive measures.

Address capacity warnings promptly
:   When capacity warnings are issued, it is important to address them promptly. Ignoring or delaying action on these warnings can lead to storage capacity constraints and potential disruptions to your workloads. Treat capacity warnings as an opportunity to assess your storage needs and take appropriate measures to mitigate any potential issues.

### Capacity expansion
{: #odf-capacity}
 
Understand your options for capacity expansion
:   There are two options available for capacity expansion in ODF. The first option involves increasing the capacity by adding more OSDs (Object Storage Daemons) on existing nodes within the cluster. This allows for utilizing the available resources to expand the storage capacity. The second option is to expand the capacity by adding new nodes to the cluster. Once the number of OSDs is increased, the OSDs will automatically be provisioned on the newly added nodes.

### Update
{: #odf-update-bp}


Perform health checks replacing nodes
:   Avoid replacing a storage node if ODF is not in a healthy state. Before proceeding with node replacement, always verify the health status of ODF. Try to resolve any issues before replacing the unhealthy node.

Keep your environment up-to-date
:   Keep your cluster version updated to the default or latest version available. Staying up to date with the cluster version ensures that you can leverage the latest capabilities and maintain compatibility with other components in your environment.

Perform ODF updates after cluster upgrades
:   Always upgrade cluster master and workers node first and then go for ODF upgrade. After completing a cluster upgrade, it is essential to update ODF as well. Although ODF supports both the current cluster version (n) and the next cluster version (n+1), keep the ODF version the same as the cluster version. This alignment ensures optimal compatibility.

Upgrade storage nodes sequentially
:   When upgrading your storage nodes, it is best practice to perform the upgrades one by one. This sequential approach allows you to verify the status of ODF after each node upgrade and ensures that your storage infrastructure remains healthy throughout the process. By upgrading nodes individually, you can closely monitor the impact of each upgrade on ODF and quickly identify and resolve any issues that may arise.

### Recovery
{: #odf-removery}

Replace unhealthy hosts
:   In the event of a local disaster, it is recommended that an unhealthy cluster host be replaced with a healthy one.

Follow the documentation to recover OSDs
:   When an OSD (Object Storage Daemon) goes down in OpenShift Data Foundation (ODF), it is important to follow the recommended steps for recovery. The provided documentation from IBM Cloud Platform provides detailed instructions on how to recover an OSD in such situations.

### Uninstalling and removal
{: #odf-uninstall}

Deleting pods and persistent volumes (PVs)
:   When deleting resources that utilize ODF storage classes, it is important to follow the recommended procedure. Always delete the associated pods and PVs created using OF storage classes before proceeding with the deletion of other resources.

Follow the correct cleanup order
:   When decommissioning or removing ODF from your cluster, make sure you follow the documentation when cleaning up resources. Start by deleting the `ocscluster` resource, which is responsible for managing the ODF. Once the `ocscluster` resource is removed, proceed to remove the ODF add-on from the IBM console. Following this sequence ensures a smooth and proper removal of ODF from your cluster, preventing any potential issues or conflicts.

### Troubleshooting
{: #odf-ts-bp}

Review the capacity alerts and thresholds
:   ODF generates capacity alerts when the cluster storage capacity reaches certain thresholds. These thresholds are set at 75% (near-full) and 85% (full) of the total capacity. These alerts indicate that the storage capacity is approaching its limits and requires attention.

Review the common issues
:   When encountering issues with OpenShift Data Foundation (ODF), it is helpful to refer to the available runbooks that provide guidance on troubleshooting common problems. The runbooks contain a comprehensive list of known issues and their corresponding solutions for ODF.

  

## Deploying OpenShift Data Foundation
{: #odf-deploy-options}

Review the deployment options for your infrastructure provider.
{: shortdesc}

Virtual Private Cloud (VPC) clusters
:   You can deploy ODF by using dynamic provisioning with {{site.data.keyword.block_storage_is_short}}. For more information, see [Deploying OpenShift Data Foundation on VPC clusters](/docs/openshift?topic=openshift-deploy-odf-vpc).

{{site.data.keyword.satelliteshort}} clusters
:   If you want to deploy ODF to {{site.data.keyword.satelliteshort}} clusters, you can use the {{site.data.keyword.satelliteshort}} storage template. For more information, see the following links.
:   [Deploying the OpenShift Data Foundation template for remote, dynamically provisioned disks](/docs/satellite?topic=satellite-storage-odf-remote).
:   [Deploying the OpenShift Data Foundation template for local disks](/docs/satellite?topic=satellite-storage-odf-local).

Classic clusters
:   You can deploy ODF by using local disks on your bare metal worker nodes. For more information, see [Deploying OpenShift Data Foundation on Classic clusters](/docs/openshift?topic=openshift-deploy-odf-classic).
