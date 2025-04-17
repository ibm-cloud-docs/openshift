---

copyright: 
  years: 2023, 2025
lastupdated: "2025-04-17"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, red hat, encrypt, security, kms, root key, crk

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Setting up cluster secret encryption
{: #encryption-secrets}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}

After creating a cluster, you can protect Kubernetes secrets and any credentials stored in your secrets by enabling a key management service (KMS) provider, such as {{site.data.keyword.keymanagementservicefull}} or {{site.data.keyword.hscrypto}}.
{: shortdesc}

## Enabling secret encryption from the CLI
{: #encryption-secrets-cli}
{: cli}

You can enable a KMS provider, update the KMS provider instance, or update the root key through the CLI.

Setting up cross-account encryption by using a KMS in a different account is supported in the CLI or API. 
{: note}

1. [Create a KMS instance and root key](/docs/openshift?topic=openshift-encryption-setup). If you want to use cross account KMS encryption, make sure to create the KMS and root key in the account whose KMS instance you want to use.
1. Get the ID of the KMS instance that you previously created.
    ```sh
    ibmcloud oc kms instance ls
    ```
    {: pre}

1. Get the **ID** of the root key that you previously created.
    ```sh
    ibmcloud oc kms crk ls --instance-id <KMS_instance_ID>
    ```
    {: pre}

1. Enable the KMS provider to encrypt secrets in your cluster. Complete the options with the information that you previously retrieved. The KMS provider's private cloud service endpoint is used by default to download the encryption keys. To use the public cloud service endpoint instead, include the `--public-endpoint` option. The enablement process can take some time to complete.
    ```sh
    ibmcloud oc kms enable -c <cluster_name_or_ID> --instance-id <kms_instance_ID> --crk <root_key_ID> [--public-endpoint]
    ```
    {: pre}
    
    During the enablement, you might not be able to access the Kubernetes master such as to update YAML configurations for deployments.
    {: important}

1. Verify that the KMS enablement process is finished. The process is finished when that the **Master Status** is **Ready** and **Key management service** is **enabled**.
    ```sh
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}

    Example output when the enablement is in progress
    ```sh
    NAME:                   <cluster_name>   
    ID:                     <cluster_ID>   
    ...
    Master Status:          Key management service feature enablement in progress.  
    ```
    {: screen}

    Example output when the master is ready
    ```sh
    NAME:                   <cluster_name>   
    ID:                     <cluster_ID>   
    ...
    Master Status:          Ready (1 min ago)
    ...
    Key Management Service: enabled   
    ```
    {: screen}

    After the KMS provider is enabled in the cluster, all cluster secrets are automatically encrypted.
    {: note}

1. Optional: [Verify that your secrets are encrypted](#encryption-secrets-verify).

Key enablement, which is initiated through {{site.data.keyword.redhat_openshift_notm}}, means that the encryption switches to a new key from the KMS provider. Key rotation, which is initiated through the KMS provider, means the encryption switches to a new version of the existing key. Do not delete any root key in your KMS instance if it is rotated from the KMS provider. A root key can be deleted only when it is no longer in use. For example, after you enable a new key and verify that the cluster is not using the old key anymore, you can delete the old key. If you delete a root key that a cluster uses, the cluster becomes unusable, loses all its data, and can't be recovered. When you rotate a root key, you can't reuse a previous root key for the same cluster. Similarly, if you disable a root key, operations that rely on reading secrets fail. Unlike deleting a root key, however, you can re-enable a disabled key to make your cluster usable again.
{: important}

## Enabling secret encryption from the console
{: #encryption-secrets-console}
{: ui}

You can enable a KMS provider, update the KMS provider instance, or update the root key through the {{site.data.keyword.cloud_notm}} console.


1. [Create a KMS instance and root key](/docs/openshift?topic=openshift-encryption-setup). If you want to use cross account KMS encryption, make sure to create the KMS and root key in the account whose KMS instance you want to use.
1. From the [console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}, select the cluster that you want to enable encryption for.
1. In the **Key management service** section, click **Enable**. If you already enabled the KMS provider, click **Update**.
1. Select the **Key management service instance** and **Root key** that you want to use for the encryption.

    During the enablement, you might not be able to access the Kubernetes master such as to update YAML configurations for deployments.
    {: important}
    
1. Click **Enable** (or **Update**).
1. Verify that the KMS enablement process is finished.
    Example output when the enablement is in progress.
    ```sh
    Master status   KMS feature enablement in progress.  
    ```
    {: screen}

    Example output when the master is ready.
    ```sh
    Master status   Ready
    ```
    {: screen}

    After the KMS provider is enabled in the cluster, all cluster secrets are automatically encrypted.
    {: note}

1. Optional: [Verify that your secrets are encrypted](#encryption-secrets-verify).

Key enablement, which is initiated through {{site.data.keyword.redhat_openshift_notm}}, means the encryption switches to a new key from the KMS provider. Key rotation, which is initiated through the KMS provider, means the encryption switches to a new version of the existing key. Do not delete any root key in your KMS instance if it is rotated from the KMS provider. A root key can be deleted only when it is no longer in use. For example, after you enable a new key and verify that the cluster is not using the old key anymore, you can delete the old key. If you delete a root key that a cluster uses, the cluster becomes unusable, loses all its data, and can't be recovered. When you rotate a root key, you can't reuse a previous root key for the same cluster. Similarly, if you disable a root key, operations that rely on reading secrets fail. Unlike deleting a root key, however, you can re-enable a disabled key to make your cluster usable again.
{: important}

## Rotating the root key for your cluster
{: #encryption-secrets-rotate}

To rotate the root key that is used to encrypt your cluster, repeat the steps to enable KMS encryption. When you rotate a root key, you can't reuse a previous root key for the same cluster.

You can rotate the root key manually from your KMS instance. This action automatically re-enables KMS in your cluster with the new root key. To manually rotate your keys, see your KMS provider docs.

* {{site.data.keyword.keymanagementservicefull}}: See [Rotating your keys](/docs/key-protect?topic=key-protect-getting-started-tutorial#get-started-next-steps-best-practices-key-rotate).
* {{site.data.keyword.hscrypto}}: See [Rotating root keys manually](/docs/hs-crypto?topic=hs-crypto-rotate-keys).


## Verifying secret encryption
{: #encryption-secrets-verify}

After you enable a KMS provider in your {{site.data.keyword.openshiftlong_notm}} cluster, you can verify that your cluster secrets are encrypted by disabling the root key. When you disable the root key, the cluster can no longer decrypt the secrets and becomes unusable, which signifies that your secrets were encrypted.

Make sure that you have the {{site.data.keyword.cloud_notm}} IAM **Administrator** platform and **Manager** service access role for the cluster.
{: note}

1. To check that KMS encryption is enabled, verify that the **Key Management Service** status is set to `enabled` in the output of the following command.
    ```sh
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
1. Verify that you can list the secrets in your cluster.
    ```sh
    oc get secrets --all-namespaces
    ```
    {: pre}

1. In your KMS instance, [disable the root key](/docs/key-protect?topic=key-protect-disable-keys) that is used to encrypt your cluster. If you encrypted your cluster with a KMS and CRK from a different account, the CRK can only be disabled from the account where it is located.

1. Wait for the cluster to detect the change to your root key.

1. Try to list your secrets. You get a timeout error because you can no longer connect to your cluster. If you try to set the context for your cluster by running `ibmcloud oc cluster config`, the command fails.
    ```sh
    oc get secrets --all-namespaces
    ```
    {: pre}

    Example output

    ```sh
    Unable to connect to the server: dial tcp 169.48.110.250:32346: i/o timeout
    ```
    {: screen}

1. Check that your cluster is in a **warning** state. Your cluster remains in this state and is unusable until you enable your root key again.
    ```sh
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}

1. In your KMS instance, enable the root key so that your cluster returns to a **normal** state and becomes usable again.
