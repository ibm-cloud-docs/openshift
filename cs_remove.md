---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-26"

keywords: kubernetes, iks, clusters, worker nodes, worker pools, delete

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
{:gif: data-image-type='gif'}

# Removing clusters
{: #remove}

Free and standard clusters that are created with a billable account must be removed manually when they are not needed anymore so that those clusters are no longer consuming resources.
{:shortdesc}

<p class="important">
No backups are created of your cluster or your data in your persistent storage. When you delete a cluster, you can choose to delete your persistent storage. Persistent storage that you provisioned by using a `delete` storage class is permanently deleted in IBM Cloud infrastructure if you choose to delete your persistent storage. If you provisioned your persistent storage by using a `retain` storage class and you choose to delete your storage, the cluster, the PV, and PVC are deleted, but the persistent storage instance in your IBM Cloud infrastructure account remains.</br>
</br>When you remove a cluster, you also remove any subnets that were automatically provisioned when you created the cluster and that you created by using the `ibmcloud ks cluster-subnet-create` command. However, if you manually added existing subnets to your cluster by using the `ibmcloud ks cluster-subnet-add command`, these subnets are not removed from your IBM Cloud infrastructure account and you can reuse them in other clusters.</p>

Before you begin:
* Note your cluster ID. You might need the cluster ID to investigate and remove related IBM Cloud infrastructure resources that are not automatically deleted with your cluster.
* If you want to delete the data in your persistent storage, [understand the delete options](/docs/containers?topic=containers-cleanup#cleanup).
* Make sure that you have the [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/containers?topic=containers-users#platform).

To remove a cluster:
 
1. Optional: From the CLI, save a copy of all data in your cluster to a local YAML file.
  ```
  {[kubectl]} get all --all-namespaces -o yaml
  ```
  {: pre}

2. Remove the cluster.
  - From the {{site.data.keyword.cloud_notm}} console
    1.  Select your cluster and click **Delete** from the **More actions...** menu.

  - From the {{site.data.keyword.cloud_notm}} CLI
    1.  List the available clusters.

        ```
        ibmcloud ks clusters
        ```
        {: pre}

    2.  Delete the cluster.

        ```
        ibmcloud ks cluster-rm --cluster <cluster_name_or_ID>
        ```
        {: pre}

    3.  Follow the prompts and choose whether to delete cluster resources, which include containers, pods, bound services, persistent storage, and secrets.
      - **Persistent storage**: Persistent storage provides high availability for your data. If you created a persistent volume claim by using an [existing file share](/docs/containers?topic=containers-file_storage#existing_file), then you cannot delete the file share when you delete the cluster. You must manually delete the file share later from your IBM Cloud infrastructure portfolio.

          Due to the monthly billing cycle, a persistent volume claim cannot be deleted on the last day of a month. If you delete the persistent volume claim on the last day of the month, the deletion remains pending until the beginning of the next month.
          {: note}

Next steps:
- After it is no longer listed in the available clusters list when you run the `ibmcloud ks clusters` command, you can reuse the name of a removed cluster.
- If you kept the subnets, you can [reuse them in a new cluster](/docs/containers?topic=containers-subnets#subnets_custom) or manually delete them later from your IBM Cloud infrastructure portfolio.
- If you kept the persistent storage, you can [delete your storage](/docs/containers?topic=containers-cleanup#cleanup) later through the IBM Cloud infrastructure dashboard in the {{site.data.keyword.cloud_notm}} console.


