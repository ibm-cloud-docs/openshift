---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-16"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why do pods remain in pending state?
{: #ts-app-pod-pending}
{: support}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


When you run `oc get pods`, you can see pods that remain in a **Pending** state.
{: tsSymptoms}


If you just created the {{site.data.keyword.openshiftshort}} cluster, the worker nodes might still be configuring.
{: tsCauses}

If this cluster is an existing one:
*  You might not have enough capacity in your cluster to deploy the pod.
*  The pod might have exceeded a resource request or limit.


This task requires the {{site.data.keyword.cloud_notm}} IAM [**Administrator** platform access role](/docs/openshift?topic=openshift-users#checking-perms) for the cluster and the [**Manager** service access role](/docs/openshift?topic=openshift-users#checking-perms) for all namespaces.
{: tsResolve}

If you just created the {{site.data.keyword.openshiftshort}} cluster, run the following command and wait for the worker nodes to initialize.

```sh
oc get nodes
```
{: pre}

If this cluster is an existing one, check your cluster capacity.



1. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select your cluster.
2. Click **{{site.data.keyword.openshiftshort}} web console**.

3. Check if you have enough capacity in your cluster to deploy your pod.

4. If you don't have enough capacity in your cluster, resize your worker pool to add more nodes.

    1. Review the current sizes and flavors of your worker pools to decide which one to resize.

        ```sh
        ibmcloud oc worker-pool ls
        ```
        {: pre}

    2. Resize your worker pools to add more nodes to each zone that the pool spans.

        ```sh
        ibmcloud oc worker-pool resize --worker-pool <worker_pool> --cluster <cluster_name_or_ID> --size-per-zone <workers_per_zone>
        ```
        {: pre}

5. Optional: Check your pod resource requests.

    1. Confirm that the `resources.requests` values are not larger than the worker node's capacity. For example, if the pod request `cpu: 4000m`, or 4 cores, but the worker node size is only 2 cores, the pod can't be deployed.

        ```sh
        oc get pod <pod_name> -o yaml
        ```
        {: pre}

    2. If the request exceeds the available capacity, [add a new worker pool](/docs/openshift?topic=openshift-add_workers#add_pool) with worker nodes that can fulfill the request.

6. If your pods still stay in a **pending** state after the worker node is fully deployed, review the [Kubernetes documentation](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-pod-replication-controller/#my-pod-stays-pending){: external} to further troubleshoot the pending state of your pod.







