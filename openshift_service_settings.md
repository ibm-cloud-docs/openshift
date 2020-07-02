---

copyright:
  years: 2014, 2020
lastupdated: "2020-07-02"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---

{:beta: .beta}
{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}



# Default service settings for OpenShift components
{: #service-settings}

Review the default settings for OpenShift components in your {{site.data.keyword.openshiftlong}} clusters. 
{: shortdesc}



## Feature gates
{: #feature-gates}

Review the feature gates that are applied to all master and worker node components by default in Red Hat OpenShift on IBM Cloud clusters. These feature gates differ from the ones that are set up in community distributions. The {{site.data.keyword.cloud_notm}} provider version enables OpenShift APIs and features that are at beta. OpenShift alpha features, which are subject to change, are disabled.
{: shortdesc}

| OpenShift version | Default feature gates |
|---|---|
| 4.3 | <ul><li><code>ExpandInUsePersistentVolumes=true</code></li><li><code>NodeDisruptionExclusion=false</code></li><li><code>ServiceNodeExclusion=false</code></li><li><code>SCTPSupport=false</code></li></ul>|
{: caption="Overview of feature gates" caption-side="top"}
{: summary="The rows are read from left to right. The version is in the first column, with the default feature gates in the second column."}



## Global settings
{: #global-settings}

Because Red Hat OpenShift on IBM Cloud is a managed service, many OpenShift Container Platform global settings are set up for you. You can configure some of these global settings, but other global settings you can only review, and any changes are overwritten. For more information, see [Comparison between clusters that run in {{site.data.keyword.cloud_notm}} and standard OCP](/docs/openshift?topic=openshift-cs_ov#ocp_vs_roks). You can also review the control plane components in the [Red Hat OpenShift on IBM Cloud Toolkit](https://github.com/openshift/ibm-roks-toolkit){: external} project on GitHub.
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

