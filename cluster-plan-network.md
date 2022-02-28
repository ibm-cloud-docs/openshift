---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-28"

keywords: openshift, multi az, multi-az, szr, mzr

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Planning your cluster network setup   
{: #plan_clusters}

Design a network setup for your {{site.data.keyword.openshiftlong}} cluster that meets the needs of your workloads and environment.
{: shortdesc}

Get started by planning your setup for a VPC or a classic cluster.
- ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) With [{{site.data.keyword.openshiftlong_notm}} clusters in VPC](#plan_vpc_basics), you can create your cluster in the next generation of the {{site.data.keyword.cloud_notm}} platform, in [Virtual Private Cloud](/docs/vpc?topic=vpc-about-vpc) for Generation 2 compute resources. VPC gives you the security of a private cloud environment with the dynamic scalability of a public cloud.
- ![Classic infrastructure provider icon.](images/icon-classic-2.svg) With [{{site.data.keyword.openshiftlong_notm}} classic clusters](#plan_basics), you can create your cluster on classic infrastructure. Classic clusters include all the {{site.data.keyword.openshiftlong_notm}} mature and robust features for compute, networking, and storage.

First time creating a cluster? First, try out the [tutorial for creating a VPC cluster](/docs/openshift?topic=openshift-vpc_rh_tutorial) or the [tutorial for creating {{site.data.keyword.openshiftshort}} clusters](/docs/openshift?topic=openshift-openshift_tutorial). Then, come back here when you’re ready to plan out your production-ready clusters.
{: tip}

Review the following cluster configurations and take the appropriate action in your account before provisioning your clusters. For more information, see [Preparing to create clusters at the account level](/docs/openshift?topic=openshift-clusters#cluster_prepare).

- For VPC Clusters that don't require Classic Infrastructure Access, no account changes are required.

- For VPC Clusters that require Classic Infrastructure Access, you must [enable VRF](/docs/account?topic=account-vrf-service-endpoint&interface=ui#vrf) & [service endpoints](/docs/account?topic=account-vrf-service-endpoint&interface=ui#service-endpoint) in your account.

- For Classic clusters with a private service endpoint enabled, you must [enable VRF](/docs/account?topic=account-vrf-service-endpoint&interface=ui#vrf) & [service endpoints](/docs/account?topic=account-vrf-service-endpoint&interface=ui#service-endpoint).






