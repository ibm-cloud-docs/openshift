---

copyright:
  years: 2026, 2026
lastupdated: "2026-05-06"

keywords: openshift, vni, virtual network interface, vpc, bare metal, networking

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Understanding Virtual Network Interfaces in VPC clusters
{: #vpc-vni}

[Virtual Private Cloud]{: tag-vpc}
[4.20 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}

Virtual Network Interfaces (VNIs) provide advanced network connectivity options for workloads running on {{site.data.keyword.openshiftlong_notm}} VPC clusters with bare metal worker nodes.
{: shortdesc}

## What are Virtual Network Interfaces?
{: #vpc-vni-about}

A Virtual Network Interface (VNI) is an {{site.data.keyword.cloud_notm}} VPC abstraction that represents individual network connections. VNIs embed properties of a network connection, including:

- IP addresses (primary and secondary)
- MAC addresses
- VPC subnet association
- Security group membership
- Floating IP attachment capability

VNIs are available only on clusters with bare metal worker nodes running Red Hat CoreOS (RHCOS).
{: note}

## VNI architecture in OpenShift clusters
{: #vpc-vni-architecture}

### Static VNIs
{: #vpc-vni-static}

When you create a bare metal-based {{site.data.keyword.openshiftshort}} cluster or add a new bare metal worker pool in IBM Cloud VPC, two VNIs are automatically created and attached to every bare metal worker node:

Primary VNI
:   Handles regular worker traffic including pod network, overlay User Defined Networks (UDNs), and communication with the cluster master.

Secondary VNI (carrier)
:   Acts as a carrier for dynamic VNI attachments that you manage. This VNI enables you to attach additional network interfaces to workloads running on the worker node.

### Dynamic VNIs
{: #vpc-vni-dynamic}

Dynamic VNIs are created and managed on-demand after cluster creation. These VNIs can be:

- Attached to specific worker nodes
- Configured to float between workers in the same zone
- Used for direct VPC network connectivity
- Associated with floating IPs for external access

## Key capabilities
{: #vpc-vni-capabilities}

Direct VPC connectivity
:   VNIs enable workloads to connect directly to VPC networks, bypassing the pod network overlay. This provides native VPC networking features like security groups, network ACLs, and routing.

Floating IP support
:   VNIs can have floating IPs attached, allowing workloads to be directly accessible from the internet or other VPC networks.

Security group integration
:   VNIs can be associated with VPC security groups, providing fine-grained network access control at the interface level.

Zone-specific networking
:   VNIs are attached to a specific VPC subnet and zone. They can handle traffic only for workloads running on cluster workers in the same zone where the VNI is provisioned.

Network preservation during migration
:   For workloads that support live migration (such as OpenShift Virtualization VMs), VNIs can implicitly float and follow the workload between bare metal worker instances within the same zone, preserving network connections.

## Use cases
{: #vpc-vni-use-cases}

OpenShift Virtualization
:   Enable direct VPC network connectivity for virtual machines, allowing VMs to have their own VPC IP addresses and floating IPs. See [Managing virtual network interfaces for OpenShift Virtualization](/docs/openshift?topic=openshift-vni-virtualization).

Multi-network workloads
:   Connect workloads to multiple VPC subnets simultaneously, enabling complex network topologies and traffic segregation.

Legacy application migration
:   Provide VM-like networking for containerized applications that require specific IP addresses or direct network access.

Network function virtualization
:   Deploy network functions that require direct access to VPC networking features.

## Limitations and considerations
{: #vpc-vni-limitations}

Zone constraints
:   VNIs cannot float between zones. In multi-zone clusters, VNIs can only handle traffic for workloads in the same zone where the VNI is provisioned.

Bare metal requirement
:   VNIs are only supported on bare metal worker nodes. Virtual server instance (VSI) worker nodes do not support VNIs.

RHCOS requirement
:   Worker nodes must run Red Hat CoreOS (RHCOS) operating system.

OVN-Kubernetes CNI
:   Clusters must use the OVN-Kubernetes Container Network Interface (CNI) plugin.

Cross-account management
:   In {{site.data.keyword.openshiftlong_notm}}, worker nodes are provisioned in IBM's account, not your account. This means VNI lifecycle management differs from standalone VPC bare metal instances, and you have different visibility into VNI attachments.

Version requirement
:   VNI support requires OpenShift 4.20 or later.

## Prerequisites
{: #vpc-vni-prereqs}

Before using VNIs in your cluster, ensure you have:

- A {{site.data.keyword.openshiftlong_notm}} cluster at version 4.20 or later
- Bare metal worker nodes in your cluster
- Red Hat CoreOS (RHCOS) operating system on worker nodes
- OVN-Kubernetes CNI configured
- VPC infrastructure with appropriate subnets
- The **Operator** platform access role for **Kubernetes Service** in {{site.data.keyword.cloud_notm}} IAM
- The **Editor** or **Administrator** platform access role for VPC Infrastructure Services in {{site.data.keyword.cloud_notm}} IAM

## Managing VNIs with the CLI
{: #vpc-vni-cli}

You can use the {{site.data.keyword.openshiftlong_notm}} CLI to attach, list, and detach VNIs from your cluster worker nodes.

### Attaching a VNI to a worker node
{: #vpc-vni-cli-attach}

To attach a VNI to a specific bare metal worker node, use the `vni attach baremetal` command. You must specify a VLAN ID (range: 1-500) that matches your network configuration.

```sh
ibmcloud ks vni attach baremetal --worker WORKER_ID --vni VNI_ID --vlan VLAN_ID [--auto-delete]
```
{: pre}

To attach a floating VNI that can follow workloads between workers in the same zone, specify the cluster ID instead of a worker ID:

```sh
ibmcloud ks vni attach baremetal --cluster-id CLUSTER_ID --vni VNI_ID --vlan VLAN_ID [--auto-delete]
```
{: pre}

The `--auto-delete` flag automatically deletes the VNI when it is removed from the cluster.
{: tip}

### Listing VNI attachments
{: #vpc-vni-cli-list}

To list all VNIs attached to a cluster:

```sh
ibmcloud ks vni ls --cluster-id CLUSTER_ID
```
{: pre}

To list VNIs attached to a specific worker node:

```sh
ibmcloud ks vni ls --worker WORKER_ID
```
{: pre}

### Detaching a VNI
{: #vpc-vni-cli-detach}

To detach a VNI from a worker node, specify both the VNI ID and the worker ID:

```sh
ibmcloud ks vni detach --worker WORKER_ID --vni VNI_ID
```
{: pre}

For floating VNIs, first list the VNIs to find the current worker ID, then detach using that worker ID.
{: tip}

For more detailed examples and use cases, see [Managing virtual network interfaces for OpenShift Virtualization](/docs/openshift?topic=openshift-vni-virtualization).

## Next steps
{: #vpc-vni-next-steps}

- [Managing virtual network interfaces for OpenShift Virtualization](/docs/openshift?topic=openshift-vni-virtualization)
- [About virtual network interfaces in VPC](/docs/vpc?topic=vpc-vni-about)
- [VPC security groups](/docs/openshift?topic=openshift-vpc-security-group2)
- [VPC subnets](/docs/openshift?topic=openshift-vpc-subnets)
