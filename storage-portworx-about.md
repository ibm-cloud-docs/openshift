---

copyright: 
  years: 2014, 2026
lastupdated: "2026-04-07"


keywords: portworx, kubernetes, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# About Portworx
{: #storage_portworx_about}

Review frequently asked questions to learn more about Portworx and how Portworx provides highly available persistent storage management for your containerized apps.
{: shortdesc}

## What is software-defined storage (SDS)?
{: #about-px-sds}

An SDS solution abstracts storage devices that are attached to worker nodes in your cluster. These devices can vary in type, size, and vendor. Worker nodes with available hard-disk storage are added as nodes in a storage cluster. In this cluster, the physical storage is virtualized and presented as a virtual storage pool. The SDS software manages the storage cluster and decides where to store data for the highest availability. Your virtual storage includes a common set of capabilities and services, regardless of the underlying storage architecture.

[Portworx](https://portworx.com/products/portworx-enterprise){: external} is a highly available software-defined storage solution that you can use to manage local persistent storage for your containerized databases and other stateful apps, or to share data between pods across multiple zones.
{: shortdesc}


## What are the benefits of Portworx?
{: #portworx-benefits}

|Benefit|Description|
|-------------|------------------------------|
|Cloud native storage and data management for stateful apps|Portworx aggregates available local storage that is attached to your worker nodes and that can vary in size or type, and creates a unified persistent storage layer for containerized databases or other stateful apps that you want to run in the cluster. By using Kubernetes persistent volume claims (PVC), you can add local persistent storage to your apps to store your data.|
|Highly available data with volume replication|Portworx automatically replicates data in your volumes across worker nodes and zones in your cluster so that your data can always be accessed and that your stateful app can be rescheduled to another worker node in case of a worker node failure or reboot. |
|Support to run `hyper-converged`|Portworx can be configured to run [`hyper-converged`](https://docs.portworx.com/portworx-enterprise/concepts/kubernetes-storage-101/hyperconvergence){: external} to ensure that your compute resources and the storage are always placed onto the same worker node. When your app must be rescheduled, Portworx moves your app to a worker node where one of your volume replicas resides to ensure local-disk access speed and high performance for your stateful app. |
|Encrypt data with {{site.data.keyword.keymanagementservicelong_notm}}|You can [set up {{site.data.keyword.keymanagementservicelong_notm}} encryption keys](/docs/openshift?topic=openshift-storage_portworx_encryption) that are secured by FIPS 140-2 Level 2 certified cloud-based hardware security modules (HSMs) to protect the data in your volumes. You can choose between using one encryption key to encrypt all your volumes in a cluster or using one encryption key for each volume. Portworx uses this key to encrypt data at rest and during transit when data is sent to a different worker node.|
|Built-in snapshots and cloud backups|You can save the current state of a volume and its data by creating a [Portworx snapshot](https://docs.portworx.com/portworx-enterprise/operations/create-snapshots){: external}. Snapshots can be stored on your local Portworx cluster or in the cloud.|
|Integrated monitoring |You can view the health of your Portworx cluster, including the number of available storage nodes, volumes and available capacity, and analyze your data in Prometheus, Grafana, or Kibana.|
{: caption="Benefits of using Portworx" caption-side="bottom"}

## How does Portworx work?
{: #about-px-work}

As a software-defined storage solution, Portworx aggregates storage that is attached to your worker nodes and creates a unified persistent storage layer for your stateful apps. Portworx replicates each volume across multiple worker nodes to help ensure data persistence and accessibility across zones.

Portworx also includes features such as volume snapshots, volume encryption, isolation, and Storage Orchestrator for Kubernetes (Stork) to help optimize volume placement in the cluster. For more information, see the [Portworx documentation](https://docs.portworx.com/){: external}.

## What are the requirements to run Portworx?
{: #about-px-requirments}

Review the requirements to [install Portworx](https://docs.portworx.com/portworx-enterprise/platform/prerequisites){: external}.

For production environments, choose one of the [SDS worker node flavors](/docs/openshift?topic=openshift-classic-flavors) for best performance. In the tables for each metro area section, SDS flavors are in the **Bare Metal** tabs and end with `.ssd`.
{: tip}

## How can I make sure that my data is stored highly available?
{: #about-px-ha}

You need at least three worker nodes in your Portworx cluster so that Portworx can replicate your data across nodes. By replicating your data across worker nodes, Portworx can ensure that your stateful app can be rescheduled to a different worker node in case of a failure without losing data. For even higher availability, use a multizone cluster and replicate your volumes across worker nodes in 3 or more zones.

## What volume topology offers the best performance for my pods?
{: #about-px-topology}

One of the biggest challenges when you run stateful apps in a cluster is to make sure that your container can be rescheduled onto another host if the container or the entire host fails. In Docker, when a container must be rescheduled onto a different host, the volume does not move to the new host. Portworx can be configured to run `hyper-converged` to ensure that your compute resources and the storage are always placed onto the same worker node. When your app must be rescheduled, Portworx moves your app to a worker node where one of your volume replicas resides to ensure local-disk access speed and best performance for your stateful app. Running `hyper-converged` offers the best performance for your pods, but requires storage to be available on all worker nodes in your cluster.

You can also choose to use only a subset of worker nodes for your Portworx storage layer. For example, you might have a worker pool with SDS worker nodes that come with local raw block storage, and another worker pool with virtual worker nodes that don't come with local storage. When you install Portworx, a Portworx pod is scheduled onto every worker node in your cluster as part of a DaemonSet. Because your SDS worker nodes have local storage, these worker nodes are into the Portworx storage layer only. Your virtual worker nodes are not included as a storage node because of the missing local storage. However, when you deploy an app pod to your virtual worker node, this pod can still access data that is physically stored on an SDS worker node by using the Portworx DaemonSet pod. This setup is referred to as `storage-heavy` and offers slightly slower performance than the `hyper-converged` setup because the virtual worker node must talk to the SDS worker node over the private network to access the data.

{{site.data.keyword.openshiftlong_notm}} does not support the [Portworx experimental `InitializerConfiguration` admission controller](https://github.com/libopenstorage/stork#initializer-experimental){: external}.
{: note}


## Can I install Portworx in a private cluster?
{: #about-px-private}

Yes. If you want to install Portworx in a private cluster, your {{site.data.keyword.cloud_notm}} account must be set up with [Virtual Routing and Forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint&interface=ui) and access to private cloud service endpoints for {{site.data.keyword.cloud_notm}} services. 

If you want to install Portworx in a cluster that doesn't have VRF or access to private cloud service endpoints (CSEs), you must create a rule in the default security group to allow inbound and outbound traffic for the following IP addresses: `166.9.24.81`, `166.9.22.100`, `166.9.20.178`. For more information, see [Updating the default security group](/docs/vpc?topic=vpc-updating-the-default-security-group#updating-the-default-security-group).
{: important}

## Can I install Autopilot while using Portworx?
{: #about-px-ap}

Yes. Autopilot can be installed by following the [Installing Autopilot documentation](/docs/openshift?topic=openshift-storage-portworx-autopilot).

## How do I get support?
{: #portworx-billing-support}


Contact Portworx support by using one of the following methods.

- Sending an email to `support@purestorage.com`.

- Calling `+1 (866) 244-7121` or `+1 (650) 729-4088` in the United States or one of the [International numbers](https://support.purestorage.com/bundle/m_contact_us/page/Pure_Storage_Technical_Services/Technical_Services_Information/topics/reference/r_contact_us.html).

- Opening an issue in the [Portworx Service Portal](https://support.purestorage.com/bundle/m_contact_us/page/Pure_Storage_Technical_Services/Technical_Services_Information/topics/reference/r_contact_us.html){: external}. If you don't have an account, see [Request access](https://purestorage.my.site.com/customers/CustomerAccessRequest){: external}.



## Next steps
{: #about-px-next}

To get started, [create a cluster with an SDS worker pool of at least three worker nodes](/docs/openshift?topic=openshift-clusters). If you want to include non-SDS worker nodes in your Portworx cluster, [add raw block storage](/docs/openshift?topic=openshift-utilities#manual_block) to each worker node. After your cluster is prepared, [install Portworx](/docs/openshift?topic=openshift-storage_portworx_deploy) in your cluster and create your first hyper-converged storage cluster.

## Explore other Portworx features
{: #features}

Using existing Portworx volumes
:   If you have an existing Portworx volume that you created manually, or that was not automatically deleted when you deleted the PVC, you can statically provision the corresponding PV and PVC and use the volume with your app. For more information, see [Using existing volumes](https://docs.portworx.com/portworx-enterprise/provision-storage/create-pvcs/using-preprovisioned-volumes){: external}.

Running StatefulSets on Portworx
:   If you have a stateful app that you want to deploy as a StatefulSet in your cluster, you can configure it to use storage from your Portworx cluster. For more information, see [Create a MySQL StatefulSet](https://docs.portworx.com/portworx-enterprise/deploy-your-applications/application-install-with-kubernetes/cassandra){: external}.

Running your pods hyperconverged
:   You can configure your Portworx cluster to schedule pods on the same worker node where the pod volume resides. This setup is also referred to as `hyperconverged` and can improve storage performance. For more information, see [Run pods on same host as a volume](https://docs.portworx.com/portworx-enterprise/operations/tune-performance/hyperconvergence){: external}.

Creating snapshots of your Portworx volumes
:   You can save the current state of a volume and its data by creating a Portworx snapshot. Snapshots can be stored on your local Portworx cluster or in the cloud. For more information, see [Create and use local snapshots](https://docs.portworx.com/portworx-enterprise/deploy-your-applications/application-install-with-kubernetes/cassandra/snapshots){: external}.

Monitoring and managing your Portworx cluster with Lighthouse
:   You can view the health of your Portworx cluster, including the number of available storage nodes, volumes, and available capacity. You can also analyze your data in [Prometheus, Grafana, or Kibana](https://docs.portworx.com/portworx-enterprise/operations/observability){: external}.

Configuring Autopilot
:   You can monitor cluster resources and specify conditions and actions for Autopilot to take when those conditions occur. For more information, see the [Autopilot documentation](https://docs.portworx.com/portworx-enterprise/operations/scale-portworx-cluster/autopilot){: external}.
