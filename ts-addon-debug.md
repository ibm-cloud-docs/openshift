---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-07"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Debugging cluster add-ons
{: #debug_addons}
{: support}

As you use {{site.data.keyword.openshiftlong}}, consider these techniques for troubleshooting [managed add-ons](/docs/containers?topic=containers-managed-addons), such as HPCS Router.
{: shortdesc}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

You can check the health state and status of a cluster add-on by running the following command.

```sh
ibmcloud oc cluster addon ls -c <cluster_name_or_ID>
```
{: pre}

Example output
```sh
Name            Version   Health State   Health Status
debug-tool      2.0.0     normal         Addon Ready
kube-terminal   1.0.0     normal         Addon Ready
```
{: screen}

The **Health State** reflects the lifecycle of the add-on components. Each state is described in the following table.

|Add-on health state|Description|
|--- |--- |
|`critical`|The add-on is not ready to be used for one of the following reasons:  \n - Some or all the add-on components are unhealthy.  \n - The add-on failed to deploy.  \n - The add-on may be at an unsupported version.  \n - Check the **Health Status** field for more information.|
|`normal`|The add-on is successfully deployed. Check the status to verify that the add-on is `Ready` or to see if an update is available.|
|`pending`|Some or all components of the add-on are currently deploying. Wait for the state to become `normal` before working with your add-on.|
|`updating`|The add-on is updating and is not ready to be used. Check the **Health Status** field for the version that the add-on is updating to.|
|`warning`|The add-on might not function properly due to cluster limitations. Check the **Health Status** field for more information.|
{: caption="Add-on health states"}


The **Health Status** provides details of what add-on operation is in progress. Each status is described in the following table.


|Status code|Add-on health status|Description|
|--- |--- |--- |
|H1500|`Addon Ready`|The add-on is successfully deployed and is healthy.|
|H1501, H1502, H1503|`Addon Not Ready`|Some or all the add-on components are unhealthy. Check whether all add-on component pods are running.  <img src="images/icon-satellite.svg" alt="{{site.data.keyword.satelliteshort}} infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **{{site.data.keyword.satelliteshort}} clusters**: Also see [Why doesn't my cluster add-on work?](/docs/satellite?topic=satellite-addon-errors).|
|H1504, H1505, H1506, H1507, H1508|`Failure determining health status.`|The add-on health can't be determined. [Open a support case](/docs/get-support?topic=get-support-using-avatar). In the description, include the error code from the health status.|
|H1509|`Addon Unsupported`|The add-on runs an unsupported version, or the add-on version is unsupported for your cluster version. [Update your add-on to the latest version](/docs/openshift?topic=openshift-managed-addons#updating-managed-add-ons).|
|H1510|`Cluster resources low, not enough workers in Ready state.`|The add-on is not ready to be used for one of the following reasons:  \n - The cluster does not meet the size criteria for the add-on.  \n - Worker nodes in your cluster are not in a `Normal` state. [Review the worker nodes' state and status](/docs/containers?topic=containers-debug_worker_nodes). |
|\-|`Enabling`|The add-on is currently deploying to the cluster. Note that the add-on might take up to 15 minutes to install.|
|H1512|`Addon daemonset may not be available on all Ready nodes.`|For the static route add-on: The static route operator `DaemonSet` is not available on any worker nodes, which prevents you from applying static route resources. Your worker nodes can't run the static route operator `DaemonSet` for the following reasons:  \n - One or more worker nodes reached their [resource limits](/docs/containers?topic=containers-debug_worker_nodes).  \n - One or more worker nodes are running the [maximum number of pods per worker node](/docs/openshift?topic=openshift-openshift_limitations#classic_limits).|
{: caption="Add-on health statuses"}






