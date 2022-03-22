---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-22"

keywords: openshift, node scaling, ca, autoscaler

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# (Deprecated) Installing the cluster autoscaler Helm chart in your cluster
{: #cluster-scaling-helm}

The cluster autoscaler Helm chart is deprecated. For the latest version of the cluster autoscaler, [install the add-on](/docs/containers?topic=containers-cluster-scaling-install-addon)
{: deprecated}



Install the {{site.data.keyword.cloud_notm}} cluster autoscaler plug-in with a Helm chart to autoscale worker pools in your cluster.
{: shortdesc}

1. [Prepare your cluster for autoscaling](/docs/containers?topic=containers-cluster-scaling-classic-vpc).
2. [Follow the instructions](/docs/openshift?topic=openshift-helm#install_v3) to install the **Helm version 3** client on your local machine.
3. Add and update the Helm repo where the cluster autoscaler Helm chart is.

    ```sh
    helm repo add iks-charts https://icr.io/helm/iks-charts
    ```
    {: pre}

    ```sh
    helm repo update
    ```
    {: pre}

4. Decide if you want to [customize the cluster autoscaler settings](#ca_chart_values), such as the worker pools that are autoscaled, or the amount of time that the cluster autoscaler waits before scaling worker nodes up or down. You can customize your settings by using the `--set` flag in the `helm install` command. Depending on the settings that you want to customize, you might need to prepare multiple `--set` flags before you can install the Helm chart. For example, you might want to autoscale your default worker pool by preparing the following `--set` flag. Note: If your default command line shell is `zsh`, start a `bash` session before running the following command.
    ```sh
    --set workerpools[0].<pool_name>.max=<number_of_workers>,workerpools[0].<pool_name>.min=<number_of_workers>,workerpools[0].<pool_name>.enabled=(true|false)
    ```
    {: codeblock}

    
    `workerpools[0]`
    :   The first worker pool to enable or disable for autoscaling. You must include three parameters for each worker pool for the command to succeed: the maximum number of worker nodes (`max`), the minimum number of worker nodes (`min`), and whether you want to enable (`true`) or disable (`false`) autoscaling for this worker pool. To include multiple worker pools, include a comma-separated list and increase the number in brackets, such as: `workerpools[0].default...,workerpools[1].pool1...,workerpools[2].pool2...`.
    
    `<pool_name>`
    :   The name or ID of the worker pool that you want to enable or disable for autoscaling. To list available worker pools, run `ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>`.
    
    `max=<number_of_workers>`
    :   Specify the maximum number of worker nodes per zone that the cluster autoscaler can scale up to. The value must be equal to or greater than the value that you set for the `min=<number_of_workers>` size.
    
    `min=<number_of_workers>`
    :   Specify the minimum number of worker nodes per zone that the cluster autoscaler can scale down to. The value must be `2` or greater so that your ALB pods can be spread for high availability. If you [disabled](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) all public ALBs in each zone of your standard cluster, you can set the value to `1`. Keep in mind that setting a `min` size does not automatically trigger a scale-up. The `min` size is a threshold so that the cluster autoscaler does not scale below this minimum number of worker nodes per zone. If your cluster does not have this number of worker nodes per zone yet, the cluster autoscaler does not scale up until you have workload resource requests that require more resources.
    
    `enabled=(true|false)`
    :   Set the value to `true` to enable the cluster autoscaler to scale your worker pool. Set the value to `false` to stop the cluster autoscaler from scaling the worker pool. Later, if you want to [remove the cluster autoscaler](#ca_rm),  you must first disable each worker pool in the configmap.

5. Install the cluster autoscaler Helm chart in the `kube-system` namespace of your cluster. In the example command, the `autoscale` worker pool is enabled for autoscaling with the Helm chart installation. The worker pool details are added to the cluster autoscaler config map.

    ```sh
    helm install ibm-iks-cluster-autoscaler iks-charts/ibm-iks-cluster-autoscaler --namespace kube-system --set workerpools[0].default.max=5,workerpools[0].autoscale.min=2,workerpools[0].default.enabled=true
    ```
    {: pre}

    Example output
    
    ```sh
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
        ```sh
        oc get pods --namespace=kube-system | grep ibm-iks-cluster-autoscaler
        ```
        {: pre}

        Example output
        
        ```sh
        ibm-iks-cluster-autoscaler-8497bfc968-dbn7w   1/1       Running   0          9m
        ```
        {: screen}

    2. Check that the cluster autoscaler service is created.
        ```sh
        oc get service --namespace=kube-system | grep ibm-iks-cluster-autoscaler
        ```
        {: pre}

        Example output
        
        ```sh
        ibm-iks-cluster-autoscaler   ClusterIP   172.21.xxx.xx    <none>        8085/TCP        9m
        ```
        {: screen}

    3. Optional: If you enabled autoscaling for a worker pool during the Helm chart installation, verify that the config map is correct by checking that the `workerPoolsConfig.json` field is updated and that the `workerPoolsConfigStatus` field shows a `SUCCESS` message.
        ```sh
        oc get cm iks-ca-configmap -n kube-system -o yaml
        ```
        {: pre}

        Example output where the default worker pool is enabled for autoscaling:
        ```yaml
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

8. Optional: If you did not set any worker pools for autoscaling with the installation, you can [Update the cluster autoscaler configuration](/docs/containers?topic=containers-cluster-scaling-enable).


## Customizing the cluster autoscaler Helm chart values
{: #ca_chart_values}

The cluster autoscaler Helm chart is deprecated. For the latest version of the cluster autoscaler, [install the add-on](/docs/containers?topic=containers-cluster-scaling-install-addon)
{: deprecated}

1. To change any of the cluster autoscaler configuration values, update the config map or the Helm chart with the new values. Include the `--recreate-pods` flag so that any existing cluster autoscaler pods are re-created to pick up the custom setting changes. The following example command changes the scan interval to `2m` and enables autoscaling for the `autoscale` worker pool, with a maximum of `5` and minimum of `3` worker nodes per zone.

    ```sh
    helm upgrade --set scanInterval=2m --set workerpools[0].default.max=5,workerpools[0].autoscale.min=3,workerpools[0].default.enabled=true ibm-iks-cluster-autoscaler iks-charts/ibm-iks-cluster-autoscaler -i --recreate-pods --namespace kube-system
    ```
    {: pre}

    To reset the Helm chart to the default values:
    ```sh
    helm upgrade --reset-values ibm-iks-cluster-autoscaler iks-charts/ibm-iks-cluster-autoscaler --recreate-pods
    ```
    {: pre}

2. Verify your changes. Review the Helm chart values again.
    
    ```sh
    helm get values ibm-iks-cluster-autoscaler -a
    ```
    {: pre}

3. Verify that the installation is successful. Check that the cluster autoscaler pod is in a **Running** state.

    ```sh
    oc get pods --namespace=kube-system | grep ibm-iks-cluster-autoscaler
    ```
    {: pre}

    Example output
    ```sh
    ibm-iks-cluster-autoscaler-8497bfc968-dbn7w   1/1       Running   0          9m
    ```
    {: screen}

4. Check that the cluster autoscaler service is created.

    ```sh
    oc get service --namespace=kube-system | grep ibm-iks-cluster-autoscaler
    ```
    {: pre}

    Example output
    
    ```sh
    ibm-iks-cluster-autoscaler   ClusterIP   172.21.xxx.xx    <none>        8085/TCP        9m
    ```
    {: screen}

5. Verify that the config map is correct by checking that the `workerPoolsConfig.json` field is updated and that the `workerPoolsConfigStatus` field shows a `SUCCESS` message.

    ```sh
    oc get cm iks-ca-configmap -n kube-system -o yaml
    ```
    {: pre}

    Example output where the `autoscale` worker pool is enabled for autoscaling:
    ```yaml
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
    
    
    
## Upgrading a cluster autoscaler Helm chart release
{: #ca_helm_up}

This topic applies only to the cluster autoscaler Helm chart.
{: important}

The cluster autoscaler Helm chart is deprecated. For the latest version of the cluster autoscaler, [install the add-on](/docs/containers?topic=containers-cluster-scaling-install-addon). You can not have both the cluster autoscaler Helm chart and the cluster autoscaler add-on installed at the same time.
{: deprecated}

You can upgrade your existing cluster autoscaler release to the latest version of the Helm chart. To check your current release version, run `helm list -n <namespace> | grep cluster-autoscaler`. Compare your version to the latest available release by reviewing the **Chart Version** in the [{{site.data.keyword.cloud_notm}} Helm Catalog](https://cloud.ibm.com/kubernetes/helm/iks-charts/ibm-iks-cluster-autoscaler){: external}.
{: shortdesc}

### Prerequisites
{: #ca_helm_up_prereqs}

Before you begin to upgrade your cluster autoscaler release, complete the following steps.
{: shortdesc}

This topic applies only to the cluster autoscaler Helm chart.
{: important}

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
2. To review the changelog of chart versions, [download the source code `tar` file](https://cloud.ibm.com/kubernetes/helm/iks-charts/ibm-iks-cluster-autoscaler) and open the `RELEASENOTES.MD` file.

### Upgrading the cluster autoscaler release version
{: #ca_helm_up_general}

This topic applies only to the cluster autoscaler Helm chart.
{: important}

To upgrade your cluster autoscaler release, you can update the Helm chart repo and re-create the cluster autoscaler pods. Use the same version of Helm that you used to install the initial Helm chart and release.

Before you begin, see the [Prerequisites](#ca_helm_up_prereqs).

1. Update the Helm repo to retrieve the latest version of all Helm charts in this repo.

    ```sh
    helm repo update
    ```
    {: pre}

2. Optional: Download the latest Helm chart to your local machine. Then, extract the package and review the `release.md` file to find the latest release information.

    ```sh
    helm pull iks-charts/ibm-iks-cluster-autoscaler
    ```
    {: pre}

3. Find the name of the cluster autoscaler release that you installed in your cluster.

    ```sh
    helm list -n <namespace> | grep cluster-autoscaler
    ```
    {: pre}

    Example output

    ```sh
    myhelmchart     1           Mon Jan  7 14:47:44 2019    DEPLOYED    ibm-iks-cluster-autoscaler-1.0.1      kube-system
    ```
    {: screen}

4. Upgrade the cluster autoscaler release to the latest version.

    ```sh
    helm upgrade --force --recreate-pods <helm_chart_name>  iks-charts/ibm-iks-cluster-autoscaler
    ```
    {: pre}

5. Verify that the [cluster autoscaler configmap](/docs/containers?topic=containers-cluster-scaling-enable) `workerPoolsConfig.json` section is set to `"enabled": true` for the worker pools that you want to scale.

    ```sh
    oc describe cm iks-ca-configmap -n kube-system
    ```
    {: pre}

    Example output

    ```sh
    NAME:         iks-ca-configmap
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

If you don't want to automatically scale your worker pools, you can uninstall the cluster autoscaler Helm chart. After the removal, you must [resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) or [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) your worker pools manually.
{: shortdesc}

Before you begin: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Optional: To refer to your autoscaling settings later, make a backup of your configmap.

    ```sh
    oc get cm iks-ca-configmap -n kube-system -o yaml > backup_configmap.yaml
    ```
    {: pre}

2. In the [cluster autoscaler configmap](/docs/containers?topic=containers-cluster-scaling-enable), remove the worker pool by setting the `"enabled"` value to `false`.
    ```sh
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


    If you already deleted the Helm chart and see a message such as `iks-ca-configmap not found`, [redeploy the cluster autoscaler Helm chart](#cluster-scaling-helm) to your cluster and try to remove it again.
    {: tip}

3. Disable the add-on or uninstall the Helm chart.

4. **Add-on** Disable the add-on.

    ```sh
    ibmcloud oc cluster addon disable cluster-autoscaler --cluster <cluster_name>
    ```
    {: pre}

5. Verify the add-on is disabled.

    ```sh
    ibmcloud oc cluster addon ls --cluster <cluster_name>
    ```
    {: pre}


6. **Helm chart** List your existing Helm charts and note the name of the cluster autoscaler.

    ```sh
    helm list --all-namespaces
    ```
    {: pre}

7. Remove the existing Helm chart from your cluster.

    ```sh
    helm uninstall ibm-iks-cluster-autoscaler -n <namespace>
    ```
    {: pre}



## Cluster autoscaler Helm chart parameter reference
{: #ca_helm_ref}

This table refers to the cluster autoscaler Helm chart parameters. For add-on values, see [Cluster autoscaler add-on parameter reference](/docs/openshift?topic=openshift-cluster-scaling-install-addon#ca_addon_ref)
{: note}


`api_route`
:   Set the {{site.data.keyword.openshiftlong_notm}} API [endpoint](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cli_api) for the region that your cluster is in. No default; uses the targeted region that your cluster is in.

`resources.limits.cpu`
:   Set the maximum amount of worker node CPU that the `ibm-iks-cluster-autoscaler` pod can consume. The default value is `300m`.

`resources.limits.memory`
:   Set the maximum amount of worker node memory that the `ibm-iks-cluster-autoscaler` pod can consume. The default value is `300Mi`. 

`resources.requests.cpu`
:   Set the minimum amount of worker node CPU that the `ibm-iks-cluster-autoscaler` pod starts with.| The default value is `100m`.

`resources.requests.memory`
:   Set the minimum amount of worker node memory that the `ibm-iks-cluster-autoscaler` pod starts with. The default value is `100Mi`.

`maxNodeProvisionTime`
:   Set the maximum amount of time in minutes that a worker node can take to begin provisioning before the cluster autoscaler cancels the scale-up request. The default value is `120m`.


`scaleDownUnneededTime`
:   Set the amount of time in minutes that a worker node must be unnecessary before it can be scaled down. The default value is `10m`.

`scaleDownDelayAfterAdd`
:   Set the amount of time after scale up that scale down evaluation resumes. The default value for `scaleDownDelayAfterAdd` is 10 minutes. The default value is `10m`.

`scaleDownDelayAfterDelete`
:   Set the amount of time after node deletion that scale down evaluation resumes. The default value for `scaleDownDelayAfterDelete` is the same as the `scan-interval` which is `1m`. The default value is `1m`.

`scaleDownUtilizationThreshold`
:   Set the worker node utilization threshold. If the worker node utilization goes below the threshold, the worker node is considered to be scaled down. Worker node utilization is calculated as the sum of the CPU and memory resources that are requested by all pods that run on the worker node, divided by the worker node resource capacity. The default value is `0.5`.

`scanInterval`
:   Set how often in minutes that the cluster autoscaler scans for workload usage that triggers scaling up or down. The default value is `1m`.

`expander`
:   Specify how the cluster autoscaler determines which worker pool to scale if you have multiple worker pools. The default value is `random`.
:   `random`: Selects randomly between `most-pods` and `least-waste`.
:   `most-pods`: Selects the worker pool that is able to schedule the most pods when scaling up. Use this method if you are using `nodeSelector` to make sure that pods land on specific worker nodes.
:   `least-waste`: Selects the worker pool that has the least unused CPU after scaling up. If two worker pools use the same amount of CPU resources after scaling up, the worker pool with the least unused memory is selected.

`ignoreDaemonSetsUtilization`
:   When set to `true`, the cluster autoscaler ignores DaemonSet pods when it calculates resource utilization for scale-down. The default value is `false`.

`maxBulkSoftTaintCount`
:   Set the maximum number of worker nodes that can be tainted or untainted with `PreferNoSchedule` at the same time. To disable this feature, set to `0`. The default value is `0`.

`maxBulkSoftTaintTime`
:   Set the maximum amount of time that worker nodes can be tainted or untainted with `PreferNoSchedule` at the same time. The default value is `10m`.

`skipNodes.withLocalStorage`
:   When set to `true`, worker nodes that have pods that are saving data to local storage are not scaled down. The default value is `true`.

`skipNodes.withSystemPods`
:   When set to `true`, worker nodes that have `kube-system` pods are not scaled down. Do not set the value to `false` because scaling down `kube-system` pods might have unexpected results. The default value is `true`.

`image.repository`
:   Specify the cluster autoscaler Docker image to use. To get a list of cluster autoscaler images, target the global {{site.data.keyword.registrylong_notm}} API by running `ibmcloud cr region-set global`. Then, list the available cluster autoscaler images by running `ibmcloud cr images --include-ibm | grep cluster-autoscaler`. To review the supported Kubernetes versions for each cluster autoscaler image version, [download the source code `tar` [file](https://cloud.ibm.com/kubernetes/helm/iks-charts/ibm-iks-cluster-autoscaler) and open the `RELEASENOTES.MD` file. The default value is `icr.io/iks-charts/ibm-iks-cluster-autoscaler`.

`image.pullPolicy`
:   Specify when to pull the Docker image. The default value is `IfNotPreset`.
:   `Always`: Pulls the image every time that the pod is started.
:   `IfNotPresent`: Pulls the image only if the image is not already present locally.
:   `Never`: Assumes that the image exists locally and never pulls the image. 

`livenessProbe.periodSeconds`
:   Specify the interval in seconds that the `kubelet` performs a liveness probe. The default value is `10`.|

`livenessProbe.failureThreshold`
:   Specify the number of times that the `kubelet` retries a liveness probe after the pod starts and the first liveness probe fails. After the failure threshold is reached, the container is restarted and the pod is marked `Unready` for a readiness probe, if applicable. The default value is `3`.

`livenessProbe.successThreshold`
:   Specify the minimum, consecutive number of times that the liveness probe must be successful after a previous failure before the pod is marked `Ready`. If you set a liveness probe, you must set this value to at least `1`. The default value is `1`.

`livenessProbe.timeoutSeconds`
:   Specify the time in seconds after which the liveness probe times out. The default value is `10`.

`max-inactivity`
:   Set the maximum time in minutes that the cluster autoscaler pod runs without any recorded activity before the pod is automatically restarted. The default value is `10m`.

`max-failing-time`
:   Set the maximum time in minutes that the cluster autoscaler pod runs without a successfully completed action before the pod is automatically restarted. The default value is `15m`.

`customImageVersion`
:   To override the default installation version, specify the version of the cluster autoscaler Helm chart that you want to install. There is no default value for this parameter.

`maxRetryGap`
:   Set the maximum time in seconds to retry after failing to connect to the service API. Use this parameter and the `retryAttempts` parameter to adjust the retry window for the cluster autoscaler. The default value is `60`.

`retryAttempts`
:   Set the maximum number of attempts to retry after failing to connect to the service API. Use this parameter and the `maxRetryGap` parameter to adjust the retry window for the cluster autoscaler.| The default value is `32`.

`workerpools`
:   The worker pools that you want to autoscale, including their minimum and maximum number of worker nodes per zone. . These settings are mirrored in the [cluster autoscaler](/docs/containers?topic=containers-cluster-scaling-enable) config map. To set the worker pool, format the option as follows: `--set workerpools[0].<pool_name>.max=<number_of_workers>,workerpools[0].<pool_name>.min=<number_of_workers>,workerpools[0].<pool_name>.enabled=(true|false)` Understanding the `--set workerpools` options:
:   `workerpools[0]`: The first worker pool to enable or disable for autoscaling. You must include three parameters for each worker pool for the command to succeed: the maximum number of worker nodes (`max`), the minimum number of worker nodes (`min`), and whether you want to enable (`true`) or disable (`false`) autoscaling for this worker pool. To include multiple worker pools, include a comma-separated list and increase the number in brackets, such as: `workerpools[0].default...,workerpools[1].pool1...,workerpools[2].pool2...`.
:   `<pool_name>`: The name or ID of the worker pool that you want to enable or disable for autoscaling. To list available worker pools, run `ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>`.
:   `max=<number_of_workers>`: Specify the maximum number of worker nodes per zone that the cluster autoscaler can scale up to. The value must be equal to or greater than the value that you set for the `min=<number_of_workers>` size.
:   `min=<number_of_workers>`: Specify the minimum number of worker nodes per zone that the cluster autoscaler can scale down to. The value must be `2` or greater so that your ALB pods can be spread for high availability. If you disabled all public ALBs in each zone of your standard cluster, you can set the value to `1`. Keep in mind that setting a `min` size does not automatically trigger a scale-up. The `min` size is a threshold so that the cluster autoscaler does not scale below this minimum number of worker nodes per zone. If your cluster does not have this number of worker nodes per zone yet, the cluster autoscaler does not scale up until you have workload resource requests that require more resources.
:   `enabled=(true|false)`: Set the value to `true` to enable the cluster autoscaler to scale your worker pool. Set the value to `false` to stop the cluster autoscaler from scaling the worker pool. Later, if you want to [remove the cluster autoscaler](#ca_rm), you must first disable each worker pool in the configmap. If you enable a worker pool for autoscaling and then later add a zone to this worker pool, restart the cluster autoscaler pod so that it picks up this change: `oc delete pod -n kube-system <cluster_autoscaler_pod>`. By default, the `default` worker pool is **not** enabled, with a `max` value of `2` and a `min` value of `1`. The default value is `false`.




