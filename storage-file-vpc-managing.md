---

copyright: 
  years: 2023, 2025
lastupdated: "2025-12-03"


keywords: kubernetes, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}




# Managing {{site.data.keyword.filestorage_vpc_full_notm}}
{: #storage-file-vpc-managing}

When you set up persistent storage in your cluster, you have three main components: the Kubernetes persistent volume claim (PVC) that requests storage, the Kubernetes persistent volume (PV) that is mounted to a pod and described in the PVC, and the file share. Depending on how you created your storage, you might need to delete all three components separately. 
{: shortdesc}




The following limitations apply to the add-on.

- It is recommended that your cluster and VPC are part of same resource group. If your cluster and VPC are in separate resource groups, then before you can provision file shares, you must create your own storage class and provide your VPC resource group ID. For more information, see [Creating your own storage class](/docs/openshift?topic=openshift-storage-file-vpc-apps#storage-file-vpc-custom-sc).
- New security group rules were introduced in cluster versions 4.11 and later. These rule changes mean that you must sync your security groups before you can use {{site.data.keyword.filestorage_vpc_short}}. For more information, see [Adding {{site.data.keyword.filestorage_vpc_short}} to apps](/docs/openshift?topic=openshift-storage-file-vpc-apps).
- New storage classes were added with version 2.0 of the add-on. You can no longer provision new file shares that use the older storage classes. Existing volumes that use the older storage classes continue to function, however you cannot expand the volumes that were created using the older classes. For more information, see the [Migrating to a new storage class](/docs/openshift?topic=openshift-storage-file-vpc-apps#storage-file-expansion-migration).


## Updating the {{site.data.keyword.filestorage_vpc_short}} cluster add-on
{: #storage-file-vpc-update}

[Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Get your cluster ID.
    ```shell
    ibmcloud oc cluster ls
    ```
    {: pre}

1. Review the available add-on versions.
    ```shell
    ibmcloud oc cluster addon versions
    ```
    {: pre}


1. Disable the add-on.
    ```sh
    ibmcloud oc cluster addon disable vpc-file-csi-driver --cluster CLUSTER
    ```
    {: pre}


1. Enable the newer version of the add-on.
    ```sh
    ibmcloud oc cluster addon enable vpc-file-csi-driver --cluster CLUSTER --version VERSION
    ```
    {: pre}

1. Verify the add-on is enabled by running the following commands.

    ```sh
    oc get deploy -n kube-system | grep file
    ```
    {: pre}

    ```sh
    ibm-vpc-file-csi-controller   2/2     2            2           13m
    ```
    {: screen}
    
    ```sh
    oc get ds -n kube-system | grep file
    ```
    {: pre}

    ```sh
    ibm-vpc-file-csi-node    2         2         2       2            2           <none>          14m
    ```
    {: screen}

    ```sh
    oc get pods -n kube-system  | grep file
    ```
    {: pre}

    ```sh
    ibm-vpc-file-csi-controller-7899db784-kc29g   5/5     Running   0             14m
    ibm-vpc-file-csi-controller-7899db784-mp5jt   5/5     Running   0             14m
    ibm-vpc-file-csi-node-bfqdz                   4/4     Running   0             14m
    ibm-vpc-file-csi-node-n7jbx                   4/4     Running   0             14m
    ```
    {: screen}

## Setting resource and request limits in the configmap
{: #edit-vpc-file-configmap}

1. Run the following command to edit the configmap.

    ```sh
    oc edit cm addon-vpc-file-csi-driver-configmap -n kube-system
    ```
    {: pre}


    Example output.
    ```yaml
    apiVersion: v1
    data:
      CSIBlockDriverCPULimit: 300m
      CSIBlockDriverCPURequest: 75m
      CSIBlockDriverMemoryLimit: 600Mi
      CSIBlockDriverMemoryRequest: 150Mi
      CSIDriverRegistrarCPULimit: 40m
      CSIDriverRegistrarCPURequest: 10m
      CSIDriverRegistrarMemoryLimit: 80Mi
      CSIDriverRegistrarMemoryRequest: 20Mi
      CSILivenessProbeCPULimit: 20m
      CSILivenessProbeCPURequest: 5m
      CSILivenessProbeMemoryLimit: 40Mi
      CSILivenessProbeMemoryRequest: 10Mi
      CSINodeDriverCPULimit: 120m
      CSINodeDriverCPURequest: 30m
      CSINodeDriverMemoryLimit: 300Mi
      CSINodeDriverMemoryRequest: 75Mi
      CSIProvisionerCPULimit: 80m
      CSIProvisionerCPURequest: 20m
      CSIProvisionerMemoryLimit: 160Mi
      CSIProvisionerMemoryRequest: 40Mi
      CSIResizerCPULimit: 80m
      CSIResizerCPURequest: 20m
      CSIResizerMemoryLimit: 160Mi
      CSIResizerMemoryRequest: 40Mi
      EIT_ENABLED_WORKER_POOLS: ""
      ENABLE_EIT: "false"
      SET_DEFAULT_STORAGE_CLASS: ""
      SecretSidecarCPULimit: 60m
      SecretSidecarCPURequest: 15m
      SecretSidecarMemoryLimit: 80Mi
      SecretSidecarMemoryRequest: 20Mi
    kind: ConfigMap
    metadata:
      creationTimestamp: "2025-06-19T11:23:13Z"
      labels:
        app.kubernetes.io/name: ibm-vpc-file-csi-driver
      name: addon-vpc-file-csi-driver-configmap
    ```
    {: codeblock}

1. Edit the parameters as needed then save file.





## Disabling the add-on
{: #storage-file-vpc-disable}

Disabling the `vpc-file-csi-driver` removes the encryption in-transit packages from your worker nodes.
{: note}

1. Run the following command to disable the add-on.

    ```sh
    ibmcloud oc cluster addon disable --addon vpc-file-csi-driver --cluster CLUSTER
    ```
    {: pre}

1. Verify the pods have been removed.

    ```sh
    oc get pods -n kube-system  | grep file
    ```
    {: pre}




## Understanding your storage removal options
{: #vpc-storage-delete-options-file}

Tagging was not supported in version 1.2. This impacts the removal of file shares when a cluster is deleted with the `--force-delete-storage` option. Make sure you clean up all PVCs that were created with version 1.2 of the add-on before deleting your cluster.
{: note}

Removing persistent storage from your {{site.data.keyword.cloud_notm}} account varies depending on how you provisioned the storage and what components you already removed.
{: shortdesc}

Is my persistent storage deleted when I delete my cluster?
:   During cluster deletion, you have the option to remove your persistent storage. However, depending on how your storage was provisioned, the removal of your storage might not include all storage components. If you dynamically provisioned storage with a storage class that sets `reclaimPolicy: Delete`, your PVC, PV, and the storage instance are automatically deleted when you delete the cluster. For storage that was statically provisioned or storage that you provisioned with a storage class that sets `reclaimPolicy: Retain`, the PVC and the PV are removed when you delete the cluster, but your storage instance and your data remain. You are still charged for your storage instance. Also, if you deleted your cluster in an unhealthy state, the storage might still exist even if you chose to remove it.

How do I delete the storage when I want to keep my cluster?
:   When you dynamically provisioned the storage with a storage class that sets `reclaimPolicy: Delete`, you can remove the PVC to start the deletion process of your persistent storage. Your PVC, PV, and storage instance are automatically removed. For storage that was statically provisioned or storage that you provisioned with a storage class that sets `reclaimPolicy: Retain`, you must manually remove the PVC, PV, and the storage instance to avoid further charges.

How does the billing stop after I delete my storage?
:   Depending on what storage components you delete and when, the billing cycle might not stop immediately. If you delete the PVC and PV, but not the storage instance in your {{site.data.keyword.cloud_notm}} account, that instance still exists and you are charged for it.

If you delete the PVC, PV, and the storage instance, the billing cycle stops depending on the `billingType` that you chose when you provisioned your storage and how you chose to delete the storage.

- When you manually cancel the persistent storage instance from the {{site.data.keyword.cloud_notm}} console or the CLI, billing stops as follows:
    - **Hourly storage**: Billing stops immediately. After your storage is canceled, you might still see your storage instance in the console for up to 72 hours.
    - **Monthly storage**: You can choose between immediate cancellation or cancellation on the anniversary date. In both cases, you are billed until the end of the current billing cycle, and billing stops for the next billing cycle. After your storage is canceled, you might still see your storage instance in the console or the CLI for up to 72 hours.
    - **Immediate cancellation**: Choose this option to immediately remove your storage. Neither you nor your users can use the storage anymore or recover the data.
    - **Anniversary date**: Choose this option to cancel your storage on the next anniversary date. Your storage instances remain active until the next anniversary date and you can continue to use them until this date, such as to give your team time to make backups of your data.

- When you dynamically provisioned the storage with a storage class that sets `reclaimPolicy: Delete` and you choose to remove the PVC, the PV and the storage instance are immediately removed. For hourly billed storage, billing stops immediately. For monthly billed storage, you are still charged for the remainder of the month. After your storage is removed and billing stops, you might still see your storage instance in the console or the CLI for up to 72 hours.

What do I need to be aware of before I delete persistent storage?
:   When you clean up persistent storage, you delete all the data that is stored in it. If you need a copy of the data, make a backup.

I deleted my storage instance. Why can I still see my instance?
:   After you remove persistent storage, it can take up to 72 hours for the removal to be fully processed and for the storage to disappear from your {{site.data.keyword.cloud_notm}} console or CLI.



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
    claim1   Bound     pvc-06886b77-102b-11e8-968a-f6612bb731fb   20Gi       RWO           class       78d
    claim2     Bound     pvc-457a2b96-fafc-11e7-8ff9-b6c8f770356c   4Gi        RWX           class 105d
    claim3      Bound     pvc-1efef0ba-0c48-11e8-968a-f6612bb731fb   24Gi       RWX           class        83d
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
    depl-12345-prz7b:    claim1
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
    

1. List your shares.

    ```sh
    ibmcloud is shares
    ```
    {: pre}


1. List each file share and find the associated cluster ID.
    ```sh
    ibmcloud is share SHARE | grep CLUSTER-ID
    ```
    {: pre}


1. Delete the shares.
    ```sh
    ibmcloud is share-delete (SHARE1 SHARE2 ...)
    ```
    {: pre}
