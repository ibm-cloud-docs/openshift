---

copyright:
  years: 2026, 2026

lastupdated: "2026-04-16"

keywords: openshift virtualization, vm performance, node resources, storage performance, bare metal

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is virtual machine performance poor?
{: #ts-virt-vm-performance-is-poor}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

Your virtual machine (VM) starts, but the workload performance is lower than expected.
{: tsSymptoms}

Performance can be affected by node sizing, storage characteristics, VM placement, and resource contention on the worker node.
{: tsCauses}

Use the following checks to investigate the environment.
{: tsResolve}

1. Review the VM resource allocation.
   ```sh
   oc get vm <vm_name> -n <namespace> -o yaml | grep -A 5 resources
   ```
   {: pre}

2. Verify that the VM is running on a bare metal worker node.
   ```sh
   oc get vmi <vm_name> -n <namespace> -o wide
   ```
   {: pre}

3. Review node resource utilization.
   ```sh
   oc describe node <node_name>
   oc adm top node <node_name>
   ```
   {: pre}

4. Review your storage configuration.
   ```sh
   oc get storageclass <storage_class_name> -o yaml
   ```
   {: pre}

5. Compare the current deployment to the planning guidance in [Planning your OpenShift Virtualization deployment](/docs/openshift?topic=openshift-virt-plan#virt-plan-flavors) and the storage guidance in [Setting up storage for OpenShift Virtualization](/docs/openshift?topic=openshift-virt-storage-setup).
   If needed, adjust your worker flavor selection, VM sizing, or storage choice to better match the workload profile.

6. If you use ODF, review the storage cluster status.
   ```sh
   oc get storagecluster -n openshift-storage
   ```
   {: pre}

7. If performance remains poor, collect node, VM, and storage details before you contact [{{site.data.keyword.cloud_notm}} support](/docs/get-support).
   Include the command output when you open a support case so that the cluster, node, and storage conditions can be reviewed.
