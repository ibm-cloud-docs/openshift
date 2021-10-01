---

copyright:
  years: 2014, 2021
lastupdated: "2021-10-01"

keywords: openshift, satellite, distributed cloud, on-prem, hybrid

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

  

# Creating {{site.data.keyword.openshiftshort}} clusters in {{site.data.keyword.satelliteshort}}
{: #satellite-clusters}

You can create {{site.data.keyword.openshiftlong}} clusters in an {{site.data.keyword.satellitelong}} location, and use the hosts of your own infrastructure that you added to your location as the worker nodes for the cluster.
{: shortdesc}

## Prerequisites
{: #satcluster-prereqs}

Before you can create clusters on your own infrastructure, you must set up an {{site.data.keyword.satellitelong_notm}} location.
{: shortdesc}

1. [Create an {{site.data.keyword.satellitelong_notm}} location](/docs/satellite?topic=satellite-locations#location-create).
2. [Set up the location control plane](/docs/satellite?topic=satellite-locations#setup-control-plane).
3. [Attach at least 3 hosts to your location](/docs/satellite?topic=satellite-hosts#attach-hosts) to use as the worker nodes for your {{site.data.keyword.openshiftlong_notm}} cluster.



## Creating {{site.data.keyword.openshiftshort}} clusters on {{site.data.keyword.satelliteshort}} from the console
{: #satcluster-create-console}

Use the {{site.data.keyword.cloud_notm}} console to create your {{site.data.keyword.openshiftshort}} clusters on your {{site.data.keyword.satelliteshort}} infrastructure.
{: shortdesc}

1. [Complete the prerequisite steps](#satcluster-prereqs).
2. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click **Create**.
3. In the **Infrastructure** section, select **{{site.data.keyword.satelliteshort}}**.
4. In the **OCP entitlement** section, specify an existing OCP entitlement for the worker nodes in this cluster by providing your [{{site.data.keyword.redhat_full}} account pull secret ![External link icon](../icons/launch-glyph.svg "External link icon")](https://console.redhat.com/openshift/install/pull-secret) as a file or in raw JSON format. The cluster also uses this pull secret to download {{site.data.keyword.openshiftshort}} images from your own {{site.data.keyword.redhat_notm}} account.
5. In the **Location** section, select the {{site.data.keyword.satelliteshort}} location where you want to create the cluster. Make sure that the location that you select is in a **Normal** state.
6. In the **Worker pools** section, configure the details for your default worker pool.
    1. Select the **Satellite zones** that {{site.data.keyword.satelliteshort}} uses to evenly assign hosts across zones that represent zones in your underlying infrastructure provider. Generally, create your worker pool across 3 zones for high availability.
    2. Request the **vCPU**, **Memory (GB)**, and number of **Worker nodes per zone** that you want to create the worker pool with. {{site.data.keyword.satelliteshort}} can automatically assign available hosts to the worker pool to fulfill your request. Generally, select at least 1 worker node per zone for a total of 3 worker nodes in your cluster.
7. In the **{{site.data.keyword.satelliteshort}} Config** section, decide whether to enable cluster admin access for {{site.data.keyword.satelliteshort}} Config. If you do not grant {{site.data.keyword.satelliteshort}} Config access, you cannot later use the {{site.data.keyword.satelliteshort}} Config functionality to view or deploy Kubernetes resources for your clusters.If you want to enable access later, you can [create custom RBAC roles for {{site.data.keyword.satelliteshort}} Config](/docs/satellite?topic=satellite-setup-clusters-satconfig#setup-clusters-satconfig-access).
8. For the **Resource details**, enter a **Cluster name** and any [{{site.data.keyword.cloud_notm}} tags](/docs/account?topic=account-tag) that you want to associate with your cloud resource. The cluster name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer.
9. Click **Create**. When you create the cluster, the cluster master is automatically created in your {{site.data.keyword.satelliteshort}} location control plane, and your worker pool is automatically assigned available hosts that match your worker node request.
10. Wait for the cluster to reach a **Normal** state.

    If you do not have any available and matching hosts in your {{site.data.keyword.satelliteshort}} location, the cluster is still created but enters a **Warning** state. [Attach hosts](/docs/satellite?topic=satellite-hosts#attach-hosts) to your {{site.data.keyword.satelliteshort}} location so that hosts can be assigned as worker nodes to the worker pool. If the hosts are not automatically assigned, you can also manually [assign {{site.data.keyword.satelliteshort}} hosts to your cluster](/docs/satellite?topic=satellite-hosts#host-assign). Ensure that hosts are assigned as worker nodes in each zone of your default worker pool.
    {: note}

11. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, verify that your cluster reaches a **Normal** state.
12. [Access your cluster](/docs/openshift?topic=openshift-access_cluster#access_cluster_sat) to access the {{site.data.keyword.openshiftshort}} web console or to run `oc` and `kubectl` commands from the CLI. If you enabled {{site.data.keyword.satelliteshort}} Config access, you must complete this step to synchronize the permissions.

    If your location hosts have private network connectivity only, or if you use Amazon Web Services, Google Cloud Platform, or Microsoft Azure hosts, you must be connected to your hosts' private network, such as through VPN access, to connect to your cluster and access the {{site.data.keyword.openshiftshort}} web console. Alternatively, if your hosts have public network connectivity, you can test access to your cluster by changing your cluster's and location's DNS records to [use your hosts' public IP addresses](/docs/openshift?topic=openshift-access_cluster#sat_public_access).
    {: note}

13. Optional: [Set up the internal container image registry](#satcluster-internal-registry).



## Creating {{site.data.keyword.openshiftshort}} clusters on {{site.data.keyword.satelliteshort}} from the CLI
{: #satcluster-create-cli}

Use the {{site.data.keyword.satelliteshort}} CLI to create your {{site.data.keyword.openshiftshort}} clusters on your {{site.data.keyword.satelliteshort}} infrastructure.
{: shortdesc}

Before you begin, [install the {{site.data.keyword.satelliteshort}} CLI plug-in](/docs/satellite?topic=satellite-setup-cli).

To create the cluster in a {{site.data.keyword.satelliteshort}} location, you must use {{site.data.keyword.openshiftshort}} version 4.5 or later. 
{: note}

1. [Complete the prerequisite steps](#satcluster-prereqs).
2. Verify that your location is in a **Normal** state. The location is in a **Normal** state when you successfully created the {{site.data.keyword.satelliteshort}} control plane and all hosts that you use for the control plane are in a healthy state.
    ```
    ibmcloud sat location ls
    ```
    {: pre}

    Example output

    ```sh
    Retrieving locations...
    OK
    Name         ID                     Status            Ready   Created      Hosts (used/total)   Managed From   
    mylocation   brhtfum2015a6mgqj16g   normal            yes     4 days ago   3 / 6                Dallas   
    ```
    {: screen}

3. Create an {{site.data.keyword.openshiftshort}} cluster in your {{site.data.keyword.satelliteshort}} location. Specify {{site.data.keyword.openshiftshort}} version 4.5 or later. When you create the cluster, the cluster master is automatically created in your {{site.data.keyword.satelliteshort}} control plane. 

    * To ensure that hosts are automatically assigned as worker nodes in the default worker pool of your cluster, specify those hosts' labels in the `--host-label` flags, and specify the number of worker nodes per zone in the `--workers` flag. 
    * To enable cluster admin access for {{site.data.keyword.satelliteshort}} Config, include the `--enable-admin-agent` flag. If you do not grant {{site.data.keyword.satelliteshort}} Config access, you cannot later use the {{site.data.keyword.satelliteshort}} Config functionality to view or deploy Kubernetes resources for your clusters. If you want to enable access later, you can [create custom RBAC roles for {{site.data.keyword.satelliteshort}} Config](/docs/satellite?topic=satellite-setup-clusters-satconfig#setup-clusters-satconfig-access).
    * For more information about this command's options, see the [CLI reference documentation](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-satellite).

    ```sh
    ibmcloud oc cluster create satellite --location <location_name_or_ID> --name <cluster_name> --pull-secret <secret> --version 4.7_openshift [--enable-admin-agent] [--host-label LABEL ...] [--pod-subnet SUBNET] [-q] [--service-subnet SUBNET] [--workers <workers_per_zone>] [--zone <zone_name>]
    ```
    {: pre}

    Example output

    ```sh
    Creating cluster...
    OK
    Cluster created with ID brkhsd220b6ktv7sjl50
    ```
    {: screen}

4. Wait for the cluster to reach a **Warning** state. The **Warning** state indicates that the cluster master is fully deployed, but no worker nodes could be detected in the cluster.
    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

    Example output

    ```sh
    OK
    Name                ID                     State     Created          Workers   Location           Version                 Resource Group Name   Provider   
    satcluster          brkhsd220b6ktv7sjl50   warning   12 minutes ago   0         mylocation         4.5.23_1525_openshift   Default               satellite  
    ```
    {: screen}

5. Make sure that hosts are assigned as worker nodes to the cluster.
    * **Autoassignment**: If you included `--host-labels` when you created the cluster and you have available hosts with matching labels in your {{site.data.keyword.satelliteshort}} location, the worker nodes are automatically assigned to the cluster. If you do not have any available and matching hosts, the cluster is still created but enters a **Warning** state. [Attach hosts](/docs/satellite?topic=satellite-hosts#attach-hosts) to your {{site.data.keyword.satelliteshort}} location so that hosts can be assigned as worker nodes to the worker pool. If the hosts are not automatically assigned, you can also manually [assign {{site.data.keyword.satelliteshort}} hosts to your cluster](/docs/satellite?topic=satellite-hosts#host-assign).
    * **Manual assignment**: [Assign {{site.data.keyword.satelliteshort}} hosts to your cluster](/docs/satellite?topic=satellite-hosts#host-assign-cli). After the hosts successfully bootstrap, the hosts function as the worker nodes for your cluster to run {{site.data.keyword.openshiftshort}} workloads. Generally, assign at least 3 hosts as worker nodes in your cluster.

6. Verify that your cluster reaches a **normal** state.
    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

    Example output

    ```sh
    OK
    Name         ID                     State    Created        Workers   Location     Version                 Resource Group Name   Provider   
    satcluster   brkhsd220b6ktv7sjl50   normal   2 hours ago    3         mylocation   4.3.23_1525_openshift   Default               satellite   
    ```
    {: screen}

7. [Access your cluster](/docs/openshift?topic=openshift-access_cluster#access_cluster_sat) to run `oc` and `kubectl` commands or access the {{site.data.keyword.openshiftshort}} web console. If you enabled {{site.data.keyword.satelliteshort}} Config access, you must complete this step to synchronize the permissions.

    If your location hosts have private network connectivity only, or if you use Amazon Web Services, Google Cloud Platform, or Microsoft Azure hosts, you must be connected to your hosts' private network, such as through VPN access, to connect to your cluster and access the {{site.data.keyword.openshiftshort}} web console. Alternatively, if your hosts have public network connectivity, you can test access to your cluster by changing your cluster's and location's DNS records to [use your hosts' public IP addresses](/docs/openshift?topic=openshift-access_cluster#sat_public_access).
    {: note}

8. Optional: [Set up the internal container image registry](#satcluster-internal-registry).

After you [access your cluster](/docs/openshift?topic=openshift-access_cluster#access_cluster_sat) and run `oc get nodes` or `oc describe node <worker_node>`, you might see that the worker nodes have `master,worker` roles. In OpenShift Container Platform clusters, operators use the master role as a `nodeSelector` so that OCP can deploy default components that are controlled by operators, such as the internal registry, in your cluster. The {{site.data.keyword.satelliteshort}} hosts that you assigned to your cluster function as worker nodes only, and no master node processes, such as the API server or Kubernetes scheduler, run on your worker nodes.
{: note}



## Accessing and working with your {{site.data.keyword.openshiftshort}} clusters
{: #satcluster-access}

After you created your {{site.data.keyword.openshiftshort}} cluster, you can use the capabilities in {{site.data.keyword.openshiftlong_notm}} to work with your cluster.
{: shortdesc}

Review common tasks that you might be interested in:

- [Accessing {{site.data.keyword.openshiftshort}} clusters on {{site.data.keyword.satelliteshort}}](/docs/openshift?topic=openshift-access_cluster#access_cluster_sat)
- [Assigning cluster access](/docs/openshift?topic=openshift-users)



## Setting up the internal container image registry
{: #satcluster-internal-registry}

By default, the internal registry does not run in your {{site.data.keyword.satelliteshort}} cluster because no backing storage is set up for the internal registry. Review the following options to set up the internal registry.
{: shortdesc}

*  **Non-persistent data on the worker node**: See [Storing images in the worker node empty directory](/docs/openshift?topic=openshift-registry#emptydir_internal_registry).
*  **Persistent data in {{site.data.keyword.cos_full_notm}}**: See the resolution steps in [Cluster create error about cloud object storage bucket](/docs/openshift?topic=openshift-ts_cos_bucket_cluster_create).

By default, the [image registry operator management state](https://docs.openshift.com/container-platform/4.7/registry/configuring-registry-operator.html#registry-operator-configuration-resource-overview_configuring-registry-operator){: external} is set to `Unmanaged`. After you change the storage section in the configmap to use a different solution such as the `emptyDir`, you must update the management state to `Managed`. Then, the operator creates the internal registry pod. Use the following command: `oc patch configs.imageregistry.operator.openshift.io/cluster --type merge -p '{"spec":{"managementState":"Managed"}}'`
{: note}



## Managing {{site.data.keyword.satelliteshort}} worker pools
{: #satcluster-worker-pools-sat}

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
 cluster ls --provider satellite
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

* When host autoassignment is enabled, {{site.data.keyword.satelliteshort}} automatically assigns availabe hosts to the worker pool, as long as the host labels match the host labels of the worker pool. If no hosts are available, [attach more hosts](/docs/satellite?topic=satellite-hosts#attach-hosts) with matching labels to the {{site.data.keyword.satelliteshort}} location.
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



## Exposing apps
{: #satcluster-expose-apps}

Several options exist to securely expose apps to traffic requests from the public network, from resources that are connected to your hosts' private network, or from resources in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Although these options include services that are available in standard {{site.data.keyword.openshiftshort}} clusters, the implementation of these services is different in {{site.data.keyword.openshiftshort}} clusters that were created on {{site.data.keyword.satelliteshort}}-provided infrastructure. For example, no load balancer services are created for the {{site.data.keyword.openshiftshort}} router in your cluster. For a list of app exposure options and steps to configure them, see [Exposing apps in {{site.data.keyword.satelliteshort}} clusters](/docs/openshift?topic=openshift-sat-expose-apps).

## Storing application data in persistent storage
{: #satcluster-storage}

Unlike standard {{site.data.keyword.openshiftshort}} clusters that are created on {{site.data.keyword.cloud_notm}} infrastructure, your {{site.data.keyword.satelliteshort}} clusters do not come installed with a storage driver that provides Kubernetes storage classes that are ready to use with Kubernetes persistent volumes for your apps. However, you can install your own storage driver to set up your apps to save their data in a backing storage device. Review the following common options.
{: shortdesc}

*  Install the [{{site.data.keyword.cos_full_notm}} plug-in](/docs/openshift?topic=openshift-object_storage) in your cluster.
*  Manually set up a storage operator that uses a backing storage provider in your cluster. For more information, see the storage operator provider documentation.
*  Use local storage on the host, such as the [local storage operator](https://docs.openshift.com/container-platform/4.7/storage/persistent_storage/persistent-storage-local.html){: external}.



## Removing {{site.data.keyword.satelliteshort}} worker nodes or clusters
{: #satcluster-rm}

When you remove {{site.data.keyword.openshiftshort}} clusters or worker nodes in a cluster, the hosts that provide the compute capacity for your worker nodes are not automatically deleted. Instead, the hosts remain attached to your {{site.data.keyword.satelliteshort}} location, but require you to reload the host to be able to reassign the hosts to other {{site.data.keyword.satelliteshort}} resources.
{: shortdesc}

1. Back up any data that runs in the worker node or cluster that you want to save. For example, you might save a copy of all the data in your cluster and upload these files to a persistent storage solution, such as {{site.data.keyword.cos_full_notm}}.
    ```sh
    oc get all --all-namespaces -o yaml
    ```
    {: pre}

2. Get the **Worker ID** of each host in your cluster.
    ```
    ibmcloud sat host ls --location <satellite_location_name_or_ID>
    ```
    {: pre}

    Example output

    ```sh
    Retrieving hosts...
    OK
    Name              ID                     State      Status   Cluster          Worker ID                                                 Worker IP       
    machine-name-1    aaaaa1a11aaaaaa111aa   assigned   Ready    infrastructure   sat-virtualser-4d7fa07cd3446b1f9d8131420f7011e60d372ca2   169.xx.xxx.xxx       
    machine-name-2    bbbbbbb22bb2bbb222b2   assigned   Ready    infrastructure   sat-virtualser-9826f0927254b12b4018a95327bd0b45d0513f59   169.xx.xxx.xxx       
    machine-name-3    ccccc3c33ccccc3333cc   assigned   Ready    mycluster12345   sat-virtualser-948b454ea091bd9aeb8f0542c2e8c19b82c5bf7a   169.xx.xxx.xxx       
    ```
    {: screen}

3. Remove the worker nodes or clusters by referring to the following options. The corresponding hosts in your {{site.data.keyword.satelliteshort}} location become unassigned and require a reload before you can use them for other {{site.data.keyword.satelliteshort}} resources.
    *  [Resize worker pools](/docs/openshift?topic=openshift-add_workers#resize_pool) to reduce the number of worker nodes in the cluster.
    *  [Remove individual worker nodes](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_rm) from the cluster.
    *  [Remove the cluster](/docs/openshift?topic=openshift-remove).
4. For each worker node that you removed, decide what to do with the corresponding host in your {{site.data.keyword.satelliteshort}} location.
    *  Reload the host operating system so that you can re-attach and re-assign the host to other {{site.data.keyword.satelliteshort}} resources such as the location control plane or other clusters. For more information, see the update process in [Updating {{site.data.keyword.satelliteshort}} location control plane hosts](/docs/satellite?topic=satellite-hosts#host-update-location).
    *  Delete the hosts from your underlying infrastructure provider. For more information, refer to the infrastructure provider documentation.

   

## Limitations for {{site.data.keyword.openshiftshort}} clusters in {{site.data.keyword.satellitelong_notm}}
{: #satcluster-limitations}

See [{{site.data.keyword.satelliteshort}} cluster limitations](/docs/openshift?topic=openshift-openshift_limitations#satellite_limits).
{: shortdesc}






