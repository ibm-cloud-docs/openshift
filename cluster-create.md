---

copyright: 
  years: 2014, 2023
lastupdated: "2023-08-03"

keywords: openshift, clusters, worker nodes, worker pools

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Preparing your account to create clusters
{: #clusters}



Complete the following steps to prepare your account for creating {{site.data.keyword.openshiftlong_notm}} clusters.
{: shortdesc}


After the account administrator makes these preparations, you might not need to change them each time that you create a cluster. However, each time that you create a cluster, you still want to verify that the current account-level state is what you need it to be.


1. [Create or upgrade your account to a billable account ({{site.data.keyword.cloud_notm}} Pay-As-You-Go or Subscription)](https://cloud.ibm.com/registration).{: #cluster_prepare}

2. [Set up an API key for {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-access-creds) in the region and resource groups where you want to create clusters. Assign the API key with the [required service and infrastructure permissions to create clusters](/docs/openshift?topic=openshift-access_reference#cluster_create_permissions).
    Are you the account owner? You already have the necessary permissions! When you create a cluster, the API key for that region and resource group is set with your credentials.
    {: tip}

3. Verify that you as a user (not just the API key) have the required permissions to create clusters.
    1. From the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external} menu bar, click **Manage > Access (IAM)**.
    2. Click the **Users** page, and then from the table, select yourself.
    3. From the **Access policies** tab, confirm that you [have the required permissions to create clusters](/docs/openshift?topic=openshift-access_reference#cluster_create_permissions). Make sure that your account administrator does not assign you the **Administrator** platform access role at the same time as scoping the access policy to a namespace.

4. If your account uses multiple resource groups, figure out your account's strategy for [managing resource groups](/docs/openshift?topic=openshift-access-overview#resource_groups).
    * The cluster is created in the resource group that you target when you log in to {{site.data.keyword.cloud_notm}}. If you don't target a resource group, the default resource group is automatically targeted.
    * If you want to create a cluster in a different resource group than the default, you need at least the **Viewer** role for the resource group. If you don't have any role for the resource group, your cluster is created in the default resource group.
    * You can't change a cluster's resource group.
    * If you need to use the `ibmcloud oc cluster service bind` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_service_bind) to [integrate with an {{site.data.keyword.cloud_notm}} service](/docs/openshift?topic=openshift-service-binding#bind-services), that service must be in the same resource group as the cluster. Services that don't use resource groups like {{site.data.keyword.registrylong_notm}} or that don't need service binding like {{site.data.keyword.la_full_notm}} work even if the cluster is in a different resource group.
    * Consider giving clusters unique names across resource groups and regions in your account to avoid naming conflicts. You can't rename a cluster.

5. **Classic clusters only**: Consider [creating a reservation](/docs/openshift?topic=openshift-reservations) to lock in a discount over 1 or 3 year terms for your worker nodes. After you create the cluster, add worker pools that use the reserved instances. Typical savings range between 30-50% compared to regular worker node costs.

6. **VPC clusters only**: Set up your IBM Cloud infrastructure networking to allow worker-to-master and user-to-master communication. Your VPC clusters are created with a public and a private cloud service endpoint by default. **Optional**: If you want your VPC clusters to communicate with classic clusters over the private network interface, you can choose to set up classic infrastructure access from the VPC that your cluster is in. Note that you can set up classic infrastructure access for only one VPC per region and [Virtual Routing and Forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf) is required in your {{site.data.keyword.cloud_notm}} account. For more information, see [Setting up access to your Classic Infrastructure from VPC](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure).




Looking for a fast way to create a cluster from the UI? Try out [Automating cluster creation with {{site.data.keyword.bpfull_notm}} templates](/docs/openshift?topic=openshift-templates).
{: preview}




## Create a cluster
{: #next_steps}

- [Create a classic cluster](/docs/openshift?topic=openshift-cluster-create-classic).
- [Create a VPC cluster](/docs/openshift?topic=openshift-cluster-create-vpc-gen2).



