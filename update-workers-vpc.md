---

copyright:
  years: 2026, 2026
lastupdated: "2026-11-05"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, update VPC worker nodes, worker replace, worker reload, bare metal

subcollection: openshift

content-type: howto

---

{{site.data.keyword.attribute-definition-list}}


# Updating VPC worker nodes
{: #update-workers-vpc}

VPC worker nodes are updated differently depending on their type and cluster platform. The `ibmcloud oc worker update` command is not supported for any VPC worker node. In all cases, the cluster master must be updated first.
{: shortdesc}

## How VPC worker node updates work
{: #vpc-worker-faq}


- **VPC bare metal workers**: Updated in place using `ibmcloud oc worker reload`. The node retains its IP address.
- **VPC virtual server instance (VSI) workers**: Replaced using `ibmcloud oc worker replace --update` (to match the master version) or `ibmcloud oc worker replace` (patch refresh only). The old node is deleted and a new one is provisioned.



You can make two types of updates:

* **Patch**: Applies security fixes and updates to the latest patch of the current BOM version. For VPC bare metal workers, use `ibmcloud oc worker reload`. For VPC VSI workers, use `ibmcloud oc worker replace`.
* **Major.minor**: Moves the worker node Kubernetes version up to match the master. Your worker nodes can be at most one version behind the master (`n-1`). For VPC bare metal workers, use `ibmcloud oc worker reload`. For VPC VSI workers, use `ibmcloud oc worker replace --update`.

What happens to my apps during an update?
:   Apps that run on updated worker nodes are rescheduled onto other worker nodes in the cluster. These worker nodes might be in a different worker pool. To avoid downtime, make sure that you have enough capacity in your cluster to carry the workload before you start the update. For more information, see [Adding worker nodes to Classic clusters](/docs/openshift?topic=openshift-add-workers-classic) or [Adding worker nodes to VPC clusters](/docs/openshift?topic=openshift-add-workers-vpc).

What happens to my worker node during an update?
:   For VPC bare metal workers, the worker node is reloaded in place using `worker reload`. The node retains its IP address; data on local disks is deleted and must be stored outside the worker node. For VPC virtual server instance (VSI) workers, the worker node is replaced by removing the old worker node and provisioning a new worker node that runs at the updated patch or `major.minor` version. The replacement worker node is created in the same zone, same worker pool, and with the same flavor as the deleted worker node. However, the replacement worker node is assigned a new private IP address, and loses any custom labels or taints that you applied to the old worker node (worker pool labels and taints are still applied to the replacement worker node).

What if I replace multiple worker nodes at the same time?
:   If you replace multiple worker nodes at the same time, they are deleted and replaced concurrently, not one by one. Make sure that you have enough capacity in your cluster to reschedule your workloads before you replace worker nodes.

What if a replacement worker node is not created?
:   A replacement worker node is not created if the worker pool does not have [automatic rebalancing enabled](/docs/openshift?topic=openshift-auto-rebalance-off).



What happens to the VNIs that are attached to my bare metal worker nodes?
:   A dynamic VNI that is used by an OpenShift Virtualization VM follows the VM when the VM is live migrated off the worker node. A VNI that is attached to the worker node or to the cluster but is not used by any VM is detached when the worker node is replaced. If auto-delete is enabled for the VNI, the VNI is also deleted. You are not notified when unused VNIs are detached. For more information, see [Why are my unused VNIs no longer attached after I replaced a worker node?](/docs/openshift?topic=openshift-vni-virtualization#vni-ts-unused-detached).



## Prerequisites
{: #vpc-worker-prereqs}

Before you update your VPC infrastructure worker nodes, complete the following prerequisite steps.
{: shortdesc}

For VPC VSI workers, the worker node is deleted and replaced with a new node. For VPC bare metal workers, the node is reloaded in place. In both cases, data that is not [stored on persistent storage](/docs/openshift?topic=openshift-storage-plan) is permanently deleted. Verify that any data you need to retain is stored outside the worker node before you begin.
{: important}

Also consider the following storage and networking cases before you update.

* If you have Portworx deployed in your cluster, follow the steps to [update VPC worker nodes with Portworx volumes](/docs/openshift?topic=openshift-storage_portworx_update#portworx_vpc_up) instead of the steps on this page.

* If you have OpenShift Data Foundation deployed in your cluster, follow the steps to [update VPC worker nodes with OpenShift Data Foundation](/docs/openshift?topic=openshift-openshift-storage-update-vpc) instead of the steps on this page.
* If you attached [VNIs](/docs/openshift?topic=openshift-vni-virtualization) to your bare metal worker nodes or cluster, VNIs that are not used by an OpenShift Virtualization VM are detached when the worker node is replaced, and deleted if auto-delete is enabled. Before you replace a worker node, run `ibmcloud oc vni ls --worker WORKER_ID` and note the attached VNIs so that you can reattach them after the replacement. For more information, see [Why are my unused VNIs no longer attached after I replaced a worker node?](/docs/openshift?topic=openshift-vni-virtualization#vni-ts-unused-detached).


1. Complete the steps in [Preparing to update your cluster](/docs/openshift?topic=openshift-update-prepare).
2. [Update the master](/docs/openshift?topic=openshift-update-master). The worker node version can't be higher than the API server version that runs in the master.

## Updating VPC worker nodes in the CLI
{: #vpc-worker-cli}
{: cli}

Complete the following steps to update your worker nodes by using the CLI.
{: shortdesc}

1. Complete the [prerequisite steps](#vpc-worker-prereqs).
2. Optional: Add capacity to your cluster by resizing the worker pool. The pods on the worker node can be rescheduled and continue running on the added worker nodes during the update. For more information, see [Adding worker nodes to Classic clusters](/docs/openshift?topic=openshift-add-workers-classic) or [Adding worker nodes to VPC clusters](/docs/openshift?topic=openshift-add-workers-vpc).
3. List the worker nodes in your cluster and note the **ID** and **Primary IP** of the worker node that you want to update.
    ```sh
    ibmcloud oc worker ls --cluster CLUSTER
    ```
    {: pre}

4. Update the worker node. When you replace or reload a worker node, the pods that run on it are drained and rescheduled onto the remaining worker nodes, and the node is cordoned. The command to use depends on the worker node type.

    **VPC bare metal workers**: Use `worker reload` to reimage the node in place. The node retains its IP address and is updated to the latest patch version.

    ```sh
    ibmcloud oc worker reload --cluster CLUSTER --worker WORKER-NODE-ID
    ```
    {: pre}

    **VPC virtual server instance (VSI) workers**: Use the `worker replace` command to update either the patch version or the `major.minor` version that matches the master version.

    *  To update the worker node to the same `major.minor` version as the master, include the `--update` option.
        ```sh
        ibmcloud oc worker replace --cluster CLUSTER --worker WORKER-NODE-ID --update
        ```
        {: pre}

    *  To update the worker node to the latest patch version at the same `major.minor` version, don't include the `--update` option.
        ```sh
        ibmcloud oc worker replace --cluster CLUSTER --worker WORKER-NODE-ID
        ```
        {: pre}

5. Repeat these steps for each worker node that you must update.
6. Optional: After the replaced worker nodes are in a **Ready** status, resize the worker pool to meet the cluster capacity that you want. For more information, [Adding worker nodes to VPC clusters](/docs/openshift?topic=openshift-add-workers-vpc).

If you are running Portworx in your VPC cluster, you must [manually attach your {{site.data.keyword.block_storage_is_short}} volume to your new worker node.](/docs/openshift?topic=openshift-storage_portworx_update)
{: note}


## Firmware updates during VPC bare metal worker reload
{: #vpc-bm-firmware}

When you reload a VPC bare metal worker node, {{site.data.keyword.cloud_notm}} infrastructure automatically checks whether a firmware update is pending for that server and applies it as part of the reload process. No additional action is required to trigger the firmware update.

Be aware of the following considerations when you reload a VPC bare metal worker node:

Extended reload time
:   If a firmware update is applied during the reload, the total reload time can increase significantly (by 30 minutes or more) beyond the typical reload duration. Plan your maintenance windows accordingly.

No advance visibility into pending updates
:   There is no visibility into whether a firmware update is pending for a worker node before you issue the reload command.

Data loss risk
:   As with all VPC bare metal worker reloads, data on local disks is deleted during the reload regardless of whether a firmware update is applied. Back up any data that is not stored on persistent storage before you reload.

Reload failure due to firmware update
:   In some cases, a firmware update can fail, which causes the worker node to enter a `reload_failed` state (`Failed to reload worker`) with status detail `The infrastructure firmware update has failed. (P4056)`. If this occurs:
    1. Wait a few minutes, then retry the reload by running `ibmcloud oc worker reload --cluster CLUSTER --worker WORKER-NODE-ID` again.
    2. If the error persists after 2–3 attempts, open an [{{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-get-help).


## Updating VPC worker nodes in the console
{: #vpc-worker-ui}
{: ui}

You can update your VPC worker nodes in the console. Before you begin, consider [adding worker nodes](/docs/openshift?topic=openshift-add-workers-vpc) to the cluster to help avoid downtime for your apps.
{: shortdesc}

What the **Update** action does depends on the worker node type and cluster platform:
- **VPC bare metal workers**: The node is reloaded in place. No replacement node is provisioned.
- **VPC virtual server instance (VSI) workers**: The worker node is replaced with a new node at the updated version.


1. Complete the [prerequisite steps](#vpc-worker-prereqs).
2. From the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external} menu ![Menu icon](../icons/icon_hamburger.svg "Menu icon"), click **Containers** > **Clusters**.
3. From the **Clusters** page, click your cluster.
4. From the **Worker Nodes** tab, select the checkbox for each worker node that you want to update. An action bar is displayed over the table header row.
5. From the action bar, click **Update**.

## Next steps
{: #vpc-worker-next-steps}

Repeat the update process with other worker pools. When all worker pools are updated, [update your cluster components and managed add-ons](/docs/openshift?topic=openshift-update-components).

Notify all developers who work in the cluster to [update their `oc` CLI](/docs/openshift?topic=openshift-cli-install) to match the Kubernetes master version. Running a `oc` client that is two or more versions apart from the server version is not supported and can cause unexpected errors.
{: important}

## Related links
{: #vpc-worker-related}

* [Updating clusters, worker nodes, and cluster components](/docs/openshift?topic=openshift-update)
* [Worker node states](/docs/openshift?topic=openshift-worker-node-state-reference)
* [Why doesn't replacing a worker node create a worker node?](/docs/openshift?topic=openshift-auto-rebalance-off)
