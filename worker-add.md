---

copyright: 
  years: 2014, 2021
lastupdated: "2021-11-10"

keywords: openshift, clusters, worker nodes, worker pools, delete

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Adding worker nodes and zones to clusters
{: #add_workers}

To increase the availability of your apps, you can add worker nodes to an existing zone or multiple existing zones in your cluster. To help protect your apps from zone failures, you can add zones to your cluster.
{: shortdesc}

When you create a cluster, the worker nodes are provisioned in a worker pool. After cluster creation, you can add more worker nodes to a pool by resizing it or by adding more worker pools. By default, the worker pool exists in one zone. Clusters that have a worker pool in only one zone are called single zone clusters. When you add more zones to the cluster, the worker pool exists across the zones. Clusters that have a worker pool that is spread across more than one zone are called multizone clusters.

<p class="tip">If you have a multizone cluster, keep its worker node resources balanced. Make sure that all the worker pools are spread across the same zones, and add or remove workers by resizing the pools instead of adding individual nodes.</br></br>
After you set up your worker pool, you can [set up the cluster autoscaler](/docs/openshift?topic=openshift-ca#ca) to automatically add or remove worker nodes from your worker pools based on your workload resource requests.</p>


## Adding worker nodes by resizing an existing worker pool
{: #resize_pool}

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

2. Resize the worker pool by designating the number of worker nodes that you want to deploy in each zone. The minimum value is 2. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).
    ```sh
    ibmcloud oc worker-pool resize --cluster <cluster_name_or_ID> --worker-pool <pool_name>  --size-per-zone <number_of_workers_per_zone>
    ```
    {: pre}

3. Verify that the worker pool is resized.
    ```sh
    ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <pool_name>
    ```
    {: pre}

    Example output for a worker pool that is in two zones, `dal10` and `dal12`, and is resized to two worker nodes per zone:
    ```sh
    ID                                                 Public IP        Private IP      Machine Type      State    Status  Zone    Version
    kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w7   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal10   1.20.11
    kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w8   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal10   1.20.11
    kube-dal12-crb20b637238ea471f8d4a8b881aae4962-w9   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal12   1.20.11
    kube-dal12-crb20b637238ea471f8d4a8b881aae4962-w10  169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal12   1.20.11
    ```
    {: screen}




## Adding worker nodes in VPC clusters
{: #vpc_pools}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) Add worker nodes to your VPC cluster.
{: shortdesc}

### Creating a new worker pool
{: #vpc_add_pool}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) You can add worker nodes to your VPC cluster by creating a new worker pool.
{: shortdesc}

Before you begin, make sure that you have the [**Operator** or **Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-users).

1. Retrieve the **VPC ID** and **Worker Zones** of your cluster and choose the zone where you want to deploy the worker nodes in your worker pool. You can choose any of the existing **Worker Zones** of your cluster, or add one of the [multizone locations](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc) for the region that your cluster is in. You can list available zones by running `ibmcloud oc zone ls --provider vpc-gen2`.
    ```sh
    ibmcloud oc cluster get --cluster <cluster_name_or_ID>
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

2. For each zone, note the ID of VPC subnet that you want to use for the worker pool. If you do not have a VPC subnet in the zone, [create a VPC subnet](/docs/vpc?topic=vpc-creating-a-vpc-using-cli#create-a-subnet-cli). VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256.
    ```sh
    ibmcloud oc subnets --zone <zone> --provider vpc-gen2 --vpc-id <VPC_ID>
    ```
    {: pre}

3. For each zone, review the [available flavors for worker nodes](/docs/openshift?topic=openshift-planning_worker_nodes#vm).
    ```sh
    ibmcloud oc flavors --zone <zone> --provider vpc-gen2
    ```
    {: pre}

4. Optional: To encrypt the local disk of each worker node in the worker pool, get the details of your key management service (KMS) provider.
    1. Complete the steps in [VPC worker nodes](/docs/openshift?topic=openshift-encryption#worker-encryption-vpc) to create your KMS instance and to authorize your service in IAM. 
    2. List available KMS instances and note the **ID**.
        ```sh
        ibmcloud oc kms instance ls
        ```
        {: pre}

    3. List the available root keys for the KMS instance that you want to use and note the **ID**.
        ```sh
        ibmcloud oc kms crk ls --instance-id <KMS_instance_ID>
        ```
        {: pre}

5. Create a worker pool. Include the `--label` option to automatically label worker nodes that are in the pool with the label `key=value`. Include the `--vpc-id` option if the worker pool is the first in the cluster.Optionally include the `--kms-instance` and `--crk` flags with the values you previously retrieved. For more options, see the [CLI documentation](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_pool_create_vpc_gen2). Note that the new worker nodes run the same `major.minor` version as the cluster master, but the latest worker node patch of that `major.minor` version.
    ```sh
    ibmcloud oc worker-pool create vpc-gen2 --name <name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_worker_nodes_min_2> [--label <key>=<value>] [--vpc-id] [--kms-instance <KMS_instance_ID> --crk <root_key_ID>]
    ```
    {: pre}

6. Verify that the worker pool is created.
    ```sh
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

7. By default, adding a worker pool creates a pool with no zones. To deploy worker nodes in a zone, you must add the zones that you previously retrieved to the worker pool. If you want to spread your worker nodes across multiple zones, repeat this command for each zone.
    ```sh
    ibmcloud oc zone add vpc-gen2 --zone <zone> --subnet-id <subnet_id> --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name>
    ```
    {: pre}

8. Verify that worker nodes provision in the zone that you added. Your worker nodes are ready when the **State** changes from `provisioning` to `normal`.
    ```sh
    ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <pool_name>
    ```
    {: pre}

    Example output

    ```sh
    ID                                                     Primary IP     Flavor   State          Status                                        Zone       Version   
    kube-<ID_string>-<cluster_name>-<pool_name>-00000002   10.xxx.xx.xxx   c2.2x4   provisioning   Infrastructure instance status is 'pending'   us-south-1   -   
    kube-<ID_string>-<cluster_name>-<pool_name>-00000003   10.xxx.xx.xxx   c2.2x4   normal   Ready   us-south-1   1.20.11_1511   
    ```
    {: screen}

### Adding a zone to a worker pool
{: #vpc_add_zone}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) You can span your VPC cluster across multiple zones within one region by adding a zone to your existing worker pool.
{: shortdesc}

When you add a zone to a worker pool, the worker nodes that are defined in your worker pool are provisioned in the new zone and considered for future workload scheduling. {{site.data.keyword.openshiftlong_notm}} automatically adds the `failure-domain.beta.kubernetes.io/region` label for the region and the `failure-domain.beta.kubernetes.io/zone` label for the zone to each worker node. The Kubernetes scheduler uses these labels to spread pods across zones within the same region.

If you have multiple worker pools in your cluster, add the zone to all of them so that worker nodes are spread evenly across your cluster. Note that when you add worker nodes to your cluster, the new worker nodes run the same `major.minor` version as the cluster master, but the latest worker node patch of that `major.minor` version.

**Before you begin**: Make sure that you have the [**Operator** or **Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-users).

1. Get the **Location** of your cluster, and note the existing **Worker Zones** and **VPC ID**.
    ```sh
    ibmcloud oc cluster get --cluster <cluster_name_or_ID>
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

2. List available zones for your cluster's location to see what other zones you can add.
    ```sh
    ibmcloud oc zone ls --provider vpc-gen2 | grep <location>
    ```
    {: pre}

3. List available VPC subnets for each zone that you want to add. If you do not have a VPC subnet in the zone, [create a VPC subnet](/docs/vpc?topic=vpc-creating-a-vpc-using-cli#create-a-subnet-cli). VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256. You cannot change the number of IP addresses that a VPC subnet has later.
    ```sh
    ibmcloud oc subnets --zone <zone> --provider vpc-gen2 --vpc-id <VPC_ID>
    ```
    {: pre}

4. List the worker pools in your cluster and note their names.
    ```sh
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

5. Add the zone to your worker pool. Repeat this step for each zone that you want to add to your worker pool. If you have multiple worker pools, add the zone to all your worker pools so that your cluster is balanced in all zones. Include the `--worker-pool` flag for each worker pool.

    If you want to use different VPC subnets for different worker pools, repeat this command for each subnet and its corresponding worker pools. Any new worker nodes are added to the VPC subnets that you specify, but the VPC subnets for any existing worker nodes are not changed.
    {: tip}

    ```sh
    ibmcloud oc zone add vpc-gen2 --zone <zone> --subnet-id <subnet_id> --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name>
    ```
    {: pre}

6. Verify that the zone is added to your cluster. Look for the added zone in the **Worker Zones** field of the output. Note that the total number of workers in the **Workers** field has increased as new worker nodes are provisioned in the added zone.
    ```sh
    ibmcloud oc cluster get --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output

    ```sh
    Workers:       9
    Worker Zones:  us-south-1, us-south-2, us-south-3
    ```
    {: screen}

7. To expose apps with [Ingress](/docs/openshift?topic=openshift-ingress-about-roks4), you must [update the VPC load balancer that exposes the router](/docs/openshift?topic=openshift-router-mzr-error) to include the subnet for the new zone in your cluster.




## Adding worker nodes in classic clusters
{: #classic_pools}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) Add worker nodes to your classic cluster.
{: shortdesc}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) Want to save on your classic worker node costs? [Create a reservation](/docs/containers?topic=containers-reservations) to lock in a discount over 1 or 3 year terms! Then, create your worker pool by using the reserved instances.
{: tip}

### Creating a new worker pool
{: #add_pool}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) You can add worker nodes to your classic cluster by creating a new worker pool.
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

2. For each zone, list available private and public VLANs. Note the private and the public VLAN that you want to use. If you do not have a private or a public VLAN, the VLAN is automatically created for you when you add a zone to your worker pool.
    ```sh
    ibmcloud oc vlan ls --zone <zone>
    ```
    {: pre}

3. For each zone, review the [available flavors for worker nodes](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes).

    ```sh
    ibmcloud oc flavors --zone <zone>
    ```
    {: pre}

4. Create a worker pool. For more options, see the [CLI documentation](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_create).  
    * The minimum number of worker nodes per zone is 2. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).
    * Include the `--label` option to automatically label worker nodes that are in the pool with the label `key=value`.
    * If you provision a bare metal or dedicated VM worker pool, specify `--hardware dedicated`.
    * The new worker nodes run the same `major.minor` version as the cluster master, but the latest worker node patch of that `major.minor` version.

    ```sh
    ibmcloud oc worker-pool create classic --name <pool_name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_workers_per_zone_min_2> [--label key=value]
    ```
    {: pre}

5. Verify that the worker pool is created.
    ```sh
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

6. By default, adding a worker pool creates a pool with no zones. To deploy worker nodes in a zone, you must add the zones that you previously retrieved to the worker pool. If you want to spread your worker nodes across multiple zones, repeat this command for each zone.
    ```sh
    ibmcloud oc zone add classic --zone <zone> --cluster <cluster_name_or_ID> --worker-pool <pool_name> --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
    ```
    {: pre}

7. Verify that worker nodes provision in the zone that you added. Your worker nodes are ready when the status changes from **provision_pending** to **normal**.
    ```sh
    ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <pool_name>
    ```
    {: pre}

    Example output

    ```sh
    ID                                                 Public IP        Private IP      Machine Type      State    Status  Zone    Version
    kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w7   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          provision_pending   Ready   dal10   1.20.11
    kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w8   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          provision_pending   Ready   dal10   1.20.11
    ```
    {: screen}



### Adding a zone to a worker pool
{: #add_zone}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) You can span your classic cluster across multiple zones within one region by adding a zone to your existing worker pool.
{: shortdesc}

When you add a zone to a worker pool, the worker nodes that are defined in your worker pool are provisioned in the new zone and considered for future workload scheduling. {{site.data.keyword.openshiftlong_notm}} automatically adds the `failure-domain.beta.kubernetes.io/region` label for the region and the `failure-domain.beta.kubernetes.io/zone` label for the zone to each worker node. The Kubernetes scheduler uses these labels to spread pods across zones within the same region.

If you have multiple worker pools in your cluster, add the zone to all of them so that worker nodes are spread evenly across your cluster. Note that when you add worker nodes to your cluster, the new worker nodes run the same `major.minor` version as the cluster master, but the latest worker node patch of that `major.minor` version.

Before you begin:
*  To add a zone to your worker pool, your worker pool must be in a [multizone-capable zone](/docs/openshift?topic=openshift-regions-and-zones#zones-mz). If your worker pool is not in a multizone-capable zone, consider [creating a new worker pool](#add_pool).
*  Make sure that you have the [**Operator** or **Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-users).
*  In classic clusters, if you have multiple VLANs for your cluster, multiple subnets on the same VLAN, or a multizone classic cluster, you must enable a [Virtual Router Function (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf) for your IBM Cloud infrastructure account so your worker nodes can communicate with each other on the private network. To enable VRF, see [Enabling VRF](/docs/account?topic=account-vrf-service-endpoint#vrf). To check whether a VRF is already enabled, use the `ibmcloud account show` command. If you cannot or do not want to enable VRF, enable [VLAN spanning](/docs/vlans?topic=vlans-vlan-spanning#vlan-spanning). To perform this action, you need the **Network > Manage Network VLAN Spanning** [infrastructure permission](/docs/openshift?topic=openshift-access-creds#infra_access), or you can request the account owner to enable it. To check whether VLAN spanning is already enabled, use the `ibmcloud oc vlan spanning get --region <region>` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vlan_spanning_get).

To add a zone with worker nodes to your worker pool:

1. List available zones and pick the zone that you want to add to your worker pool. The zone that you choose must be a multizone-capable zone.
    ```sh
    ibmcloud oc zone ls
    ```
    {: pre}

2. List available VLANs in that zone. If you do not have a private or a public VLAN, the VLAN is automatically created for you when you add a zone to your worker pool.
    ```sh
    ibmcloud oc vlan ls --zone <zone>
    ```
    {: pre}

3. List the worker pools in your cluster and note their names.
    ```sh
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

4. Add the zone to your worker pool. If you have multiple worker pools, add the zone to all your worker pools so that your cluster is balanced in all zones.

    A private and a public VLAN must exist before you can add a zone to multiple worker pools. If you do not have a private and a public VLAN in that zone, add the zone to one worker pool first so that a private and a public VLAN is created for you. Then, you can add the zone to other worker pools by specifying the private and the public VLAN that was created for you.
    {: note}

    If you want to use different VLANs for different worker pools, repeat this command for each VLAN and its corresponding worker pools. Any new worker nodes are added to the VLANs that you specify, but the VLANs for any existing worker nodes are not changed.
    {: tip}

    ```sh
    ibmcloud oc zone add classic --zone <zone> --cluster <cluster_name_or_ID> -w <pool_name> [-w <pool2_name>] --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
    ```
    {: pre}

5. Verify that the zone is added to your cluster. Look for the added zone in the **Worker zones** field of the output. Note that the total number of workers in the **Workers** field has increased as new worker nodes are provisioned in the added zone.
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
    Version:                        1.20.11_1524
    Owner:                          owner@email.com
    Resource Group ID:              a8a12accd63b437bbd6d58fb6a462ca7
    Resource Group Name:            Default
    ```
    {: screen}



## Managing {{site.data.keyword.satelliteshort}} worker pools
{: #satcluster-worker-pools}

Review the following differences from classic {{site.data.keyword.openshiftlong_notm}} clusters when you manage the worker pool life cycle of clusters that are in a {{site.data.keyword.satelliteshort}} location.
{: shortdesc}

### Creating {{site.data.keyword.satelliteshort}} worker pools with host labels for autoassignment
{: #sat-pool-create-labels}

Create a worker pool in your {{site.data.keyword.satelliteshort}} cluster with host labels. Then, {{site.data.keyword.satelliteshort}} can automatically assign available hosts to the worker pool. For more information, see [Using host autoassignment](/docs/satellite?topic=satellite-hosts#host-autoassign-ov).
{: shortdesc}

**Before you begin**:
*   Make sure that you have the **Operator** platform access role to **Kubernetes Service** for the cluster in {{site.data.keyword.cloud_notm}} IAM.
*   Optional: [Attach](/docs/satellite?topic=satellite-hosts#attach-hosts) or [list available](/docs/satellite?topic=satellite-satellite-cli-reference#host-ls) hosts to your {{site.data.keyword.satelliteshort}} location with host labels that match your worker pool. Then, after you create your worker pool, these available hosts can be automatically assigned to the worker pool.

**To create a worker pool in a {{site.data.keyword.satelliteshort}} cluster**:
1. List the {{site.data.keyword.satelliteshort}} clusters in your account.
    ```sh
    ibmcloud oc cluster ls --provider satellite
    ```
    {: pre}

2. Get the details of the cluster that you want to create the worker pool in. Note the **Worker Zones**.
    ```sh
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}

3. Create the worker pool in your {{site.data.keyword.satelliteshort}} cluster, with the following parameters.

    * `--cluster`: Enter the name or ID of your cluster.
    * `--name`: Give a name for your worker pool.
    * `--size-per-zone`: Specify the number of worker nodes that you want to have in each zone that the worker pool spans. You can change this value later by resizing the worker pool.
    * `--zone`: Select the initial zone in your {{site.data.keyword.satelliteshort}} location to create the worker pool in, that you retrieved from your cluster details. You can add more zones later.
    * `--host-label`: Add labels to match the requested capacity of the worker pool with the available hosts in the {{site.data.keyword.satelliteshort}} location. You can use just the `cpu=number` host label because {{site.data.keyword.satelliteshort}} hosts automatically get this host label. You can also add a custom host label like `env=prod`. **Important**: You cannot update host labels on the worker pool later, so make sure to configure the labels properly. You can change the labels on {{site.data.keyword.satelliteshort}} hosts, if needed.

    ```sh
    ibmcloud oc worker-pool create satellite --cluster <cluster_name_or_ID> --name <pool_name> --size-per-zone <number> --zone <satellite_zone> --host-label <cpu=number> --host-label <memory=number> [--host-label <key=value>]
    ```
    {: pre}

Your worker pool is created!
* If {{site.data.keyword.satelliteshort}} hosts with matching labels are available, the hosts are assigned to the worker pool as worker nodes. Keep in mind that hosts might also have a zone label and are assigned only to that zone.
* If no hosts are available, you can [manually assign hosts](/docs/satellite?topic=satellite-hosts#host-assign) to the worker pool. Keep in mind that if you manually assign hosts, host autoassignment is disabled for future actions until you rebalance the worker pool.

When you assign hosts, you are charged a {{site.data.keyword.satelliteshort}} management fee per host vCPU.
{: note}

### Maintaining {{site.data.keyword.satelliteshort}} worker pools
{: #sat-pool-maintenance}

You can maintain your worker pools by using the same worker pool lifecycle operations as you use for {{site.data.keyword.openshiftlong_notm}} clusters. Review the {{site.data.keyword.satelliteshort}} considerations for common operations.
{: shortdesc}

#### Resizing a {{site.data.keyword.satelliteshort}} worker pool
{: #sat-pool-maintenance-resize}

Resize your worker pool to request more compute capacity in your cluster.
{: shortdesc}

* When host autoassignment is enabled, {{site.data.keyword.satelliteshort}} automatically assigns available hosts to the worker pool, as long as the host labels match the host labels of the worker pool. If no hosts are available, [attach more hosts](/docs/satellite?topic=satellite-hosts#attach-hosts) with matching labels to the {{site.data.keyword.satelliteshort}} location.
* If host autoassignment is disabled, resizing the worker pool enables autoassignment again.

For more information, see [Adding worker nodes by resizing an existing worker pool](/docs/openshift?topic=openshift-add_workers#resize_pool).

#### Rebalancing a {{site.data.keyword.satelliteshort}} worker pool
{: #sat-pool-maintenance-rebalance}

When you rebalance a worker pool, the worker pool is sized up or down depending on the most recently requested number of worker nodes per zone. You can check the requested number in the worker pool details, or set the requested number by resizing the worker pool.
{: shortdesc}

In {{site.data.keyword.satelliteshort}} worker pool, rebalancing also re-enables [host autoassignment](/docs/satellite?topic=satellite-hosts#host-autoassign-ov). You can rebalance the worker pool from the {{site.data.keyword.cloud_notm}} console or the `ibmcloud oc worker-pool rebalance` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance).

#### Updating worker nodes in a {{site.data.keyword.satelliteshort}} worker pool
{: #sat-pool-maintenance-update}

Follow the same process as [Updating classic worker nodes](/docs/openshift?topic=openshift-update#worker_node).
{: shortdesc}

#### Adding zones to a {{site.data.keyword.satelliteshort}} worker pool
{: #sat-pool-maintenance-addzone}

You can add zones to a worker pool. Available {{site.data.keyword.satelliteshort}} hosts with a zone label can be assigned only to that zone in the worker pool.
{: shortdesc}

* For more information about zones in {{site.data.keyword.satelliteshort}}, see [{{site.data.keyword.satelliteshort}} concepts](/docs/satellite?topic=satellite-infrastructure-plan).
* To add a zone, see the [`ibmcloud oc zone add satellite` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_zone_add_sat).

#### Removing a {{site.data.keyword.satelliteshort}} worker pool
{: #sat-pool-maintenance-remove}

When you remove a worker pool, all of the worker nodes in the cluster are removed. The hosts that the worker nodes ran on are unassigned from the cluster, and become unusable by but still attached to the {{site.data.keyword.satelliteshort}} location. For more information, see [Removing {{site.data.keyword.satelliteshort}} worker nodes or clusters](/docs/satellite?topic=openshift-satellite-clusters#satcluster-rm).
{: shortdesc}




## Deprecated: Adding stand-alone worker nodes
{: #standalone}

If you have a cluster that was created before worker pools were introduced, you can use the deprecated commands to add stand-alone worker nodes.
{: deprecated}

If you have a cluster that was created after worker pools were introduced, you cannot add stand-alone worker nodes. Instead, you can [create a worker pool](#add_pool), [resize an existing worker pool](#resize_pool), or [add a zone to a worker pool](#add_zone) to add worker nodes to your cluster.
{: note}

1. List available zones and pick the zone where you want to add worker nodes.
    ```sh
    ibmcloud oc zone ls
    ```
    {: pre}

2. List available VLANs in that zone and note their ID.
    ```sh
    ibmcloud oc vlan ls --zone <zone>
    ```
    {: pre}

3. List available flavors in that zone.
    ```sh
    ibmcloud oc flavors --zone <zone>
    ```
    {: pre}

4. Add stand-alone worker nodes to the cluster. For bare metal flavors, specify `dedicated`.
    ```sh
    ibmcloud oc worker add --cluster <cluster_name_or_ID> --workers <number_of_worker_nodes> --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID> --flavor <flavor> --hardware <shared_or_dedicated>
    ```
    {: pre}

5. Verify that the worker nodes are created.
    ```sh
    ibmcloud oc worker ls --cluster <cluster_name_or_ID>
    ```
    {: pre}




## Installing SGX drivers and platform software on SGX-capable worker nodes
{: #install-sgx}

Intel Software Guard Extensions (SGX) is a technology that can protect data-in-use through hardware-based server security. With Intel SGX, you can protect select code and data from disclosure or modification. Through the use of trusted execution environments (TEE), known as enclaves, you can encrypt the pieces of your app memory that contain sensitive data while the data or code is being used. To use Intel SGX, you must install the SGX drivers and platform software on SGX-capable worker nodes. Then, design your app to run in an SGX environment.
{: shortdesc}

![An example SGX application.](images/cc-iks.png){: caption="Figure. Example SGX application set up" caption-side="bottom"}

When you develop a confidential computing application, you must design it in a way that you can segment the information that needs to be encrypted. At runtime, the segmented information is kept confidential through a process that is known as attestation. When a request for information from the segmented code or app data is received, the enclave verifies that the request comes from the part of the application that exists outside of the enclave within the same application before sharing any information. Through the attestation process, information is kept confidential and data leakage is prevented.

Don't have an app that's configured to use Intel SGX but you still want to take advantage of the technology? Try using [IBM Cloud Data Shield](/docs/data-shield?topic=data-shield-getting-started).
{: tip}

### Installing with a script
{: #intel-sgx-script}

Before you begin, [create a worker pool](/docs/openshift?topic=openshift-add_workers#add_pool) with SGX-capable worker nodes. To work with Intel SGX, you must use one of the following machine types: `me4c.4x32` and `me4c.4x32.1.9tb.ssd`.


1. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

2. Create an `sgx-admin` project with a privileged security context constraint that is added to the project service account so that the drivers and platform software can pull and run the required images.

    ```sh
    curl -fssl https://raw.githubusercontent.com/ibm-cloud-security/data-shield-reference-apps/master/scripts/sgx-driver-psw/config_openshift/create_openshift_config.sh | bash
    ```
    {: codeblock}

3. Create a daemon set to install the drivers and platform software on your SGX-capable worker nodes.

    ```sh
    oc create -f https://raw.githubusercontent.com/ibm-cloud-security/data-shield-reference-apps/master/scripts/sgx-driver-psw/install_sgx/deployment_install_sgx_openshift.yaml
    ```
    {: codeblock}

4. Verify that the drivers and platform software were installed by running the following command to check for a pod that begins with `sgx-installer`.

    ```sh
    oc get pods
    ```
    {: codeblock}

5. Get the logs for your `sgx-installer` pod to verify that you see the messages `SGX driver installed` and `PSW installed`.

    ```sh
    oc logs <name_of_SGX_installer_pod>
    ```

6. Now that the drivers and platform software are installed, remove the daemon set.

    ```sh
    oc delete daemonset sgx-installer
    ```
    {: codeblock}

7. Delete the security context and service account that you created.

    ```sh
    oc delete scc sgx-admin
    oc delete serviceaccount sgx-admin
    ```
    {: codeblock}

Now, you can develop your confidential computing app to use the enclave for sensitive data.

To uninstall the drivers and platform software, you can follow the same steps, but with the following installation command: `oc create -f https://raw.githubusercontent.com/ibm-cloud-security/data-shield-reference-apps/master/scripts/sgx-driver-psw/uninstall_sgx/deployment_uninstall_sgx_openshift.yaml`
{: note}





## Adding tags to existing clusters
{: #cluster_tags}


You can assign a tag to {{site.data.keyword.openshiftlong_notm}} clusters to help manage your {{site.data.keyword.cloud_notm}} resources. For example, you might add `key:value` tags to your cluster and other cloud resources so that your billing department track resources, such as `costctr:1234`. Tags are visible account-wide. For more information, see [Working with tags](/docs/account?topic=account-tag).
{: shortdesc}

Tags are not the same thing as Kubernetes labels. [Kubernetes labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/){: external} are `key:value` pairs that can be used as selectors for the resources that are in your cluster, such as [adding a label to worker pool](#worker_pool_labels) to [deploy an app to only certain worker nodes](/docs/containers?topic=containers-deploy_app#node_affinity). Tags are an {{site.data.keyword.cloud_notm}} tool that you can use to filter your {{site.data.keyword.cloud_notm}} resources, such as clusters, storage devices, or {{site.data.keyword.watson}} services.
{: note}

Do not include personal information in your tags. Learn more about [securing your personal information](/docs/openshift?topic=openshift-security#pi) when you work with Kubernetes resources.
{: important}

Choose among the following options:

*   [Create a cluster in the console](/docs/containers?topic=containers-clusters) with a tag. You cannot create a cluster with a tag in the CLI.
*   Add tags to an existing cluster in the console or CLI.

| Adding tags to clusters with the console. |
|:-----------------|
| <p><ol><li>Log in to the <a href="https://cloud.ibm.com/kubernetes/clusters"><strong>{{site.data.keyword.cloud_notm}} clusters</strong> console</a> <img src="../icons/launch-glyph.svg" alt="External link icon">.</li><li>Select a cluster with existing tags.</li><li>Next to the cluster name and status, click the <strong>Edit tags</strong> pencil icon.<p class="note">If your cluster does not have any existing tags, you do not have an <strong>Edit tags</strong> pencil icon. Instead, use the <a href="/docs/account?topic=account-tag">resource list</a> or CLI.</p></li><li>Enter the tag that you want to add to your cluster. To assign a key-value pair, use a colon such as <code>costctr:1234</code>.</li></ol></p> |
{: caption="Adding tags to clusters with the console." caption-side="top"}
{: #tags-1}
{: tab-title="Console"}
{: tab-group="tags"}
{: class="simple-tab-table"}

| Adding tags to clusters with the CLI. |
|:-----------------|
| <p><ol><li>Log in to the <a href="/docs/cli/reference/ibmcloud?topic=cli-ibmcloud_cli#ibmcloud_login">{{site.data.keyword.cloud_notm}} CLI</a>.<pre class="pre"><code>ibmcloud login [--sso]</code></pre></li><li><a href="/docs/cli/reference/ibmcloud?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_tag_attach">Tag your cluster</a>. Replace the <code>--resource-name</code> with the name of your cluster. To list available clusters, run <code>ibmcloud oc cluster ls</code>. If you want to check your existing tags so as not to duplicate any, run <code>ibmcloud resource tags</code>.<pre class="pre"><code>ibmcloud resource tag-attach --resource-name &lt;cluster_name&gt; --tag-names &lt;tag1,tag2&gt;</code></pre><p class="note">If you have more than one resource of the same name in your {{site.data.keyword.cloud_notm}} account, the error message lists the resource CRNs and details, and instructs you to try again with the <code>--resource-id</code> flag.</p></li></ol></p> |
{: caption="Adding tags to clusters with the CLI." caption-side="top"}
{: #tags-2}
{: tab-title="CLI"}
{: tab-group="tags"}
{: class="simple-tab-table"}



## Adding labels to existing worker pools
{: #worker_pool_labels}

You can assign a worker pool a label when you [create the worker pool](#add_pool), or later by following these steps. After a worker pool is labeled, all existing and subsequent worker nodes get this label. You might use labels to deploy specific workloads only to worker nodes in the worker pool, such as [edge nodes for load balancer network traffic](/docs/openshift?topic=openshift-edge).
{: shortdesc}

Do not include personal information in your labels. Learn more about [securing your personal information](/docs/openshift?topic=openshift-security#pi) when you work with Kubernetes resources.
{: important}

Before you begin: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. List the worker pools in your cluster.
    ```sh
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

2. List the existing custom labels on worker nodes in the worker pool that you want to label.
    ```sh
    ibmcloud oc worker-pool get -c <cluster_name_or_ID> --worker-pool <pool>
    ```
    {: pre}

3. Label the worker pool with a `key=value` label. When you set a worker pool label, all the existing custom labels are replaced. To keep any existing custom labels on the worker pool, include those labels with this flag.

    You can also rename an existing label by assigning the same key a new value. However, do not modify the worker pool or worker node labels that are provided by default because these labels are required for worker pools to function properly. Modify only custom labels that you previously added.
    {: important}

    ```sh
    ibmcloud oc worker-pool label set <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID> --label <key=value>
    ```
    {: pre}

    Example to set `<key>: <value>` as a new custom label in a worker pool with existing labels `team: DevOps` and `app: test`:
    ```sh
    ibmcloud oc worker-pool label set <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID> --label <key=value> --label team=DevOps --label app=test
    ```
    {: pre}

4. Verify that the worker pool and worker node have the `key=value` label that you assigned.
    *   To check worker pools:
        ```sh
        ibmcloud oc worker-pool get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
        ```
        {: pre}

    *   To check worker nodes:
        1. List the worker nodes in the worker pool and note the **Private IP**.
            ```sh
            ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
            ```
            {: pre}

        2. Review the **Labels** field of the output.
            ```sh
            oc describe node <worker_node_private_IP>
            ```
            {: pre}

            Example output for an added label (`app=test`):
            ```sh
            Labels:   app=test
            arch=amd64
            ...
            ```
            {: screen}

            Example output for a removed label (the `app=test` label is gone):
            ```sh
            Labels:   arch=amd64
            ...
            ```
            {: screen}            

5. **Optional**: To remove an individual label from a worker pool, you can run the `ibmcloud oc worker-pool label set` command with only the custom labels that you want to keep. To remove all custom labels from a worker pool, you can run the `ibmcloud oc worker-pool label rm` command.

    Do not remove the worker pool and worker node labels that are provided by default because these labels are required for worker pools to function properly. Remove only custom labels that you previously added.
    {: important}

    Example to keep only the `team: DevOps` and `app: test` labels and remove all other custom labels from a worker pool:
    ```sh
    ibmcloud oc worker-pool label set <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID> --label team=DevOps --label app=test
    ```
    {: pre}

    Example to remove all custom label from a worker pool:
    ```sh
    ibmcloud oc worker-pool label rm <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
    ```
    {: pre}

After you label your worker pool, you can use the [label in your app deployments](/docs/openshift?topic=openshift-openshift_apps#label) so that your workloads run on only these worker nodes, or [taints](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external} to prevent deployments from running on these worker nodes.




