---

copyright:
  years: 2025, 2026
lastupdated: "2026-06-16"

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


[OpenShift Virtualization Service](/docs/openshift?topic=openshift-rovs-overview) is the fastest option with automatic setup of storage, networking, and operators - ready in minutes instead of hours.
{: tip}

This service is currently available as a beta release. Access is controlled by an allowlist. During the beta period, only console-based cluster creation is supported.
{: beta}


## Prerequisites
{: #virt-prereqs}

To deploy OpenShift Virtualization, you need an {{site.data.keyword.cloud_notm}} account with appropriate IAM permissions. Specifically, you need the **Operator** role for Kubernetes Service and either the **Editor** or **Administrator** role for VPC Infrastructure Services.

Your VPC infrastructure must include a VPC with subnets in your desired zones and sufficient quota for bare metal worker nodes. Your OpenShift cluster must be version 4.17 or later, running on VPC bare metal workers with RHCOS. The cluster must use the OVN-Kubernetes CNI, and outbound traffic protection must be disabled.

## Planning your cluster configuration
{: #virt-plan-cluster}

### Choosing bare metal flavors
{: #virt-plan-flavors}

Select bare metal flavors based on your workload requirements. For a complete list of supported flavors, see [Bare metal flavors](/docs/openshift?topic=openshift-virt-overview#virt-bm-flavors).

If you plan to use OpenShift Data Foundation (ODF), choose bare metal flavors with the `d` suffix or `3d` in the name, which include NVME local storage. ODF requires local disks for optimal performance. For VPC File Storage, any supported bare metal flavor can be used, though flavors with local storage are still recommended for better overall performance.

Match your bare metal flavor to your workload type. For high-performance workloads, choose bare metal flavors with local storage and ODF. Memory-intensive workloads perform best on `mx` series bare metal flavors, while compute-intensive workloads benefit from `cx` series flavors. For balanced workloads, select `bx` series bare metal flavors. If cost optimization is your priority, consider smaller bare metal flavors with VPC File Storage.

### Worker pool architecture
{: #virt-plan-worker-pools}

For cost optimization, consider a two-pool setup with a bare metal pool for VM workloads and a VSI pool for infrastructure components. Alternatively, you can use a single-pool setup where all components run on bare metal nodes. This approach is simpler but has higher costs.

Single-zone deployments are recommended for virtualization workloads because they minimize storage latency for VM workloads, simplify VNI configuration (VNIs are zone-specific), and reduce cross-zone storage replication overhead. Multi-zone deployments provide better high availability, and ODF requires 3 or more zones for HA. However, cross-zone storage replication can impact VM performance, and you should avoid cross-zone VM migration when using VNIs.

## Planning your storage solution
{: #virt-plan-storage}

OpenShift Virtualization requires storage that supports ReadWriteMany (RWX) access mode. Choose a storage solution based on your workload requirements.

### Storage decision matrix
{: #virt-storage-matrix}

| Use case | OpenShift Data Foundation | VPC File Storage |
|----------|---------------------------|------------------|
| High availability (multi-zone) | Recommended | Not recommended |
| High read/write workloads | Recommended | Possible with high IOPS classes |
| Low read/write or non-production | Costly | Recommended |
| Snapshot and cloning support | Supported | Not supported |
| Live migration | Supported | Supported |
| Cost | Higher | Lower |
{: caption="Storage solution comparison"}

### Storage options
{: #virt-storage-options}

OpenShift Data Foundation (ODF)
:   ODF is best suited for production environments with high I/O requirements and when you need snapshot or cloning support. ODF requires bare metal with local NVME storage, at least 3 nodes, and 3 or more zones for high availability. For more information, see [Understanding ODF](/docs/openshift?topic=openshift-ocs-storage-prep).


VPC File Storage
:   VPC File storage is ideal for development environments, cost-sensitive deployments, and workloads with low to moderate I/O requirements. You can use any bare metal flavor with VPC File Storage, and you need the VPC File CSI driver. Note that VPC File Storage does not support snapshots or cloning. For best performance, use the `ibmc-vpc-file-1000-iops` or `ibmc-vpc-file-6000-iops` storage classes. For more information, see [VPC File Storage profiles](/docs/vpc?topic=vpc-file-storage-profiles).


## Planning your networking setup
{: #virt-plan-networking}

### Networking options
{: #virt-plan-networking-options}

OpenShift 4.17 and later supports basic networking, which uses the default pod network, Services, Routes, and VPC load balancers. For more advanced networking capabilities, OpenShift 4.20 and later supports Virtual Network Interfaces (VNIs), which provide direct VPC connectivity, floating IPs, and network preservation during migration. VNIs require the NMState operator, OVS bridges, UDNs, and the OVN-Kubernetes CNI. Keep in mind that VNIs are zone-specific. The VNI feature is generally available with OpenShift 4.20.



The VNI feature is generally available. A small number of accounts might still be blocked; contact IBM Cloud support if you need access.
{: note}

For information about installing the NMState operator and configuring VNIs, see [Managing virtual network interfaces for OpenShift Virtualization](/docs/openshift?topic=openshift-vni-virtualization).


## Node placement
{: #virt-plan-node-placement}

For cost optimization, deploy infrastructure components such as KubeVirt operators, CDI, and controllers on VSI nodes using node selectors or taints and tolerations. Deploy VM workloads on bare metal nodes for best performance, using node selectors to target bare metal nodes.

An effective placement strategy involves creating separate `baremetal-pool` and `vsi-pool` worker pools, then labeling nodes appropriately. Label bare metal nodes with `node-role.kubernetes.io/worker-vm=true` and VSI nodes with `node-role.kubernetes.io/infra=true`. Finally, configure the HyperConverged CR with node placement rules to enforce this separation.

## Sizing and optimization
{: #virt-plan-sizing}

The minimum cluster configuration requires 3 bare metal nodes in a single zone. For production deployments, a single-zone configuration is recommended with 3 or more bare metal nodes plus additional VSI nodes for infrastructure. If you need high availability, deploy 3 or more bare metal nodes per zone across 3 zones, along with additional VSI nodes for infrastructure.

When planning VM resources, reserve approximately 10 vCPU and 32 GB RAM per node for system overhead. For example, a 96 vCPU node provides approximately 86 vCPU for VMs.

To optimize costs, use VPC File Storage for non-production environments, deploy infrastructure components on VSIs, right-size your VM resources, use appropriate storage IOPS classes, and consider reserved capacity for long-term use. For more information, see [Understanding cluster costs](/docs/openshift?topic=openshift-costs).

For security, use security groups and network policies to control traffic, enable storage encryption to protect data at rest, configure RBAC for VM management to control access, and use {{site.data.keyword.secrets-manager_short}} for sensitive data such as credentials and certificates.

## Next steps
{: #virt-plan-next-steps}

After planning your deployment:

1. [Set up storage for OpenShift Virtualization](/docs/openshift?topic=openshift-virt-storage-setup)
2. [Install the OpenShift Virtualization Operator](/docs/openshift?topic=openshift-oc-virtualization) (not required for [OpenShift Virtualization Service](/docs/openshift?topic=openshift-rovs-getting-started) - operators are pre-installed)
3. [Configure virtual network interfaces (optional)](/docs/openshift?topic=openshift-vni-virtualization) (for Virtualization Service, skip the NMState operator installation and NNCP resource creation steps)
