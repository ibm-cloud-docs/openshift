---

copyright: 
  years: 2022, 2023
lastupdated: "2023-11-21"

keywords: access, private, ,openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}






# Accessing private clusters
{: #cluster-access-wireguard}


When you have an {{site.data.keyword.redhat_openshift_notm}} cluster created with a private-only endpoint, you might need to access your cluster from outside of {{site.data.keyword.cloud_notm}}. 
{: shortdesc}

The {{site.data.keyword.redhat_openshift_notm}} master is accessible through the private cloud service endpoint if authorized cluster users are in your {{site.data.keyword.cloud_notm}} private network or are connected to the private network. There are two ways to set up your VPN to access your private clusters: client-to-site or site-to-site. For more details, see [VPNs for VPC overview](/docs/vpc?topic=vpc-vpn-overview). 

To understand the fundamentals about how to apply the client-to-site VPN in {{site.data.keyword.cloud_notm}} to access private clusters, start with this [blog](https://community.ibm.com/community/user/cloud/blogs/neela-shah/2023/11/17/on-the-go-client-to-site-vpc-vpn-to-the-rescue){: external}. This blog article does a walkthrough of creating a client-to-site VPN service that you can use to connect client machines such as Macs and PCs to your {{site.data.keyword.cloud_notm}} VPC network, {{site.data.keyword.redhat_openshift_notm}} clusters, Cloud Service Endpoints (CSE),  IaaS services, and to your private classic subnets.  

