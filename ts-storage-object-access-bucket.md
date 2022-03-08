---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-08"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}


# Why can't my PVC access an existing bucket?
{: #cos_access_bucket_fails}
{: support}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


![Version 3.11 icon.](images/icon-version-311.png) This troubleshooting topic applies only to {{site.data.keyword.redhat_openshift_notm}} clusters that run version 3.11.
{: note}




When you create the PVC, the bucket in {{site.data.keyword.cos_full_notm}} can't be accessed. You see an error message similar to the following:
{: tsSymptoms}

```sh
Failed to provision volume with StorageClass "ibmc-s3fs-standard-regional": pvc:1b2345678b69175abc98y873e2:can't access bucket <bucket_name>: NotFound: Not Found
```
{: screen}


You might have used the wrong storage class to access your existing bucket, or you tried to access a bucket that you did not create. You can't access a bucket that you did not create.
{: tsCauses}


Verify your bucket details and storage class and recreate your PVC.
{: tsResolve}

1. From the [{{site.data.keyword.cloud_notm}} dashboard](https://cloud.ibm.com/){: external}, select your {{site.data.keyword.cos_full_notm}} service instance.
2. Select **Buckets**.
3. Review the **Class** and **Location** information for your existing bucket.
4. Choose the appropriate [storage class](/docs/containers?topic=containers-storage_cos_reference).
5. Make sure that you provide the correct name of your existing bucket.






