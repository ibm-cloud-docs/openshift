---

copyright:
  years: 2026, 2026
lastupdated: "2026-10-29"

keywords: openshift, classic, vpc, migrate, migration, quickstart, wizard

subcollection: openshift

content-type: tutorial
services: openshift
account-plan: paid
completion-time: 30m

---

{{site.data.keyword.attribute-definition-list}}

# Migration wizard quickstart guide
{: #vpc-migrate-quickstart}
{: toc-content-type="tutorial"}
{: toc-services="openshift"}
{: toc-completion-time="30m"}

[Classic infrastructure]{: tag-classic-inf}

Use the migration wizard to migrate a Classic cluster to VPC in a guided, end-to-end workflow from the {{site.data.keyword.cloud_notm}} console.
{: shortdesc}

This quickstart shows you how to open the migration wizard and what to expect in each step. For a full explanation of each step, see [Migrating from Classic to VPC](/docs/openshift?topic=openshift-vpc-migrate-overview).

## Before you begin
{: #vpc-migrate-quickstart-prereqs}

Make sure that you have the following items.

- A Classic cluster. To check, go to **Containers** > **Clusters** in the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/containers/cluster-management/clusters){: external} and confirm that at least one cluster shows **Classic** as the infrastructure type.
- At least the **Operator** (`containers-kubernetes.cluster.operate`) {{site.data.keyword.iamlong}} platform access role for {{site.data.keyword.openshiftlong_notm}} on both the Classic cluster and the VPC cluster. See [Assigning cluster access](/docs/openshift?topic=openshift-iam-platform-access-roles).
- An {{site.data.keyword.cos_full_notm}} (COS) instance in the same account. The migration service uses COS to store generated metadata and migration plans.
- An {{site.data.keyword.cloud_notm}} Backup and Recovery Service (BRS) instance in the same account and resource group as your Classic cluster. BRS is required to migrate workload and storage data.
- [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

## Step 1: Open the migration wizard
{: #vpc-migrate-quickstart-open}

You can open the migration wizard from the Migration hub or from the Containers page. Choose the entry point that you prefer.

### Open the wizard from the Migration hub
{: #vpc-migrate-quickstart-hub}

1. Go to **Migration hub**.
2. Click the **Clusters** tile, or use the navigation to go to **Clusters**.
3. Open **Eligible clusters**.
4. Find your Classic cluster and click **Open wizard**.

### Open the wizard from the Containers page
{: #vpc-migrate-quickstart-containers}

1. Go to **Containers** > **Clusters**.
2. In the row actions for your Classic cluster, select **Migrate to VPC**.

The wizard opens on the **Migrating CLUSTER_NAME** page. The left navigation panel shows your progress through each step.

## Step 2: Follow the migration wizard
{: #vpc-migrate-quickstart-wizard}

Complete the wizard steps in order. The steps in the following table match the steps in the migration wizard.

| Phase | Step | What you do |
|-------|------|-------------|
| Phase 1 | Step 1: Assess | Select a COS instance, run the assessment, and review the proposed VPC configuration. |
| Phase 1 | Step 2: Create | Provision the VPC cluster. Infrastructure migration starts automatically. |
| Phase 1 | Step 3: Migrate | Choose a backup and recovery instance, create migration plans, and move workloads to the VPC cluster, namespace by namespace. |
| Phase 2 | Cutover | Redirect DNS traffic to the VPC cluster, validate your workloads, and complete the finish migration checklist. |
{: caption="Migration wizard phases and steps" caption-side="bottom"}

Cutover and deleting the Classic cluster are manual processes. The migration wizard does not do them for you.
{: important}

## Next steps
{: #vpc-migrate-quickstart-next}

- [Assess your Classic cluster](/docs/openshift?topic=openshift-vpc-migrate-assess) and generate the VPC configuration metadata.
- Review [what is and is not migrated automatically](/docs/openshift?topic=openshift-vpc-migrate-overview#vpc-migrate-overview-limitations) before you start.
- Prepare for cutover by reading [Cut over and validate](/docs/openshift?topic=openshift-vpc-migrate-cutover).
