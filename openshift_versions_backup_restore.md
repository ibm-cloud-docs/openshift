---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-13"

keywords: back up, restore, changelog, roks, openshift

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
  

# Back up and restore Helm chart 
{: #backup_restore_changelog}

View information for updates to the back up and restore Helm chart in your {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

Refer to the following tables for a summary of changes for each version of the [back up and restore Helm chart](/docs/openshift?topic=openshift-utilities#ibmcloud-backup-restore).

| `ibmcloud-backup-restore` Helm chart version | Supported? | {{site.data.keyword.openshiftshort}} version support |
| -------------------- | -----------|--------------------------- |
| 2.0.5 | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | {{site.data.keyword.openshiftshort}} 4.3 - 4.6 |
{: caption="Back up and restore Helm chart versions" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the back up and restore Helm chart version. The second column is the version's supported state. The third column is the {{site.data.keyword.openshiftshort}} version of your cluster that the back up and restore Helm chart version is supported for."}

<br />

## Changelog for 1.0.5
{: #0105_br_chart}

The following table shows the changes that are included in version 1.0.5 of the `ibmcloud-backup-restore` Helm chart.
{: shortdesc}


| Version | Image tag | Release date | Supported {{site.data.keyword.openshiftshort}} versions | Description |
| --- | --- | --- | --- | --- |
| `1.0.5` | `v100` | 17 December 2020 | 4.3 - 4.6 | Updates in this release:<ul><li>Images are now signed.</li><li>The <code>ibmcloud-backup-restore</code> Helm chart now pulls the universal base image (UBI) from the proxy image registry.</li><li>Resources that are deployed by the <code>ibmcloud-backup-restore</code> Helm chart are now linked with the corresponding source code and build URLs.</li></ul> |
{: row-headers}
{: class="comparison-table"}
{: caption="Back up and restore Helm chart version 1.0.5" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the version of the component. The second column lists the images tags of the component. The third column contains the release date of the component. The fourth column contains the supported cluster versions. The fifth column contains a brief description of the change made to the component."}



