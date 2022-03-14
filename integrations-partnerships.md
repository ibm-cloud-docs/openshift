---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-14"

keywords: kubernetes, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.openshiftlong_notm}} partners
{: #service-partners}

IBM is dedicated to make {{site.data.keyword.openshiftlong}} the best {{site.data.keyword.redhat_openshift_notm}} service that helps you migrate, operate, and administer your containerized workloads. To provide you with all the capabilities that you need to run production workloads in the cloud, {{site.data.keyword.openshiftlong_notm}} partners with other third-party service providers to enhance your cluster with top-notch logging, monitoring, and storage tools.
{: shortdesc}

Review our partners and the benefits of each solution that they provide. To find other proprietary {{site.data.keyword.cloud_notm}} and third-party open source services that you can use in your cluster, see [Understanding {{site.data.keyword.cloud_notm}} and 3rd party integrations](/docs/containers?topic=containers-ibm-3rd-party-integrations).

## Portworx
{: #portworx-parter}

[Portworx ![External link icon](../icons/launch-glyph.svg "External link icon")](https://portworx.com/products/portworx-enterprise//) is a highly available software-defined storage solution that you can use to manage local persistent storage for your containerized databases and other stateful apps, or to share data between pods across multiple zones.
{: shortdesc}

**What is software-defined storage (SDS)?**

An SDS solution abstracts storage devices of various types, sizes, or from different vendors that are attached to the worker nodes in your cluster. Worker nodes with available storage on hard disks are added as a node to a storage cluster. In this cluster, the physical storage is virtualized and presented as a virtual storage pool to the user. The storage cluster is managed by the SDS software. If data must be stored on the storage cluster, the SDS software decides where to store the data for highest availability. Your virtual storage comes with a common set of capabilities and services that you can leverage without caring about the actual underlying storage architecture.

### Benefits
{: #portworx-benefits}

Review the following table to find a list of key benefits that you can get by using Portworx.
{: shortdesc}

|Benefit|Description|
|-------------|------------------------------|
|Cloud native storage and data management for stateful apps|Portworx aggregates available local storage that is attached to your worker nodes and that can vary in size or type, and creates a unified persistent storage layer for containerized databases or other stateful apps that you want to run in the cluster. By using Kubernetes persistent volume claims (PVC), you can add local persistent storage to your apps to store your data.|
|Highly available data with volume replication|Portworx automatically replicates data in your volumes across worker nodes and zones in your cluster so that your data can always be accessed and that your stateful app can be rescheduled to another worker node in case of a worker node failure or reboot. |
|Support to run `hyper-converged`|Portworx can be configured to run [`hyper-converged` ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/hyperconvergence/) to ensure that your compute resources and the storage are always placed onto the same worker node. When your app must be rescheduled, Portworx moves your app to a worker node where one of your volume replicas resides to ensure local-disk access speed and high performance for your stateful app. |
|Encrypt data with {{site.data.keyword.keymanagementservicelong_notm}}|You can [set up {{site.data.keyword.keymanagementservicelong_notm}} encryption keys](/docs/openshift?topic=openshift-portworx#encrypt_volumes) that are secured by FIPS 140-2 Level 2 certified cloud-based hardware security modules (HSMs) to protect the data in your volumes. You can choose between using one encryption key to encrypt all your volumes in a cluster or using one encryption key for each volume. Portworx uses this key to encrypt data at rest and during transit when data is sent to a different worker node.|
|Built-in snapshots and cloud backups|You can save the current state of a volume and its data by creating a [Portworx snapshot ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/create-snapshots/). Snapshots can be stored on your local Portworx cluster or in the cloud.|
|Integrated monitoring with Lighthouse|[Lighthouse ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.portworx.com/reference/lighthouse/) is an intuitive, graphical tool to help you manage and monitor your Portworx clusters and volume snapshots. With Lighthouse, you can view the health of your Portworx cluster, including the number of available storage nodes, volumes and available capacity, and analyze your data in Prometheus, Grafana, or Kibana.|
{: caption="Benefits of using Portworx" caption-side="top"}

### Integration with {{site.data.keyword.openshiftlong_notm}}
{: #portworx-integration}

If you have a classic {{site.data.keyword.openshiftlong_notm}} cluster, you can choose worker node flavors that are optimized for SDS usage and that come with one or more raw, unformatted, and unmounted local disks that you can use to store your data. Portworx offers best performance when you use [SDS worker node machines](/docs/openshift?topic=openshift-planning_worker_nodes#sds) that come with 10Gbps network speed. However, you can install Portworx on non-SDS worker node flavors in classic clusters, but you might not get the performance benefits that your app requires.
{: shortdesc}

Portworx is installed by using a [Helm chart](/docs/openshift?topic=openshift-portworx#install_portworx). When you install the Helm chart, Portworx automatically analyzes the local persistent storage that is available in your cluster and adds the storage to the Portworx storage layer. To add storage from your Portworx storage layer to your apps, you must use [Kubernetes persistent volume claims](/docs/openshift?topic=openshift-portworx#add_portworx_storage).

For more information about how to install and use Portworx with {{site.data.keyword.openshiftlong_notm}}, see [Storing data on software-defined storage (SDS) with Portworx](/docs/containers?topic=containers-portworx).

### Billing and support
{: #portworx-billing-support}

Classic SDS worker node machines that come with local disks, and classic virtual machines that you use for Portworx are in your monthly {{site.data.keyword.openshiftlong_notm}} bill. For pricing information, see the [{{site.data.keyword.cloud_notm}} catalog ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/catalog/about). The Portworx license is a separate cost and is not included in your monthly bill.
{: shortdesc}

If you run into an issue with using Portworx, you can open an issue in the [Portworx Service Portal](https://pure1.purestorage.com/support){: external}. You can also submit a request by sending an e-mail to `support@purestorage.com`. If you don't have an account on the Portworx Service Portal, send an e-mail to `support@purestorage.com` or see [requeset access](https://purestorage.force.com/customers/CustomerAccessRequest){: external}. You can also [gather logging information](/docs/openshift?topic=openshift-portworx#portworx_logs) before opening a support ticket.




