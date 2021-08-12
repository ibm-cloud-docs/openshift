---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-12"

keywords: odf, openshift data foundation add-on, changelog

subcollection: openshift, container storage

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
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
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
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:note:.deprecated}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
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
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
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

 
  

# OpenShift Data Foundation add-on changelog
{: #odf_addon_changelog}

View information for updates to the OpenShift Data Foundation add-on in your {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

Note that the add-on supports`n+1` cluster versions.
{: note}

As of 10 July 2021, version `0.0.2` of the OpenShift Container Storage add-on is deprecated and becomes unsupported on 24 July 2021. Add-on versions `4.6.0` and `4.7.0` are now available. If you have version `0.0.2` of the add-on installed in your cluster, update the add-on to a supported version. The OpenShift Container Storage add-on supports n+1 cluster versions. If you have a 4.6 cluster, update to add-on version `4.6.0` or `4.7.0`. If you have a 4.7 cluster, update to add-on version `4.7.0`.
{: important}

To view a list of add-ons and the supported {{site.data.keyword.openshiftshort}} versions, run the following command.
```sh
ibmcloud oc cluster addon versions --addon openshift-container-storage
```
{: pre}

Refer to the following table for a summary of changes for each version of the [OpenShift Data Foundation} add-on](/docs/openshift?topic=openshift-deploy-odf-vpc).

Refer to the following tables for a summary of changes for each version of the [OpenShift Data Foundation} add-on.

| OpenShift Data Foundation add-on | Is default? | Supported? | {{site.data.keyword.openshiftshort}} version support |
| --- | --- | --- | --- |
| 4.7.0 | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | 4.7 |
| 4.6.0 | | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | 4.6 |
{: caption="Add-on versions" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the add-on version. The second column indicates the default version. The third column is the version's supported state. The fourth column is the {{site.data.keyword.openshiftshort}} version of your cluster that the add-on version is supported for."}


