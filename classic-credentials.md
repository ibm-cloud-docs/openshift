---

copyright:
  years: 2024, 2024
lastupdated: "2024-05-10"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, clusters, access, endpoint, credentials, classic

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# Understanding Classic infrastructure credentials
{: #classic-credentials}

Determine whether your account has access to the IBM Cloud infrastructure portfolio and learn about how {{site.data.keyword.openshiftlong_notm}} uses the API key to access the portfolio.

Access to {{site.data.keyword.cloud_notm}} infrastructure works differently in Classic clusters. Infrastructure resources for Classic clusters are created in a separate {{site.data.keyword.cloud_notm}} infrastructure account. Usually, your Pay-As-You-Go or Subscription account is linked to the {{site.data.keyword.cloud_notm}} infrastructure account so that account owners can access classic infrastructure automatically. To authorize other users to access classic compute, storage, and networking resources, you must assign [classic infrastructure roles](/docs/openshift?topic=openshift-iam-platform-access-roles).

To access the IBM Cloud infrastructure portfolio, you use an {{site.data.keyword.cloud_notm}} Pay-As-You-Go or Subscription account.


You have two separate IBM Cloud infrastructure accounts and billing. By default, your new {{site.data.keyword.cloud_notm}} account uses the new infrastructure account. To continue using the previous classic infrastructure account, manually set the credentials.


## Accessing a different classic infrastructure account
{: #credentials}

Instead of using the default linked IBM Cloud infrastructure account to order infrastructure for clusters within a region, you might want to use a different IBM Cloud infrastructure account that you already have. You can link this infrastructure account to your {{site.data.keyword.cloud_notm}} account by using the [`ibmcloud oc credential set`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_set) command. The IBM Cloud infrastructure credentials are used instead of the default Pay-As-You-Go or Subscription account's credentials that are stored for the region.
{: shortdesc}

You can manually set infrastructure credentials to a different account only for classic clusters, not for VPC clusters.
{: note}

The IBM Cloud infrastructure credentials that are set by the `ibmcloud oc credential set` command persist after your session ends. If you remove IBM Cloud infrastructure credentials that were manually set with the [`ibmcloud oc credential unset --region <region>`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_unset) command, the credentials of the Pay-As-You-Go or Subscription account are used instead. Note that this change can cause [orphaned clusters](/docs/openshift?topic=openshift-cluster_infra_errors).
{: important}

**Before you begin**:
- If you are not using the account owner's credentials, [ensure that the user whose credentials you want to set for the API key has the correct permissions](/docs/openshift?topic=openshift-iam-platform-access-roles).
- [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

To set infrastructure account credentials to access the IBM Cloud infrastructure portfolio:

1. Get the infrastructure account that you want to use to access the IBM Cloud infrastructure portfolio.


1. Find and record your `infrastructure username`. You use this username when you set API credentials. 
    ```sh
    ibmcloud oc ibmcloud sl user list
    ```
    {: pre}   

    1. Set the infrastructure API credentials to use.
        ```sh
        ibmcloud oc credential set classic --infrastructure-username <infrastructure_API_username> --infrastructure-api-key <infrastructure_API_authentication_key> --region <region>
        ```
        {: pre}

    1. Verify that the correct credentials are set.
        ```sh
        ibmcloud oc credential get --region <region>
        ```
        {: pre}

        Example output
        ```sh
        Infrastructure credentials for user name user@email.com set for resource group default.
        ```
        {: screen}

1. [Create a cluster](/docs/openshift?topic=openshift-clusters). To create the cluster, the infrastructure credentials that you set for the region and resource group are used.

1. Verify that your cluster uses the infrastructure account credentials that you set.
    1. Open the [{{site.data.keyword.cloud_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters){: external} and select your cluster. 
    1. In the Overview tab, look for an **Infrastructure User** field. 
    1. If you see that field, you don't use the default infrastructure credentials that come with your Pay-As-You-Go or Subscription account in this region. Instead, the region is set to use the different infrastructure account credentials that you set.



