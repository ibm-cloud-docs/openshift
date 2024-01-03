---

copyright: 
  years: 2014, 2024
lastupdated: "2024-01-03"


keywords: openshift, kubernetes, clusters, worker nodes, worker pools, delete

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Removing clusters
{: #remove}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}

Clusters that are created with a billable account must be removed manually when they are not needed anymore so that those clusters are no longer consuming resources.
{: shortdesc}

When you delete the cluster, all worker nodes, apps, and containers are permanently deleted. This action can't be undone. Before you proceed, make sure to back up all required data and configuration files.
{: important}

No backups are created of your cluster or your data in your persistent storage. When you delete a cluster, you can choose to delete your persistent storage. Persistent storage that you provisioned by using a `delete` storage class is permanently deleted in IBM Cloud infrastructure if you choose to delete your persistent storage. If you provisioned your persistent storage by using a `retain` storage class and you choose to delete your storage, the cluster, the PV, and PVC are deleted, but the persistent storage instance in your IBM Cloud infrastructure account remains.
{: important}

**Classic clusters only**: When you remove a cluster, you also remove any subnets that were automatically provisioned when you created the cluster and that you created by using the `ibmcloud oc cluster subnet create` command. However, if you manually added existing subnets to your cluster by using the `ibmcloud oc cluster subnet add` command, these subnets are not removed from your IBM Cloud infrastructure account and you can reuse them in other clusters.
{: note}


**Before you begin**:
* Note your cluster ID. You might need the cluster ID to investigate and remove related IBM Cloud infrastructure resources that are not automatically deleted with your cluster.
* Make sure that you have the [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-users#checking-perms).
* If you want to delete the data in your persistent storage, review the delete options for the type of storage that you use.
    * [File storage](/docs/openshift?topic=openshift-file_storage#storage_delete_options_file)
    * [Block storage](/docs/openshift?topic=openshift-block_storage#cleanup_block) for classic clusters
    * [Block storage](/docs/openshift?topic=openshift-storage-block-vpc-remove) for VPC clusters
    * [Object storage](/docs/cloud-object-storage?topic=cloud-object-storage-deleting-multiple-objects-patterns)
    * [Portworx](/docs/openshift?topic=openshift-storage_portworx_removing)

**To remove a cluster**:

1. Optional: From the CLI, save a copy of all data in your cluster to a local YAML file.
    ```sh
    oc get all --all-namespaces -o yaml
    ```
    {: pre}

2. Remove the cluster.
    - From the {{site.data.keyword.cloud_notm}} console
        1. Select your cluster and click **Delete** from the **More actions** menu.

    - From the {{site.data.keyword.cloud_notm}} CLI
        1. List the available clusters.

            ```sh
            ibmcloud oc cluster ls
            ```
            {: pre}

        2. Delete the cluster.

            ```sh
            ibmcloud oc cluster rm --cluster <cluster_name_or_ID>
            ```
            {: pre}

3. Follow the prompts and choose whether to delete cluster resources, which include containers, pods, bound services, persistent storage, and secrets.
    - **Persistent storage**: If you dynamically provisioned storage with a storage class that sets `reclaimPolicy: Delete`, your persistent volume claim (PVC), persistent volume (PV), and the storage instance are automatically deleted when you delete the cluster. However, depending on when you delete the cluster, you might still see your storage instance in the {{site.data.keyword.cloud_notm}} console for up to 72 hours or until the new billing cycle begins. VPC Block Storage is not removed automatically, even if you used a `Delete` storage class. 

      For storage that was statically provisioned or storage that you provisioned with a storage class that sets `reclaimPolicy: Retain`, the PVC and the PV are removed when you delete the cluster, but your storage instance and your data remain. You are still charged for your storage instance.

      To manually remove the storage and find frequently asked questions about storage removal, review the documentation for each storage type in the links in the **Before you begin** section.


## Removing {{site.data.keyword.satelliteshort}} worker nodes or clusters
{: #satcluster-rm}

When you remove {{site.data.keyword.redhat_openshift_notm}} clusters or worker nodes in a cluster, the hosts that provide the compute capacity for your worker nodes are not automatically deleted. Instead, the hosts remain attached to your {{site.data.keyword.satelliteshort}} location, but require you to reload the host to be able to reassign the hosts to other {{site.data.keyword.satelliteshort}} resources.

1. Back up any data that runs in the worker node or cluster that you want to save. For example, you might save a copy of all the data in your cluster and upload these files to a persistent storage solution, such as {{site.data.keyword.cos_full_notm}}.
    ```sh
    oc get all --all-namespaces -o yaml
    ```
    {: pre}

2. Get the **Worker ID** of each host in your cluster.
    ```sh
    ibmcloud sat host ls --location <satellite_location_name_or_ID>
    ```
    {: pre}

    Example output

    ```sh
    Retrieving hosts...
    OK
    Name              ID                     State      Status   Cluster          Worker ID                                                 Worker IP       
    machine-name-1    aaaaa1a11aaaaaa111aa   assigned   Ready    infrastructure   sat-virtualser-4d7fa07cd3446b1f9d8131420f7011e60d372ca2   169.xx.xxx.xxx       
    machine-name-2    bbbbbbb22bb2bbb222b2   assigned   Ready    infrastructure   sat-virtualser-9826f0927254b12b4018a95327bd0b45d0513f59   169.xx.xxx.xxx       
    machine-name-3    ccccc3c33ccccc3333cc   assigned   Ready    mycluster12345   sat-virtualser-948b454ea091bd9aeb8f0542c2e8c19b82c5bf7a   169.xx.xxx.xxx       
    ```
    {: screen}

3. Remove the worker nodes or clusters by referring to the following options. The corresponding hosts in your {{site.data.keyword.satelliteshort}} location become unassigned and require a reload before you can use them for other {{site.data.keyword.satelliteshort}} resources.
    *  [Resize worker pools](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) to reduce the number of worker nodes in the cluster.
    *  [Remove individual worker nodes](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_rm) from the cluster.
    *  [Remove the cluster](/docs/openshift?topic=openshift-remove).
4. For each worker node that you removed, decide what to do with the corresponding host in your {{site.data.keyword.satelliteshort}} location.
    *  Reload the host operating system so that you can attach and assign the host to other {{site.data.keyword.satelliteshort}} resources such as the location control plane or other clusters. For more information, see the update process in [Updating {{site.data.keyword.satelliteshort}} location control plane hosts](/docs/satellite?topic=satellite-host-update-location).
    *  Delete the hosts from your underlying infrastructure provider. For more information, refer to the infrastructure provider documentation.

## Next steps
{: #cluster-remove-next-steps}


- After the cluster is no longer listed when you run the `ibmcloud oc cluster ls` command, you can reuse the name of a removed cluster.
- **Classic clusters only**: If you kept the subnets, you can [reuse them in a new cluster](/docs/openshift?topic=openshift-subnets#subnets_custom) or manually delete them later from your IBM Cloud infrastructure portfolio.
- **VPC clusters only**: If you have infrastructure resources that you no longer want to use, such as the VPC or subnets, remove these resources in the VPC portal.
- **Persistent storage**: If you kept the persistent storage, you can delete your storage later through the {{site.data.keyword.cloud_notm}} console for the corresponding storage service.
- **{{site.data.keyword.satelliteshort}} clusters**:  If you have hosts attached to your location that you no longer want to use, remove them. For more information see [Removing hosts and locations](/docs/satellite?topic=satellite-host-remove).



