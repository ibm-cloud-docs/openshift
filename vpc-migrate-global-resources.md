---

copyright:
  years: 2026, 2026
lastupdated: "2026-10-29"

keywords: openshift, classic, vpc, migrate, global resources, IAM policies, add-ons, clusterMigrationStatus

subcollection: openshift

content-type: howto

---

{{site.data.keyword.attribute-definition-list}}

# Monitor global resource migration
{: #vpc-migrate-global-resources}

[Classic infrastructure]{: tag-classic-inf}

After the VPC cluster is created and all worker nodes reach `normal` state, the migration service automatically runs background sub-operations for policy migration, add-on migration, and global resources migration. Monitor these sub-operations until all complete, then review any flagged items that require your attention before proceeding to workload migration.
{: shortdesc}

## Before you begin
{: #vpc-migrate-global-prereqs}

- The VPC cluster is provisioned and in `normal` state. See [Create the VPC cluster](/docs/openshift?topic=openshift-vpc-migrate-create).
- [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

## What is migrated automatically
{: #vpc-migrate-global-auto}

The migration service runs the following sub-operations automatically after cluster creation completes:

| Sub-operation | What it does |
|---------------|-------------|
| **Policy migration** | Migrates IAM policies, trusted profiles, tags, and context-based restriction (CBR) rules. |
| **Add-on migration** | Migrates the `cluster-autoscaler`, `image-key-synchronizer`, and `static-route` add-ons to the VPC cluster. The `vpc-file-csi-driver` add-on is enabled by default on the VPC cluster. |
| **Global resources migration** | Migrates the NodeLocal DNS Cache ConfigMap, the CoreDNS and DNS Operator configuration, the Kubernetes Metrics Server ConfigMap, the Ingress controller configuration, and MTU settings. |
{: caption="Automatic migration sub-operations" caption-side="bottom"}

## Monitor migration status
{: #vpc-migrate-global-monitor}

Monitor each sub-operation until it shows `completed`. If any sub-operation shows `failed`, see [Troubleshoot a failed sub-operation](#vpc-migrate-global-troubleshoot) before proceeding.

### From the console
{: #vpc-migrate-global-monitor-ui}
{: ui}

1. After clicking **Create** in the cluster creation form, return to the migration wizard. Go to **Migration hub** > **Clusters** > **Eligible clusters**, or go to **Containers** > **Clusters**, and open the wizard for your Classic cluster.
2. In the migration wizard, navigate to the **Create** step in the left navigation panel.
3. Monitor the sub-operation status indicators for **Policy migration**, **Add-on migration**, and **Global resources migration**. Each sub-operation shows its current status.
4. When all sub-operations show a checkmark, the **Create** step is complete. Navigate to the **Migrate** step to proceed with workload migration.

If any sub-operation shows an error, expand it for details and see [Troubleshoot a failed sub-operation](#vpc-migrate-global-troubleshoot).
{: tip}

### From the CLI
{: #vpc-migrate-global-monitor-cli}
{: cli}

1. Run the following command every 60 seconds until all sub-operations report `completed`. If any report `failed`, see [Troubleshoot a failed sub-operation](#vpc-migrate-global-troubleshoot).

   ```sh
   ibmcloud oc replatform cluster get --cluster-id CLASSIC_CLUSTER_ID
   ```
   {: pre}

   Example output (all completed):
   ```text
   Sub-operation                  Status       Message
   policy-migration               completed    Policy migration complete.
   addon-migration                completed    Add-on migration complete.
   global-resources-migration     completed    Global resources migration complete.
   ```
   {: screen}

   Each sub-operation reports one of the following statuses: `pending`, `in_progress`, `completed`, or `failed`. Do not proceed to the Migrate step until all report `completed`.

### From the API
{: #vpc-migrate-global-monitor-api}
{: api}

1. Poll the `clusterMigrationStatus` query every 60 seconds until all `status` fields return `completed`. If any return `failed`, see [Troubleshoot a failed sub-operation](#vpc-migrate-global-troubleshoot).

   ```graphql
   query MigrationStatus($id: ID!) {
     node(id: $id) {
       ... on KubernetesCluster {
         vpcMigration {
           clusterMigrationStatus {
             policyMigrationStatus          { status message errorMessage }
             addonMigrationStatus           { status message errorMessage }
             globalResourcesMigrationStatus {
               status message errorMessage
               additionalDetails { key value }
             }
           }
         }
       }
     }
   }
   ```
   {: codeblock}

   ```json
   { "id": "CLASSIC_CLUSTER_ID" }
   ```
   {: codeblock}

   Example response (all completed):
   ```json
   {
     "data": {
       "node": {
         "vpcMigration": {
           "clusterMigrationStatus": {
             "policyMigrationStatus":          { "status": "completed", "message": "Policy migration complete.",          "errorMessage": null },
             "addonMigrationStatus":           { "status": "completed", "message": "Add-on migration complete.",          "errorMessage": null },
             "globalResourcesMigrationStatus": { "status": "completed", "message": "Global resources migration complete.", "errorMessage": null, "additionalDetails": [] }
           }
         }
       }
     }
   }
   ```
   {: screen}

   Each sub-operation reports a `status` of `pending`, `in_progress`, `completed`, or `failed`. Do not proceed to the Migrate step until all return `completed`.

## Understanding network policy migration
{: #vpc-migrate-global-network-policies}

The policy migration sub-operation does not migrate network policies. It migrates only IAM policies, trusted profiles, tags, and CBR rules.

- Global Network Policies (GNPs) are not migrated. Moving them to VPC security groups is your responsibility.
- Namespace-scoped Kubernetes and Calico network policies are migrated as is during the workload migration step. See [Which network policies are migrated?](/docs/openshift?topic=openshift-vpc-migrate-overview#vpc-migrate-overview-limitations-networking).

## Troubleshoot a failed sub-operation
{: #vpc-migrate-global-troubleshoot}

If a sub-operation reports `failed`, review the error details and resolve the issue before retrying.

| Error | Resolution |
|-------|-----------|
| Add-on not compatible with VPC | Remove the incompatible add-on from the Classic cluster and re-trigger add-on migration. |
| IAM permission error | The migration service uses the API key associated with your account. Ensure that API key has **Administrator** IAM platform access to the resource group that contains the Classic and VPC clusters. |
{: caption="Common migration sub-operation errors" caption-side="bottom"}

### From the console
{: #vpc-migrate-global-troubleshoot-ui}
{: ui}

1. On the VPC cluster overview page, click the **Add-on status** tile if it shows an error.
2. Review the error details displayed. Resolve the issue indicated.
3. Reopen the migration wizard. Go to **Migration hub** > **Clusters** > **Eligible clusters**, or go to **Containers** > **Clusters**, and open the wizard for your Classic cluster.
4. On the **Create** step, the failed sub-operation is highlighted. Click **Retry** next to the failed sub-operation to re-trigger it.
5. Monitor the status until the sub-operation shows as complete before proceeding.

### From the CLI
{: #vpc-migrate-global-troubleshoot-cli}
{: cli}

1. Check which sub-operation failed and review the error message.

   ```sh
   ibmcloud oc replatform cluster get --cluster-id CLASSIC_CLUSTER_ID
   ```
   {: pre}

   Example output showing a failure:
   ```text
   Sub-operation                  Status       Message
   policy-migration               failed       [VERIFY: example error message]
   addon-migration                completed    Add-on migration complete.
   global-resources-migration     completed    Global resources migration complete.
   ```
   {: screen}

2. Resolve the issue, then re-trigger the failed sub-operation using the API or console — CLI retry is not available in this release. See [From the API](#vpc-migrate-global-troubleshoot-api) below.

3. Run the status command again every 60 seconds until all sub-operations report `completed`.

   ```sh
   ibmcloud oc replatform cluster get --cluster-id CLASSIC_CLUSTER_ID
   ```
   {: pre}

   Example output (all completed):
   ```text
   Sub-operation                  Status       Message
   policy-migration               completed    Policy migration complete.
   addon-migration                completed    Add-on migration complete.
   global-resources-migration     completed    Global resources migration complete.
   ```
   {: screen}

### From the API
{: #vpc-migrate-global-troubleshoot-api}
{: api}

1. Query the migration status to identify which sub-operation failed and read its `errorMessage`.

   ```graphql
   query MigrationStatus($id: ID!) {
     node(id: $id) {
       ... on KubernetesCluster {
         vpcMigration {
           clusterMigrationStatus {
             policyMigrationStatus          { status message errorMessage }
             addonMigrationStatus           { status message errorMessage }
             globalResourcesMigrationStatus { status message errorMessage additionalDetails { key value } }
           }
         }
       }
     }
   }
   ```
   {: codeblock}

   ```json
   { "id": "CLASSIC_CLUSTER_ID" }
   ```
   {: codeblock}

2. Resolve the issue, then call the `retryMigrationSubOperation` mutation to re-trigger the failed sub-operation. Replace `OPERATION_NAME` with one of: `policy-migration`, `addon-migration`, or `global-resources-migration`.

   ```graphql
   mutation RetrySubOp($input: RetryMigrationSubOperationInput!) {
     retryMigrationSubOperation(input: $input) {
       message status
     }
   }
   ```
   {: codeblock}

   ```json
   {
     "input": {
       "clusterID":     "CLASSIC_CLUSTER_ID",
       "operationName": "OPERATION_NAME"
     }
   }
   ```
   {: codeblock}

   Example response:
   ```json
   {
     "data": {
       "retryMigrationSubOperation": {
         "message": "Sub-operation 'policy-migration' re-triggered successfully.",
         "status": "in_progress"
       }
     }
   }
   ```
   {: screen}

3. Poll `clusterMigrationStatus` again every 60 seconds until all sub-operations return `completed`.

Your Classic cluster is not affected by a failed sub-operation and continues to serve traffic. If retrying a sub-operation does not resolve the issue, open a support case. Include the `errorMessage` value from the `clusterMigrationStatus` query and your Classic cluster ID so that IBM Support can investigate.
{: note}

## Next steps
{: #vpc-migrate-global-next}

[Migrate workloads](/docs/openshift?topic=openshift-vpc-migrate-workloads)
