---

copyright:
  years: 2026, 2026
lastupdated: "2026-09-09"

keywords: openshift, classic, vpc, migrate, migration, overview, replatform

subcollection: openshift

content-type: overview

---

{{site.data.keyword.attribute-definition-list}}

# Migrating from Classic to VPC
{: #vpc-migrate-overview}

[Classic infrastructure]{: tag-classic-inf}

Migrate your {{site.data.keyword.openshiftlong_notm}} workloads from Classic infrastructure to VPC to take advantage of improved security, networking flexibility, and better performance.
{: shortdesc}

Classic infrastructure is a legacy compute platform. New Classic cluster creation is restricted to accounts that already have existing Classic clusters. VPC infrastructure is the strategic direction for new workloads. To learn more about the Classic creation restriction, see [Classic cluster creation restrictions](/docs/openshift?topic=openshift-classic-create-restriction). By migrating, your clusters gain:

- Enhanced network security with security groups and private endpoints
- Faster storage provisioning with VPC Block Storage
- Simplified infrastructure management with a modern API

## Limitations
{: #vpc-migrate-overview-limitations}

Before you begin, review the [Classic to VPC migration limitations](/docs/openshift?topic=openshift-vpc-migrate-limitations). Key constraints include:

- Only standard clusters are supported. Free clusters and Satellite-location clusters cannot be migrated.
- A single workload migration plan supports up to 20 namespaces.
- Some managed add-ons (such as Istio, ALB OAuth Proxy, and ODF) are not migrated automatically and must be re-enabled on the VPC cluster after migration.
- VPC security groups are allow-only and do not support SCTP. Classic deny rules and SCTP network policies are not migrated.
- The migration service does not migrate on-premises connectivity such as Classic VPN or Direct Link. You must set up VPC-equivalent connectivity before you start workload migration.

## How the migration works
{: #vpc-migrate-overview-how}

Migration is a phased, non-disruptive process. Your Classic cluster continues to run throughout, so there is no forced downtime. The migration service analyzes your Classic cluster, generates a VPC configuration, provisions a new VPC cluster, migrates global resources and network policies automatically, then guides you through migrating your application workloads and cutting over traffic.

You can start the migration from the **Migration hub** in the {{site.data.keyword.cloud_notm}} console. In the hub, find your Classic cluster under **Assets** > **Clusters** and click **Open wizard**. The wizard opens on the **Migrating `<cluster-name>`** page and tracks your progress through each phase in the left navigation panel.

For scripted or automated migrations, you can also use:

- A **GraphQL API** at `/graphql` (Bearer token auth)
- **ibmcloud oc CLI** commands as an alternative to the API for each phase

## Migration phases
{: #vpc-migrate-overview-phases}

The migration follows two phases across six topics.

### Phase 1 — Infrastructure migration
{: #vpc-migrate-overview-phase1}

| Step | Topic | Description |
|------|-------|-------------|
| Assess | [Assess your Classic cluster](/docs/openshift?topic=openshift-vpc-migrate-assess) | Select a Cloud Object Storage instance, run the assessment to generate VPC metadata, and review the proposed VPC cluster configuration. |
| Plan | [Plan your VPC environment](/docs/openshift?topic=openshift-vpc-migrate-plan) | Review and adjust the proposed VPC topology, worker pool flavors, network policy migration behavior, and private connectivity before provisioning. |
| Create | [Create the VPC cluster](/docs/openshift?topic=openshift-vpc-migrate-create) | Provision the VPC cluster from the generated metadata. Infrastructure migration (network policies, add-ons, global resources) starts automatically after provisioning. |
| Monitor | [Monitor global resource migration](/docs/openshift?topic=openshift-vpc-migrate-global-resources) | Monitor the four automatic background sub-operations until all complete, then review any items that require your attention. |
| Migrate | [Migrate workloads](/docs/openshift?topic=openshift-vpc-migrate-workloads) | Select a Backup and Recovery Service (BRS) instance and create migration plans to move workloads namespace by namespace to the VPC cluster. |
{: caption="Phase 1 steps — infrastructure migration" caption-side="bottom"}

### Phase 2 — Traffic cutover
{: #vpc-migrate-overview-phase2}

| Step | Topic | Description |
|------|-------|-------------|
| Cut over and decommission | [Cut over and validate](/docs/openshift?topic=openshift-vpc-migrate-cutover) | Redirect live traffic to the VPC cluster, validate that all workloads are functioning correctly, observe a stabilization period, then remove the Classic cluster. |
{: caption="Phase 2 steps — traffic cutover" caption-side="bottom"}

## Before you begin
{: #vpc-migrate-overview-prereqs}

- Ensure that you have the **Administrator** {{site.data.keyword.iamlong}} platform access role for the Classic cluster. See [Assigning cluster access](/docs/openshift?topic=openshift-iam-platform-access-roles).
- Install and update the {{site.data.keyword.cloud_notm}} CLI and the {{site.data.keyword.openshiftlong_notm}} plug-in. See [Installing the CLI](/docs/openshift?topic=openshift-cli-install).
- Provision an IBM Cloud Object Storage (COS) instance in the same account. The migration service uses COS to store generated metadata and migration plans.
- Provision an IBM Cloud Backup and Recovery Service (BRS) instance in the same account and region as your Classic cluster. The BRS instance is required for workload and storage migration.
- If your Classic cluster uses on-premises connectivity (Classic VPN, Direct Link 1.0), set up the equivalent VPC connectivity before you start workload migration. The migration service does not migrate these connections. See [Plan your VPC environment](/docs/openshift?topic=openshift-vpc-migrate-plan#vpc-migrate-plan-connectivity).
- [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

## Next steps
{: #vpc-migrate-overview-next}

- [Classic to VPC migration limitations](/docs/openshift?topic=openshift-vpc-migrate-limitations)
- [Assess your Classic cluster](/docs/openshift?topic=openshift-vpc-migrate-assess)
