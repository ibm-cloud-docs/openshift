---

copyright:
  years: 2025, 2025
lastupdated: "2025-07-31"


keywords: rhel, os, operating system, rhcos, 418, migration, deprecation

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Red Hat Enterprise Linux (RHEL) deprecation
{: #rhel-deprecation}

Review the following information about deprecation of Red Hat Enterprise Linux (RHEL) worker nodes for {{site.data.keyword.openshiftlong_notm}} clusters and the migration to Red Hat Enterprise Linux CoreOS (RHCOS) worker nodes.
{: shortdesc}

Beginning with version 4.18 clusters on VPC, Red Hat Enterprise Linux (RHEL) RHEL worker nodes are deprecated. Support for RHEL worker nodes ends with the release of version 4.21. Migrate your clusters to use RHCOS worker nodes as soon as possible.
{: deprecated}

Red Hat Enterprise Linux CoreOS (RHCOS) is the default operating system and beginning with version 4.21, RHCOS will be the only supported operated system for {{site.data.keyword.openshiftlong_notm}}.

RHCOS represents the next generation of single-purpose container operating system technology by providing the quality standards of RHEL with automated, remote upgrade features.

## Timeline
{: #timeline}

| Stage | Date | Description |
| --- | --- | --- |
| Announcement | 4.18 release date: {{site.data.keyword.openshift_418_release_date}} | Beginning with cluster version 4.18, Red Hat Enterprise Linux CoreOS (RHCOS) is the default operating system and RHEL worker nodes are deprecated in this version. RHEL workers are still available in version 4.18 only to complete the migration to RHCOS workers. |
| Reminders | Ongoing | Periodic reminders will be sent to all users with deployments of RHEL worker nodes in their clusters informing them that the end of support date is coming with increasing frequency as the EOS date approaches. |
| End of support | 4.21 release date date | Cluster version 4.21 supports only RHCOS worker nodes. Migrate your RHEL 9 worker nodes to RHCOS before updating to version 4.21. |
{: caption="RHEL deprecation timeline" caption-side="bottom"}

## Migration steps
{: #migration}

Review and complete the following steps for migration.

1. Understand the timeline and plan for key milestone dates.
3. Work with your CSM or TAM if one is assigned to your account.
1. Complete the migration steps that apply to your use case.
    - [Migrating worker nodes to RHCOS](/docs/openshift?topic=openshift-rhel_migrate#migrate-rhcos).
    - [Migrating GPU worker nodes to RHCOS](/docs/openshift?topic=openshift-rhel_migrate#rhcos-migrate-gpu).
1. Verify your migration.
