---

copyright:
  years: 2025, 2026
lastupdated: "2026-04-16"

keywords: openshift, virtualization, virtual machines, vms, bare metal

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Understanding OpenShift Virtualization
{: #virt-overview}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

OpenShift Virtualization enables you to run virtual machines (VMs) alongside containerized workloads on {{site.data.keyword.openshiftlong_notm}} clusters, providing a unified platform for both traditional and cloud-native applications.
{: shortdesc}

## What is OpenShift Virtualization?
{: #virt-what-is}

OpenShift Virtualization uses KubeVirt technology to run virtual machines alongside containerized workloads in your Kubernetes environment. You can:

- Run traditional VM-based applications with containerized workloads
- Migrate existing VMs to a cloud-native platform
- Manage VMs using Kubernetes tools and APIs
- Live migrate VMs between nodes without downtime

## Requirements
{: #virt-requirements}

- {{site.data.keyword.openshiftlong_notm}} version 4.17 or later
- VPC bare metal worker nodes
- Red Hat CoreOS (RHCOS) operating system
- OVN-Kubernetes CNI
- Outbound traffic protection disabled
- Storage with ReadWriteMany (RWX) access mode

## Supported configurations
{: #virt-supported-configs}

### Cluster requirements
{: #virt-cluster-reqs}

- {{site.data.keyword.openshiftlong_notm}} version 4.17 or later
- VPC infrastructure
- Bare metal worker nodes with supported flavors
- Red Hat CoreOS (RHCOS) operating system
- OVN-Kubernetes container network interface (CNI)
- Outbound traffic protection disabled

### Bare metal flavors
{: #virt-bm-flavors}

The following VPC bare metal flavors are supported for OpenShift Virtualization:

| Flavor | Generation | vCPU | Memory | Network | Local Storage | Min Version |
|--------|------------|------|--------|---------|---------------|-------------|
| `bx2.metal.96x384` | 2 | 96 | 384 GB | 100 Gbps | - | All |
| `bx2d.metal.96x384` | 2 | 96 | 384 GB | 100 Gbps | 480 GB NVME | All |
| `cx2.metal.96x192` | 2 | 96 | 192 GB | 100 Gbps | - | All |
| `cx2d.metal.96x192` | 2 | 96 | 192 GB | 100 Gbps | 480 GB NVME | All |
| `mx2.metal.96x768` | 2 | 96 | 768 GB | 100 Gbps | - | All |
| `mx2d.metal.96x768` | 2 | 96 | 768 GB | 100 Gbps | 480 GB NVME | All |
| `bx3d.metal.48x256` | 3 | 24 | 256 GB | 200 Gbps | 480 GB NVME | 4.17+ |
| `bx3d.metal.64x256` | 3 | 32 | 256 GB | 200 Gbps | 480 GB NVME | 4.17+ |
| `bx3d.metal.192x1024` | 3 | 96 | 1024 GB | 200 Gbps | 480 GB NVME | 4.17+ |
| `cx3d.metal.48x128` | 3 | 24 | 128 GB | 200 Gbps | 480 GB NVME | 4.17+ |
| `cx3d.metal.64x128` | 3 | 32 | 128 GB | 200 Gbps | 480 GB NVME | 4.17+ |
| `mx3d.metal.16x128` | 3 | 8 | 128 GB | 200 Gbps | 480 GB NVME | 4.17+ |
| `mx3d.metal.48x512` | 3 | 24 | 512 GB | 200 Gbps | 480 GB NVME | 4.17+ |
| `mx3d.metal.64x512` | 3 | 32 | 512 GB | 200 Gbps | 480 GB NVME | 4.17+ |
| `mx3d.metal.96x1024` | 3 | 48 | 1024 GB | 200 Gbps | 480 GB NVME | 4.17+ |
| `mx3d.metal.128x1024` | 3 | 64 | 1024 GB | 200 Gbps | 480 GB NVME | 4.17+ |
{: caption="Supported bare metal flavors for OpenShift Virtualization"}

Generation 2 flavors with `d` suffix and all Generation 3 flavors include NVME local storage, which is recommended for OpenShift Data Foundation deployments. Generation 3 flavors offer improved network performance (200 Gbps) and are available for clusters running OpenShift 4.17 and later.
{: tip}

### Storage options
{: #virt-storage-options}

| Storage | Performance | Snapshots | Cloning | Best for |
|---------|-------------|-----------|---------|----------|
| OpenShift Data Foundation (ODF) | High | Yes | Yes | Production workloads |
| {{site.data.keyword.filestorage_vpc_short}} | Moderate | No | No | Development, cost-sensitive workloads |
| IBM Storage Fusion | High | Yes | Yes | Enterprise workloads with backup needs |
{: caption="Storage options for OpenShift Virtualization"}

For detailed guidance, see [Planning storage](/docs/openshift?topic=openshift-virt-plan#virt-plan-storage).

### Networking options
{: #virt-networking-options}

Basic networking (4.17+)
:   Use default pod network, Kubernetes Services, Routes, and VPC load balancers.



## Limitations
{: #virt-limitations}

- OpenShift Virtualization is supported only on VPC bare metal worker nodes
- Remote block volume attachment is not supported for VPC bare metal nodes

- Live migration is supported only within the same zone
- Windows VMs require appropriate licensing

## Next steps
{: #virt-next-steps}

- [Planning your OpenShift Virtualization deployment](/docs/openshift?topic=openshift-virt-plan)
- [Setting up storage for OpenShift Virtualization](/docs/openshift?topic=openshift-virt-storage-setup)
- [Installing the OpenShift Virtualization Operator](/docs/openshift?topic=openshift-virt-install)
