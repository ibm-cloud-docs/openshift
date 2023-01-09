---

copyright: 
  years: 2022, 2023
lastupdated: "2023-01-06"

keywords: openshift, calico, node

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}




# Why does my worker node show a `NetworkUnavailable` error?
{: #ts-network-calico-node}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}

When you update your master or worker nodes, your worker nodes enter a `NetworkUnavailable` state.
{: tsSymptoms}

Your worker nodes might enter a `NetworkUnavailable` state whenever the `calico-node` pod has been shut down. This might happen during a Calico patch update, but shouldn't impact your application availability.
{: tsCauses}

When Calico is updated, the `node.kubernetes.io/network-unavailable:NoSchedule` taint is added to your worker node and the `NetworkUnavailable` condition becomes `True`. Both of these conditions are cleared when Calico restarts, which typically takes only a few seconds.

Sometimes, the restart might take longer. In nearly all cases, the restart is fast enough to avoid any worker node network issues. However, there are situations where a Calico restart is delayed and thus, there could be network interruptions. For these cases, the node network unavailable taint and condition are designed to keep new apps from being deployed to the new node until Calico and the node are fixed. Calico updates are rolled out in a very controlled manner so as to minimize overall application impact should there be a node problem.

Monitor the `NetworkUnavailable` state with {{site.data.keyword.monitoringlong_notm}}
{: tsResolve}

By using services to monitor applications such as {{site.data.keyword.monitoringlong_notm}}, you can configure alerts for when a worker node goes into a `NetworkUnavailable` state, and count each time this happens. You can also configure thresholds and tune your alerts to allow for when worker nodes `NetworkUnavailable` state during routine Calico patches.

When you set up {{site.data.keyword.monitoringlong_notm}} alerts, take the following scenarios into consideration.

- A `NetworkUnavailable` alert might become a problem when a `calico-node` pod fails to achieve a `Running` state, and its container restart count continues to increase.
- A worker node remains in `NetworkUnavailable` state for a long amount of time.

After a worker update or replace, sometimes the `calico-node` pod still does not start on {{site.data.keyword.redhat_openshift_notm}} VPC Cluster. The `calico_node` pod might get stuck in a state where it is unable to start on a {{site.data.keyword.redhat_openshift_notm}} VPC cluster. This is not an issue on IKS or Classic clusters. This can occur when you have the `sysdig-admission-controller-webhook` installed and try to do a worker update or replace. This happens because:

1. The VPN client pod gets moved to the new worker as it is starting.
2. `calico-node` on the new worker starts up, but gets stuck because it makes an `apiserver` call and times out after 2 seconds.
3. The `apiserver` call then tries to call the webhook which fails because the VPN client pod was trying to start on the new node. The VPN node cannot successfully do so because `calico-node` hasn't started up yet.

In summary, the `calico-node` pod startup depends on the webhook working; the webhook depends on the VPN client pod; and the VPN client pod depends on `calico-node` starting up. The system is stuck in a circular dependency. If you are able to gather logs from a successfully deployed `calico-node` pod, you might see an error like this:

```txt
2022-09-08 07:13:19.719 [WARNING][9] startup/utils.go 228: Failed to set NetworkUnavailable; will retry error=Patch "https://172.21.0.1:443/api/v1/nodes/10.242.64.17/status?timeout=2s": net/http: request canceled (Client.Timeout exceeded while awaiting headers)
```
{: pre}

## Workarounds for `calico-node`
{: #ts-network-calico-node-work}

You can use one of the following methods to work around the issue and get the `calico-node` pod running again.
1. Remove the `sysdig-admission-controller-webhook` from the system. 
2. Modify the `sysdig-admission-controller-webhook` and change the timeout to be less than 2 seconds. 
3. Modify the `sysdig-admission-controller-webhook` to scope it to the appropriate namespaces, and avoid system-critical namespaces such as `calico-system`.  
4. Cordon the new node but don't drain it. Delete the VPN pod and wait for it to start on another worker. Uncordon the node.

After performing any of the previous workarounds, the `calico-node` pod can start successfully.

