---

copyright: 
  years: 2014, 2025
lastupdated: "2025-09-26"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, infrastructure, rbac, policy

subcollection: openshift


---


{{site.data.keyword.attribute-definition-list}}


# Setting the cluster credentials 
{: #access-creds}
{: help}
{: support}

{{site.data.keyword.openshiftlong_notm}} accesses the infrastructure portfolio and other services that you use in your cluster by using an [API key](/docs/account?topic=account-manapikey). This API key stores the credentials of a user in the account to the infrastructure and other services. {{site.data.keyword.openshiftlong_notm}} uses the API key to order resources in the service, such as new worker nodes or VLANs in IBM Cloud infrastructure.
{: shortdesc}

By default, the account owner's credentials are stored in the API key. However, to avoid tying your cluster resources to a specific user, such as the account owner, consider using a [functional ID](/docs/account?topic=account-identity-overview#functionalid-bestpract) instead of a personal user. If an account owner leaves the organization or is removed from the account, a functional ID prevents other users from losing access to the account and prevents disruptions to services and commands requiring certain credentials that might not be available after the account owner leaves.

Need to remove a user from your account? Make sure you reset your API key. See [Removing user credentials and permissions](#apikey-remove-user).
{: tip}

## Resetting the cluster API key
{: #admin-set-credentials}

Complete the following steps to reset the API key that is used by the cluster. When the API key is reset, the previous API key that was used, if any, for the region and resource group is now obsolete. You can then delete the old API key from your list of API keys.

Before you begin:

- If you use the {{site.data.keyword.block_storage_is_short}} or cluster autoscaler add-ons in your cluster, you must re-create the add-on pods after you reset your API key. For more information, see [{{site.data.keyword.block_storage_is_short}} PVC creation fails after API key reset](/docs/openshift?topic=openshift-vpc-block-api-key-reset-ts) and [Autoscaling fails after API key reset](/docs/openshift?topic=openshift-ts-storage-ca-apikey-reset).

- Make sure that the identity that is used to run this command has the required [Administrator platform role in {{site.data.keyword.containerlong_notm}}](/docs/openshift?topic=openshift-iam-platform-access-roles), the Operator platform role in the IAM Identity Service if you are using a service ID, and also the required permissions for the other services or integrations. Target the resource group and region that you want to set the API key for. The user that runs the `api-key reset` command replaces the API key associated with the targeted resource group in the specified region. If that user doesn't have sufficient permissions, other users in the resource group in the specified region might be impacted.

To reset the cluster API key:

1. As the account owner, [invite a functional ID](/docs/account?topic=account-iamuserinv) to your {{site.data.keyword.cloud_notm}}.
1. [Assign the functional ID the correct permissions](/docs/openshift?topic=openshift-iam-platform-access-roles).
1. Log in as the functional ID or user whose credentials you want to use in the cluster.
    ```sh
    ibmcloud login
    ```
    {: pre}

1. Target the resource group the cluster is in.

    If you don't target a resource group, the API key is set for the default resource group. To list available resource groups, run `ibmcloud resource groups`.
    {: note }

    ```sh
    ibmcloud target -g <resource_group_name>
    ```
    {: pre}

1. Reset the API key.
    ```sh
    ibmcloud oc api-key reset --region <region>
    ```
    {: pre}    

1. Verify that the API key is set up.
    ```sh
    ibmcloud oc api-key info --cluster <cluster_name_or_ID>
    ```
    {: pre}

1. Repeat these steps for each region and resource group where you want to reset the cluster API key.


## Removing user credentials and permissions
{: #apikey-remove-user}

In certain scenarios, such as staffing changes, your organization might need to remove user credentials and permissions from your account. To ensure that processes requiring certain user credentials are not disrupted when a user is removed from the account, you must reset the API key with another user's infrastructure credentials. For more information, see [Removing users](/docs/openshift?topic=openshift-removing-user-permissions).
