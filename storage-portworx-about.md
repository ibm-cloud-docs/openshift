---

copyright: 
  years: 2014, 2024
lastupdated: "2024-07-18"


keywords: portworx, kubernetes, <containers>containers</containers><openshift>openshift</openshift>

subcollection: <containers>containers</containers><openshift>openshift</openshift>


---

{{site.data.keyword.attribute-definition-list}}


# About Portworx
{: #storage_portworx_about}

Review frequently asked questions to learn more about Portworx and how Portworx provides highly available persistent storage management for your containerized apps.
{: shortdesc}

## What is software-defined storage (SDS)?
{: #about-px-sds}

An SDS solution abstracts storage devices of various types, sizes, or from different vendors that are attached to the worker nodes in your cluster. Worker nodes with available storage on hard disks are added as a node to a storage cluster. In this cluster, the physical storage is virtualized and presented as a virtual storage pool to the user. The storage cluster is managed by the SDS software. If data must be stored on the storage cluster, the SDS software decides where to store the data for highest availability. Your virtual storage comes with a common set of capabilities and services that you can leverage without caring about the actual underlying storage architecture.

[Portworx](https://portworx.com/services/kubernetes-storage/){: external} is a highly available software-defined storage solution that you can use to manage local persistent storage for your containerized databases and other stateful apps, or to share data between pods across multiple zones.
{: shortdesc}

An software defined storage (SDS), such as Portworx, solution abstracts storage devices of various types, sizes, or from different vendors that are attached to the worker nodes in your cluster. Worker nodes with available storage on hard disks are added as a node to a storage cluster. In this cluster, the physical storage is virtualized and presented as a virtual storage pool to the user. The storage cluster is managed by the SDS software. If data must be stored on the storage cluster, the SDS software decides where to store the data for highest availability. Your virtual storage comes with a common set of capabilities and services that you can leverage without caring about the actual underlying storage architecture.


## What are the benefits of Portworx?
{: #portworx-benefits}

|Benefit|Description|
|-------------|------------------------------|
|Cloud native storage and data management for stateful apps|Portworx aggregates available local storage that is attached to your worker nodes and that can vary in size or type, and creates a unified persistent storage layer for containerized databases or other stateful apps that you want to run in the cluster. By using Kubernetes persistent volume claims (PVC), you can add local persistent storage to your apps to store your data.|
|Highly available data with volume replication|Portworx automatically replicates data in your volumes across worker nodes and zones in your cluster so that your data can always be accessed and that your stateful app can be rescheduled to another worker node in case of a worker node failure or reboot. |
|Support to run `hyper-converged`|Portworx can be configured to run [`hyper-converged`](https://docs.portworx.com/portworx-enterprise/concepts/kubernetes-storage-101/hyperconvergence){: external} to ensure that your compute resources and the storage are always placed onto the same worker node. When your app must be rescheduled, Portworx moves your app to a worker node where one of your volume replicas resides to ensure local-disk access speed and high performance for your stateful app. |
|Encrypt data with {{site.data.keyword.keymanagementservicelong_notm}}|You can [set up {{site.data.keyword.keymanagementservicelong_notm}} encryption keys](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-storage_portworx_encryption) that are secured by FIPS 140-2 Level 2 certified cloud-based hardware security modules (HSMs) to protect the data in your volumes. You can choose between using one encryption key to encrypt all your volumes in a cluster or using one encryption key for each volume. Portworx uses this key to encrypt data at rest and during transit when data is sent to a different worker node.|
|Built-in snapshots and cloud backups|You can save the current state of a volume and its data by creating a [Portworx snapshot](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/storage-operations/create-snapshots){: external}. Snapshots can be stored on your local Portworx cluster or in the cloud.|
|Integrated monitoring |You can view the health of your Portworx cluster, including the number of available storage nodes, volumes and available capacity, and analyze your data in Prometheus, Grafana, or Kibana.|
{: caption="Benefits of using Portworx" caption-side="bottom"}

## How does Portworx work?
{: #about-px-work}

As a software defined storage solution, Portworx aggregates available storage that is attached to your worker nodes and creates a unified persistent storage layer for containerized databases or other stateful apps that you want to run in the cluster. By using volume replication of each container-level volume across multiple worker nodes, Portworx ensures data persistence and data accessibility across zones.

Portworx also comes with additional features that you can use for your stateful apps, such as volume snapshots, volume encryption, isolation, and an integrated Storage Orchestrator for Kubernetes (Stork) to ensure optimal placement of volumes in the cluster. For more information, see the [Portworx documentation](https://docs.portworx.com/){: external}.

## What are the requirements to run Portworx?
{: #about-px-requirments}

Review the requirements to [install Portworx](https://docs.portworx.com/portworx-enterprise/platform/prerequisites){: external}.

For production environments, choose one of the [SDS worker node flavors](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-planning_worker_nodes#sds-table) for best performance. 
{: tip}

## How can I make sure that my data is stored highly available?
{: #about-px-ha}

You need at least three worker nodes in your Portworx cluster so that Portworx can replicate your data across nodes. By replicating your data across worker nodes, Portworx can ensure that your stateful app can be rescheduled to a different worker node in case of a failure without losing data. For even higher availability, use a [multizone cluster](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-ha_clusters#mz-clusters) and replicate your volumes across worker nodes in 3 or more zones.

## What volume topology offers the best performance for my pods?
{: #about-px-topology}

One of the biggest challenges when you run stateful apps in a cluster is to make sure that your container can be rescheduled onto another host if the container or the entire host fails. In Docker, when a container must be rescheduled onto a different host, the volume does not move to the new host. Portworx can be configured to run `hyper-converged` to ensure that your compute resources and the storage are always placed onto the same worker node. When your app must be rescheduled, Portworx moves your app to a worker node where one of your volume replicas resides to ensure local-disk access speed and best performance for your stateful app. Running `hyper-converged` offers the best performance for your pods, but requires storage to be available on all worker nodes in your cluster.

You can also choose to use only a subset of worker nodes for your Portworx storage layer. For example, you might have a worker pool with SDS worker nodes that come with local raw block storage, and another worker pool with virtual worker nodes that don't come with local storage. When you install Portworx, a Portworx pod is scheduled onto every worker node in your cluster as part of a DaemonSet. Because your SDS worker nodes have local storage, these worker nodes are into the Portworx storage layer only. Your virtual worker nodes are not included as a storage node because of the missing local storage. However, when you deploy an app pod to your virtual worker node, this pod can still access data that is physically stored on an SDS worker node by using the Portworx DaemonSet pod. This setup is referred to as `storage-heavy` and offers slightly slower performance than the `hyper-converged` setup because the virtual worker node must talk to the SDS worker node over the private network to access the data.

<containers>{{site.data.keyword.containerlong_notm}}</containers><openshift>{{site.data.keyword.openshiftlong_notm}}</openshift> does not support the [Portworx experimental `InitializerConfiguration` admission controller](https://github.com/libopenstorage/stork#initializer-experimental){: external}.
{: note}


## Can I install Portworx in a private cluster?
{: #about-px-private}

Yes. If you want to install Portworx in a private cluster, your {{site.data.keyword.cloud_notm}} account must be set up with [Virtual Routing and Forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint&interface=ui) and access to private cloud service endpoints for {{site.data.keyword.cloud_notm}} services. 

If you want to install Portworx in a cluster that doesn't have VRF or access to private cloud service endpoints (CSEs), you must create a rule in the default security group to allow inbound and outbound traffic for the following IP addresses: `166.9.24.81`, `166.9.22.100`, `166.9.20.178`. For more information, see [Updating the default security group](/docs/vpc?topic=vpc-updating-the-default-security-group#updating-the-default-security-group).
{: important}

## Can I install Autopilot while using Portworx?
{: #about-px-ap}

Yes. Autopilot can be installed by following the [Installing Autopilot documentation](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-storage-portworx-autopilot).

## How do I get support?
{: #portworx-billing-support}


Contact Portworx support by using one of the following methods.

- Sending an e-mail to `support@purestorage.com`.

- Calling `+1 (866) 244-7121` or `+1 (650) 729-4088` in the United States or one of the [International numbers](https://support.purestorage.com/bundle/m_contact_us/page/Pure_Storage_Technical_Services/Technical_Services_Information/topics/reference/r_contact_us.html).

- Opening an issue in the [Portworx Service Portal](https://support.purestorage.com/bundle/m_contact_us/page/Pure_Storage_Technical_Services/Technical_Services_Information/topics/reference/r_contact_us.html){: external}. If you don't have an account, see [Request access](https://purestorage.my.site.com/customers/CustomerAccessRequest){: external}.



## What's next?
{: #about-px-next}

All set? Let's start with [creating a cluster with an SDS worker pool of at least three worker nodes](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-clusters). If you want to include non-SDS worker nodes into your Portworx cluster, [add raw block storage](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-utilities#manual_block) to each worker node. After your cluster is prepared, [install Portworx](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-storage_portworx_deploy) in your cluster and create your first hyper-converged storage cluster.


## Exploring other Portworx features
{: #features}


Using existing Portworx volumes
:   If you have an existing Portworx volume that you created manually or that was not automatically deleted when you deleted the PVC, you can statically provision the corresponding PV and PVC and use this volume with your app. For more information, see [Using existing volumes](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/storage-operations/create-pvcs/using-preprovisioned-volumes){: external}.

Running stateful sets on Portworx
:   If you have a stateful app that you want to deploy as a stateful set into your cluster, you can set up your stateful set to use storage from your Portworx cluster. For more information, see [Create a MySQL StatefulSet](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/application-install-with-kubernetes/cassandra){: external}.

Running your pods hyperconverged
:   You can configure your Portworx cluster to schedule pods on the same worker node where the pod's volume resides. This setup is also referred to as `hyperconverged` and can improve the data storage performance. For more information, see [Run pods on same host as a volume](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/storage-operations/hyperconvergence){: external}.

Creating snapshots of your Portworx volumes
:   You can save the current state of a volume and its data by creating a Portworx snapshot. Snapshots can be stored on your local Portworx cluster or in the Cloud. For more information, see [Create and use local snapshots](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/application-install-with-kubernetes/cassandra/snapshots.html){: external}.

Monitoring and managing your Portworx cluster with Lighthouse
:   You can view the health of your Portworx cluster, including the number of available storage nodes, volumes and available capacity, and analyze your data in [Prometheus, Grafana, or Kibana](https://docs.portworx.com/portworx-enterprise/operations/operate-other/monitoring){: external}.

Configuring Autopilot 
:   You can monitor your cluster resources and specify conditions along with actions it should take when those conditions occur. For more information, refer to the [Autopilot docs](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/autopilot){: external}.

