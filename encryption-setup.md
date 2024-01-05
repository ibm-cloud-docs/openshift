---

copyright: 
  years: 2023, 2024
lastupdated: "2024-01-05"


keywords: openshift, kubernetes, red hat, encrypt, security, kms, root key, crk

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Setting up a key management service (KMS) provider
{: #encryption-setup}


[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}

You can protect Kubernetes secrets and any credentials stored in your secrets by enabling a key management service (KMS) provider, such as {{site.data.keyword.keymanagementservicefull}} or {{site.data.keyword.hscrypto}}.



Do not delete root keys in your KMS instance, even if you rotate to a new key. If you delete a root key that a cluster uses, the cluster becomes unusable, loses all its data, and can't be recovered. Similarly, if you disable a root key, operations that rely on reading secrets fail. Unlike deleting a root key, however, you can reenable a disabled key to make your cluster usable again.
{: important}

Before you can enable a key management service (KMS) provider in your cluster, you must first create a KMS instance and a root key. 

1. Create an instance of the KMS provider that you want to use.
    - [{{site.data.keyword.keymanagementserviceshort}}](/docs/key-protect?topic=key-protect-provision#provision).
    - [{{site.data.keyword.hscrypto}}](https://cloud.ibm.com/catalog/services/hyper-protect-crypto-services){: external}.

1. Create a root key in your KMS instance.
    - [{{site.data.keyword.keymanagementserviceshort}} root key](/docs/key-protect?topic=key-protect-create-root-keys#create-root-keys).
    - [{{site.data.keyword.hscrypto}} root key](/docs/hs-crypto?topic=hs-crypto-create-root-keys). By default, the root key is created without an expiration date.

    **{{site.data.keyword.keymanagementserviceshort}}:** Need to set an expiration date to comply with internal security policies? [Create the root key by using the API](/docs/key-protect?topic=key-protect-create-root-keys&interface=api#create-root-key-api) and include the `expirationDate` parameter. **Important**: Before your root key expires, repeat these steps to update your cluster to use a new root key. When a root key expires, the cluster secrets can't be decrypted and your cluster becomes unusable. Depending on the cluster version, the time lapse between the root key expiring and the cluster no longer being able to decrypt secrets might be about an hour, or when the master is refreshed.
    {: tip}

1. Make sure that you have the correct permissions in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) to enable KMS in your cluster.
    * Ensure that you have the [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-users#checking-perms) for the cluster.
    * Ensure that the API key owner of the [API key](/docs/openshift?topic=openshift-access-creds#api_key_about) that is set for the region and resource group that your cluster is in has the correct permissions for the KMS provider. For more information on granting access in IAM to the KMS provider, see the [{{site.data.keyword.keymanagementserviceshort}} user access documentation](/docs/key-protect?topic=key-protect-manage-access) or [{{site.data.keyword.hscrypto}} user access documentation](/docs/hs-crypto?topic=hs-crypto-manage-access#platform-mgmt-roles).
        * For example, to create an instance and root key, you need at least the **Editor** platform and **Writer** service access roles for your KMS provider.
        * If you plan to use an existing KMS instance and root key, you need at least the **Viewer** platform and **Reader** service access roles for your KMS provider.
    * An additional **Reader** [service-to-service authorization policy](/docs/account?topic=account-serviceauth) between {{site.data.keyword.openshiftlong_notm}} and {{site.data.keyword.keymanagementserviceshort}} is automatically created for your cluster, if the policy does not already exist. Without this policy, your cluster can't use all the {{site.data.keyword.keymanagementserviceshort}} features.

1. **Optional** Complete the following additional steps if you plan to [set up worker node disk encryption for a VPC cluster](/docs/openshift?topic=openshift-encryption-vpc-worker-disks).

1. Create a cluster and enable secret encryption.

## Rotating your KMS root key
{: #encryption-rotate}

To rotate the root key that is used to encrypt your cluster, you can repeat the steps to enable KMS encryption from your KMS provider CLI or console. When you rotate a root key, you can't reuse a previous root key for the same cluster.

You can rotate the root key from your KMS instance. This action automatically re-enables KMS in your cluster with the new root key. To manually rotate your keys, see your KMS provider docs.

* {{site.data.keyword.keymanagementservicefull}}: See [Rotating your keys](/docs/key-protect?topic=key-protect-getting-started-tutorial#get-started-next-steps-best-practices-key-rotate).
* {{site.data.keyword.hscrypto}}: See [Rotating root keys manually](/docs/hs-crypto?topic=hs-crypto-rotate-keys).



