---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-14"

keywords: kubernetes, worker nodes, state

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Worker node states
{: #worker-node-state-reference}


You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

## Critical
{: #worker-node-critical}

You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

A worker node can go into a `Critical` state for many reasons: 
- You initiated a reboot for your worker node without cordoning and draining your worker node. Rebooting a worker node can cause data corruption in `containerd`, `kubelet`, `kube-proxy`, and `calico`.
- The pods that are deployed to your worker node don't use proper resource limits for [memory](https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource){: external} and [CPU](https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource){: external}. If you set none or excessive resource limits, pods can consume all available resources, leaving no resources for other pods to run on this worker node. This overcommitment of workload causes the worker node to fail.
    1. List the pods that run on your worker node and review the CPU and memory usage, requests and limits. 
        ```bash
        oc describe node <worker_private_IP>
        ```
        {: pre}

    2. For pods that consume a lot of memory and CPU resources, check if you set proper resource limits for memory and CPU.
        ```bash
        oc get pods <pod_name> -n <namespace> -o json
        ```
        {: pre}

    3. Optional: Remove the resource-intensive pods to free up compute resources on your worker node.
        ```bash
        oc delete pod <pod_name>
        ```
        {: pre}
        
        ```bash
        oc delete deployment <deployment_name>
        ```
        {: pre}

- `containerd`, `kubelet`, or `calico` went into an unrecoverable state after it ran hundreds or thousands of containers over time.
- You set up a Virtual Router Appliance for your worker node that went down and cut off the communication between your worker node and the Kubernetes master. 
- Current networking issues in {{site.data.keyword.containerlong_notm}} or IBM Cloud infrastructure that causes the communication between your worker node and the Kubernetes master to fail.
- Your worker node ran out of capacity. Check the **Status** of the worker node to see whether it shows **Out of disk** or **Out of memory**. If your worker node is out of capacity, consider to either reduce the workload on your worker node or add a worker node to your cluster to help load balance the workload.
- The device was powered off from the [{{site.data.keyword.cloud_notm}} console resource list](https://cloud.ibm.com/resources){: external}. Open the resource list and find your worker node ID in the **Devices** list. In the action menu, click **Power On**.
- In many cases, [reloading](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) your worker node can solve the problem. When you reload your worker node, the latest [patch version](/docs/containers?topic=containers-cs_versions#update_types) is applied to your worker node. The major and minor version is not changed. Before you reload your worker node, make sure to cordon and drain your worker node to ensure that the existing pods are terminated gracefully and rescheduled onto remaining worker nodes. If reloading the worker node does not resolve the issue, go to the next step to continue troubleshooting your worker node.
        






## Deleting
{: #worker-node-deleting}

You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

A `Deleting` state means that you requested to delete the worker node, possibly as part of resizing a worker pool or autoscaling the cluster. Other operations can't be issued against the worker node while the worker node deletes. You can't reverse the deletion process. When the deletion process completes, you are no longer billed for the worker nodes.

## Deleted
{: #worker-node-deleted}

You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

A `Deleted` state means that your worker node is deleted, and no longer is listed in the cluster or billed. This state can't be undone. Any data that was stored only on the worker node, such as container images, are also deleted.



## Deployed
{: #worker-node-deployed}

You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

Updates are successfully deployed to your worker node. After updates are deployed, {{site.data.keyword.openshiftlong_notm}} starts a health check on the worker node. After the health check is successful, the worker node goes into a `Normal` state. Worker nodes in a `Deployed` state usually are ready to receive workloads, which you can check by running `oc get nodes` and confirming that the state shows `Normal`. 



## Deploying
{: #worker-node-deploying}

You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

A `Deploying` state means that when you update the Kubernetes version of your worker node, your worker node is redeployed to install the updates. If you reload or reboot your worker node, the worker node is redeployed to automatically install the latest patch version. If your worker node is stuck in this state for a long time, check whether a problem occurred during the deployment. 



## Deploy_failed
{: #worker-node-deploy-failed}

You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

A `Deploy_failed` state means that your worker node could not be deployed. List the details for the worker node to find the details for the failure by running `ibmcloud oc worker get --cluster <cluster_name_or_id> --worker <worker_node_id>`.


## Normal
{: #worker-node-normal}

You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

A `Normal` state means that your worker node is fully provisioned and ready to be used in the cluster. This state is considered healthy and does not require an action from the user. 

Although the worker nodes might be normal, other infrastructure resources, such as [networking](/docs/containers?topic=containers-coredns_lameduck) and [storage](/docs/containers?topic=containers-debug_storage_file), might still need attention.
{: note}

## Provisioned
{: #worker-node-provisioned}

You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

A `Provisioned` state means that your worker node completed provisioning and is part of the cluster. Billing for the worker node begins. The worker node state soon reports a regular health state and status, such as `normal` and `ready`.


## Provisioning
{: #worker-node-provisioning}

You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

A `Provisioning` state means that your worker node is being provisioned and is not available in the cluster yet. You can monitor the provisioning process in the **Status** column of your CLI output. If your worker node is stuck in this state for a long time, check whether a problem occurred during the provisioning.



## Provision pending
{: #worker-node-provision-pending}

You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

A `Provision pending` state means that another process is completing before the worker node provisioning process starts. You can monitor the other process that must complete first in the **Status** column of your CLI output. For example, in VPC clusters, the `Pending security group creation` indicates that the security group for your worker nodes is creating first before the worker nodes can be provisioned. If your worker node is stuck in this state for a long time, check whether a problem occurred during the other process.




## Provision_failed
{: #worker-node-provision-failed}

You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

Your worker node could not be provisioned. List the details for the worker node to find the details for the failure by running `ibmcloud oc worker get --cluster <cluster_name_or_id> --worker <worker_node_id>`.



## Reloading
{: #worker-node-reloading}

You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

A `Reloading` state means that your worker node is being reloaded and is not available in the cluster. You can monitor the reloading process in the **Status** column of your CLI output. If your worker node is stuck in this state for a long time, check whether a problem occurred during the reloading.


## Reloading_failed
{: #worker-node-reloading-failed}

You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

A `Reloading_failed` state means that your worker node could not be reloaded. List the details for the worker node to find the details for the failure by running `ibmcloud oc worker get --cluster <cluster_name_or_id> --worker <worker_node_id>`.

## Reload_pending
{: #worker-node-reload-pending}

You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

You requested to reload or to update the Kubernetes version of your worker node. When reloading begins, the state changes to `Reloading`.

## Unknown
{: #worker-node-unknown}

You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

An `Unknown` state means that the Kubernetes master is not reachable for one of the following reasons:
- You requested an update of your Kubernetes master. The state of the worker node can't be retrieved during the update. If the worker node remains in this state for an extended period of time even after the Kubernetes master is successfully updated, try to [reload the worker node](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload).
- You might have another firewall that is protecting your worker nodes, or changed firewall settings recently. {{site.data.keyword.openshiftlong_notm}} requires certain IP addresses and ports to be opened to allow communication from the worker node to the Kubernetes master and vice versa. For more information, see [Firewall prevents worker nodes from connecting](/docs/openshift?topic=openshift-firewall#vyatta_firewall).
- The Kubernetes master is down. Contact {{site.data.keyword.cloud_notm}} support by opening an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-get-help).

## Warning
{: #worker-node-warning}

You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
{: shortdesc}

A `Warning` state means that your worker node is reaching the limit for memory or disk space. You can either reduce workload on your worker node or add a worker node to your cluster to help load balance the workload.





