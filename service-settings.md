---

copyright: 
  years: 2014, 2021
lastupdated: "2021-12-06"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Default service settings for {{site.data.keyword.openshiftshort}} components
{: #service-settings}

Review the default settings for {{site.data.keyword.openshiftshort}} components in your {{site.data.keyword.openshiftlong}} clusters. 
{: shortdesc}



## Feature gates
{: #feature-gates}

Review the feature gates that are applied to all master and worker node components by default in {{site.data.keyword.openshiftlong_notm}} clusters. These feature gates differ from the ones that are set up in community distributions. The {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.openshiftshort}} APIs and features that are at beta. {{site.data.keyword.openshiftshort}} alpha features, which are subject to change, are disabled.
{: shortdesc}

| {{site.data.keyword.openshiftshort}} version | Default feature gates |
|---|---|
| 4.8 | <ul><li><code>LegacyNodeRoleBehavior=false</code></li><li><code>DownwardAPIHugePages=true</code></li></ul>|
| 4.7 | <ul><li><code>LegacyNodeRoleBehavior=false</code></li><li><code>RemoveSelfLink=false</code></li></ul>|
| 4.6 | <ul><li><code>APIPriorityAndFairness=true</code></li><li><code>LegacyNodeRoleBehavior=false</code></li><li><code>SCTPSupport=false</code></li><li><code>ServiceAppProtocol=false</code></li></ul>|
| 4.5 | <ul><li><code>ExperimentalCriticalPodAnnotation=true</code></li><li><code>LocalStorageCapacityIsolation=false</code></li></ul>|
| 4.4 | <ul><li><code>ExperimentalCriticalPodAnnotation=true</code></li><li><code>LocalStorageCapacityIsolation=false</code></li></ul>|
| 4.3 | <ul><li><code>ExperimentalCriticalPodAnnotation=true</code></li><li><code>LocalStorageCapacityIsolation=false</code></li></ul>|
| 1.22 | <ul><li><code>ServiceLBNodePortControl=false</code></li><li><code>CustomCPUCFSQuotaPeriod=true</code></li><li><code>IPv6DualStack=false</code></li></ul>
| 1.21 | <ul><li><code>CustomCPUCFSQuotaPeriod=true</code></li><li><code>IPv6DualStack=false</code></li></ul>|
| 1.20 | <ul><li><code>AllowInsecureBackendProxy=false</code></li><li><code>CustomCPUCFSQuotaPeriod=true</code></li></ul>|
| 1.19 | <ul><li><code>RuntimeClass=false</code></li><li><code>CustomCPUCFSQuotaPeriod=true</code></li><li><code>AllowInsecureBackendProxy=false</code></li><li><code>SCTPSupport=false</code></li><li><code>ServiceAppProtocol=false</code></li></ul>|
| 1.18 | <ul><li><code>RuntimeClass=false</code></li><li><code>CustomCPUCFSQuotaPeriod=true</code></li><li><code>AllowInsecureBackendProxy=false</code></li></ul>|
{: caption="Overview of feature gates" caption-side="top"}
{: summary="The rows are read from left to right. The version is in the first column, with the default feature gates in the second column."}





## Global settings
{: #global-settings}

Because {{site.data.keyword.openshiftlong_notm}} is a managed service, many OpenShift Container Platform global settings are set up for you. You can configure somese global settings, but other global settings you can only review, and any changes are overwritten. For more information, see [Comparison between clusters that run in {{site.data.keyword.cloud_notm}} and standard OCP](/docs/openshift?topic=openshift-cs_ov#compare_ocp). You can also review the control plane components in the [{{site.data.keyword.openshiftlong_notm}} Toolkit](https://github.com/openshift/ibm-roks-toolkit){: external} project on GitHub.
{: shortdesc}

**Configurable global settings**:
*   `Image.InternalRegistryHostname`
*   `Image.AllowedRegistriesForImport` (for an example, see [Adding a private registry to the global pull secret](/docs/openshift?topic=openshift-registry#cluster_global_pull_secret))
*   `Build.BuildControllerConfig`
*   `Project.RequestMessage`
*   `Project.RequestTemplateName`

**Read-only custom resource definitions in the `config.openshift.io` resource group**:
*   `APIServer`
*   `Authentication`
*   `ClusterVersion`
*   `DNS`
*   `FeatureGate`
*   `Image`
*   `Infrastructure`
*   `Ingress`
*   `Network`
*   `OAuth`
*   `Proxy`
*   `Scheduler`





