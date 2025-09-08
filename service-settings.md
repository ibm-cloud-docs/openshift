---

copyright: 
  years: 2014, 2025
lastupdated: "2025-09-08"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Default service settings for {{site.data.keyword.redhat_openshift_notm}} components
{: #service-settings}

Review the default settings for {{site.data.keyword.redhat_openshift_notm}} components in your {{site.data.keyword.openshiftlong}} clusters. 
{: shortdesc}



## Feature gates
{: #feature-gates}



Review the feature gates that are applied to all master and worker node components by default in {{site.data.keyword.openshiftlong_notm}} clusters. These feature gates differ from the ones that are set up in community distributions. Most new beta features are disabled by default. {{site.data.keyword.redhat_openshift_notm}} alpha features, (also known as developer or technology preview features) which are subject to change, are disabled. In clusters that run version 4.14 or later, the `oc get featuregate cluster -o yaml` command can be used to view the cluster feature gate specification and status.
{: shortdesc}




Modifying feature gates is not supported in {{site.data.keyword.openshiftlong_notm}}.
{: important}

4.19
:   `KMSv1=false`

4.18
:   `KMSv1=false`
:   `ServiceAccountTokenNodeBinding=true`
:   `StrictCostEnforcementForVAP=true`
:   `StrictCostEnforcementForWebhooks=true`

4.17
:   `KMSv1=false`
:   `StrictCostEnforcementForVAP=true`
:   `StrictCostEnforcementForWebhooks=true`

4.16
:   `KMSv1=false`
:   `StructuredAuthenticationConfiguration=true`

4.15
:   Community feature gates applied.

4.14
:   `RetroactiveDefaultStorageClass=false`

4.13
:   `RetroactiveDefaultStorageClass=false`

4.12
:   Community feature gates applied.

4.11
:   Community feature gates applied. 

4.10
:   `ServiceLBNodePortControl=false`
  
4.9
:   `ServiceLBNodePortControl=false`

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

Because {{site.data.keyword.openshiftlong_notm}} is a managed service, many OpenShift Container Platform global settings are set up for you. You can configure some global settings, but other global settings you can only review, and any changes are overwritten. For more information, see [Comparison between clusters that run in {{site.data.keyword.cloud_notm}} and standard OCP](/docs/openshift?topic=openshift-overview#compare_ocp). You can also review the control plane components in the [{{site.data.keyword.openshiftlong_notm}} Toolkit](https://github.com/openshift/ibm-roks-toolkit){: external} project on GitHub.
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
