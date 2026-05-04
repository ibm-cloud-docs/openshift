---

copyright:
  years: 2025, 2026
lastupdated: "2026-05-04"

keywords: openshift, virtualization, virtual machines, vms, bare metal

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# OpenShift Virtualization on IBM Cloud
{: #virt-overview}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

Run virtual machines (VMs) alongside containerized workloads on {{site.data.keyword.openshiftlong_notm}} clusters. OpenShift Virtualization provides a unified platform for both traditional VM-based applications and cloud-native containerized workloads.
{: shortdesc}

## Overview
{: #virt-what-is}

OpenShift Virtualization uses KubeVirt technology to enable virtual machine management within your Kubernetes environment. Key capabilities include:

Unified platform
:   Run VMs and containers on the same infrastructure

Kubernetes-native management
:   Manage VMs using familiar Kubernetes tools and APIs

Live migration
:   Move VMs between nodes without downtime

Flexible networking
:   Connect VMs to pod networks or directly to VPC networks

Enterprise storage
:   Use OpenShift Data Foundation or IBM Cloud storage services

## Deployment options
{: #virt-deployment-options}

Choose the deployment approach that best fits your needs:



### Manual deployment (For custom configurations)
{: #virt-manual-deployment}

Full control over component selection and configuration.

Create a standard {{site.data.keyword.openshiftlong_notm}} cluster and manually install and configure OpenShift Virtualization components.

What you configure:
- OpenShift Virtualization Operator installation
- Storage solution (ODF, VPC File Storage, or other)
- Networking optimization
- Node placement and resource allocation

Best for:
- Mixed container and VM workloads
- Custom storage configurations
- Specific networking requirements
- Full control over all components

Requirements:
- OpenShift 4.17 or later
- VPC bare metal worker nodes
- Manual storage setup

[Plan your manual deployment](/docs/openshift?topic=openshift-virt-plan){: .btn .btn-primary}



## Common requirements
{: #virt-requirements}

OpenShift Virtualization requires:

Infrastructure
:   - VPC with bare metal worker nodes
    - Red Hat CoreOS (RHCOS) operating system
    - OVN-Kubernetes CNI
    - Outbound traffic protection disabled

Storage
:   - ReadWriteMany (RWX) access mode support
    - OpenShift Data Foundation (recommended) or VPC File Storage

Networking
:   - 100 Gbps (Gen 2) or 200 Gbps (Gen 3) network connectivity
    - MTU optimization for VM workloads

## Supported bare metal flavors
{: #virt-bm-flavors}

OpenShift Virtualization requires VPC bare metal worker nodes. The following flavors are supported:

| Flavor | vCPU | Memory | Network | Local Storage | Min Version | Best for |
|--------|------|--------|---------|---------------|-------------|----------|
| `bx2.metal.96x384` | 96 | 384 GB | 100 Gbps | - | All | Balanced workloads |
| `bx2d.metal.96x384` | 96 | 384 GB | 100 Gbps | 480 GB NVME | All | Balanced + ODF |
| `cx2.metal.96x192` | 96 | 192 GB | 100 Gbps | - | All | Compute-intensive |
| `cx2d.metal.96x192` | 96 | 192 GB | 100 Gbps | 480 GB NVME | All | Compute + ODF |
| `mx2.metal.96x768` | 96 | 768 GB | 100 Gbps | - | All | Memory-intensive |
| `mx2d.metal.96x768` | 96 | 768 GB | 100 Gbps | 480 GB NVME | All | Memory + ODF |
| `bx3d.metal.48x256` | 24 | 256 GB | 200 Gbps | 480 GB NVME | 4.17+ | Small balanced + ODF |
| `bx3d.metal.64x256` | 32 | 256 GB | 200 Gbps | 480 GB NVME | 4.17+ | Medium balanced + ODF |
| `bx3d.metal.192x1024` | 96 | 1024 GB | 200 Gbps | 480 GB NVME | 4.17+ | Large balanced + ODF |
| `cx3d.metal.48x128` | 24 | 128 GB | 200 Gbps | 480 GB NVME | 4.17+ | Small compute + ODF |
| `cx3d.metal.64x128` | 32 | 128 GB | 200 Gbps | 480 GB NVME | 4.17+ | Medium compute + ODF |
| `mx3d.metal.16x128` | 8 | 128 GB | 200 Gbps | 480 GB NVME | 4.17+ | Small memory + ODF |
| `mx3d.metal.48x512` | 24 | 512 GB | 200 Gbps | 480 GB NVME | 4.17+ | Medium memory + ODF |
| `mx3d.metal.64x512` | 32 | 512 GB | 200 Gbps | 480 GB NVME | 4.17+ | Large memory + ODF |
| `mx3d.metal.96x1024` | 48 | 1024 GB | 200 Gbps | 480 GB NVME | 4.17+ | XL memory + ODF |
| `mx3d.metal.128x1024` | 64 | 1024 GB | 200 Gbps | 480 GB NVME | 4.17+ | XXL memory + ODF |
{: caption="Supported bare metal flavors for OpenShift Virtualization" caption-side="bottom"}

Flavors with `d` suffix include NVME local storage, which is required for OpenShift Data Foundation. Flavors with `3d` in the name offer improved network performance (200 Gbps) and require OpenShift 4.17 or later.
{: tip}

## Storage and networking
{: #virt-storage-networking}

### Storage options
{: #virt-storage-options}

| Storage | Performance | Snapshots | Cloning | Best for |
|---------|-------------|-----------|---------|----------|
| OpenShift Data Foundation | High | Yes | Yes | Production, high I/O workloads |
| IBM Storage Fusion | High | Yes | Yes | Enterprise with backup needs |
{: caption="Storage options for OpenShift Virtualization" caption-side="bottom"}

### Networking capabilities
{: #virt-networking-options}

Basic networking (4.17+)
:   - Pod network connectivity
    - Kubernetes Services and Routes
    - VPC load balancers
    - Standard VM networking

Advanced networking with VNIs (4.20+)
:   - Direct VPC network connectivity
    - Floating IP addresses
    - Network preservation during live migration
    - Multiple network interfaces per VM
    - See [Managing virtual network interfaces](/docs/openshift?topic=openshift-vni-virtualization)

## Key capabilities
{: #virt-capabilities}

Live migration
:   Move running VMs between nodes without downtime (within same zone)

VM templates
:   Pre-configured templates for common operating systems

Snapshots and cloning
:   Create VM snapshots and clones (with ODF storage)

Multi-zone deployment
:   Deploy across multiple zones for high availability

Integration
:   Works with IBM Cloud services (monitoring, logging, security)

## Limitations
{: #virt-limitations}

- Supported only on VPC bare metal worker nodes
- Requires Red Hat CoreOS (RHCOS) operating system
- Remote block volume attachment not supported for bare metal nodes
- Live migration supported only within the same zone
- VNI features require OpenShift 4.20 or later
- Windows VMs require appropriate licensing

## Getting started
{: #virt-next-steps}

Choose your deployment path:



For custom deployment:
1. [Plan your deployment](/docs/openshift?topic=openshift-virt-plan)
2. [Set up storage](/docs/openshift?topic=openshift-virt-storage-setup)
3. [Install the operator](/docs/openshift?topic=openshift-oc-virtualization)

Additional resources:
- [Managing virtual network interfaces](/docs/openshift?topic=openshift-vni-virtualization)
- [Red Hat OpenShift Virtualization documentation](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/virtualization/index){: external}
