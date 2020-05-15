---

copyright:
  years: 2014, 2020
lastupdated: "2020-05-15"

keywords: kubernetes, openshift, roks, rhoks, rhos

subcollection: openshift

---

{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}


# Red Hat OpenShift on IBM Cloud partners
{: #service-partners}

IBM is dedicated to make {{site.data.keyword.openshiftlong}} the best OpenShift service that helps you migrate, operate, and administer your containerized workloads. To provide you with all the capabilities that you need to run production workloads in the cloud, Red Hat OpenShift on IBM Cloud partners with other third-party service providers to enhance your cluster with top-notch logging, monitoring, and storage tools.
{: shortdesc}

Review our partners and the benefits of each solution that they provide. To find other proprietary {{site.data.keyword.cloud_notm}} and third-party open source services that you can use in your cluster, see [Understanding {{site.data.keyword.cloud_notm}} and 3rd party integrations](/docs/openshift?topic=openshift-ibm-3rd-party-integrations).

## LogDNA
{: #logdna-partner}

{{site.data.keyword.la_full_notm}} provides [LogDNA ![External link icon](../icons/launch-glyph.svg "External link icon")](https://logdna.com/) as a third-party service that you can use to add intelligent logging capabilities to your cluster and apps.

### Benefits
{: #logdna-benefits}

Review the following table to find a list of key benefits that you can get by using LogDNA.
{: shortdesc}

|Benefit|Description|
|-------------|------------------------------|
|Centralized log management and log analysis|When you configure your cluster as a log source, LogDNA automatically starts collecting logging information for your worker nodes, pods, apps, and network. Your logs are automatically parsed, indexed, tagged, and aggregated by LogDNA and visualized in the LogDNA dashboard so that you can easily dive into your cluster resources. You can use the built-in graphing tool to visualize most common error codes or log entries. |
|Easy findability with Google-like search syntax|LogDNA uses Google-like search syntax that supports standard terms, `AND` and `OR` operations, and lets you exclude or combine search terms to help you find your logs more easily. With smart indexing of logs, you can jump to a specific log entry in any moment in time. |
|Encryption in transit and at rest|LogDNA automatically encrypts your logs to secure your logs during transit and at rest. |
|Custom alerts and log views|You can use the dashboard to find the logs that match your search criteria, save these logs in a view, and share this view with other users to simplify debugging across team members. You can also use this view to create an alert that you can send to downstream systems, like PagerDuty, Slack, or email.   |
|Out-of-the-box and custom dashboards|You can choose between a variety of existing dashboards or create your own dashboard to visualize logs in the way you need it. |

### Integration with Red Hat OpenShift on IBM Cloud
{: #logdna-integration}

LogDNA is provided by {{site.data.keyword.la_full_notm}}, an {{site.data.keyword.cloud_notm}} platform service that you can use with your cluster. {{site.data.keyword.la_full_notm}} is operated by LogDNA in partnership with IBM.
{: shortdesc}

To use LogDNA in your cluster, you must provision an instance of {{site.data.keyword.la_full_notm}} in your {{site.data.keyword.cloud_notm}} account and configure your Kubernetes clusters as a log source. After the cluster is configured, logs are automatically collected and forwarded to your {{site.data.keyword.la_full_notm}} service instance. You can use the {{site.data.keyword.la_full_notm}} dashboard to access your logs.

For more information, see [Managing Kubernetes cluster logs with {{site.data.keyword.la_full_notm}}](/docs/Log-Analysis-with-LogDNA?topic=LogDNA-kube).

### Billing and support
{: #logdna-billing-support}

{{site.data.keyword.la_full_notm}} is fully integrated into the {{site.data.keyword.cloud_notm}} support system. If you run into an issue with using {{site.data.keyword.la_full_notm}}, post a question in the `logdna-on-iks` channel in the [Red Hat OpenShift on IBM Cloud Slack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://ibm-cloud-success.slack.com/), or open an [{{site.data.keyword.cloud_notm}} support case](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support). Log in to Slack by using your IBMid. If you do not use an IBMid for your {{site.data.keyword.cloud_notm}} account, [request an invitation to this Slack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/slack).

## Sysdig
{: #sydig-partner}

{{site.data.keyword.mon_full_notm}} provides [Sysdig Monitor ![External link icon](../icons/launch-glyph.svg "External link icon")](https://sysdig.com/products/monitor/) as a third-party, cloud-native container analytics system that you can use to gain insight into the performance and health of your compute hosts, apps, containers, and networks.
{: shortdesc}

### Benefits
{: #sydig-benefits}

Review the following table to find a list of key benefits that you can get by using Sysdig.
{: shortdesc}

|Benefit|Description|
|-------------|------------------------------|
|Automatic access to cloud-native and Prometheus-custom metrics|Choose from a variety of pre-defined cloud-native and Prometheus-custom metrics to gain insight into the performance and health of your compute hosts, apps, containers, and networks.|
|Troubleshoot with advanced filters|Sysdig Monitor creates network topologies that show how your worker nodes are connected and how your Kubernetes services communicate with each other. You can navigate from your worker nodes to containers and single system calls, and group and view important metrics for each resource along the way. For example, use these metrics to find services that receive most requests, or services with slow queries and response times. You can combine this data with Kubernetes events, custom CI/CD events, or code commits.
|Automatic anomaly detection and custom alerts|Define rules and thresholds for when you want to get notified to detect anomalies in your cluster or group resources to let Sysdig notify you when one resource acts differently than the rest. You can send these alerts to downstream tools, such as ServiceNow, PagerDuty, Slack, VictorOps, or email.|
|Out-of-the-box and custom dashboards|You can choose between a variety of existing dashboards or create your own dashboard to visualize metrics of your microservices in the way you need it. |
{: caption="Benefits of using Sysdig Monitor" caption-side="top"}

### Integration with Red Hat OpenShift on IBM Cloud
{: #sysdig-integration}

Sysdig Monitor is provided by {{site.data.keyword.mon_full_notm}}, an {{site.data.keyword.cloud_notm}} platform service that you can use with your cluster. {{site.data.keyword.mon_full_notm}} is operated by Sysdig in partnership with IBM.
{: shortdesc}

To use Sysdig Monitor in your cluster, you must provision an instance of {{site.data.keyword.mon_full_notm}} in your {{site.data.keyword.cloud_notm}} account and configure your cluster as a metrics source. After the cluster is configured, metrics are automatically collected and forwarded to your {{site.data.keyword.mon_full_notm}} service instance. You can use the {{site.data.keyword.mon_full_notm}} dashboard to access your metrics.

For more information, see [Analyze metrics for an app that is deployed in a Kubernetes cluster](/docs/Monitoring-with-Sysdig?topic=Sysdig-kubernetes_cluster).

### Billing and support
{: #sysdig-billing-support}

Because Sysdig Monitor is provided by {{site.data.keyword.mon_full_notm}}, your usage is included in the {{site.data.keyword.cloud_notm}} bill for platform services. For pricing information, review available plans in the [{{site.data.keyword.cloud_notm}} catalog ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/observe/monitoring/create).

{{site.data.keyword.mon_full_notm}} is fully integrated into the {{site.data.keyword.cloud_notm}} support system. If you run into an issue with using {{site.data.keyword.mon_full_notm}}, post a question in the `sysdig-monitoring` channel in the [Red Hat OpenShift on IBM Cloud Slack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://ibm-cloud-success.slack.com/), or open an [{{site.data.keyword.cloud_notm}} support case](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support). Log in to Slack by using your IBMid. If you do not use an IBMid for your {{site.data.keyword.cloud_notm}} account, [request an invitation to this Slack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/slack).

## Portworx
{: #portworx-parter}

[Portworx ![External link icon](../icons/launch-glyph.svg "External link icon")](https://portworx.com/products/portworx-enterprise//) is a highly available software-defined storage solution that you can use to manage local persistent storage for your containerized databases and other stateful apps, or to share data between pods across multiple zones.
{: shortdesc}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> Portworx is supported only in clusters that run version 3.11, and not available in version 4.3.
{: important}

**What is software-defined storage (SDS)?** </br>
An SDS solution abstracts storage devices of various types, sizes, or from different vendors that are attached to the worker nodes in your cluster. Worker nodes with available storage on hard disks are added as a node to a storage cluster. In this cluster, the physical storage is virtualized and presented as a virtual storage pool to the user. The storage cluster is managed by the SDS software. If data must be stored on the storage cluster, the SDS software decides where to store the data for highest availability. Your virtual storage comes with a common set of capabilities and services that you can leverage without caring about the actual underlying storage architecture.

### Benefits
{: #portworx-benefits}

Review the following table to find a list of key benefits that you can get by using Portworx.
{: shortdesc}

|Benefit|Description|
|-------------|------------------------------|
|Cloud native storage and data management for stateful apps|Portworx aggregates available local storage that is attached to your worker nodes and that can vary in size or type, and creates a unified persistent storage layer for containerized databases or other stateful apps that you want to run in the cluster. By using Kubernetes persistent volume claims (PVC), you can add local persistent storage to your apps to store your data.|
|Highly available data with volume replication|Portworx automatically replicates data in your volumes across worker nodes and zones in your cluster so that your data can be accessed at all times and that your stateful app can be rescheduled to another worker node in case of a worker node failure or reboot. |
|Support to run `hyper-converged`|Portworx can be configured to run [`hyper-converged` ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/hyperconvergence/) to ensure that your compute resources and the storage are always placed onto the same worker node. When your app must be rescheduled, Portworx moves your app to a worker node where one of your volume replicas resides to ensure local-disk access speed and high performance for your stateful app. |
|Encrypt data with {{site.data.keyword.keymanagementservicelong_notm}}|You can [set up {{site.data.keyword.keymanagementservicelong_notm}} encryption keys](/docs/openshift?topic=openshift-portworx#encrypt_volumes) that are secured by FIPS 140-2 Level 2 certified cloud-based hardware security modules (HSMs) to protect the data in your volumes. You can choose between using one encryption key to encrypt all your volumes in a cluster or using one encryption key for each volume. Portworx uses this key to encrypt data at rest and during transit when data is sent to a different worker node.|
|Built-in snapshots and cloud backups|You can save the current state of a volume and its data by creating a [Portworx snapshot ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/create-snapshots/). Snapshots can be stored on your local Portworx cluster or in the cloud.|
|Integrated monitoring with Lighthouse|[Lighthouse ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.portworx.com/reference/lighthouse/) is an intuitive, graphical tool to help you manage and monitor your Portworx clusters and volume snapshots. With Lighthouse, you can view the health of your Portworx cluster, including the number of available storage nodes, volumes and available capacity, and analyze your data in Prometheus, Grafana, or Kibana.|
{: caption="Benefits of using Portworx" caption-side="top"}

### Integration with Red Hat OpenShift on IBM Cloud
{: #portworx-integration}

If you have a classic Red Hat OpenShift on IBM Cloud cluster, you can choose worker node flavors that are optimized for SDS usage and that come with one or more raw, unformatted, and unmounted local disks that you can use to store your data. Portworx offers best performance when you use [SDS worker node machines](/docs/openshift?topic=openshift-planning_worker_nodes#sds) that come with 10Gbps network speed. However, you can install Portworx on non-SDS worker node flavors in classic clusters, but you might not get the performance benefits that your app requires.
{: shortdesc}

Portworx is installed by using a [Helm chart](/docs/openshift?topic=openshift-portworx#install_portworx). When you install the Helm chart, Portworx automatically analyzes the local persistent storage that is available in your cluster and adds the storage to the Portworx storage layer. To add storage from your Portworx storage layer to your apps, you must use [Kubernetes persistent volume claims](/docs/openshift?topic=openshift-portworx#add_portworx_storage).

For more information about how to install and use Portworx with Red Hat OpenShift on IBM Cloud, see [Storing data on software-defined storage (SDS) with Portworx](/docs/openshift?topic=openshift-portworx).

### Billing and support
{: #portworx-billing-support}

Classic SDS worker node machines that come with local disks, and classic virtual machines that you use for Portworx are included in your monthly Red Hat OpenShift on IBM Cloud bill. For pricing information, see the [{{site.data.keyword.cloud_notm}} catalog ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/catalog/about). The Portworx license is a separate cost and is not included in your monthly bill.
{: shortdesc}

If you run into an issue with using Portworx or you want to chat about Portworx configurations for your specific use case, post a question in the `portworx-on-iks` channel in the [Red Hat OpenShift on IBM Cloud Slack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://ibm-cloud-success.slack.com/). Log in to Slack by using your IBMid. If you do not use an IBMid for your {{site.data.keyword.cloud_notm}} account, [request an invitation to this Slack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/slack).


