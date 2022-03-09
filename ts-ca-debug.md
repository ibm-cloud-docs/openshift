---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-09"

keywords: openshift, autoscaler

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Debugging the cluster autoscaler
{: #debug_cluster_autoscaler}
{: support}

Review the options that you have to debug your cluster autoscaler and find the root causes for failures.
{: shortdesc}

Before you begin: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

## Step 1: Check the version
{: #ca-debug-version}

1. Verify that the cluster autoscaler addon is installed and ready.
    ```sh
    ibmcloud oc cluster addon ls --cluster <CLUSTER_NAME>
    ```
    {: pre}

    Example output
    ```sh
    Name                 Version   Health State   Health Status   
    cluster-autoscaler   1.0.4     normal         Addon Ready 
    ```
    {: screen}

2. Compare the version that runs in your cluster against the latest version in Cluster autoscaler add-on [changelog](/docs/containers?topic=containers-ca_changelog).
3. If your version is outdated, deploy the latest cluster autoscaler version to your cluster.

**Deprecated** You can install the cluster autoscaler Helm chart, but the helm chart is deprecated and becomes unsupported tentatively 15 September 2020. You can't install the add-on and the Helm chart in the same cluster at the same time. 

## Step 2: Check the configuration
{: #ca-debug-config}

Check that the cluster autoscaler is configured correctly.
1. Get the YAML configuration file of the cluster autoscaler configmap.
    ```sh
    oc get cm iks-ca-configmap -n kube-system -o yaml > iks-ca-configmap.yaml
    ```
    {: pre}

2. In the `data.workerPoolsConfig.json` field, check that the correct worker pools are enabled with the minimum and maximum size per worker pool.

    *  **`"name": "<worker_pool_name>"`**: The name of your worker pool in the configmap must be exactly the same as the name of the worker pool in your cluster. Multiple worker pools must be comma-separated. To check the name of your cluster worker pools, run `ibmcloud oc worker-pool ls -c <cluster_name_or_ID>`.
    *  **`"minSize": 2`**: In general, the `minSize` must be `2` or greater. Remember that the`minSize` value can't be `0`, and you can only have a `minSize` of 1 if you [disable the public ALBs](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure).
    * **`"maxSize": 3`**: The `maxSize` must be equal to or greater than the `minSize`.
    * **`"enabled": true`**: Set the value to `true` to enable autoscaling the worker pool.

    ```sh
    data:
        workerPoolsConfig.json: |
            [{"name": "default", "minSize": 2, "maxSize": 3, "enabled": true }]
    ```
    {: screen}

3. In the `metadata.annotations.workerPoolsConfigStatus` field, check for a **FAILED CODE** error message. Follow any recovery steps that are in the error message. For example, you might get a message similar to the following, where you must have the correct permissions to the resource group that the cluster is in.

    ```yaml
    annotations:
        workerPoolsConfigStatus: '{"1:3:default":"FAILED CODE: 400
        ...
        \"description\":\"Unable
        to validate the request with resource group manager.\",\"type\":\"Authentication\\"recoveryCLI\":\"To
        list available resource groups, run ''ibmcloud resource groups''. Make sure
        that your cluster and the other IBM Cloud resources that you are trying to use
        are in the same resource group. Verify that you have permissions to work with
        the resource group. If you think that the resource group is set up correctly
        and you still can't use it, contact IBM Cloud support.\"}"}'
    ```
    {: screen}

## Step 3: Review the cluster autoscaler status
{: #ca-debug-status}

Review the status of the cluster autoscaler.
```sh
oc describe cm -n kube-system cluster-autoscaler-status
```
{: pre}

* **`status`**: Review the status message for more troubleshooting information, if any.
* **`Health`**: Review the overall health of the cluster autoscaler for any errors or failures.
* **`ScaleUp`**: Review the status of scaleup activity. In general, if the number of worker nodes that are ready and registered match, the scaleup has `NoActivity` because your worker pool has enough worker nodes.
* **`ScaleDown`**: Review the status of scaledown activity. If the cluster autoscaler identifies `NoCandidates`, your worker pool is not scaled down because none of the worker nodes can be removed without taking away requested resources from your workloads.
* **`Events`**: Review the events for more troubleshooting information, if any.

**Example of a healthy cluster autoscaler status**

```sh
Data
====
status:
----
Cluster-autoscaler status at 2020-02-04 19:51:50.326683568 +0000 UTC:
Cluster-wide:
Health:      Healthy (ready=2 unready=0 notStarted=0 longNotStarted=0 registered=2longUnregistered=0)
            LastProbeTime:      2020-02-04 19:51:50.324437686 +0000 UTC m=+9022588.836540262
            LastTransitionTime: 2019-10-23 09:36:25.741087445 +0000 UTC m=+64.253190008
ScaleUp:     NoActivity (ready=2 registered=2)
            LastProbeTime:      2020-02-04 19:51:50.324437686 +0000 UTC m=+9022588.836540262
            LastTransitionTime: 2019-10-23 09:36:25.741087445 +0000 UTC m=+64.253190008
ScaleDown:   NoCandidates (candidates=0)
            LastProbeTime:      2020-02-04 19:51:50.324437686 +0000 UTC m=+9022588.836540262
            LastTransitionTime: 2019-10-23 09:36:25.741087445 +0000 UTC m=+64.253190008
Events:  none
```
{: screen}

## Step 4: Check the cluster autoscaler pod
{: #ca-debug-pod}

Check the health of the cluster autoscaler pod.
1. Get the cluster autoscaler pod. If the status is not **Running**, describe the pod.
    ```sh
    oc get pods -n kube-system | grep ibm-iks-cluster-autoscaler
    ```
    {: pre}

2. Describe the cluster autoscaler pod. Review the **Events** section for more troubleshooting information.

    ```sh
    oc describe pod -n kube-system <pod_name>
    ```
    {: pre}

3. Review the **Command** section to check that the [custom cluster autoscaler configuration](/docs/openshift?topic=openshift-cluster-scaling-enable) matches what you expect, such as the`scale-down-delay-after-add` value.
    ```sh
    Command:
        ./cluster-autoscaler
        --v=4
        --balance-similar-node-groups=true
        --alsologtostderr=true
        --stderrthreshold=info
        --cloud-provider=IKS
        --skip-nodes-with-local-storage=true
        --skip-nodes-with-system-pods=true
        --scale-down-unneeded-time=10m
        --scale-down-delay-after-add=10m
        --scale-down-delay-after-delete=10m
        --scale-down-utilization-threshold=0.5
        --scan-interval=1m
        --expander=random
        --leader-elect=false
        --max-node-provision-time=120m
    ```
    {: screen}

## Step 5: Search the pod logs
{: #ca-debug-pod-logs}

Search the logs of the cluster autoscaler pod for relevant messages, such as failure messages like `lastScaleDownFailTime`, the `Final scale-up plan`, or [cluster autoscaler events](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#what-events-are-emitted-by-ca){: external}.

If your cluster autoscaler pod is unhealthy and can't stream logs, check your [{{site.data.keyword.la_full}} instance](https://cloud.ibm.com/observe/logging) for the pod logs. Note that if your cluster administrator did not [enable {{site.data.keyword.la_short}} for your cluster](/docs/containers?topic=containers-health), you might not have any logs to review.
{: tip}

```sh
oc logs -n kube-system <pod_name> > logs.txt
```
{: screen}

## Step 5: Restart the pod
{: #ca-debug-pod-restart}

If you don't find any failures or error messages and you already enabled logging, restart the cluster autoscaler pod. The deployment re-creates the pod.

```sh
oc delete pod -n kube-system <pod_name>
```
{: pre}

## Step 6: Disable and reenable
{: #ca-debug-disable}

Optional: If you completed the debugging steps and your cluster still does not scale, you can disable and reenable the autoscaler by editing the config map.
1. Edit the `iks-ca-configmap`.

    ```sh
    oc edit cm iks-ca-configmap -n kube-system
    ```
    {: pre}

    Example output:
    ```yaml
    apiVersion: v1
    data:
    workerPoolsConfig.json: |
        [{"name": "default", "minSize": 2, "maxSize": 5, "enabled": true }]
    kind: ConfigMap
    metadata:
    annotations:
        workerPoolsConfigStatus: '{"2:5:default":"SUCCESS"}'
    creationTimestamp: "2020-03-24T17:44:35Z"
    name: iks-ca-configmap
    namespace: kube-system
    resourceVersion: "40964517"
    selfLink: /api/v1/namespaces/kube-system/configmaps/iks-ca-configmap
    uid: 11a1111a-aaaa-1a11-aaa1-aa1aaaa11111
    ```
    {: codeblock}

2. Set the `enabled` parameter to `false` and save your changes.
3. Edit the `iks-ca-configmap` again. Set the enabled parameter to `true` and save your changes.
    ```sh
    oc edit cm iks-ca-configmap -n kube-system
    ```
    {: pre}

4. If your cluster still does not scale after disabling and reenabling the cluster autoscaler,you can edit the `minSize` or `maxSize` parameters in the `iks-ca-configmap`. Sometimes,editing the `minSize` and `maxSize` worker parameters successfully restarts the cluster autoscaler.
    ```sh
    oc edit cm iks-ca-configmap -n kube-system
    ```
    {: pre}

5. Edit the `minSize` or `maxSize` parameters and save your changes.

## Step 8: Check if the issue is resolved
{: #ca-debug-more}

Monitor the cluster autoscaler activities in your cluster to see if the issue is resolved. If you still experience issues, see [Feedback, questions, and support](/docs/containers?topic=containers-get-help).




