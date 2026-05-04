---

copyright:
  years: 2025, 2026
lastupdated: "2026-05-04"

keywords: openshift, virtualization, storage, odf, vpc file, openshift data foundation

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Setting up storage for OpenShift Virtualization
{: #virt-storage-setup}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

OpenShift Virtualization requires storage that supports ReadWriteMany (RWX) access mode for VM disks, live migration, and snapshots. You can use OpenShift Data Foundation (ODF) or {{site.data.keyword.filestorage_vpc_short}} as your storage solution.
{: shortdesc}

## Before you begin
{: #virt-storage-prereqs}

- Create a {{site.data.keyword.openshiftlong_notm}} cluster with bare metal worker nodes. For more information, see [Creating VPC clusters](/docs/openshift?topic=openshift-cluster-create-vpc-gen2).
- Ensure your cluster meets the [prerequisites for OpenShift Virtualization](/docs/openshift?topic=openshift-virt-plan#virt-prereqs).
- Decide which storage solution to use based on your workload requirements. For guidance, see [Planning your storage solution](/docs/openshift?topic=openshift-virt-plan#virt-plan-storage).

Your cluster must have exactly one properly configured storage solution before installing OpenShift Virtualization.
{: important}

## Setting up OpenShift Data Foundation
{: #virt-storage-odf}

OpenShift Data Foundation (ODF) is recommended for production workloads that require high performance, snapshots, and cloning capabilities.

### Prerequisites for ODF
{: #virt-storage-odf-prereqs}

Bare metal worker nodes with local NVME storage
:   Use flavors with the `d` suffix that include local NVME disks.

Worker node requirements
:   ODF requires at least 3 worker nodes for high availability and data redundancy.

Zone configuration
:   - **OpenShift Virtualization deployments**: Single-zone clusters are recommended to minimize storage latency for VM workloads. While multi-zone deployments provide better high availability, cross-zone storage replication can impact VM performance.
    - **General ODF deployments**: At least 3 zones are recommended for high availability and disaster recovery.

### Installing ODF from the console
{: #virt-storage-odf-ui}

1. Log in to your {{site.data.keyword.cloud_notm}} account and navigate to your cluster.

2. Click **Add-ons** in the cluster navigation.

3. On the **OpenShift Data Foundation** card, click **Install**.

4. Select the **Local Storage** option.
   
   Remote block volume attachment is not supported for VPC bare metal nodes.
   {: note}

5. Choose one of the following discovery methods:

   **Automatic discovery (recommended)**
   :   Select **Automatic discovery** to automatically detect and use available disks on your bare metal worker nodes.

   **Manual disk specification**
   :   If you prefer to specify disks manually, follow these steps:

   1. Log in to each worker node to identify available disks.
      ```sh
      oc debug node/<node-name>
      ```
      {: pre}

   2. Allow host binaries.
      ```sh
      chroot /host
      ```
      {: pre}

   3. List available devices.
      ```sh
      lsblk
      ```
      {: pre}

   4. Find the by-id for each disk.
      ```sh
      ls -l /dev/disk/by-id/
      ```
      {: pre}

   5. Add the disk IDs in the **OSD pod disk IDs** parameter.

6. Configure additional parameters as needed:
   - **Resource profile**: Choose `balanced` or `performance` based on your workload
   - **Encryption**: Enable encryption with {{site.data.keyword.hscrypto}} if required
   - **Number of OSD disks**: Specify the number of disks per worker node

7. Click **Install** to deploy ODF.

For more information about ODF parameters, see [OpenShift Data Foundation parameter reference](/docs/openshift?topic=openshift-openshift_storage_parameters).

### Installing ODF from the CLI
{: #virt-storage-odf-cli}

1. Review the available add-on options.
   ```sh
   ibmcloud oc cluster addon options --addon openshift-data-foundation --version 4.20.0
   ```
   {: pre}

2. Enable the OpenShift Data Foundation add-on with automatic disk discovery and virtualization support.
   ```sh
   ibmcloud oc cluster addon enable openshift-data-foundation \
     -c <cluster-name> \
     --version 4.20.0 \
     --param "odfDeploy=true" \
     --param "osdStorageClassName=localblock" \
     --param "autoDiscoverDevices=true" \
     --param "resourceProfile=performance" \
     --param "setDefaultStorageClassForVirtualization=true"
   ```
   {: pre}

3. Verify the add-on is in a Ready state.
   ```sh
   oc get storagecluster -n openshift-storage
   ```
   {: pre}

   Example output:
   ```sh
   NAME                 AGE   PHASE   EXTERNAL   CREATED AT             VERSION
   ocs-storagecluster   53m   Ready              2025-03-10T12:20:52Z   4.20.0
   ```
   {: screen}

### Verifying ODF installation
{: #virt-storage-odf-verify}

1. Check the storage cluster status.
   ```sh
   oc get storagecluster -n openshift-storage
   ```
   {: pre}

2. Verify that storage classes are available.
   ```sh
   oc get storageclass | grep ocs
   ```
   {: pre}

3. Confirm that ODF pods are running.
   ```sh
   oc get pods -n openshift-storage
   ```
   {: pre}

For more information about deploying ODF, see [Deploying OpenShift Data Foundation on VPC clusters](/docs/openshift?topic=openshift-deploy-odf-vpc).



## Storage comparison
{: #virt-storage-comparison}

| Feature | OpenShift Data Foundation |
|---------|---------------------------|
| Performance | High (local disks) |
| Snapshots | Supported |
| Cloning | Supported |
| Live migration | Supported |
| Multi-zone HA | Supported (3+ zones) |
| Cost | Higher |
| Best for | Production workloads |
{: caption="Storage solution comparison"}

## Troubleshooting storage setup
{: #virt-storage-troubleshoot}

### ODF installation fails
{: #virt-storage-ts-odf-fail}

If ODF installation fails, check the following:

- Verify that your bare metal nodes have local NVME storage
- Ensure you have at least 3 worker nodes
- Check that disks are unmounted and unformatted
- Review ODF operator logs: `oc logs -n openshift-storage -l app=ocs-operator`



## Next steps
{: #virt-storage-next-steps}

After setting up storage:

1. [Install the OpenShift Virtualization Operator](/docs/openshift?topic=openshift-oc-virtualization)
2. [Create and manage virtual machines](/docs/openshift?topic=openshift-virt-manage-vms)
3. [Configure virtual network interfaces (optional)](/docs/openshift?topic=openshift-vni-virtualization)
