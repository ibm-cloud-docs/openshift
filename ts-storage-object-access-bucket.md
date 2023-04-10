---

copyright: 
  years: 2014, 2023
lastupdated: "2023-04-10"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}





# Why can't my PVC access an existing bucket?
{: #cos_access_bucket_fails}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}



When you create the PVC, the bucket in {{site.data.keyword.cos_full_notm}} can't be accessed. You see an error message similar to the following:
{: tsSymptoms}

```sh
Failed to provision volume with StorageClass "ibmc-s3fs-standard-regional": pvc:1b2345678b69175abc98y873e2:can't access bucket <bucket_name>: NotFound: Not Found
```
{: screen}


You might have used the wrong storage class to access your existing bucket, you tried to access a bucket that you did not create, or there has been a change in the endpoints that are used in the storage class. You can't access a bucket that you did not create.
{: tsCauses}


Verify your bucket details and storage class and recreate your PVC.
{: tsResolve}

1. From the [{{site.data.keyword.cloud_notm}} dashboard](https://cloud.ibm.com/){: external}, select your {{site.data.keyword.cos_full_notm}} service instance.
1. Select **Buckets**.
1. Review the **Class** and **Location** information for your existing bucket.
1. Choose the appropriate [storage class](/docs/openshift?topic=openshift-storage_cos_reference).
1. Make sure that you provide the correct name of your existing bucket.






