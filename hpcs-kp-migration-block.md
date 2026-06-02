---

copyright:
  years: 2026, 2026
lastupdated: "2026-06-02"


keywords: key protect, hpcs, kms, migrate, block storage, vpc, csi driver, encryption, crk

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# Migrating VPC Block Storage from HPCS to Key Protect
{: #migrate_hpcs_kms_block}

Migrate your Hyper Protect Crypto Services (HPCS) encryption for VPC Block Storage volumes to use {{site.data.keyword.keymanagementservicelong_notm}} (Key Protect) instead.
{: shortdesc}

## Before you begin
{: #hpcs-kms-block-before}

If you have not already done so, review the information in the [migration overview](/docs/openshift?topic=openshift-migrate_hpcs_kp) to determine if you need to migrate your VPC Block storage volumes to use Key Protect instead of HPCS.

## Prerequisites for migration
{: #hpcs-kms-block-prereqs}

Complete these steps before you begin the migration.

1. [Create a new](/docs/key-protect?topic=key-protect-provision) or use an existing {{site.data.keyword.keymanagementservicelong_notm}} Dedicated instance.

2. From the Key Protect instance, note the destination Customer Root Key (CRK) CRN.

    ```sh
    ibmcloud kp keys -i <kp-instance-id>
    ```
    {: pre}

3. Ensure VPC Block Storage has read access to the Key Protect instance. You might need to [assign access by using IAM](/docs/iam?topic=iam-serviceauth). This access can be cross-account and must be configured correctly before proceeding.

4. If you have not done so, [download the migration tools](/docs/openshift?topic=openshift-migrate_hpcs_kp#request) found in the migration overview.

## Migration steps
{: #hpcs-kms-block-steps}

Follow these steps to migrate your VPC Block Storage volumes from HPCS to Key Protect.

1. Create a CSV file that maps your source HPCS CRK to the destination Key Protect CRK.

    1. Get the CRN of your HPCS root key.

        ```sh
        ibmcloud resource service-instance <hpcs-instance-name>
        ```
        {: pre}

    2. Get the CRN of your Key Protect root key.

        ```sh
        ibmcloud resource service-instance <kp-instance-name>
        ```
        {: pre}

    3. Create a CSV file (for example, `hpcs-kms-migration.csv`) with the following format:

        ```csv
        <source-hpcs-crk-crn>,<destination-kp-crk-crn>
        ```
        {: codeblock}

        Example:
        ```csv
        crn:v1:staging:public:hs-crypto:us-south:a/1152aa1c1ec54274ac42b807c90c:0ce92f39-69fd-4200-ba53-5ed555689:key:43eb6a-5451-4ea1-8080-0ca2d6cc7,crn:v1:staging:public:kms:us-south:a/1152aa1c1ec54274ac4ad8507c90c:b2ee9d-b658-4939-bb63-ffb6e7442:key:8cf424f4-bd6a-4de9-8ad5-5c60332de
        ```
        {: codeblock}

2. Set up the required environment variables for the migration tool.

    1. Export the required environment variables. Replace the placeholder values with your actual endpoints and API key.

        ```sh
        export HPCS_API_ENDPOINT=https://<hpcs-instance-id>.api.<region>.hs-crypto.appdomain.cloud
        export KP_ST_ENDPOINT=https://<kp-instance-id>.api.<region>.kms.appdomain.cloud
        export IBMCLOUD_API_KEY=<api-key-with-access-to-kms-and-hpcs>
        export IBMCLOUD_API_KEY_KP_ST=$IBMCLOUD_API_KEY
        ```
        {: pre}

        For staging environments, also set:
        ```sh
        export IBMCLOUD_STAGE=true
        export DEBUG_MODE=true
        ```
        {: pre}

3. Validate the CSV file and check the current migration state.

    1. Run the status command to validate your configuration.

        ```sh
        ./crk-migration-tool-darwin-arm64-1.1.0 status hpcs-kms-migration.csv
        ```
        {: pre}

    2. Review the output to ensure the source and destination CRKs are correctly identified.

4. Create the CRK migration intent using the CSV file.

    1. Run the create command to establish the migration intent.

        ```sh
        ./crk-migration-tool-darwin-arm64-1.1.0 create hpcs-kms-migration.csv
        ```
        {: pre}

    2. Verify that the intent was created successfully by checking the command output.

5. Perform the actual CRK migration by syncing the intent.

    1. Run the sync command to execute the migration.

        ```sh
        ./crk-migration-tool-darwin-arm64-1.1.0 sync hpcs-kms-migration.csv
        ```
        {: pre}

    2. Wait for the sync operation to complete. This process migrates the encryption keys for your volumes.

6. Verify that your volumes now reference the Key Protect CRK.

    1. List your Persistent Volumes and note the volume IDs.

        ```sh
        oc get pv
        ```
        {: pre}

    2. Describe a Persistent Volume to get the volume ID.

        ```sh
        oc describe pv <pv-name>
        ```
        {: pre}

    3. Check the volume details using the IBM Cloud CLI.

        ```sh
        ibmcloud is volume <volume-id>
        ```
        {: pre}

    4. In the output, verify that the `Encryption Key` field now references the CRK CRN from your Key Protect instance instead of the HPCS instance.

7. Update your storage classes to ensure that all future PVCs use the Key Protect CRK.

    1. List your existing storage classes.

        ```sh
        oc get storageclass
        ```
        {: pre}

    2. Identify storage classes that reference the HPCS CRK in their parameters.

    3. Delete the HPCS-backed storage classes.

        ```sh
        oc delete storageclass <storageclass-name>
        ```
        {: pre}

    4. Create new storage classes with the Key Protect CRK CRN. Use the following example as a template:

        ```yaml
        apiVersion: storage.k8s.io/v1
        kind: StorageClass
        metadata:
          name: ibmc-vpc-block-kms
        provisioner: vpc.block.csi.ibm.io
        parameters:
          profile: "general-purpose"
          encrypted: "true"
          encryptionKey: "<key-protect-crk-crn>"
          csi.storage.k8s.io/fstype: "ext4"
        reclaimPolicy: Delete
        allowVolumeExpansion: true
        volumeBindingMode: WaitForFirstConsumer
        ```
        {: codeblock}

    5. Apply the new storage class.

        ```sh
        oc apply -f <storageclass-file>
        ```
        {: pre}

## Next steps
{: #hpcs-kms-block-next}

- Verify that your applications continue to function correctly with the migrated volumes.
- Monitor your Key Protect instance for any access or encryption issues.
- Update your documentation and runbooks to reflect the new Key Protect configuration.
- Consider setting up [key rotation policies](/docs/key-protect?topic=key-protect-set-rotation-policy) for your Key Protect root keys.
