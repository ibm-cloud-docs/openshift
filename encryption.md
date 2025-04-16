---

copyright: 
  years: 2014, 2025
lastupdated: "2025-04-16"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, red hat, encrypt, security, kms, root key, crk

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Encryption overview
{: #encryption}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}

Protect sensitive information in your {{site.data.keyword.openshiftlong}} cluster to ensure data integrity and to prevent your data from being exposed to unauthorized users by setting up a key management service (KMS) provider.
{: shortdesc}

{{site.data.keyword.openshiftlong_notm}} offers encryption at several layers in your cluster. Encryption for some components is managed by IBM while, for other components, you have the option to bring your own KMS provider credentials to manage encryption yourself.

When you're done with this page, [try out the quiz](https://quizzes.12dekrh4l1b4.us-south.codeengine.appdomain.cloud/openshift/strategy/quiz.php).
{: tip}

The following table outlines the encryption options for {{site.data.keyword.openshiftlong_notm}} clusters.


| Component | Encrypted by default? | Bring your own key support? | Enablement time | Supported KMS providers | Cross account support? |
| --- | --- | --- | --- | --- | --- |
| [Control plane](#control-plane-encryption) | Yes | No | During cluster creation. | IBM managed {{site.data.keyword.keymanagementserviceshort}} | N/A | N/A | No |
| [Worker node disks](#worker-node-encryption) | Yes | Yes | During cluster creation or worker pool creation. | - {{site.data.keyword.hscrypto}}  \n - {{site.data.keyword.keymanagementserviceshort}} | Yes |
| [Cluster secrets](#cluster-secret-encryption) | No | Yes | After cluster creation by using `kms enable`. | - {{site.data.keyword.hscrypto}}  \n - {{site.data.keyword.keymanagementserviceshort}} | Cross account supported for Classic and VPC clusters only. |
| [Persistent storage](#persistent-encryption) | Depends on the storage provider. | Depends on provider | After cluster creation, when setting up storage. | - {{site.data.keyword.hscrypto}}  \n - {{site.data.keyword.keymanagementserviceshort}} | Depends on the storage provider. |
{: caption="Default and optional data encryption" caption-side="bottom"}



## Control plane
{: #control-plane-encryption}

Control plane encryption is managed by IBM.
- Components in the {{site.data.keyword.redhat_openshift_notm}} master boot up on a LUKS-encrypted drive using an IBM-managed key.
- The etcd component of the master stores the configuration files of your Kubernetes resources, such as deployments and secrets.
- Data in etcd is stored on the local disk of the Kubernetes master and is backed up to {{site.data.keyword.cos_full_notm}}.
- Data is encrypted during transit to {{site.data.keyword.cos_full_notm}} and at rest. 



## Worker node disks
{: #worker-node-encryption}

Attached disks are used to boot your worker node, host the container file system, and store locally pulled images. The encryption and number of disks varies by infrastructure provider.

VPC worker nodes
:   By default, the one primary disk of VPC worker nodes is AES-256 bit encrypted at rest by the [underlying VPC infrastructure provider](/docs/vpc?topic=vpc-block-storage-about#vpc-storage-encryption). You can manage the encryption of the worker nodes by enabling a KMS provider at the worker pool level. For more information, about encryption VPC worker node disks, see [Setting up worker node disk encryption for VPC clusters](/docs/openshift?topic=openshift-encryption-vpc-worker-disks).

Classic worker nodes
:   The primary disk has the kernel images to boot your worker node. This disk is unencrypted. The secondary disk has the container file system and locally pulled images. This disk is AES 256-bit encrypted with an IBM-managed LUKS encryption key that is unique to the worker node and stored as a Kubernetes secret in your cluster. When you reload or update your worker nodes, the LUKS keys are rotated.



{{site.data.keyword.satelliteshort}} worker nodes
:   The encryption of the OS disk and secondary disk is managed at the IAAS layer of the platform Satellite is deployed on. The encryption of persistent storage volumes utilized within the cluster is managed at the persistent storage plug-in level and backing storage device level. For more information about encryption for storage devices or plug-ins, see the device provider documentation or the storage plug-in documentation.




## Cluster secrets
{: #cluster-secret-encryption}

Kubernetes secrets are base64 encoded by default. You can further protect Kubernetes secrets and any credentials stored in secrets by enabling a key management service (KMS) provider, such as {{site.data.keyword.keymanagementservicefull}} or {{site.data.keyword.hscrypto}}.

When you enable a key management service (KMS) provider for your cluster, you bring your own root key. The root key is used to encrypt the data encryption keys (DEKs) which are then used to encrypt the secrets in your cluster. The root key is stored in the KMS provider instance that you control. The encrypted DEKs are stored in etcd and can only be unencrypted using the root key from the KMS provider. For more information about how key encryption works, see [Envelope encryption](/docs/key-protect?topic=key-protect-envelope-encryption).

Review the following notes about cluster secret encryption.
- Cluster secrets are encrypted by using your KMS.
- Cluster secrets are automatically updated after rotating root keys.
- Clusters that use the root key are viewable from the KMS provider interface.
- Clusters automatically respond if you disable, enable, or restore root keys.
- Disabling a root key restricts cluster functionality until you reenable the key.
- Deleting a root key makes the cluster unusable and unrecoverable.
- You can have only one KMS provider and key enabled in the cluster at a time. 
- You can switch the KMS provider and key.
- You can't disable KMS provider encryption.


To set up cluster secret encryption, see [Setting up cluster secret encryption](/docs/openshift?topic=openshift-encryption-secrets).


## Persistent storage
{: #persistent-encryption}

Depending on the type of persistent storage you use, you can encrypt the data written to the storage volumes by enabling a KMS provider. For more information about the types of persistent storage and encryption available, see [Understanding your storage options](/docs/openshift?topic=openshift-storage-plan).





## Next steps
{: #plan-storage-next}

[Test your knowledge with a quiz](https://quizzes.12dekrh4l1b4.us-south.codeengine.appdomain.cloud/openshift/encryption/quiz.php).
{: tip}

To continue the planning process, choose a [storage option](/docs/openshift?topic=openshift-storage-plan). If you're ready to get started with encryption, move on to [creating a KMS instance and root key](/docs/openshift?topic=openshift-encryption-setup). 
