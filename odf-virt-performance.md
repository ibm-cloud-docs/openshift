---

copyright:
  years: 2026

lastupdated: "2026-07-09"

keywords: openshift, odf, openshift data foundation, virtualization, performance, osd, ceph, bulk flag, resource limits

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Tuning ODF performance for virtualization workloads
{: #odf-virt-performance}

[Virtual Private Cloud]{: tag-vpc}
[4.20 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}

You can improve OpenShift Data Foundation (ODF) storage performance for virtualization workloads by selecting the appropriate performance profile, adjusting OSD pod resource limits, and configuring bulk data operations. These configurations apply to both {{site.data.keyword.openshiftlong_notm}} clusters with manually deployed OpenShift Virtualization and Red Hat OpenShift Virtualization Service clusters.
{: shortdesc}

## Before you begin
{: #odf-virt-performance-prereqs}

- You must have `cluster-admin` access to the cluster.
- [Install](/docs/openshift?topic=openshift-cli-install) or update the {{site.data.keyword.cloud_notm}} CLI and the `oc` CLI.
- ODF must be installed and in a healthy state before you adjust resource limits or configure storage pools. To verify ODF health, see [Checking Ceph cluster health](#odf-virt-health).

## Selecting an ODF performance profile
{: #odf-virt-profile}

ODF provides two performance profiles that control how CPU and memory resources are allocated to storage components. Choose the profile that best fits your workload requirements.

Performance
:   Allocates the maximum available CPU and memory to ODF storage components. Use this profile for VM workloads that require high throughput and low latency, such as database servers or high-traffic applications.

Balanced
:   Allocates moderate CPU and memory resources. Use this profile for general-purpose workloads, mixed environments, or cost-optimized deployments.

When you deploy ODF, select the **Performance** profile in the **Resource profile** field under **Backing storage**. On Virtualization Service clusters, **Performance** is selected by default.

### From the console
{: #odf-virt-profile-console}

- **Standard {{site.data.keyword.openshiftlong_notm}} clusters**: When you install the ODF add-on, select **Performance** as the resource profile in the **Backing storage** section of the install panel.
- **Virtualization Service clusters**: **Performance** is selected by default. To change it, click **Edit** on the **OpenShift Data Foundation** card in the **Virtualization integrations** section when creating your cluster.

### From the CLI
{: #odf-virt-profile-cli}

This option applies to standard {{site.data.keyword.openshiftlong_notm}} clusters only. For Virtualization Service clusters, the profile is set during cluster creation
{: note}

Include the `--param "resourceProfile=performance"` option when you enable the add-on. For example:

```sh
ibmcloud oc cluster addon enable openshift-data-foundation \
  -c <cluster-name> \
  --version <addon-version> \
  --param "odfDeploy=true" \
  --param "osdStorageClassName=localblock" \
  --param "autoDiscoverDevices=true" \
  --param "resourceProfile=performance" \
  --param "setDefaultStorageClassForVirtualization=true"
```
{: pre}

For a full list of ODF add-on parameters, see [OpenShift Data Foundation parameter reference](/docs/openshift?topic=openshift-openshift_storage_parameters).

## Configuring OSD pod resource limits
{: #odf-virt-osd-resources}

Object Storage Daemon (OSD) pods are responsible for data placement and replication. For high I/O virtualization workloads, you can increase the CPU and memory limits on OSD pods to prevent resource bottlenecks.

### Check current OSD resource limits
{: #odf-virt-osd-check}

Before modifying resource limits, check the current CPU and memory settings assigned to your OSD pods.

```sh
oc get pods -n openshift-storage -l app=rook-ceph-osd \
  -o jsonpath='{range .items[*]}{.metadata.name}{"\n"}{range .spec.containers[*]}  Container: {.name}{"\n"}    Requests - CPU: {.resources.requests.cpu}, Memory: {.resources.requests.memory}{"\n"}    Limits   - CPU: {.resources.limits.cpu}, Memory: {.resources.limits.memory}{"\n"}{end}{"\n"}{end}'
```
{: pre}

Review the output to identify the current CPU and memory requests and limits for each OSD container. If the actual usage approaches or exceeds these values, increasing the limits can improve performance.

To check actual resource consumption, run the following command and compare the output to the limits you noted:

```sh
oc adm top pods -n openshift-storage -l app=rook-ceph-osd
```
{: pre}

### Increase OSD resource limits
{: #odf-virt-osd-modify}

If the current limits are insufficient for your VM workload, update them by editing the `ocs-storagecluster` resource.

Resource limits for other Rook-Ceph pods, such as `mon`, `mgr`, and `rgw`, can also be modified in the `ocs-storagecluster` configuration. For details, see [Red Hat Solution 6959127](https://access.redhat.com/solutions/6959127){: external}.
{: note}

1. Open the storage cluster resource for editing.

   ```sh
   oc edit storagecluster ocs-storagecluster -n openshift-storage
   ```
   {: pre}

2. Locate the `storageDeviceSets` section and add or update the `resources` field with values appropriate for your workload. The following example sets 4 CPUs and 24 Gi of memory:

   ```yaml
   storageDeviceSets:
     resources:
       limits:
         cpu: "4"
         memory: "24Gi"
       requests:
         cpu: "2"
         memory: "24Gi"
   ```
   {: codeblock}

   CPU and memory requests must be less than or equal to the limits.
   {: important}

3. Save and exit the editor.

   After you save the changes, all OSD pods restart automatically to apply the new resource configuration. Wait for the rolling restart to complete before performing any other storage operations.

### Verify the updated resource limits
{: #odf-virt-osd-verify}

After the rolling restart completes, confirm that the updated limits are applied to all OSD pods.

1. Monitor the rolling restart to verify all OSD pods return to a `Running` state. The restart is complete when all OSD pods show `Running` and none are in a `Pending` or `Terminating` state.

   ```sh
   oc get pods -n openshift-storage | grep osd | grep -v prepare | grep -v rotation
   ```
   {: pre}

2. Confirm the new resource values are in effect.

   ```sh
   oc get pods -n openshift-storage -l app=rook-ceph-osd \
     -o jsonpath='{range .items[*]}{.metadata.name}{"\n"}{range .spec.containers[*]}  Container: {.name}{"\n"}    Requests - CPU: {.resources.requests.cpu}, Memory: {.resources.requests.memory}{"\n"}    Limits   - CPU: {.resources.limits.cpu}, Memory: {.resources.limits.memory}{"\n"}{end}{"\n"}{end}'
   ```
   {: pre}

   Verify that the CPU and memory values in the output match the values you configured.

## Configuring the bulk flag for large data operations
{: #odf-virt-bulk}

When you perform large data operations — such as VM migrations, bulk imports, or data archival — enabling the bulk flag on a Ceph block pool improves initial data distribution across OSDs. This reduces rebalancing overhead and minimizes performance impact during large data transfers.

The bulk flag is recommended for:
- VM disk migrations and imports involving multiple TBs of data
- Backup and restore operations
- Initial data loads for new applications
- Data archival pools

To configure a `CephBlockPool` resource with the bulk flag enabled, create or update the resource with the following configuration:

```yaml
apiVersion: ceph.rook.io/v1
kind: CephBlockPool
metadata:
  name: <pool-name>
  namespace: openshift-storage
spec:
  replicated:
    size: 3
  parameters:
    bulk: "true"
```
{: codeblock}

Apply the configuration:

```sh
oc apply -f <pool-config-file>.yaml
```
{: pre}

After applying the configuration, Ceph distributes new data across the pool more evenly from the start, which reduces the cluster rebalancing that typically occurs as a pool fills up.

## Checking Ceph cluster health
{: #odf-virt-health}

Regularly monitoring your Ceph cluster helps you identify performance issues and ensure data integrity. Run health checks before and after making configuration changes.

### Run a basic health check
{: #odf-virt-health-basic}

Run the following command to get an overall health summary of the Ceph cluster. A healthy cluster returns `HEALTH_OK`.

```sh
oc rsh -n openshift-storage $(oc get pods -n openshift-storage -l app=rook-ceph-tools -o name) ceph status
```
{: pre}

For detailed information about any active warnings or errors, run:

```sh
oc rsh -n openshift-storage $(oc get pods -n openshift-storage -l app=rook-ceph-tools -o name) ceph health detail
```
{: pre}

### Understand cluster states
{: #odf-virt-health-states}

The output of `ceph status` includes placement group (PG) states that indicate the current health of your data.

Active/clean
:   The ideal state. All placement groups are active, all data is replicated, and no data is being moved. No action is required.

Active+remapped, active+backfilling, active+recovering
:   Data is being redistributed. These states are normal after an OSD resource change, a node replacement, or a scaling operation. Wait for the cluster to return to `active/clean` before making additional changes.

The following example shows healthy output:

```
HEALTH_OK
```
{: screen}

The following example shows output during a rebalancing operation:

```
HEALTH_WARN
  Degraded data redundancy: 123/456 objects degraded (26.974%)
  Recovery 50/456 objects degraded (10.965%)
```
{: screen}

### Check placement group and OSD status
{: #odf-virt-health-pg-osd}

For a more detailed view of data distribution and individual OSD health, run the following commands.

To check placement group status:

```sh
oc rsh -n openshift-storage $(oc get pods -n openshift-storage -l app=rook-ceph-tools -o name) ceph pg stat
```
{: pre}

To check individual OSD status:

```sh
oc rsh -n openshift-storage $(oc get pods -n openshift-storage -l app=rook-ceph-tools -o name) ceph osd status
```
{: pre}

## Next steps
{: #odf-virt-next-steps}

- [Deploying OpenShift Data Foundation on VPC clusters](/docs/openshift?topic=openshift-deploy-odf-vpc)
- [OpenShift Data Foundation parameter reference](/docs/openshift?topic=openshift-openshift_storage_parameters)
- [Managing OpenShift Data Foundation](/docs/openshift?topic=openshift-ocs-manage-deployment)
- [Red Hat OpenShift Data Foundation documentation](https://access.redhat.com/documentation/en-us/red_hat_openshift_data_foundation){: external}
