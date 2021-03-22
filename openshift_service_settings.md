---

copyright:
  years: 2014, 2021
lastupdated: "2021-03-22"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}
 


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
| 4.6 | <ul><li><code>APIPriorityAndFairness=true</code></li><li><code>LegacyNodeRoleBehavior=false</code></li><li><code>SCTPSupport=false</code></li><li><code>ServiceAppProtocol=false</code></li></ul>|
| 4.5 | <ul><li><code>ExperimentalCriticalPodAnnotation=true</code></li><li><code>LocalStorageCapacityIsolation=false</code></li></ul>|
| 4.4 | <ul><li><code>ExperimentalCriticalPodAnnotation=true</code></li><li><code>LocalStorageCapacityIsolation=false</code></li></ul>|
| 4.3 | <ul><li><code>ExperimentalCriticalPodAnnotation=true</code></li><li><code>LocalStorageCapacityIsolation=false</code></li></ul>||
{: caption="Overview of feature gates" caption-side="top"}
{: summary="The rows are read from left to right. The version is in the first column, with the default feature gates in the second column."}



## Global settings
{: #global-settings}

Because {{site.data.keyword.openshiftlong_notm}} is a managed service, many OpenShift Container Platform global settings are set up for you. You can configure some of these global settings, but other global settings you can only review, and any changes are overwritten. For more information, see [Comparison between clusters that run in {{site.data.keyword.cloud_notm}} and standard OCP](/docs/openshift?topic=openshift-cs_ov#compare_ocp). You can also review the control plane components in the [{{site.data.keyword.openshiftlong_notm}} Toolkit](https://github.com/openshift/ibm-roks-toolkit){: external} project on GitHub.
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
