---

copyright: 
  years: 2014, 2025
lastupdated: "2025-02-14"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, clusters, worker nodes, worker pools, add

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Adding worker nodes to VPC clusters
{: #add-workers-vpc}

[Virtual Private Cloud]{: tag-vpc}

Reviewing the following sections for information on how to add worker nodes to your VPC cluster.
{: shortdesc}

To increase the availability of your apps, you can add worker nodes to an existing zone or multiple existing zones in your cluster. To help protect your apps from zone failures, you can add zones to your cluster.

When you create a cluster, the worker nodes are provisioned in a worker pool. After cluster creation, you can add more worker nodes to a pool by resizing it or by adding more worker pools. By default, the worker pool exists in one zone. Clusters that have a worker pool in only one zone are called single zone clusters. When you add more zones to the cluster, the worker pool exists across the zones. Clusters that have a worker pool that is spread across more than one zone are called multizone clusters.

If you have a multizone cluster, keep its worker node resources balanced. Make sure that all the worker pools are spread across the same zones, and add or remove workers by resizing the pools instead of adding individual nodes. After you set up your worker pool, you can [set up the cluster autoscaler](/docs/openshift?topic=openshift-cluster-scaling-install-addon) to automatically add or remove worker nodes from your worker pools based on your workload resource requests.

Looking to add workers to Classic clusters? See [Adding worker nodes to Classic clusters](/docs/openshift?topic=openshift-add-workers-classic).
{: tip}

## Resizing a worker pool
{: #resize-pool-vpc}

You can add or reduce the number of worker nodes in your cluster by resizing an existing worker pool, regardless of whether the worker pool is in one zone or spread across multiple zones.
{: shortdesc}

Before you begin, make sure that you have the [**Operator** or **Administrator** IAM platform access role](/docs/openshift?topic=openshift-iam-platform-access-roles).

To resize the worker pool, change the number of worker nodes that the worker pool deploys in each zone:

1. Get the name of the worker pool that you want to resize.
    ```sh
    ibmcloud oc worker-pool ls --cluster CLUSTER-NAME
    ```
    {: pre}

1. Resize the worker pool by designating the number of worker nodes that you want to deploy in each zone.
    ```sh
    ibmcloud oc worker-pool resize --cluster CLUSTER-NAME --worker-pool <pool_name>  --size-per-zone <number_of_workers_per_zone>
    ```
    {: pre}

1. Verify that the worker pool is resized.
    ```sh
    ibmcloud oc worker ls --cluster CLUSTER-NAME --worker-pool <pool_name>
    ```
    {: pre}

    Example output for a worker pool that is in two zones, `us-south-1` and `us-south-2`, and is resized to two worker nodes per zone:
    ```sh
    ID                                                 Public IP        Private IP      Machine Type      State    Status  Zone    Version
    kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w7   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   us-south-1   1.31
    kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w8   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   us-south-1   1.31
    kube-dal12-crb20b637238ea471f8d4a8b881aae4962-w9   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   us-south-2   1.31
    kube-dal12-crb20b637238ea471f8d4a8b881aae4962-w10  169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   us-south-2   1.31
    ```
    {: screen}

## Creating a new worker pool
{: #vpc_add_pool}


Want to create a new worker pool on dedicated hosts? See [Setting up dedicated hosts in the CLI](/docs/openshift?topic=openshift-dedicated-hosts#setup-dedicated-host-cli).
{: tip}

Before you begin, make sure that you have the [**Operator** or **Administrator** IAM platform access role](/docs/openshift?topic=openshift-iam-platform-access-roles).

1. Retrieve the **VPC ID** and **Worker Zones** of your cluster and choose the zone where you want to deploy the worker nodes in your worker pool. You can choose any of the existing **Worker Zones** of your cluster, or add one of the [multizone locations](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc) for the region that your cluster is in. You can list available zones by running `ibmcloud oc zone ls --provider vpc-gen2`.
    ```sh
    ibmcloud oc cluster get --cluster CLUSTER-NAME
    ```
    {: pre}

    Example output

    ```sh
    ...
    VPC ID:        <VPC_ID>
    ...
    Worker Zones: us-south-1, us-south-2, us-south-3
    ```
    {: screen}

1. For each zone, note the ID of VPC subnet that you want to use for the worker pool. If you don't have a VPC subnet in the zone, [create a VPC subnet](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#create-a-subnet-cli). VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256.
    ```sh
    ibmcloud oc subnets --zone <ZONE> --provider vpc-gen2 --vpc-id <VPC_ID>
    ```
    {: pre}

1. For each zone, review the available flavors for worker nodes.
    ```sh
    ibmcloud oc flavors --zone <ZONE> --provider vpc-gen2
    ```
    {: pre}

1. Optional: To encrypt the local disk of each worker node in the worker pool, get the details of your key management service (KMS) provider. If you want to use a KMS instance from a different account, you need to do these steps under the account where the KMS instance resides.
    1. Complete the steps in [VPC worker nodes](/docs/openshift?topic=openshift-encryption-vpc-worker-disks) to create your KMS instance and to authorize your service in IAM. 

    1. List available KMS instances and note the **ID**.

        ```sh
        ibmcloud oc kms instance ls
        ```
        {: pre}

    1. List the available root keys for the KMS instance that you want to use and note the **ID**.

        ```sh
        ibmcloud oc kms crk ls --instance-id <KMS_instance_ID>
        ```
        {: pre}

1. Create a worker pool. For more options, see the [CLI documentation](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_pool_create_vpc_gen2).

    ```sh
    ibmcloud oc worker-pool create vpc-gen2 --name <name> --cluster CLUSTER-NAME --flavor <flavor> --size-per-zone <number_of_worker_nodes> [--label <key>=<value>] [--vpc-id] [[--kms-account-id <KMS_account_ID>] --kms-instance <KMS_instance_ID> --crk <root_key_ID>] [--dedicated-host-pool <dedicated-host-pool>] [--security-group <group-id>] [--operating-system SYSTEM]
    ```
    {: pre}

    `--label KEY=VALUE`
    :   **Optional**: Automatically label worker nodes that are in the pool with the label `key=value` pair.

    `--vpc-id VPC`
    :   Specify this  option if the worker pool is the first in the cluster.

    `--operating-system REDHAT_9_64|REDHAT_8_64|RHCOS`
:   Optional. The operating system of the worker nodes in your cluster. For a list of available operating systems by cluster version, see the [{{site.data.keyword.openshiftshort}} version information](/docs/openshift?topic=openshift-openshift_versions). If no option is specified, the default operating system that corresponds to the cluster version is used.

    `--kms-account-id ACCOUNT`
    :   **Optional**: Specify the account where your KMS instance resides. Include the `--kms-instance-id` and `--crk` options as well.


    `--kms-instance INSTANCE`
    :   **Optional**: Specify your KMS instance ID. Include the `--kms-account-id` and `--crk` options as well.

    `--crk KEY`
    :   **Optional**: Specify your KMS root key. Include the `--kms-account-id` and `--kms-instance` options as well.

    `--security-group GROUP`
    :   Specify this option to attach additional security groups to the workers in the worker pool. Include the security group IDs that you want to attach.
    
    `--dedicated-host-pool POOL`
    :   Specify this option if you want to create your worker pool on dedicated hosts.


1. Verify that the worker pool is created.
    ```sh
    ibmcloud oc worker-pool ls --cluster CLUSTER-NAME
    ```
    {: pre}

1. By default, adding a worker pool creates a pool with no zones. To deploy worker nodes in a zone, you must add the zones that you previously retrieved to the worker pool. If you want to spread your worker nodes across multiple zones, repeat this command for each zone.
    ```sh
    ibmcloud oc zone add vpc-gen2 --zone <zone> --subnet-id <subnet_id> --cluster CLUSTER-NAME --worker-pool <worker_pool_name>
    ```
    {: pre}

1. Verify that worker nodes provision in the zone that you added. Your worker nodes are ready when the **State** changes from `provisioning` to `normal`.
    ```sh
    ibmcloud oc worker ls --cluster CLUSTER-NAME --worker-pool <pool_name>
    ```
    {: pre}

    Example output

    ```sh
    ID                                                     Primary IP     Flavor   State          Status                                        Zone       Version   
    kube-<ID_string>-<cluster_name>-<pool_name>-00000002   10.xxx.xx.xxx   c2.2x4   provisioning   Infrastructure instance status is 'pending'   us-south-1   -   
    kube-<ID_string>-<cluster_name>-<pool_name>-00000003   10.xxx.xx.xxx   c2.2x4   normal   Ready   us-south-1   1.31_1511   
    ```
    {: screen}


## Adding a zone to a worker pool
{: #vpc_add_zone}

You can span your VPC cluster across multiple zones within one region by adding a zone to your existing worker pool.
{: shortdesc}

When you add a zone to a worker pool, the worker nodes that are defined in your worker pool are provisioned in the new zone and considered for future workload scheduling. {{site.data.keyword.openshiftlong_notm}} automatically adds the `failure-domain.beta.kubernetes.io/region` label for the region and the `failure-domain.beta.kubernetes.io/zone` label for the zone to each worker node. The Kubernetes scheduler uses these labels to spread pods across zones within the same region.

If you have multiple worker pools in your cluster, add the zone to all them so that worker nodes are spread evenly across your cluster. Note that when you add worker nodes to your cluster, the new worker nodes run the same `major.minor` version as the cluster master, but the latest worker node patch of that `major.minor` version.

**Before you begin**: Make sure that you have the [**Operator** or **Administrator** IAM platform access role](/docs/openshift?topic=openshift-iam-platform-access-roles.

1. Get the **Location** of your cluster, and note the existing **Worker Zones** and **VPC ID**.
    ```sh
    ibmcloud oc cluster get --cluster CLUSTER-NAME
    ```
    {: pre}

    Example output

    ```sh
    ...
    VPC ID:        <VPC_ID>
    Workers:       3
    Worker Zones:  us-south-1
    ...
    Location:      Dallas   
    ```
    {: screen}

1. List available zones for your cluster's location to see what other zones you can add.
    ```sh
    ibmcloud oc zone ls --provider vpc-gen2 | grep <location>
    ```
    {: pre}

1. List available VPC subnets for each zone that you want to add. If you don't have a VPC subnet in the zone, [create a VPC subnet](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#create-a-subnet-cli). VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256. You can't change the number of IP addresses that a VPC subnet has later.
    ```sh
    ibmcloud oc subnets --zone <zone> --provider vpc-gen2 --vpc-id <VPC_ID>
    ```
    {: pre}

1. List the worker pools in your cluster and note their names.
    ```sh
    ibmcloud oc worker-pool ls --cluster CLUSTER-NAME
    ```
    {: pre}

1. Add the zone to your worker pool. Repeat this step for each zone that you want to add to your worker pool. If you have multiple worker pools, add the zone to all your worker pools so that your cluster is balanced in all zones. Include the `--worker-pool` option for each worker pool.

    If you want to use different VPC subnets for different worker pools, repeat this command for each subnet and its corresponding worker pools. Any new worker nodes are added to the VPC subnets that you specify, but the VPC subnets for any existing worker nodes are not changed.
    {: tip}

    ```sh
    ibmcloud oc zone add vpc-gen2 --zone <zone> --subnet-id <subnet_id> --cluster CLUSTER-NAME --worker-pool <worker_pool_name>
    ```
    {: pre}

1. Verify that the zone is added to your cluster. Look for the added zone in the **Worker Zones** field of the output. Note that the total number of workers in the **Workers** field has increased as new worker nodes are provisioned in the added zone.
    ```sh
    ibmcloud oc cluster get --cluster CLUSTER-NAME
    ```
    {: pre}

    Example output

    ```sh
    Workers:       9
    Worker Zones:  us-south-1, us-south-2, us-south-3
    ```
    {: screen}
    


1. To expose apps with [Ingress](/docs/openshift?topic=openshift-ingress-about-roks4), [update the VPC load balancer that exposes the router](/docs/openshift?topic=openshift-router-mzr-error) to include the subnet for the new zone in your cluster.
