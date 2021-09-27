---

copyright: 
  years: 2014, 2021
lastupdated: "2021-09-27"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---




{{site.data.keyword.attribute-definition-list}}


# Classic: Restricting network traffic to edge worker nodes
{: #edge}

Edge worker nodes can improve the security of your {{site.data.keyword.openshiftlong}} cluster by allowing fewer worker nodes to be accessed externally and by isolating the networking workload.
{: shortdesc}

When these worker nodes are marked for networking only, other workloads cannot consume the CPU or memory of the worker node and interfere with networking.

If you want to restrict network traffic to edge worker nodes in a multizone cluster, at least two edge worker nodes must be enabled per zone for high availability of load balancer or Ingress pods. Create an edge node worker pool that spans all the zones in your cluster, with at least two worker nodes per zone.
{: tip}

## Isolating networking workloads to edge nodes
{: #edge_nodes}

Add the `dedicated=edge` label to worker nodes on each public or private VLAN in your cluster.

* <img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> In version 4 clusters, the labels ensure that network load balancer (NLB) pods are deployed to those worker nodes only. For NLBs, ensure that two or more worker nodes per zone are edge nodes. Note that router pods for Ingress controllers and routes are not deployed to edge nodes and remain on non-edge worker nodes.
* <img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> In version 3.11 clusters, the labels ensure that network load balancers (NLBs) and Ingress application load balancers (ALBs) are deployed to those worker nodes only. For NLBs, ensure that two or more worker nodes per zone are edge nodes. For ALBs, ensure that three or more worker nodes per zone are edge nodes. Both public and private NLBs and ALBs can deploy to edge worker nodes. Note that router pods are not deployed to edge nodes and remain on non-edge worker nodes.

Before you begin

* Ensure that you have the following [{{site.data.keyword.cloud_notm}} IAM roles](/docs/containers?topic=containers-users#checking-perms):
    * Any platform access role for the cluster
    * **Writer** or **Manager** service access role for all namespaces
* [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To create an edge node worker pool,

1. [Create a worker pool](/docs/containers?topic=containers-add_workers#add_pool) that spans all zones in your cluster and has at least two workers per zone if you use NLBs or for version 3.11 clusters, 3 or more workers per zone if you use ALBs. In the `ibmcloud oc worker-pool create` command, include the `--label dedicated=edge` flag to label all worker nodes in the pool. All worker nodes in this pool, including any worker nodes that you add later, are labeled as edge nodes.

    If you want to use an existing worker pool, the pool must span all zones in your cluster and have at least two worker nodes per zone. You can label the worker pool with `dedicated=edge` by using the [`ibmcloud oc worker-pool label set` command](/docs/containers?topic=containers-kubernetes-service-cli#cs_worker_pool_label_set).
    {: tip}

    Version 3.11 clusters: To ensure that ALB pods are always scheduled to edge worker nodes if they are present and not scheduled to non-edge worker nodes, you must create or use an existing worker pool that has at least three edge worker nodes per zone. During the update of an ALB pod, a new ALB pod rolls out to replace an existing ALB pod. However, ALB pods have anti-affinity rules that do not permit a pod to deploy to a worker node where another ALB pod already exists. If you have only two edge nodes per zone, both ALB pod replicas already exist on those edge nodes, so the new ALB pod must be scheduled on a non-edge worker node. When three edge nodes are present in a zone, the new ALB pod can be scheduled to the third edge node. Then, the old ALB pod is removed.
    {: important}

2. Verify that the worker pool and worker nodes have the `dedicated=edge` label.
    * To check the worker pool
        ```
        ibmcloud oc worker-pool get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
        ```
        {: pre}

    * To check individual worker nodes, review the **Labels** field of the output of the following command.
        ```
        oc describe node <worker_node_private_IP>
        ```
        {: pre}

3. Retrieve all existing NLBs and ALBs in the cluster.
    ```
    oc get services --all-namespaces | grep LoadBalancer
    ```
    {: pre}

    In the output, note the **Namespace** and **Name** of each load balancer service. For example, the following output shows four load balancer services: one public NLB in the `default` namespace, and one private and two public ALBs in the `kube-system` namespace.
    ```
    NAMESPACE     NAME                                             TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                                     AGE
    default       webserver-lb                                     LoadBalancer   172.21.190.18    169.46.17.2     80:30597/TCP                                11m
    kube-system   private-crdf253b6025d64944ab99ed63bb4567b6-alb1  LoadBalancer   172.21.158.78    10.185.94.150   80:31015/TCP,443:31401/TCP,9443:32352/TCP   25d
    kube-system   public-crdf253b6025d64944ab99ed63bb4567b6-alb1   LoadBalancer   172.21.84.248    169.48.228.78   80:30286/TCP,443:31363/TCP                  25d
    kube-system   public-crdf253b6025d64944ab99ed63bb4567b6-alb2   LoadBalancer   172.21.229.73    169.46.17.6     80:31104/TCP,443:31138/TCP                  25d
    ```
    {: screen}

4. Using the output from the previous step, run the following command for each NLB and ALB. This command redeploys the NLB or ALB to an edge worker node.

    ```
    oc get service -n <namespace> <service_name> -o yaml | oc apply -f -
    ```
    {: pre}

    Example output
    ```
    service "webserver-lb" configured
    ```
    {: screen}

5. To verify that networking workloads are restricted to edge nodes, confirm that NLB and ALB pods are scheduled onto the edge nodes and are not scheduled onto non-edge nodes.

    * NLB pods
        1. Confirm that the NLB pods are deployed to edge nodes. Search for the external IP address of the load balancer service that is listed in the output of step 3. Replace the periods (`.`) with hyphens (`-`). Example for the `webserver-lb` NLB that has an external IP address of `169.46.17.2`:
        ```
        oc describe nodes -l dedicated=edge | grep "169-46-17-2"
        ```
        {: pre}

        Example output
        ```
        ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-wz6dg                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
        ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-2z64r                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
        ```
        {: screen}

    2. Confirm that no NLB pods are deployed to non-edge nodes. Example for the `webserver-lb` NLB that has an external IP address of `169.46.17.2`:
        ```
        oc describe nodes -l dedicated!=edge | grep "169-46-17-2"
        ```
        {: pre}

        * If the NLB pods are correctly deployed to edge nodes, no NLB pods are returned. Your NLBs are successfully rescheduled onto only edge worker nodes.
        * If NLB pods are returned, continue to the next step.

    * ALB pods (version 3.11 only):
        1. Confirm that all ALB pods are deployed to edge nodes. Each public and private ALB that is enabled in your cluster has two pods.
        ```
        oc describe nodes -l dedicated=edge | grep alb
        ```
        {: pre}

        Example output for a cluster with two zones in which one default private and two default public ALBs are enabled:
        ```
        kube-system                private-crdf253b6025d64944ab99ed63bb4567b6-alb1-d5dd478db-27pv4    0 (0%)        0 (0%)      0 (0%)           0 (0%)
        kube-system                private-crdf253b6025d64944ab99ed63bb4567b6-alb1-d5dd478db-7p9q6    0 (0%)        0 (0%)      0 (0%)           0 (0%)
        kube-system                public-crdf253b6025d64944ab99ed63bb4567b6-alb1-5ff8cdff89-s77z6    0 (0%)        0 (0%)      0 (0%)           0 (0%)
        kube-system                public-crdf253b6025d64944ab99ed63bb4567b6-alb1-5ff8cdff89-kvs9f    0 (0%)        0 (0%)      0 (0%)           0 (0%)
        kube-system                public-crdf253b6025d64944ab99ed63bb4567b6-alb2-57df7c7b5b-tp6xw    0 (0%)        0 (0%)      0 (0%)           0 (0%)
        kube-system                public-crdf253b6025d64944ab99ed63bb4567b6-alb2-57df7c7b5b-z5p2v    0 (0%)        0 (0%)      0 (0%)           0 (0%)
        ```
        {: screen}

    2. Confirm that no ALB pods are deployed to non-edge nodes.
        ```
        oc describe nodes -l dedicated!=edge | grep alb
        ```
        {: pre}

        * If the ALB pods are correctly deployed to edge nodes, no ALB pods are returned. Your ALBs are successfully rescheduled onto only edge worker nodes.
        * If ALB pods are returned, continue to the next step.

6. If NLB or ALB pods are still deployed to non-edge nodes, you can delete the pods so that they redeploy to edge nodes. **Important**: Delete only one pod at a time, and verify that the pod is rescheduled onto an edge node before you delete other pods.
    1. Delete a pod. Example for if one of the `webserver-lb` NLB pods did not schedule to an edge node:
    ```
    oc delete pod ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-wz6dg
    ```
    {: pre}

    2. Verify that the pod is rescheduled onto an edge worker node. Rescheduling is automatic, but might take a few minutes. Example for the `webserver-lb` NLB that has an external IP address of `169.46.17.2`:
    ```
    oc describe nodes -l dedicated=edge | grep "169-46-17-2"
    ```
    {: pre}

    Example output:
    ```
    ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-wz6dg                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
    ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-2z64r                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
    ```
    {: screen}

</br>You labeled worker nodes in a worker pool with `dedicated=edge` and redeployed all of the existing ALBs and NLBs to the edge nodes. All subsequent ALBs and NLBs that are added to the cluster are also deployed to an edge node in your edge worker pool. Next, prevent other [workloads from running on edge worker nodes](#edge_workloads) and [block inbound traffic to NodePorts on worker nodes](/docs/containers?topic=containers-network_policies#block_ingress).


## Preventing app workloads from running on edge worker nodes
{: #edge_workloads}

A benefit of edge worker nodes is that they can be specified to run networking services only.
{: shortdesc}

Using the `dedicated=edge` toleration means that all network load balancer (NLB) and, in version 3.11 clusters, Ingress application load balancer (ALB) services are deployed to the labeled worker nodes only. However, to prevent other workloads from running on edge worker nodes and consuming worker node resources, you must use [Kubernetes taints](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external}.



Before you begin
- Ensure you that have the [**Manager** {{site.data.keyword.cloud_notm}} IAM service access role for all namespaces](/docs/containers?topic=containers-users#checking-perms).
- [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To prevent other workloads from running on edge worker nodes,

1. Apply a taint to the worker nodes with the `dedicated=edge` label. The taint prevents pods from running on the worker node and removes pods that do not have the `dedicated=edge` label from the worker node. The pods that are removed are redeployed to other worker nodes with capacity.

    To apply a taint to all existing and future worker nodes in a worker pool:
    ```
    ibmcloud oc worker-pool taint set -c <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID> --taint dedicated=edge:NoExecute
    ```
    {: pre}

    To apply a taint to individual worker nodes:
    ```
    oc adm taint node -l dedicated=edge dedicated=edge:NoExecute
    ```
    {: pre}

    Now, only pods with the `dedicated=edge` toleration are deployed to your edge worker nodes.

2. Verify that your edge nodes are tainted.
    ```
    oc describe nodes -l dedicated=edge | egrep "Taints|Hostname"
    ```
    {: pre}

    Example output:
    ```
    Taints:             dedicated=edge:NoExecute
        Hostname:    10.176.48.83
      Taints:             dedicated=edge:NoExecute
    Hostname:    10.184.58.7
    ```
    {: screen}

3. If you choose to [enable source IP preservation for an NLB 1.0 service](/docs/containers?topic=containers-loadbalancer#lb_source_ip), ensure that app pods are scheduled onto the edge worker nodes by [adding edge node affinity to app pods](/docs/containers?topic=containers-loadbalancer#lb_edge_nodes). App pods must be scheduled onto edge nodes to receive incoming requests.

4. Optional: You can remove a taint from the worker nodes.

    To remove all taints from all worker nodes in a worker pool,
    ```
    ibmcloud oc worker-pool taint rm -c <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
    ```
    {: pre}

    To remove individual taints from individual worker nodes,
    ```
    oc adm taint node <node_name> dedicated:NoSchedule- dedicated:NoExecute-
    ```
    {: pre}




