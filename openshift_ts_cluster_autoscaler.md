---

copyright:
  years: 2014, 2020
lastupdated: "2020-03-18"

keywords: openshift, roks, rhoks, rhos

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


# Cluster autoscaler
{: #troubleshoot_cluster_autoscaler}

As you use the [cluster autoscaler](/docs/openshift?topic=openshift-ca) for {{site.data.keyword.openshiftlong}}, consider these techniques for troubleshooting.
{: shortdesc}

## Debugging the cluster autoscaler
{: #debug_cluster_autoscaler}

Review the options that you have to debug your cluster autoscaler and find the root causes for failures.
{: shortdesc}

Before you begin, [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster)..

1.  Check that your cluster runs the latest version of the cluster autoscaler Helm chart. 
    1.  Check the chart version. The **CHART** name has the version in the format `ibm-iks-cluster-autoscaler-1.1.2`.
        ```
        helm ls
        ```
        {: pre}

        Example output:
        ```
        NAME                      	REVISION	UPDATED                 	STATUS  	CHART                           	APP VERSION	NAMESPACE  
        ibm-iks-cluster-autoscaler	1       	Wed Aug 28 16:38:23 2019	DEPLOYED	ibm-iks-cluster-autoscaler-1.0.8	           	kube-system
        ```
        {: screen}
    2.  Compare the version that runs in your cluster against the [latest **CHART VERSION** of the `ibm-iks-cluster-autoscaler` Helm chart](https://cloud.ibm.com/kubernetes/helm/iks-charts/ibm-iks-cluster-autoscaler) in the **Helm Catalog** console.
    3.  If your version is outdated, [deploy the latest cluster autoscaler to your cluster](/docs/openshift?topic=openshift-ca#ca_helm).
2.  Check that the cluster autoscaler is configured correctly.
    1.  Get the YAML configuration file of the cluster autoscaler configmap.
        ```
        oc get cm iks-ca-configmap -n kube-system -o yaml > iks-ca-configmap.yaml
        ```
        {: pre}
    2.  In the `data.workerPoolsConfig.json` field, check that the correct worker pools are enabled with the minimum and maximum size per worker pool. 
        *  **`"name": "<worker_pool_name>"`**: The name of your worker pool in the configmap must be exactly the same as the name of the worker pool in your cluster. Multiple worker pools must be comma-separated. To check the name of your cluster worker pools, run `ibmcloud oc worker-pool ls -c <cluster_name_or_ID>`.
        *  **`"minSize": 2`**: In general, the `minSize` must be `2` or greater. Remember that the `minSize` value cannot be `0`, and you can only have a `minSize` of 1 if you [disable the public ALBs](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure).
        * **`"maxSize": 3`**: The `maxSize` must be equal to or greater than the `minSize`.
        * **`"enabled": true`**: Set the value to `true` to enable autoscaling the worker pool.
        ```
        data:
            workerPoolsConfig.json: |
                [{"name": "default", "minSize": 2, "maxSize": 3, "enabled": true }]
        ```
        {: screen}
    3.  In the `metadata.annotations.workerPoolsConfigStatus` field, check for a **FAILED CODE** error message. Follow any recovery steps that are included in the error message. For example, you might get a message similar to the following, where you must have the correct permissions to the resource group that the cluster is in.
        ```
        annotations:
            workerPoolsConfigStatus: '{"1:3:default":"FAILED CODE: 400
            ...
            \"description\":\"Unable
            to validate the request with resource group manager.\",\"type\":\"Authentication\",\"recoveryCLI\":\"To
            list available resource groups, run ''ibmcloud resource groups''. Make sure
            that your cluster and the other IBM Cloud resources that you are trying to use
            are in the same resource group. Verify that you have permissions to work with
            the resource group. If you think that the resource group is set up correctly
            and you still cannot use it, contact IBM Cloud support.\"}"}'
        ```
        {: screen}
3.  Review the status of the cluster autoscaler.
    ```
    oc describe cm -n kube-system cluster-autoscaler-status
    ```
    {: pre}

    * **`status`**: Review the status message for more troubleshooting information, if any.
    * **`Health`**: Review the overall health of the cluster autoscaler for any errors or failures.
    * **`ScaleUp`**: Review the status of scaleup activity. In general, if the number of worker nodes that are ready and registered match, the scaleup has `NoActivity` because your worker pool has enough worker nodes.
    * **`ScaleDown`**: Review the status of scaledown activity. If the cluster autoscaler identifies `NoCandidates`, your worker pool is not scaled down because none of the worker nodes can be removed without taking away requested resources from your workloads.
    * **`Events`**: Review the events for more troubleshooting information, if any.

    Example of a healthy cluster autoscaler status.
    ```
    Data
    ====
    status:
    ----
    Cluster-autoscaler status at 2020-02-04 19:51:50.326683568 +0000 UTC:
    Cluster-wide:
    Health:      Healthy (ready=2 unready=0 notStarted=0 longNotStarted=0 registered=2 longUnregistered=0)
                LastProbeTime:      2020-02-04 19:51:50.324437686 +0000 UTC m=+9022588.836540262
                LastTransitionTime: 2019-10-23 09:36:25.741087445 +0000 UTC m=+64.253190008
    ScaleUp:     NoActivity (ready=2 registered=2)
                LastProbeTime:      2020-02-04 19:51:50.324437686 +0000 UTC m=+9022588.836540262
                LastTransitionTime: 2019-10-23 09:36:25.741087445 +0000 UTC m=+64.253190008
    ScaleDown:   NoCandidates (candidates=0)
                LastProbeTime:      2020-02-04 19:51:50.324437686 +0000 UTC m=+9022588.836540262
                LastTransitionTime: 2019-10-23 09:36:25.741087445 +0000 UTC m=+64.253190008

    Events:  <none>
    ```
    {: screen}
4.  Check the health of the cluster autoscaler pod.
    1.  Get the cluster autoscaler pod. If the status is not **Running**, describe the pod.
        ```
        oc get pods -n kube-system | grep ibm-iks-cluster-autoscaler
        ```
        {: pre}
    2.  Describe the cluster autoscaler pod. Review the **Events** section for more troubleshooting information.
        ```
        oc describe pod -n kube-system <pod_name>
        ```
        {: pre}
    3.  Review the **Command** section to check that the [custom cluster autoscaler configuration](/docs/openshift?topic=openshift-ca#ca_chart_values) matches what you expect, such as the `scale-down-delay-after-add` value.
        ```
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
5.  Search the logs of the cluster autoscaler pod for relevant messages, such as failure messages like `lastScaleDownFailTime`, the `Final scale-up plan`, or [cluster autoscaler events](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#what-events-are-emitted-by-ca){: external}.

    If your cluster autoscaler pod is unhealthy and cannot stream logs, check your [{{site.data.keyword.la_full}} instance](https://cloud.ibm.com/observe/logging) for the pod logs. Note that if your cluster administrator did not [enable {{site.data.keyword.la_short}} for your cluster](/docs/containers?topic=containers-health), you might not have any logs to review.
    {: tip}

    ```
    oc logs -n kube-system <pod_name> > logs.txt
    ```
    {: screen}

6.  If you do not find any failures or error messages and you already enabled logging, restart the cluster autoscaler pod. The deployment recreates the pod.
    ```
    oc delete pod -n kube-system <pod_name>
    ```
    {: pre}
7.  Monitor the cluster autoscaler activities in your cluster to see if the issue is resolved. If you still experience issues, see [Feedback, questions, and support](#getting_help).

## Feedback, questions, and support
{: #getting_help}

Still having issues with your cluster? Review different ways to get help and support for your Red Hat OpenShift on IBM Cloud clusters. For any questions or feedback, post in Slack.
{: shortdesc}

**General ways to resolve issues**<br>
1. Keep your cluster environment up to date.
   * Check monthly for available security and operating system patches to [update your worker nodes](/docs/openshift?topic=openshift-update#worker_node).
   * [Update your cluster](/docs/openshift?topic=openshift-update#master) to the latest default version for [OpenShift](/docs/openshift?topic=openshift-openshift_versions).
2. Make sure that your command line tools are up to date.
   * In the terminal, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and flags.
   * Make sure that [your `oc` CLI](/docs/openshift?topic=openshift-openshift-cli#kubectl) client matches the same Kubernetes version as your cluster server. [Kubernetes does not support](https://kubernetes.io/docs/setup/release/version-skew-policy/){: external} `oc` client versions that are 2 or more versions apart from the server version (n +/- 2).
<br>

**Reviewing issues and status**<br>
1. To see whether {{site.data.keyword.cloud_notm}} is available, [check the {{site.data.keyword.cloud_notm}} status page](https://cloud.ibm.com/status?selected=status){: external}.
2. Filter for the **Kubernetes Service** component.
<br>

**Feedback and questions**<br>
1. Post in the {{site.data.keyword.containershort}} Slack.
   * If you are an external user, post in the [#openshift](https://ibm-cloud-success.slack.com/messages/CKCJLJCH4){: external} channel.
   * If you are an IBMer, use the [#iks-openshift-users](https://ibm-argonauts.slack.com/messages/CJH0UPN2D){: external} channel.<p class="tip">If you do not use an IBMid for your {{site.data.keyword.cloud_notm}} account, [request an invitation](https://cloud.ibm.com/kubernetes/slack){: external} to this Slack.</p>
2. Review forums such as OpenShift help, Stack Overflow, and IBM Developer to see whether other users ran into the same issue. When you use the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.
   * If you have technical questions about developing or deploying clusters or apps with Red Hat OpenShift on IBM Cloud, post your question on [Stack Overflow](https://stackoverflow.com/questions/tagged/ibm-cloud+containers){: external} and tag your question with `ibm-cloud`, `containers`, and `openshift`.
   * For questions about the service and getting started instructions, use the [IBM Developer Answers](https://developer.ibm.com/answers/topics/containers/?smartspace=bluemix){: external} forum. Include the `ibm-cloud` and `containers` tags.
   * See [Getting help](/docs/get-support?topic=get-support-getting-customer-support#using-avatar) for more details about using the forums.
<br>

**Getting help**<br>
1. Before you open a support case, gather relevant information about your cluster environment.
   1. Get your cluster details.
      ```
      ibmcloud oc cluster get -c <cluster_name_or_ID>
      ```
      {: pre}
   2. If your issue involves worker nodes, get the worker node details.
      1. List all worker nodes in the cluster, and note the **ID** of any worker nodes with an unhealthy **State** or **Status**.
         ```
         ibmcloud oc worker ls -c <cluster_name_or_ID>
         ```
         {: pre}
      2. Get the details of the unhealthy worker node.
         ```
         ibmcloud oc worker get -w <worker_ID> -c <cluster_name_or_ID>
         ```
         {: pre}
   3. For issues with resources within your cluster such as pods or services, log in to the cluster and use the Kubernetes API to get more information about them. 
   
   3.11 clusters only: You can also use the [{{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool](/docs/openshift?topic=openshift-cs_troubleshoot#debug_utility) to gather and export pertinent information to share with IBM Support.
   {: tip}

2.  Contact IBM Support by opening a case. To learn about opening an IBM support case, or about support levels and case severities, see [Contacting support](/docs/get-support?topic=get-support-getting-customer-support).
3.  In your support case, for **Category**, select **Containers**.
4.  For the **Offering**, select your OpenShift cluster. Include the relevant information that you previously gathered.



