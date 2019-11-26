---

copyright:
  years: 2014, 2019
lastupdated: "2019-11-26"

keywords: openshift, roks, rhos, rhoks, multi az, multi-az, szr, mzr

subcollection: openshift

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

# Planning your cluster for high availability
{: #ha_clusters}

Design your standard cluster for maximum availability and capacity for your app with {{site.data.keyword.openshiftlong}}.
{: shortdesc}

Your users are less likely to experience downtime when you distribute your apps across multiple worker nodes, zones, and clusters. Built-in capabilities, like load balancing and isolation, increase resiliency against potential failures with hosts, networks, or apps. Review these potential cluster setups that are ordered with increasing degrees of availability.

![High availability for clusters](images/cs_cluster_ha_roadmap_multizone_public.png)

1. A [single zone cluster](#single_zone) with multiple worker nodes in a worker pool.
2. A [multizone cluster](#multizone) that spreads worker nodes across zones within one region.
3. **Clusters with public network connectivity**: [Multiple clusters](#multiple_clusters) that are set up across zones or regions and that are connected via a global load balancer.


## Single zone cluster
{: #single_zone}

Single zone clusters can be created in one of the supported [single zone cities or multizone metro locations](/docs/openshift?topic=openshift-regions-and-zones#zones). To improve availability for your app and to allow failover for the case that one worker node is not available in your cluster, add additional worker nodes to your single zone cluster.
{: shortdesc}<roks311-vpc>

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC clusters are supported only in [multizone metro locations](/docs/openshift?topic=openshift-regions-and-zones#zones). If your cluster must reside in one of the single zone cities, create a classic cluster instead.
{: note}</roks311-vpc>

<img src="images/cs_cluster_singlezone.png" alt="High availability for clusters in a single zone" width="230" style="width:230px; border-style: none"/>

You can add more worker nodes to your cluster by [resizing an existing worker pool](/docs/openshift?topic=openshift-add_workers#resize_pool) or by [adding a new worker pool](/docs/openshift?topic=openshift-add_workers#add_pool). When you add more worker nodes, app instances can be distributed across multiple worker nodes. If one worker node goes down, app instances on available worker nodes continue to run. OpenShift automatically reschedules pods from unavailable worker nodes to ensure performance and capacity for your app. To ensure that your pods are evenly distributed across worker nodes, implement [pod affinity](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#inter-pod-affinity-and-anti-affinity-beta-feature).

**Is my master highly available in a single zone cluster?**</br>
If your cluster is created in a single zone city, the Kubernetes master of your classic cluster is highly available and includes replicas on separate physical hosts for your master API server, etcd, scheduler, and controller manager to protect against an outage such as during a master update. If your cluster resides in one of the multizone metro locations, the master is automatically deployed with three replicas and spread across the zones of the metro.

**How can I protect my workloads against a single zone failure?** </br>
If your single zone cluster is created in one of the [multizone metro location](/docs/openshift?topic=openshift-regions-and-zones#zones), you can change your single zone cluster to a [multizone cluster](#multizone). In a multizone cluster, your workloads are distributed across worker nodes in different zones. If one zone is not available, your workloads continue to run in the remaining zones. If you prefer single zone clusters for simplified management, or if your cluster must reside in a specific [single zone city](/docs/openshift?topic=openshift-regions-and-zones#zones) that does not support multizone capabilities, you can create [multiple clusters](#multiple_clusters) and connect them with a global load balancer.

## Multizone cluster
{: #multizone}

Create a multizone cluster to distribute your workloads across multiple worker nodes and zones, and protect against zone failures with hosts, networks, or apps. If resources in one zone go down, your cluster workloads continue to run in the other zones.
{: shortdesc}

<img src="images/cs_cluster_multizone-ha.png" alt="High availability for multizone clusters" width="500" style="width:500px; border-style: none"/>

In a multizone cluster, the worker nodes in your worker pools are replicated across multiple zones within one region. Multizone clusters are designed to evenly schedule pods across worker nodes and zones to assure availability and failure recovery. If worker nodes are not spread evenly across the zones or capacity is insufficient in one of the zones, the Kubernetes scheduler or OpenShift controller might fail to schedule all requested pods. As a result, pods might go into a **Pending** state until enough capacity is available. If you want to change the default behavior to make Kubernetes scheduler or OpenShift controller distribute pods across zones in a best effort distribution, use the `preferredDuringSchedulingIgnoredDuringExecution` [pod affinity policy](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#inter-pod-affinity-and-anti-affinity-beta-feature).

<p class="note">You can create a multizone cluster in one of the supported [multizone metro locations](/docs/openshift?topic=openshift-regions-and-zones#zones) only.</p>

**Why do I need worker nodes in three zones?** </br>
Distributing your work load across three zones ensures high availability for your app in case one or two zones are not available, but it also makes your cluster setup more cost-efficient. Why is that, you ask? Here is an example.

Let's say you need a worker node with six cores to handle the workload for your app. To make your cluster more available, you have the following options:

- **Duplicate your resources in another zone:** This option leaves you with two worker nodes, each with six cores in each zone for a total of 12 cores. </br>
- **Distribute resources across three zones:** With this option, you deploy three cores per zone, which leaves you with a total capacity of nine cores. To handle your workload, two zones must be up at a time. If one zone is unavailable, the other two zones can fully handle your six-core workload. If two zones are unavailable, the three remaining cores are up to handle your parts of your workload, and you could temporarily add another worker node to that zone. Deploying three cores per zone means smaller machines and hence reduced cost for you.</br>

**How is my OpenShift master set up?** </br>
When you create a cluster in a [multizone metro location](/docs/openshift?topic=openshift-regions-and-zones#zones), a highly available master is automatically deployed and three replicas are spread across the zones of the metro. For example, if the cluster is in `dal10`, `dal12`, or `dal13` zones, the replicas of the master are spread across each zone in the Dallas multizone metro.

**Do I have to do anything so that the master can communicate with the workers across zones?**</br>
<roks311-vpc>If you created a VPC multizone cluster, the subnets in each zone are automatically set up with Access Control Lists (ACLs) that allow communication between the master and the worker nodes across zones. </roks311-vpc>In classic clusters, if you have multiple VLANs for your cluster, multiple subnets on the same VLAN, or a multizone classic cluster, you must enable a [Virtual Router Function (VRF)](/docs/resources?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) for your IBM Cloud infrastructure account so your worker nodes can communicate with each other on the private network. To enable VRF, [contact your IBM Cloud infrastructure account representative](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). To check whether a VRF is already enabled, use the `ibmcloud account show` command. If you cannot or do not want to enable VRF, enable [VLAN spanning](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). To perform this action, you need the **Network > Manage Network VLAN Spanning** [infrastructure permission](/docs/openshift?topic=openshift-users#infra_access), or you can request the account owner to enable it. To check whether VLAN spanning is already enabled, use the `ibmcloud oc vlan spanning get --region <region>` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vlan_spanning_get).

**Can I convert my single zone cluster to a multizone cluster?**</br>
To convert a single zone cluster to a multizone cluster, your cluster must be set up in one of the supported [multizone metro locations](/docs/openshift?topic=openshift-regions-and-zones#zones). <roks311-vpc>VPC clusters can be set up only in multizone metro locations, and as such can always be converted from a single zone cluster to a multizone cluster. </roks311-vpc>C<roks311-vpc>lassic c</roks311-vpc>lusters that are set up in a single zone data center cannot be converted to a multizone cluster. To convert a single zone cluster to a multizone cluster, see [Adding worker nodes by adding a zone to a worker pool](/docs/openshift?topic=openshift-add_workers#add_zone).




## Multiple public clusters connected with a global load balancer
{: #multiple_clusters}

To protect your app from a master failure or for classic clusters that must reside in one of the supported [single zone cities](/docs/openshift?topic=openshift-regions-and-zones#zones), you can create multiple clusters in different zones within a region and connect them with a global load balancer.
{: shortdesc}

To connect multiple clusters with a global load balancer, the clusters must be set up with public network connectivity.
{: note}

<img src="images/cs_multiple_cluster_zones.png" alt="High availability for multiple clusters" width="700" style="width:700px; border-style: none"/>

To balance your workload across multiple clusters, you must set up a global load balancer and add the public IP addresses of your application load balancers (ALBs) or load balancer services to your domain. By adding these IP addresses, you can route incoming traffic between your clusters. For the global load balancer to detect if one of your clusters is unavailable, consider adding a ping-based health check to every IP address. When you set up this check, your DNS provider regularly pings the IP addresses that you added to your domain. If one IP address becomes unavailable, then traffic is not sent to this IP address anymore. However, OpenShift does not automatically restart pods from the unavailable cluster on worker nodes in available clusters. If you want OpenShift to automatically restart pods in available clusters, consider setting up a [multizone cluster](#multizone).

**Why do I need 3 clusters in three zones?** </br>
Similar to using [3 zones in multizone clusters](#multizone), you can provide more availability to your app by setting up three clusters across zones. You can also reduce costs by purchasing smaller machines to handle your workload.

**What if I want to set up multiple clusters across regions?** </br>
You can set up multiple clusters in different regions of one geolocation (such as US South and US East) or across geolocations (such as US South and EU Central). Both setups offer the same level of availability for your app, but also add complexity when it comes to data sharing and data replication. For most cases, staying within the same geolocation is sufficient. But if you have users across the world, it might be better to set up a cluster where your users are so that your users do not experience long waiting times when they send a request to your app.

**What options do I have to load balance workloads across multiple clusters?** </br>
To load balance workloads across multiple clusters, you must make your apps available on the public network by using [Application Load Balancers (ALBs)](/docs/openshift?topic=openshift-ingress-about) or [Network Load Balancers (NLBs)](/docs/openshift?topic=openshift-loadbalancer-about). The ALBs and NLBs are assigned a public IP address that you can use to access your apps.

To load balance workloads across your apps, add the public IP addresses of your ALBs and NLBs to a CIS global load balancer or your own global load balancer.

**To use a CIS global load balancer**:
1.  Set up the service by following steps 1 - 5 in [Getting Started with {{site.data.keyword.cloud_notm}} Internet Services (CIS)](/docs/infrastructure/cis?topic=cis-getting-started#getting-started). These steps walk you through provisioning the service instance, adding your app domain, and configuring your name servers, and creating DNS records. Create a DNS record for each ALB or NLB IP address that you collected. These DNS records map your app domain to all of your cluster ALBs or NLBs, and ensure that requests to your app domain are forwarded to your clusters in a round-robin cycle.
2. [Add health checks](/docs/infrastructure/cis?topic=cis-set-up-and-configure-your-load-balancers#add-a-health-check) for the ALBs or NLBs. You can use the same health check for the ALBs or NLBs in all of your clusters, or create specific health checks to use for specific clusters.
3. [Add an origin pool](/docs/infrastructure/cis?topic=cis-set-up-and-configure-your-load-balancers#add-a-pool) for each cluster by adding the cluster's ALB or NLB IPs. For example, if you have 3 clusters that each have two ALBs, create three origin pools that each have twp ALB IP addresses. Add a health check to each origin pool that you create.
4. [Add a global load balancer](/docs/infrastructure/cis?topic=cis-set-up-and-configure-your-load-balancers#set-up-and-configure-your-load-balancers).

**To use your own global load balancer**:
1. Configure your domain to route incoming traffic to your ALB or NLB services by adding the IP addresses of all public enabled ALBs and NLB services to your domain.
2. For each IP address, enable a ping-based health check so that your DNS provider can detect unhealthy IP addresses. If an unhealthy IP address is detected, traffic is not routed to this IP address anymore.

**What if I want to load balance workloads on the private network?** </br>
{{site.data.keyword.cloud_notm}} does not offer a load balancer service on the private network. However, you can connect your cluster to a private load balancer that you host in your on-prem network by using one of the [supported VPN options](/docs/openshift?topic=openshift-vpn). Make sure to expose your apps on the private network by using [Application Load Balancers (ALBs)](/docs/openshift?topic=openshift-ingress-about) or [Network Load Balancers (NLBs)](/docs/openshift?topic=openshift-loadbalancer-about), and use the private IP address in your VPN settings to connect your app to your on-prem network.




