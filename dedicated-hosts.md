---

copyright: 
  years: 2014, 2022
lastupdated: "2022-06-01"

keywords: openshift dedicated hosts

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Creating and managing dedicated hosts on VPC Gen 2 infrastructure
{: #dedicated-hosts}

**Supported infrastructure provider**: ![VPC](../icons/vpc.svg "VPC") VPC

Dedicated hosts are single-tenant managed hypervisors that can only be used to deploy {{site.data.keyword.openshiftlong_notm}} clusters. 

Dedicated hosts, including those with instance storage, are available in Beta for allowlisted accounts only. [Contact support](/docs/containers?topic=containers-get-help) for information about how to get added to the allowlist. Additionally, if you want to use dedicated hosts with instance storage, include this in your support case.
{: important}


## Setting up dedicated hosts in the CLI
{: #setup-dedicated-host-cli}

To order dedicated hosts, you must first create a host pool. Then, you can create hosts in the pool.
{: shortdesc}

**Minimum required permissions**: **Administrator** platform access role for the cluster in {{site.data.keyword.containerlong_notm}}.

1. Review the available dedicated host flavors and make a note of the flavor class that you want to create your host pool with, for example `bx2`. Dedicated host flavors that include instance storage are indicated with the letter `d` in the fourth position of the name, for example `bx2d-2x8`. For more information about using instance storage, see [Instance storage](/docs/vpc?topic=vpc-instance-storage).
    ```sh
    ibmcloud oc dedicated flavors --zone ZONE --provider PROVIDER
    ```
    {: pre}

1. Create a dedicated host pool.

    ```sh
    ibmcloud oc dedicated pool create --flavor-class CLASS --metro METRO --name NAME
    ```
    {: pre}

    `--flavor-class CLASS`
    :    The flavor-class of the dedicated host pool. To see available options, run the `ibmcloud oc dedicated flavors` command. Example: `bx2`.

    `--metro METRO`
    :    The metro to create the dedicated host pool in, such as `dal` or `wdc`.

    `--name NAME`
    :    The name of the dedicated host pool. 

1. Create at least one dedicated host in each zone where your workers reside.

    To improve redundancy, create more than one dedicated host in each zone where your workers reside.
    {: tip}

    ```sh
    ibmcloud oc dedicated host create --flavor FLAVOR --pool POOL --zone ZONE 
    ```
    {: pre}

    `-- flavor FLAVOR`
    :    The flavor of the dedicated host. To see available options, run `ibmcloud oc dedicated flavors`.

    `-- pool POOL`
    :    The name of the dedicated host pool where the dedicated host is added.

    `--zone ZONE`
    :    The zone to create the dedicated host in. For a list of available

1. [Create a cluster with your dedicated host](/docs/openshift?topic=openshift-clusters#cluster_dedicated_host_cli). Or, [add a worker pool in an existing cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_pool_create_vpc_gen2).


## Removing worker nodes from a dedicated host in the CLI
{: #remove-worker-nodes-cli}

To remove worker nodes from a dedicated host, you must disable dedicated host placement and then replace or remove the worker nodes. During replacement, when new worker nodes are created, they are only created on hosts with placement enabled.
{: shortdesc}

1. List your dedicated hosts and host pools. Make a note of the dedicated host and the dedicated host pool that you want to remove.

    ```sh
    ibmcloud oc dedicated host ls
    ibmcloud oc dedicated pool ls
    ```
    {: pre}

1. Disable dedicated host placement.

    ```sh
    ibmcloud oc dedicated host placement disable --host HOST --pool POOL 
    ```
    {: pre}

    `--host HOST`
    :    The ID of the dedicated host to disable placement for. 

    `--pool POOL`
    :    The ID of the dedicated host pool that the dedicated host is located in. To list dedicated host pools run `ibmcloud oc dedicated pool ls`.

1. [Replace](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_replace) or [remove](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_rm){: external} each worker node on the dedicated host. 
    * Replace the worker nodes if you want to keep the same cluster capacity, but move the worker nodes off the dedicated host. During replacement, when new worker nodes are created, they are only created on hosts with placement enabled.
    * Remove the worker nodes if you are deleting your cluster or reducing capacity.

1. Verify that your worker nodes are no longer on the dedicated host where placement is disabled. You can use the `dedicated host get` command to view the details of the host, including the worker nodes placed on it.
    ```sh
    ibmcloud oc dedicated host get --pool POOL --host HOST
    ```
    {: pre}
  


## Removing dedicated hosts in the CLI
{: #remove-dedicated-hosts-cli}


**Minimum required permissions**: **Administrator** platform access role for the cluster in {{site.data.keyword.containerlong_notm}}.


1. List your dedicated host pools. Make a note of the dedicated hosts that you want to remove and the dedicated host pool that the hosts are in.
    ```sh
    ibmcloud oc dedicated pool ls --pool POOL
    ```
    {: pre}

1. [Replace or remove any worker nodes from the dedicated host you want to remove](#remove-worker-nodes-cli).

1. Remove the dedicated host.

    ```sh
    ibmcloud oc dedicated host rm --host HOST --pool POOL [-q]
    ```
    {: pre}

    `--pool POOL`
    :    The ID of the dedicated host pool that contains the dedicated host to delete. To list dedicated host pools run `ibmcloud oc dedicated pool ls`.

1. **Optional**: [Remove the dedicated host pool](#remove-dedicated-host-pool-cli).



## Removing dedicated hosts pools in the CLI
{: #remove-dedicated-host-pool-cli}

1. Follow the steps in the previous sections to replace or remove [each worker node on the dedicated host](#remove-worker-nodes-cli). 
    
1. After removing the worker nodes from the dedicate host, follow the steps to [remove each dedicated host from the dedicated host pool](#remove-dedicated-hosts-cli).

1. List your dedicated host pools and make a note of the pool that you want to remove.
    ```sh
    ibmcloud oc dedicated host pool ls
    ```
    {: pre}
    
1. Get the details of your dedicated host pool. 
    ```sh
    ibmcloud oc dedicated pool get --pool POOL
    ```
    {: pre}
    
1. Get the details of each host in the pool and verify no worker nodes are placed on it.
    ```sh
    ibmcloud oc dedicated host get --pool POOL --host HOST
    ```
    {: pre}

1. Delete the dedicated host pool.

    ```sh
    ibmcloud oc dedicated pool rm ---pool POOL
    ```
    {: pre}


1. Verify the dedicated host pool is removed.
    ```sh
    ibmcloud oc dedicated pool get --pool POOL
    ```
    {: pre}
    
    


