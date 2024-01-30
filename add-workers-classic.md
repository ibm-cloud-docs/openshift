---

copyright: 
  years: 2014, 2024
lastupdated: "2024-01-30"


keywords: openshift, clusters, worker nodes, worker pools, add, classic

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Adding worker nodes to Classic clusters
{: #add-workers-classic}

[Classic infrastructure]{: tag-classic-inf}

Reviewing the following sections for information on how to add worker nodes to your Classic cluster.
{: shortdesc}

Looking to add workers to VPC clusters? See [Adding worker nodes to VPC clusters](/docs/openshift?topic=openshift-add-workers-classic).
{: tip}


To increase the availability of your apps, you can add worker nodes to an existing zone or multiple existing zones in your cluster. To help protect your apps from zone failures, you can add zones to your cluster.

When you create a cluster, the worker nodes are provisioned in a worker pool. After cluster creation, you can add more worker nodes to a pool by resizing it or by adding more worker pools. By default, the worker pool exists in one zone. Clusters that have a worker pool in only one zone are called single zone clusters. When you add more zones to the cluster, the worker pool exists across the zones. Clusters that have a worker pool that is spread across more than one zone are called multizone clusters.

If you have a multizone cluster, keep its worker node resources balanced. Make sure that all the worker pools are spread across the same zones, and add or remove workers by resizing the pools instead of adding individual nodes. After you set up your worker pool, you can [set up the cluster autoscaler](/docs/openshift?topic=openshift-cluster-scaling-install-addon) to automatically add or remove worker nodes from your worker pools based on your workload resource requests.


Want to save on your classic worker node costs? [Create a reservation](/docs/containers?topic=containers-reservations) to lock in a discount over 1 or 3 year terms! Then, create your worker pool by using the reserved instances. Note that autoscaling can't be enabled on worker pools that use reservations.
{: tip}

## Creating a new worker pool
{: #add_pool}

You can add worker nodes to your classic cluster by creating a new worker pool.
{: shortdesc}

Before you begin, make sure that you have the [**Operator** or **Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-users).

1. Retrieve the **Worker Zones** of your cluster and choose the zone where you want to deploy the worker nodes in your worker pool. If you have a single zone cluster, you must use the zone that you see in the **Worker Zones** field. For multizone clusters, you can choose any of the existing **Worker Zones** of your cluster, or add one of the [multizone locations](/docs/openshift?topic=openshift-regions-and-zones#zones-mz) for the region that your cluster is in. You can list available zones by running `ibmcloud oc zone ls`.
    ```sh
    ibmcloud oc cluster get --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output

    ```sh
    ...
    Worker Zones: dal10, dal12, dal13
    ```
    {: screen}

1. For each zone, list available private and public VLANs. Note the private and the public VLAN that you want to use. If you don't have a private or a public VLAN, the VLAN is automatically created for you when you add a zone to your worker pool.
    ```sh
    ibmcloud oc vlan ls --zone <zone>
    ```
    {: pre}

1. For each zone, review the [available flavors for worker nodes](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes).

    ```sh
    ibmcloud oc flavors --zone <zone>
    ```
    {: pre}

1. Create a worker pool. For more options, see the [CLI documentation](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_create).  
    * The minimum number of worker nodes per zone is 2. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).
    * Include the `--label` option to automatically label worker nodes that are in the pool with the label `key=value`.
    * If you provision a bare metal or dedicated VM worker pool, specify `--hardware dedicated`.
    * The new worker nodes run the same `major.minor` version as the cluster master, but the latest worker node patch of that `major.minor` version.


    ```sh
    ibmcloud oc worker-pool create classic --name <pool_name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_workers_per_zone_min_2> [--operating-system (REDHAT_7_64|REDHAT_8_64)] [--label key=value]
    ```
    {: pre}

1. Verify that the worker pool is created.
    ```sh
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

1. By default, adding a worker pool creates a pool with no zones. To deploy worker nodes in a zone, you must add the zones that you previously retrieved to the worker pool. If you want to spread your worker nodes across multiple zones, repeat this command for each zone.
    ```sh
    ibmcloud oc zone add classic --zone <zone> --cluster <cluster_name_or_ID> --worker-pool <pool_name> --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
    ```
    {: pre}

1. Verify that worker nodes provision in the zone that you added. Your worker nodes are ready when the status changes from `provision_pending` to `normal`.
    ```sh
    ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <pool_name>
    ```
    {: pre}

    Example output

    ```sh
    ID                                                 Public IP        Private IP      Machine Type      State    Status  Zone    Version
    kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w7   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          provision_pending   Ready   dal10   1.28
    kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w8   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          provision_pending   Ready   dal10   1.28
    ```
    {: screen}

## Resizing a worker pool
{: #resize-pool}

You can add or reduce the number of worker nodes in your cluster by resizing an existing worker pool, regardless of whether the worker pool is in one zone or spread across multiple zones.
{: shortdesc}

For example, consider a cluster with one worker pool that has three worker nodes per zone.
* If the cluster is single zone and exists in `dal10`, then the worker pool has three worker nodes in `dal10`. The cluster has a total of three worker nodes.
* If the cluster is multizone and exists in `dal10` and `dal12`, then the worker pool has three worker nodes in `dal10` and three worker nodes in `dal12`. The cluster has a total of six worker nodes.

For bare metal worker pools, keep in mind that billing is monthly. If you resize up or down, it impacts your costs for the month. When you add worker nodes by resizing a worker pool, the new worker nodes run the same `major.minor` version as the cluster master, but the latest worker node patch of that `major.minor` version.
{: tip}

Before you begin, make sure that you have the [**Operator** or **Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-users).

To resize the worker pool, change the number of worker nodes that the worker pool deploys in each zone:

1. Get the name of the worker pool that you want to resize.
    ```sh
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

1. Resize the worker pool by designating the number of worker nodes that you want to deploy in each zone. The minimum value is 2. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).
    ```sh
    ibmcloud oc worker-pool resize --cluster <cluster_name_or_ID> --worker-pool <pool_name>  --size-per-zone <number_of_workers_per_zone>
    ```
    {: pre}

1. Verify that the worker pool is resized.
    ```sh
    ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <pool_name>
    ```
    {: pre}

    Example output for a worker pool that is in two zones, `dal10` and `dal12`, and is resized to two worker nodes per zone:
    ```sh
    ID                                                 Public IP        Private IP      Machine Type      State    Status  Zone    Version
    kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w7   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal10   1.28
    kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w8   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal10   1.28
    kube-dal12-crb20b637238ea471f8d4a8b881aae4962-w9   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal12   1.28
    kube-dal12-crb20b637238ea471f8d4a8b881aae4962-w10  169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal12   1.28
    ```
    {: screen}



## Adding a zone to a worker pool
{: #add_zone}

You can span your classic cluster across multiple zones within one region by adding a zone to your existing worker pool.
{: shortdesc}

When you add a zone to a worker pool, the worker nodes that are defined in your worker pool are provisioned in the new zone and considered for future workload scheduling. {{site.data.keyword.openshiftlong_notm}} automatically adds the `failure-domain.beta.kubernetes.io/region` label for the region and the `failure-domain.beta.kubernetes.io/zone` label for the zone to each worker node. The Kubernetes scheduler uses these labels to spread pods across zones within the same region.

If you have multiple worker pools in your cluster, add the zone to all them so that worker nodes are spread evenly across your cluster. Note that when you add worker nodes to your cluster, the new worker nodes run the same `major.minor` version as the cluster master, but the latest worker node patch of that `major.minor` version.

Before you begin:
*  To add a zone to your worker pool, your worker pool must be in a [multizone-capable zone](/docs/openshift?topic=openshift-regions-and-zones#zones-mz). If your worker pool is not in a multizone-capable zone, consider [creating a new worker pool](#add_pool).
*  Make sure that you have the [**Operator** or **Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-users).
*  In classic clusters, if you have multiple VLANs for your cluster, multiple subnets on the same VLAN, or a multizone classic cluster, you must enable a [Virtual Router Function (VRF)](/docs/account?topic=account-vrf-service-endpoint&interface=ui) for your IBM Cloud infrastructure account so your worker nodes can communicate with each other on the private network. To enable VRF, see [Enabling VRF](/docs/account?topic=account-vrf-service-endpoint&interface=ui). To check whether a VRF is already enabled, use the `ibmcloud account show` command. If you can't or don't want to enable VRF, enable [VLAN spanning](/docs/vlans?topic=vlans-vlan-spanning#vlan-spanning). To perform this action, you need the **Network > Manage Network VLAN Spanning** [infrastructure permission](/docs/containers?topic=containers-access-creds#infra_access), or you can request the account owner to enable it. To check whether VLAN spanning is already enabled, use the `ibmcloud oc vlan spanning get --region <region>` [command](/docs/containers?topic=containers-kubernetes-service-cli#cs_vlan_spanning_get).

To add a zone with worker nodes to your worker pool:

1. List available zones and pick the zone that you want to add to your worker pool. The zone that you choose must be a multizone-capable zone.
    ```sh
    ibmcloud oc zone ls
    ```
    {: pre}

1. List available VLANs in that zone. If you don't have a private or a public VLAN, the VLAN is automatically created for you when you add a zone to your worker pool.
    ```sh
    ibmcloud oc vlan ls --zone <zone>
    ```
    {: pre}

1. List the worker pools in your cluster and note their names.
    ```sh
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

1. Add the zone to your worker pool. If you have multiple worker pools, add the zone to all your worker pools so that your cluster is balanced in all zones.

    A private and a public VLAN must exist before you can add a zone to multiple worker pools. If you don't have a private and a public VLAN in that zone, add the zone to one worker pool first so that a private and a public VLAN is created for you. Then, you can add the zone to other worker pools by specifying the private and the public VLAN that was created for you.
    {: note}

    If you want to use different VLANs for different worker pools, repeat this command for each VLAN and its corresponding worker pools. Any new worker nodes are added to the VLANs that you specify, but the VLANs for any existing worker nodes are not changed.
    {: tip}

    ```sh
    ibmcloud oc zone add classic --zone <zone> --cluster <cluster_name_or_ID> -p <pool_name> [-p <pool2_name>] --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
    ```
    {: pre}

1. Verify that the zone is added to your cluster. Look for the added zone in the **Worker zones** field of the output. Note that the total number of workers in the **Workers** field has increased as new worker nodes are provisioned in the added zone.
    ```sh
    ibmcloud oc cluster get --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output

    ```sh
    NAME:                           mycluster
    ID:                             df253b6025d64944ab99ed63bb4567b6
    State:                          normal
    Status:                         healthy cluster
    Created:                        2018-09-28T15:43:15+0000
    Location:                       dal10
    Pod Subnet:                     172.30.0.0/16
    Service Subnet:                 172.21.0.0/16
    Master URL:                     https://c3.<region>.containers.cloud.ibm.com:30426
    Public Service Endpoint URL:    https://c3.<region>.containers.cloud.ibm.com:30426
    Private Service Endpoint URL:   https://c3-private.<region>.containers.cloud.ibm.com:31140
    Master Location:                Dallas
    Master Status:                  Ready (21 hours ago)
    Ingress Subdomain:              mycluster-<hash>-0000.us-south.containers.appdomain.cloud
    Ingress Secret:                 mycluster-<hash>-0000
    Workers:                        6
    Worker Zones:                   dal10, dal12
    Version:                        1.28_1524
    Owner:                          owner@email.com
    Resource Group ID:              a8a12accd63b437bbd6d58fb6a462ca7
    Resource Group Name:            Default
    ```
    {: screen}





    