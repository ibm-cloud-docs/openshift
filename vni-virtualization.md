---

copyright:
  years: 2026, 2026
lastupdated: "2026-04-21"

keywords: openshift, vni, virtual network interface, virtualization, bare metal, localnet, udn

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Managing virtual network interfaces for OpenShift Virtualization
{: #vni-virtualization}

[Virtual Private Cloud]{: tag-vpc}
[4.20 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}
[OVN-Kubernetes CNI required]{: tag-blue}

You can use Virtual Network Interfaces (VNIs) to enable advanced network connectivity for virtual machines (VMs) running on {{site.data.keyword.openshiftlong_notm}} clusters with OpenShift Virtualization.
{: shortdesc}

VNI support for OpenShift Virtualization is available for allowlisted accounts only. To request access, see [Requesting access to allowlisted features](/docs/openshift?topic=openshift-allowlist-request).
{: important}

## Understanding Virtual Network Interfaces
{: #vni-about}

A Virtual Network Interface (VNI) is an {{site.data.keyword.cloud_notm}} VPC abstraction that represents individual network connections. VNIs embed properties of a network connection, such as IP addresses, MAC addresses, and the VPC subnet they belong to. Floating IPs and secondary IPs can be attached directly to a VNI.

VNIs are available only on clusters with bare metal worker nodes.
{: note}

{{site.data.keyword.openshiftlong_notm}} uses VNI-based network attachments to enable flexible connectivity between workloads running on the cluster and outside the cluster. VNIs enable direct network exposure of OpenShift Virtualization-based virtual machines (VMs) to the VPC network by using OVN User Defined Networks (UDN) with the `Localnet` topology. With VNIs attached to bare metal worker nodes, live migrations of VMs can preserve network connections, as the VNI can implicitly float and follow the VM workload between bare metal worker instances within the same zone.

### Key features
{: #vni-features}

Static VNIs per worker node
:   When you create a bare metal-based {{site.data.keyword.openshiftshort}} cluster or a new worker pool in IBM Cloud VPC, two VNIs are automatically created and attached statically to every bare metal worker node. One VNI handles regular worker traffic (pod network, overlay UDNs, and master communication). The second VNI acts as a carrier for dynamic VNI attachments that you manage.

Dynamic VNI attachments
:   You can create and manage VNIs on-demand after cluster creation. Dynamic VNIs can be attached to specific workers or configured to float between workers in the same zone, following VM workloads during live migration.

Live migration support
:   With VNIs attached to bare metal worker nodes, live migrations of OpenShift Virtualization-based VMs can preserve network connections. The VNI implicitly floats and follows the workload between bare metal worker instances within the same zone.

Zone constraints
:   VNIs are attached to a specific VPC subnet and cannot float between zones. In multi-zone {{site.data.keyword.openshiftshort}} clusters, VNIs can handle traffic only for workloads running on cluster workers in the same zone where the VNI is provisioned. This also means you must avoid OpenShift Virtualization VM live migration between zones when the specific VM is using a VNI on a Localnet UDN.

### Cross-account attachment
{: #vni-cross-account}

In {{site.data.keyword.openshiftlong_notm}}, worker nodes are not provisioned in your account, which means the lifecycle management of VNIs is slightly different from standalone VPC bare metal instances. The {{site.data.keyword.openshiftshort}} cluster administrator has different visibility to the attachments of the VNIs because they are attached to workloads that are not visible within the account. The differences in VNI management are covered in this documentation.

For more information about VNIs on standalone VPC bare metal instances, see [About virtual network interfaces](/docs/vpc?topic=vpc-vni-about).

## Prerequisites
{: #vni-prereqs}

Before you begin, make sure that you have the following resources and permissions.

- A {{site.data.keyword.openshiftlong_notm}} cluster at version 4.20 or later with bare metal worker nodes
- VPC infrastructure with VNIs created
- RHCOS operating system on worker nodes
- [OpenShift Virtualization Operator installed](/docs/openshift?topic=openshift-virt-install)
- [Storage configured for OpenShift Virtualization](/docs/openshift?topic=openshift-virt-storage-setup)
- The **Operator** platform access role for **Kubernetes Service** in {{site.data.keyword.cloud_notm}} IAM
- The **Editor** or **Administrator** platform access role for VPC Infrastructure Services in {{site.data.keyword.cloud_notm}} IAM
- Allowlisted account access for VNI features
- OVN-Kubernetes CNI (required for VNI support in 4.20+)

For general information about multi-network configurations, see the [Red Hat OpenShift multiple networks documentation](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/multiple_networks/index){: external}.
{: tip}

## Creating overlay UDNs for Pods and VMs
{: #vni-overlay-udns}

You can create overlay User Defined Networks for use with pods or VM workloads. The OpenShift console UI experience for User Defined Networks is subject to change with recent releases. The examples in this documentation use YAML definitions for reusability.

### Creating a Primary UDN
{: #vni-primary-udn}

To use a Primary User Defined Network for pods or VM workload, first create the UDN itself.

Example for a Cluster User Defined Network that can be used across namespaces:

```yaml
apiVersion: k8s.ovn.org/v1
kind: ClusterUserDefinedNetwork
metadata:
  name: primary
spec:
  namespaceSelector:
    matchLabels:
      kubernetes.io/metadata.name: green
  network:
    layer2:
      ipam:
        lifecycle: Persistent
      role: Primary
      subnets:
        - 10.0.0.0/24
    topology: Layer2
```
{: codeblock}

Then, create the namespace(s) that will use it. The namespace must contain a specific label (called `k8s.ovn.org/primary-user-defined-network`) on creation for Primary UDN usage.

Example:

```yaml
kind: Namespace
apiVersion: v1
metadata:
  name: green
  labels:
    k8s.ovn.org/primary-user-defined-network: ''
```
{: codeblock}

Once the (C)UDN and the namespaces are in place, any workload created in this namespace will access the UDN with the default route.

### Creating a Secondary UDN
{: #vni-secondary-udn}

Secondary UDN configuration is similar to Primary UDN, but with the role set to `Secondary`. For detailed information, see the [Red Hat OpenShift multiple networks documentation](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/multiple_networks/index){: external}.

## Exposing VMs with VPC load balancers
{: #vni-alb-lbaas}

You can expose VMs without using UDN or localnet VNI by using VPC Application Load Balancers. For more information about configuring load balancers, see [About VPC load balancers](/docs/openshift?topic=openshift-vpc-lbaas).

## Setting up localnet user defined networks
{: #vni-setup-localnet}

Localnet UDNs require preparation of the {{site.data.keyword.openshiftshort}} cluster's OVN network. On bare metal cluster nodes, the two static network interfaces have predictable names on the host operating system. The network interface dedicated to carrying dynamic attached VNI traffic is called `eth1`. Leveraging Localnet requires the creation of a dedicated OVS bridge on the bare metal cluster nodes, on top of `eth1`. Prepare a VLAN ID that you will use to attach the VNIs. It will be referred to in the CUDN resource as well.

### Installing the NMState operator
{: #vni-install-nmstate}

1. Deploy the NMState Operator from the OperatorHub in the {{site.data.keyword.openshiftshort}} console or by using the CLI.

2. Create an NMState instance with the default configuration.
    ```yaml
    apiVersion: nmstate.io/v1
    kind: NMState
    metadata:
      name: nmstate
    spec:
      probeConfiguration:
        dns:
          host: root-servers.net
    ```
    {: codeblock}

### Creating the OVS bridge
{: #vni-create-bridge}

1. Create a dedicated OVS bridge with `eth1` attached to it by deploying the following NMState custom resource.
    ```yaml
    apiVersion: nmstate.io/v1
    kind: NodeNetworkConfigurationPolicy
    metadata:
      name: "br-eth1"
    spec:
      desiredState:
        interfaces:
        - name: "br-eth1"
          description: A dedicated OVS bridge with a NIC as a port
          type: ovs-bridge
          state: up
          bridge:
            allow-extra-patch-ports: true
            options:
              stp: false
            port:
            - name: "eth1"
    ```
    {: codeblock}

2. Check the custom resource status and wait until all applicable cluster nodes reconcile the bridge creation request.

3. Patch the new OVS bridge to the default one by creating the following NMState custom resource. Replace `vpc-vlans` with your desired network name.
    ```yaml
    apiVersion: nmstate.io/v1
    kind: NodeNetworkConfigurationPolicy
    metadata:
      name: "vpc-vlans"
    spec:
      desiredState:
        ovn:
          bridge-mappings:
          - localnet: "vpc-vlans"
            bridge: "br-eth1"
            state: present
    ```
    {: codeblock}

4. Check the custom resource status and wait until all applicable cluster nodes reconcile the bridge mapping request.

### Creating a localnet user defined network
{: #vni-create-udn}

Create a UDN or ClusterUserDefinedNetwork (CUDN) that makes available the traffic from VNIs by using the selected VLAN.

```yaml
apiVersion: k8s.ovn.org/v1
kind: ClusterUserDefinedNetwork
metadata:
  name: "vlan250"
spec:
  namespaceSelector:
    matchExpressions:
    - key: kubernetes.io/metadata.name
      operator: In
      values:
      - "default"
  network:
    topology: Localnet
    localnet:
      role: "Secondary"
      physicalNetworkName: "vpc-vlans"
      ipam:
        mode: Disabled
      vlan:
        mode: Access
        access:
          id: 250
```
{: codeblock}

Replace the following values:
- `vlan250`: The name of your CUDN
- `default`: The namespace where you want to use the CUDN
- `vpc-vlans`: The physical network name you defined in the bridge mapping
- `250`: Your desired VLAN ID (range: 1-500)

This concludes the network plumbing of a specific VLAN. You can define multiple CUDNs by using different VLAN IDs while reusing the bridge mappings.
{: tip}

After completing the localnet UDN setup, use the IBM Cloud CLI `ks vni` command to attach VNIs to the cluster. See the command examples in the following sections.

## Attaching VNIs to your cluster
{: #vni-attach}

After you set up the localnet UDN, you can attach VNIs to your cluster by using the {{site.data.keyword.cloud_notm}} CLI.

### Before you begin
{: #vni-attach-prereqs}

1. [Create VNIs in your VPC](/docs/vpc?topic=vpc-vni-create&interface=cli) with the appropriate subnet and IP address configuration.

2. Make sure that you are logged in to the {{site.data.keyword.cloud_notm}} CLI with an account that has permissions to manage both the cluster and VNIs.

### Attaching a VNI
{: #vni-attach-steps}

You can attach a VNI to a specific worker node (non-floating) or to the cluster (floating). Floating VNIs can follow workloads between workers in the same zone.

To attach a VNI to a specific worker node, run the following command.
```sh
ibmcloud ks experimental vni attach baremetal --worker WORKER_ID --vni VNI_ID --vlan VLAN_ID [--auto-delete]
```
{: pre}

To attach a floating VNI to the cluster, run the following command.
```sh
ibmcloud ks experimental vni attach baremetal --cluster-id CLUSTER_ID --vni VNI_ID --vlan VLAN_ID [--auto-delete]
```
{: pre}

`--worker WORKER_ID`
:   The ID of the worker node. To list worker IDs, run `ibmcloud ks workers --cluster CLUSTER`.

`--cluster-id CLUSTER_ID`
:   The ID of the cluster. To list cluster IDs, run `ibmcloud ks clusters`.

`--vni VNI_ID`
:   The ID of the VNI to attach.

`--vlan VLAN_ID`
:   The VLAN ID for the attachment (range: 1-500). This must match the VLAN ID in your CUDN configuration.

`--auto-delete`
:   Optional: Automatically delete the VNI when it is removed from the cluster.

VNIs, subnets, and worker nodes are zonal resources. The VNI compute zone must match the selected worker zone. For floating attachments, the zone of the VNI is assumed, and the floating attachment also has the zone constraint. VNIs can be attached from arbitrary subnets, but only from within the same VPC as the cluster.
{: note}

### Example
{: #vni-attach-example}

```sh
ibmcloud ks experimental vni attach baremetal --vni 0716-aac49630-f3b4-4ef6-9a3a-5145481697ba --worker kube-c9pqfcmw0tq431jdnrrg-mycluster-default-00000123 --vlan 251
```
{: pre}

Example output
```sh
OK
Successfully attached VNI 0716-aac49630-f3b4-4ef6-9a3a-5145481697ba to worker node kube-c9pqfcmw0tq431jdnrrg-mycluster-default-00000123.
Worker Node ID                                         VNI ID                                      VLAN ID
kube-c9pqfcmw0tq431jdnrrg-mycluster-default-00000123   0716-aac49630-f3b4-4ef6-9a3a-5145481697ba   251
```
{: screen}

## Listing VNI attachments
{: #vni-list}

To list all VNIs attached to a cluster, run the following command.
```sh
ibmcloud ks experimental vni ls --cluster-id CLUSTER_ID
```
{: pre}

To list VNIs attached to a specific worker, run the following command.
```sh
ibmcloud ks experimental vni ls --worker WORKER_ID
```
{: pre}

### Example output
{: #vni-list-example}

```sh
ibmcloud ks experimental vni ls --cluster-id c9pqfcmw0tq431jdnrrg
```
{: pre}

```sh
OK
VNI ID                                      Worker Node                                            IP Address   MAC Address         VLAN   Floating   Auto-delete
0716-d97d3626-acb2-476b-8b12-bcafa1dec5bb   kube-c9pqfcmw0tq431jdnrrg-mycluster-default-00000456   10.240.1.5   02:00:02:00:73:A5   250    -          false
0716-aac49630-f3b4-4ef6-9a3a-5145481697ba   kube-c9pqfcmw0tq431jdnrrg-mycluster-default-00000123   10.240.1.4   02:00:01:00:73:A5   251    -          false
```
{: screen}

## Detaching VNIs
{: #vni-detach}

To detach a VNI from a worker node, you must specify both the VNI ID and the worker ID.

```sh
ibmcloud ks experimental vni detach --worker WORKER_ID --vni VNI_ID
```
{: pre}

For floating VNIs, first list the VNIs to find the current worker ID, then detach using that worker ID.
{: tip}

### Example
{: #vni-detach-example}

```sh
ibmcloud ks experimental vni detach --vni 0716-aac49630-f3b4-4ef6-9a3a-5145481697ba --worker kube-c9pqfcmw0tq431jdnrrg-mycluster-default-00000123
```
{: pre}

```sh
Detach VNI 0716-aac49630-f3b4-4ef6-9a3a-5145481697ba from worker node kube-c9pqfcmw0tq431jdnrrg-mycluster-default-00000123? This action cannot be undone. [y/N]> y
OK
Successfully detached VNI 0716-aac49630-f3b4-4ef6-9a3a-5145481697ba from worker node kube-c9pqfcmw0tq431jdnrrg-mycluster-default-00000123.
```
{: screen}

## Using VNIs with OpenShift Virtualization
{: #vni-use-virtualization}

After you attach VNIs and configure localnet UDNs, you can use them with OpenShift Virtualization VMs.

1. Create VMs with OpenShift Virtualization and add the CUDN as a secondary network. Localnet attachments cannot be used as primary networks. You can use the OpenShift Console to add the attachment.

2. Specify the MAC address for the attachment to allow the VM operating system to get its IP address by using DHCP. Alternatively, you can assign the VNI IP address statically to the respective network interface in the VM.

For more information about creating and managing VMs, see the following Red Hat documentation:
- [Creating virtual machines from Red Hat images overview](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/virtualization/virtual-machines#virt-creating-vms-from-rh-images-overview){: external}
- [Creating virtual machines from the command line](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/virtualization/virtual-machines#virt-creating-vms-from-cli){: external}
- [Connecting to virtual machine consoles](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/virtualization/virtual-machines#virt-accessing-vm-consoles){: external}

## Troubleshooting VNIs
{: #vni-troubleshooting}

### Why can't I attach regular pods to localnet UDNs?
{: #vni-ts-pods}

Localnet UDNs have IP Address Management (IPAM) disabled on the OVN side, which means static IP address assignment to pods does not happen from OVN. This configuration is designed for VM workloads that use DHCP or set up static IPs inside the guest operating system. These options are not available for pod workloads.

### Why is live migration pending across worker pools?
{: #vni-ts-migration}

Different worker pools might have different worker flavors with CPUs from different generations and capabilities. If the full CPU feature set is transparently visible to the VM workload, you cannot live migrate the VM to another worker that does not support all the CPU features. You can limit the guest operating system visible CPU features at the beginning to gain more compatibility across worker flavors.

### Why are dynamic attached VNIs not working?
{: #vni-ts-not-working}

Check the following items:
- Verify that the VLAN ID in the CUDN matches the VLAN ID in the VNI attachment. VPC DHCP might still work without further traffic if the VLAN is mismatched.
- If floating is not enabled, make sure the workload is scheduled on the worker where the VNI is attached.
- Verify that the dedicated OVS bridge and the mapping are present on the workers. Check the NodeNetworkConfigurationPolicy resource status.
