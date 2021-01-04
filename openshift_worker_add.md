---

copyright:
  years: 2014, 2021
lastupdated: "2021-01-04"

keywords: openshift, roks, rhoks, rhos, clusters, worker nodes, worker pools, delete

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}



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

For bare metal worker pools, keep in mind that billing is monthly. If you resize up or down, it impacts your costs for the month.
{: tip}

Before you begin, make sure that you have the [**Operator** or **Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/openshift?topic=openshift-users#platform).

To resize the worker pool, change the number of worker nodes that the worker pool deploys in each zone:

1. Get the name of the worker pool that you want to resize.
    ```
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

2. Resize the worker pool by designating the number of worker nodes that you want to deploy in each zone. The minimum value is 2. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).
    ```
    ibmcloud oc worker-pool resize --cluster <cluster_name_or_ID> --worker-pool <pool_name>  --size-per-zone <number_of_workers_per_zone>
    ```
    {: pre}

3. Verify that the worker pool is resized.
    ```
    ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <pool_name>
    ```
    {: pre}

    Example output for a worker pool that is in two zones, `dal10` and `dal12`, and is resized to two worker nodes per zone:
    ```
    ID                                                 Public IP        Private IP      Machine Type      State    Status  Zone    Version
    kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w7   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal10   1.18.12
    kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w8   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal10   1.18.12
    kube-dal12-crb20b637238ea471f8d4a8b881aae4962-w9   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal12   1.18.12
    kube-dal12-crb20b637238ea471f8d4a8b881aae4962-w10  169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal12   1.18.12
    ```
    {: screen}

<br />


## Adding worker nodes in VPC clusters
{: #vpc_pools}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Add worker nodes to your VPC cluster.
{: shortdesc}

### Creating a new worker pool
{: #vpc_add_pool}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> You can add worker nodes to your VPC cluster by creating a new worker pool.
{: shortdesc}

Before you begin, make sure that you have the [**Operator** or **Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/openshift?topic=openshift-users#platform).

1. Retrieve the **VPC ID** and **Worker Zones** of your cluster and choose the zone where you want to deploy the worker nodes in your worker pool. You can choose any of the existing **Worker Zones** of your cluster, or add one of the [multizone metro locations](/docs/openshift?topic=openshift-regions-and-zones#zones) for the region that your cluster is in. You can list available zones by running `ibmcloud oc zone ls --provider vpc-classic` for Generation 1 compute or `ibmcloud oc zone ls --provider vpc-gen2` for Generation 2 compute.
   ```
   ibmcloud oc cluster get --cluster <cluster_name_or_ID>
   ```
   {: pre}

   Example output:
   ```
   ...
   VPC ID:        <VPC_ID>
   ...
   Worker Zones: us-south-1, us-south-2, us-south-3
   ```
   {: screen}

2. For each zone, note the ID of VPC subnet that you want to use for the worker pool. If you do not have a VPC subnet in the zone, [create a VPC subnet](/docs/vpc?topic=vpc-creating-a-vpc-using-cli#create-a-subnet-cli). VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256.
   ```
   ibmcloud oc subnets --zone <zone> --provider >vpc-gen2 --vpc-id <VPC_ID>
   ```
   {: pre}

3.  For each zone, review the [available flavors for worker nodes](/docs/openshift?topic=openshift-planning_worker_nodes#vm).

    ```
    ibmcloud oc flavors --zone <zone> --provider vpc-gen2
    ```
    {: pre}

4. Create a worker pool. Include the `--label` option to automatically label worker nodes that are in the pool with the label `key=value`. Include the `--vpc-id` option if the worker pool is the first in the cluster. For more options, see the [CLI documentation](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_pool_create_vpc_gen2).
     ```
     ibmcloud oc worker-pool create vpc-gen2 --name <name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_worker_nodes_min_2> [--label <key>=<value>] [--vpc-id]
     ```
     {: pre}

5. Verify that the worker pool is created.
   ```
   ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
   ```
   {: pre}

6. By default, adding a worker pool creates a pool with no zones. To deploy worker nodes in a zone, you must add the zones that you previously retrieved to the worker pool. If you want to spread your worker nodes across multiple zones, repeat this command for each zone.
   ```
   ibmcloud oc zone add vpc-gen2 --zone <zone> --subnet-id <subnet_id> --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name>
   ```
   {: pre}

7. Verify that worker nodes provision in the zone that you added. Your worker nodes are ready when the **State** changes from `provisioning` to `normal`.
   ```
   ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <pool_name>
   ```
   {: pre}

   Example output:
   ```
   ID                                                     Primary IP     Flavor   State          Status                                        Zone       Version   
   kube-<ID_string>-<cluster_name>-<pool_name>-00000002   10.xxx.xx.xxx   c2.2x4   provisioning   Infrastructure instance status is 'pending'   us-south-1   -   
   kube-<ID_string>-<cluster_name>-<pool_name>-00000003   10.xxx.xx.xxx   c2.2x4   normal   Ready   us-south-1   1.18.12_1511   
   ```
   {: screen}

### Adding a zone to a worker pool
{: #vpc_add_zone}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> You can span your VPC cluster across multiple zones within one region by adding a zone to your existing worker pool.
{: shortdesc}

When you add a zone to a worker pool, the worker nodes that are defined in your worker pool are provisioned in the new zone and considered for future workload scheduling. {{site.data.keyword.openshiftlong_notm}} automatically adds the `failure-domain.beta.kubernetes.io/region` label for the region and the `failure-domain.beta.kubernetes.io/zone` label for the zone to each worker node. The Kubernetes scheduler uses these labels to spread pods across zones within the same region.

If you have multiple worker pools in your cluster, add the zone to all of them so that worker nodes are spread evenly across your cluster.

Before you begin, make sure that you have the [**Operator** or **Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/openshift?topic=openshift-users#platform).

1. Get the **Location** of your cluster, and note the existing **Worker Zones** and **VPC ID**.
   ```
   ibmcloud oc cluster get --cluster <cluster_name_or_ID>
   ```
   {: pre}

   Example output:
   ```
   ...
   VPC ID:        <VPC_ID>
   Workers:       3
   Worker Zones:  us-south-1
   ...
   Location:      Dallas   
   ```
   {: screen}

2. List available zones for your cluster's location to see what other zones you can add.
   ```
   ibmcloud oc zone ls --provider vpc-gen2 | grep <location>
   ```
   {: pre}

3. List available VPC subnets for each zone that you want to add. If you do not have a VPC subnet in the zone, [create a VPC subnet](/docs/vpc?topic=vpc-creating-a-vpc-using-cli#create-a-subnet-cli). VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256. You cannot change the number of IPs that a VPC subnet has later.
   ```
   ibmcloud oc subnets --zone <zone> --provider vpc-gen2 --vpc-id <VPC_ID>
   ```
   {: pre}

4. List the worker pools in your cluster and note their names.
   ```
   ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
   ```
   {: pre}

5. Add the zone to your worker pool. Repeat this step for each zone that you want to add to your worker pool. If you have multiple worker pools, add the zone to all your worker pools so that your cluster is balanced in all zones. Include the `--worker-pool` flag for each worker pool.

   If you want to use different VPC subnets for different worker pools, repeat this command for each subnet and its corresponding worker pools. Any new worker nodes are added to the VPC subnets that you specify, but the VPC subnets for any existing worker nodes are not changed.
   {: tip}
     ```
     ibmcloud oc zone add vpc-gen2 --zone <zone> --subnet-id <subnet_id> --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name>
     ```
     {: pre}

6. Verify that the zone is added to your cluster. Look for the added zone in the **Worker Zones** field of the output. Note that the total number of workers in the **Workers** field has increased as new worker nodes are provisioned in the added zone.
  ```
  ibmcloud oc cluster get --cluster <cluster_name_or_ID>
  ```
  {: pre}

  Example output:
  ```
  Workers:       9
  Worker Zones:  us-south-1, us-south-2, us-south-3
  ```
  {: screen}

7. To expose apps with [Ingress](/docs/openshift?topic=openshift-ingress-about-roks4), you must [update the VPC load balancer that exposes the router](/docs/openshift?topic=openshift-cs_troubleshoot_debug_ingress#router-mzr-error) to include the subnet for the new zone in your cluster.


<br />

## Adding worker nodes in classic clusters
{: #classic_pools}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Add worker nodes to your classic cluster.
{: shortdesc}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Want to save on your classic worker node costs? [Create a reservation](/docs/openshift?topic=openshift-reservations) to lock in a discount over 1 or 3 year terms! Then, create your worker pool by using the reserved instances.
{: tip}

### Creating a new worker pool
{: #add_pool}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> You can add worker nodes to your classic cluster by creating a new worker pool.
{: shortdesc}

Before you begin, make sure that you have the [**Operator** or **Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/openshift?topic=openshift-users#platform).

1. Retrieve the **Worker Zones** of your cluster and choose the zone where you want to deploy the worker nodes in your worker pool. If you have a single zone cluster, you must use the zone that you see in the **Worker Zones** field. For multizone clusters, you can choose any of the existing **Worker Zones** of your cluster, or add one of the [multizone metro locations](/docs/openshift?topic=openshift-regions-and-zones#zones) for the region that your cluster is in. You can list available zones by running `ibmcloud oc zone ls`.
   ```
   ibmcloud oc cluster get --cluster <cluster_name_or_ID>
   ```
   {: pre}

   Example output:
   ```
   ...
   Worker Zones: dal10, dal12, dal13
   ```
   {: screen}

2. For each zone, list available private and public VLANs. Note the private and the public VLAN that you want to use. If you do not have a private or a public VLAN, the VLAN is automatically created for you when you add a zone to your worker pool.
   ```
   ibmcloud oc vlan ls --zone <zone>
   ```
   {: pre}

3.  For each zone, review the [available flavors for worker nodes](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes).

    ```
    ibmcloud oc flavors --zone <zone>
    ```
    {: pre}

4. Create a worker pool. For more options, see the [CLI documentation](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_create).  
   * The minimum number of worker nodes per zone is 2. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).
   * Include the `--label` option to automatically label worker nodes that are in the pool with the label `key=value`.
   * If you provision a bare metal or dedicated VM worker pool, specify `--hardware dedicated`.

   ```
   ibmcloud oc worker-pool create classic --name <pool_name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_workers_per_zone_min_2> [--label key=value]
   ```
   {: pre}

5. Verify that the worker pool is created.
   ```
   ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
   ```
   {: pre}

6. By default, adding a worker pool creates a pool with no zones. To deploy worker nodes in a zone, you must add the zones that you previously retrieved to the worker pool. If you want to spread your worker nodes across multiple zones, repeat this command for each zone.
  ```
  ibmcloud oc zone add classic --zone <zone> --cluster <cluster_name_or_ID> --worker-pool <pool_name> --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
  ```
  {: pre}

7. Verify that worker nodes provision in the zone that you added. Your worker nodes are ready when the status changes from **provision_pending** to **normal**.
   ```
   ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <pool_name>
   ```
   {: pre}

   Example output:
   ```
   ID                                                 Public IP        Private IP      Machine Type      State    Status  Zone    Version
   kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w7   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          provision_pending   Ready   dal10   1.18.12
   kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w8   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          provision_pending   Ready   dal10   1.18.12
   ```
   {: screen}

<br />

### Adding a zone to a worker pool
{: #add_zone}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> You can span your classic cluster across multiple zones within one region by adding a zone to your existing worker pool.
{: shortdesc}

When you add a zone to a worker pool, the worker nodes that are defined in your worker pool are provisioned in the new zone and considered for future workload scheduling. {{site.data.keyword.openshiftlong_notm}} automatically adds the `failure-domain.beta.kubernetes.io/region` label for the region and the `failure-domain.beta.kubernetes.io/zone` label for the zone to each worker node. The Kubernetes scheduler uses these labels to spread pods across zones within the same region.

If you have multiple worker pools in your cluster, add the zone to all of them so that worker nodes are spread evenly across your cluster.

Before you begin:
*  To add a zone to your worker pool, your worker pool must be in a [multizone-capable zone](/docs/openshift?topic=openshift-regions-and-zones#zones). If your worker pool is not in a multizone-capable zone, consider [creating a new worker pool](#add_pool).
*  Make sure that you have the [**Operator** or **Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/openshift?topic=openshift-users#platform).
*  In classic clusters, if you have multiple VLANs for your cluster, multiple subnets on the same VLAN, or a multizone classic cluster, you must enable a [Virtual Router Function (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf) for your IBM Cloud infrastructure account so your worker nodes can communicate with each other on the private network. To enable VRF, see [Enabling VRF](/docs/account?topic=account-vrf-service-endpoint#vrf). To check whether a VRF is already enabled, use the `ibmcloud account show` command. If you cannot or do not want to enable VRF, enable [VLAN spanning](/docs/vlans?topic=vlans-vlan-spanning#vlan-spanning). To perform this action, you need the **Network > Manage Network VLAN Spanning** [infrastructure permission](/docs/openshift?topic=openshift-users#infra_access), or you can request the account owner to enable it. To check whether VLAN spanning is already enabled, use the `ibmcloud oc vlan spanning get --region <region>` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vlan_spanning_get).

To add a zone with worker nodes to your worker pool:

1. List available zones and pick the zone that you want to add to your worker pool. The zone that you choose must be a multizone-capable zone.
   ```
   ibmcloud oc zone ls
   ```
   {: pre}

2. List available VLANs in that zone. If you do not have a private or a public VLAN, the VLAN is automatically created for you when you add a zone to your worker pool.
   ```
   ibmcloud oc vlan ls --zone <zone>
   ```
   {: pre}

3. List the worker pools in your cluster and note their names.
   ```
   ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
   ```
   {: pre}

4. Add the zone to your worker pool. If you have multiple worker pools, add the zone to all your worker pools so that your cluster is balanced in all zones.

    A private and a public VLAN must exist before you can add a zone to multiple worker pools. If you do not have a private and a public VLAN in that zone, add the zone to one worker pool first so that a private and a public VLAN is created for you. Then, you can add the zone to other worker pools by specifying the private and the public VLAN that was created for you.
    {: note}

   If you want to use different VLANs for different worker pools, repeat this command for each VLAN and its corresponding worker pools. Any new worker nodes are added to the VLANs that you specify, but the VLANs for any existing worker nodes are not changed.
   {: tip}
   ```
   ibmcloud oc zone add classic --zone <zone> --cluster <cluster_name_or_ID> -w <pool_name> [-w <pool2_name>] --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
   ```
   {: pre}

5. Verify that the zone is added to your cluster. Look for the added zone in the **Worker zones** field of the output. Note that the total number of workers in the **Workers** field has increased as new worker nodes are provisioned in the added zone.
  ```
  ibmcloud oc cluster get --cluster <cluster_name_or_ID>
  ```
  {: pre}

  Example output:
  ```
  Name:                           mycluster
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
  Version:                        1.18.12_1524
  Owner:                          owner@email.com
  Resource Group ID:              a8a12accd63b437bbd6d58fb6a462ca7
  Resource Group Name:            Default
  ```
  {: screen}

<br />

## Deprecated: Adding stand-alone worker nodes
{: #standalone}

If you have a cluster that was created before worker pools were introduced, you can use the deprecated commands to add stand-alone worker nodes.
{: deprecated}

If you have a cluster that was created after worker pools were introduced, you cannot add stand-alone worker nodes. Instead, you can [create a worker pool](#add_pool), [resize an existing worker pool](#resize_pool), or [add a zone to a worker pool](#add_zone) to add worker nodes to your cluster.
{: note}

1. List available zones and pick the zone where you want to add worker nodes.
   ```
   ibmcloud oc zone ls
   ```
   {: pre}

2. List available VLANs in that zone and note their ID.
   ```
   ibmcloud oc vlan ls --zone <zone>
   ```
   {: pre}

3. List available flavors in that zone.
   ```
   ibmcloud oc flavors --zone <zone>
   ```
   {: pre}

4. Add stand-alone worker nodes to the cluster. For bare metal flavors, specify `dedicated`.
   ```
   ibmcloud oc worker add --cluster <cluster_name_or_ID> --workers <number_of_worker_nodes> --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID> --flavor <flavor> --hardware <shared_or_dedicated>
   ```
   {: pre}

5. Verify that the worker nodes are created.
   ```
   ibmcloud oc worker ls --cluster <cluster_name_or_ID>
   ```
   {: pre}

<br />


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

  ```
  curl -fssl https://raw.githubusercontent.com/ibm-cloud-security/data-shield-reference-apps/master/scripts/sgx-driver-psw/config_openshift/create_openshift_config.sh | bash
  ```
  {: codeblock}

3. Create a daemon set to install the drivers and platform software on your SGX-capable worker nodes.

  ```
  oc create -f https://raw.githubusercontent.com/ibm-cloud-security/data-shield-reference-apps/master/scripts/sgx-driver-psw/install_sgx/deployment_install_sgx_openshift.yaml
  ```
  {: codeblock}

4. Verify that the drivers and platform software were installed by running the following command to check for a pod that begins with `sgx-installer`.

  ```
  oc get pods
  ```
  {: codeblock}

5. Get the logs for your `sgx-installer` pod to verify that you see the messages `SGX driver installed` and `PSW installed`.

  ```
  oc logs <name_of_SGX_installer_pod>
  ```

6. Now that the drivers and platform software are installed, remove the daemon set.

  ```
  oc delete daemonset sgx-installer
  ```
  {: codeblock}

7. Delete the security context and service account that you created.

  ```
  oc delete scc sgx-admin
  oc delete serviceaccount sgx-admin
  ```
  {: codeblock}

Now, you can develop your confidential computing app to use the enclave for sensitive data.

To uninstall the drivers and platform software, you can follow the same steps, but with the following installation command: `oc create -f https://raw.githubusercontent.com/ibm-cloud-security/data-shield-reference-apps/master/scripts/sgx-driver-psw/uninstall_sgx/deployment_uninstall_sgx_openshift.yaml`
{: note}

<br />



## Adding tags to existing clusters
{: #cluster_tags}


You can assign a tag to {{site.data.keyword.openshiftlong_notm}} clusters to help manage your {{site.data.keyword.cloud_notm}} resources. For example, you might add `key:value` tags to your cluster and other cloud resources so that your billing department track resources, such as `costctr:1234`. Tags are visible account-wide. For more information, see [Working with tags](/docs/account?topic=account-tag).
{: shortdesc}

Tags are not the same thing as Kubernetes labels. [Kubernetes labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/){: external} are `key:value` pairs that can be used as selectors for the resources that are in your cluster, such as [adding a label to worker pool](#worker_pool_labels) to [deploy an app to only certain worker nodes](/docs/openshift?topic=openshift-deploy_app#node_affinity). Tags are an {{site.data.keyword.cloud_notm}} tool that you can use to filter your {{site.data.keyword.cloud_notm}} resources, such as clusters, storage devices, or {{site.data.keyword.watson}} services.
{: note}

Do not include personal information in your tags. Learn more about [securing your personal information](/docs/openshift?topic=openshift-security#pi) when you work with Kubernetes resources.
{: important}

Choose among the following options:

*   [Create a cluster in the console](/docs/openshift?topic=openshift-clusters) with a tag. You cannot create a cluster with a tag in the CLI.
*   Add tags to an existing cluster in the console or CLI.

| Adding tags to clusters with the console. |
|:-----------------|
| <p><ol><li>Log in to the [**{{site.data.keyword.cloud_notm}} clusters** console](https://cloud.ibm.com/kubernetes/clusters){: external}.</li><li>Select a cluster with existing tags.</li><li>Next to the cluster name and status, click the **Edit tags** pencil icon.<p class="note">If your cluster does not have any existing tags, you do not have an **Edit tags** pencil icon. Instead, use the [resource list](/docs/account?topic=account-tag#add-remove) or CLI.</p></li><li>Enter the tag that you want to add to your cluster. To assign a key-value pair, use a colon such as `costctr:1234`.</li></ol></p> |
{: caption="Adding tags to clusters with the console." caption-side="top"}
{: #tags-1}
{: tab-title="Console"}
{: tab-group="tags"}
{: class="simple-tab-table"}

| Adding tags to clusters with the CLI. |
|:-----------------|
| <p><ol><li>Log in to the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/reference/ibmcloud?topic=cli-ibmcloud_cli#ibmcloud_login).<pre class="pre"><code>ibmcloud login [--sso]</code></pre></li><li>[Tag your cluster](/docs/cli/reference/ibmcloud?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_tag_attach). Replace the `--resource-name` with the name of your cluster. To list available clusters, run `ibmcloud oc cluster ls`. If you want to check your existing tags so as not to duplicate any, run `ibmcloud resource tags`.<pre class="pre"><code>ibmcloud resource tag-attach --resource-name <cluster_name> --tag-names &lt;tag1,tag2&gt;</code></pre><p class="note">If you have more than one resource of the same name in your {{site.data.keyword.cloud_notm}} account, the error message lists the resource CRNs and details, and instructs you to try again with the `--resource-id` flag.</p></li></ol></p> |
{: caption="Adding tags to clusters with the CLI." caption-side="top"}
{: #tags-2}
{: tab-title="CLI"}
{: tab-group="tags"}
{: class="simple-tab-table"}

<br />

## Adding labels to existing worker pools
{: #worker_pool_labels}

You can assign a worker pool a label when you [create the worker pool](#add_pool), or later by following these steps. After a worker pool is labeled, all existing and subsequent worker nodes get this label. You might use labels to deploy specific workloads only to worker nodes in the worker pool, such as [edge nodes for load balancer network traffic](/docs/openshift?topic=openshift-edge).
{: shortdesc}

Do not include personal information in your labels. Learn more about [securing your personal information](/docs/openshift?topic=openshift-security#pi) when you work with Kubernetes resources.
{: important}

Before you begin: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1.  List the worker pools in your cluster.
    ```
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}
2.  To label the worker pool with a `key=value` label, use the [POST worker pool labels API](https://containers.cloud.ibm.com/global/swagger-global-api/#/v2/v2SetWorkerPoolLabels){: external}. When you set a worker pool label, all the existing custom labels are replaced. Format the body of the request as in the following JSON example. <p class="important">You can also rename an existing label by assigning the same key a new value. However, do not modify the worker pool or worker node labels that are provided by default because these labels are required for worker pools to function properly. Modify only custom labels that you previously added. To list existing worker node labels, run `oc describe node <worker_node_private_IP>`.</p>

    Example to set `<key>: <value>` as the only custom label in the worker pool.
    ```
    {
      "labels": {"<key>":"<value>"},
      "state": "labels"
    }
    ```
    {: codeblock}

    Example to set `<key>: <value>` as a new custom label in a worker pool with existing labels `team: DevOps` and `app: test`.
    ```
    {
      "labels": {"<key>":"<value>","team":"DevOps","app":"test"},
      "state": "labels"
    }
    ```
    {: codeblock}

3.  **Optional**: To remove a label from a worker pool, use the [POST worker pool labels API](https://containers.cloud.ibm.com/global/swagger-global-api/#/v2/v2SetWorkerPoolLabels){: external} again with the label's key field included but the value field empty. Remember that when you set a label, all existing custom labels are replaced. If you want to keep existing custom labels, include these labels in the body.<p class="important">Do not remove the worker pool and worker node labels that are provided by default because these labels are required for worker pools to function properly. Remove only custom labels that you previously added.</p>

    Example to remove a label. All other custom labels are also removed.
    ```
    {
      "labels": {"<key>":""},
      "state": "labels"
    }
    ```
    {: codeblock}

    Example to remove a `<key>` label but keep other custom labels `team: DevOps` and `app: test`.
    ```
    {
      "labels": {"<key>":"","team":"DevOps","app":"test"},
      "state": "labels"
    }
    ```
    {: codeblock}

4.  Verify that the worker pool and worker node have the `key=value` label that you assigned.
    *   To check worker pools:
        ```
        ibmcloud oc worker-pool get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
        ```
        {: pre}
    *   To check worker nodes:
        1.  List the worker nodes in the worker pool and note the **Private IP**.
            ```
            ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
            ```
            {: pre}
        2.  Review the **Labels** field of the output.
            ```
            oc describe node <worker_node_private_IP>
            ```
            {: pre}

            Example output for an added label (`app=test`):
            ```
            Labels:   app=test
                      arch=amd64
                      ...
            ```
            {: screen}

            Example output for a removed label (the `app=test` label is gone):
            ```
            Labels:   arch=amd64
                      ...
            ```
            {: screen}

After you label your worker pool, you can use the [label in your app deployments](/docs/openshift?topic=openshift-openshift_apps#label) so that your workloads run on only these worker nodes, or [taints](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external} to prevent deployments from running on these worker nodes.


