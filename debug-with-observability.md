---

copyright:
  years: 2026
lastupdated: "2026-09-17"

keywords: monitoring, logging, sysdig, cloud logs, debug, troubleshoot, observability, cluster health, dashboards

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Using {{site.data.keyword.mon_full_notm}} and {{site.data.keyword.logs_full_notm}} to debug your cluster
{: #debug-with-observability}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

Use the built-in dashboards and queries in {{site.data.keyword.mon_full_notm}} and {{site.data.keyword.logs_full_notm}} to investigate and diagnose cluster problems without needing direct `oc` access to each node or pod.
{: shortdesc}

Many troubleshooting guides in this documentation direct you to run `oc` commands to gather data manually. If your cluster is connected to {{site.data.keyword.mon_full_notm}} or {{site.data.keyword.logs_full_notm}}, you can often find the same information — and additional historical context — directly in those services' dashboards. This approach is especially useful when a worker node is unreachable or when you want to review events that occurred in the past.

## Before you begin
{: #debug-observability-prereqs}

Before you can use the observability services to debug your cluster, ensure that the following requirements are met.

- Your cluster is connected to an {{site.data.keyword.mon_full_notm}} instance. To connect your cluster, see [Enabling metrics for {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-monitoring#monitoring-enable).
- Your cluster is connected to an {{site.data.keyword.logs_full_notm}} instance. To connect your cluster, see [Enabling logging](/docs/openshift?topic=openshift-logging#log-enable).
- You have at least **Viewer** access to the {{site.data.keyword.mon_full_notm}} and {{site.data.keyword.logs_full_notm}} service instances in your account.

## Check worker node resource usage with {{site.data.keyword.mon_full_notm}}
{: #debug-observability-nodes}

When worker nodes enter a `Critical` or `NotReady` state, high CPU or memory usage is a common cause. Use the {{site.data.keyword.mon_full_notm}} pre-built dashboards to identify resource pressure quickly.

1. Open the {{site.data.keyword.mon_full_notm}} dashboard for your cluster.
   1. In the {{site.data.keyword.cloud_notm}} console, navigate to your cluster resource page and click the relevant cluster.
   1. Under **Integrations**, find the **Monitoring** option and click **Launch**. The {{site.data.keyword.mon_full_notm}} UI opens in a new window.

1. Navigate to the **Kubernetes** > **Nodes** pre-built dashboard to view per-node CPU and memory usage.
   - Look for nodes where **CPU %** or **Memory %** exceeds 80%. Nodes at or above this threshold are at risk of becoming overloaded and may start failing to schedule new pods.
   - Look for nodes where CPU or memory usage shows a sudden spike or has been consistently elevated over the past hour or day. This can help you determine whether the issue is momentary or ongoing.

1. To investigate a specific node, click the node name in the dashboard to filter all charts to that node. Check the following metrics:
   - **CPU usage %** — a sustained value above 90% indicates CPU saturation.
   - **Memory usage %** — a value consistently above 85% increases the risk of out-of-memory (OOM) events.
   - **Network bytes in/out** — an unexpected traffic spike can indicate a runaway workload or a network attack.

1. To check which pods are consuming the most resources on a node, navigate to the **Kubernetes** > **Pods** dashboard and filter by the affected node. Note the names of any pods that show consistently high CPU or memory usage, as these are likely candidates for the worker node instability.

## Check pod health and restart counts with {{site.data.keyword.mon_full_notm}}
{: #debug-observability-pods}

Pods that crash-loop or restart frequently are a common sign of application-level issues, such as OOM kills or misconfigured readiness probes. Use {{site.data.keyword.mon_full_notm}} to identify these pods without running `oc get pods` repeatedly.

1. In the {{site.data.keyword.mon_full_notm}} UI, navigate to the **Kubernetes** > **Pods** pre-built dashboard.

1. Review the **Container Restarts** panel. Look for pods that show a restart count greater than zero in the past 15 minutes, or that show a rapid increase over a longer time period.
   - A restart count that increments repeatedly indicates a crash loop. Note the pod name and namespace for use in the log investigation steps that follow.
   - A restart count of zero but a **Pending** or **Unknown** status indicates a scheduling or node connectivity issue rather than an application failure.

1. To set up an alert for future pod restart events, click the **Alerts** icon in the {{site.data.keyword.mon_full_notm}} UI and create a metric alert on the `kubernetes.pod.restart.count` metric. Set the threshold to trigger when the count exceeds two restarts within five minutes for any pod. This provides early warning before a crash loop becomes disruptive. For more information about configuring alerts, see [Setting up {{site.data.keyword.mon_full}} alerts](/docs/openshift?topic=openshift-health-monitor#monitoring-alerts).

## Investigate container logs with {{site.data.keyword.logs_full_notm}}
{: #debug-observability-logs}

When a pod has restarted or a node is experiencing issues, reviewing container logs is essential for understanding the root cause. {{site.data.keyword.logs_full_notm}} retains historical log data that is not available through `oc logs` after a container is restarted.

1. Open the {{site.data.keyword.logs_full_notm}} dashboard.
   1. In the {{site.data.keyword.cloud_notm}} console, navigate to your cluster resource page and click the relevant cluster.
   1. Under **Integrations**, find the **Logging** option and click **Launch**. The {{site.data.keyword.logs_full_notm}} UI opens in a new window.

1. Set the time range to cover the window when the issue occurred. If the issue is ongoing, set the range to the past one hour. If you are investigating a past event, set the specific start and end time to narrow the results.

1. Search for the affected pod or namespace. Use the query bar at the top of the UI to filter logs. For example, to show logs from all pods in the `default` namespace, enter the following query:
   ```text
   kubernetes.namespace_name:"default"
   ```
   {: codeblock}

   To narrow results to a specific pod by name, use:
   ```text
   kubernetes.pod_name:"MY_POD_NAME"
   ```
   {: codeblock}

1. Review the log lines for error-level entries. Look for any of the following patterns that indicate common failure modes:
   - `OOMKilled` or `out of memory` — the container exceeded its memory limit and was terminated by the kernel.
   - `CrashLoopBackOff` — the container is restarting repeatedly, often due to an application error on startup.
   - `failed to pull image` or `ImagePullBackOff` — the node cannot pull the container image from the registry.
   - `Connection refused` or `context deadline exceeded` — the application cannot reach a dependent service or the Kubernetes API server.

1. If you find an OOM-related log entry, note the timestamp and check the {{site.data.keyword.mon_full_notm}} **Kubernetes** > **Pods** dashboard for the same time window to confirm that the pod's memory usage reached its limit immediately before the restart.

## Check Kubernetes events with {{site.data.keyword.logs_full_notm}}
{: #debug-observability-events}

Kubernetes events capture important cluster activity such as pod scheduling failures, node conditions, and volume mount errors. {{site.data.keyword.logs_full_notm}} ingests these events automatically and lets you search and filter them historically — unlike `oc get events`, which only shows recent events from the current session.

1. In the {{site.data.keyword.logs_full_notm}} UI, use the following query to show all Kubernetes warning events across the cluster:
   ```text
   kubernetes.event.type:"Warning"
   ```
   {: codeblock}

1. To filter events to a specific worker node, add the node name to the query. Replace NODE_NAME with the name of the affected node:
   ```text
   kubernetes.event.type:"Warning" AND kubernetes.event.involvedObject.name:"NODE_NAME"
   ```
   {: codeblock}

1. Review the **Reason** field in the event log entries. The following reasons are most relevant for debugging worker node and workload issues:

   `NodeNotReady`
   :   The node is reporting a `NotReady` condition. This event often precedes or accompanies a worker node entering a `Critical` state.

   `OOMKilling`
   :   The kernel terminated a process on the node due to memory exhaustion.

   `FailedScheduling`
   :   The scheduler could not place a pod on any available node. The message field typically explains why, such as insufficient CPU, memory, or a node selector mismatch.

   `BackOff`
   :   A container is in a crash loop. The event is generated each time the `kubelet` backs off before restarting the container.

   `FailedMount` or `FailedAttachVolume`
   :   A persistent volume could not be mounted or attached to a pod, which prevents the pod from starting.

1. For any event that seems relevant, note the `involvedObject.name` and `involvedObject.namespace` values, and use them to correlate with the log and metric data you gathered in the previous sections.

## Next steps
{: #debug-observability-next}

- If you identified a worker node under resource pressure, consider [reloading or replacing the worker node](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-reload-cli) or adjusting resource requests and limits on the pods running on that node.
- If pods are crash-looping due to OOM kills, increase the memory limits for the affected containers or move memory-intensive workloads to a worker pool with larger nodes.
- If logs reveal image pull failures, check your [image pull secrets](/docs/openshift?topic=openshift-registry#use_imagePullSecret_secret) and verify that the worker node can reach the container registry.
- For issues that cannot be resolved with the information gathered here, see [Gathering data for a support case](/docs/openshift?topic=openshift-ts-critical-notready#ts-critical-notready-gather) to collect the information needed to open a support ticket.

## Related links
{: #debug-observability-related}

- [Monitoring cluster health](/docs/openshift?topic=openshift-health-monitor)
- [Getting started with {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-getting-started){: external}
- [Getting started with {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-getting-started){: external}
- [Troubleshooting worker nodes in `Critical` or `NotReady` state](/docs/openshift?topic=openshift-ts-critical-notready)
- [Setting up {{site.data.keyword.mon_full}} alerts](/docs/openshift?topic=openshift-health-monitor#monitoring-alerts)
