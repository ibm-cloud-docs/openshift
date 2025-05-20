---

copyright:
  years: 2022, 2025
lastupdated: "2025-05-20"


keywords: rhel, os, operating system, rhocs, 418, migration

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Migrating to a new operating system
{: #rhel_migrate}

[Classic]{: tag-classic-inf} [VPC]{: tag-vpc}

Complete the following steps to migrate your worker nodes to a new operating system.
{: shortdesc}



## Migrating to Red Hat Enterprise Linux 9
{: #migrate-rhel-9}

For RHEL 9, the `/tmp` directory is a separate partition that has the `nosuid`, `noexec`, and `nodev` options set. If your apps install to and run scripts or binaries under the `/tmp` directory, they might fail. Update your apps to use the `/var/tmp` directory instead of the `/tmp` directory to run temporary scripts or binaries.

The default `cgroup` implementation is `cgroup` v2. In RHEL 9, `cgroup` v1 isn't supported. Review the [Kubernetes migration documentation for `cgroup` v2](https://kubernetes.io/docs/concepts/architecture/cgroups/#migrating-to-cgroup-v2) and verify that your applications fully support `cgroup` v2. There are known issues with older versions of Java that may cause out of memory (OOM) issues for workloads.
{: important}

1. Review your worker pool operating systems to find which pools you need to migrate.
    ```sh
    ibmcloud ks worker-pools -c CLUSTER
    ```
    {: pre}

1. Specify the `RHEL_9_64` version for the worker pool. 

    ```sh
    ibmcloud oc worker-pool operating-system set --cluster CLUSTER --worker-pool POOL --operating-system RHEL_9_64
    ```
    {: pre}

1. Update each worker node in the worker pool by running the [`ibmcloud oc worker update`](/docs/containers?topic=containers-kubernetes-service-cli#cs_worker_update) for Classic clusters or [`ibmcloud oc worker replace`](/docs/containers?topic=containers-kubernetes-service-cli#cli_worker_replace) for VPC clusters. 

    Make sure you have enough worker nodes to support your workload while you update or replace the relevant worker nodes. For more information, see [Updating VPC worker nodes](/docs/containers?topic=containers-update&interface=ui#vpc_worker_node) or [Updating classic worker nodes](/docs/containers?topic=containers-update&interface=ui#worker_node).
    {: tip}

    Example command to update Classic worker nodes.

    ```sh
    ibmcloud oc worker update --cluster CLUSTER --worker WORKER1_ID [--worker WORKER2_ID] 
    ```
    {: pre}

    Example command to replace VPC worker nodes.

    ```sh
    ibmcloud oc worker replace --cluster CLUSTER --worker WORKER_ID
    ```
    {: pre}

1. Get the details for your worker pool and workers. In the output, verify that your worker nodes run the `RHEL_9_64` operating system.

    Get the details for a worker pool. 
    ```sh
    ibmcloud oc worker-pools -c CLUSTER
    ```
    {: pre}

    Get the details for a worker node. 
    ```sh
    ibmcloud oc worker get --cluster CLUSTER --worker WORKER_NODE_ID 
    ```
    {: pre}
