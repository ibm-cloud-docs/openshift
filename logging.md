---

copyright:
  years: 2024, 2025
lastupdated: "2025-05-29"

keywords: logging, cloud logs, logs, log analysis, containers

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Logging for {{site.data.keyword.openshiftlong_notm}}
{: #logging}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.openshiftlong_notm}}, generate platform logs that you can use to investigate abnormal activity and critical actions in your account, and troubleshoot problems.
{: shortdesc}

You can use {{site.data.keyword.logs_routing_full_notm}}, a platform service, to route platform logs in your account to a destination of your choice by configuring a tenant that defines where platform logs are sent. For more information, see [About Logs Routing](/docs/logs-router?topic=logs-router-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on platform logs that are generated in your account and routed by {{site.data.keyword.logs_routing_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.


As of 28 March 2024, the {{site.data.keyword.la_full_notm}} service is deprecated and is no longer supported. Learn more about [{{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-about-cl). 
{: important}

## Locations where logs are generated
{: #log-locations}

{{site.data.keyword.openshiftlong_notm}} logs are generated in all regions. 

## Locations where logs are sent to {{site.data.keyword.logs_full_notm}}
{: #la-legacy-locations}

{{site.data.keyword.openshiftlong_notm}} sends logs to {{site.data.keyword.logs_full_notm}} in all regions. 

## Locations where logs are sent by {{site.data.keyword.logs_routing_full_notm}}
{: #lr-locations}

{{site.data.keyword.openshiftlong_notm}} sends logs by {{site.data.keyword.logs_routing_full_notm}} in all regions. 

## Logs that are generated
{: #log-platform}

Logs are generated and written locally for all the following {{site.data.keyword.openshiftlong_notm}} cluster components: worker nodes, containers, applications, persistent storage, Ingress application load balancer, Kubernetes API, and the `kube-system` namespace.

A logging agent collects logs with the extension `*.log` and extensionless files that are stored in the `/var/log/containers` directory of your pod from all namespaces, including `kube-system`. The agent then forwards the logs to your service instance. You can also track user-initiated administrative activity made in your cluster.  {{site.data.keyword.containershort_notm}} automatically generates cluster management events and forwards these event logs to {{site.data.keyword.logs_full_notm}}. For more information, see [Getting started with {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-getting-started).

To deploy a logging agent to your cluster, see [Deploying the Logging agent for OpenShift clusters using a Helm chart](/docs/cloud-logs?topic=cloud-logs-agent-helm-os-deploy) or [Deploying the Logging agent for Kubernetes clusters using a Helm chart](/docs/cloud-logs?topic=cloud-logs-agent-helm-kube-deploy).

## Enabling logging
{: #log-enable}

To enable logging for your cluster, connect your cluster to a logging service instance that exists in your IBM Cloud account. You can enable logging in existing clusters, or during cluster create time. The logging service instance must belong to the same IBM Cloud account where you created your cluster, but can be in a different resource group and IBM Cloud region than your cluster. 

Note that a cluster can only be connected to one logging service instance at a time. You can change which logging service instance a cluster is connected in to in the console by disconnecting the cluster from one instance and then connecting to a different instance. 
{: tip}
 
## Enable logging in an existing cluster
{: #log-enable-existing}

1. If you do not already have a logging service instance in your account, [create one](/docs/cloud-logs?topic=cloud-logs-instance-provision&interface=ui).
2. In the console, navigate to the cluster resource page and click the relevant cluster. 
3. Under **Integrations**, find the logging option and click **Connect**. 
4. Select the logging service instance you want to connect to your cluster. If you have more than one logging service instance, you can filter them by the region they were created in. 
5. Click **Connect**. 

## Enable logging while creating a cluster
{: #log-enable-create}

1. If you do not already have a logging service instance in your account, [create one](/docs/cloud-logs?topic=cloud-logs-instance-provision&interface=ui).
2. In the cluster create UI, configure you cluster as required.
3. In the **Observability integrations** section, enable the **Logging** option. 
4. Select the instance you want to connect to your cluster. 
5. Continue configuring the cluster. 

## Viewing logs
{: #log-viewing}

To view your logs, navigate to your cluster resource page in the console and click the relevant cluster. In the **Integrations** section, find the **Logging** option and click **Launch**. A separate window opens where you can view your cluster logs. 

## Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone-ob}



For more information about launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

## Fields by log type
{: #log-fields}



For information about fields included in every platform log, see [Fields for platform logs](/docs/logs-router?topic=logs-router-about-platform-logs#about-platform-logs-2). 





| Field             | Type       | Description             |
|-------------------|------------|-------------------------|
| `logSourceCRN`    | Required   | Defines the account and flow log instance where the log is published. |
| `saveServiceCopy` | Required   | Defines whether IBM saves a copy of the record for operational purposes. |
{: caption="Log record fields" caption-side="bottom"}






## Line identifiers by type
{: #line-indentifiers}

| Identifier | Description      |
|------------|------------------|
| `Source` | The service the logs are sent from. |
| `App` | The CRN of the component or service that sent the log. |
{: caption="Log record fields" caption-side="bottom"}


## Analyzing {{site.data.keyword.openshiftlong_notm}} logs
{: #cloud-logs}

You can view your logs to view details on events that affect your cluster components. For example, if a pod fails, you can view your logs in the dashboard to see related error messages. 
