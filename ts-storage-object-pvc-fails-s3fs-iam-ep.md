---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-10"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}


# Why do I see wrong s3fs or IAM API endpoints when I create a PVC?
{: #cos_api_endpoint_failure}
{: support}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


![Version 3.11 icon.](images/icon-version-311.png) This troubleshooting topic applies only to {{site.data.keyword.redhat_openshift_notm}} clusters that run version 3.11.
{: note}




When you create the PVC, the PVC remains in a pending state. After you run the `oc describe pvc <pvc_name>` command, you see one of the following error messages:
{: tsSymptoms}

```sh
Bad value for ibm.io/object-store-endpoint XXXX: scheme is missing. Must be of the form http://<hostname> or https://<hostname>
```
{: screen}

```sh
Bad value for ibm.io/iam-endpoint XXXX: scheme is missing. Must be of the form http://<hostname> or https://<hostname>
```
{: screen}


The s3fs API endpoint for the bucket that you want to use might have the wrong format, or your cluster is deployed in a location that is supported in {{site.data.keyword.openshiftlong_notm}} but is not yet supported by the {{site.data.keyword.cos_full_notm}} plug-in.
{: tsCauses}

Complete the following steps:
{: tsResolve}

1. Check the s3fs API endpoint that was automatically assigned by the `ibmc` Helm plug-in to your storage classes during the {{site.data.keyword.cos_full_notm}} plug-in installation. The endpoint is based on the location that your cluster is deployed to.  
    ```sh
    oc get sc ibmc-s3fs-standard-regional -o yaml | grep object-store-endpoint
    ```
    {: pre}

    If the command returns `ibm.io/object-store-endpoint: NA`, your cluster is deployed in a location that is supported in {{site.data.keyword.openshiftlong_notm}} but is not yet supported by the {{site.data.keyword.cos_full_notm}} plug-in. To add the location to the {{site.data.keyword.openshiftlong_notm}}, post a question in our public Slack or open an {{site.data.keyword.cloud_notm}} support case. For more information, see [Getting help and support](/docs/containers?topic=containers-getting_help_storage).

2. If you manually added the s3fs API endpoint with the `ibm.io/endpoint` annotation or the IAM API endpoint with the `ibm.io/iam-endpoint` annotation in your PVC, make sure that you added the endpoints in the format `https://<s3fs_api_endpoint>` and `https://<iam_api_endpoint>`. The annotation overwrites the API endpoints that are automatically set by the `ibmc` plug-in in the {{site.data.keyword.cos_full_notm}} storage classes.
    ```sh
    oc describe pvc <pvc_name>
    ```
    {: pre}






