---

copyright:
  years: 2025, 2025
lastupdated: "2025-01-10"

keywords: logging, cloud logs, logs, log analysis, containers

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Migrating your {{site.data.keyword.openshiftlong_notm}} clusters to Cloud Logs
{: #cloud-logs-migration}

Log Analysis and Activity Tracker are deprecated and support ends on 28 March 2025. For more details about the deprecation, including migration steps, see [Migrating to Cloud Logs](/docs/log-analysis?topic=log-analysis-deprecation_migration).
{: deprecated}

You need to migrate if your clusters are using the deprecated logging agent.

Additonally, the observability CLI plug-in `ibmcloud ob` and the `v2/observe` endpoints are deprecated and support ends on 28 March 2025. You can now manage your logging and monitoring integrations from the console or through the Helm charts.

## Determining if you need to migrate
{: #migrate-check}

Check if your clusters are using the deprecated agent.

1. Run the following command. If you a logging config is returned, you must migrate your existing Log Analysis and Activity Tracker instances to Cloud Logs instances.
    ```sh
    ibmcloud ob logging config ls --cluster <cluster>
    ```
    {: pre}

1. The Cloud Logs service has provided migration guides for moving your instances. For more information, see [Migrating instances](/docs/cloud-logs?topic=cloud-logs-migration-intro).


## Enabling your clusters to use your Cloud Logs instance
{: #migrate-cloud-logs-clusters}

After you’ve migrated your Log Analysis and Activity Tracker instances to Cloud Logs, you must migrate your clusters to use the new instances.

You can migrate your clusters from the Console or by using the CLI.

### Enabling Cloud Logs in the console
{: #cloud-logs-console-enable}


1. From the cluster dashboard, disable **Log Analysis** and **Activity Tracker**.
1. Enable the **Cloud Logs** integration.

### Enabling Cloud Logs in the CLI
{: #cloud-logs-cli-enable}


1. Delete your deprecated logging config.

    ```sh
    ibmcloud ob logging config delete --cluster INSTANCE --instance INSTANCE
    ```
    {: pre}


1. Enable the Cloud Logs Helm chart in your cluster. For more information, see the following links
    - [Deploying the Logging agent for OpenShift clusters using a Helm chart](/docs/cloud-logs?topic=cloud-logs-agent-helm-os-deploy).
    - [Deploying the Logging agent for Kubernetes clusters using a Helm chart](/docs/cloud-logs?topic=cloud-logs-agent-helm-kube-deploy).

## Migrating to the new monitoring agent
{: #monitoring}

Because the `ibmcloud ob` plug-in is deprecated, if you have a monitoring agent installed that used the deprecated plug-in, you must migrate to a new agent.

1. Check whether you need to migrate by running the following command.
    ```sh
    ibmcloud ob monitoring config ls --cluster <cluster>
    ```
    {: pre}

1. Delete the monitoring config.
    ```sh
    ibmcloud ob monitoring config delete --cluster INSTANCE --instance INSTANCE
    ```
    {: pre}

1. Install the new monitoring agent. For more information, see the following links.
    - [Working with the Kubernetes agent](/docs/monitoring?topic=monitoring-agent_Kube).
    - [Working with the Red Hat OpenShift agent](/docs/monitoring?topic=monitoring-agent_openshift).
