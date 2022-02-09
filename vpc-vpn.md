---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-09"

keywords: openshift, strongswan, ipsec, on-prem, vpnaas, direct link

subcollection: openshift


---


{{site.data.keyword.attribute-definition-list}}


# Setting up VPC VPN connectivity
{: #vpc-vpnaas}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) This VPN information is specific to VPC clusters. For VPN information for classic clusters, see [Setting up VPN connectivity](/docs/containers?topic=containers-vpn).
{: note}

Securely connect apps and services in a VPC cluster in {{site.data.keyword.openshiftlong}} to on-premises networks, other VPCs, and {{site.data.keyword.cloud_notm}} classic infrastructure resources. You can also connect apps that are external to your cluster to an app that runs inside your cluster.
{: shortdesc}

The following table compares the connection options that are available based on the type of destination that you want to connect your VPC cluster to.

| Destination | {{site.data.keyword.vpc_short}} VPN | {{site.data.keyword.tg_short}} | {{site.data.keyword.dl_short}} | Classic-access VPC |
|---|---|---|---|---|
| [On-premises networks](#onprem) |Yes||Yes||
| [Other VPCs](#vpc-vpc) |Yes|Yes|||
| [Classic infrastructure resources](#vpc-classic) ||Yes||Yes|
{: caption="Comparison of connection options based on destination type" caption-side="top"}

## Communication with resources in on-premises data centers
{: #onprem}

To connect your cluster with your on-premises data center, you can use the {{site.data.keyword.vpc_full}} VPN or {{site.data.keyword.dl_full}}.
{: shortdesc}

You might have subnet conflicts with the IBM-provided default 172.30.0.0/16 range for pods and 172.21.0.0/16 range for services. You can avoid subnet conflicts when you [create a cluster from the CLI](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-vpc-gen2) by specifying a custom subnet CIDR for pods in the `--pod-subnet` flag and a custom subnet CIDR for services in the `--service-subnet` flag.

If your VPN solution preserves the source IP addresses of requests, you can [create custom static routes](/docs/containers?topic=containers-static-routes) to ensure that your worker nodes can route responses from your cluster back to your on-premises network.

The `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16` subnet ranges are prohibited because they are reserved for {{site.data.keyword.openshiftlong_notm}} control plane functionality.
{: note}

### {{site.data.keyword.vpc_short}} VPN
{: #vpc-vpn-def}

With the {{site.data.keyword.vpc_short}} VPN, you connect an entire VPC to an on-premises data center. This option allows you to remain VPC-native in you VPN connection setup. To get started:
1. [Configure an on-prem VPN gateway](/docs/vpc?topic=vpc-vpn-onprem-example#configuring-onprem-gateway).
2. [Create a VPN gateway in your VPC, and create the connection between the VPC VPN gateway and your local VPN gateway](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console#vpn-ui). If you have a multizone cluster, you must create a VPC gateway on a subnet in each zone where you have worker nodes.

### {{site.data.keyword.dl_short}}
{: #vpc-directlink-def}

With {{site.data.keyword.dl_short}}, you can create a direct, private connection between your remote network environments and {{site.data.keyword.openshiftlong_notm}} without routing over the public internet. [{{site.data.keyword.dl_full_notm}} (2.0)](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl) is configured for native integration with VPC. Any clusters that you create in the VPC can access the {{site.data.keyword.dl_short}} connection.

To get started, see [Ordering {{site.data.keyword.dl_full_notm}} Dedicated](/docs/dl?topic=dl-how-to-order-ibm-cloud-dl-dedicated). In step 8, you can create a network connection to your VPC to be attached to the {{site.data.keyword.dl_short}} gateway.


## Communication with resources in other VPCs
{: #vpc-vpc}

To connect an entire VPC to another VPC in your account, you can use the {{site.data.keyword.vpc_short}} VPN or {{site.data.keyword.tg_full}}.
{: shortdesc}

### {{site.data.keyword.vpc_short}} VPN
{: #vpc-vpn-other}

Create a VPC gateway on a subnet in each VPC and create a VPN connection between the two VPC gateways. For example, you can connect subnets in a VPC in one region through a VPN connection to subnets in a VPC in another region. To get started, follow the steps in [Connecting two VPCs using VPN](/docs/vpc?topic=vpc-vpn-example). Note that if you use [access control lists (ACLs)](/docs/containers?topic=containers-vpc-network-policy) for your VPC subnets, you must create inbound or outbound rules to allow your worker nodes to communicate with the subnets in other VPCs.

### {{site.data.keyword.tg_full_notm}}
{: #vpc-transit-def}

Use {{site.data.keyword.tg_full_notm}} to manage access between your VPCs. {{site.data.keyword.tg_short}} instances can be configured to route between VPCs that are in the same region (local routing) or VPCs that are in different regions (global routing). To get started, see the [{{site.data.keyword.tg_short}} documentation](/docs/transit-gateway?topic=transit-gateway-getting-started).


## Communication with {{site.data.keyword.cloud_notm}} classic resources
{: #vpc-classic}

If you need to connect your cluster to resources in your {{site.data.keyword.cloud_notm}} classic infrastructure, you can set up a VPC with classic access or use {{site.data.keyword.tg_full_notm}}.
{: shortdesc}

### Create a classic-access VPC
{: #vpc-create-classic}

If you plan to connect only one VPC to classic infrastructure, you can set up a VPC for classic access. Every virtual server instance or bare metal server without a public interface on your classic infrastructure in your account can send and receive packets to and from instances in the VPC.

Before you connect a VPC to a classic infrastructure account, note the following limitations and requirements:
* You must enable the VPC for classic access when you create the VPC. You can't convert an existing VPC to use classic access.
* You can set up classic infrastructure access for only one VPC per region. You can't set up more than one VPC with classic infrastructure access in a region.
* [Virtual Routing and Forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf) is required in your {{site.data.keyword.cloud_notm}} account.

To get started, see [Setting up access to classic infrastructure](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure).

### Use {{site.data.keyword.tg_full_notm}}
{: #vpc-use-transit-gw}

If you plan to connect multiple VPCs to classic infrastructure, you can use {{site.data.keyword.tg_full_notm}} to manage access between your VPCs in multiple regions to resources in your {{site.data.keyword.cloud_notm}} classic infrastructure. To get started, see the [{{site.data.keyword.tg_short}} documentation](/docs/transit-gateway?topic=transit-gateway-getting-started).




