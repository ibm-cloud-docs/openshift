---

copyright: 
  years: 2014, 2023
lastupdated: "2023-08-08"

keywords: portworx, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Removing Portworx
{: #storage_portworx_removing}

Remove a [Portworx volume](#remove_pvc_apps_volumes), a [storage node](#remove_storage_node_cluster-px), or the [entire Portworx cluster](#remove_storage_node_cluster-px) if you don't need it anymore.
{: shortdesc}

## Removing Portworx volumes from apps
{: #remove_pvc_apps_volumes}

When you added storage from your Portworx cluster to your app, you have three main components: the Kubernetes persistent volume claim (PVC) that requested the storage, the Kubernetes persistent volume (PV) that is mounted to your pod and described in the PVC, and the Portworx volume that blocks space on the physical disks of your Portworx cluster. To remove storage from your app, you must remove all components.
{: shortdesc}

1. List the PVCs in your cluster and note the **NAME** of the PVC, and the name of the PV that is bound to the PVC and shown as **VOLUME**.
    ```sh
    oc get pvc
    ```
    {: pre}

    Example output

    ```sh
    NAME                  STATUS    VOLUME                                     CAPACITY   ACCESSMODES   STORAGECLASS            AGE
    px-pvc          Bound     pvc-06886b77-102b-11e8-968a-f6612bb731fb   20Gi       RWO           px-high                 78d
    ```
    {: screen}

2. Review the **`ReclaimPolicy`** for the storage class.
    ```sh
    oc describe storageclass <storageclass_name>
    ```
    {: pre}

    If the reclaim policy says `Delete`, your PV and the data on your physical storage in your Portworx cluster are removed when you remove the PVC. If the reclaim policy says `Retain`, or if you provisioned your storage without a storage class, then your PV and your data are not removed when you remove the PVC. You must remove the PVC, PV, and the data separately.

3. Remove any pods that mount the PVC.
    1. List the pods that mount the PVC.
        ```sh
        oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"
        ```
        {: pre}

        Example output
        ```sh
        blockdepl-12345-prz7b:    claim1-block-bronze  
        ```
        {: screen}

        If no pod is returned in your CLI output, you don't have a pod that uses the PVC.

    2. Remove the pod that uses the PVC.

        If the pod is part of a deployment, remove the deployment.
        {: tip}

        ```sh
        oc delete pod <pod_name>
        ```
        {: pre}

    3. Verify that the pod is removed.
        ```sh
        oc get pods
        ```
        {: pre}

4. Remove the PVC.
    ```sh
    oc delete pvc <pvc_name>
    ```
    {: pre}

5. Review the status of your PV. Use the name of the PV that you retrieved earlier as **VOLUME**.
    ```sh
    oc get pv <pv_name>
    ```
    {: pre}

    When you remove the PVC, the PV that is bound to the PVC is released. Depending on how you provisioned your storage, your PV goes into a `Deleting` state if the PV is deleted automatically, or into a `Released` state, if you must manually delete the PV. **Note**: For PVs that are automatically deleted, the status might briefly say `Released` before it is deleted. Rerun the command after a few minutes to see whether the PV is removed.

6. If your PV is not deleted, manually remove the PV.
    ```sh
    oc delete pv <pv_name>
    ```
    {: pre}

7. Verify that the PV is removed.
    ```sh
    oc get pv
    ```
    {: pre}

8. Verify that your Portworx volume is removed. Log in to one of your Portworx pods in your cluster to list your volumes. To find available Portworx pods, run `oc get pods -n kube-system | grep portworx`.
    ```sh
    oc exec <portworx-pod>  -it -n kube-system -- /opt/pwx/bin/pxctl volume list
    ```
    {: pre}

9. If your Portworx volume is not removed, manually remove the volume.
    ```sh
    oc exec <portworx-pod>  -it -n kube-system -- /opt/pwx/bin/pxctl volume delete <volume_ID>
    ```
    {: pre}

## Removing a worker node from your Portworx cluster or the entire Portworx cluster
{: #remove_storage_node_cluster-px}

You can exclude worker nodes from your Portworx cluster or remove the entire Portworx cluster if you don't want to use Portworx anymore.


Removing your Portworx cluster removes all the data from your Portworx cluster. Make sure to [create a snapshot for your data and save this snapshot to the cloud](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/create-snapshots/){: external}.
{: important}

- **Remove a worker node from the Portworx cluster:** If you want to remove a worker node that runs Portworx and stores data in your Portworx cluster,  you must migrate existing pods to remaining worker nodes and then uninstall Portworx from the node. For more information, see [Decommission a Portworx node in Kubernetes](https://docs.portworx.com/portworx-install-with-kubernetes/operate-and-maintain-on-kubernetes/uninstall/decommission-a-node/){: external}.
- **Remove the Portworx DaemonSet**: When you remove the Portworx DaemonSet, the Portworx containers are removed from your worker nodes. However, the Portworx configuration files remain on the worker nodes and the storage devices, and the data volumes are still intact. You can use the data volumes again if you restart the Portworx DaemonSet and containers by using the same configuration files. For more information, see [Removing the Portworx DaemonSet](#remove_px_daemonset).
- **Remove Portworx from your cluster:** If you want to remove Portworx and all your data from your cluster, follow the steps to [remove Portworx](#remove_portworx) from your cluster.

## Removing the Portworx DaemonSet
{: #remove_px_daemonset}

When you remove the Portworx DaemonSet, the Portworx containers are removed from your worker nodes. However, the Portworx configuration files remain on the worker nodes and the storage devices, and the data volumes are still intact. You can use the data volumes again if you restart the Portworx DaemonSet and containers by using the same configuration files.
{: shortdesc}

Before you begin: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Clone the `ibmcloud-storage-utilities` repo.
    ```sh
    git clone https://github.com/IBM/ibmcloud-storage-utilities.git
    ```
    {: pre}

2. Change directories to the `px-utils/px_cleanup` directory.
    ```sh
    cd ibmcloud-storage-utilities/px-utils/px_cleanup
    ```
    {: pre}

3. Run the `px_cleanup.sh` script to remove the DaemonSet from your cluster.
    ```sh
    sh ./px_cleanup.sh
    ```
    {: pre}



## Removing Portworx from your cluster
{: #remove_portworx}


To stop billing for Portworx, you must remove the Portworx installation from your cluster and remove the Portworx service instance from your {{site.data.keyword.cloud_notm}} account.
{: important}

The following steps remove Portworx from your cluster, including all storage volumes and the data on those volumes.
{: important}

1. Follow the Portworx documentation to [uninstall Portworx](https://docs.portworx.com/operations/operate-kubernetes/uninstall/uninstall-operator/){: external}.

1. Clean up for your Portworx volume attachments, PVCs, and PVs.
    1. List your volume attachments.
        ```sh
        kubectl get volumeattachments
        ```
        {: pre}

    1. Delete the Portworx volume attachments.
        ```sh
        kubectl delete volumeattachments ATTACHMENT-NAME
        ```
        {: pre}

    1. Delete the PVC that starts with name `px-do-not-delete`.
        ```sh
        kubectl delete pvc px-do-not-delete-*** -n PORTWOX-NAMESPACE
        ```
        {: pre}


    1. Delete the PVs that were created for Portworx and are in the `Released` state.
        ```sh
        kubectl delete pv PV-NAME
        ```
        {: pre}

1. Remove the Portworx service instance from your {{site.data.keyword.cloud_notm}} account.
    1. From the [{{site.data.keyword.cloud_notm}} resource list](https://cloud.ibm.com/resources), find the Portworx service that you created.
    2. From the actions menu, click **Delete**.
    3. Confirm the deletion of the service instance by clicking **Delete**.




