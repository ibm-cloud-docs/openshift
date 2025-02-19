---

copyright: 
  years: 2025, 2025
lastupdated: "2025-02-19"


keywords: openshift

subcollection: openshift, logging, refresh, tags

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I connect Cloud Logs to my cluster?
{: #ts-cloud-logs-refresh}


You can't connect your Cloud Logs instance to your cluster or you can't view the logs for your Cluster in the Cloud Logs instance.
{: tsSymptoms}

When you connect Cloud Logs to your cluster, a Schematics workspace is created to manage your instance. Don't delete this workspace. Deleting this workspace can cause you to not be able to view Cloud Logs or not be able to connect your instance.
{: tsCauses}

To resolve this issue, complete the following steps.
{: tsResolve}

1. In the console, review the [tags on your cluster](https://cloud.ibm.com/containers/cluster-management/clusters){: external}.

1. Delete the tags related to your Cloud Logs instance and Schematic workspace. For example: `logging-workspace:$workspaceId` and `logging-instance:${loggingInstanceId}`.

1. After deleting the tags, retry connecting to Cloud Logs.

1. If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.

