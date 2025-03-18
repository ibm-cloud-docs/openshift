---

copyright: 
  years: 2014, 2025
lastupdated: "2025-03-18"


keywords: kubernetes, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Adding services by using managed add-ons
{: #managed-addons}

Managed {{site.data.keyword.openshiftlong_notm}} add-ons are an easy way to enhance your cluster with extra capabilities and open-source capabilities, such as the Diagnostics and Debug Tool, {{site.data.keyword.block_storage_is_short}}, or the Cluster Autoscaler. The version of the driver, plug-in, or open-source tool that you add to your cluster is tested by IBM and approved to be used in {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

The managed add-ons that you can install in your cluster depend on the type of cluster, the container platform, and the infrastructure provider that you choose.
{: note}

Support
:    Managed add-ons are fully integrated into the {{site.data.keyword.cloud_notm}} support organization. If you have a question or an issue with using the managed add-ons, you can use one of the {{site.data.keyword.openshiftlong_notm}} support channels. For more information, see [Getting help and support](/docs/openshift?topic=openshift-get-help).

Billing
:    If the tool that you add to your cluster incurs costs, these costs are automatically integrated and listed as part of your {{site.data.keyword.openshiftlong_notm}} billing. The billing cycle is determined by {{site.data.keyword.cloud_notm}} depending on when you enabled the add-on in your cluster.

:    In general, no additional setup, such as opening ports or IP addresses is required. However, refer to the documentation of each managed add-on to find the prerequisites that your cluster must meet before you install the managed add-on.

## Adding managed add-ons
{: #adding-managed-add-ons}

To enable a managed add-on in your cluster from the CLI, use the [`ibmcloud oc cluster addon enable` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable). To enable a managed add-on in your cluster in the [console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}, use the **Add-ons** pane of the cluster details page. When you enable the managed add-on, a supported version of the tool, including all Kubernetes resources are automatically installed in your cluster. Refer to the documentation of each managed add-on to find the prerequisites that your cluster must meet before you install the managed add-on.

For more information about the prerequisites for each add-on, see:
- [{{site.data.keyword.block_storage_is_short}}](/docs/openshift?topic=openshift-vpc-block)
- [Cluster Autoscaler](/docs/openshift?topic=openshift-cluster-scaling-install-addon)
- [Diagnostics and Debug Tool](/docs/openshift?topic=openshift-debug-tool)
- [HPCS Router](/docs/openshift?topic=openshift-hpcs-router-changelog)
- [Image Key Synchronizer](/docs/openshift?topic=openshift-images#encrypted-images)
- [OpenShift Data Foundation](/docs/openshift?topic=openshift-deploy-odf-vpc)
- [Static routes](/docs/openshift?topic=openshift-static-routes)

## Updating managed add-ons
{: #updating-managed-add-ons}

The versions of each managed add-on are tested by {{site.data.keyword.cloud_notm}} and approved for use in {{site.data.keyword.openshiftlong_notm}}. To update the components of an add-on to the most recent version supported by {{site.data.keyword.openshiftlong_notm}}, use the following steps.
{: shortdesc}
    
Review the following links for specific update steps for each add-on.
- [{{site.data.keyword.block_storage_is_short}}](/docs/openshift?topic=openshift-vpc-block#vpc-addon-update)
- [Cluster Autoscaler](/docs/openshift?topic=openshift-cluster-scaling-install-addon#cluster-scaling-install-addon-update-addon)
- [HPCS Router](/docs/openshift?topic=openshift-hpcs-router-changelog)
- [OpenShift Data Foundation](/docs/openshift?topic=openshift-ocs-manage-deployment)
   


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
```
{: screen}

The **Health State** reflects the lifecycle of the add-on components. Each state is described in the following table.

|Add-on health state|Description|
|--- |--- |
|`critical`|The add-on is not ready to be used for one of the following reasons:  \n - Some or all the add-on components are unhealthy.  \n - The add-on failed to deploy.  \n - The add-on might be at an unsupported version.  \n - Check the **Health Status** field for more information.|
|`normal`|The add-on is successfully deployed. Check the status to verify that the add-on is `Ready` or to see if an update is available.|
|`pending`|Some or all components of the add-on are currently deploying. Wait for the state to become `normal` before working with your add-on.|
|`updating`|The add-on is updating and is not ready to be used. Check the **Health Status** field for the version that the add-on is updating to.|
|`warning`|The add-on might not function properly due to cluster limitations. Check the **Health Status** field for more information.|
{: caption="Add-on health states"}


The **Health Status** provides details of what add-on operation is in progress. Each status is described in the following table.


|Status code|Add-on health status|Description|
|--- |--- |--- |
|H1500|`Addon Ready`|The add-on is successfully deployed and is healthy.|
|H1501, H1502, H1503|`Addon Not Ready`|Some or all the add-on components are unhealthy. Check whether all add-on component pods are running. \n - **{{site.data.keyword.satelliteshort}} clusters**: Also see [Why doesn't my cluster add-on work?](/docs/satellite?topic=satellite-addon-errors).\n  |
|H1504, H1505, H1506, H1507, H1508|`Failure determining health status.`|The add-on health can't be determined. [Open a support case](/docs/account?topic=account-using-avatar). In the description, include the error code from the health status.|
|H1509|`Addon Unsupported`|The add-on runs an unsupported version, or the add-on version is unsupported for your cluster version. [Update your add-on to the latest version](/docs/containers?topic=containers-managed-addons#updating-managed-add-ons).|
|H1510|`Cluster resources low, not enough workers in Ready state.`|The add-on is not ready to be used for one of the following reasons:  \n - The cluster does not meet the size criteria for the add-on.  \n - Worker nodes in your cluster are not in a `Normal` state. [Review the worker nodes' state and status](/docs/containers?topic=containers-debug_worker_nodes). |
|\-|`Enabling`|The add-on is currently deploying to the cluster. Note that the add-on might take up to 15 minutes to install.|
|H1512|`Addon daemonset might not be available on all Ready nodes.`|For the static route add-on: The static route operator `DaemonSet` is not available on any worker nodes, which prevents you from applying static route resources. Your worker nodes can't run the static route operator `DaemonSet` for the following reasons:  \n - One or more worker nodes reached their [resource limits](/docs/containers?topic=containers-debug_worker_nodes).  \n - One or more worker nodes are running the [maximum number of pods per worker node](/docs/openshift?topic=openshift-limitations#classic_limits).|
{: caption="Add-on health statuses"}





## Supported add-ons for clusters in {{site.data.keyword.satelliteshort}} locations
{: #addons-satellite}

Review which managed add-ons are available for {{site.data.keyword.redhat_openshift_notm}} clusters that are created in an {{site.data.keyword.satellitelong_notm}} location.
{: shortdesc}

The following list of add-ons for clusters are supported in {{site.data.keyword.satelliteshort}} locations.

- [Diagnostics and Debug Tool](/docs/openshift?topic=openshift-debug-tool)
- [HPCS Router](/docs/openshift?topic=openshift-hpcs-router-changelog)
- [Image Key Synchronizer](/docs/openshift?topic=openshift-images#encrypted-images)
- **Deprecated**: [Kubernetes web terminal](/docs/openshift?topic=openshift-cli-install)
- [OpenShift Data Foundation](/docs/openshift?topic=openshift-deploy-odf-vpc) (However, you can also use [{{site.data.keyword.satelliteshort}} storage templates](/docs/satellite?topic=satellite-storage-odf-local) to consistently deploy ODF across clusters in your location.)
- [Static routes](/docs/openshift?topic=openshift-static-routes)

The following list of add-ons for clusters are unsupported in {{site.data.keyword.satelliteshort}} locations.

- [ALB OAuth Proxy](/docs/containers?topic=containers-comm-ingress-annotations#app-id-auth)
- [Cluster Autoscaler](/docs/openshift?topic=openshift-cluster-scaling-install-addon)
- [Istio](/docs/containers?topic=containers-istio)
- [{{site.data.keyword.block_storage_is_short}}](/docs/openshift?topic=openshift-vpc-block)
