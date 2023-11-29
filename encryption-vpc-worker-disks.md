---

copyright: 
  years: 2023, 2023
lastupdated: "2023-11-28"

keywords: openshift, kubernetes, red hat, encrypt, security, kms, root key, crk

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Setting up worker node disk encryption for VPC clusters
{: #encryption-vpc-worker-disks}

[Virtual Private Cloud]{: tag-vpc}


By default, the one primary disk of VPC worker nodes is AES-256 bit encrypted at rest by the [underlying VPC infrastructure provider](/docs/vpc?topic=vpc-block-storage-about#vpc-storage-encryption).


You can manage the encryption of the worker nodes by enabling a KMS provider at the worker pool level.

1. [Create a KMS instance and root key](/docs/openshift?topic=openshift-encryption-setup).
2. Make sure that you have the following service authorization policies in {{site.data.keyword.cloud_notm}} IAM, created under the account where the KMS instance resides, with the following details:
    - **Required service access policy for Kubernetes Service and the KMS provider**
        1. Set the **Source account** for **This account** if the cluster you want to authorize accessing KMS resides in the current account, otherwise if the cluster located under a different account, select **Other account** and provide the account ID.
        2. Set the **Source service** to **Kubernetes Service**.
        3. Set the **Target service** to your KMS provider, such as **Key Protect**.
        4. Include at least **Reader** service access.
        5. Enable the authorization to be delegated by the source and dependent services.
    - **Required service access policy for Cloud Block Storage and the KMS provider**
        1. Set the **Source account** for **This account** if the cluster you want to authorize accessing KMS resides in the current account, otherwise if the cluster located under a different account, select **Other account** and provide the account ID.
        2. Set the **Source service** to **Cloud Block Storage**.
        3. Set the **Target service** to your KMS provider, such as **Key Protect**.
        4. Include at least **Reader** service access.

    {{site.data.keyword.openshiftlong_notm}} automatically creates a service-to-service delegation policy for the Cloud Block Storage service in the IBM-managed service account to the KMS provider instance under the account where the KMS instance and CRK reside. This delegation policy is required so that the VPC infrastructure can encrypt the boot volume of the worker nodes in the IBM-managed service account with your customer-provided root key of the KMS provider. 
    {: note}

3. Create a cluster or worker pool that includes the account where the KMS instance resides, the KMS provider instance and root key. Each worker node in the worker pool then is encrypted by the KMS provider that you manage. Each worker pool in your cluster can use the same KMS instance and root key, the same KMS instance with different root keys, or different instances.
    - **Creating a cluster**: Only the `default` worker pool's nodes are encrypted. After you create the cluster, if you create more worker pools, you must enable encryption in each pool separately. For more information, see [Creating clusters](/docs/containers?topic=containers-cluster-create-vpc-gen2&interface=ui) or the [CLI reference documentation](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-vpc-gen2).

    - **Creating a worker pool**: For more information, see [Creating VPC worker pools](/docs/openshift?topic=openshift-add-workers-vpc#vpc_add_pool) or the [CLI reference documentation](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_pool_create_vpc_gen2).


4. Verify that your worker pool is encrypted by reviewing the worker pool details.
    - **UI**: After selecting your cluster from the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click **Worker pools**. Then, click your worker pool.
    - **CLI**: Review the **KMS** and **CRK** fields in the output of the following command.
        ```sh
        ibmcloud oc worker-pool get --name <worker_pool_name> --cluster <cluster_name_or_ID>
        ```
        {: codeblock}

5. Optional: [Rotate the root key](/docs/vpc?topic=vpc-vpc-encryption-managing&interface=ui) periodically per your company's security compliance guidelines. For more information, see the [Managing encryption topic in the VPC documentation](/docs/vpc?topic=vpc-vpc-encryption-managing).

    Do not delete your KMS instance. You can't change the KMS instance that is used to encrypt the worker pool. If you disable or delete the root key, your worker nodes enter a `critical` state until you restore the root key and [reboot](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot) the worker nodes.
    {: important}

The encryption for the disks of the worker nodes in your worker pool are now managed by the root key in your KMS provider. If you created a cluster, the worker pool is the `default` worker pool.


