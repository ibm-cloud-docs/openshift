---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-16"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}


# File storage and block storage: Why does my PVC remain in a pending state?
{: #file_pvc_pending}
{: support}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


When you create a PVC and you run `oc get pvc <pvc_name>`, your PVC remains in a **Pending** state, even after waiting for some time.
{: tsSymptoms}


During the PVC creation and binding, many different tasks are executed by the file and block storage plug-in. Each task can fail and cause a different error message.
{: tsCauses}


Find the root cause by describing your PVC and reviewing the common error messages.
{: tsResolve}

1. Describe the PVC and state.
    ```sh
    oc describe pvc <pvc_name> -n <project>
    ```
    {: pre}

2. Review common error message descriptions and resolutions.

| Error message | Description | Steps to resolve |
| --- | --- | --- |
| `User doesn't have permissions to create or manage Storage` `Failed to find any valid softlayer credentials in configuration file` `Storage with the order ID %d could not be created after retrying for %d seconds.` `Unable to locate datacenter with name <datacenter_name>.` | The IAM API key or the IBM Cloud infrastructure API key that is stored in the `storage-secret-store` Kubernetes secret of your cluster does not have all the required permissions to provision persistent storage. | See [PVC creation fails because of missing permissions](/docs/containers?topic=containers-missing_permissions). |
| `Your order will exceed the maximum number of storage volumes allowed. Please contact Sales` | Every {{site.data.keyword.cloud_notm}} account is set up with a maximum number of file and block storage instances that can be created. By creating the PVC, you exceed the maximum number of storage instances. For more information about the maximum number of volumes that you can create and how to retrieve the number of volumes in your account, see the documentation for [file](/docs/FileStorage?topic=FileStorage-managinglimits) and [block](/docs/BlockStorage?topic=BlockStorage-managingstoragelimits) storage. | To create a PVC, choose from the following options. <ul><li>Remove any unused PVCs.</li><li>Ask the {{site.data.keyword.cloud_notm}} account owner to increase your storage quota by <a href="/docs/get-support?topic=get-support-using-avatar">opening a support case</a>.</li></ul> |
| `Unable to find the exact ItemPriceIds(type|size|iops) for the specified storage` `Failed to place storage order with the storage provider` | The storage size and IOPS that you specified in your PVC are not supported by the storage type that you chose and can't be used with the specified storage class. | Review [Deciding on the file storage configuration](/docs/openshift?topic=openshift-file_storage#file_predefined_storageclass) and [Deciding on the block storage configuration](/docs/openshift?topic=openshift-block_storage#block_predefined_storageclass) to find supported storage sizes and IOPS for the storage class that you want to use. Correct the size and IOPS, and re-create the PVC. |
| Failed to find the datacenter name in configuration file. | The data center that you specified in your PVC does not exist. | Run `ibmcloud oc locations` to list available data centers. Correct the data center in your PVC and re-create the PVC. |
| `Failed to place storage order with the storage provider` `Storage with the order ID 12345 could not be created after retrying for xx seconds.` `Failed to do subnet authorizations for the storage 12345.` `Storage 12345 has ongoing active transactions and could not be completed after retrying for xx seconds.` | The storage size, IOPS, and storage type might be incompatible with the storage class that you chose, or the {{site.data.keyword.cloud_notm}} infrastructure API endpoint is currently unavailable. | Review [Deciding on the file storage configuration](/docs/openshift?topic=openshift-file_storage#file_predefined_storageclass) and [Deciding on the block storage configuration](/docs/openshift?topic=openshift-block_storage#block_predefined_storageclass) to find supported storage sizes and IOPS for the storage class and storage type that you want to use. Then, delete the PVC and re-create the PVC. |
| Failed to find the storage with storage id 12345. | You want to create a PVC for an existing storage instance by using Kubernetes static provisioning, but the storage instance that you specified could not be found. | Follow the instructions to provision existing [file storage](/docs/openshift?topic=openshift-file_storage#existing_file) or [block storage](/docs/openshift?topic=openshift-block_storage#existing_block) in your cluster and make sure to retrieve the correct information for your existing storage instance. Then, delete the PVC and re-create the PVC. |
| Storage type not provided, expected storage type is `Endurance` or `Performance`. | You created a custom storage class and specified a storage type that is not supported. | Update your custom storage class to specify `Endurance` or `Performance` as your storage type. To find examples for custom storage classes, see the sample custom storage classes for [file storage](/docs/openshift?topic=openshift-file_storage#file_custom_storageclass) and [block storage](/docs/openshift?topic=openshift-block_storage#block_custom_storageclass). | 
{: caption="File Storage error messages" caption-side="top"}
{: summary="The columns are read from left to right. The first column has the error message. The second column describes the error message. The third column provides steps to resolve the error."}







