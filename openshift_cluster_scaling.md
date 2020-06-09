---

copyright:
  years: 2014, 2020
lastupdated: "2020-06-09"

keywords: openshift, roks, rhoks, rhos, node scaling, ca, autoscaler

subcollection: openshift

---

{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}


# Autoscaling clusters
{: #ca}

With the `ibm-iks-cluster-autoscaler` plug-in, you can scale the worker pools in your {{site.data.keyword.openshiftlong}} cluster automatically to increase or decrease the number of worker nodes in the worker pool based on the sizing needs of your scheduled workloads. The `ibm-iks-cluster-autoscaler` plug-in is based on the [Kubernetes Cluster-Autoscaler project](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler).
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

The cluster autoscaler adjusts the number of worker nodes by considering the [resource requests](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/){: external} that you define for your deployments, not actual worker node usage. If your pods and deployments don't request appropriate amounts of resources, you must adjust their configuration files. The cluster autoscaler can't adjust them for you. Also, keep in mind that worker nodes use some of their compute resources for basic cluster functionality, default and custom [add-ons](/docs/openshift?topic=openshift-update#addons), and [resource reserves](/docs/openshift?topic=openshift-planning_worker_nodes#resource_limit_node).
{: note}

<br>
**What does scaling up and down look like?**<br>
In general, the cluster autoscaler calculates the number of worker nodes that your cluster needs to run its workload. Scaling the cluster up or down depends on many factors, including the following.
*   The minimum and maximum worker node size per zone that you set.
*   Your pending pod resource requests and certain metadata that you associate with the workload, such as anti-affinity, labels to place pods only on certain flavors, or [pod disruption budgets](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/){: external}.
*   The worker pools that the cluster autoscaler manages, potentially across zones in a [multizone cluster](/docs/openshift?topic=openshift-ha_clusters#multizone).
*   The [custom Helm chart values](#ca_chart_values) that are set, such as skipping worker nodes for deletion if they use local storage.

For more information, see the Kubernetes Cluster Autoscaler FAQs for [How does scale-up work?](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-scale-up-work){: external} and [How does scale-down work?](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-scale-down-work){: external}.

<br>

**Can I change how scale-up and scale-down work?**<br>
You can customize settings or use other Kubernetes resources to affect how scaling up and down work.
* **Scale-up**: [Customize the cluster autoscaler Helm chart values](#ca_chart_values) such as `scanInterval`, `expander`, `skipNodes`, or `maxNodeProvisionTime`. Review ways to [overprovision worker nodes](#ca_scaleup) so that you can scale up worker nodes before a worker pool runs out of resources. You can also [set up Kubernetes pod budget disruptions and pod priority cutoffs](#scalable-practices-apps) to affect how scaling up works.
* **Scale-down**: [Customize the cluster autoscaler Helm chart values](#ca_chart_values) such as `scaleDownUnneededTime`, `scaleDownDelayAfterAdd`, `scaleDownDelayAfterDelete`, or `scaleDownUtilizationThreshold`.

<br>
**Can I set the minimum size per zone to immediately scale up my cluster to that size?**<br>
No, setting a `minSize` does not automatically trigger a scale-up. The `minSize` is a threshold so that the cluster autoscaler does not scale below a certain number of worker nodes per zone. If your cluster does not yet have that number per zone, the cluster autoscaler does not scale up until you have workload resource requests that require more resources. For example, if you have a worker pool with one worker node per three zones (three total worker nodes) and set the `minSize` to `4` per zone, the cluster autoscaler does not immediately provision an additional three worker nodes per zone (12 worker nodes total). Instead, the scale-up is triggered by resource requests. If you create a workload that requests the resources of 15 worker nodes, the cluster autoscaler scales up the worker pool to meet this request. Now, the `minSize` means that the cluster autoscaler does not scale down below four worker nodes per zone even if you remove the workload that requests the amount.

<br>
**How is this behavior different from worker pools that are not managed by the cluster autoscaler?**<br>
When you [create a worker pool](/docs/openshift?topic=openshift-add_workers#add_pool), you specify how many worker nodes per zone it has. The worker pool maintains that number of worker nodes until you [resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) or [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) it. The worker pool does not add or remove worker nodes for you. If you have more pods than can be scheduled, the pods remain in pending state until you resize the worker pool.

When you enable the cluster autoscaler for a worker pool, worker nodes are scaled up or down in response to your pod spec settings and resource requests. You don't need to resize or rebalance the worker pool manually.

<br>
**Can I see an example of how the cluster autoscaler scales up and down?**<br>
Consider the following image for an example of scaling the cluster up and down.

_Figure: Autoscaling a cluster up and down._
![Autoscaling a cluster up and down GIF](images/cluster-autoscaler-x3.gif){: gif}

1.  The cluster has four worker nodes in two worker pools that are spread across two zones. Each pool has one worker node per zone, but **Worker Pool A** has a flavor of `u2c.2x4` and **Worker Pool B** has a flavor of `b2c.4x16`. Your total compute resources are roughly 10 cores (2 cores x 2 worker nodes for **Worker Pool A**, and 4 cores x 2 worker nodes for **Worker Pool B**). Your cluster currently runs a workload that requests 6 of these 10 cores. Additional computing resources are taken up on each worker node by the [reserved resources](/docs/openshift?topic=openshift-planning_worker_nodes#resource_limit_node) that are required to run the cluster, worker nodes, and any add-ons such as the cluster autoscaler.
2.  The cluster autoscaler is configured to manage both worker pools with the following minimum and maximum size-per-zone:
    *  **Worker Pool A**: `minSize=1`, `maxSize=5`.
    *  **Worker Pool B**: `minSize=1`, `maxSize=2`.
3.  You schedule deployments that require 14 additional pod replicas of an app that requests one core of CPU per replica. One pod replica can be deployed on the current resources, but the other 13 are pending.
4.  The cluster autoscaler scales up your worker nodes within these constraints to support the additional 13 pod replicas resource requests.
    *  **Worker Pool A**: Seven worker nodes are added in a round-robin method as evenly as possible across the zones. The worker nodes increase the cluster compute capacity by roughly 14 cores (2 cores x 7 worker nodes).
    *  **Worker Pool B**: Two worker nodes are added evenly across the zones, reaching the `maxSize` of two worker nodes per zone. The worker nodes increase cluster capacity by roughly 8 cores (4 cores x 2 worker node).
5.  The 20 pods with one-core requests are distributed as follows across the worker nodes. Because worker nodes have resource reserves as well as pods that run to cover default cluster features, the pods for your workload cannot use all the available compute resources of a worker node. For example, although the `b2c.4x16` worker nodes have four cores, only three pods that request a minimum of one core each can be scheduled onto the worker nodes.
    <table summary="A table that describes the distribution of workload in scaled cluster.">
    <caption>Distribution of workload in scaled cluster.</caption>
    <thead>
    <tr>
      <th>Worker Pool</th>
      <th>Zone</th>
      <th>Type</th>
      <th># worker nodes</th>
      <th># pods</th>
    </tr>
    </thead>
    <tbody>
    <tr>
      <td>A</td>
      <td>dal10</td>
      <td>u2c.2x4</td>
      <td>Four nodes</td>
      <td>Three pods</td>
    </tr>
    <tr>
      <td>A</td>
      <td>dal12</td>
      <td>u2c.2x4</td>
      <td>Five nodes</td>
      <td>Five pods</td>
    </tr>
    <tr>
      <td>B</td>
      <td>dal10</td>
      <td>b2c.4x16</td>
      <td>Two nodes</td>
      <td>Six pods</td>
    </tr>
    <tr>
      <td>B</td>
      <td>dal12</td>
      <td>b2c.4x16</td>
      <td>Two nodes</td>
      <td>Six pods</td>
    </tr>
    </tbody>
    </table>
6.  You no longer need the additional workload, so you delete the deployment. After a short period of time, the cluster autoscaler detects that your cluster no longer needs all its compute resources and scales down the worker nodes one at a time.
7.  Your worker pools are scaled down. The cluster autoscaler scans at regular intervals to check for pending pod resource requests and underutilized worker nodes to scale your worker pools up or down.

## Following scalable deployment practices
{: #scalable-practices}

Make the most out of the cluster autoscaler by using the following strategies for your worker node and workload deployment strategies. For more information, see the [Kubernetes Cluster Autoscaler FAQs](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md){: external}.
{: shortdesc}

[Try out the cluster autoscaler](#ca_helm) with a few test workloads to get a good feel for how [scale-up and scale-down work](#ca_about), what [custom values](#ca_chart_values) you might want to configure, and any other aspects that you might want, like [overprovisioning](#ca_scaleup) worker nodes or [limiting apps](#ca_limit_pool). Then, clean up your test environment and plan to include these custom values and additional settings with a fresh installation of the cluster autoscaler.

### Can I autoscale multiple worker pools at once?
{: #scalable-practices-multiple}
Yes, after you install the Helm chart, you can choose which worker pools within the cluster to autoscale [in the configmap](#ca_cm). You can run only one `ibm-iks-cluster-autoscaler` Helm chart per cluster.
{: shortdesc}

### How can I make sure that the cluster autoscaler responds to what resources my app needs?
{: #scalable-practices-resrequests}

The cluster autoscaler scales your cluster in response to your workload [resource requests](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/){: external}. As such, specify [resource requests](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/){: external} for all your deployments because the resource requests are what the cluster autoscaler uses to calculate how many worker nodes are needed to run the workload. Keep in mind that autoscaling is based on the compute usage that your workload configurations request, and does not consider other factors such as machine costs.
{: shortdesc}

### Can I scale down a worker pool to zero (0) nodes?
{: #scalable-practices-zero}

No, you cannot set the cluster autoscaler `minSize` to `0`. Additionally, unless you [disable](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) all public application load balancers (ALBs) in each zone of your cluster, you must change the `minSize` to `2` worker nodes per zone so that the ALB pods can be spread for high availability.
{: shortdesc}

If your worker pool has zero (0) worker nodes, the worker pool cannot be scaled. [Disable cluster autoscaling](/docs/openshift?topic=openshift-ca#ca_cm) for the worker pool, [manually resize the worker pool](/docs/openshift?topic=openshift-add_workers#resize_pool) to at least one, and [re-enable cluster autoscaling](/docs/openshift?topic=openshift-ca#ca_cm).

### Can I optimize my deployments for autoscaling?
{: #scalable-practices-apps}

Yes, you can add several Kubernetes features to your deployment to adjust how the cluster autoscaler considers your resource requests for scaling.
{: shortdesc}
*   Use [pod disruption budgets](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/){: external} to prevent abrupt rescheduling or deletions of your pods.
*   If you're using pod priority, you can [edit the priority cutoff](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-cluster-autoscaler-work-with-pod-priority-and-preemption){: external} to change what types of priority trigger scaling up. By default, the priority cutoff is zero (`0`).

### Can I use taints and tolerations with autoscaled worker pools?
{: #scalable-practices-taints}

Yes, but make sure to apply taints at the worker pool level so that all existing and future worker nodes get the same taint. Then, you must include a [matching toleration in your workload configuration](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external} so that these workloads are scheduled onto your autoscaled worker pool with the matching taint. Keep in mind that if you deploy a workload that is not tolerated by the tainted worker nodes, the worker nodes are not considered for scale-up and more worker nodes might be ordered even if the cluster has sufficient capacity. However, the tainted worker nodes are still identified as underutilized if they have less than the threshold (by default 50%) of their resources utilized and thus are considered for scale-down.
{: shortdesc}

### Why are my autoscaled worker pools unbalanced?
{: #scalable-practices-unbalanced}

During a scale-up, the cluster autoscaler balances nodes across zones, with a permitted difference of plus or minus one (+/- 1) worker node. Your pending workloads might not request enough capacity to make each zone balanced. In this case, if you want to manually balance the worker pools, [update your cluster autoscaler configmap](#ca_cm) to remove the unbalanced worker pool. Then run the `ibmcloud oc worker-pool rebalance` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance), and add the worker pool back to the cluster autoscaler configmap.
{: shortdesc}


### Why can't I resize or rebalance my worker pool?
{: #scalable-practices-resize}

When the cluster autoscaler is enabled for a worker pool, you cannot [resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) or [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) your worker pools. You must [edit the configmap](#ca_cm) to change the worker pool minimum or maximum sizes, or disable cluster autoscaling for that worker pool. Don't use the `ibmcloud oc worker rm` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_rm) to remove individual worker nodes from your worker pool, which can unbalance the worker pool.
{: shortdesc}

Further, if you do not disable the worker pools before you uninstall the `ibm-iks-cluster-autoscaler` Helm chart, the worker pools cannot be resized manually. Reinstall the `ibm-iks-cluster-autoscaler` Helm chart, [edit the configmap](#ca_cm) to disable the worker pool, and try again.

<br />


## Deploying the cluster autoscaler Helm chart to your cluster
{: #ca_helm}

Install the {{site.data.keyword.cloud_notm}} cluster autoscaler plug-in with a Helm chart to autoscale worker pools in your cluster.
{: shortdesc}

**Before you begin**:

1.  [Install the required CLI and plug-ins](/docs/cli?topic=cli-getting-started):
    *  {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`)
    *  {{site.data.keyword.containerlong_notm}} plug-in (`ibmcloud oc` alias for OpenShift clusters)
    *  {{site.data.keyword.registrylong_notm}} plug-in (`ibmcloud cr`)
    *  Kubernetes (`kubectl`)
2.  [Create a standard cluster](/docs/openshift?topic=openshift-clusters).
3.  [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
4.  Confirm that your {{site.data.keyword.cloud_notm}} Identity and Access Management credentials are stored in the cluster. The cluster autoscaler uses this secret to authenticate credentials. If the secret is missing, [create it by resetting credentials](/docs/openshift?topic=openshift-cs_troubleshoot_storage#missing_permissions).
    ```
    oc get secrets -n kube-system | grep storage-secret-store
    ```
    {: pre}
5.  The cluster autoscaler can scale only worker pools that have the `ibm-cloud.kubernetes.io/worker-pool-id` label.
    1.  Check whether your worker pool has the required label.
        ```
        ibmcloud oc worker-pool get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID> | grep Labels
        ```
        {: pre}

        Example output of a worker pool with the label:
        ```
        Labels:             ibm-cloud.kubernetes.io/worker-pool-id=a1aa111111b22b22cc3c3cc444444d44-4d555e5
        ```
        {: screen}
    2.  If your worker pool does not have the required label, [add a new worker pool](/docs/openshift?topic=openshift-add_workers#add_pool) and use this worker pool with the cluster autoscaler.

<br>
**To install the `ibm-iks-cluster-autoscaler` plug-in in your cluster**:

1.  [Follow the instructions](/docs/openshift?topic=openshift-openshift_apps#roks_helm) to install the **Helm version 3** client on your local machine.

2.  Add and update the Helm repo where the cluster autoscaler Helm chart is.
    ```
    helm repo add iks-charts https://icr.io/helm/iks-charts
    ```
    {: pre}
    ```
    helm repo update
    ```
    {: pre}
3.  Decide if you want to [customize the cluster autoscaler settings](#ca_chart_values), such as the worker pools that are autoscaled, or the amount of time that the cluster autoscaler waits before scaling worker nodes up or down. You can customize your settings by using the `--set` flag in the `helm install` command. Depending on the settings that you want to customize, you might need to prepare multiple `--set` flags before you can install the Helm chart. For example, you might want to autoscale your default worker pool by preparing the following `--set` flag.
    ```
    --set workerpools[0].<pool_name>.max=<number_of_workers>,workerpools[0].<pool_name>.min=<number_of_workers>,workerpools[0].<pool_name>.enabled=(true|false)
    ```
    {: codeblock}

    Understanding the `--set workerpools` options:
    * **`workerpools[0]`**: The first worker pool to enable or disable for autoscaling. You must include three parameters for each worker pool for the command to succeed: the maximum number of worker nodes (`max`), the minimum number of worker nodes (`min`), and whether you want to enable (`true`) or disable (`false`) autoscaling for this worker pool. To include multiple worker pools, include a comma-separated list and increase the number in brackets, such as: `workerpools[0].default...,workerpools[1].pool1...,workerpools[2].pool2...`.
    * **`<pool_name>`**: The name or ID of the worker pool that you want to enable or disable for autoscaling. To list available worker pools, run `ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>`.
    * **`max=<number_of_workers>`**: Specify the maximum number of worker nodes per zone that the cluster autoscaler can scale up to. The value must be equal to or greater than the value that you set for the `min=<number_of_workers>` size.
    * **`min=<number_of_workers>`**: Specify the minimum number of worker nodes per zone that the cluster autoscaler can scale down to. The value must be `2` or greater so that your ALB pods can be spread for high availability. If you [disabled](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) all public ALBs in each zone of your standard cluster, you can set the value to `1`.<p class="note">Keep in mind that setting a `min` size does not automatically trigger a scale-up. The `min` size is a threshold so that the cluster autoscaler does not scale below this minimum number of worker nodes per zone. If your cluster does not have this number of worker nodes per zone yet, the cluster autoscaler does not scale up until you have workload resource requests that require more resources.</p>
    * **`enabled=(true|false)`**: Set the value to `true` to enable the cluster autoscaler to scale your worker pool. Set the value to `false` to stop the cluster autoscaler from scaling the worker pool. Later, if you want to [remove the cluster autoscaler](/docs/openshift?topic=openshift-ca#ca_rm), you must first disable each worker pool in the configmap.

4.  Install the cluster autoscaler Helm chart in the `kube-system` namespace of your cluster. In the example command, the default worker pool is enabled for autoscaling with the Helm chart installation. The worker pool details are added to the cluster autoscaler config map.

    <table class="simple-tab-table" id="helm3" tab-title="Helm 3 install command" tab-group="helm-install" aria-describedby="tableSummary-19ecbef4c01853826b42de82471b9035">
    <caption caption-side="top">
      Install the cluster autoscaler chart in Helm version 3<br>
      <span class="table-summary" id="tableSummary-19ecbef4c01853826b42de82471b9035">The row contains the installation command.</span>
    </caption>
    <thead>
    <tr>
    <th>Command</th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td><p><pre class="pre"><code>helm install ibm-iks-cluster-autoscaler iks-charts/ibm-iks-cluster-autoscaler --namespace kube-system --set workerpools[0].default.max=5,workerpools[0].default.min=2,workerpools[0].default.enabled=true</code></pre></p></td>
    </tr>
    </tbody>
    </table>
    <table class="simple-tab-table" id="helm2" tab-title="Helm 2 install command" tab-group="helm-install" aria-describedby="tableSummary-19ecbef4c01853826b42de82471b9034">
    <caption caption-side="top">
      Install the cluster autoscaler chart in Helm version 2<br>
      <span class="table-summary" id="tableSummary-19ecbef4c01853826b42de82471b9034">The row contains the installation command.</span>
    </caption>
    <thead>
    <tr>
    <th>Command</th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td><p><pre class="pre"><code>helm install iks-charts/ibm-iks-cluster-autoscaler --namespace kube-system --name ibm-iks-cluster-autoscaler --set workerpools[0].default.max=5,workerpools[0].default.min=2,workerpools[0].default.enabled=true</code></pre></p></td>
    </tr>
    </tbody>
    </table><p>Example output:</p>
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

5.  Verify that the installation is successful.

    1.  Check that the cluster autoscaler pod is in a **Running** state.
        ```
        oc get pods --namespace=kube-system | grep ibm-iks-cluster-autoscaler
        ```
        {: pre}
        Example output:
        ```
        ibm-iks-cluster-autoscaler-8497bfc968-dbn7w   1/1       Running   0          9m
        ```
        {: screen}
    2.  Check that the cluster autoscaler service is created.
        ```
        oc get service --namespace=kube-system | grep ibm-iks-cluster-autoscaler
        ```
        {: pre}
        Example output:
        ```
        ibm-iks-cluster-autoscaler   ClusterIP   172.21.xxx.xx    <none>        8085/TCP        9m
        ```
        {: screen}
    3.  Optional: If you enabled autoscaling for a worker pool during the Helm chart installation, verify that the config map is correct by checking that the `workerPoolsConfig.json` field is updated and that the `workerPoolsConfigStatus` field shows a `SUCCESS` message.
        ```
        oc get cm iks-ca-configmap -n kube-system -o yaml
        ```
        {: pre}

        Example output where the default worker pool is enabled for autoscaling:
        ```
        apiVersion: v1
        data:
          workerPoolsConfig.json: |
            [{"name": "default", "minSize": 1, "maxSize": 2, "enabled": true }]
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

6.  Repeat these steps for every cluster where you want to provision the cluster autoscaler.

7.  Optional: If you did not set any worker pools for autoscaling with the installation, you can [Update the cluster autoscaler configuration](#ca_cm).

<br />


## Updating the cluster autoscaler configmap to enable scaling
{: #ca_cm}

Update the cluster autoscaler configmap to enable automatically scaling worker nodes in your worker pools based on the minimum and maximum values that you set.
{: shortdesc}

After you edit the configmap to enable a worker pool, the cluster autoscaler scales your cluster in response to your workload requests. As such, you cannot [resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) or [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) your worker pools. Scanning and scaling up and down happens at regular intervals over time, and depending on the number of worker nodes might take a longer period of time to complete, such as 30 minutes. Later, if you want to [remove the cluster autoscaler](#ca_rm), you must first disable each worker pool in the configmap.
{: note}

**Before you begin**:
*  [Install the `ibm-iks-cluster-autoscaler` plug-in](#ca_helm).
*  [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

**To update the cluster autoscaler configmap and values**:

1.  Edit the cluster autoscaler configmap YAML file.
    ```
    oc edit cm iks-ca-configmap -n kube-system -o yaml
    ```
    {: pre}
    Example output:
    ```
    apiVersion: v1
    data:
      workerPoolsConfig.json: |
        [
         {"name": "default","minSize": 1,"maxSize": 2,"enabled":false}
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
2.  Edit the configmap with the parameters to define how the cluster autoscaler scales your cluster worker pool. **Note:** Unless you [disabled](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) all public application load balancers (ALBs) in each zone of your standard cluster, you must change the `minSize` to `2` per zone so that the ALB pods can be spread for high availability.

    <table>
    <caption>Cluster autoscaler configmap parameters</caption>
    <col width="20%">
    <thead>
    <th id="parameter-with-default">Parameter with default value</th>
    <th id="parameter-with-description">Description</th>
    </thead>
    <tbody>
    <tr>
    <td id="parameter-name" headers="parameter-with-default">`"name": "default"`</td>
    <td headers="parameter-name parameter-with-description">Replace `"default"` with the name or ID of the worker pool that you want to scale. To list worker pools, run `ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>`.<br><br>
    To manage more than one worker pool, copy the JSON line to a comma-separated line, such as follows. <pre class="codeblock">[
     {"name": "default","minSize": 1,"maxSize": 2,"enabled":false},
     {"name": "Pool2","minSize": 2,"maxSize": 5,"enabled":true}
    ]</pre><br><br>
    <p class="note">The cluster autoscaler can scale only worker pools that have the `ibm-cloud.kubernetes.io/worker-pool-id` label. To check whether your worker pool has the required label, run `ibmcloud oc worker-pool get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID> | grep Labels`. If your worker pool does not have the required label, [add a new worker pool](/docs/openshift?topic=openshift-add_workers#add_pool) and use this worker pool with the cluster autoscaler.</p></td>
    </tr>
    <tr>
    <td id="parameter-minsize" headers="parameter-with-default">`"minSize": 1`</td>
    <td headers="parameter-minsize parameter-with-description">Specify the minimum number of worker nodes per zone that the cluster autoscaler can scale down the worker pool to. The value must be `2` or greater so that your ALB pods can be spread for high availability. If you [disabled](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) all public ALBs in each zone of your standard cluster, you can set the value to `1`.
    <p class="note">Setting a `minSize` does not automatically trigger a scale-up. The `minSize` is a threshold so that the cluster autoscaler does not scale below a certain number of worker nodes per zone. If your cluster does not yet have that number per zone, the cluster autoscaler does not scale up until you have workload resource requests that require more resources. For example, if you have a worker pool with one worker node per three zones (three total worker nodes) and set the `minSize` to `4` per zone, the cluster autoscaler does not immediately provision an additional three worker nodes per zone (12 worker nodes total). Instead, the scale-up is triggered by resource requests. If you create a workload that requests the resources of 15 worker nodes, the cluster autoscaler scales up the worker pool to meet this request. Now, the `minSize` means that the cluster autoscaler does not scale down below four worker nodes per zone even if you remove the workload that requests the amount. For more information, see the [Kubernetes docs](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#when-does-cluster-autoscaler-change-the-size-of-a-cluster).</p></td>
    </tr>
    <tr>
    <td id="parameter-maxsize" headers="parameter-with-default">`"maxSize": 2`</td>
    <td headers="parameter-maxsize parameter-with-description">Specify the maximum number of worker nodes per zone that the cluster autoscaler can scale up the worker pool to. The value must be equal to or greater than the value that you set for the `minSize`.</td>
    </tr>
    <tr>
    <td id="parameter-enabled" headers="parameter-with-default">`"enabled": false`</td>
    <td headers="parameter-enabled parameter-with-description">Set the value to `true` for the cluster autoscaler to manage scaling for the worker pool. Set the value to `false` to stop the cluster autoscaler from scaling the worker pool.<br><br>
    Later, if you want to [remove the cluster autoscaler](#ca_rm), you must first disable each worker pool in the configmap.</td>
    </tr>
    </tbody>
    </table>
3.  Save the configuration file.
4.  Get your cluster autoscaler pod.
    ```
    oc get pods -n kube-system
    ```
    {: pre}
5.  Review the **`Events`** section of the cluster autoscaler pod for a **`ConfigUpdated`** event to verify that the configmap is successfully updated. The event message for your configmap is in the following format: `minSize:maxSize:PoolName:<SUCCESS|FAILED>:error message`.

    ```
    oc describe pod -n kube-system <cluster_autoscaler_pod>
    ```
    {: pre}

    Example output:
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

<p class="note">If you enable a worker pool for autoscaling and then later add a zone to this worker pool, restart the cluster autoscaler pod so that it picks up this change: `oc delete pod -n kube-system <cluster_autoscaler_pod>`.</p>

## Customizing the cluster autoscaler Helm chart configuration values
{: #ca_chart_values}

Customize the cluster autoscaler settings such as the amount of time it waits before scaling worker nodes up or down.
{: shortdesc}

**Before you begin**:
*  [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
*  [Install the `ibm-iks-cluster-autoscaler` plug-in](#ca_helm).

**To update the cluster autoscaler values**:

1.  Review the cluster autoscaler Helm chart configuration values. The cluster autoscaler comes with default settings. However, you might want to change some values such as the scale-down or scanning intervals, depending on how often you change your cluster workloads.
    ```
    helm get values ibm-iks-cluster-autoscaler -a
    ```
    {: pre}

    Example output:
    ```
    resources:
      limits:
        cpu: 600m
        memory: 600Mi
      requests:
        cpu: 200m
        memory: 200Mi
    maxNodeProvisionTime: 120m
    scaleDownUnneededTime: 10m
    scaleDownDelayAfterAdd: 10m
    scaleDownDelayAfterDelete: 10m
    scaleDownUtilizationThreshold: 0.5
    scanInterval: 1m
    expander: random
    ignoreDaemonSetsUtilization: false
    maxBulkSoftTaintCount: 0
    maxBulkSoftTaintTime: 10m
    extractor: ""
    skipNodes:
      withLocalStorage: true
      withSystemPods: true
    image:
      repository: icr.io/ibm/ibmcloud-cluster-autoscaler
      pullPolicy: Always
    livenessProbe:
      periodSeconds: 10
      failureThreshold: 3
      successThreshold: 1
      timeoutSeconds: 10
    maxInactivityTimeFlag: 10m
    maxFailingTimeFlag: 15m
    customImageVersion: ""
    maxRetryGap: "60"
    retryAttempts: "32"
    workerpools:
      - default:
          max: 2
          min: 1
          enabled: false
    ```
    {: screen}

    Understanding the parameters and default values:
    <table>
    <caption>Cluster autoscaler configuration values</caption>
    <col width="25%">
    <thead>
    <th>Parameter</th>
    <th>Description</th>
    <th>Default value</th>
    </thead>
    <tbody>
    <tr>
    <td>`api_route` parameter</td>
    <td>Set the [Red Hat OpenShift on IBM Cloud API endpoint](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cli_api) for the region that your cluster is in.</td>
    <td>No default; uses the targeted region that your cluster is in.</td>
    </tr>
    <tr>
    <td>`resources.limits.cpu` parameter</td>
    <td>Set the maximum amount of worker node CPU that the `ibm-iks-cluster-autoscaler` pod can consume.</td>
    <td>`300m`</td>
    </tr>
    <tr>
    <td>`resources.limits.memory` parameter</td>
    <td>Set the maximum amount of worker node memory that the `ibm-iks-cluster-autoscaler` pod can consume.</td>
    <td>`300Mi`</td>
    </tr>
    <tr>
    <td>`resources.requests.cpu` parameter</td>
    <td>Set the minimum amount of worker node CPU that the `ibm-iks-cluster-autoscaler` pod starts with.</td>
    <td>`100m`</td>
    </tr>
    <tr>
    <td>`resources.requests.memory` parameter</td>
    <td>Set the minimum amount of worker node memory that the `ibm-iks-cluster-autoscaler` pod starts with.</td>
    <td>`100Mi`</td>
    </tr>
    <tr>
    <td>`maxNodeProvisionTime` parameter</td>
    <td>Set the maximum amount of time in minutes that a worker node can take to begin provisioning before the cluster autoscaler cancels the scale-up request.</td>
    <td>`120m`</td>
    </tr>
    <tr>
    <td>`scaleDownUnneededTime` parameter</td>
    <td>Set the amount of time in minutes that a worker node must be unnecessary before it can be scaled down.</td>
    <td>`10m`</td>
    </tr>
    <tr>
    <td>`scaleDownDelayAfterAdd`, `scaleDownDelayAfterDelete` parameters</td>
    <td>Set the amount of time in minutes that the cluster autoscaler waits to start scaling actions again after scaling up (`add`) or scaling down (`delete`).</td>
    <td>`10m`</td>
    </tr>
    <tr>
    <td>`scaleDownUtilizationThreshold` parameter</td>
    <td>Set the worker node utilization threshold. If the worker node utilization goes below the threshold, the worker node is considered to be scaled down. Worker node utilization is calculated as the sum of the CPU and memory resources that are requested by all pods that run on the worker node, divided by the worker node resource capacity.</td>
    <td>`0.5`</td>
    </tr>
    <tr>
    <td>`scanInterval` parameter</td>
    <td>Set how often in minutes that the cluster autoscaler scans for workload usage that triggers scaling up or down.</td>
    <td>`1m`</td>
    </tr>
    <tr>
    <td>`expander` parameter</td>
    <td>Specify how the cluster autoscaler determines which worker pool to scale if you have multiple worker pools. Possible values are:
    <ul><li>`random`: Selects randomly between `most-pods` and `least-waste`.</li>
    <li>`most-pods`: Selects the worker pool that is able to schedule the most pods when scaling up. Use this method if you are using `nodeSelector` to make sure that pods land on specific worker nodes.</li>
    <li>`least-waste`: Selects the worker pool that has the least unused CPU after scaling up. If two worker pools use the same amount of CPU resources after scaling up, the worker pool with the least unused memory is selected.</li></ul></td>
    <td>random</td>
    </tr>
    <tr>
    <td>`ignoreDaemonSetsUtilization`</td>
    <td>When set to `true`, the cluster autoscaler ignores DaemonSet pods when it calculates resource utilization for scale-down.</td>
    <td>`false`</td>
    </tr>
    <tr>
    <td>`maxBulkSoftTaintCount`</td>
    <td>Set the maximum number of worker nodes that can be tainted or untainted with `PreferNoSchedule` at the same time. To disable this feature, set to `0`.</td>
    <td>`0`</td>
    </tr>
    <tr>
    <td>`maxBulkSoftTaintTime` </td>
    <td>Set the maximum amount of time that worker nodes can be tainted or untainted with `PreferNoSchedule` at the same time.</td>
    <td>`10m`</td>
    </tr>
    <tr>
    <td>`skipNodes.withLocalStorage` parameter</td>
    <td>When set to `true`, worker nodes that have pods that are saving data to local storage are not scaled down.</td>
    <td>`true`</td>
    </tr>
    <tr>
    <td>`skipNodes.withSystemPods` parameter</td>
    <td>When set to `true`, worker nodes that have `kube-system` pods are not scaled down. Do not set the value to `false` because scaling down `kube-system` pods might have unexpected results.</td>
    <td>`true`</td>
    </tr>
    <tr>
    <td>`image.repository` parameter</td>
    <td>Specify the cluster autoscaler Docker image to use.</td>
    <td>`icr.io/iks-charts/ibm-iks-cluster-autoscaler`</td>
    </tr>
    <tr>
    <td>`image.pullPolicy` parameter</td>
    <td>Specify when to pull the Docker image. Possible values are:
    <ul><li>`Always`: Pulls the image every time that the pod is started.</li>
    <li>`IfNotPresent`: Pulls the image only if the image is not already present locally.</li>
    <li>`Never`: Assumes that the image exists locally and never pulls the image.</li></ul></td>
    <td>`IfNotPreset`</td>
    </tr>
    <tr>
      <td>`livenessProbe.periodSeconds`</td>
      <td>Specify the interval in seconds that the `kubelet` performs a liveness probe.</td>
      <td>`10`</td>
    </tr>
    <tr>
      <td>`livenessProbe.failureThreshold`</td>
      <td>Specify the number of times that the `kubelet` retries a liveness probe after the pod starts and the first liveness probe fails. After the failure threshold is reached, the container is restarted and the pod is marked `Unready` for a readiness probe, if applicable.</td>
      <td>`3`</td>
    </tr>
    <tr>
      <td>`livenessProbe.successThreshold`</td>
      <td>Specify the minimum, consecutive number of times that the liveness probe must be successful after a previous failure before the pod is marked `Ready`. If you set a liveness probe, you must set this value to at least `1`.</td>
      <td>`1`</td>
    </tr>
    <tr>
      <td>`livenessProbe.timeoutSeconds`</td>
      <td>Specify the time in seconds after which the liveness probe times out.</td>
      <td>`10`</td>
    </tr>
    <tr>
      <td>`max-inactivity`</td>
      <td>Set the maximum time in minutes that the cluster autoscaler pod runs without any recorded activity before the pod is automatically restarted.</td>
      <td>`10m`</td>
    </tr>
    <tr>
      <td>`max-failing-time`</td>
      <td>Set the maximum time in minutes that the cluster autoscaler pod runs without a successfully completed action before the pod is automatically restarted.</td>
      <td>`15m`</td>
    </tr>
    <tr>
    <td>`customImageVersion`</td>
    <td>To override the default installation version, specify the version of the cluster autoscaler Helm chart that you want to install.</td>
    </tr>
    <tr>
    <td>`maxRetryGap`</td>
    <td>Set the maximum time in seconds to retry after failing to connect to the service API.</td>
    <td>60</td>
    </tr>
    <tr>
    <td>`retryAttempts`</td>Set the maximum number of attempts to retry after failing to connect to the service API.</td>
    <td>32</td>
    </tr>
    <tr>
    <td>`workerpools` parameter</td>
    <td>The worker pools that you want to autoscale, including their minimum and maximum number of worker nodes per zone. These settings are mirrored in the [cluster autoscaler config map](#ca_cm). To set the worker pool, format the option as follows: <code>--set workerpools[0].<pool_name>.max=<number_of_workers>,workerpools[0].<pool_name>.min=<number_of_workers>,workerpools[0].<pool_name>.enabled=(true|false)</code><br><br>
    Understanding the `--set workerpools` options:
      <ul><li>**`workerpools[0]`**: The first worker pool to enable or disable for autoscaling. You must include three parameters for each worker pool for the command to succeed: the maximum number of worker nodes (`max`), the minimum number of worker nodes (`min`), and whether you want to enable (`true`) or disable (`false`) autoscaling for this worker pool. To include multiple worker pools, include a comma-separated list and increase the number in brackets, such as: `workerpools[0].default...,workerpools[1].pool1...,workerpools[2].pool2...`.</li>
      <li>**`<pool_name>`**: The name or ID of the worker pool that you want to enable or disable for autoscaling. To list available worker pools, run `ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>`.</li>
      <li>**`max=<number_of_workers>`**: Specify the maximum number of worker nodes per zone that the cluster autoscaler can scale up to. The value must be equal to or greater than the value that you set for the `min=<number_of_workers>` size.</li>
      <li>**`min=<number_of_workers>`**: Specify the minimum number of worker nodes per zone that the cluster autoscaler can scale down to. The value must be `2` or greater so that your ALB pods can be spread for high availability. If you [disabled](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) all public ALBs in each zone of your standard cluster, you can set the value to `1`.<p class="note">Keep in mind that setting a `min` size does not automatically trigger a scale-up. The `min` size is a threshold so that the cluster autoscaler does not scale below this minimum number of worker nodes per zone. If your cluster does not have this number of worker nodes per zone yet, the cluster autoscaler does not scale up until you have workload resource requests that require more resources.</p></li>
      <li>**`enabled=(true|false)`**: Set the value to `true` to enable the cluster autoscaler to scale your worker pool. Set the value to `false` to stop the cluster autoscaler from scaling the worker pool. Later, if you want to [remove the cluster autoscaler](/docs/openshift?topic=openshift-ca#ca_rm), you must first disable each worker pool in the configmap.</li></ul>
      <p class="note">If you enable a worker pool for autoscaling and then later add a zone to this worker pool, restart the cluster autoscaler pod so that it picks up this change: `oc delete pod -n kube-system <cluster_autoscaler_pod>`.</p>
      <br><br>By default, the `default` worker pool is **not** enabled, with a `max` value of `2` and a `min` value of `1`.</td><td>Disabled</td>
    </tbody>
    </table>
2.  To change any of the cluster autoscaler configuration values, update the Helm chart with the new values. Include the `--recreate-pods` flag so that any existing cluster autoscaler pods are re-created to pick up the custom setting changes. The following example command changes the scan interval to `2m` and enables autoscaling for the `default` worker pool, with a maximum of `5` and minimum of `3` worker nodes per zone.
    ```
    helm upgrade --set scanInterval=2m --set workerpools[0].default.max=5,workerpools[0].default.min=3,workerpools[0].default.enabled=true ibm-iks-cluster-autoscaler iks-charts/ibm-iks-cluster-autoscaler -i --recreate-pods --namespace kube-system
    ```
    {: pre}

    To reset the chart to the default values:
    ```
    helm upgrade --reset-values ibm-iks-cluster-autoscaler iks-charts/ibm-iks-cluster-autoscaler --recreate-pods
    ```
    {: pre}
3. Verify your changes.
    1. Review the Helm chart values again.
      ```
      helm get values ibm-iks-cluster-autoscaler -a
      ```
      {: pre}

    2. Verify that the config map is correct by checking that the `workerPoolsConfig.json` field is updated and that the `workerPoolsConfigStatus` field shows a `SUCCESS` message.
      ```
      oc get cm iks-ca-configmap -n kube-system -o yaml
      ```
      {: pre}

      Example output where the default worker pool is enabled for autoscaling:
      ```
      apiVersion: v1
      data:
        workerPoolsConfig.json: |
          [{"name": "default", "minSize": 3, "maxSize": 5, "enabled": true }]
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

## Limiting apps to run on only certain autoscaled worker pools
{: #ca_limit_pool}

To limit a pod deployment to a specific worker pool that is managed by the cluster autoscaler, use labels and `nodeSelector` or `nodeAffinity`. With `nodeAffinity`, you have more control over how the scheduling behavior works to match pods to worker nodes. For more information about assigning pods to worker nodes, [see the Kubernetes docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/).
{: shortdesc}

**Before you begin**:
*  [Install the `ibm-iks-cluster-autoscaler` plug-in](#ca_helm).
*  [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

**To limit pods to run on certain autoscaled worker pools**:

1.  Create the worker pool with the label that you want to use. For example, your label might be `app: nginx`.
    ```
    ibmcloud oc worker-pool create classic --name <name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_worker_nodes> --label <key>=<value>
    ```
    {: pre}
2.  [Add the worker pool to the cluster autoscaler configuration](#ca_cm).
3.  In your pod spec template, match the `nodeSelector` or `nodeAffinity` to the label that you used in your worker pool.

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
              - key: app
                operator: In
                values:
                - nginx
    ```
    {: codeblock}
4.  Deploy the pod. Because of the matching label, the pod is scheduled onto a worker node that is in the labeled worker pool.
    ```
    oc apply -f pod.yaml
    ```
    {: pre}

<br />


## Scaling up worker nodes before the worker pool has insufficient resources
{: #ca_scaleup}

As described in the [Understanding how the cluster autoscaler works](#ca_about) topic and the [Kubernetes Cluster Autoscaler FAQs](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md){: external}, the cluster autoscaler scales up your worker pools in response to your requested resources of the workload against the available recourses of the worker pool. However, you might want the cluster autoscaler to scale up worker nodes before the worker pool runs out of resources. In this case, your workload does not need to wait as long for worker nodes to be provisioned because the worker pool is already scaled up to meet the resource requests.
{: shortdesc}

The cluster autoscaler does not support early scaling (overprovisioning) of worker pools. However, you can configure other Kubernetes resources to work with the cluster autoscaler to achieve early scaling.

<dl>
  <dt><strong>Pause pods</strong></dt>
  <dd>You can create a deployment that deploys [pause containers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://stackoverflow.com/questions/48651269/what-are-the-pause-containers) in pods with specific resource requests, and assign the deployment a low pod priority. When these resources are needed by higher priority workloads, the pause pod is preempted and becomes a pending pod. This event triggers the cluster autoscaler to scale up.<br><br>For more information about setting up a pause pod deployment, see the [Kubernetes FAQ ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-can-i-configure-overprovisioning-with-cluster-autoscaler). You can use [this example overprovisioning configuration file ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Cloud/kube-samples/blob/master/ibm-ks-cluster-autoscaler/overprovisioning-autoscaler.yaml) to create the priority class, service account, and deployments.<p class="note">If you use this method, make sure that you understand how [pod priority](/docs/openshift?topic=openshift-pod_priority) works and how to set pod priority for your deployments. For example, if the pause pod does not have enough resources for a higher priority pod, the pod is not preempted. The higher priority workload remains in pending, so the cluster autoscaler is triggered to scale up. However, in this case, the scale-up action is not early because the workload that you want to run cannot be scheduled because of insufficient resources.</p></dd>

  <dt><strong>Horizontal pod autoscaling (HPA)</strong></dt>
  <dd>Because horizontal pod autoscaling is based on the average CPU usage of the pods, the CPU usage limit that you set is reached before the worker pool runs out of resources. More pods are requested, which then triggers the cluster autoscaler to scale up the worker pool.<br><br>For more information about setting up HPA, see the [Kubernetes docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/).</dd>
</dl>

<br />


## Upgrading a cluster autoscaler release
{: #ca_helm_up}

You can upgrade the existing cluster autoscaler release to the latest version of the Helm chart. To check your current release version, run `helm list -n <namespace> | grep cluster-autoscaler`. Compare your version to the latest available release by reviewing the **Chart Version** in the [{{site.data.keyword.cloud_notm}} Helm Catalog](https://cloud.ibm.com/kubernetes/helm/iks-charts/ibm-iks-cluster-autoscaler){: external}.
{: shortdesc}

### Prerequisites
{: #ca_helm_up_prereqs}

Before you begin to upgrade your cluster autoscaler release, complete the following steps.
{: shortdesc}

1. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
3. To review the changelog of chart versions, [download the source code `tar` file](https://cloud.ibm.com/kubernetes/helm/iks-charts/ibm-iks-cluster-autoscaler) and open the `RELEASENOTES.MD` file.

### Upgrading the cluster autoscaler release version
{: #ca_helm_up_general}

To upgrade your cluster autoscaler release, you can update the Helm chart repo and re-create the cluster autoscaler pods. Use the same version of Helm that you used to install the initial Helm chart and release. For example, if you installed the release with Helm version 2, these upgrade steps might not work if you now have Helm version 3. Instead, see [Upgrading a release from Helm version 2 to version 3](#ca_helm_up_2to3).

Before you begin, see the [Prerequisites](#ca_helm_up_prereqs).

1.  Update the Helm repo to retrieve the latest version of all Helm charts in this repo.
    ```
    helm repo update
    ```
    {: pre}

2.  Optional: Download the latest Helm chart to your local machine. Then, extract the package and review the `release.md` file to find the latest release information.
    ```
    helm pull iks-charts/ibm-iks-cluster-autoscaler
    ```
    {: pre}

3.  Find the name of the cluster autoscaler release that you installed in your cluster.
    ```
    helm list -n <namespace> | grep cluster-autoscaler
    ```
    {: pre}

    Example output:
    ```
    myhelmchart 	1       	Mon Jan  7 14:47:44 2019	DEPLOYED	ibm-ks-cluster-autoscaler-1.0.0  	kube-system
    ```
    {: screen}

4.  Upgrade the cluster autoscaler release to the latest version.
    ```
    helm upgrade --force --recreate-pods <helm_chart_name>  iks-charts/ibm-iks-cluster-autoscaler
    ```
    {: pre}

5.  Verify that the [cluster autoscaler configmap](#ca_cm) `workerPoolsConfig.json` section is set to `"enabled": true` for the worker pools that you want to scale.
    ```
    oc describe cm iks-ca-configmap -n kube-system
    ```
    {: pre}

    Example output:
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
     {"name": "docs","minSize": 1,"maxSize": 3,"enabled":true}
    ]

    Events:  <none>
    ```
    {: screen}

### Upgrading a release from Helm v2 to v3
{: #ca_helm_up_2to3}

When you upgrade a release of the cluster autoscaler, you must use the same version of Helm that you used to install the initial Helm chart and release. The cluster autoscaler Helm chart supports both Helm version 2.15 and 3.0. If you installed the Helm chart and release with Helm v2 and then try to upgrade from a Helm v3 client, you might experience errors. Instead, uninstall the release and reinstall the latest release with Helm v3. For more information, see [Migrating from Helm v2 to v3](/docs/openshift?topic=openshift-helm#migrate_v3).
{: shortdesc}

Additionally, if you have release version 1.0.2 or earlier, you must uninstall that release before you install the latest release.

Before you begin, see the [Prerequisites](#ca_helm_up_prereqs).

1.  [Migrate to](/docs/openshift?topic=openshift-helm#migrate_v3) or [install](/docs/openshift?topic=openshift-helm#install_v3) Helm version 3.
2.  Get your cluster autoscaler configmap.
    ```
    oc get cm iks-ca-configmap -n kube-system -o yaml > iks-ca-configmap.yaml
    ```
    {: pre}
3.  Remove all worker pools from the configmap by setting the `"enabled"` value to `false`.
    ```
    oc edit cm iks-ca-configmap -n kube-system
    ```
    {: pre}
4.  If you applied custom settings to the Helm chart, note your custom settings.
    ```
    helm get values ibm-ks-cluster-autoscaler -a
    ```
    {: pre}
5.  Uninstall your current Helm chart.
    ```
    helm uninstall ibm-ks-cluster-autoscaler -n <namespace>
    ```
    {: pre}
6.  Update the Helm chart repo to get the latest cluster autoscaler Helm chart version.
    ```
    helm repo update
    ```
    {: pre}
7.  Install the latest cluster autoscaler Helm chart. Apply any custom settings that you previously used with the `--set` flag, such as `scanInterval=2m`.
    ```
    helm install ibm-iks-cluster-autoscaler iks-charts/ibm-iks-cluster-autoscaler --namespace kube-system [--set <custom_settings>]
    ```
    {: pre}
8.  Apply the cluster autoscaler configmap that you previously retrieved to enable autoscaling for your worker pools.
    ```
    oc apply -f iks-ca-configmap.yaml
    ```
    {: pre}
9.  Get your cluster autoscaler pod.
    ```
    oc get pods -n kube-system
    ```
    {: pre}
10.  Review the **`Events`** section of the cluster autoscaler pod and look for a **`ConfigUpdated`** event to verify that the configmap is successfully updated. The event message for your configmap is in the following format: `minSize:maxSize:PoolName:<SUCCESS|FAILED>:error message`.
    ```
    oc describe pod -n kube-system <cluster_autoscaler_pod>
    ```
    {: pre}

    Example output:
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

<br />


## Removing the cluster autoscaler
{: #ca_rm}

If you do not want to automatically scale your worker pools, you can uninstall the cluster autoscaler Helm chart. After the removal, you must [resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) or [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) your worker pools manually.
{: shortdesc}

Before you begin: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1.  In the [cluster autoscaler configmap](#ca_cm), remove the worker pool by setting the `"enabled"` value to `false`.
    ```
    oc edit cm iks-ca-configmap -n kube-system
    ```
    {: pre}
    Example output:
    ```
    apiVersion: v1
    data:
      workerPoolsConfig.json: |
        [
         {"name": "default","minSize": 1,"maxSize": 2,"enabled":false},
         {"name":"mypool","minSize":1,"maxSize":5,"enabled":false}
        ]
    kind: ConfigMap
    ...
    ```
    {: screen}

    If you already deleted the Helm chart and see a message such as `iks-ca-configmap not found`, [redeploy the cluster autoscaler Helm chart](#ca_helm) to your cluster and try to remove it again.
    {: tip}

2.  List your existing Helm charts and note the name of the cluster autoscaler.
    ```
    helm list --all-namespaces
    ```
    {: pre}
3.  Remove the existing Helm chart from your cluster.
    ```
    helm uninstall ibm-ks-cluster-autoscaler -n <namespace>
    ```
    {: pre}



