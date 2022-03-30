---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-30"

keywords: openshift, node scaling, ca, autoscaler

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Setting up autoscaling for your worker pools
{: #cluster-scaling-enable}

Update the cluster autoscaler configmap to enable automatically scaling worker nodes in your worker pools based on the minimum and maximum values that you set.
{: shortdesc}

After you edit the configmap to enable a worker pool, the cluster autoscaler scales your cluster in response to your workload requests. As such, you can't [resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) or [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) your worker pools. Scanning and scaling up and down happens at regular intervals over time, and depending on the number of worker nodes might take a longer period of time to complete, such as 30 minutes. Later, if you want to [remove the cluster autoscaler](/docs/openshift?topic=openshift-cluster-scaling-install-addon#ca-addon-rm), you must first disable each worker pool in the configmap.
{: note}

**Before you begin**:
*  Install the [cluster autoscaler add-on](/docs/containers?topic=containers-cluster-scaling-install-addon).
*  [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

**To update the cluster autoscaler configmap and values**:

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

2. Edit the configmap with the parameters to define how the cluster autoscaler scales your cluster worker pool. **Note:** Unless you [disabled](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) all public application load balancers (ALBs) in each zone of your standard cluster, you must change the `minSize` to `2` per zone so that the ALB pods can be spread for high availability.

    - `"name": "default"`: Replace `"default"` with the name or ID of the worker pool that you want to scale. To list worker pools, run `ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>`. To manage more than one worker pool, copy the JSON line to a comma-separated line, such as follows.
    
        ```sh
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
    - `"enabled": false`: Set the value to `true` for the cluster autoscaler to manage scaling for the worker pool. Set the value to `false` to stop the cluster autoscaler from scaling the worker pool. Later, if you want to [remove the cluster autoscaler](/docs/openshift?topic=openshift-cluster-scaling-install-addon#ca-addon-rm), you must first disable each worker pool in the configmap.

3. Save the configuration file.

4. Get your cluster autoscaler pod.

    ```sh
    oc get pods -n kube-system
    ```
    {: pre}

5. Review the **`Events`** section of the cluster autoscaler pod for a **`ConfigUpdated`** event to verify that the configmap is successfully updated. The event message for your configmap is in the following format: `minSize:maxSize:PoolName:<SUCCESS|FAILED>:error message`.

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

**Before you begin**:
*  [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
*  [Install the `ibm-iks-cluster-autoscaler` add-on](/docs/containers?topic=containers-cluster-scaling-install-addon).

### Customizing the cluster autoscaler add-on configmap
{: #cluster-scaling-customize}

When you modify a configmap parameter other than the worker pool `minSize`, `maxSize`, or if you enable or disable a worker pool, the cluster autoscaler pods are restarted.
{: note}

1. Review the [cluster autoscaler configmap](/docs/openshift?topic=openshift-cluster-scaling-install-addon#ca_addon_ref) parameters.

2. Download the cluster autoscaler add-on configmap and review the parameters.

    ```sh
    oc get cm iks-ca-configmap -n kube-system -o yaml > configmap.yaml
    ```
    {: pre}

3. Open the `configmap.yaml` file and update the settings that you want to change.

4. Reapply the cluster autoscaler add-on configmap.

    ```sh
    oc apply -f configmap.yaml
    ```
    {: pre}

5. Verify that the pods are restarted successfully.

    ```sh
    oc get pods -n kube-system | grep autoscaler
    ```
    {: pre}
    
    
    
    
