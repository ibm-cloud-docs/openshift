---

copyright: 
  years: 2023, 2024
lastupdated: "2024-03-07"


keywords: openshift, kubernetes, oauth, console, access, vpe, pse, network

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Setting the OAuth access type for VPC clusters
{: #setting-oauth-access-type}

[Virtual Private Cloud]{: tag-vpc}

You can set the OpenShift console and OAuth exposure method for private-only {{site.data.keyword.openshiftlong_notm}} clusters on VPC infrastructure.
{: shortdesc}

Choose between the following options when setting the OpenShift console and OAuth exposure method.

Virtual Private Endpoint Gateway
:   This is default access type for version 4.13. For more information, see [Accessing VPC clusters through the VPE gateway](/docs/openshift?topic=openshift-access_cluster#vpc_vpe).

Private Service Endpoint URL
:   This is default access type for cluster versions 4.12 and earlier and 4.14 and later. For more information, see [Accessing clusters through the private cloud service endpoint](/docs/openshift?topic=openshift-access_cluster#access_private_se).

Setting the Virtual Private Endpoint Gateway for OAuth and console as the default behavior for all clusters is available on an allowlist basis. To request that your account be allowlisted, see [Requesting access to allowlisted features](/docs/openshift?topic=openshift-get-help).
{: tip}


## Setting the OAuth access type for a cluster from the API
{: #oauth-access-set-api}
{: api}

You can use the `POST /network/v2/oauth-access-type/{idOrName}/set` API to set the access type for your cluster.


1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
1. Get the name or ID of your cluster. To list the clusters that you have access to, use the `GET /v1/clusters` API or run `ibmcloud ks cluster ls`.
1. [Generate an IAM token](/docs/account?topic=account-iamtoken_from_apikey&interface=ui).

1. Run the following request. Replace `{idOrName}` with the name or ID of your cluster.

    ```sh
    curl -X POST "https://containers.cloud.ibm.com/network/v2/oauth-access-type/{idOrName}/set" -H "accept: application/json" -H "Authorization: TOKEN" -H "X-Auth-Resource-Group: RESOURCE-GROUP" -H "Content-Type: application/json" -d "{ \"oauth_access_type\": \"string\"}"
    ```
    {: pre}

    `oauth-access-type`
    :   `vpegw`: Specify `vpegw` to expose the OpenShift console and OAuth using the Virtual Private Endpoint gateway.
    :   `legacy`: Specify `legacy` to expose the OpenShift console and OAuth using the Private Service Endpoint URL.

1. Review the output and verify the OAuth access type is set.

1. After setting the access type, you must perform a [cluster master refresh](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_apiserver_refresh).
    ```sh
    ibmcloud oc cluster master refresh --cluster CLUSTER
    ```
    {: pre}


## Getting the OAuth access type for a cluster from the API
{: #oauth-access-get-api}
{: api}

You can use the `GET /network/v2/oauth-access-type/{idOrName}` API to get the access type details for your cluster.

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
1. Get the name or ID of your cluster. To list the clusters that you have access to, use the `GET /v1/clusters` API or run `ibmcloud ks cluster ls`.
1. Run the following request.

    ```sh
    curl -X GET "https://containers.cloud.ibm.com/global/network/v2/oauth-access-type/{idORName}" -H "accept: application/json" -H "Authorization: TOKEN" -H "X-Auth-Resource-Group: RESOURCE-GROUP" -H "Content-Type: application/json"
    ```
    {: pre}


1. Review the output and verify the OAuth access type.
   - [4.13 clusters]{: tag-red}: If the value is empty, the `vpegw` behavior is being used.
   - [4.14 clusters]{: tag-red}: If the value is empty, the `legacy` behavior is being used.


