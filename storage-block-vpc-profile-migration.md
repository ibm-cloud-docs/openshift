---

copyright:
  years: 2026
lastupdated: "2026-06-16"

keywords: openshift, block storage, vpc, gen-1, gen-2, sdp, migration, profile, iops

subcollection: openshift

content-type: tutorial
services: containers, vpc
account-plan: paid
completion-time: 30m

---

{{site.data.keyword.attribute-definition-list}}

# Migrating {{site.data.keyword.block_storage_is_short}} volumes from Gen-1 to Gen-2 profiles
{: #storage-block-vpc-profile-migration}
{: toc-content-type="tutorial"}
{: toc-services="containers, vpc"}
{: toc-completion-time="30m"}

[Virtual Private Cloud]{: tag-vpc}

Migrate your {{site.data.keyword.block_storage_is_short}} volumes from Generation 1 (tier-based) profiles to Generation 2 (Software Defined Performance) profiles to take advantage of improved performance, dynamic IOPS adjustment, and better cost optimization.
{: shortdesc}

## Understanding the profile generations
{: #vpc-block-profile-generations}

{{site.data.keyword.block_storage_is_short}} has evolved from Generation 1 (tier-based) to Generation 2 (Software Defined Performance) profiles.

Generation 1 (tier-based)
:   IOPS are calculated based on volume size. For more information, see [Block Storage profiles](/docs/vpc?topic=vpc-block-storage-profiles&interface=ui#tiers){: external}.

Generation 2 (SDP)
:   Custom IOPS independent of volume size. For more information, see [SDP Block Storage profile](/docs/vpc?topic=vpc-block-storage-profiles&interface=ui#sdp){: external}.

For the latest details on block storage profiles and their capabilities, see [Block Storage profiles](/docs/vpc?topic=vpc-block-storage-profiles&interface=ui){: external}.

## Before you begin
{: #vpc-block-profile-migration-prereqs}

Before you migrate your volumes, complete the following steps.

- Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started){: external}.
- Ensure you have `kubectl` or `oc` access to your cluster.
- Verify that the VPC Block CSI Driver add-on is version 5.0 or later. To check the version, run the following {{site.data.keyword.mfp_cli_long_notm}}
	```sh
	oc get deployment -n kube-system vpc-block-csi-controller -o jsonpath='{.spec.template.spec.containers[0].image}'
	```
	{: pre}

- Ensure that the VPC Block CSI Driver add-on is installed. For more information, see [Installing the VPC Block CSI Driver add-on](/docs/openshift?topic=openshift-vpc-block-csi-driver-add-on).
- Ensure that the VPC Block CSI Driver add-on is configured. For more information, see [Configuring the VPC Block CSI Driver add-on](/docs/openshift?topic=openshift-vpc-block-csi-driver-add-on).
- Ensure that the VPC Block CSI Driver add-on is running. For more information, see [Verifying the VPC Block CSI Driver add-on](/docs/openshift?topic=openshift-vpc-block-csi-driver-add-on).
- Ensure that the VPC Block CSI Driver add-on is up-to-date. For more information, see [Upgrading the VPC Block CSI Driver add-on](/docs/openshift?topic=openshift-vpc-block-csi-driver-add-on).
- Document your current performance requirements.
- Create a backup or snapshot of your data. For more information, see [Setting up snapshots with the {{site.data.keyword.block_storage_is_short}} cluster add-on](/docs/openshift?topic=openshift-vpc-volume-snapshot).

## Identify volumes for migration
{: #vpc-block-profile-identify}
{: step}

Find PVCs that use Gen-1 block storage profiles.

1. List all block storage PVCs in your cluster.

    ```sh
    oc get pvc --all-namespaces -o custom-columns=NAMESPACE:.metadata.namespace,NAME:.metadata.name,STORAGECLASS:.spec.storageClassName,STATUS:.status.phase | grep vpc-block
    ```
    {: pre}

1. Get the VPC volume ID from a PVC.

    ```sh
    PV_NAME=$(oc get pvc <pvc-name> -n <namespace> -o jsonpath='{.spec.volumeName}')
    VOLUME_ID=$(oc get pv $PV_NAME -o jsonpath='{.spec.csi.volumeHandle}')
    echo "Volume ID: $VOLUME_ID"
    ```
    {: pre}

    Example output

    ```sh
    Volume ID: r026-3afe630d-1a47-482c-aade-e37f5e0bb9f4
    ```
    {: screen}

## Check the current volume configuration
{: #vpc-block-profile-check}
{: step}

1. View the current block volume profile and configuration.

    ```sh
    ibmcloud is vol $VOLUME_ID
    ```
    {: pre}

    Example output before migration

    ```txt
    ID                      r026-3afe630d-1a47-482c-aade-e37f5e0bb9f4
    Name                    pvc-d4a2b016-a5e4-46de-9214-a64f5fc8e344
    Status                  available
    Attachment state        attached
    Capacity                100
    IOPS                    3000
    Bandwidth(Mbps)         393
    Profile                 5iops-tier
    Storage Generation      1
    Adjustable IOPS         false
    Busy                    false
    ```
    {: screen}

1. Note the following values from the output. You'll use these to verify the migration was successful.
    - Profile: `5iops-tier` (Gen-1)
    - Storage Generation: `1`
    - Adjustable IOPS: `false`

## Start the migration
{: #vpc-block-profile-migrate}
{: step}

The migration process runs in the background while your volume remains attached to your pod and your application continues running. IOPS are automatically adjusted to SDP defaults, and the process typically takes 5-15 minutes.

1. Initiate the migration to the SDP profile.

    ```sh
    ibmcloud is volume-job-create $VOLUME_ID --profile sdp
    ```
    {: pre}

## Monitor migration progress
{: #vpc-block-profile-monitor}
{: step}

1. Check the migration job status. If the output indicates `Status: updating` and `Busy: true`, the migration is in progress. When the output shows `Status: available` and `Busy: false`, the migration is complete.

    ```sh
    ibmcloud is volume-jobs $VOLUME_ID
    ```
    {: pre}

1. Check the volume status.

    ```sh
    watch -n 30 "ibmcloud is vol $VOLUME_ID | grep -E 'Status|Busy|Profile'"
    ```
    {: pre}

    Example output during migration

    ```txt
    Status                  updating
    Busy                    true
    Profile                 5iops-tier
    ```
    {: screen}

## Verify migration completion
{: #vpc-block-profile-verify}
{: step}

1. Confirm that the volume is using the Gen-2 profile.

    ```sh
    ibmcloud is vol $VOLUME_ID
    ```
    {: pre}

    Example output after migration

    ```txt
    ID                          r026-3afe630d-1a47-482c-aade-e37f5e0bb9f4
    Name                        pvc-d4a2b016-a5e4-46de-9214-a64f5fc8e344
    Status                      available
    Attachment state            attached
    Capacity                    100
    IOPS                        4000
    Bandwidth(Mbps)             1000
    Profile                     sdp
    Storage Generation          2
    Adjustable IOPS             true
    Adjustable Capacity States  unattached,attached
    Adjustable IOPS States      unattached,attached
    Busy                        false
    ```
    {: screen}

1. Verify the following success indicators:
    - Profile: `sdp`
    - Storage Generation: `2`
    - Adjustable IOPS: `true`
    - IOPS: Increased (for example, 3000 to 4000)
    - Bandwidth: Improved

## Updating the PersistentVolume metadata
{: #vpc-block-profile-update-pv}
{: step}

1. Update the PV metadata to reflect the Gen-2 profile.

    ```sh
    oc patch pv $PV_NAME --type='json' -p='[
      {"op": "replace", "path": "/spec/storageClassName", "value": "ibmc-vpc-block-sdp"},
      {"op": "replace", "path": "/spec/csi/volumeAttributes/profile", "value": "sdp"},
      {"op": "replace", "path": "/spec/csi/volumeAttributes/iops", "value": "4000"}
    ]'
    ```
    {: pre}

1. Verify the update.

    ```sh
    oc get pv $PV_NAME -o jsonpath='{.spec.storageClassName}'
    ```
    {: pre}

    Expected output

    ```txt
    ibmc-vpc-block-sdp
    ```
    {: screen}

    The PVC continues to show the original StorageClass name. This behavior is expected because the `storageClassName` field in a PVC is immutable. The actual storage profile is determined by the PV, which you updated in this step.
    {: note}

## Validate your application
{: #vpc-block-profile-validate}
{: step}

Verify that your application is functioning correctly after the migration.

1. Check the pod status. Verify that all pods are in the `Running` state.

    ```sh
    oc get pods -n <namespace>
    ```
    {: pre}

1. Verify the volume attachment. Confirm that the volume is mounted correctly.

    ```sh
    oc describe pod <pod-name> -n <namespace> | grep -A 5 "Volumes:"
    ```
    {: pre}

1. Check the application logs. Look for any errors related to storage or I/O operations.

    ```sh
    oc logs <pod-name> -n <namespace> --tail=50
    ```
    {: pre}

1. Test the application endpoint if applicable. Verify that the application responds correctly.

    ```sh
    curl -I https://<app-endpoint>/health
    ```
    {: pre}

## Create a Gen-2 StorageClass
{: #vpc-block-profile-storageclass}
{: step}

Create an SDP StorageClass for provisioning new volumes.

1. Create a YAML file for the StorageClass. Save the following configuration as `storageclass-sdp.yaml`.

    ```yaml
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: ibmc-vpc-block-sdp-general
      labels:
        app: ibm-vpc-block-csi-driver
    provisioner: vpc.block.csi.ibm.io
    parameters:
      profile: "sdp"
      iops: "5000"
      csi.storage.k8s.io/fstype: "ext4"
      billingType: "hourly"
      encrypted: "false"
      region: ""
      zone: ""
      tags: "generation:2,profile:sdp"
    reclaimPolicy: Delete
    allowVolumeExpansion: true
    volumeBindingMode: WaitForFirstConsumer
    ```
    {: codeblock}

1. Apply the StorageClass.

    ```sh
    oc apply -f storageclass-sdp.yaml
    ```
    {: pre}

1. Verify the StorageClass creation.

    ```sh
    oc get storageclass ibmc-vpc-block-sdp-general
    ```
    {: pre}

## Adjust IOPS and throughput to optimize performance
{: #vpc-block-profile-optimize}

After migration, you can adjust IOPS and throughput (bandwidth) dynamically based on your workload requirements.

- Start with 5,000 IOPS for general workloads.
- Use 10,000 or more IOPS for databases.
- Monitor usage and adjust based on actual requirements.

### Updating IOPS
{: #vpc-block-profile-update-iops}

1. Increase IOPS for higher performance.

    ```sh
    ibmcloud is volume-update $VOLUME_ID --iops 8000
    ```
    {: pre}

1. Verify the IOPS update.

    ```sh
    ibmcloud is vol $VOLUME_ID | grep IOPS
    ```
    {: pre}

### Updating throughput (bandwidth)
{: #vpc-block-profile-update-bandwidth}

After migration to the SDP profile, volumes have a default bandwidth allocation. You can increase the bandwidth to improve throughput for I/O-intensive workloads.

1. Check the current bandwidth allocation.

    ```sh
    ibmcloud is vol $VOLUME_ID | grep Bandwidth
    ```
    {: pre}

1. Increase bandwidth for higher throughput. Use the `--bandwidth` option to specify the desired bandwidth in Mbps.

    ```sh
    ibmcloud is volume-update $VOLUME_ID --bandwidth 2000
    ```
    {: pre}

1. Verify the bandwidth update.

    ```sh
    ibmcloud is vol $VOLUME_ID | grep Bandwidth
    ```
    {: pre}

    The bandwidth value represents the maximum throughput in MB/s that the volume can achieve. Higher bandwidth values provide better performance for data-intensive operations.
    {: tip}

## Troubleshooting
{: #vpc-block-profile-troubleshooting}

### Migration stuck in updating status
{: #vpc-block-profile-ts-stuck}

If the migration status remains `updating` for more than 30 minutes, complete the following steps. Note that larger volumes take longer to migrate and might remain in the `updating` state for 45 minutes.

1. Check the job details.

    ```sh
    ibmcloud is volume-jobs $VOLUME_ID
    ```
    {: pre}

1. Check the volume status for errors or warnings.

    ```sh
    ibmcloud is vol $VOLUME_ID | grep -E "Status|Busy"
    ```
    {: pre}

1. Wait an additional 15 minutes as large volumes take longer to migrate.

1. Check the [IBM Cloud status page](https://cloud.ibm.com/status){: external} for VPC service issues.

1. If the migration is stuck for more than 1 hour, contact [IBM Support](/docs/get-support){: external} with the job ID.

### PVC shows old StorageClass
{: #vpc-block-profile-ts-pvc-class}

If the PVC still references the Gen-1 StorageClass after migration, this behavior is expected and requires no action. The PVC `storageClassName` field is immutable. The actual storage profile is determined by the PV, which you updated in the previous steps. Functionality is not affected.

1. Verify that the PV (not PVC) is correct.

    ```sh
    oc get pv $PV_NAME -o jsonpath='{.spec.storageClassName}'
    ```
    {: pre}

    Expected output

    ```txt
    ibmc-vpc-block-sdp
    ```
    {: screen}

### Performance not improved
{: #vpc-block-profile-ts-performance}

If you don't see a performance increase after migration, complete the following steps.

1. Check the actual IOPS allocation.

    ```sh
    ibmcloud is vol $VOLUME_ID | grep IOPS
    ```
    {: pre}

1. Check the volume profile.

    ```sh
    ibmcloud is vol $VOLUME_ID | grep Profile
    ```
    {: pre}

1. Increase the IOPS allocation.

    ```sh
    ibmcloud is volume-update $VOLUME_ID --iops 10000
    ```
    {: pre}

1. Verify the update.

    ```sh
    ibmcloud is vol $VOLUME_ID | grep IOPS
    ```
    {: pre}

## Next steps
{: #vpc-block-profile-next-steps}

After completing the migration, consider the following next steps.

- Migrate additional volumes by repeating this tutorial.
- Monitor volume performance and adjust IOPS as needed.
- Update your deployment templates to use Gen-2 StorageClasses for new volumes.
- Review [Block Storage capacity and performance](/docs/vpc?topic=vpc-capacity-performance&interface=ui){: external} for optimization guidance.
