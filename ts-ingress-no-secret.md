---

copyright: 
  years: 2014, 2022
lastupdated: "2022-11-21"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}




# Why does no Ingress secret exist after cluster creation?
{: #ingress_secret}
{: support}

Supported infrastructure providers
:   Classic
:   VPC


When you run `ibmcloud oc ingress status-report get -c <cluster_name_or_ID>`, one of the following messages continues to be displayed:
{: tsSymptoms}

```sh
Creating TLS certificate for Ingress subdomain, which might take several minutes. Ensure you have the correct IAM permissions.
```
{: screen}

```sh
Could not upload certificates to Certificate Manager instance. Ensure you have the correct IAM service permissions.
```
{: screen}

```sh
Could not create a Certificate Manager instance. Ensure you have the correct IAM platform permissions.
```
{: screen}


When you run `ibmcloud oc ingress secret ls`, no secrets are listed.

Previously, an [{{site.data.keyword.cloudcerts_long}}](/docs/certificate-manager?topic=certificate-manager-about-certificate-manager) instance was automatically created for each cluster and used to manage the cluster's Ingress TLS certificates. Automatic provisioning is no longer supported for new clusters. However, for exisiting {{site.data.keyword.cloudcerts_short}} instances to continue managing certificates in a cluster, the API key for the region and resource group that the cluster is created in must have the correct IAM permissions. 
{: tsCauses}

{{site.data.keyword.cloudcerts_short}} is deprecated and instances are no longer automatically provisioned in new clusters. Support for {{site.data.keyword.cloudcerts_short}} ends on 1 December 2022 and any remaining {{site.data.keyword.cloudcerts_short}} instances are set to be deleted on 31 Dec 2022. After this date, certificates are set to be written only to the cluster unless you set up a {{site.data.keyword.secrets-manager_short}} instance. [Migrate your certificates to IBM Cloud {{site.data.keyword.secrets-manager_short}}](/docs/openshift?topic=openshift-certs-mgr-migration) as soon as possible.
{: deprecated}


Also, if you used the same cluster name repeatedly, you might have a rate limiting issue. For more information, see [No Ingress subdomain exists after you create clusters of the same or similar name](/docs/openshift?topic=openshift-cs_rate_limit).


1. Check the ID of the user or functional user who sets the API key for this cluster.
{: tsResolve}

    ```sh
    ibmcloud oc api-key info -c <cluster_name_or_ID>
    ```
    {: pre}

2. [Assign the following IAM permissions](/docs/openshift?topic=openshift-users#add_users) to the user or functional user who sets the API key.
    * The **Administrator** or **Editor** platform access role for {{site.data.keyword.cloudcerts_short}} in **All resource groups**
    * The **Manager** service access role for {{site.data.keyword.cloudcerts_short}} in **All resource groups**
3. The user must [reset the API key for the region and resource group](/docs/openshift?topic=openshift-access-creds#api_key_most_cases).

    When the API key is reset, the previous API key that was used for the region and resource group is deleted. Before you reset the API key, check whether you have other services that use the existing API key, such as a [key management service (KMS) provider](/docs/openshift?topic=openshift-encryption#keyprotect).
    {: important}

4. After the cluster has access to the updated permissions in the API key, the creation of the {{site.data.keyword.cloudcerts_short}} instance is automatically triggered. Note that the {{site.data.keyword.cloudcerts_short}} instance might take up to an hour to become visible in the {{site.data.keyword.cloud_notm}} console.
5. Verify that your cluster is automatically assigned a {{site.data.keyword.cloudcerts_short}} instance.
    1. In the {{site.data.keyword.cloud_notm}} console, navigate to your [{{site.data.keyword.cloud_notm}} resource list](https://cloud.ibm.com/resources){: external}.
    2. Expand the **Services** row.
    3. Look for a {{site.data.keyword.cloudcerts_short}} instance that is named in the format `kube-crtmgr-<cluster_ID>`. To find your cluster's ID, run `ibmcloud oc cluster ls`.
    4. Click the instance's name. The **Your certificates** details page opens.
6. Verify that the TLS secret for your cluster's Ingress subdomain is created and listed in your cluster.
    ```sh
    ibmcloud oc ingress secret ls -c <cluster_name_or_ID>
    ```
    {: pre}




