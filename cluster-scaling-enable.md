---

copyright: 
  years: 2014, 2024
lastupdated: "2024-01-17"


keywords: openshift, kubernetes, node scaling, ca, autoscaler

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Setting up autoscaling for your worker pools
{: #cluster-scaling-install-addon-enable}

Update the cluster autoscaler configmap to enable automatically scaling worker nodes in your worker pools based on the minimum and maximum values that you set.
{: shortdesc}

After you edit the configmap to enable a worker pool, the cluster autoscaler scales your cluster in response to your workload requests. As such, you can't [resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) or [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) your worker pools. Scanning and scaling up and down happens at regular intervals over time, and depending on the number of worker nodes might take a longer period of time to complete, such as 30 minutes. Later, if you want to [remove the cluster autoscaler](/docs/openshift?topic=openshift-cluster-scaling-install-addon&interface=ui#autoscaler-remove-console), you must first disable each worker pool in the ConfigMap.
{: note}

**Before you begin**:
*  Install the [cluster autoscaler add-on](/docs/openshift?topic=openshift-cluster-scaling-install-addon).
*  [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).


1. Edit the cluster autoscaler configmap YAML file.
    ```sh
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

2. Edit the ConfigMap with the parameters to define how the cluster autoscaler scales your cluster worker pool. **Note:** Unless you [disabled](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) all public application load balancers (ALBs) in each zone of your standard cluster, you must change the `minSize` to `2` per zone so that the ALB pods can be spread for high availability.

    - `"name": "default"`: Replace `"default"` with the name or ID of the worker pool that you want to scale. To list worker pools, run `ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>`. To manage more than one worker pool, copy the JSON line to a comma-separated line, such as follows.
    
        ```sh
        [
        {"name": "default","minSize": 1,"maxSize": 2,"enabled":false},
        {"name": "Pool2","minSize": 2,"maxSize": 5,"enabled":true}
        ]
        ```
        {: codeblock}
        
        The cluster autoscaler can scale only worker pools that have the `ibm-cloud.kubernetes.io/worker-pool-id` label. To check whether your worker pool has the required label, run `ibmcloud oc worker-pool get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID> | grep Labels`. If your worker pool does not have the required label, add a new worker pool and use this worker pool with the cluster autoscaler.
        {: note}

    - `"minSize": 1`: Specify the minimum number of worker nodes per zone that the cluster autoscaler can scale down the worker pool to. The value must be `2` or greater so that your ALB pods can be spread for high availability. If you [disabled](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) all public ALBs in each zone of your standard cluster, you can set the value to `1`.

        Setting a `minSize` does not automatically trigger a scale-up. The `minSize` is a threshold so that the cluster autoscaler does not scale to fewer than a certain number of worker nodes per zone. If your cluster does not yet have that number per zone, the cluster autoscaler does not scale up until you have workload resource requests that require more resources. For example, if you have a worker pool with one worker node per three zones (three total worker nodes) and set the `minSize` to `4` per zone, the cluster autoscaler does not immediately provision an additional three worker nodes per zone (12 worker nodes total). Instead, the scale-up is triggered by resource requests. If you create a workload that requests the resources of 15 worker nodes, the cluster autoscaler scales up the worker pool to meet this request. Now, the `minSize` means that the cluster autoscaler does not scale down to fewer than four worker nodes per zone even if you remove the workload that requests the amount. For more information, see the [Kubernetes docs](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#when-does-cluster-autoscaler-change-the-size-of-a-cluster){: external}.
        {: note}

    - `"maxSize": 2`: Specify the maximum number of worker nodes per zone that the cluster autoscaler can scale up the worker pool to. The value must be equal to or greater than the value that you set for the `minSize`.
    - `"enabled": false`: Set the value to `true` for the cluster autoscaler to manage scaling for the worker pool. Set the value to `false` to stop the cluster autoscaler from scaling the worker pool. Later, if you want to [remove the cluster autoscaler](/docs/openshift?topic=openshift-cluster-scaling-install-addon&interface=ui#autoscaler-remove-console), you must first disable each worker pool in the ConfigMap.

3. Save the configuration file.

4. Get your cluster autoscaler pod.

    ```sh
    oc get pods -n kube-system
    ```
    {: pre}

5. Review the **`Events`** section of the cluster autoscaler pod for a **`ConfigUpdated`** event to verify that the ConfigMap is successfully updated. The event message for your ConfigMap is in the following format: `minSize:maxSize:PoolName:<SUCCESS|FAILED>:error message`.

    ```sh
    oc describe pod -n kube-system <cluster_autoscaler_pod>
    ```
    {: pre}

    Example output

    ```sh
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


*  [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
*  [Enable the add-on](/docs/openshift?topic=openshift-cluster-scaling-install-addon).

    When you modify a ConfigMap parameter other than the worker pool `minSize`, `maxSize`, or if you enable or disable a worker pool, the cluster autoscaler pods are restarted.
    {: note}

1. Review the [cluster autoscaler ConfigMap](#ca-configmap) parameters.

1. Download the cluster autoscaler add-on ConfigMap and review the parameters.

    ```sh
    oc get cm iks-ca-configmap -n kube-system -o yaml > configmap.yaml
    ```
    {: pre}

1. Open the `configmap.yaml` file and update the settings that you want to change.

1. Reapply the cluster autoscaler add-on configmap.

    ```sh
    oc apply -f configmap.yaml
    ```
    {: pre}

1. Verify that the pods are restarted successfully.

    ```sh
    oc get pods -n kube-system | grep autoscaler
    ```
    {: pre}
    
    
## Cluster autoscaler configmap reference
{: #ca-configmap}


| Parameter | Description | Default |
| --- | --- | --- |
| `expander` | How the cluster autoscaler determines which worker pool to scale if you have multiple worker pools.  \n - `random`: Selects randomly between `most-pods` and `least-waste`.  \n - `most-pods`: Selects the worker pool that is able to schedule the most pods when scaling up. Use this method if you are using `nodeSelector` to make sure that pods land on specific worker nodes.  \n - `least-waste`: Selects the worker pool that has the least unused CPU after scaling up. If two worker pools use the same amount of CPU resources after scaling up, the worker pool with the least unused memory is selected. | `random` |
| `prometheusScrape` | Set to `true` to send Prometheus metrics. To stop sending metrics, set to `false`. | `true` |
| `ignoreDaemonSetsUtilization` | Ignores autoscaler DaemonSet pods when calculating resource utilization for scale-down. | `false` |
| `imagePullPolicy` | When to pull the Docker image.  \n - `Always`: Pulls the image every time that the pod is started.  \n - `IfNotPresent`: Pulls the image only if the image isn't already present locally.  \n - `Never`: Assumes that the image exists locally and never pulls the image. | `Always` |
| `livenessProbeFailureThreshold` | The number of times that the `kubelet` retries a liveness probe after the pod starts and the first liveness probe fails. After the failure threshold is reached, the container is restarted and the pod is marked `Unready` for a readiness probe, if applicable. | `3` |
| `livenessProbePeriodSeconds` | The interval in seconds that the `kubelet` performs a liveness probe. | `600` |
| `livenessProbeTimeoutSeconds` | The time in seconds after which the liveness probe times out. | `10` |
| `maxBulkSoftTaintCount` | The maximum number of worker nodes that can be tainted or untainted with `PreferNoSchedule` at the same time. To disable this feature, set to `0`. | `0` |
| `maxBulkSoftTaintTime` | The maximum amount of time that worker nodes can be tainted or untainted with `PreferNoSchedule` at the same time. | `10m` |
| `maxFailingTime` | The maximum time in minutes that the cluster autoscaler pod runs without a completed action before the pod is automatically restarted. | `15m` |
| `maxInactivity` | The maximum time in minutes that the cluster autoscaler pod runs without any recorded activity before the pod is automatically restarted. | `10m` |
| `maxNodeProvisionTime` | The maximum amount of time in minutes that a worker node can take to begin provisioning before the cluster autoscaler cancels the scale-up request. | `120m` |
| `maxNodeGroupBinpackingDuration` |  Maximum time in seconds spent in bin packing simulation for each worker-pool. | `10s` |
| `maxNodesPerScaleUp` | Maximum number of nodes that can be added in a single scale up. This is intended strictly for optimizing autoscaler algorithm latency and should not be used as a rate limit for scale-up. | `1000` |
| `maxRetryGap` | The maximum time in seconds to retry after failing to connect to the service API. Use this parameter and the `retryAttempts` parameter to adjust the retry window for the cluster autoscaler. | `60` |
| `parallelDrain` | Set to `true` to allow parallel draining of nodes. | `false` |
| `maxScaleDownParallelism` | The maximum number of nodes, both empty and still needing to be drained, that can be deleted in parallel. | `10` |
| `maxDrainParallelism` | Maximum number of nodes that still need to be drained that can be drained and deleted in parallel. | `1` |
| `nodeDeletionBatcherInterval` | How long in minutes that the autoscaler can gather nodes to delete them in batch. | `0m` |
| `nodeDeleteDelayAfterTaint` | How long in seconds to wait before deleting a node after tainting it. | `5s` |
| `enforceNodeGroupMinSize` | Set this value to `true` to scale up the worker pool to the configured min size if needed. | `false` |
| `resourcesLimitsCPU` | The maximum amount of worker node CPU that the `ibm-iks-cluster-autoscaler` pod can consume. | `600m` |
| `resourcesLimitsMemory` | The maximum amount of worker node memory that the `ibm-iks-cluster-autoscaler` pod can consume. | `600Mi` |
| `coresTotal` | The minimum and maximum number of cores in the cluster. Cluster autoscaler does not scale the cluster beyond these numbers. | `0:320000` |
| `memoryTotal` | Minimum and maximum amount of memory in gigabytes for the cluster. Cluster autoscaler does not scale the cluster beyond these numbers. | `0:6400000` |
| `resourcesRequestsCPU` | The minimum amount of worker node CPU that the `ibm-iks-cluster-autoscaler` pod starts with. | `200m` |
| `resourcesRequestsMemory` | The minimum amount of worker node memory that the `ibm-iks-cluster-autoscaler` pod starts with. | `200Mi` |
| `retryAttempts` | The maximum number of attempts to retry after failing to connect to the service API. Use this parameter and the `maxRetryGap` parameter to adjust the retry window for the cluster autoscaler. | `64` |
| `logLevel` | The log level for the autoscaler. Logging levels are `info`, `debug`, `warning`, `error` | `info` |
| `scaleDownDelayAfterAdd` | The amount of time after scale up that scale down evaluation resumes. The default value for `scaleDownDelayAfterAdd` is 10 minutes. | `10m` |
| `scaleDownDelayAfterDelete` | The amount of time after node deletion that scale down evaluation resumes. The default value for `scaleDownDelayAfterDelete` is the same as the `scan-interval` which is `1m` | `1m` |
| `scaleDownDelayAfterFailure` | The amount of time in minutes that the autoscaler must wait after a failure. | `3m` |
| `kubeClientBurst` | Allowed burst for the Kubernetes client. | `300` |
| `kubeClientQPS` | The QPS value for Kubernetes client. How many queries are accepted once the burst has been exhausted. | `5.0` |
| `maxEmptyBulkDelete` | The maximum number of empty nodes that can be deleted by the autoscaler at the same time. | `10` |
| `maxGracefulTerminationSec` | The maximum number of seconds the autoscaler waits for pod to end when it scales down a node. | `600` |
| `maxTotalUnreadyPercentage` | The maximum percentage of unready nodes in the cluster. After this value is exceeded, the autoscaler stops operations. | `45` |
| `okTotalUnreadyCount` | Number of allowed unready nodes, irrespective of the `maxTotalUnreadyPercentage` value. | `3` |
| `unremovableNodeRecheckTimeout` | The timeout in minutes before the autoscaler rechecks a node that couldn't be removed in earlier attempt. | `5m` |
| `scaleDownUnneededTime` | The amount of time in minutes that a worker node must be unnecessary before it can be scaled down. | `10m` |
| `scaleDownUtilizationThreshold` | The worker node utilization threshold. If the worker node utilization is less than the threshold, the worker node is considered to be scaled down. Worker node utilization is calculated as the sum of the CPU and memory resources that are requested by all pods that run on the worker node, divided by the worker node resource capacity. | `0.5` |
| `scaleDownUnreadyTime` | The amount of time in minutes that autoscaler must wait before an unready node is considered for scale down. | `20m` |
| `scaleDownNonEmptyCandidatesCount` | The maximum number of non-empty nodes considered in one iteration as candidates for scale down with drain. | `30` |
| `scaleDownCandidatesPoolRatio` | The ratio of nodes that are considered as additional non-empty candidates for scale down when some candidates from previous iteration are no longer valid. | `0.1` |
| `scaleDownCandidatesPoolMinCount` | The minimum number of nodes that are considered as additional non-empty candidates for scale down when some candidates from previous iterations are no longer valid. | `50` |
| `scaleDownEnabled` | When set to `false`, the autoscaler does not perform scale down. | `true` |
| `scaleDownUnreadyEnabled` | When set to `true` unready nodes are scheduled for scale down. | `true` |
| `scanInterval` | Set how often in minutes that the cluster autoscaler scans for workload usage that triggers scaling up or down. | `1m` |
| `skipNodesWithLocalStorage` | When set to `true`, worker nodes that have pods that are saving data to local storage are not scaled down. The default value is `true` |
| `skipNodesWithSystemPods` | When set to `true`, worker nodes that have `kube-system` pods are not scaled down. Do not set the value to `false` because scaling down `kube-system` pods might have unexpected results. | `true` |
| `expendablePodsPriorityCutoff` | Pods with priority under the cutoff are expendable. They can be removed without consideration during scale down and they don't cause scale up. Pods that `PodPriority` set to null are not expendable. | `-10` |
| `minReplicaCount` | The minimum number of replicas that a replicaSet or replication controller must allow to be deleted during scale down. | `0` |
| maxPodEvictionTime | Maximum time the autoscaler tries to evict a pod before stopping. | `2m` | 
| `newPodScaleUpDelay` | Pods newer than this value in seconds are not considered for scale-up. Can be increased for individual pods through the `cluster-autoscaler.kubernetes.io/pod-scale-up-delay` annotation. | `0s` |
| `balancingIgnoreLabel` | The node label key to ignore during zone balancing. Apart from the fixed node labels, the autoscaler can ignore an additional 5 node labels during zone balancing. For example, `balancingIgnoreLabel1:label1`, `balancingIgnoreLabel2: custom-label2`. |
| `workerPoolsConfig.json` | The worker pools that you want to autoscale, including their minimum and maximum number of worker nodes per zone.  \n - `{"name": "<pool_name>","minSize": 1,"maxSize": 2,"enabled":false}`.  \n - `<pool_name>`: The name or ID of the worker pool that you want to enable or disable for autoscaling. To list available worker pools, run `ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>`  \n - `maxSize: <number_of_workers>`: The maximum number of worker nodes per zone that the cluster autoscaler can scale up to. The value must be equal to or greater than the value that you set for the `minSize: <number_of_workers>` size.  \n - `min=<number_of_workers>`: The minimum number of worker nodes per zone that the cluster autoscaler can scale down to. The value must be `2` or greater so that your ALB pods can be spread for high availability. If you [disabled](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) all public ALBs in each zone of your standard cluster, you can set the value to `1`. Keep in mind that setting a `min` size does not automatically trigger a scale-up. The `min` size is a threshold so that the cluster autoscaler does not scale to fewer than this minimum number of worker nodes per zone. If your cluster does not have this number of worker nodes per zone yet, the cluster autoscaler does not scale up until you have workload resource requests that require more resources.  \n - `enabled=`: When `true`, the cluster autoscaler can scale your worker pool. When `false`, the cluster autoscaler won't scale the worker pool. Later, if you want to remove the cluster autoscaler, you must first disable each worker pool in the ConfigMap. If you enable a worker pool for autoscaling and then later add a zone to this worker pool, restart the cluster autoscaler pod so that it picks up this change: `oc delete pod -n kube-system <cluster_autoscaler_pod>`. | By default, the `default` worker pool is **not** enabled, with a `max` value of `2` and a `min` value of `1` |
{: caption="Autoscaler add-on parameter reference" caption-side="bottom"}  
    
