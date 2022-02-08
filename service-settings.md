---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-08"

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



4.8
:   `ServiceLoadBalancerClass=true`
:   `LegacyNodeRoleBehavior=false`
:   `DownwardAPIHugePages=true`

4.7
:   `LegacyNodeRoleBehavior=false`
:   `RemoveSelfLink=false`

4.6
:   `APIPriorityAndFairness=true`
:   `LegacyNodeRoleBehavior=false`
:   `SCTPSupport=false`
:   `ServiceAppProtocol=false`

4.5
:   `ExperimentalCriticalPodAnnotation=true`
:   `LocalStorageCapacityIsolation=false`

4.4
:   `ExperimentalCriticalPodAnnotation=true`
:   `LocalStorageCapacityIsolation=false`

4.3
:   `ExperimentalCriticalPodAnnotation=true`
:   `LocalStorageCapacityIsolation=false`




## Global settings
{: #global-settings}

Because {{site.data.keyword.openshiftlong_notm}} is a managed service, many OpenShift Container Platform global settings are set up for you. You can configure some global settings, but other global settings you can only review, and any changes are overwritten. For more information, see [Comparison between clusters that run in {{site.data.keyword.cloud_notm}} and standard OCP](/docs/openshift?topic=openshift-cs_ov#compare_ocp). You can also review the control plane components in the [{{site.data.keyword.openshiftlong_notm}} Toolkit](https://github.com/openshift/ibm-roks-toolkit){: external} project on GitHub.
{: shortdesc}

Configurable global settings:
* `Image.InternalRegistryHostname`
* `Image.AllowedRegistriesForImport` For an example, see [Adding a private registry to the global pull secret](/docs/openshift?topic=openshift-registry#cluster_global_pull_secret).
* `Build.BuildControllerConfig`
* `Project.RequestMessage`
* `Project.RequestTemplateName`

Read-only custom resource definitions in the `config.openshift.io` resource group:
* `APIServer`
* `Authentication`
* `ClusterVersion`
* `DNS`
* `FeatureGate`
* `Image`
* `Infrastructure`
* `Ingress`
* `Network`
* `OAuth`
* `Proxy`
* `Scheduler`




