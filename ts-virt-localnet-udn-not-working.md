---

copyright:
  years: 2026, 2026

lastupdated: "2026-05-06"

keywords: openshift virtualization, localnet, udn, nmstate, ovs bridge, vlan

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is the localnet user defined network not working?
{: #ts-virt-localnet-udn-not-working}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.20 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

You configure a localnet user defined network (UDN) for OpenShift Virtualization, but the network does not work as expected.
{: tsSymptoms}

A localnet UDN depends on the NMState Operator, an OVS bridge on `eth1`, a bridge mapping, and a matching VLAN configuration in the ClusterUserDefinedNetwork (CUDN). If any part of this setup is missing or inconsistent, the network does not work correctly.
{: tsCauses}

To resolve the issue,
{: tsResolve}

 verify the NMState installation, the OVS bridge, the bridge mapping, and the VLAN configuration.

1. Verify that the NMState Operator pods are running.
   ```sh
   oc get pods -n openshift-nmstate
   ```
   {: pre}

2. Check the OVS bridge configuration.
   ```sh
   oc get nodenetworkconfigurationpolicy
   oc describe nodenetworkconfigurationpolicy br-eth1
   ```
   {: pre}

3. Verify the bridge mapping configuration.
   ```sh
   oc get nodenetworkconfigurationpolicy
   oc describe nodenetworkconfigurationpolicy vpc-vlans
   ```
   {: pre}

4. Verify that the VLAN ID in the CUDN matches the VLAN that you plan to use.
   ```sh
   oc get clusteruserdefinednetwork <cudn_name> -o yaml | grep vlan
   ibmcloud ks vni ls --cluster-id <cluster_id>
   ```
   {: pre}

5. Review [Managing virtual network interfaces for OpenShift Virtualization](/docs/openshift?topic=openshift-vni-virtualization#vni-setup-localnet) to confirm that the OVS bridge, bridge mapping, and CUDN definitions match the documented configuration.
