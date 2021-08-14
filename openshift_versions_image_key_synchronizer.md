---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-14"

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
  


# {{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on changelog
{: #image-key-synchronizer-changelog}

View information for version updates to the [{{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on](/docs/openshift?topic=openshift-images#encrypted-images) in clusters that run {{site.data.keyword.openshiftshort}} version 4.5 and later.
{: shortdesc}

* **Patch updates**: {{site.data.keyword.cloud_notm}} keeps all your add-on components up-to-date by automatically rolling out patch updates to the most recent version of the Image Key Synchronizer that is offered by {{site.data.keyword.openshiftlong_notm}}.
* **Minor version updates**: To update your add-on components to the most recent minor version of the Image Key Synchronizer that is offered by {{site.data.keyword.openshiftlong_notm}}, follow the steps in [Updating managed add-ons](/docs/openshift?topic=openshift-managed-addons#updating-managed-add-ons).

Review the supported versions of {{site.data.keyword.openshiftlong_notm}} for each add-on version. In the CLI, you can run `ibmcloud oc cluster addon ls -c <cluster_name_or_ID>` to check the current version of your add-on, and `ibmcloud oc cluster get -c <cluster_name_or_ID>` to check the current version of your cluster.

| Image Key Synchronizer add-on version | Supported? | {{site.data.keyword.openshiftshort}} version support |
| -------------------------- | -----------|----------------------------------------------------- |
| 1.0.0 | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | 4.6, 4.5, 4.4 |
{: summary="The rows are read from left to right. The first column is the Image Key Synchronizer add-on version. The second column is the version's supported state. The third column is the {{site.data.keyword.openshiftshort}} version of your cluster that the add-on version is supported for."}
{: caption="Supported Image Key Synchronizer add-on versions" caption-side="top"}

## Version 1.0.0
{: #1_0_0}

|Version build|Release date|Changes|
|-------------|------------|-------|
| 1.0.0_614 | 10 August 2021 | Updates to address [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-33910){: external} and [CVE-2021-34558](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-34558){: external} |
| 1.0.0_575 | 23 July 2021 | Updates to address [CVE-2021-20271](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-20271){: external}, [CVE-2021-3516](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3516){: external}, [CVE-2021-3517](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3517){: external}, [CVE-2021-3518](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3518){: external}, [CVE-2021-3537](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3537){: external}, [CVE-2021-3541](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3541){: external}, and [CVE-2021-3520](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3520){: external}. |
| 1.0.0_549 | 17 Jun 2021 | Updates to address [CVE-2021-31525](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-31525){: external} and [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-33194){: external}.|
| 1.0.0_529 | 02 Jun 2021 | Updates to address [CVE-2016-10228](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-10228){: external}, [CVE-2019-13012](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13012){: external}, [CVE-2019-18276](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-18276){: external}, [CVE-2019-25013](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-25013){: external}, [CVE-2019-2708](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-2708){: external}, [CVE-2019-3842](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-3842){: external}, [CVE-2019-9169](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9169){: external}, [CVE-2020-13434](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13434){: external}, [CVE-2020-13543](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13543){: external}, [CVE-2020-13584](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13584){: external}, [CVE-2020-13776](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13776){: external}, [CVE-2020-15358](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-15358){: external}, [CVE-2020-24977](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24977){: external}, [CVE-2020-27618](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-27618){: external}, [CVE-2020-28196](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28196){: external}, [CVE-2020-29361](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-29361){: external}, [CVE-2020-29362](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-29362){: external}, [CVE-2020-29363](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-29363){: external}, [CVE-2020-8231](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8231){: external}, [CVE-2020-8284](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8284){: external}, [CVE-2020-8285](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8285){: external}, [CVE-2020-8286](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8286){: external}, [CVE-2020-8927](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8927){: external}, [CVE-2020-9948](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9948){: external}, [CVE-2020-9951](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9951){: external}, [CVE-2020-9983](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9983){: external}, [CVE-2021-3326](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3326){: external}, [RHSA-2021:1581](https://access.redhat.com/errata/RHSA-2021:1581){: external}, [RHSA-2021:1585](https://access.redhat.com/errata/RHSA-2021:1585){: external}, [RHSA-2021:1586](https://access.redhat.com/errata/RHSA-2021:1586){: external}, [RHSA-2021:1593](https://access.redhat.com/errata/RHSA-2021:1593){: external}, [RHSA-2021:1597](https://access.redhat.com/errata/RHSA-2021:1597){: external}, [RHSA-2021:1609](https://access.redhat.com/errata/RHSA-2021:1609){: external}, [RHSA-2021:1610](https://access.redhat.com/errata/RHSA-2021:1610){: external}, [RHSA-2021:1611](https://access.redhat.com/errata/RHSA-2021:1611){: external}, [RHSA-2021:1675](https://access.redhat.com/errata/RHSA-2021:1675){: external}, [RHSA-2021:1679](https://access.redhat.com/errata/RHSA-2021:1679){: external}, and [RHSA-2021:1702](https://access.redhat.com/errata/RHSA-2021:1702){: external}.|
| 1.0.0_485 | 28 Apr 2021 | Updates to address [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}.|
| 1.0.0_473 | 19 Apr 2021 | Updates to address [CVE-2021-3121](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3121){: external}, [CVE-2021-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-28851){: external}, and [CVE-2021-28852](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-28852){: external}.|
| 1.0.0_461 | 14 Apr 2021 | Updates to address [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3450){: external}.|
|1.0.0_438|30 Mar 2021|Updates the Go version to 1.15.10 for [CVE-2021-3114](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3114){: external} and [CVE-2021-3115](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3115){: external}.|
{: summary="The rows are read from left to right. The first column is the build of the image version. The second column is the build release date. The third column contains a brief description of the change made in the version build."}
{: caption="Changelog for version 1.0.0 of the Image Key Synchronizer add-on" caption-side="top"}


