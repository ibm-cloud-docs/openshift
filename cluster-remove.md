---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-06"

keywords: openshift, roks, rhos, rhoks, clusters, delete, remove

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Removing clusters
{: #remove}

Clusters that are created with a billable account must be removed manually when they are not needed anymore so that those clusters are no longer consuming resources.
{: shortdesc}

When you delete the cluster, all worker nodes, apps, and containers are permanently deleted. This action cannot be undone. Before you proceed, make sure to back up all required data and configuration files.
{: important}

No backups are created of your cluster or your data in your persistent storage. When you delete a cluster, you can choose to delete your persistent storage. Persistent storage that you provisioned by using a `delete` storage class is permanently deleted in IBM Cloud infrastructure if you choose to delete your persistent storage. If you provisioned your persistent storage by using a `retain` storage class and you choose to delete your storage, the cluster, the PV, and PVC are deleted, but the persistent storage instance in your IBM Cloud infrastructure account remains.
{: important}

**Classic clusters only**: When you remove a cluster, you also remove any subnets that were automatically provisioned when you created the cluster and that you created by using the `ibmcloud oc cluster subnet create` command. However, if you manually added existing subnets to your cluster by using the `ibmcloud oc cluster subnet add` command, these subnets are not removed from your IBM Cloud infrastructure account and you can reuse them in other clusters.
{: note}

When you delete your cluster, the default {{site.data.keyword.cloudcerts_short}} instance for your cluster, which is named in the format `kube-crtmgr-<cluster_ID>`, is also automatically deleted. Any certificates that are stored in the {{site.data.keyword.cloudcerts_short}} instance for your cluster are deleted when the {{site.data.keyword.cloudcerts_short}} instance is deleted.
{: note}

**Before you begin**:
* Note your cluster ID. You might need the cluster ID to investigate and remove related IBM Cloud infrastructure resources that are not automatically deleted with your cluster.
* Make sure that you have the [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/containers?topic=containers-users#checking-perms).
* If you want to delete the data in your persistent storage, review the delete options for the type of storage that you use.
    * [File storage](/docs/containers?topic=containers-file_storage#storage_delete_options_file)
    * [Block storage](/docs/containers?topic=containers-block_storage#cleanup_block) for classic clusters
    * [Block storage](/docs/containers?topic=containers-vpc-block#cleanup_block_vpc) for VPC clusters
    * [Object storage](/docs/cloud-object-storage?topic=cloud-object-storage-deleting-multiple-objects-patterns)
    * [Portworx](/docs/containers?topic=containers-portworx#portworx_cleanup)

**To remove a cluster**:

1. Optional: From the CLI, save a copy of all data in your cluster to a local YAML file.
    ```sh
    oc get all --all-namespaces -o yaml
    ```
    {: pre}

2. Remove the cluster.
    - From the {{site.data.keyword.cloud_notm}} console
        1. Select your cluster and click **Delete** from the **More actions...** menu.

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
    - **Persistent storage**: If you [dynamically provisioned](/docs/containers?topic=containers-kube_concepts#dynamic_provisioning) storage with a storage class that sets `reclaimPolicy: Delete`, your persistent volume claim (PVC), persistent volume (PV), and the storage instance are automatically deleted when you delete the cluster. However, depending on when you delete the cluster, you might still see your storage instance in the {{site.data.keyword.cloud_notm}} console for up to 72 hours or until the new billing cycle begins. 

      For storage that was [statically provisioned](/docs/containers?topic=containers-kube_concepts#static_provisioning), or storage that you provisioned with a storage class that sets `reclaimPolicy: Retain`, the PVC and the PV are removed when you delete the cluster, but your storage instance and your data remain. You are still charged for your storage instance.

      To manually remove the storage and find frequently asked questions about storage removal, review the documentation for each storage type in the links in the **Before you begin** section.

Next steps:
- After it is no longer listed in the available clusters list when you run the `ibmcloud oc cluster ls` command, you can reuse the name of a removed cluster.
- ![Classic infrastructure provider icon.](images/icon-classic-2.svg) **Classic clusters only**: If you kept the subnets, you can [reuse them in a new cluster](/docs/containers?topic=containers-subnets#subnets_custom) or manually delete them later from your IBM Cloud infrastructure portfolio.
- ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) **VPC clusters only**: If you have infrastructure resources that you no longer want to use, such as the VPC or subnets, remove these resources in the VPC portal.
- If you kept the persistent storage, you can delete your storage later through the {{site.data.keyword.cloud_notm}} console for the corresponding storage service.




