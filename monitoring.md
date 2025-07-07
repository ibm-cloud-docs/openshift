---

copyright:
  years: 2024, 2025
lastupdated: "2025-07-07"

keywords: monitoring, openshift, observability, metrics

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Monitoring metrics for {{site.data.keyword.openshiftlong_notm}}
{: #monitoring}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.openshiftlong_notm}}, generate platform metrics that you can use to gain operational visibility into the performance and health of the service in your account.
{: shortdesc}

{{site.data.keyword.mon_full_notm}} is a third-party cloud-native, and container-intelligence management system that can be included as part of your {{site.data.keyword.cloud_notm}} architecture. It offers administrators, DevOps teams, and developers full-stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards. For more information, see [Monitoring in IBM Cloud](/docs/monitoring?topic=monitoring-about-monitor).

You can use {{site.data.keyword.metrics_router_full_notm}}, a platform service, to route platform metrics in your account to a destination of your choice by configuring targets and routes that define where platform metrics are sent. For more information, see [About {{site.data.keyword.metrics_router_full_notm}} in {{site.data.keyword.cloud_notm}}](/docs/metrics-router?topic=metrics-router-about).

You can use {{site.data.keyword.mon_full}} to visualize and alert on metrics that are generated in your account and routed by {{site.data.keyword.metrics_router_full_notm}} to an {{site.data.keyword.mon_full_notm}} instance.

## Locations where metrics are generated
{: #mon-locations}

{{site.data.keyword.openshiftlong_notm}} sends metrics in all supported regions.

## Enabling metrics for {{site.data.keyword.openshiftlong_notm}}
{: #monitoring-enable}

To enable monitoring for your cluster, connect your cluster to a monitoring service instance that exists in your IBM Cloud account. You can enable monitoring in existing clusters, or during cluster create time. The monitoring service instance must belong to the same IBM Cloud account where you created your cluster, but can be in a different resource group and IBM Cloud region than your cluster. 

Note that a cluster can only be connected to one monitoring service instance at a time. You can change which monitoring service instance a cluster is connected in to in the console by disconnecting the cluster from one instance and then connecting to a different instance. 
{: tip}

## Enable monitoring in an existing cluster
{: #monintoring-enable-existing}

1. If you do not already have a monitoring service instance in your account, [create one](/docs/monitoring?topic=monitoring-provision). 
2. In the console, navigate to the cluster resource page and click the relevant cluster. 
3. Under **Integrations**, find the monitoring option and click **Connect**. 
4. Select the monitoring service instance you want to connect to your cluster. If you have more than one monitoring service instance, you can filter them by the region they were created in. 
5. Click **Connect**. 

## Enable monitoring while creating a cluster
{: #monintoring-enable-create}

1. If you do not already have a monitoring service instance in your account, [create one](/docs/monitoring?topic=monitoring-provision). 
2. In the cluster create UI, configure you cluster as required.
3. In the **Observability integrations** section, enable the **Monitoring** option. 
4. Select the monitoring instance you want to connect to your cluster. If you do not have a monitoring instance in your account, or if you want to create a new monitoring instance, select **Create one**. 
5. Continue configuring the cluster. 

## Viewing metrics
{: #monitoring-view}

To view your metrics, navigate to your cluster resource page in the console and click the relevant cluster. In the **Integrations** section, find the **Monitoring** option and click **Launch**. A separate window opens where you can view your cluster metrics. 

### Launching {{site.data.keyword.mon_full}} from the Observability page
{: #monitoring-view-ob}

For more information about launching the {{site.data.keyword.mon_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.mon_full_notm}} documentation.](/docs/monitoring?topic=monitoring-launch)

## Monitoring {{site.data.keyword.openshiftlong_notm}}
{: #monitoring-monitor}

With {{site.data.keyword.mon_full_notm}}, you can collect cluster and pod metrics, such as the CPU and memory usage of your worker nodes, incoming and outgoing HTTP traffic for your pods, and data about several infrastructure components. For more information, see [Monitoring cluster health](/docs/openshift?topic=openshift-health-monitor).


## Migrating to the new monitoring agent
{: #migrating-new-agent}

The observability CLI plug-in `ibmcloud ob` and the `v2/observe` endpoints are no longer supported. You can now manage your logging and monitoring integrations from the console or through the Helm charts.
{: unsupported}

For more information, see the following links.
- [Working with the Kubernetes agent](/docs/monitoring?topic=monitoring-kubernetes_cluster).
- [Working with the Red Hat OpenShift agent](/docs/monitoring?topic=monitoring-openshift_cluster).
