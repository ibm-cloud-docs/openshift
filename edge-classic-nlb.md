---

copyright: 
  years: 2024, 2024
lastupdated: "2024-07-31"


keywords: openshift, kubernetes, affinity, taint, edge node, edge

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



#  Isolating Classic NLBs to edge worker nodes
{: #edge-nlb-classic}

[Classic]{: tag-classic-inf}

In the following steps, you add the `dedicated=edge` label to worker nodes on each public or private VLAN in your cluster. This label is used to deploy your network load balancers (NLBs) to those worker nodes only. You can deploy both public and private NLBs can deploy to edge worker nodes.

If you plan to use an existing worker pool, the pool must span all zones in your cluster and have at least two worker nodes per zone. You can label the worker pool with `dedicated=edge` by using the [`ibmcloud oc worker-pool label set` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_label_set).
{: note}

Before you begin

* Ensure that you have the following [{{site.data.keyword.cloud_notm}} IAM roles](/docs/openshift?topic=openshift-iam-platform-access-roles):
    * Any platform access role for the cluster
    * **Writer** or **Manager** service access role for all namespaces
* [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Create a worker pool with the label `dedicated=edge` or add the label to one of your existing worker pools.
    * To create a worker pool you can use the `worker-pool create classic` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_create).
        ```sh
        ibmcloud oc worker-pool create classic --name POOL_NAME --cluster CLUSTER --flavor FLAVOR --size-per-zone WORKERS_PER_ZONE --hardware ISOLATION --label dedicated=edge
        ```
        {: pre}

    * To label an existing worker pool, you can use the `worker-pool label set` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_label_set).
        ```sh
        ibmcloud oc worker-pool label set --cluster CLUSTER --worker-pool POOL --label dedicated=edge
        ```
        {: pre}

2. Verify that the worker pool and worker nodes have the `dedicated=edge` label.
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




1. Retrieve all existing NLBs in the cluster. In the output, note the **namespace** and **name** of each load balancer.
    ```sh
    oc get services --all-namespaces | grep LoadBalancer
    ```
    {: pre}
    
    Example output

    ```sh
    PORT(S)                      AGE
    router-default
    80:31228/TCP,443:31655/TCP   4h54m
    LoadBalancer   172.21.71.79    169.46.17.2
    ```
    {: screen}

4. Using the output from the previous step, run the following command for each NLB. This command redeploys the NLB to an edge worker node.

    ```sh
    oc get service -n <namespace> <name> -o yaml | oc apply -f -
    ```
    {: pre}

    Example output

    ```sh
    service "router-default" configured
    ```
    {: screen}


1. To verify that networking workloads are restricted to edge nodes, confirm that the load balancers are scheduled onto the edge nodes and are not scheduled onto non-edge nodes.

    * NLB pods
        1. Confirm that the NLB pods are deployed to edge nodes. Search for the external IP address of the load balancer service that is listed in the output of step 3. Replace the periods (`.`) with hyphens (`-`). In the following example for the `crc81nk5l10gfhdql4i3qg`, the NLB has an external IP address of `169.46.17.2`. 
            ```sh
            oc describe nodes -l dedicated=edge | grep "169-46-17-2"
            ```
            {: pre}

            Example output
            ```sh
            ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-wz6dg                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
            ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-2z64r                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
            ```
            {: screen}

        1. Confirm that no NLB pods are deployed to non-edge nodes. Example for the `public-crc81nk5l10gfhdql4i3qg-nlb1` NLB that has an external IP address of `169.46.17.2`:
            ```sh
            oc describe nodes -l dedicated!=edge | grep "169-46-17-2"
            ```
            {: pre}

            * If the NLB pods are correctly deployed to edge nodes, no NLB pods are returned. Your NLBs are successfully rescheduled onto only edge worker nodes.
            * If NLB pods are returned, continue to the next step.


1. If NLB pods are still deployed to non-edge nodes, you can delete the pods so that they redeploy to edge nodes.
    Delete only one pod at a time, and verify that the pod is rescheduled onto an edge node before you delete other pods.
    {: important}

    1. Delete a pod. Example for if one of the `public-crc81nk5l10gfhdql4i3qg-alb1` NLB pods did not schedule to an edge node:
        ```sh
        oc delete pod ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-wz6dg -n ibm-system
        ```
        {: pre}

    2. Verify that the pod is rescheduled onto an edge worker node. Rescheduling is automatic, but might take a few minutes. Example for the `public-crc81nk5l10gfhdql4i3qg-alb1` NLB that has an external IP address of `169.46.17.2`:
        ```sh
        oc describe nodes -l dedicated=edge | grep "169-46-17-2"
        ```
        {: pre}

        Example output

        ```sh
        ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-wz6dg                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
        ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-2z64r                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
        ```
        {: screen}



You labeled worker nodes in a worker pool with `dedicated=edge` and redeployed all the existing NLBs to the edge nodes. All subsequent NLBs that are added to the cluster are also deployed to an edge node in your edge worker pool. Next, prevent other [workloads from running on edge worker nodes](/docs/openshift?topic=openshift-edge-workload-prevent) and [block inbound traffic to NodePorts on worker nodes](/docs/openshift?topic=openshift-network_policies#block_ingress).

