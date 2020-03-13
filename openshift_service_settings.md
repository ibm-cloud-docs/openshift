---

copyright:
  years: 2014, 2020
lastupdated: "2020-03-13"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---

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
|------|--------------|
| 4.3 | <ul><li><code>ExpandInUsePersistentVolumes=true</code></li><li><code>NodeDisruptionExclusion=false</code></li><li><code>ServiceNodeExclusion=false</code></li><li><code>SCTPSupport=false</code></li></ul>|
{: summary="The rows are read from left to right. The version is in the first column, with the default feature gates in the second column."}
{: caption="Overview of feature gates" caption-side="top"}