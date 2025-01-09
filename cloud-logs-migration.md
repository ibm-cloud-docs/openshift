---

copyright:
  years: 2025, 2025
lastupdated: "2025-01-09"

keywords: logging, cloud logs, logs, log analysis, containers

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Migrating your {{site.data.keyword.openshiftlong_notm}} clusters to Cloud Logs
{: #cloud-logs-migration}

Log Analysis and Activity Tracker are deprecated and support ends on 28 March 2025. For more details about the deprecation, including migration steps, see [Migrating to Cloud Logs](/docs/log-analysis?topic=log-analysis-deprecation_migration).
{: deprecated}

## Migrating to Cloud Logs
{: #migration-cloud-logs}

You need to migrate if your clusters are using the deprecated logging agent.

### Determining if you need to migrate
{: #migrate-check}

1. Check if your clusters are using the deprecated agent.

    ```sh
    ibmcloud ob logging config ls --cluster <cluster>
    ```
    {: pre}

1. If you have the deprecated logging agent installed in your cluster, migrate your existing Log Analysis and Activity Tracker instances to Cloud Logs instances.

The Cloud Logs service has provided migration guides for moving your instances to Cloud Logs. For more information, see [Migrating instances](/docs/cloud-logs?topic=cloud-logs-migration-intro).


### Enabling your clusters to use your Cloud Logs instance
{: #migrate-cloud-logs-clusters}

After you’ve migrated your Log Analysis and Activity Tracker instances to Cloud Logs, you must migrate your clusters to use the new instances.

You can migrate your clusters from the Console or by using the CLI.

#### Enabling Cloud Logs in the console
{: #cloud-logs-console-enable}
{: ui}


1. From the cluster dashboard, disable Log Analysis.
1. Enable the Cloud Logs integration via the UI.

#### Enabling Cloud Logs in the CLI
{: #cloud-logs-cli-enable}
{: cli}

1. Delete your logging config.

    ```sh
    ic ob logging config delete --cluster INSTANCE --instance INSTANCE
    ```
    {: pre}


1. Enable the Cloud Logs Helm chart in your cluster. For more information, see the following links
    - [Deploying the Logging agent for OpenShift clusters using a Helm chart](/docs/cloud-logs?topic=cloud-logs-agent-helm-os-deploy).
    - [Deploying the Logging agent for Kubernetes clusters using a Helm chart](/docs/cloud-logs?topic=cloud-logs-agent-helm-kube-deploy).

## Migrating to the new monitoring agent
{: #monitoring}

1. Check whether you need to migrate by running the following command.
    ```sh
    ibmcloud ob monitoring config ls --cluster <cluster>
    ```
    {: pre}

1. Delete the monitoring config.
    ```sh
    ic ob monitoring config delete --cluster INSTANCE --instance INSTANCE
    ```
    {: pre}

1. Install the new monitoring agent. For more information, see the following links.
    - [Working with the Kubernetes agent](/docs/monitoring?topic=monitoring-agent_Kube).
    - [Working with the Red Hat OpenShift agent](/docs/monitoring?topic=monitoring-agent_openshift).



## What else do I need to know?
{: #ob-plugin-dep}

The observability CLI plug-in `ibmcloud ob` and the `v2/observe` endpoints are deprecated and support ends on 28 March 2025. You can now manage your Cloud Logs integrations from the cluster dashboard or from the Helm chart.
