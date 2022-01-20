---

copyright: 
  years: 2014, 2022
lastupdated: "2022-01-20"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Planning highly available persistent storage
{: #storage_planning}


## Choosing a storage solution
{: #choose_storage_solution}


Before you can decide what type of storage is the right solution for your {{site.data.keyword.openshiftlong}} clusters, you must understand the {{site.data.keyword.cloud_notm}} infrastructure provider, your app requirements, the type of data that you want to store, and how often you want to access this data.

1. Decide whether your data must be permanently stored, or if your data can be removed at any time.
    - **Persistent storage:** Your data must still be available, even if the container, the worker node, or the cluster is removed. Use persistent storage in the following scenarios:
        - Stateful apps
        - Core business data
        - Data that must be available due to legal requirements, such as a defined retention period
        - Auditing
        - Data that must be accessed and shared across app instances
    - **Non-persistent storage:** Your data can be removed when the container, the worker node, or the cluster is removed. Non-persistent storage is typically used for logging information, such as system logs or container logs, development testing, or when you want to access data from the host's file system. To find an overview of available non-persistent storage options, see [Comparison of non-persistent storage options](#non_persistent_overview).

2. If you must persist your data, analyze if your app requires a specific type of storage. When you use an existing app, the app might be designed to store data in one of the following ways:  
    - **In a file system:** The data can be stored as a file in a directory. For example, you could store this file on your local hard disk. Some apps require data to be stored in a specific file system, such as `nfs` or `ext4` to optimize the data store and achieve performance goals.
    - **In a database:** The data must be stored in a database that follows a specific schema. Some apps come with a database interface that you can use to store your data. For example, WordPress is optimized to store data in a MySQL database. In these cases, the type of storage is selected for you.

3. If your app does not have a limitation on the type of storage that you must use, determine the type of data that you want to store.
    - **Structured data:** Data that you can store in a relational database where you have a table with columns and rows. Data in tables can be connected by using keys and is usually easy to access due to the pre-defined data model. Examples are phone numbers, account numbers, Social Security numbers, or postal codes.
    - **Semi-structured data:** Data that does not fit into a relational database, but that comes with some organizational properties that you can use to read and analyze this data more easily. Examples are markup language files such as CSV, XML, or JSON.  
    - **Unstructured data:** Data that does not follow an organizational pattern and that is so complex that you can't store it in a relational database with pre-defined data models. To access this data, you need advanced tools and software. Examples are e-mail messages, videos, photos, audio files, presentations, social media data, or web pages.

    If you have structured and unstructured data, try to store each data type separately in a storage solution that is designed for this data type. Using an appropriate storage solution for your data type eases up access to your data and gives you the benefits of performance, scalability, durability, and consistency.
    {: tip}

4. Analyze how you want to access your data. Storage solutions are usually designed and optimized to support read or write operations.  
    - **Read-only:** You don't want to write or change your data. Your data is read-only.
    - **Read and write:** You want to read, write, and change your data. For data that is read and written, it is important to understand if the operations are read-heavy, write-heavy, or balanced.

5. Determine the frequency that your data is accessed. Understanding the frequency of data access can help you understand the performance that you require for your storage. For example, data that is accessed frequently usually resides on fast storage.
    - **Hot data:** Data that is accessed frequently. Common use cases are web or mobile apps.
    - **Cool or warm data:** Data that is accessed infrequently, such as once a month or less. Common use cases are archives, short-term data retention, or disaster recovery.
    - **Cold data:** Data that is rarely accessed, if at all. Common use cases are archives, long-term backups, historical data.
    - **Frozen data:** Data that is not accessed and that you need to keep due to legal reasons.

    If you can't predict the frequency or the frequency does not follow a strict pattern, determine whether your workloads are read-heavy, write-heavy, or balanced. Then, look at the storage option that fits your workload and investigate what storage tier gives you the flexibility that you need. For example, {{site.data.keyword.cos_full_notm}} provides a `flex` storage class that considers how frequent data is accessed in a month and takes into account this measurement to optimize your monthly billing.
    {: tip}

6. Investigate if your data must be shared across multiple app instances, zones, or regions.
    - **Access across pods:** When you use Kubernetes persistent volumes to access your storage, you can determine the number of pods that can mount the volume at the same time. Some storage solutions, such as block storage, can be accessed by one pod at a time only. With other storage solutions, you can share volume across multiple pods.
    - **Access across zones and regions:** You might require your data to be accessible across zones or regions. Some storage solutions, such as file and block storage, are data center-specific and can't be shared across zones in a multizone cluster setup.

    If you want to make your data accessible across zones or regions, make sure to consult your legal department to verify that your data can be stored in multiple zones or a different country.
    {: note}

7. Understand other storage characteristics that impact your choice.
    - **Consistency:** The guarantee that a read operation returns the latest version of a file. Storage solutions can provide `strong consistency` when you are guaranteed to always receive the latest version of a file, or `eventual consistency` when the read operation might not return the latest version. You often find eventual consistency in geographically distributed systems where a write operation first must be replicated across all instances.
    - **Performance:** The time that it takes to complete a read or write operation.
    - **Durability:** The guarantee that a write operation that is committed to your storage survives permanently and does not get corrupted or lost, even if gigabytes or terabytes of data are written to your storage at the same time.
    - **Resiliency:** The ability to recover from an outage and continue operations, even if a hardware or software component failed. For example, your physical storage experiences a power outage, a network outage, or is destroyed during a natural disaster.
    - **Availability:** The ability to provide access to your data, even if a data center or a region is unavailable. Availability for your data is usually achieved by adding redundancy and setting up failover mechanisms.
    - **Scalability:** The ability to extend capacity and customize performance based on your needs.
    - **Encryption:** The masking of data to prevent visibility when data is accessed by an unauthorized user.

8. [Review available persistent storage solutions](#persistent_storage_overview) and pick the solution that best fits your app and data requirements.




## Comparison of non-persistent storage options
{: #non_persistent_overview}

You can use non-persistent storage options if your data is not required to be persistently stored or if you want to unit-test your app components.
{: shortdesc}

The following image shows available non-persistent data storage options in {{site.data.keyword.openshiftlong_notm}}. These options are available for free and standard clusters.

![Non-persistent data storage options](images/cs_storage_nonpersistent.png)


| Characteristics | Inside the container | On the worker node's primary or secondary disk |
| --- | --- | --- |
| Multizone capable | No | No | 
| Supported in VPC clusters | Yes | No |
| Supported OpenShift versions | 3.11, 4.3 - 4.6 | 3.11, 4.3 - 4.6 |
| Data types | All | All |
| Capacity| Limited to the worker node's available secondary disk. To limit the amount of secondary storage that is consumed by your pod, use resource requests and limits for [ephemeral storage](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#local-ephemeral-storage){: external}. | Limited to the worker node's available space on the primary (`hostPath`) or secondary disk (`emptyDir`). To limit the amount of secondary storage that is consumed by your pod, use resource requests and limits for [ephemeral storage](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#local-ephemeral-storage){: external}. | 
| Data access pattern | Read and write operations of any frequency| Read and write operations of any frequency |
| Access | Via the container's local file system | Via [Kubernetes `hostPath`](https://kubernetes.io/docs/concepts/storage/volumes/#hostpath){: external} for access to worker node primary storage. Via [Kubernetes `emptyDir` volume](https://kubernetes.io/docs/concepts/storage/volumes/#emptydir){: exteral} for access to worker node secondary storage. | 
| Performance | High | High with lower latency when you use SSD | Consistency | Strong | Strong |
| Resiliency | Low | Low |
| Availability | Specific to the container | Specific to the worker node |
| Scalability | Difficult to extend as limited to the worker node's secondary disk capacity| Difficult to extend as limited to the worker node's primary and secondary disk capacity | 
| Durability | Data is lost when the container crashes or is removed. | Data in `hostPath` or `emptyDir` volumes is lost when the worker node is deleted, the worker node is reloaded or updated, the cluster is deleted, the {{site.data.keyword.cloud_notm}} account reaches a suspended state. In addition, data in an `emptyDir` volume is removed when the assigned pod is permanently deleted from the worker node, the assigned pod is scheduled on another worker node. |
| Common use cases | Local image cache or container logs | Setting up a high-performance local cache, accessing files from the worker node file system, or running unit tests. | 
| Non-ideal use cases | Persistent data storage or sharing data between containers | Persistent data storage |
{: summary="The columns are read from left to right. The first column has the characteristic of the non-persistent storage option. The second column says whether the non-persistent storage is inside the container. The third column says whether the non-persistent storage is on the worker node disk."}
{: caption="Non-persistent storage options"}




## Comparison of persistent storage options for single zone clusters
{: #single_zone_persistent_storage}

If you have a single zone cluster, you can choose between the following options in {{site.data.keyword.openshiftlong_notm}} that provide fast access to your data. For higher availability, use a storage option that is designed for [geographically distributed data](#persistent_storage_overview) and, if possible for your requirements, create a multizone cluster.
{: shortdesc}

Persistent data storage options are available for standard clusters only.
{: note}

The following image shows the options that you have in {{site.data.keyword.openshiftlong_notm}} to permanently store your data in a single cluster.

![Persistent storage options for single zone cluster](images/cs_storage_single_zone.png)


| Characteristics | Classic File Storage | Classic Block Storage / VPC Block Storage
| --- | --- | --- |
| Multizone-capable | No, as specific to a data center. Data can't be shared across zones, unless you implement your own data replication. |No, as specific to a data center. Data can't be shared across zones, unless you implement your own data replication. | 
| Supported in VPC clusters | No | Yes |
| Supported OpenShift versions | 3.11, 4.3 - 4.6 | 3.11, 4.3 - 4.6 |
| Ideal data types | All | All | 
| Data usage pattern | Random read-write operations, sequential read-write operations, or write-intensive workloads | 
| Access | Via file system on mounted volume | Via file system on mounted volume|
| Supported Kubernetes access writes | ReadWriteMany (RWX), ReadOnlyMany (ROX), ReadWriteOnce (RWO) | ReadWriteOnce (RWO) | 
| Performance | Predictable due to assigned IOPS and size. IOPS are shared between the pods that access the volume.| Predictable due to assigned IOPS and size. IOPS are not shared between pods. | 
| Consistency| Strong| Strong | 
| Durability | High | High | 
| Resiliency| Medium as specific to a data center. File storage server is clustered by IBM with redundant networking.| Medium as specific to a data center. Block storage server is clustered by IBM with redundant networking. | 
| Availability | Medium as specific to a data center. | Medium as specific to a data center. |
| Scalability | Difficult to extend beyond the data center. You can't change an existing storage tier. | Difficult to extend beyond the data center. You can't change an existing storage tier. |
| Encryption | At rest |   \n **Classic Block Storage**: Encryption at rest.   \n - **VPC Block Storage**: Encryption in transit with Key Protect.|
| Backup and recovery | Set up periodic snapshots, replicate snapshots, duplicate storage, back up data to {{site.data.keyword.cos_full_notm}}, or copy data to and from pod and containers. |   \n **Classic Block Storage**: Set up periodic snapshots, replicate snapshots, duplicate storage, back up data to {{site.data.keyword.cos_full_notm}}, or copy data to and from pod and containers.  \n - **VPC Block Storage**: Kubernetes [`oc cp`](https://kubernetes.io/docs/reference/kubectl/overview/#cp) command. |
| Common use cases | Mass or single file storage or file sharing across a single zone cluster. | Stateful sets, backing storage when you run your own database, or high-performance access for single pods. | 
| Non-ideal use cases| Multizone clusters or geographically distributed data | Multizone clusters, geographically distributed data, or sharing data across multiple app instances. | 
{: summary="The columns are read from left to right. The first column has the characteristic of the single-zone persistent storage option. The second column describes the characteristic for file storage. The third column describes the characteristic for block storage."}
{: caption="Persistent storage options for single zone clusters"}





## Comparison of persistent storage options for multizone clusters
{: #persistent_storage_overview}

If you have a multizone cluster, choose between the following persistent storage options to access your data from worker nodes that are spread across zones.
{: shortdesc}

Persistent data storage options are available for standard clusters only.

Looking to connect your cluster to an on-prem database instead? See [Setting up VPN connectivity to your cluster](/docs/openshift?topic=openshift-vpn#vpn).
{: tip}

The following image shows the options that you have in {{site.data.keyword.openshiftlong_notm}} to permanently store your data in a multizone cluster and make your data highly available. You can use these options in a single zone cluster, but you might not get the high availability benefits that your app requires.

![High availability options for persistent storage in a multizone cluster](images/cs_storage_options_multizone.png)


| Characteristics | Object Storage | SDS (Portworx) | {{site.data.keyword.cloud_notm}} Databases|
| --- | --- | --- | --- |
| Multizone-capable | Yes | Yes | Yes |
| Supported in VPC clusters| Yes | Yes | Yes |
| Supported OpenShift versions |  3.11, 4.3 - 4.6 |  3.11, 4.3 - 4.6 |  3.11, 4.3 - 4.6 |
| Ideal data types | Semi-structured and unstructured data | All | Depends on the DBaaS |
| Data usage pattern | Read-intensive workloads. Few or no write operations. | Write-intensive workloads. Random read and write operation. Sequential read and write operations | Read-write-intensive workloads |
| Access | Via file system on mounted volume (plug-in) or via REST API from your app | Via file system on mounted volume or NFS client access to the volume. | Via REST API from your app. | 
| Supported Kubernetes access writes |  \n - ReadWriteMany (RWX)  \n - ReadOnlyMany (ROX)  \n - ReadWriteOnce (RWO) | All | N/A as accessed from the app directly. | 
| Performance | High for read operations. Predictable due to assigned IOPS and size when you use non-SDS machines. |Close to bare metal performance for sequential read and write operations when you use SDS machines. Provides [profiles](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/create-pvcs/dynamic-provisioning/#using-dynamic-provisioning){: external} to run high-performance databases. Possibility to create a storage layer with different performance profiles that your app can choose from.| High if deployed to the same data center as your app. |
| Consistency| Eventual | Strong | Depends on the DBaaS | 
| Durability | Very high as data slices are dispersed across a cluster of storage
nodes. Every node stores only a part of the data. | Very high as three copies of your data are always maintained. | High | 
| Resiliency | High as data slices are dispersed across three zones or regions. Medium, when set up in a single zone only. | High when set up with replication across three zones. Medium, when you store data in a single zone only. | Depends on the DBaaS and your setup. |
| Availability | High due to the distribution across zones or regions. | High when you replicate data across three worker nodes in different zones. | High if you set up multiple instances. |
| Scalability | Scales automatically | Increase volume capacity by resizing the volume. To increase overall storage layer capacity, you must add worker nodes or remote block storage. Both scenarios require monitoring of capacity by the user. | Scales automatically | 
| Encryption | In transit and at rest | Bring your own key to protect your data in transit and at rest with {{site.data.keyword.keymanagementservicelong_notm}}. | At rest |
| Backup and recovery| Data is automatically replicated across multiple nodes for high durability. For more information, see the SLA in the [{{site.data.keyword.cos_full_notm}} service terms](http://www.ibm.com/support/customer/csol/terms/?id=i126-7857&lc=en){: external}.  You can also use the  Kubernetes [`oc cp`](https://kubernetes.io/docs/reference/kubectl/overview/#cp){: external} command to copy data to and from pod and containers. | Use local or cloud snapshots to save the current state of a volume. For more information, see [Create and use local snapshots](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/create-snapshots/){: external}. You can also use the  Kubernetes [`oc cp`](https://kubernetes.io/docs/reference/kubectl/overview/#cp) command to copy data to and from pod and containers. | Depends on the DBaaS | 
| Common use cases | Multizone clusters. Geographically distributed data. Static big data. Static multimedia content | Web apps | Backups | Archives | Stateful sets. Geographically distributed data. Common storage solution when you run apps across multiple cloud providers. Backing storage when you run your own database. High-performance access for single pods. Shared storage access across multiple pods and worker nodes. | Multizone clusters, relational and non-relational databases, or geographically distributed data. | 
| Non-ideal use cases | Write-intensive workloads, random write operations, incremental data updates, or transaction databases. | N/A | App that is designed to write to a file system. | 
{: caption: Persistent storage options for multizone clusters"}
{: summary="The columns are read from left to right. The first column has the characteristic of the multizone persistent storage option. The second column describes the characteristic for object storage. The third column describes the characteristic for SDS Portworx storage. The fourth column describes the characteristic for database-as-a-service storage."}





