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

You can improve OpenShift Data Foundation (ODF) storage performance for virtualization workloads by selecting the appropriate performance profile, adjusting OSD pod resource limits, and configuring bulk data operations. These options apply to {{site.data.keyword.openshiftlong_notm}} clusters with manually deployed OpenShift Virtualization and Red Hat OpenShift Virtualization Service clusters.
{: shortdesc}

## Before you begin
{: #odf-virt-performance-prereqs}

- You must have `cluster-admin` access to the cluster.
- [Install](/docs/openshift?topic=openshift-cli-install) or update the {{site.data.keyword.cloud_notm}} CLI and the `oc` CLI.
- ODF must be installed and in a healthy state before you adjust resource limits or configure storage pools. To verify ODF health, see [Checking Ceph cluster health](#odf-virt-health).

## Selecting an ODF performance profile
{: #odf-virt-profile}

ODF provides two performance profiles that control CPU and memory allocation for storage components. Choose the profile that best fits your workload.

Performance
:   Allocates more CPU and memory than the **Balanced** profile. Use this profile for VM workloads that need high throughput and low latency, such as databases or high-traffic applications.

Balanced
:   Allocates moderate CPU and memory. Use this profile for general-purpose workloads, mixed environments, or cost-optimized deployments.

When you deploy ODF, select **Performance** in the **Resource profile** field under **Backing storage**. On Virtualization Service clusters, **Performance** is selected by default.

You can set the profile from the console or CLI.

- **Console - Standard {{site.data.keyword.openshiftlong_notm}} clusters**: When you install the ODF add-on, select **Performance** in the **Backing storage** section.
- **Console - Virtualization Service clusters**: **Performance** is selected by default. To change it, select **Edit** on the **OpenShift Data Foundation** card in the **Virtualization integrations** section during cluster creation.

This option applies only to standard {{site.data.keyword.openshiftlong_notm}} clusters. For Virtualization Service clusters, you set the profile during cluster creation.
{: note}

From the CLI, include `--param "resourceProfile=performance"` when you enable the add-on:

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

For all ODF add-on parameters, see [OpenShift Data Foundation parameter reference](/docs/openshift?topic=openshift-openshift_storage_parameters).

## Configuring OSD pod resource limits
{: #odf-virt-osd-resources}

Object Storage Daemon (OSD) pods store data and participate in data placement and replication. For virtualization workloads with high I/O, you can increase CPU and memory limits on OSD pods to help reduce bottlenecks.

### Check current OSD resource limits
{: #odf-virt-osd-check}

Before you modify resource limits, check the current CPU and memory settings for your OSD pods. Note the current requests and limits so that you can compare them with actual usage and the updated values later.

```sh
oc get pods -n openshift-storage -l app=rook-ceph-osd \
  -o jsonpath='{range .items[*]}{.metadata.name}{"\n"}{range .spec.containers[*]}  Container: {.name}{"\n"}    Requests - CPU: {.resources.requests.cpu}, Memory: {.resources.requests.memory}{"\n"}    Limits   - CPU: {.resources.limits.cpu}, Memory: {.resources.limits.memory}{"\n"}{end}{"\n"}{end}'
```
{: pre}

Review the output to identify the current CPU and memory requests and limits for each OSD container. Compare these values with actual usage in the next command. If CPU or memory usage consistently approaches the configured limits, increasing the limits might help reduce bottlenecks.

To check actual resource consumption, run the following command and compare CPU and memory usage with the limits you noted:

```sh
oc adm top pods -n openshift-storage -l app=rook-ceph-osd
```
{: pre}

### Increase OSD resource limits
{: #odf-virt-osd-modify}

If the current limits are insufficient for your VM workload, update them by editing the `ocs-storagecluster` resource.

You can also modify limits for other Rook-Ceph pods, such as `mon`, `mgr`, and `rgw`, in the `ocs-storagecluster` configuration. For details, see [Red Hat Solution 6959127](https://access.redhat.com/solutions/6959127){: external}.
{: note}

1. Open the storage cluster resource for editing.

   ```sh
   oc edit storagecluster ocs-storagecluster -n openshift-storage
   ```
   {: pre}

2. In the relevant `storageDeviceSets` entry, add or update the `resources` field. The following partial example sets a limit of 4 CPUs and 24 Gi of memory, and a request of 2 CPUs and 24 Gi of memory:

   ```yaml
   storageDeviceSets:
     - name: ocs-deviceset
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

   After you save the changes, the OSD pods restart automatically. Wait for the rolling restart to complete before you perform other storage operations.

### Verify the updated resource limits
{: #odf-virt-osd-verify}

After the rolling restart completes, confirm that the updated limits are applied to all OSD pods.

1. Monitor the rolling restart to verify that all OSD pods return to a `Running` state. The restart is complete when all OSD pods show `Running` and none are `Pending` or `Terminating`.

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

   Verify that the CPU and memory values match the values you configured.

## Configuring the bulk flag for large data operations
{: #odf-virt-bulk}

For large data operations, such as VM migrations, bulk imports, or data archival, enabling the bulk flag on a Ceph block pool can improve initial data distribution across OSDs and reduce rebalancing overhead.

The bulk flag is commonly used for:

- VM disk migrations and imports involving multiple TBs of data.
- Backup and restore operations.
- Initial data loads for new applications.
- Data archival pools.

To configure a `CephBlockPool` resource with the bulk flag enabled, complete the following steps.

1. Create or update the `CephBlockPool` resource definition so that the `parameters` section includes `bulk: "true"`.

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

2. Apply the configuration file.

   ```sh
   oc apply -f <pool-config-file>.yaml
   ```
   {: pre}

   After you apply the configuration, Ceph can distribute new data more evenly across the pool from the start. This behavior can reduce rebalancing as the pool fills.

## Checking Ceph cluster health
{: #odf-virt-health}

Regularly monitor your Ceph cluster to identify performance issues and ensure data integrity. Run health checks before and after you make configuration changes.

### Run a basic health check
{: #odf-virt-health-basic}

Run the following command to get an overall Ceph health summary. A healthy cluster returns `HEALTH_OK`.

```sh
oc rsh -n openshift-storage $(oc get pods -n openshift-storage -l app=rook-ceph-tools -o name) ceph status
```
{: pre}

To view active warnings or errors, run the following command:

```sh
oc rsh -n openshift-storage $(oc get pods -n openshift-storage -l app=rook-ceph-tools -o name) ceph health detail
```
{: pre}

### Understand cluster states
{: #odf-virt-health-states}

The output of `ceph status` includes placement group (PG) states that indicate data health.

Active/clean
:   The ideal state. All placement groups are active, all data is replicated, and no data is moving. No action is required.

Active+remapped, active+backfilling, active+recovering
:   Data is being redistributed. These states are normal after an OSD resource change, node replacement, or scaling operation. Wait for the cluster to return to `active/clean` before making additional changes.

Example healthy output:

```
HEALTH_OK
```
{: screen}

Example output during rebalancing:

```
HEALTH_WARN
  Degraded data redundancy: 123/456 objects degraded (26.974%)
  Recovery 50/456 objects degraded (10.965%)
```
{: screen}

### Check placement group and OSD status
{: #odf-virt-health-pg-osd}

For a more detailed view of data distribution and OSD health, complete the following checks.

1. Check placement group status to identify groups that are not in the `active+clean` state.

   ```sh
   oc rsh -n openshift-storage $(oc get pods -n openshift-storage -l app=rook-ceph-tools -o name) ceph pg stat
   ```
   {: pre}

2. Check individual OSD status to verify that the OSDs are `up` and `in`.

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
