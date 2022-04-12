---

copyright: 
  years: 2014, 2022
lastupdated: "2022-04-12"

keywords: openshift, node scaling, ca, autoscaler

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Preparing {{site.data.keyword.satelliteshort}} clusters for autoscaling
{: #prepare-autoscale-sat}

Before you can use the cluster autoscaler add-on in your {{site.data.keyword.satelliteshort}} cluster, complete the following steps.
{: shortdesc}

Autoscaling on {{site.data.keyword.satelliteshort}} clusters is available in Beta for allowlisted accounts only. You can get added to the allowlist by [opening a case](https://cloud.ibm.com/unifiedsupport/cases/form){: external} with support.
{: beta}

To set up autoscaling, you must complete the following steps.

1. Create a {{site.data.keyword.satelliteshort}} location.
1. Set up the location control plane.
1. Attach hosts for the default worker pool.
1. Create a cluster that uses your {{site.data.keyword.satelliteshort}} hosts.
1. Verify or create the required storage secrets in your cluster.
1. Attach more hosts to your location and create a second worker pool in your cluster.
1. Attach more hosts to your location and leave them unassigned and available for scaling.
1. Install the `cluster-autoscaler` add-on.
1. Edit the autoscaler ConfigMap and enable scaling.

To get started, see [Setting up your location and cluster for autoscaling](#setup-location-cluster-scale-sat).

## Setting up your location and cluster for autoscaling
{: #setup-location-cluster-scale-sat}

1. [Create a location](/docs/satellite?topic=satellite-locations) and set up your control plane.

1. After setting up your control plane, [attach more hosts](/docs/satellite?topic=satellite-attach-hosts) that you want to use in the default worker pool for your cluster.

1. [Create a cluster in your location](/docs/openshift?topic=openshift-satellite-clusters).

1. Verify that the `storage-secret-store` secret exists in the `kube-system` namespace of your cluster.
    ```sh
    oc get secrets -n kube-system | grep storage
    ```
    {: pre}
    
    Example output.
    
    ```sh
    storage-secret-store     Opaque      1      54d
    ```
    {: pre}
    
1. **Optional**: If the `storage-secret-store` secret doesn't exist in your cluster, create it.
    1. Create a file called `slclient.toml` and include your API key. If you have a private-only {{site.data.keyword.satelliteshort}} cluster, you must also include the `satellite-link-route`. You can find the `satellite-link-route` by viewing the Link endpoints for your Location in the [console](https://cloud.ibm.com/satellite/locations){: external}
        ```sh
        [Bluemix]
          iam_api_key = "APIKEY"
          containers_api_route = "satellite-link-route" # private clusters only
        ```
        {: pre}
        
    1. Create a secret by using the `slclient.toml` file.
        ```sh
        oc create secret generic storage-secret-store --from-file=slclient.toml -n kube-system
        ```
        {: pre}

1. Attach more hosts to your location that you want to use in your autoscaled worker pool. As a best practice, don't set up autoscaling on the default worker pool. When you attach the hosts that you want to use in the autoscaled worker pool, be sure specify host labels such as the host `cpu=16` and `memory=64`. Host labels are used by the cluster autoscaler add-on to find hosts that are available for scaling.
    Example command to attach hosts while specifying host labels for CPU and memory.
    ```sh
    ibmcloud sat host attach --location LOCATION --host-label "cpu=16" --host-label "memory=64" [--operating-system SYSTEM] 
    ```
    {: pre}
    
1. Create a second worker pool using the hosts that you attached. For more information see, [Managing {{site.data.keyword.satelliteshort}} worker pools](/docs/openshift?topic=openshift-satellite-clusters#satcluster-worker-pools-sat).

1. Attach more hosts to your location, but do not assign them to a worker pool. These `Ready/Unassigned` hosts are available for autoscaling. When you attach the hosts that you want to leave available for autoscaling, be sure specify host labels such as the host `cpu=16` and `memory=64`. Host labels are used by the cluster autoscaler add-on to find hosts that are available for scaling.
1. Install the cluster [add-on in your cluster](/docs/containers?topic=containers-cluster-scaling-install-addon) in your cluster. Note that if you see an error message `The 'cluster-autoscaler' add-on is not supported on satellite clusters`, your account is not allowlisted to use the add-on. To get added to the allowlist, [open a case](https://cloud.ibm.com/unifiedsupport/cases/form){: external} with support.
1. Edit the cluster autoscaler configmap and specify the autoscaling parameters that you want to use like `MinSize`, `MaxSize`, and the worker pools that you want to use for scaling.

## Understanding autoscaling in {{site.data.keyword.satelliteshort}} clusters
{: #cluster-scaling-sat}

How does scale-up work for {{site.data.keyword.satelliteshort}} clusters?
:   The cluster autoscaler periodically checks for pods that are stuck in pending state due to lack of memory or CPU resources. 
    1. The autoscaler checks whether scaling is enabled on any of the work pools in the cluster, if scaling is enabled, then the autoscaler calculates the required number to worker nodes to accommodate all the pods that are stuck in pending state. If no worker pools have autoscaling enabled, then no action occurs.
    1. The autoscaler compares required worker node count, which was calculated in the previous step, and compares it to the `MaxSize` or total amount worker nodes allowed for scaling. If the `MaxSize` allowed is less than or equal to the required worker node count to satisfy all pods, the autoscaler sends a resize request to the instance group.
    1. The autoscaler fetches the hosts that are `Ready` or `Unassigned` in the location and that have host labels that match the labels on the worker nodes in the worker pool where autoscaling is enabled. 
    1. The autoscaler determines if there are enough available `Ready` or `Unassigned` hosts to satisfy the resize request. 
        * If there are not enough hosts available in the location, then a warning is added to the logs that the resize operation was incomplete.
        * If there are available hosts that are `Ready` or `Unassigned` and have the matching host labels, the autoscaler uses those hosts to fulfill the request.
        * If no hosts are available with the matching host labels, the autoscaler filters the `Ready` or `Unassigned` hosts for those with only the default host labels. Then, the autoscaler updates the labels on those hosts to match the host labels of the worker pool where scaling is enabled and uses these hosts to fulfill the request.

How does scale-down work in {{site.data.keyword.satelliteshort}} clusters?
:   When the cluster autoscaler determines that a worker node is underutilized for the specified `scaleDownUnneededTime` time, then the workers are deleted from the cluster.
:   The hosts where that were used for those worker nodes are then in the `Reload Required` or `Unassigned` state in the location. These hosts can't be used by any other cluster until they are reloaded and re-attached to the location.
