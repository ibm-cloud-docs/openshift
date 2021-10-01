---

copyright:
  years: 2014, 2021
lastupdated: "2021-10-01"

keywords: oks, iro, openshift, red hat, red hat openshift, rhos, roks, rhoks

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

  


# Monitoring cluster health
{: #health-monitor}

For cluster metrics and app monitoring, {{site.data.keyword.openshiftlong}} clusters include built-in tools to help you manage the health of your single cluster instance. You can also set up {{site.data.keyword.cloud_notm}} tools for multi-cluster analysis or other use cases, such as {{site.data.keyword.containerlong_notm}} add-ons: {{site.data.keyword.la_full_notm}} and {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

## Understanding options for monitoring
{: #oc_logmet_options}

To help understand when to use the built-in {{site.data.keyword.openshiftshort}} tools or {{site.data.keyword.cloud_notm}} integrations, review the following information.
{: shortdesc}

### {{site.data.keyword.mon_full_notm}}
Review the following details about {{site.data.keyword.mon_full_notm}}. 
{: shortdesc}

- Customizable user interface for a unified look at your cluster metrics, container security, resource usage, alerts, and custom events.
- Quick integration with the cluster via a script.
- Aggregated metrics and container monitoring across clusters and cloud providers.
- Historical access to metrics that is based on the timeline and plan, and ability to capture and download trace files.
- Highly available, scalable, and compliant with industry security standards.
- Integrated with {{site.data.keyword.cloud_notm}} IAM for user access management.
- Free trial to try out the capabilities.
- To get started, see [Forwarding cluster and app metrics to {{site.data.keyword.mon_full_notm}}](#openshift_monitoring).

For more information, see [the {{site.data.keyword.openshiftshort}} documentation](http://docs.openshift.com/container-platform/4.7/monitoring/understanding-the-monitoring-stack.html){: external}.

### Built-in {{site.data.keyword.openshiftshort}} monitoring tools
{: #built-in-mon-tools}

Review the following details about built-in monitoring tools for your cluster. 
{: shortdesc}

- Built-in Prometheus and Grafana deployments in the `openshift-monitoring` project for cluster metrics.
- At-a-glance, real-time view of how your pods consume cluster resources that can be accessed from the {{site.data.keyword.openshiftshort}} **Cluster Console**.
- Monitoring is on a per-cluster basis.
- The `openshift-monitoring` project stack is set up in a single zone only. No persistant storage is available to back up or view metric history.

For more information, see [the {{site.data.keyword.openshiftshort}} documentation](http://docs.openshift.com/container-platform/4.7/monitoring/understanding-the-monitoring-stack.html){: external}.

## Forwarding cluster and app metrics to {{site.data.keyword.mon_full_notm}}
{: #openshift_monitoring}

Use the {{site.data.keyword.openshiftlong_notm}} observability plug-in to create a monitoring configuration for {{site.data.keyword.mon_full_notm}} in your cluster, and use this monitoring configuration to automatically collect and forward metrics to {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

With {{site.data.keyword.mon_full_notm}}, you can collect cluster and pod metrics, such as the CPU and memory usage of your worker nodes, incoming and outgoing HTTP traffic for your pods, and data about several infrastructure components. In addition, the agent can collect custom application metrics by using either a Prometheus-compatible scraper or a StatsD facade.

Considerations for using the {{site.data.keyword.openshiftlong_notm}} observability plug-in:
- You can have only one monitoring configuration for {{site.data.keyword.mon_full_notm}} in your cluster at a time. If you want to use a different {{site.data.keyword.mon_full_notm}} service instance to send metrics to, use the [`ibmcloud ob monitoring config replace`](/docs/containers?topic=containers-observability_cli#monitoring_config_replace) command.
- {{site.data.keyword.openshiftshort}} clusters in {{site.data.keyword.satelliteshort}} cannot currently use the {{site.data.keyword.openshiftlong_notm}} console or the observability plug-in CLI to enable monitoring for {{site.data.keyword.satelliteshort}} clusters. You must manually deploy monitoring agents to your cluster to forward metrics to {{site.data.keyword.mon_short}}.
- If you created a {{site.data.keyword.mon_short}} configuration in your cluster without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, you can use the [`ibmcloud ob monitoring agent discover`](/docs/containers?topic=containers-observability_cli#monitoring_agent_discover) command to make the configuration visible to the plug-in. Then, you can use the observability plug-in commands and functionality in the {{site.data.keyword.cloud_notm}} console to manage the configuration.

Before you begin:
- Verify that you are assigned the **Editor** platform access role and **Manager** server access role for {{site.data.keyword.mon_full_notm}}.
- Verify that you are assigned the **Administrator** platform access role and the **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}} to create the monitoring configuration. To view a monitoring configuration or launch the {{site.data.keyword.mon_short}} dashboard after the monitoring configuration is created, users must be assigned the **Administrator** platform access role and the **Manager** service access role for the `ibm-observe` Kubernetes namespace in {{site.data.keyword.containerlong_notm}}.
- If you want to use the CLI to set up the monitoring configuration:
    - [Install the {{site.data.keyword.openshiftlong_notm}} observability CLI plug-in (`ibmcloud ob`)](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps).
    - [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To set up a monitoring configuration for your cluster:

1. Create an [{{site.data.keyword.mon_full_notm}} service instance](/docs/monitoring?topic=monitoring-provision) and note the name of the instance. The service instance must belong to the same {{site.data.keyword.cloud_notm}} account where you created your cluster, but can be in a different resource group and {{site.data.keyword.cloud_notm}} region than your cluster.
2. Set up a monitoring configuration for your cluster. When you create the monitoring configuration, an {{site.data.keyword.openshiftshort}} project `ibm-observe` is created and a {{site.data.keyword.mon_short}} agent is deployed as a Kubernetes daemon set to all worker nodes in your cluster. This agent collects cluster and pod metrics, such as the worker node CPU and memory usage, or the amount incoming and outgoing network traffic to your pods.

    - **From the console**
        1. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster for which you want to create a {{site.data.keyword.mon_short}} configuration.
        2. On the cluster **Overview** page, click **Connect**.
        3. Select the region and the {{site.data.keyword.mon_full_notm}} service instance that you created earlier, and click **Connect**.

    - **From the CLI**
        1. Create the {{site.data.keyword.mon_short}} configuration. When you create the {{site.data.keyword.mon_short}} configuration, the access key that was last added is retrieved automatically. If you want to use a different access key, add the `--sysdig-access-key <access_key>` option to the command.

            To use a different service access key after you created the monitoring configuration, use the [`ibmcloud ob monitoring config replace`](/docs/containers?topic=containers-observability_cli#monitoring_config_replace) command.
            {: tip}

            ```sh
            ibmcloud ob monitoring config create --cluster <cluster_name_or_ID> --instance <Monitoring_instance_name_or_ID>
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
    1. If you used the console to create the {{site.data.keyword.mon_short}} configuration, log in to your cluster. For more information, see [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
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

    3. Review the configmap that was created for your {{site.data.keyword.mon_short}} agent.
        ```sh
        oc describe configmap -n ibm-observe
        ```
        {: pre}

4. Access the metrics for your pods and cluster from the {{site.data.keyword.mon_short}} dashboard.
    1. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster that you configured.
    2. On the cluster **Overview** page, click **Launch**. The {{site.data.keyword.mon_short}} dashboard opens.
    3. Review the pod and cluster metrics that the {{site.data.keyword.mon_short}} agent collected from your cluster. It might take a few minutes for your first metrics to show.

5. Review how you can work with the [{{site.data.keyword.mon_short}} dashboard](/docs/monitoring?topic=monitoring-panels) to further analyze your metrics.

## Viewing cluster states
{: #states}

Review the state of an {{site.data.keyword.openshiftshort}} cluster to get information about the availability and capacity of the cluster, and potential problems that might occur.
{: shortdesc}

To view information about a specific cluster, such as its zones, service endpoint URLs, Ingress subdomain, version, and owner, use the `ibmcloud oc cluster get --cluster <cluster_name_or_ID>` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_get). Include the `--show-resources` flag to view more cluster resources such as add-ons for storage pods or subnet VLANs for public and private IPs.

You can review information about the overall cluster, the IBM-managed master, and your worker nodes. To troubleshoot your cluster and worker nodes, see [Troubleshooting clusters](/docs/openshift?topic=openshift-debug_clusters).

For more information about cluster and worker states, see:
- [Cluster states](/docs/openshift?topic=openshift-cluster-states-reference).
- [Worker node states](/docs/openshift?topic=openshift-worker-node-state-reference).

### Master states
{: #states_master}

Your {{site.data.keyword.openshiftlong_notm}} cluster includes an IBM-managed master with highly available replicas, automatic security patch updates applied for you, and automation in place to recover in case of an incident. You can check the health, status, and state of the cluster master by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
{: shortdesc}

The **Master Health** reflects the state of master components and notifies you if something needs your attention. The health might be one of the following states.
- `error`: The master is not operational. IBM is automatically notified and takes action to resolve this issue. You can continue monitoring the health until the master is `normal`. You can also [open an {{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-get-help).
- `normal`: The master is operational and healthy. No action is required.
- `unavailable`: The master might not be accessible, which means some actions such as resizing a worker pool are temporarily unavailable. IBM is automatically notified and takes action to resolve this issue. You can continue monitoring the health until the master is `normal`.
- `unsupported`: The master runs an unsupported version of Kubernetes. You must [update your cluster](/docs/containers?topic=containers-update) to return the master to `normal` health.

The **Master Status** provides details of what operation from the master state is in progress. The status includes a timestamp of how long the master has been in the same state, such as `Ready (1 month ago)`. The **Master State** reflects the lifecycle of possible operations that can be performed on the master, such as deploying, updating, and deleting. Each state is described in the following table.

|Master state|Description|
|--- |--- |
|`deployed`|The master is successfully deployed. Check the status to verify that the master is `Ready` or to see if an update is available.|
|`deploying`|The master is currently deploying. Wait for the state to become `deployed` before working with your cluster, such as adding worker nodes.|
|`deploy_failed`|The master failed to deploy. IBM Support is notified and works to resolve the issue. Check the **Master Status** field for more information, or wait for the state to become `deployed`.|
|`deleting`|The master is currently deleting because you deleted the cluster. You cannot undo a deletion. After the cluster is deleted, you can no longer check the master state because the cluster is completely removed.|
|`delete_failed`|The master failed to delete. IBM Support is notified and works to resolve the issue. You cannot resolve the issue by trying to delete the cluster again. Instead, check the **Master Status** field for more information, or wait for the cluster to delete. You can also [open an {{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-get-help).|
|`updating`|The master is updating its Kubernetes version. The update might be a patch update that is automatically applied, or a minor or major version that you applied by updating the cluster. During the update, your highly available master can continue processing requests, and your app workloads and worker nodes continue to run. After the master update is complete, you can [update your worker nodes](/docs/containers?topic=containers-update#worker_node).</br></br>If the update is unsuccessful, the master returns to a `deployed` state and continues running the previous version. IBM Support is notified and works to resolve the issue. You can check if the update failed in the **Master Status** field.|
|`update_cancelled`|The master update is canceled because the cluster was not in a healthy state at the time of the update. Your master remains in this state until your cluster is healthy and you manually update the master. To update the master, use the `ibmcloud oc cluster master update` [command](/docs/containers?topic=containers-kubernetes-service-cli#cs_cluster_update). If you do not want to update the master to the default `major.minor` version during the update, include the `--version` flag and specify the latest patch version that is available for the `major.minor` version that you want, such as `1.20.7`. To list available versions, run `ibmcloud oc versions`.|
|`update_failed`|The master update failed. IBM Support is notified and works to resolve the issue. You can continue to monitor the health of the master until the master reaches a normal state. If the master remains in this state for more than 1 day, [open an {{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-get-help). IBM Support might identify other issues in your cluster that you must fix before the master can be updated.|
{: caption="Master states"}
{: summary="Table rows read from left to right, with the master state in column one and a description in column two."}


## Disabling remote health reporting
{: #oc_disable_telemetry_reports}

OpenShift Container Platform collects anonymized health reports about your cluster through a [telemetry component that is enabled by default](https://docs.openshift.com/container-platform/4.7/support/remote_health_monitoring/about-remote-health-monitoring.html){: external} in your {{site.data.keyword.openshiftlong_notm}} cluster.
{: shortdesc}

You might want to disable this remote health reporting to comply with privacy laws, organizational standards, or data governance practices. To disable, you must modify the global configuration for the cluster and reload all of the worker nodes.

1. Check that the telemetry reporting pod runs in your cluster.
    ```sh
    oc get pods -n openshift-monitoring
    ```
    {: pre}

    Example output

    ```sh
    NAME                              READY   STATUS      RESTARTS   AGE
    telemeter-client-7cfd7cb85-lm9dt  3/3     Running     0          4d13h
    ...
    ```
    {: screen}

2. Follow the {{site.data.keyword.openshiftshort}} instructions to [update the global pull secret in the cluster to disable remote health reporting](https://docs.openshift.com/container-platform/4.7/support/remote_health_monitoring/opting-out-of-remote-health-reporting.html){: external}.
3. To pick up the global configuration changes, reload all of the worker nodes in your cluster.
    1. Note the **ID** of the worker nodes in your cluster.
        ```sh
        ibmcloud oc worker ls -c <cluster_name_or_ID>
        ```
        {: pre}

    2. Reload each worker node. You can reload multiple worker nodes by including multiple `-w` flags, but make sure to leave enough worker nodes running at the same time for your apps to avoid an outage.
        ```sh
        ibmcloud oc worker reload -c <cluster_name_or_ID> -w <workerID_1> -w <workerID_2>
        ```
        {: pre}

4. After the worker nodes are back in a healthy state, verify that the telemetry reporting pod no longer runs in your cluster.
    ```sh
    oc get pods -n openshift-monitoring
    ```
    {: pre}






