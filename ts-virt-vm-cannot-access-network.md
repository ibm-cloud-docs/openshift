---

copyright:
  years: 2026, 2026

lastupdated: "2026-04-16"

keywords: openshift virtualization, vm network, user defined network, vni, ovn

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't a virtual machine access the network?
{: #ts-virt-vm-cannot-access-network}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

You start a virtual machine (VM), but the VM cannot access the expected network.
{: tsSymptoms}

The VM network configuration might not match the configured User Defined Network (UDN) or VNI setup. This issue can occur if the VM is missing the expected network interface, if the UDN configuration is incorrect, or if OVN networking components report errors.
{: tsCauses}

To resolve the issue,
{: tsResolve}

 review the VM network configuration, verify the attached interfaces, and confirm the UDN and OVN configuration.

1. Check the VM network configuration.
   ```sh
   oc describe vm <vm_name> -n <namespace>
   ```
   {: pre}

2. Verify that the VM has the expected network interface.
   ```sh
   oc get vmi <vm_name> -n <namespace> -o yaml | grep -A 10 interfaces
   ```
   {: pre}

3. If you use VNI-based networking, review the VNI attachments for the cluster.
   ```sh
   ibmcloud ks vni ls --cluster-id <cluster_id>
   ```
   {: pre}

4. Check the User Defined Network configuration.
   ```sh
   oc get clusteruserdefinednetwork
   oc describe clusteruserdefinednetwork <udn_name>
   ```
   {: pre}

5. Review OVN logs for networking errors.
   ```sh
   oc logs -n openshift-ovn-kubernetes -l app=ovnkube-node
   ```
   {: pre}
