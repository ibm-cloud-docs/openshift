---

copyright: 
  years: 2014, 2022
lastupdated: "2022-01-11"

keywords: portworx, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Storing data on software-defined storage (SDS) with Portworx
{: #portworx}

[Portworx](https://portworx.com/products/portworx-enterprise//){: external} is a highly available software-defined storage solution that you can use to manage local persistent storage for your containerized databases and other stateful apps, or to share data between pods across multiple zones.
{: shortdesc}

**Supported infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


## About Portworx
{: #about-portworx}

Review frequently asked questions to learn more about Portworx and how Portworx provides highly available persistent storage management for your containerized apps.
{: shortdesc}

### What is software-defined storage (SDS)?
{: #about-px-sds}

An SDS solution abstracts storage devices of various types, sizes, or from different vendors that are attached to the worker nodes in your cluster. Worker nodes with available storage on hard disks are added as a node to a storage cluster. In this cluster, the physical storage is virtualized and presented as a virtual storage pool to the user. The storage cluster is managed by the SDS software. If data must be stored on the storage cluster, the SDS software decides where to store the data for highest availability. Your virtual storage comes with a common set of capabilities and services that you can leverage without caring about the actual underlying storage architecture.

### How does Portworx work?
{: #about-px-work}

Portworx aggregates available storage that is attached to your worker nodes and creates a unified persistent storage layer for containerized databases or other stateful apps that you want to run in the cluster. By using volume replication of each container-level volume across multiple worker nodes, Portworx ensures data persistence and data accessibility across zones.

Portworx also comes with additional features that you can use for your stateful apps, such as volume snapshots, volume encryption, isolation, and an integrated Storage Orchestrator for Kubernetes (Stork) to ensure optimal placement of volumes in the cluster. For more information, see the [Portworx documentation](https://docs.portworx.com/){: external}.

### What worker node flavor in {{site.data.keyword.openshiftlong_notm}} is the right one for Portworx?
{: #about-px-flavors}

The worker node flavor that you need depends on the infrastructure provider that you use. If you have a classic cluster, {{site.data.keyword.openshiftlong_notm}} provides bare metal worker node flavors that are optimized for [software-defined storage (SDS) usage](/docs/openshift?topic=openshift-planning_worker_nodes#sds). These flavors also come with one or more raw, unformatted, and unmounted local disks that you can use for your Portworx storage layer. In classic clusters, Portworx offers the best performance when you use SDS worker node machines that come with 10 Gbps network speed.

In VPC clusters, make sure to select a [virtual server flavor](/docs/vpc?topic=vpc-profiles) that meets the [minimum hardware requirements for Portworx](https://docs.portworx.com/start-here-installation/){: external}. The flavor that you choose must have a network speed of 10 Gpbs or more for optimal performance. None of the VPC flavors are set up with raw and unformatted block storage devices. To successfully install and run Portworx, you must [manually attach block storage devices](/docs/openshift?topic=openshift-utilities#vpc_api_attach) to each of your worker nodes first.

### What if I want to run Portworx in a classic cluster with non-SDS worker nodes?
{: #about-px-non-sds}

You can install Portworx on non-SDS worker node flavors, but you might not get the performance benefits that your app requires. Non-SDS worker nodes can be virtual or bare metal. If you want to use virtual machines, use a worker node flavor of `b3c.16x64` or better. Virtual machines with a flavor of `b3c.4x16` or `u3c.2x4` don't provide the required resources for Portworx to work properly. Bare metal machines come with sufficient compute resources and network speed for Portworx, but you must [add raw, unformatted, and unmounted block storage](#create_block_storage) before you can use these machines.

For classic clusters, virtual machines have only 1000 Mbps of networking speed, which is not sufficient to run production workloads with Portworx. Instead, provision Portworx on bare metal machines for the best performance.
{: important}

If your classic cluster has deprecated Ubuntu 16 x1c or x2c worker node flavors, update your cluster to have [Ubuntu 18 x3c worker nodes](/docs/containers?topic=containers-update#machine_type).
{: tip}

### How can I make sure that my data is stored highly available?
{: #about-px-ha}

You need at least three worker nodes in your Portworx cluster so that Portworx can replicate your data across nodes. By replicating your data across worker nodes, Portworx can ensure that your stateful app can be rescheduled to a different worker node in case of a failure without losing data. For even higher availability, use a [multizone cluster](/docs/openshift?topic=openshift-ha_clusters#multizone) and replicate your volumes across worker nodes in 3 or more zones.

### What volume topology offers the best performance for my pods?
{: #about-px-topology}

One of the biggest challenges when you run stateful apps in a cluster is to make sure that your container can be rescheduled onto another host if the container or the entire host fails. In Docker, when a container must be rescheduled onto a different host, the volume does not move to the new host. Portworx can be configured to run `hyper-converged` to ensure that your compute resources and the storage are always placed onto the same worker node. When your app must be rescheduled, Portworx moves your app to a worker node where one of your volume replicas resides to ensure local-disk access speed and best performance for your stateful app. Running `hyper-converged` offers the best performance for your pods, but requires storage to be available on all worker nodes in your cluster.

You can also choose to use only a subset of worker nodes for your Portworx storage layer. For example, you might have a worker pool with SDS worker nodes that come with local raw block storage, and another worker pool with virtual worker nodes that don't come with local storage. When you install Portworx, a Portworx pod is scheduled onto every worker node in your cluster as part of a DaemonSet. Because your SDS worker nodes have local storage, these worker nodes are into the Portworx storage layer only. Your virtual worker nodes are not included as a storage node because of the missing local storage. However, when you deploy an app pod to your virtual worker node, this pod can still access data that is physically stored on an SDS worker node by using the Portworx DaemonSet pod. This setup is referred to as `storage-heavy` and offers slightly slower performance than the `hyper-converged` setup because the virtual worker node must talk to the SDS worker node over the private network to access the data.

{{site.data.keyword.openshiftlong_notm}} does not support the [Portworx experimental `InitializerConfiguration` admission controller](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/hyperconvergence/#initializer-experimental-feature-in-stork-v1-1).
{: note}


### Can I install Portworx in a private cluster?
{: #about-px-private}

Yes. To install Portworx in a private cluster, your {{site.data.keyword.cloud_notm}} account must be set up with [Virtual Routing and Forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf) and access to private cloud service endpoints for {{site.data.keyword.cloud_notm}} services. To install Portworx in a cluster that doesn't have VRF or access to private CSEs, you must create a rule in the default security group to allow inbound and outbound traffic for the following IP addresses: `166.9.24.81`, `166.9.22.100`, `166.9.20.178`. For more information, see [Updating the default security group](/docs/vpc?topic=vpc-updating-the-default-security-group#updating-the-default-security-group).



### What's next?
{: #about-px-next}

All set? Let's start with [creating a cluster with an SDS worker pool of at least three worker nodes](/docs/containers?topic=containers-clusters). If you want to include non-SDS worker nodes into your Portworx cluster, [add raw block storage](#create_block_storage) to each worker node. After your cluster is prepared, [install Portworx](#install_portworx) in your cluster and create your first hyper-converged storage cluster.



## Planning your Portworx setup
{: #portworx_planning}

Before you create your cluster and install Portworx, review the following planning steps.
{: shortdesc}

**Minimum required permissions**:
* **Administrator** and **VirtualServerConsoleAdmin** for the VPC service.
* **Manager** and **Administrator** for the {{site.data.keyword.registrylong_notm}} service.
* **Operator** and **Manager** for the Kubernetes service.

1. Review the [Portworx limitations](#portworx_limitations).
2. Create a [multizone cluster](/docs/containers?topic=containers-clusters).
    1. Infrastructure provider: If you use classic infrastructure, you must choose a bare metal flavor for the worker nodes. For classic clusters, virtual machines have only 1000 Mbps of networking speed, which is not sufficient to run production workloads with Portworx. Instead, provision Portworx on bare metal machines for the best performance.
    2. Worker node flavor: Choose an SDS or bare metal flavor. If you want to use virtual machines, use a worker node with 16 vCPU and 64 GB memory or more, such as `b3c.16x64`. Virtual machines with a flavor of `b3c.4x16` or `u3c.2x4` don't provide the required resources for Portworx to work properly.
    3. Minimum number of workers: Two worker nodes per zone across three zones, for a minimum total of six worker nodes.
3. **VPC and non-SDS classic worker nodes only**: [Create raw, unformatted, and unmounted block storage](#create_block_storage).
4. For production workloads, create an [external Databases for etcd](#portworx_database) instance for your Portworx metadata key-value store.
5. **Optional** [Set up encryption](#setup_encryption).
6. [Install Portworx](#install_portworx).
7. Maintain the lifecycle of your Portworx deployment in your cluster.
    1. When you update worker nodes in [VPC](#portworx_vpc_up) clusters, you must take additional steps to re-attach your Portworx volumes. You can attach your storage volumes by using the API or CLI.
        * [Attaching {{site.data.keyword.block_storage_is_short}} volumes with the CLI](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_storage_att_cr).
        * [Attaching {{site.data.keyword.block_storage_is_short}} volumes with the API](/docs/openshift?topic=openshift-utilities#vpc_api_attach).
    2. To remove a Portworx volume, storage node, or the entire Portworx cluster, see [Portworx cleanup](#portworx_cleanup).

## Creating raw, unformatted, and unmounted block storage for VPC and non-SDS classic worker nodes
{: #create_block_storage}

If you want to build your Portworx storage layer on non-SDS worker nodes in your classic cluster or VPC worker nodes, you must add raw, unformatted, and unmounted block storage to your worker nodes first.
{: shortdesc}

Raw block storage can't be provisioned by using Kubernetes persistent volume claims (PVCs) as the block storage device is automatically formatted by {{site.data.keyword.openshiftlong_notm}}. Instead, you can use the {{site.data.keyword.cloud_notm}} Block Volume Attacher plug-in in classic clusters or the VPC console, CLI, or API in VPC clusters to add block storage to your worker nodes.

Portworx supports block storage only. Worker nodes that mount file or object storage can't be used for the Portworx storage layer.
{: note}

Keep in mind that the networking of non-SDS worker nodes in classic clusters is not optimized for Portworx and might not offer the performance benefits that your app requires.
{: note}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) **Classic clusters:**

1. [Install the {{site.data.keyword.cloud_notm}} Block Volume Attacher plug-in](/docs/openshift?topic=openshift-utilities#block_storage_attacher).
2. [Manually add block storage](/docs/openshift?topic=openshift-utilities#manual_block) to your worker nodes. For highly available data storage, Portworx requires at least 3 worker nodes with raw and unformatted block storage.
3. If you want to use [journal devices](https://docs.portworx.com/install-with-other/operate-and-maintain/performance-and-tuning/tuning/){: external}, choose from the following options.
    - Attach an additional disk to at least 3 worker nodes to use for the journal. [Manually add](/docs/openshift?topic=openshift-utilities#manual_block) a 3 GB block storage device to a worker node in your cluster and find the device path. To find the device path after attaching the disk, log in to your worker node with `oc debug <node>` and run `lsblk` to list the devices on that node.
    - Select one of the block storage devices that you added earlier to use for the journal and find the device path. To find the device path after attaching the disk, log in to your worker node with `oc debug <node>` and run `lsblk` to list the devices on that node.
    - Let Portworx automatically create a journal partition during installation.
4. If you want to use a specific device for the internal Portworx key value database (KVDB), choose from the following options.
    - Attach an additional disk to at least 3 worker nodes to use for key value database (KVDB). [Manually add](/docs/openshift?topic=openshift-utilities#manual_block) a 3 GB block storage device to at least 3 worker nodes in your cluster and find the device path. To find the device path after attaching the disk, log in to your worker node with `oc debug <node>` and run `lsblk` to list the devices on that node.
    - Select one of the block storage devices that you added earlier and find the device path. To find the device path after attaching the disk, log in to your worker node with `oc debug <node>` and run `lsblk` to list the devices on that node.
5. [Attach the block storage](/docs/openshift?topic=openshift-utilities#attach_block) to your worker nodes.
6. Continue with your Portworx setup by [Setting up a key-value store for Portworx metadata](#portworx_database).

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) **VPC clusters:**
1. Follow the [steps](/docs/openshift?topic=openshift-utilities#vpc_cli_attach) to create the {{site.data.keyword.block_storage_is_short}} instances and attach these to each worker node that you want to add to the Portworx storage layer. For highly available data storage, Portworx requires at least 3 worker nodes with raw and unformatted block storage.
2. If you want to use [journal devices](https://docs.portworx.com/install-with-other/operate-and-maintain/performance-and-tuning/tuning/){: external}, choose from the following options.
    - [Attach](/docs/openshift?topic=openshift-utilities#vpc_cli_attach) an additional 3 GB disk to at least 3 worker nodes in your cluster and find the device path. To find the device path after you attach the disk, log in to your worker node with `oc debug <node>` and run `lsblk` to list the devices on that node.
    - Select a device on a worker node where you want Portworx to create the journal.
3. If you want to use a specific device for the internal Portworx KVDB, choose from the following options.
    - Attach an additional disk to at least 3 worker nodes use for the KVDB. [Manually add](/docs/openshift?topic=openshift-utilities#manual_block) a 3 GB block storage device to at least 3 worker nodes in your cluster and find the device path. To find the device path after attaching the disk, log in to your worker node with `oc debug <node>` and run `lsblk` to list the devices on that node.
    - Select one of the block storage devices that you added earlier to use for the KVDB and find the device path. To find the device path after attaching the disk, log in to your worker node with `oc debug <node>` and run `lsblk` to list the devices on that node.
4. Continue with your Portworx setup by [Setting up a key-value store for Portworx metadata](#portworx_database).





## Setting up a key-value store for Portworx metadata
{: #portworx_database}

Decide on the key-value store that you want to use to store Portworx metadata.
{: shortdesc}

Before you begin, review the [Planning your Portworx setup section](#portworx_planning)
{: important}

The Portworx key-value store serves as the single source of truth for your Portworx cluster. If the key-value store is not available, then you can't work with your Portworx cluster to access or store your data. Existing data is not changed or removed when the Portworx database is unavailable.

To set up your key-value store, choose between the following options:
- [Automatically set up a key-value database (KVDB) during the Portworx installation](#portworx-kvdb)
- [Set up a Databases for etcd service instance](#databases-for-etcd)

### Using the Portworx key-value database
{: #portworx-kvdb}

Automatically set up a key-value database (KVDB) during the Portworx installation that uses the space on the additional local disks that are attached to your worker nodes.
{: shortdesc}

You can keep the Portworx metadata inside your cluster and store them along with the operational data that you plan to store with Portworx by using the internal key-value database (KVDB) that is included in Portworx. For general information about the internal Portworx KVDB, see the [Portworx documentation](https://docs.portworx.com/concepts/internal-kvdb/){: external}.

To set up the internal Portworx KDVB, follow the steps in [Installing Portworx in your cluster](#install_portworx).

If you plan to use the internal KVDB, make sure that your cluster has a minimum of 3 worker nodes with additional local block storage so that the KVDB can be set up for high availability. Your data is automatically replicated across these 3 worker nodes and you can choose to scale this deployment to replicate data across up to 25 worker nodes.
{: note}

### Optional: Setting up a Databases for etcd service instance
{: #databases-for-etcd}

If you want to use an external database service for your Portworx cluster metadata and keep the metadata separate from the operational data that you plan to store with Portworx, set up a [Databases for etcd](/docs/databases-for-etcd?topic=databases-for-etcd-getting-started) service instance in your cluster.
{: shortdesc}

Databases for etcd is a managed etcd service that securely stores and replicates your data across three storage instances to provide high availability and resiliency for your data. For more information, see the [Databases for etcd getting started tutorial](/docs/databases-for-etcd?topic=databases-for-etcd-getting-started#getting-started). Your Databases for etcd storage automatically scales in size if required and you are charged for the amount storage that you use.

1. Make sure that you have the [**Administrator** platform access role in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM)](/docs/account?topic=account-assign-access-resources#assign-new-access) for the Databases for etcd service.  

2. Provision your Databases for etcd service instance.
    1. Open the [Databases for etcd catalog page](https://cloud.ibm.com/databases/databases-for-etcd/create){: external}
    2. Enter a name for your service instance, such as `px-etcd`.
    3. Select the region where you want to deploy your service instance. For optimal performance, choose the region that your cluster is in.
    4. Select the same resource group that your cluster is in.
    5. Use the following settings for the initial memory and disk allocation:
        * **Initial memory allocation:** 8GB/member (24GB total)
        * **Initial disk allocation:** 128GB/member (384GB total)
        * **Initial CPU allocation:** 3 dedicated cores/member (9 cores total)
        * **Database version:** 3.3
    6. Decide if you want to use the default {{site.data.keyword.keymanagementserviceshort}} service instance or your own.
    7. Review the pricing plan.
    8. Click **Create** to set up your service instance. The setup might take a few minutes to complete.
3. Create service credentials for your Databases for etcd service instance.

    1. In the navigation on the service details page, click **Service Credentials**.
    2. Click **New credentials**.
    3. Enter a name for your service credentials and click **Add**.

4. Retrieve your service credentials and certificate.{: #databases_credentials}
    1. From the navigation on the service details page, select **Service credentials**.
    2. Find the credentials that you want to use, and from the **Actions** column in the service credentials table, click **View credentials**.
    3. Find the `grp.authentication` section of your service credentials and note the **`username`** and **`password`**.

        Example output for username and password:
        ```sh
        "grpc": {
        "authentication": {
        "method": "direct",
        "password": "123a4567ab89cde09876vaa543a2bc2a10a123456bcd123456f0a7895aab1de",
        "username": "ibm_cloud_1abd2e3f_g12h_3bc4_1234_5a6bc7890ab"
        }
        ```
        {: screen}

    4. Find the `composed` section of your service credentials and note the etcd **`--endpoints`**. You need this information when you install Portworx.

        Example output for `--endpoints`:
        ```sh
        --endpoints=https://1ab234c5-12a1-1234-a123-123abc45cde1.123456ab78cd9ab1234a456740ab123c.databases.appdomain.cloud:32059
        ```
        {: screen}

    5. Find the `certificate` section of your service credentials and note the **`certificate_base64`**.

        Example output for `certificate`:
        ```sh
        "certificate": {
        "certificate_base64": "AB0cAB1CDEaABcCEFABCDEF1ACB3ABCD1ab2AB0cAB1CDEaABcCEFABCDEF1ACB3ABCD1ab2AB0cAB1CDEaABcCEFABCDEF1ACB3ABCD1ab2..."
        ```
        {: screen}

5. Encode your username and password to base64.
    ```sh
    echo -n "<username_or_password>" | base64
    ```
    {: pre}

6. Create a Kubernetes secret for your certificate.
    1. Create a configuration file for your secret.
        ```yaml
        apiVersion: v1
        kind: Secret
        metadata:
        name: px-etcd-certs
        namespace: kube-system
        type: Opaque
        data:
          ca.pem: <certificate_base64>
          username: <username_base64>
          password: <password_base64>
        ```
        {: codeblock}

    2. Create the secret in your cluster.
        ```sh
        oc apply -f secret.yaml
        ```
        {: pre}

7. Choose if you want to [set up encryption for your volumes with {{site.data.keyword.keymanagementservicelong_notm}}](#encrypt_volumes). If you don't want to set up {{site.data.keyword.keymanagementservicelong_notm}} encryption for your volumes, continue with [installing Portworx in your cluster](#install_portworx).



## Setting up volume encryption
{: #encrypt_volumes}

To protect your data in a Portworx volume, you can optionally encrypt your cluster's volumes with {{site.data.keyword.keymanagementservicelong_notm}} or {{site.data.keyword.hscrypto}}.
{: shortdesc}

{{site.data.keyword.keymanagementservicelong_notm}} helps you to provision encrypted keys that are secured by FIPS 140-2 Level 2 certified cloud-based hardware security modules (HSMs). You can use these keys to securely protect your data from unauthorized users. You can choose between using one encryption key to encrypt all your volumes in a cluster or using one encryption key for each volume. Portworx uses this key to encrypt data at rest and during transit when data is sent to a different worker node. For more information, see [Volume encryption](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/create-pvcs/create-encrypted-pvcs/#volume-encryption){: external}. For higher security, set up per-volume encryption.

If you don't want to use {{site.data.keyword.keymanagementservicelong_notm}} or {{site.data.keyword.hscrypto}} root keys to encrypt your volumes, you can select **Kubernetes Secret** as your Portworx secret store type during the Portworx installation. This setting gives you the option to store your own custom encryption key in a Kubernetes secret after you install Portworx. For more information, see the [Portworx documentation](https://docs.portworx.com/key-management/kubernetes-secrets/#configuring-kubernetes-secrets-with-portworx){: external}.
{: tip}

Review the following information:
- Overview of the [Portworx volume encryption workflow](#px_encryption) for per-volume encryption
- Overview of the [Portworx volume decryption workflow](#decryption) for per-volume encryption
- [Setting up per-volume encryption](#setup_encryption) for your Portworx volumes.

### Portworx per-volume encryption workflow
{: #px_encryption}

The following image illustrates the encryption workflow in Portworx when you set up per-volume encryption.
{: shortdesc}


![Encrypting Portworx volumes](images/cs_px_volume_encryption.png "Encrypting Portworx volumes"){: caption="Figure 1. Encrypting Portworx volumes" caption-side="bottom"}


1. The user creates a PVC with a Portworx storage class and requests the storage to be encrypted.
2. Portworx invokes the {{site.data.keyword.keymanagementservicelong_notm}} or {{site.data.keyword.hscrypto}} API `WrapCreateDEK` to create a passphrase by using the customer root key (CRK) that is stored in the Portworx secret.
3. The {{site.data.keyword.keymanagementservicelong_notm}} or {{site.data.keyword.hscrypto}} service instance generates a 256-bit passphrase and wraps the passphrase in the DEK. The DEK is returned to the Portworx cluster.
4. The Portworx cluster uses the passphrase to encrypt the volume.
5. The Portworx cluster stores the DEK in plain text in the Portworx etcd database, associates the volume ID with the DEK, and removes the passphrase from its memory.

### Portworx per-volume decryption workflow
{: #decryption}

The following image illustrates the decryption workflow in Portworx when you set up per-volume encryption.


![Decrypting Portworx volumes](images/cs_px_volume_decryption.png "Decrypting Portworx volumes"){: caption="Figure 2. Decrypting Portworx volumes" caption-side="bottom"}

1. Kubernetes sends a request to decrypt an encrypted volume.
2. Portworx requests the DEK for the volume from the Portworx etcd database.
3. The Portworx etcd looks up the DEK and returns the DEK to the Portworx cluster.
4. The Portworx cluster calls the {{site.data.keyword.keymanagementservicelong_notm}} or {{site.data.keyword.hscrypto}} API `UnWrapDEK` by providing the DEK and the root key (CRK) that is stored in the Portworx secret.
5. {{site.data.keyword.keymanagementservicelong_notm}} or {{site.data.keyword.hscrypto}} unwraps the DEK to extract the passphrase and returns the passphrase to the Portworx cluster.
6. The Portworx cluster uses the passphrase to decrypt the volume. After the volume is decrypted, the passphrase is removed from the Portworx cluster.  

### Enabling per-volume encryption for your Portworx volumes
{: #setup_encryption}

Follow these steps to set up encryption for your Portworx volumes.
{: shortdesc}

1. Make sure that you are [assigned the `Editor` platform access role and the `Writer` service access role](/docs/key-protect?topic=key-protect-manage-access) in {{site.data.keyword.cloud_notm}} Identity and Access Management for the KMS provider that you want to use.

2. Create a service instance of the KMS provider that you want to use. Note the name of the service instance that you created.
    * **[{{site.data.keyword.keymanagementservicelong_notm}}](/docs/key-protect?topic=key-protect-provision)**
    * **[{{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-provision)**
3. Create a root key. Note the ID of the root key that you created.
    * [Create a **{{site.data.keyword.keymanagementservicelong_notm}}** root key](/docs/key-protect?topic=key-protect-create-root-keys).
    * [Create a **{{site.data.keyword.hscrypto}}** root key](/docs/hs-crypto?topic=hs-crypto-create-root-keys).
4. Retrieve the **GUID** of the service instance that you created.
    ```sh
    ibmcloud resource service-instance <service_instance_name_or_ID>
    ```
    {: pre}

    Example output

    ```sh
    Retrieving service instance <name> in resource group default under account IBM as <user>...
    OK

    Name:                  <name>   
    ID:                    crn:v1:bluemix:public:kms:us-south:a/1ab123ab3c456789cde1f1234ab1cd123:a1a2b345-1d12-12ab-a12a-1abc2d3e1234::   
    GUID:                  a1a2b345-1d12-12ab-a12a-1abc2d3e1234
    ...
    ```
    {: screen}

5. [Create a service ID for your account](/docs/account?topic=account-serviceids#serviceids).  

6. [Assign your service ID permissions](/docs/account?topic=account-serviceids) to your **{{site.data.keyword.keymanagementservicelong_notm}}** or **{{site.data.keyword.hscrypto}}** service instance.

7. [Create an API key for your service ID](/docs/account?topic=account-serviceidapikeys#serviceidapikeys). This API key is used by Portworx to access the **{{site.data.keyword.keymanagementservicelong_notm}}** or **{{site.data.keyword.hscrypto}}** API.

8. If you are using {{site.data.keyword.keymanagementservicelong_notm}}, retrieve the API endpoint. If you are using {{site.data.keyword.hscrypto}}, retrieve the Key Management endpoint URL:

    * **{{site.data.keyword.keymanagementservicelong_notm}}**: [Retrieve the region](/docs/key-protect?topic=key-protect-regions#regions) where you created your service instance. Make sure that you note your API endpoint in the correct format. Example: `https://us-south.kms.cloud.ibm.com`.
    * **{{site.data.keyword.hscrypto}}**: [Retrieve the Key Management public endpoint URL](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). Make sure that you note your endpoint in the correct format. Example: `https://api.us-south.hs-crypto.cloud.ibm.com:<port>`. For more information, see the [{{site.data.keyword.hscrypto}} API documentation](https://cloud.ibm.com/apidocs/hs-crypto#getinstance).

    If you enter an incorrect endpoint for the KMS that you are using, Portworx gives an error similar to the following: `kp.Error: correlation_id='673bb68a-be17-4720-9ae1-85baf109924e', msg='Unauthorized: The user does not have access to the specified resource'"`. Ensure that you retrieve the correct endpoint for the KMS that you use.
    {: note}


### Creating a secret to store the KMS credentials
{: #px_create_km_secret}

**Before you begin:** [Set up encryption](#setup_encryption)

1. Encode the credentials that you retrieved in the previous section to base64 and note all the base64 encoded values. Repeat this command for each parameter to retrieve the base64 encoded value.
    ```sh
    echo -n "<value>" | base64
    ```
    {: pre}

2. Create a project in your cluster called `portworx`.
    ```sh
    oc create ns portworx
    ```
    {: pre}

3. Create a Kubernetes secret named `px-ibm` in the `portworx` project of your cluster to store your {{site.data.keyword.keymanagementservicelong_notm}} information.
    1. Create a configuration file for your Kubernetes secret with the following content.
        ```yaml
        apiVersion: v1
        kind: Secret
        metadata:
          name: px-ibm
          namespace: portworx
        type: Opaque
        data:
          IBM_SERVICE_API_KEY: <base64_apikey>
          IBM_INSTANCE_ID: <base64_guid>
          IBM_CUSTOMER_ROOT_KEY: <base64_rootkey>
          IBM_BASE_URL: <base64_endpoint>
        ```
        {: codeblock}

        `metadata.name`
        :   Enter `px-ibm` as the name for your Kubernetes secret. If you use a different name, Portworx does not recognize the secret during installation.
        
        `data.IBM_SERVICE_API_KEY`
        :   Enter the base64 encoded {{site.data.keyword.keymanagementservicelong_notm}} or {{site.data.keyword.hscrypto}} API key that you retrieved earlier.
        
        `data.IBM_INSTANCE_ID`
        :   Enter the base64 encoded service instance GUID that you retrieved earlier.
        
        `data.IBM_CUSTOMER_ROOT_KEY`
        :   Enter the base64 encoded root key that you retrieved earlier.
        
        `data.IBM_BASE_URL`
        :   {{site.data.keyword.keymanagementservicelong_notm}}: Enter the base64 encoded API endpoint of your service instance.
        :   {{site.data.keyword.hscrypto}}: Enter the base64 encoded Key Management public endpoint.

    2. Create the secret in the `portworx` project of your cluster.
        ```sh
        oc apply -f secret.yaml
        ```
        {: pre}

    3. Verify that the secret is created successfully.
        ```sh
        oc get secrets -n portworx
        ```
        {: pre}

4. If you set up encryption before your installed Portworx, you can now [install Portworx in your cluster](#add_portworx_storage). To add encryption to your cluster after you installed Portworx, update the Portworx DaemonSet to add `"-secret_type"` and `"ibm-kp"` as additional arguments to the Portworx container definition.
    1. Update the Portworx DaemonSet.
        ```sh
        oc edit daemonset portworx -n kube-system
        ```
        {: pre}

        Example updated DaemonSet
        ```sh
        containers:
        - args:
        - -c
        - testclusterid
        - -s
        - /dev/sdb
        - -x
        - kubernetes
        - -secret_type
        - ibm-kp
        name: portworx
        ```
        {: codeblock}

        After you edit the DaemonSet, the Portworx pods are restarted and automatically update the `config.json` file on the worker node to reflect that change.

    2. List the Portworx pods in your `kube-system` project.
        ```sh
        oc get pods -n kube-system | grep portworx
        ```
        {: pre}

    3. Log in to one of your Portworx pods.
        ```sh
        oc exec -it <pod_name> -it -n kube-system
        ```
        {: pre}

    4. Navigate in to the `pwx` directory.
        ```sh
        cd etc/pwx
        ```
        {: pre}

    5. Review the `config.json` file to verify that `"secret_type": "ibm-kp"` is added to the **secret** section of your CLI output.
        ```sh
        cat config.json
        ```
        {: pre}

        Example output
        ```sh
        {
        "alertingurl": "",
        "clusterid": "px-kp-test",
        "dataiface": "",
        "kvdb": [
          "etcd:https://portal-ssl748-34.bmix-dal-yp-12a2312v5-123a-44ac-b8f7-5d8ce1d123456.123456789.composedb.com:56963",
          "etcd:https://portal-ssl735-35.bmix-dal-yp-12a2312v5-123a-44ac-b8f7-5d8ce1d123456.12345678.composedb.com:56963"
        ],
        "mgtiface": "",
        "password": "ABCDEFGHIJK",
        "scheduler": "kubernetes",
        "secret": {
            "cluster_secret_key": "",
            "secret_type": "ibm-kp"
        },
        "storage": {
            "devices": [
          "/dev/sdc1"
            ],
            "journal_dev": "",
            "max_storage_nodes_per_zone": 0,
            "system_metadata_dev": ""
        },
        "username": "root",
        "version": "1.0"
        }
        ```
        {: screen}

    6. Exit the pod.

Check out how to [encrypt the secrets in your cluster](/docs/openshift?topic=openshift-encryption#keyprotect), including the secret where you stored your {{site.data.keyword.keymanagementserviceshort}} CRK for your Portworx storage cluster.
{: tip}



## Installing Portworx in your cluster
{: #install_portworx}

Provision a Portworx service instance from the {{site.data.keyword.cloud_notm}} catalog. After you create the service instance, the latest Portworx enterprise edition (`px-enterprise`) is installed on your cluster by using Helm. In addition, [Stork](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/stork/){: external} is also installed on your {{site.data.keyword.openshiftlong_notm}} cluster. Stork is the Portworx storage scheduler. With Stork, you can co-locate pods with their data and create and restore snapshots of Portworx volumes.
{: shortdesc}

Looking for instructions about how to update or remove Portworx? See [Updating Portworx](#update_portworx) and [Removing Portworx](#remove_portworx).
{: tip}

Before you begin:
- Make sure that you have the right [permissions](/docs/openshift?topic=openshift-clusters#cluster_prepare) to create {{site.data.keyword.openshiftlong_notm}} clusters.

- [Create or use an existing cluster](/docs/containers?topic=containers-clusters).

- If you want to use non-SDS worker nodes in a classic cluster, or VPC worker nodes for your Portworx storage layer, [add a block storage device to your worker node](#create_block_storage).

- Choose if you want to [use the internal Portworx key-value database (KVDB)](#portworx-kvdb) or [create a Databases for etcd service instance](#databases-for-etcd) to store the Portworx configuration and metadata.

- Decide whether you want to encrypt your Portworx volumes. To encrypt your volumes, you must [set up an {{site.data.keyword.keymanagementservicelong_notm}} or a {{site.data.keyword.hscrypto}} instance and store your service information in a Kubernetes secret](#encrypt_volumes).

- Make sure that you [copied the image pull secrets from the `default` to the `kube-system` project](/docs/openshift?topic=openshift-registry#copy_imagePullSecret) so that you can pull images from {{site.data.keyword.registryshort}}. Make sure that you [add the image pull secrets to the Kubernetes service account](/docs/openshift?topic=openshift-registry#store_imagePullSecret) of the `kube-system` project.

- Decide if you want to include your cluster in a Portworx disaster recovery configuration. For more information, see [Setting up disaster recovery with Portworx](#px-dr).

- If you attached a separate device for the Portworx journal, make sure that you retrieve the device path by running `lsblk` while logged into your worker node.

- If you attached a separate devices for the Portworx KVDB, make sure that you retrieve the device path by running `lsblk` while logged into your worker node.

- [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To install Portworx:

1. Open the Portworx service from the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog/services/portworx-enterprise){: external} and complete the fields as follows:

    1. Select the region where your {{site.data.keyword.openshiftlong_notm}} cluster is located.
    
    2.  Review the Portworx pricing information.
    
    3. Enter a name for your Portworx service instance.
    
    4. Select the resource group that your cluster is in.
    
    5. In the **Tag** field, enter the name of the cluster where you want to install Portworx. After you create the Portworx service instance, you can't see the cluster that you installed Portworx into. To find the cluster more easily later, make sure that you enter the cluster name and any additional information as tags.
    
    6. Enter an {{site.data.keyword.cloud_notm}} API key to retrieve the list of clusters that you have access to. If you don't have an API key, see [Managing user API keys](/docs/account?topic=account-userapikey). After you enter the API key, the **Kubernetes or OpenShift cluster name** field appears at the bottom of the page.
    
    7. Enter a unique name for the Portworx cluster within your {{site.data.keyword.openshiftlong_notm}} cluster.
    8. From the **Portworx metadata key-value store** drop down, choose the type of key-value store that you want to use to store Portworx metadata. Select **Portworx KVDB** to automatically create a key-value store during the Portworx installation, or select **Databases for etcd** if you want to use an existing Databases for etcd instance. If you choose **Databases for etcd**, the **Etcd API endpoints** and **Etcd secret name** fields appear.
    9. **Required for Databases for etcd only**: Enter the information of your Databases for etcd service instance.
        1. [Retrieve the etcd endpoint, and the name of the Kubernetes secret](#databases_credentials) that you created for your Databases for etcd service instance.
        2. In the **Etcd API endpoints** field, enter the API endpoint of your Databases for etcd service instance that you retrieved earlier. Make sure to enter the endpoint in the format `etcd:<etcd_endpoint1>;etcd:<etcd_endpoint2>`. If you have more than one endpoint, include all endpoints and separate them with a semicolon (`;`).
        3. In the **Etcd secret name** field, enter the name of the Kubernetes secret that you created in your cluster to store the Databases for etcd service credentials.
    10. From the **Kubernetes or OpenShift cluster name** drop down list, select the cluster where you want to install Portworx. If your cluster is not listed, make sure that you select the correct {{site.data.keyword.cloud_notm}} region. If the region is correct, verify that you have the correct [permissions](/docs/openshift?topic=openshift-clusters#cluster_prepare) to view and work with your cluster. Make sure that you select a cluster that meets the [minimum hardware requirements for Portworx](https://docs.portworx.com/start-here-installation/){: external}.
    11. **Optional**: From the **Portworx secret store type** drop down list, choose the secret store type that you want to use to store the volume encryption key.
        - **Kubernetes Secret**: Choose this option if you want to store your own custom key to encrypt your volumes in a Kubernetes Secret in your cluster. The secret must not be present before you install Portworx. You can create the secret after you install Portworx. For more information, see the [Portworx documentation](https://docs.portworx.com/key-management/kubernetes-secrets/#configuring-kubernetes-secrets-with-portworx){: external}.
        - **{{site.data.keyword.keymanagementservicelong_notm}}**: Choose this option if you want to use root keys in {{site.data.keyword.keymanagementservicelong_notm}} to encrypt your volumes. Make sure that you follow the [instructions](#setup_encryption) to create your {{site.data.keyword.keymanagementservicelong_notm}} service instance, and to store the credentials for how to access your service instance in a Kubernetes secret in the `portworx` project before you install Portworx.
    12. **Optional**: If you want to set up a journal device or KVDB devices, enter the device details in the **Advanced Options** field. Choose from the following options for journal devices:
        
        - Enter `j;auto` to allow Portworx to automatically create a 3 GB partition on one of your block storage devices to use for the journal.
        - Enter `j;</device/path>` to use a specific device for the journal. For example, enter `j;/dev/vde` to use the disk located at `/dev/vde`. To find the path of the device that you want to use for the journal, log in to a worker node and run `lsblk`.
        - Enter `kvdb_dev;<device path>` to specify the device where you want to store internal KVDB data. For example, `kvdb_dev;/dev/vdd`. To find the path of the device that you want to use, log in to a worker node and run `lsblk`. To use a specific device for KVDB data, you must have an available storage device of 3GB or on at least 3 worker nodes. The devices must also and on the same path on each worker node. For example: `/dev/vdd`.

1. Click **Create** to start the Portworx installation in your cluster. This process might take a few minutes to complete. The service details page opens with instructions for how to verify your Portworx installation, create a persistent volume claim (PVC), and mount the PVC to an app.
1. From the [{{site.data.keyword.cloud_notm}} resource list](https://cloud.ibm.com/resources){: external}, find the Portworx service that you created.
1. Review the **Status** column to see if the installation succeeded or failed. The status might take a few minutes to update.
1. If the **Status** changes to `Provision failure`, follow the [instructions](/docs/containers?topic=containers-debug-portworx) to start troubleshooting why your installation failed.
1. If the **Status** changes to `Provisioned`, verify that your Portworx installation completed successfully and that all your local disks were recognized and added to the Portworx storage layer.
    1. List the Portworx pods in the `kube-system` project. The installation is successful when you see one or more `portworx`, `stork`, and `stork-scheduler` pods. The number of pods equals the number of worker nodes that are in your Portworx cluster. All pods must be in a `Running` state.
        ```sh
        oc get pods -n kube-system | grep 'portworx\|stork'
        ```
        {: pre}

        Example output
        ```sh
        portworx-594rw                          1/1       Running     0          20h
        portworx-rn6wk                          1/1       Running     0          20h
        portworx-rx9vf                          1/1       Running     0          20h
        stork-6b99cf5579-5q6x4                  1/1       Running     0          20h
        stork-6b99cf5579-slqlr                  1/1       Running     0          20h
        stork-6b99cf5579-vz9j4                  1/1       Running     0          20h
        stork-scheduler-7dd8799cc-bl75b         1/1       Running     0          20h
        stork-scheduler-7dd8799cc-j4rc9         1/1       Running     0          20h
        stork-scheduler-7dd8799cc-knjwt         1/1       Running     0          20h
        ```
        {: screen}

    2. Log in to one of your `portworx` pods and list the status of your Portworx cluster.
        ```sh
        oc exec <portworx_pod> -it -n kube-system -- /opt/pwx/bin/pxctl status
        ```
        {: pre}

        Example output
        ```sh
        Status: PX is operational
        License: Trial (expires in 30 days)
        Node ID: 10.176.48.67
        IP: 10.176.48.67
        Local Storage Pool: 1 pool
        POOL    IO_PRIORITY    RAID_LEVEL    USABLE    USED    STATUS    ZONE    REGION
          0    LOW        raid0        20 GiB    3.0 GiB    Online    dal10    us-south
        Local Storage Devices: 1 device
        Device    Path                        Media Type        Size        Last-Scan
            0:1    /dev/mapper/3600a09803830445455244c4a38754c66    STORAGE_MEDIUM_MAGNETIC    20 GiB        17 Sep 18 20:36 UTC
                total                            -            20 GiB
        Cluster Summary
        Cluster ID: mycluster
            Cluster UUID: a0d287ba-be82-4aac-b81c-7e22ac49faf5
        Scheduler: kubernetes
        Nodes: 2 node(s) with storage (2 online), 1 node(s) without storage (1 online)
          IP        ID        StorageNode    Used    Capacity    Status    StorageStatus    Version        Kernel            OS
          10.184.58.11    10.184.58.11    Yes        3.0 GiB    20 GiB        Online    Up        1.5.0.0-bc1c580    4.4.0-133-generic    Ubuntu 18.04.5 LTS
          10.176.48.67    10.176.48.67    Yes        3.0 GiB    20 GiB        Online    Up (This node)    1.5.0.0-bc1c580    4.4.0-133-generic    Ubuntu 18.04.5 LTS
          10.176.48.83    10.176.48.83    No        0 B    0 B        Online    No Storage    1.5.0.0-bc1c580    4.4.0-133-generic    Ubuntu 18.04.5 LTS
        Global Storage Pool
          Total Used        :  6.0 GiB
          Total Capacity    :  40 GiB
        ```
        {: screen}

    3. Verify that all worker nodes that you wanted to include in your Portworx storage layer are included by reviewing the **StorageNode** column in the **Cluster Summary** section of your CLI output. Worker nodes that are in the storage layer are displayed with `Yes` in the **StorageNode** column.

        Because Portworx runs as a DaemonSet in your cluster, existing worker nodes are automatically inspected for raw block storage and added to the Portworx data layer when you deploy Portworx. If you add worker nodes to your cluster and add raw block storage to those workers, restart the Portworx pods on the new worker nodes so that your storage volumes are detected by the DaemonSet.
        {: note}

    4. Verify that each storage node is listed with the correct amount of raw block storage by reviewing the **Capacity** column in the **Cluster Summary** section of your CLI output.

    5. Review the Portworx I/O classification that was assigned to the disks that are part of the Portworx cluster. During the setup of your Portworx cluster, every disk is inspected to determine the performance profile of the device. The profile classification depends on how fast the network is that your worker node is connected to and the type of storage device that you have. Disks of SDS worker nodes are classified as `high`. If you manually attach disks to a virtual worker node, then these disks are classified as `low` due to the lower network speed that comes with virtual worker nodes.
        ```sh
        oc exec -it <portworx_pod> -n kube-system -- /opt/pwx/bin/pxctl cluster provision-status
        ```
        {: pre}

        Example output
        
        ```sh
        NODE        NODE STATUS    POOL    POOL STATUS    IO_PRIORITY    SIZE    AVAILABLE    USED    PROVISIONED    RESERVEFACTOR    ZONE    REGION        RACK
        10.184.58.11    Up        0    Online        LOW        20 GiB    17 GiB        3.0 GiB    0 B        0        dal12    us-south    default
        10.176.48.67    Up        0    Online        LOW        20 GiB    17 GiB        3.0 GiB    0 B        0        dal10    us-south    default
        10.176.48.83    Up        0    Online        HIGH        3.5 TiB    3.5 TiB        10 GiB    0 B        0        dal10    us-south    default
        ```
        {: screen}

### Updating Portworx in your cluster
{: #update_portworx}

You can upgrade Portworx to the latest version.
{: shortdesc}

1. [Follow the instructions](/docs/openshift?topic=openshift-helm#install_v3) to install the Helm version 3 client on your local machine.

2. Update your Helm repos.
    ```sh
    helm repo update
    ```
    {: pre}

3. Find release name of your Portworx Helm chart.
    ```sh
    helm list -A | grep portworx
    ```
    {: pre}

    Example output
    ```sh
    <release_name>      default      1    2020-06-10 16:05:31.86058777 +0000 UTC    deployed    portworx-1.0.18         2.5.1    
    ```
    {: screen}

4. Update your Portworx release with the latest version of the Helm chart.
    ```sh
    helm upgrade <release_name> ibm-community/portworx/
    ```
    {: pre}



## Creating a Portworx volume
{: #add_portworx_storage}

Start creating Portworx volumes by using [Kubernetes dynamic provisioning](/docs/openshift?topic=openshift-kube_concepts#dynamic_provisioning).
{: shortdesc}

1. List available storage classes in your cluster and check whether you can use an existing Portworx storage class that was set up during the Portworx installation. The pre-defined storage classes are optimized for database usage and to share data across pods.
    ```sh
    oc get storageclasses | grep portworx
    ```
    {: pre}

    To view the details of a storage class, run `oc describe storageclass <storageclass_name>`.
    {: tip}

2. If you don't want to use an existing storage class, create a customized storage class. For a full list of supported options that you can specify in your storage class, see [Using Dynamic Provisioning](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/create-pvcs/dynamic-provisioning/#using-dynamic-provisioning){: external}.
    1. Create a configuration file for your storage class.
        ```yaml
        kind: StorageClass
        apiVersion: storage.k8s.io/v1
        metadata:
        name: <storageclass_name>
        provisioner: kubernetes.io/portworx-volume
        parameters:
          repl: "<replication_factor>"
          secure: "<true_or_false>"
          priority_io: "<io_priority>"
          shared: "<true_or_false>"
        ```
        {: codeblock}

        `metadata.name`
        :   Enter a name for your storage class.
        
        `parameters.repl`
        :   Enter the number of replicas for your data that you want to store across different worker nodes. Allowed numbers are `1`,`2`, or `3`. For example, if you enter `3`, then your data is replicated across three different worker nodes in your Portworx cluster. To store your data highly available, use a multizone cluster and replicate your data across three worker nodes in different zones. <strong>Note: </strong>You must have enough worker nodes to fulfill your replication requirement. For example, if you have two worker nodes, but you specify three replicas, then the creation of the PVC with this storage class fails.
        
        `parameters.secure`
        :   Specify whether you want to encrypt the data in your volume with {{site.data.keyword.keymanagementservicelong_notm}}. Choose between the following options.
            - `true`: Enter `true` to enable encryption for your Portworx volumes. To encrypt volumes, you must have an {{site.data.keyword.keymanagementservicelong_notm}} service instance and a Kubernetes secret that holds your customer root key. For more information about how to set up encryption for Portworx volumes, see [Encrypting your Portworx volumes](#encrypt_volumes). 
            - `false`: When you enter `false`, your Portworx volumes are not encrypted. If you don't specify this option, your Portworx volumes are not encrypted by default. You can choose to enable volume encryption in your PVC, even if you disabled encryption in your storage class. The setting that you make in the PVC take precedence over the settings in the storage class.

        `parameters.priority_io`
        :   Enter the Portworx I/O priority that you want to request for your data. Available options are `high`, `medium`, and `low`. During the setup of your Portworx cluster, every disk is inspected to determine the performance profile of the device. The profile classification depends on the network bandwidth of your worker node and the type of storage device. Disks of SDS worker nodes are classified as `high`. If you manually attach disks to a virtual worker node, then these disks are classified as `low` due to the lower network speed that comes with virtual worker nodes. <br> When you create a PVC with a storage class, the number of replicas that you specify in `parameters/repl` overrides the I/O priority. For example, when you specify three replicas that you want to store on high-speed disks, but you have only one worker node with a high-speed disk in your cluster, then your PVC creation still succeeds. Your data is replicated across both high and low speed disks.
        
        `parameters.shared`
        :   Define whether you want to allow multiple pods to access the same volume. Choose between the following options:
            - True: If you set this option to `true`, then you can access the same volume by multiple pods that are distributed across worker nodes in different zones.
            - False: If you set this option to `false`, you can access the volume from multiple pods only if the pods are deployed onto the worker node that attaches the physical disk that backs the volume. If your pod is deployed onto a different worker node, the pod can't access the volume.

    2. Create the storage class.
        ```sh
        oc apply -f storageclass.yaml
        ```
        {: pre}

    3. Verify that the storage class is created.
        ```sh
        oc get storageclasses
        ```
        {: pre}

3. Create a persistent volume claim (PVC).
    1. Create a configuration file for your PVC.
        ```yaml
        kind: PersistentVolumeClaim
        apiVersion: v1
        metadata:
        name: mypvc
        spec:
          accessModes:
            - <access_mode>
          resources:
            requests:
              storage: <size>
          storageClassName: portworx-shared-sc
        ```
        {: codeblock}

        `metadata.name`
        :   Enter a name for your PVC, such as `mypvc`.
        
        `spec.accessModes`
        :   Enter the [Kubernetes access mode](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes){: external} that you want to use.
        
        `resources.requests.storage`
        :   Enter the amount of storage in gigabytes that you want to assign from your Portworx cluster. For example, to assign 2 gigabytes from your Portworx cluster, enter `2Gi`. The amount of storage that you can specify is limited by the amount of storage that is available in your Portworx cluster. If you specified a replication factor in your storage class higher than 1, then the amount of storage that you specify in your PVC is reserved on multiple worker nodes.
        
        `spec.storageClassName`
        :   Enter the name of the storage class that you chose or created earlier and that you want to use to provision your PV. The example YAML file uses the `portworx-shared-sc` storage class.

    2. Create your PVC.
        ```sh
        oc apply -f pvc.yaml
        ```
        {: pre}

    3. Verify that your PVC is created and bound to a persistent volume (PV). This process might take a few minutes.
        ```sh
        oc get pvc
        ```
        {: pre}

        

## Mounting the volume to your app
{: #mount_pvc}

To access the storage from your app, you must mount the PVC to your app.
{: shortdesc}

1. Create a configuration file for a deployment that mounts the PVC.

    For tips on how to deploy a stateful set with Portworx, see [StatefulSets](https://portworx.com/blog/cassandra-openshift-run-ha-cassandra-red-hat-openshift/){: external}. The Portworx documentation also includes examples for how to deploy [Cassandra](https://portworx.com/blog/cassandra-openshift-run-ha-cassandra-red-hat-openshift/){: external}, [Kafka](https://docs.portworx.com/portworx-install-with-kubernetes/application-install-with-kubernetes/kafka-with-zookeeper/){: external}, [ElasticSearch with Kibana](https://docs.portworx.com/portworx-install-with-kubernetes/application-install-with-kubernetes/elastic-search-and-kibana/){: external}, and [WordPress with MySQL](https://docs.portworx.com/portworx-install-with-kubernetes/application-install-with-kubernetes/wordpress/){: external}.
    {: tip}

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: <deployment_name>
      labels:
        app: <deployment_label>
    spec:
      selector:
        matchLabels:
          app: <app_name>
      template:
        metadata:
          labels:
            app: <app_name>
        spec:
          schedulerName: stork
          containers:
          - image: <image_name>
            name: <container_name>
          securityContext:
              fsGroup: <group_ID>
            volumeMounts:
            - name: <volume_name>
              mountPath: /<file_path>
          volumes:
          - name: <volume_name>
            persistentVolumeClaim:
              claimName: <pvc_name>
    ```
    {: codeblock}

    `metadata.labels.app`
    :   A label for the deployment.
    
    `spec.selector.matchLabels.app` and `spec.template.metadata.labels.app`
    :   A label for your app.
    
    `template.metadata.labels.app`
    :   A label for the deployment.
    
    `spec.schedulerName`</td>
    :   Use [Stork](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/stork/){: external} as the scheduler for your Portworx cluster. With Stork, you can co-locate pods with their data, provides seamless migration of pods in case of storage errors and makes it easier to create and restore snapshots of Portworx volumes.
    
    `spec.containers.image`
    :   The name of the image that you want to use. To list available images in your {{site.data.keyword.registrylong_notm}} account, run `ibmcloud cr image-list`.
    
    `spec.containers.name`
    :   The name of the container that you want to deploy to your cluster.
    
    `spec.containers.securityContext.fsGroup`
    :   Optional: To access your storage with a non-root user, specify the [security context](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/){: external} for your pod and define the set of users that you want to grant access in the `fsGroup` section on your deployment YAML. For more information, see [Accessing Portworx volumes with a non-root user](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/create-pvcs/access-via-non-root-users/){: external}.
    
    `spec.containers.volumeMounts.mountPath`
    :   The absolute path of the directory to where the volume is mounted inside the container. If you want to share a volume between different apps, you can specify [volume sub paths](https://kubernetes.io/docs/concepts/storage/volumes/#using-subpath){: external} for each of your apps.
    
    `spec.containers.volumeMounts.name`
    :   The name of the volume to mount to your pod.
    
    `volumes.name`
    :   The name of the volume to mount to your pod. Typically this name is the same as `volumeMounts/name`.
    
    `volumes.persistentVolumeClaim.claimName`
    :   The name of the PVC that binds the PV that you want to use.

2. Create your deployment.
    ```sh
    oc apply -f deployment.yaml
    ```
    {: pre}

3. Verify that the PV is successfully mounted to your app.
    ```sh
    oc describe deployment <deployment_name>
    ```
    {: pre}

    The mount point is in the **Volume Mounts** field and the volume is in the **Volumes** field.
    ```sh
    Volume Mounts:
            /var/run/secrets/kubernetes.io/serviceaccount from default-token-tqp61 (ro)
            /volumemount from myvol (rw)
    ...
    Volumes:
        myvol:
        Type:    PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
        ClaimName:    mypvc
        ReadOnly:    false
    ```
    {: screen}

4. Verify that you can write data to your Portworx cluster.
    1. Log in to the pod that mounts your PV.
        ```sh
        oc exec <pod_name> -it bash
        ```
        {: pre}

    2. Navigate to your volume mount path that you defined in your app deployment.
    3. Create a text file.
        ```sh
        echo "This is a test" > test.txt
        ```
        {: pre}

    4. Read the file that you created.
        ```sh
        cat test.txt
        ```
        {: pre}

        



## VPC: Updating worker nodes with Portworx volumes
{: #portworx_vpc_up}

When you update a worker node in a VPC cluster, the worker node is removed from your cluster and replaced with a new worker node. If Portworx volumes are attached to the worker node that you replaced, you must attach the volumes to the new worker node.
{: shortdesc}

Update only one worker node at a time. When the worker node update is complete, attach your {{site.data.keyword.block_storage_is_short}} and restart the Portworx pod.
{: important}

**Supported infrastructure provider**: ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

1. [Enter maintenance mode on the worker nodes that you want to update](https://docs.portworx.com/portworx-install-with-kubernetes/operate-and-maintain-on-kubernetes/troubleshooting/enter-maintenance-mode/){: external}.

2. [Update your VPC worker nodes](/docs/containers?topic=containers-update#vpc_worker_node).

3. [Attach raw {{site.data.keyword.block_storage_is_short}} to your worker nodes](/docs/openshift?topic=openshift-utilities#vpc_api_attach).

4. Verify that your storage is attached by running the following command.
    ```sh
    oc get pv -o yaml | grep "attachstatus"
    ```
    {: pre}

5. Restart the Portworx pod on the new worker node.
    ```sh
    oc delete pod <portworx_pod> -n <portworx_namespace>
    ```
    {: pre}

6. Exit maintenance mode
    ```sh
    pxctl service maintenance --exit
    ```
    {: pre}

7. [Mount the volume to your app](/docs/openshift?topic=openshift-portworx#mount_pvc).



## Backing up and restoring apps and data with PX-Backup
{: #px-backup}

PX-Backup is a Portworx proprietary backup solution that is compatible with any {{site.data.keyword.openshiftlong_notm}} cluster. You can use PX-Backup to back up and restore {{site.data.keyword.openshiftlong_notm}} resources, apps and data across multiple clusters. For more information on PX-Backup, see [Understanding PX-Backup](https://backup.docs.portworx.com/understand/){: external}.
{: shortdesc}

To back up the data in your persistent volumes, you must have a storage class that supports snapshots in your cluster. Clusters with Portworx Enterprise have storage classes available that support snapshots by default. However, for clusters that don't have Portworx Enterprise, you must have a storage classes with snapshot support to back up your persistent volume data. The {{site.data.keyword.block_storage_is_short}} driver, {{site.data.keyword.blockstorageshort}} driver, and the {{site.data.keyword.filestorage_short}} driver don't have storage classes that support snapshots. If you have workloads that use these drivers, you can use PX-Backup to back up your apps, but not the data in the persistent volumes. For more information see [Backing up and restoring cluster data with PX-Backup](#px-backup-and-restore).
{: important}

### Installing PX-Backup on a {{site.data.keyword.openshiftlong_notm}} cluster
{: #px-backup-install}

Install PX-Backup on a {{site.data.keyword.openshiftlong_notm}} cluster in your {{site.data.keyword.cloud_notm}} account. After you install PX-backup on one cluster in your account, you can use it to back up or restore data and apps for any cluster in that same account.
{: shortdesc}

Before you begin:
- Make sure that your cluster meets the [minimum Portworx requirements](https://docs.portworx.com/start-here-installation/){: external}. 
- [Log in to your cluster](/docs/openshift?topic=openshift-access_cluster).
- Provision and attach 320Gi of block storage to your cluster. See [Storing data on classic {{site.data.keyword.cloud_notm}} Block Storage](/docs/containers?topic=containers-block_storage) or [Storing data on Block Storage for VPC](/docs/containers?topic=containers-vpc-block).


If you are installing PX-Backup in a newly-provisioned cluster, [you must log in to it at least once](/docs/openshift?topic=openshift-access_cluster) before beginning the installation.
{: important}


1. Open the PX-Backup service from the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog/services/px-backup-for-kubernetes){: external}.
2. Select the same location where the  cluster you want to install PX-Backup on is located. You can find the location of your cluster from the {{site.data.keyword.openshiftlong_notm}} dashboard.
3. Enter the name for your PX-Backup service in the **Service name** field.
4. Select the resource group where you want to create the PX-Backup service.
5. In the **Tag** field, enter the name of the cluster where you want to install PX-Backup. After you complete the installation, you can't see the name of the cluster where you installed PX-Backup. To find the cluster more easily later, make sure that you enter the cluster name and any additional information as tags.
6. Enter your {{site.data.keyword.cloud_notm}} API key. After you enter the API key, the **Kubernetes or OpenShift cluster name** field appears. If you don't have an {{site.data.keyword.cloud_notm}} API key, see [Creating an API key](/docs/account?topic=account-userapikey#create_user_key) to create one.
7. In the **Kubernetes or OpenShift cluster name** field, select the cluster where you want to install PX-Backup.
8. Enter the name of the {{site.data.keyword.openshiftshort}} project where you want to install your PX-Backup service components. Do not use the `kube-system` or `default` namespace. If the {{site.data.keyword.openshiftshort}} project that you enter does not already exist in your cluster, it is automatically created during the installation.
9. Select an existing storage class in your cluster to provision persistent volumes for the PX-Backup service. The service uses this storage to store service metadata and is not used to back up your apps and data. [Your apps and data are backed up to an {{site.data.keyword.cos_full_notm}} service instance](#px-backup-storage).
10. Click **Create** to begin the PX-Backup installation. The installation may take a few minutes to complete.
11. [Verify that your PX-Backup service is installed corrrectly](#px-backup-verify).


### Verifying your PX-Backup installation
{: #px-backup-verify}

Verify that PX-Backup is correctly installed on your cluster.
{: shortdesc}


From the console

1. From the {{site.data.keyword.cloud_notm}} [Resource list](https://cloud.ibm.com/resources){: external}, find the PX-Backup service that you created.
2. Review the **Status** column to see if the installation succeeded or failed. The status might take a few minutes to update.
3. If the status changes to **Active**, verify that the PX-Backup pods, services and jobs are running in your cluster.
    1. From the {{site.data.keyword.cloud_notm}} [Resource list](https://cloud.ibm.com/resources){: external}, select the cluster where you installed PX-Backup.
    2. Open the {{site.data.keyword.openshiftshort}} web console.
    10. Click on **Projects**.
    11. Select the namespace where you installed the PX-Backup service components.
    12. In the **Inventory** section, select the option to display your pods.
    13. In the **Pods** table, verify that the status of each pod is **Running**.
    14. Click on **Networking>Routes**.
    15. Find the **px-backup-ui** route and verify that a URL is listed in the **Location** column.
    16. Click **Workloads>Jobs**.
    17. Verify that the **pxcentral-post-install-hook** job is complete.

From the CLI

1. From the {{site.data.keyword.cloud_notm}} [Resource list](https://cloud.ibm.com/resources){: external}, find the PX-Backup service you created.
2. Review the **Status** column to see if the installation succeeded or failed. The status might take a few minutes to update.
3. If the status changes to **Active**, verify that the PX-Backup pods are running in your cluster.
    1. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
    2. Run the command to verify that the installation has completed.
        ```sh
        oc get po -n <px_backup_namespace> -ljob-name=pxcentral-post-install-hook  -o wide | awk '{print $1   $3}' | grep -iv error
        ```
        {: pre}

        Example output
        ```sh
        NAMESTATUS
        pxcentral-post-install-hook-5b86qCompleted
        ```
        {: screen}


### Logging in to the PX-Backup console
{: #px-backup-ui}

Access the PX-Backup console through the URL supplied in the {{site.data.keyword.openshiftlong_notm}} dashboard for the cluster where you installed the service.
{: shortdesc}

For VPC clusters

1. From the {{site.data.keyword.cloud_notm}} [Resource list](https://cloud.ibm.com/resources){: external}, select the cluster where you installed PX-Backup.
2. Open the {{site.data.keyword.openshiftshort}} web console .
5. Click on **Networking>Routes**.
6. Find the **px-backup-ui** route and click on the URL that is listed in the **Location** column to open the PX-Backup console.
7. Log in to the PX-Backup console. If you are the first user to access the console, you must log in in with the username `admin` and the password `admin`. You are redirected to a registration page to set a unique username and password. Subsequent users must register a new account to access the console.


For public classic clusters

1. From the {{site.data.keyword.cloud_notm}} [Resource list](https://cloud.ibm.com/resources){: external}, select the cluster where you installed PX-Backup.
2. Open the {{site.data.keyword.openshiftshort}} web console .
6. Click on **Networking>Routes**.
7. Find the **px-backup-ui** route and note the IP address and node port listed in the **Locations** column.
8. Copy and paste the IP address and node port into your web browser to open the PX-Backup console.
9. Log in to the PX-Backup console. If you are the first user to access the console, you must log in in with the username `admin` and the password `admin`. You are redirected to a registration page to set a unique username and password. Subsequent users must register a new account to access the console.


For private classic clusters, [expose the **px-backup-ui** service on your private cluster to access the PX-Backup console](/docs/containers?topic=containers-ingress-types#alb-comm-create-private).
{: note}

### Adding a backup location to your PX-Backup service
{: #px-backup-storage}

Create an {{site.data.keyword.cos_full_notm}} instance and bucket, and add them as a backup location to your PX-Backup service.
{: shortdesc}

Before you begin, [log in to the PX-Backup console](#px-backup-ui). Note that if you are the first user to access the console, you must login in with the username `admin` and the password `admin`. You are redirected to a registration page to set a unique username and password. Subsequent users must register a new account to access the console.

1. [Create your {{site.data.keyword.cos_full_notm}} service instance](/docs/openshift?topic=openshift-object_storage#create_cos_service).
2. [Create service credentials for your {{site.data.keyword.cos_full_notm}} service instance](/docs/openshift?topic=openshift-object_storage#service_credentials). Be sure to enable HMAC authentication by clicking **Advanced Options** in the **Create credential** dialog box and switching the **Include HMAC Credential** parameter to **On**.
3. Expand your credentials in the service credentials table. Note the **access_key_id** and the **secret_access_key** in the **cos_hmac_keys** section.
4. [Create a storage bucket in your {{site.data.keyword.cos_full_notm}} instance](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage).
5. Click on your bucket and note its location.
6. Open the bucket configuration page and note the endpoint that you must use to connect to your {{site.data.keyword.cos_full_notm}} instance.
    - If you installed PX-Backup on a private classic cluster, note the **private** endpoint.
    - If you installed PX-Backup on a private VPC cluster, note the **direct** endpoint.
    - For all other cluster types, note the **public** endpoint.
7. In the PX-Backup console, click **Backups**.
8. Click **Settings**>**Cloud Settings**.
9. Create a cloud account to specify your {{site.data.keyword.cos_full_notm}} instance as the backup location where your data and apps are stored.
    1. For the cloud provider, choose **AWS / S3 Compliant Object Store**.
    2. Enter a name for your cloud account.
    3. Enter the **access_key_id** that you retrieved earlier.
    4. Enter the **secret_access_key** that you retrieved earlier.
    5. Click **Add+** and return to the **Cloud Settings** page.
10. In the **Backup Locations** section, add your {{site.data.keyword.cos_full_notm}} bucket as the backup location for your PX-Backup service.
    1. Enter a name for your backup location.
    2. Select the cloud account that you created earlier.
    3. In the **Path/Bucket** field, enter the name of your bucket.
    4. In the **Region** field, enter the location of your bucket that you retrieved earlier.
    5. In the **Endpoint** field, enter the endpoint for your bucket that you retrieved earlier.
    6. Click **Add+** to create the backup location.

### Adding a {{site.data.keyword.openshiftlong_notm}} cluster to your PX-Backup service
{: #px-backup-cluster}

Add the {{site.data.keyword.openshiftlong_notm}} cluster that you want to back up with PX-Backup. You can select any cluster in your account, including the cluster where you installed PX-Backup.
{: shortdesc}

Before you begin:
- [Log in to the PX-Backup console](#px-backup-ui).
- [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

The Kubeconfig in clusters with PX-Backup expires after 24 hours. To prevent your cluster's Kubeconfig file from expiring, set the context with your cluster using the `--admin` flag.
`
ibmcloud oc cluster config --cluster <cluster_name> --admin
`
{: tip}

Adding a cluster:

1. In the PX-Backup console, click **Backups**.
2. Click **Add Cluster**.
3. Enter the name of the cluster that you want to back up.
4. In the CLI, get the Kubeconfig file output for your cluster. Make sure that you have set the context to your cluster with the `--admin` flag to prevent the Kubeconfig from expiring.
    ```sh
    oc config view --flatten --minify
    ```
    {: pre}

5. Copy the entire Kubeconfig CLI output and paste it into the **Kubeconfig** field in the PX-Backup console.
6. Select **Others** as your **Kubernetes Service**.
7. If the cluster that you want to add to the PX-Backup service does not have Portworx installed in it, [you must install Stork onto the cluster](#px-backup-stork). If you installed Portworx Enterprise in your cluster, Stork is installed by default.
8. Click **Submit**. If your cluster is successfully added, you are redirected to the **Backups** page. Make sure that your cluster is listed.
9. [Back up data from your cluster](#px-backup-and-restore).
10. Repeat these steps to add more clusters to your PX-Backup service.

#### Installing Stork on a non-Portworx cluster
{: #px-backup-stork}

If a cluster that you want to back up with PX-Backup does not have Portworx Enterprise installed on it, you must install Stork on to the cluster before adding it to your PX-Backup service.
{: shortdesc}

1. From the **Add Cluster** page in the PX-Backup console, copy the command to install Stork on a **Non-PX** cluster.
2. Open a text editor and paste the command.
3. Copy the URL in the command and enter it in to your web browser to open the YAML file for the Stork installation.
4. Copy and paste the entire YAML file into a new file in your text editor.
5. If the cluster you want to add is a private cluster, find the **image** field and replace `openstorage/stork:<version_number>` with `icr.io/ext/portworx/stork:<version_numer>`. To find the latest available version of Stork, see the [Stork releases](https://github.com/libopenstorage/stork/releases){: external}.
    ```sh
    - --health-monitor-interval=120
    - --webhook-controller=false
    image: openstore/stork:2.6.2
    imagePullPolicy:Always
    resources:
      requests:
         cpu: '0.1'
      name: stork
   serviceAccountName: stork-account  
    ```
    {: screen}

6. Save the file and run the command to apply the file to your cluster and install Stork.
    ```sh
    oc apply -f <file_name>.yaml
    ```
    {: pre}

7. Verify that Stork is successfully installed on your cluster and that all pods are running.
    ```sh
    oc get deployment -n kube-system | grep stork
    ```
    {: pre}

    Example output

    ```sh
    stork                3/3   3      3      7d20h
    ```
    {: screen}



### Backing up and restoring cluster data with PX-Backup
{: #px-backup-and-restore}


To back up data from your cluster or to restore data to your cluster, refer to the [PX-Backup documentation](https://backup.docs.portworx.com/use-px-backup/backup-restore/){: external}.
{: shortdesc}

**Back up apps and data from your cluster to {{site.data.keyword.cos_full_notm}}**: 
You can back up an entire cluster namespace, single apps, and the data that is stored in your persistent volumes to the {{site.data.keyword.cos_full_notm}} service instance that you set up as your backup location. Note that in order to back up data in persistent volumes, you must have a CSI snapshot storage class in your cluster. PX-Backup uses this storage class to first take a snapshot of your data and then sends this data to your {{site.data.keyword.cos_full_notm}} backup location. For more information, see the [PX-Backup documentation](https://backup.docs.portworx.com/use-px-backup/backup-restore/perform-backup/){: external}.

**Restore any backup that you created to another cluster**: 
You can restore an entire namespace, your apps, or your data to any cluster that you added to the PX-Backup service. Use this PX-Backup capability if you want to migrate apps and data from one cluster to another. For more information, see the [PX-Backup documentation](https://backup.docs.portworx.com/use-px-backup/backup-restore/restore-backup/){: external}.

### Upgrading PX-Backup
{: #px-backup-upgrade}

Follow the Portworx documentation to [upgrade PX-backup](https://1.2.backup.docs.portworx.com/use-px-backup/upgrade/){: external}
{: shortdesc}



## Setting up disaster recovery with Portworx
{: #px-dr}

You can configure disaster recovery for your data that you store in your {{site.data.keyword.openshiftshort}} clusters by using Portworx. When one of your clusters becomes unavailable, Portworx automatically fails over to another cluster so that you can still access your data.  
{: shortdesc}

Disaster recovery with Portworx requires at least two {{site.data.keyword.openshiftshort}} clusters where Portworx is installed and configured for disaster recovery. One of the two clusters is considered the active cluster where your data is primarily stored. All data is then replicated to the standby cluster. If your active cluster becomes unavailable, Portworx automatically fails over to the standby cluster and makes the standby cluster the new active cluster so that data can continue to be accessed.

If you installed Portworx in one of your clusters without the Portworx disaster recovery plan, you must re-install Portworx with the disaster recovery plan so that you can include this cluster in your disaster recovery configuration.
{: important}

Depending on your cluster setup, Portworx offers the following two disaster recovery configurations:
- [**Metro DR**](https://docs.portworx.com/portworx-install-with-kubernetes/disaster-recovery/#1-metro-dr-nodes-are-in-the-metro-area-network-man): Your {{site.data.keyword.openshiftshort}} clusters are in the same metro location, such as both clusters are deployed in one or multiple zones of the `us-south` region. All clusters are configured to use the same Portworx cluster and share the same Portworx key-value store. Data is automatically replicated between the clusters because the Portworx storage layer is shared. RPO (Recovery Point Objective) and RTO (Recovery Time Objective) for this configuration is less than 60 seconds.
- [**Asynchronous DR**](https://docs.portworx.com/portworx-install-with-kubernetes/disaster-recovery/#2-asynchronous-dr-nodes-are-across-different-regions-datacenters): Your {{site.data.keyword.openshiftshort}} clusters are deployed in different regions, such as `us-south` and `us-east`. Each cluster has its own Portworx installation and uses a separate Portworx key-value store that is not shared. To replicate data between clusters, you must set up scheduled replication between these clusters. Because of the higher latency and scheduled replication times, the RPO for this scenario might be up to 15 minutes.

To include your cluster in a Portworx disaster recovery configuration:

1. [Choose the disaster recovery configuration that works for your cluster setup](https://docs.portworx.com/portworx-install-with-kubernetes/disaster-recovery/).
2. Review the prerequisites for the [**Metro DR**](https://docs.portworx.com/portworx-install-with-kubernetes/disaster-recovery/px-metro/1-install-px/#prerequisites){: external} and [**Asynchronous DR**](https://docs.portworx.com/portworx-install-with-kubernetes/disaster-recovery/async-dr/#pre-requisites){: external} configuration.
3. Configure disaster recovery for your cluster. 
    **Metro DR**:
    1. Choose at least two {{site.data.keyword.openshiftshort}} clusters that are located in the same metro location. If you have one cluster only, you can still configure this cluster for metro disaster recovery, but Portworx can't do a proper failover until a second cluster is configured.
    2. Make sure that all your clusters have sufficient [raw and unformatted block storage](#create_block_storage) so that you can build your Portworx storage layer.
    3. Set up a [Databases for etcd service instance](#databases-for-etcd) for your Portworx key-value store. Because both {{site.data.keyword.openshiftshort}} clusters must share the key-value store, you can't use the internal Portworx KVDB.
    4. Optional: Decide if you want to set up [encryption for your Portworx volumes](#encrypt_volumes).
    5. Follow the instructions to [install Portworx](#install_portworx) with the disaster recovery plan in both of your clusters. If you installed Portworx without the disaster recovery plan in one of your clusters already, you must re-install Portworx in that cluster with the disaster recovery plan. Make sure that you select **Databases for etcd** from the **Portworx metadata key-value store** drop-down and that you enter the same Databases for etcd API endpoint and Kubernetes secret name in both of your clusters.
    6. Continue following the [Portworx documentation](https://docs.portworx.com/portworx-install-with-kubernetes/disaster-recovery/px-metro/2-pair-clusters/){: external} to pair your clusters, sync data between them, and try out a failover of an application.

    **Asynchronous DR**:
    1. Choose at least two {{site.data.keyword.openshiftshort}} clusters that are located in different regions. If you have one cluster only, you can still configure this cluster for asynchronous disaster recovery, but Portworx can't do a proper failover until a second cluster is configured.
    2. Make sure that all your clusters have sufficient [raw and unformatted block storage](#create_block_storage) so that you can build your Portworx storage layer.
    3. Review your [options to configure a Portworx key-value store](#portworx_database). Because both clusters are in different regions, each cluster must use its own key-value store. You can use the internal Portworx KVDB or set up a Databases for etcd instance.
    4. Enable Portworx [volume encryption](#setup_encryption) for both of your clusters. The {{site.data.keyword.keymanagementservicelong_notm}} credentials are later used by Portworx to encrypt data traffic between the clusters.
    5. Follow the instructions to [install Portworx](#install_portworx) with the disaster recovery plan in both of your clusters. If you installed Portworx without the disaster recovery plan in one of your clusters already, you must re-install Portworx in that cluster with the disaster recovery plan. Make sure that you configure the Portworx key-value store that each cluster uses.
    6. Follow the [Portworx documentation](https://docs.portworx.com/portworx-install-with-kubernetes/disaster-recovery/async-dr/){: external} to create a cluster pair, enable disaster recovery mode, and schedule data migrations between your clusters.

## Exploring other Portworx features
{: #features}


Using existing Portworx volumes
:   If you have an existing Portworx volume that you created manually or that was not automatically deleted when you deleted the PVC, you can statically provision the corresponding PV and PVC and use this volume with your app. For more information, see [Using existing volumes](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/create-pvcs/using-preprovisioned-volumes/#using-the-portworx-volume){: external}.

Running stateful sets on Portworx
:   If you have a stateful app that you want to deploy as a stateful set into your cluster, you can set up your stateful set to use storage from your Portworx cluster. For more information, see [Create a MySQL StatefulSet](https://docs.portworx.com/portworx-install-with-kubernetes/application-install-with-kubernetes/cassandra/#create-a-mysql-statefulset){: external}.

Running your pods hyperconverged
:   You can configure your Portworx cluster to schedule pods on the same worker node where the pod's volume resides. This setup is also referred to as `hyperconverged` and can improve the data storage performance. For more information, see [Run pods on same host as a volume](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/hyperconvergence/){: external}.

Creating snapshots of your Portworx volumes
:   You can save the current state of a volume and its data by creating a Portworx snapshot. Snapshots can be stored on your local Portworx cluster or in the Cloud. For more information, see [Create and use local snapshots](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/create-snapshots/){: external}.

Monitoring and managing your Portworx cluster with Lighthouse
:   [Lighthouse](https://docs.portworx.com/reference/lighthouse/){: external} is an intuitive, graphical tool to help you manage and monitor your Portworx clusters and volume snapshots. With Lighthouse, you can view the health of your Portworx cluster, including the number of available storage nodes, volumes and available capacity, and analyze your data in Prometheus, Grafana, or Kibana.



## Cleaning up your Portworx volumes and cluster
{: #portworx_cleanup}

Remove a [Portworx volume](#remove_pvc_apps_volumes), a [storage node](#remove_storage_node_cluster-px), or the [entire Portworx cluster](#remove_storage_node_cluster-px) if you don't need it anymore.
{: shortdesc}

### Removing Portworx volumes from apps
{: #remove_pvc_apps_volumes}

When you added storage from your Portworx cluster to your app, you have three main components: the Kubernetes persistent volume claim (PVC) that requested the storage, the Kubernetes persistent volume (PV) that is mounted to your pod and described in the PVC, and the Portworx volume that blocks space on the physical disks of your Portworx cluster. To remove storage from your app, you must remove all components.
{: shortdesc}

1. List the PVCs in your cluster and note the **NAME** of the PVC, and the name of the PV that is bound to the PVC and shown as **VOLUME**.
    ```sh
    oc get pvc
    ```
    {: pre}

    Example output

    ```sh
    NAME                  STATUS    VOLUME                                     CAPACITY   ACCESSMODES   STORAGECLASS            AGE
    px-pvc          Bound     pvc-06886b77-102b-11e8-968a-f6612bb731fb   20Gi       RWO           px-high                 78d
    ```
    {: screen}

2. Review the **`ReclaimPolicy`** for the storage class.
    ```sh
    oc describe storageclass <storageclass_name>
    ```
    {: pre}

    If the reclaim policy says `Delete`, your PV and the data on your physical storage in your Portworx cluster are removed when you remove the PVC. If the reclaim policy says `Retain`, or if you provisioned your storage without a storage class, then your PV and your data are not removed when you remove the PVC. You must remove the PVC, PV, and the data separately.

3. Remove any pods that mount the PVC.
    1. List the pods that mount the PVC.
        ```sh
        oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"
        ```
        {: pre}

        Example output
        ```sh
        blockdepl-12345-prz7b:    claim1-block-bronze  
        ```
        {: screen}

        If no pod is returned in your CLI output, you don't have a pod that uses the PVC.

    2. Remove the pod that uses the PVC.

        If the pod is part of a deployment, remove the deployment.
        {: tip}

        ```sh
        oc delete pod <pod_name>
        ```
        {: pre}

    3. Verify that the pod is removed.
        ```sh
        oc get pods
        ```
        {: pre}

4. Remove the PVC.
    ```sh
    oc delete pvc <pvc_name>
    ```
    {: pre}

5. Review the status of your PV. Use the name of the PV that you retrieved earlier as **VOLUME**.
    ```sh
    oc get pv <pv_name>
    ```
    {: pre}

    When you remove the PVC, the PV that is bound to the PVC is released. Depending on how you provisioned your storage, your PV goes into a `Deleting` state if the PV is deleted automatically, or into a `Released` state, if you must manually delete the PV. **Note**: For PVs that are automatically deleted, the status might briefly say `Released` before it is deleted. Rerun the command after a few minutes to see whether the PV is removed.

6. If your PV is not deleted, manually remove the PV.
    ```sh
    oc delete pv <pv_name>
    ```
    {: pre}

7. Verify that the PV is removed.
    ```sh
    oc get pv
    ```
    {: pre}

8. Verify that your Portworx volume is removed. Log in to one of your Portworx pods in your cluster to list your volumes. To find available Portworx pods, run `oc get pods -n kube-system | grep portworx`.
    ```sh
    oc exec <portworx-pod>  -it -n kube-system -- /opt/pwx/bin/pxctl volume list
    ```
    {: pre}

9. If your Portworx volume is not removed, manually remove the volume.
    ```sh
    oc exec <portworx-pod>  -it -n kube-system -- /opt/pwx/bin/pxctl volume delete <volume_ID>
    ```
    {: pre}

### Removing a worker node from your Portworx cluster or the entire Portworx cluster
{: #remove_storage_node_cluster-px}

You can exclude worker nodes from your Portworx cluster or remove the entire Portworx cluster if you don't want to use Portworx anymore.
{: shortdesc}

Removing your Portworx cluster removes all the data from your Portworx cluster. Make sure to [create a snapshot for your data and save this snapshot to the cloud](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/create-snapshots/){: external}.
{: important}

- **Remove a worker node from the Portworx cluster:** If you want to remove a worker node that runs Portworx and stores data in your Portworx cluster,  you must migrate existing pods to remaining worker nodes and then uninstall Portworx from the node. For more information, see [Decommission a Portworx node in Kubernetes](https://docs.portworx.com/portworx-install-with-kubernetes/operate-and-maintain-on-kubernetes/uninstall/decommission-a-node/){: external}.
- **Remove the Portworx DaemonSet**: When you remove the Portworx DaemonSet, the Portworx containers are removed from your worker nodes. However, the Portworx configuration files remain on the worker nodes and the storage devices, and the data volumes are still intact. You can use the data volumes again if you restart the Portworx DaemonSet and containers by using the same configuration files. For more information, see [Removing the Portworx DaemonSet](#remove_px_daemonset).
- **Remove Portworx from your cluster:** If you want to remove Portworx and all your data from your cluster, follow the steps to [remove Portworx](#remove_portworx) from your cluster.

### Removing the Portworx DaemonSet
{: #remove_px_daemonset}

When you remove the Portworx DaemonSet, the Portworx containers are removed from your worker nodes. However, the Portworx configuration files remain on the worker nodes and the storage devices, and the data volumes are still intact. You can use the data volumes again if you restart the Portworx DaemonSet and containers by using the same configuration files.
{: shortdesc}

Before you begin: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Clone the `ibmcloud-storage-utilities` repo.
    ```sh
    git clone https://github.com/IBM/ibmcloud-storage-utilities.git
    ```
    {: pre}

2. Change directories to the `px-utils/px_cleanup` directory.
    ```sh
    cd ibmcloud-storage-utilities/px-utils/px_cleanup
    ```
    {: pre}

3. Run the `px_cleanup.sh` script to remove the DaemonSet from your cluster.
    ```sh
    sh ./px_cleanup.sh
    ```
    {: pre}



### Removing Portworx from your cluster
{: #remove_portworx}

If you don't want to use Portworx in your cluster, you can uninstall the Helm chart and delete your Portworx instance.
{: shortdesc}

The following steps walk you through deleting the Portworx Helm chart from your cluster and deleting your Portworx instance. If you want to clean up your Portworx installation by removing your volumes from your apps, removing individual worker nodes from Portworx, or if you want to completely remove Portworx and all your volumes and data, see [Cleaning up your Portworx cluster](#portworx_cleanup).
{: note}

The following commands result in data loss.
{: important}

1. Follow the steps to [uninstall Portworx](https://docs.portworx.com/portworx-install-with-kubernetes/operate-and-maintain-on-kubernetes/uninstall/uninstall/#delete-wipe-px-cluster-configuration){: external}. Note that for private clusters, you must specify the `px-node-wiper` image from the private `icr.io` registry.
    ```sh
    curl  -fSsL https://install.portworx.com/px-wipe | bash -s -- --talismanimage icr.io/ext/portworx/talisman --talismantag 1.1.0 --wiperimage icr.io/ext/portworx/px-node-wiper --wipertag 2.5.0
    ```
    {: pre}

2. Find the installation name of your Portworx Helm chart.
    ```sh
    helm ls -A | grep portworx
    ```
    {: pre}

    Example output

    ```sh
    NAME             NAMESPACE      REVISION    UPDATED                                 STATUS       CHART                                  APP VERSION
    <release_name>     <namespace>        1     2020-01-27 09:18:33.046018 -0500 EST    deployed  portworx-1.0.0     default     
    ```
    {: screen}

3. Delete Portworx by removing the Helm chart.
    ```sh
    helm uninstall <release_name>
    ```
    {: pre}

4. Verify that the Portworx pods are removed.
    ```sh
    oc get pod -n kube-system | grep 'portworx\|stork'
    ```
    {: pre}

    The removal of the pods is successful if no pods are displayed in your CLI output.

5. Delete the Portworx storage classes from your cluster.
    ```sh
    oc delete sc portworx-db-sc portworx-db-sc-remote portworx-db2-sc portworx-null-sc portworx-shared-sc
    ```
    {: pre}

6. Verify that the storage classes are removed.
    ```sh
    oc get sc
    ```
    {: pre}

7. Verify that the Portworx resources are removed.
    ```sh
    oc get all -A | grep portworx
    ```
    {: pre}

8. Remove the Portworx service instance from your {{site.data.keyword.cloud_notm}} account.
    1. From the [{{site.data.keyword.cloud_notm}} resource list](https://cloud.ibm.com/resources), find the Portworx service that you created.
    2. From the actions menu, click **Delete**.
    3. Confirm the deletion of the service instance by clicking **Delete**.

To stop billing for Portworx, you must remove the Portworx Helm installation from your cluster and remove the Portworx service instance from your {{site.data.keyword.cloud_notm}} account.
{: important}



## Getting help and support
{: #portworx_help_sup}

If you run into an issue with using Portworx, you can open an issue in the [Portworx Service Portal](https://pure1.purestorage.com/support){: external}. You can also submit a request by sending an e-mail to `support@purestorage.com`. If you don't have an account on the Portworx Service Portal, send an e-mail to `support@purestorage.com` or see [requeset access](https://purestorage.force.com/customers/CustomerAccessRequest){: external}. You can also [gather logging information](/docs/openshift?topic=openshift-portworx#portworx_logs) before opening a support ticket.

### Gathering logs
{: #portworx_logs}

You can use the following script to collect log information from your Portworx cluster.
{: shortdesc}

The following script collects Portworx logs from your cluster and saves them on your local machine in the `/tmp/pxlogs` directory.

Before you begin: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Clone the `ibmcloud-storage-utilities` repo.
    ```sh
    git clone https://github.com/IBM/ibmcloud-storage-utilities.git
    ```
    {: pre}

2. Navigate to the `px_logcollector` directory.
    ```sh
    cd ibmcloud-storage-utilities/px_utils/px_logcollector/ 
    ```
    {: pre}

3. Run the `px_logcollect.sh` script. You can collect logs from all your worker nodes, or you can specify the `--workers` flag and pass the private IP addresses of the worker nodes from where you want to collect logs. If you specify the `--workers` flag, the log files are saved in the `/tmp/pxlogs/<worker_node_IP>` directory with the private IP address of each worker node as the folder name. To get the private IP addresses of your worker nodes, run the `oc get nodes` command.

    * **Collect the logs from all worker nodes in your cluster.**

        ```sh
        sudo ./px_logcollect.sh
        ```
        {: pre}

    * **Collect the logs from only certain worker nodes in your cluster.**
        ```sh
        sudo ./px_logcollect.sh --workers <worker-IP> <worker-IP> <worker-IP>
        ```
        {: pre}

4. Review the log files locally. If you can't resolve your issue by reviewing the logs, [open a support ticket](/docs/openshift?topic=openshift-portworx#portworx_help_sup) and provide the log information that you collected.

## Limitations
{: #portworx_limitations}

Review the following Portworx limitations.

| Limitation | Description |
| --- | --- |
| **Classic clusters** Pod restart required when adding worker nodes. | Because Portworx runs as a DaemonSet in your cluster, existing worker nodes are automatically inspected for raw block storage and added to the Portworx data layer when you deploy Portworx. If you add or update worker nodes to your cluster and add raw block storage to those workers, restart the Portworx pods on the new or updated worker nodes so that your storage volumes are detected by the DaemonSet. |
| **VPC clusters** Storage volume reattachment required when updating worker nodes. | When you update a worker node in a VPC cluster, the worker node is removed from your cluster and replaced with a new worker node. If Portworx volumes are attached to the worker node that is replaced, you must attach the volumes to the new worker node. You can attach storage volumes with the [API](/docs/openshift?topic=openshift-utilities#vpc_api_attach) or the [CLI](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_storage_att_cr). |
| The Portworx experimental `InitializerConfiguration` feature is not supported. | {{site.data.keyword.openshiftlong_notm}} does not support the [Portworx experimental `InitializerConfiguration` admission controller](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/hyperconvergence/#initializer-experimental-feature-in-stork-v1-1). |
| Private clusters | To install Portworx in a cluster that doesn't have VRF or access to private CSEs, you must create a rule in the default security group to allow inbound and outbound traffic for the following IP addresses: `166.9.24.81`, `166.9.22.100`, and `166.9.20.178`. For more information, see [Updating the default security group](/docs/vpc?topic=vpc-updating-the-default-security-group#updating-the-default-security-group). |
{: summary="This table contains information on limitations for Portworx on {{site.data.keyword.openshiftlong_notm}} clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="Portworx limitations"}




