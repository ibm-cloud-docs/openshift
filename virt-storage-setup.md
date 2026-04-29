---

copyright:
  years: 2025, 2026
lastupdated: "2026-04-29"

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

## Option 1: Setting up OpenShift Data Foundation
{: #virt-storage-odf}

OpenShift Data Foundation (ODF) is recommended for production workloads that require high performance, snapshots, and cloning capabilities.

### Prerequisites for ODF
{: #virt-storage-odf-prereqs}

Bare metal worker nodes with local NVME storage
:   Use flavors with the `d` suffix that include local NVME disks.

Worker node requirements
:   ODF requires at least 3 worker nodes for high availability and data redundancy.

Zone configuration
:   - **General ODF deployments**: At least 3 zones are recommended for high availability and disaster recovery.
    - **OpenShift Virtualization deployments**: Single-zone clusters are typically preferred to minimize storage latency for VM workloads. While multi-zone deployments provide better high availability, cross-zone storage replication can impact VM performance.

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

## Option 2: Setting up VPC File Storage
{: #virt-storage-vpc-file}

{{site.data.keyword.filestorage_vpc_short}} is a cost-effective option for non-production workloads or environments with lower I/O requirements.

### Prerequisites for VPC File Storage
{: #virt-storage-vpc-file-prereqs}

- Any supported bare metal flavor
- VPC infrastructure

### Step 1: Disable VPC Block Storage as default
{: #virt-storage-vpc-file-disable-block}

1. Edit the VPC Block CSI driver configmap.
   ```sh
   oc edit cm addon-vpc-block-csi-driver-configmap -n kube-system
   ```
   {: pre}

2. Set `IsStorageClassDefault` to `false`.
   ```yaml
   data:
     IsStorageClassDefault: "false"
   ```
   {: codeblock}

3. Save and exit the editor.

### Step 2: Install the VPC File CSI driver
{: #virt-storage-vpc-file-install}

#### From the console
{: #virt-storage-vpc-file-install-console}

1. In your cluster dashboard, click **Add-ons**.

2. Locate the **File Storage for VPC** add-on.

3. Click **Install**.

4. Wait for the add-on to reach a **Normal** state.

#### From the CLI
{: #virt-storage-vpc-file-install-cli}

1. Enable the VPC File CSI driver add-on.
   ```sh
   ibmcloud ks cluster addon enable vpc-file-csi-driver -c <cluster-name>
   ```
   {: pre}

2. Verify the add-on is enabled.
   ```sh
   ibmcloud ks cluster addon ls -c <cluster-name>
   ```
   {: pre}

### Step 3: Set a default storage class
{: #virt-storage-vpc-file-default}

1. List available storage classes.
   ```sh
   oc get storageclass | grep vpc-file
   ```
   {: pre}

2. Choose an appropriate storage class based on your workload:
   - `ibmc-vpc-file-1000-iops`: For moderate workloads (40 GB - 2000 IOPS)
   - `ibmc-vpc-file-6000-iops`: For higher workloads (100 GB - 6000 IOPS)
   - `ibmc-vpc-file-metro-1000-iops`: For multi-zone deployments

3. Edit the VPC File CSI driver configmap.
   ```sh
   oc edit cm addon-vpc-file-csi-driver-configmap -n kube-system
   ```
   {: pre}

4. Set the `SET_DEFAULT_STORAGE_CLASS` field to your chosen storage class.
   ```yaml
   data:
     SET_DEFAULT_STORAGE_CLASS: "ibmc-vpc-file-metro-1000-iops"
   ```
   {: codeblock}

5. Save and exit the editor.

6. Wait a few minutes for the changes to take effect.

7. Verify the default storage class.
   ```sh
   oc get storageclass | grep "(default)"
   ```
   {: pre}

### Step 4: Configure storage profiles for VPC File Storage
{: #virt-storage-vpc-file-profiles}

After installing the OpenShift Virtualization Operator, you must configure storage profiles for VPC File Storage because the Container Disk Importer (CDI) does not automatically recognize VPC File Storage properties.

This step must be completed after installing the OpenShift Virtualization Operator.
{: important}

#### Option 1: Patch all VPC File storage profiles (recommended)
{: #virt-storage-vpc-file-patch-all}

Use this utility command to patch all storage profiles for the VPC File CSI provisioner:

```sh
for sp in $(oc get storageprofile.cdi.kubevirt.io -o json | jq -r '.items[] | select(.status.provisioner == "vpc.file.csi.ibm.io") | .metadata.name'); do
  oc patch storageprofile.cdi.kubevirt.io "$sp" --type=merge -p '{
    "spec": {
      "claimPropertySets": [
        {
          "accessModes": ["ReadWriteMany"],
          "volumeMode": "Filesystem"
        }
      ]
    }
  }'
done
```
{: pre}

#### Option 2: Manually edit a specific storage profile
{: #virt-storage-vpc-file-patch-manual}

1. List available storage profiles.
   ```sh
   oc get storageprofile
   ```
   {: pre}

2. Edit the storage profile for your default storage class.
   ```sh
   oc edit storageprofile <storage-profile-name>
   ```
   {: pre}

3. Add the following configuration under `spec`:
   ```yaml
   spec:
     claimPropertySets:
     - accessModes:
       - ReadWriteMany
       volumeMode: Filesystem
   ```
   {: codeblock}

4. Save and exit the editor.

5. Verify the storage profile is updated.
   ```sh
   oc get storageprofile <storage-profile-name> -o yaml
   ```
   {: pre}

For more information about storage profiles, see [Customizing the storage profile](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/virtualization/storage#virt-customizing-storage-profile_virt-configuring-storage-profile){: external}.

### Verifying VPC File Storage installation
{: #virt-storage-vpc-file-verify}

1. Verify the VPC File CSI driver pods are running.
   ```sh
   oc get pods -n kube-system | grep vpc-file
   ```
   {: pre}

2. Confirm the default storage class is set correctly.
   ```sh
   oc get storageclass | grep "(default)"
   ```
   {: pre}

3. Test storage provisioning by creating a test PVC.
   ```yaml
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: test-pvc
   spec:
     accessModes:
     - ReadWriteMany
     resources:
       requests:
         storage: 10Gi
   ```
   {: codeblock}

4. Verify the PVC is bound.
   ```sh
   oc get pvc test-pvc
   ```
   {: pre}

5. Delete the test PVC.
   ```sh
   oc delete pvc test-pvc
   ```
   {: pre}

## Storage comparison
{: #virt-storage-comparison}

| Feature | OpenShift Data Foundation | VPC File Storage |
|---------|---------------------------|------------------|
| Performance | High (local disks) | Moderate (network storage) |
| Snapshots | Supported | Not supported |
| Cloning | Supported | Not supported |
| Live migration | Supported | Supported |
| Multi-zone HA | Supported (3+ zones) | Supported (lower throughput) |
| Cost | Higher | Lower |
| Best for | Production workloads | Non-production workloads |
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

### VPC File Storage PVCs remain pending
{: #virt-storage-ts-vpc-pending}

If PVCs remain in a pending state:

- Verify the VPC File CSI driver add-on is installed and healthy
- Check that the default storage class is set correctly
- Ensure storage profiles are configured with RWX access mode
- Review CSI driver logs: `oc logs -n kube-system -l app=ibm-vpc-file-csi-controller`

### Storage profiles not updated
{: #virt-storage-ts-profiles}

If storage profiles are not showing the correct configuration:

- Ensure the OpenShift Virtualization Operator is installed
- Wait for storage profiles to be created automatically
- Manually patch storage profiles using the commands provided
- Verify the provisioner name matches `vpc.file.csi.ibm.io`

## Next steps
{: #virt-storage-next-steps}

After setting up storage:

1. [Install the OpenShift Virtualization Operator](/docs/openshift?topic=openshift-virt-overview)
2. [Create and manage virtual machines](/docs/openshift?topic=openshift-virt-overview)
3. [Configure virtual network interfaces (optional)](/docs/openshift?topic=openshift-vni-virtualization)
