---

copyright: 
  years: 2014, 2025
lastupdated: "2025-07-29"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, clusters, worker nodes, worker pools

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Preparing your account to create clusters
{: #clusters}

Complete the following steps to prepare your account for creating {{site.data.keyword.openshiftlong_notm}} clusters.
{: shortdesc}

After the account administrator makes these preparations, you might not need to change them each time that you create a cluster. However, each time that you create a cluster, you still want to verify that the current account-level state is what you need it to be.


## Create or upgrade your account
{: #prepare-create-account}
{: step}

[Create or upgrade your account to a billable account ({{site.data.keyword.cloud_notm}} Pay-As-You-Go or Subscription)](https://cloud.ibm.com/registration).{: #cluster_prepare}


## Set user permissions
{: #prepare-verify-permissions}
{: step}

Confirm that you [have the required permissions to create clusters](/docs/openshift?topic=openshift-iam-platform-access-roles). Make sure that your account administrator does not assign you the **Administrator** platform access role at the same time as scoping the access policy to a namespace. Otherwise, the permissions might not be set properly.



## Plan your resource groups
{: #prepare-resource-groups}
{: step}

If your account uses multiple resource groups, figure out your account's strategy for [managing resource groups](/docs/openshift?topic=openshift-iam-platform-access-roles). You might want one resource group and create all clusters within that one. You might want to set up different resource groups to group different environments or resource types.


Keep in mind:
    * To create a cluster in a different resource group than the default, you need at least the **Viewer** role for the resource group. If you don't have any role for the resource group, your cluster is created in the default resource group.


## Cluster-specific account setup
{: #prepare-cluster-account}
{: step}

If you know what kind of cluster you need already, you can start thinking about what kind of cluster-specific setup tasks you might complete. If you don't know what kind of cluster you need yet, no worries! You can make these decisions later.

1. **Classic clusters only**: Consider [creating a reservation](/docs/openshift?topic=openshift-reservations) to lock in a discount over 1 or 3 year terms for your worker nodes. After you create the cluster, add worker pools that use the reserved instances. Typical savings range between 30-50% compared to regular worker node costs.

1. **VPC clusters only**: Set up your IBM Cloud infrastructure networking to allow worker-to-master and user-to-master communication. Your VPC clusters are created with a public and a private cloud service endpoint by default. **Optional**: If you want your VPC clusters to communicate with classic clusters over the private network interface, you can choose to set up classic infrastructure access from the VPC that your cluster is in. Note that you can set up classic infrastructure access for only one VPC per region and [Virtual Routing and Forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint&interface=ui) is required in your {{site.data.keyword.cloud_notm}} account. For more information, see [Setting up access to your Classic Infrastructure from VPC](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure).


## Next steps
{: #next-steps}
{: step}

[Set up an API key for {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-access-creds) in the region and resource groups where you want to create clusters. 
