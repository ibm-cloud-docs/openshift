---

copyright: 
  years: 2024, 2025
lastupdated: "2025-11-10"


keywords: openshift, kubernetes, affinity, taint, edge node, edge

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Isolating routers to edge nodes
{: #edge}




* Ensure that you have the following IAM roles:
    * Any platform access role for the cluster
    * **Writer** or **Manager** service access role for all namespaces
* [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

To isolate your workload to edge worker nodes:

1. Create a worker pool with the label `dedicated=edge` or add the label to one of your existing worker pools.
    * To create a Classic worker pool, you can use the `worker-pool create classic` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_create).
        ```sh
        ibmcloud oc worker-pool create classic --name POOL_NAME --cluster CLUSTER --flavor FLAVOR --size-per-zone WORKERS_PER_ZONE --hardware ISOLATION --label dedicated=edge
        ```
        {: pre}

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
    * To check the worker pool, use the `get` command.
        ```sh
        ibmcloud oc worker-pool get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
        ```
        {: pre}

    * To check individual worker nodes, review the **Labels** field of the output of the following command.
        ```sh
        oc describe node <worker_node_private_IP>
        ```
        {: pre}




1. Retrieve all existing Ingress Controllers in the cluster.
    ```sh
    oc get ingresscontroller -n openshift-ingress-operator
    ```
    {: pre}

    Example output
    ```txt
    NAME      AGE
    default   5h37m
    ```
    {: screen}


1. Edit the Ingress Controller.

    ```sh
    oc edit ingresscontroller -n openshift-ingress-operator default
    ```
    {: pre}
    
1. Set the `spec.nodePlacement` field to the following. For more information, see the [Red Hat documentation](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html-single/networking_operators/index#nw-ingress-controller-configuration-parameters_configuring-ingress){: external}. 
    ```yaml
    nodePlacement:
      nodeSelector:
        matchLabels:
          dedicated: edge
        tolerations:
        - effect: NoSchedule
          operator: Exists
    ```
    {: codeblock}

1. Save and close the file. 

1. Verify that router pods are scheduled onto edge nodes and are not scheduled onto compute nodes.
    
    ```sh
    oc describe nodes -l dedicated=edge | grep "router-*"
    ```
    {: pre}

    Example output

    ```sh
    openshift-ingress                       router-default-7784f69c7c-qq577           100m (2%)     0 (0%)      256Mi (1%)       0 (0%)         5m4s
    openshift-ingress                       router-default-7784f69c7c-7rwrj           100m (2%)     0 (0%)      256Mi (1%)       0 (0%)         5m5s
    ```
    {: screen}

1. Confirm that no router pods are deployed to non-edge nodes.
    ```sh
    oc describe nodes -l dedicated!=edge | grep "router-*"
    ```
    {: pre}

    If the router pods are correctly deployed to edge nodes, no router pods are returned. Your routers are successfully rescheduled onto only edge worker nodes.



You labeled worker nodes in a worker pool with `dedicated=edge` and redeployed all the existing ALBs to the edge nodes. All subsequent ALBs that are added to the cluster are also deployed to an edge node in your edge worker pool. Next, you can prevent other [workloads from running on edge worker nodes](/docs/openshift?topic=openshift-edge-workload-prevent).
