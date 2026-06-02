---

copyright:
  years: 2024, 2026
lastupdated: "2026-06-02"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, red hat, encrypt, security, kms, root key, crk, hpcs, key protect, migration

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Migrating cluster secrets and worker nodes from HPCS to Key Protect
{: #encryption-hpcs-to-kp-migration}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

You can migrate your cluster secret encryption, worker pool, and worker node disk encryption from {{site.data.keyword.hscrypto}} (HPCS) to {{site.data.keyword.keymanagementservicefull}} by using the Key Protect migration tools. This process updates the encryption key and instance references and usage for cluster secrets, encrypted workers, and worker pools.
{: shortdesc}

The migration process can take up to an hour or longer depending on the number of resources you need to migrate. Make sure to plan accordingly.
{: important}


## Before you begin
{: #encryption-hpcs-to-kp-migration-prereqs}

Before you migrate from HPCS to Key Protect, review the following requirements and considerations.

- You must have a {{site.data.keyword.keymanagementserviceshort}} instance and root key created. For more information, see [Setting up a key management service (KMS) provider](/docs/openshift?topic=openshift-encryption-setup).
- You must have the correct permissions in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) to enable KMS in your cluster. For more information, see [Setting up a key management service (KMS) provider](/docs/openshift?topic=openshift-encryption-setup).
- Service-to-service authorization policies must be in place and must be scoped at the Key Protect instance or service level, not at the key ring or key level. This is a current limitation that applies to both worker node and cluster secret encryption.

Do not delete your HPCS root key until the migration is completed and its success is verfied.
{: important}

## Step 1. Setting up service-to-service authorization
{: #encryption-hpcs-to-kp-migration-auth}

Before you can migrate from HPCS to Key Protect, you must set up the required service-to-service authorization policies in {{site.data.keyword.cloud_notm}} IAM. This step must be completed individually for cluster secrets and worker nodes. Note that you might have these policies in place already, in which case you do not need to recreate them.

### Authorization for cluster secret encryption
{: #encryption-hpcs-to-kp-migration-auth-secrets}

To migrate cluster secret encryption, you need a service authorization policy from {{site.data.keyword.containerlong_notm}} to your Key Protect instance.

1. Navigate to the [service authorizations](https://cloud.ibm.com/iam/authorizations){: external} page in the {{site.data.keyword.cloud_notm}} console.
2. Click **Create**.
3. Set the **Source account** to **This account** if the cluster resides in the current account. If the cluster is in a different account, select **Other account** and provide the account ID.
4. Set the **Source service** to **Kubernetes Service**.
5. Set the **Target service** to **Key Protect**.
6. Scope the authorization to the Key Protect **service** or **instance** level. Do not scope to a specific key ring or key.
7. Include at least **Reader** service access.
8. Enable the authorization to be delegated by the source and dependent services.
9. Click **Authorize**.

### Authorizations for worker node disk encryption
{: #encryption-hpcs-to-kp-migration-auth-workers}

To migrate worker node disk encryption for VPC clusters, you need service authorization policies for both {{site.data.keyword.containerlong_notm}} and Cloud Block Storage to your Key Protect instance.

Follow these steps to create the authorization for {{site.data.keyword.containerlong_notm}}. If these policies already exist, you do not need to recreate them.
1. Navigate to the [service authorizations](https://cloud.ibm.com/iam/authorizations){: external} page in the {{site.data.keyword.cloud_notm}} console.
2. Click **Create**.
3. Set the **Source account** to **This account** if the cluster resides in the current account. If the cluster is in a different account, select **Other account** and provide the account ID.
4. Set the **Source service** to **Kubernetes Service**.
5. Set the **Target service** to **Key Protect**.
6. Scope the authorization to the Key Protect **service** or **instance** level. Do not scope to a specific key ring or key.
7. Include at least **Reader** service access.
8. Enable the authorization to be delegated by the source and dependent services.
9. Click **Authorize**.

Follow these steps to create the authorization for Cloud Block Storage.
1. Navigate to the [service authorizations](https://cloud.ibm.com/iam/authorizations){: external} page in the {{site.data.keyword.cloud_notm}} console.
2. Click **Create**.
3. Set the **Source account** to **This account** if the cluster resides in the current account. If the cluster is in a different account, select **Other account** and provide the account ID.
4. Set the **Source service** to **Cloud Block Storage**. Note that in the CLI, the source service is referred to as **server-protect**.
5. Set the **Target service** to **Key Protect**.
6. Scope the authorization to the Key Protect **service** or **instance** level. Do not scope to a specific key ring or key.
7. Include at least **Reader** service access.
8. Click **Authorize**.

{{site.data.keyword.openshiftlong_notm}} automatically creates an additional service-to-service delegation policy for the Cloud Block Storage service in the IBM-managed service account to the Key Protect instance. This delegation policy is required so that the VPC infrastructure can encrypt the boot volume of the worker nodes with your Key Protect root key. If you have issues after migration, verify that this delegated authorization policy exists in your [IAM authorizations](https://cloud.ibm.com/iam/authorizations){: external}.
{: note}


## Step 2. Identify key usage for migration
{: #encryption-hpcs-to-kp-migration-detect}

Identify which resources in your account need to be migrated from HPCS to Key Protect. For information on different methods for identifying usage, see [Searching for usage](/docs/key-protect?topic=key-protect-migrate-st#migration-search-for-usage) in the Key Protect documentation.

For each cluster, you can view key registrations with the `ibmcloud kp registrations -i KMS_INSTNACE_ID KEY_ID` command. The output shows the following key registrations:
    - One registration for cluster secrets
    - One registration for *each* encrypted worker pool
    - One registration for *each* encrypted worker

The registrations might look similar to the following:

```yaml
"crn:v1:staging:public:containers-kubernetes:us-south:a/1152aa1c1ec54274ac42b8ad8507c90c:d70mi70206f7fchch5h0::
crn:v1:staging:public:containers-kubernetes:us-south:a/1152aa1c1ec54274ac42b8ad8507c90c:d79qqpt20aca2a0ii8v0:worker-pool:d79qqpt20aca2a0ii8v0-edea88a
crn:v1:staging:public:is:us-south-1:a/e2523561f3864f058711d94392c19e9b::volume:r134-799cdc60-c598-4a58-913b-b29ad312a143
```
{: json}

### Optional: Using the Key Usage Reporter tool
{: #kur-tool}

One available method for identifying key usage is the Key Usage Reporter (KUR) tool, which scans your account and provides a report of HPCS keys in use. This detection tool helps you identify which clusters have secret encryption enabled with HPCS keys and which worker pools have worker node disk encryption enabled with HPCS keys. The report output shows cluster secrets, workers, and worker pools as separate resources tied to a specific HPCS key and instance. For detailed instructions on running the detection tool, see [Detecting HPCS key usage](/docs/key-protect?topic=key-protect-kur) in the Key Protect documentation.

Note that the KUR tool might not show every HPCS usage case, so it's important to review all methods for identifying usage. If you use a cross-account KMS instance, you must run the KUR tool in all relevant accounts.
{: important}


## Step 3. Running the migration tool
{: #encryption-hpcs-to-kp-migration-migrate}

After you have identified the resources using HPCS keys and set up the required service authorizations, use the Key Protect migration tool to migrate your encryption keys. Before you complete this step, make sure you have created the [required service-to-service authorization policies](#encryption-hpcs-to-kp-migration-auth).

For detailed instructions on running the migration tool, see [Migrating to Key Protect](/docs/key-protect?topic=key-protect-migrate-tool) in the Key Protect documentation.


### What happens during migration
{: #encryption-hpcs-to-kp-migration-process}

When you run the migration tool, the following actions occur:

Cluster secret encryption
:   The migration triggers the creation of a key registration on the Key Protect key. Then, the data encryption key is re-encrypted using the Key Protect key instead of the HPCS key. The registration is then deleted from the HCPS key. There is no expected downtime during the operation and your cluster continues to function normally.

Worker node disk encryption
:   - **For encrypted worker pools**: The migration triggers the creation of a key registration on the worker pool for the encrypted workers. The references to the HPCS instance and key are updated to point to the Key Protect instance and key. The registration is then deleted from the HPCS key. Any new workers added to the worker pool now use the updated key info. There is no expected downtime during the operation and your worker pool continues to function normally.
:   - **For individual workers**: The migration triggers the creation of a key registration on the Key Protect key. Then, the data encryption key is re-encrypted using the Key Protect key instead of the HPCS key. The registration is then deleted from the HCPS key. There is no expected downtime during the operation and your worker continues to function normally.

During the migration, {{site.data.keyword.openshiftlong_notm}} automatically creates an additional service-to-service delegation policy for the Cloud Block Storage service in the IBM-managed service account to the Key Protect instance. This delegation policy is required so that the VPC infrastructure can encrypt the boot volume of the worker nodes with your Key Protect root key. If you have issues during or after migration, verify that this delegated authorization policy exists in your [IAM authorizations](https://cloud.ibm.com/iam/authorizations){: external}.
{: note}


### Step 4. Verifying the migration
{: #encryption-hpcs-to-kp-migration-verify}

After the migration completes, verify that your cluster is using the Key Protect key.

1. Check the cluster status to ensure the master is ready.
    ```sh
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}

    In the output, verify that the **Master Status** is **Ready** and the **Key Management Service** shows the KMS Instance ID and KMS Root Key ID of the Key Protect instance.

1. For worker node encryption, verify that the worker pool references the Key Protect key.
    ```sh
    ibmcloud oc worker-pool get --worker-pool <worker_pool_name_or_ID> --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Review the **KMS** and **CRK** fields in the output to confirm they reference your Key Protect instance and root key.

1. Verify that you can access cluster secrets.
    ```sh
    oc get secrets --all-namespaces
    ```
    {: pre}

1. In your Key Protect instance, verify that the cluster, workers and worker pools are registered to the new root key, and that the key registrations do not exist on the old HPCS keys. For more information, see [Viewing associations between root keys and encrypted {{site.data.keyword.cloud_notm}} resources](/docs/key-protect?topic=key-protect-view-protected-resources).

## Next steps
{: #encryption-hpcs-to-kp-migration-next}

After successfully migrating to Key Protect and verifying the migration:

- Monitor your cluster for any issues related to encryption or key access.
- Update any documentation or runbooks that reference the HPCS instance.
- Consider [rotating your Key Protect root key](/docs/key-protect?topic=key-protect-key-rotation) according to your security policies.
