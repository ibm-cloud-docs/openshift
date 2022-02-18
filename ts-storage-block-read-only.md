---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-18"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does block storage change to read-only?
{: #readonly_block}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


You might see the following symptoms:
{: tsSymptoms}
- When you run `oc get pods -o wide`, you see that multiple pods on the same worker node are stuck in the `ContainerCreating` or `CrashLoopBackOff` state. All these pods use the same block storage instance.
- When you run a `oc describe pod` command, you see the following error in the **Events** section: `MountVolume.SetUp failed for volume ... read-only`.


If a network error occurs while a pod writes to a volume, IBM Cloud infrastructure protects the data on the volume from getting corrupted by changing the volume to a read-only mode. Pods that use this volume can't continue to write to the volume and fail.
{: tsCauses}

Verify the plug-in version, re-create your app, and gracefully reload your worker node.
{: tsResolve}

1. Check the version of the {{site.data.keyword.cloud_notm}} Block Storage plug-in that is installed in your cluster.
    ```sh
    helm list --all-namespaces
    ```
    {: pre}

2. Verify that you use the [latest version of the {{site.data.keyword.cloud_notm}} Block Storage plug-in](https://cloud.ibm.com/kubernetes/helm/iks-charts/ibmcloud-block-storage-plugin). If not, [update your plug-in](/docs/containers?topic=containers-block_storage#update_block).
3. If you used a Kubernetes deployment for your pod, restart the pod that is failing by removing the pod and letting Kubernetes re-create it. If you did not use a deployment, retrieve the YAML file that was used to create your pod by running `oc get pod <pod_name> -o yaml >pod.yaml`. Then, delete and manually re-create the pod.
    ```sh
    oc delete pod <pod_name>
    ```
    {: pre}

4. Check whether re-creating your pod resolved the issue. If not, reload the worker node.
    1. Find the worker node where your pod runs and note the private IP address that is assigned to your worker node.
        ```sh
        oc describe pod <pod_name> | grep Node
        ```
        {: pre}

        Example output:
        ```sh
        Node:               10.75.XX.XXX/10.75.XX.XXX
        Node-Selectors:  <none>
        ```
        {: screen}

    2. Retrieve the **ID** of your worker node by using the private IP address from the previous step.
        ```sh
        ibmcloud oc worker ls --cluster <cluster_name_or_ID>
        ```
        {: pre}

    3. Gracefully [reload the worker node](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload).







