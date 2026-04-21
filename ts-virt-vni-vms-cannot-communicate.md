---

copyright:
  years: 2026, 2026

lastupdated: "2026-04-21"

keywords: openshift virtualization, vni, vm communication, cudn, vlan, security group

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't VMs with VNI attachments communicate?
{: #ts-virt-vni-vms-cannot-communicate}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.20 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

You configure VNI attachments for virtual machines (VMs), but the VMs still cannot communicate as expected.
{: tsSymptoms}

The communication path can fail if the VLAN configuration, VM interface settings, or VPC networking settings do not match across the VNI and localnet UDN configuration.
{: tsCauses}

Use the following checks to investigate the configuration.
{: tsResolve}

1. Verify that the VLAN ID matches between the ClusterUserDefinedNetwork (CUDN) and the VNI attachment.
   ```sh
   oc get clusteruserdefinednetwork <cudn_name> -o yaml
   ibmcloud ks experimental vni ls --cluster-id <cluster_id>
   ```
   {: pre}

2. Check that the VM is using the expected MAC address.
   ```sh
   oc get vmi <vm_name> -n <namespace> -o yaml | grep macAddress
   ```
   {: pre}

3. Review the VNI configuration.
   ```sh
   ibmcloud is virtual-network-interface <vni_id>
   ```
   {: pre}

4. Review the VPC security group configuration.
   ```sh
   ibmcloud is security-groups
   ibmcloud is security-group <security_group_id>
   ```
   {: pre}

5. Review the guest operating system network configuration inside the VM.
   Confirm that the guest operating system network settings, such as the configured IP address, routes, and interface state, match your expected VNI and VLAN design.

6. Review [Managing virtual network interfaces for OpenShift Virtualization](/docs/openshift?topic=openshift-vni-virtualization) to confirm that the VNI, VLAN, and localnet configuration are aligned.
   If the configuration does not align, update the CUDN, VLAN, or VNI settings so that they match across the cluster and the VM configuration.
