---

copyright:
  years: 2014, 2021
lastupdated: "2021-06-03"

keywords: object storage, plug-in, changelog

subcollection: openshift, object storage

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
{:terraform: .ph data-hd-interface='terraform'}
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
  
  

# Object storage plug-in 
{: #cos_plugin_changelog}

View information for updates to the {{site.data.keyword.cos_full_notm}} plug-in in your {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

With version 2.1.0, a new version of the `ibmc` plug-in is included. To update the `ibmc` plugin, uninstall and re-install the {{site.data.keyword.cos_full_notm}} plugin. For more information, see [Updating the {{site.data.keyword.cos_full_notm}}](/docs/openshift?topic=openshift-object_storage#update_cos_plugin) plug-in.
{: note}

With version 2.0.9, there is a new version of the `ibmc` plug-in. Storage classes created with earlier chart versions are immutable and cannot be upgraded. To remove the storage classes from previous versions and install the latest storage classes in your cluster, uninstall and re-install the {{site.data.keyword.cos_full_notm}} plugin. For more information, see [Updating the {{site.data.keyword.cos_full_notm}}](/docs/openshift?topic=openshift-object_storage#update_cos_plugin).
{: note}

Refer to the following tables for a summary of changes for each version of the [Object Storage plug-in](/docs/openshift?topic=openshift-object_storage).

| Object Storage plug-in version | Supported? | {{site.data.keyword.openshiftshort}} version support |
| -------------------- | -----------|--------------------------- |
| 2.1.1 | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | {{site.data.keyword.openshiftshort}} 4.3 - 4.6 |
| 2.1.0 | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | {{site.data.keyword.openshiftshort}} 4.3 - 4.6 |
| 2.0.9 | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | {{site.data.keyword.openshiftshort}} 4.3 - 4.6 |
| 2.0.8 | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | {{site.data.keyword.openshiftshort}} 4.3 - 4.6 |
| 2.0.7 | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | {{site.data.keyword.openshiftshort}} 4.3 - 4.6 |
| 2.0.6 | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | {{site.data.keyword.openshiftshort}} 4.3 - 4.6 |
| 2.0.5 | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | {{site.data.keyword.openshiftshort}} 4.3 - 4.6 |
{: caption="Object Storage plug-in versions" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the Object Storage plug-in version. The second column is the version's supported state. The third column is the {{site.data.keyword.openshiftshort}} version of your cluster that the Object Storage plug-in version is supported for."}


## Changelog for version 2.1.1
{: #0211_object_plugin}

| Version | Image tags | Release date | Description |
| --- | --- | --- | --- |
| `2.1.1` | `1.8.29` | 03 June 2021 | Updates in this version: <ul><li>Fixes an upgrade issue in version `2.1.0`.</li><li>Includes a new version of the `helm ibmc` plug-in. For more information, see [Updating the {{site.data.keyword.cos_full_notm}}](/docs/openshift?topic=openshift-object_storage#update_cos_plugin) plug-in.</li><li>Users can now specify `default` in PVC configurations to use the default TLS cipher suite when a connection to {{site.data.keyword.cos_full_notm}} is established via the HTTPS endpoint. If your worker nodes run an Ubuntu operating system, your storage classes are set up to use the `AESGCM` cipher suite by default. For worker nodes that run a Red Hat operating system, the `ecdhe_rsa_aes_128_gcm_sha_256` cipher suite is used by default. For more information, see [Adding object storage to apps](/docs/openshift?topic=openshift-object_storage#add_cos).</li><li>Fixes [CVE-2020-28851](https://nvd.nist.gov/vuln/detail/CVE-2020-28851){: external}.</li></ul> |
{: row-headers}
{: class="comparison-table"}
{: caption="Object Storage plug-in version 2.1.1" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the version of the component. The second column contains image tag. The third column contains the release date of the component. The fourth column contains a brief description of the change made to the component."}

## Changelog for version 2.1.0
{: #0210_object_plugin}

| Version | Image tags | Release date | Description |
| --- | --- | --- | --- |
| `2.1.0` | `1.8.28` | 26 May 2021 | Updates the UBI to `8.4-200`. |
{: row-headers}
{: class="comparison-table"}
{: caption="Object Storage plug-in version 2.1.0" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the version of the component. The second column contains image tag. The third column contains the release date of the component. The fourth column contains a brief description of the change made to the component."}

## Changelog for version 2.0.9
{: #0209_object_plugin}

| Version | Image tags | Release date | Description |
| --- | --- | --- | --- |
| `2.0.9` | `1.8.27` | 10 May 2021 | Updates in this version: <ul><li>Updates the UBI to `8.3-298.1618432845`.</li><li>Replaces the Flex storage classes with Smart Tier storage classes.</li><li>Fixes [CVE-2021-20305](https://nvd.nist.gov/vuln/detail/CVE-2021-20305){: external}.</li><li>Updates IAM Endpoints.</li><li>Updates the `object-store-endpoint`.</li><li>Fixes a PVC mount issue in private-only VPC clusters.</li><li>Updates the `ResourceConfiguration` endpoint.</li></ul> |
{: row-headers}
{: class="comparison-table"}
{: caption="Object Storage plug-in version 2.0.9" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the version of the component. The second column contains image tag. The third column contains the release date of the component. The fourth column contains a brief description of the change made to the component."}

## Changelog for version 2.0.8
{: #0208_object_plugin}
| Version | Image tags | Release date | Description |
| --- | --- | --- | --- |
| `2.0.8` | `1.8.25` | 19 April 2021 | Updates in this version: <ul><li>Updates the Go version to `1.15.9`.</li><li>Updates the UBI from `ubi-minimal:8.3-291` to `ubi-minimal:8.3-298`.</li><li>Fixes [CVE-2021-3449](https://nvd.nist.gov/vuln/detail/CVE-2021-3449){: external}, [CVE-2021-3450](https://nvd.nist.gov/vuln/detail/CVE-2021-3450){: external}, [CVE-2021-27919](https://nvd.nist.gov/vuln/detail/CVE-2021-27919){: external}, and [CVE-2021-27918](https://nvd.nist.gov/vuln/detail/CVE-2021-27918){: external}.</li></ul> |
{: row-headers}
{: class="comparison-table"}
{: caption="Object Storage plug-in version 2.0.8" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the version of the component. The second column contains image tag. The third column contains the release date of the component. The fourth column contains a brief description of the change made to the component."}


## Changelog for version 2.0.7
{: #0207_object_plugin}
| Version | Image tags | Release date | Description |
| --- | --- | --- | --- |
| `2.0.7` | `1.8.24` | 26 March 2021 | Updates in this version: <ul><li>Updates the Go version to `1.15.8`.</li><li>The plug-in now uses a universal base image (UBI).</li><li>Fixes for [CVE-2021-3114](https://nvd.nist.gov/vuln/detail/CVE-2021-3114){: external}, [CVE-2021-3115](https://nvd.nist.gov/vuln/detail/CVE-2021-3115){: external}, [CVE-2020-28852](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28852){: external}, and [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}.</li></ul> |
{: row-headers}
{: class="comparison-table"}
{: caption="Object Storage plug-in version 2.0.7" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the version of the component. The second column contains image tag. The third column contains the release date of the component. The fourth column contains a brief description of the change made to the component."}

## Changelog for version 2.0.6
{: #0206_object_plugin}

| Version | Image tags | Release date | Description |
| --- | --- | --- | --- |
| `2.0.6` | `1.8.23` | 18 December 2020 | Updates in this version: <ul><li>The `1.8.23` image is signed.</li><li>Updates the Go version to `1.15.5`.</li><li>Fixes `CVE-2020-28362`, `CVE-2020-28367`, and `CVE-2020-28366`.</li><li>Resources that are deployed by the Object Storage plug-in are now linked with the corresponding source code and build URLs.</li><li>The Object Storage plug-in now pulls the universal base image (UBI) from the proxy image registry.</li></ul> |
{: row-headers}
{: class="comparison-table"}
{: caption="Object Storage plug-in version 2.0.6" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the version of the component. The second column contains image tag. The third column contains the release date of the component. The fourth column contains a brief description of the change made to the component."}


<br />
## Changelog for version 2.0.5
{: #0205_object_plugin}

The following table shows the changes that are included in version 2.0.5 of the Object Storage plug-in.
{: shortdesc}

| Version | Release date | Description |
| --- | --- | --- |
| `2.0.5` | 25 November 2020 | Fixes a `NilPointer` error and the following CVEs: `CVE-2018-20843`, `CVE-2019-13050`, `CVE-2019-13627`, `CVE-2019-14889`, `CVE-2019-1551`, `CVE-2019-15903`, `,CVE-2019-16168`, `CVE-2019-16935`, `CVE-2019-19221`, `CVE-2019-19906`, `CVE-2019-19956`, `CVE-2019-20218`, `CVE-2019-20386`, `CVE-2019-20387`, `CVE-2019-20388`, `CVE-2019-20454`, `CVE-2019-20907`, `CVE-2019-5018`, `CVE-2020-10029`, `CVE-2020-13630`, `CVE-2020-13631`, `CVE-2020-13632`, `CVE-2020-14422`, `CVE-2020-1730`, `CVE-2020-1751`, `CVE-2020-1752`, `CVE-2020-6405`, `CVE-2020-7595`, and `CVE-2020-8177`. |
{: row-headers}
{: class="comparison-table"}
{: caption="Object Storage plug-in version 2.0.5" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the version of the component. The second column contains the release date of the component. The third column contains a brief description of the change made to the component."}
