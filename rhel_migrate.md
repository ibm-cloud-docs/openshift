---

copyright:
  years: 2022, 2022
lastupdated: "2022-08-03"

keywords: rhel, os, operating system

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Migrating to a new Red Hat Enterprise Linux version
{: #rhel_migrate}

With the release of RHEL 8, the use of RHEL 7 worker nodes is deprecated in clusters that run version 4.10 and is not supported in clusters that run 4.11 or greater. You cannot upgrade RHEL 7 worker nodes to RHEL 8. Instead, you must provision a new worker pool and then delete the previous worker pool. In versions 4.10 and later, worker nodes in the new worker pool run RHEL 8 by default. 
{: shortdesc}

Supported infrastructure providers
:   Classic
:   VPC
:   Satellite

This page is a preview of the migration steps for moving to Red Hat Enterprise Linux (RHEL) version 8. Some of the commands listed here are not yet available. RHEL 8 for Classic and VPC clusters is planned to be released in August 2022. For {{site.data.keyword.satelliteshort}} clusters, you can now add RHEL 8 hosts to your location control plane and clusters in your location.
{: preview}

For Classic and VPC clusters, if you want to upgrade a 4.9 cluster with RHEL 7 worker nodes to a 4.10 cluster with RHEL 8 worker nodes, [upgrade your cluster to version 4.10](#prep-up-410) before you follow the steps to migrate your worker nodes. 
{: important}

Version 4.10 clusters
:   After the release of RHEL 8, new Classic and VPC clusters version 4.10 and later clusters are created with RHEL 8.
:   RHEL 7 for version 4.10 clusters becomes deprecated.
:   Existing 4.10 clusters must be migrated to RHEL 8 before support for RHEL 7 with version 4.10 ends in October 2022.

Version 4.9 clusters
:   If you update your version 4.9 cluster before October 2022, you must migrate to RHEL 8 after updating to 4.10. For more information about updating to 4.9, see the [Version information and update actions](/docs/openshift?topic=openshift-cs_versions_49) Version 4.9 supports both RHEL 7 and 8 until end of support for 4.9. RHEL 7 remains the default version when creating new clusters.

Version 4.6, 4.7 and 4.8 clusters
:   RHEL 7 is supported until end of support for these cluster versions. For more information about cluster version support, see the [Version information](/docs/openshift?topic=openshift-openshift_versions).

1. Create a new worker pool with RHEL 8 worker nodes. You must include the `--operating-system` flag and specify `RHEL8`.

    Example command to create a RHEL 8 worker pool in a classic cluster. For more information about the `worker pool create classic` command, see the [CLI reference](/docs/containers?topic=containers-kubernetes-service-cli#cs_worker_pool_create). For more information about creating worker pools and adding worker nodes, see [Adding worker nodes in classic clusters](/docs/openshift?topic=openshift-add_workers#classic_pools).

    ```sh
    ibmcloud oc worker-pool create classic --name POOL_NAME --cluster CLUSTER --flavor FLAVOR --size-per-zone WORKERS_PER_ZONE --hardware ISOLATION [--disable-disk-encrypt] [--label KEY1=VALUE1] --operating-system RHEL8
    ```
    {: pre}

    Example command to create a RHEL 8 worker pool in a VPC Gen 2 cluster. For more information about the `worker pool create vpc-gen2` command, see the [CLI reference](/docs/containers?topic=containers-kubernetes-service-cli#cli_worker_pool_create_vpc_gen2) for command details. [Adding worker nodes in VPC clusters](/docs/openshift?topic=openshift-add_workers#vpc_pools).

    ```sh
    ibmcloud oc worker-pool create vpc-gen2 --name <worker_pool_name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_workers_per_zone> [--vpc-id <VPC ID>] [--label KEY1=VALUE1] [--kms-instance KMS_INSTANCE_ID] --operating-system RHEL8 [--crk ROOT_KEY_ID]
    ```
    {: pre}
    
    Example command to create a RHEL 8 worker pool in a {{site.data.keyword.satelliteshort}} cluster. Note that for {{site.data.keyword.satelliteshort}} clusters, you must first [attach RHEL 8 hosts to your location](/docs/satellite?topic=satellite-attach-hosts) before you can create a worker pool.
    
    ```sh
    ibmcloud oc worker-pool create satellite --cluster CLUSTER --host-label "os=RHEL8" --name NAME --size-per-zone SIZE --operating-system RHEL8 --zone ZONE [--label LABEL ...] 
    ```
    {: pre}

1. Verify that the worker pool is created and note the worker pool ID.

    ```sh
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output.

    ```sh
    Name            ID                              Flavor                 OS              Workers 
    my_workerpool   aaaaa1a11a1aa1aaaaa111aa11      b3c.4x16.encrypted     REDHAT_7_64    0 
    ```
    {: screen}

1. Add more RHEL 8 worker nodes to the new worker pool. By default, Classic and VPC worker pools are created with zero worker nodes. To add worker nodes, you must [resize the worker pool](/docs/containers?topic=containers-kubernetes-service-cli#cs_worker_pool_resize). To avoid disruptions in your cluster, ensure that the size of the new worker pool is large enough to support your current workload. You can do this by making sure that the number of RHEL 8 worker nodes you add is at least the number of RHEL 7 worker nodes that will be removed.

    ```sh
    ibmcloud oc worker-pool resize --cluster CLUSTER --worker-pool WORKER_POOL --size-per-zone WORKERS_PER_ZONE
    ```
    {: pre}

1. Migrate your workload to the new RHEL 8 worker pool. For more information about restricting your workload to the new worker pool, see [Deploying apps to specific worker nodes by using labels](/docs/containers?topic=containers-deploy_app#node_affinity).

    Your RHEL 8 worker nodes have the `os=RHEL8` label set by default, which can be used to [create an affinity rule](/docs/containers?topic=containers-deploy_app#node_affinity) that runs your work load in your RHEL 8 worker pool. 
    {: tip}

1. Scale down the worker pool that contains the RHEL 7 hosts by [manually resizing the worker pool to zero](/docs/containers?topic=containers-add_workers#resize_pool).

    Consider scaling down your RHEL 7 worker pool and keeping it for several days before you delete it. This way, you can easily scale the worker pool back up if your workload experiences disruptions during the migration process. After you delete the worker pool, you cannot provision another RHEL 7 worker pool in the event of disruptions. When you have determined that your workload is stable and functions normally, you can safely delete the RHEL 7 worker pool.
    {: important}

1. [Remove the worker pool](/docs/containers?topic=containers-kubernetes-service-cli#cs_worker_pool_rm) that contains the RHEL 7 workers. 

    1. List your worker pools and note the name of the worker pool you want to remove.
        ```sh
        ibmcloud oc worker-pool ls --cluster CLUSTER
        ```
        {: pre}

    2. Run the command to remove the worker pool.
        ```sh
        ibmcloud oc worker-pool rm --worker-pool WORKER_POOL --cluster CLUSTER
        ```
        {: pre}


