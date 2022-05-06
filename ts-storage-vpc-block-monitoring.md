---

copyright: 
  years: 2022, 2022
lastupdated: "2022-05-06"

keywords: vpc, monitoring, block storage, metrics

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Debugging {{site.data.keyword.block_storage_is_short}} metrics 
{: #debug_monitoring}
{: troubleshoot}
{: support}

When you try to view {{site.data.keyword.block_storage_is_short}} metrics in the monitoring dashboard, the metrics do not populate. 
{: tsSymptoms}

Metrics might fail to populate in the dashboard for one of the following reasons: 
* The PVC you want to monitor may not be mounted. Metrics are only populated for PVCs that are mounted to a pod.
* There may be a console-related issue, which can be verified by manually viewing the storage metrics in the CLI. 
{: tsCauses}

Check that the PVC is mounted. If the issue persists, manually view your metrics in the CLI to determine if the cause is related to issues with the console. 
{: tsResolve}

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

2. Describe the PVC. If the **Used By** row of the output is populated with the name of a pod, then the PVC is mounted. 

    ```sh
    oc describe pvc <pvc_name>
    ```
    {: pre}

    Example output. 

    ```sh
    Name:          my-pvc
    Namespace:     default
    StorageClass:  ibmc-vpc-block-5iops-tier
    Status:        Bound
    Volume:        pvc-a11a11a1-111a-111a-a1a1-aaa111aa1a1a 
    Labels:        <none>
    Annotations:   pv.kubernetes.io/bind-completed: yes
                   pv.kubernetes.io/bound-by-controller: yes
                   volume.beta.kubernetes.io/storage-provisioner: vpc.block.csi.ibm.io
    Finalizers:    [kubernetes.io/pvc-protection]
    Capacity:      10Gi
    Access Modes:  RWO
    VolumeMode:    Filesystem
    Used By:       my-pod-11a1a1a1a1-1a11a 
    Events:        <none>
    ```
    {: screen}

3. If the PVC is not mounted to a pod, review the steps for [setting up {{site.data.keyword.block_storage_is_short}}](/docs/openshift?topic=openshift-vpc-block#vpc-block-add) and mount the PVC to a pod. Then try to view the metrics again. 
4. If the PVC is mounted, follow the steps for [manually verifying the {{site.data.keyword.block_storage_is_short}} metrics](#manual-monitor-metrics) then [open a support issue](/docs/openshift?topic=openshift-get-help#help-support). The steps for manual verification in the CLI allow you to view your metrics, but are not a solution for metrics that do not populate in the console. However, if you are able to manually verify your metrics, this indicates that there is a console issue for which you must open an issue.

## Manually viewing storage metrics in the CLI
{: #manual-monitor-metrics}

If your storage metrics are not visible in the monitoring dashboard, you can manually view them in the CLI. Note that manual verification of your storage metrics is a temporary workaround and not a permanent monitoring solution for viewing metrics. After completing the following steps, if you are able to manually view the metrics in the CLI and not the dashboard, this indicates that there is a console issue for which you must [open a support issue](/docs/openshift?topic=openshift-get-help#help-support).
{: shortdesc}

After you complete the following steps, make sure to remove the resources you created while debugging. 
{: important}


1. Create and deploy a custom `clusterRole` configuration. In this example, the `clusterRole` is named `test-metrics-reader`.

    ```yaml
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRole
    metadata:
    name: test-metrics-reader
    rules:
    - nonResourceURLs:
        - "/metrics"
        verbs:
        - get
    - apiGroups:
        - ""
        resources:
        - nodes/metrics
        verbs:
        - get
    ```
    {: pre}

    ```sh
    oc apply -f <file_name>
    ```
    {: pre}

1. Create a service account. In this example, the service account is named `test-sa`.

    ```sh
    oc create sa test-sa
    ```
    {: pre}

1. Add a `clusterRoleBinding` to the `clusterRole`.

    ```sh
    oc create clusterrolebinding test-metrics-reader --clusterrole test-metrics-reader --serviceaccount=default:test-sa
    ```
    {: pre}

1. List your nodes and note the name and IP of the node for which you want to gather metrics. 

    ```sh
    oc get nodes
    ```
    {: pre}

    Example output.

    ```sh
    NAME          STATUS    ROLES    AGE     VERSION              
    10.111.1.11   Ready     <none>   1d      v1.22.7+IKS            
    ```
    {: screen}

1. Create a yaml file to deploy a pod onto the node. Make sure to specify the service account you created and the node IP address.

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
    name: testpod
    spec:
    nodeName: 10.111.1.111
    containers:
    - image: nginx
        name: nginx
    serviceAccountName: test-sa
    ```
    {: pre}

    ```sh
    oc apply -f <file_name>
    ```
    {: pre}

1. Retrieve the service account token from within the pod. 

    1. Log in to the pod.

        ```sh
        kubectl exec testpod -it -- bash
        ```
        {: pre}

    1. Run the following command to get the token. Note that there is no output. 

        ```sh
        token=$(cat /var/run/secrets/kubernetes.io/serviceaccount/token)
        ```
        {: pre}

1. While you are still logged in to the pod, run the command to view the storage metrics. Make sure to specify the node IP address. 

    ```sh
    curl -k -H "authorization: bearer <token> https://<node_IP>:10250/metrics | grep kubelet_volume_stats
    ```
    {: pre}

1. View the metrics in the terminal output. You may have to wait several minutes for the metrics to output. If you are still unable to view metrics, [open a support issue](/docs/openshift?topic=openshift-get-help#help-support).

1. After you have finished viewing the metrics, and determined whether the issue is related to dashboard or the metrics agent, delete the configurations and resources that you created in the previous steps.

Do not skip this step. 
{: important}

1. Exit the pod.
    ```sh
    exit
    ```
    {: pre}

1. Delete the pod.
    ```sh 
    oc delete pod testpod
    ```
    {: pre}

1. Delete the `clusterRoleBinding`.
    ```sh
    oc delete clusterrolebinding test-metrics-reader
    ```
    {: pre}

1. Delete the service account. 
    ```sh
    oc delete sa test-sa
    ```
    {: pre}

1. Delete the cluster role.
    ```sh
    oc delete clusterrole test-metrics-reader
    ```
    {: pre}
    
    
    
