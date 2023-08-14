---

copyright:
  years: 2014, 2023
lastupdated: "2023-08-14"

keywords: openshift, openshift data foundation, openshift container storage, ocs

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}



# Removing OpenShift Data Foundation
{: #ocs-manage-deployment}


Review the following topics to manage your OpenShift Data Foundation deployment.
{: shortdesc}


## Removing ODF from your apps
{: #ocs-remove-apps-storage}
{: step}

To remove ODF from your apps, you can delete your app or deployment and the corresponding PVCs.
{: shortdesc}

If you want to fully remove ODF and all your data, you can [remove your storage cluster](#ocs-rm-crd).
{: note}

1. List your PVCs and note the name of the PVC and the corresponding PV that you want to remove.
    ```sh
    oc get pvc
    ```
    {: pre}

2. Remove any pods that mount the PVC.
    1. List all the pods that currently mount the PVC that you want to delete. If no pods are returned, you don't have any pods that currently use your PVC.
        ```sh
        oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"
        ```
        {: pre}

        Example output
        ```sh
        app    ocs-storagecluster-cephfs
        ```
        {: screen}

    2. Remove the pod that uses the PVC. If the pod is part of a deployment, remove the deployment.
        ```sh
        oc delete pod <pod_name>
        ```
        {: pre}

        ```sh
        oc delete deployment <deployment_name>
        ```
        {: pre}

    3. Verify that the pod or the deployment is removed.
        ```sh
        oc get pods
        ```
        {: pre}

        ```sh
        oc get deployments
        ```
        {: pre}

3. **Optional** Delete the PVC. Deleting the PVC deletes your app data from the storage volume.
    ```sh
    oc delete pvc <pvc_name>
    ```
    {: pre}



## Removing your ODF custom resource
{: #ocs-rm-crd}
{: step}

Complete the following steps to remove the ODF resources from your cluster.
{: shortdesc}

The following steps result in data loss. Back up the data on your local volumes before you remove your ODF deployment.
{: important}

When you delete the `OcsCluster` custom resource from your cluster, the following resources are deleted. Additionally, any apps that require access to the data on your local volumes might experience downtime.
    - ODF driver pods.
    - The MON and OSD PVCs.
    - All data from your volumes. However, if you created PVCs by using the NooBaa storage class, and your apps wrote data to your backing store, the data in your backing store is not deleted.

1. Get the name of your `OcsCluster` custom resource.
    ```sh
    oc get ocscluster
    ```
    {: pre}

    **Example output for a custom resource called `ocscluster-vpc`.**
    ```sh
    NAME             AGE
    ocscluster-vpc   4s
    ```
    {: screen}

1. Delete your `OcsCluster` custom resource. Replace `<ocscluster_name>` with the name of your custom resource.
    ```sh
    oc delete ocscluster <ocscluster_name>
    ```
    {: pre}

    **Example command for an `OcsCluster` custom resource called `ocscluster-vpc`.**
    ```sh
    oc delete ocscluster ocscluster-vpc
    ```
    {: pre}

1. Delete any PVCs that you created.
    ```sh
    oc get pvc
    ```
    {: pre}

1. **Optional** If you don't want to reinstall ODF, you can [Remove the ODF add-on from your cluster](#ocs-rm-cleanup-resources).


## Cleaning up ODF
{: #odf-cleanup}
{: step}

1. Copy one of the following clean up scripts based on your ODF deployment.
    * **VPC or {{site.data.keyword.satelliteshort}} with dynamically provisioned disks** Clean up the remaining Kubernetes resources from your cluster. Save the following script in a file called `cleanup.sh` to your local machine.
        ```sh
        #!/bin/bash
        ocscluster_name=`oc get ocscluster | awk 'NR==2 {print $1}'`
        oc delete ocscluster --all --wait=false
        kubectl patch ocscluster/$ocscluster_name -p '{"metadata":{"finalizers":[]}}' --type=merge
        oc delete ns openshift-storage --wait=false
        sleep 20
        kubectl -n openshift-storage patch persistentvolumeclaim/db-noobaa-db-0 -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch cephblockpool.ceph.rook.io/ocs-storagecluster-cephblockpool -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch cephcluster.ceph.rook.io/ocs-storagecluster-cephcluster -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch cephfilesystem.ceph.rook.io/ocs-storagecluster-cephfilesystem -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch cephobjectstore.ceph.rook.io/ocs-storagecluster-cephobjectstore -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch cephobjectstoreuser.ceph.rook.io/noobaa-ceph-objectstore-user -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch cephobjectstoreuser.ceph.rook.io/ocs-storagecluster-cephobjectstoreuser -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch noobaa/noobaa -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch backingstores.noobaa.io/noobaa-default-backing-store -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch bucketclasses.noobaa.io/noobaa-default-bucket-class -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch storagecluster.ocs.openshift.io/ocs-storagecluster -p '{"metadata":{"finalizers":[]}}' --type=merge
        sleep 20
        oc delete pods -n openshift-storage --all --force --grace-period=0
        sleep 20
        ```
        {: codeblock}

    * **Classic clusters or {{site.data.keyword.satelliteshort}} clusters with local disks** Clean up the remaining Kubernetes resources from your cluster. Save the following script in a file called `cleanup.sh` to your local machine.
        ```sh
        #!/bin/bash
        ocscluster_name=`oc get ocscluster | awk 'NR==2 {print $1}'`
        oc delete ocscluster --all --wait=false
        kubectl patch ocscluster/$ocscluster_name -p '{"metadata":{"finalizers":[]}}' --type=merge
        oc delete ns openshift-storage --wait=false
        sleep 20
        kubectl -n openshift-storage patch persistentvolumeclaim/db-noobaa-db-0 -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch cephblockpool.ceph.rook.io/ocs-storagecluster-cephblockpool -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch cephcluster.ceph.rook.io/ocs-storagecluster-cephcluster -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch cephfilesystem.ceph.rook.io/ocs-storagecluster-cephfilesystem -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch cephobjectstore.ceph.rook.io/ocs-storagecluster-cephobjectstore -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch cephobjectstoreuser.ceph.rook.io/noobaa-ceph-objectstore-user -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch cephobjectstoreuser.ceph.rook.io/ocs-storagecluster-cephobjectstoreuser -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch noobaa/noobaa -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch backingstores.noobaa.io/noobaa-default-backing-store -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch bucketclasses.noobaa.io/noobaa-default-bucket-class -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n openshift-storage patch storagecluster.ocs.openshift.io/ocs-storagecluster -p '{"metadata":{"finalizers":[]}}' --type=merge
        sleep 20
        oc delete pods -n openshift-storage --all --force --grace-period=0
        oc delete ns local-storage --wait=false
        sleep 20
        kubectl -n local-storage patch localvolume.local.storage.openshift.io/local-block -p '{"metadata":{"finalizers":[]}}' --type=merge
        kubectl -n local-storage patch localvolume.local.storage.openshift.io/local-file -p '{"metadata":{"finalizers":[]}}' --type=merge
        sleep 20
        oc delete pods -n local-storage --all --force --grace-period=0
        ```
        {: codeblock}

1. Run the `cleanup.sh` script.
    ```sh
    sh ./cleanup.sh
    ```
    {: pre}

1. ****Classic clusters or {{site.data.keyword.satelliteshort}} clusters with local disks** After you run the cleanup script, log in to each worker node and run the following commands.
    1. Deploy a debug pod and run `chroot /host`.
        ```sh
        oc debug node/<node_name> -- chroot /host
        ```
        {: pre}

    1. Run the following command to remove any files or directories on the specified paths. Repeat this step for each worker node that you used in your OCS configuration.
        ```sh
        rm -rvf /var/lib/rook /mnt/local-storage
        ```
        {: codeblock}

        Example output:
        ```sh
        removed '/var/lib/rook/openshift-storage/log/ocs-deviceset-0-data-0-6fgp6/ceph-volume.log'
        removed directory: '/var/lib/rook/openshift-storage/log/ocs-deviceset-0-data-0-6fgp6'
        removed directory: '/var/lib/rook/openshift-storage/log'
        removed directory: '/var/lib/rook/openshift-storage/crash/posted'
        removed directory: '/var/lib/rook/openshift-storage/crash'
        removed '/var/lib/rook/openshift-storage/client.admin.keyring'
        removed '/var/lib/rook/openshift-storage/openshift-storage.config'
        removed directory: '/var/lib/rook/openshift-storage'
        removed directory: '/var/lib/rook'
        removed '/mnt/local-storage/localblock/nvme3n1'
        removed directory: '/mnt/local-storage/localblock'
        removed '/mnt/local-storage/localfile/nvme2n1'
        removed directory: '/mnt/local-storage/localfile'
        removed directory: '/mnt/local-storage'
        ```
        {: codeblock}

1. **Optional**: **Classic clusters or {{site.data.keyword.satelliteshort}} clusters with local disks** If you no longer want to use the local volumes that you used in your configuration, you can delete them from the cluster. List the local PVs.
    ```sh
    oc get pv
    ```
    {: pre}

    Example output:
    ```sh
    local-pv-180cfc58   139Gi      RWO            Delete           Available           localfile               11m
    local-pv-67f21982   139Gi      RWO            Delete           Available           localfile               12m
    local-pv-80c5166    100Gi      RWO            Delete           Available           localblock              12m
    local-pv-9b049705   139Gi      RWO            Delete           Available           localfile               12m
    local-pv-b09e0279   100Gi      RWO            Delete           Available           localblock              12m
    local-pv-f798e570   100Gi      RWO            Delete           Available           localblock              12m
    ```
    {: screen}

1. Delete the local PVs.
    ```sh
    oc delete pv <pv_name> <pv_name> <pv_name>
    ```
    {: pre}
    
1. After deleting your PVCs and PVs, you also need to delete the storage volumes from your account. To locate and remove unused storage volumes in your account, see [Why am I still seeing charges for block storage devices after deleting my cluster?](/docs/containers?topic=containers-ts_storage_clean_volume).

## Uninstalling the OpenShift Data Foundation add-on
{: #odf-addon-rm}
{: step}

### Uninstalling the OpenShift Data Foundation add-on from the console
{: #ocs-addon-rm-console}
{: ui}

To remove the OpenShift Data Foundation add-on from your cluster, complete the following steps.
{: shortdesc}

If you want to remove all ODF resources and data from your cluster, [remove the CRDs](/docs/openshift?topic=openshift-ocs-manage-deployment#ocs-rm-crd) before uninstalling the add-on.
{: important}

1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster for which you want to remove the OpenShift Data Foundation add-on.
1. On the cluster **Overview** page, scroll to your installed add-ons.
1. On the OpenShift Data Foundation card, click the **Actions** icon and then **Uninstall**.

### Uninstalling the OpenShift Data Foundation add-on from the CLI
{: #ocs-addon-rm-cli}
{: cli}

You can uninstall the OpenShift Data Foundation add-on from your cluster by using the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} or the CLI.
{: shortdesc}

If you want to remove all ODF resources and data from your cluster, [remove the CRDs](/docs/openshift?topic=openshift-ocs-manage-deployment#ocs-rm-crd) before uninstalling the add-on.
{: important}

1. Uninstall the add-on.
    ```sh
    ibmcloud oc cluster addon disable openshift-container-storage -c <cluster_name>
    ```
    {: pre}

1. Verify that the add-on is removed.
    ```sh
    ibmcloud oc cluster addon ls -c <cluster_name>
    ```
    {: pre}


## Troubleshooting ODF
{: #odf-troubleshooting-gather}

To gather the information to troubleshoot ODF, you can use the `oc adm must-gather` command and specify the ODF image. For more information, see [Gathering cluster data](https://docs.openshift.com/container-platform/4.12/support/gathering-cluster-data.html).
{: shortdesc}

Example command:

```sh
oc adm must-gather --image=registry.redhat.io/ocs4/ocs-must-gather-rhel8:latest --dest-dir=ocs_mustgather
```
{: pre}

You can use the Rook community toolbox to debug issues with your Ceph cluster. For more information, see the [Rook documentation](https://rook.io/docs/rook/v1.3/ceph-toolbox.html){: external}.
{: tip}

For more information, review the [common troubleshooting topics](/docs/openshift?topic=openshift-sitemap#sitemap_openshift_data_foundation).






