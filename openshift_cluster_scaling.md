---

copyright:
  years: 2014, 2021
lastupdated: "2021-09-10"

keywords: openshift, roks, rhoks, rhos, node scaling, ca, autoscaler

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}  


# Autoscaling clusters
{: #ca}

With the `cluster-autoscaler` add-on, you can scale the worker pools in your {{site.data.keyword.openshiftlong}} classic or VPC cluster automatically to increase or decrease the number of worker nodes in the worker pool based on the sizing needs of your scheduled workloads. The `cluster-autoscaler` add-on is based on the [Kubernetes Cluster-Autoscaler project](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler).
{: shortdesc}

Want to autoscale your pods instead? Check out [Scaling apps](/docs/openshift?topic=openshift-update_app#app_scaling).
{: tip}

## Understanding scale-up and scale-down
{: #ca_about}

The cluster autoscaler periodically scans the cluster to adjust the number of worker nodes within the worker pools that it manages in response to your workload resource requests and any custom settings that you configure, such as scanning intervals. Every minute, the cluster autoscaler checks for the following situations.
{: shortdesc}

* **Pending pods to scale up**: A pod is considered pending when insufficient compute resources exist to schedule the pod on a worker node. When the cluster autoscaler detects pending pods, the autoscaler scales up your worker nodes evenly across zones to meet the workload resource requests.
* **Underutilized worker nodes to scale down**: By default, worker nodes that run with less than 50% of the total compute resources that are requested for 10 minutes or more and that can reschedule their workloads onto other worker nodes are considered underutilized. If the cluster autoscaler detects underutilized worker nodes, it scales down your worker nodes one at a time so that you have only the compute resources that you need. If you want, you can [customize](/docs/openshift?topic=openshift-ca#ca_chart_values) the default scale-down utilization threshold of 50% for 10 minutes.

Scanning and scaling up and down happens at regular intervals over time, and depending on the number of worker nodes might take a longer period of time to complete, such as 30 minutes.

The cluster autoscaler adjusts the number of worker nodes by considering the [resource requests](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/){: external} that you define for your deployments, not actual worker node usage. If your pods and deployments don't request appropriate amounts of resources, you must adjust their configuration files. The cluster autoscaler can't adjust them for you. Also, keep in mind that worker nodes use some of their compute resources for basic cluster functionality, default and custom [add-ons](/docs/containers?topic=containers-update#addons), and [resource reserves](/docs/openshift?topic=openshift-planning_worker_nodes#resource_limit_node).
{: note}

<br>

**What does scaling up and down look like?**

In general, the cluster autoscaler calculates the number of worker nodes that your cluster needs to run its workload. Scaling the cluster up or down depends on many factors, including the following.
*   The minimum and maximum worker node size per zone that you set.
*   Your pending pod resource requests and certain metadata that you associate with the workload, such as anti-affinity, labels to place pods only on certain flavors, or [pod disruption budgets](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/){: external}.
*   The worker pools that the cluster autoscaler manages, potentially across zones in a [multizone cluster](/docs/openshift?topic=openshift-ha_clusters#multizone).
*   The [custom Helm chart values](#ca_chart_values) that are set, such as skipping worker nodes for deletion if they use local storage.

For more information, see the Kubernetes Cluster Autoscaler FAQs for [How does scale-up work?](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-scale-up-work){: external} and [How does scale-down work?](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-scale-down-work){: external}.

<br>

**Can I change how scale-up and scale-down work?**

You can customize settings or use other Kubernetes resources to affect how scaling up and down work.

* **Scale-up**: [Customize the cluster autoscaler configmap values](#ca_customize) such as `scanInterval`, `expander`, `skipNodes`, or `maxNodeProvisionTime`. Review ways to [overprovision worker nodes](#ca_scaleup) so that you can scale up worker nodes before a worker pool runs out of resources. You can also [set up Kubernetes pod budget disruptions and pod priority cutoffs](#scalable-practices-apps) to affect how scaling up works.
* **Scale-down**: [Customize the cluster autoscaler configmap values](#ca_customize) such as `scaleDownUnneededTime`, `scaleDownDelayAfterAdd`, `scaleDownDelayAfterDelete`, or `scaleDownUtilizationThreshold`.

<br>

**Can I increase the minimum size per zone to trigger a scale up my cluster to that size?**

No, setting a `minSize` does not automatically trigger a scale-up. The `minSize` is a threshold so that the cluster autoscaler does not scale below a certain number of worker nodes per zone. If your cluster does not yet have that number per zone, the cluster autoscaler does not scale up until you have workload resource requests that require more resources. For example, if you have a worker pool with one worker node per three zones (three total worker nodes) and set the `minSize` to `4` per zone, the cluster autoscaler does not immediately provision an additional three worker nodes per zone (12 worker nodes total). Instead, the scale-up is triggered by resource requests. If you create a workload that requests the resources of 15 worker nodes, the cluster autoscaler scales up the worker pool to meet this request. Now, the `minSize` means that the cluster autoscaler does not scale down below four worker nodes per zone even if you remove the workload that requests the amount.

<br>

**How is this behavior different from worker pools that are not managed by the cluster autoscaler?**

When you [create a worker pool](/docs/openshift?topic=openshift-add_workers#add_pool), you specify how many worker nodes per zone it has. The worker pool maintains that number of worker nodes until you [resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) or [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) it. The worker pool does not add or remove worker nodes for you. If you have more pods than can be scheduled, the pods remain in pending state until you resize the worker pool.

When you enable the cluster autoscaler for a worker pool, worker nodes are scaled up or down in response to your pod spec settings and resource requests. You don't need to resize or rebalance the worker pool manually.


## Following scalable deployment practices
{: #scalable-practices}

Make the most out of the cluster autoscaler by using the following strategies for your worker node and workload deployment strategies. For more information, see the [Kubernetes Cluster Autoscaler FAQs](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md){: external}.
{: shortdesc}

[Try out the cluster autoscaler](#ca_helm) with a few test workloads to get a good feel for how [scale-up and scale-down work](#ca_about), what [custom values](#ca_chart_values) you might want to configure, and any other aspects that you might want, like [overprovisioning](#ca_scaleup) worker nodes or [limiting apps](#ca_limit_pool). Then, clean up your test environment and plan to include these custom values and additional settings with a fresh installation of the cluster autoscaler.

### Can I autoscale multiple worker pools at once?
{: #scalable-practices-multiple}
Yes, after you install the cluster autoscaler, you can choose which worker pools within the cluster to autoscale [in the configmap](#ca_cm). You can run only one autoscaler per cluster. Create and enable autoscaling on worker pools other than the default worker pool, because the default worker pool has system components that can prevent automatically scaling down.
{: shortdesc}

### How can I make sure that the cluster autoscaler responds to what resources my app needs?
{: #scalable-practices-resrequests}

The cluster autoscaler scales your cluster in response to your workload [resource requests](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/){: external}. As such, specify [resource requests](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/){: external} for all your deployments because the resource requests are what the cluster autoscaler uses to calculate how many worker nodes are needed to run the workload. Keep in mind that autoscaling is based on the compute usage that your workload configurations request, and does not consider other factors such as machine costs.
{: shortdesc}

### Can I scale down a worker pool to zero (0) nodes?
{: #scalable-practices-zero}

No, you cannot set the cluster autoscaler `minSize` to `0`. Additionally, unless you [disable](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) all public application load balancers (ALBs) in each zone of your cluster, you must change the `minSize` to `2` worker nodes per zone so that the ALB pods can be spread for high availability. Additionally, you can [taint](/docs/openshift?topic=openshift-kubernetes-service-cli#worker_pool_taint) your worker pool to achieve a scale to down a minimum of `1`.
{: shortdesc}

If your worker pool has zero (0) worker nodes, the worker pool cannot be scaled. [Disable cluster autoscaling](/docs/openshift?topic=openshift-ca#ca_cm) for the worker pool, [manually resize the worker pool](/docs/openshift?topic=openshift-add_workers#resize_pool) to at least one, and [re-enable cluster autoscaling](/docs/openshift?topic=openshift-ca#ca_cm).

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

### Why are my autoscaled worker pools unbalanced?
{: #scalable-practices-unbalanced}

During a scale-up, the cluster autoscaler balances nodes across zones, with a permitted difference of plus or minus one (+/- 1) worker node. Your pending workloads might not request enough capacity to make each zone balanced. In this case, if you want to manually balance the worker pools, [update your cluster autoscaler configmap](#ca_cm) to remove the unbalanced worker pool. Then run the `ibmcloud oc worker-pool rebalance` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance), and add the worker pool back to the cluster autoscaler configmap.
{: shortdesc}


### Why can't I resize or rebalance my worker pool?
{: #scalable-practices-resize}

When the cluster autoscaler is enabled for a worker pool, you cannot [resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) or [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) your worker pools. You must [edit the configmap](#ca_cm) to change the worker pool minimum or maximum sizes, or disable cluster autoscaling for that worker pool. Don't use the `ibmcloud oc worker rm` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_rm) to remove individual worker nodes from your worker pool, which can unbalance the worker pool. For more information, see [Resizing or rebalancing autoscaled worker pools](#ca_update_worker_node_pool).
{: shortdesc}

Further, if you do not disable the worker pools before you disable the `cluster-autoscaler` add-on, the worker pools cannot be resized manually. Reinstall the cluster autoscaler, [edit the configmap](#ca_cm) to disable the worker pool, and try again.



## Preparing your cluster for autoscaling
{: #ca_prepare_cluster}

Before you install the {{site.data.keyword.cloud_notm}} cluster autoscaler add-on, you can set up your cluster to prepare the cluster for autoscaling.
{: shortdesc}

The cluster autoscaler add-on is not supported for baremetal worker nodes.
{: important}

1. [Install the required CLI and plug-ins](/docs/cli?topic=cli-getting-started):
    *  {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`)
    *  {{site.data.keyword.containerlong_notm}} plug-in (`ibmcloud oc` alias for {{site.data.keyword.openshiftshort}} clusters)
    *  {{site.data.keyword.registrylong_notm}} plug-in (`ibmcloud cr`)
    *  Kubernetes (`kubectl`)
2. [Create a standard cluster](/docs/openshift?topic=openshift-clusters).
3. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
4. Confirm that your {{site.data.keyword.cloud_notm}} Identity and Access Management credentials are stored in the cluster. The cluster autoscaler uses this secret to authenticate credentials. If the secret is missing, [create it by resetting credentials](/docs/containers?topic=containers-missing_permissions).
    ```sh
    oc get secrets -n kube-system | grep storage-secret-store
    ```
    {: pre}

5. Plan to autoscale a worker pool other than the `default` worker pool, because the `default` worker pool has system components that can prevent automatically scaling down. Include a label for the worker pool so that you can set [node affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity){: external} for the workloads that you want to deploy to the worker pool that has autoscaling enabled. For example, your label might be `app: nginx`. Choose from the following options:
    * Create a [VPC](/docs/openshift?topic=openshift-add_workers#vpc_pools) or [classic](/docs/openshift?topic=openshift-add_workers#classic_pools) worker pool other than the `default` worker pool with the label that you want to use with the workloads to run on the autoscaled worker pool.
    * [Add the label to an existing worker pool](/docs/openshift?topic=openshift-add_workers#worker_pool_labels) other than the `default` worker pool.
6. Confirm that your worker pool has the necessary labels for autoscaling. In the output, you see the required `ibm-cloud.kubernetes.io/worker-pool-id` label and the label that you previously created for node affinity. If you do not see these labels, [add a new worker pool](/docs/openshift?topic=openshift-add_workers#add_pool), and then [add your label for node affinity](/docs/openshift?topic=openshift-add_workers#worker_pool_labels).
    ```sh
    ibmcloud oc worker-pool get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID> | grep Labels
    ```
    {: pre}

    Example output of a worker pool with the label:
    ```
    Labels:             ibm-cloud.kubernetes.io/worker-pool-id=a1aa111111b22b22cc3c3cc444444d44-4d555e5
    ```
    {: screen}

7. [Taint the worker pools](/docs/openshift?topic=openshift-kubernetes-service-cli#worker_pool_taint) that you want to autoscale so that the worker pool does not accept workloads except the ones that you want to run on the autoscaled worker pool. You can learn more about taints and tolerations in the [community Kubernetes documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/). As an example, you might set a taint of `use=autoscale:NoExecute`. In this example, the `NoExecute` taint evicts pods that do not have the toleration corresponding to this taint.

8. [Install the cluster autoscaler add-on](#ca_addon).

    You might also install the cluster autoscaler Helm chart, but the Helm chart is deprecated and becomes unsupported tentatively 15 September 2020. You cannot install the add-on and the Helm chart in the same cluster at the same time.
    {: deprecated}



## Installing the cluster autoscaler add-on in your cluster
{: #ca_addon}

1. [Prepare your cluster for autoscaling](#ca_prepare_cluster).

2. If you previously installed the cluster autoscaler Helm chart, [make a backup of your configmap, disable autoscaling, and remove the Helm chart](#ca_rm).

    The cluster autoscaler add-on configmap contains different parameters than the cluster autoscaler Helm chart configmap. You can make a backup of your Helm chart configmap to use as reference, but do not apply the backup directly to your cluster with the add-on. Instead, you can update the cluster autoscaler add-on configmap with the values from your Helm chart backup.
    {: note}

3. Install the cluster autoscaler add-on to your cluster.

    **In the console**
    1. From the [{{site.data.keyword.openshiftlong_notm}} cluster dashboard](https://cloud.ibm.com/kubernetes/clusters), select the cluster where you want to enable autoscaling.
    2. On the **Overview** page, click **Add-ons**.
    3. On the **Add-ons** page, locate the Cluster Autoscaler add-on and click **Install**

    **In the CLI**
    1. Install the `cluster-autoscaler` add-on.
        ```
        ibmcloud oc cluster addon enable cluster-autoscaler —-cluster <cluster_name>
        ```
        {: pre}

        Example output
        ```
        Enabling add-on `cluster-autoscaler` for cluster <cluster_name>...
        The add-on might take several minutes to deploy and become ready for use.
        OK
        ```
        {: screen}

    2. Verify that the add-on is installed and `Ready`.
        ```
        ibmcloud oc cluster addon ls --cluster <cluster_name>
        ```
        {: pre}

        Example output

        ```
        Name                 Version   Health State   Health Status   
        cluster-autoscaler   1.0.1     normal         Addon Ready
        ```
        {: screen}

4. By default, no worker pools are enabled for autoscaling. To enable autoscaling on your worker pools, [update the cluster autoscaler configmap to enable scaling for your worker pools](#ca_cm).

## Installing the cluster autoscaler Helm chart in your cluster
{: #ca_helm}

The cluster autoscaler Helm chart is deprecated. For the latest version of the cluster autoscaler, [install the add-on](#ca_addon)
{: deprecated}



Install the {{site.data.keyword.cloud_notm}} cluster autoscaler plug-in with a Helm chart to autoscale worker pools in your cluster.
{: shortdesc}

1. [Prepare your cluster for autoscaling](#ca_prepare_cluster).
2. [Follow the instructions](/docs/openshift?topic=openshift-helm#install_v3) to install the **Helm version 3** client on your local machine.
3. Add and update the Helm repo where the cluster autoscaler Helm chart is.
    ```
    helm repo add iks-charts https://icr.io/helm/iks-charts
    ```
    {: pre}

    ```
    helm repo update
    ```
    {: pre}

4. Decide if you want to [customize the cluster autoscaler settings](#ca_chart_values), such as the worker pools that are autoscaled, or the amount of time that the cluster autoscaler waits before scaling worker nodes up or down. You can customize your settings by using the `--set` flag in the `helm install` command. Depending on the settings that you want to customize, you might need to prepare multiple `--set` flags before you can install the Helm chart. For example, you might want to autoscale your default worker pool by preparing the following `--set` flag. Note: If your default command line shell is `zsh`, start a `bash` session before running the following command.
    ```
    --set workerpools[0].<pool_name>.max=<number_of_workers>,workerpools[0].<pool_name>.min=<number_of_workers>,workerpools[0].<pool_name>.enabled=(true|false)
    ```
    {: codeblock}

    Understanding the `--set workerpools` options:
    * **`workerpools[0]`**: The first worker pool to enable or disable for autoscaling. You must include three parameters for each worker pool for the command to succeed: the maximum number of worker nodes (`max`), the minimum number of worker nodes (`min`), and whether you want to enable (`true`) or disable (`false`) autoscaling for this worker pool. To include multiple worker pools, include a comma-separated list and increase the number in brackets, such as: `workerpools[0].default...,workerpools[1].pool1...,workerpools[2].pool2...`.
    * **`<pool_name>`**: The name or ID of the worker pool that you want to enable or disable for autoscaling. To list available worker pools, run `ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>`.
    * **`max=<number_of_workers>`**: Specify the maximum number of worker nodes per zone that the cluster autoscaler can scale up to. The value must be equal to or greater than the value that you set for the `min=<number_of_workers>` size.
    * **`min=<number_of_workers>`**: Specify the minimum number of worker nodes per zone that the cluster autoscaler can scale down to. The value must be `2` or greater so that your ALB pods can be spread for high availability. If you [disabled](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) all public ALBs in each zone of your standard cluster, you can set the value to `1`. Keep in mind that setting a `min` size does not automatically trigger a scale-up. The `min` size is a threshold so that the cluster autoscaler does not scale below this minimum number of worker nodes per zone. If your cluster does not have this number of worker nodes per zone yet, the cluster autoscaler does not scale up until you have workload resource requests that require more resources.
    * **`enabled=(true|false)`**: Set the value to `true` to enable the cluster autoscaler to scale your worker pool. Set the value to `false` to stop the cluster autoscaler from scaling the worker pool. Later, if you want to [remove the cluster autoscaler](/docs/openshift?topic=openshift-ca#ca_rm), you must first disable each worker pool in the configmap.

5. Install the cluster autoscaler Helm chart in the `kube-system` namespace of your cluster. In the example command, the `autoscale` worker pool is enabled for autoscaling with the Helm chart installation. The worker pool details are added to the cluster autoscaler config map.
    ```
    helm install ibm-iks-cluster-autoscaler iks-charts/ibm-iks-cluster-autoscaler --namespace kube-system --set workerpools[0].default.max=5,workerpools[0].autoscale.min=2,workerpools[0].default.enabled=true
    ```
    {: pre}

    Example output
    
    ```
    NAME: ibm-iks-cluster-autoscaler
    LAST DEPLOYED: Fri Jan 17 12:20:30 2020
    NAMESPACE: kube-system
    STATUS: deployed
    REVISION: 1
    TEST SUITE: None
    NOTES:
    Thank you for installing: ibm-iks-cluster-autoscaler. Your release is named: ibm-iks-cluster-autoscaler

    For more information about using the cluster autoscaler, refer to the chart README.md file.
    ```
    {: screen}

6. Verify that the installation is successful.

    1. Check that the cluster autoscaler pod is in a **Running** state.
        ```
        oc get pods --namespace=kube-system | grep ibm-iks-cluster-autoscaler
        ```
        {: pre}

        Example output
        ```
        ibm-iks-cluster-autoscaler-8497bfc968-dbn7w   1/1       Running   0          9m
        ```
        {: screen}

    2. Check that the cluster autoscaler service is created.
        ```
        oc get service --namespace=kube-system | grep ibm-iks-cluster-autoscaler
        ```
        {: pre}

        Example output
        ```
        ibm-iks-cluster-autoscaler   ClusterIP   172.21.xxx.xx    <none>        8085/TCP        9m
        ```
        {: screen}

    3. Optional: If you enabled autoscaling for a worker pool during the Helm chart installation, verify that the config map is correct by checking that the `workerPoolsConfig.json` field is updated and that the `workerPoolsConfigStatus` field shows a `SUCCESS` message.
        ```
        oc get cm iks-ca-configmap -n kube-system -o yaml
        ```
        {: pre}

        Example output where the default worker pool is enabled for autoscaling:
        ```
        apiVersion: v1
        data:
          workerPoolsConfig.json: |
            [{"name": "autoscale", "minSize": 1, "maxSize": 2, "enabled": true }]
        kind: ConfigMap
        metadata:
          annotations:
            workerPoolsConfigStatus: '{"1:2:default":"SUCCESS"}'
          creationTimestamp: "2019-08-23T14:26:54Z"
          name: iks-ca-configmap
          namespace: kube-system
          resourceVersion: "12757878"
          selfLink: /api/v1/namespaces/kube-system/configmaps/iks-ca-configmap
          uid: bd661f95-35ef-433d-97e0-5d1ac092eafb
        ```
        {: screen}

7. Repeat these steps for every cluster where you want to provision the cluster autoscaler.

8. Optional: If you did not set any worker pools for autoscaling with the installation, you can [Update the cluster autoscaler configuration](#ca_cm).



## Updating the cluster autoscaler configmap to enable scaling
{: #ca_cm}

Update the cluster autoscaler configmap to enable automatically scaling worker nodes in your worker pools based on the minimum and maximum values that you set.
{: shortdesc}

After you edit the configmap to enable a worker pool, the cluster autoscaler scales your cluster in response to your workload requests. As such, you cannot [resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) or [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) your worker pools. Scanning and scaling up and down happens at regular intervals over time, and depending on the number of worker nodes might take a longer period of time to complete, such as 30 minutes. Later, if you want to [remove the cluster autoscaler](#ca_rm), you must first disable each worker pool in the configmap.
{: note}

**Before you begin**:
*  Install the [cluster autoscaler add-on](#ca_addon) or the [Helm chart](#ca_helm).
*  [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

**To update the cluster autoscaler configmap and values**:

1. Edit the cluster autoscaler configmap YAML file.
    ```
    oc edit cm iks-ca-configmap -n kube-system -o yaml
    ```
    {: pre}

    Example output
    ```yaml
    apiVersion: v1
    data:
      workerPoolsConfig.json: |
        [
         {"name": "<worker_pool>","minSize": 1,"maxSize": 2,"enabled":false}
        ]
    kind: ConfigMap
    ```
    {: screen}

2. Edit the configmap with the parameters to define how the cluster autoscaler scales your cluster worker pool. **Note:** Unless you [disabled](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) all public application load balancers (ALBs) in each zone of your standard cluster, you must change the `minSize` to `2` per zone so that the ALB pods can be spread for high availability.

    - `"name": "default"`: Replace `"default"` with the name or ID of the worker pool that you want to scale. To list worker pools, run `ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>`. To manage more than one worker pool, copy the JSON line to a comma-separated line, such as follows.
        ```
        [
        {"name": "default","minSize": 1,"maxSize": 2,"enabled":false},
        {"name": "Pool2","minSize": 2,"maxSize": 5,"enabled":true}
        ]
        ```
        {: codeblock}
        
        The cluster autoscaler can scale only worker pools that have the `ibm-cloud.kubernetes.io/worker-pool-id` label. To check whether your worker pool has the required label, run `ibmcloud oc worker-pool get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID> | grep Labels`. If your worker pool does not have the required label, [add a new worker pool](/docs/openshift?topic=openshift-add_workers#add_pool) and use this worker pool with the cluster autoscaler.
        {: note}

    - `"minSize": 1`: Specify the minimum number of worker nodes per zone that the cluster autoscaler can scale down the worker pool to. The value must be `2` or greater so that your ALB pods can be spread for high availability. If you [disabled](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) all public ALBs in each zone of your standard cluster, you can set the value to `1`.

        Setting a `minSize` does not automatically trigger a scale-up. The `minSize` is a threshold so that the cluster autoscaler does not scale below a certain number of worker nodes per zone. If your cluster does not yet have that number per zone, the cluster autoscaler does not scale up until you have workload resource requests that require more resources. For example, if you have a worker pool with one worker node per three zones (three total worker nodes) and set the `minSize` to `4` per zone, the cluster autoscaler does not immediately provision an additional three worker nodes per zone (12 worker nodes total). Instead, the scale-up is triggered by resource requests. If you create a workload that requests the resources of 15 worker nodes, the cluster autoscaler scales up the worker pool to meet this request. Now, the `minSize` means that the cluster autoscaler does not scale down below four worker nodes per zone even if you remove the workload that requests the amount. For more information, see the [Kubernetes docs](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#when-does-cluster-autoscaler-change-the-size-of-a-cluster){: external}.
        {: note}

    - `"maxSize": 2`: Specify the maximum number of worker nodes per zone that the cluster autoscaler can scale up the worker pool to. The value must be equal to or greater than the value that you set for the `minSize`.
    - `"enabled": false`: Set the value to `true` for the cluster autoscaler to manage scaling for the worker pool. Set the value to `false` to stop the cluster autoscaler from scaling the worker pool. Later, if you want to [remove the cluster autoscaler](#ca_rm), you must first disable each worker pool in the configmap.

4. Save the configuration file.
5. Get your cluster autoscaler pod.
    ```
    oc get pods -n kube-system
    ```
    {: pre}

6. Review the **`Events`** section of the cluster autoscaler pod for a **`ConfigUpdated`** event to verify that the configmap is successfully updated. The event message for your configmap is in the following format: `minSize:maxSize:PoolName:<SUCCESS|FAILED>:error message`.

    ```
    oc describe pod -n kube-system <cluster_autoscaler_pod>
    ```
    {: pre}

    Example output
    ```
        Name:               ibm-iks-cluster-autoscaler-857c4d9d54-gwvc6
        Namespace:          kube-system
        ...
        Events:
        Type     Reason         Age   From                                        Message
        ----     ------         ----  ----                                        -------

        Normal  ConfigUpdated  3m    ibm-iks-cluster-autoscaler-857c4d9d54-gwvc6  {"1:3:default":"SUCCESS:"}
    ```
    {: screen}


If you enable a worker pool for autoscaling and then later add a zone to this worker pool, restart the cluster autoscaler pod so that it picks up this change: `oc delete pod -n kube-system <cluster_autoscaler_pod>`.
{: note}

## Customizing the cluster autoscaler configuration values
{: #ca_customize}
Customize the cluster autoscaler settings such as the amount of time it waits before scaling worker nodes up or down.
{: shortdesc}

**Before you begin**:
*  [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
*  [Install the `ibm-iks-cluster-autoscaler` add-on](#ca_addon).

### Customizing the cluster autoscaler add-on configmap
{: #ca_addon_values}

When you modify a configmap parameter other than the worker pool `minSize`, `maxSize`, or if you enable or disable a worker pool, the cluster autoscaler pods are restarted.
{: note}

1. Review the default parameters for the [cluster autoscaler configmap](#ca_addon_ref).

2. Download the cluster autoscaler add-on configmap and review the parameters.
    ```
    oc get cm iks-ca-configmap -n kube-system -o yaml > configmap.yaml
    ```
    {: pre}

3. Open the `configmap.yaml` file and update the settings that you want to change.

4. Reapply the cluster autoscaler add-on configmap.
    ```
    oc apply -f configmap.yaml
    ```
    {: pre}

5. Verify that the pods are restarted successfully.
    ```
    oc get pods -n kube-system | grep autoscaler
    ```
    {: pre}

### Customizing the cluster autoscaler Helm chart values
{: #ca_chart_values}

The cluster autoscaler Helm chart is deprecated. For the latest version of the cluster autoscaler, [install the add-on](#ca_addon)
{: deprecated}

1. To change any of the cluster autoscaler configuration values, update the config map or the Helm chart with the new values. Include the `--recreate-pods` flag so that any existing cluster autoscaler pods are re-created to pick up the custom setting changes. The following example command changes the scan interval to `2m` and enables autoscaling for the `autoscale` worker pool, with a maximum of `5` and minimum of `3` worker nodes per zone.
    ```
    helm upgrade --set scanInterval=2m --set workerpools[0].default.max=5,workerpools[0].autoscale.min=3,workerpools[0].default.enabled=true ibm-iks-cluster-autoscaler iks-charts/ibm-iks-cluster-autoscaler -i --recreate-pods --namespace kube-system
    ```
    {: pre}

    To reset the Helm chart to the default values:
    ```
    helm upgrade --reset-values ibm-iks-cluster-autoscaler iks-charts/ibm-iks-cluster-autoscaler --recreate-pods
    ```
    {: pre}

2. Verify your changes.
    1. Review the Helm chart values again.
        ```
        helm get values ibm-iks-cluster-autoscaler -a
        ```
        {: pre}

3. Verify that the installation is successful.

    1. Check that the cluster autoscaler pod is in a **Running** state.
        ```
        oc get pods --namespace=kube-system | grep ibm-iks-cluster-autoscaler
        ```
        {: pre}

        Example output
        ```
        ibm-iks-cluster-autoscaler-8497bfc968-dbn7w   1/1       Running   0          9m
        ```
        {: screen}

    2. Check that the cluster autoscaler service is created.
        ```
        oc get service --namespace=kube-system | grep ibm-iks-cluster-autoscaler
        ```
        {: pre}

        Example output
        ```
        ibm-iks-cluster-autoscaler   ClusterIP   172.21.xxx.xx    <none>        8085/TCP        9m
        ```
        {: screen}

2. Verify that the config map is correct by checking that the `workerPoolsConfig.json` field is updated and that the `workerPoolsConfigStatus` field shows a `SUCCESS` message.
    ```
    oc get cm iks-ca-configmap -n kube-system -o yaml
    ```
    {: pre}

    Example output where the `autoscale` worker pool is enabled for autoscaling:
    ```
    apiVersion: v1
    data:
      workerPoolsConfig.json: |
        [{"name": "autoscale", "minSize": 3, "maxSize": 5, "enabled": true }]
    kind: ConfigMap
    metadata:
      annotations:
        workerPoolsConfigStatus: '{"1:2:default":"SUCCESS"}'
      creationTimestamp: "2019-08-23T14:26:54Z"
      name: iks-ca-configmap
      namespace: kube-system
      resourceVersion: "12757878"
      selfLink: /api/v1/namespaces/kube-system/configmaps/iks-ca-configmap
      uid: bd661f95-35ef-433d-97e0-5d1ac092eafb
    ```
    {: screen}

## Deploying apps to your autoscaled worker pools
{: #ca_limit_pool}

To limit a pod deployment to a specific worker pool that is managed by the cluster autoscaler, use a combination of labels and `nodeSelector` or `nodeAffinity` to deploy apps only to the autoscaled worker pools. With `nodeAffinity`, you have more control over how the scheduling behavior works to match pods to worker nodes. Then, use taints and tolerations so that only these apps can run on your autoscaled worker pools.
{: shortdesc}

For more information, see the following Kubernetes docs:
* [Assigning pods to nodes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/){: external}
* [Taints and tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external}

**Before you begin**:
*  [Install the `ibm-iks-cluster-autoscaler` plug-in](#ca_helm).
*  [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

**To limit pods to run on certain autoscaled worker pools**:

1. Make sure that you labeled and tainted your autoscaled worker pool as described in [Preparing your cluster for autoscaling](#ca_prepare_cluster).
2. In your pod spec template, match the `nodeSelector` or `nodeAffinity` to the label that you used in your worker pool.

    Example of `nodeSelector`:
    ```yaml
    ...
    spec:
      containers:
      - name: nginx
        image: nginx
        imagePullPolicy: IfNotPresent
      nodeSelector:
        app: nginx
    ...
    ```
    {: codeblock}

    Example of `nodeAffinity`:
    ```yaml
    spec:
      containers:
      - name: nginx
        image: nginx
        imagePullPolicy: IfNotPresent
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: use
                operator: In
                values:
                - autoscale
    ```
    {: codeblock}

3. In your pod spec template, match the `toleration` to the taint you set on your worker pool.

    Example `NoExecute` toleration:
    ```yaml
    tolerations:
      - key: use
        operator: "Exists"
        effect: "NoExecute"
    ```
    {: codeblock}

4. Deploy the pod. Because of the matching label, the pod is scheduled onto a worker node that is in the labeled worker pool. Because of the matching toleration, the pod can run on the tainted worker pool.
    ```
    oc apply -f pod.yaml
    ```
    {: pre}



## Scaling up worker nodes before the worker pool has insufficient resources
{: #ca_scaleup}

As described in the [Understanding how the cluster autoscaler works](#ca_about) topic and the [Kubernetes Cluster Autoscaler FAQs](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md){: external}, the cluster autoscaler scales up your worker pools in response to your requested resources of the workload against the available recourses of the worker pool. However, you might want the cluster autoscaler to scale up worker nodes before the worker pool runs out of resources. In this case, your workload does not need to wait as long for worker nodes to be provisioned because the worker pool is already scaled up to meet the resource requests.
{: shortdesc}

The cluster autoscaler does not support early scaling (overprovisioning) of worker pools. However, you can configure other Kubernetes resources to work with the cluster autoscaler to achieve early scaling.

### Pause pods
{: #pause-pods-ca}

You can create a deployment that deploys [pause containers](https://stackoverflow.com/questions/48651269/what-are-the-pause-containers){: external} in pods with specific resource requests, and assign the deployment a low pod priority. When these resources are needed by higher priority workloads, the pause pod is preempted and becomes a pending pod. This event triggers the cluster autoscaler to scale up.
{: shortdesc}

For more information about setting up a pause pod deployment, see the [Kubernetes FAQ ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-can-i-configure-overprovisioning-with-cluster-autoscaler). You can use [this example overprovisioning configuration file ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Cloud/kube-samples/blob/master/ibm-ks-cluster-autoscaler/overprovisioning-autoscaler.yaml) to create the priority class, service account, and deployments.

If you use this method, make sure that you understand how [pod priority](/docs/openshift?topic=openshift-pod_priority) works and how to set pod priority for your deployments. For example, if the pause pod does not have enough resources for a higher priority pod, the pod is not preempted. The higher priority workload remains in pending, so the cluster autoscaler is triggered to scale up. However, in this case, the scale-up action is not early because the workload that you want to run cannot be scheduled because of insufficient resources. Pause pod must have the matching `nodeAffinity` or `nodeSelector` as well as the matching tolerations that you set for your worker pool.
{: note}

### Horizontal pod autoscaling (HPA)
{: #hpca}

Because horizontal pod autoscaling is based on the average CPU usage of the pods, the CPU usage limit that you set is reached before the worker pool runs out of resources.
{: shortdesc}

More pods are requested, which then triggers the cluster autoscaler to scale up the worker pool.<br><br>For more information about setting up HPA, see the [Kubernetes docs](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/){: external}.

## Updating the cluster autoscaler add-on
{: #ca_addon_up}

This topic applies only to the cluster autoscaler add-on.
{: important}

If you upgrade your cluster to a version that is not supported by the cluster autoscaler add-on, your apps might experience downtime and your cluster might not scale.
{: important}

The cluster autoscaler has two types of updates.

Patch updates
: Patch updates are delivered automatically by IBM and do not contain any feature updates or changes in the supported add-on and cluster versions.

Release updates
:   Release updates contain new features for the cluster autoscaler or changes in the supported add-on or cluster versions. You must manually apply release updates to your cluster autoscaler add-on.


1. Check the version of the cluster autoscaler add-on that is deployed in your cluster. If an update is available, review the [release notes](/docs/openshift?topic=openshift-ca_changelog) for the latest add-on version.
    ```
    ibmcloud oc cluster addon ls --cluster <cluster_name>
    ```
    {: pre}

2. Disable the cluster autoscaler add-on. You might see a warning that resources or data might be deleted. For the cluster autoscaler update, any autoscaling operations that are in process when you disable fail. When you re-enable the add-on, the autoscaling operation is restarted for you. Existing cluster autoscaler resources like the `iks-ca-configmap` are retained even after you disable the add-on. Your worker nodes are not deleted because of disabling the add-on.
    ```
    ibmcloud oc cluster addon disable cluster-autoscaler --cluster <cluster_name>
    ```
    {: pre}

    Example output
    ```sh
    Data and resources that you created for the add-on might be deleted when the add-on is disabled. Continue? [y/N]>
    ```
    {: screen}

3. Enable the add-on to install the latest version.
    ```sh
    ibmcloud oc cluster addon enable cluster-autoscaler --cluster <cluster_name>
    ```
    {: pre}

3. Verify the add-on is successfully updated and `Ready`.
    ```
    ibmcloud oc cluster addon ls --cluster <cluster_name>
    ```
    {: pre}

## Rebalancing or resizing autoscaled worker pools
{: #ca_update_worker_node_pool}

Before you can rebalance or resize your worker pool, you must remove the worker pool from the autoscaler configmap to disable autoscaling.
{: shortdesc}

1. Edit `iks-ca-configmap` and disable the worker pool that you want to resize or rebalance by removing it from the `workerPoolsConfigStatus` section.
    ```sh
    oc edit cm -n kube-system iks-ca-configmap
    ```
    {: pre}

    **Example `workerPoolsConfigStatus` section with no worker pools enabled**
    ```yaml
    workerPoolsConfigStatus: '{}'
    ```
    {: screen}

3. Save the `iks-ca-configmap`.

4. [Resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) or [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) your worker pool.

5. **Optional** [Update your VPC worker nodes](/docs/containers?topic=containers-update#vpc_worker_node).

6. Add the worker pool to the `iks-ca-configmap`.
    ```sh
    oc edit cm -n kube-system iks-ca-configmap
    ```
    {: pre}

    **Example**
    ```yaml
    workerPoolsConfigStatus: '{"name": "<worker_pool>","minSize": 1,"maxSize": 3,"enabled":true}'
    ```
    {: screen}


## Upgrading a cluster autoscaler Helm chart release
{: #ca_helm_up}

This topic applies only to the cluster autoscaler Helm chart.
{: important}

The cluster autoscaler Helm chart is deprecated. For the latest version of the cluster autoscaler, [install the add-on](#ca_addon). You can not have both the cluster autoscaler Helm chart and the cluster autoscaler add-on installed at the same time.
{: deprecated}

You can upgrade your existing cluster autoscaler release to the latest version of the Helm chart. To check your current release version, run `helm list -n <namespace> | grep cluster-autoscaler`. Compare your version to the latest available release by reviewing the **Chart Version** in the [{{site.data.keyword.cloud_notm}} Helm Catalog](https://cloud.ibm.com/kubernetes/helm/iks-charts/ibm-iks-cluster-autoscaler){: external}.
{: shortdesc}

### Prerequisites
{: #ca_helm_up_prereqs}

Before you begin to upgrade your cluster autoscaler release, complete the following steps.
{: shortdesc}

This topic applies only to the cluster autoscaler Helm chart.
{: important}

1. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
2. To review the changelog of chart versions, [download the source code `tar` file](https://cloud.ibm.com/kubernetes/helm/iks-charts/ibm-iks-cluster-autoscaler) and open the `RELEASENOTES.MD` file.

### Upgrading the cluster autoscaler release version
{: #ca_helm_up_general}

This topic applies only to the cluster autoscaler Helm chart.
{: important}

To upgrade your cluster autoscaler release, you can update the Helm chart repo and re-create the cluster autoscaler pods. Use the same version of Helm that you used to install the initial Helm chart and release.

Before you begin, see the [Prerequisites](#ca_helm_up_prereqs).

1. Update the Helm repo to retrieve the latest version of all Helm charts in this repo.
    ```
    helm repo update
    ```
    {: pre}

2. Optional: Download the latest Helm chart to your local machine. Then, extract the package and review the `release.md` file to find the latest release information.
    ```
    helm pull iks-charts/ibm-iks-cluster-autoscaler
    ```
    {: pre}

3. Find the name of the cluster autoscaler release that you installed in your cluster.
    ```
    helm list -n <namespace> | grep cluster-autoscaler
    ```
    {: pre}

    Example output
    ```
    myhelmchart     1           Mon Jan  7 14:47:44 2019    DEPLOYED    ibm-iks-cluster-autoscaler-1.0.1      kube-system
    ```
    {: screen}

4. Upgrade the cluster autoscaler release to the latest version.
    ```
    helm upgrade --force --recreate-pods <helm_chart_name>  iks-charts/ibm-iks-cluster-autoscaler
    ```
    {: pre}

5. Verify that the [cluster autoscaler configmap](#ca_cm) `workerPoolsConfig.json` section is set to `"enabled": true` for the worker pools that you want to scale.
    ```
    oc describe cm iks-ca-configmap -n kube-system
    ```
    {: pre}

    Example output
    ```
    Name:         iks-ca-configmap
    Namespace:    kube-system
    Labels:       <none>
    Annotations:  kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"v1","data":{"workerPoolsConfig.json":"[\n {\"name\": \"docs\",\"minSize\": 1,\"maxSize\": 3,\"enabled\":true}\n]\n"},"kind":"ConfigMap",...

    Data
    ====
    workerPoolsConfig.json:
    ----
    [
        {"name": "<worker_pool","minSize": 1,"maxSize": 3,"enabled":true}
    ]

    Events:  <none>
    ```
    {: screen}

## Removing the cluster autoscaler
{: #ca_rm}

If you do not want to automatically scale your worker pools, you can uninstall the cluster autoscaler Helm chart. After the removal, you must [resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) or [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) your worker pools manually.
{: shortdesc}

Before you begin: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Optional: To refer to your autoscaling settings later, make a backup of your configmap.
    ```
    oc get cm iks-ca-configmap -o yaml > backup_configmap.yaml
    ```
    {: pre}

1. In the [cluster autoscaler configmap](#ca_cm), remove the worker pool by setting the `"enabled"` value to `false`.
    ```
    oc edit cm iks-ca-configmap -n kube-system
    ```
    {: pre}

    Example output

    ```yaml
    apiVersion: v1
    data:
      workerPoolsConfig.json: |
        [
         {"name": "<worker_pool>","minSize": 1,"maxSize": 2,"enabled":false}
        ]
    kind: ConfigMap
    metadata:
      creationTimestamp: 2018-11-29T18:43:46Z
      name: iks-ca-configmap
      namespace: kube-system
      resourceVersion: "2227854"
      selfLink: /api/v1/namespaces/kube-system/configmaps/iks-ca-configmap
      uid: b45d047b-f406-11e8-b7f0-82ddffc6e65e
    ```
    {: screen}


    If you already deleted the Helm chart and see a message such as `iks-ca-configmap not found`, [redeploy the cluster autoscaler Helm chart](#ca_helm) to your cluster and try to remove it again.
    {: tip}

2. Disable the add-on or uninstall the Helm chart.

    **Add-on**
    1. Disable the add-on.
    ```
    ibmcloud oc cluster addon disable cluster-autoscaler --cluster <cluster_name>
    ```
    {: pre}

    2. Verify the add-on is disabled.
    ```
    ibmcloud oc cluster addon ls --cluster <cluster_name>
    ```
    {: pre}

    **Helm chart**
    1. List your existing Helm charts and note the name of the cluster autoscaler.
        ```
        helm list --all-namespaces
        ```
        {: pre}

    2. Remove the existing Helm chart from your cluster.
        ```
        helm uninstall ibm-iks-cluster-autoscaler -n <namespace>
        ```
        {: pre}



## Cluster autoscaler add-on parameter reference
{: #ca_addon_ref}

This table refers to the cluster autoscaler add-on parameters. For Helm chart values, see [Cluster autoscaler Helm chart parameter reference](#ca_helm_ref)
{: note}

<table summary="The columns are read from left to right. The first column has the parameter of the configuration values. The second column describes the parameter. The third column includes the default value of the parameter.">
<caption>Cluster autoscaler configuration values</caption>
<col width="25%">
<thead>
<th>Parameter</th>
<th>Description</th>
<th>Default value</th>
</thead>
<tbody>
<tr>
<td><code>expander</code></td>
<td>Specify how the cluster autoscaler determines which worker pool to scale if you have multiple worker pools. Possible values are:
<ul><li><code>random</code>: Selects randomly between <code>most-pods</code> and <code>least-waste</code>.</li>
<li><code>most-pods</code>: Selects the worker pool that is able to schedule the most pods when scaling up. Use this method if you are using <code>nodeSelector</code> to make sure that pods land on specific worker nodes.</li>
<li><code>least-waste</code>: Selects the worker pool that has the least unused CPU after scaling up. If two worker pools use the same amount of CPU resources after scaling up, the worker pool with the least unused memory is selected.</li></ul></td>
<td>random</td>
</tr>
<tr>
<td><code>ignoreDaemonSetsUtilization</code></td>
<td>When set to <code>true</code>, the cluster autoscaler ignores DaemonSet pods when it calculates resource utilization for scale-down.</td>
<td><code>false</code></td>
</tr>
<tr>
<td><code>imagePullPolicy</code></td>
<td>Specify when to pull the Docker image. Possible values are:
<ul><li><code>Always</code>: Pulls the image every time that the pod is started.</li>
<li><code>IfNotPresent</code>: Pulls the image only if the image is not already present locally.</li>
<li><code>Never</code>: Assumes that the image exists locally and never pulls the image.</li></ul></td>
<td><code>Always</code></td>
</tr>
<tr>
<td><code>livenessProbeFailureThreshold</code></td>
<td>Specify the number of times that the <code>kubelet</code> retries a liveness probe after the pod starts and the first liveness probe fails. After the failure threshold is reached, the container is restarted and the pod is marked <code>Unready</code> for a readiness probe, if applicable.</td>
<td><code>3</code></td>
</tr>
<tr>
<td><code>livenessProbePeriodSeconds</code></td>
<td>Specify the interval in seconds that the <code>kubelet</code> performs a liveness probe.</td>
<td><code>10</code></td>
</tr>
<tr>
<td><code>livenessProbeTimeoutSeconds</code></td>
<td>Specify the time in seconds after which the liveness probe times out.</td>
<td><code>10</code></td>
</tr>
<tr>
<tr>
<td><code>maxBulkSoftTaintCount</code></td>
<td>Set the maximum number of worker nodes that can be tainted or untainted with <code>PreferNoSchedule</code> at the same time. To disable this feature, set to <code>0</code>.</td>
<td><code>0</code></td>
</tr>
<tr>
<td><code>maxBulkSoftTaintTime</code></td>
<td>Set the maximum amount of time that worker nodes can be tainted or untainted with <code>PreferNoSchedule</code> at the same time.</td>
<td><code>10m</code></td>
</tr>
<tr>
<tr>
<td><code>maxFailingTime</code></td>
<td>Set the maximum time in minutes that the cluster autoscaler pod runs without a successfully completed action before the pod is automatically restarted.</td>
<td><code>15m</code></td>
</tr>
<td><code>maxInactivity</code></td>
<td>Set the maximum time in minutes that the cluster autoscaler pod runs without any recorded activity before the pod is automatically restarted.</td>
<td><code>10m</code></td>
</tr>
<tr>
<td><code>maxNodeProvisionTime</code></td>
<td>Set the maximum amount of time in minutes that a worker node can take to begin provisioning before the cluster autoscaler cancels the scale-up request.</td>
<td><code>120m</code></td>
</tr>
<tr>
<td><code>maxRetryGap</code></td>
<td>Set the maximum time in seconds to retry after failing to connect to the service API. Use this parameter and the <code>retryAttempts</code> parameter to adjust the retry window for the cluster autoscaler.</td>
<td>60</td>
</tr>
<tr>
<td><code>resourcesLimitsCPU</code></td>
<td>Set the maximum amount of worker node CPU that the <code>ibm-iks-cluster-autoscaler</code> pod can consume.</td>
<td><code>600m</code></td>
</tr>
<tr>
<td><code>resourcesLimitsMemory</code></td>
<td>Set the maximum amount of worker node memory that the <code>ibm-iks-cluster-autoscaler</code> pod can consume.</td>
<td><code>600Mi</code></td>
</tr>
<tr>
<td><code>resourcesRequestsCPU</code></td>
<td>Set the minimum amount of worker node CPU that the <code>ibm-iks-cluster-autoscaler</code> pod starts with.</td>
<td><code>200m</code></td>
</tr>
<tr>
<td><code>resourcesRequestsMemory</code></td>
<td>Set the minimum amount of worker node memory that the <code>ibm-iks-cluster-autoscaler</code> pod starts with.</td>
<td><code>200Mi</code></td>
</tr>
<tr>
<td><code>retryAttempts</code></td>
<td>Set the maximum number of attempts to retry after failing to connect to the service API. Use this parameter and the <code>maxRetryGap</code> parameter to adjust the retry window for the cluster autoscaler.</td>
<td>64</td>
</tr>
<tr>
<td><code>scaleDownDelayAfterAdd</code></td>
<td>Set the amount of time after scale up that scale down evaluation resumes. The default value for <code>scaleDownDelayAfterAdd</code> is 10 minutes.</td>
<td><code>10m</code></td>
<td><code>scaleDownDelayAfterDelete</code></td>
<td>Set the amount of time after node deletion that scale down evaluation resumes. The default value for <code>scaleDownDelayAfterDelete</code> is the same as the <code>scan-interval</code> which is <code>1m</code>.</td>
<td><code>1m</code></td>
</tr>
<tr>
<td><code>scaleDownUnneededTime</code></td>
<td>Set the amount of time in minutes that a worker node must be unnecessary before it can be scaled down.</td>
<td><code>10m</code></td>
</tr>
<tr>
<td><code>scaleDownUtilizationThreshold</code></td>
<td>Set the worker node utilization threshold. If the worker node utilization goes below the threshold, the worker node is considered to be scaled down. Worker node utilization is calculated as the sum of the CPU and memory resources that are requested by all pods that run on the worker node, divided by the worker node resource capacity.</td>
<td><code>0.5</code></td>
</tr>
<tr>
<td><code>scanInterval</code></td>
<td>Set how often in minutes that the cluster autoscaler scans for workload usage that triggers scaling up or down.</td>
<td><code>1m</code></td>
</tr>
<tr>
<td><code>skipNodesWithLocalStorage</code></td>
<td>When set to <code>true</code>, worker nodes that have pods that are saving data to local storage are not scaled down.</td>
<td><code>true</code></td>
</tr>
<tr>
<td><code>skipNodesWithSystemPods</code></td>
<td>When set to <code>true</code>, worker nodes that have <code>kube-system</code> pods are not scaled down. Do not set the value to <code>false</code> because scaling down <code>kube-system</code> pods might have unexpected results.</td>
<td><code>true</code></td>
</tr>
<tr>
<td><code>workerPoolsConfig.json</code></td>
<td>The worker pools that you want to autoscale, including their minimum and maximum number of worker nodes per zone:
    <ul><li><code>{"name": "&lt;pool_name&gt;","minSize": 1,"maxSize": 2,"enabled":false}</code>.</li>
    <li><strong><code>&lt;pool_name&gt;</code></strong>: The name or ID of the worker pool that you want to enable or disable for autoscaling. To list available worker pools, run <code>ibmcloud oc worker-pool ls --cluster &lt;cluster_name_or_ID&gt;</code>.</li>
    <li><strong><code>maxSize: &lt;number_of_workers&gt;</code></strong>: Specify the maximum number of worker nodes per zone that the cluster autoscaler can scale up to. The value must be equal to or greater than the value that you set for the <code>minSize: &lt;number_of_workers&gt;</code> size.</li>
    <li><strong><code>min=&lt;number_of_workers&gt;</code></strong>: Specify the minimum number of worker nodes per zone that the cluster autoscaler can scale down to. The value must be <code>2</code> or greater so that your ALB pods can be spread for high availability. If you <a href="/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure">disabled</a> all public ALBs in each zone of your standard cluster, you can set the value to <code>1</code>.<p class="note">Keep in mind that setting a <code>min</code> size does not automatically trigger a scale-up. The <code>min</code> size is a threshold so that the cluster autoscaler does not scale below this minimum number of worker nodes per zone. If your cluster does not have this number of worker nodes per zone yet, the cluster autoscaler does not scale up until you have workload resource requests that require more resources.</p></li>
    <li><strong><code>enabled=(true|false)</code></strong>: Set the value to <code>true</code> to enable the cluster autoscaler to scale your worker pool. Set the value to <code>false</code> to stop the cluster autoscaler from scaling the worker pool. Later, if you want to <a href="/docs/openshift?topic=openshift-ca#ca_rm">remove the cluster autoscaler</a>, you must first disable each worker pool in the configmap.</li></ul>
    <p class="note">If you enable a worker pool for autoscaling and then later add a zone to this worker pool, restart the cluster autoscaler pod so that it picks up this change: <code>oc delete pod -n kube-system &lt;cluster_autoscaler_pod&gt;</code>.</p>
    <br><br>By default, the <code>default</code> worker pool is <strong>not</strong> enabled, with a <code>max</code> value of <code>2</code> and a <code>min</code> value of <code>1</code>.</td><td>Disabled</td>
</tbody>
</table>

## Cluster autoscaler Helm chart parameter reference
{: #ca_helm_ref}

This table refers to the cluster autoscaler Helm chart parameters. For add-on values, see [Cluster autoscaler add-on parameter reference](#ca_addon_ref)
{: note}

<table summary="The columns are read from left to right. The first column has the parameter of the configuration. The second column describes the parameter. The third column has the default vale of the parameter.">
<caption>Cluster autoscaler configuration values</caption>
<col width="25%">
<thead>
<th>Parameter</th>
<th>Description</th>
<th>Default value</th>
</thead>
<tbody>
<tr>
<td><code>api_route</code> parameter</td>
<td>Set the <a href="/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cli_api">{{site.data.keyword.openshiftlong_notm}} API endpoint</a> for the region that your cluster is in.</td>
<td>No default; uses the targeted region that your cluster is in.</td>
</tr>
<tr>
<td><code>resources.limits.cpu</code> parameter</td>
<td>Set the maximum amount of worker node CPU that the <code>ibm-iks-cluster-autoscaler</code> pod can consume.</td>
<td><code>300m</code></td>
</tr>
<tr>
<td><code>resources.limits.memory</code> parameter</td>
<td>Set the maximum amount of worker node memory that the <code>ibm-iks-cluster-autoscaler</code> pod can consume.</td>
<td><code>300Mi</code></td>
</tr>
<tr>
<td><code>resources.requests.cpu</code> parameter</td>
<td>Set the minimum amount of worker node CPU that the <code>ibm-iks-cluster-autoscaler</code> pod starts with.</td>
<td><code>100m</code></td>
</tr>
<tr>
<td><code>resources.requests.memory</code> parameter</td>
<td>Set the minimum amount of worker node memory that the <code>ibm-iks-cluster-autoscaler</code> pod starts with.</td>
<td><code>100Mi</code></td>
</tr>
<tr>
<td><code>maxNodeProvisionTime</code> parameter</td>
<td>Set the maximum amount of time in minutes that a worker node can take to begin provisioning before the cluster autoscaler cancels the scale-up request.</td>
<td><code>120m</code></td>
</tr>
<tr>
<td><code>scaleDownUnneededTime</code> parameter</td>
<td>Set the amount of time in minutes that a worker node must be unnecessary before it can be scaled down.</td>
<td><code>10m</code></td>
</tr>
<tr>
<td><code>scaleDownDelayAfterAdd</code></td>
<td>Set the amount of time after scale up that scale down evaluation resumes. The default value for <code>scaleDownDelayAfterAdd</code> is 10 minutes.</td>
<td><code>10m</code></td>
<td><code>scaleDownDelayAfterDelete</code></td>
<td>Set the amount of time after node deletion that scale down evaluation resumes. The default value for <code>scaleDownDelayAfterDelete</code> is the same as the <code>scan-interval</code> which is <code>1m</code>.</td>
<td><code>1m</code></td>
</tr>
<tr>
<td><code>scaleDownUtilizationThreshold</code> parameter</td>
<td>Set the worker node utilization threshold. If the worker node utilization goes below the threshold, the worker node is considered to be scaled down. Worker node utilization is calculated as the sum of the CPU and memory resources that are requested by all pods that run on the worker node, divided by the worker node resource capacity.</td>
<td><code>0.5</code></td>
</tr>
<tr>
<td><code>scanInterval</code> parameter</td>
<td>Set how often in minutes that the cluster autoscaler scans for workload usage that triggers scaling up or down.</td>
<td><code>1m</code></td>
</tr>
<tr>
<td><code>expander</code> parameter</td>
<td>Specify how the cluster autoscaler determines which worker pool to scale if you have multiple worker pools. Possible values are:
<ul><li><code>random</code>: Selects randomly between <code>most-pods</code> and <code>least-waste</code>.</li>
<li><code>most-pods</code>: Selects the worker pool that is able to schedule the most pods when scaling up. Use this method if you are using <code>nodeSelector</code> to make sure that pods land on specific worker nodes.</li>
<li><code>least-waste</code>: Selects the worker pool that has the least unused CPU after scaling up. If two worker pools use the same amount of CPU resources after scaling up, the worker pool with the least unused memory is selected.</li></ul></td>
<td>random</td>
</tr>
<tr>
<td><code>ignoreDaemonSetsUtilization</code></td>
<td>When set to <code>true</code>, the cluster autoscaler ignores DaemonSet pods when it calculates resource utilization for scale-down.</td>
<td><code>false</code></td>
</tr>
<tr>
<td><code>maxBulkSoftTaintCount</code></td>
<td>Set the maximum number of worker nodes that can be tainted or untainted with <code>PreferNoSchedule</code> at the same time. To disable this feature, set to <code>0</code>.</td>
<td><code>0</code></td>
</tr>
<tr>
<td><code>maxBulkSoftTaintTime</code> </td>
<td>Set the maximum amount of time that worker nodes can be tainted or untainted with <code>PreferNoSchedule</code> at the same time.</td>
<td><code>10m</code></td>
</tr>
<tr>
<td><code>skipNodes.withLocalStorage</code> parameter</td>
<td>When set to <code>true</code>, worker nodes that have pods that are saving data to local storage are not scaled down.</td>
<td><code>true</code></td>
</tr>
<tr>
<td><code>skipNodes.withSystemPods</code> parameter</td>
<td>When set to <code>true</code>, worker nodes that have <code>kube-system</code> pods are not scaled down. Do not set the value to <code>false</code> because scaling down <code>kube-system</code> pods might have unexpected results.</td>
<td><code>true</code></td>
</tr>
<tr>
<td><code>image.repository</code> parameter</td>
<td>Specify the cluster autoscaler Docker image to use. To get a list of cluster autoscaler images, target the global {{site.data.keyword.registrylong_notm}} API by running <code>ibmcloud cr region-set global</code>. Then, list the available cluster autoscaler images by running <code>ibmcloud cr images --include-ibm | grep cluster-autoscaler</code>. To review the supported Kubernetes versions for each cluster autoscaler image version, <a href="https://cloud.ibm.com/kubernetes/helm/iks-charts/ibm-iks-cluster-autoscaler">download the source code <code>tar</code> file</a> and open the <code>RELEASENOTES.MD</code> file.</td>
<td><code>icr.io/iks-charts/ibm-iks-cluster-autoscaler</code></td>
</tr>
<tr>
<td><code>image.pullPolicy</code> parameter</td>
<td>Specify when to pull the Docker image. Possible values are:
<ul><li><code>Always</code>: Pulls the image every time that the pod is started.</li>
<li><code>IfNotPresent</code>: Pulls the image only if the image is not already present locally.</li>
<li><code>Never</code>: Assumes that the image exists locally and never pulls the image.</li></ul></td>
<td><code>IfNotPreset</code></td>
</tr>
<tr>
    <td><code>livenessProbe.periodSeconds</code></td>
    <td>Specify the interval in seconds that the <code>kubelet</code> performs a liveness probe.</td>
    <td><code>10</code></td>
</tr>
<tr>
    <td><code>livenessProbe.failureThreshold</code></td>
    <td>Specify the number of times that the <code>kubelet</code> retries a liveness probe after the pod starts and the first liveness probe fails. After the failure threshold is reached, the container is restarted and the pod is marked <code>Unready</code> for a readiness probe, if applicable.</td>
    <td><code>3</code></td>
</tr>
<tr>
    <td><code>livenessProbe.successThreshold</code></td>
    <td>Specify the minimum, consecutive number of times that the liveness probe must be successful after a previous failure before the pod is marked <code>Ready</code>. If you set a liveness probe, you must set this value to at least <code>1</code>.</td>
    <td><code>1</code></td>
</tr>
<tr>
    <td><code>livenessProbe.timeoutSeconds</code></td>
    <td>Specify the time in seconds after which the liveness probe times out.</td>
    <td><code>10</code></td>
</tr>
<tr>
    <td><code>max-inactivity</code></td>
    <td>Set the maximum time in minutes that the cluster autoscaler pod runs without any recorded activity before the pod is automatically restarted.</td>
    <td><code>10m</code></td>
</tr>
<tr>
    <td><code>max-failing-time</code></td>
    <td>Set the maximum time in minutes that the cluster autoscaler pod runs without a successfully completed action before the pod is automatically restarted.</td>
    <td><code>15m</code></td>
</tr>
<tr>
<td><code>customImageVersion</code></td>
<td>To override the default installation version, specify the version of the cluster autoscaler Helm chart that you want to install.</td>
<td>N/A</td>
</tr>
<tr>
<td><code>maxRetryGap</code></td>
<td>Set the maximum time in seconds to retry after failing to connect to the service API. Use this parameter and the <code>retryAttempts</code> parameter to adjust the retry window for the cluster autoscaler.</td>
<td>60</td>
</tr>
<tr>
<td><code>retryAttempts</code></td>
<td>Set the maximum number of attempts to retry after failing to connect to the service API. Use this parameter and the <code>maxRetryGap</code> parameter to adjust the retry window for the cluster autoscaler.</td>
<td>32</td>
</tr>
<tr>
<td><code>workerpools</code> parameter</td>
<td>The worker pools that you want to autoscale, including their minimum and maximum number of worker nodes per zone. These settings are mirrored in the <a href="#ca_cm">cluster autoscaler config map</a>. To set the worker pool, format the option as follows: <code>--set workerpools[0].&lt;pool_name&gt;.max=&lt;number_of_workers&gt;,workerpools[0].&lt;pool_name&gt;.min=&lt;number_of_workers&gt;,workerpools[0].&lt;pool_name&gt;.enabled=(true|false)</code><br><br>
Understanding the <code>--set workerpools</code> options:
    <ul><li><strong><code>workerpools[0]</code></strong>: The first worker pool to enable or disable for autoscaling. You must include three parameters for each worker pool for the command to succeed: the maximum number of worker nodes (<code>max</code>), the minimum number of worker nodes (<code>min</code>), and whether you want to enable (<code>true</code>) or disable (<code>false</code>) autoscaling for this worker pool. To include multiple worker pools, include a comma-separated list and increase the number in brackets, such as: <code>workerpools[0].default...,workerpools[1].pool1...,workerpools[2].pool2...</code>.</li>
    <li><strong><code>&lt;pool_name&gt;</code></strong>: The name or ID of the worker pool that you want to enable or disable for autoscaling. To list available worker pools, run <code>ibmcloud oc worker-pool ls --cluster &lt;cluster_name_or_ID&gt;</code>.</li>
    <li><strong><code>max=&lt;number_of_workers></code></strong>: Specify the maximum number of worker nodes per zone that the cluster autoscaler can scale up to. The value must be equal to or greater than the value that you set for the <code>min=&lt;number_of_workers&gt;</code> size.</li>
    <li><strong><code>min=&lt;number_of_workers&gt;</code></strong>: Specify the minimum number of worker nodes per zone that the cluster autoscaler can scale down to. The value must be <code>2</code> or greater so that your ALB pods can be spread for high availability. If you [disabled</a> all public ALBs in each zone of your standard cluster, you can set the value to <code>1</code>.<p class="note">Keep in mind that setting a <code>min</code> size does not automatically trigger a scale-up. The <code>min</code> size is a threshold so that the cluster autoscaler does not scale below this minimum number of worker nodes per zone. If your cluster does not have this number of worker nodes per zone yet, the cluster autoscaler does not scale up until you have workload resource requests that require more resources.</p></li>
    <li><strong><code>enabled=(true|false)</code></strong>: Set the value to <code>true</code> to enable the cluster autoscaler to scale your worker pool. Set the value to <code>false</code> to stop the cluster autoscaler from scaling the worker pool. Later, if you want to <a href="/docs/openshift?topic=openshift-ca#ca_rm">remove the cluster autoscaler</a>, you must first disable each worker pool in the configmap.</li></ul>
    <p class="note">If you enable a worker pool for autoscaling and then later add a zone to this worker pool, restart the cluster autoscaler pod so that it picks up this change: <code>oc delete pod -n kube-system &lt;cluster_autoscaler_pod&gt;</code>.</p>
    <br><br>By default, the <code>default</code> worker pool is <strong>not</strong> enabled, with a <code>max</code> value of <code>2</code> and a <code>min</code> value of <code>1</code>.</td><td>Disabled</td>
</tbody>
</table>




