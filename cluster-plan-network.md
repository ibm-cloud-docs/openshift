---

copyright: 
  years: 2014, 2021
lastupdated: "2021-09-27"

keywords: openshift, rhoks, roks, rhos, multi az, multi-az, szr, mzr

subcollection: openshift

---




{{site.data.keyword.attribute-definition-list}}


# Planning your cluster network setup   
{: #plan_clusters}

Design a network setup for your {{site.data.keyword.openshiftlong}} cluster that meets the needs of your workloads and environment.
{: shortdesc}

Get started by planning your setup for a VPC or a classic cluster.
* <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> With [{{site.data.keyword.openshiftlong_notm}} clusters in VPC](#plan_vpc_basics), you can create your cluster in the next generation of the {{site.data.keyword.cloud_notm}} platform, in [Virtual Private Cloud](/docs/vpc?topic=vpc-about-vpc) for Generation 2 compute resources. VPC gives you the security of a private cloud environment with the dynamic scalability of a public cloud.
* <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> With [{{site.data.keyword.openshiftlong_notm}} classic clusters](#plan_basics), you can create your cluster on classic infrastructure. Classic clusters include all of the {{site.data.keyword.openshiftlong_notm}} mature and robust features for compute, networking, and storage.

First time creating a cluster? First, try out the [tutorial for creating a VPC cluster](/docs/openshift?topic=openshift-vpc_rh_tutorial) or the [tutorial for creating {{site.data.keyword.openshiftshort}} clusters](/docs/openshift?topic=openshift-openshift_tutorial). Then, come back here when you’re ready to plan out your production-ready clusters.
{: tip}


## Understanding network basics of VPC clusters
{: #plan_vpc_basics}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> When you create your cluster, you must choose a networking setup so that certain cluster components can communicate with each other and with networks or services outside of the cluster.
{: shortdesc}

* [Worker-to-worker communication](#vpc-worker-worker): All worker nodes must be able to communicate with each other on the private network through VPC subnets.
* [Worker-to-master and user-to-master communication](#vpc-workeruser-master): Your worker nodes and your authorized cluster users can communicate with the Kubernetes master securely over virtual private endpoints or cloud service endpoints.
* [Worker communication to other services or networks](#vpc-worker-services-onprem): Allow your worker nodes to securely communicate with other {{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.registrylong}}, to on-premises networks, to other VPCs, or to classic infrastructure resources.
* [External communication to apps that run on worker nodes](#vpc-external-workers): Allow public or private requests into the cluster as well as requests out of the cluster to a public endpoint.
</br>

### Worker-to-worker communication: VPC subnets
{: #vpc-worker-worker}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Before you create a VPC cluster for the first time, you must [create a VPC subnet](https://cloud.ibm.com/vpc/provision/network){: external} in each zone where you want to deploy worker nodes. A VPC subnet is a specified private IP address range (CIDR block) and configures a group of worker nodes and pods as if they are attached to the same physical wire.
{: shortdesc}

When you create a cluster, you specify an existing VPC subnet for each zone. Each worker node that you add in a cluster is deployed with a private IP address from the VPC subnet in that zone. After the worker node is provisioned, the worker node IP address persists after a `reboot` operation, but the worker node IP address changes after `replace` and `update` operations.

Subnets provide a channel for connectivity among the worker nodes within the cluster. Additionally, any system that is connected to any of the private subnets in the same VPC can communicate with workers. For example, all subnets in one VPC can communicate through private layer 3 routing with a built-in VPC router. If you have multiple clusters that must communicate with each other, you can create the clusters in the same VPC. However, if your clusters do not need to communicate, you can achieve better network segmentation by creating the clusters in separate VPCs. You can also create [access control lists (ACLs)](/docs/containers?topic=containers-vpc-network-policy#acls) for your VPC subnets to mediate traffic on the private network. ACLs consist of inbound and outbound rules that define which ingress and egress is permitted for each VPC subnet.

When you create a VPC cluster and enable both the public and private cloud service endpoints during cluster creation, the public cloud service endpoint is used by default for access to components such as the {{site.data.keyword.openshiftshort}} web console for your cluster. In order for console pods to establish a secure, public connection over the internet through the public service endpoint, you must enable a public gateway on each VPC subnet that your worker nodes are deployed to.

When you create a VPC cluster and enable only the private cloud service endpoint during cluster creation, the private cloud service endpoint is used by default to access {{site.data.keyword.openshiftshort}} components such as the {{site.data.keyword.openshiftshort}} web console or OperatorHub. You must be connected to the private VPC network, such as through a VPN connection, to access these components or run `kubectl` commands on your cluster.

The default IP address range for VPC subnets is 10.0.0.0 – 10.255.255.255. For a list of IP address ranges per VPC zone, see the [VPC default address prefixes](/docs/vpc?topic=vpc-configuring-address-prefixes).

If you enable classic access when you create your VPC, [classic access default address prefixes](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure#classic-access-default-address-prefixes) automatically determine the IP ranges of any subnets that you create. However, the default IP ranges for classic access VPC subnets conflict with the subnets for the {{site.data.keyword.openshiftlong_notm}} control plane. Instead, you must [create the VPC without the automatic default address prefixes, and then create your own address prefixes and subnets within those ranges for you cluster](/docs/containers?topic=containers-vpc-subnets#classic_access_subnets).

Need to create your cluster by using custom-range subnets? Check out this guidance on [custom address prefixes](/docs/vpc?topic=vpc-configuring-address-prefixes). If you use custom-range subnets for your worker nodes, you must [ensure that your worker node subnets do not overlap with your cluster's pod subnet](/docs/containers?topic=containers-vpc-subnets#vpc-ip-range).
{: tip}

Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
{: important}

When you create VPC subnets for your clusters, keep in mind the following features and limitations. For more information about VPC subnets, see [Characteristics of subnets in the VPC](/docs/vpc?topic=vpc-about-networking-for-vpc#subnets-in-the-vpc).
* The default CIDR size of each VPC subnet is `/24`, which can support up to 253 worker nodes. If you plan to deploy more than 250 worker nodes per zone in one cluster, consider creating a subnet of a larger size.
* After you create a VPC subnet, you cannot resize it or change its IP range.
* Multiple clusters in the same VPC can share subnets.
* VPC subnets are bound to a single zone and cannot span multiple zones or regions.
* After you create a subnet, you cannot move it to a different zone, region, or VPC.
* If you have worker nodes that are attached to an existing subnet in a zone, you cannot change the subnet for that zone in the cluster.
* The `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16` ranges are prohibited.

</br>

### Worker-to-master and user-to-master communication: Virtual private endpoints or cloud service endpoints
{: #vpc-workeruser-master}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> {{site.data.keyword.openshiftlong_notm}} uses different types of service endpoints to establish a connection from authorized cluster users and worker nodes to the Kubernetes master.  Authorized cluster users communicate with the Kubernetes master through cloud service endpoints. Depending on your cluster version, worker nodes communicate with the Kubernetes master through cloud service endpoints or VPC virtual private endpoints.
{: shortdesc}

Before you create a cluster, you must enable your account to use service endpoints. To enable service endpoints, run `ibmcloud account update --service-endpoint-enable true`.

In VPC clusters in {{site.data.keyword.openshiftlong_notm}}, you cannot disable the private cloud service endpoint or set up a cluster with the public cloud service endpoint only.
{: note}

Your VPC cluster is created with both a public and a private cloud service endpoint by default. To create clusters with worker nodes that are connected to the private network only, you must enable only the private service endpoint during cluster creation. Do not enable the public service endpoint. For example, to create a VPC cluster with only a private cloud service endpoint [in the CLI](/docs/openshift?topic=openshift-clusters#cluster_vpcg2_cli), include the `--disable-public-service-endpoint` flag. If you include this flag, your cluster is created with routers and Ingress controllers that expose your apps on the private network only by default. If you later want to expose apps to a public network, you must manually create public routers and Ingress controllers.
{: important}

**Worker-to-master communication**

Worker node communication to the Kubernetes master is established differently based on your cluster version.

* {{site.data.keyword.openshiftshort}} version 4.6 or later: Worker node communication to the Kubernetes master is established over the [VPC virtual private endpoint (VPE)](/docs/containers?topic=containers-vpc-subnets#vpc_basics_vpe). If the public cloud service endpoint is also enabled, worker-to-master traffic is established half over the public endpoint and half over the VPE for protection from potential outages of the public or private network.
* {{site.data.keyword.openshiftshort}} version 4.5 or earlier: Worker node communication to the Kubernetes master is established over the private cloud service endpoint. If the public cloud service endpoint is also enabled, worker-to-master traffic is established half over the public endpoint and half over the private endpoint for protection from potential outages of the public or private network.

To secure communication over public and private cloud service endpoints or VPEs, {{site.data.keyword.openshiftlong_notm}} automatically sets up an OpenVPN connection between the Kubernetes master and worker nodes when the cluster is created. Worker nodes securely talk to the master through TLS certificates, and the master talks to workers through the OpenVPN connection.

**User-to-master communication**

You can allow authorized cluster users to communicate with the Kubernetes master by enabling the public and private cloud service endpoints, or the private cloud service endpoint only.

* Public and private cloud service endpoints: By default, all calls to the master that are initiated by authorized cluster users are routed through the public cloud service endpoint. If authorized cluster users are in your VPC network or are connected through a [VPC VPN connection](/docs/containers?topic=containers-vpc-vpnaas), the master is privately accessible through the private cloud service endpoint.
* Private cloud service endpoint only: To access the master through the private cloud service endpoint, authorized cluster users must either be in your VPC network or connected through a [VPC VPN connection](/docs/containers?topic=containers-vpc-vpnaas).

You can secure access to your private cloud service endpoint by creating a subnet allowlist. Only authorized requests to your cluster master that originate from subnets in the allowlist are permitted through the cluster's private cloud service endpoint. For more information, see [Creating an allowlist for the private cloud service endpoint](/docs/containers?topic=containers-access_cluster#private-se-allowlist).
{: tip}

</br>

### Worker communication to other services or networks
{: #vpc-worker-services-onprem}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Allow your worker nodes to securely communicate with other {{site.data.keyword.cloud_notm}} services, on-premises networks, other VPCs, and {{site.data.keyword.cloud_notm}} classic infrastructure resources.
{: shortdesc}

**Communication with other {{site.data.keyword.cloud_notm}} services over the private or public network**

Your worker nodes can automatically and securely communicate with other [{{site.data.keyword.cloud_notm}} services that support private cloud service endpoints](/docs/account?topic=account-vrf-service-endpoint), such as {{site.data.keyword.registrylong}}, over the private network. If an {{site.data.keyword.cloud_notm}} service does not support private cloud service endpoints, worker nodes can securely communicate with the services over the public network through the subnet's public gateway.

Note that if you use [access control lists (ACLs)](/docs/containers?topic=containers-vpc-network-policy#acls) for your VPC subnets, you must create inbound or outbound rules to allow your worker nodes to communicate with these services.

**Communication with resources in on-premises data centers**

To connect your cluster with your on-premises data center, you can use the {{site.data.keyword.vpc_full}} VPN or {{site.data.keyword.dl_full}}.
* To get started with the Virtual Private Cloud VPN, see [Configure an on-prem VPN gateway](/docs/vpc?topic=vpc-vpn-onprem-example#configuring-onprem-gateway) and [Create a VPN gateway in your VPC, and create the connection between the VPC VPN gateway and your local VPN gateway](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console#vpn-ui). If you have a multizone cluster, you must create a VPC gateway on a subnet in each zone where you have worker nodes.
* To get started with {{site.data.keyword.dl_short}}, see [Ordering {{site.data.keyword.dl_full_notm}} Dedicated](/docs/dl?topic=dl-how-to-order-ibm-cloud-dl-dedicated). In step 8, you can create a network connection to your VPC to be attached to the {{site.data.keyword.dl_short}} gateway.

If you plan to connect your cluster to on-premises networks, check out the following helpful information:
{: tip}

* You might have subnet conflicts with the IBM-provided default 172.30.0.0/16 range for pods and 172.21.0.0/16 range for services. You can avoid subnet conflicts when you [create a cluster from the CLI](/docs/containers?topic=containers-kubernetes-service-cli#cli_cluster-create-vpc-gen2) by specifying a custom subnet CIDR for pods in the `--pod-subnet` flag and a custom subnet CIDR for services in the `--service-subnet` flag.
* If your VPN solution preserves the source IP addresses of requests, you can [create custom static routes](/docs/containers?topic=containers-static-routes) to ensure that your worker nodes can route responses from your cluster back to your on-premises network.
* Note that the `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16` subnet ranges are prohibited because they are reserved for {{site.data.keyword.openshiftlong_notm}} control plane functionality.

**Communication with resources in other VPCs**

To connect an entire VPC to another VPC in your account, you can use the {{site.data.keyword.vpc_short}} VPN or {{site.data.keyword.tg_full}}.
* To get started with the {{site.data.keyword.vpc_short}} VPN, follow the steps in [Connecting two VPCs using VPN](/docs/vpc?topic=vpc-vpn-example) to create a VPC gateway on a subnet in each VPC and create a VPN connection between the two VPC gateways. Note that if you use [access control lists (ACLs)](/docs/containers?topic=containers-vpc-network-policy) for your VPC subnets, you must create inbound or outbound rules to allow your worker nodes to communicate with the subnets in other VPCs.
* To get started with {{site.data.keyword.tg_full_notm}}, see the [{{site.data.keyword.tg_short}} documentation](/docs/transit-gateway?topic=transit-gateway-getting-started). {{site.data.keyword.tg_short}} instances can be configured to route between VPCs that are in the same region (local routing) or VPCs that are in different regions (global routing).

**Communication with {{site.data.keyword.cloud_notm}} classic resources**

If you need to connect your cluster to resources in your {{site.data.keyword.cloud_notm}} classic infrastructure, you can set up a VPC with classic access or use {{site.data.keyword.tg_full_notm}}.
* To get started with a VPC with classic access, see [Setting up access to classic infrastructure](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure). Note that you must enable classic access when you create the VPC, and you cannot convert an existing VPC to use classic access. Additionally, you can set up classic infrastructure access for only one VPC per region, and you cannot set up more than one VPC with classic infrastructure access in a region.
* To get started with {{site.data.keyword.tg_full_notm}}, see the [{{site.data.keyword.tg_short}} documentation](/docs/transit-gateway?topic=transit-gateway-getting-started). You can connect multiple VPCs to classic infrastructure, such as using {{site.data.keyword.tg_full_notm}} to manage access between your VPCs in multiple regions to resources in your {{site.data.keyword.cloud_notm}} classic infrastructure.

</br>

### External communication to apps that run on worker nodes
{: #vpc-external-workers}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Allow private or public traffic requests from outside the cluster to your apps that run on worker nodes.
{: shortdesc}

**Private traffic to cluster apps**

When you deploy an app in your cluster, you might want to make the app accessible to only users and services that are on the same private network as your cluster. Private load balancing is ideal for making your app available to requests from outside the cluster without exposing the app to the general public. You can also use private load balancing to test access, request routing, and other configurations for your app before you later expose your app to the public with public network services.

To allow private network traffic requests from outside the cluster to your apps, you can use private Kubernetes networking services, such as creating [`LoadBalancer` services](/docs/containers?topic=containers-vpc-lbaas). For example, when you create a Kubernetes `LoadBalancer` service in your cluster, a load balancer for VPC is automatically created in your VPC outside of your cluster. The VPC load balancer is multizonal and routes requests for your app through the private NodePorts that are automatically opened on your worker nodes. You can then modify the default VPC security group for your worker nodes to allow inbound network traffic requests from specified sources.

For more information, see [Planning private external load balancing](/docs/openshift?topic=openshift-cs_network_planning#private_access).

**Public traffic to cluster apps**

To make your apps accessible from the public internet, you can use public networking services. Even though your worker nodes are connected to private VPC subnets only, the VPC load balancer that is created for public networking services can route public requests to your app on the private network by providing your app a public URL. When an app is publicly exposed, anyone that has the public URL can send a request to your app.

You can use public Kubernetes networking services, such as creating [`LoadBalancer` services](/docs/containers?topic=containers-vpc-lbaas). For example, when you create a Kubernetes `LoadBalancer` service in your cluster, a load balancer for VPC is automatically created in your VPC outside of your cluster. The VPC load balancer is multizonal and routes requests for your app through the private NodePorts that are automatically opened on your worker nodes. You can then modify the default security group for your cluster to allow inbound network traffic requests from specified sources to your worker nodes.

<br />

## Example scenarios for VPC cluster network setups
{: #vpc-scenarios}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Now that you understand the basics of cluster networking, check out some example scenarios in which various VPC cluster network setups can meet your workload needs.
{: shortdesc}

### Scenario: Run internet-facing app workloads in a VPC cluster
{: #vpc-no-pgw}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> In this scenario, you run workloads in a VPC cluster that are accessible to requests from the Internet. Public access is controlled by security groups so that end users can access your apps while unwanted public requests to your apps are denied. Additionally, your workers have automatic access to any {{site.data.keyword.cloud_notm}} services that support private cloud service endpoints.
{: shortdesc}

<p>
<figure>
    <img src="images/roks_ov_vpc_pub.png" width="850" style="width:850px; border-style: none" alt="Network setup for a VPC cluster that runs internet-facing app workloads"/>
    <figcaption>Network setup for a VPC cluster that runs internet-facing app workloads</figcaption>
</figure>
</p>

**Worker-to-worker communication**

To achieve this setup, you create VPC subnets in each zone where you want to deploy worker nodes. To run default {{site.data.keyword.openshiftshort}} components such as the web console or OperatorHub, public gateways are required for these subnets. Then, you create a VPC cluster that uses these VPC subnets.

**Worker-to-master and user-to-master communication**

You can choose to allow worker-to-master and user-to-master communication over the public and private networks, or over the private network only.
* Public and private cloud service endpoints: Communication between worker nodes and master is established over the private network through the private cloud service endpoint. By default, all calls to the master that are initiated by authorized cluster users are routed through the public cloud service endpoint.
* Private service endpoint only: Communication to master from both worker nodes and cluster users is established over the private network through the private cloud service endpoint. Cluster users must either be in your VPC network or connect through a [VPC VPN connection](/docs/containers?topic=containers-vpc-vpnaas).

**Worker communication to other services or networks**

If your app workload requires other {{site.data.keyword.cloud_notm}} services, your worker nodes can automatically, securely communicate with {{site.data.keyword.cloud_notm}} services that support private cloud service endpoints over the private VPC network.

**External communication to apps that run on worker nodes**

After you test your app, you can expose it to the internet by creating a public Kubernetes `LoadBalancer` service or using the default public Ingress application load balancers (ALBs). The VPC load balancer that is automatically created in your VPC outside of your cluster when you use one of these services routes traffic to your app. You can improve the security of your cluster and control public network traffic to your apps by modifying the default VPC security group for your cluster. Security groups consist of rules that define which inbound traffic is permitted for your worker nodes.

Ready to get started with a cluster for this scenario? After you plan your [high availability](/docs/containers?topic=containers-ha_clusters) and [worker node](/docs/containers?topic=containers-planning_worker_nodes) setups, see [Creating VPC clusters](/docs/containers?topic=containers-clusters).

<br />


### Scenario: Extend your on-premises data center to a VPC cluster
{: #vpc-vpn}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> In this scenario, you run workloads in a VPC cluster. However, you want these workloads to be accessible only to services, databases, or other resources in your private networks in an on-premises data center. Your cluster workloads might need to access a few other {{site.data.keyword.cloud_notm}} services that support communication over the private network.
{: shortdesc}

<p>
<figure>
    <img src="images/roks_ov_vpc_priv.png" width="850" style="width:850px; border-style: none" alt="Network setup for a VPC cluster that extends an on-prem data center"/>
    <figcaption>Network setup for a VPC cluster that extends an on-prem data center</figcaption>
</figure>
</p>

**Worker-to-worker communication**

To achieve this setup, you create VPC subnets in each zone where you want to deploy worker nodes. To run default {{site.data.keyword.openshiftshort}} components such as the web console or OperatorHub, public gateways are required for these subnets. Then, you create a VPC cluster that uses these VPC subnets.

Note that you might have subnet conflicts between the default ranges for workers nodes, pods, and services, and the subnets in your on-premises networks. When you create your VPC subnets, you can choose [custom address prefixes](/docs/vpc?topic=vpc-configuring-address-prefixes) and then create your cluster by using these subnets. Additionally, you can specify a custom subnet CIDR for pods and services by using the `--pod-subnet` and `--service-subnet` flags in the `ibmcloud oc cluster create` command when you create your cluster.

**Worker-to-master and user-to-master communication**

When you create the cluster, you enable private cloud service endpoint only to allow worker-to-master and user-to-master communication over the private network. Cluster users must either be in your VPC network or connect through a [VPC VPN connection](/docs/containers?topic=containers-vpc-vpnaas).

**Worker communication to other services or networks**

To connect your cluster with your on-premises data center, you can set up the VPC VPN service. The {{site.data.keyword.vpc_short}} VPN connects your entire VPC to an on-premises data center. If your app workload requires other {{site.data.keyword.cloud_notm}} services that support private cloud service endpoints, your worker nodes can automatically, securely communicate with these services over the private VPC network.

**External communication to apps that run on worker nodes**

After you test your app, you can expose it to the private network by creating a private Kubernetes `LoadBalancer` service or using the default private Ingress application load balancers (ALBs). The VPC load balancer that is automatically created in your VPC outside of your cluster when you use one of these services routes traffic to your app. Note that the VPC load balancer exposes your app to the private network only so that any on-premises system with a connection to the VPC subnet can access the app. You can improve the security of your cluster and control public traffic apps by modifying the default VPC security group for your cluster. Security groups consist of rules that define which inbound traffic is permitted for your worker nodes.

Ready to get started with a cluster for this scenario? After you plan your [high availability](/docs/containers?topic=containers-ha_clusters) and [worker node](/docs/containers?topic=containers-planning_worker_nodes) setups, see [Creating VPC clusters](/docs/containers?topic=containers-clusters).

<br />

## Understanding network basics of classic clusters
{: #plan_basics}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> When you create a classic cluster, you must choose a networking setup so that certain cluster components can communicate with each other and with networks or services outside of the cluster.
{: shortdesc}

* [Worker-to-worker communication](#worker-worker): All worker nodes must be able to communicate with each other on the private network. In many cases, communication must be permitted across multiple private VLANs to allow workers on different VLANs and in different zones to connect with each other.
* [Worker-to-master and user-to-master communication](#workeruser-master): Your worker nodes and your authorized cluster users can communicate with the Kubernetes master securely over the public network with TLS or over the private network through private cloud service endpoints.
* [Worker communication to other {{site.data.keyword.cloud_notm}} services or on-premises networks](#worker-services-onprem): Allow your worker nodes to securely communicate with other {{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.registrylong}}, and to an on-premises network.
* [External communication to apps that run on worker nodes](#external-workers): Allow public or private requests into the cluster as well as requests out of the cluster to a public endpoint.

### Worker-to-worker communication: classic VLANs and subnets
{: #worker-worker}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> When you create a classic cluster, the cluster's worker nodes are connected automatically to a private VLAN and a public VLAN. A VLAN configures a group of worker nodes and pods as if they were attached to the same physical wire and provides a channel for connectivity among the workers.
{: shortdesc}

You cannot create classic {{site.data.keyword.openshiftlong_notm}} clusters that are connected to a private VLAN only. Your worker nodes must be connected to both public and private VLANs.
{: important}

**VLAN connections for worker nodes**

All worker nodes must be connected to a private VLAN so that each worker node can send information to and receive information from other worker nodes. The private VLAN provides private subnets that are used to assign private IP addresses to your worker nodes and private app services. Your worker nodes also must be connected to a public VLAN. The public VLAN provides public subnets that are used to assign public IP addresses to your worker nodes and public app services. However, if you need to secure your apps from the public network interface, several options are available to secure your cluster such as using [Calico network policies](/docs/containers?topic=containers-network_policies) or isolating external network workloads to [edge worker nodes](/docs/containers?topic=containers-edge).

In standard clusters, the first time that you create a cluster in a zone, a public VLAN and a private VLAN in that zone are automatically provisioned for you in your IBM Cloud infrastructure account. For every subsequent cluster that you create in that zone, you can specify the VLAN pair that you want to use. You can reuse the same public and private VLANs that were created for you because multiple clusters can share VLANs.

For more information about VLANs, subnets, and IP addresses, see [Overview of networking in {{site.data.keyword.openshiftlong_notm}}](/docs/containers?topic=containers-subnets#basics).

Need to create your cluster by using custom subnets? Check out [Using existing subnets to create a cluster](/docs/containers?topic=containers-subnets#subnets_custom).
{: tip}

**Worker node communication across subnets and VLANs**

In several situations, components in your cluster must be permitted to communicate across multiple private VLANs. For example, if you want to create a multizone cluster, if you have multiple VLANs for a cluster, or if you have multiple subnets on the same VLAN, the worker nodes on different subnets in the same VLAN or in different VLANs cannot automatically communicate with each other. You must enable either Virtual Routing and Forwarding (VRF) or VLAN spanning for your IBM Cloud infrastructure account.

* [Virtual Routing and Forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf): VRF enables all the private VLANs and subnets in your infrastructure account to communicate with each other. Additionally, VRF is required to allow your workers and master to communicate over the private cloud service endpoint, and to communicate with other {{site.data.keyword.cloud_notm}} instances that support private cloud service endpoints. To check whether a VRF is already enabled, use the `ibmcloud account show` command. To enable VRF, run `ibmcloud account update --service-endpoint-enable true`. This command output prompts you to open a support case to enable your account to use VRF and service endpoints. VRF eliminates the VLAN spanning option for your account because all VLANs are able to communicate.</br></br>
When VRF is enabled, any system that is connected to any of the private VLANs in the same {{site.data.keyword.cloud_notm}} account can communicate with the cluster worker nodes. You can isolate your cluster from other systems on the private network by applying [Calico private network policies](/docs/containers?topic=containers-network_policies#isolate_workers).</dd>
* [VLAN spanning](/docs/vlans?topic=vlans-vlan-spanning#vlan-spanning): If you cannot or do not want to enable VRF, such as if you do not need the master to be accessible on the private network or if you use a gateway appliance to access the master over the public VLAN, enable VLAN spanning. For example, if you have an existing gateway appliance and then add a cluster, the new portable subnets that are ordered for the cluster aren't configured on the gateway appliance but VLAN spanning enables routing between the subnets. To enable VLAN spanning, you need the **Network > Manage Network VLAN Spanning** [infrastructure permission](/docs/containers?topic=containers-access-creds#infra_access), or you can request the account owner to enable it. To check whether VLAN spanning is already enabled, use the `ibmcloud oc vlan spanning get` [command](/docs/containers?topic=containers-kubernetes-service-cli#cs_vlan_spanning_get). You cannot enable the private cloud service endpoint if you choose to enable VLAN spanning instead of VRF.

</br>

### Worker-to-master and user-to-master communication: Service endpoints
{: #workeruser-master}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> A communication channel must be set up so that worker nodes can establish a connection to the Kubernetes master. You must enable the public cloud service endpoint in your cluster, and you can optionally enable the private cloud service endpoint. You cannot have only the private cloud service endpoint, and after you create the cluster, you cannot change the cloud service endpoints.
{: shortdesc}

To secure communication over public and private cloud service endpoints, {{site.data.keyword.openshiftlong_notm}} automatically sets up an OpenVPN connection between the Kubernetes master and the worker node when the cluster is created. Workers securely talk to the master through TLS certificates, and the master talks to workers through the OpenVPN connection.

**Public service endpoint only**

By default, your worker nodes can automatically connect to the Kubernetes master over the public VLAN through the public cloud service endpoint.
* Communication between worker nodes and master is established securely over the public network through the public cloud service endpoint.
* The master is publicly accessible to authorized cluster users only through the public cloud service endpoint. Your cluster users can securely access your Kubernetes master over the internet to run `oc` commands, for example.

**Public and private cloud service endpoints**

To make your master publicly or privately accessible to cluster users, you can enable the public and private cloud service endpoints. VRF is required in your {{site.data.keyword.cloud_notm}} account, and you must enable your account to use service endpoints. To enable VRF and service endpoints, run `ibmcloud account update --service-endpoint-enable true`.
* Communication between worker nodes and master is established over both the private network through the private cloud service endpoint and the public network through the public cloud service endpoint. By routing half of the worker-to-master traffic over the public endpoint and half over the private endpoint, your master-to-worker communication is protected from potential outages of the public or private network.
* The master is publicly accessible to authorized cluster users through the public cloud service endpoint. The master is privately accessible through the private cloud service endpoint if authorized cluster users are in your {{site.data.keyword.cloud_notm}} private network or are connected to the private network through a VPN connection or {{site.data.keyword.dl_full_notm}}. Note that you must [expose the master endpoint through a private load balancer](/docs/openshift?topic=openshift-access_cluster#access_private_se) so that users can access the master through a VPN or {{site.data.keyword.dl_full_notm}} connection.
* You can optionally secure access to your private cloud service endpoint by creating a subnet allowlist. Only authorized requests to your cluster master that originate from subnets in the allowlist are permitted through the cluster's private cloud service endpoint. For more information, see [Creating an allowlist for the private cloud service endpoint](/docs/containers?topic=containers-access_cluster#private-se-allowlist).

</br>

### Worker communication to other {{site.data.keyword.cloud_notm}} services or on-premises networks
{: #worker-services-onprem}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Allow your worker nodes to securely communicate with other {{site.data.keyword.cloud_notm}} services and to an on-premises network.
{: shortdesc}

**Communication with other {{site.data.keyword.cloud_notm}} services over the private or public network**

Your worker nodes can automatically and securely communicate with other [{{site.data.keyword.cloud_notm}} services that support private cloud service endpoints](/docs/account?topic=account-vrf-service-endpoint), such as {{site.data.keyword.registrylong}}, over your IBM Cloud infrastructure private network. If an {{site.data.keyword.cloud_notm}} service does not support private cloud service endpoints, your worker nodes must be connected to a public VLAN so that they can securely communicate with the services over the public network.

If you use Calico policies or a gateway appliance to control the public or private networks of your worker nodes, you must allow access to the public IP addresses of the services that support public cloud service endpoints, and optionally to the private IP addresses of the services that support private cloud service endpoints.
* [Allow access to services' public IP addresses in Calico policies](/docs/containers?topic=containers-network_policies#isolate_workers_public)
* [Allow access to the private IP addresses of services that support private cloud service endpoints in Calico policies](/docs/containers?topic=containers-network_policies#isolate_workers)
* [Allow access to services' public IP addresses and to the private IP addresses of services that support private cloud service endpoints in a gateway appliance firewall](/docs/containers?topic=containers-firewall#firewall_outbound)

**{{site.data.keyword.BluDirectLink}} for communication over the private network with resources in on-premises data centers**

To connect your cluster with your on-premises data center, such as with {{site.data.keyword.icpfull_notm}}, you can set up [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl). With {{site.data.keyword.dl_full_notm}}, you create a direct, private connection between your remote network environments and {{site.data.keyword.openshiftlong_notm}} without routing over the public internet.

**strongSwan IPSec VPN connection for communication over the public network with resources in on-premises data centers**
Set up a [strongSwan IPSec VPN service](https://www.strongswan.org/about.html){: external} directly in your cluster. The strongSwan IPSec VPN service provides a secure end-to-end communication channel over the internet that is based on the industry-standard Internet Protocol Security (IPSec) protocol suite. To set up a secure connection between your cluster and an on-premises network, [configure and deploy the strongSwan IPSec VPN service](/docs/containers?topic=containers-vpn#vpn-setup) directly in a pod in your cluster.

If you plan to use a gateway appliance, set up an IPSec VPN endpoint on a gateway appliance, such as a Virtual Router Appliance (Vyatta). Then, [configure the strongSwan IPSec VPN service](/docs/containers?topic=containers-vpn#vpn-setup) in your cluster to use the VPN endpoint on your gateway. If you do not want to use strongSwan, you can [set up VPN connectivity directly with VRA](/docs/containers?topic=containers-vpn#vyatta).
{: note}

If you plan to connect your cluster to on-premises networks, check out the following helpful information:
{: tip}

* You might have subnet conflicts with the IBM-provided default 172.30.0.0/16 range for pods and 172.21.0.0/16 range for services. You can avoid subnet conflicts when you [create a cluster from the CLI](/docs/containers?topic=containers-kubernetes-service-cli#cs_cluster_create) by specifying a custom subnet CIDR for pods in the `--pod-subnet` flag and a custom subnet CIDR for services in the `--service-subnet` flag.
* If your VPN solution preserves the source IP addresses of requests, you can [create custom static routes](/docs/containers?topic=containers-static-routes) to ensure that your worker nodes can route responses from your cluster back to your on-premises network.
* Note that the `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16` subnet ranges are prohibited because they are reserved for {{site.data.keyword.openshiftlong_notm}} control plane functionality.

</br>

### External communication to apps that run on worker nodes
{: #external-workers}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Allow public or private traffic requests from outside the cluster to your apps that run on worker nodes.
{: shortdesc}

**Private traffic to cluster apps**

When you deploy an app in your cluster, you might want to make the app accessible to only users and services that are on the same private network as your cluster. Private load balancing is ideal for making your app available to requests from outside the cluster without exposing the app to the general public. You can also use private load balancing to test access, request routing, and other configurations for your app before you later expose your app to the public with public network services. To allow private traffic requests from outside the cluster to your apps, you can create private Kubernetes networking services, such as private NodePorts, NLBs, and Ingress ALBs. You can then use Calico pre-DNAT policies to block traffic to public NodePorts of private networking services. For more information, see [Planning private external load balancing](/docs/openshift?topic=openshift-cs_network_planning#private_access).

**Public traffic to cluster apps**

To make your apps externally accessible from the public internet, you can create public NodePorts, network load balancers (NLBs), and Ingress application load balancers (ALBs). Public networking services connect to this public network interface by providing your app with a public IP address and, depending on the service, a public URL. When an app is publicly exposed, anyone that has the public service IP address or the URL that you set up for your app can send a request to your app. You can then use Calico pre-DNAT policies to control traffic to public networking services, such as allowing traffic from only certain source IP addresses or CIDRs and blocking all other traffic. For more information, see [Planning public external load balancing](/docs/openshift?topic=openshift-cs_network_planning#openshift_routers).

Edge worker nodes can improve the security of your cluster by allowing fewer worker nodes that are connected to public VLANs to be accessed externally and by isolating the networking workload. When you [label worker nodes as edge nodes](/docs/containers?topic=containers-edge#edge_nodes), NLB and ALB pods are deployed to only those specified worker nodes. Router pods remain deployed to the non-edge worker nodes. To also prevent other workloads from running on edge nodes, you can [taint the edge nodes](/docs/containers?topic=containers-edge#edge_workloads). Then, you can deploy both public and private NLBs and ALBs to edge nodes.

<br />

## Example scenarios for classic cluster network setups
{: #classic-scenarios}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Now that you understand the basics of cluster networking, check out some example scenarios in which various classic cluster network setups can meet your workload needs.
{: shortdesc}

### Scenario: Run internet-facing app workloads in a classic cluster
{: #internet-facing}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> In this scenario, you want to run workloads in a classic cluster that are accessible to requests from the Internet so that end users can access your apps. You want the option of isolating public access in your cluster and of controlling what public requests are permitted to your cluster. Additionally, your workers have automatic access to any {{site.data.keyword.cloud_notm}} services that you want to connect with your cluster.
{: shortdesc}

<p>
<figure>
    <img src="images/cs_clusters_planning_internet.png" alt="Architecture image for a cluster that runs internet-facing workloads"/>
    <figcaption>Network setup for a cluster that runs internet-facing workloads</figcaption>
</figure>
</p>

**Worker-to-worker communication**

To achieve this setup, you create a cluster by connecting worker nodes to public and private VLANs.

If you create the cluster with both public and private VLANs, you cannot later remove all public VLANs from that cluster. Removing all public VLANs from a cluster causes several cluster components to stop working. Instead, create a new worker pool that is connected to a private VLAN only.
{: note}

**Worker-to-master and user-to-master communication**

You can choose to allow worker-to-master and user-to-master communication over the public and private networks, or over the public network only.
* Public and private cloud service endpoints: Your account must be enabled with VRF and enabled to use service endpoints. Communication between worker nodes and master is established over both the private network through the private cloud service endpoint and the public network through the public cloud service endpoint. The master is publicly accessible to authorized cluster users through the public cloud service endpoint.
* Public service endpoint: If you don’t want to or cannot enable VRF for your account, your worker nodes and authorized cluster users can automatically connect to the Kubernetes master over the public network through the public cloud service endpoint.

**Worker communication to other services or networks**

Your worker nodes can automatically, securely communicate with other {{site.data.keyword.cloud_notm}} services that support private cloud service endpoints over your IBM Cloud infrastructure private network. If an {{site.data.keyword.cloud_notm}} service does not support private cloud service endpoints, workers can securely communicate with the services over the public network. You can lock down the public or private interfaces of worker nodes by using Calico network policies for public network or private network isolation. You might need to allow access to the public and private IP addresses of the services that you want to use in these Calico isolation policies.

If your worker nodes need to access services in private networks outside of your {{site.data.keyword.cloud_notm}} account, you can configure and deploy the strongSwan IPSec VPN service in your cluster or leverage {{site.data.keyword.cloud_notm}} {{site.data.keyword.dl_full_notm}} services to connect to these networks.

**External communication to apps that run on worker nodes**

To expose an app in your cluster to the internet, you can create a public network load balancer (NLB) or Ingress application load balancer (ALB) service. You can improve the security of your cluster by creating a pool of worker nodes that are labeled as edge nodes. The pods for public network services are deployed to the edge nodes so that external traffic workloads are isolated to only a few workers in your cluster. You can further control public traffic to the network services that expose your apps by creating Calico pre-DNAT policies, such as allowlist and blocklist policies.

Ready to get started with a cluster for this scenario? After you plan your [high availability](/docs/containers?topic=containers-ha_clusters) and [worker node](/docs/containers?topic=containers-planning_worker_nodes) setups, see [Creating clusters](/docs/containers?topic=containers-clusters).

<br />

### Scenario: Extend your on-premises data center to a classic cluster and add limited public access
{: #limited-public}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> In this scenario, you want to run workloads in a classic cluster that are accessible to services, databases, or other resources in your on-premises data center. However, you might need to provide limited public access to your cluster, and want to ensure that any public access is controlled and isolated in your cluster. For example, you might need your workers to access an {{site.data.keyword.cloud_notm}} service that does not support private cloud service endpoints, and must be accessed over the public network. Or you might need to provide limited public access to an app that runs in your cluster.
{: shortdesc}

To achieve this cluster setup, you can create a firewall by [using a gateway appliance](#vyatta-gateway).

#### Using a gateway appliance
{: #vyatta-gateway}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Allow limited public connectivity to your classic cluster by configuring a gateway appliance, such as a Virtual Router Appliance (Vyatta), as a public gateway and firewall.
{: shortdesc}

<p>
<figure>
    <img src="images/cs_clusters_planning_gateway.png" width="850" style="width:850px; border-style: none" alt="Architecture image for a cluster that uses a gateway appliance for secure public access"/>
    <figcaption>Network setup for a cluster that uses a gateway appliance for secure public access</figcaption>
</figure>
</p>

**Worker-to-worker communication, worker-to-master and user-to-master communication**

Configure a gateway appliance to provide network connectivity between your worker nodes and the master over the public network. For example, you might choose to set up a [Virtual Router Appliance](/docs/virtual-router-appliance?topic=virtual-router-appliance-about-the-vra) or a [Fortigate Security Appliance](/docs/vmwaresolutions/services?topic=vmwaresolutions-fsa_considerations).

You can set up your gateway appliance with custom network policies to provide dedicated network security for your cluster and to detect and remediate network intrusion. When you set up a firewall on the public network, you must open up the required ports and private IP addresses for each region so that the master and the worker nodes can communicate. If you also configure this firewall for the private network, you must also open up the required ports and private IP addresses to allow communication between worker nodes and let your cluster access infrastructure resources over the private network. You must also enable VLAN spanning for your account so that subnets can route on the same VLAN and across VLANs.

**Worker communication to other services or networks**

To securely connect your worker nodes and apps to an on-premises network or services outside of {{site.data.keyword.cloud_notm}}, set up an IPSec VPN endpoint on your gateway appliance and the strongSwan IPSec VPN service in your cluster to use the gateway VPN endpoint. If you do not want to use strongSwan, you can set up VPN connectivity directly with VRA.

Your worker nodes can securely communicate with other {{site.data.keyword.cloud_notm}} services and public services outside of {{site.data.keyword.cloud_notm}} through your gateway appliance. You can configure your firewall allow access to the public and private IP addresses of only the services that you want to use

**External communication to apps that run on worker nodes**

To provide private access to an app in your cluster, you can create a private network load balancer (NLB) or Ingress application load balancer (ALB) to expose your app to the private network only. If you need to provide limited public access to an app in your cluster, you can create a public NLB or ALB to expose your app. Because all traffic goes through your gateway appliance firewall, you can control public and private traffic to the network services that expose your apps by opening up the service's ports and IP addresses in your firewall to permit inbound traffic to these services.

Ready to get started with a cluster for this scenario? After you plan your [high availability](/docs/containers?topic=containers-ha_clusters) and [worker node](/docs/containers?topic=containers-planning_worker_nodes) setups, see [Creating clusters](/docs/containers?topic=containers-clusters).

<br />



