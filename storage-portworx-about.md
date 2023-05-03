---

copyright: 
  years: 2014, 2023
lastupdated: "2023-05-03"

keywords: portworx, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# About Portworx
{: #storage_portworx_about}

Review frequently asked questions to learn more about Portworx and how Portworx provides highly available persistent storage management for your containerized apps.
{: shortdesc}

## What is software-defined storage (SDS)?
{: #about-px-sds}

An SDS solution abstracts storage devices of various types, sizes, or from different vendors that are attached to the worker nodes in your cluster. Worker nodes with available storage on hard disks are added as a node to a storage cluster. In this cluster, the physical storage is virtualized and presented as a virtual storage pool to the user. The storage cluster is managed by the SDS software. If data must be stored on the storage cluster, the SDS software decides where to store the data for highest availability. Your virtual storage comes with a common set of capabilities and services that you can leverage without caring about the actual underlying storage architecture.

### How does Portworx work?
{: #about-px-work}

Portworx aggregates available storage that is attached to your worker nodes and creates a unified persistent storage layer for containerized databases or other stateful apps that you want to run in the cluster. By using volume replication of each container-level volume across multiple worker nodes, Portworx ensures data persistence and data accessibility across zones.

Portworx also comes with additional features that you can use for your stateful apps, such as volume snapshots, volume encryption, isolation, and an integrated Storage Orchestrator for Kubernetes (Stork) to ensure optimal placement of volumes in the cluster. For more information, see the [Portworx documentation](https://docs.portworx.com/){: external}.

### What worker node flavor in {{site.data.keyword.openshiftlong_notm}} is the correct one for Portworx?
{: #about-px-flavors}

The worker node flavor that you need depends on the infrastructure provider that you use. If you have a classic cluster, {{site.data.keyword.openshiftlong_notm}} provides bare metal worker node flavors that are optimized for [software-defined storage (SDS) usage](/docs/openshift?topic=openshift-planning_worker_nodes#sds). These flavors also come with one or more raw, unformatted, and unmounted local disks that you can use for your Portworx storage layer. In classic clusters, Portworx offers the best performance when you use SDS worker node machines that come with 10 Gbps network speed.

In VPC clusters, make sure to select a [virtual server flavor](/docs/vpc?topic=vpc-profiles) that meets the [minimum hardware requirements for Portworx](https://docs.portworx.com/start-here-installation/){: external}. The flavor that you choose must have a network speed of 10 GBPS or more for optimal performance. None of the VPC flavors are set up with raw and unformatted block storage devices. To successfully install and run Portworx, you must [manually attach block storage devices](/docs/openshift?topic=openshift-utilities#vpc_api_attach) to each of your worker nodes first.

### What if I want to run Portworx in a classic cluster with non-SDS worker nodes?
{: #about-px-non-sds}

You can install Portworx on non-SDS worker node flavors, but you might not get the performance benefits that your app requires. Non-SDS worker nodes can be virtual or bare metal. If you want to use virtual machines, use a worker node flavor of `b3c.16x64` or better. Virtual machines with a flavor of `b3c.4x16` or `u3c.2x4` don't provide the required resources for Portworx to work properly. Bare metal machines come with sufficient compute resources and network speed for Portworx, but you must [add raw, unformatted, and unmounted block storage](#create_block_storage) before you can use these machines.

For classic clusters, virtual machines have only 1000 Mbps of networking speed, which is not sufficient to run production workloads with Portworx. Instead, provision Portworx on bare metal machines for the best performance.
{: important}

### How can I make sure that my data is stored highly available?
{: #about-px-ha}

You need at least three worker nodes in your Portworx cluster so that Portworx can replicate your data across nodes. By replicating your data across worker nodes, Portworx can ensure that your stateful app can be rescheduled to a different worker node in case of a failure without losing data. For even higher availability, use a [multizone cluster](/docs/openshift?topic=openshift-ha_clusters#mz-clusters) and replicate your volumes across worker nodes in 3 or more zones.

### What volume topology offers the best performance for my pods?
{: #about-px-topology}

One of the biggest challenges when you run stateful apps in a cluster is to make sure that your container can be rescheduled onto another host if the container or the entire host fails. In Docker, when a container must be rescheduled onto a different host, the volume does not move to the new host. Portworx can be configured to run `hyper-converged` to ensure that your compute resources and the storage are always placed onto the same worker node. When your app must be rescheduled, Portworx moves your app to a worker node where one of your volume replicas resides to ensure local-disk access speed and best performance for your stateful app. Running `hyper-converged` offers the best performance for your pods, but requires storage to be available on all worker nodes in your cluster.

You can also choose to use only a subset of worker nodes for your Portworx storage layer. For example, you might have a worker pool with SDS worker nodes that come with local raw block storage, and another worker pool with virtual worker nodes that don't come with local storage. When you install Portworx, a Portworx pod is scheduled onto every worker node in your cluster as part of a DaemonSet. Because your SDS worker nodes have local storage, these worker nodes are into the Portworx storage layer only. Your virtual worker nodes are not included as a storage node because of the missing local storage. However, when you deploy an app pod to your virtual worker node, this pod can still access data that is physically stored on an SDS worker node by using the Portworx DaemonSet pod. This setup is referred to as `storage-heavy` and offers slightly slower performance than the `hyper-converged` setup because the virtual worker node must talk to the SDS worker node over the private network to access the data.

{{site.data.keyword.openshiftlong_notm}} does not support the [Portworx experimental `InitializerConfiguration` admission controller](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/hyperconvergence/#initializer-experimental-feature-in-stork-v1-1){: external}.
{: note}


### Can I install Portworx in a private cluster?
{: #about-px-private}

Yes. If you want to install Portworx in a private cluster, your {{site.data.keyword.cloud_notm}} account must be set up with [Virtual Routing and Forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf) and access to private cloud service endpoints for {{site.data.keyword.cloud_notm}} services. 

If you want to install Portworx in a cluster that doesn't have VRF or access to private cloud service endpoints (CSEs), you must create a rule in the default security group to allow inbound and outbound traffic for the following IP addresses: `166.9.24.81`, `166.9.22.100`, `166.9.20.178`. For more information, see [Updating the default security group](/docs/vpc?topic=vpc-updating-the-default-security-group#updating-the-default-security-group).
{: important}


## What's next?
{: #about-px-next}

All set? Let's start with [creating a cluster with an SDS worker pool of at least three worker nodes](/docs/openshift?topic=openshift-clusters). If you want to include non-SDS worker nodes into your Portworx cluster, [add raw block storage](#create_block_storage) to each worker node. After your cluster is prepared, [install Portworx](#install_portworx) in your cluster and create your first hyper-converged storage cluster.




