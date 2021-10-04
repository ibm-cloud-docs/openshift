---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-04"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why do pods remain in pending state?
{: #ts-app-pod-pending}

**Infrastructure provider**:
* <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC


When you run `oc get pods`, you can see pods that remain in a **Pending** state.
{: tsSymptoms}


If you just created the {{site.data.keyword.openshiftshort}} cluster, the worker nodes might still be configuring.
{: tsCauses}

If this cluster is an existing one:
*  You might not have enough capacity in your cluster to deploy the pod.
*  The pod might have exceeded a resource request or limit.


This task requires the {{site.data.keyword.cloud_notm}} IAM [**Administrator** platform access role](/docs/containers?topic=containers-users#checking-perms) for the cluster and the [**Manager** service access role](/docs/containers?topic=containers-users#checking-perms) for all namespaces.
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

    1. Confirm that the `resources.requests` values are not larger than the worker node's capacity. For example, if the pod request `cpu: 4000m`, or 4 cores, but the worker node size is only 2 cores, the pod cannot be deployed.

        ```sh
        oc get pod <pod_name> -o yaml
        ```
        {: pre}

    2. If the request exceeds the available capacity, [add a new worker pool](/docs/containers?topic=containers-add_workers#add_pool) with worker nodes that can fulfill the request.

6. If your pods still stay in a **pending** state after the worker node is fully deployed, review the [Kubernetes documentation](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-pod-replication-controller/#my-pod-stays-pending){: external} to further troubleshoot the pending state of your pod.







