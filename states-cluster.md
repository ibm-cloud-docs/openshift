---

copyright: 
  years: 2014, 2025
lastupdated: "2025-10-06"


keywords: kubernetes, worker nodes, state

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Cluster states and statuses
{: #cluster-states-reference}

The **Master Status** provides details of what operation from the master state is in progress. The status includes a timestamp of how long the master has been in the same state, such as `Ready (1 month ago)`. The **Master State** reflects the lifecycle of possible operations that can be performed on the master, such as deploying, updating, and deleting. Each state and status is described in the following documentation.
{: shortdesc}


Review your cluster state in the console or by running the following commands.

```sh
ibmcloud oc cluster ls
```
{: pre}

```sh
ibmcloud oc cluster get --cluster <cluster_name_or_ID>
```
{: pre}



## Aborted
{: #cluster-state-aborted}

You sent a delete request before the Kubernetes master deployment completed. After your cluster is deleted, it is removed from your dashboard. If your cluster is stuck in this state for a long time, open an [{{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-get-help).

## Critical
{: #cluster-state-critical}

The Kubernetes master can't be reached or all worker nodes in the cluster are down. If you enabled {{site.data.keyword.keymanagementservicelong_notm}} in your cluster, the {{site.data.keyword.keymanagementserviceshort}} container might fail to encrypt or decrypt your cluster secrets. If so, you can view an error with more information when you run `oc get secrets`.

## Create failed
{: #cluster-state-create-failed}

The cluster cannot be created. Delete the failed cluster and try to create another one. If the issue persists when creating additional clusters, open an [{{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-get-help). 

## Delete failed
{: #cluster-state-delete-failed}

The Kubernetes master or at least one worker node can't be deleted. List worker nodes by running `ibmcloud oc worker ls --cluster <cluster_name_or_ID>`.

IBM Support is notified and works to resolve the issue. You can't resolve the issue by trying to delete the cluster again.

Instead, check the **Master Status** field for more information, or wait for the cluster to delete. 
- If worker nodes are listed, see [Unable to create or delete worker nodes](/docs/openshift?topic=openshift-cluster_infra_errors).
- If no workers are listed, open an [{{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-get-help).

## Deleted
{: #cluster-state-deleted}

The cluster is deleted but not yet removed from your dashboard. If your cluster is stuck in this state for a long time, open an [{{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-get-help).

## Deleting
{: #cluster-state-deleting}

The cluster is being deleted and cluster infrastructure is being dismantled. You can't access the cluster. You can't undo a deletion. After the cluster is deleted, you can no longer check the master state because the cluster is completely removed.

## Deployed
{: #cluster-state-deployed}

The master is successfully deployed. Check the status to verify that the master is `Ready` or to see if an update is available.

## Deploy failed
{: #cluster-state-deploy-failed}

The deployment of the Kubernetes master can't be completed. You can't resolve this state. Contact {{site.data.keyword.cloud_notm}} support by opening an [{{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-get-help).

## Deploying
{: #cluster-state-deploying}

The Kubernetes master is not fully deployed yet. You can't access your cluster. Wait until your cluster is fully deployed to review the health of your cluster.

## Error 
{: #cluster-state-error}

The master is not operational. IBM is automatically notified and takes action to resolve this issue. You can continue monitoring the health until the master is `normal`. You can also [open an {{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-get-help).

## Normal
{: #cluster-state-normal}

All worker nodes in a cluster are up and running. You can access the cluster and deploy apps to the cluster. This state is considered healthy and does not require an action from you.

Although the worker nodes might be normal, other infrastructure resources, such as [networking](/docs/containers?topic=containers-coredns_lameduck) and [storage](/docs/openshift?topic=openshift-debug_storage_file), might still need attention. If you just created the cluster, some parts of the cluster that are used by other services such as Ingress secrets or registry image pull secrets, might still be in process.
{: note}


## Pending
{: #cluster-state-pending}

The Kubernetes master is deployed. The worker nodes are provisioning and aren't available in the cluster yet. You can access the cluster, but you can't deploy apps to the cluster.

## Requested
{: #cluster-state-requested}

A request to create the cluster and order the infrastructure for the Kubernetes master and worker nodes is sent. When the deployment of the cluster starts, the cluster state changes to `Deploying`. If your cluster is stuck in the `Requested` state for a long time, open an [{{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-get-help).

## Scaled down
{: #cluster-state-scaled-down}

The master resources have been scaled down to zero replicas. This is a temporary state that occurs while etcd is being restored after a backup. You cannot interact with your cluster while it is in this state. Wait for the etcd restoration to complete and the master state to return to `deployed`.

## Update failed
{: #cluster-state-failed}

The master update failed. IBM Support is notified and works to resolve the issue. You can continue to monitor the health of the master until the master reaches a normal state. If the master remains in this state for more than 1 day, [open an {{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-get-help). IBM Support might identify other issues in your cluster that you must fix before the master can be updated.


## Updating
{: #cluster-state-updating}

The master is updating its Kubernetes version. The update might be a patch update that is automatically applied, or a minor or major version that you applied by updating the cluster. The Kubernetes API server that runs in your Kubernetes master is being updated to a new Kubernetes API version. During the update, you can still access and change the cluster. However, you cannot initiate concurrent master operations, such as enabling API server auditing. Worker nodes, apps, and resources that the user deployed aren't modified and continue to run. Wait for the update to complete to review the health of your cluster. During the update, your highly available master can continue processing requests, and your app workloads and worker nodes continue to run. After the master update is complete, you can [update your worker nodes](/docs/openshift?topic=openshift-update#worker_node). If the update is unsuccessful, the master returns to a `deployed` state and continues running the previous version. IBM Support is notified and works to resolve the issue. You can check if the update failed in the **Master Status** field.

## Update canceled
{: #cluster-state-canceled}

The master update is canceled because the cluster was not in a healthy state at the time of the update. Your master remains in this state until your cluster is healthy and you manually update the master. To update the master, use the `ibmcloud oc cluster master update` [command](/docs/containers?topic=containers-kubernetes-service-cli#cs_cluster_update). If you don't want to update the master to the default `major.minor` version during the update, include the `--version` option and specify the latest patch version that is available for the `major.minor` version that you want, such as `1.33`. To list available versions, run `ibmcloud oc versions`.

## Unavailable
{: #cluster-state-unavailable}

The master might not be accessible, which means some actions such as resizing a worker pool are temporarily unavailable. IBM is automatically notified and takes action to resolve this issue. You can continue monitoring the health until the master is `normal`.

## Unsupported
{: #cluster-state-unsupported}

The [Kubernetes version](/docs/containers?topic=containers-cs_versions#cs_versions) that the cluster runs is no longer supported. Your cluster's health is no longer actively monitored or reported. Additionally, you can't add or reload worker nodes. To continue receiving important security updates and support, you must update your cluster. Review the [version update preparation actions](/docs/containers?topic=containers-cs_versions#prep-up), then [update your cluster](/docs/openshift?topic=openshift-update#update) to a supported Kubernetes version.

## Warning
{: #cluster-state-warning}

At least one worker node in the cluster is not available, but other worker nodes are available and can take over the workload. Try to [reload](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) the unavailable worker nodes.
- Your cluster has zero worker nodes, such as if you created a cluster without any worker nodes or manually removed all the worker nodes from the cluster. Resize your worker pool to add worker nodes to recover from a `Warning` state, and then [update the Calico node entries for your worker nodes](/docs/openshift?topic=openshift-zero_nodes_calico_failure).
- A control plane operation for your cluster failed. View the cluster in the console or run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>` to [check](/docs/openshift?topic=openshift-debug_master) the **Master Status** for further debugging.
