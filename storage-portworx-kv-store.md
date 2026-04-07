---

copyright: 
  years: 2014, 2026
lastupdated: "2026-04-07"


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

Decide which key-value store you want to use for Portworx metadata.
{: shortdesc}

Before you begin, review [Planning your Portworx setup](/docs/openshift?topic=openshift-storage_portworx_plan).
{: important}

The Portworx key-value store is the single source of truth for your Portworx cluster. If the key-value store is unavailable, you can't use the Portworx cluster to access or store data. Existing data is not changed or removed when the Portworx metadata store is unavailable.

For most environments, set up the internal key-value database (KVDB) during the Portworx installation.

## Using the Portworx key-value database
{: #portworx-kvdb}

Automatically set up a key-value database (KVDB) during the Portworx installation that uses the space on the additional local disks that are attached to your worker nodes.
{: shortdesc}

You can keep Portworx metadata in your cluster by using the internal key-value database (KVDB) that is included with Portworx. Use this option when you want to store metadata together with the operational data that you manage with Portworx. For more information about the internal Portworx KVDB, see the [Portworx documentation](https://docs.portworx.com/portworx-enterprise/concepts/kvdb-for-portworx/internal-kvdb){: external}.

To set up the internal Portworx KVDB, follow the steps in [Installing Portworx in your cluster](/docs/openshift?topic=openshift-storage_portworx_deploy).

If you plan to use the internal KVDB, make sure that your cluster has a minimum of 3 worker nodes with additional local block storage so that the KVDB can be set up for high availability. Your data is automatically replicated across these 3 worker nodes and you can choose to scale this deployment to replicate data across up to 25 worker nodes.
{: note}
