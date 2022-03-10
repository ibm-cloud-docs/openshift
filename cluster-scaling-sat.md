---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-10"

keywords: openshift, node scaling, ca, autoscaler

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Preparing to autoscale {{site.data.keyword.satelliteshort}} clusters
{: #cluster-scaling-sat}

Autoscaling on {{site.data.keyword.satelliteshort}} clusters is available in Beta for allowlisted accounts only.
{: beta}

How does scale-up work for {{site.data.keyword.satelliteshort}} clusters?
:   The cluster autoscaler periodically checks for pods that are stuck in pending state due to lack of memory or CPU resources. 
    1. The autoscaler checks whether scaling is enabled on any of the work pools in the cluster, if scaling is enabled, then the autoscaler calculates the required number to worker nodes to accommodate all the pods that are stuck in pending state. If no worker pools have autoscaling enabled, then no action occurs.
    1. The autoscaler compares required worker node count, which was calculated in the previous step, and compares it to the `MaxSize` or total amount worker nodes allowed for scaling. If the `MaxSize` allowed is less than or equal to the required worker node count to satisfy all pods, the autoscaler sends a resize request to the instance group.
    1. The autoscaler fetches the hosts that are `Ready` or `Unassigned` in the location and that have host labels that match the labels on the worker nodes in the worker pool where autoscaling is enabled. 
    1. The autoscaler determines if there are enough available `Ready` or `Unassigned` hosts to satisfy the resize request. 
        * If there are not enough hosts available in the location, then a warning is added to the logs that the resize operation was incomplete.
        * If there are available hosts that are `Ready` or `Unassigned` and have the matching host labels, the autoscaler uses those hosts to fulfill the request.
        * If no hosts are available with the matching host labels, the autoscaler filters the `Ready` or `Unassigned` hosts for those with only the default host labels. Then, the autoscaler updates the labels on those hosts to match the host labels of the worker pool where scaling is enabled and uses these hosts to fulfill the request.

How does scale-down happen in {{site.data.keyword.satelliteshort}} clusters?
:   When the cluster autoscaler determines that a worker node is underutilized for the specified `scaleDownUnneededTime` time, then the workers are deleted from the cluster.
:   The hosts where that were used for those worker nodes are then in the `Reload Required` or `Unassigned` state in the location. These hosts cannot be used by any other cluster until they are Reloaded and re-attached to the location.


## Preparing {{site.data.keyword.satelliteshort}} clusters for autoscaling
{: #prepare-autoscale-sat}

1. [Create a location](/docs/satellite?topic=satellite-locations) and set up your control plane.
1. [Create a cluster in your location](/docs/openshift?topic=openshift-satellite-clusters).
1. Attach additional hosts to your location, but leave them unassigned. These `Ready/Unassigned` hosts are available for autoscaling.
1. Install the cluster [add-on in your cluster](/docs/containers?topic=containers-cluster-scaling-install-addon) in your cluster.
1. Edit the cluster autoscaler configmap and specify the autoscaling parameters that you want to use like `MinSize`, `MaxSize`, and the worker pools that you want to use for scaling.


