---

copyright:
  years: 2021, 2021
lastupdated: "2021-11-15"

keywords: openshift, storage

subcollection: openshift
content-type: troubleshoot

---


# Why is the status of my OpenShift Data Foundation storage cluster stuck at `Progressing`?
{: #ocs-ts-error-progressing}


When you run `oc describe noobaa` or `oc describe ocscluster <ocscluster_name>`, the status is stuck at `Progressing`.
{: tsSymptoms} 


To determine why your storage cluster status is stuck, describe your storage cluster resources and review the `Status`.
{: tsCauses}

1. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

2. Run the command to describe NooBaa. Note any error messages in the `Events` section of the output.
    ```sh 
    oc describe noobaa -n openshift-storage
    ```
    {: pre}

3. List the name of your ODF storage cluster.
    ```sh
    oc get ocscluster
    ```
    {: pre}

    **Example output**:
    ```sh
    NAME             AGE
    ocscluster-vpc   71d
    ```
    {: screen}

4. Describe your ODF storage cluster. Note any error messages in the `Events` section of the output.
    ```sh 
    oc describe ocscluster <ocscluster_name>
    ```
    {: pre}


Review the following common storage cluster error messages for steps to resolve the issue.
{: tsResolve}




## Error: Cloud credentials secret "ibm-cloud-cos-creds" is not ready yet
{: #ts-storage-ocs-cos-cred}

When you run `oc describe noobaa` or `oc describe ocscluster <ocscluster_name>`, the status is stuck at `Progressing` and you see the following error message:
```
Error: Cloud credentials secret "ibm-cloud-cos-creds" is not ready yet
```
{: screen}

You want to use {{site.data.keyword.cos_full_notm}} as a backingstore for your ODF cluster, but the credentials specified in the `ibm-cloud-cos-creds` secret are invalid. 

Verify your {{site.data.keyword.cos_short}} credentials and [update the Kubernetes secret for your {{site.data.keyword.cos_short}} service credentials](/docs/openshift?topic=openshift-object_storage#create_cos_secret).







