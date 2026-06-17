---

copyright:
  years: 2026, 2026
lastupdated: "2026-06-17"


keywords: key protect, hpcs, kms, migrate, odf, openshift data foundation, encryption, csi, osd, noobaa, ceph

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# Migrating OpenShift Data Foundation from HPCS to Key Protect
{: #migrate_hpcs_kp_odf}

Migrate your Hyper Protect Crypto Services (HPCS) encryption for OpenShift Data Foundation (ODF) to use {{site.data.keyword.keymanagementservicelong_notm}} (Key Protect) instead.

## Before you begin
{: #hpcs-kp-migration-odf-before}

Before you begin the migration, complete the following steps to determine if your cluster requires migration and to prepare your environment.

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
2. Ensure you have the following tools installed:
    - `oc` or `oc` CLI with access to your ODF cluster
    - `jq` for JSON processing
    - `curl` for API requests
3. If you have not already done so, [Create a Key Protect instance](/docs/key-protect?topic=key-protect-provision) or use an existing {{site.data.keyword.keymanagementservicelong_notm}} instance in the same region as your cluster.
4. Verify that the Ceph toolbox pod is enabled in your cluster. Set `storagecluster.spec.enableCephTools: true` in your StorageCluster configuration if it is not already enabled.
5. Download the ODF HPCS to Key Protect migration scripts to use for migrating your volumes. The scripts are `migrate-odf.sh` (the main script that invokes the other three), `migrate-osd.sh`, `migrate-csi.sh`, and `migrate-noobaa.sh`, and are included in the `hpcs-2-kp-k8s.zip` file when you request tool access. See step 1 of the [migration overview](/docs/openshift?topic=openshift-migrate_hpcs_kp) for more information.


## Migration steps
{: #hpcs-kp-migration-odf-steps}

1. Use the following script to determine if the cluster is using HPCS keys that need to be migrated.

    ```sh
    ./migrate-odf.sh detect
    ```
    {: pre}

2. Create a `.env` file in the current directory and fill in your Key Protect details.

    ```sh
    $ cat .env
    KP_INSTANCE_ID=XXX
    KP_IAM_API_KEY=XXX
    KP_KEY_ID=XXX
    KP_URL=https://XXX.api.us-south.kms.appdomain.cloud
    ```
    {: pre}

3. Run the migration script.
    ```sh
    ./migrate-odf.sh migrate
    ```
    {: pre}

4. After the migration is complete, verify that your resources are accessible and use {{site.data.keyword.keymanagementserviceshort}} as the key management service (KMS).
