---

copyright:
  years: 2014, 2022
lastupdated: "2022-04-07"

keywords: openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Storing data on {{site.data.keyword.cos_full_notm}}
{: #storage-cos-understand}

[{{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage) is persistent, highly available storage that you can mount to your apps. The plug-in is a Kubernetes Flex-Volume plug-in that connects Cloud {{site.data.keyword.cos_short}} buckets to pods in your cluster. Information stored with {{site.data.keyword.cos_full_notm}} is encrypted in transit and at rest, dispersed across many geographic locations, and accessed over HTTP by using a REST API.
{: shortdesc}

If you want to use {{site.data.keyword.cos_full_notm}} in a private cluster without public network access, you must set up your {{site.data.keyword.cos_full_notm}} service instance for HMAC authentication. If you don't want to use HMAC authentication, you must open up all outbound network traffic on port 443 for the plug-in to work properly in a private cluster.
{: important}

## Creating your object storage service instance
{: #create_cos_service}

Before you can start using object storage in your cluster, you must provision an {{site.data.keyword.cos_full_notm}} service instance in your account.
{: shortdesc}

The {{site.data.keyword.cos_full_notm}} plug-in works with any s3 API endpoint. For example, you might want to use a local Cloud Object Storage server, such as [Minio](https://min.io/){: external}, or connect to an s3 API endpoint that you set up at a different cloud provider instead of an {{site.data.keyword.cos_full_notm}} service instance.

Follow these steps to create an {{site.data.keyword.cos_full_notm}} service instance. If you plan to use a local Cloud Object Storage server or a different s3 API endpoint, see the provider documentation to set up your Cloud Object Storage instance.

1. Open the [{{site.data.keyword.cos_full_notm}} catalog page](https://cloud.ibm.com/objectstorage/create).
2. Enter a name for your service instance, such as `cos-backup`, and select the same resource group that your cluster is in. To view the resource group of your cluster, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.   
3. Review the [plan options](https://cloud.ibm.com/objectstorage/create#pricing){: external} for pricing information and select a plan.
4. Click **Create**. The service details page opens.
5. To continue to set up {{site.data.keyword.cos_short}} to use with your cluster, see [Creating service credentials](#service_credentials).

## Creating {{site.data.keyword.cos_full_notm}} service credentials
{: #service_credentials}

Before you begin, [Create your object storage service instance](#create_cos_service).

1. In the navigation on the service details page for your {{site.data.keyword.cos_short}} instance, click **Service Credentials**.
2. Click **New credential**. A dialog box opens.
3. Enter a name for your credentials.
4. From the **Role** drop-down list, select the [{{site.data.keyword.cos_short}} access role](/docs/cloud-object-storage?topic=cloud-object-storage-iam#iam-roles) for the actions that you want storage users in your cluster to have access to. You must select at least **Writer** service access role to use the `auto-create-bucket` dynamic provisioning feature. If you select `Reader`, then you can't use the credentials to create buckets in {{site.data.keyword.cos_full_notm}} and write data to it.
5. Optional: In **Add Inline Configuration Parameters (Optional)**, enter `{"HMAC":true}` to create more HMAC credentials for the {{site.data.keyword.cos_full_notm}} service. HMAC authentication adds an extra layer of security to the OAuth2 authentication by preventing the misuse of expired or randomly created OAuth2 tokens.
6. Click **Add**. Your new credentials are in the **Service Credentials** table.
7. Click **View credentials**.
8. Make note of the **apikey** to use OAuth2 tokens to authenticate with the {{site.data.keyword.cos_full_notm}} service. For HMAC authentication, in the **cos_hmac_keys** section, note the **access_key_id** and the **secret_access_key**.
9. [Store your service credentials in a Kubernetes secret inside the cluster](#create_cos_secret) to enable access to your {{site.data.keyword.cos_full_notm}} service instance.


## Creating a secret for the object storage service credentials
{: #create_cos_secret}

To access your {{site.data.keyword.cos_full_notm}} service instance to read and write data, you must securely store the service credentials in a Kubernetes secret. The {{site.data.keyword.cos_full_notm}} plug-in uses these credentials for every read or write operation to your bucket.
{: shortdesc}

Follow these steps to create a Kubernetes secret for the credentials of an {{site.data.keyword.cos_full_notm}} service instance. If you plan to use a local Cloud Object Storage server or a different s3 API endpoint, create a Kubernetes secret with the appropriate credentials.

Before you begin:
* [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
* Make sure that you have the **Manager** service access role for the cluster.

To create a secret for your {{site.data.keyword.cos_full_notm}} credentials:

1. Retrieve the **apikey**, or the **access_key_id** and the **secret_access_key** of your [{{site.data.keyword.cos_full_notm}} service credentials](#service_credentials). Note that the service credentials must be enough for the bucket operations that your app needs to perform. For example, if your app reads data from a bucket, the service credentials you see in your secret must have **Reader** permissions at minimum.

2. Get the **GUID** of your {{site.data.keyword.cos_full_notm}} service instance.
    ```sh
    ibmcloud resource service-instance <service_name> | grep GUID
    ```
    {: pre}

3. Create a Kubernetes secret to store your service credentials. When you create your secret, all values are automatically encoded to base64. In the following example the secret name is `cos-write-access`.

    Example `create secret` command that uses an API key.
    ```sh
    oc create secret generic cos-write-access --type=ibm/ibmc-s3fs --from-literal=api-key=<api_key> --from-literal=service-instance-id=<service_instance_guid>
    ```
    {: pre}

    Example `create secret` command that uses HMAC authentication.
    ```sh
    oc create secret generic cos-write-access --type=ibm/ibmc-s3fs --from-literal=access-key=<access_key_ID> --from-literal=secret-key=<secret_access_key>    
    ```
    {: pre}

    `api-key`
    :   Enter the API key that you retrieved from your {{site.data.keyword.cos_full_notm}} service credentials earlier. If you want to use HMAC authentication, specify the `access-key` and `secret-key` instead.
    
    `access-key`
    :   Enter the access key ID that you retrieved from your {{site.data.keyword.cos_full_notm}} service credentials earlier. If you want to use OAuth2 authentication, specify the `api-key` instead.
    
    `secret-key`
    :   Enter the secret access key that you retrieved from your {{site.data.keyword.cos_full_notm}} service credentials earlier. If you want to use OAuth2 authentication, specify the `api-key` instead.
    
    `service-instance-id`
    :   Enter the GUID of your {{site.data.keyword.cos_full_notm}} service instance that you retrieved earlier.

4. Get the secrets in your cluster and verify the output.
    ```sh
    oc get secret
    ```
    {: pre}

    Example output

    ```sh
    NAME                  TYPE                                  DATA   AGE
    cos-write-access      ibm/ibmc-s3fs                         2      7d19h
    default-au-icr-io     kubernetes.io/dockerconfigjson        1      55d
    default-de-icr-io     kubernetes.io/dockerconfigjson        1      55d
    ...
    ```
    {: screen}

5. [Install the {{site.data.keyword.cos_full_notm}} plug-in](/docs/containers?topic=containers-storage_cos_install), or if you already installed the plug-in, [decide on the configuration](/docs/openshift?topic=openshift-storage_cos_install#configure_cos) for your {{site.data.keyword.cos_full_notm}} bucket.

6. **Optional**: [Add your secret to the default storage classes](/docs/containers?topic=containers-storage_cos_install).





## Limitations
{: #cos_limitations}

* {{site.data.keyword.cos_full_notm}} is based on the `s3fs-fuse` file system. You can review a list of limitations in the [`s3fs-fuse` repository](https://github.com/s3fs-fuse/s3fs-fuse#limitations){: external}.
* To access a file in {{site.data.keyword.cos_full_notm}} with a non-root user, you must set the `runAsUser` and `fsGroup` values in your deployment to the same value.
