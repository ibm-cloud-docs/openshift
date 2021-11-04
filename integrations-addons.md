---

copyright: 
  years: 2014, 2021
lastupdated: "2021-11-04"

keywords: kubernetes, openshift, roks, rhoks, rhos

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Adding services by using managed add-ons
{: #managed-addons}

Quickly add extra capabilities and open-source technologies to your cluster with managed add-ons.
{: shortdesc}

**What are managed add-ons?**

Managed {{site.data.keyword.openshiftlong_notm}} add-ons are an easy way to enhance your cluster with extra capabilities and open-source capabilities, such asthe Diagnostics and Debug Tool, {{site.data.keyword.block_storage_is_short}}, or the Cluster Autoscaler. The version of the driver, plug-in, or open-source tool that you add to your cluster is tested by IBM and approved to be used in {{site.data.keyword.openshiftlong_notm}}.

The managed add-ons that you can install in your cluster depend on the type of cluster, the container platform, and the infrastructure provider that you choose.
{: note}

**How does the billing and support work for managed add-ons?**

Managed add-ons are fully integrated into the {{site.data.keyword.cloud_notm}} support organization. If you have a question or an issue with using the managed add-ons, you can use one of the {{site.data.keyword.openshiftlong_notm}} support channels. For more information, see [Getting help and support](/docs/containers?topic=containers-get-help).

If the tool that you add to your cluster incurs costs, these costs are automatically integrated and listed as part of your {{site.data.keyword.openshiftlong_notm}} billing. The billing cycle is determined by {{site.data.keyword.cloud_notm}} depending on when you enabled the add-on in your cluster.

**What limitations do I need to account for?**

If you installed an admission controller that blocks unsigned images, such as [Portieris](/docs/openshift?topic=openshift-images#portieris-image-sec), you cannot enable managed add-ons in your cluster.

## Adding managed add-ons
{: #adding-managed-add-ons}

To enable a managed add-on in your cluster from the CLI, use the [`ibmcloud oc cluster addon enable` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable). To enable a managed add-on in your cluster in the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, use the **Add-ons** pane of the cluster details page. When you enable the managed add-on, a supported version of the tool, including all Kubernetes resources are automatically installed in your cluster. Refer to the documentation of each managed add-on to find the prerequisites that your cluster must meet to install the managed add-on.

For more information about the prerequisites for each add-on, see:
- [{{site.data.keyword.block_storage_is_short}}](/docs/containers?topic=containers-vpc-block)
- [Cluster Autoscaler](/docs/openshift?topic=openshift-ca)
- [Diagnostics and Debug Tool](/docs/containers?topic=containers-debug-tool)
- [HPCS Router](/docs/openshift?topic=openshift-hpcs-router)
- [Image Key Synchronizer](/docs/openshift?topic=openshift-images#encrypted-images)
- [OpenShift Data Foundation](/docs/openshift?topic=openshift-deploy-odf-vpc)
- [Static routes](/docs/containers?topic=containers-static-routes)

## Updating managed add-ons
{: #updating-managed-add-ons}

The versions of each managed add-on are tested by {{site.data.keyword.cloud_notm}} and approved for use in {{site.data.keyword.openshiftlong_notm}}. To update the components of an add-on to the most recent version supported by {{site.data.keyword.openshiftlong_notm}}, use the following steps.
{: shortdesc}

1. Check for update instructions that are specific to your managed add-on. If you do not find update instructions, continue with the next step.
2. If your add-on does not have specific update instructions, select the cluster where you installed managed add-ons from your [cluster dashboard](https://cloud.ibm.com/kubernetes/clusters).
3. Select the **Add-ons** tab.
4. From the actions menu, select **Update** to start updating the managed add-on. When the update is installed, the latest version of the managed add-on is listed on the cluster add-on page.



## Reviewing add-on states and statuses
{: #debug_addons_review}

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

The **Health State** reflects the lifecycle of the add-on components. The **Health Status** provides details of what add-on operation is in progress. Each state and status is described in the following tables.

|Add-on health state|Description|
|--- |--- |
|`critical`|The add-on is not ready to be used for one of the following reasons:  \n - Some or all of the add-on components are unhealthy.  \n - The add-on failed to deploy.  \n - The add-on may be at an unsupported version.  \n - Check the **Health Status** field for more information.|
|`normal`|The add-on is successfully deployed. Check the status to verify that the add-on is `Ready` or to see if an update is available.|
|`pending`|Some or all components of the add-on are currently deploying. Wait for the state to become `normal` before working with your add-on.|
|`updating`|The add-on is updating and is not ready to be used. Check the **Health Status** field for the version that the add-on is updating to.|
|`warning`|The add-on might not function properly due to cluster limitations. Check the **Health Status** field for more information.|
{: caption="Add-on health states"}
{: summary="Table rows read from left to right, with the add-on state in column one and a description in column two."}





|Status code|Add-on health status|Description|
|--- |--- |--- |
|H1500|`Addon Ready`|The add-on is successfully deployed and is healthy.|
|H1501, H1502, H1503|`Addon Not Ready`|Some or all of the add-on components are unhealthy. Check whether all add-on component pods are running.  <img src="images/icon-satellite.svg" alt="{{site.data.keyword.satelliteshort}} infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **{{site.data.keyword.satelliteshort}} clusters**: Also see [Why doesn't my cluster add-on work?](/docs/satellite?topic=satellite-addon-errors).|
|H1504, H1505, H1506, H1507, H1508|`Failure determining health status.`|The add-on health cannot be determined. [Open a support case](/docs/get-support?topic=get-support-using-avatar). In the description, include the error code from the health status.|
|H1509|`Addon Unsupported`|The add-on runs an unsupported version, or the add-on version is unsupported for your cluster version. [Update your add-on to the latest version](/docs/openshift?topic=openshift-managed-addons#updating-managed-add-ons).|
|H1510|`Cluster resources low, not enough workers in Ready state.`|The add-on is not ready to be used for one of the following reasons:  \n - The cluster does not meet the size criteria for the add-on.  \n - Worker nodes in your cluster are not in a `Normal` state. [Review the worker nodes' state and status](/docs/containers?topic=containers-debug_worker_nodes). |
|\-|`Enabling`|The add-on is currently deploying to the cluster. Note that the add-on might take up to 15 minutes to install.|
|H1512|`Addon daemonset may not be available on all Ready nodes.`|For the static route add-on: The static route operator `DaemonSet` is not available on any worker nodes, which prevents you from applying static route resources. Your worker nodes cannot run the static route operator `DaemonSet` for the following reasons:  \n - One or more worker nodes reached their [resource limits](/docs/containers?topic=containers-debug_worker_nodes).  \n - One or more worker nodes are running the [maximum number of pods per worker node](/docs/openshift?topic=openshift-openshift_limitations#classic_limits).|
{: caption="Add-on health statuses"}
{: summary="Table rows read from left to right, with the add-on status in column one and a description in column two."}







## Supported add-ons for clusters in {{site.data.keyword.satelliteshort}} locations
{: #addons-satellite}

Review which managed add-ons are available for {{site.data.keyword.openshiftshort}} clusters that are created in an {{site.data.keyword.satellitelong_notm}} location.
{: shortdesc}

Supported add-ons for clusters in {{site.data.keyword.satelliteshort}} locations:
- [Diagnostics and Debug Tool](/docs/containers?topic=containers-debug-tool)
- [HPCS Router](/docs/openshift?topic=openshift-hpcs-router)
- [Image Key Synchronizer](/docs/openshift?topic=openshift-images#encrypted-images)
- **Deprecated**: [Kubernetes web terminal](/docs/containers?topic=containers-cs_cli_install#cli_web)
- [OpenShift Data Foundation](/docs/openshift?topic=openshift-deploy-odf-vpc) (However, you can also use [{{site.data.keyword.satelliteshort}} storage templates](/docs/satellite?topic=satellite-config-storage-ocs-local) to consistently deploy ODF across clusters in your location.)
- [Static routes](/docs/containers?topic=containers-static-routes)

Unsupported add-ons for clusters in {{site.data.keyword.satelliteshort}} locations:
- [ALB OAuth Proxy](/docs/containers?topic=containers-comm-ingress-annotations#app-id)
- [Cluster Autoscaler](/docs/openshift?topic=openshift-ca)
- [Istio](/docs/containers?topic=containers-istio)
- [{{site.data.keyword.block_storage_is_short}}](/docs/containers?topic=containers-vpc-block)






