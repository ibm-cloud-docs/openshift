---

copyright:
  years: 2022, 2022
lastupdated: "2022-11-17"

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

## Migration actions by cluster version
{: #rhel_migrate_versions}

If you have Portworx installed, follow the steps to upgrade your installation to use at least image version `2.11.4`. For more information, see [Upgrading Portworx to a specific version](/docs/openshift?topic=openshift-portworx#px-update-specific).
{: important}

Version 4.10+ clusters
:   By default, clusters that run version 4.10 and later are created with RHEL 8 worker nodes.
:   The RHEL 7 operating system is deprecated for version 4.10.
:   Existing 4.10 clusters must be migrated to RHEL 8 before support for RHEL 7 in version 4.10 ends on 6 December 2022.

Version 4.9 clusters
:   Version 4.9 supports both RHEL 7 and 8 until end of support for 4.9. RHEL 7 remains the default version when creating new clusters.
:   If you want to upgrade a 4.9 cluster to 4.10, make sure to migrate your worker nodes from RHEL 7 to RHEL 8 before you upgrade.
:   For more information about updating to 4.9, see the [Version information and update actions](/docs/openshift?topic=openshift-cs_versions_49).

Version 4.6, 4.7 and 4.8 clusters
:   RHEL 7 is supported until end of support for these cluster versions. For more information about cluster version support, see the [Version information](/docs/openshift?topic=openshift-openshift_versions).
:   If you want to upgrade a version 4.8 cluster to 4.9, make sure to migrate your worker nodes to RHEL 8 after you upgrade.

## Creating RHEL 8 worker pools in the command line
{: #rhel-migrate-create-pools-cli}

1. You can use the following example commands to create a new worker pool with RHEL 8 worker nodes for your cluster type. Note that you must include the `--operating-system` flag and specify `REDHAT_8_64`. Make sure that the number of nodes specified with the `--size-per-zone` option matches the number of RHEL 7 worker nodes that are to be replaced.

    **Classic**: Example command to create a RHEL 8 worker pool. For more information about the `worker pool create classic` command, see the [CLI reference](/docs/containers?topic=containers-kubernetes-service-cli#cs_worker_pool_create). For more information about creating worker pools and adding worker nodes, see [Adding worker nodes in classic clusters](/docs/openshift?topic=openshift-add_workers#classic_pools).

    ```sh
    ibmcloud oc worker-pool create classic --name <worker_pool_name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_workers_per_zone> --operating-system REDHAT_8_64 
    ```
    {: pre}

    **VPC**: Example command to create a RHEL 8 worker pool. For more information about the `worker pool create vpc-gen2` command, see the [CLI reference](/docs/containers?topic=containers-kubernetes-service-cli#cli_worker_pool_create_vpc_gen2) for command details. [Adding worker nodes in VPC clusters](/docs/openshift?topic=openshift-add_workers#vpc_pools).

    ```sh
    ibmcloud oc worker-pool create vpc-gen2 --name <worker_pool_name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_workers_per_zone> --operating-system REDHAT_8_64 
    ```
    {: pre}
    
    **{{site.data.keyword.satelliteshort}}**: Example command to create a RHEL 8 worker pool. Note that for {{site.data.keyword.satelliteshort}} clusters, you must first [attach RHEL 8 hosts to your location](/docs/satellite?topic=satellite-attach-hosts) before you can create a worker pool.
    
    ```sh
    ibmcloud oc worker-pool create satellite --cluster CLUSTER --host-label "os=RHEL8" --name NAME --size-per-zone SIZE --operating-system REDHAT_8_64 --zone ZONE [--label LABEL ...] 
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
    my_workerpool   aaaaa1a11a1aa1aaaaa111aa11      b3c.4x16.encrypted     REDHAT_8_64    0 
    ```
    {: screen}

1. Add a zone to your worker pool. When you add a zone, the number of worker nodes you specified with the `--size-per-zone` option are added to the zone. These worker nodes run the RHEL 8 operating system. 
    * For classic and VPC clusters:
        * [Adding a zone to a worker pool in a classic cluster](/docs/containers?topic=containers-add_workers#add_zone)
        * [Adding a zone to a worker pool in a VPC cluster](/docs/containers?topic=containers-add_workers#vpc_add_zone)
    * For Satellite clusters:
        ```sh
        ibmcloud oc zone add satellite --zone <zone_name> --cluster <cluster_name_or_ID> --worker-pool <worker_pool> 
        ```
        {: pre}



1. Migrate your workload to the new RHEL 8 worker pool. For more information about restricting your workload to the new worker pool, see [Deploying apps to specific worker nodes by using labels](/docs/containers?topic=containers-deploy_app#node_affinity).

    If you have software-defined storage (SDS) solutions like OpenShift Data Foundation or Portworx, update your storage configurations to include the new worker nodes and verify your workloads before removing your RHEL 7 worker nodes.
    {: important}

    Your RHEL 8 worker nodes have the `os` label set by default, which can be used to [create an affinity rule](/docs/containers?topic=containers-deploy_app#node_affinity) to reschedule your workload in your RHEL 8 worker pool. 
    {: tip}
    
    For more information about rescheduling workloads, see [Safely Drain a Node](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/){: external} in the Kubernetes docs or [Understanding how to evacuate pods on nodes](https://docs.openshift.com/container-platform/4.9/nodes/nodes/nodes-nodes-working.html){: external} in the {{site.data.keyword.redhat_openshift_notm}} docs.
    {: tip}


1. [Remove the worker pool](/docs/containers?topic=containers-kubernetes-service-cli#cs_worker_pool_rm) that contains the RHEL 7 workers. 

    Consider scaling down your RHEL 7 worker pool and keeping it for several days before you remove it. This way, you can easily scale the worker pool back up if your workload experiences disruptions during the migration process. After you remove the worker pool, you cannot provision another RHEL 7 worker pool in the event of disruptions. When you have determined that your workload is stable and functions normally, you can safely remove the RHEL 7 worker pool.
    {: important}

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


