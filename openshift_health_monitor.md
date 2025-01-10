---

copyright:
  years: 2014, 2025
lastupdated: "2025-01-10"


keywords: oks, iro, openshift, red hat, red hat openshift

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}





# Monitoring cluster health
{: #health-monitor}

For cluster metrics and app monitoring, {{site.data.keyword.openshiftlong}} clusters include built-in tools to help you manage the health of your single cluster instance. You can also set up {{site.data.keyword.cloud_notm}} tools for multi-cluster analysis or other use cases, such as {{site.data.keyword.containerlong_notm}} cluster add-ons: {{site.data.keyword.la_full_notm}} and {{site.data.keyword.mon_full_notm}}.
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

OpenShift includes a preconfigured, preinstalled, and self-updating monitoring stack that provides monitoring for core platform components on a per-cluster basis. This monitoring includes built-in Prometheus and Grafana deployments in the `openshift-monitoring` project for cluster metrics, which is available in a single zone only. You can view and manage your monitoring dashboards, metrics, and alerts from the {{site.data.keyword.redhat_openshift_notm}} web console. For more information, see [Monitoring](https://docs.openshift.com/container-platform/4.16/observability/monitoring/monitoring-overview.html){: external} in the Red Hat OpenShift documentation. 

By default, the monitoring stack does not use persistent storage to back up metric history, and instead uses a temporary `EmptyDir` volume in the host filesystem. The retention period for metrics history ranges from 11 to 15 days, depending on your cluster version. For some workloads, these settings might use a significant amount of disk space and memory, or might not meet requirements for metrics retention. You can configure the monitoring stack to use persistent storage, change the metrics retention policies, or run Prometheus on dedicated nodes. For more information, see [Configuring the monitoring stack](https://docs.openshift.com/container-platform/4.16/observability/monitoring/configuring-the-monitoring-stack.html){: external}.

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

Want to set up storage monitoring alerts for platforms such as email or Slack? See [Sending notifications to external systems](https://docs.openshift.com/container-platform/4.10/monitoring/managing-alerts.html#sending-notifications-to-external-systems_managing-alerts){: external} in the {{site.data.keyword.redhat_openshift_notm}} documentation. 
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

For more information, see [Monitoring](https://docs.openshift.com/container-platform/4.16/observability/monitoring/monitoring-overview.html){: external}.

If your volume is reaching capacity, try setting up [volume expansion](/docs/openshift?topic=openshift-vpc-block#vpc-block-volume-expand).
{: tip}

## Forwarding cluster and app metrics to {{site.data.keyword.mon_full_notm}}
{: #openshift_monitoring}

The following steps are deprecated. The observability CLI plug-in `ibmcloud ob` and the `v2/observe` endpoints are deprecated and support ends on 28 March 2025. You can now manage your logging and monitoring integrations from the console or through the Helm charts. For the latest steps, see [Working with the Kubernetes agent](/docs/monitoring?topic=monitoring-agent_Kube) or [Working with the Red Hat OpenShift agent](/docs/monitoring?topic=monitoring-agent_openshift).
{: deprecated}

Use the {{site.data.keyword.openshiftlong_notm}} observability plug-in to create a monitoring configuration for {{site.data.keyword.mon_full_notm}} in your cluster, and use this monitoring configuration to automatically collect and forward metrics to {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

With {{site.data.keyword.mon_full_notm}}, you can collect cluster and pod metrics, such as the CPU and memory usage of your worker nodes, incoming and outgoing HTTP traffic for your pods, and data about several infrastructure components. In addition, the agent can collect custom application metrics by using either a Prometheus-compatible scraper or a statsd facade.

Considerations for using the {{site.data.keyword.openshiftlong_notm}} observability plug-in:
- You can have only one monitoring configuration for {{site.data.keyword.mon_full_notm}} in your cluster at a time. If you want to use a different {{site.data.keyword.mon_full_notm}} service instance to send metrics to, use the [`ibmcloud ob monitoring config replace`](/docs/containers?topic=containers-observability_cli#monitoring_config_replace) command.
- {{site.data.keyword.redhat_openshift_notm}} clusters in {{site.data.keyword.satelliteshort}} can't currently use the {{site.data.keyword.openshiftlong_notm}} console or the observability plug-in CLI to enable monitoring for {{site.data.keyword.satelliteshort}} clusters. You must manually deploy monitoring agents to your cluster to forward metrics to {{site.data.keyword.mon_short}}.
- If you created a {{site.data.keyword.mon_short}} configuration in your cluster without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, you can use the [`ibmcloud ob monitoring agent discover`](/docs/containers?topic=containers-observability_cli#monitoring_agent_discover) command to make the configuration visible to the plug-in. Then, you can use the observability plug-in commands and functionality in the {{site.data.keyword.cloud_notm}} console to manage the configuration.

Before you begin:
- Verify that you are assigned the **Editor** platform access role and **Manager** server access role for {{site.data.keyword.mon_full_notm}}.
- Verify that you are assigned the **Administrator** platform access role and the **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}} to create the monitoring configuration. To view a monitoring configuration or launch the {{site.data.keyword.mon_short}} dashboard after the monitoring configuration is created, users must be assigned the **Administrator** platform access role and the **Manager** service access role for the `ibm-observe` Kubernetes namespace in {{site.data.keyword.containerlong_notm}}.
- If you want to use the CLI to set up the monitoring configuration:
    - [Install the {{site.data.keyword.openshiftlong_notm}} observability CLI plug-in (`ibmcloud ob`)](/docs/containers?topic=containers-cli-install).
    - [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

To set up a monitoring configuration for your cluster:

1. Create an [{{site.data.keyword.mon_full_notm}} service instance](/docs/monitoring?topic=monitoring-provision) and note the name of the instance. The service instance must belong to the same {{site.data.keyword.cloud_notm}} account where you created your cluster, but can be in a different resource group and {{site.data.keyword.cloud_notm}} region than your cluster.
2. Set up a monitoring configuration for your cluster. When you create the monitoring configuration, an {{site.data.keyword.redhat_openshift_notm}} project `ibm-observe` is created and a {{site.data.keyword.mon_short}} agent is deployed as a Kubernetes daemon set to all worker nodes in your cluster. This agent collects cluster and pod metrics, such as the worker node CPU and memory usage, or the amount incoming and outgoing network traffic to your pods.

    In the console.
    
    1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster for which you want to create a {{site.data.keyword.mon_short}} configuration.
    2. On the cluster **Overview** page, click **Connect**.
    3. Select the region and the {{site.data.keyword.mon_full_notm}} service instance that you created earlier, and click **Connect**.

    In the CLI.
    
    1. Create the {{site.data.keyword.mon_short}} configuration. When you create the {{site.data.keyword.mon_short}} configuration, the access key that was last added is retrieved automatically. If you want to use a different access key, add the `--sysdig-access-key <access_key>` option to the command.

        To use a different service access key after you created the monitoring configuration, use the [`ibmcloud ob monitoring config replace`](/docs/containers?topic=containers-observability_cli#monitoring_config_replace) command.
        {: tip}

        **Version 4.15 and later**: If your cluster has outbound traffic protection enabled, you must set up monitoring by using the private endpoint. To do this, specify the `--private-endpoint` option.

        ```sh
        ibmcloud ob monitoring config create --cluster <cluster_name_or_ID> --instance <Monitoring_instance_name_or_ID> [--private-endpoint]
        ```
        {: pre}

        Example output
        ```sh
        Creating configuration...
        OK
        ```
        {: screen}

    2. Verify that the monitoring configuration was added to your cluster.
        ```sh
        ibmcloud ob monitoring config list --cluster <cluster_name_or_ID>
        ```
        {: pre}

        Example output
        ```sh
        Listing configurations...

        OK
        Instance Name                Instance ID                            CRN   
        IBM Cloud Monitoring-aaa     1a111a1a-1111-11a1-a1aa-aaa11111a11a   crn:v1:prod:public:sysdig:us-south:a/a11111a1aaaaa11a111aa11a1aa1111a:1a111a1a-1111-11a1-a1aa-aaa11111a11a::  
        ```
        {: screen}

3. Optional: Verify that the {{site.data.keyword.mon_short}} agent was set up successfully.
    1. If you used the console to create the {{site.data.keyword.mon_short}} configuration, log in to your cluster.
    2. Verify that the daemon set for the {{site.data.keyword.mon_short}} agent was created and all instances are listed as `AVAILABLE`.
        ```sh
        oc get daemonsets -n ibm-observe
        ```
        {: pre}

        Example output
        ```sh
        NAME           DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
        sysdig-agent   9         9         9       9            9           <none>          14m
        ```
        {: screen}

        The number of daemon set instances that are deployed equals the number of worker nodes in your cluster.

    3. Review the ConfigMap that was created for your {{site.data.keyword.mon_short}} agent.
        ```sh
        oc describe configmap -n ibm-observe
        ```
        {: pre}

4. Access the metrics for your pods and cluster from the {{site.data.keyword.mon_short}} dashboard.
    1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster that you configured.
    2. On the cluster **Overview** page, click **Launch**. The {{site.data.keyword.mon_short}} dashboard opens.
    3. Review the pod and cluster metrics that the {{site.data.keyword.mon_short}} agent collected from your cluster. It might take a few minutes for your first metrics to show.

5. Review how you can work with the [{{site.data.keyword.mon_short}} dashboard](/docs/monitoring?topic=monitoring-panels) to further analyze your metrics.





## Enabling remote health reporting
{: #oc_enable_telemetry_reports}

Telemetry is a remote health monitoring feature that collects aggregated data about your cluster, such as the health of your components and the number and types of resources in use. If you have a public cluster, you can elect to have your own Telemetry data visible in your account for your use. For more information, see [Telemetry for remote health monitoring](/docs/openshift?topic=openshift-telemetry).
