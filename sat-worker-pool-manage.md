---

copyright: 
  years: 2014, 2024
lastupdated: "2024-04-19"


keywords: openshift, satellite, clusters, worker nodes, worker pools, delete

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Managing {{site.data.keyword.satelliteshort}} worker pools
{: #satcluster-worker-pools}

Review the following differences from classic {{site.data.keyword.openshiftlong_notm}} clusters when you manage the worker pool life cycle of clusters that are in a {{site.data.keyword.satelliteshort}} location.
{: shortdesc}

## Creating {{site.data.keyword.satelliteshort}} worker pools with host labels for autoassignment
{: #sat-pool-create-labels}

Create a worker pool in your {{site.data.keyword.satelliteshort}} cluster with host labels. Then, {{site.data.keyword.satelliteshort}} can automatically assign available hosts to the worker pool. For more information, see [Using host autoassignment](/docs/satellite?topic=satellite-host-autoassign-ov).
{: shortdesc}

Before you begin

- Make sure that you have the **Operator** platform access role to **Kubernetes Service** for the cluster in {{site.data.keyword.cloud_notm}} IAM.
- Optional: [Attach](/docs/satellite?topic=satellite-attach-hosts) or [list available](/docs/satellite?topic=satellite-satellite-cli-reference#<review>host-ls-cli</review>host-ls-cli) hosts to your {{site.data.keyword.satelliteshort}} location with host labels that match your worker pool. Then, after you create your worker pool, these available hosts can be automatically assigned to the worker pool.

To create a worker pool in a {{site.data.keyword.satelliteshort}} cluster

1. List the {{site.data.keyword.satelliteshort}} clusters in your account.
    ```sh
    ibmcloud oc cluster ls --provider satellite
    ```
    {: pre}

1. Get the details of the cluster that you want to create the worker pool in. Note the **Worker Zones**.
    ```sh
    ibmcloud oc cluster get --cluster CLUSTER
    ```
    {: pre}

1. Create the worker pool in your {{site.data.keyword.satelliteshort}} cluster, with the following parameters.

    `--cluster`
    :   Enter the name or ID of your cluster.

    `--name`
    :   Give a name for your worker pool.
    
    `--size-per-zone`
    :   Specify the number of worker nodes for each zone that the worker pool spans. You can change this value later by resizing the worker pool.
    
    `--zone`
    :   Select the initial zone in your {{site.data.keyword.satelliteshort}} location to create the worker pool in, which you retrieved from your cluster details. You can add more zones later.
    `--host-label`
    :   Add labels to match the requested capacity of the worker pool with the available hosts in the {{site.data.keyword.satelliteshort}} location. You can use just the `cpu=number` host label because {{site.data.keyword.satelliteshort}} hosts automatically get this host label. You can also add a custom host label like `env=prod`. **Important**: You can't update host labels on the worker pool later, so take care when assigning them. You can change the labels on {{site.data.keyword.satelliteshort}} hosts, if needed.

    `--operating-system REDHAT_8_64|RHCOS`
:   Optional. The operating system of the worker nodes in your cluster. For a list of available operating sysems by cluster version, see the [{{site.data.keyword.openshiftshort}} version information](/docs/openshift?topic=openshift-openshift_versions). If no option is specified, the default operating system that corresponds to the cluster version is used.

    `--entitlement ENTITLEMENT`
    :   **Optional**: Set this option to `ocp_entitled` if you have a {{site.data.keyword.redhat_openshift_notm}} entitlement. When you specify the number of workers (`--workers`) and flavor (`--flavor`), make sure to specify only the number and size of worker nodes that you are entitled to use in [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/index.html){: external}.

Do not exceed your entitlement. Keep in mind that your OpenShift Container Platform entitlements can be used with other cloud providers or in other environments. To avoid billing issues later, make sure that you use only what you are entitled to use. For example, you might have an entitlement for the OCP licenses for two worker nodes of 4 CPU and 16 GB memory, and you create this worker pool with two worker nodes of 4 CPU and 16 GB memory. You used your entire entitlement, and you can't use the same entitlement for other worker pools, cloud providers, or environments.
{: note}

    
Example `worker-pool create` command

```sh
ibmcloud oc worker-pool create satellite --cluster <cluster_name_or_ID> --name <pool_name> --size-per-zone <number> --zone <satellite_zone> --entitlement <entitlement> --host-label <cpu=number> --host-label <memory=number> [--host-label <key=value>] [--operating-system SYSTEM]
```
{: pre}

Example `worker-pool create` command for creating a worker pool that uses Red Hat CoreOS hosts.

```sh
ibmcloud oc worker-pool create satellite --cluster <cluster_name_or_ID> --name <pool_name> --size-per-zone <number> --zone <satellite_zone> --host-label <cpu=number> --host-label <memory=number> --operating-system RHCOS
```
{: pre}
    

Your worker pool is created!
* If {{site.data.keyword.satelliteshort}} hosts with matching labels are available, the hosts are assigned to the worker pool as worker nodes. Keep in mind that hosts might also have a zone label and are assigned only to that zone.
* If no hosts are available, you can [manually assign hosts](/docs/satellite?topic=satellite-assigning-hosts) to the worker pool. Keep in mind that if you manually assign hosts, host autoassignment is disabled for future actions until you rebalance the worker pool.

When you assign hosts, you are charged a {{site.data.keyword.satelliteshort}} management fee per host vCPU. [Learn more](/docs/satellite?topic=satellite-faqs#pricing).
{: note}


## Resizing a {{site.data.keyword.satelliteshort}} worker pool
{: #sat-pool-maintenance-resize}

Resize your worker pool to request more compute capacity in your cluster.


* When host autoassignment is enabled, {{site.data.keyword.satelliteshort}} automatically assigns available hosts to the worker pool, as long as the host labels match the host labels of the worker pool. If no hosts are available, [attach more hosts](/docs/satellite?topic=satellite-attach-hosts) with matching labels to the {{site.data.keyword.satelliteshort}} location.
* If host autoassignment is disabled, resizing the worker pool enables autoassignment again.

## Rebalancing a {{site.data.keyword.satelliteshort}} worker pool
{: #sat-pool-maintenance-rebalance}

When you rebalance a worker pool, the worker pool is sized up or down depending on the most recently requested number of worker nodes per zone. You can check the requested number in the worker pool details, or set the requested number by resizing the worker pool.


In {{site.data.keyword.satelliteshort}} worker pool, rebalancing also re-enables [host autoassignment](/docs/satellite?topic=satellite-host-autoassign-ov). You can rebalance the worker pool from the {{site.data.keyword.cloud_notm}} console or the `ibmcloud oc worker-pool rebalance` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance).

## Updating worker nodes in a {{site.data.keyword.satelliteshort}} worker pool
{: #sat-pool-maintenance-update}

Follow the same process as [Updating classic worker nodes](/docs/openshift?topic=openshift-update#worker_node).


## Adding zones to a {{site.data.keyword.satelliteshort}} worker pool
{: #sat-pool-maintenance-addzone}

You can add zones to a worker pool. Available {{site.data.keyword.satelliteshort}} hosts with a zone label can be assigned only to that zone in the worker pool.


* For more information about zones in {{site.data.keyword.satelliteshort}}, see [Planning your infrastructure environment for {{site.data.keyword.satelliteshort}}](/docs/satellite?topic=satellite-infrastructure-plan).
* To add a zone, see the [`ibmcloud oc zone add satellite` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_zone_add_sat).

## Removing a {{site.data.keyword.satelliteshort}} worker pool
{: #sat-pool-maintenance-remove}

When you remove a worker pool, all the worker nodes in the cluster are removed. The hosts that the worker nodes ran on are unassigned from the cluster, and become unusable by but still attached to the {{site.data.keyword.satelliteshort}} location. For more information, see [Removing {{site.data.keyword.satelliteshort}} worker nodes or clusters](/docs/openshift?topic=openshift-remove).



