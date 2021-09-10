---

copyright:
  years: 2014, 2021
lastupdated: "2021-09-10"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}  

# Why do I get an error about a cloud object storage bucket when I create a cluster?
{: #ts_cos_bucket_cluster_create}

**Infrastructure provider**: <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC 


When you create a cluster, you see an error message similar to the following.
{: tsSymptoms}

```
Could not store the cloud object storage bucket and IAM service key.
```
{: screen}

```
Could not find the specified cloud object storage instance.
```
{: screen}

```
Could not create an IAM service key to access the cloud object storage bucket '{{.Name}}'.
```
{: screen}

```
Could not create a bucket in your cloud object storage instance.
```
{: screen}

```
Verify your user permissions and the API key permissions to Cloud Object Storage, or use a different instance that you have permissions to, and try again. For more information, see 'http://ibm.biz/roks_cos_ts'.
```
{: screen}


When you create a {{site.data.keyword.openshiftlong_notm}} version 4 cluster on VPC generation 2 compute infrastructure, a bucket is automatically created in a standard {{site.data.keyword.cos_full_notm}} instance that you select in your account.
{: tsCauses}

However, the bucket might not create for several reasons such as:
* {{site.data.keyword.cos_full_notm}} is temporarily unavailable.
* No standard {{site.data.keyword.cos_full_notm}} instance exists in your account, or the person whose API key is set for the region and resouce group does not have permissions to view the instance.
* The person who created your cluster did not have the **Administrator** platform access role to {{site.data.keyword.cos_full_notm}} in IAM.
* The service failed to set up service key access to the object storage instance, such as if the API key lacks permissions or {{site.data.keyword.cloud_notm}} IAM is unavailable.
* Other conflicts, such as naming conflicts that exhaust the preset number of retries or saving the bucket and service key data in the backend service.


Manually set up your cluster to back up the internal registry to an {{site.data.keyword.cos_full_notm}} bucket.
{: tsResolve}

1. Make sure that the API key for the region and resource group is set and that you have the [required permissions to create a cluster](/docs/openshift?topic=openshift-access_reference#cluster_create_permissions).
2. If corporate network policies prevent access from your local system to public endpoints via proxies or firewalls, [allow access to the {{site.data.keyword.cos_full_notm}} subdomain](/docs/openshift?topic=openshift-vpc-firewall#openshift-registry).
3. Identify the {{site.data.keyword.cos_full_notm}} instance to use. You can create an instance or use an existing one.
    * [Create a standard {{site.data.keyword.cos_full_notm}} service, at least one bucket, and HMAC service credentials](/docs/openshift?topic=openshift-object_storage#create_cos_service).
    * To use an existing instance, make sure that you and the API key that is set for the region have permissions to the instance.
4. Create a cluster with your {{site.data.keyword.cos_full_notm}} instance ID. For more information, see the [CLI reference](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-vpc-gen2).
    ```
    ibmcloud oc cluster create vpc-gen2 --name NAME --zone ZONE --vpc-id VPC_ID --subnet-id VPC_SUBNET_ID --flavor WORKER_FLAVOR --cos-instance COS_CRN --workers 3
    ```
    {: pre}

5. Verify that the internal registry images are backed up to {{site.data.keyword.cos_full_notm}}.
    1. [Build an image for your app](/docs/openshift?topic=openshift-images) and [push it to {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-images#push-images).
    2. [Import the image into your internal {{site.data.keyword.openshiftshort}} registry](/docs/openshift?topic=openshift-registry#imagestream_registry).
    3. [Deploy an app](/docs/openshift?topic=openshift-images#pod_imagePullSecret) that references your image.
    4. From the [{{site.data.keyword.cloud_notm}} console resource list](https://cloud.ibm.com/resources), select your **Cloud Object Storage** instance.
    5. From the menu, click **Buckets**, then click the bucket that you used for your {{site.data.keyword.openshiftlong_notm}} cluster.
    6. Review the recent **Objects** to see your backed up images from the internal registry of your {{site.data.keyword.openshiftlong_notm}} cluster.


