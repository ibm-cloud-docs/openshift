---

copyright:
  years: 2022, 2024
lastupdated: "2024-12-10"


keywords: rhel, os, operating system

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Migrating to a new Red Hat Enterprise Linux version
{: #rhel_migrate}

[Virtual Private Cloud]{: tag-vpc} 

RHEL 9 is available for {{site.data.keyword.redhat_openshift_notm}} Classic and VPC clusters that run version 4.16 or higher. Follow these steps to migrate your worker nodes from RHEL 8 to RHEL 9.
{: shortdesc}

For more information on RHEL 9, see the [Red Hat OpenShift release notes](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/9.4_release_notes/index){: external}. 

To find your worker node operating system, run the **`ibmcloud oc worker-pools -c CLUSTER`** command.
{: tip}

For RHEL 9, the `/tmp` directory is a separate partition that has the `nosuid`, `noexec`, and `nodev` options set. If your apps install to and run scripts or binaries under the `/tmp` directory, they might fail. Update your apps to use the `/var/tmp` directory instead of the `/tmp` directory to run temporary scripts or binaries.

The default `cgroup` implementation is `cgroup` v2. Please review the [Kubernetes migration documentation for `cgroup` v2](https://kubernetes.io/docs/concepts/architecture/cgroups/#migrating-to-cgroup-v2) and verify that your applications fully support `cgroup` v2. There are known issues with older versions of Java that may cause out of memory (OOM) issues for workloads.
{: important}

1. Review your worker pool operating systems to determine which pools you need to migrate.
    ```sh
    ibmcloud ks worker-pools -c CLUSTER
    ```
    {: pre}

1. Specify the `REDHAT_9_64` version for the worker pool. 

    ```sh
    ibmcloud oc worker-pool operating-system set --cluster CLUSTER --worker-pool POOL --operating-system REDHAT_9_64
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

1. Get the details for your worker pool and workers. In the output, verify that your worker nodes run the `REDHAT_9_64` operating system.

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
