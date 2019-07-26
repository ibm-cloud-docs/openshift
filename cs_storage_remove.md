---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-26"

keywords: kubernetes, iks

subcollection: containers

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}
 
# Removing persistent storage from a cluster
{: #cleanup}

When you set up persistent storage in your cluster, you have three main components: the Kubernetes persistent volume claim (PVC) that requests storage, the Kubernetes persistent volume (PV) that is mounted to a pod and described in the PVC, and the IBM Cloud infrastructure instance, such as NFS file or block storage. Depending on how you created your storage, you might need to delete all three separately.
{:shortdesc}

## Cleaning up persistent storage
{: #storage_remove}

Understanding your delete options:

**I deleted my cluster. Do I have to delete anything else to remove persistent storage?**</br>
It depends. When you delete a cluster, the PVC and PV are deleted. However, you choose whether to remove the associated storage instance in IBM Cloud infrastructure. If you chose not to remove it, then the storage instance still exists. Also, if you deleted your cluster in an unhealthy state, the storage might still exist even if you chose to remove it. Follow the instructions, particularly the step to [delete your storage instance](#sl_delete_storage) in IBM Cloud infrastructure.

**Can I delete the PVC to remove all my storage?**</br>
Sometimes. If you [create the persistent storage dynamically](/docs/containers?topic=containers-kube_concepts#dynamic_provisioning) and select a storage class without `retain` in its name, then when you delete the PVC, the PV and the IBM Cloud infrastructure storage instance are also deleted.

In all other cases, follow the instructions to check the status of your PVC, PV, and the physical storage device and delete them separately if necessary.

**Am I still charged for storage after I delete it?**</br>
It depends on what you delete and the billing type. If you delete the PVC and PV, but not the instance in your IBM Cloud infrastructure account, that instance still exists and you are charged for it. You must delete everything to avoid charges. Further, when you specify the `billingType` in the PVC, you can choose `hourly` or `monthly`. If you chose `monthly`, your instance is billed monthly. When you delete the instance, you are charged for the remainder of the month.

When you manually cancel the persistent storage instance from the IBM Cloud infrastructure console or the `ibmcloud sl` CLI, billing is stopped as follows: 
- **Hourly storage**: Billing is stopped immediately. After your storage is canceled, you might still see your storage instance in the console for up to 72 hours.  
- **Monthly storage**: You can choose between **immediate cancellation** or **cancellation on the anniversary date**. If you choose immediate cancellation, your storage is immediately removed and you cannot use your storage anymore. If you choose to cancel your storage on the next anniversary date, your storage instances remain active until the next anniversary date and you can continue to use them until this date. In both cases, billing is stopped for the next billing cycle, but you are still billed until the end of the current billing cycle. After your storage is canceled, you might still see your storage instance in the console or the CLI for up to 72 hours.  

If you remove persistent storage with a `Delete` reclaim policy that you dynamically provisioned by deleting the PVC, the storage is removed immediately independent if you chose an hourly or monthly billing type. After your storage is removed, you might still see your storage instance in the console or the CLI for up to 72 hours. Persistent storage that uses a `Retain` reclaim policy is not removed and you are still charged for using it. 

<p class="important">When you clean up persistent storage, you delete all the data that is stored in it. If you need a copy of the data, make a backup for [file storage](/docs/containers?topic=containers-file_storage#file_backup_restore) or [block storage](/docs/containers?topic=containers-block_storage#block_backup_restore).  </p>

**I deleted my storage. Why can I still see my instances?** </br>
After you remove persistent storage, it can take up to 72 hours for the removal to be fully processed and for the storage to disappear from your IBM Cloud infrastructure console or CLI. 

Before you begin: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

To clean up persistent data:

1.  List the PVCs in your cluster and note the **`NAME`** of the PVC, the **`STORAGECLASS`**, and the name of the PV that is bound to the PVC and shown as **`VOLUME`**.
    ```
    kubectl get pvc
    ```
    {: pre}

    Example output:
    ```
    NAME                  STATUS    VOLUME                                     CAPACITY   ACCESSMODES   STORAGECLASS            AGE
    claim1-block-bronze   Bound     pvc-06886b77-102b-11e8-968a-f6612bb731fb   20Gi       RWO           ibmc-block-bronze       78d
    claim-file-bronze     Bound     pvc-457a2b96-fafc-11e7-8ff9-b6c8f770356c   4Gi        RWX           ibmc-file-bronze-retain 105d
    claim-file-silve      Bound     pvc-1efef0ba-0c48-11e8-968a-f6612bb731fb   24Gi       RWX           ibmc-file-silver        83d
    ```
    {: screen}

2. Review the **`ReclaimPolicy`** and **`billingType`** for the storage class.
   ```
   kubectl describe storageclass <storageclass_name>
   ```
   {: pre}

   If the reclaim policy says `Delete`, your PV and the physical storage are removed when you remove the PVC. If the reclaim policy says `Retain`, or if you provisioned your storage without a storage class, then your PV and physical storage are not removed when you remove the PVC. You must remove the PVC, PV, and the physical storage separately.

   If your storage is charged monthly, you still get charged for the entire month, even if you remove the storage before the end of the billing cycle.
   {: important}

3. Remove any pods that mount the PVC.
   1. List the pods that mount the PVC.
      ```
      kubectl get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"
      ```
      {: pre}

      Example output:
      ```
      blockdepl-12345-prz7b:	claim1-block-bronze  
      ```
      {: screen}

      If no pod is returned in your CLI output, you do not have a pod that uses the PVC.

   2. Remove the pod that uses the PVC. If the pod is part of a deployment, remove the deployment.
      ```
      kubectl delete pod <pod_name>
      ```
      {: pre}

   3. Verify that the pod is removed.
      ```
      kubectl get pods
      ```
      {: pre}

4. Remove the PVC.
   ```
   kubectl delete pvc <pvc_name>
   ```
   {: pre}

5. Review the status of your PV. Use the name of the PV that you retrieved earlier as **`VOLUME`**.
   ```
   kubectl get pv <pv_name>
   ```
   {: pre}

   When you remove the PVC, the PV that is bound to the PVC is released. Depending on how you provisioned your storage, your PV goes into a `Deleting` state if the PV is deleted automatically, or into a `Released` state, if you must manually delete the PV. **Note**: For PVs that are automatically deleted, the status might briefly say `Released` before it is deleted. Rerun the command after a few minutes to see whether the PV is removed.

6. If your PV is not deleted, manually remove the PV.
   ```
   kubectl delete pv <pv_name>
   ```
   {: pre}

7. Verify that the PV is removed.
   ```
   kubectl get pv
   ```
   {: pre}

8. {: #sl_delete_storage}List the physical storage instance that your PV pointed to and note the **`id`** of the physical storage instance.

   **File storage:**
   ```
   ibmcloud sl file volume-list --columns id  --columns notes | grep <pv_name>
   ```
   {: pre}
   **Block storage:**
   ```
   ibmcloud sl block volume-list --columns id --columns notes | grep <pv_name>
   ```
   {: pre}

   If you removed your cluster and cannot retrieve the name of the PV, replace `grep <pv_name>` with `grep <cluster_id>` to list all storage devices that are associated with your cluster.
   {: tip}

   Example output:
   ```
   id         notes   
   12345678   {"plugin":"ibm-file-plugin-5b55b7b77b-55bb7","region":"us-south","cluster":"aa1a11a1a11b2b2bb22b22222c3c3333","type":"Endurance","ns":"default","pvc":"mypvc","pv":"pvc-d979977d-d79d-77d9-9d7d-d7d97ddd99d7","storageclass":"ibmc-file-gold"}
   ```
   {: screen}

   Understanding the **Notes** field information:
   *  **`"plugin":"ibm-file-plugin-5b55b7b77b-55bb7"`**: The storage plug-in that the cluster uses.
   *  **`"region":"us-south"`**: The region that your cluster is in.
   *  **`"cluster":"aa1a11a1a11b2b2bb22b22222c3c3333"`**: The cluster ID that is associated with the storage instance.
   *  **`"type":"Endurance"`**: The type of file or block storage, either `Endurance` or `Performance`.
   *  **`"ns":"default"`**: The namespace that the storage instance is deployed to.
   *  **`"pvc":"mypvc"`**: The name of the PVC that is associated with the storage instance.
   *  **`"pv":"pvc-d979977d-d79d-77d9-9d7d-d7d97ddd99d7"`**: The PV that is associated with the storage instance.
   *  **`"storageclass":"ibmc-file-gold"`**: The type of storage class: bronze, silver, gold, or custom.

9. Remove the physical storage instance.

   **File storage:**
   ```
   ibmcloud sl file volume-cancel <filestorage_id>
   ```
   {: pre}

   **Block storage:**
   ```
   ibmcloud sl block volume-cancel <blockstorage_id>
   ```
   {: pre}

10. Verify that the physical storage instance is removed. 
   
   The deletion process might take up to 72 hours to complete.
   {: important}

   **File storage:**
   ```
   ibmcloud sl file volume-list
   ```
   {: pre}
   **Block storage:**
   ```
   ibmcloud sl block volume-list
   ```
   {: pre}


