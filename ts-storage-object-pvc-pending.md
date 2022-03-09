---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-09"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}


# Why does my PVC remain in a pending state?
{: #cos_pvc_pending}
{: support}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


![Version 3.11 icon.](images/icon-version-311.png) This troubleshooting topic applies only to {{site.data.keyword.redhat_openshift_notm}} clusters that run version 3.11.
{: note}




When you create a PVC and you run `oc get pvc <pvc_name>`, your PVC remains in a **Pending** state, even after waiting for some time.
{: tsSymptoms}


During the PVC creation and binding, many different tasks are executed by the {{site.data.keyword.cos_full_notm}} plug-in. Each task can fail and cause a different error message.
{: tsCauses}

Describe your PVC and review the common error messages.
{: tsResolve}

1. Find the root cause for why the PVC remains in a **Pending** state.
    ```sh
    oc describe pvc <pvc_name> -n <namespace>
    ```
    {: pre}

2. Review common error message descriptions and resolutions.


| Error message | Description | Steps to resolve |
| --- | --- | --- |
| `can't get credentials: can't get secret <secret_name>: secrets "<secret_name>" not found` | The Kubernetes secret that holds your {{site.data.keyword.cos_full_notm}} service credentials does not exist in the same namespace as the PVC or pod. | See [PVC or pod creation fails due to not finding the Kubernetes secret](/docs/containers?topic=containers-cos_secret_access_fails).|
| `can't get credentials: Wrong Secret Type.Provided secret of type XXXX.Expected type ibm/ibmc-s3fs` | The Kubernetes secret that you created for your {{site.data.keyword.cos_full_notm}} service instance does not include the `type: ibm/ibmc-s3fs`.| Edit the Kubernetes secret that holds your {{site.data.keyword.cos_full_notm}} credentials to add or change the `type` to `ibm/ibmc-s3fs`. |
|`Bad value for ibm.io/object-store-endpoint XXXX: scheme is missing. Must be of the form http://<hostname> or https://<hostname>` `Bad value for ibm.io/iam-endpoint XXXX: scheme is missing. Must be of the form http://<hostname> or https://<hostname>` | The s3fs API or IAM API endpoint has the wrong format, or the s3fs API endpoint could not be retrieved based on your cluster location. | See [PVC creation fails due to wrong s3fs API endpoint](/docs/containers?topic=containers-cos_api_endpoint_failure).|
|`object-path can't be set when auto-create is enabled`| You specified an existing subdirectory in your bucket that you want to mount to your PVC by using the `ibm.io/object-path` annotation. If you set a subdirectory, you must disable the bucket auto-create feature. | In your PVC, set `ibm.io/auto-create-bucket: "false"` and provide the name of the existing bucket in `ibm.io/bucket`. |
|`bucket auto-create must be enabled when bucket auto-delete is enabled` | In your PVC, you set `ibm.io/auto-delete-bucket: true` to automatically delete your data, the bucket, and the PV when you remove the PVC. This option requires `ibm.io/auto-create-bucket` to be set to `true`, and `ibm.io/bucket` to be set to `""` at the same time.| In your PVC, set `ibm.io/auto-create-bucket: true` and `ibm.io/bucket: ""` so that your bucket is automatically created with a name with the format `tmp-s3fs-xxxx`. |
|`bucket can't be set when auto-delete is enabled`| In your PVC, you set `ibm.io/auto-delete-bucket: true` to automatically delete your data, the bucket, and the PV when you remove the PVC. This option requires `ibm.io/auto-create-bucket` to be set to `true`, and `ibm.io/bucket` to be set to `""` at the same time. | In your PVC, set `ibm.io/auto-create-bucket: true` and `ibm.io/bucket: ""` so that your bucket is automatically created with a name with the format `tmp-s3fs-xxxx`. |
|`can't create bucket using API key without service-instance-id`| If you want to use IAM API keys to access your {{site.data.keyword.cos_full_notm}} service instance, you must store the API key and the ID of the {{site.data.keyword.cos_full_notm}} service instance in a Kubernetes secret. | See [Creating a secret for the object storage service credentials](/docs/openshift?topic=openshift-storage-cos-understand#create_cos_secret). |
|`object-path “<subdirectory_name>” not found inside bucket <bucket_name>`| You specified an existing subdirectory in your bucket that you want to mount to your PVC by using the `ibm.io/object-path` annotation. This subdirectory could not be found in the bucket that you specified. | Verify that the subdirectory that you specified in `ibm.io/object-path` exists in the bucket that you specified in `ibm.io/bucket`. |
|`BucketAlreadyExists: The requested bucket name is not available. The bucket namespace is shared by all users of the system. Please select a different name and try again.`| You set `ibm.io/auto-create-bucket: true` and specified a bucket name at the same time, or you specified a bucket name that already exists in {{site.data.keyword.cos_full_notm}}. Bucket names must be unique across all service instances and regions in {{site.data.keyword.cos_full_notm}}. | Make sure that you set `ibm.io/auto-create-bucket: false` and that you provide a bucket name that is unique in {{site.data.keyword.cos_full_notm}}. If you want to use the {{site.data.keyword.cos_full_notm}} plug-in to automatically create a bucket name for you, set `ibm.io/auto-create-bucket: true` and `ibm.io/bucket: ""`. Your bucket is created with a unique name in the format `tmp-s3fs-xxxx`. If you want to specify a bucket name for the auto-created bucket, set `ibm.io/auto-create-bucket: true` and `ibm.io/auto-delete-bucket: false` and `ibm.io/bucket: "<bucket_name>"`.|
|`can't access bucket <bucket_name>: NotFound: Not Found`| You tried to access a bucket that you did not create, or the storage class and s3fs API endpoint that you specified don't match the storage class and s3fs API endpoint that were used when the bucket was created. | See [can't access an existing bucket](/docs/containers?topic=containers-cos_access_bucket_fails). |
|`Put https://s3-api.dal-us-geo.objectstorage.service.networklayer.com/<bucket_name>: net/http: invalid header field value "AWS4-HMAC-SHA256 Credential=1234a12a123a123a1a123aa1a123a123\n\n/20190412/us-standard/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=12aa1abc123456aabb12aas12aa123456sb123456abc" for key Authorization`| The values in your Kubernetes secret are not correctly encoded to base64. | Review the values in your Kubernetes secret and encode every value to base64. You can also use the [`oc create secret`](/docs/openshift?topic=openshift-storage-cos-understand#create_cos_secret) command to create a new secret and let Kubernetes automatically encode your values to base64. |
| `can't access bucket <bucket_name>: Forbidden: Forbidden`| You specified `ibm.io/auto-create-bucket: false` and tried to access a bucket that you did not create or the secret access key or access key ID of your {{site.data.keyword.cos_full_notm}} HMAC credentials are incorrect. | You can't access a bucket that you did not create. Automatically create a bucket instead by setting `ibm.io/auto-create-bucket: true` and `ibm.io/bucket: ""`. If you are the owner of the bucket, see [PVC creation fails due to wrong credentials or access denied](/docs/containers?topic=containers-cred_failure) to check your credentials. |
|`can't create bucket <bucket_name>: AccessDenied: Access Denied` | You specified `ibm.io/auto-create-bucket: true` to automatically create a bucket in {{site.data.keyword.cos_full_notm}}, but the credentials that you provided in the Kubernetes secret are assigned the **Reader** IAM service access role. This role does not allow bucket creation in {{site.data.keyword.cos_full_notm}}. | See [PVC creation fails due to wrong credentials or access denied](/docs/containers?topic=containers-cred_failure). |
|`can't create bucket <bucket_name>: AccessForbidden: Access Forbidden`| You specified `ibm.io/auto-create-bucket: true` and provided a name of an existing bucket in `ibm.io/bucket`. In addition the credentials that you provided in the Kubernetes secret are assigned the **Reader** IAM service access role. This role does not allow bucket creation in {{site.data.keyword.cos_full_notm}}. | To use an existing bucket, set `ibm.io/auto-create-bucket: false` and provide the name of your existing bucket in `ibm.io/bucket`. To automatically create a bucket by using your existing Kubernetes secret, set `ibm.io/bucket: ""` and follow [PVC creation fails due to wrong credentials or access denied](/docs/containers?topic=containers-cred_failure) to verify the credentials in your Kubernetes secret.|
|`can't create bucket <bucket_name>: SignatureDoesNotMatch: The request signature we calculated does not match the signature you provided. Check your AWS Secret Access Key and signing method. For more information, see REST Authentication and SOAP Authentication for details`| The {{site.data.keyword.cos_full_notm}} secret access key of your HMAC credentials that you provided in your Kubernetes secret is not correct. | See [PVC creation fails due to wrong credentials or access denied](/docs/containers?topic=containers-cred_failure).|
|`can't create bucket <bucket_name>: InvalidAccessKeyId: The AWS Access Key ID you provided does not exist in our records`| The {{site.data.keyword.cos_full_notm}} access key ID or the secret access key of your HMAC credentials that you provided in your Kubernetes secret is not correct.| See [PVC creation fails due to wrong credentials or access denied](/docs/containers?topic=containers-cred_failure). |
|`can't create bucket <bucket_name>: CredentialsEndpointError: failed to load credentials` </br> </br> `can't access bucket <bucket_name>: CredentialsEndpointError: failed to load credentials`| The {{site.data.keyword.cos_full_notm}} API key of your IAM credentials and the GUID of your {{site.data.keyword.cos_full_notm}} service instance are not correct.| See [PVC creation fails due to wrong credentials or access denied](/docs/containers?topic=containers-cred_failure). |
| `TokenManagerRetrieveError: error retrieving the token` | This error occurs when you create a PVC with IAM credentials on a cluster that does not have public outbound access.| If your cluster does not have public outbound access, [create a {{site.data.keyword.cos_full_notm}} instance that uses HMAC credentials](/docs/openshift?topic=openshift-storage-cos-understand#create_cos_service).|
| `set-access-policy not supported for classic cluster` | This error occurs when you install the `ibm-object-storage-plugin` in a Classic cluster and set the `bucketAccessPolicy=true` flag. The `bucketAccessPolicy=true` flag is only used with VPC clusters.| [Install the plug-in](/docs/containers?topic=containers-storage_cos_install) and set the `bucketAccessPolicy=false` flag. |
{: caption="Block Storage error messages" caption-side="top"}
{: summary="The columns are read from left to right. The first column has the symptom or error message. The second column describes the message. The third column provides steps to resolve the error."}




