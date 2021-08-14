---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-14"

keywords: openshift, openshift data foundation, openshift container storage, storage classes

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
  

# Storage class reference
{: #ocs-sc-ref}

Review the following ODF storage classes.
{: shortdesc}

The ODF storage classes all support dynamic provisioning and are multizone capable.
{: note}

| Feature | Description |
|-----|-----|
| Supported access | rwx |
| Volume mode | File |
| Performance | High |
| Consistency | Strong |
| Resiliency | High |
| Scalability | Multizone |
| Encryption | At rest |
{: caption="Ceph FS storage class details." caption-side="top"}
{: #ocs_sc1}
{: tab-title="ocs-storagecluster-cephfs"}
{: tab-group="sc_ref"}
{: class="simple-tab-table"}
{: summary="The first column contains a feature of the storage class. The second column contains a brief description of the feature."}

| Feature | Description |
|-----|-----|
| Supported access | rwx |
| Volume mode | Block |
| Performance | High |
| Consistency | Strong |
| Resiliency | High |
| Scalability | Multizone |
| Encryption | At rest |
{: caption="Ceph RBD storage class details." caption-side="top"}
{: #ocs_sc2}
{: tab-title="ocs-storagecluster-ceph-rbd"}
{: tab-group="sc_ref"}
{: class="simple-tab-table"}
{: summary="The first column contains a feature of the storage class. The second column contains a brief description of the feature."}

| Feature | Description |
|-----|-----|
| Supported access | rwx |
| Volume mode | s3fs (Cloud Object Storage s3fs plug-in) |
| Performance | High |
| Consistency | Eventual |
| Resiliency | High |
| Scalability | Multizone |
| Encryption | In transit and at rest |
{: caption="Ceph RGW storage class details." caption-side="top"}
{: #ocs_sc3}
{: tab-title="ocs-storagecluster-ceph-rgw"}
{: tab-group="sc_ref"}
{: class="simple-tab-table"}
{: summary="The first column contains a feature of the storage class. The second column contains a brief description of the feature."}








