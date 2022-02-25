---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-25"

keywords: openshift, disaster recovery, dr, ha, hadr

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Understanding high availability and disaster recovery for {{site.data.keyword.openshiftlong_notm}}
{: #ha}

Use the built-in {{site.data.keyword.openshiftshort}}, Kubernetes, and {{site.data.keyword.cloud}} features to make your {{site.data.keyword.openshiftshort}} cluster more highly available and to protect your app from downtime when a component in your cluster fails.
{: shortdesc}


## About high availability
{: #ha-about}

High availability (HA) is a core discipline in an IT infrastructure to keep your apps up and running, even after a partial or full site failure. The main purpose of high availability is to eliminate potential points of failures in an IT infrastructure. For example, you can prepare for the failure of one system by adding redundancy and setting up failover mechanisms.
{: shortdesc}

**What level of availability do I need?**

You can achieve high availability on different levels in your IT infrastructure and within different components of your cluster. The level of availability that is right for you depends on several factors, such as your business requirements, the Service Level Agreements that you have with your customers, and the resources that you want to expend.

**What level of availability does {{site.data.keyword.cloud_notm}} offer?**

See [How {{site.data.keyword.cloud_notm}} ensures high availability and disaster recovery](/docs/overview?topic=overview-zero-downtime).

The level of availability that you set up for your cluster impacts your coverage under the [{{site.data.keyword.cloud_notm}} HA service level agreement terms](/docs/overview?topic=overview-slas). For example, to receive full HA coverage under the SLA terms, you must set up a multizone cluster with a total of at least 6 worker nodes, two worker nodes per zone that are evenly spread across three zones.

**What other cluster components can I set up in highly available architecture?**

See [Overview of potential points of failure in {{site.data.keyword.openshiftlong_notm}}](#fault_domains).

**Where is the service located?**

See [Locations](/docs/openshift?topic=openshift-regions-and-zones#regions-and-zones).

**What am I responsible to configure disaster recovery options for?**

See [Your responsibilities with using {{site.data.keyword.openshiftlong_notm}}](/docs/containers?topic=containers-responsibilities_iks).

## Overview of potential points of failure in {{site.data.keyword.openshiftlong_notm}}
{: #fault_domains}

The {{site.data.keyword.openshiftlong_notm}} architecture and infrastructure is designed to ensure reliability, low processing latency, and a maximum uptime of the service. However, failures can happen. Depending on the service that you host in {{site.data.keyword.cloud_notm}}, you might not be able to tolerate failures, even if failures last for only a few minutes.
{: shortdesc}

{{site.data.keyword.openshiftlong_notm}} provides several approaches to add more availability to your cluster by adding redundancy and anti-affinity. Review the following image to learn about potential points of failure and how to eliminate them.

![Overview of fault domains in a high availability cluster within an {{site.data.keyword.cloud_notm}} region.](images/cs_failure_ov.png){: caption="Figure 1. Overview of fault domains in a high availability cluster" caption-side="bottom"}


### 1. Container or pod availability
{: #ha-container}

Containers and pods are, by design, short-lived and can fail unexpectedly. For example, a container or pod might crash if an error occurs in your app. To make your app highly available, you must ensure that you have enough instances of your app to handle the workload plus additional instances in the case of a failure. Ideally, these instances are distributed across multiple worker nodes to protect your app from a worker node failure.
{: shortdesc}

See [Deploying highly available apps](/docs/openshift?topic=openshift-plan_deploy#highly_available_apps).

### 2. Worker node availability
{: #ha-worker}

A worker node is a VM that runs on top of physical hardware. Worker node failures include hardware outages, such as power, cooling, or networking, and issues on the VM itself. You can account for a worker node failure by setting up multiple worker nodes in your cluster.
{: shortdesc}

See [Creating clusters with multiple worker nodes](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_create).

Worker nodes in one zone are not guaranteed to be on separate physical compute hosts. For example, you might have a cluster with three worker nodes, but all three worker nodes were created on the same physical compute host in the IBM zone. If this physical compute host goes down, all your worker nodes are down. To protect against this failure, you must [set up a multizone cluster to spread worker nodes across three zones, or create multiple single zone clusters](/docs/openshift?topic=openshift-ha_clusters#ha_clusters) in different zones.
{: note}

### 3. Cluster availability
{: #ha-cluster}

The [{{site.data.keyword.openshiftshort}} master](/docs/openshift?topic=openshift-service-architecture) is the main component that keeps your cluster up and running. The master stores cluster resources and their configurations in the etcd database that serves as the single point of truth for your cluster. The {{site.data.keyword.openshiftshort}} API server is the main entry point for all cluster management requests from the worker nodes to the master, or when you want to interact with your cluster resources.

If a master failure occurs, your workloads continue to run on the worker nodes, but you can't use `oc` commands to work with your cluster resources or view the cluster health until the {{site.data.keyword.openshiftshort}} API server in the master is back up. If a pod goes down during the master outage, the pod can't be rescheduled until the worker node can reach the {{site.data.keyword.openshiftshort}} API server again.

During a master outage, you can still run `ibmcloud oc` commands against the {{site.data.keyword.containerlong_notm}} API to work with your infrastructure resources, such as worker nodes or VLANs. If you change the current cluster configuration by adding or removing worker nodes to the cluster, your changes don't happen until the master is back up.

Do not restart or reboot a worker node during a master outage. This action removes the pods from your worker node. Because the Kubernetes API server is unavailable, the pods can't be rescheduled onto other worker nodes in the cluster.
{: important}
{: shortdesc}

The cluster masters are highly available and include replicas for your Kubernetes API server, etcd, scheduler, and controller manager on separate hosts to protect against an outage such as during a master update.

To protect your cluster master from a zone failure, you can:
* Create a cluster in a [classic](/docs/openshift?topic=openshift-regions-and-zones#zones-mz) or [VPC](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc) multizone location, which spreads the master across zones.
* Set up a second cluster in another zone.

See [Setting up highly available clusters](/docs/openshift?topic=openshift-ha_clusters#ha_clusters).

### 4. Zone availability
{: #ha-zone}

A zone failure affects all physical compute hosts and NFS storage. Failures include power, cooling, networking, or storage outages, and natural disasters, like flooding, earthquakes, and hurricanes. To protect against a zone failure, you must have clusters in two different zones that are load balanced by an external load balancer.
{: shortdesc}

See [Setting up highly available clusters](/docs/openshift?topic=openshift-ha_clusters#ha_clusters).

### 5. Region availability
{: #ha-region}

Every region is set up with a highly available load balancer that is accessible from the region-specific API endpoint. The load balancer routes incoming and outgoing requests to clusters in the regional zones. The likelihood of a full regional failure is low. However, to account for this failure, you can set up multiple clusters in different regions and connect them by using an external load balancer. If an entire region fails, the cluster in the other region can take over the work load.

See [Setting up highly available clusters](/docs/openshift?topic=openshift-ha_clusters#ha_clusters).

A multi-region cluster requires several Cloud resources, and depending on your app, can be complex and expensive. Check whether you need a multi-region setup or if you can accommodate a potential service disruption. If you want to set up a multi-region cluster, ensure that your app and the data can be hosted in another region, and that your app can handle global data replication.
{: note}

### 6. Storage availability
{: #ha-storage}

In a stateful app, data plays an important role to keep your app up and running. Make sure that your data is highly available so that you can recover from a potential failure. In {{site.data.keyword.openshiftlong_notm}}, you can choose from several options to persist your data. For example, you can provision NFS storage by using Kubernetes native persistent volumes, or store your data by using an {{site.data.keyword.cloud_notm}} database service.
{: shortdesc}

See [Planning highly available data](/docs/openshift?topic=openshift-storage_planning#persistent_storage_overview).




