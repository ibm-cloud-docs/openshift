---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-03"

keywords: openshift, node scaling, ca, autoscaler

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Deploying apps to your autoscaled worker pools
{: #cluster-scaling-deploy-apps}

To limit a pod deployment to a specific worker pool that is managed by the cluster autoscaler, use a combination of labels and `nodeSelector` or `nodeAffinity` to deploy apps only to the autoscaled worker pools. With `nodeAffinity`, you have more control over how the scheduling behavior works to match pods to worker nodes. Then, use taints and tolerations so that only these apps can run on your autoscaled worker pools.
{: shortdesc}

For more information, see the following Kubernetes docs:
* [Assigning pods to nodes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/){: external}
* [Taints and tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external}

**Before you begin**:
*  [Install the `ibm-iks-cluster-autoscaler` plug-in](/docs/openshift?topic=openshift-cluster-scaling-install-addon).
*  [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

**To limit pods to run on certain autoscaled worker pools**:

1. Make sure that you labeled and tainted your autoscaled worker pool as described in [Preparing your cluster for autoscaling](/docs/openshift?topic=openshift-cluster-scaling-classic-vpc).
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
    ```sh
    oc apply -f pod.yaml
    ```
    {: pre}



## Scaling up worker nodes before the worker pool has insufficient resources
{: #ca_scaleup}

As described in the [Understanding how the cluster autoscaler works](/docs/openshift?topic=openshift-cluster-scaling-classic-vpc#ca_about) topic and the [Kubernetes Cluster Autoscaler FAQs](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md){: external}, the cluster autoscaler scales up your worker pools in response to your requested resources of the workload against the available recourses of the worker pool. However, you might want the cluster autoscaler to scale up worker nodes before the worker pool runs out of resources. In this case, your workload does not need to wait as long for worker nodes to be provisioned because the worker pool is already scaled up to meet the resource requests.
{: shortdesc}

The cluster autoscaler does not support early scaling (overprovisioning) of worker pools. However, you can configure other Kubernetes resources to work with the cluster autoscaler to achieve early scaling.

## Pause pods
{: #pause-pods-ca}

You can create a deployment that deploys [pause containers](https://stackoverflow.com/questions/48651269/what-are-the-pause-containers){: external} in pods with specific resource requests, and assign the deployment a low pod priority. When these resources are needed by higher priority workloads, the pause pod is preempted and becomes a pending pod. This event triggers the cluster autoscaler to scale up.
{: shortdesc}

For more information about setting up a pause pod deployment, see the [Kubernetes FAQ ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-can-i-configure-overprovisioning-with-cluster-autoscaler). You can use [this example overprovisioning configuration file ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Cloud/kube-samples/blob/master/ibm-ks-cluster-autoscaler/overprovisioning-autoscaler.yaml) to create the priority class, service account, and deployments.

If you use this method, make sure that you understand how [pod priority](/docs/containers?topic=containers-pod_priority) works and how to set pod priority for your deployments. For example, if the pause pod does not have enough resources for a higher priority pod, the pod is not preempted. The higher priority workload remains in pending, so the cluster autoscaler is triggered to scale up. However, in this case, the scale-up action is not early because the workload that you want to run can't be scheduled because of insufficient resources. Pause pod must have the matching `nodeAffinity` or `nodeSelector` as well as the matching tolerations that you set for your worker pool.
{: note}

## Horizontal pod autoscaling (HPA)
{: #hpca}

Because horizontal pod autoscaling is based on the average CPU usage of the pods, the CPU usage limit that you set is reached before the worker pool runs out of resources.
{: shortdesc}

More pods are requested, which then triggers the cluster autoscaler to scale up the worker pool.  For more information about setting up HPA, see the [Kubernetes docs](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/){: external}.




