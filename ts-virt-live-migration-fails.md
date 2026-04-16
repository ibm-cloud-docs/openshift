---

copyright:
  years: 2026, 2026

lastupdated: "2026-04-16"

keywords: openshift virtualization, live migration, vmim, rwx, vni, zone

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does live migration fail for a virtual machine?
{: #ts-virt-live-migration-fails}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

You try to live migrate a virtual machine (VM), but the migration does not complete successfully.
{: tsSymptoms}

Live migration depends on storage and node placement. Migration can fail if the VM storage does not support `ReadWriteMany` (RWX), if the target node does not have enough resources, or if a VNI-based VM is moved across zones.
{: tsCauses}

To resolve the issue,
{: tsResolve}

 review the migration resource, confirm that the storage supports RWX, and verify the node and zone placement.

1. Check the migration status.
   ```sh
   oc get vmim -n <namespace>
   oc describe vmim <migration_name> -n <namespace>
   ```
   {: pre}

2. Verify that the VM storage supports `ReadWriteMany` (RWX).
   ```sh
   oc get pvc -n <namespace>
   oc describe pvc <pvc_name> -n <namespace>
   ```
   {: pre}

3. Check the zone placement of the cluster nodes.
   ```sh
   oc get nodes -L topology.kubernetes.io/zone
   ```
   {: pre}

4. Review the target node resources.
   ```sh
   oc describe node <target_node_name>
   ```
   {: pre}

5. Review the `virt-handler` logs.
   ```sh
   oc logs -n openshift-cnv -l kubevirt.io=virt-handler
   ```
   {: pre}

6. If the VM uses VNIs, confirm that the migration stays within the same zone. For more information, see [Managing virtual network interfaces for OpenShift Virtualization](/docs/openshift?topic=openshift-vni-virtualization#vni-about).
