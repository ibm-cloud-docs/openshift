---

copyright:
  years: 2026, 2026
lastupdated: "2026-11-05"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, update flavor, machine type, change worker node flavor, worker pool

subcollection: openshift

content-type: howto

---

{{site.data.keyword.attribute-definition-list}}


# Updating flavors (machine types)
{: #update-flavors}

Update the flavor (machine type) of your worker nodes when you need different compute resources, for example, more memory, additional CPUs, or a GPU-enabled machine. Updating a flavor provisions a new worker pool with the new flavor and then removes the old worker pool. Because this process replaces nodes, all data on the worker nodes that is not stored on persistent storage is permanently deleted.
{: shortdesc}

## Before you begin
{: #machine-type-prereqs}

- [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
- Verify that any data you need to retain is stored on [persistent storage](/docs/openshift?topic=openshift-storage-plan) outside the worker node. Data stored only on the worker node is lost and cannot be recovered.
- Make sure that you have the [**Operator** or **Administrator** IAM platform access role](/docs/openshift?topic=openshift-iam-platform-access-roles). If you're unsure of your access role, go to **Manage** > **Access (IAM)** > **Users** in the {{site.data.keyword.cloud_notm}} console, or ask your account administrator.

## Updating the flavor
{: #machine-type-steps}

1. List available worker nodes and note their private IP address.

    1. List available worker pools in your cluster.
        ```sh
        ibmcloud oc worker-pool ls --cluster CLUSTER
        ```
        {: pre}

    2. List the worker nodes in the worker pool. Note the **ID** and **Private IP**.
        ```sh
        ibmcloud oc worker ls --cluster CLUSTER --worker-pool WORKER-POOL
        ```
        {: pre}

    3. Get the details for a worker node. In the output, note the zone and either the private and public VLAN ID for classic clusters or the subnet ID for VPC clusters.
        ```sh
        ibmcloud oc worker get --cluster CLUSTER --worker WORKER-ID
        ```
        {: pre}

2. List available flavors in the zone.
    ```sh
    ibmcloud oc flavors --zone ZONE
    ```
    {: pre}

3. Create a worker node with the new machine type.
    1. Create a worker pool with the number of worker nodes that you want to replace.
        * Classic clusters:
            ```sh
            ibmcloud oc worker-pool create classic --name WORKER-POOL --cluster CLUSTER --flavor FLAVOR --size-per-zone NUMBER-OF-WORKERS-PER-ZONE
            ```
            {: pre}

        * VPC Generation 2 clusters:
            ```sh
            ibmcloud oc worker-pool create vpc-gen2 --name NAME --cluster CLUSTER --flavor FLAVOR --size-per-zone NUMBER-OF-WORKERS-PER-ZONE --label LABEL
            ```
            {: pre}

    2. Verify that the worker pool is created.
        ```sh
        ibmcloud oc worker-pool ls --cluster CLUSTER
        ```
        {: pre}

    3. Add the zone to your worker pool that you retrieved earlier. When you add a zone, the worker nodes that are defined in your worker pool are provisioned in the zone and considered for future workload scheduling. If you want to spread your worker nodes across multiple zones, choose a [classic](/docs/openshift?topic=openshift-regions-and-zones#zones-mz) or [VPC](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc) multizone location.
        * Classic clusters:
            ```sh
            ibmcloud oc zone add classic --zone ZONE --cluster CLUSTER --worker-pool WORKER-POOL --private-vlan PRIVATE-VLAN-ID --public-vlan PUBLIC-VLAN-ID
            ```
            {: pre}

        * VPC clusters:
            ```sh
            ibmcloud oc zone add vpc-gen2 --zone ZONE --cluster CLUSTER --worker-pool WORKER-POOL --subnet-id VPC-SUBNET-ID
            ```
            {: pre}

4. Wait for the worker nodes to be deployed. When the worker node state changes to **Normal**, the deployment is finished.
    ```sh
    ibmcloud oc worker ls --cluster CLUSTER
    ```
    {: pre}

5. Remove the old worker pool. If you are removing a Classic bare metal flavor (which is billed monthly), you are charged for the entire month even if you remove it mid-month. VPC workers, including bare metal, are billed hourly.
{: important}

    1. Remove the worker pool with the old machine type. Removing a worker pool removes all worker nodes in the pool in all zones. This process might take a few minutes to complete.
        ```sh
        ibmcloud oc worker-pool rm --worker-pool WORKER-POOL --cluster CLUSTER
        ```
        {: pre}

    2. Verify that the worker pool is removed.
        ```sh
        ibmcloud oc worker-pool ls --cluster CLUSTER
        ```
        {: pre}

6. Verify that the worker nodes are removed from your cluster.
    ```sh
    ibmcloud oc worker ls --cluster CLUSTER
    ```
    {: pre}

7. Repeat these steps to update other worker pools or stand-alone worker nodes to different flavors.

## Next steps
{: #update-flavors-next}

[Learn how worker pools are scaled down](/docs/openshift?topic=openshift-worker-scaledown-logic) when worker nodes are removed. To keep your worker nodes current, see [Updating clusters, worker nodes, and cluster components](/docs/openshift?topic=openshift-update).

## Related links
{: #update-flavors-related}

* [Adding worker nodes to Classic clusters](/docs/openshift?topic=openshift-add-workers-classic)
* [Adding worker nodes to VPC clusters](/docs/openshift?topic=openshift-add-workers-vpc)
