---

copyright:
  years: 2014, 2020
lastupdated: "2020-11-25"

keywords: vpc block, add-on, vpc block changelog

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
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# {{site.data.keyword.block_storage_is_short}} add-on changelog
{: #vpc_bs_changelog}

View information for patch updates to the {{site.data.keyword.block_storage_is_full}} add-on in your {{site.data.keyword.openshiftlong_notm}} clusters.
{: shortdesc}

* **Patch updates**: Patch updates are delivered automatically by IBM and do not contain any feature updates or changes in the supported add-on and cluster versions.
* **Release updates**: Release updates contain new features for the {{site.data.keyword.block_storage_is_full}} or changes in the supported add-on or cluster versions. You must manually apply release updates to your {{site.data.keyword.block_storage_is_full}} add-on. To update your {{site.data.keyword.block_storage_is_full}} add-on, see [Updating the {{site.data.keyword.block_storage_is_full}} add-on](/docs/openshift?topic=openshift-vpc-block#vpc-addon-update).

Refer to the following tables for a summary of changes for each version of the {{site.data.keyword.block_storage_is_full}} add-on.

| {{site.data.keyword.block_storage_is_full}} add-on version | Supported? | {{site.data.keyword.openshiftlong_notm}} version support |
| -------------------- | -----------|--------------------------- |
| 2.0.3 | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | 4.3 - 4.5 |
{: summary="The rows are read from left to right. The first column is the {{site.data.keyword.block_storage_is_full}} add-on version. The second column is the version's supported state. The third column is the {{site.data.keyword.openshiftshort}} version of your cluster that the {{site.data.keyword.block_storage_is_full}} version is supported for."}

## Changelog for version 2.0.3
{: #0203_is_block}

The following table shows the changes that are included in version 2.0.3 {{site.data.keyword.block_storage_is_full}} add-on.
{: shortdesc}

To view a list of add-ons and the supported {{site.data.keyword.openshiftshort}} versions, run the following command.
```
ibmcloud oc addon-versions
```
{: pre}

| Patch version | `vpc-block-driver` image tag | Release date | Supported {{site.data.keyword.openshiftshort}} versions | Description |
| --- | --- | --- | --- |
| `2.0.3_404` | `v2.0.7` | 25 November 2020 | 4.3 - 4.5 | Updates in this patch:<ul><li>Fixed a vulernability scan fix in `v2.0.6` image tag.</li><li>Updated the base image from `alpine` to `UBI`.</li><li>Pods and containers now run as `non-root` except for the `node-server` pod's containers.</li></ul> |
| `2.0.3_375` | `v2.0.6` | 17 September 2020 | 4.3 - 4.5 | Fixed an issue with volume attachment when replacing workers. |
| `2.0.3_374+` | `v2.0.5` | 29 August 2020 | 4.3 - 4.5 | Added the `/var/lib/kubelet` path for CSI driver calls on OCP 4.4. |
| `2.0.3_365` | `v2.0.4` | 05 August 2020 | 4.3 - 4.5 | <ul><li>Updated sidecar container images.</li><li>Added liveness probe.</li><li>Enabled parallel attachment and detachment of volumes to worker nodes. Previously, worker nodes were attached and detached sequentially.</li></ul> |
{: summary="The rows are read from left to right. The first column is the patch version number of the component. The second column is the image tag the component. The third column contains the release date of the patch. The fourth column contains a brief description of the change made to the component."}
{: caption="Patch updates for version 2.0.3" caption-side="top"}
{: caption="{{site.data.keyword.block_storage_is_full}}" caption-side="top"}