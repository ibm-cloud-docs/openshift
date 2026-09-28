---

copyright:
  years: 2014, 2026
lastupdated: "2026-09-28"


keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}





# Why doesn't replacing a worker node create a worker node?
{: #auto-rebalance-off}
{: support}

Troubleshoot worker node autorebalancing issues.
{: shortdesc}


[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}


When you [replace a worker node](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-replace-cli) or [update a VPC worker node](/docs/openshift?topic=openshift-update#vpc_worker_node), a worker node is not automatically added back to your cluster.
{: tsSymptoms}


By default, your worker pools are set to automatically rebalance when you replace a worker node. However, you might have disabled automatic rebalancing by manually removing a worker node, such as in the following scenario.
{: tsCauses}

1. You have a worker pool that automatically rebalances by default.
2. You have a troublesome worker node in the worker pool that you removed individually, such as with the `ibmcloud oc worker rm` command.
3. Now, automatic rebalancing is disabled for your worker pool, and is not reset unless you try to rebalance or resize the worker pool.
4. You try to maintain a worker node using one of the following commands, but no additional worker node is created to replace it.
    - **Classic bare metal workers**: `ibmcloud oc worker reload` reloads the worker in place (no deletion or addition). `ibmcloud oc worker update` moves the worker to the master BOM version.
    - **VPC bare metal workers**: `ibmcloud oc worker reload` reloads the worker in place (no deletion or addition). `ibmcloud oc worker replace` or `ibmcloud oc worker replace --update` are also supported and delete and reprovision the node with a new IP address.
    - **VPC virtual server instance (VSI) workers**: `ibmcloud oc worker replace --update` deletes the existing worker and provisions a new one at the master version. `ibmcloud oc worker replace` does the same at the current patch version. Note that `ibmcloud oc worker update` is not supported for VPC worker nodes.

You might also have issued the `remove` command shortly after the `replace` command. If the `remove` command is processed before the `replace` command, the worker pool automatic rebalancing is still disabled, so your worker node is not replaced.
{: note}

To enable automatic rebalancing, [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-rebalance-cli) or [resize](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-resize-cli) your worker pool. Now, when you replace a worker node, another worker node is created for you.
{: tsResolve}
