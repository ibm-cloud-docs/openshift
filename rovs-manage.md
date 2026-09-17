---

copyright:
  years: 2026, 2026
lastupdated: "2026-09-17"

keywords: openshift, virtualization service, rovs, manage, add-ons, worker nodes, maintenance

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Managing Virtualization Service clusters
{: #rovs-manage}

[Virtual Private Cloud]{: tag-vpc}
[4.21 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

Learn how to manage your OpenShift Virtualization Service cluster, including working with pre-configured components, managing worker nodes, and performing maintenance tasks.
{: shortdesc}

## Understanding managed components
{: #rovs-manage-components}

Virtualization Service clusters include several pre-configured components that are managed differently than in standard OpenShift clusters.

### Core components (cannot be disabled)
{: #rovs-manage-core}

The following components are essential to Virtualization Service and cannot be disabled:

OpenShift Virtualization add-on
:   The `openshift-virtualization` add-on is automatically enabled on all Virtualization Service clusters and cannot be disabled. This add-on manages the installation and updates of the OpenShift Virtualization, NMState, and Node Maintenance operators. For more information, see [Managing the OpenShift Virtualization add-on](/docs/openshift?topic=openshift-rovs-addon-virtualization).

OpenShift Virtualization Operator
:   Provides virtual machine management capabilities. This operator is automatically installed by the add-on and updated as part of the cluster lifecycle. Installation from Red Hat OperatorHub is blocked.

NMState Operator
:   Manages network configuration for virtual machines and nodes. This operator is automatically installed by the add-on.

Node Maintenance Operator
:   Handles node maintenance operations for virtual machine workloads. This operator is automatically installed by the add-on.

OpenShift Data Foundation (ODF)
:   Provides storage for VM disks and enables live migration. ODF is pre-configured to use local NVME storage on bare metal nodes.

### Viewing managed add-ons
{: #rovs-manage-view-addons}

List all add-ons in your cluster:

```sh
ibmcloud ks cluster addon ls --cluster CLUSTER_NAME
```
{: pre}

Example output:
```sh
Name                         Version   Health State   Health Status
ibm-storage-operator         1.0       normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)
openshift-virtualization     4.21      normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)
```
{: screen}

The `openshift-virtualization` add-on is automatically enabled and cannot be disabled on Virtualization Service clusters.
{: important}

For detailed information about managing the OpenShift Virtualization add-on, including viewing details, checking versions, and updating, see [Managing the OpenShift Virtualization add-on](/docs/openshift?topic=openshift-rovs-addon-virtualization).

## Managing worker nodes
{: #rovs-manage-workers}

### Viewing worker nodes
{: #rovs-manage-view-workers}

List all worker nodes in your cluster:

```sh
ibmcloud ks workers --cluster CLUSTER_NAME
```
{: pre}

Or use the OpenShift CLI:

```sh
oc get nodes
```
{: pre}

### Adding worker nodes
{: #rovs-manage-add-workers}

Add worker nodes to an existing worker pool:

```sh
ibmcloud ks worker-pool resize --cluster CLUSTER_NAME \
  --worker-pool default \
  --size-per-zone NUMBER_OF_WORKERS
```
{: pre}

All worker nodes in a Virtualization Service cluster must use supported bare metal flavors.
{: important}

### Replacing worker nodes
{: #rovs-manage-replace-workers}

Replace a worker node:

```sh
ibmcloud ks worker replace --cluster CLUSTER_NAME --worker WORKER_ID
```
{: pre}

The replacement worker is provisioned with the same configuration as the original.

### Reloading worker nodes
{: #rovs-manage-reload-workers}

Before you reload a worker node, place the node into maintenance by using the Node Maintenance Operator or migrate running VMs to other nodes. For more information, see [Placing a node into maintenance](#rovs-manage-node-maintenance) and [Live migrating VMs](#rovs-manage-migrate-vms).
{: important}

Reload a worker node to apply updates or fix issues:

```sh
ibmcloud ks worker reload --cluster CLUSTER_NAME --worker WORKER_ID
```
{: pre}

## Managing worker pools
{: #rovs-manage-pools}

### Viewing worker pools
{: #rovs-manage-view-pools}

```sh
ibmcloud ks worker-pool ls --cluster CLUSTER_NAME
```
{: pre}

### Creating additional worker pools
{: #rovs-manage-create-pools}

Create a new worker pool with a different bare metal flavor:

```sh
ibmcloud ks worker-pool create vpc-gen2 \
  --name POOL_NAME \
  --cluster CLUSTER_NAME \
  --flavor BARE_METAL_FLAVOR \
  --size-per-zone NUMBER_OF_WORKERS
```
{: pre}

All worker pools in a Virtualization Service cluster must use bare metal flavors that support the `openshift-vs` offering.
{: note}

### Adding zones to worker pools
{: #rovs-manage-add-zones}

Add a zone to an existing worker pool:

```sh
ibmcloud ks zone add vpc-gen2 \
  --cluster CLUSTER_NAME \
  --zone ZONE \
  --subnet-id SUBNET_ID \
  --worker-pool POOL_NAME
```
{: pre}

## Updating the cluster
{: #rovs-manage-update}

### Checking for updates
{: #rovs-manage-check-updates}

Check if updates are available for your cluster:

```sh
ibmcloud ks cluster get --cluster CLUSTER_NAME | grep "Master Version"
```
{: pre}

View available versions:

```sh
ibmcloud ks versions --show-version openshift
```
{: pre}

### Updating the cluster master
{: #rovs-manage-update-master}

Update the cluster master to a new version:

```sh
ibmcloud ks cluster master update --cluster CLUSTER_NAME --version VERSION
```
{: pre}

The master update typically takes 30-60 minutes. During this time, you cannot access the Kubernetes API or OpenShift console.
{: note}

### Updating worker nodes
{: #rovs-manage-update-workers}

After updating the master, update worker nodes:

```sh
ibmcloud ks worker update --cluster CLUSTER_NAME --worker WORKER_ID
```
{: pre}

Or update all workers in a worker pool:

```sh
ibmcloud ks worker-pool update --cluster CLUSTER_NAME --worker-pool POOL_NAME
```
{: pre}

Before you update worker nodes, place each node into maintenance by using the Node Maintenance Operator or migrate running VMs to other nodes. For more information, see [Placing a node into maintenance](#rovs-manage-node-maintenance) and [Live migrating VMs](#rovs-manage-migrate-vms).
{: important}

## Monitoring cluster health
{: #rovs-manage-monitor}

### Checking cluster status
{: #rovs-manage-check-status}

```sh
ibmcloud ks cluster get --cluster CLUSTER_NAME
```
{: pre}

Look for:
- **State**: Should be `normal`
- **Master Status**: Should be `Ready`
- **Master Health**: Should be `normal`

### Monitoring component health
{: #rovs-manage-monitor-components}

Check OpenShift Virtualization health:

```sh
oc get hyperconverged -n openshift-cnv
```
{: pre}

Check ODF health:

```sh
oc get storagecluster -n openshift-storage
```
{: pre}

### Viewing cluster logs
{: #rovs-manage-logs}

View cluster activity:

```sh
ibmcloud ks cluster get --cluster CLUSTER_NAME --show-resources
```
{: pre}

For detailed logging, configure {{site.data.keyword.la_full_notm}}. See [Logging for clusters](/docs/openshift?topic=openshift-health).

## Managing virtual machines
{: #rovs-manage-vms}

### Viewing virtual machines
{: #rovs-manage-view-vms}

List all VMs in the cluster:

```sh
oc get vms -A
```
{: pre}

View VMs in a specific namespace:

```sh
oc get vms -n NAMESPACE
```
{: pre}

### Placing a node into maintenance
{: #rovs-manage-node-maintenance}

Before you perform maintenance actions such as updating, reloading, or replacing a bare metal worker node, put the node into maintenance mode. The Node Maintenance Operator cordons the node and automatically evicts or live-migrates all eligible virtual machine workloads to other nodes in the same zone without interrupting workloads.

If your cluster uses OpenShift Data Foundation (ODF), nodes that run ODF storage components must follow the ODF upgrade and maintenance procedures instead of this process. For more information, see [Understanding OpenShift Data Foundation](/docs/openshift?topic=openshift-ocs-storage-prep).
{: important}

#### Starting node maintenance from the web console
{: #rovs-node-maintenance-console}

You can initiate node maintenance directly from the Red Hat OpenShift web console.

1. In the OpenShift web console Administrator perspective, go to **Compute** > **Nodes**.
2. Find the bare metal worker node you want to perform maintenance on.
3. Click the actions menu (three vertical dots) for that node and select **Start maintenance**.
4. In the confirmation dialog, review the maintenance settings and click **Start**.
5. Verify that the node status displays as `Scheduling disabled` and that the actions menu shows **Stop maintenance** instead of **Start maintenance**. Wait until all VM instances migrate to other available nodes before proceeding with your node-level action (such as `ibmcloud ks worker reload` or `ibmcloud ks worker update`).
6. After your maintenance action completes and the node is healthy, return to **Compute** > **Nodes**, click the actions menu for the node, and select **Stop maintenance**.

#### Starting node maintenance from the CLI
{: #rovs-node-maintenance-cli}

You can also initiate node maintenance by creating a `NodeMaintenance` custom resource.

1. Create a YAML file named `node-maintenance.yaml` with the `NodeMaintenance` custom resource definition. Specify the target bare metal worker node name in the `nodeName` field.

   ```yaml
   apiVersion: nodemaintenance.medik8s.io/v1beta1
   kind: NodeMaintenance
   metadata:
     name: nodemaintenance-NODE_NAME
   spec:
     nodeName: NODE_NAME
     reason: Node maintenance for update or reload
   ```
   {: codeblock}

2. Apply the custom resource to put the node into maintenance mode:

   ```sh
   oc apply -f node-maintenance.yaml
   ```
   {: pre}

3. Monitor the status of the `NodeMaintenance` resource to verify that the drain operation succeeds:

   ```sh
   oc get nodemaintenance nodemaintenance-NODE_NAME -o jsonpath='{.status.phase}'
   ```
   {: pre}

   Verify that the phase reports `Succeeded` before you proceed to reload, update, or replace the node.

4. Perform your planned node-level action, such as reloading or updating the worker node:

   ```sh
   ibmcloud ks worker reload --cluster CLUSTER_NAME --worker WORKER_ID
   ```
   {: pre}

5. After the node reload or update is complete and the node status in `oc get nodes` is `Ready`, remove the node from maintenance by deleting the `NodeMaintenance` resource:

   ```sh
   oc delete nodemaintenance nodemaintenance-NODE_NAME
   ```
   {: pre}

### Live migrating VMs manually
{: #rovs-manage-migrate-vms}

If you want to manually trigger a live migration for an individual virtual machine instead of using the Node Maintenance Operator:

1. List the virtual machine instances in the namespace to identify the name of the VM you want to migrate:

   ```sh
   oc get vmi -n NAMESPACE
   ```
   {: pre}

2. Trigger a live migration for the VM:

   ```sh
   virtctl migrate VM_NAME -n NAMESPACE
   ```
   {: pre}

If a VM has a Virtual Network Interface (VNI) attached, live migration is supported only within the same zone. Migrating such a VM across zones succeeds, but the VM ends up with a broken network because VNIs cannot attach across zones.
{: note}

### Stopping and starting VMs
{: #rovs-manage-vm-lifecycle}

Stop a VM:

```sh
virtctl stop VM_NAME -n NAMESPACE
```
{: pre}

Start a VM:

```sh
virtctl start VM_NAME -n NAMESPACE
```
{: pre}

## Storage management
{: #rovs-manage-storage}

### Monitoring storage capacity
{: #rovs-manage-storage-capacity}

Check ODF storage capacity:

```sh
oc get cephcluster -n openshift-storage -o jsonpath='{.items[0].status.ceph.capacity}'
```
{: pre}

View storage usage:

```sh
oc get cephblockpool -n openshift-storage
```
{: pre}

### Managing persistent volume claims
{: #rovs-manage-pvcs}

List PVCs used by VMs:

```sh
oc get pvc -A | grep virtualmachine
```
{: pre}

View PVC details:

```sh
oc describe pvc PVC_NAME -n NAMESPACE
```
{: pre}

## Troubleshooting
{: #rovs-manage-troubleshoot}

For troubleshooting common issues with Virtualization Service clusters, see the following topics:

- [Troubleshooting clusters](/docs/openshift?topic=openshift-debug_clusters) - Worker node issues, cluster access, and general cluster problems
- [Troubleshooting OpenShift Virtualization](/docs/openshift?topic=openshift-ts-virt-operator-install-fails) - Virtual machine issues, operator problems, and virtualization-specific errors
- [Troubleshooting storage](/docs/openshift?topic=openshift-debug_storage) - OpenShift Data Foundation and persistent volume issues

## Next steps
{: #rovs-manage-next-steps}

- [Learn about OpenShift Virtualization limitations](/docs/openshift?topic=openshift-rovs-limitations)
- [Explore VM management in Red Hat documentation](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/virtualization/virtual-machines){: external}
- [Configure monitoring and alerts](/docs/openshift?topic=openshift-health-monitor)
- [Set up backup and disaster recovery](/docs/openshift?topic=openshift-storage_br)
