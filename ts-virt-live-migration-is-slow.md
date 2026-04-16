---

copyright:
  years: 2026, 2026

lastupdated: "2026-04-16"

keywords: openshift virtualization, live migration, migration performance, storage, node bandwidth

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is live migration slow?
{: #ts-virt-live-migration-is-slow}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

You start a live migration for a virtual machine (VM), but the migration takes longer than expected.
{: tsSymptoms}

Migration duration can be affected by node bandwidth, storage performance, and VM memory activity during the migration.
{: tsCauses}

Use the following checks to investigate the environment.
{: tsResolve}

1. Review the node placement and network details.
   ```sh
   oc get nodes -o wide
   ```
   {: pre}

2. Review the storage that backs the VM.
   ```sh
   oc get pvc -n <namespace>
   ```
   {: pre}

3. Review the migration details.
   ```sh
   oc describe vmim <migration_name> -n <namespace>
   ```
   {: pre}

4. Review the planning guidance in [Planning your OpenShift Virtualization deployment](/docs/openshift?topic=openshift-virt-plan#virt-plan-storage).
   Compare the current storage configuration to the guidance for your selected storage backend and confirm that it is appropriate for live migration workloads.

5. If migration remains slow, collect the migration details, node placement, and storage information before you contact [{{site.data.keyword.cloud_notm}} support](/docs/get-support).
   Include the migration status, node details, and storage information when you open a support case so that the environment can be reviewed.
