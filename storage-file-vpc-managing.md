---

copyright: 
  years: 2022, 2022
lastupdated: "2022-08-03"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Managing {{site.data.keyword.filestorage_vpc_full_notm}}
{: #storage-file-vpc-managing}

When you set up persistent storage in your cluster, you have three main components: the Kubernetes persistent volume claim (PVC) that requests storage, the Kubernetes persistent volume (PV) that is mounted to a pod and described in the PVC, and the file share. Depending on how you created your storage, you might need to delete all three components separately. 
{: shortdesc}


## Creating a custom storage class
{: #storage-file-vpc-custom-sc}

Create your own customized storage class with the preferred settings for your {{site.data.keyword.filestorage_vpc_short}} instance.
{: shortdesc}

To create your own storage class:

1. Review the [Storage class reference](/docs/containers?topic=containers-storage-vpc-sc-ref) to determine the `profile` that you want to use for your storage class. 

    If you want to use a pre-installed storage class as a template, you can get the details of a storage class by using the `oc get sc <storageclass> -o yaml` command.
    {: tip}

2. Create a customized storage class configuration file.

    ```yaml
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: ibmc-vpc-file-custom
    provisioner: vpc.file.csi.ibm.io
    mountOptions:
        - hard
        - nfsvers=4.0
        - sec=sys
    parameters:
      profile: "custom-iops"            # The VPC Storage profile used. https://cloud.ibm.com/docs/vpc?topic=vpc-block-storage-profiles&interface=ui#tiers-beta
      iops: "400"                       # Default IOPS. User can override from secrets
      billingType: "hourly"             # The default billing policy used. User can override this default
      encrypted: "false"                # By default, all PVC using this class will only be provider managed encrypted. The user can override this default
      encryptionKey: ""                 # If encrypted is true, then a user must specify the encryption key used associated KP instance
      resourceGroup: ""                 # Use resource group if specified here. else use the one mentioned in storage-secrete-store
      zone: ""                          # By default, the storage vpc driver will select a zone. The user can override this default
      tags: ""                          # A list of tags "a, b, c" that will be created when the volume is created. This can be overidden by user
      classVersion: "1"
      UID: ""                           # The initial user identifier for the file share.
      GID: ""                           # The initial group identifier for the file share.
    reclaimPolicy: "Delete"
    allowVolumeExpansion: true
    ```
    {: codeblock}

    `name`
    :   Enter a name for your storage class.
    
    `profile`
    :   Enter the profile that you selected in the previous step, or enter `custom` to use a custom IOPs value. To find supported storage sizes for a specific profile, see [Tiered IOPS profile](/docs/vpc?topic=vpc-block-storage-profiles). Any PVC that uses this storage class must specify a size value that is within this range.

    `encrypted`
    :   In the parameters, enter **true** to create a storage class that sets up encryption for your {{site.data.keyword.filestorage_vpc_short}} volume. If you set this option to **true**, you must provide the root key CRN of your {{site.data.keyword.keymanagementserviceshort}} service instance that you want to use in `parameterencryptionKey`. For more information about encrypting your data, see [Setting up encryption for your {{site.data.keyword.block_storage_is_short}}](#vpc-block-encryption).

    `encryptionKey`
    :   If you entered **true** for `parameters.encrypted`, then enter the root key CRN of your {{site.data.keyword.keymanagementserviceshort}} service instance that you want to use to encrypt your {{site.data.keyword.filestorage_vpc_short}} volume. For more information about encrypting your data, see [Setting up encryption for your {{site.data.keyword.block_storage_is_short}}](#vpc-block-encryption).

    `zone`
    :   In the parameters, enter the VPC zone where you want to create the {{site.data.keyword.block_storage_is_short}} instance. Make sure that you use a zone that your worker nodes are connected to. To list VPC zones that your worker nodes use, run `ibmcloud oc cluster get --cluster CLUSTER` and look at the **Worker Zones** field in your CLI output. If you don't specify a zone, one of the worker node zones is automatically selected for your {{site.data.keyword.block_storage_is_short}} instance.

    `region`
    :   The region of the worker node where you want to attach storage.

    `tags`
    :   In the parameters, enter a comma-separated list of tags to apply to your file share. Tags can help you group your file shares based on common characteristics, such as the app or the environment that it is used for. 

    `iops`
    :   If you entered `custom` for the `profile`, enter a value for the IOPs that you want your {{site.data.keyword.block_storage_is_short}} to use. Refer to the [{{site.data.keyword.block_storage_is_short}} custom IOPs profile](/docs/vpc?topic=vpc-block-storage-profiles#custom) table for a list of supported IOPs ranges by volume size.

    `reclaimPolicy`
    :   Enter the reclaim policy for your storage class. If you want to keep the PV, the physical storage device and your data when you remove the PVC, enter `Retain`. If you want to delete the PV, the physical storage device and your data when you remove the PVC, enter `Delete`.

    `allowVolumeExpansion`
    :   Enter the volume expansion policy for your storage class. If you want to allow volume expansion, enter `true`. If you don't want to allow volume expansion, enter `false`.

    `volumeBindingMode`
    :   Choose if you want to delay the creation of the {{site.data.keyword.block_storage_is_short}} instance until the first pod that uses this storage is ready to be scheduled. To delay the creation, enter `WaitForFirstConsumer`. To create the instance when you create the PVC, enter `Immediate`.


3. Create the customized storage class in your cluster.

    ```sh
    oc apply -f custom-storageclass.yaml
    ```
    {: pre}

4. Verify that your storage class is available in the cluster.

    ```sh
    oc get storageclasses
    ```
    {: pre}

    Example output
    
    ```sh
    NAME                                          PROVISIONER
    ibmc-vpc-file-10iops-tier                     vpc.file.csi.ibm.io
    ibmc-vpc-file-3iops-tier                      vpc.file.csi.ibm.io
    ibmc-vpc-file-5iops-tier                      vpc.file.csi.ibm.io
    ibmc-vpc-file-retain-10iops-tier              vpc.file.csi.ibm.io
    ibmc-vpc-file-retain-3iops-tier               vpc.file.csi.ibm.io
    ibmc-vpc-file-retain-5iops-tier               vpc.file.csi.ibm.io
    ibmc-vpc-file-custom                         vpc.file.csi.ibm.io
    ```
    {: screen}


## Updating the {{site.data.keyword.filestorage_vpc_short}} add-on
{: #storage-file-vpc-update}

1. Disable the add-on.

  ```sh
  ibmcloud oc cluster addon disable vpc-file-csi-driver --version VERSION 
  ```
  {: pre}

1. Enable the newer version of the add-on.The add-on might take a few minutes to become ready.
  ```sh
  ibmcloud oc cluster addon enable vpc-file-csi-driver --version VERSION
  ```
  {: pre}

## Understanding your storage removal options
{: #vpc_storage_delete_options_file}

Removing persistent storage from your {{site.data.keyword.cloud_notm}} account varies depending on how you provisioned the storage and what components you already removed.
{: shortdesc}

**Is my persistent storage deleted when I delete my cluster?**

During cluster deletion, you have the option to remove your persistent storage. However, depending on how your storage was provisioned, the removal of your storage might not include all storage components.

If you [dynamically provisioned](/docs/openshift?topic=openshift-kube_concepts#dynamic_provisioning) storage with a storage class that sets `reclaimPolicy: Delete`, your PVC, PV, and the storage instance are automatically deleted when you delete the cluster. For storage that was [statically provisioned](/docs/openshift?topic=openshift-kube_concepts#static_provisioning), or storage that you provisioned with a storage class that sets `reclaimPolicy: Retain`, the PVC and the PV are removed when you delete the cluster, but your storage instance and your data remain. You are still charged for your storage instance. Also, if you deleted your cluster in an unhealthy state, the storage might still exist even if you chose to remove it.

**How do I delete the storage when I want to keep my cluster?**

When you dynamically provisioned the storage with a storage class that sets `reclaimPolicy: Delete`, you can remove the PVC to start the deletion process of your persistent storage. Your PVC, PV, and storage instance are automatically removed.

For storage that was [statically provisioned](/docs/openshift?topic=openshift-kube_concepts#static_provisioning), or storage that you provisioned with a storage class that sets `reclaimPolicy: Retain`, you must manually remove the PVC, PV, and the storage instance to avoid further charges.

**How does the billing stop after I delete my storage?**

Depending on what storage components you delete and when, the billing cycle might not stop immediately. If you delete the PVC and PV, but not the storage instance in your {{site.data.keyword.cloud_notm}} account, that instance still exists and you are charged for it.

If you delete the PVC, PV, and the storage instance, the billing cycle stops depending on the `billingType` that you chose when you provisioned your storage and how you chose to delete the storage.

- When you manually cancel the persistent storage instance from the {{site.data.keyword.cloud_notm}} console or the `ibmcloud sl` CLI, billing stops as follows:
    - **Hourly storage**: Billing stops immediately. After your storage is canceled, you might still see your storage instance in the console for up to 72 hours.
    - **Monthly storage**: You can choose between immediate cancellation or cancellation on the anniversary date. In both cases, you are billed until the end of the current billing cycle, and billing stops for the next billing cycle. After your storage is canceled, you might still see your storage instance in the console or the CLI for up to 72 hours.
        - **Immediate cancellation**: Choose this option to immediately remove your storage. Neither you nor your users can use the storage anymore or recover the data.
    - **Anniversary date**: Choose this option to cancel your storage on the next anniversary date. Your storage instances remain active until the next anniversary date and you can continue to use them until this date, such as to give your team time to make backups of your data.

- When you dynamically provisioned the storage with a storage class that sets `reclaimPolicy: Delete` and you choose to remove the PVC, the PV and the storage instance are immediately removed. For hourly billed storage, billing stops immediately. For monthly billed storage, you are still charged for the remainder of the month. After your storage is removed and billing stops, you might still see your storage instance in the console or the CLI for up to 72 hours.

**What do I need to be aware of before I delete persistent storage?**

When you clean up persistent storage, you delete all the data that is stored in it. If you need a copy of the data, make a backup for [file storage](/docs/openshift?topic=openshift-file_storage#file_backup_restore) or [block storage](/docs/openshift?topic=openshift-block_storage#block_backup_restore).

**I deleted my storage instance. Why can I still see my instance?**

After you remove persistent storage, it can take up to 72 hours for the removal to be fully processed and for the storage to disappear from your {{site.data.keyword.cloud_notm}} console or CLI.

**I deleted my cluster. How do I remove the remaining storage volumes?**

See the steps in [Why am I still seeing charges for block storage devices after deleting my cluster](/docs/containers?topic=containers-ts_storage_clean_volume).

## Cleaning up persistent storage
{: #vpc-storage-remove-file}

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
    

