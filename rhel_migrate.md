---

copyright:
  years: 2022, 2022
lastupdated: "2022-07-07"

keywords: rhel, os, operating system

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Migrating to a new Red Hat Enterprise Linux version
{: #rhel_migrate}

With the release of RHEL 8, the use of RHEL 7 worker nodes is deprecated in clusters that run version 4.10 and is not supported in clusters that run 4.11 or greater. You cannot upgrade RHEL 7 worker nodes to RHEL 8. Instead, you must provision a new worker pool and then delete the previous worker pool. In versions 4.10 and later, worker nodes in the new worker pool run RHEL 8 by default. 
{: shortdesc}

For more information about creating worker pools and adding worker nodes, see [Adding worker nodes in classic clusters](/docs/openshift?topic=openshift-add_workers#classic_pools) or [Adding worker nodes in VPC clusters](/docs/openshift?topic=openshift-add_workers#vpc_pools).

If you want to upgrade a 4.9 cluster with RHEL 7 worker nodes to a 4.10 cluster with RHEL 8 worker nodes, [upgrade your cluster to version 4.10](#prep-up-410) before you follow the steps to migrate your worker nodes. 
{: important}

1. Create a new worker pool with RHEL 8 worker nodes. 

Example command to create a RHEL 8 worker pool in a classic cluster. For more information about the `worker pool create classic` command, see the [CLI reference](/docs/containers?topic=containers-kubernetes-service-cli#cs_worker_pool_create).

```sh
ibmcloud oc worker-pool create classic --name POOL_NAME --cluster CLUSTER --flavor FLAVOR --size-per-zone WORKERS_PER_ZONE --hardware ISOLATION [--disable-disk-encrypt] [--label KEY1=VALUE1] 
```
{: pre}

Example command to create a RHEL 8 worker pool in a VPC Gen 2 cluster. For more information about the `worker pool create vpc-gen2` command, see the [CLI reference](/docs/containers?topic=containers-kubernetes-service-cli#cli_worker_pool_create_vpc_gen2) for command details.

```sh
ibmcloud oc worker-pool create vpc-gen2 --name <worker_pool_name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_workers_per_zone> [--vpc-id <VPC ID>] [--label KEY1=VALUE1] [--kms-instance KMS_INSTANCE_ID]  [--crk ROOT_KEY_ID]
```
{: pre}

2. Verify that the worker pool is created and note the worker pool ID.

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

3. Add RHEL 8 worker nodes to the new worker pool. By default, worker pools are created with zero worker nodes. To add worker nodes, you must [resize the worker pool](/docs/containers?topic=containers-kubernetes-service-cli#cs_worker_pool_resize). To avoid disruptions in your cluster, ensure that the size of the new worker pool is large enough to support your current workload. You can do this by making sure that the number of RHEL 8 worker nodes you add is at least the number of RHEL 7 worker nodes that will be removed.

```sh
ibmcloud oc worker-pool resize --cluster CLUSTER --worker-pool WORKER_POOL --size-per-zone WORKERS_PER_ZONE [-q]
```
{: pre}

4. Migrate your workload to the new RHEL 8 worker pool. For more information about restricting your workload to the new worker pool, see [Deploying apps to specific worker nodes by using labels](/docs/containers?topic=containers-deploy_app#node_affinity).

Your RHEL 8 worker nodes have the `os=RHEL8` label set by default, which can be used to [create an affinity rule](/docs/containers?topic=containers-deploy_app#node_affinity) that runs your work load in your RHEL 8 worker pool. 
{: tip}

5. Scale down the worker pool that contains the RHEL 7 hosts by [manually resizing the worker pool to zero](/docs/containers?topic=containers-add_workers#resize_pool).

Consider scaling down your RHEL 7 worker pool and keeping it for several days before you delete it. This way, you can easily scale the worker pool back up if your workload experiences disruptions during the migration process. After you delete the worker pool, you cannot provision another RHEL 7 worker pool in the event of disruptions. When you have determined that your workload is stable and functions normally, you can safely delete the RHEL 7 worker pool.
{: important}

5. [Remove the worker pool](/docs/containers?topic=containers-kubernetes-service-cli#cs_worker_pool_rm) that contains the RHEL 7 hosts. 

    1. List your worker pools and note the name of the worker pool you want to remove.
    ```sh
    ibmcloud oc worker-pool ls --cluster CLUSTER [--output json] [-q]
    ```
    {: pre}

    2. Run the command to remove the worker pool.
    ```sh
    ibmcloud oc worker-pool rm --worker-pool WORKER_POOL --cluster CLUSTER [-q] [-f]
    ```
    {: pre}


