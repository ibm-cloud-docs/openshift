---

copyright: 
  years: 2014, 2025
lastupdated: "2025-12-02"


keywords: portworx, kubernetes, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Setting up the Portworx key-value store
{: #storage_portworx_kv_store}

You can set up Portworx to use a key-value database (KVDB). A KVDB stores your cluster's state, configuration data, and metadata associated with storage volumes and snapshots.
{: shortdesc}

## Setting up a key-value store for Portworx metadata
{: #portworx_database}

Decide on the key-value store that you want to use to store Portworx metadata.
{: shortdesc}

Before you begin, review the [Planning your Portworx setup section](/docs/openshift?topic=openshift-storage_portworx_plan).
{: important}

The Portworx key-value store serves as the single source of truth for your Portworx cluster. If the key-value store is not available, then you can't work with your Portworx cluster to access or store your data. Existing data is not changed or removed when the Portworx database is unavailable.

To set up your key-value store, [automatically set up a key-value database (KVDB) during the Portworx installation](#portworx-kvdb).

## Using the Portworx key-value database
{: #portworx-kvdb}

Automatically set up a key-value database (KVDB) during the Portworx installation that uses the space on the additional local disks that are attached to your worker nodes.
{: shortdesc}

You can keep the Portworx metadata inside your cluster and store it along with the operational data that you plan to store with Portworx by using the internal key-value database (KVDB) that is included in Portworx. For general information about the internal Portworx KVDB, see the [Portworx documentation](https://docs.portworx.com/portworx-enterprise/concepts/kvdb-for-portworx/internal-kvdb){: external}.

To set up the internal Portworx KDVB, follow the steps in [Installing Portworx in your cluster](/docs/openshift?topic=openshift-storage_portworx_deploy).

If you plan to use the internal KVDB, make sure that your cluster has a minimum of 3 worker nodes with additional local block storage so that the KVDB can be set up for high availability. Your data is automatically replicated across these 3 worker nodes and you can choose to scale this deployment to replicate data across up to 25 worker nodes.
{: note}
