---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-26"

keywords: kubernetes, iks, multi az, multi-az, szr, mzr

subcollection: containers

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Planning your worker node setup
{: #planning_worker_nodes}

Your {{site.data.keyword.containerlong}} cluster consists of worker nodes that are grouped in worker node pools and is centrally monitored and managed by the Kubernetes master. Cluster administrators decide how to set up the cluster of worker nodes to ensure that cluster users have all the resources to deploy and run apps in the cluster.
{:shortdesc}

When you create a standard cluster, worker nodes of the same memory, CPU, and disk space specifications (flavor) are ordered in IBM Cloud infrastructure on your behalf and added to the default worker node pool in your cluster. Every worker node is assigned a unique worker node ID and domain name that must not be changed after the cluster is created. You can choose between virtual or physical (bare metal) servers. Depending on the level of hardware isolation that you choose, virtual worker nodes can be set up as shared or dedicated nodes. To add different flavors to your cluster, [create another worker pool](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_pool_create).

Kubernetes limits the maximum number of worker nodes that you can have in a cluster. Review [worker node and pod quotas ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/setup/cluster-large/) for more information.


Want to be sure that you always have enough worker nodes to cover your workload? Try out [the cluster autoscaler](/docs/containers?topic=containers-ca#ca).
{: tip}

<br />


## Available hardware for worker nodes
{: #shared_dedicated_node}

When you create a standard cluster in {{site.data.keyword.cloud_notm}}, you can choose whether your worker pools consists of worker nodes that are either physical machines (bare metal) or virtual machines that run on physical hardware. You also select the worker node flavor, or combination of memory, CPU, and other machine specifications such as disk storage.
{:shortdesc}

<img src="images/cs_clusters_hardware.png" width="700" alt="Hardware options for worker nodes in a standard cluster" style="width:700px; border-style: none"/>

If you want more than one flavor of worker node, you must create a worker pool for each flavor. You cannot resize existing worker nodes to have different resources such as CPU or memory. When you create a free cluster, your worker node is automatically provisioned as a virtual, shared node in the IBM Cloud infrastructure account. In standard clusters, you can choose the type of machine that works best for your workload. As you plan, consider the [worker node resource reserves](#resource_limit_node) on the total CPU and memory capacity.

Select one of the following options to decide what type of worker pool you want.
* [Virtual machines](#vm)
* [Physical machines (bare metal)](#bm)
* [Software-defined storage (SDS) machines](#sds)



## Virtual machines
{: #vm}

With VMs, you get greater flexibility, quicker provisioning times, and more automatic scalability features than bare metal, at a more cost-effective price. You can use VMs for most general-purpose use cases such as testing and development environments, staging, and prod environments, microservices, and business apps. However, there is a trade-off in performance. If you need high-performance computing for RAM-, data-, or GPU-intensive workloads, use [bare metal](#bm).
{: shortdesc}

**Do I want to use shared or dedicated hardware?**</br>
When you create a standard virtual cluster, you must choose whether you want the underlying hardware to be shared by multiple {{site.data.keyword.IBM_notm}} customers (multi tenancy) or to be dedicated to you only (single tenancy).

* **In a multi-tenant, shared hardware setup**: Physical resources, such as CPU and memory, are shared across all virtual machines that are deployed to the same physical hardware. To ensure that every virtual machine can run independently, a virtual machine monitor, also referred to as the hypervisor, segments the physical resources into isolated entities and allocates them as dedicated resources to a virtual machine (hypervisor isolation).
* **In a single-tenant, dedicated hardware setup**: All physical resources are dedicated to you only. You can deploy multiple worker nodes as virtual machines on the same physical host. Similar to the multi-tenant setup, the hypervisor assures that every worker node gets its share of the available physical resources.

Shared nodes are usually less costly than dedicated nodes because the costs for the underlying hardware are shared among multiple customers. However, when you decide between shared and dedicated nodes, you might want to check with your legal department to discuss the level of infrastructure isolation and compliance that your app environment requires.

Some flavors are available for only one type of tenancy setup. For example, the `m3c` VMs are only available as `shared` tenancy setup.
{: note}

**What are the general features of VMs?**</br>
Virtual machines use local disk instead of storage area networking (SAN) for reliability. Reliability benefits include higher throughput when serializing bytes to the local disk and reduced file system degradation due to network failures. Every VM comes with 1000 Mbps networking speed, 25 GB primary local disk storage for the OS file system, and 100 GB secondary local disk storage for data such as the container runtime and the `kubelet`. Local storage on the worker node is for short-term processing only, and the primary and secondary disks are wiped when you update or reload the worker node. For persistent storage solutions, see [Planning highly available persistent storage](/docs/containers?topic=containers-storage_planning#storage_planning).

**What if I have older machine types?**</br>
If your cluster has deprecated `x1c` or older Ubuntu 16 `x2c` worker node flavors, you can [update your cluster to have Ubuntu 18 `x3c` worker nodes](/docs/containers?topic=containers-update#machine_type).

**What virtual machine flavors are available?**</br>
Worker node flavors vary by zone. The following table includes the most recent version of a flavor, such as `x3c` Ubuntu 18 worker nodes flavors, as opposed to the older `x2c` Ubuntu 16 worker node flavors. To see the flavors available in your zone, run . You can also review available [bare metal](#bm) or [SDS](#sds) machine types.



{: #vm-table}
<table>
<caption>Available virtual machine types in {{site.data.keyword.containerlong_notm}}.</caption>
<thead>
<th>Name and use case</th>
<th>Cores / Memory</th>
<th>Primary / Secondary disk</th>
<th>Network speed</th>
</thead>
<tbody>
<tr>
<td><strong>Virtual, u3c.2x4</strong>: Use this smallest size VM for quick testing, proofs of concept, and other light workloads.<p class="note">Available for only Kubernetes clusters. Not available for OpenShift clusters.</p></td>
<td>2 / 4 GB</td>
<td>25 GB / 100 GB</td>
<td>1000 Mbps</td>
</tr>
<tr>
<td><strong>Virtual, b3c.4x16</strong>: Select this balanced VM for testing and development, and other light workloads.</td>
<td>4 / 16 GB</td>
<td>25 GB / 100 GB</td>
<td>1000 Mbps</td>
</tr>
<tr>
<td><strong>Virtual, b3c.16x64</strong>: Select this balanced VM for mid-sized workloads.</td></td>
<td>16 / 64 GB</td>
<td>25 GB / 100 GB</td>
<td>1000 Mbps</td>
</tr>
<tr>
<td><strong>Virtual, b3c.32x128</strong>: Select this balanced VM for mid to large workloads, such as a database and a dynamic website with many concurrent users.</td>
<td>32 / 128 GB</td>
<td>25 GB / 100 GB</td>
<td>1000 Mbps</td>
</tr>
<tr>
<td><strong>Virtual, c3c.16x16</strong>: Use this flavor when you want an even balance of compute resources from the worker node for light workloads.</td>
<td>16 / 16 GB</td>
<td>25 GB / 100 GB</td>
<td>1000 Mbps</td>
</tr><tr>
<td><strong>Virtual, c3c.16x32</strong>: Use this flavor when you want a 1:2 ratio of CPU and memory resources from the worker node for light to mid-sized workloads.</td>
<td>16 / 32 GB</td>
<td>25 GB / 100 GB</td>
<td>1000 Mbps</td>
</tr><tr>
<td><strong>Virtual, c3c.32x32</strong>: Use this flavor when you want an even balance of compute resources from the worker node for mid-sized workloads.</td>
<td>32 / 32 GB</td>
<td>25 GB / 100 GB</td>
<td>1000 Mbps</td>
</tr><tr>
<td><strong>Virtual, c3c.32x64</strong>: Use this flavor when you want a 1:2 ratio of CPU and memory resources from the worker node for mid-sized workloads.</td>
<td>32 / 64 GB</td>
<td>25 GB / 100 GB</td>
<td>1000 Mbps</td>
</tr>
<tr>
<td><strong>Virtual, m3c.8x64</strong>: Use this flavor when you want a 1:8 ratio of CPU and memory resources for light to mid-sized workloads that require more memory, similar to databases such as {{site.data.keyword.Db2_on_Cloud_short}}. Available only in Dallas and as `--hardware shared` tenancy.</td>
<td>8 / 64 GB</td>
<td>25 GB / 100 GB</td>
<td>1000 Mbps</td>
</tr><tr>
<td><strong>Virtual, m3c.16x128</strong>: Use this flavor when you want a 1:8 ratio of CPU and memory resources for mid-sized workloads that require more memory, similar to databases such as {{site.data.keyword.Db2_on_Cloud_short}}. Available only in Dallas and as `--hardware shared` tenancy.</td>
<td>16 / 128 GB</td>
<td>25 GB / 100 GB</td>
<td>1000 Mbps</td>
</tr><tr>
<td><strong>Virtual, m3c.30x240</strong>: Use this flavor when you want a 1:8 ratio of CPU and memory resources for mid to large-sized workloads that require more memory, similar to databases such as {{site.data.keyword.Db2_on_Cloud_short}}. Available only in Dallas and as `--hardware shared` tenancy.</td>
<td>30 / 240 GB</td>
<td>25 GB / 100 GB</td>
<td>1000 Mbps</td>
</tr>
<tr>
<td><strong>Virtual, z1.2x4</strong>: Use this flavor when you want a worker node to be created on Hyper Protect Containers on IBM Z Systems.</td>
<td>2 / 4 GB</td>
<td>25 GB / 100 GB</td>
<td>1000 Mbps</td>
</tr>
</tbody>
</table>

## Physical machines (bare metal)
{: #bm}

You can provision your worker node as a single-tenant physical server, also referred to as bare metal.
{: shortdesc}

**How is bare metal different than VMs?**</br>
Bare metal gives you direct access to the physical resources on the machine, such as the memory or CPU. This setup eliminates the virtual machine hypervisor that allocates physical resources to virtual machines that run on the host. Instead, all of a bare metal machine's resources are dedicated exclusively to the worker, so you don't need to worry about "noisy neighbors" sharing resources or slowing down performance. Physical machine types have more local storage than virtual, and some have RAID to increase data availability. Local storage on the worker node is for short-term processing only, and the primary and secondary disks are wiped when you update or reload the worker node. For persistent storage solutions, see [Planning highly available persistent storage](/docs/containers?topic=containers-storage_planning#storage_planning).

**Besides better specs for performance, can I do something with bare metal that I can't with VMs?**</br>
Yes, with bare metal worker nodes, you can use {{site.data.keyword.datashield_full}}. {{site.data.keyword.datashield_short}} is integrated with Intel® Software Guard Extensions (SGX) and Fortanix® technology so that your {{site.data.keyword.Bluemix_notm}} container workload code and data are protected in use. The app code and data run in CPU-hardened enclaves. CPU-hardened enclaves are trusted areas of memory on the worker node that protect critical aspects of the app, which helps to keep the code and data confidential and unmodified. If you or your company require data sensitivity due to internal policies, government regulations, or industry compliance requirements, this solution might help you to move to the cloud. Example use cases include financial and healthcare institutions, or countries with government policies that require on-premises cloud solutions.

**Bare metal sounds awesome! What's stopping me from ordering one right now?**</br>
Bare metal servers are more expensive than virtual servers, and are best suited for high-performance apps that need more resources and host control.

Bare metal servers are billed monthly. If you cancel a bare metal server before the end of the month, you are charged through the end of that month. After you order or cancel a bare metal server, the process is completed manually in your IBM Cloud infrastructure account. Therefore, it can take more than one business day to complete.
{: important}

**What bare metal flavors can I order?**</br>
Worker node flavors vary by zone. The following table includes the most recent version of a flavor, such as `x3c` Ubuntu 18 worker nodes flavors, as opposed to the older `x2c` Ubuntu 16 worker node flavors. To see the flavors available in your zone, run . You can also review available [VM](#vm) or [SDS](#sds) machine types.

Bare metal machines are optimized for different use cases such as RAM-intensive, data-intensive, or GPU-intensive workloads.

Choose a machine type with the right storage configuration to support your workload. Some flavors have a mix of the following disks and storage configurations. For example, some flavors might have a SATA primary disk with a raw SSD secondary disk.

* **SATA**: A magnetic spinning disk storage device that is often used for the primary disk of the worker node that stores the OS file system.
* **SSD**: A solid-state drive storage device for high-performance data.
* **Raw**: The storage device is unformatted and the full capacity is available for use.
* **RAID**: A storage device with data distributed for redundancy and performance that varies depending on the RAID level. As such, the disk capacity that is available for use varies.

{: #bm-table}
<table>
<caption>Available bare metal machine types in {{site.data.keyword.containerlong_notm}}.</caption>
<thead>
<th>Name and use case</th>
<th>Cores / Memory</th>
<th>Primary / Secondary disk</th>
<th>Network speed</th>
</thead>
<tbody>
<tr>
<td><strong>RAM-intensive bare metal, mr3c.28x512</strong>: Maximize the RAM available to your worker nodes.</td>
<td>28 / 512 GB</td>
<td>2 TB SATA / 960 GB SSD</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>GPU bare metal, mg3c.16x128</strong>: Choose this type for mathematically intensive workloads such as high-performance computing, machine learning, or 3D applications. This flavor has one Tesla K80 physical card that has two graphics processing units (GPUs) per card for a total of two GPUs.</td>
<td>16 / 128 GB</td>
<td>2 TB SATA / 960 GB SSD</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>GPU bare metal, mg3c.28x256</strong>: Choose this type for mathematically intensive workloads such as high-performance computing, machine learning, or 3D applications. This flavor has two Tesla K80 physical cards that have two GPUs per card for a total of four GPUs.</td>
<td>28 / 256 GB</td>
<td>2 TB SATA / 960 GB SSD</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>Data-intensive bare metal, md3c.16x64.4x4tb</strong>: Use this type for a significant amount of local disk storage, including RAID to increase data availability, for workloads such as distributed file systems, large databases, and big data analytics.</td>
<td>16 / 64 GB</td>
<td>2x2 TB RAID1 / 4x4 TB SATA RAID10</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>Data-intensive bare metal, md3c.28x512.4x4tb</strong>: Use this type for a significant amount of local disk storage, including RAID to increase data availability, for workloads such as distributed file systems, large databases, and big data analytics..</td>
<td>28 / 512 GB</td>
<td>2x2 TB RAID1 / 4x4 TB SATA RAID10</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>Balanced bare metal, mb3c.4x32</strong>: Use for balanced workloads that require more compute resources than virtual machines offer. This flavor can also be enabled with Intel® Software Guard Extensions (SGX) so that you can use <a href="/docs/services/data-shield?topic=data-shield-getting-started#getting-started" target="_blank">{{site.data.keyword.datashield_short}}<img src="../icons/launch-glyph.svg" alt="External link icon"></a> to encrypt your data memory.</td>
<td>4 / 32 GB</td>
<td>2 TB SATA / 2 TB SATA</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>Balanced bare metal, mb3c.16x64</strong>: Use for balanced workloads that require more compute resources than virtual machines offer.</td>
<td>16 / 64 GB</td>
<td>2 TB SATA / 960 GB SSD</td>
<td>10000 Mbps</td>
</tr>
<tr>
</tbody>
</table>

## Software-defined storage (SDS) machines
{: #sds}

Software-defined storage (SDS) flavors are physical machines that are provisioned with additional raw disks for physical local storage. Unlike the primary and secondary local disk, these raw disks are not wiped during a worker node update or reload. Because data is co-located with the compute node, SDS machines are suited for high-performance workloads.
{: shortdesc}

**When do I use SDS flavors?**</br>
You typically use SDS machines in the following cases:
*  If you use an SDS add-on such as [Portworx](/docs/containers?topic=containers-portworx#portworx) to the cluster, use an SDS machine.
*  If your app is a [StatefulSet ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/) that requires local storage, you can use SDS machines and provision [Kubernetes local persistent volumes (beta) ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/blog/2018/04/13/local-persistent-volumes-beta/).
*  If you have custom apps that require additional raw local storage.

For more storage solutions, see [Planning highly available persistent storage](/docs/containers?topic=containers-storage_planning#storage_planning).

**What SDS flavors can I order?**</br>
Worker node flavors vary by zone. The following table includes the most recent version of a flavor, such as `x3c` Ubuntu 18 worker nodes flavors, as opposed to the older `x2c` Ubuntu 16 worker node flavors. To see the flavors available in your zone, run . You can also review available [bare metal](#bm) or [VM](#vm) machine types.

Choose a machine type with the right storage configuration to support your workload. Some flavors have a mix of the following disks and storage configurations. For example, some flavors might have a SATA primary disk with a raw SSD secondary disk.

* **SATA**: A magnetic spinning disk storage device that is often used for the primary disk of the worker node that stores the OS file system.
* **SSD**: A solid-state drive storage device for high-performance data.
* **Raw**: The storage device is unformatted and the full capacity is available for use.
* **RAID**: A storage device with data distributed for redundancy and performance that varies depending on the RAID level. As such, the disk capacity that is available for use varies.

{: #sds-table}
<table>
<caption>Available SDS machine types in {{site.data.keyword.containerlong_notm}}.</caption>
<thead>
<th>Name and use case</th>
<th>Cores / Memory</th>
<th>Primary / Secondary disk</th>
<th>Additional raw disks</th>
<th>Network speed</th>
</thead>
<tbody>
<tr>
<td><strong>Bare metal with SDS, ms3c.4x32.1.9tb.ssd</strong>: If you need extra local storage for performance, use this disk-heavy flavor that supports software-defined storage (SDS).</td>
<td>4 / 32 GB</td>
<td>2 TB SATA / 960 GB SSD</td>
<td>1.9 TB Raw SSD (device path: `/dev/sdc`)</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>Bare metal with SDS, ms3c.16x64.1.9tb.ssd</strong>: If you need extra local storage for performance, use this disk-heavy flavor that supports software-defined storage (SDS).</td>
<td>16 / 64 GB</td>
<td>2 TB SATA / 960 GB SSD</td>
<td>1.9 TB Raw SSD (device path: `/dev/sdc`)</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>Bare metal with SDS, ms3c.28x256.3.8tb.ssd</strong>: If you need extra local storage for performance, use this disk-heavy flavor that supports software-defined storage (SDS).</td>
<td>28 / 256 GB</td>
<td>2 TB SATA / 1.9 TB SSD</td>
<td>3.8 TB Raw SSD (device path: `/dev/sdc`)</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>Bare metal with SDS, ms3c.28x512.4x3.8tb.ssd</strong>: If you need extra local storage for performance, use this disk-heavy flavor that supports software-defined storage (SDS).</td>
<td>28 / 512 GB</td>
<td>2 TB SATA / 1.9 TB SSD</td>
<td>4 disks, 3.8 TB Raw SSD (device paths: `/dev/sdc`, `/dev/sdd`, `/dev/sde`, `/dev/sdf`)</td>
<td>10000 Mbps</td>
</tr>
</tbody>
</table>

## Worker node resource reserves
{: #resource_limit_node}

{{site.data.keyword.containerlong_notm}} sets compute resource reserves that limit available compute resources on each worker node. Reserved memory and CPU resources cannot be used by pods on the worker node, and reduces the allocatable resources on each worker node. When you initially deploy pods, if the worker node does not have enough allocatable resources, the deployment fails. Further, if pods exceed the worker node resource limit, the pods are evicted. In Kubernetes, this limit is called a [hard eviction threshold ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/tasks/administer-cluster/out-of-resource/#hard-eviction-thresholds).
{:shortdesc}

If less CPU or memory is available than the worker node reserves, Kubernetes starts to evict pods to restore sufficient compute resources. The pods reschedule onto another worker node if a worker node is available. If your pods are evicted frequently, add more worker nodes to your cluster or set [resource limits ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#resource-requests-and-limits-of-pod-and-container) on your pods.

The resources that are reserved on your worker node depend on the amount of CPU and memory that your worker node comes with. {{site.data.keyword.containerlong_notm}} defines memory and CPU tiers as shown in the following tables. If your worker node comes with compute resources in multiple tiers, a percentage of your CPU and memory resources is reserved for each tier.

To review how much compute resources are currently used on your worker node, run [`{[kubectl]} top node` ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/reference/kubectl/overview/#top).
{: tip}

| Memory tier | % or amount reserved | <code>b3c.4x16</code> worker node (16 GB) example | <code>mg1c.28x256</code> worker node (256 GB) example|
|:-----------------|:-----------------|:-----------------|:-----------------|
| First 4 GB (0 - 4 GB) | 25% of memory | 1 GB | 1 GB|
| Next 4 GB (5 - 8 GB) | 20% of memory | 0.8 GB | 0.8 GB|
| Next 8 GB (9 - 16 GB) | 10% of memory | 0.8 GB | 0.8 GB|
| Next 112 GB (17 - 128 GB) | 6% of memory | N/A | 6.72 GB|
| Remaining GBs (129 GB+) | 2% of memory | N/A | 2.54 GB|
| Additional reserve for [`kubelet` eviction ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/tasks/administer-cluster/out-of-resource/) | 100 MB | 100 MB (flat amount) | 100 MB (flat amount)|
| **Total reserved** | **(varies)** | **2.7 GB of 16 GB total** | **11.96 GB of 256 GB total**|
{: class="simple-tab-table"}
{: caption="Worker node memory reserves by tier" caption-side="top"}
{: #worker-memory-reserves}
{: tab-title="Worker node memory reserves by tier"}
{: tab-group="Worker Node"}

| CPU tier | % or amount reserved | <code>b3c.4x16</code> worker node (four cores) example | <code>mg1c.28x256</code> worker node (28 cores) example|
|:-----------------|:-----------------|:-----------------|:-----------------|
| First core (Core 1) | 6% cores | 0.06 cores | 0.06 cores|
| Next two cores (Cores 2 - 3) | 1% cores | 0.02 cores | 0.02 cores|
| Next two cores (Cores 4 - 5) | 0.5% cores | 0.005 cores | 0.01 cores|
| Remaining cores (Cores 6+) | 0.25% cores | N/A | 0.0575 cores|
| **Total reserved** | **(varies)** | **0.085 cores of four cores total** | **0.1475 cores of 28 cores total**|
{: class="simple-tab-table"}
{: caption="Worker node CPU reserves by tier" caption-side="top"}
{: #worker-cpu-reserves}
{: tab-title="Worker node CPU reserves by tier"}
{: tab-group="Worker Node"}



