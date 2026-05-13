---

copyright: 
  years: 2014, 2026
lastupdated: "2026-05-13"


keywords: openshift, storage

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}





# {{site.data.keyword.block_storage_is_short}} PVC creation fails after API key reset
{: #vpc-block-api-key-reset-ts}
{: support}

[Virtual Private Cloud]{: tag-vpc}

After you reset your API key, {{site.data.keyword.block_storage_is_short}} PVC creation fails with an IAM permission error.
{: tsSymptoms}

Resetting your API key means the credentials that the {{site.data.keyword.block_storage_is_short}} cluster add-on uses to provision volumes are no longer valid. After resetting your API key, you must reset the {{site.data.keyword.block_storage_is_short}} controller to use the latest API key for volume provisioning.
{: tsCauses}

## Resolving the issue
{: #vpc-block-api-key-resolve}

After resetting your API key, you must re-create the {{site.data.keyword.block_storage_is_short}} controller pod.
{: tsResolve}

1. Get the {{site.data.keyword.block_storage_is_short}} controller pod name.

    ```sh
    oc get pods -n kube-system | grep ibm-vpc-block-csi-controller  
    ```
    {: pre}

1. Delete the {{site.data.keyword.block_storage_is_short}} controller pod.

    ```sh
    oc delete pod -n kube-system POD_NAME
    ```
    {: pre}
