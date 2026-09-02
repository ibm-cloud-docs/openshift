---

copyright:
  years: 2025, 2026
lastupdated: "2026-09-02"


keywords: rhel, os, operating system, rhcos, 418, migration, deprecation

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# RHEL deprecation for VPC clusters
{: #rhel-deprecation}

[Virtual Private Cloud only]{: tag-vpc}

Review the following information about the deprecation of Red Hat Enterprise Linux (RHEL) worker nodes for VPC clusters and the migration to Red Hat Enterprise Linux CoreOS (RHCOS) worker nodes.
{: shortdesc}

The information on this page applies to VPC clusters only. It does not apply to Satellite or Classic clusters.
{: important}

Beginning with version 4.18 clusters on VPC infrastructure, Red Hat Enterprise Linux (RHEL) worker nodes are deprecated. Version 4.22 is the last version to support RHEL worker nodes. Migrate your clusters to use RHCOS worker nodes as soon as possible.
{: deprecated}

Red Hat Enterprise Linux CoreOS (RHCOS) is the default operating system for {{site.data.keyword.openshiftlong_notm}}. Version 4.22 is the last version to support RHEL worker nodes. Future versions will require RHCOS worker nodes.

RHCOS represents the next generation of single-purpose container operating system technology by providing the quality standards of RHEL with automated, remote upgrade features.

**RHEL 8 users:** Version 4.17 is the last {{site.data.keyword.openshiftlong_notm}} release that supports RHEL 8 worker nodes. RHEL 8 is not supported in version 4.18 or later. If you have RHEL 8 worker nodes, you must migrate them to RHEL 9 or RHCOS before upgrading your cluster to version 4.18.
{: important}

## Timeline
{: #timeline}

| Stage | Date | Description |
| --- | --- | --- |
| RHEL 8 end of support | 4.17 last supported version | Version 4.17 is the last {{site.data.keyword.openshiftlong_notm}} release that supports RHEL 8 worker nodes. Before upgrading to version 4.18, migrate all RHEL 8 worker nodes to RHEL 9 or RHCOS. See [Migrating to Red Hat Enterprise Linux 9](/docs/openshift?topic=openshift-migrate-rhel-9) or [Migrating VPC worker nodes to RHCOS](/docs/openshift?topic=openshift-rhel_migrate). |
| Announcement | 4.18 release date: {{site.data.keyword.openshift_418_release_date}} | Beginning with cluster version 4.18, Red Hat Enterprise Linux CoreOS (RHCOS) is the default operating system and RHEL worker nodes are deprecated in this version. RHEL workers are still available in version 4.18 only to complete the migration to RHCOS workers. |
| Reminders | Ongoing | Periodic reminders will be sent to all users with deployments of RHEL worker nodes in their clusters informing them that end of support is coming with increasing frequency as the date approaches. |
| Last supported version | 4.22 | Version 4.22 is the last version to support RHEL worker nodes on VPC. Migrate your RHEL 9 worker nodes to RHCOS before upgrading to future versions. |
{: caption="RHEL deprecation timeline" caption-side="bottom"}

## Migration steps
{: #migration}

Review and complete the following steps for migration.

1. Understand the timeline and plan for key milestone dates.
3. Work with your CSM or TAM if one is assigned to your account.
1. Complete the migration steps that apply to your use case.
    - [Migrating VPC worker nodes to RHCOS](/docs/openshift?topic=openshift-rhel_migrate).
    - [Migrating GPU worker nodes to RHCOS](/docs/openshift?topic=openshift-rhel_migrate).
1. Verify your migration.
