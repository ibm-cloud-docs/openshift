---

copyright:
  years: 2014, 2023
lastupdated: "2023-06-07"

keywords: openshift, openshift data foundation, openshift container storage, ocs

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}







# Managing your OpenShift Data Foundation deployment
{: #ocs-manage-deployment}


Review the following topics to manage your OpenShift Data Foundation deployment.
{: shortdesc}


## Updating the add-on from the console
{: #odf-addon-update-console}
{: ui}

Update your OpenShift Data Foundation deployment from the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}.
{: shortdesc}

1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster for which you want to update the OpenShift Data Foundation add-on.
1. On the cluster **Overview** page, scroll to your installed add-ons.
1. On the OpenShift Data Foundation card, click the **Actions** icon and then **Update**.


## Updating the add-on from the CLI
{: #odf-addon-update-cli}
{: cli}

The ODF add-on supports `n+1` cluster versions. For example, if you have version `4.10.0` of the add-on, it is supported on cluster versions `4.9` to `4.11`.
{: shortdesc}


1. Check the existing version.
    ```sh
    ibmcloud oc cluster addon ls --cluster <cluster>
    ```
    {: pre}

1. Update the add-on.
    ```sh
    ibmcloud oc cluster addon update openshift-data-foundation --cluster <cluster-name>
    ```
    {: pre}

1. Get the name of you ODF storage cluster
    ```sh
    oc get ocscluster
    ```
    {: pre}

    Example output
    ```sh
    NAME             AGE
    ocscluster-vpc   19d
    ```
    {: screen}

1. Run the following command to edit your `OcsCluster`.
    ```sh
    oc edit ocscluster <ocs-cluster-name>
    ```
    {: pre}

1. Edit the `OcsCluster` and set the `OcsUpgrade` parameter to `true`.
    ```yaml
    ...
    spec:
        billingType: hourly
    monSize: 20Gi
    monStorageClassName: ibmc-vpc-block-10iops-tier
    numOfOsd: 1
    ocsUpgrade: true
    osdSize: 100Gi
    osdStorageClassName: ibmc-vpc-block-10iops-tier
    status:
        storageClusterStatus: Decreasing the capacity not allowed
    ```
    {: codeblock}

1. Save and close the `OcsCluster` to reapply it to your cluster.
    
## Updating worker nodes that use OpenShift Data Foundation
{: #odf-update-worker}



For clusters with a storage solution such as OpenShift Data Foundation or Portworx, you must cordon, drain, and replace each worker node sequentially. If you deployed OpenShift Data Foundation to a subset of worker nodes in your cluster, then after you replace the worker node, you must then edit the `ocscluster` resource to include the new worker node.
{: shortdesc}

[Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cli-install#cs_cli_configure)

Before updating your worker nodes, make sure to back up your app data. Also, plan to complete the following steps for one worker node at a time. Repeat the steps for each worker node that you want to update.
{: important}

1. List your worker nodes by using `oc get nodes` and determine which worker nodes you want to update.

    ```sh
    oc get nodes
    ```
    {: pre}
    
    Example output
        
    ```sh
    NAME           STATUS   ROLES           AGE    VERSION
    10.241.0.4     Ready    master,worker   106s   v1.21.6+4b61f94
    10.241.128.4   Ready    master,worker   22d    v1.21.6+bb8d50a
    10.241.64.4    Ready    master,worker   22d    v1.21.6+bb8d50a
    ```
    {: screen}

1. Identify the monitor pod and OSDs that are running in the node that you want to replace.
    ```sh
    oc get pods -n openshift-storage -o wide | grep -i <node_name>
    ```
    {: pre}

1. Scale down the deployments that you found in the previous step. For example the `rook-ceph-mon` and `rook-ceph-osd` deployments.
    ```sh
    oc scale deployment rook-ceph-mon-DEPLOYMENT_NAME --replicas=0 -n openshift-storage
    ```
    {: pre}

1.  Cordon the node. Cordoning the node prevents any pods from being scheduled on this node.
    ```sh
    oc adm cordon NODE_NAME
    ```
    {: pre}
    
    Example output
    
    ```sh
    node/10.241.0.4 cordoned
    ```
    {: screen}
    
1. Drain the node to remove all the pods. When you drain the worker node, the pods move to the other worker nodes ensuring there is no downtime. Draining also ensures that there is no disruption of the pod disruption budget. 
    ```sh
    oc adm drain NODE_NAME --force --delete-emptydir-data --ignore-daemonsets
    ```
    {: pre}
    
    Example output
    ```sh
    evicting pod "managed-storage-validation-webhooks-7fd79bc9f7-pdpv6"
    evicting pod "calico-kube-controllers-647dbbd685-fmrp9"
    evicting pod "certified-operators-2v852"
    evicting pod "csi-snapshot-controller-77fbf474df-47ddt"
    evicting pod "calico-typha-8574d89b8c-7f2cc"
    evicting pod "dns-operator-6d48cbff67-vrrsw"
    evicting pod "router-default-6fc798b98b-9m6kh"
    evicting pod "prometheus-adapter-5b77ffdd5f-hzqrp"
    evicting pod "alertmanager-main-1"
    evicting pod "prometheus-k8s-0"
    evicting pod "network-check-source-66c7fbb86-2r78z"
    ```
    {: screen}
    
1. Wait until draining finishes, then complete the following steps to replace the worker node. When you replace a worker node in VPC Gen 2 you get a new worker node with the latest patch updates. For more information, see [Updating VPC Gen 2 worker nodes](/docs/containers?topic=containers-update#vpc_worker_node).

1. List your worker nodes by using `ibmcloud oc worker ls` and determine which worker node you want to update.
    ```sh
    ibmcloud oc worker ls -c CLUSTER
    ```
    {: pre}
    
    Example output
    ```sh
    ID                                                 Primary IP     Flavor     State    Status   Zone        Version   
    kube-c85ra07w091uv4nid9ug-vpcoc-default-000001c1   10.241.128.4   bx2.4x16   normal   Ready    us-east-3   4.8.29_1544_openshift*   
    kube-c85ra07w091uv4nid9ug-vpcoc-default-00000288   10.241.0.4     bx2.4x16   normal   Ready    us-east-1   4.8.29_1544_openshift*   
    kube-c85ra07w091uv4nid9ug-vpcoc-default-00000352   10.241.64.4    bx2.4x16   normal   Ready    us-east-2   4.8.29_1544_openshift*
    ```
    {: pre}

    **Classic Clusters**: Update one worker node at a time by using the  `worker update` [command](/docs/containers?topic=containers-kubernetes-service-cli#cs_worker_update). 

    ```sh
    ibmcloud ks worker update --cluster CLUSTER --worker WORKER_ID 
    ```
    {: pre}

    **VPC Clusters**: Replace one worker node at a time by using the  `worker replace` [command](/docs/containers?topic=containers-kubernetes-service-cli#cli_worker_replace). For more information, see [Updating VPC Gen 2 worker nodes](/docs/containers?topic=containers-update#vpc_worker_node).
    ```sh
    ibmcloud oc worker replace -c CLUSTER --worker kube-***
    ```
    {: pre}
        
    Example output
    ```sh
    The replacement worker node is created in the same zone with the same flavor, but gets new public or private IP addresses. During the replacement, all pods might be rescheduled onto other worker nodes and data is deleted if not stored outside the pod. To avoid downtime, ensure that you have enough worker nodes to handle your workload while the selected worker nodes are being replaced.
    Replace worker node kube-c85ra07w091uv4nid9ug-cluster-default-00000288? [y/N]> y
    Deleting worker node kube-c85ra07w091uv4nid9ug-cluster-default-00000288 and creating a new worker node in cluster
    ```
    {: screen}
    
1. Wait for the replacement node to be provisioned and then list your worker nodes. Note that this process might take 20 minutes or more.
    ```sh
    oc get nodes
    ```
    {: pre}
    
    Example output
    
    ```sh
    NAME           STATUS   ROLES           AGE   VERSION
    10.241.0.4     Ready    master,worker   22d   v1.21.6+bb8d50a
    10.241.128.4   Ready    master,worker   22d   v1.21.6+bb8d50a
    10.241.64.4    Ready    master,worker   22d   v1.21.6+bb8d50a
    ```
    {: screen}

1. Navigate to the openshift-storage project.
    ```sh
    oc project openshift-storage
    ```
    {: pre}

1. Remove the failed OSD from the cluster. You can specify multiple failed OSDs if required:
    ```sh
    oc process -n openshift-storage ocs-osd-removal \ -p FAILED_OSD_IDS=<failed_osd_id> | oc create -f <failed_osd_id_1>,<failed_osd_id_2>, <failed_osd_id_3>
    ```
    {: pre}

    The `FORCE_OSD_REMOVAL` value must be changed to true in clusters that only have three OSDs, or clusters with insufficient space to restore all three replicas of the data after the OSD is removed.
    {: note}

1. Verify that the OSD was removed successfully by checking the status of the ocs-osd-removal-job pod.
    ```sh
    oc get pod -l job-name=ocs-osd-removal-job -n openshift-storage
    ```
    {: pre}

1. Verify that the OSD removal is completed.
    ```sh
    oc logs -l job-name=ocs-osd-removal-job -n openshift-storage --tail=-1 | egrep -i 'completed removal'
    ```
    {: pre}

    Example output

    ```sh
    2023-03-10 06:50:04.501511 I | cephosd: completed removal of OSD 0
    ```
    {: screen}


    1. For clusters using local storage configurations identify the Persistent Volume (PV) associated with the Persistent Volume Claim (PVC).
        ```sh
        oc get pv -L kubernetes.io/hostname | grep localblock | grep Released
        ```
        {: pre}

        Example output:
        ```sh
        PV_NAME 1490Gi  RWO  Delete  Released  openshift-storage/ocs-deviceset-0-data-0-6c5pw  localblock  2d22h  compute-1
        ```
        {: screen}

    1. If there is a PV in Released state, delete it:
        ```sh
        oc delete pv <persistent_volume>
        ```
        {: pre}
    

1. If you limited your ODF deployment to a subset of worker nodes by specifying node names during installation, you must update the `ocscluster` CRD to include the new name. 
    If you did not limit your configuration to only certain worker nodes, you do not need to update `ocscluster`.
    {: important}
    
    ```sh
    oc edit ocscluster 
    ```
    {: pre}

1. Wait for the OpenShift Data Foundation pods to deploy to the new worker. Verify the OSD persistent volumes get created and that all pods are `Running`.
    ```sh
    oc get pv
    oc get ocscluster
    oc get pods -n openshift-storage
    ```
    {: pre}

1. Identify the `crashcollector` pod deployment.
    ```sh
    oc get deployment --selector=app=rook-ceph-crashcollector,node_name=<failed_node_name> -n openshift-storage
    ```
    {: pre}

1. If there is an existing `crashcollector` deployment, delete it.
    ```sh
    oc delete deployment --selector=app=rook-ceph-crashcollector,node_name=<failed_node_name> -n openshift-storage
    ```
    {: pre}

1. Delete the ocs-osd-removal-job. 
    ```sh
    oc delete -n openshift-storage job ocs-osd-removal-job
    ```
    {: pre}

    Example output:
    ```sh
    job.batch "ocs-osd-removal-job" deleted
    ```
    {: screen}
    
    


## Removing the OpenShift Data Foundation add-on from your cluster
{: #ocs-addon-rm}

You can remove ODF add-on from your cluster by using the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} or the CLI.
{: shortdesc}

When you disable the OpenShift Data Foundation add-on, only the ODF operator is removed from your cluster. Your existing workloads remain, but you can't create more ODF workloads. You also can't delete your `OcsCluster` custom resource after the operator is removed. If you want to remove all your ODF resources and data, see [Removing ODF from your cluster](/docs/openshift?topic=openshift-ocs-manage-deployment#ocs-rm-crd). If you removed the add-on and can't delete your `OcsCluster`, reinstall the add-on, then delete the `OcsCluster`.
{: note}

## Removing ODF from your apps
{: #ocs-remove-apps-storage}

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

## Cleaning up your ODF deployment
{: #ocs-rm-cleanup-resources}

After you remove ODF from your apps, and remove your ODF storage cluster, you can clean up the remaining Kubernetes resources that were deployed with ODF.
{: shortdesc}

### Cleaning up ODF
{: #ocs-cleanup}

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

To gather the information to troubleshoot ODF, you can use the `oc adm must-gather` command and specify the ODF image. For more information, see [Gathering cluster data](https://docs.openshift.com/container-platform/4.11/support/gathering-cluster-data.html).
{: shortdesc}

Example command:

```sh
oc adm must-gather --image=registry.redhat.io/ocs4/ocs-must-gather-rhel8:latest --dest-dir=ocs_mustgather
```
{: pre}

You can use the Rook community toolbox to debug issues with your Ceph cluster. For more information, see the [Rook documentation](https://rook.io/docs/rook/v1.3/ceph-toolbox.html){: external}.
{: tip}

For more information, review the [common troubleshooting topics](/docs/openshift?topic=openshift-sitemap#sitemap_openshift_data_foundation).






