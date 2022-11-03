---

copyright: 
  years: 2014, 2022
lastupdated: "2022-11-03"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Supported infrastructure providers
{: #infrastructure_providers}

With {{site.data.keyword.openshiftlong}}, you can create a cluster from the following infrastructure providers. All the worker nodes in a cluster must be from the same provider. Originally, {{site.data.keyword.openshiftlong_notm}} provisioned your worker nodes in a single provider, classic infrastructure.

Virtual private cloud (VPC)
:   Create your cluster on the next generation of IBM Cloud infrastructure virtual servers.



Classic
:   Create your cluster on a classic compute, networking, and storage environment in IBM Cloud infrastructure.


## Compute and worker node resources
{: #infra-compute}

VPC
:   Worker nodes are created as virtual machines using either shared infrastructure or dedicated hosts. Unlike classic clusters, VPC cluster worker nodes on shared hardware don't appear in your infrastructure portal or a separate infrastructure bill. Instead, you manage all maintenance and billing activity for the worker nodes through {{site.data.keyword.openshiftlong_notm}}. Your worker node instances are connected to certain VPC instances that do reside in your infrastructure account, such as the VPC subnet or storage volumes. For dedicated hosts, the dedicated host price covers the vCPU, memory and any [instance storage](/docs/vpc?topic=vpc-instance-storage) to be used by any workers placed on the host.



Classic
:   [Virtual](/docs/openshift?topic=openshift-planning_worker_nodes#vm), [bare metal](/docs/openshift?topic=openshift-planning_worker_nodes#bm), and [software-defined storage](/docs/openshift?topic=openshift-planning_worker_nodes#sds) machines are available for your worker nodes. Your worker node instances reside in your IBM Cloud infrastructure account, but you can manage them through {{site.data.keyword.openshiftlong_notm}}. You own the worker node instances.


## Security
{: #infra-security}

VPC
:   Clusters on shared hardware run in an isolated environment in the public cloud. Clusters on dedicated hosts do not run in a shared environment, instead only your clusters are present on your hosts. Network access control lists protect the subnets that provide the floating IPs for your worker nodes. For more information, see the [VPC documentation](/docs/vpc?topic=vpc-about-vpc).



Classic
:   Built-in security features that help you protect your cluster infrastructure, isolate resources, and ensure security compliance. For more information, see the [classic Network Infrastructure documentation](/docs/cloud-infrastructure?topic=cloud-infrastructure-compare-infrastructure).


## High availability
{: #infra-high-availability}

Classic and VPC
:   For both classic and VPC clusters, the master includes three replicas for high availability. Further, if you create your cluster in a multizone metro, the master replicas are spread across zones and you can also spread your worker pools across zones. For more information, see [High availability for {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-ha).




## Reservations
{: #infar-reservations}

VPC
:   Reservations aren't available for VPC. 




Classic
:   [Create a reservation](/docs/openshift?topic=openshift-reservations) with contracts for 1 or 3 year terms for classic worker nodes to lock in a reduced cost for the life of the contract. Typical savings range between 30-50% compared to on-demand worker node costs.


## Cluster administration
{: #infra-cluster-admin}

VPC
:   VPC clusters can't be reloaded or updated. Instead, use the [`worker replace --update` CLI](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_replace) or [API operation](https://containers.cloud.ibm.com/global/swagger-global-api/#/beta/replaceWorker){: external} to replace worker nodes that are outdated or in a troubled state.



Classic
:   Classic clusters support the entire set of `v1` API operations, such as resizing worker pools, reloading worker nodes, and updating masters and worker nodes across major, minor, and patch versions. When you delete a cluster, you can choose to remove any attached subnet or storage instances.


## Cluster networking
{: #infra-cluster-networking}

VPC
:   Unlike classic infrastructure, the worker nodes of your VPC cluster are attached to VPC subnets and assigned private IP addresses. The worker nodes are not connected to the public network, which instead is accessed through a public gateway, floating IP, or VPN gateway. For more information, see [Overview of VPC networking in {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics).



Classic
:   Your worker nodes are provisioned on private VLANs that provide private IP addresses to communicate on the private IBM Cloud infrastructure network. For communication on the public network, you can also provision the worker nodes on a public VLAN. Communication to the cluster master can be on the public or private cloud service endpoint. For more information, see [Understanding cluster network basics](/docs/openshift?topic=openshift-plan_clusters).


## Apps and container platform
{: #infra-apps-cp}

VPC
:   You can choose to create [community Kubernetes or {{site.data.keyword.redhat_openshift_notm}} clusters](/docs/openshift?topic=openshift-faqs#container_platforms) to manage your containerized apps. Your app build processes don't differ because of the infrastructure provider, but how you expose the app does. For more information, see [App networking](#infra-app-networking).



Classic
:   You can choose to create [community Kubernetes or {{site.data.keyword.redhat_openshift_notm}} clusters](/docs/openshift?topic=openshift-faqs#container_platforms) to manage your containerized apps. Your app build processes don't differ because of the infrastructure provider, but how you expose the app does. For more information, see [App networking](#infra-app-networking).


## App networking
{: #infra-app-networking}

VPC
:   All pods that are deployed to a worker node are assigned a private IP address in the 172.30.0.0/16 range and are routed between worker nodes on the worker node private IP address of the private VPC subnet. To expose the app on the public network, you can create a Kubernetes `LoadBalancer` service, which provisions a VPC load balancer and public hostname address for your worker nodes. For more information, see [Exposing apps with VPC load balancers](/docs/openshift?topic=openshift-vpc-lbaas).



Classic
:   All pods that are deployed to a worker node are assigned a private IP address in the 172.30.0.0/16 range and are routed between worker nodes on the worker node private IP address of the private VLAN. To expose the app on the public network, your cluster must have worker nodes on the public VLAN. Then, you can create a NodePort, LoadBalancer (NLB), or Ingress (ALB) service. For more information, see [Planning in-cluster and external networking for apps](/docs/openshift?topic=openshift-cs_network_planning).




## Storage
{: #infra-storage}

VPC
:   For persistent storage, use [block](/docs/openshift?topic=openshift-vpc-block). For the number of volumes that can be attached per worker node, see [Volume attachment limits](/docs/vpc?topic=vpc-attaching-block-storage#vol-attach-limits). The storage class limits the volume size to 20TB and IOPS capacity to 20,000. For non-persistent storage, secondary storage on the local worker node is not available.



Classic
:   You can choose from non-persistent and persistent storage solutions such as file, block, object, and software-defined storage. For more information, see [Planning highly available persistent storage](/docs/openshift?topic=openshift-storage_planning).


## User access
{: #infra-user-access}

VPC
:   You can use [{{site.data.keyword.cloud_notm}} IAM access policies](/docs/vpc?topic=vpc-iam-getting-started) to authorize users to create infrastructure, manage your cluster, and access cluster resources. The cluster can be in a different resource group than the VPC.



Classic
:   To create classic infrastructure clusters, you must set up [infrastructure credentials](/docs/openshift?topic=openshift-access-creds) for each region and resource group. To let users manage the cluster, use [{{site.data.keyword.cloud_notm}} IAM platform access roles](/docs/openshift?topic=openshift-iam-platform-access-roles). To grant users access to cluster resources, use [{{site.data.keyword.cloud_notm}} IAM service access roles](/docs/openshift?topic=openshift-iam-service-access-roles), which correspond with Kubernetes RBAC roles.


## Integrations
{: #infra-integrations}


VPC
:   VPC supports a select list of supported {{site.data.keyword.cloud_notm}} services, add-ons, and third-party integrations. For a list, see [Supported {{site.data.keyword.cloud_notm}} and third-party integrations](/docs/openshift?topic=openshift-supported_integrations).



Classic
:   You can extend your cluster and app capabilities with a variety of {{site.data.keyword.cloud_notm}} services, add-ons, and third-party integrations. For a list, see [Supported {{site.data.keyword.cloud_notm}} and third-party integrations](/docs/openshift?topic=openshift-supported_integrations).



## Locations and versions
{: #infra-locations}

VPC
:   VPC clusters are available worldwide in the [multizone location](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc).



Classic
:   Classic clusters are available in multizone and single zone locations [worldwide](/docs/openshift?topic=openshift-regions-and-zones#locations).




## Service interface
{: #infra-interface}


VPC
:   VPC clusters are supported by the [next version (`v2`) of the {{site.data.keyword.containerlong_notm}} API](/docs/openshift?topic=openshift-cs_api_install), and you can manage your VPC clusters through the same CLI and console as classic clusters.



Classic
:  Classic clusters are fully supported in the {{site.data.keyword.containershort_notm}} [`v1` API](https://containers.cloud.ibm.com/global/swagger-global-api/#/){: external}, [CLI](/docs/openshift?topic=openshift-kubernetes-service-cli), and [console](https://cloud.ibm.com/kubernetes/clusters).


## Service compliance
{: #infra-compliance}

VPC
:   See the VPC section in [What standards does the service comply to?](/docs/openshift?topic=openshift-faqs#standards).



Classic
:   See the classic section in [What standards does the service comply to?](/docs/openshift?topic=openshift-faqs#standards).


## Service limitations
{: #infra-limitations}

VPC
:   See [Service limitations](/docs/openshift?topic=openshift-limitations#tech_limits). For VPC-specific limitations in {{site.data.keyword.openshiftlong_notm}}, see [VPC cluster limitations](/docs/openshift?topic=openshift-limitations#ks_vpc_gen2_limits). For general VPC infrastructure provider limitations, see [Limitations](/docs/vpc?topic=vpc-limitations). 



Classic
:   See [Service limitations](/docs/openshift?topic=openshift-limitations#tech_limits). Feature-specific limitations are documented by section.


## Troubleshooting and support
{: #infra-troubleshoot}

Classic, VPC, and {{site.data.keyword.satelliteshort}} clusters are supported through the same {{site.data.keyword.cloud_notm}} Support processes. 

For cluster issues, check out the [Debugging your clusters](/docs/openshift?topic=openshift-debug_clusters) guide. 



For VPC-specific topics. For questions, try posting in the [Slack channel](https://cloud.ibm.com/kubernetes/slack){: external}.





