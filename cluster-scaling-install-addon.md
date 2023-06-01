---

copyright: 
  years: 2014, 2023
lastupdated: "2023-06-01"

keywords: openshift, node scaling, ca, autoscaler

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}




# Enabling the cluster autoscaler add-on in your cluster
{: #cluster-scaling-install-addon}

You can enable the add-on from the console or the command the line.

* To enable from the console, complete the following steps.
    
    1. From the [{{site.data.keyword.openshiftlong_notm}} cluster dashboard](https://cloud.ibm.com/kubernetes/clusters), select the cluster where you want to enable autoscaling.
    1. On the **Overview** page, click **Add-ons**.
    1. On the **Add-ons** page, locate the Cluster Autoscaler add-on and click **Install**

* To enable from the the CLI, complete the following steps.
    
    1. Enable the `cluster-autoscaler` add-on.
        ```sh
        ibmcloud oc cluster addon enable cluster-autoscaler --cluster <cluster_name>
        ```
        {: pre}

        Example output
        
        ```sh
        Enabling add-on `cluster-autoscaler` for cluster <cluster_name>...
        The add-on might take several minutes to deploy and become ready for use.
        OK
        ```
        {: screen}

    1. Verify that the add-on is installed and `Ready`.
        ```sh
        ibmcloud oc cluster addon ls --cluster <cluster_name>
        ```
        {: pre}

        Example output

        ```sh
        NAME                 Version   Health State   Health Status   
        cluster-autoscaler   1.0.1     normal         Addon Ready
        ```
        {: screen}

By default, no worker pools are enabled for autoscaling. To enable autoscaling on your worker pools, [update the cluster autoscaler ConfigMap to enable scaling for your worker pools](/docs/openshift?topic=openshift-cluster-scaling-enable).




## Updating the cluster autoscaler add-on
{: #cluster-scaling-update-addon}

This topic applies only to the cluster autoscaler add-on.
{: important}

If you upgrade your cluster to a version that isn't supported by the cluster autoscaler add-on, your apps might experience downtime and your cluster might not scale.
{: important}

The cluster autoscaler has two types of updates.

Patch updates
:   Patch updates are delivered automatically by IBM and don't contain any feature updates or changes in the supported add-on and cluster versions.

Release updates
:   Release updates contain new features for the cluster autoscaler or changes in the supported add-on or cluster versions. You must manually apply release updates to your cluster autoscaler add-on.


1. Check the version of the cluster autoscaler add-on that is deployed in your cluster. If an update is available, review the [release notes](/docs/openshift?topic=openshift-ca_changelog) for the latest add-on version.
    ```sh
    ibmcloud oc cluster addon ls --cluster <cluster_name>
    ```
    {: pre}

2. Disable the cluster autoscaler add-on. You might see a warning that resources or data might be deleted. For the cluster autoscaler update, any autoscaling operations that are in process when you disable fail. When you re-enable the add-on, the autoscaling operation is restarted for you. Existing cluster autoscaler resources like the `iks-ca-configmap` are retained even after you disable the add-on. Your worker nodes are not deleted because of disabling the add-on.

    ```sh
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

4. Verify the add-on is successfully updated and `Ready`.

    ```sh
    ibmcloud oc cluster addon ls --cluster <cluster_name>
    ```
    {: pre}
    
    
## Removing the cluster autoscaler add-on
{: #ca-addon-rm}

Before disabling the add-on, [edit the autoscaler ConfigMap](/docs/openshift?topic=openshift-cluster-scaling-enable) to stop scaling your working pools.
{: important}

You can enable the add-on from the console or the command the line.

* To disable from the console, complete the following steps.
    
    1. From the [{{site.data.keyword.openshiftlong_notm}} cluster dashboard](https://cloud.ibm.com/kubernetes/clusters), select the cluster where you want to enable autoscaling.
    1. On the **Overview** page, click **Add-ons**.
    1. On the **Add-ons** page, locate the Cluster Autoscaler add-on and click **Uninstall**

* To disable from the the CLI, complete the following steps.
    
    1. Disable the `cluster-autoscaler` add-on.
    
        ```sh
        ibmcloud oc cluster addon disable cluster-autoscaler --cluster <cluster_name>
        ```
        {: pre}

    1. Verify that the add-on was removed.
    
        ```sh
        ibmcloud oc cluster addon ls --cluster <cluster_name>
        ```
        {: pre}
    
    
## Cluster autoscaler add-on parameter reference
{: #ca_addon_ref}

This table refers to the cluster autoscaler add-on parameters. For Helm chart values, see [Cluster autoscaler Helm chart parameter reference](/docs/openshift?topic=openshift-cluster-scaling-helm#ca_helm_ref)
{: note}


`expander`
:   Specify how the cluster autoscaler determines which worker pool to scale if you have multiple worker pools. The default value is `random`.
:  `random`: Selects randomly between `most-pods` and `least-waste`.
:   `most-pods`: Selects the worker pool that is able to schedule the most pods when scaling up. Use this method if you are using `nodeSelector` to make sure that pods land on specific worker nodes.
:   `least-waste`: Selects the worker pool that has the least unused CPU after scaling up. If two worker pools use the same amount of CPU resources after scaling up, the worker pool with the least unused memory is selected.

:   

`ignoreDaemonSetsUtilization`
:   When set to `true`, the cluster autoscaler ignores DaemonSet pods when it calculates resource utilization for scale-down. The default value is `false`.

`imagePullPolicy`
:   Specify when to pull the Docker image. The default value is `Always`.
:  `Always`: Pulls the image every time that the pod is started.
:   `IfNotPresent`: Pulls the image only if the image isn't already present locally.
:   `Never`: Assumes that the image exists locally and never pulls the image. 

`livenessProbeFailureThreshold`
:   Specify the number of times that the `kubelet` retries a liveness probe after the pod starts and the first liveness probe fails. After the failure threshold is reached, the container is restarted and the pod is marked `Unready` for a readiness probe, if applicable. The default value is `3`.

`livenessProbePeriodSeconds`
:   Specify the interval in seconds that the `kubelet` performs a liveness probe. The default value is `600`.

`livenessProbeTimeoutSeconds`
:   Specify the time in seconds after which the liveness probe times out. The default value is `10`.

`maxBulkSoftTaintCount`
:   Set the maximum number of worker nodes that can be tainted or untainted with `PreferNoSchedule` at the same time. To disable this feature, set to `0`. The default value is `0`.

`maxBulkSoftTaintTime`
:   Set the maximum amount of time that worker nodes can be tainted or untainted with `PreferNoSchedule` at the same time. The default value is `10m`.

`maxFailingTime`
:   Set the maximum time in minutes that the cluster autoscaler pod runs without a completed action before the pod is automatically restarted. The default is `15m`.

`maxInactivity`
:   Set the maximum time in minutes that the cluster autoscaler pod runs without any recorded activity before the pod is automatically restarted. The default value is `10m`.

`maxNodeProvisionTime`
:   Set the maximum amount of time in minutes that a worker node can take to begin provisioning before the cluster autoscaler cancels the scale-up request. The default value is `120m`.

`maxNodeGroupBinpackingDuration`
:    Maximum time in seconds spent in bin packing simulation for each worker-pool. The default value is `10s`.

`maxNodesPerScaleUp`
:   Maximum number of nodes that can be added in a single scale up. This is intended strictly for optimizing autoscaler algorithm latency and should not be used as a rate limit for scale-up. The default value is `1000`.

`maxRetryGap`
:   Set the maximum time in seconds to retry after failing to connect to the service API. Use this parameter and the `retryAttempts` parameter to adjust the retry window for the cluster autoscaler. The default value is `60`.

`parallelDrain`
:   Set to `true` to allow parallel draining of nodes. The default value is `false`.

`maxScaleDownParallelism`
:   Maximum number of nodes, both empty and still needing to be drained, that can be deleted in parallel. The default value is `10`.


`maxDrainParallelism`
:   Maximum number of nodes that still need to be drained that can be drained and deleted in parallel. The default value is `1`.

`nodeDeletionBatcherInterval`
:   How long in minutes that the autoscaler can gather nodes to delete them in batch. The default value is `0m`.

`nodeDeleteDelayAfterTaint`
:   How long in seconds to wait before deleting a node after tainting it. The default value is `5s`.

`enforceNodeGroupMinSize`
:   Set this value to `true` to scale up the worker pool to the configured min size if needed. The default value is `false`.

`resourcesLimitsCPU`
:  Set the maximum amount of worker node CPU that the `ibm-iks-cluster-autoscaler` pod can consume. The default value is `600m`.

`resourcesLimitsMemory`
:   Set the maximum amount of worker node memory that the `ibm-iks-cluster-autoscaler` pod can consume. The default value is `600Mi`.

`coresTotal`
:   Minimum and maximum number of cores in the cluster. Cluster autoscaler does not scale the cluster beyond these numbers. The default value is `0:320000`.

`memoryTotal`
:   Minimum and maximum amount of memory in gigabytes for the cluster. Cluster autoscaler does not scale the cluster beyond these numbers. The default value is `0:6400000`.

`resourcesRequestsCPU`
:   Set the minimum amount of worker node CPU that the `ibm-iks-cluster-autoscaler` pod starts with. The default value is `200m`.

`resourcesRequestsMemory`
:   Set the minimum amount of worker node memory that the `ibm-iks-cluster-autoscaler` pod starts with. The default value is `200Mi`.

`retryAttempts`
:   Set the maximum number of attempts to retry after failing to connect to the service API. Use this parameter and the `maxRetryGap` parameter to adjust the retry window for the cluster autoscaler. The default value is 64.

`logLevel`
:   Set the log level for the autoscaler. Logging levels are `info`, `debug`, `warning`, `error`. The default value is `info`.

`scaleDownDelayAfterAdd`
:   Set the amount of time after scale up that scale down evaluation resumes. The default value for `scaleDownDelayAfterAdd` is 10 minutes. The default value is `10m`.

`scaleDownDelayAfterDelete`
:   Set the amount of time after node deletion that scale down evaluation resumes. The default value for `scaleDownDelayAfterDelete` is the same as the `scan-interval` which is `1m`. The default value is `1m`.

`scaleDownDelayAfterFailure`
:   Set the amount of time in minutes that the autoscaler must wait after a failure. The default value is `3m`.

`maxEmptyBulkDelete`
:   Maximum number of empty nodes that can be deleted by the autoscaler at the same time. The default value is `10`.

`maxGracefulTerminationSec`
:   Maximum number of seconds the autoscaler waits for pod to end when it scales down a node. The default value is `600`.

`maxTotalUnreadyPercentage`
:   Maximum percentage of unready nodes in the cluster. After this value is exceeded, the autoscaler stops operations. The default value is `45`.

`okTotalUnreadyCount`
:   Number of allowed unready nodes, irrespective of the `maxTotalUnreadyPercentage` value. The default value is `3`.

`unremovableNodeRecheckTimeout`
:   The timeout in minutes before the autoscaler rechecks a node that couldn't be removed in earlier attempt. The default value is `5m`.

`scaleDownUnneededTime`
:   Set the amount of time in minutes that a worker node must be unnecessary before it can be scaled down. The default value is `10m`.

`scaleDownUtilizationThreshold`
:   Set the worker node utilization threshold. If the worker node utilization is less than the threshold, the worker node is considered to be scaled down. Worker node utilization is calculated as the sum of the CPU and memory resources that are requested by all pods that run on the worker node, divided by the worker node resource capacity. The default value is `0.5`.

`scaleDownUnreadyTime`
:   Set the amount of time in minutes that autoscaler must wait before an unready node is considered for scale down. The default value is `20m`.

`scaleDownNonEmptyCandidatesCount`
:   Set the maximum number of non-empty nodes considered in one iteration as candidates for scale down with drain. The default value is `30`.

`scaleDownCandidatesPoolRatio`
:   A ratio of nodes that are considered as additional non-empty candidates for scale down when some candidates from previous iteration are no longer valid. The default value is `0.1`.

`scaleDownCandidatesPoolMinCount`
:   Minimum number of nodes that are considered as additional non-empty candidates for scale down when some candidates from previous iterations are no longer valid. The default value is `50`.

`scaleDownEnabled`
:   When set to `false`, the autoscaler does not perform scale down. The default value is `true`.

`scanInterval`
:  Set how often in minutes that the cluster autoscaler scans for workload usage that triggers scaling up or down. The default value is `1m`.

`skipNodesWithLocalStorage`
:   When set to `true`, worker nodes that have pods that are saving data to local storage are not scaled down. The default value is`true`.

`skipNodesWithSystemPods`
:  When set to `true`, worker nodes that have `kube-system` pods are not scaled down. Do not set the value to `false` because scaling down `kube-system` pods might have unexpected results. The default value is `true`.

`expendablePodsPriorityCutoff`
:   Pods with priority below cutoff are expendable. They can be removed without consideration during scale down and they don't cause scale up. Pods with null priority (PodPriority disabled) are non-expendable. The default value is `-10`.

`minReplicaCount`
:   Minimum number of replicas that a replicaSet or replication controller must allow to be deleted during scale down. The default value is `0`.

`newPodScaleUpDelay`
:   Pods newer than this value in seconds are not considered for scale-up. Can be increased for individual pods through the `cluster-autoscaler.kubernetes.io/pod-scale-up-delay` annotation. The default value is `0s`.

`balancingIgnoreLabel[1-5]`
:   Apart from the fixed node labels, the autoscaler can ignore an additional 5 node labels during zone balancing. Example: `balancingIgnoreLabel1:key=value`.



`workerPoolsConfig.json`
:   The worker pools that you want to autoscale, including their minimum and maximum number of worker nodes per zone. The default value is `false`
:   `{"name": "<pool_name>","minSize": 1,"maxSize": 2,"enabled":false}`.
:   `<pool_name>`: The name or ID of the worker pool that you want to enable or disable for autoscaling. To list available worker pools, run `ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>`.
:   `maxSize: <number_of_workers>`: Specify the maximum number of worker nodes per zone that the cluster autoscaler can scale up to. The value must be equal to or greater than the value that you set for the `minSize: <number_of_workers>` size.
:   `min=<number_of_workers>`: Specify the minimum number of worker nodes per zone that the cluster autoscaler can scale down to. The value must be `2` or greater so that your ALB pods can be spread for high availability. If you [disabled](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) all public ALBs in each zone of your standard cluster, you can set the value to `1`. Keep in mind that setting a `min` size does not automatically trigger a scale-up. The `min` size is a threshold so that the cluster autoscaler does not scale to fewer than this minimum number of worker nodes per zone. If your cluster does not have this number of worker nodes per zone yet, the cluster autoscaler does not scale up until you have workload resource requests that require more resources.
:   `enabled=(true|false)`: Set the value to `true` to enable the cluster autoscaler to scale your worker pool. Set the value to `false` to stop the cluster autoscaler from scaling the worker pool. Later, if you want to [remove the cluster autoscaler](/docs/openshift?topic=openshift-cluster-scaling-install-addon#ca-addon-rm), you must first disable each worker pool in the ConfigMap. If you enable a worker pool for autoscaling and then later add a zone to this worker pool, restart the cluster autoscaler pod so that it picks up this change: `oc delete pod -n kube-system <cluster_autoscaler_pod>`. By default, the `default` worker pool is **not** enabled, with a `max` value of `2` and a `min` value of `1`.



