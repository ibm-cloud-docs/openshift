---

copyright:
  years: 2026, 2026
lastupdated: "2026-06-02"


keywords: key protect, hpcs, kms, migrate, block storage, classic, encryption, crk, dek

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# Migrating Classic Block Storage from HPCS to Key Protect
{: #migrate_hpcs_kms_classic_block}

Migrate your Hyper Protect Crypto Services (HPCS) encryption for Classic Block Storage volumes to use {{site.data.keyword.keymanagementservicelong_notm}} (Key Protect) instead.
{: shortdesc}

## Before you begin
{: #hpcs-kms-classic-block-before}

Before you begin, verify that you need to migrate your Classic Block Storage volumes to use Key Protect instead of HPCS. You can complete this process manually by following the steps in this section, or you can see the [migration overview]() for details on using an automated detection script.

Follow these steps to manually determine if you need to migrate your Classic Block Storage volumes.

1. Verify that HPCS encryption is being used by the block storage plugin on your cluster.

    1. List all `kms-config` secrets in your cluster.

        ```sh
        oc get secrets -A --field-selector type=ibm.io/kms-config
        ```
        {: pre}

    2. For each `kms-config` secret found, verify that it is of type `hpcs` by checking if the configuration contains `hs-crypto`.

        ```sh
        oc get secret <kms-config-name> -n <namespace> -o json | jq '.data | map_values(@base64d)' | grep "hs-crypto"
        ```
        {: pre}

    3. For each HPCS configuration found, identify the PVCs that use them.

        ```sh
        oc get pvc -A -l "encryptionKeySecret=<kms-config-name>"
        ```
        {: pre}

2. If no HPCS-encrypted PVCs are found, no migration is required. If HPCS-encrypted PVCs are found, proceed with the migration steps.

## Prerequisites for migration
{: #hpcs-kms-classic-block-prereqs}

Complete these steps before you begin the migration.

1. Back up all cluster resources before starting the migration process.

    Plan to keep your resource backups for several weeks in case a rollback is required.
    {: tip}

    ```sh
    oc get pvc --all-namespaces -o yaml > all-pvcs.yaml
    oc get pv -o yaml > all-pv.yaml
    oc get storageclass -o yaml > all-storage-classes.yaml
    oc get secrets --field-selector type=ibm.io/kms-config --all-namespaces -o yaml > all-kms-config.yaml
    oc get secrets -n ibm-block-secrets --field-selector type=ibm.io/dek-secret -o yaml > all-dek-secrets.yaml
    ```
    {: pre}

2. [Create a new](/docs/key-protect?topic=key-protect-provision) or use an existing {{site.data.keyword.keymanagementservicelong_notm}} instance.

3. [Create a root key](/docs/key-protect?topic=key-protect-create-root-keys) in your Key Protect instance. Note the root key ID for use in the migration steps.

4. Ensure you have the necessary IAM permissions to access both the HPCS and Key Protect instances.

5. Install the {{site.data.keyword.keymanagementserviceshort}} CLI plug-in if not already installed.

    ```sh
    ibmcloud plugin install kp -r "IBM Cloud"
    ```
    {: pre}

## Migration steps
{: #hpcs-kms-classic-block-steps}

Follow these steps to migrate your Classic Block Storage volumes from HPCS to Key Protect.

### Step 1: Replace the HPCS secret with a Key Protect configuration
{: #replace-secret}

1. Create a new KMS configuration file for your Key Protect instance. Save the following file as `target-kp-config.yaml`. Make sure to replace the placeholder values with your Key Protect instance details.

    ```yaml
    apiVersion: v1
    kind: Secret
    metadata:
      name: <kms-config-name>
      namespace: <namespace>
    stringData:
      config: |-
        {
          "api_key":"<your-api-key>",
          "iam_endpoint":"https://iam.cloud.ibm.com",
          "key_protect_endpoint":"https://<region>.api.<region>.kms.appdomain.cloud",
          "instance_id":"<kp-instance-id>",
          "root_key_id":"<kp-root-key-id>"
        }
    type: ibm.io/kms-config
    ```
    {: codeblock}

    Values
    - `<kms-config-name>`: The name of your existing HPCS KMS configuration secret.
    - `<namespace>`: The namespace where the secret is located.
    - `<your-api-key>`: An API key with access to your Key Protect instance.
    - `<region>`: The region where your Key Protect instance is located.
    - `<kp-instance-id>`: Your Key Protect instance ID.
    - `<kp-root-key-id>`: The root key ID you created in Key Protect.

2. Delete the existing HPCS KMS configuration secret.

    ```sh
    oc delete secret <kms-config-name> -n <namespace>
    ```
    {: pre}

3. Create the new Key Protect configuration secret.

    ```sh
    oc create -f target-kp-config.yaml
    ```
    {: pre}

### Step 2: Update PVC encryption keys to use Key Protect
{: #migrate-keys}

For each encrypted PVC that needs to be migrated, follow these steps to unwrap the data encryption key (DEK) from HPCS and rewrap it with Key Protect.

1. Configure the {{site.data.keyword.keymanagementserviceshort}} CLI to point to your HPCS instance.

    ```sh
    export KP_PRIVATE_ADDR=https://<hpcs-instance-id>.api.<region>.hs-crypto.appdomain.cloud
    export KP_INSTANCE_ID=<hpcs-instance-id>
    export ROOT_KEY_ID=<hpcs-root-key-id>
    ```
    {: pre}

2. Retrieve the HPCS wrapped DEK (WDEK) for the encrypted PVC.

    1. Find the DEK secret for your PVC.

        ```sh
        oc get secrets -n ibm-block-secrets --field-selector type=ibm.io/dek-secret | grep <pv-name>
        ```
        {: pre}

    2. Extract the wrapped DEK from the secret.

        ```sh
        oc get secrets -n ibm-block-secrets <pv-secret-name> -o yaml | grep wrappedDEK | awk '{print $2}' | base64 --decode
        ```
        {: pre}

3. Unwrap the wrapped DEK using the HPCS root key. Save the unwrapped DEK from the output.

    ```sh
    ibmcloud kp key unwrap $ROOT_KEY_ID <wrapped-dek>
    ```
    {: pre}


4. Configure the {{site.data.keyword.keymanagementserviceshort}} CLI to point to your Key Protect instance.

    Use a separate terminal window to avoid accidentally switching between HPCS and Key Protect configurations.
    {: tip}

    ```sh
    export KP_PRIVATE_ADDR=https://<kp-instance-id>.api.<region>.kms.appdomain.cloud
    export KP_INSTANCE_ID=<kp-instance-id>
    export ROOT_KEY_ID=<kp-root-key-id>
    ```
    {: pre}

5. Rewrap the DEK using the Key Protect root key. Save the wrapped DEK from the output.

    ```sh
    ibmcloud kp key wrap $ROOT_KEY_ID -p <unwrapped-dek-base64>
    ```
    {: pre}



6. Replace the HPCS wrapped DEK with the Key Protect wrapped DEK in the PVC secret.

    1. Encode the new wrapped DEK to base64.

        ```sh
        echo <kp-wrapped-dek> | base64
        ```
        {: pre}

    2. Edit the DEK secret and replace the `wrappedDEK` value with the new base64-encoded Key Protect wrapped DEK.

        ```sh
        oc edit secret -n ibm-block-secrets <pv-secret-name>
        ```
        {: pre}

7. Optional: Verify the volume by restarting the pod that uses the encrypted PVC.

    ```sh
    oc delete pod <pod-name> -n <namespace>
    ```
    {: pre}

8. Repeat these steps for all encrypted PVCs that need to be migrated from HPCS to Key Protect.

9. Check that all pods using encrypted PVCs are in a running state.

    ```sh
    oc get pods -A
    ```
    {: pre}


## Next steps
{: #hpcs-kms-classic-block-next}

- Update your documentation and runbooks to reflect the new Key Protect configuration.
- Consider setting up [key rotation policies](/docs/key-protect?topic=key-protect-set-rotation-policy) for your Key Protect root keys.
- If you encounter any issues during or after the migration, [open an IBM Cloud support ticket](/docs/support?topic=support-using-avatar).
