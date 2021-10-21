---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-21"

keywords: openshift, roks, rhos, rhoks, vlan

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Changing service endpoints or VLAN connections in {{site.data.keyword.openshiftshort}} 3.11
{: #cs_network_cluster}

After you initially set up your network when you [create a cluster](/docs/containers?topic=containers-clusters), you can change the service endpoints that your cluster master is accessible through or change the VLAN connections for your worker nodes.
{: shortdesc}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) The content on this page is specific to **classic clusters only**. For information about VPC clusters, see [Understanding network basics of VPC clusters](/docs/containers?topic=containers-vpc-subnets).
{: note}


<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> The content on this page is specific to **classic clusters that run {{site.data.keyword.openshiftshort}} 3.11 only**. In clusters that run {{site.data.keyword.openshiftshort}} 3.11, you must enable the public cloud service endpoint during cluster creation, and you cannot disable it later. You can later enable the private cloud service endpoint. In clusters that run version 4, you choose the public cloud service endpoint only or public and private cloud service endpoints during cluster creation, and you cannot later change the cloud service endpoints.
{: important}



## Setting up the private cloud service endpoint
{: #set-up-private-se}

Enable the private cloud service endpoint for your cluster.
{: shortdesc}

The private cloud service endpoint makes your Kubernetes master privately accessible. Your worker nodes and your authorized cluster users can communicate with the Kubernetes master over the private network. To determine whether you can enable the private cloud service endpoint, see [Worker-to-master and user-to-master communication](/docs/openshift?topic=openshift-plan_clusters#workeruser-master). Note that you cannot disable the private cloud service endpoint after you enable it.

1. Enable [VRF](/docs/account?topic=account-vrf-service-endpoint#vrf) in your IBM Cloud infrastructure account. To check whether a VRF is already enabled, use the `ibmcloud account show` command.
2. [Enable your {{site.data.keyword.cloud_notm}} account to use service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint).
3. Enable the private cloud service endpoint.
    ```sh
    ibmcloud oc cluster master private-service-endpoint enable --cluster <cluster_name_or_ID>
    ```
    {: pre}

4. Refresh the Kubernetes master API server to use the private cloud service endpoint. You can follow the prompt in the CLI, or manually run the following command. It might take several minutes for the master to refresh.
    ```sh
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

5. [Create a configmap](/docs/containers?topic=containers-update#worker-up-configmap) to control the maximum number of worker nodes that can be unavailable at a time in your cluster. When you update your worker nodes, the configmap helps prevent downtime for your apps as the apps are rescheduled orderly onto available worker nodes.
6. Update all the worker nodes in your cluster to pick up the private cloud service endpoint configuration.

    By issuing the update command, the worker nodes are reloaded to pick up the service endpoint configuration. If no worker update is available, you must [reload the worker nodes manually](/docs/containers?topic=containers-kubernetes-service-cli). If you reload, be sure to cordon, drain, and manage the order to control the maximum number of worker nodes that are unavailable at a time.
    {: important}
    
    ```sh
    ibmcloud oc worker update --cluster <cluster_name_or_ID> --worker <worker1,worker2>
    ```
    {: pre}

7. If the cluster is in an environment behind a firewall:
    - [Allow your authorized cluster users to run `kubectl` commands to access the master through the private cloud service endpoint.](/docs/openshift?topic=openshift-firewall#firewall_kubectl)
    - [Allow outbound network traffic to the private IPs](/docs/openshift?topic=openshift-firewall#firewall_outbound) for infrastructure resources and for the {{site.data.keyword.cloud_notm}} services that you plan to use.


## Setting up the public cloud service endpoint
{: #set-up-public-se}

Enable the public cloud service endpoint for your cluster.
{: shortdesc}

Your cluster must have a public cloud service endpoint on classic infrastructre. For a cluster with only a private cloud service endpoint, create a VPC cluster instead.
{: important}

The public cloud service endpoint makes your Kubernetes master publicly accessible. Your worker nodes and your authorized cluster users can securely communicate with the Kubernetes master over the public network. For more information, see [Worker-to-master and user-to-master communication](/docs/openshift?topic=openshift-plan_clusters#internet-facing).

### Steps to enable the public cloud service endpoint
{: #steps-set-up-public}

If you previously disabled the public endpoint, you can re-enable it.
1. Enable the public cloud service endpoint.
    ```sh
    ibmcloud oc cluster master public-service-endpoint enable --cluster <cluster_name_or_ID>
    ```
    {: pre}

2. Refresh the Kubernetes master API server to use the public cloud service endpoint. You can follow the prompt in the CLI, or manually run the following command. It might take several minutes for the master to refresh.
    ```sh
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

3. [Create a configmap](/docs/containers?topic=containers-update#worker-up-configmap) to control the maximum number of worker nodes that can be unavailable at a time in your cluster. When you update your worker nodes, the configmap helps prevent downtime for your apps as the apps are rescheduled orderly onto available worker nodes.
4. Update all the worker nodes in your cluster to remove the public cloud service endpoint configuration.<p class="important">By issuing the update command, the worker nodes are reloaded to pick up the service endpoint configuration. If no worker update is available, you must reload the worker nodes manually with the `ibmcloud oc worker reload` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload). If you reload, be sure to cordon, drain, and manage the order to control the maximum number of worker nodes that are unavailable at a time.</p>
    ```sh
    ibmcloud oc worker update --cluster <cluster_name_or_ID> --worker <worker1,worker2>
    ```
    {: pre}




## Changing your worker node VLAN connections
{: #change-vlans}



When you create a cluster, you choose the public and private VLANs to connect your worker nodes to. Your worker nodes are part of worker pools, which store networking metadata that includes the VLANs to use to provision future worker nodes in the pool. You might want to change your cluster's VLAN connectivity setup later, such as if the worker pool VLANs in a zone run out of capacity, and you need to provision a new VLAN for your cluster worker nodes to use.

Trying to change the service endpoint for master-worker communication instead? Check out the topics to set up the [private](#set-up-private-se) service endpoint.
{: tip}



Before you begin [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To change the VLANs that a worker pool uses to provision worker nodes.

1. List the names of the worker pools in your cluster.
    ```sh
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

2. Determine the zones for one of the worker pools. In the output, look for the **Zones** field.
    ```sh
    ibmcloud oc worker-pool get --cluster <cluster_name_or_ID> --worker-pool <pool_name>
    ```
    {: pre}

3. For each zone that you found in the previous step, get an available public and private VLAN that are compatible with each other.

    1. Check the available public and private VLANs that are listed under **Type** in the output.
        ```sh
        ibmcloud oc vlan ls --zone <zone>
        ```
        {: pre}

    2. Check that the public and private VLANs in the zone are compatible. To be compatible, the **Router** must have the same pod ID. In this example output, the **Router** pod IDs match: `01a` and `01a`. If one pod ID was `01a` and the other was `02a`, you cannot set these public and private VLAN IDs for your worker pool.
        ```
        ID        Name   Number   Type      Router         Supports Virtual Workers
        229xxxx          1234     private   bcr01a.dal12   true
        229xxxx          5678     public    fcr01a.dal12   true
        ```
        {: screen}

    3. If you need to order a new public or private VLAN for the zone, you can order in the [{{site.data.keyword.cloud_notm}} console](/docs/vlans?topic=vlans-ordering-premium-vlans#ordering-premium-vlans), or use the following command. Remember that the VLANs must be compatible, with matching **Router** pod IDs as in the previous step. If you are creating a pair of new public and private VLANs, they must be compatible with each other.
        ```sh
        ibmcloud sl vlan create -t [public|private] -d <zone> -r <compatible_router>
        ```
        {: pre}

    4. Note the IDs of the compatible VLANs.

4. Set up a worker pool with the new VLAN network metadata for each zone. You can create a new worker pool, or modify an existing worker pool.

    - **Create a new worker pool**: See [adding worker nodes by creating a new worker pool](/docs/openshift?topic=openshift-add_workers#add_pool).

    - **Modify an existing worker pool**: Set the worker pool's network metadata to use the VLAN for each zone. Worker nodes that were already created in the pool continue to use the previous VLANs, but new worker nodes in the pool use new VLAN metadata that you set.
        ```sh
        ibmcloud oc zone network-set --zone <zone> --cluster <cluster_name_or_ID> --worker-pool <pool_name> --private-vlan <private_vlan_id> --public-vlan <public_vlan_id>
        ```
        {: pre}

5. Add worker nodes to the worker pool by resizing the pool.
    ```sh
    ibmcloud oc worker-pool resize --cluster <cluster_name_or_ID> --worker-pool <pool_name> --size-per-zone <number_of_workers_per_zone>
    ```
    {: pre}

    If you want to remove worker nodes that use the previous network metadata, change the number of workers per zone to double the previous number of workers per zone. Later in these steps, you can cordon, drain, and remove the previous worker nodes.
    {: tip}

6. Verify that new worker nodes are created with **Public IP** and **Private IP** addresses in the output.
    ```sh
    ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <pool_name>
    ```
    {: pre}

7. Optional: Remove the worker nodes with the previous network metadata from the worker pool.
    1. In the output of the previous step, note the **ID** of the worker nodes that you want to remove from the worker pool.
    2. Remove the worker node.
        ```sh
        ibmcloud oc worker rm --cluster <cluster_name_or_ID> --worker <worker_name_or_ID>
        ```
        {: pre}

    3. Verify that the worker node is removed.
        ```sh
        ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <pool_name>
        ```
        {: pre}

    4. Rebalance the worker pool.
        ```sh
        ibmcloud oc worker-pool rebalance --cluster <cluster_name_or_ID> --worker-pool <pool_name>
        ```
        {: pre}

8. Optional: You can repeat steps 2 - 7 for each worker pool in your cluster. After you complete these steps, all worker nodes in your cluster are set up with the new VLANs.

9. Move networking services to the new VLANs. The networking services in your cluster are still bound to the old VLAN because their IP addresses are from a subnet on that VLAN.
    - Routers: Because routers cannot be moved across VLANs, you can instead [create router services on the new VLANs and delete router services on the old VLANs](/docs/openshift?topic=openshift-openshift_routes#migrate-router-vlan-classic).
    - Ingress ALBs ({{site.data.keyword.openshiftshort}} version 3.11 only): Because ALBs cannot be moved across VLANs, you can instead [create ALBs on the new VLANs and disable ALBs on the old VLANs](/docs/containers?topic=containers-ingress-types#migrate-alb-vlan).

10. Optional: If you no longer need the subnets on the old VLANs, you can [remove them](/docs/openshift?topic=openshift-subnets#remove-subnets).




