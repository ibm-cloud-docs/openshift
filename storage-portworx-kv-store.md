---

copyright: 
  years: 2014, 2023
lastupdated: "2023-05-09"

keywords: portworx, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Setting up the Portworx key-value store
{: #storage_portworx_kv_store}


## Setting up a key-value store for Portworx metadata
{: #portworx_database}

Decide on the key-value store that you want to use to store Portworx metadata.
{: shortdesc}

Before you begin, review the [Planning your Portworx setup section](/docs/openshift?topic=openshift-storage_portworx_plan).
{: important}

The Portworx key-value store serves as the single source of truth for your Portworx cluster. If the key-value store is not available, then you can't work with your Portworx cluster to access or store your data. Existing data is not changed or removed when the Portworx database is unavailable.

To set up your key-value store, choose between the following options.
- [Automatically set up a key-value database (KVDB) during the Portworx installation](/docs/openshift?topic=openshift-storage_portworx_kv_store).
- [Set up a Databases for etcd service instance](/docs/openshift?topic=openshift-storage_portworx_kv_store).

## Using the Portworx key-value database
{: #portworx-kvdb}

Automatically set up a key-value database (KVDB) during the Portworx installation that uses the space on the additional local disks that are attached to your worker nodes.
{: shortdesc}

You can keep the Portworx metadata inside your cluster and store it along with the operational data that you plan to store with Portworx by using the internal key-value database (KVDB) that is included in Portworx. For general information about the internal Portworx KVDB, see the [Portworx documentation](https://docs.portworx.com/concepts/internal-kvdb/){: external}.

To set up the internal Portworx KDVB, follow the steps in [Installing Portworx in your cluster](/docs/openshift?topic=openshift-storage_portworx_deploy).

If you plan to use the internal KVDB, make sure that your cluster has a minimum of 3 worker nodes with additional local block storage so that the KVDB can be set up for high availability. Your data is automatically replicated across these 3 worker nodes and you can choose to scale this deployment to replicate data across up to 25 worker nodes.
{: note}

### Optional: Setting up a Databases for etcd service instance
{: #portworx-kv-db}


If you want to use an external database service for your Portworx cluster metadata and keep the metadata separate from the operational data that you plan to store with Portworx, set up a [Databases for etcd](/docs/databases-for-etcd?topic=databases-for-etcd-getting-started) service instance in your cluster.
{: shortdesc}

Databases for etcd is a managed etcd service that securely stores and replicates your data across 3 storage instances to provide high availability and resiliency for your data. For more information, see the [Databases for etcd getting started tutorial](/docs/databases-for-etcd?topic=databases-for-etcd-getting-started#getting-started). Your Databases for etcd storage automatically scales in size if required and you are charged for the amount storage that you use.

1. Make sure that you have the [**Administrator** platform access role in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM)](/docs/account?topic=account-assign-access-resources#assign-new-access) for the Databases for etcd service.  

2. Provision your Databases for etcd service instance.
    1. Open the [Databases for etcd catalog page](https://cloud.ibm.com/databases/databases-for-etcd/create){: external}.
    2. Enter a name for your service instance, such as `px-etcd`.
    3. Select the region where you want to deploy your service instance. For optimal performance, choose the region that your cluster is in.
    4. Select the same resource group that your cluster is in.
    5. Use the following settings for the initial memory and disk allocation.
        * **Initial memory allocation:** 8 GB per member (24GB total)
        * **Initial disk allocation:** 128 GB per member (384GB total)
        * **Initial CPU allocation:** 3 dedicated cores per member (9 cores total)
        * **Database version:** 3.3
    6. Decide if you want to use the default {{site.data.keyword.keymanagementserviceshort}} service instance or your own key management service provider.
    7. Review the pricing plan.
    8. Click **Create** to set up your service instance. The setup might take a few minutes to complete.
3. Create service credentials for your Databases for etcd service instance.

    1. In the navigation on the service details page, click **Service Credentials**.
    2. Click **New credentials**.
    3. Enter a name for your service credentials and click **Add**.

4. Retrieve your service credentials and certificate.{: /docs/openshift?topic=openshift-storage_portworx_kv_store}
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

7. Choose if you want to [set up encryption for your volumes with {{site.data.keyword.keymanagementservicelong_notm}}](/docs/openshift?topic=openshift-storage_portworx_encryption). If you don't want to set up {{site.data.keyword.keymanagementservicelong_notm}} encryption for your volumes, continue with [installing Portworx in your cluster](/docs/openshift?topic=openshift-storage_portworx_deploy).








