---

copyright: 
  years: 2022, 2026
lastupdated: "2026-08-11"


keywords: access, private, ,openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}






# Accessing private clusters
{: #cluster-access-wireguard}


When you have an {{site.data.keyword.redhat_openshift_notm}} cluster created with a private-only endpoint, you might need to access your cluster from outside of {{site.data.keyword.cloud_notm}}. 
{: shortdesc}

The {{site.data.keyword.redhat_openshift_notm}} master is accessible through the private cloud service endpoint if authorized cluster users are in your {{site.data.keyword.cloud_notm}} private network or are connected to the private network. You can set up a client-to-site or site-to-site VPN to access your private clusters. For more information, see [VPNs for VPC overview](/docs/vpc?topic=vpc-vpn-overview).
