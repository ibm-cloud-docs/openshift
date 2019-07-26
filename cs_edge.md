---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-26"

keywords: kubernetes, iks

subcollection: containers

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Restricting network traffic to edge worker nodes
{: #edge}

Edge worker nodes can improve the security of your {{site.data.keyword.containerlong}} cluster by allowing fewer worker nodes to be accessed externally and by isolating the networking workload.
{:shortdesc}

When these worker nodes are marked for networking only, other workloads cannot consume the CPU or memory of the worker node and interfere with networking.

If you have a multizone cluster and want to restrict network traffic to edge worker nodes, at least two edge worker nodes must be enabled in each zone for high availability of load balancer or Ingress pods. Create an edge node worker pool that spans all the zones in your cluster, with at least two worker nodes per zone.
{: tip}

## Labeling worker nodes as edge nodes
{: #edge_nodes}

Add the `dedicated=edge` label to two or more worker nodes on each public or private VLAN in your cluster to ensure that network load balancers (NLBs) and Ingress application load balancers (ALBs) are deployed to those worker nodes only.
{:shortdesc}

**Community Kubernetes clusters**: In Kubernetes 1.14 and later, both public and private NLBs and ALBs can deploy to edge worker nodes. In Kubernetes 1.13 and earlier, public and private ALBs and public NLBs can deploy to edge nodes, but private NLBs must deploy to non-edge worker nodes in your cluster only.
{: note}

Before you begin:

* Ensure that you have the following [{{site.data.keyword.cloud_notm}} IAM roles](/docs/containers?topic=containers-users#platform):
  * Any platform role for the cluster
  * **Writer** or **Manager** service role for all namespaces
* [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

</br>To label worker nodes as edge nodes:

1. [Create a new worker pool](/docs/containers?topic=containers-add_workers#add_pool) that spans all zones in your cluster and has at least two workers per zone. In the `ibmcloud ks worker-pool-create` command, include the `--labels dedicated=edge` flag to label all worker nodes in the pool. All worker nodes in this pool, including any worker nodes that you add later, are labeled as edge nodes. After the worker pool is marked with `dedicated=edge`, all existing and subsequent worker nodes get this label, and Ingress and load balancers are deployed to an edge worker node.
  <p class="tip">If you want to use an existing worker pool, the pool must span all zones in your cluster and have at least two workers per zone. You can label the worker pool with `dedicated=edge` by using the [PATCH worker pool API](https://containers.cloud.ibm.com/global/swagger-global-api/#/clusters/PatchWorkerPool). In the body of the request, pass in the following JSON.
      <pre class="screen">
      {
        "labels": {"dedicated":"edge"},
        "state": "labels"
      }</pre></p>

2. Verify that the worker pool and worker nodes have the `dedicated=edge` label.
  * To check the worker pool:
    ```
    ibmcloud ks worker-pool-get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
    ```
    {: pre}

  * To check individual worker nodes, review the **Labels** field of the output of the following command.
    ```
    kubectl describe node <worker_node_private_IP>
    ```
    {: pre}

3. Retrieve all existing NLBs and ALBs in the cluster.
  ```
  kubectl get services --all-namespaces | grep LoadBalancer
  ```
  {: pre}

  In the output, note the **Namespace** and **Name** of each load balancer service. For example, in the following output, there are four load balancer services: one public NLB in the `default` namespace, and one private and two public ALBs in the `kube-system` namespace.
  ```
  NAMESPACE     NAME                                             TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                                     AGE
  default       webserver-lb                                     LoadBalancer   172.21.190.18    169.46.17.2     80:30597/TCP                                10m
  kube-system   private-crdf253b6025d64944ab99ed63bb4567b6-alb1  LoadBalancer   172.21.158.78    10.185.94.150   80:31015/TCP,443:31401/TCP,9443:32352/TCP   25d
  kube-system   public-crdf253b6025d64944ab99ed63bb4567b6-alb1   LoadBalancer   172.21.84.248    169.48.228.78   80:30286/TCP,443:31363/TCP                  25d
  kube-system   public-crdf253b6025d64944ab99ed63bb4567b6-alb2   LoadBalancer   172.21.229.73    169.46.17.6     80:31104/TCP,443:31138/TCP                  25d
  ```
  {: screen}

4. Using the output from the previous step, run the following command for each NLB and ALB. This command redeploys the NLB or ALB to an edge worker node.

  **Community Kubernetes clusters**: If your cluster runs Kubernetes 1.14 or later, you can deploy both public and private NLBs and ALBs to the edge worker nodes. In Kubernetes 1.13 and earlier, only public and private ALBs and public NLBs can deploy to edge nodes, so do not redeploy private NLB services.
  {: note}

  ```
  kubectl get service -n <namespace> <service_name> -o yaml | kubectl apply -f -
  ```
  {: pre}

  Example output:
  ```
  service "webserver-lb" configured
  ```
  {: screen}

5. To verify that networking workloads are restricted to edge nodes, confirm that NLB and ALB pods are scheduled onto the edge nodes and are not scheduled onto non-edge nodes.

  * NLB pods:
    1. Confirm that the NLB pods are deployed to edge nodes. Search for the external IP address of the load balancer service that is listed in the output of step 3. Replace the periods (`.`) with hyphens (`-`). Example for the `webserver-lb` NLB that has an external IP address of `169.46.17.2`:
      ```
      kubectl describe nodes -l dedicated=edge | grep "169-46-17-2"
      ```
      {: pre}

      Example output:
      ```
      ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-wz6dg                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
      ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-2z64r                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
      ```
      {: screen}
    2. Confirm that no NLB pods are deployed to non-edge nodes. Example for the `webserver-lb` NLB that has an external IP address of `169.46.17.2`:
      ```
      kubectl describe nodes -l dedicated!=edge | grep "169-46-17-2"
      ```
      {: pre}
      * If the NLB pods are correctly deployed to edge nodes, no NLB pods are returned. Your NLBs are successfully rescheduled onto only edge worker nodes.
      * If NLB pods are returned, continue to the next step.

  * ALB pods:
    1. Confirm that all ALB pods are deployed to edge nodes. Search for the keyword `alb`. Each public and private ALB has two pods. Example:
      ```
      kubectl describe nodes -l dedicated=edge | grep alb
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

    2. Confirm that no ALB pods are deployed to non-edge nodes. Example:
      ```
      kubectl describe nodes -l dedicated!=edge | grep alb
      ```
      {: pre}
      * If the ALB pods are correctly deployed to edge nodes, no ALB pods are returned. Your ALBs are successfully rescheduled onto only edge worker nodes.
      * If ALB pods are returned, continue to the next step.

6. If NLB or ALB pods are still deployed to non-edge nodes, you can delete the pods so that they redeploy to edge nodes. **Important**: Delete only one pod at a time, and verify that the pod is rescheduled onto an edge node before you delete other pods.
  1. Delete a pod. Example for if one of the `webserver-lb` NLB pods did not schedule to an edge node:
    ```
    kubectl delete pod ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-wz6dg
    ```
    {: pre}

  2. Verify that the pod is rescheduled onto an edge worker node. Rescheduling is automatic, but might take a few minutes. Example for the `webserver-lb` NLB that has an external IP address of `169.46.17.2`:
    ```
    kubectl describe nodes -l dedicated=edge | grep "169-46-17-2"
    ```
    {: pre}

    Example output:
    ```
    ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-wz6dg                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
    ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-2z64r                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
    ```
    {: screen}

</br>You labeled worker nodes in a worker pool with `dedicated=edge` and redeployed all of the existing ALBs and NLBs to the edge nodes. All subsequent ALBs and NLBs that are added to the cluster are also deployed to an edge node in your edge worker pool. Next, prevent other [workloads from running on edge worker nodes](#edge_workloads) and [block inbound traffic to NodePorts on worker nodes](/docs/containers?topic=containers-network_policies#block_ingress).

<br />


## Preventing workloads from running on edge worker nodes
{: #edge_workloads}

A benefit of edge worker nodes is that they can be specified to run networking services only.
{:shortdesc}

Using the `dedicated=edge` toleration means that all network load balancer (NLB) and Ingress application load balancer (ALB) services are deployed to the labeled worker nodes only. However, to prevent other workloads from running on edge worker nodes and consuming worker node resources, you must use [Kubernetes taints ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/).

Before you begin:
- Ensure you that have the [**Manager** {{site.data.keyword.cloud_notm}} IAM service role for all namespaces](/docs/containers?topic=containers-users#platform).
- [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

</br>To prevent other workloads from running on edge worker nodes:

1. Apply a taint to all worker nodes with the `dedicated=edge` label that prevents pods from running on the worker node and that removes pods that do not have the `dedicated=edge` label from the worker node. The pods that are removed are redeployed to other worker nodes with capacity.
  ```
  kubectl taint node -l dedicated=edge dedicated=edge:NoSchedule dedicated=edge:NoExecute
  ```
  {: pre}
  Now, only pods with the `dedicated=edge` toleration are deployed to your edge worker nodes.

2. Verify that your edge nodes are tainted.
  ```
  kubectl describe nodes -l dedicated=edge | grep "Taint|Hostname"
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

3. If you choose to [enable source IP preservation for an NLB 1.0 service](/docs/containers?topic=containers-loadbalancer#node_affinity_tolerations), ensure that app pods are scheduled onto the edge worker nodes by [adding edge node affinity to app pods](/docs/containers?topic=containers-loadbalancer#lb_edge_nodes). App pods must be scheduled onto edge nodes to receive incoming requests.

4. To remove a taint, run the following command.
    ```
    kubectl taint node <node_name> dedicated:NoSchedule- dedicated:NoExecute-
    ```
    {: pre}


