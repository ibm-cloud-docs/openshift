---

copyright: 
  years: 2014, 2021
lastupdated: "2021-09-24"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---



{{site.data.keyword.attribute-definition-list}}

# Debugging cluster add-ons
{: #debug_addons}

As you use {{site.data.keyword.openshiftlong}}, consider these techniques for troubleshooting [managed add-ons](/docs/openshift?topic=openshift-managed-addons), such as HPCS Router.
{: shortdesc}

**Infrastructure provider**:
* <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

You can check the health state and status of a cluster add-on by running the following command:
```
ibmcloud oc cluster addon ls -c <cluster_name_or_ID>
```
{: pre}

Example output:
```
Name            Version   Health State   Health Status
debug-tool      2.0.0     normal         Addon Ready
kube-terminal   1.0.0     normal         Addon Ready
```
{: screen}

The **Health State** reflects the lifecycle of the add-on components. The **Health Status** provides details of what add-on operation is in progress. Each state and status is described in the following tables.

|Add-on health state|Description|
|--- |--- |
|`critical`|The add-on is not ready to be used for one of the following reasons:<ul><li>Some or all of the add-on components are unhealthy.</li><li>The add-on failed to deploy.</li><li>The add-on may be at an unsupported version.</li></ul>Check the **Health Status** field for more information.|
|`normal`|The add-on is successfully deployed. Check the status to verify that the add-on is `Ready` or to see if an update is available.|
|`pending`|Some or all components of the add-on are currently deploying. Wait for the state to become `normal` before working with your add-on.|
|`updating`|The add-on is updating and is not ready to be used. Check the **Health Status** field for the version that the add-on is updating to.|
|`warning`|The add-on might not function properly due to cluster limitations. Check the **Health Status** field for more information.|
{: caption="Add-on health states"}
{: summary="Table rows read from left to right, with the add-on state in column one and a description in column two."}

</br>

|Status code|Add-on health status|Description|
|--- |--- |--- |
|H1500|`Addon Ready`|The add-on is successfully deployed and is healthy.|
|H1501, H1502, H1503|`Addon Not Ready`|Some or all of the add-on components are unhealthy. Check whether all add-on component pods are running. <br><br><img src="../images/icon-satellite.svg" alt="{{site.data.keyword.satelliteshort}} infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **{{site.data.keyword.satelliteshort}} clusters**: Also see [Why doesn't my cluster add-on work?](/docs/satellite?topic=satellite-addon-errors).|
|H1504, H1505, H1506, H1507, H1508|`Failure determining health status.`|The add-on health cannot be determined. [Open a support case](/docs/get-support?topic=get-support-using-avatar). In the description, include the error code from the health status.|
|H1509|`Addon Unsupported`|The add-on runs an unsupported version, or the add-on version is unsupported for your cluster version. [Update your add-on to the latest version](/docs/openshift?topic=openshift-managed-addons#updating-managed-add-ons).|
|H1510|`Cluster resources low, not enough workers in Ready state.`|The add-on is not ready to be used for one of the following reasons:<ul><li>The cluster does not meet the size criteria for the add-on. </li><li>Worker nodes in your cluster are not in a <code>Normal</code> state. <a href="/docs/openshift?topic=openshift-debug_worker_nodes">Review the worker nodes' state and status</a>.</li></ul>|
|-|`Enabling`|The add-on is currently deploying to the cluster. Note that the add-on might take up to 15 minutes to install.|
|H1512|`Addon daemonset may not be available on all Ready nodes.`|For the static route add-on: The static route operator `DaemonSet` is not available on any worker nodes, which prevents you from applying static route resources. Your worker nodes cannot run the static route operator `DaemonSet` for the following reasons:<ul><li>One or more worker nodes reached their <a href="/docs/openshift?topic=openshift-debug_worker_nodes">resource limits</a>.</li><li>One or more worker nodes are running the <a href="/docs/openshift?topic=openshift-openshift_limitations#classic_limits">maximum number of pods per worker node</a>.</li></ul>|
{: caption="Add-on health statuses"}
{: summary="Table rows read from left to right, with the add-on status in column one and a description in column two."}




