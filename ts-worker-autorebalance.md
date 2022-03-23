---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-23"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# VPC: Why doesn't replacing a worker node create a worker node?
{: #auto-rebalance-off}
{: support}

**Infrastructure provider**: 
![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC
![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic


When you [replace a worker node](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_replace) or [update a VPC worker node](/docs/containers?topic=containers-update#vpc_worker_node), a worker node is not automatically added back to your cluster.
{: tsSymptoms}


By default, your worker pools are set to automatically rebalance when you replace a worker node. However, you might have disabled automatic rebalancing by manually removing a worker node, such as in the following scenario.
{: tsCauses}

1. You have a worker pool that automatically rebalances by default.
2. You have a troublesome worker node in the worker pool that you removed individually, such as with the `ibmcloud oc worker rm` command.
3. Now, automatic rebalancing is disabled for your worker pool, and is not reset unless you try to rebalance or resize the worker pool.
4. You try to replace a worker node with the `ibmcloud oc worker replace` command or update a VPC worker node with the `ibmcloud oc worker replace --update` command. The worker node is removed, but another worker node is not added back to your worker pool.

You might also have issued the `remove` command shortly after the `replace` command. If the `remove` command is processed before the `replace` command, the worker pool automatic rebalancing is still disabled, so your worker node is not replaced.
{: note}


To enable automatic rebalancing, [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) or [resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) your worker pool. Now, when you replace a worker node, another worker node is created for you.
{: tsResolve}






