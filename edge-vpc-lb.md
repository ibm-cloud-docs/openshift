---

copyright: 
  years: 2024, 2025
lastupdated: "2025-04-17"


keywords: openshift, kubernetes, affinity, taint, edge node, edge

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Isolating network workloads to edge nodes in VPC clusters
{: #edge-vpc-workloads}

Add the `dedicated=edge` label to worker nodes in your cluster. The labels ensure that load balancers are deployed to those worker nodes only. Note that router pods for Ingress controllers and routers are not deployed to edge nodes and remain on non-edge worker nodes.

## Prerequisites
{: #edge-vpc-workloads-pre}

- Ensure that you have the following IBM Cloud IAM roles:
    - Any platform access role for the cluster
    - **Writer** or **Manager** service access role for all namespaces
- Access to your Red Hat OpenShift cluster from the CLI.

## Isolating workloads to edge nodes
{: #edge-vpc-workloads-steps}

1. Create a worker pool with the label `dedicated=edge` or add the label to one of your existing worker pools.
    * To create a VPC worker pool, you can use the `worker-pool create vpc-gen2` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_pool_create_vpc_gen2).
        ```sh
        ibmcloud oc worker-pool create vpc-gen2 --name POOL_NAME --cluster CLUSTER --flavor FLAVOR --size-per-zone WORKERS_PER_ZONE --hardware ISOLATION --label dedicated=edge
        ```
        {: pre}

    * To label an existing worker pool, you can use the `worker-pool label set` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_label_set).
        ```sh
        ibmcloud oc worker-pool label set --cluster CLUSTER --worker-pool POOL --label dedicated=edge
        ```
        {: pre}

1. Verify that the worker pool and worker nodes have the `dedicated=edge` label.
    * To check the worker pool, run the `get` command.
        ```sh
        ibmcloud oc worker-pool get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
        ```
        {: pre}

    * To check individual worker nodes, review the **Labels** field of the output of the following command.
        ```sh
        oc describe node <worker_node_private_IP>
        ```
        {: pre}

1. Refresh your cluster master to trigger an update to your VPC load balancer member pool.
    ```sh
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}


## Next steps
{: #edge-workloads-vpc-next}





[Isolate routers to edge worker nodes](/docs/openshift?topic=openshift-edge#edge).
