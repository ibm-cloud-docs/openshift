---

copyright:
  years: 2014, 2025
lastupdated: "2025-05-29"


keywords: oks, iro, openshift, red hat, red hat openshift

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}





# Monitoring cluster health
{: #health-monitor}

For cluster metrics and app monitoring, {{site.data.keyword.openshiftlong}} clusters include built-in tools to help you manage the health of your single cluster instance. You can also set up {{site.data.keyword.cloud_notm}} tools for multi-cluster analysis or other use cases, such as {{site.data.keyword.containerlong_notm}} cluster add-ons: {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

## Understanding options for monitoring
{: #oc_logmet_options_monitoring}

To help understand when to use the built-in {{site.data.keyword.redhat_openshift_notm}} tools or {{site.data.keyword.cloud_notm}} integrations, review the following information.
{: shortdesc}



**Monitoring limitation in private-only clusters with RHCOS worker nodes**: The monitoring agent relies on kernel headers in the operating system, however RHCOS doesn't have kernel headers. In this scenario, the agent reaches back to `sysdig.com` to use the pre-compiled agent. In clusters with no public network access this process fails. To allow monitoring on RHCOS clusters, you must either [allow outbound traffic](/docs/openshift?topic=openshift-sbd-allow-outbound#existing-cluster-sbd) or see the Sysdig documentation for [installing the agent on air-gapped environments](https://docs.sysdig.com/en/docs/administration/on-premises-deployments/installation/airgapped-installation/){: external}.
{: important}



### {{site.data.keyword.mon_full_notm}}
{: #oc_mon_details}

Review the following details about {{site.data.keyword.mon_full_notm}}. 
{: shortdesc}

- Customizable user interface for a unified look at your cluster metrics, container security, resource usage, alerts, and custom events.
- Quick integration with the cluster via a script.
- Aggregated metrics and container monitoring across clusters and cloud providers.
- Historical access to metrics that is based on the timeline and plan, and ability to capture and download trace files.
- Highly available, scalable, and compliant with industry security standards.
- Integrated with {{site.data.keyword.cloud_notm}} IAM for user access management.


### Built-in {{site.data.keyword.redhat_openshift_notm}} monitoring tools
{: #built-in-mon-tools}

OpenShift includes a preconfigured, preinstalled, and self-updating monitoring stack that provides monitoring for core platform components on a per-cluster basis. This monitoring includes built-in Prometheus and Grafana deployments in the `openshift-monitoring` project for cluster metrics, which is available in a single zone only. You can view and manage your monitoring dashboards, metrics, and alerts from the {{site.data.keyword.redhat_openshift_notm}} web console. For more information, see [Monitoring](https://docs.openshift.com/container-platform/4.17/virt/monitoring/virt-monitoring-overview.html){: external} in the Red Hat OpenShift documentation. 

By default, the monitoring stack does not use persistent storage to back up metric history, and instead uses a temporary `EmptyDir` volume in the host file system. The retention period for metrics history ranges from 11 to 15 days, depending on your cluster version. For some workloads, these settings might use a significant amount of disk space and memory, or might not meet requirements for metrics retention. You can configure the monitoring stack to use persistent storage, change the metrics retention policies, or run Prometheus on dedicated nodes. For more information, see [Configuring the monitoring stack](https://docs.redhat.com/documentation/openshift_container_platform/4.17/html/red_hat_build_of_opentelemetry/otel-configuring-metrics-for-monitoring-stack){: external}.

Note that {{site.data.keyword.openshiftlong_notm}} version 4.16 sets a default 10 GB size retention. 


### Monitoring {{site.data.keyword.openshiftlong}} storage metrics
{: #monitor-metrics}

{{site.data.keyword.openshiftlong}} clusters include built-in tools to help cluster administrators get information about the availability and capacity of storage volumes.
{: shortdesc}

If you are unable to view storage metrics in the {{site.data.keyword.redhat_openshift_notm}} monitoring dashboard, see [Debugging {{site.data.keyword.block_storage_is_short}} metrics](/docs/openshift?topic=openshift-debug_monitoring).
{: tip}

The following metrics can be monitored for {{site.data.keyword.openshiftlong}} clusters.
- `kubelet_volume_stats_available_bytes`
- `kubelet_volume_stats_capacity_bytes`
- `kubelet_volume_stats_inodes`
- `kubelet_volume_stats_inodes_free`
- `kubelet_volume_stats_inodes_used`

Want to set up storage monitoring alerts for platforms such as email or Slack? See [Sending notifications to external systems](https://docs.redhat.com/en/documentation/openshift_container_platform/4.10/html/monitoring/managing-alerts#sending-notifications-to-external-systems_managing-alerts){: external} in the {{site.data.keyword.redhat_openshift_notm}} documentation. 
{: tip}

Before monitoring metrics for {{site.data.keyword.block_storage_is_short}}, you must have a cluster with the {{site.data.keyword.block_storage_is_short}} cluster add-on enabled and you must have a {{site.data.keyword.block_storage_is_short}} volume attached to a worker node. {{site.data.keyword.openshiftlong}} Storage Metrics are populated only for mounted storage volumes.


1. Navigate to the {{site.data.keyword.redhat_openshift_notm}} web console and select **Monitoring** and then **Metrics**. 

1. Input the metric you want to monitor in the dialog box and select **Run queries**. 
    ```sh
    kubelet_volume_stats_used_bytes{persistentvolumeclaim="NAME OF PVC"} / kubelet_volume_stats_capacity_bytes{persistentvolumeclaim="NAME OF PVC"}
    ```
    {: pre}

    Example output
    
    ```sh
    endpoint       instance      job     metrics_path  namespace  node         persistentvolumeclaim  prometheus               service  value 
    https-metrics  11.111.1.1:XX kubelet /metrics      default    11.111.1.1   PVC-NAME               openshift-monitoring/k8s kubelet  0.003596851526321722
    ```
    {: screen}

For more information, see [Monitoring](https://docs.openshift.com/container-platform/4.17/virt/monitoring/virt-monitoring-overview.html){: external}.

If your volume is reaching capacity, try setting up [volume expansion](/docs/openshift?topic=openshift-vpc-block#vpc-block-volume-expand).
{: tip}


## Migrating logging and monitoring agents to Cloud Logs
{: #openshift_monitoring}

The observability CLI plug-in `ibmcloud ob` and the `v2/observe` endpoints are no longer supported. There is no direct replacement, but you can now manage your logging and monitoring integrations from the console or through the Helm charts. For the latest steps, [Managing the Logging agent for Red Hat OpenShift on IBM Cloud clusters](/docs/cloud-logs?topic=cloud-logs-agent-openshift) and [Working with the Red Hat OpenShift monitoring agent](/docs/monitoring?topic=monitoring-agent_openshift).
{: unsupported}

You can no longer use the `ob` plugin, Terraform, or API to install observability agents on a cluster or to modify your existing configuration. Sysdig agents continue to send metrics to the specified IBM Cloud Monitoring instance. LogDNA agents can no longer send logs since IBM Cloud Log Analysis is replaced by IBM Cloud Logs. 

### Reviewing your observability agents
{: #ob-review-mon}

The observability plug-in installs Sysdig and LogDNA agents in the `ibm-observe` namespace.

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

2) Review the configmaps in the `ibm-observe` namespace.
    ```sh
    kubectl get cm -n ibm-observe
    ```
    {: pre}

    ```sh
    Example output

    NAME                                   DATA   AGE

    e405f1fc-feba-4350-9337-e7e249af871c   6      25m

    f59851a6-ede6-4719-afa0-eee7ce65eeb5   6      20m
    ```
    {: pre}

1. Observability agents installed by the observability plug-in use a configmap with the GUID of the IBM Cloud Monitoring instance or the IBM Cloud Log Analysis instance that logs or metrics are being sent to. If your cluster has agents in a namespace other than `ibm-observe` or the configmaps in `ibm-observe` are not named with the instance GUIDs, then these agents were not installed with the IKS observability (ob) plug-in.

### Removing the observability plug-in agents
{: #ob-remove-mon}

1. Clean up the daemonsets and configmaps.
    ```sh
    kubectl delete daemonset logdna-agent -n ibm-observe
    kubectl delete daemonset sysdig-agent -n ibm-observe
    kubectl delete configmap <logdna-configmap> -n ibm-observe
    kubectl delete configmap <sysdig-configmap> -n ibm-observe
    ```
    {: pre}

1. Optional: Delete the namespace. After no other resources are running in the namespace.
    ```sh
    kubectl delete namespace ibm-observe
    ```
    {: pre}

After removing the plug-in has been removed, reinstall Logging and Monitoring agents in your cluster using the Cluster dashboard, Terraform, or manually. 

For more information, see the following links:
- [Managing the Logging agent for Red Hat OpenShift on IBM Cloud clusters](/docs/cloud-logs?topic=cloud-logs-agent-openshift).
- [Working with the Red Hat OpenShift monitoring agent](/docs/monitoring?topic=monitoring-agent_openshift).


## Enabling remote health reporting
{: #oc_enable_telemetry_reports}

Telemetry is a remote health monitoring feature that collects aggregated data about your cluster, such as the health of your components and the number and types of resources in use. If you have a public cluster, you can elect to have your own Telemetry data visible in your account for your use. For more information, see [Telemetry for remote health monitoring](/docs/openshift?topic=openshift-telemetry).
