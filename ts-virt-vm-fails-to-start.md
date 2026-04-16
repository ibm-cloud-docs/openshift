---

copyright:
  years: 2026, 2026

lastupdated: "2026-04-16"

keywords: openshift virtualization, vm start, virtualmachineinstance, virt-launcher, bare metal

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does a virtual machine fail to start?
{: #ts-virt-vm-fails-to-start}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

You try to start a virtual machine (VM), but the VM does not reach a running state.
{: tsSymptoms}

The virtual machine configuration, the VirtualMachineInstance (VMI), or the target node might not meet the requirements for OpenShift Virtualization. Startup can also fail if the VM is not scheduled on a supported bare metal worker node.
{: tsCauses}

To resolve the issue,
{: tsResolve}

 review the VM status, inspect the VMI, and check the node that the VM is scheduled to use.

1. Check the VM status and events.
   ```sh
   oc describe vm <vm_name> -n <namespace>
   ```
   {: pre}

2. Review the VirtualMachineInstance status.
   ```sh
   oc get vmi <vm_name> -n <namespace>
   oc describe vmi <vm_name> -n <namespace>
   ```
   {: pre}

3. Review the `virt-launcher` pod logs.
   ```sh
   oc logs -n <namespace> virt-launcher-<vm_name>-xxxxx
   ```
   {: pre}

4. Verify that the target node has sufficient resources.
   ```sh
   oc describe node <node_name>
   ```
   {: pre}

5. Ensure that the VM is scheduled on a bare metal worker node.
   ```sh
   oc get vmi <vm_name> -n <namespace> -o wide
   ```
   {: pre}

6. If the issue continues, review the requirements in [Understanding OpenShift Virtualization](/docs/openshift?topic=openshift-virt-overview) and the node placement guidance in [Installing the OpenShift Virtualization Operator](/docs/openshift?topic=openshift-oc-virtualization#virt-install-node-placement).
