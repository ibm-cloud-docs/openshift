---

copyright: 
  years: 2014, 2024
lastupdated: "2024-03-15"


keywords: openshift, kubernetes, infrastructure, rbac, policy

subcollection: openshift


---


{{site.data.keyword.attribute-definition-list}}


# Setting which credentials to use for creating clusters
{: #access-creds}
{: help}
{: support}

To successfully provision and work with clusters, you must ensure that your {{site.data.keyword.cloud_notm}} account is correctly set up to access infrastructure and other services that you use in each resource group and region that your clusters are in.
{: shortdesc}

{{site.data.keyword.openshiftlong_notm}} accesses the infrastructure portfolio and other services that you use in your cluster by using an [API key](/docs/account?topic=account-manapikey). This API key stores the credentials of a user in the account to the infrastructure and other services. {{site.data.keyword.openshiftlong_notm}} uses the API key to order resources in the service, such as new worker nodes or VLANs in IBM Cloud infrastructure.

By default, the account owner's credentials are stored in the API key. However, to avoid tying your cluster resources to a specific user, such as the account owner, consider using a functional ID instead of a personal user.


## Setting the cluster credentials
{: #admin-set-credentials}

1. As the account owner, [invite a functional ID](/docs/account?topic=account-iamuserinv) to your {{site.data.keyword.cloud_notm}}.
1. [Assign the functional ID the correct permissions](/docs/openshift?topic=openshift-iam-platform-access-roles).
1. Log in as the functional ID.
    ```sh
    ibmcloud login
    ```
    {: pre}

1. Target the resource group where you want to set the API key.

    If you don't target a resource group, the API key is set for the default resource group. To list available resource groups, run `ibmcloud resource groups`.
    {: note }

    ```sh
    ibmcloud target -g <resource_group_name>
    ```
    {: pre}

1. Create an API key.
    ```sh
    ibmcloud oc api-key reset --region <region>
    ```
    {: pre}    

1. Verify that the API key is set up.
    ```sh
    ibmcloud oc api-key info --cluster <cluster_name_or_ID>
    ```
    {: pre}

1. Repeat these steps for each region and resource group that you want to create clusters in.



