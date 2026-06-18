---

copyright:
  years: 2026, 2026
lastupdated: "2026-06-17"


keywords: key protect, hpcs, kms, migrate, block storage, classic, encryption, crk, dek

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}

# Migrate Portworx volumes from HPCS to Key Protect
{: #migrate_hpcs_kp_px}

Migrate your Hyper Protect Crypto Services (HPCS) encryption for Portworx storage volumes to use {{site.data.keyword.keymanagementservicelong_notm}} (Key Protect) instead.
{: shortdesc}


## Before you begin
{: #hpcs-kp-migration-px-prereqs}

Before you migrate your Portworx encrypted volumes from {{site.data.keyword.hscrypto}} to {{site.data.keyword.keymanagementserviceshort}}, complete the following steps.

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
2. Make sure you have installed the [Key Protect CLI plugin](/docs/cli?topic=cli-ibmcloud_commands_settings).
3. If you do not already have one, create a [Key Protect instance](/docs/key-protect?topic=key-protect-provision) to use for the migration.
3. Make sure you have the Portworx HPCS to Key Protect migration script to use for migrating your volumes. This tool is included in the `hpcs-2-kp-k8s.zip` file when you request tool access. See step 1 of the [migration overview](/docs/openshift?topic=openshift-migrate_hpcs_kp) for more information.


## Migrating Portworx encrypted volumes
{: #hpcs-kp-migration-px-steps}

Follow the steps to migrate your Portworx encrypted volumes from {{site.data.keyword.hscrypto}} to {{site.data.keyword.keymanagementserviceshort}}. These steps include running a migration script.

1. Set your {{site.data.keyword.cloud_notm}} API key as an environment variable.
    ```sh
    export IC_API_KEY="YOUR_API_KEY"
    ```
    {: pre}

2. Run the migration script with the required flags. Replace the placeholder values with your specific configuration details.
    ```sh
    ./hpcs_kp_px_migration_script.sh \
      --region us-south \
      --resource-group Default \
      --hpcs-endpoint https://api.us-south.hs-crypto.cloud.ibm.com:8389/ \
      --hpcs-instance-id <hpcs-instance-id> \
      --hpcs-root-key-id <hpcs-root-key-id> \
      --kp-endpoint https://us-south.kms.cloud.ibm.com/ \
      --kp-instance-id <kp-instance-id> \
      --kp-root-key-id <kp-root-key-id> \
      --cluster-name my-px-cluster \
      --etcd-endpoints <etcd-endpoints> \
      --px-namespace kube-system
    ```
    {: pre}

    Review the table for required command parameters.

    | Flag | Description |
    | --- | --- |
    | `--region` | {{site.data.keyword.cloud_notm}} region (for example, `us-south`). |
    | `--resource-group` | {{site.data.keyword.cloud_notm}} resource group. |
    | `--hpcs-endpoint` | {{site.data.keyword.hscrypto}} key management endpoint URL. |
    | `--hpcs-instance-id` | {{site.data.keyword.hscrypto}} instance ID. |
    | `--hpcs-root-key-id` | {{site.data.keyword.hscrypto}} root key ID. |
    | `--kp-endpoint` | {{site.data.keyword.keymanagementserviceshort}} endpoint URL. |
    | `--kp-instance-id` | {{site.data.keyword.keymanagementserviceshort}} instance ID. |
    | `--kp-root-key-id` | {{site.data.keyword.keymanagementserviceshort}} root key ID. |
    | `--cluster-name` | Portworx cluster name (from `pxctl status` output). |
    | `--px-namespace` | Namespace where Portworx runs on your cluster. |
    {: caption="Migration script flags" caption-side="bottom"}

3. After the migration script completes, update the `px-ibm` Kubernetes secret in the `portworx` namespace to point to the {{site.data.keyword.keymanagementserviceshort}} instance and root key you configured. Update the following fields:
    - `IBM_SERVICE_API_KEY`
    - `IBM_INSTANCE_ID`
    - `IBM_BASE_URL`
    - `IBM_CUSTOMER_ROOT_KEY`

4. Restart Portworx on each cluster nodes. Wait for Portworx to show as healthy on each node before proceeding to the next.

    Restart Portworx on a node.
    ```sh
    kubectl label node px/service=restart
    ```
    {: pre}

6. Validate that encrypted volumes are accessible and that new volumes use {{site.data.keyword.keymanagementserviceshort}} as the key management service (KMS).
