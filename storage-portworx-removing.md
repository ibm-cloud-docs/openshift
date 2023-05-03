---

copyright: 
  years: 2014, 2023
lastupdated: "2023-05-03"

keywords: portworx, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


## Cleaning up your Portworx volumes and cluster
{: #storage-portworx-removing}

Remove a [Portworx volume](#remove_pvc_apps_volumes), a [storage node](#remove_storage_node_cluster-px), or the [entire Portworx cluster](#remove_storage_node_cluster-px) if you don't need it anymore.
{: shortdesc}

### Removing Portworx volumes from apps
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

### Removing a worker node from your Portworx cluster or the entire Portworx cluster
{: #remove_storage_node_cluster-px}

You can exclude worker nodes from your Portworx cluster or remove the entire Portworx cluster if you don't want to use Portworx anymore.
{: shortdesc}

Removing your Portworx cluster removes all the data from your Portworx cluster. Make sure to [create a snapshot for your data and save this snapshot to the cloud](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/create-snapshots/){: external}.
{: important}

- **Remove a worker node from the Portworx cluster:** If you want to remove a worker node that runs Portworx and stores data in your Portworx cluster,  you must migrate existing pods to remaining worker nodes and then uninstall Portworx from the node. For more information, see [Decommission a Portworx node in Kubernetes](https://docs.portworx.com/portworx-install-with-kubernetes/operate-and-maintain-on-kubernetes/uninstall/decommission-a-node/){: external}.
- **Remove the Portworx DaemonSet**: When you remove the Portworx DaemonSet, the Portworx containers are removed from your worker nodes. However, the Portworx configuration files remain on the worker nodes and the storage devices, and the data volumes are still intact. You can use the data volumes again if you restart the Portworx DaemonSet and containers by using the same configuration files. For more information, see [Removing the Portworx DaemonSet](#remove_px_daemonset).
- **Remove Portworx from your cluster:** If you want to remove Portworx and all your data from your cluster, follow the steps to [remove Portworx](/docs/openshift?topic=openshift-storage-portworx-removing) from your cluster.

### Removing the Portworx DaemonSet
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



### Removing Portworx from your cluster
{: #remove_portworx}

If you don't want to use Portworx in your cluster, you can uninstall the Helm chart and delete your Portworx instance.
{: shortdesc}

The following steps walk you through deleting the Portworx Helm chart from your cluster and deleting your Portworx instance. If you want to clean up your Portworx installation by removing your volumes from your apps, removing individual worker nodes from Portworx, or if you want to completely remove Portworx and all your volumes and data, see [Cleaning up your Portworx cluster](#portworx_cleanup).
{: note}

The following commands result in data loss.
{: important}

1. Follow the steps to [uninstall Portworx](https://docs.portworx.com/portworx-install-with-kubernetes/operate-and-maintain-on-kubernetes/uninstall/uninstall/#delete-wipe-px-cluster-configuration){: external}. Note that for private clusters, you must specify the `px-node-wiper` image from the private `icr.io` registry.
    ```sh
    curl  -fSsL https://install.portworx.com/px-wipe | bash -s -- --talismanimage icr.io/ext/portworx/talisman --talismantag 1.1.0 --wiperimage icr.io/ext/portworx/px-node-wiper --wipertag 2.5.0
    ```
    {: pre}

2. Find the installation name of your Portworx Helm chart.
    ```sh
    helm ls -A | grep portworx
    ```
    {: pre}

    Example output

    ```sh
    NAME             NAMESPACE      REVISION    UPDATED                                 STATUS       CHART                                  APP VERSION
    <release_name>     <namespace>        1     2020-01-27 09:18:33.046018 -0500 EST    deployed  portworx-1.0.0     default     
    ```
    {: screen}

3. Delete Portworx by removing the Helm chart.
    ```sh
    helm uninstall <release_name>
    ```
    {: pre}

4. Verify that the Portworx pods are removed.
    ```sh
    oc get pod -n kube-system | grep 'portworx\|stork'
    ```
    {: pre}

    The removal of the pods is successful if no pods are displayed in your CLI output.

5. Delete the Portworx storage classes from your cluster.
    ```sh
    oc delete sc portworx-db-sc portworx-db-sc-remote portworx-db2-sc portworx-null-sc portworx-shared-sc
    ```
    {: pre}

6. Verify that the storage classes are removed.
    ```sh
    oc get sc
    ```
    {: pre}

7. Verify that the Portworx resources are removed.
    ```sh
    oc get all -A | grep portworx
    ```
    {: pre}

8. Remove the Portworx service instance from your {{site.data.keyword.cloud_notm}} account.
    1. From the [{{site.data.keyword.cloud_notm}} resource list](https://cloud.ibm.com/resources), find the Portworx service that you created.
    2. From the actions menu, click **Delete**.
    3. Confirm the deletion of the service instance by clicking **Delete**.

To stop billing for Portworx, you must remove the Portworx Helm installation from your cluster and remove the Portworx service instance from your {{site.data.keyword.cloud_notm}} account.
{: important}




