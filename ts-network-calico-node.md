---

copyright: 
  years: 2022, 2022
lastupdated: "2022-10-03"

keywords: openshift, calico, node

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why does my worker node show a `NetworkUnavailable` error?
{: #ts-network-calico-node}
{: support}

Supported infrastructure providers
:   Classic
:   VPC
:   {{site.data.keyword.satelliteshort}}

When you update your master or worker nodes, your worker nodes enter a `NetworkUnavailable` state.
{: tsSymptoms}

Your worker nodes might enter a `NetworkUnavailable` state whenever the `calico-node` pod has been shut down. This might happen during a Calico patch update, but shouldn't impact your application availability.
{: tsCauses}

When Calico is updated, the `node.kubernetes.io/network-unavailable:NoSchedule` taint is added to your worker node and the `NetworkUnavailable` condition becomes `True`. Both of these conditions are cleared when Calico restarts, which typically takes only a few seconds.

In some cases. the restart might take longer. In nearly all cases, the restart is fast enough to avoid any worker node network issues. However, there are situations where a Calico restart is delayed and thus, there could be network interruptions.  For these cases, the node network unavailable taint and condition are designed to keep new apps from being deployed to the new node until Calico and the node are fixed. Calico updates are rolled out in a very controlled manner so as to minimize overall application impact should there be a node problem.

Monitor the `NetworkUnavailable` state with {{site.data.keyword. monitoringlong_notm}}
{: tsResolve}

By using monitoring applications such as {{site.data.keyword.monitoringlong_notm}}, you can configure alters for when a worker node goes into a `NetworkUnavailable` state, and count each time this happens. You can also configure thresholds and tune your alerts to allow for when worker nodes `NetworkUnavailable` state during routine Calico patches.

When you set up {{site.data.keyword.monitoringlong_notm}} alerts, take the following scenarios into consideration.

- A `NetworkUnavailable` alert might become a problem when a `calico-node` pod fails to achieve a `Running` state, and its container restart count continues to increase.
- A worker node remains in `NetworkUnavailable` state for a long amount of time.
