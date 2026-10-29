---

copyright:
  years: 2026, 2026
lastupdated: "2026-10-29"

keywords: openshift, classic, vpc, migrate, workloads, migration plan, createMigrationPlan, startWorkloadMigration, BRS, storage class

subcollection: openshift

content-type: howto

---

{{site.data.keyword.attribute-definition-list}}

# Migrate workloads
{: #vpc-migrate-workloads}

[Classic infrastructure]{: tag-classic-inf}

Create a workload migration plan for your selected namespaces, review it for items that require your action, then start the migration to move your application workloads and persistent storage to the VPC cluster.
{: shortdesc}

## Before you begin
{: #vpc-migrate-workloads-prereqs}

- You must have at least the **Operator** (`containers-kubernetes.cluster.operate`) {{site.data.keyword.iamlong}} platform access role for {{site.data.keyword.openshiftlong_notm}} on both the Classic cluster and the VPC cluster. See [Assigning cluster access](/docs/openshift?topic=openshift-iam-platform-access-roles).
- A worker pool for the BRS connectors exists on the Classic cluster. A VPC cluster has one by default unless you disabled it when you created the cluster. See [Preparing a worker pool for BRS connectors](#vpc-migrate-workloads-prereqs-brs-pool).
- All infrastructure migration sub-operations are `completed`. See [Monitor global resource migration](/docs/openshift?topic=openshift-vpc-migrate-global-resources).
- [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

## Workload migration prerequisites
{: #vpc-migrate-workloads-prereqs-workload}

Before creating a migration plan, address the following prerequisites to avoid failures during migration.

VPC quota limits
:   All [VPC quotas and service limits](/docs/vpc?topic=vpc-quotas){: external} apply to the resources that the migration creates. Review the quotas for all VPC resource types that your workloads use. If your workloads would exceed any limit, [open a support ticket](https://cloud.ibm.com/unifiedsupport/cases/add){: external} to request a quota increase before you start migration.

Cluster-scoped resource migration
:   Cluster-scoped resources (such as custom `ClusterRole`, `ClusterRoleBinding`, custom `SecurityContextConstraints`, `PriorityClass`, `CustomResourceDefinition`, and admission webhooks) are not included in automated namespace-scoped migration plans. Review, export, and apply any required cluster-scoped resources to the VPC cluster before you migrate dependent namespaces. For step-by-step instructions, see [Migrating cluster-scoped resources](#vpc-migrate-workloads-cluster-scoped).

Worker pool for BRS connectors
:   Configure a worker pool on your cluster for the {{site.data.keyword.cloud_notm}} Backup and Recovery Service (BRS) connectors. You can create a dedicated worker pool or use an existing worker pool, and apply the required label and optional taint. This step is required for Classic clusters. For VPC clusters, this step is required only if the BRS worker pool was not created during cluster creation. See [Preparing a worker pool for BRS connectors](#vpc-migrate-workloads-prereqs-brs-pool).

IAM permissions
:   You must have at least the **Operator** (`containers-kubernetes.cluster.operate`) {{site.data.keyword.iamlong}} platform access role for {{site.data.keyword.openshiftlong_notm}} on both the Classic cluster and the VPC cluster. If you do not have this role on the target VPC cluster, the migration wizard displays an *IAM Operator role access required* warning message when you attempt to create a migration plan. For more information, see [Assigning cluster access](/docs/openshift?topic=openshift-iam-platform-access-roles).

## Preparing a worker pool for BRS connectors
{: #vpc-migrate-workloads-prereqs-brs-pool}

The {{site.data.keyword.cloud_notm}} Backup and Recovery Service (BRS) connectors run on a labeled worker pool in your cluster. You can create a new dedicated worker pool or configure an existing worker pool.

- **Classic clusters:** Complete these steps.
- **VPC clusters:** When you create a VPC cluster, the BRS worker pool (`BRS_Workerpool`) is created by default. If you kept the default, you do not need to create, label, or taint a worker pool, and you can skip these steps. Complete these steps only if you disabled the BRS worker pool when you created the cluster and you later decide to use BRS.

### Option 1: Create a dedicated worker pool (recommended)
{: #vpc-migrate-brs-pool-dedicated}

1. Create a dedicated worker pool for the BRS connectors. [VERIFY: minimum worker pool size and flavor requirements for the BRS connectors.]

   - On a Classic cluster:
     ```sh
     ibmcloud oc worker-pool create classic --cluster CLASSIC_CLUSTER_NAME_OR_ID --name BRS_WORKER_POOL_NAME --flavor FLAVOR --size-per-zone SIZE_PER_ZONE
     ```
     {: pre}

     For more information, see [`ibmcloud oc worker-pool create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-create-classic-cli).

   - On a VPC cluster:
     ```sh
     ibmcloud oc worker-pool create vpc-gen2 --cluster VPC_CLUSTER_NAME_OR_ID --name BRS_WORKER_POOL_NAME --flavor FLAVOR --size-per-zone SIZE_PER_ZONE --vpc-id VPC_ID --subnet-id SUBNET_ID
     ```
     {: pre}

     For more information, see [`ibmcloud oc worker-pool create vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-create-vpc-gen2-cli).

2. Label the worker pool with `brs-workload=true`:

   ```sh
   ibmcloud oc worker-pool label set \
     --cluster CLUSTER_NAME_OR_ID \
     --worker-pool BRS_WORKER_POOL_NAME_OR_ID \
     --label brs-workload=true
   ```
   {: pre}

3. Taint the worker pool with `brs-workload=true:NoSchedule` to prevent other workloads from being scheduled on it:

   ```sh
   ibmcloud oc worker-pool taint set \
     --cluster CLUSTER_NAME_OR_ID \
     --worker-pool BRS_WORKER_POOL_NAME_OR_ID \
     --taint brs-workload=true:NoSchedule
   ```
   {: pre}

### Option 2: Use an existing worker pool
{: #vpc-migrate-brs-pool-existing}

If you do not want to create a dedicated worker pool, you can use any existing worker pool on your cluster to run the BRS connectors.

1. Add the required label to the chosen worker pool:

   ```sh
   ibmcloud oc worker-pool label set \
     --cluster CLUSTER_NAME_OR_ID \
     --worker-pool WORKER_POOL_NAME_OR_ID \
     --label brs-workload=true
   ```
   {: pre}

2. (Optional) If you want to reserve this worker pool exclusively for BRS connectors, taint the worker pool:

   ```sh
   ibmcloud oc worker-pool taint set \
     --cluster CLUSTER_NAME_OR_ID \
     --worker-pool WORKER_POOL_NAME_OR_ID \
     --taint brs-workload=true:NoSchedule
   ```
   {: pre}

   Adding this taint restricts other workloads from being scheduled on that worker pool unless they explicitly tolerate the taint.
   {: note}

## Step 1: Select a backup and recovery instance
{: #vpc-migrate-workloads-brs}

Select the {{site.data.keyword.cloud_notm}} Backup and Recovery Service (BRS) instance that is used to back up and restore workload data during migration.

If you need to change your BRS instance or clean up BRS artifacts from a cluster that was previously registered to another BRS instance, see [Cleaning up Backup and Recovery Service registrations](#vpc-migrate-workloads-brs-cleanup).
{: tip}

### From the console
{: #vpc-migrate-workloads-brs-ui}
{: ui}

1. In the migration wizard, navigate to the **Migrate** step in the left navigation panel.
2. On the **Migrate workloads** page, under **Backup and recovery**, confirm or change the **Backup and recovery instance** shown. Click the edit icon to select a different instance if needed.
3. If you do not yet have a BRS instance, click **Create a BRS instance** to provision one. The provisioning page opens outside the wizard — after provisioning completes, return to the wizard and refresh the page to continue. You cannot switch BRS instances after migration has started.
4. Review the **Namespaces migrated** progress bar and the **Source cluster** link to confirm you are migrating from the correct cluster.

### From the CLI
{: #vpc-migrate-workloads-brs-cli}
{: cli}

Record your BRS instance ID from your account. You need to pass it as `--backup-recovery-instance-id BRS_INSTANCE_ID` in step 5.

To find your BRS instance ID, run the following command:

```sh
ibmcloud resource service-instances --service-name backup-recovery --output json | jq '.[].guid'
```
{: pre}

Example output:
```text
"a1b2c3d4-e5f6-7890-abcd-ef1234567890"
```
{: screen}

### From the API
{: #vpc-migrate-workloads-brs-api}
{: api}

Record your BRS instance ID from your account. You need to pass it as `brsInstanceID` in the `startWorkloadMigration` mutation in step 5.

To find your BRS instance ID, run the following command:

```sh
ibmcloud resource service-instances --service-name backup-recovery --output json | jq '.[].guid'
```
{: pre}

Example output:
```text
"a1b2c3d4-e5f6-7890-abcd-ef1234567890"
```
{: screen}

## Step 2: List namespaces
{: #vpc-migrate-workloads-namespaces}

Before selecting namespaces, review [Workload migration prerequisites](#vpc-migrate-workloads-prereqs-workload) to ensure your cluster is ready.

Identify the namespaces that contain the workloads you want to migrate. System namespaces (`kube-system`, `ibm-system`, `calico-system`, and others) are excluded automatically. A single migration plan can include up to 20 namespaces.

### From the console
{: #vpc-migrate-workloads-ns-ui}
{: ui}

The namespace list is displayed in the **Select namespaces** step inside the **Create plan then migrate** side panel. You can filter by **Migration status** and search by name to locate specific namespaces. Each row shows three columns: **Namespace**, **Migration status**, and **Label**.

No separate action is required — proceed to step 3 to open the side panel and select namespaces there.

### From the CLI
{: #vpc-migrate-workloads-ns-cli}
{: cli}

1. List all namespaces on your Classic cluster to identify which ones to include:

   ```sh
   oc get namespaces
   ```
   {: pre}

   Example output:
   ```text
   NAME              STATUS   AGE
   default           Active   210d
   monitoring        Active   182d
   production        Active   190d
   staging           Active   185d
   ```
   {: screen}

   Note the names of the application namespaces to include. You pass these to the plan creation command in step 3.

### From the API
{: #vpc-migrate-workloads-ns-api}
{: api}

Increase `offset` in increments of `limit` to page through all namespaces. The maximum `limit` is 100.
{: note}

1. Submit the query to list namespaces and identify which to include:

   ```graphql
   query ListNS($id: ID!) {
     node(id: $id) {
       ... on KubernetesCluster {
         vpcMigration {
           listNamespaces(limit: 50, offset: 0) {
             total
             items { name status }
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

   Example response:
   ```json
   {
     "data": {
       "node": {
         "vpcMigration": {
           "listNamespaces": {
             "total": 4,
             "items": [
               { "name": "default",    "status": "Active" },
               { "name": "monitoring", "status": "Active" },
               { "name": "production", "status": "Active" },
               { "name": "staging",    "status": "Active" }
             ]
           }
         }
       }
     }
   }
   ```
   {: screen}

   Note the namespace names to include. You pass these to the `createMigrationPlan` mutation in step 3.

Migration plans cannot be saved. If you generate a plan and close the side panel without proceeding to migrate, the plan is lost. Complete the plan creation and migration in a single session.
{: important}

## Step 3: Create a migration plan
{: #vpc-migrate-workloads-plan}

A migration plan maps the namespace configuration changes from Classic to VPC, including the storage class mappings that the migration service provides, load balancer type changes, and Ingress host mappings. You can create multiple plans, each covering up to 20 namespaces. Plan creation is asynchronous.

### From the console
{: #vpc-migrate-workloads-plan-ui}
{: ui}

The **Create plan then migrate** side panel has three steps: **Select namespaces**, **Storage class mapping**, and **Network mapping**.

1. On the **Migrate workloads** page, click **Create plan**. The **Create plan then migrate** side panel opens at the **Select namespaces** step.
2. Select up to 20 namespaces to include. The table shows three columns: **Namespace**, **Migration status**, and **Label**. Use the **Migration status** filter and search bar to narrow the list.
   - Namespaces that are part of another migration plan already in progress cannot be selected. Their **Migration status** shows **In progress** and the selection checkbox is disabled.
3. Click **Next**. The side panel advances to the **Storage class mapping** step.

   One of the following scenarios applies based on whether PVCs were detected:

   - **No PVCs detected**: No storage class mappings are required. Click **Next** to continue to the **Network mapping** step.
   - **PVCs detected**: The migration service provides the storage class mapping. The closest matching VPC storage class is selected by default for each Classic storage class. You can choose a different tier from the VPC class list or select from mappings used in previous plans. The table shows two columns: **Classic** and **VPC** (with a dropdown selector).

4. Review or adjust the storage class mappings and click **Next**. The side panel advances to the **Network mapping** step.
5. Review how Classic network resources map to VPC equivalents. The table shows two columns: **Namespace** and **Application load balancer quota**.
    - All [VPC quotas](/docs/vpc?topic=vpc-quotas){: external} apply to the resources that the migration creates.
    - If your plan would exceed any quota limit, you must [open a support ticket](https://cloud.ibm.com/unifiedsupport/cases/add){: external} to request a quota increase before migrating, or the affected resources will remain `pending` until the quota is extended.
6. Optionally, click **Download plan** to save a detailed JSON file listing all recommended actions.
7. Click **Migrate** to start the workload migration.

### From the CLI
{: #vpc-migrate-workloads-plan-cli}
{: cli}

1. Create the migration plan for your selected namespaces. Replace `CLASSIC_CLUSTER_ID` with your Classic cluster ID and the `--namespace` values with your application namespace names. Save the plan ID from the output — you need it in subsequent steps.

   ```sh
   ibmcloud oc replatform workload-plan create --cluster-id CLASSIC_CLUSTER_ID \
     --namespace production \
     --namespace staging \
     --namespace monitoring
   ```
   {: pre}

   Example output:
   ```text
   OK
   Migration plan created.
   Migration plan ID: a1b2c3d4-e5f6-7890-abcd-ef1234567890
   Status: MIGRATION_PLAN_IN_PROGRESS
   ```
   {: screen}

2. Check the plan status periodically until it shows `MIGRATION_PLAN_COMPLETED`.

   ```sh
   ibmcloud oc replatform workload-plan get --cluster-id CLASSIC_CLUSTER_ID --migration-plan-id PLAN_ID
   ```
   {: pre}

   Example output:
   ```text
   Migration plan ID: a1b2c3d4-e5f6-7890-abcd-ef1234567890
   Status: MIGRATION_PLAN_COMPLETED
   Namespaces: production, staging, monitoring
   User-action items: 2
   ```
   {: screen}

### From the API
{: #vpc-migrate-workloads-plan-api}
{: api}

1. Submit the `createMigrationPlan` mutation. Replace the `namespaces` values with your application namespace names. Save the `migrationPlanID` from the response — you need it in subsequent steps.

   ```graphql
   mutation CreatePlan($input: CreateMigrationPlanInput!) {
     createMigrationPlan(input: $input) {
       migrationPlanID clusterID region message
     }
   }
   ```
   {: codeblock}

   ```json
   {
     "input": {
       "clusterID":  "CLASSIC_CLUSTER_ID",
       "namespaces": ["production", "staging", "monitoring"]
     }
   }
   ```
   {: codeblock}

   Example response:
   ```json
   {
     "data": {
       "createMigrationPlan": {
         "migrationPlanID": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
         "clusterID": "CLASSIC_CLUSTER_ID",
         "region": "us-south",
         "message": "Migration plan creation initiated."
       }
     }
   }
   ```
   {: screen}

2. Plan creation is asynchronous. Poll until `state` is `MIGRATION_PLAN_COMPLETED`:

   ```graphql
   query GetPlan($id: ID!, $planID: String!) {
     node(id: $id) {
       ... on KubernetesCluster {
         vpcMigration {
           migrationPlan(migrationPlanID: $planID) {
             migrationPlanID state
             plan {
               id
               namespaces {
                 name
                 networking {
                   loadBalancers {
                     name
                     loadBalancerTypeMappings { classic vpc }
                     notes { description isUserActionRequired }
                   }
                   ingressObjs {
                     name
                     hosts { type hostMappings { classic vpc } }
                     notes { description isUserActionRequired }
                   }
                   nodePorts { name notes { description isUserActionRequired } }
                 }
               }
               storage {
                 name
                 storageClassNameMappings { classic vpc }
                 notes { description isUserActionRequired }
               }
             }
           }
         }
       }
     }
   }
   ```
   {: codeblock}

   ```json
   {
     "id": "CLASSIC_CLUSTER_ID",
     "planID": "MIGRATION_PLAN_ID"
   }
   ```
   {: codeblock}

   Example response:
   ```json
   {
     "data": {
       "node": {
         "vpcMigration": {
           "migrationPlan": {
             "migrationPlanID": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
             "state": "MIGRATION_PLAN_COMPLETED",
             "plan": {
               "id": "plan-001",
               "namespaces": [
                 {
                   "name": "production",
                   "networking": {
                     "loadBalancers": [
                       {
                         "name": "my-app-lb",
                         "loadBalancerTypeMappings": { "classic": "NLB", "vpc": "ALB" },
                         "notes": [{ "description": "Load balancer type will change from NLB to ALB.", "isUserActionRequired": true }]
                       }
                     ]
                   }
                 }
               ],
               "storage": [
                 {
                   "name": "my-app-pvc",
                   "storageClassNameMappings": { "classic": "ibmc-block-gold", "vpc": "ibmc-vpc-block-10iops-tier" },
                   "notes": []
                 }
               ]
             }
           }
         }
       }
     }
   }
   ```
   {: screen}

## Step 4: Review the migration plan
{: #vpc-migrate-workloads-review-plan}

Before starting the migration, review the plan for items that require your action. Resolve all required items before proceeding — the migration will not succeed while unresolved items exist.

Common user-action items include:

| Item | What to do |
|------|-----------|
| Load balancer type change (NLB → ALB or vice versa) | Confirm the proposed type mapping or update the Service annotation on the VPC cluster. To enable source IP preservation on VPC, annotate the Service with `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: nlb`. See [VPC load balancer annotations](/docs/openshift?topic=openshift-vpc-lbaas#vpc_lb_annotations). |
| Ingress host mapping | Confirm the VPC Ingress subdomain mapping is correct. Update external DNS at cutover. |
| Storage class not mapped | Confirm or override the storage class mapping in step 5. |
| Security group rule limit warning | Consolidate security group rules before proceeding. |
{: caption="Common migration plan user-action items" caption-side="bottom"}

### From the console
{: #vpc-migrate-workloads-review-ui}
{: ui}

The storage class and network mapping steps in the **Create plan then migrate** side panel serve as the review interface. In **Step 2 — Storage class mapping**, review the Classic-to-VPC storage class assignments. In **Step 3 — Network mapping**, review load balancer and Ingress mappings and address any quota warnings before clicking **Migrate**.

### From the CLI
{: #vpc-migrate-workloads-review-cli}
{: cli}

1. Retrieve the full plan details and review each namespace for user-action items. Replace `PLAN_ID` with the migration plan ID from step 3.

   ```sh
   ibmcloud oc replatform workload-plan get --cluster-id CLASSIC_CLUSTER_ID --migration-plan-id PLAN_ID --output json
   ```
   {: pre}

   Scan the output for any entries where `isUserActionRequired` is `true`. These must be resolved before starting the migration.

2. For each PVC in the plan, review the `storageClassNameMappings` entries to verify that the storage class mapping that the migration service provides is correct.

   To override a mapping, pass `--storage-class-mapping classic-class=vpc-class` when you run `replatform workload-plan migrate` in step 5.

### From the API
{: #vpc-migrate-workloads-review-api}
{: api}

1. Review the `plan` object returned by the `GetPlan` query from step 3. For each namespace, check the `notes` arrays on `loadBalancers`, `ingressObjs`, `nodePorts`, and `storage` entries. Any note with `"isUserActionRequired": true` must be resolved before starting the migration.

2. Review the `storageClassNameMappings` for each storage entry in the plan. To override a mapping, pass your custom values in the `storageClassMapping` field of the `startWorkloadMigration` mutation in step 5.

## Step 5: Start workload migration
{: #vpc-migrate-workloads-start}

After you have reviewed the plan and resolved all user-action items, start the workload migration.

Workload migration cannot be stopped once it is started. If issues arise during migration, do not delete the Classic cluster — the Classic cluster remains fully operational throughout and continues serving traffic. You can roll back at cutover by keeping DNS pointed at the Classic cluster.
{: important}

### From the console
{: #vpc-migrate-workloads-start-ui}
{: ui}

1. In the **Network mapping** step of the **Create plan then migrate** side panel, click **Migrate** to start the workload migration.
2. The side panel closes. The **Migrate workloads** page displays the new plan in the migration plans table with a status of **In progress**.
3. Monitor the **Namespaces migrated** progress bar and the **Migration status** column. Each plan row shows its namespace count and current status.
4. Click **View details** on a table row to open the **Migration plan details** panel, where you can:
   - Download the detailed migration plan in JSON format.
   - Re-run the migration if a previous attempt failed or was interrupted.

### From the CLI
{: #vpc-migrate-workloads-start-cli}
{: cli}

1. Start the workload migration. Replace `CLASSIC_CLUSTER_ID`, `PLAN_ID`, and `BRS_INSTANCE_ID` with the values from earlier steps. Include `--storage-class-mapping` flags for each PVC where you want to override the default mapping. Omit all `--storage-class-mapping` flags if no PVC migration is needed.

   ```sh
   ibmcloud oc replatform workload-plan migrate \
     --cluster-id CLASSIC_CLUSTER_ID \
     --workload-plan-id PLAN_ID \
     --backup-recovery-instance-id BRS_INSTANCE_ID \
     --storage-class-mapping ibmc-block-gold=ibmc-vpc-block-10iops-tier \
     --storage-class-mapping ibmc-block-silver=ibmc-vpc-block-5iops-tier
   ```
   {: pre}

   Example output:
   ```text
   OK
   Workload migration started.
   Migration plan ID: a1b2c3d4-e5f6-7890-abcd-ef1234567890
   Namespaces: production, staging, monitoring
   Status: in_progress
   ```
   {: screen}

2. Check the migration status periodically until all namespaces show `completed`. Use `replatform workload-plan get` to retrieve the current plan state.

   ```sh
   ibmcloud oc replatform workload-plan get --cluster-id CLASSIC_CLUSTER_ID --migration-plan-id PLAN_ID
   ```
   {: pre}

   Example output:
   ```text
   Namespace     Status       Message
   production    completed    Workload migration complete.
   staging       in_progress  Migrating pods...
   monitoring    completed    Workload migration complete.
   ```
   {: screen}

### From the API
{: #vpc-migrate-workloads-start-api}
{: api}

1. Submit the `startWorkloadMigration` mutation. Replace `CLASSIC_CLUSTER_ID`, `BRS_INSTANCE_ID`, and `MIGRATION_PLAN_ID` with the values from earlier steps. Include `storageClassMapping` overrides for any PVC where you want to change the default mapping. Pass an empty object `{}` to skip PVC migration.

   ```graphql
   mutation StartMigration($input: StartWorkloadMigrationInput!) {
     startWorkloadMigration(input: $input) {
       classicClusterID migrationPlanID region message
     }
   }
   ```
   {: codeblock}

   With storage class mapping overrides:

   ```json
   {
     "input": {
       "clusterID":           "CLASSIC_CLUSTER_ID",
       "brsInstanceID":       "BRS_INSTANCE_ID",
       "migrationPlanID":     "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
       "storageClassMapping": {
         "ibmc-block-gold":      "ibmc-vpc-block-10iops-tier",
         "ibmc-block-silver":    "ibmc-vpc-block-5iops-tier",
         "ibmc-file-bronze-gid": "ibmc-vpc-file-dp2"
       }
     }
   }
   ```
   {: codeblock}

   To skip PVC migration, pass an empty `storageClassMapping` object:

   ```json
   {
     "input": {
       "clusterID":           "CLASSIC_CLUSTER_ID",
       "brsInstanceID":       "BRS_INSTANCE_ID",
       "migrationPlanID":     "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
       "storageClassMapping": {}
     }
   }
   ```
   {: codeblock}

2. Poll the migration status periodically until all namespaces show `completed`.

   ```graphql
   query WorkloadMigrationStatus($id: ID!, $planID: String!) {
     node(id: $id) {
       ... on KubernetesCluster {
         vpcMigration {
           workloadMigrationStatus(migrationPlanID: $planID) {
             migrationPlanID state
             namespaces { name status message }
           }
         }
       }
     }
   }
   ```
   {: codeblock}

   ```json
   {
     "id": "CLASSIC_CLUSTER_ID",
     "planID": "MIGRATION_PLAN_ID"
   }
   ```
   {: codeblock}

   Example response:
   ```json
   {
     "data": {
       "node": {
         "vpcMigration": {
           "workloadMigrationStatus": {
             "migrationPlanID": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
             "state": "in_progress",
             "namespaces": [
               { "name": "production", "status": "completed",   "message": "Workload migration complete." },
               { "name": "staging",    "status": "in_progress", "message": "Migrating pods..." },
               { "name": "monitoring", "status": "completed",   "message": "Workload migration complete." }
             ]
           }
         }
       }
     }
   }
   ```
   {: screen}

## Step 6: Verify workloads
{: #vpc-migrate-workloads-verify}

After the migration completes, verify that all pods are running correctly on the VPC cluster before proceeding to cutover. Any pod in `Error`, `CrashLoopBackOff`, or `Pending` state requires investigation.

### From the console
{: #vpc-migrate-workloads-verify-ui}
{: ui}

1. From the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}, click your VPC cluster.
2. Click **Kubernetes dashboard** to open the cluster console.
3. Navigate to **Workloads** > **Pods** and set the namespace filter to each migrated namespace in turn. Confirm that all pods show a status of **Running** or **Completed**.
4. Click into any pod that shows a non-running status to view its events and logs. Look for image pull errors, configuration issues, or storage mount failures.
5. Return to the migration wizard and confirm the **Migrate** step shows all namespaces as complete before proceeding to the **Cutover** phase.

### From the CLI
{: #vpc-migrate-workloads-verify-cli}
{: cli}

1. Check that all application pods are `Running` or `Completed` across all migrated namespaces:

   ```sh
   oc get pods --all-namespaces
   ```
   {: pre}

   Example output:
   ```text
   NAMESPACE    NAME                          READY   STATUS    RESTARTS   AGE
   production   my-app-6d4b9f7d8-xk2np        1/1     Running   0          5m
   production   my-db-0                        1/1     Running   0          5m
   monitoring   prometheus-5c8d9b7f4-lm3qr     1/1     Running   0          5m
   staging      my-app-7f5c8b9d6-pn4rs         1/1     Running   0          4m
   ```
   {: screen}

2. Check recent logs for errors in each deployment. Look for stack traces, connection refused messages, or repeated restart cycles that indicate a workload did not migrate cleanly. If you see these errors, see [Debugging app deployments](/docs/openshift?topic=openshift-ts-app-01-debug) or [Why is my pod in a CrashLoopBackOff state?](/docs/openshift?topic=openshift-ts-app-container-start).

   ```sh
   oc logs -n NAMESPACE DEPLOYMENT_NAME --tail=100
   ```
   {: pre}

3. Review cluster events for warnings across all namespaces:

   ```sh
   oc get events --all-namespaces --sort-by='.lastTimestamp' | tail -30
   ```
   {: pre}

### From the API
{: #vpc-migrate-workloads-verify-api}
{: api}

1. Use the migration status query to confirm all namespaces in the plan report `completed`.

   ```graphql
   query WorkloadMigrationStatus($id: ID!, $planID: String!) {
     node(id: $id) {
       ... on KubernetesCluster {
         vpcMigration {
           workloadMigrationStatus(migrationPlanID: $planID) {
             migrationPlanID state
             namespaces { name status message }
           }
         }
       }
     }
   }
   ```
   {: codeblock}

   ```json
   {
     "id": "CLASSIC_CLUSTER_ID",
     "planID": "MIGRATION_PLAN_ID"
   }
   ```
   {: codeblock}

   Example response (all complete):
   ```json
   {
     "data": {
       "node": {
         "vpcMigration": {
           "workloadMigrationStatus": {
             "migrationPlanID": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
             "state": "completed",
             "namespaces": [
               { "name": "production", "status": "completed", "message": "Workload migration complete." },
               { "name": "staging",    "status": "completed", "message": "Workload migration complete." },
               { "name": "monitoring", "status": "completed", "message": "Workload migration complete." }
             ]
           }
         }
       }
     }
   }
   ```
   {: screen}

2. Additionally, retrieve pod status directly from the VPC cluster to confirm workloads are running:

   ```sh
   oc get pods --all-namespaces --output json | jq '[.items[] | select(.status.phase != "Running" and .status.phase != "Succeeded") | {namespace: .metadata.namespace, name: .metadata.name, phase: .status.phase}]'
   ```
   {: pre}

   An empty array `[]` confirms all pods are in a running or completed state.

## Re-running a migration
{: #vpc-migrate-workloads-rerun}

If a migration fails or is interrupted, you can re-run it without re-migrating already completed namespaces.

- Migration resumes from where it stopped and processes only the remaining namespaces. Already migrated data is not affected.

### From the console
{: #vpc-migrate-workloads-rerun-ui}
{: ui}

1. On the **Migrate workloads** page, find the plan in the migration plans table.
   - To re-run from the table: click the overflow menu (⋮) at the end of the plan row and select **Re-run migration**.
   - To re-run from the details panel: click **View details** on the plan row, then click **Re-run migration** in the panel.

## Migrating cluster-scoped resources
{: #vpc-migrate-workloads-cluster-scoped}

Non-namespaced objects configured at the cluster level are not automatically migrated by the workload migration service. Before you migrate your namespaces, identify the custom cluster-scoped resources on your Classic cluster, export and sanitize their manifests, and apply them to your target VPC cluster.

### Step 1: Log in to the Classic cluster
{: #vpc-migrate-cluster-scoped-login-classic}

1. Set your CLI context to the source Classic cluster:

   ```sh
   ibmcloud oc cluster config --cluster CLASSIC_CLUSTER_ID_OR_NAME
   ```
   {: pre}

2. Verify that your context points to the Classic cluster:

   ```sh
   oc config current-context
   ```
   {: pre}

### Step 2: Discover cluster-scoped resource types
{: #vpc-migrate-cluster-scoped-discover}

1. List all cluster-scoped resource types available on the cluster (excluding nodes, namespaces, and projects):

   ```sh
   oc api-resources --namespaced=false | grep -vE '^(nodes|namespaces|projects)\s'
   ```
   {: pre}

### Step 3: Identify and export resources
{: #vpc-migrate-cluster-scoped-export}

1. List the resources of the specific types you want to migrate and select the ones required in your target cluster.

   Example commands:
   - View ClusterRoles: `oc get clusterroles`
   - View ClusterRoleBindings: `oc get clusterrolebindings`
   - View PriorityClasses: `oc get priorityclasses`
   - View SecurityContextConstraints (`oc`): `oc get scc`
   - View CustomResourceDefinitions: `oc get crds`
   - View Webhook configurations: `oc get validatingwebhookconfigurations` and `oc get mutatingwebhookconfigurations`

2. Export and sanitize the resource YAML manifest.

   When you export resources, remove runtime and cluster-specific metadata fields (`resourceVersion`, `uid`, `creationTimestamp`, `generation`, `managedFields`, `ownerReferences`, and the `status` block) before applying them to the VPC cluster.

   Choose one of the following methods to export and sanitize your resource manifests:

   - **Option A: Python 3** (built-in on macOS and Linux)

     ```sh
     oc get RESOURCE_TYPE RESOURCE_NAME -o yaml | python3 -c '
     import sys, yaml
     data = yaml.safe_load(sys.stdin)
     for key in ["resourceVersion", "uid", "creationTimestamp", "generation", "managedFields", "ownerReferences"]:
         data.get("metadata", {}).pop(key, None)
     data.pop("status", None)
     print(yaml.dump(data, sort_keys=False))
     ' > RESOURCE_NAME.yaml
     ```
     {: codeblock}

     Example for a custom ClusterRole:
     ```sh
     oc get clusterrole my-custom-role -o yaml | python3 -c '
     import sys, yaml
     data = yaml.safe_load(sys.stdin)
     for key in ["resourceVersion", "uid", "creationTimestamp", "generation", "managedFields", "ownerReferences"]:
         data.get("metadata", {}).pop(key, None)
     data.pop("status", None)
     print(yaml.dump(data, sort_keys=False))
     ' > my-custom-role.yaml
     ```
     {: codeblock}

   - **Option B: `yq` CLI**

     ```sh
     oc get RESOURCE_TYPE RESOURCE_NAME -o yaml | \
       yq eval 'del(.metadata.resourceVersion, .metadata.uid, .metadata.creationTimestamp, .metadata.generation, .metadata.managedFields, .metadata.ownerReferences, .status)' - \
       > RESOURCE_NAME.yaml
     ```
     {: codeblock}

   - **Option C: Manual export and edit**

     ```sh
     oc get RESOURCE_TYPE RESOURCE_NAME -o yaml > RESOURCE_NAME.yaml
     ```
     {: pre}

     Open `RESOURCE_NAME.yaml` in an editor and delete the following runtime fields:
     - `metadata.uid`
     - `metadata.resourceVersion`
     - `metadata.creationTimestamp`
     - `metadata.generation`
     - `metadata.managedFields`
     - `metadata.ownerReferences`
     - `status` (entire section)

### Step 4: Log in to the target VPC cluster
{: #vpc-migrate-cluster-scoped-login-vpc}

1. Switch your CLI context to the target VPC cluster:

   ```sh
   ibmcloud oc cluster config --cluster VPC_CLUSTER_ID_OR_NAME
   ```
   {: pre}

2. Verify that your context points to the VPC cluster:

   ```sh
   oc config current-context
   ```
   {: pre}

### Step 5: Apply manifests to the target VPC cluster
{: #vpc-migrate-cluster-scoped-apply}

1. Apply the exported and sanitized YAML manifests to the VPC cluster:

   - To apply a single resource manifest:
     ```sh
     oc apply -f RESOURCE_NAME.yaml
     ```
     {: pre}

   - To apply multiple manifests from a directory:
     ```sh
     oc apply -f ./manifests-directory/
     ```
     {: pre}

### Step 6: Verify resource creation
{: #vpc-migrate-cluster-scoped-verify}

1. Confirm that the resources were created successfully on the VPC cluster:

   ```sh
   oc get RESOURCE_TYPE RESOURCE_NAME
   ```
   {: pre}

## Cleaning up Backup and Recovery Service (BRS) registrations
{: #vpc-migrate-workloads-brs-cleanup}

If you need to change your {{site.data.keyword.cloud_notm}} Backup and Recovery Service (BRS) instance or remove BRS artifacts from a cluster that was already in use, you must unregister the cluster and remove the BRS connector and related resources before registering with a new BRS instance.

### Step 1: Delete the protection group in the BRS dashboard
{: #vpc-migrate-brs-cleanup-protection-group}

Deleting the protection group removes snapshots if the snapshot deletion option is selected. Only proceed if you have completed recovery or are troubleshooting an error.
{: attention}

1. In the {{site.data.keyword.cloud_notm}} console, click the navigation menu (☰).
2. Go to **Backup and Recovery** > **Backup Service Instances**.
3. Select your BRS instance, then click **Launch dashboard**.
4. In the BRS dashboard, click the navigation menu (☰), expand **Data Protection**, and click **Protection**.
5. Locate the protection group created for your cluster.
6. Click the actions menu (⋮) on the protection group and select **Delete**.

### Step 2: Deregister the data source in the BRS dashboard
{: #vpc-migrate-brs-cleanup-deregister}

You must delete the protection group before you can deregister the data source.
{: important}

1. In the BRS dashboard, click the navigation menu (☰), expand **System**, and click **Data Source Connections**.
2. Locate the connection named `brs-<cluster-id>`.
3. Click the connection name to open its details.
4. Click the **Linked Sources** tab.
5. Click the actions menu (⋮) on the linked source and select **Unregister Source**.

### Step 3: Remove the connector in the BRS dashboard
{: #vpc-migrate-brs-cleanup-remove-connector}

1. In the BRS dashboard, return to **System** > **Data Source Connections** and open the `brs-<cluster-id>` connection.
2. Click the **Connection Details** tab.
3. Click the actions menu (⋮) and select **Remove from Connection**.

### Step 4: Uninstall the BRS Helm chart from the cluster
{: #vpc-migrate-brs-cleanup-helm}

1. Log in to your cluster from the CLI:

   ```sh
   ibmcloud oc cluster config --cluster CLUSTER_ID
   ```
   {: pre}

2. Uninstall the BRS connector Helm release from the `ibm-backup-recovery` namespace:

   ```sh
   helm uninstall brs-connector -n ibm-backup-recovery
   ```
   {: pre}

### Step 5: Delete BRS-labeled namespaces and connector namespace
{: #vpc-migrate-brs-cleanup-namespaces}

1. Identify any namespaces that have BRS registration labels:

   ```sh
   oc get ns -l cohesity/exclude-ns=true,cohesity/is-registered=true -o jsonpath='{.items[*].metadata.name}'
   ```
   {: pre}

2. Delete each BRS-labeled namespace identified:

   ```sh
   oc delete namespace NAMESPACE
   ```
   {: pre}

3. Check that all pods in the `ibm-backup-recovery` namespace have terminated:

   ```sh
   oc get pods -n ibm-backup-recovery
   ```
   {: pre}

4. When all pods are terminated, delete the `ibm-backup-recovery` namespace:

   ```sh
   oc delete namespace ibm-backup-recovery
   ```
   {: pre}

After completing these cleanup steps, you can onboard the cluster to a new BRS instance.

## Next steps
{: #vpc-migrate-workloads-next}

[Cut over and validate](/docs/openshift?topic=openshift-vpc-migrate-cutover)
