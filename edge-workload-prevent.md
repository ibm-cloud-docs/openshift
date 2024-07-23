---

copyright: 
  years: 2024, 2024
lastupdated: "2024-07-23"


keywords: openshift, kubernetes, affinity, taint, edge node, edge

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Preventing app workloads from running on edge worker nodes
{: #edge-workload-prevent}

A benefit of edge worker nodes is that they can be specified to run networking services only.
{: shortdesc}

You can prevent workloads from running on edge worker nodes and consuming worker node resources by using [Kubernetes taints](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external}.


Before you begin
* Ensure that you have the following IAM roles:
    * Any platform access role for the cluster
    * **Manager** service access role for all namespaces
* [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

{[dedicated-edge.md]}

1. Apply a taint to the worker nodes with the `dedicated=edge` label. The taint prevents pods from running on the worker node and removes pods that don't have the `dedicated=edge` label from the worker node. The pods that are removed are redeployed to other worker nodes with capacity.

    To apply a taint to all existing and future worker nodes in a worker pool:
    ```sh
    ibmcloud oc worker-pool taint set -c <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID> --taint dedicated=edge:NoExecute
    ```
    {: pre}

    To apply a taint to individual worker nodes:
    ```sh
    oc adm taint node -l dedicated=edge dedicated=edge:NoExecute
    ```
    {: pre}

    Now, only pods with the `dedicated=edge` toleration are deployed to your edge worker nodes.

2. Verify that your edge nodes are tainted.
    ```sh
    oc describe nodes -l dedicated=edge | egrep "Taints|Hostname"
    ```
    {: pre}

    Example output

    ```sh
    Taints:             dedicated=edge:NoExecute
        Hostname:    10.176.48.83
      Taints:             dedicated=edge:NoExecute
    Hostname:    10.184.58.7
    ```
    {: screen}



