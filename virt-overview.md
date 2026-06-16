---

copyright:
  years: 2025, 2026
lastupdated: "2026-06-16"

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

OpenShift Virtualization uses KubeVirt technology to enable virtual machine management within your Kubernetes environment. This unified platform allows you to run VMs and containers on the same infrastructure, manage VMs using familiar Kubernetes tools and APIs, and leverage enterprise storage solutions like OpenShift Data Foundation or IBM Cloud storage services.

## Key capabilities
{: #virt-capabilities}

OpenShift Virtualization on IBM Cloud provides enterprise-grade virtualization features integrated with your Kubernetes environment.

**Live migration** moves running VMs between nodes without downtime, allowing you to perform maintenance or rebalance workloads within the same zone. **VM templates** provide pre-configured templates for common operating systems, accelerating deployment. With **snapshots and cloning** (available with ODF storage), you can create VM snapshots and clones for backup, testing, or rapid deployment. **Multi-zone deployment** enables you to deploy across multiple zones for high availability, and **IBM Cloud integration** ensures your VMs work seamlessly with IBM Cloud services for monitoring, logging, and security.

**Flexible networking** options let you connect VMs to pod networks for standard Kubernetes networking, or use Virtual Network Interfaces (VNIs) in OpenShift 4.20+ for direct VPC network connectivity with floating IP addresses and network preservation during live migration.

## Deployment options
{: #virt-deployment-options}



Virtualization Service is currently available as a beta release. Access is controlled by an allowlist. During the beta period, only console-based cluster creation is supported.
{: beta}


| Deployment option | Description | Best for | Setup time | More information |
| ----------------- | ----------- | -------- | ---------- | ---------------- |
| OpenShift Virtualization Service (Recommended) | Ready-to-use virtualization environment with all components automatically installed and configured during cluster creation | VM-focused workloads, quick deployment, simplified management with managed add-ons, cost-optimized licensing | Minutes (automated) | [Get started](/docs/openshift?topic=openshift-rovs-getting-started), [Create cluster](/docs/openshift?topic=openshift-rovs-cluster-create), [Learn more](/docs/openshift?topic=openshift-rovs-overview) |
| Manual deployment | Full control over component selection and configuration. Create a standard cluster and manually install OpenShift Virtualization components | Mixed container and VM workloads, custom storage configurations, specific networking requirements, full control over all components | Hours (manual) | [Plan deployment](/docs/openshift?topic=openshift-virt-plan), [Set up storage](/docs/openshift?topic=openshift-virt-storage-setup), [Install operator](/docs/openshift?topic=openshift-oc-virtualization) |
{: caption="Deployment options for OpenShift Virtualization" caption-side="bottom"}

### Feature comparison
{: #virt-choose-deployment}

| Feature | Virtualization Service | Manual Deployment |
|---------|----------------------|-------------------|
| Setup time | Minutes (automated) | Hours (manual) |
| OpenShift version | 4.20+ | 4.17+ |
| Storage | ODF pre-configured with local NVME | Your choice (ODF, VPC File, etc.) |
| Networking | Pre-optimized (MTU 8900/9000) | Manual configuration |
| Licensing | OVE (cost-effective) | Full OCP |
| Management | Managed add-ons | Self-managed |
| Flexibility | Pre-configured | Full control |
| Best for | VM-focused workloads | Custom configurations |
{: caption="Deployment option feature comparison" caption-side="bottom"}


## Characteristics
{: #virt-requirements}

Both deployment options have the following characteristics:OpenShift Virtualization has the following characteristics:

| Category | Requirements |
| -------- | ------------ |
| Infrastructure | VPC with bare metal worker nodes, Red Hat CoreOS (RHCOS) operating system, OVN-Kubernetes CNI, outbound traffic protection disabled |
| Storage | ReadWriteMany (RWX) access mode support, OpenShift Data Foundation (recommended) or VPC File Storage |
| Networking | 100 Gbps (Gen 2) or 200 Gbps (Gen 3) network connectivity, MTU optimization for VM workloads |
{: caption="OpenShift Virtualization characteristics" caption-side="bottom"}

## Supported bare metal flavors
{: #virt-bm-flavors}

OpenShift Virtualization requires VPC bare metal worker nodes. The following flavors are supported:

| Flavor | Cores | Memory | Network | Local Storage | Min Version | Best for |
|--------|----------------|--------|---------|---------------|-------------|----------|
| `bx2.metal.96x384` | 48 | 384 GB | 100 Gbps | 960 GB SSD | All | Balanced workloads |
| `bx2d.metal.96x384` | 48 | 384 GB | 100 Gbps | 960 GB SSD | All | Balanced + ODF |
| `cx2.metal.96x192` | 48 | 192 GB | 100 Gbps | 960 GB SSD | All | Compute-intensive |
| `cx2d.metal.96x192` | 48 | 192 GB | 100 Gbps | 960 GB SSD | All | Compute + ODF |
| `mx2.metal.96x768` | 48 | 768 GB | 100 Gbps | 960 GB SSD | All | Memory-intensive |
| `mx2d.metal.96x768` | 48 | 768 GB | 100 Gbps | 960 GB SSD | All | Memory + ODF |
| `bx3.metal.48x256` | 24 | 256 GB | 100 Gbps | 480 GB SSD | 4.17+ | Small balanced |
| `bx3.metal.64x256` | 32 | 256 GB | 100 Gbps | 480 GB SSD | 4.17+ | Medium balanced |
| `bx3d.metal.48x256` | 24 | 256 GB | 100 Gbps | 480 GB SSD | 4.17+ | Small balanced + ODF |
| `bx3d.metal.64x256` | 32 | 256 GB | 100 Gbps | 480 GB SSD | 4.17+ | Medium balanced + ODF |
| `bx3d.metal.192x1024` | 96 | 1024 GB | 100 Gbps | 480 GB SSD | 4.17+ | Large balanced + ODF |
| `cx3d.metal.48x128` | 24 | 128 GB | 100 Gbps | 480 GB SSD | 4.17+ | Small compute + ODF |
| `cx3d.metal.64x128` | 32 | 128 GB | 100 Gbps | 480 GB SSD | 4.17+ | Medium compute + ODF |
| `mx3.metal.48x512` | 24 | 512 GB | 100 Gbps | 480 GB SSD | 4.17+ | Medium memory |
| `mx3.metal.64x512` | 32 | 512 GB | 100 Gbps | 480 GB SSD | 4.17+ | Large memory |
| `mx3d.metal.16x128` | 8 | 128 GB | 100 Gbps | 480 GB SSD | 4.17+ | Small memory + ODF |
| `mx3d.metal.48x512` | 24 | 512 GB | 100 Gbps | 480 GB SSD | 4.17+ | Medium memory + ODF |
| `mx3d.metal.64x512` | 32 | 512 GB | 100 Gbps | 480 GB SSD | 4.17+ | Large memory + ODF |
| `mx3d.metal.96x1024` | 48 | 1024 GB | 100 Gbps | 480 GB SSD | 4.17+ | XL memory + ODF |
| `mx3d.metal.128x1024` | 64 | 1024 GB | 100 Gbps | 480 GB SSD | 4.17+ | XXL memory + ODF |
| `mx3de.metal.48x512` | 24 | 512 GB | 100 Gbps | 480 GB SSD | 4.17+ | Medium memory + ODF + encryption |
| `mx3de.metal.64x512` | 32 | 512 GB | 100 Gbps | 480 GB SSD | 4.17+ | Large memory + ODF + encryption |
| `ux3de.metal.16x512` | 8 | 512 GB | 100 Gbps | 480 GB SSD | 4.17+ | Ultra-high memory + ODF + encryption |
{: caption="Supported bare metal flavors for OpenShift Virtualization" caption-side="bottom"}

Flavors with `d` suffix include local SSD storage, which is required for OpenShift Data Foundation. The `mx3de` and `ux3de` flavors provide encrypted local storage for enhanced security.
{: tip}

## Storage and networking
{: #virt-storage-networking}

### Storage options
{: #virt-storage-options}

| Storage | Performance | Snapshots | Cloning | Best for |
|---------|-------------|-----------|---------|----------|
| OpenShift Data Foundation | High | Yes | Yes | Production, high I/O workloads |
| VPC File Storage | Moderate | No | No | Development, cost-sensitive |
| IBM Storage Fusion | High | Yes | Yes | Enterprise with backup needs |
{: caption="Storage options for OpenShift Virtualization" caption-side="bottom"}

### Networking capabilities
{: #virt-networking-options}

| Networking option | Available in | Capabilities |
| ----------------- | ------------ | ------------ |
| Basic networking | OpenShift 4.17+ | Pod network connectivity, Kubernetes Services and Routes, VPC load balancers, standard VM networking |
| Advanced networking with VNIs | OpenShift 4.20+ | Direct VPC network connectivity, floating IP addresses, network preservation during live migration, multiple network interfaces per VM. See [Managing virtual network interfaces](/docs/openshift?topic=openshift-vni-virtualization) |
{: caption="Networking capabilities for OpenShift Virtualization" caption-side="bottom"}

Virtualization Service clusters running version 4.21 and later have access to advanced networking options, including enhanced capabilities for virtual network interfaces and improved network performance.
{: note}

## Limitations
{: #virt-limitations}

- Bare metal worker nodes are required; virtual server instances are not supported
- Red Hat CoreOS (RHCOS) operating system is required
- Remote block volume attachment is not supported for bare metal nodes
- Live migration is supported only within the same zone
- VNI features require OpenShift 4.20 or later
- Windows VMs require appropriate licensing
- If you mark more than one StorageClass with the annotation `storageclass.kubernetes.io/is-default-class: "true"`, the following occurs:
    - **Selection Logic**: For a PersistentVolumeClaim (PVC) created without a `storageClassName`, Kubernetes typically selects the most recently created default StorageClass.
    - **Potential Failure**: In some older versions or specific configurations, having multiple defaults might cause PVC creation to fail if no explicit class is specified, as the system cannot resolve which one to use.
    - **Monitoring Alerts**: In managed environments like OpenShift, having multiple defaults triggers a `MultipleDefaultStorageClasses` alert to warn administrators of the conflict.

## Getting started
{: #virt-next-steps}

Choose your deployment path:


For quick deployment:
1. [Get started with Virtualization Service](/docs/openshift?topic=openshift-rovs-getting-started)
2. [Create a Virtualization Service cluster](/docs/openshift?topic=openshift-rovs-cluster-create)


For custom deployment:
1. [Plan your deployment](/docs/openshift?topic=openshift-virt-plan)
2. [Set up storage](/docs/openshift?topic=openshift-virt-storage-setup)
3. [Install the operator](/docs/openshift?topic=openshift-oc-virtualization)

Additional resources:
- [Managing virtual network interfaces](/docs/openshift?topic=openshift-vni-virtualization)
- [Red Hat OpenShift Virtualization documentation](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/virtualization/index){: external}
