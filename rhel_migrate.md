---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-30"


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


1. Review your worker pool operating systems to determine which pools you need to migrate.
    ```sh
    ibmcloud ks worker-pools -c CLUSTER
    ```
    {: pre}

1. Specify the `REDHAT_9_64` version for the worker pool. 

    ```sh
    ibmcloud oc worker-pool operating-system set --cluster CLUSTER --worker-pool POOL --operating-system `REDHAT_9_64`
    ```
    {: pre}

1. Update each worker node in the worker pool by running the [`ibmcloud oc worker update`](/docs/containers?topic=containers-kubernetes-service-cli#cs_worker_update) or [`ibmcloud oc worker replace`](h/docs/containers?topic=containers-kubernetes-service-cli#cli_worker_replace) command. 

    Make sure you have enough worker nodes to support your workload while you update or replace the relevant worker nodes. For more information, see [Updating VPC worker nodes](/docs/containers?topic=containers-update&interface=ui#vpc_worker_node) or [Updating classic worker nodes](/docs/containers?topic=containers-update&interface=ui#worker_node).
    {: tip}

    ```sh
    ibmcloud oc worker update --cluster CLUSTER --worker WORKER1_ID [--worker WORKER2_ID] 
    ```
    {: pre}

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
