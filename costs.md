---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-21"

keywords: oks, iro, openshift, red hat, red hat openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Understanding costs for your clusters
{: #costs}

With {{site.data.keyword.cloud}}, you can plan for, estimate, review, and modify your cluster environment to control costs. Just by using a managed service like {{site.data.keyword.openshiftlong}}, you are saving many expenses that are associated with managing, updating, and maintaining an infrastructure environment.
{: shortdesc}

## Understanding costs by component
{: #costs-for-clusters}

With {{site.data.keyword.openshiftlong_notm}} clusters, you can use IBM Cloud infrastructure compute, networking, and storage resources with platform services such as {{site.data.keyword.watson}} AI or Compose Database-as-a-Service. Each resource might entail its own charges that can be [fixed, metered, tiered, or reserved](/docs/billing-usage?topic=billing-usage-charges#charges) and billed by various incremental rates such as monthly or hourly.
{: shortdesc}

Monthly resources are billed based on the first of the month for usage in the preceding month. If you order a monthly resource in the middle of the month, you are charged a prorated amount for that month. However, if you cancel a resource in the middle of the month, you are still charged the full amount for the monthly resource.
{: note}

### Worker nodes
{: #nodes}

Clusters can have two main types of worker nodes: virtual or physical (bare metal) machines. Flavor (machine type) availability and pricing varies by the zone that you deploy your cluster to.
{: shortdesc}

**When do worker nodes begin to incur charges?**

Worker nodes begin to incur charges after they successfully complete the `provisioning` state and continue until you delete the worker nodes and they complete the `deleting` state. For more information, see [Worker node states](/docs/containers?topic=containers-health-monitor#states).

**What is the difference between virtual and physical machines?**


**Virtual machines** feature greater flexibility, quicker provisioning times, and more automatic scalability features than bare metal, at a more cost-effective price than bare-metal. However, VMs have a performance trade-off when compared to bare metal specs, such as networking Gbps, RAM and memory thresholds, and storage options. Keep in mind these factors that impact your VM costs.
* **Shared vs. dedicated**: If you share the underlying hardware of the VM, the cost is lower than dedicated hardware, but the physical resources are not dedicated to your VM. VPC clusters are available only as **shared**.
* **Hourly billing only**: Hourly billing offers more flexibility to order and cancel VMs quickly. You are charged an hourly rate that is metered for only the time that that the worker node is provisioned. The time is not rounded up or down to the nearest hour, but is metered in minutes and charged at the hourly rate. For example, if your worker node is provisioned for 90 minutes, you are charged the hourly rate for 1.5 hours, not 2 hours.
* **Tiered hours per month**: The [pricing](https://cloud.ibm.com/kubernetes/catalog/about#pricing){: external} is billed hourly in [graduated tiered](/docs/billing-usage?topic=billing-usage-charges#graduated_tier). As your VM remains ordered for a tier of hours within a billing month, the hourly rate that you are charged lowers. The tiers of hours are as follows:
    * 0 - 150 hours
    * 151 - 290 hours
    * 291 - 540 hours
    * 541+ hours

**Physical machines, or bare metal, (not available for VPC clusters)** yield high-performance benefits for workloads such as data, GPU, and AI. Additionally, all the hardware resources are dedicated to your workloads, so you don't have "noisy neighbors". Keep in mind these factors that impact your bare metal costs.
* **Monthly billing only**: All bare metals are charged monthly.
* **Longer ordering process**: After you order or cancel a bare metal server, the process is completed manually in your IBM Cloud infrastructure account. Therefore, it can take more than one business day to complete.

    ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) **VPC Generation 2 only**: Prices vary by region where the underlying worker node infrastructure resides, and you can get sustained usage discounts. For more information, see [What are the regional uplift charges and sustained usage discounts for VPC worker nodes?](#charges_vpc_gen2).
    {: note}

For more information about worker node specifications, see [Available hardware for worker nodes](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes).



### Compute licenses
{: #licenses}

In {{site.data.keyword.openshiftlong_notm}}, worker nodes require OpenShift Container Platform licenses to cover the use of Red Hat OpenShift Container Platform and Red Hat Enterprise Linux. OpenShift Container Platform licenses can be supplied by an [existing {{site.data.keyword.cloud_notm}} Pak entitlement](#licenses-cloud-pak) or [on-demand by {{site.data.keyword.openshiftlong_notm}}](#licenses-on-demand).
{: shortdesc}

#### On-demand OCP licenses from {{site.data.keyword.openshiftlong_notm}}
{: #licenses-on-demand}

When you create worker nodes by adding a worker pool or cluster, {{site.data.keyword.openshiftlong_notm}} helps you include the purchase of OpenShift Container Platform licenses for the worker nodes. The way that these OpenShift Container Platform licenses are billed varies by the type of OpenShift Container Platform licenses that the worker nodes have.
{: shortdesc}

* [New OCP licenses](#licenses-on-demand-new) with reduced pricing, available 9 November 2020. Create a cluster or worker pool with the latest flavors to use the new OCP licenses.
* **Deprecated**: [Old OCP licenses](#licenses-on-demand-old) for existing worker nodes before 9 November 2020 or deprecated bare metal flavors. [Migrate](#licenses-on-demand-migrate) your existing worker nodes to take advantage of the new OCP licenses.

##### New OCP licenses with reduced pricing, available 9 November 2020
{: #licenses-on-demand-new}

New OCP licenses include reduced pricing from Red Hat. An {{site.data.keyword.openshiftshort}} license is billed for every two virtual cores (or one physical cores) of the worker node flavor. Charges vary by the type of worker node that you have, for as long as you have the worker node. For more information, see the [{{site.data.keyword.cloud_notm}} blog](https://www.ibm.com/cloud/blog/announcements/run-workloads-by-the-hour-with-red-hat-openshift-on-ibm-cloud){: external}.

* **Virtual machines (VMs)**: The OCP licenses are billed hourly. For example, you create a worker pool with VMs, test an app for 3 days, and then delete the worker pool. You are billed for only the hours that your worker nodes were deployed.
* **Physical machines (bare metal)**: The OCP licenses are prorated for the first month that you create the worker nodes in, and then billed monthly for the remaining lifecycle of the worker node. For example, you create a cluster with bare metal worker nodes on 15 August and delete the cluster on 14 September. You are charged a prorated monthly cost for the first month of August, but the full monthly cost for September.

When you estimate the cost of a new cluster or worker node, the OCP licenses are included as part of the worker node cost. The OCP licenses are also part of the worker node plan and listed as a sub-item of the worker nodes in your {{site.data.keyword.cloud_notm}} bill.

##### Deprecated: Old OCP licenses for existing worker nodes before 9 November 2020 or deprecated bare metal flavors
{: #licenses-on-demand-old}

An {{site.data.keyword.openshiftshort}} license is billed for every four virtual cores (or two physical cores) of the worker node flavor. You are charged for the entire license for each month that you have worker nodes in a `deployed` state. The monthly charge applies to both virtual and physical worker nodes. For example, if you create the cluster on 15 August and delete the cluster on 14 September, you are still charged for the OCP licenses for two monthly periods: August and September.
* If you delete your worker node before the end of the month, your monthly license is available for other worker nodes in the same cluster. If the other worker nodes are not the same CPU size, you need additional licenses.
* If you delete the cluster before the end of the month, you are still charged the entire monthly price for the {{site.data.keyword.openshiftshort}} license.

When you estimate the cost of a new cluster or worker node, the OCP licenses are included as a separate line item. The OCP licenses are also listed as separate plans in your {{site.data.keyword.cloud_notm}} bill.

**How can I migrate from the old to new OCP licenses?**
{: #licenses-on-demand-migrate}

You can follow the same procedure to [update flavors](/docs/openshift?topic=openshift-update#machine_type) by adding new worker pools and removing the old worker pools. If you use bare metal, make sure that you use the latest series 4 flavors. Many existing bare metal flavors don't support the new OCP licenses.

You can check the new rates in the pricing estimate when you create a cluster or worker pool in the console. The OCP licenses are no longer a separate line item in the estimate, but instead are in the cost of the worker nodes.

#### OCP licenses from Cloud Pak entitlements
{: #licenses-cloud-pak}

When you purchase products such as {{site.data.keyword.cloud_notm}} Paks, your purchase might include OCP licenses. When you create a cluster or worker pool, you can choose to apply your entitlement to cover the cost of the OCP licenses.

Do not exceed your entitlement. Keep in mind that your OpenShift Container Platform entitlements can be used with other cloud providers or in other environments. To avoid billing issues later, make sure that you use only what you are entitled to use. For example, you might have an entitlement for the OCP licenses for two worker nodes of 4 CPU and 16 GB memory, and you create this worker pool with two worker nodes of 4 CPU and 16 GB memory. You used your entire entitlement, and you can't use the same entitlement for other worker pools, cloud providers, or environments.
{: important}



### Public bandwidth
{: #bandwidth}

Bandwidth refers to the public data transfer of inbound and outbound network traffic, both to and from {{site.data.keyword.cloud_notm}} resources in data centers around the globe.
{: shortdesc}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) **Classic clusters**: Public bandwidth is charged per GB. You can review your current bandwidth summary by logging into the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/), from the menu ![Menu icon](../icons/icon_hamburger.svg "Menu icon") selecting **Classic Infrastructure**, and then selecting the **Network > Bandwidth > Summary** page.

Review the following factors that impact public bandwidth charges:
* **Location**: As with worker nodes, charges vary depending on the zone that your resources are deployed in.
* **Pay-As-You-Go for VM**: Because VMs are billed at an hourly rate, your VM worker node machines have a Pay-As-You-Go allocation of outbound networking based on GB usage.
* **Included bandwidth and tiered packages for BM**: Bare metal worker nodes might come with a certain allocation of outbound networking per month that varies by geography: 20 TB for North America and Europe, or 5 TB for Asia Pacific and South America. After you exceed your included bandwidth, you are charged according to a tiered usage scheme for your geography. If you exceed a tier allotment, you might also be charged a standard data transfer fee. For more information, see [Bandwidth packages](https://www.ibm.com/cloud/bandwidth){: external}.

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) **VPC clusters**: For more information about how internet data transfer works in your Virtual Private Cloud, see [Pricing for VPC](https://www.ibm.com/cloud/vpc/pricing){: external}.

### Subnet IP addresses
{: #subnet_ips}

Subnets for {{site.data.keyword.openshiftlong_notm}} clusters vary by infrastructure provider.
{: shortdesc}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) **Classic clusters**: When you create a standard cluster, a portable public subnet with 8 public IP addresses is ordered and charged to your account monthly. For pricing information, see the [Subnets and IPs](/docs/subnets?topic=subnets-pricing-for-ibm-cloud-subnets) documentation or estimate your costs in the [classic subnets console)](https://cloud.ibm.com/classic/network/subnet/provision){: external}.  If you already have available portable public subnets in your infrastructure account, you can use these subnets instead. Create the cluster with the `--no-subnets` [flag](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_create), and then [reuse your subnets](/docs/openshift?topic=openshift-subnets#subnets_custom).

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) **VPC clusters**: For more information about charges for floating IPs and other networking costs, see [Pricing for VPC](https://www.ibm.com/cloud/vpc/pricing){: external}.

### Multizone load balancer
{: #mzlb_pricing}

When you create a multizone cluster or add zones to a single zone cluster, you must have a load balancer to health check Ingress and load balancer IP addresses in each zone, and forward requests to your apps across zones in the region.
{: shortdesc}

The type of load balancer that is automatically created varies depending on the type of cluster. For more information, see [Multizone load balancer (MZLB) or Load Balancer for VPC](/docs/containers?topic=containers-ingress-about#mzlb).
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) **Classic clusters**: An Akamai MZLB is automatically created for each multizone cluster. You can view the hourly rate in the pricing summary when you create the cluster.
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) **VPC clusters**: A Load Balancer for VPC is automatically created in your VPC for your cluster. For cost information, see [Pricing for Load Balancer for VPC](https://www.ibm.com/cloud/vpc/pricing){: external}.



### Default storage for images
{: #storage_images}

To store images in the internal registry, {{site.data.keyword.openshiftlong_notm}} creates a storage instance that varies by infrastructure provider.
{: shortdesc}

* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) **Classic clusters**: A classic {{site.data.keyword.cloud_notm}} File Storage volume is automatically created for you. Your file storage volume is provisioned with an `ibmc-file-gold` storage class of 100 GB capacity at 10 IOPS/GB, and billed at an hourly rate. If you need more image storage capacity, you can [update the volume size](/docs/openshift?topic=openshift-registry#openshift_internal_registry), which modifies the cost. For more information, see [Pricing](https://www.ibm.com/cloud/file-storage/pricing){: external}.
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) **VPC clusters**: A bucket in an existing {{site.data.keyword.cos_full_notm}} instance is created for you. For more information, see [Billing and pricing in the {{site.data.keyword.cos_short}} documentation](/docs/cloud-object-storage?topic=cloud-object-storage-billing).



### Storage for apps
{: #persistent_storage}

When you provision storage, you can choose the storage type and storage class that is right for your use case. Charges vary depending on the type of storage, the location, and the specs of the storage instance. Some storage solutions, such as file and block storage offer hourly and monthly rates that you can choose from.
{: shortdesc}

To choose the right storage solution, see [Planning highly available persistent storage](/docs/openshift?topic=openshift-storage_planning#storage_planning). For more information, see:
* [NFS file storage pricing](https://www.ibm.com/cloud/file-storage/pricing){: external}
* [Block storage pricing](https://www.ibm.com/cloud/block-storage/pricing){: external}
* [Object storage plans](https://cloud.ibm.com/objectstorage/create#pricing){: external}
* [Portworx Enterprise pricing](https://cloud.ibm.com/catalog/services/portworx-enterprise){: external}

### {{site.data.keyword.cloud_notm}} services
{: #services}

Each service that you integrate with your cluster has its own pricing model. Review each product documentation and use the {{site.data.keyword.cloud_notm}} console to [estimate costs](/docs/billing-usage?topic=billing-usage-cost#cost).
{: shortdesc}

### Operators and other third-party integrations
{: #operators_pricing}

[Operators](/docs/openshift?topic=openshift-operators) and other [third-party integrations](/docs/containers?topic=containers-supported_integrations) are a convenient way to add services to your cluster from community, third-party, your own, or other providers. Keep in mind that you are responsible for additional charges and how these services operate in your cluster, from deployment and maintenance to integration with your apps. If you have issues with an operator or third-party integration, work with the appropriate provider to troubleshoot the issue.
{: shortdesc}

### VPC worker nodes
{: #charges_vpc_gen2}

Pricing for VPC infrastructure varies based on regional location and sustained usage.
{: shortdesc}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) This information applies to VPC worker nodes only.
{: note}

Regional uplift charges
:    When you create a cluster on VPC infrastructure, the worker nodes might incur an uplift charge that varies by the [multizone location](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc) that you create the cluster in. The uplift charge is a percentage (`%`) of the hourly rate (`r`), and is added to the hourly rate of the worker node. The total hourly rate cost for a worker node can be calculated as `r + (r × %)`. In the [{{site.data.keyword.openshiftshort}} cluster creation console](https://cloud.ibm.com/kubernetes/catalog/create?platformType=openshift){: external}, this uplift is reflected in the pricing calculator as you configure your cluster details. The following table describes the pricing uplift by region.

:    For a table that describes the pricing uplift by region, see [Regional pricing for VPC](https://www.ibm.com/cloud/vpc/pricing){: external}.

Sustained usage discounts
:    For virtual server instances that are billed at an hourly rate, discounted prices depend on how long the instance runs during the billing month. For more information, expand the **Sustained usage discounts on {{site.data.keyword.cloud_notm}} {{site.data.keyword.vsi_is_short}}** section on the [Pricing for VPC](https://www.ibm.com/cloud/vpc/pricing){: external} page.

## Estimating costs
{: #costs-estimate}

See [Estimating your costs](/docs/billing-usage?topic=billing-usage-cost#cost).

Keep in mind that some charges are not reflected in the estimate, such as tiered pricing for increased hourly usage. For more information, see [Understanding costs for your clusters](#costs-for-clusters).

## Managing costs
{: #costs-manage}

The following steps present a general process to manage costs for your {{site.data.keyword.openshiftlong_notm}} clusters.
{: shortdesc}

1. Decide on a cloud platform strategy to manage your resources.
    * See [Best practices for billing and usage](/docs/billing-usage?topic=billing-usage-best-practices).
    * Organize your billing with [resource groups](/docs/account?topic=account-rgs).
    * [Add tags to your clusters](/docs/openshift?topic=openshift-add_workers#cluster_tags) according to your organizational strategy.
2. Plan the type of cluster that you need.
    * [Size your cluster to support your workloads](/docs/openshift?topic=openshift-strategy#sizing), including the network bandwidth that your workloads need.
    * [Decide the cluster environment that you want](/docs/openshift?topic=openshift-strategy#kube_env).
    * [Consider the availability that you want for your cluster](/docs/containers?topic=containers-ha_clusters). For example, a basic high availability setup is one multizone cluster with two worker nodes in each of three zones, for a minimum total of 6 worker nodes.
3. Check out other {{site.data.keyword.cloud_notm}} services, add-ons, operators, and other third-party software that you might use that can increase your cost. To get an idea of what other costs clusters typically incur, review [Understanding costs for your clusters](#costs-for-clusters).
4. [Estimate your costs](/docs/billing-usage?topic=billing-usage-cost#cost) and review detailed pricing information for the service, see [{{site.data.keyword.openshiftlong_notm}} Pricing plans](https://cloud.ibm.com/kubernetes/catalog/about?platformType=openshift#pricing){: external}.
5. Manage the lifecycle of your cluster to control costs.
    * Consider [enabling the cluster autoscaler](/docs/containers?topic=containers-ca) to automatically add or remove worker nodes in response to your cluster workload resource requests.
    * Manually [resize your worker pool](/docs/containers?topic=containers-add_workers) to remove worker nodes that you don't need. Keep in mind that you can't scale a worker pool down to zero worker nodes.
    * Use Kubernetes features such as [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/){: external}, [pod priority](/docs/containers?topic=containers-pod_priority), and [resource requests and limits](/docs/containers?topic=containers-app#resourcereq) to control how resources are used within your cluster.
    * Consider setting up a [monitoring tool](/docs/openshift?topic=openshift-health) such as {{site.data.keyword.mon_full_notm}} and creating alerts for your workloads when they need more resources.
6. [View your usage](/docs/billing-usage?topic=billing-usage-viewingusage#viewingusage) to continuously refine how you consume {{site.data.keyword.cloud_notm}} services.
7. [Set spending notifications](/docs/billing-usage?topic=billing-usage-spending).




