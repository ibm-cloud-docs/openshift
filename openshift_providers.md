<roks311-vpc>---

copyright:
  years: 2014, 2019
lastupdated: "2019-11-26"

keywords: openshift, roks, rhos, rhoks, vpc

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

# Supported infrastructure providers
{: #infrastructure_providers}

With {{site.data.keyword.openshiftlong}}, you can create a cluster from a variety of infrastructure providers. All the worker nodes in a cluster must be from the same provider. Originally, Red Hat OpenShift on IBM Cloud provisioned your worker nodes in a single provider, classic infrastructure. As of **19 November 2019**, you can choose from Classic or Virtual Private Cloud (VPC) Generation 1 compute infrastructure providers.

<table summary="The rows are read from left to right, with the area of comparison in column one, classic infrastructure provider in column two, and VPC Generation 1 compute infrastructure provider in column three.">
<caption>Infrastructure providers for Red Hat OpenShift on IBM Cloud clusters</caption>
<col width="20%">
<col width="40%">
<col width="40%">
 <thead>
 <th>Area</th>
 <th>Classic</th>
 <th>VPC Gen 1 compute</th>
 </thead>
 <tbody>
 <tr>
   <td>Overview</td>
   <td>Generally available now, your clusters on IBM Cloud infrastructure Classic include all of the Red Hat OpenShift on IBM Cloud mature and robust features for compute, networking, and storage. To get started, create a [Kubernetes](/docs/containers?topic=containers-cs_cluster_tutorial#cs_cluster_tutorial) or [OpenShift](/docs/openshift?topic=openshift-openshift_tutorial) cluster.</td>
   <td>With the VPC Gen 1 compute, you can create your cluster in the next generation of the {{site.data.keyword.cloud_notm}} platform, in your [Virtual Private Cloud](/docs/vpc-on-classic?topic=vpc-on-classic-about). VPC gives you the security of a private cloud environment with the dynamic scalability of a public cloud. To get started, try out the [VPC Gen 1 compute cluster tutorial](/docs/containers?topic=containers-vpc_ks_tutorial#vpc_ks_tutorial).</td>
 </tr>
 <tr>
  <td>Doc icons</td>
  <td><img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="25" style="width:25px; border-style: none"/> Throughout the documentation, pages and topics might include a note that the content applies only to the classic infrastructure provider.</td>
  <td><img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="25" style="width:25px; border-style: none"/> Throughout the documentation, pages and topics might include a note that the content applies only to the VPC infrastructure provider.</td>
 </tr>
 <tr>
   <td>Compute and worker node resources</td>
   <td>[Virtual](/docs/openshift?topic=openshift-planning_worker_nodes#vm), [bare metal](/docs/openshift?topic=openshift-planning_worker_nodes#bm), and [software-defined storage](/docs/openshift?topic=openshift-planning_worker_nodes#sds) machines are available for your worker nodes. Your worker node instances reside in your IBM Cloud infrastructure account, but you can manage them through Red Hat OpenShift on IBM Cloud. You own the worker node instances.</td>
   <td>VPC Generation 1 compute has a [select group of virtual machines only](/docs/openshift?topic=openshift-planning_worker_nodes#vm) for your worker nodes. Unlike classic clusters, your VPC cluster worker nodes do not appear in your infrastructure portal or a separate infrastructure bill. Instead, you manage all maintenance and billing activity for the worker nodes through Red Hat OpenShift on IBM Cloud. Your worker node instances are connected to certain VPC instances that do reside in your infrastructure account, such as the VPC subnet or storage volumes.</td>
 </tr>
 <tr>
   <td>Security</td>
   <td>Classic clusters have many built-in security features that help you protect your cluster infrastructure, isolate resources, and ensure security compliance. For more information, see [Security in your Virtual Private Cloud](/docs/vpc-on-classic-network?topic=vpc-on-classic-network-security-in-your-ibm-cloud-vpc).</td>
   <td>With VPC, your cluster runs in an isolated environment in the public cloud. Network access control lists protect the subnets that provide the floating IPs for your worker nodes. For more information, see [About Virtual Private Cloud](/docs/vpc-on-classic?topic=vpc-on-classic-about).</td>
 </tr>
 <tr>
   <td>High availability</td>
   <td>For both classic and VPC clusters, the master includes three replicas for high availability. Further, if you create your cluster in a multizone metro, the master replicas are spread across zones and you can also spread your worker pools across zones. For more information, see [High availability for Red Hat OpenShift on IBM Cloud](/docs/openshift?topic=openshift-ha).</td>
   <td>Same as Classic; see [High availability for Red Hat OpenShift on IBM Cloud](/docs/openshift?topic=openshift-ha).</td>
 </tr>
 <tr>
   <td>Cluster administration</td>
   <td>Classic clusters support the entire set of v1 API automation, such as resizing worker pools, reloading worker nodes, and updating masters and worker nodes across major, minor, and patch versions. When you delete a cluster, you can choose to remove any attached subnet or storage instances.</td>
   <td>VPC Gen 1 compute clusters cannot be reloaded or updated. Instead, use the [`worker replace --update` operation](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_replace) to replace worker nodes that are outdated or in a troubled state.</td>
 </tr>
 <tr>
   <td>Cluster networking</td>
   <td>Your worker nodes are provisioned on private VLANs that provide private IP addresses to communicate on the private IBM Cloud infrastructure network. For communication on the public network, you can also provision the worker nodes on a public VLAN. Communication to the cluster master can be on the public or private service endpoint. For more information, see [Understanding cluster network basics](/docs/openshift?topic=openshift-plan_clusters#plan_basics).</td>
   <td>Unlike classic infrastructure, your VPC Gen 1 compute cluster's worker nodes are attached to VPC subnets and assigned private IP addresses. The worker nodes are not connected to the public network, which instead is accessed through a public gateway, floating IP, or VPN gateway. For more information, see [About Networking for VPC](/docs/vpc-on-classic-network?topic=vpc-on-classic-network-about-networking-for-vpc).</td>
 </tr>
 <tr>
   <td>Apps and container platform</td>
  <td>You can choose to create [community Kubernetes or OpenShift clusters](/docs/containers?topic=containers-faqs#container_platforms) to manage your containerized apps. Your app build processes do not differ because of the infrastructure provider, but how you expose the app does, as described in the next _App networking_ entry.</td>
  <td>You can create only community Kubernetes clusters, not OpenShift clusters.</td>
   </td>
 </tr>
 <tr>
   <td>App networking</td>
   <td>All pods that are deployed to a worker node are assigned a private IP address in the 172.30.0.0/16 range and are routed between worker nodes on the worker node private IP address of the private VLAN. To expose the app on the public network, your cluster must have worker nodes on the public VLAN. Then, you can create a NodePort, LoadBalancer (NLB), or Ingress (ALB) service. For more information, see [Planning in-cluster and external networking for apps](/docs/containers?topic=containers-cs_network_planning).</td>
   <td>All pods that are deployed to a worker node are assigned a private IP address in the 172.30.0.0/16 range and are routed between worker nodes on the worker node private IP address of the private VPC subnet. To expose the app on the public network, you can create a Kubernetes `LoadBalancer` service, which provisions a VPC load balancer and public hostname address for your worker nodes. For more information, see [Setting up a VPC load balancer to expose your app publicly](/docs/containers?topic=containers-vpc_ks_tutorial#vpc_ks_vpc_lb).</td>
 </tr>
 <tr>
   <td>Storage</td>
   <td>You can choose from non-persistent and persistent storage solutions such as file, block, object, and software-defined storage. For more information, see [Planning highly available persistent storage](/docs/openshift?topic=openshift-storage_planning).</td>
   <td>For persistent storage, use [block](/docs/openshift?topic=openshift-vpc-block). Only 5 volumes can be attached per worker node, with volume limits of 2TB and 20,000 IOPS. For non-persistent storage, secondary storage on the local worker node is not available.</td>
 </tr>
 <tr>
   <td>User access</td>
   <td>To create classic infrastructure clusters, you must set up [infrastructure credentials](/docs/openshift?topic=openshift-users#api_key) for each region and resource group. To let users manage the cluster, use [{{site.data.keyword.cloud_notm}} IAM platform roles](/docs/openshift?topic=openshift-access_reference#iam_platform). To grant users access to Kubernetes resources within the cluster, use [{{site.data.keyword.cloud_notm}} IAM service roles](/docs/openshift?topic=openshift-access_reference#service), which correspond with Kubernetes RBAC roles.</td>
   <td>Unlike for classic infrastructure, with VPC, you can use only [{{site.data.keyword.cloud_notm}} IAM access policies](/docs/vpc-on-classic?topic=vpc-on-classic-setting-up-access-to-your-classic-infrastructure-from-vpc) to authorize users to create infrastructure, manage your cluster, and access Kubernetes resources. The cluster can be in a different resource group than the VPC.</td>
 </tr>
 <tr>
   <td>Integrations</td>
   <td>You can extend your cluster and app capabilities with a variety of {{site.data.keyword.cloud_notm}} services, add-ons, and third-party integrations. For a list, see [Supported {{site.data.keyword.cloud_notm}} and third-party integrations](/docs/containers?topic=containers-supported_integrations).</td>
   <td>VPC supports a select list of supported {{site.data.keyword.cloud_notm}} services, add-ons, and third-party integrations. For a list, see [Supported {{site.data.keyword.cloud_notm}} and third-party integrations](/docs/containers?topic=containers-supported_integrations).</td>
 </tr>
 <tr>
   <td>Available locations and versions</td>
   <td>Classic clusters are [available worldwide](/docs/openshift?topic=openshift-regions-and-zones#locations), including all six {{site.data.keyword.cloud_notm}} multizone metros and 20 single zone locations in more than a dozen countries.</td>
   <td>VPC clusters are available in the following multizone metros: Dallas, Frankfurt, London, Sydney, and Tokyo.</td>
 </tr>
 <tr>
   <td>Service interface (API, CLI, UI)</td>
   <td>Classic clusters are fully supported in the {{site.data.keyword.containershort_notm}} [v1 API ![External link icon](../icons/launch-glyph.svg "External link icon")](https://containers.cloud.ibm.com/global/swagger-global-api/), [CLI](/docs/openshift?topic=openshift-kubernetes-service-cli), and [console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/clusters).</td>
   <td>VPC clusters are supported by the [next version (`v2`) of the {{site.data.keyword.containerlong_notm}} API](/docs/containers?topic=containers-cs_api_install#about_api), and you can manage your VPC clusters through the same CLI and console as classic clusters.</td>
 </tr>
 <tr>
   <td>Service limitations</td>
   <td>See [Service limitations](/docs/openshift?topic=openshift-limitations#tech_limits). Feature-specific limitations are documented by section.</td>
   <td>See [Service limitations](/docs/openshift?topic=openshift-limitations#tech_limits). For VPC cluster limitations, see [VPC cluster limitations](/docs/openshift?topic=openshift-limitations#vpc_ks_limits). For VPC-specific limitations, see [Known limitations](/docs/vpc-on-classic?topic=vpc-on-classic-known-limitations).</td>
 </tr>
 <tr>
   <td>Troubleshooting and support</td>
   <td>Both classic and VPC clusters are supported through the same {{site.data.keyword.cloud_notm}} Support processes. For cluster issues, check out the [Debugging your clusters](/docs/containers?topic=containers-cs_troubleshoot) guide. For questions, try posting in the [internal](https://ibm-argonauts.slack.com/messages/C4S4NUCB1) or [external](https://ibm-container-service.slack.com/messages/C4G6362ER) Slack channels.</td>
   <td>Both classic and VPC clusters are supported through the same {{site.data.keyword.cloud_notm}} Support processes. For cluster issues, check out the [VPC troubleshooting](/docs/openshift?topic=openshift-vpc_troubleshoot#vpc_troubleshoot) specific information. For questions, try posting in the [internal](https://ibm-argonauts.slack.com/messages/CJ58JHD9C) or [external](https://ibm-container-service.slack.com/messages/C4G6362ER) Slack channels.</td>
 </tr>
 </tbody>
</table>



</roks311-vpc>
