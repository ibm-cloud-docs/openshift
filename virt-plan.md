---

copyright:
  years: 2025, 2026
lastupdated: "2026-04-16"

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

**For OpenShift Data Foundation (ODF)**
:   Use bare metal flavors with the `d` suffix or `3d` in the name, which include NVME local storage. ODF requires local disks for optimal performance.

**For VPC File Storage**
:   Any supported bare metal flavor can be used. However, flavors with local storage are still recommended for better overall performance.

**Workload considerations**
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

Multi-zone deployments
:   - ODF requires 3+ zones for high availability

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
:   - Best for: Production, high I/O, snapshots/cloning needed
    - Requires: Bare metal with local NVME storage, 3+ nodes, 3+ zones for HA
    - See [Understanding ODF](/docs/openshift?topic=openshift-ocs-storage-prep)

VPC File Storage
:   - Best for: Development, cost-sensitive, low-moderate I/O
    - Requires: Any bare metal flavor, VPC File CSI driver
    - No snapshot/cloning support
    - Recommended classes: `ibmc-vpc-file-1000-iops` or `ibmc-vpc-file-6000-iops`
    - See [VPC File Storage profiles](/docs/vpc?topic=vpc-file-storage-profiles)

## Planning your networking setup
{: #virt-plan-networking}

### Networking options
{: #virt-plan-networking}

Basic networking (4.17+)
:   Default pod network, Services, Routes, VPC load balancers



The VNI feature is generally available. A small number of accounts may still be blocked; contact IBM Cloud support if you need access.
{: note}

### Installing the NMState operator
{: #virt-plan-nmstate}

The Kubernetes NMState operator is required for advanced networking with VNIs. Install it before configuring virtual network interfaces.

**From the console**

1. In the OpenShift console, navigate to **Ecosystem** > **OperatorHub** (or **Operators** > **OperatorHub** in earlier versions).

2. Search for **Kubernetes NMState Operator**.

3. Click the **Kubernetes NMState Operator** tile and then click **Install**.

4. On the Install Operator page, accept the default settings:
   - **Update channel**: stable
   - **Installation mode**: All namespaces on the cluster
   - **Installed Namespace**: openshift-nmstate
   - **Update approval**: Automatic

5. Click **Install**.

6. Wait for the operator installation to complete.

**From the CLI**

1. Create the namespace for the NMState operator.
   ```sh
   cat <<EOF | oc apply -f -
   apiVersion: v1
   kind: Namespace
   metadata:
     name: openshift-nmstate
   EOF
   ```
   {: codeblock}

2. Create an OperatorGroup.
   ```sh
   cat <<EOF | oc apply -f -
   apiVersion: operators.coreos.com/v1
   kind: OperatorGroup
   metadata:
     name: openshift-nmstate
     namespace: openshift-nmstate
   spec: {}
   EOF
   ```
   {: codeblock}

3. Create a Subscription to install the operator.
   ```sh
   cat <<EOF | oc apply -f -
   apiVersion: operators.coreos.com/v1alpha1
   kind: Subscription
   metadata:
     name: kubernetes-nmstate-operator
     namespace: openshift-nmstate
   spec:
     channel: stable
     name: kubernetes-nmstate-operator
     source: redhat-operators
     sourceNamespace: openshift-marketplace
   EOF
   ```
   {: codeblock}

4. Verify the operator installation.
   ```sh
   oc get csv -n openshift-nmstate
   ```
   {: pre}

5. Create an NMState instance.
   ```sh
   cat <<EOF | oc apply -f -
   apiVersion: nmstate.io/v1
   kind: NMState
   metadata:
     name: nmstate
   EOF
   ```
   {: codeblock}

6. Verify the NMState pods are running.
   ```sh
   oc get pods -n openshift-nmstate
   ```
   {: pre}

For more information, see [Installing the Kubernetes NMState Operator](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html-single/networking_operators/index#installing-the-kubernetes-nmstate-operator-cli){: external}.

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
:   3 bare metal nodes, 1 or 3 zones

Production cluster
:   3+ bare metal nodes per zone, 3 zones, additional VSI nodes for infrastructure

VM resource planning
:   - Reserve ~10 vCPU and ~32 GB RAM per node for system overhead
    - Example: 96 vCPU node provides ~86 vCPU for VMs

Cost optimization
:   1. Use VPC File Storage for non-production
    2. Deploy infrastructure on VSIs
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
2. [Install the OpenShift Virtualization Operator](/docs/openshift?topic=openshift-virt-install)
