---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-09"

keywords: openshift, node scaling, ca, autoscaler

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Preparing to autoscale classic and VPC Gen 2 clusters
{: #cluster-scaling-classic-vpc}

With the `cluster-autoscaler` add-on, you can scale the worker pools in your {{site.data.keyword.openshiftlong}} classic or VPC cluster automatically to increase or decrease the number of worker nodes in the worker pool based on the sizing needs of your scheduled workloads. The `cluster-autoscaler` add-on is based on the [Kubernetes Cluster-Autoscaler project](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler){: external}.
{: shortdesc}



Want to autoscale your pods instead? Check out [Scaling apps](/docs/openshift?topic=openshift-update_app#app_scaling).
{: tip}

You can't enable the cluster autoscaler on worker pools that use reservations.
{: important}

## Understanding scale-up and scale-down
{: #ca_about}

The cluster autoscaler periodically scans the cluster to adjust the number of worker nodes within the worker pools that it manages in response to your workload resource requests and any custom settings that you configure, such as scanning intervals. Every minute, the cluster autoscaler checks for the following situations.
{: shortdesc}

* **Pending pods to scale up**: A pod is considered pending when insufficient compute resources exist to schedule the pod on a worker node. When the cluster autoscaler detects pending pods, the autoscaler scales up your worker nodes evenly across zones to meet the workload resource requests.
* **Underutilized worker nodes to scale down**: By default, worker nodes that run with less than 50% of the total compute resources that are requested for 10 minutes or more and that can reschedule their workloads onto other worker nodes are considered underutilized. If the cluster autoscaler detects underutilized worker nodes, it scales down your worker nodes one at a time so that you have only the compute resources that you need. If you want, you can [customize](/docs/openshift?topic=openshift-cluster-scaling-enable) the default scale-down utilization threshold of 50% for 10 minutes.

Scanning and scaling up and down happens at regular intervals over time, and depending on the number of worker nodes might take a longer period of time to complete, such as 30 minutes.

The cluster autoscaler adjusts the number of worker nodes by considering the [resource requests](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/){: external} that you define for your deployments, not actual worker node usage. If your pods and deployments don't request appropriate amounts of resources, you must adjust their configuration files. The cluster autoscaler can't adjust them for you. Also, keep in mind that worker nodes use some compute resources for basic cluster functionality, default and custom [add-ons](/docs/containers?topic=containers-update#addons), and [resource reserves](/docs/openshift?topic=openshift-planning_worker_nodes#resource_limit_node).
{: note}



What does scaling up and down look like?
:   In general, the cluster autoscaler calculates the number of worker nodes that your cluster needs to run its workload. Scaling the cluster up or down depends on many factors, including the following.
    *   The minimum and maximum worker node size per zone that you set.
    *   Your pending pod resource requests and certain metadata that you associate with the workload, such as anti-affinity, labels to place pods only on certain flavors, or [pod disruption budgets](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/){: external}.
    *   The worker pools that the cluster autoscaler manages, potentially across zones in a [multizone cluster](/docs/openshift?topic=openshift-ha_clusters#multizone).
    *   The [custom Helm chart values](/docs/openshift?topic=openshift-cluster-scaling-helm#ca_chart_values) that are set, such as skipping worker nodes for deletion if they use local storage.

For more information, see the Kubernetes Cluster Autoscaler FAQs for [How does scale-up work?](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-scale-up-work){: external} and [How does scale-down work?](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-scale-down-work){: external}.



Can I change how scale-up and scale-down work?
:   You can customize settings or use other Kubernetes resources to affect how scaling up and down work.

Scale-up
:   [Customize the cluster autoscaler configmap values](/docs/openshift?topic=openshift-cluster-scaling-customize) such as `scanInterval`, `expander`, `skipNodes`, or `maxNodeProvisionTime`. Review ways to [overprovision worker nodes](/docs/openshift?topic=openshift-cluster-scaling-deploy-apps#ca_scaleup) so that you can scale up worker nodes before a worker pool runs out of resources. You can also [set up Kubernetes pod budget disruptions and pod priority cutoffs](#scalable-practices-apps) to affect how scaling up works.

Scale-down
:   [Customize the cluster autoscaler configmap values](/docs/openshift?topic=openshift-cluster-scaling-customize) such as `scaleDownUnneededTime`, `scaleDownDelayAfterAdd`, `scaleDownDelayAfterDelete`, or `scaleDownUtilizationThreshold`.


Can I increase the minimum size per zone to trigger a scale up my cluster to that size?
:   No, setting a `minSize` does not automatically trigger a scale-up. The `minSize` is a threshold so that the cluster autoscaler does not scale below a certain number of worker nodes per zone. If your cluster does not yet have that number per zone, the cluster autoscaler does not scale up until you have workload resource requests that require more resources. For example, if you have a worker pool with one worker node per three zones (three total worker nodes) and set the `minSize` to `4` per zone, the cluster autoscaler does not immediately provision an additional three worker nodes per zone (12 worker nodes total). Instead, the scale-up is triggered by resource requests. If you create a workload that requests the resources of 15 worker nodes, the cluster autoscaler scales up the worker pool to meet this request. Now, the `minSize` means that the cluster autoscaler does not scale down below four worker nodes per zone even if you remove the workload that requests the amount.


How is this behavior different from worker pools that are not managed by the cluster autoscaler?
:   When you [create a worker pool](/docs/openshift?topic=openshift-add_workers#add_pool), you specify how many worker nodes per zone it has. The worker pool maintains that number of worker nodes until you [resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) or [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) it. The worker pool does not add or remove worker nodes for you. If you have more pods than can be scheduled, the pods remain in pending state until you resize the worker pool. When you enable the cluster autoscaler for a worker pool, worker nodes are scaled up or down in response to your pod spec settings and resource requests. You don't need to resize or rebalance the worker pool manually.


## Following scalable deployment practices
{: #scalable-practices}

Make the most out of the cluster autoscaler by using the following strategies for your worker node and workload deployment strategies. For more information, see the [Kubernetes Cluster Autoscaler FAQs](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md){: external}.
{: shortdesc}

[Try out the cluster autoscaler](/docs/openshift?topic=openshift-cluster-scaling-helm) with a few test workloads to get a good feel for how [scale-up and scale-down work](#ca_about), what [custom values](/docs/openshift?topic=openshift-cluster-scaling-helm#ca_chart_values) you might want to configure, and any other aspects that you might want, like [overprovisioning](/docs/openshift?topic=openshift-cluster-scaling-deploy-apps#ca_scaleup) worker nodes or [limiting apps](/docs/openshift?topic=openshift-cluster-scaling-deploy-apps). Then, clean up your test environment and plan to include these custom values and additional settings with a fresh installation of the cluster autoscaler.

### Can I autoscale multiple worker pools at once?
{: #scalable-practices-multiple}

Yes, after you install the cluster autoscaler, you can choose which worker pools within the cluster to autoscale [in the configmap](/docs/containers?topic=containers-cluster-scaling-enable). You can run only one autoscaler per cluster. Create and enable autoscaling on worker pools other than the default worker pool, because the default worker pool has system components that can prevent automatically scaling down.
{: shortdesc}

### How can I make sure that the cluster autoscaler responds to what resources my app needs?
{: #scalable-practices-resrequests}

The cluster autoscaler scales your cluster in response to your workload [resource requests](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/){: external}. As such, specify [resource requests](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/){: external} for all your deployments because the resource requests are what the cluster autoscaler uses to calculate how many worker nodes are needed to run the workload. Keep in mind that autoscaling is based on the compute usage that your workload configurations request, and does not consider other factors such as machine costs.
{: shortdesc}

### Can I scale down a worker pool to zero (0) nodes?
{: #scalable-practices-zero}

No, you can't set the cluster autoscaler `minSize` to `0`. Additionally, unless you [disable](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) all public application load balancers (ALBs) in each zone of your cluster, you must change the `minSize` to `2` worker nodes per zone so that the ALB pods can be spread for high availability. Additionally, you can [taint](/docs/openshift?topic=openshift-kubernetes-service-cli#worker_pool_taint) your worker pool to achieve a scale to down a minimum of `1`.
{: shortdesc}

If your worker pool has zero (0) worker nodes, the worker pool can't be scaled. [Disable cluster autoscaling](/docs/containers?topic=containers-cluster-scaling-enable) for the worker pool, [manually resize the worker pool](/docs/openshift?topic=openshift-add_workers#resize_pool) to at least one, and [re-enable cluster autoscaling](/docs/containers?topic=containers-cluster-scaling-enable).

### Can I optimize my deployments for autoscaling?
{: #scalable-practices-apps}

Yes, you can add several Kubernetes features to your deployment to adjust how the cluster autoscaler considers your resource requests for scaling.
{: shortdesc}

* [Taint your worker pool](/docs/openshift?topic=openshift-kubernetes-service-cli#worker_pool_taint) to allow only the deployments or pods with the matching toleration to be deployed to your worker pool.
* [Add a label](/docs/openshift?topic=openshift-add_workers#worker_pool_labels) to your worker pool other than the default worker pool. This label is used in your deployment configuration to specify `nodeAffinity` or `nodeSelector` which limits the workloads that can be deployed on the worker nodes in the labeled worker pool.
* Use [pod disruption budgets](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/){: external} to prevent abrupt rescheduling or deletions of your pods.
* If you're using pod priority, you can [edit the priority cutoff](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-cluster-autoscaler-work-with-pod-priority-and-preemption){: external} to change what types of priority trigger scaling up. By default, the priority cutoff is zero (`0`).

### Can I use taints and tolerations with autoscaled worker pools?
{: #scalable-practices-taints}

Yes, but make sure to [apply taints at the worker pool level](/docs/openshift?topic=openshift-kubernetes-service-cli#worker_pool_taint) so that all existing and future worker nodes get the same taint. Then, you must include a [matching toleration in your workload configuration](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external} so that these workloads are scheduled onto your autoscaled worker pool with the matching taint. Keep in mind that if you deploy a workload that is not tolerated by the tainted worker pool, the worker nodes are not considered for scale-up and more worker nodes might be ordered even if the cluster has sufficient capacity. However, the tainted worker pool is still identified as underutilized if they have less than the threshold (by default 50%) of their resources utilized and thus are considered for scale-down.
{: shortdesc}


## Rebalancing or resizing autoscaled worker pools
{: #ca_update_worker_node_pool}

Before you can rebalance or resize your worker pool, you must remove the worker pool from the autoscaler configmap to disable autoscaling.
{: shortdesc}

1. Edit `iks-ca-configmap` and disable the worker pool that you want to resize or rebalance by removing it from the `workerPoolsConfigStatus` section.

    ```sh
    oc edit cm -n kube-system iks-ca-configmap
    ```
    {: pre}

    Example `workerPoolsConfigStatus` section with no worker pools enabled.
    ```yaml
    workerPoolsConfigStatus: '{}'
    ```
    {: screen}

2. Save the `iks-ca-configmap`.

3. [Resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) or [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) your worker pool.

4. **Optional** [Update your VPC worker nodes](/docs/containers?topic=containers-update#vpc_worker_node).

5. Add the worker pool to the `iks-ca-configmap`.
    ```sh
    oc edit cm -n kube-system iks-ca-configmap
    ```
    {: pre}

    Example
    ```yaml
    workerPoolsConfigStatus: '{"name": "<worker_pool>","minSize": 1,"maxSize": 3,"enabled":true}'
    ```
    {: screen}


## Preparing classic or VPC Gen 2 clusters for autoscaling
{: #prepare-autoscale-classic-vpc}

Before you install the {{site.data.keyword.cloud_notm}} cluster autoscaler add-on, you can set up your cluster to prepare the cluster for autoscaling.
{: shortdesc}

The cluster autoscaler add-on is not supported for baremetal worker nodes.
{: important}

1. Before you begin, [Install the required CLI and plug-ins](/docs/cli?topic=cli-getting-started).
    *  {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`)
    *  {{site.data.keyword.containerlong_notm}} plug-in (`ibmcloud oc` alias for {{site.data.keyword.redhat_openshift_notm}} clusters)
    *  {{site.data.keyword.registrylong_notm}} plug-in (`ibmcloud cr`)
    *  Kubernetes (`kubectl`)

1. [Create a standard cluster](/docs/containers?topic=containers-clusters).
1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
1. Confirm that your {{site.data.keyword.cloud_notm}} Identity and Access Management credentials are stored in the cluster. The cluster autoscaler uses this secret to authenticate credentials. If the secret is missing, [create it by resetting credentials](/docs/containers?topic=containers-missing_permissions).
    ```sh
    oc get secrets -n kube-system | grep storage-secret-store
    ```
    {: pre}

1. Plan to autoscale a worker pool other than the `default` worker pool, because the `default` worker pool has system components that can prevent automatically scaling down. Include a label for the worker pool so that you can set [node affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity){: external} for the workloads that you want to deploy to the worker pool that has autoscaling enabled. For example, your label might be `app: nginx`. Choose from the following options:
    * Create a [VPC](/docs/openshift?topic=openshift-add_workers#vpc_pools) or [classic](/docs/openshift?topic=openshift-add_workers#classic_pools) worker pool other than the `default` worker pool with the label that you want to use with the workloads to run on the autoscaled worker pool.
    * [Add the label to an existing worker pool](/docs/openshift?topic=openshift-add_workers#worker_pool_labels) other than the `default` worker pool.
1. Confirm that your worker pool has the necessary labels for autoscaling. In the output, you see the required `ibm-cloud.kubernetes.io/worker-pool-id` label and the label that you previously created for node affinity. If you don't see these labels, [add a new worker pool](/docs/openshift?topic=openshift-add_workers#add_pool), and then [add your label for node affinity](/docs/openshift?topic=openshift-add_workers#worker_pool_labels).

    ```sh
    ibmcloud oc worker-pool get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID> | grep Labels
    ```
    {: pre}

    Example output of a worker pool with the label.
    
    ```sh
    Labels:             ibm-cloud.kubernetes.io/worker-pool-id=a1aa111111b22b22cc3c3cc444444d44-4d555e5
    ```
    {: screen}

1. [Taint the worker pools](/docs/openshift?topic=openshift-kubernetes-service-cli#worker_pool_taint) that you want to autoscale so that the worker pool does not accept workloads except the ones that you want to run on the autoscaled worker pool. You can learn more about taints and tolerations in the [community Kubernetes documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external}. As an example, you might set a taint of `use=autoscale:NoExecute`. In this example, the `NoExecute` taint evicts pods that don't have the toleration corresponding to this taint.

1. [Install the cluster autoscaler add-on](/docs/containers?topic=containers-cluster-scaling-install-addon).

After install the add-on, update the configmap values to [enable autoscaling in your cluster](/docs/containers?topic=containers-cluster-scaling-enable).



