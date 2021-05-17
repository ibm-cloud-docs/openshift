---

copyright:
  years: 2014, 2021
lastupdated: "2021-05-14"

keywords: autoscaler, add-on, autoscaler changelog

subcollection: openshift, cluster autoscaler, add-on, scale

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
  
  
# Cluster autoscaler add-on changelog
{: #ca_changelog}

View information for patch updates to the cluster autoscaler add-on in your {{site.data.keyword.openshiftlong_notm}} clusters.
{: shortdesc}

* **Patch updates**: Patch updates are delivered automatically by IBM and do not contain any feature updates or changes in the supported add-on and cluster versions.
* **Release updates**: Release updates contain new features for the cluster autoscaler or changes in the supported add-on or cluster versions. You must manually apply release updates to your cluster autoscaler add-on. To update your cluster autoscaler add-on, see [Updating the cluster autoscaler add-on](/docs/openshift?topic=openshift-ca#ca_addon_up).

Refer to the following tables for a summary of changes for each version of the [cluster autoscaler add-on](/docs/openshift?topic=openshift-ca).

Version `1.0.1` of {{site.data.keyword.block_storage_is_short}} add-on is deprecated. If your cluster runs a deprecated or unsupported add-on version, update your cluster to the latest version. You can update the add-on by disabling and re-enabling it. Disable the add-on by running the `ibmcloud oc cluster addon disable cluster-autoscaler --cluster <cluster-name>` command. Then, re-enable by running the `ibmcloud oc cluster addon enable cluster-autoscaler --cluster <cluster-name>` command.
{: important}

| Cluster autoscaler add-on version | Supported? | {{site.data.keyword.openshiftshort}} version support |
| -------------------- | -----------|--------------------------- |
| 1.0.2 | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | {{site.data.keyword.openshiftshort}} 4.3 - 4.6</li></ul> |
| 1.0.1 | | {{site.data.keyword.openshiftshort}} 4.3 - 4.6</li></ul> |
{: summary="The rows are read from left to right. The first column is the cluster autoscaler add-on version. The second column is the version's supported state. The third column is the {{site.data.keyword.openshiftshort}} version of your cluster that the cluster autoscaler version is supported for."}

## Changelog for 1.0.2, released 08 March 2021
{: #0102_ca_addon}

The following table shows the changes that are included in version 1.0.2 of the managed cluster autoscaler add-on.
{: shortdesc}

To view a list of add-ons and the supported {{site.data.keyword.openshiftshort}} versions, run the following command.
```sh
ibmcloud oc addon-versions
```
{: pre}

| Patch version | Image tags | Release date | Supported {{site.data.keyword.openshiftshort}} versions | Description |
| --- | --- | --- | --- | --- |
| `1.0.2_256` | <ul>`1.17.4-2`</li><li>`1.18.3-2`</li><li>`1.19.1-2`</li><li>`1.20.0-2`</li></ul> | 19 April 2021 | 4.3 - 4.6</li></ul> | Includes fixes for [CVE-2021-27919](https://nvd.nist.gov/vuln/detail/CVE-2021-27919){: external} and [CVE-2021-27918](https://nvd.nist.gov/vuln/detail/CVE-2021-27918){: external}. |
| `1.0.2_249` | <ul><li>`1.16.7-1`</li><li>`1.17.4-1`</li><li>`1.18.3-1`</li><li>`1.19.1-1`</li><li>`1.20.0-1`</li></ul> | 01 April 2021 | 4.3 - 4.6</li></ul> | <ul><li>Includes fixes for [CVE-2021-3114](https://nvd.nist.gov/vuln/detail/CVE-2021-3114){: external} and [CVE-2021-3115](https://nvd.nist.gov/vuln/detail/CVE-2021-3115){: external}.</li><li>Removes the `init` container. Prior to this update, the cluster autoscaler pods would remain in the `initContainer` state if the API key that is provided is missing or malformed. This update removes the `init` container so that if the API key is missing or malformed, the cluster autoscaler pod fails.</li></ul>.  |
| `1.0.2_224` | <ul><li>`1.16.7-0`</li><li>`1.17.4-0`</li><li>`1.18.3-0`</li><li>`1.19.1-0`</li><li>`1.20.0-0`</li></ul> | 09 March 2021 | 4.3 - 4.6</li></ul> | Adds support for Kubernetes version 1.20. |
{: row-headers}
{: class="comparison-table"}
{: caption="Cluster autoscaler 1.0.2" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the patch version of the component. The second column lists the image tags of the component. The third column contains the release date of the component. The fourth column contains a brief description of the change made to the component."}


## Changelog for 1.0.1, released 15 August 2020
{: #0101_ca_addon}

The following table shows the changes that are included in version 1.0.1 of the managed cluster autoscaler add-on.
{: shortdesc}

To view a list of add-ons and the supported {{site.data.keyword.openshiftshort}} versions, run the following command.
```
ibmcloud oc addon-versions
```
{: pre}

| Patch version | Image tags | Release date | Supported {{site.data.keyword.openshiftshort}} versions | Description |
| --- | --- | --- | --- | --- |
| `1.0.1_219` | <ul><li>`1.16.7-0`</li><li>`1.17.4-0`</li><li>`1.18.3-0`</li><li>`1.19.1-0`</li></ul> | 16 February 2021 | 4.3 - 4.6 | Updates the code base to synchronize with the community autoscaler. For more information, see the [Kubernetes autoscaler documentation](https://github.com/kubernetes/autoscaler/releases){: external}. |
| `1.0.1_210` | <ul><li>`1.16.2-9`</li><li>`1.17.0-10`</li><li>`1.18.1-9`</li><li>`1.19.0-4`</li></ul> | 13 January 2021 | 4.3 - 4.6 | Update addresses [`DLA-2509-1`](https://security-tracker.debian.org/tracker/DLA-2509-1){: external}. |
| `1.0.1_205` | <ul><li>`1.11.0-7`</li><li>`1.16.2-8`</li><li>`1.17.0-9`</li><li>`1.18.1-8`</li><li>`1.19.0-3`</li></ul> | 15 December 2020 | 4.3 - 4.6 | Updates the `initContainer` to use the universal base image (UBI). |
| `1.0.1_195` | <ul><li>`1.11.0-7`</li><li>`1.16.2-8`</li><li>`1.17.0-9`</li><li>`1.18.1-8`</li><li>`1.19.0-3`</li></ul>  | 10 December 2020 | 4.3 - 4.6 | <ul><li>The cluster autoscaler images are now signed.</li><li>Resources that are deployed by the cluster autoscaler add-on are now linked with the corresponding source code and build URLs.</li><li>Updates the Go version to `1.15.5`.</li></ul> |
| `1.0.1_146` | <ul><li>`1.15.4-4`</li><li>`1.16.2-7`</li><li>`1.17.0-8`</li><li>`1.18.1-7`</li><li>`1.19.0-2`</li></ul>  | 03 December 2020 | 4.3 - 4.6 | <ul><li>The cluster autoscaler now runs as non-root.</li><li>Adds a feature to validate secrets before the autoscaler pods are initialized.</li></ul> |
| `1.0.1_128` | <ul><li>`1.15.4-4`</li><li>`1.16.2-6`</li><li>`1.17.0-7`</li><li>`1.18.1-6`</li><li>`1.19.0-1`</li></ul> | 27 October 2020 | 4.3 - 4.5</li></ul> | Updates the Go version to `1.15.2` |
| `1.0.1_124` | <ul><li>`1.15.4-4`</li><li>`1.16.2-6`</li><li>`1.17.0-7`</li><li>`1.18.1-6`</li><li>`1.19.0-1`</li></ul> | 16 October 2020 | 4.3 - 4.5</li></ul> | <ul><li>Exposes the `--new-pod-scale-up-delay` flag in the configmap.</li><li>Adds support for Kubernetes 1.19.</li></ul> |
| `1.0.1_114` | <ul><li>`1.15.4-4`</li><li>`1.16.2-5`</li><li>`1.17.0-6`</li><li>`1.18.1-5`</li></ul> | 10 September 2020 | 4.3 - 4.5</li></ul> | <ul><li>Includes fixes for `CVE-5188` and `CVE-3180`.</li><li>Unlike the previous Helm chart, you can modify all of the add-on configuration settings via a single configmap.</li></ul> |
{: row-headers}
{: class="comparison-table"}
{: caption="Cluster autoscaler 1.0.1" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the patch version of the component. The second column lists the image tags of the component. The third column contains the release date of the component. The fourth column contains a brief description of the change made to the component."}