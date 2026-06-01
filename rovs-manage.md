---

copyright:
  years: 2026, 2026
lastupdated: "2026-06-01"

keywords: openshift, virtualization service, rovs, manage, add-ons, worker nodes, maintenance

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Managing Virtualization Service clusters
{: #rovs-manage}

[Virtual Private Cloud]{: tag-vpc}
[4.20 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

Learn how to manage your OpenShift Virtualization Service cluster, including working with pre-configured components, managing worker nodes, and performing maintenance tasks.
{: shortdesc}

This service is currently available as a beta release. Access is controlled by an allowlist. During the beta period, only console-based cluster creation is supported.
{: beta}

## Understanding managed components
{: #rovs-manage-components}

Virtualization Service clusters include several pre-configured components that are managed differently than in standard OpenShift clusters.

### Core components (cannot be disabled)
{: #rovs-manage-core}

The following components are essential to Virtualization Service and cannot be disabled:

OpenShift Virtualization add-on
:   The `openshift-virtualization` add-on is automatically enabled on all ROVS clusters and cannot be disabled. This add-on manages the installation and updates of the OpenShift Virtualization, NMState, and Node Maintenance operators. For more information, see [Managing the OpenShift Virtualization add-on](/docs/openshift?topic=openshift-rovs-addon-virtualization).

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
ibmcloud ks cluster addon ls --cluster <cluster-name>
```
{: pre}

Example output:
```sh
Name                         Version   Health State   Health Status
ibm-storage-operator         1.0       normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)
openshift-virtualization     4.20      normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)
```
{: screen}

The `openshift-virtualization` add-on is automatically enabled and cannot be disabled on ROVS clusters.
{: important}

For detailed information about managing the OpenShift Virtualization add-on, including viewing details, checking versions, and updating, see [Managing the OpenShift Virtualization add-on](/docs/openshift?topic=openshift-rovs-addon-virtualization).

## Managing worker nodes
{: #rovs-manage-workers}

### Viewing worker nodes
{: #rovs-manage-view-workers}

List all worker nodes in your cluster:

```sh
ibmcloud ks workers --cluster <cluster-name>
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
ibmcloud ks worker-pool resize --cluster <cluster-name> \
  --worker-pool default \
  --size-per-zone <number-of-workers>
```
{: pre}

All worker nodes in a Virtualization Service cluster must use supported bare metal flavors.
{: important}

### Replacing worker nodes
{: #rovs-manage-replace-workers}

Replace a worker node:

```sh
ibmcloud ks worker replace --cluster <cluster-name> --worker <worker-id>
```
{: pre}

The replacement worker is provisioned with the same configuration as the original.

### Reloading worker nodes
{: #rovs-manage-reload-workers}

Reload a worker node to apply updates or fix issues:

```sh
ibmcloud ks worker reload --cluster <cluster-name> --worker <worker-id>
```
{: pre}

Before reloading a worker node, ensure that any running VMs are migrated to other nodes or can tolerate downtime.
{: important}

## Managing worker pools
{: #rovs-manage-pools}

### Viewing worker pools
{: #rovs-manage-view-pools}

```sh
ibmcloud ks worker-pool ls --cluster <cluster-name>
```
{: pre}

### Creating additional worker pools
{: #rovs-manage-create-pools}

Create a new worker pool with a different bare metal flavor:

```sh
ibmcloud ks worker-pool create vpc-gen2 \
  --name <pool-name> \
  --cluster <cluster-name> \
  --flavor <bare-metal-flavor> \
  --size-per-zone <number-of-workers>
```
{: pre}

All worker pools in a Virtualization Service cluster must use bare metal flavors that support the `openshift-vs` offering.
{: note}

### Adding zones to worker pools
{: #rovs-manage-add-zones}

Add a zone to an existing worker pool:

```sh
ibmcloud ks zone add vpc-gen2 \
  --cluster <cluster-name> \
  --zone <zone> \
  --subnet-id <subnet-id> \
  --worker-pool <pool-name>
```
{: pre}

## Updating the cluster
{: #rovs-manage-update}

### Checking for updates
{: #rovs-manage-check-updates}

Check if updates are available for your cluster:

```sh
ibmcloud ks cluster get --cluster <cluster-name> | grep "Master Version"
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
ibmcloud ks cluster master update --cluster <cluster-name> --version <version>
```
{: pre}

The master update typically takes 30-60 minutes. During this time, you cannot access the Kubernetes API or OpenShift console.
{: note}

### Updating worker nodes
{: #rovs-manage-update-workers}

After updating the master, update worker nodes:

```sh
ibmcloud ks worker update --cluster <cluster-name> --worker <worker-id>
```
{: pre}

Or update all workers in a worker pool:

```sh
ibmcloud ks worker-pool update --cluster <cluster-name> --worker-pool <pool-name>
```
{: pre}

Before updating worker nodes, migrate VMs to other nodes or ensure they can tolerate downtime.
{: important}

## Monitoring cluster health
{: #rovs-manage-monitor}

### Checking cluster status
{: #rovs-manage-check-status}

```sh
ibmcloud ks cluster get --cluster <cluster-name>
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
ibmcloud ks cluster get --cluster <cluster-name> --show-resources
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
oc get vms -n <namespace>
```
{: pre}

### Live migrating VMs
{: #rovs-manage-migrate-vms}

Before performing maintenance on a worker node, migrate VMs to other nodes:

```sh
oc get vmi -n <namespace>
```
{: pre}

Trigger a live migration:

```sh
virtctl migrate <vm-name> -n <namespace>
```
{: pre}

Live migration is supported only within the same zone.
{: note}

### Stopping and starting VMs
{: #rovs-manage-vm-lifecycle}

Stop a VM:

```sh
virtctl stop <vm-name> -n <namespace>
```
{: pre}

Start a VM:

```sh
virtctl start <vm-name> -n <namespace>
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
oc describe pvc <pvc-name> -n <namespace>
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
- [Explore VM management in Red Hat documentation](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/virtualization/virtual-machines){: external}
- [Configure monitoring and alerts](/docs/openshift?topic=openshift-health-monitor)
- [Set up backup and disaster recovery](/docs/openshift?topic=openshift-storage-br)
