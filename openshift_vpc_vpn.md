---

copyright:
  years: 2014, 2020
lastupdated: "2020-06-15"

keywords: openshift, roks, rhoks, rhos, strongswan, ipsec, on-prem, vpnaas, direct link

subcollection: openshift

---

{:beta: .beta}
{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}



# VPC: Setting up VPN connectivity
{: #vpc-vpnaas}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> This VPN information is specific to VPC clusters. For VPN information for classic clusters, see [Setting up VPN connectivity](/docs/openshift?topic=openshift-vpn).
{: note}

With VPN connectivity, you can securely connect apps and services in a VPC cluster in {{site.data.keyword.openshiftlong}} to on-premises networks, other VPCs, and {{site.data.keyword.cloud_notm}} classic infrastructure resources. You can also connect apps that are external to your cluster to an app that runs inside your cluster.
{: shortdesc}

## Choosing a VPN solution
{: #options}

Choose a VPC VPN connection solution based on which resources or networks you want to connect your cluster to.
{: shortdesc}

### Communication with resources in on-premises data centers
{: #onprem}

To connect your cluster with your on-premises data center, you can set up the {{site.data.keyword.vpc_short}} VPN service.
{: shortdesc}

With the {{site.data.keyword.vpc_short}} VPN, you connect an entire VPC to an on-premises data center or to another VPC. This option allows you to remain VPC-native in you VPN connection setup. To get started:
1. [Configure an on-prem VPN gateway](/docs/vpc?topic=vpc-vpn-onprem-example#configuring-onprem-gateway).
2. [Create a VPN gateway in your VPC, and create the connection between the VPC VPN gateway and your local VPN gateway](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console#vpn-ui). If you have a multizone cluster, you must create a VPC gateway on a subnet in each zone where you have worker nodes.

<p class="tip">If you plan to connect your cluster to on-premises networks, check out the following helpful features:<br><br>You might have subnet conflicts with the IBM-provided default 172.30.0.0/16 range for pods and 172.21.0.0/16 range for services. You can avoid subnet conflicts when you [create a cluster from the CLI](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-vpc-classic) by specifying a custom subnet CIDR for pods in the `--pod-subnet` flag and a custom subnet CIDR for services in the `--service-subnet` flag.<br><br>If your VPN solution preserves the source IP addresses of requests, you can [create custom static routes](/docs/openshift?topic=openshift-static-routes) to ensure that your worker nodes can route responses from your cluster back to your on-premises network.</p>

### Communication with resources in other VPCs
{: #vpc-vpc}

To connect an entire VPC to another VPC in your account, you can use the {{site.data.keyword.vpc_short}} VPN.
{: shortdesc}

For example, you can connect subnets in a VPC in one region through a VPN connection to subnets in a VPC in another region. To get started: by creating a VPC gateway for your subnets, see [Using VPN with your VPC](/docs/vpc?topic=vpc-vpn-onprem-example). Note that if you use [access control lists (ACLs)](/docs/openshift?topic=openshift-vpc-network-policy) for your VPC subnets, you must create inbound or outbound rules to allow your worker nodes to communicate with the subnets in other VPCs.

### Communication with {{site.data.keyword.cloud_notm}} classic resources
{: #vpc-classic}

If you need to connect your cluster to resources in your {{site.data.keyword.cloud_notm}} classic infrastructure, you can set up access between a VPC and one {{site.data.keyword.cloud_notm}} classic infrastructure account.
{: shortdesc}

Before you connect a VPC to a classic infrastructure account, note the following limitations and requirements:
* You must enable the VPC for classic access when you create the VPC. You cannot convert an existing VPC to use classic access.
* You can set up classic infrastructure access for only one VPC per region. You cannot set up more than one VPC with classic infrastructure access in a region.
* [Virtual Routing and Forwarding (VRF)](/docs/dl?topic=dl-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) is required in your {{site.data.keyword.cloud_notm}} account.

To get started, see [Setting up access to classic infrastructure](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure).

When you create a VPC with classic infrastructure access, you can set up an [{{site.data.keyword.cloud_notm}} Direct Link](/docs/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link) connection between your classic infrastructure and your remote networks. Any clusters that you create in the VPC with classic infrastructure access can access the Direct Link connection.
{: tip}


