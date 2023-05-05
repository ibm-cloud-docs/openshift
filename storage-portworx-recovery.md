---

copyright: 
  years: 2014, 2023
lastupdated: "2023-05-05"

keywords: portworx, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Setting up disaster recovery with Portworx
{: #storage_portworx_recovery}

You can configure disaster recovery for your data that you store in your {{site.data.keyword.redhat_openshift_notm}} clusters by using Portworx. When one of your clusters becomes unavailable, Portworx automatically fails over to another cluster so that you can still access your data.  
{: shortdesc}

Disaster recovery with Portworx requires at least two {{site.data.keyword.redhat_openshift_notm}} clusters where Portworx is installed and configured for disaster recovery. One of the two clusters is considered the active cluster where your data is primarily stored. All data is then replicated to the standby cluster. If your active cluster becomes unavailable, Portworx automatically fails over to the standby cluster and makes the standby cluster the new active cluster so that data can continue to be accessed.

If you installed Portworx in one of your clusters without the Portworx disaster recovery plan, you must re-install Portworx with the disaster recovery plan so that you can include this cluster in your disaster recovery configuration.
{: important}

Depending on your cluster setup, Portworx offers the following two disaster recovery configurations:
- [**Metro DR**](https://docs.portworx.com/portworx-install-with-kubernetes/disaster-recovery/#1-metro-dr-nodes-are-in-the-metro-area-network-man){: external}: Your {{site.data.keyword.redhat_openshift_notm}} clusters are in the same metro location, such as both clusters are deployed in one or multiple zones of the `us-south` region. All clusters are configured to use the same Portworx cluster and share the same Portworx key-value store. Data is automatically replicated between the clusters because the Portworx storage layer is shared. RPO (Recovery Point Objective) and RTO (Recovery Time Objective) for this configuration is less than 60 seconds.
- [**Asynchronous DR**](https://docs.portworx.com/portworx-install-with-kubernetes/disaster-recovery/#2-asynchronous-dr-nodes-are-across-different-regions-datacenters){: external}: Your {{site.data.keyword.redhat_openshift_notm}} clusters are deployed in different regions, such as `us-south` and `us-east`. Each cluster has its own Portworx installation and uses a separate Portworx key-value store that is not shared. To replicate data between clusters, you must set up scheduled replication between these clusters. Because of the higher latency and scheduled replication times, the RPO for this scenario might be up to 15 minutes.

To include your cluster in a Portworx disaster recovery configuration:

1. [Choose the disaster recovery configuration that works for your cluster setup](https://docs.portworx.com/portworx-install-with-kubernetes/disaster-recovery/){: external}.
2. Review the prerequisites for the [**Metro DR**](https://docs.portworx.com/portworx-install-with-kubernetes/disaster-recovery/px-metro/1-install-px/#prerequisites){: external} and [**Asynchronous DR**](https://docs.portworx.com/portworx-install-with-kubernetes/disaster-recovery/async-dr/#pre-requisites){: external} configuration.
3. Configure disaster recovery for your cluster. 
    **Metro DR**:
    1. Choose at least two {{site.data.keyword.redhat_openshift_notm}} clusters that are located in the same metro location. If you have one cluster only, you can still configure this cluster for metro disaster recovery, but Portworx can't do a proper failover until a second cluster is configured.
    2. Make sure that all your clusters have sufficient [raw and unformatted block storage](/docs/openshift?topic=openshift-utilities#manual_block) so that you can build your Portworx storage layer.
    3. Set up a [Databases for etcd service instance](/docs/openshift?topic=openshift-storage_portworx_kv_store) for your Portworx key-value store. Because both {{site.data.keyword.redhat_openshift_notm}} clusters must share the key-value store, you can't use the internal Portworx KVDB.
    4. Optional: Decide if you want to set up [encryption for your Portworx volumes](/docs/openshift?topic=openshift-storage-portworx-encyrption).
    5. Follow the instructions to [install Portworx](/docs/openshift?topic=openshift-storage-portworx-deploy) with the disaster recovery plan in both of your clusters. If you installed Portworx without the disaster recovery plan in one of your clusters already, you must re-install Portworx in that cluster with the disaster recovery plan. Make sure that you select **Databases for etcd** from the **Portworx metadata key-value store** drop-down and that you enter the same Databases for etcd API endpoint and Kubernetes secret name in both of your clusters.
    6. Continue following the [Portworx documentation](https://docs.portworx.com/portworx-install-with-kubernetes/disaster-recovery/px-metro/2-pair-clusters/){: external} to pair your clusters, sync data between them, and try out a failover of an application.

    **Asynchronous DR**:
    1. Choose at least two {{site.data.keyword.redhat_openshift_notm}} clusters that are located in different regions. If you have one cluster only, you can still configure this cluster for asynchronous disaster recovery, but Portworx can't do a proper failover until a second cluster is configured.
    2. Make sure that all your clusters have sufficient [raw and unformatted block storage](/docs/openshift?topic=openshift-utilities#manual_block) so that you can build your Portworx storage layer.
    3. Review your [options to configure a Portworx key-value store](/docs/openshift?topic=openshift-storage_portworx_kv_store). Because both clusters are in different regions, each cluster must use its own key-value store. You can use the internal Portworx KVDB or set up a Databases for etcd instance.
    4. Enable Portworx [volume encryption](/docs/openshift?topic=openshift-storage-portworx-encyrption) for both of your clusters. The {{site.data.keyword.keymanagementservicelong_notm}} credentials are later used by Portworx to encrypt data traffic between the clusters.
    5. Follow the instructions to [install Portworx](/docs/openshift?topic=openshift-storage-portworx-deploy) with the disaster recovery plan in both of your clusters. If you installed Portworx without the disaster recovery plan in one of your clusters already, you must re-install Portworx in that cluster with the disaster recovery plan. Make sure that you configure the Portworx key-value store that each cluster uses.
    6. Follow the [Portworx documentation](https://docs.portworx.com/portworx-install-with-kubernetes/disaster-recovery/async-dr/){: external} to create a cluster pair, enable disaster recovery mode, and schedule data migrations between your clusters.





