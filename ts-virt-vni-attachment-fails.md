---

copyright:
  years: 2026, 2026

lastupdated: "2026-04-21"

keywords: openshift virtualization, vni attachment, vpc, iam, zone, worker

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does a VNI attachment fail?
{: #ts-virt-vni-attachment-fails}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.20 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

You try to attach a virtual network interface (VNI) for OpenShift Virtualization, but the attachment does not succeed.
{: tsSymptoms}

A VNI attachment can fail if the VNI does not exist, if it is created in a different zone than the worker node, or if the account does not have the required permissions to manage cluster and VPC resources.
{: tsCauses}

To resolve the issue,
{: tsResolve}

 verify that the VNI exists, confirm the zone placement, and review the IAM permissions and attachment status.

1. Verify that the VNI exists in your VPC.
   ```sh
   ibmcloud is virtual-network-interfaces
   ```
   {: pre}

2. Check the VNI zone and compare it with the worker node zone.
   ```sh
   ibmcloud is virtual-network-interface <vni_id>
   oc get node <node_name> -L topology.kubernetes.io/zone
   ```
   {: pre}

3. Review the IAM permissions for the user or service ID that you are using.
   ```sh
   ibmcloud iam user-policies <user_email>
   ```
   {: pre}

4. Check the VNI attachment status for the cluster.
   ```sh
   ibmcloud ks experimental vni ls --cluster-id <cluster_id>
   ```
   {: pre}

5. Review the prerequisites and zone requirements in [Managing virtual network interfaces for OpenShift Virtualization](/docs/openshift?topic=openshift-vni-virtualization#vni-prereqs).
