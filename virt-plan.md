---

copyright:
  years: 2025, 2026
lastupdated: "2026-05-04"

keywords: openshift, virtualization, planning, prerequisites, bare metal

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Planning your OpenShift Virtualization deployment
{: #virt-plan}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

Before you deploy OpenShift Virtualization on {{site.data.keyword.openshiftlong_notm}}, review the prerequisites and plan your cluster configuration, storage solution, and networking setup.
{: shortdesc}

## Prerequisites
{: #virt-prereqs}

Account and permissions
:   - {{site.data.keyword.cloud_notm}} account with IAM permissions for Kubernetes Service and VPC Infrastructure
    - **Operator** role for Kubernetes Service
    - **Editor** or **Administrator** role for VPC Infrastructure Services

Infrastructure
:   - VPC with subnets in desired zones
    - Sufficient quota for bare metal worker nodes

Cluster
:   - OpenShift 4.17 or later
    - VPC bare metal workers with RHCOS
    - OVN-Kubernetes CNI (required)
    - Outbound traffic protection disabled

## Planning your cluster configuration
{: #virt-plan-cluster}

### Choosing bare metal flavors
{: #virt-plan-flavors}

Select bare metal flavors based on your workload requirements. For a complete list of supported flavors, see [Bare metal flavors](/docs/openshift?topic=openshift-virt-overview#virt-bm-flavors).

For OpenShift Data Foundation (ODF)
:   Use bare metal flavors with the `d` suffix or `3d` in the name, which include NVME local storage. ODF requires local disks for optimal performance.



Workload considerations
:   - **High-performance workloads**: Choose bare metal flavors with local storage and ODF
:   - **Memory-intensive workloads**: Choose `mx` series bare metal flavors
:   - **Compute-intensive workloads**: Choose `cx` series bare metal flavors
:   - **Balanced workloads**: Choose `bx` series bare metal flavors
:   - **Cost-optimized workloads**: Choose smaller bare metal flavors with VPC File Storage

### Worker pool architecture
{: #virt-plan-worker-pools}

Two-pool setup (recommended for cost optimization)
:   - Bare metal pool for VM workloads
    - VSI pool for infrastructure components

Single-pool setup
:   - All components on bare metal nodes
    - Simpler but higher cost

Single-zone deployments (recommended for virtualization)
:   - Minimizes storage latency for VM workloads
    - Simplifies VNI configuration (VNIs are zone-specific)
    - Reduces cross-zone storage replication overhead

Multi-zone deployments
:   - Provides better high availability
    - ODF requires 3+ zones for HA
    - Cross-zone storage replication can impact VM performance
    - Avoid cross-zone VM migration when using VNIs

## Planning your storage solution
{: #virt-plan-storage}

OpenShift Virtualization requires storage that supports ReadWriteMany (RWX) access mode. Choose a storage solution based on your workload requirements.

### Storage decision matrix
{: #virt-storage-matrix}

| Use case | OpenShift Data Foundation |
|----------|---------------------------|
| High availability (multi-zone) | Recommended |
| High read/write workloads | Recommended |
| Low read/write or non-production | Costly |
| Snapshot and cloning support | Supported |
| Live migration | Supported |
| Cost | Higher |
{: caption="Storage solution comparison"}

### Storage options
{: #virt-storage-options}

OpenShift Data Foundation (ODF)
:   - Best for: Production, high I/O, snapshots/cloning needed
    - Requires: Bare metal with local NVME storage, 3+ nodes, 3+ zones for HA
    - See [Understanding ODF](/docs/openshift?topic=openshift-ocs-storage-prep)



## Planning your networking setup
{: #virt-plan-networking}

### Networking options
{: #virt-plan-networking}

Basic networking (4.17+)
:   Default pod network, Services, Routes, VPC load balancers

Advanced with VNIs (4.20+)
:   - Direct VPC connectivity, floating IPs, network preservation during migration
    - Requires: NMState operator, OVS bridges, UDNs, OVN-Kubernetes CNI
    - VNIs are zone-specific
    - Generally available with OpenShift 4.20



The VNI feature is generally available. A small number of accounts may still be blocked; contact IBM Cloud support if you need access.
{: note}

For information about installing the NMState operator and configuring VNIs, see [Managing virtual network interfaces for OpenShift Virtualization](/docs/openshift?topic=openshift-vni-virtualization).


## Node placement
{: #virt-plan-node-placement}

Infrastructure components (KubeVirt operators, CDI, controllers)
:   - Deploy on VSI nodes for cost optimization
    - Use node selectors or taints/tolerations

VM workloads
:   - Deploy on bare metal nodes for best performance
    - Use node selectors to target bare metal nodes

Example strategy
:   1. Create `baremetal-pool` and `vsi-pool`
    2. Label nodes: `node-role.kubernetes.io/worker-vm=true` (bare metal), `node-role.kubernetes.io/infra=true` (VSI)
    3. Configure HyperConverged CR with node placement rules

## Sizing and optimization
{: #virt-plan-sizing}

Minimum cluster
:   3 bare metal nodes in a single zone

Production cluster (single-zone recommended)
:   3+ bare metal nodes in a single zone, additional VSI nodes for infrastructure

Production cluster (multi-zone for HA)
:   3+ bare metal nodes per zone, 3 zones, additional VSI nodes for infrastructure

VM resource planning
:   - Reserve ~10 vCPU and ~32 GB RAM per node for system overhead
    - Example: 96 vCPU node provides ~86 vCPU for VMs

Cost optimization
:   Deploy infrastructure on VSIs
    3. Right-size VM resources
    4. Use appropriate storage IOPS classes
    5. Consider reserved capacity for long-term use

    See [Understanding cluster costs](/docs/openshift?topic=openshift-costs).

Security
:   - Use security groups and network policies
    - Enable storage encryption
    - Configure RBAC for VM management
    - Use {{site.data.keyword.secrets-manager_short}} for sensitive data

## Next steps
{: #virt-plan-next-steps}

After planning your deployment:

1. [Set up storage for OpenShift Virtualization](/docs/openshift?topic=openshift-virt-storage-setup)
2. [Install the OpenShift Virtualization Operator](/docs/openshift?topic=openshift-oc-virtualization)
3. [Configure virtual network interfaces (optional)](/docs/openshift?topic=openshift-vni-virtualization)
