---

copyright: 
  years: 2014, 2022
lastupdated: "2022-08-19"

keywords: kubernetes, worker nodes, state

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Cluster states
{: #cluster-states-reference}

You can view the current cluster state by running the `ibmcloud oc cluster ls` command and locating the **State** field.
{: shortdesc}

## Aborted
{: #cluster-state-aborted}

Review the following description of the `Aborted` cluster state. To view the state of your cluster, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
{: shortdesc}

You sent a delete request before the Kubernetes master deployment completed. After your cluster is deleted, it is removed from your dashboard. If your cluster is stuck in this state for a long time, open an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-get-help).

## Critical
{: #cluster-state-critical}

Review the following description of the `Critical` cluster state. To view the state of your cluster, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
{: shortdesc}

The Kubernetes master can't be reached or all worker nodes in the cluster are down. If you enabled {{site.data.keyword.keymanagementservicelong_notm}} in your cluster, the {{site.data.keyword.keymanagementserviceshort}} container might fail to encrypt or decrypt your cluster secrets. If so, you can view an error with more information when you run `oc get secrets`.

## Delete failed
{: #cluster-state-delete-failed}

Review the following description of the `Delete failed` cluster state. To view the state of your cluster, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
{: shortdesc}

The Kubernetes master or at least one worker node can't be deleted. List worker nodes by running `ibmcloud oc worker ls --cluster <cluster_name_or_ID>`. If worker nodes are listed, see [Unable to create or delete worker nodes](/docs/containers?topic=containers-cluster_infra_errors). If no workers are listed, open an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-get-help).

## Deleted
{: #cluster-state-deleted}

Review the following description of the `Deleted` cluster state. To view the state of your cluster, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
{: shortdesc}

The cluster is deleted but not yet removed from your dashboard. If your cluster is stuck in this state for a long time, open an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-get-help).

## Deleting
{: #cluster-state-deleting}

Review the following description of the `Deleting` cluster state. To view the state of your cluster, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
{: shortdesc}

The cluster is being deleted and cluster infrastructure is being dismantled. You can't access the cluster.

## Deploy failed
{: #cluster-state-deploy-failed}

Review the following description of the `Deploy failed` cluster state. To view the state of your cluster, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
{: shortdesc}

The deployment of the Kubernetes master can't be completed. You can't resolve this state. Contact {{site.data.keyword.cloud_notm}} support by opening an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-get-help).

## Deploying
{: #cluster-state-deploying}

Review the following description of the `Deploying` cluster state. To view the state of your cluster, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
{: shortdesc}

The Kubernetes master is not fully deployed yet. You can't access your cluster. Wait until your cluster is fully deployed to review the health of your cluster.

## Normal
{: #cluster-state-normal}

Review the following description of the `Normal` cluster state. To view the state of your cluster, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
{: shortdesc}

All worker nodes in a cluster are up and running. You can access the cluster and deploy apps to the cluster. This state is considered healthy and does not require an action from you.

Although the worker nodes might be normal, other infrastructure resources, such as [networking](/docs/containers?topic=containers-coredns_lameduck) and [storage](/docs/containers?topic=containers-debug_storage_file), might still need attention. If you just created the cluster, some parts of the cluster that are used by other services such as Ingress secrets or registry image pull secrets, might still be in process.
{: note}


## Pending
{: #cluster-state-pending}

Review the following description of the `Pending` cluster state. To view the state of your cluster, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
{: shortdesc}

The Kubernetes master is deployed. The worker nodes are provisioning and aren't available in the cluster yet. You can access the cluster, but you can't deploy apps to the cluster.

## Requested
{: #cluster-state-requested}

Review the following description of the `Requested` cluster state. To view the state of your cluster, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
{: shortdesc}

A request to create the cluster and order the infrastructure for the Kubernetes master and worker nodes is sent. When the deployment of the cluster starts, the cluster state changes to `Deploying`. If your cluster is stuck in the `Requested` state for a long time, open an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-get-help).

## Updating
{: #cluster-state-updating}

Review the following description of the `Updating` cluster state. To view the state of your cluster, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
{: shortdesc}

The Kubernetes API server that runs in your Kubernetes master is being updated to a new Kubernetes API version. During the update, you can't access or change the cluster. Worker nodes, apps, and resources that the user deployed aren't modified and continue to run. Wait for the update to complete to review the health of your cluster.

## Unsupported
{: #cluster-state-unsupported}

Review the following description of the `Unsupported` cluster state. To view the state of your cluster, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
{: shortdesc}

The [Kubernetes version](/docs/containers?topic=containers-cs_versions#cs_versions) that the cluster runs is no longer supported. Your cluster's health is no longer actively monitored or reported. Additionally, you can't add or reload worker nodes. To continue receiving important security updates and support, you must update your cluster. Review the [version update preparation actions](/docs/containers?topic=containers-cs_versions#prep-up), then [update your cluster](/docs/containers?topic=containers-update#update) to a supported Kubernetes version.

## Warning
{: #cluster-state-warning}

Review the following description of the `Warning` cluster state. To view the state of your cluster, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
{: shortdesc}

At least one worker node in the cluster is not available, but other worker nodes are available and can take over the workload. Try to [reload](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) the unavailable worker nodes.
    - Your cluster has zero worker nodes, such as if you created a cluster without any worker nodes or manually removed all the worker nodes from the cluster. [Resize your worker pool](/docs/openshift?topic=openshift-add_workers#resize_pool) to add worker nodes to recover from a `Warning` state, and then [update the Calico node entries for your worker nodes](/docs/containers?topic=containers-zero_nodes_calico_failure).
    - A control plane operation for your cluster failed. View the cluster in the console or run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>` to [check](/docs/containers?topic=containers-debug_master) the **Master Status** for further debugging.






