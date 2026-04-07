---

copyright: 
  years: 2014, 2026
lastupdated: "2026-04-07"


keywords: portworx, kubernetes, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Preparing your cluster for Portworx
{: #storage_portworx_preparing}

If you want to build your Portworx storage layer on non-SDS worker nodes in a classic cluster, you must first add raw, unformatted, and unmounted block storage to your worker nodes. For VPC clusters, you can either attach storage before you install Portworx or allow Portworx to dynamically create cloud drives by using the {{site.data.keyword.block_storage_is_short}} driver during installation.
{: shortdesc}

Raw block storage can't be provisioned by using Kubernetes persistent volume claims (PVCs) as the block storage device is automatically formatted by {{site.data.keyword.openshiftlong_notm}}. Instead, you can use the {{site.data.keyword.cloud_notm}} Block Volume Attacher plug-in in classic clusters or the VPC console, CLI, or API in VPC clusters to add block storage to your worker nodes.

Portworx supports block storage only. Worker nodes that mount file or object storage can't be used for the Portworx storage layer.
{: note}

Keep in mind that the networking of non-SDS worker nodes in classic clusters is not optimized for Portworx and might not offer the performance benefits that your app requires.
{: note}

## Classic clusters
{: #px-create-classic-volumes}

[Classic]{: tag-classic} 

1. [Install the {{site.data.keyword.cloud_notm}} Block Volume Attacher plug-in](/docs/openshift?topic=openshift-utilities#block_storage_attacher).
2. [Manually add block storage](/docs/openshift?topic=openshift-utilities#manual_block) to your worker nodes. For highly available data storage, Portworx requires at least 3 worker nodes with raw and unformatted block storage.
3. If you plan to use separate journal or KVDB devices, log in to the worker node by using `oc debug <node>` and run `lsblk` to identify the device paths. Save these device paths because you will need them during the Portworx installation.
4. If you want to use [journal devices](https://docs.portworx.com/portworx-enterprise/operations/add-journal-dev.html){: external}, choose from the following options. Journal devices allow Portworx to write logs directly to a local disk on your worker node.
    - Attach an additional 3 GB disk to at least 3 worker nodes to use for the journal.
    - Select one of the block storage devices that you added earlier to use for the journal.
    - Let Portworx automatically create a journal partition during installation.
5. If you want to use a specific device for the internal Portworx key-value database (KVDB), choose from the following options.
    - Attach an additional 3 GB disk to at least 3 worker nodes to use for the KVDB.
    - Select one of the block storage devices that you added earlier.
6. [Attach the block storage](/docs/openshift?topic=openshift-utilities#attach_block) to your worker nodes.
7. Continue with your Portworx setup by [Setting up a key-value store for Portworx metadata](/docs/openshift?topic=openshift-storage_portworx_kv_store).

## VPC clusters
{: #px-create-vpc-volumes}

[Virtual Private Cloud]{: tag-vpc} 

1. Follow the [steps](/docs/openshift?topic=openshift-utilities#vpc_cli_attach) to create the {{site.data.keyword.block_storage_is_short}} instances and attach them to each worker node that you want to add to the Portworx storage layer. For highly available data storage, Portworx requires at least 3 worker nodes with raw and unformatted block storage.
2. If you plan to use separate journal or KVDB devices, log in to the worker node by using `oc debug <node>` and run `lsblk` to identify the device paths. Save these device paths because you will need them during the Portworx installation.
3. If you want to use [journal devices](https://docs.portworx.com/portworx-enterprise/operations/add-journal-dev.html){: external}, choose from the following options. Journal devices allow Portworx to write logs directly to a local disk on your worker node.
    - [Attach](/docs/openshift?topic=openshift-utilities#vpc_cli_attach) an additional 3 GB disk to at least 3 worker nodes in your cluster.
    - Select a device on a worker node where you want Portworx to create the journal.
4. If you want to use a specific device for the internal Portworx KVDB, choose from the following options.
    - Attach an additional 3 GB disk to at least 3 worker nodes to use for the KVDB.
    - Select one of the block storage devices that you added earlier to use for the KVDB.
5. Continue with your Portworx setup by [Setting up a key-value store for Portworx metadata](/docs/openshift?topic=openshift-storage_portworx_kv_store).



## Satellite clusters
{: #px-create-satellite-volumes}

[Satellite]{: tag-satellite} 

1. [Create a {{site.data.keyword.satelliteshort}} location](/docs/satellite?topic=satellite-locations).
1. Create VMs in your cloud provider or set up on-premises hosts that have at least 16 vCPU, 64 GB memory, and enough storage to attach to your location, plus additional storage volumes for app data, the Portworx journal, and the KVDB. For highly available data storage, Portworx requires at least 3 worker nodes with raw and unformatted block storage.
1. If you plan to use separate journal or KVDB devices, log in to the worker node with `oc debug <node>` and run `lsblk` to identify the device paths. Save these device paths because you will need them during the Portworx installation.
1. If you want to use [journal devices](https://docs.portworx.com/portworx-enterprise/operations/add-journal-dev.html){: external}, choose from the following options. Journal devices allow Portworx to write logs directly to a local disk on your worker node.
    - Attach an additional 3 GB disk to at least 3 worker nodes in your cluster.
    - Select a device on a worker node where you want Portworx to create the journal.
1. If you want to use a specific device for the internal Portworx KVDB, choose from the following options.
    - Attach an additional 3 GB disk to at least 3 worker nodes to use for the KVDB.
    - Select one of the block storage devices that you added earlier to use for the KVDB.
1. Continue with your Portworx setup by [Setting up a key-value store for Portworx metadata](/docs/openshift?topic=openshift-storage_portworx_kv_store).
