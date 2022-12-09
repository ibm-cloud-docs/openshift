---

copyright: 
  years: 2014, 2022
lastupdated: "2022-12-09"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}




# Supported infrastructure providers
{: #infrastructure_providers}

With {{site.data.keyword.openshiftlong}}, you can create a cluster from the following infrastructure providers. All the worker nodes in a cluster must be from the same provider. Originally, {{site.data.keyword.openshiftlong_notm}} provisioned your worker nodes in a single provider, classic infrastructure.

Virtual private cloud (VPC)
:   Create your cluster on the next generation of IBM Cloud infrastructure virtual servers.


{{site.data.keyword.satelliteshort}}
:   Create your cluster on your own hardware, {{site.data.keyword.cloud_notm}} Classic or VPC, or on vritual servers in another cloud provider like AWS or Azure.


Classic
:   Create your cluster on a classic compute, networking, and storage environment in IBM Cloud infrastructure.


## Virtual Private Cloud (VPC)
{: #vpc-gen2-infra-overview}

| Component | Description | 
| --- | --- | 
| Compute and worker node resources | Worker nodes are created as virtual machines using either shared infrastructure or dedicated hosts. Unlike classic clusters, VPC cluster worker nodes on shared hardware don't appear in your infrastructure portal or a separate infrastructure bill. Instead, you manage all maintenance and billing activity for the worker nodes through {{site.data.keyword.openshiftlong_notm}}. Your worker node instances are connected to certain VPC instances that do reside in your infrastructure account, such as the VPC subnet or storage volumes. For dedicated hosts, the dedicated host price covers the vCPU, memory and any [instance storage](/docs/vpc?topic=vpc-instance-storage) to be used by any workers placed on the host. |
| Security | Clusters on shared hardware run in an isolated environment in the public cloud. Clusters on dedicated hosts do not run in a shared environment, instead only your clusters are present on your hosts. Network access control lists protect the subnets that provide the floating IPs for your worker nodes. For more information, see the [VPC documentation](/docs/vpc?topic=vpc-about-vpc).|
| High availability | The master includes three replicas for high availability. Further, if you create your cluster in a multizone metro, the master replicas are spread across zones and you can also spread your worker pools across zones. For more information, see [High availability for {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-ha). |
| Reservations | Reservations aren't available for VPC. |
| Cluster administration | VPC clusters can't be reloaded or updated. Instead, use the [`worker replace --update` CLI](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_replace) or [API operation](https://containers.cloud.ibm.com/global/swagger-global-api/#/beta/replaceWorker){: external} to replace worker nodes that are outdated or in a troubled state. |
| Cluster networking | Unlike classic infrastructure, the worker nodes of your VPC cluster are attached to VPC subnets and assigned private IP addresses. The worker nodes are not connected to the public network, which instead is accessed through a public gateway, floating IP, or VPN gateway. For more information, see [Overview of VPC networking in {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics).|
| Apps and container platform | You can choose to create [community Kubernetes or {{site.data.keyword.redhat_openshift_notm}} clusters](/docs/openshift?topic=openshift-faqs#container_platforms) to manage your containerized apps. Your app build processes don't differ because of the infrastructure provider, but how you expose the app does. For more information, see [Choosing an app exposure serivice](/docs/openshift?topic=openshift-cs_network_planning). |
| App networking | All pods that are deployed to a worker node are assigned a private IP address in the 172.30.0.0/16 range and are routed between worker nodes on the worker node private IP address of the private VPC subnet. To expose the app on the public network, you can create a Kubernetes `LoadBalancer` service, which provisions a VPC load balancer and public hostname address for your worker nodes. For more information, see [Exposing apps with VPC load balancers](/docs/openshift?topic=openshift-vpc-lbaas). |
| Storage | For persistent storage, use [block](/docs/openshift?topic=openshift-vpc-block). For the number of volumes that can be attached per worker node, see [Volume attachment limits](/docs/vpc?topic=vpc-attaching-block-storage#vol-attach-limits). The storage class limits the volume size to 20TB and IOPS capacity to 20,000. For non-persistent storage, secondary storage on the local worker node is not available. |
| User access | You can use [{{site.data.keyword.cloud_notm}} IAM access policies](/docs/vpc?topic=vpc-iam-getting-started) to authorize users to create infrastructure, manage your cluster, and access cluster resources. The cluster can be in a different resource group than the VPC. |
| Integrations | VPC supports a select list of supported {{site.data.keyword.cloud_notm}} services, add-ons, and third-party integrations. For a list, see [Supported {{site.data.keyword.cloud_notm}} and third-party integrations](/docs/openshift?topic=openshift-supported_integrations). |
| Locations and versions | VPC clusters are available worldwide in the [multizone location](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc).
| Service interface | VPC clusters are supported by the [next version (`v2`) of the {{site.data.keyword.containerlong_notm}} API](/docs/openshift?topic=openshift-cs_api_install), and you can manage your VPC clusters through the same CLI and console as classic clusters.| 
| Service compliance | See the VPC section in [What standards does the service comply to?](/docs/openshift?topic=openshift-faqs#standards).
| Service limitations | See [Service limitations](/docs/openshift?topic=openshift-openshift_limitations#tech_limits). For VPC-specific limitations in {{site.data.keyword.openshiftlong_notm}}, see [VPC cluster limitations](/docs/openshift?topic=openshift-openshift_limitations#ks_vpc_gen2_limits). For general VPC infrastructure provider limitations, see [Limitations](/docs/vpc?topic=vpc-limitations).  |
{: caption="Table 1. VPC infrastructure overview." caption-side="bottom"}



## {{site.data.keyword.satelliteshort}}
{: #satellite-infra-overview}

| Component | Description | 
| --- | --- | 
| Compute and worker node resources | Worker nodes can be virtual machines using either shared infrastructure or dedicated hosts, or even bare metal servers. You manage maintenance and billing activity for the worker nodes through your host infrastructure provider whether that is {{site.data.keyword.cloud_notm}}, your own on-premises hardware, or another cloud provider. You also manage billing through {{site.data.keyword.cloud_notm}}. For more information about pricing, see [What am I charged for when I use {{site.data.keyword.satellitelong_notm}}?](/docs/satellite?topic=satellite-faqs#pricing). |
| Security | See [Security and compliance](/docs/satellite?topic=satellite-compliance). |
| High availability | See [About high availability and recover](/docs/satellite?topic=satellite-ha). |
| Reservations | Reservations aren't available for {{site.data.keyword.satelliteshort}}. |
| Cluster administration | See [Updating hosts that are assigned as worker nodes](/docs/satellite?topic=satellite-host-update-workers). | 
| Cluster networking | If you attach {{site.data.keyword.cloud_notm}} Classic or VPC hosts to your location, refer to those descriptions. |
| Apps and container platform | You can create [{{site.data.keyword.redhat_openshift_notm}} clusters](/docs/openshift?topic=openshift-faqs#container_platforms) to manage your containerized apps. Your app build processes don't differ because of the infrastructure provider, but how you expose the app does. For more information, see [Choosing an app exposure serivice](/docs/openshift?topic=openshift-cs_network_planning). |
| App networking | All pods that are deployed to a worker node are assigned a private IP address in the 172.30.0.0/16 range by default. You can avoid subnet conflicts with the network that you use to connect to your location by specifying a custom subnet CIDR that provides the private IP addresses for your pods. To expose an app, see [Exposing apps in {{site.data.keyword.satelliteshort}} clusters](/docs/openshift?topic=openshift-sat-expose-apps). |
| Storage | Bring your own storage drivers or deploy one of the supported storage templates. For more information, see [Understanding {{site.data.keyword.satelliteshort}} storage](/docs/satellite?topic=satellite-sat-storage-template-ov). | 
| User access | You can use {{site.data.keyword.cloud_notm}} IAM access policies to authorize users to create {{site.data.keyword.cloud_notm}} infrastructure, manage your cluster, and access cluster resources. For more infomratiom, see [Mananging access overview](/docs/satellite?topic=satellite-iam). You can also further control access to your host infrastructure in policies provided by your infrastructure provider.|
| Integrations | For cluster integrations, see [Supported {{site.data.keyword.cloud_notm}} and third-party integrations](/docs/openshift?topic=openshift-supported_integrations). For supported {{site.data.keyword.satelliteshort}} service intergrations, see [Supported {{site.data.keyword.satelliteshort}} {{site.data.keyword.cloud_notm}} services](/docs/satellite?topic=satellite-managed-services).
| Locations and versions | Clusters are managed from one of the [supported {{site.data.keyword.cloud_notm}} locations](/docs/satellite?topic=satellite-sat-regions). However, you can deploy worker nodes to your own location, an {{site.data.keyword.cloud_notm}} data center, or another cloud provider. For more information see [Understanding locations and hosts](/docs/satellite?topic=satellite-location-host). |
| Service interface | {{site.data.keyword.satelliteshort}} are supported by the global [API](https://containers.cloud.ibm.com/global/swagger-global-api/) [{{site.data.keyword.containerlong_notm}}, the {{site.data.keyword.openshiftlong_notm}} [CLI](/docs/openshift?topic=openshift-openshift-cli) and the {{site.data.keyword.satelliteshort}} [CLI](/docs/satellite?topic=satellite-setup-cli&interface=cli). You can also manage your clusters from the [console](https://cloud.ibm.com/satellite/clusters). |
| Service compliance | For clusters, see [What standards does the service comply to?](/docs/openshift?topic=openshift-faqs#standards). For {{site.data.keyword.satelliteshort}}, see [Security and compliance](/docs/satellite?topic=satellite-compliance). |
| Service limitations | See [Limiations, default settings, and usage requirements](/docs/satellite?topic=satellite-requirements). |
{: caption="Table 2. Satellite infrastructure overview." caption-side="bottom"}



## Classic
{: #classic-infra-overview}

| Component | Description | 
| --- | --- | 
| Compute and worker node resources | [Virtual](/docs/openshift?topic=openshift-planning_worker_nodes#vm), [bare metal](/docs/openshift?topic=openshift-planning_worker_nodes#bm), and [software-defined storage](/docs/openshift?topic=openshift-planning_worker_nodes#sds) machines are available for your worker nodes. Your worker node instances reside in your IBM Cloud infrastructure account, but you can manage them through {{site.data.keyword.openshiftlong_notm}}. You own the worker node instances.|
| Security | Built-in security features that help you protect your cluster infrastructure, isolate resources, and ensure security compliance. For more information, see the [classic Network Infrastructure documentation](/docs/cloud-infrastructure?topic=cloud-infrastructure-compare-infrastructure). |
| High availability | For both classic and VPC clusters, the master includes three replicas for high availability. Further, if you create your cluster in a multizone metro, the master replicas are spread across zones and you can also spread your worker pools across zones. For more information, see [High availability for {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-ha). |
| Reservations | [Create a reservation](/docs/openshift?topic=openshift-reservations) with contracts for 1 or 3 year terms for classic worker nodes to lock in a reduced cost for the life of the contract. Typical savings range between 30-50% compared to regular worker node costs. | 
| Cluster administration | Classic clusters support the entire set of `v1` API operations, such as resizing worker pools, reloading worker nodes, and updating masters and worker nodes across major, minor, and patch versions. When you delete a cluster, you can choose to remove any attached subnet or storage instances. | 
| Cluster networking | Your worker nodes are provisioned on private VLANs that provide private IP addresses to communicate on the private IBM Cloud infrastructure network. For communication on the public network, you can also provision the worker nodes on a public VLAN. Communication to the cluster master can be on the public or private cloud service endpoint. For more information, see [Understanding cluster network basics](/docs/openshift?topic=openshift-plan_clusters). |
| Apps and container platform | You can choose to create [community Kubernetes or {{site.data.keyword.redhat_openshift_notm}} clusters](/docs/openshift?topic=openshift-faqs#container_platforms) to manage your containerized apps. Your app build processes don't differ because of the infrastructure provider, but how you expose the app does. For more information, see [Choosing an app exposure serivice](/docs/openshift?topic=openshift-cs_network_planning). |
| App networking | All pods that are deployed to a worker node are assigned a private IP address in the 172.30.0.0/16 range and are routed between worker nodes on the worker node private IP address of the private VLAN. To expose the app on the public network, your cluster must have worker nodes on the public VLAN. Then, you can create a NodePort, LoadBalancer (NLB), or Ingress (ALB) service. For more information, see [Planning in-cluster and external networking for apps](/docs/openshift?topic=openshift-cs_network_planning).
| Storage | You can choose from non-persistent and persistent storage solutions such as file, block, object, and software-defined storage. For more information, see [Planning highly available persistent storage](/docs/openshift?topic=openshift-storage_planning). |
| User access | To create classic infrastructure clusters, you must set up [infrastructure credentials](/docs/openshift?topic=openshift-access-creds) for each region and resource group. To let users manage the cluster, use [{{site.data.keyword.cloud_notm}} IAM platform access roles](/docs/openshift?topic=openshift-iam-platform-access-roles). To grant users access to cluster resources, use [{{site.data.keyword.cloud_notm}} IAM service access roles](/docs/openshift?topic=openshift-iam-service-access-roles), which correspond with Kubernetes RBAC roles. |
| Integrations | You can extend your cluster and app capabilities with a variety of {{site.data.keyword.cloud_notm}} services, add-ons, and third-party integrations. For a list, see [Supported {{site.data.keyword.cloud_notm}} and third-party integrations](/docs/openshift?topic=openshift-supported_integrations). |
| Locations and versions | Classic clusters are available in multizone and single zone locations [worldwide](/docs/openshift?topic=openshift-regions-and-zones#locations). |
| Service interface | Classic clusters are fully supported in the {{site.data.keyword.containershort_notm}} [`v1` API](https://containers.cloud.ibm.com/global/swagger-global-api/#/){: external}, [CLI](/docs/openshift?topic=openshift-kubernetes-service-cli), and [console](https://cloud.ibm.com/kubernetes/clusters).|
| Service compliance | See the classic section in [What standards does the service comply to?](/docs/openshift?topic=openshift-faqs#standards). |
| Service limitations | See [Service limitations](/docs/openshift?topic=openshift-openshift_limitations#tech_limits). Feature-specific limitations are documented by section. |
{: caption="Table 3. Classic infrastructure overview." caption-side="bottom"}

## Troubleshooting and support
{: #infra-troubleshoot}

Classic, VPC, and {{site.data.keyword.satelliteshort}} clusters are supported through the same {{site.data.keyword.cloud_notm}} Support processes. 

- For cluster issues, check out the [Debugging your clusters](/docs/openshift?topic=openshift-debug_clusters) guide. 
- For {{site.data.keyword.satelliteshort}}-specific issues, see [Troubleshooting errors](/docs/satellite?topic=satellite-sitemap&interface=cli#sitemap_troubleshooting_errors).
- For VPC-specific topics. For questions, try posting in the [Slack channel](https://cloud.ibm.com/kubernetes/slack){: external}.

