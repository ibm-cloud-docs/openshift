---

copyright: 
  years: 2022, 2024
lastupdated: "2024-01-03"


keywords: openshift, block storage for vpc, remove

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Removing {{site.data.keyword.block_storage_is_short}} from your cluster
{: #storage-block-vpc-remove}

When you set up persistent storage in your cluster, you have three main components: the Kubernetes persistent volume claim (PVC) that requests storage, the Kubernetes persistent volume (PV) that is mounted to a pod and described in the PVC, and the storage instance. Depending on how you created your storage, you might need to delete all three components separately.
{: shortdesc}

Removing persistent storage from your {{site.data.keyword.cloud_notm}} account varies depending on how you provisioned the storage and what components you already removed.
{: shortdesc}

Is my persistent storage deleted when I delete my cluster?
:   During cluster deletion, you have the option to remove your persistent storage. However, depending on how your storage was provisioned, the removal of your storage might not include all storage components.

If you dynamically provisioned storage with a storage class that sets `reclaimPolicy: Delete`, your PVC, PV, and the storage instance are automatically deleted when you delete the cluster. For storage that was statically provisioned, VPC Block Storage, or storage that you provisioned with a storage class that sets `reclaimPolicy: Retain`, the PVC and the PV are removed when you delete the cluster, but your storage instance and your data remain. You are still charged for your storage instance. Also, if you deleted your cluster in an unhealthy state, the storage might still exist even if you chose to remove it.

How do I delete the storage when I want to keep my cluster?
:   When you dynamically provisioned the storage with a storage class that sets `reclaimPolicy: Delete`, you can remove the PVC to start the deletion process of your persistent storage. Your PVC, PV, and storage instance are automatically removed.
:   For storage that was statically provisioned, VPC Block Storage, or storage that you provisioned with a storage class that sets `reclaimPolicy: Retain`, you must manually remove the PVC, PV, and the storage instance to avoid further charges.

How does the billing stop after I delete my storage?
:   Depending on what storage components you delete and when, the billing cycle might not stop immediately. If you delete the PVC and PV, but not the storage instance in your {{site.data.keyword.cloud_notm}} account, that instance still exists and you are charged for it.

If you delete the PVC, PV, and the storage instance, the billing cycle stops depending on the `billingType` that you chose when you provisioned your storage and how you chose to delete the storage.

- When you manually cancel the persistent storage instance from the {{site.data.keyword.cloud_notm}} console or the `ibmcloud sl` CLI, billing stops as follows:
    - **Hourly storage**: Billing stops immediately. After your storage is canceled, you might still see your storage instance in the console for up to 72 hours.
    - **Monthly storage**: You can choose between immediate cancellation or cancellation on the anniversary date. In both cases, you are billed until the end of the current billing cycle, and billing stops for the next billing cycle. After your storage is canceled, you might still see your storage instance in the console or the CLI for up to 72 hours.
        - **Immediate cancellation**: Choose this option to immediately remove your storage. Neither you nor your users can use the storage anymore or recover the data.
    - **Anniversary date**: Choose this option to cancel your storage on the next anniversary date. Your storage instances remain active until the next anniversary date and you can continue to use them until this date, such as to give your team time to make backups of your data.

- When you dynamically provisioned the storage with a storage class that sets `reclaimPolicy: Delete` and you choose to remove the PVC, the PV and the storage instance are immediately removed. For hourly billed storage, billing stops immediately. For monthly billed storage, you are still charged for the remainder of the month. After your storage is removed and billing stops, you might still see your storage instance in the console or the CLI for up to 72 hours.

What do I need to be aware of before I delete persistent storage?
:   When you clean up persistent storage, you delete all the data that is stored in it. If you need a copy of the data, make a backup for [file storage](/docs/openshift?topic=openshift-file_storage#file_backup_restore) or [block storage](/docs/openshift?topic=openshift-block_storage#block_backup_restore).

I deleted my storage instance. Why can I still see my instance?
:   After you remove persistent storage, it can take up to 72 hours for the removal to be fully processed and for the storage to disappear from your {{site.data.keyword.cloud_notm}} console or CLI.

I deleted my cluster. How do I remove the remaining storage volumes?
:   See the steps in [Why am I still seeing charges for block storage devices after deleting my cluster](/docs/openshift?topic=openshift-ts_storage_clean_volume).


## Cleaning up {{site.data.keyword.block_storage_is_short}}
{: #cleaning-up-block-vpc}


Remove the PVC, PV, and the storage instance from your {{site.data.keyword.cloud_notm}} account to avoid further charges for your persistent storage.
{: shortdesc}

Before you begin:
- Make sure that you backed up any data that you want to keep.
- [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

To clean up persistent data:

1. List the PVCs in your cluster and note the **`NAME`** of the PVC, the **`STORAGECLASS`**, and the name of the PV that is bound to the PVC and shown as **`VOLUME`**.

    ```sh
    oc get pvc
    ```
    {: pre}

    Example output
    
    ```sh
    NAME                  STATUS    VOLUME                                     CAPACITY   ACCESSMODES   STORAGECLASS            AGE
    claim1-block-bronze   Bound     pvc-06886b77-102b-11e8-968a-f6612bb731fb   20Gi       RWO           ibmc-block-bronze       78d
    claim-file-bronze     Bound     pvc-457a2b96-fafc-11e7-8ff9-b6c8f770356c   4Gi        RWX           ibmc-file-bronze-retain 105d
    claim-file-silve      Bound     pvc-1efef0ba-0c48-11e8-968a-f6612bb731fb   24Gi       RWX           ibmc-file-silver        83d
    ```
    {: screen}

1. Review the **`ReclaimPolicy`** and **`billingType`** for the storage class.

    ```sh
    oc describe storageclass <storageclass_name>
    ```
    {: pre}

    If the reclaim policy says `Delete`, your PV and the physical storage are removed when you remove the PVC. If the reclaim policy says `Retain`, or if you provisioned your storage without a storage class, then your PV and physical storage are not removed when you remove the PVC. You must remove the PVC, PV, and the physical storage separately.

    If your storage is charged monthly, you still get charged for the entire month, even if you remove the storage before the end of the billing cycle.
    {: important}

1. Remove any pods that mount the PVC. List the pods that mount the PVC. If no pod is returned in your CLI output, you don't have a pod that uses the PVC.

    ```sh
    oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"
    ```
    {: pre}

    Example output

    ```sh
    blockdepl-12345-prz7b:    claim1-block-bronze  
    ```
    {: screen}

1. Remove the pod that uses the PVC. If the pod is part of a deployment, remove the deployment.

    ```sh
    oc delete pod <pod_name>
    ```
    {: pre}

1. Verify that the pod is removed.

    ```sh
    oc get pods
    ```
    {: pre}

1. Remove the PVC.

    ```sh
    oc delete pvc <pvc_name>
    ```
    {: pre}

1. Review the status of your PV. Use the name of the PV that you retrieved earlier as **`VOLUME`**. When you remove the PVC, the PV that is bound to the PVC is released. Depending on how you provisioned your storage, your PV goes into a `Deleting` state if the PV is deleted automatically, or into a `Released` state, if you must manually delete the PV. **Note**: For PVs that are automatically deleted, the status might briefly say `Released` before it is deleted. Rerun the command after a few minutes to see whether the PV is removed.

    ```sh
    oc get pv <pv_name>
    ```
    {: pre}

1. If your PV is not deleted, manually remove the PV.

    ```sh
    oc delete pv <pv_name>
    ```
    {: pre}

1. Verify that the PV is removed.

    ```sh
    oc get pv
    ```
    {: pre}
    
1. List the physical storage instance that your PV pointed to and note the **`id`** of the physical storage instance.
    ```sh
    ibmcloud is volumes | grep <pv_name>
    ```
    {: pre}

1. Remove the physical storage instance.

    ```sh
    ibmcloud is volume-delete <vpc_block_id>
    ```
    {: pre}

1. Verify that the physical storage instance is removed.

    The deletion process might take up to 72 hours to complete.
    {: important}

    ```sh
    ibmcloud is volumes
    ```
    {: pre}


