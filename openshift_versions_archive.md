---

copyright:
 years: 2014, 2021
lastupdated: "2021-03-16"

keywords: roks

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


# Archived {{site.data.keyword.openshiftshort}} version changelogs
{: #changelog_archive}

The following versions are no longer supported for {{site.data.keyword.openshiftlong}}. You can review the archive of the changelogs.
{: shortdesc}

Unsupported versions: 4.3 (Kubernetes 1.16)

Looking for the changelogs of supported versions? See [{{site.data.keyword.openshiftshort}} version changelog](/docs/openshift?topic=openshift-openshift_changelog).
{: tip}

## Version 4.3 changelog (unsupported as of 7 March 2021)
{: #version-43}

Version 4.3 is unsupported. You can review the following archive of the 4.3 changelogs.
{: shortdesc}

### Changelog for worker node fix pack 4.3.40_1555_openshift, released 1 March 2021
{: #4340_1555_worker}

The following table shows the changes that are included in the worker node fix pack `4.3.40_1555_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.registrylong_notm}} private endpoints | N/A | N/A | **VPC Gen 2 worker nodes**: Fixed a bug where traffic to the private endpoints of {{site.data.keyword.registrylong_notm}} might fail after rebooting the worker node. |
| RHEL 7 Packages | N/A | N/A | Updated worker node with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.40_1554_openshift" caption-side="top"}

### Changelog for master fix pack 4.3.40_1555_openshift, released 22 February 2021
{: #4340_1555}

The following table shows the changes that are included in the master fix pack patch update `4.3.40_1555_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.16 | v1.1.18 | Updated to use `Go` version 1.15.7. Updated image to implement additional IBM security controls. |
| Gateway-enabled cluster controller | 1195 | 1232 | Updated to use `Go` version 1.15.7. |
| IBM Calico extension | 567 | 618 | Updated to use `Go` version 1.15.7. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.17-1 | v1.17.17-5 | Updated image for for [DLA-2509-1](https://www.debian.org/lts/security/2020/dla-2509){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 385 | 388 | Improved the retry logic for provisioning persistent volume claims (PVCs). |
| {{site.data.keyword.cloud_notm}} RBAC Operator | f859228 | 86de2b7 | Updated to use `Go` version 1.15.7. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1078 | 1165 | Updated to use `Go` version 1.15.7. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.40_1552_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.40_1554_openshift, released 15 February 2021
{: #4340_1554}

The following table shows the changes that are included in the worker node fix pack `4.3.40_1554_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | 3.10.0-1160.11.1.el7 | 3.10.0-1160.15.2.el7 | Updated worker node with image kernel and package updates for: [CVE-2020-10543](https://nvd.nist.gov/vuln/detail/CVE-2020-10543){: external}, [CVE-2020-10878](https://nvd.nist.gov/vuln/detail/CVE-2020-10878){: external}, [CVE-2020-12723](https://nvd.nist.gov/vuln/detail/CVE-2020-12723){: external}, [CVE-2020-15436](https://nvd.nist.gov/vuln/detail/CVE-2020-15436){: external}, [CVE-2020-35513](https://nvd.nist.gov/vuln/detail/CVE-2020-35513){: external}, [CVE-2019-25013](https://nvd.nist.gov/vuln/detail/CVE-2019-25013){: external}, [CVE-2020-10029](https://nvd.nist.gov/vuln/detail/CVE-2020-10029){: external}, [CVE-2020-29573](https://nvd.nist.gov/vuln/detail/CVE-2020-29573){: external}, and [CVE-2020-12321](https://nvd.nist.gov/vuln/detail/CVE-2020-12321)){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.40_1553_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.40_1553_openshift, released 1 February 2021
{: #4340_1553}

The following table shows the changes that are included in the worker node fix pack `4.3.40_1553_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates for [CVE-2021-3156](https://nvd.nist.gov/vuln/detail/CVE-2021-3156){: external}, [CVE-2020-25684](https://nvd.nist.gov/vuln/detail/CVE-2020-25684){: external}, [CVE-2020-25685](https://nvd.nist.gov/vuln/detail/CVE-2020-25685){: external}, and [CVE-2020-25686](https://nvd.nist.gov/vuln/detail/CVE-2020-25686){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.40_1551_openshift" caption-side="top"}

### Changelog for master fix pack 4.3.40_1552_openshift, released 19 January 2021
{: #4340_1552}

The following table shows the changes that are included in the master fix pack patch update `4.3.40_1552_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.13 | v1.1.16 | Updated image to implement additional IBM security controls. |
| Gateway-enabled cluster controller | 1184 | 1195 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external}. |
| IBM Calico extension | 556 | 567 | Updated image to implement additional IBM security controls and for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971) and [CVE-2020-24659](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24659){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.0.0 | v2.0.1 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external} and [CVE-2020-24659](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24659){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.16-1 | v1.17.17-1 | Updated to support the Kubernetes 1.17.17 release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 384 | 385 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external} and [CVE-2020-24659](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24659){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1004 | 1078 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.3.0-20201110 | v4.3.0-20210111 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.3.0+20210111){: external}. |
| OpenVPN Operator image | v1.0.10 | v1.1.0 | Updated image to implement additional IBM security controls and for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.3.0+20201110 | 4.3.0+20210111 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.3.0+20210111){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.40_1550_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.40_1551_openshift, released 18 January 2021
{: #4340_1551}

The following table shows the changes that are included in the worker node fix pack `4.3.40_1551_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.40_1549_openshift" caption-side="top"}

### Changelog for master fix pack 4.3.40_1550_openshift, released 6 January 2021
{: #4340_1550}

The following table shows the changes that are included in the master fix pack patch update `4.3.40_1550_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| IBM Calico extension | 538 | 556 | Updated image to include the `ip` command. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | 1.17.2 | v2.0.0 | Updated to use the universal base image (UBI), to use `Go` version 1.15.5, to run with a least privileged security context, and to improve logging. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.15-1 | v1.17.16-1 | Updated to support the Kubernetes 1.17.16 release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in | N/A | N/A | Updated to run with a privileged security context. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | c148a8a | f859228 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external} and [CVE-2020-24659](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24659){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.40_1548_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.40_1549_openshift, released 21 December 2020
{: #4340_1549}

The following table shows the changes that are included in the worker node fix pack update `4.3.40_1549_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HAProxy | db4e6d | 9b2dca | Image update for [CVE-2020-1971](https://nvd.nist.gov/vuln/detail/CVE-2020-1971){: external} and [CVE-2020-24659](https://nvd.nist.gov/vuln/detail/CVE-2020-24659){: external}. |
| RHEL 7 Packages | 3.10.0-1160.6.1.el7 | 3.10.0-1160.11.1.el7 | Updated worker node image with kernel and package updates for: [CVE-2019-18282](https://nvd.nist.gov/vuln/detail/CVE-2019-18282){: external}, [CVE-2020-10769](https://nvd.nist.gov/vuln/detail/CVE-2020-10769){: external}, [CVE-2020-14314](https://nvd.nist.gov/vuln/detail/CVE-2020-14314){: external}, [CVE-2020-14385](https://nvd.nist.gov/vuln/detail/CVE-2020-14385){: external}, [CVE-2020-24394](https://nvd.nist.gov/vuln/detail/CVE-2020-24394){: external}, [CVE-2020-25212](https://nvd.nist.gov/vuln/detail/CVE-2020-25212){: external}, [CVE-2020-25643](https://nvd.nist.gov/vuln/detail/CVE-2020-25643){: external}, and [CVE-2020-1971](https://nvd.nist.gov/vuln/detail/CVE-2020-1971){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.40_1548_openshift" caption-side="top"}

### Changelog for master fix pack 4.3.40_1548_openshift, released 14 December 2020
{: #4340_1548}

The following table shows the changes that are included in the master fix pack patch update `4.3.40_1548_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| etcd | v3.4.13 | v3.4.14 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.14){: external}. |
| Gateway-enabled cluster controller | 1105 | 1184 | Updated to use `Go` version 1.15.5. Updated image to implement additional IBM security controls. |
| IBM Calico extension | 378 | 538 | Updated to use the universal base image (UBI), to run as a non-root user and to use `Go` version 1.15.5. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.14-1 | v1.17.15-1 | Updated to support the Kubernetes 1.17.15 release. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.filestorage_full_notm}} monitor | 379 | 384 | Updated to use `Go` version 1.15.5 and to run as a non-root user. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.filestorage_full_notm}} plug-in | 379 | 384 | Updated to use `Go` version 1.15.5 and to run with a least privileged security context. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 197bc70 | c148a8a | Updated to use `Go` version 1.15.6 and updated image to implement additional IBM security controls. |
| Load balancer and load balancer monitor {{site.data.keyword.cloud_notm}} Provider | 208 | 1004 | Updated Alpine base image to version 3.12 and to use `Go` version 1.15.5. Updated image for [CVE-2020-8037](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8037){: external} and [CVE-2020-28928](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28928){: external}. Updated image to implement additional IBM security controls. |
| OpenVPN client | 2.4.6-r3-IKS-116 | 2.4.6-r3-IKS-301 | Updated image to implement additional IBM security controls. |
| OpenVPN server | 2.4.6-r3-IKS-131 | 2.4.6-r3-IKS-301 | Updated image to implement additional IBM security controls. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.40_1546_openshift" caption-side="top"}
### Changelog for worker node fix pack 4.3.40_1547_openshift, released 7 December 2020
{: #4340_1547}

The following table shows the changes that are included in the worker node fix pack update `4.3.40_1547_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HAProxy | 1.8.26-384f42 | db4e6d | Added provenance labels for source tracking. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.40_1546_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.40_1546_openshift, released 23 November 2020
{: #4340_1546_worker}

The following table shows the changes that are included in the worker node fix pack update `4.3.40_1546_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Ephemeral storage reservations | N/A | N/A | Local ephemeral storage is reserved on the Kubernetes data disk for system components. For more information, see [Worker node resource reserves](/docs/openshift?topic=openshift-planning_worker_nodes#resource_limit_node). |
| RHEL 7 Packages |  3.10.0-1160.2.2.el7 | 3.10.0-1160.6.1.el7 | Updated worker node image with kernel and package updates for [CVE-2020-8622](https://nvd.nist.gov/vuln/detail/CVE-2020-8622){: external}, [CVE-2020-8623](https://nvd.nist.gov/vuln/detail/CVE-2020-8623){: external}, [CVE-2020-8624](https://nvd.nist.gov/vuln/detail/CVE-2020-8624){: external}, [CVE-2019-20907](https://nvd.nist.gov/vuln/detail/CVE-2019-20907){: external}, [CVE-2020-15999](https://nvd.nist.gov/vuln/detail/CVE-2020-15999){: external}, [CVE-2020-8177](https://nvd.nist.gov/vuln/detail/CVE-2020-8177){: external}, [CVE-2019-20811](https://nvd.nist.gov/vuln/detail/CVE-2019-20811){: external}, [CVE-2020-14331](https://nvd.nist.gov/vuln/detail/CVE-2020-14331){: external}, [CVE-2020-8695](https://nvd.nist.gov/vuln/detail/CVE-2020-8695){: external}, [CVE-2020-8696](https://nvd.nist.gov/vuln/detail/CVE-2020-8696){: external}, and [CVE-2020-8698](https://nvd.nist.gov/vuln/detail/CVE-2020-8698){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.40_1545_openshift" caption-side="top"}

### Changelog for master fix pack 4.3.40_1546_openshift, released 16 November 2020
{: #4340_1546}

The following table shows the changes that are included in the master fix pack patch update `4.3.40_1546_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster health image | v1.1.12 | v1.1.13 | Updated image for [DLA-2424-1](https://www.debian.org/lts/security/2020/dla-2424){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.13-1 | v1.17.14-1 | Updated to support the Kubernetes 1.17.14 release. Updated image for [DLA-2424-1](https://www.debian.org/lts/security/2020/dla-2424){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 378 | 379 | Updated to use the universal base image (UBI) and to use `Go` version 1.15.2. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 31c794a | 197bc70 | Updated image for [CVE-2019-20454](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20454){: external}, [CVE-2020-10029](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-10029){: external}, [CVE-2020-1751](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1751){: external}, [CVE-2020-1752](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1752){: external}, [CVE-2019-20807](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20807){: external}, [CVE-2019-16935](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16935){: external}, [CVE-2019-20907](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20907){: external}, [CVE-2020-14422](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14422){: external}, [CVE-2020-8492](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8492){: external}, [CVE-2019-15165](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-15165){: external}, [CVE-2019-16168](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16168){: external}, [CVE-2019-20218](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20218){: external}, [CVE-2019-5018](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-5018){: external}, [CVE-2020-13630](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13630){: external}, [CVE-2020-13631](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13631){: external}, [CVE-2020-13632](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13632){: external}, [CVE-2020-6405](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-6405){: external}, [CVE-2020-9327](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9327){: external}, [CVE-2020-8177](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8177){: external}, [CVE-2019-13050](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13050){: external}, [CVE-2018-20843](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-20843){: external}, [CVE-2019-15903](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-15903){: external}, [CVE-2019-14889](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14889){: external}, [CVE-2020-1730](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1730){: external}, [CVE-2019-1551](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1551){: external}, [CVE-2020-14382](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14382){: external}, [CVE-2019-13627](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13627){: external}, [CVE-2019-19956](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19956){: external}, [CVE-2019-20388](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20388){: external}, [CVE-2020-7595](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-7595){: external}, [CVE-2019-20386](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20386){: external}, [CVE-2019-19906](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19906){: external}, [CVE-2019-20387](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20387){: external}, and [CVE-2019-19221](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19221){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.3.0-20200821 | v4.3.0-20201110 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.3.0+20201110){: external}. |
| {{site.data.keyword.openshiftshort}} | 4.3.38 | 4.3.40 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-40){: external}. |
| OpenVPN Operator image | v1.0.9 | v1.0.10 | Updated image for [CVE-2019-20454](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20454){: external}, [CVE-2020-10029](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-10029){: external}, [CVE-2020-1751](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1751){: external}, [CVE-2020-1752](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1752){: external}, [CVE-2019-20807](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20807){: external}, [CVE-2019-16935](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16935){: external}, [CVE-2019-20907](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20907){: external}, [CVE-2020-14422](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14422){: external}, [CVE-2020-8492](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8492){: external}, [CVE-2019-15165](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-15165){: external}, [CVE-2019-16168](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16168){: external}, [CVE-2019-20218](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20218){: external}, [CVE-2019-5018](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-5018){: external}, [CVE-2020-13630](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13630){: external}, [CVE-2020-13631](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13631){: external}, [CVE-2020-13632](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13632){: external}, [CVE-2020-6405](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-6405){: external}, [CVE-2020-9327](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9327){: external}, [CVE-2020-8177](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8177){: external}, [CVE-2019-13050](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13050){: external}, [CVE-2018-20843](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-20843){: external}, [CVE-2019-15903](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-15903){: external}, [CVE-2019-14889](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14889){: external}, [CVE-2020-1730](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1730){: external}, [CVE-2019-1551](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1551){: external}, [CVE-2020-14382](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14382){: external}, [CVE-2019-13627](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13627){: external}, [CVE-2019-19956](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19956){: external}, [CVE-2019-20388](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20388){: external}, [CVE-2020-7595](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-7595){: external}, [CVE-2019-20386](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20386){: external}, [CVE-2019-19906](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19906){: external}, [CVE-2019-20387](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20387){: external}, and [CVE-2019-19221](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19221){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.3.0+20200821 | 4.3.0+20201110 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.3.0+20201110){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.38_1544_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.40_1545_openshift, released 9 November 2020
{: #4340_1545}

The following table shows the changes that are included in the worker node fix pack update `4.3.40_1545_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates for [CVE-2020-15999](https://nvd.nist.gov/vuln/detail/CVE-2020-15999){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.40_1544_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.40_1544_openshift, released 26 October 2020
{: #4340_1544}

The following table shows the changes that are included in the worker node fix pack update `4.3.40_1544_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.3.38 | 4.3.40 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-40){: external}.|
| RHEL 7 Packages | 3.10.0-1160.2.1.el7 | 3.10.0-1160.2.2.el7 | Updated worker node images with kernel and package updates for [CVE-2020-12351](https://nvd.nist.gov/vuln/detail/CVE-2020-12351){: external} and [CVE-2020-12352](https://nvd.nist.gov/vuln/detail/CVE-2020-12352){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.38_1542_openshift" caption-side="top"}

### Changelog for master fix pack 4.3.38_1544_openshift, released 26 October 2020
{: #4338_1544}

The following table shows the changes that are included in the master fix pack patch update `4.3.38_1544_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster health image | v1.1.11 | v1.1.12 | Fixed check for unsupported add-ons. Updated to use `Go` version 1.15.2. |
| Gateway-enabled cluster controller | 1082 | 1105 | Updated to use `Go` version 1.15.2. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | 1.17.1 | 1.17.2 | Updated to use `Go` version 1.13.15. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.12-1 | v1.17.13-1 | Updated to support the Kubernetes 1.17.13 release. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 4b47693 | 31c794a | Updated to use `Go` version 1.15.2. |
| {{site.data.keyword.openshiftshort}} | 4.3.35 | 4.3.38 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-38){: external}. |
| {{site.data.keyword.openshiftshort}} configuration | N/A | N/A | New version 4.3 clusters that run on the VPC Gen 2 infrastructure provider and use {{site.data.keyword.cos_full_notm}} now proxy container image traffic through the internal registry pods directly to the {{site.data.keyword.cos_short}} endpoints. To configure this proxying for existing version 4.3 clusters, see [the troubleshooting topic](/docs/openshift?topic=openshift-cs_troubleshoot_app#ts-app-ocr-vpc-push). |
| OpenVPN Operator image | v1.0.8 | v1.0.9 | Updated to improve OpenVPN availability. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.35_1539_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.38_1542_openshift, released 12 October 2020
{: #4338_1542}

The following table shows the changes that are included in the worker node fix pack update `4.3.38_1542_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1127.19.1.el7 | 3.10.0-1160.2.1.el7 | Updated worker node image with kernel and package updates for: [CVE-2019-12450](https://nvd.nist.gov/vuln/detail/CVE-2019-12450){: external}, [CVE-2019-14822](https://nvd.nist.gov/vuln/detail/CVE-2019-14822){: external}, [CVE-2020-12243](https://nvd.nist.gov/vuln/detail/CVE-2020-12243){: external}, [CVE-2019-14866](https://nvd.nist.gov/vuln/detail/CVE-2019-14866){: external}, [CVE-2017-12652](https://nvd.nist.gov/vuln/detail/CVE-2017-12652){: external}, [CVE-2017-18551](https://nvd.nist.gov/vuln/detail/CVE-2017-18551){: external}, [CVE-2018-20836](https://nvd.nist.gov/vuln/detail/CVE-2018-20836){: external}, [CVE-2019-9454](https://nvd.nist.gov/vuln/detail/CVE-2019-9454){: external}, [CVE-2019-9458](https://nvd.nist.gov/vuln/detail/CVE-2019-9458){: external}, [CVE-2019-12614](https://nvd.nist.gov/vuln/detail/CVE-2019-12614){: external}, [CVE-2019-15217](https://nvd.nist.gov/vuln/detail/CVE-2019-15217){: external}, [CVE-2019-15807](https://nvd.nist.gov/vuln/detail/CVE-2019-15807){: external}, [CVE-2019-15917](https://nvd.nist.gov/vuln/detail/CVE-2019-15917){: external}, [CVE-2019-16231](https://nvd.nist.gov/vuln/detail/CVE-2019-16231){: external}, [CVE-2019-16233](https://nvd.nist.gov/vuln/detail/CVE-2019-16233){: external}, [CVE-2019-16994](https://nvd.nist.gov/vuln/detail/CVE-2019-16994){: external}, [CVE-2019-17053](https://nvd.nist.gov/vuln/detail/CVE-2019-17053){: external}, [CVE-2019-17055](https://nvd.nist.gov/vuln/detail/CVE-2019-17055){: external}, [CVE-2019-18808](https://nvd.nist.gov/vuln/detail/CVE-2019-18808){: external}, [CVE-2019-19046](https://nvd.nist.gov/vuln/detail/CVE-2019-19046){: external}, [CVE-2019-19055](https://nvd.nist.gov/vuln/detail/CVE-2019-19055){: external}, [CVE-2019-19058](https://nvd.nist.gov/vuln/detail/CVE-2019-19058){: external}, [CVE-2019-19059](https://nvd.nist.gov/vuln/detail/CVE-2019-19059){: external}, [CVE-2019-19062](https://nvd.nist.gov/vuln/detail/CVE-2019-19062){: external}, [CVE-2019-19063](https://nvd.nist.gov/vuln/detail/CVE-2019-19063){: external}, [CVE-2019-19332](https://nvd.nist.gov/vuln/detail/CVE-2019-19332){: external}, [CVE-2019-19447](https://nvd.nist.gov/vuln/detail/CVE-2019-19447){: external}, [CVE-2019-19523](https://nvd.nist.gov/vuln/detail/CVE-2019-19523){: external}, [CVE-2019-19524](https://nvd.nist.gov/vuln/detail/CVE-2019-19524){: external}, [CVE-2019-19530](https://nvd.nist.gov/vuln/detail/CVE-2019-19530){: external}, [CVE-2019-19534](https://nvd.nist.gov/vuln/detail/CVE-2019-19534){: external}, [CVE-2019-19537](https://nvd.nist.gov/vuln/detail/CVE-2019-19537){: external}, [CVE-2019-19767](https://nvd.nist.gov/vuln/detail/CVE-2019-19767){: external}, [CVE-2019-19807](https://nvd.nist.gov/vuln/detail/CVE-2019-19807){: external}, [CVE-2019-20054](https://nvd.nist.gov/vuln/detail/CVE-2019-20054){: external}, [CVE-2019-20095](https://nvd.nist.gov/vuln/detail/CVE-2019-20095){: external}, [CVE-2019-20636](https://nvd.nist.gov/vuln/detail/CVE-2019-20636){: external}, [CVE-2020-1749](https://nvd.nist.gov/vuln/detail/CVE-2020-1749){: external}, [CVE-2020-2732](https://nvd.nist.gov/vuln/detail/CVE-2020-2732){: external}, [CVE-2020-8647](https://nvd.nist.gov/vuln/detail/CVE-2020-8647){: external}, [CVE-2020-8649](https://nvd.nist.gov/vuln/detail/CVE-2020-8649){: external}, [CVE-2020-9383](https://nvd.nist.gov/vuln/detail/CVE-2020-9383){: external}, [CVE-2020-10690](https://nvd.nist.gov/vuln/detail/CVE-2020-10690){: external}, [CVE-2020-10732](https://nvd.nist.gov/vuln/detail/CVE-2020-10732){: external}, [CVE-2020-10742](https://nvd.nist.gov/vuln/detail/CVE-2020-10742){: external}, [CVE-2020-10751](https://nvd.nist.gov/vuln/detail/CVE-2020-10751){: external}, [CVE-2020-10942](https://nvd.nist.gov/vuln/detail/CVE-2020-10942){: external}, [CVE-2020-11565](https://nvd.nist.gov/vuln/detail/CVE-2020-11565){: external}, [CVE-2020-12770](https://nvd.nist.gov/vuln/detail/CVE-2020-12770){: external}, [CVE-2020-12826](https://nvd.nist.gov/vuln/detail/CVE-2020-12826){: external}, [CVE-2020-14305](https://nvd.nist.gov/vuln/detail/CVE-2020-14305){: external}, [CVE-2019-5482](https://nvd.nist.gov/vuln/detail/CVE-2019-5482){: external}, [CVE-2019-19126](https://nvd.nist.gov/vuln/detail/CVE-2019-19126){: external}, [CVE-2020-12825](https://nvd.nist.gov/vuln/detail/CVE-2020-12825){: external}, [CVE-2019-5094](https://nvd.nist.gov/vuln/detail/CVE-2019-5094){: external}, [CVE-2019-5188](https://nvd.nist.gov/vuln/detail/CVE-2019-5188){: external}, [CVE-2019-2974](https://nvd.nist.gov/vuln/detail/CVE-2019-2974){: external}, [CVE-2020-2574](https://nvd.nist.gov/vuln/detail/CVE-2020-2574){: external}, [CVE-2020-2752](https://nvd.nist.gov/vuln/detail/CVE-2020-2752){: external}, [CVE-2020-2780](https://nvd.nist.gov/vuln/detail/CVE-2020-2780){: external}, [CVE-2020-2812](https://nvd.nist.gov/vuln/detail/CVE-2020-2812){: external}, [CVE-2019-12749](https://nvd.nist.gov/vuln/detail/CVE-2019-12749){: external}, [CVE-2019-19956](https://nvd.nist.gov/vuln/detail/CVE-2019-19956){: external}, [CVE-2019-20388](https://nvd.nist.gov/vuln/detail/CVE-2019-20388){: external}, [CVE-2020-7595](https://nvd.nist.gov/vuln/detail/CVE-2020-7595){: external}, [CVE-2020-10754](https://nvd.nist.gov/vuln/detail/CVE-2020-10754){: external}, [CVE-2019-11719](https://nvd.nist.gov/vuln/detail/CVE-2019-11719){: external}, [CVE-2019-11727](https://nvd.nist.gov/vuln/detail/CVE-2019-11727){: external}, [CVE-2019-11756](https://nvd.nist.gov/vuln/detail/CVE-2019-11756){: external}, [CVE-2019-17006](https://nvd.nist.gov/vuln/detail/CVE-2019-17006){: external}, [CVE-2019-17023](https://nvd.nist.gov/vuln/detail/CVE-2019-17023){: external}, [CVE-2020-6829](https://nvd.nist.gov/vuln/detail/CVE-2020-6829){: external}, [CVE-2020-12400](https://nvd.nist.gov/vuln/detail/CVE-2020-12400){: external}, [CVE-2020-12401](https://nvd.nist.gov/vuln/detail/CVE-2020-12401){: external}, [CVE-2020-12402](https://nvd.nist.gov/vuln/detail/CVE-2020-12402){: external}, [CVE-2020-12403](https://nvd.nist.gov/vuln/detail/CVE-2020-12403){: external}, [CVE-2018-20843](https://nvd.nist.gov/vuln/detail/CVE-2018-20843){: external}, [CVE-2019-15903](https://nvd.nist.gov/vuln/detail/CVE-2019-15903){: external}, [CVE-2019-14834](https://nvd.nist.gov/vuln/detail/CVE-2019-14834){: external}, [CVE-2019-11068](https://nvd.nist.gov/vuln/detail/CVE-2019-11068){: external}, [CVE-2019-18197](https://nvd.nist.gov/vuln/detail/CVE-2019-18197){: external}, [CVE-2019-16935](https://nvd.nist.gov/vuln/detail/CVE-2019-16935){: external}, [CVE-2019-20386](https://nvd.nist.gov/vuln/detail/CVE-2019-20386){: external}, [CVE-2019-17498](https://nvd.nist.gov/vuln/detail/CVE-2019-17498){: external}, and [CVE-2020-14365](https://nvd.nist.gov/vuln/detail/CVE-2020-14365){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.38_1541_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.38_1541_openshift, released 30 September 2020
{: #4338_1541}

The following table shows the changes that are included in the worker node fix pack update `4.3.38_1541_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Automation for provisioning and reloading | N/A	| N/A | Fixes an issue that prevented SDS worker nodes with unified extensible firmware interface (UEFI) bootstrapping from provisioning or reloading.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.38_1540_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.38_1540_openshift, released 28 September 2020
{: #4338_1540}

The following table shows the changes that are included in the worker node fix pack update `4.3.38_1540_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.3.35	| 4.3.38 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-38){: external}. The update resolves CVE-2020-8557 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6343881){: external}).|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.35_1538_openshift" caption-side="top"}

### Changelog for master fix pack 4.3.35_1539_openshift, released 21 September 2020
{: #4335_1539}

The following table shows the changes that are included in the master fix pack patch update `4.3.35_1539_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster health image | v1.1.9 | v1.1.11 | Updated `Go` version for [CVE-2020-16845](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-16845){: external} and [CVE-2020-24553](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24553){: external}. |
| etcd | v3.4.10 | v3.4.13 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.13){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.11-1 | v1.17.12-1 | Updated to support the Kubernetes 1.17.12 release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 377 | 378 | Updated `Go` version for [CVE-2020-16845](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-16845){: external}. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | d80b738 | 4b47693 | Updated `Go` version for [CVE-2020-16845](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-16845){: external} and image for [CVE-2020-14352](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14352){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.3.0-20200709 | v4.3.0-20200821 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.3.0+20200821){: external}. |
| {{site.data.keyword.openshiftshort}} | 4.3.31 | 4.3.35 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-35){: external}. |
| OpenVPN Operator image | v1.0.7 | v1.0.8 | Updated image for [CVE-2020-14352](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14352){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.3.0+20200709 | 4.3.0+20200821 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.3.0+20200821){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.35_1538_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.35_1538_openshift, released 14 September 2020
{: #4335_1538}

The following table shows the changes that are included in the worker node fix pack update `4.3.35_1538_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.3.33 | 4.3.35 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-35){: external}.|
| RHEL 7 packages | N/A | N/A | Updated worker node image with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.33_1537_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.33_1537_openshift, released 31 August 2020
{: #4333_1537}

The following table shows the changes that are included in the worker node fix pack update `4.3.33_1537_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Master proxy | 1.8.25-384f42 | 1.8.26-561f1a | See the [HAProxy changelogs](https://www.haproxy.org/download/1.8/src/CHANGELOG){: external}. |
| {{site.data.keyword.openshiftshort}} | 4.3.31 | 4.3.33 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-33){: external}.|
| RHEL 7 packages |  3.10.0-1127.18.2.el7 | 3.10.0-1127.19.1.el7 | Updated worker node image with kernel and package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.31_1534_openshift" caption-side="top"}

### Changelog for master fix pack 4.3.31_1536_openshift, released 21 August 2020
{: #4331_1536}

The following table shows the changes that are included in the master fix pack patch update `4.3.31_1536_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster master operations | N/A | N/A | Fixed a problem that might cause cluster master operations to fail for clusters with a private cloud service endpoint enabled. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.9-1 | v1.17.11-1 | Updated to support the Kubernetes 1.17.11 release and to use `Go` version 1.13.15. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.31_1534_openshift" caption-side="top"}

### Changelog for master fix pack 4.3.31_1534_openshift, released 18 August 2020
{: #4331_1534_master}

The following table shows the changes that are included in the master fix pack patch update `4.3.31_1534_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster health image | v1.1.8 | v1.1.9 | Updated to use `Go` version 1.13.13. |
| Cluster master operations | N/A | N/A | Cluster master update operations are now canceled if a broken [Kubernetes admission webhook](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/){: external} is detected. |
| etcd | v3.4.9 | v3.4.10 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.10){: external}.|
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | 1.17 | 1.17.1 | Updated to use `Go` version 1.13.8. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 375 | 377 | Fixed a bug that prevents persistent volume claim (PVC) creation failures from being retried. Updated to use `Go` version 1.13.8. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 8882606 | d80b738 | Updated image for [CVE-2020-12049](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-12049){: external} and to use `Go` version 1.13.14. |
| Kubernetes configuration | N/A | N/A | The Kubernetes API server audit policy configuration is updated to include auditing of all API groups except `apiregistration.k8s.io` and `coordination.k8s.io`. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.3.0-20200615 | v4.3.0-20200709 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.3.0+20200709){: external}. |
| {{site.data.keyword.openshiftshort}} | 4.3.28 | 4.3.31 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-31){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | v4.3.0+20200615 | v4.3.0+20200709 | See the [{{site.data.keyword.openshiftlong_notm}}toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.3.0+20200709){: external}. |
| OpenVPN Operator image | v1.0.6 | v1.0.7 | Updated image for [CVE-2020-12049](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-12049){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.29_1533_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.31_1534_openshift, released 17 August 2020
{: #4331_1534}

The following table shows the changes that are included in the worker node fix pack update `4.3.31_1534_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.3.29 | 4.3.31 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-31){: external}. The update resolves CVE-2020-8558 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6319989){: external}).|
| RHEL 7 packages | N/A | N/A | Updated worker node images with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.29_1533_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.29_1533_openshift, released 3 August 2020
{: #4329_1533}

The following table shows the changes that are included in the worker node fix pack update `4.3.29_1533_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1127.13.1.el7 | 3.10.0-1127.18.2.el7 | Updated worker node images with package updates for [CVE-2020-10713](https://nvd.nist.gov/vuln/detail/CVE-2020-10713){: external}, [CVE-2020-14308](https://nvd.nist.gov/vuln/detail/CVE-2020-14308){: external}, [CVE-2020-14309](https://nvd.nist.gov/vuln/detail/CVE-2020-14309){: external}, [CVE-2020-14310](https://nvd.nist.gov/vuln/detail/CVE-2020-14310){: external}, [CVE-2020-14311](https://nvd.nist.gov/vuln/detail/CVE-2020-14311){: external}, [CVE-2020-15705](https://nvd.nist.gov/vuln/detail/CVE-2020-15705){: external}, [CVE-2020-15706](https://nvd.nist.gov/vuln/detail/CVE-2020-15706){: external}, [CVE-2020-15707](https://nvd.nist.gov/vuln/detail/CVE-2020-15707){: external}, [CVE-2019-19527](https://nvd.nist.gov/vuln/detail/CVE-2019-19527){: external}, [CVE-2020-10757](https://nvd.nist.gov/vuln/detail/CVE-2020-10757){: external}, [CVE-2020-12653](https://nvd.nist.gov/vuln/detail/CVE-2020-12653){: external}, and [CVE-2020-12654](https://nvd.nist.gov/vuln/detail/CVE-2020-12654){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.29_1532_openshift" caption-side="top"}

### Changelog for master fix pack 4.3.28_1532_openshift, released 20 July 2020
{: #4328_1532}

The following table shows the changes that are included in the master fix pack update `4.3.28_1532_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Block Storage driver configuration | N/A | N/A | Updated the pod CPU and memory requests and limits. |
| IBM Calico extension | 353 | 378 | Updated to handle any `ens` network interface. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.7-1 | v1.17.9-1 | Updated to support the Kubernetes 1.17.9 release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor configuration | N/A | N/A | Added a pod memory limit. |
| {{site.data.keyword.cloud_notm}} RBAC operator | 08ce50e | 8882606 | Updated image for [CVE-2020-13777](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13777){: external} and to use `Go` version 1.13.12. |
| Kubernetes configuration | N/A | N/A | The Kubernetes API server audit policy configuration is updated to include auditing the `apiextensions.k8s.io`, `operator.tigera.io` and `scheduling.k8s.io` API groups and the `crd.projectcalico.org`, `persistentvolumeclaims`, `persistentvolumes` and `tokenreviews` resources. |
| {{site.data.keyword.openshiftshort}} | 4.3.23 | 4.3.28 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-28){: external}. The update resolves CVE-2020-8555 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6249891){: external}). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.27_1528_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.29_1532_openshift, released 20 July 2020
{: #4329_1532}

The following table shows the changes that are included in the worker node fix pack update `4.3.29_1532_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Master Proxy | 2.0.15-afe432 | 1.8.25-384f42 | See the [HAProxy changelogs](https://www.haproxy.org/download/1.8/src/CHANGELOG){: external}. Fixes a connection leak that happens when HAProxy is under high load. |
| RHEL 7 Packages |  N/A | N/A | Updated worker node images with package updates for [CVE-2020-12049](https://nvd.nist.gov/vuln/detail/CVE-2020-12049){: external}.|
| {{site.data.keyword.openshiftshort}} | 4.3.27 | 4.3.29 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-29){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.27_1528_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.27_1528_openshift, released 6 July 2020
{: #4327_1528}

The following table shows the changes that are included in the worker node fix pack update `4.3.27_1528_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Master Proxy | 1.8.25-30b675 | 2.0.15-afe432 | See the [HAProxy changelogs](https://www.haproxy.org/download/2.0/src/CHANGELOG){: external}. |
| RHEL 7 Packages | 3.10.0-1127.10.1.el7 | 3.10.0-1127.13.1.el7 | Updated worker node images with kernel package updates for [CVE-2020-10749](https://nvd.nist.gov/vuln/detail/CVE-2020-10749){: external}, [CVE-2020-1702](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1702){: external}, [CVE-2016-8867](https://nvd.nist.gov/vuln/detail/CVE-2016-8867){: external}, [CVE-2020-14298](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14298){: external}, [CVE-2020-14300](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14300){: external}, [CVE-2020-12888](https://nvd.nist.gov/vuln/detail/CVE-2020-12888){: external}, [CVE-2020-11868](https://nvd.nist.gov/vuln/detail/CVE-2020-11868){: external}, and [CVE-2020-13817](https://nvd.nist.gov/vuln/detail/CVE-2020-13817){: external}. |
| {{site.data.keyword.openshiftshort}} | 4.3.25 | 4.3.27 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-27){: external}. |
| Worker node `drain` automation | N/A | N/A | Fixes a race condition that can cause worker node `drain` automation to fail. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.25_1527_openshift" caption-side="top"}

### Changelog for master fix pack 4.3.23_1527_openshift and worker node fix pack 4.3.25_1527_openshift, released 22 June 2020
{: #4323_1527_master}

The following table shows the changes that are included in the master fix pack update `4.3.23_1527_openshift` and in worker node fix pack update `4.3.25_1527_openshift`. Master patch updates are applied automatically. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node. For more information, see [Update types](/docs/openshift?topic=openshift-openshift_versions#openshift_update_types).
{: shortdesc}

| Component | Location | Previous | Current | Description |
| --------- | -------- | ------- | -------- | ----------- |
| Cluster health image | Master | v1.1.7 | v1.1.8 | Improved performance when handling cluster status updates. |
| CRI-O | Worker | 1.16.5 | 1.16.6 | See [CRI-O changelogs](https://github.com/cri-o/cri-o/releases/tag/v1.16.6){: external}. |
| Gateway-enabled cluster controller | Master | N/A | N/A | Added missing Calico `deny-public-nodeport` global network policy for gateway-enabled clusters. |
| {{site.data.keyword.cloud_notm}} Controller Manager | Master | v1.17.6-4 | v1.17.7-1 | Updated to support the Kubernetes 1.17.7 release. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | Master | N/A | 08ce50e | **New!**: Added a control plane operator to synchronize [{{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) service access roles](/docs/openshift?topic=openshift-access_reference#service) with Kubernetes role-based access control (RBAC) roles. |
| {{site.data.keyword.openshiftshort}} | Worker | 4.3.23 | 4.3.25 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-25){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | Master | bc493d4 | v4.3.0-20200615 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.3.0+20200615){: external}. |
| RHEL 7 packages | Worker | N/A | N/A | Updated worker node images with package updates for [CVE-2020-0543](https://nvd.nist.gov/vuln/detail/CVE-2020-0543){: external}, [CVE-2020-0548](https://nvd.nist.gov/vuln/detail/CVE-2020-0548){: external}, and [CVE-2020-0549](https://nvd.nist.gov/vuln/detail/CVE-2020-0549){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | Master | v4.3.0+20200603 | v4.3.0+20200615 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.3.0+20200615){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is where the component is located, the master, worker node, or both. The third column is the previous version number of the component. The fourth column is the current version number of the component. The fifth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.23_1525_openshift" caption-side="top"}

### Changelog for master fix pack 4.3.23_1525_openshift, released 16 June 2020
{: #4323_1525}

The following table shows the changes that are included in the master fix pack update `4.3.23_1525_openshift`. Master patch updates are applied automatically. For more information, see [Update types](/docs/openshift?topic=openshift-openshift_versions#openshift_update_types).
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico operator | N/A | N/A | The component deployment now uses the `Recreate` update strategy. |
| Cluster health image | v1.1.5 | v1.1.7 | Additional status information is included when an add-on health state is `critical`. |
| etcd | v3.4.7 | v3.4.9 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.9){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | 1.16 | 1.17 | Added support for block storage encryption. Additionally, the plug-in now sets the container memory limit. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.6-1 | v1.17.6-4 | Calico global network policies are now created for version 2.0 private network load balancers (NLBs). Updated to use `calicoctl` version 3.12.2. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 373 | 375 | Fixed a bug that might cause error handling to create additional persistent volumes. |
| {{site.data.keyword.openshiftshort}} | 4.3.19 | 4.3.23 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-23){: external}. Updated the {{site.data.keyword.cloud_notm}} command line tools documentation in the {{site.data.keyword.openshiftshort}} web console. |
| {{site.data.keyword.openshiftshort}} HyperShift toolkit | bc493d4 | N/A | This component is replaced by the {{site.data.keyword.openshiftlong_notm}} toolkit component. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | N/A | 4.3.0+20200603 | **New!**: See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.3.0+20200603){: external}. This component replaces the {{site.data.keyword.openshiftshort}} HyperShift toolkit component. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.23_1524_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.23_1524_openshift, released 8 June 2020
{: #4323_1524}

The following table shows the changes that are included in the worker node fix pack update `4.3.23_1524_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1127.8.2.el7 | 3.10.0-1127.10.1.el7 | Updated worker node images with kernel package updates for [CVE-2020-8616](https://nvd.nist.gov/vuln/detail/CVE-2020-8616){: external} and [CVE-2020-8617](https://nvd.nist.gov/vuln/detail/CVE-2020-8617){: external}. |
| {{site.data.keyword.openshiftshort}} | 4.3.21 | 4.3.23 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-23){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.21_1523_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.21_1523_openshift, released 26 May 2020
{: #4321_1523}

The following table shows the changes that are included in the worker node fix pack update `4.3.21_1523_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1127.el7 | 3.10.0-1127.8.2.el7 | Updated worker node images with kernel package updates for [CVE-2017-18595](https://nvd.nist.gov/vuln/detail/CVE-2017-18595){: external}, [CVE-2019-19768](https://nvd.nist.gov/vuln/detail/CVE-2019-19768){: external}, and [CVE-2020-10711](https://nvd.nist.gov/vuln/detail/CVE-2020-10711){: external}. |
| {{site.data.keyword.openshiftshort}} | 4.3.18 | 4.3.21 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-21){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.13_1521_openshift" caption-side="top"}

### Changelog for master fix pack 4.3.19_1523_openshift, released 26 May 2020
{: #4319_1523}

The following table shows the changes that are included in the master fix pack update `4.3.19_1523_openshift`. Master patch updates are applied automatically. For more information, see [Update types](/docs/openshift?topic=openshift-openshift_versions#openshift_update_types).
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.12.0 | v3.13.3 | See the [Calico release notes](https://docs.projectcalico.org/releases){: external}. |
| Calico Operator | v1.1.1 | v1.3.4 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.3.4){: external}. |
| Cluster health image | v1.1.4 | v1.1.5 | Cluster health state now includes Ingress health. |
| IBM Calico extension | 349 | 353 | Skips creating a Calico host endpoint when no endpoint is needed.|
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.5-1 | v1.17.6-1 | Updated to support the Kubernetes 1.17.6 release. Updated network load balancer (NLB) events to use the latest {{site.data.keyword.cloud_notm}} troubleshooting documentation. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 371 | 373 | Image updated for [CVE-2020-11655](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-11655){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 206 | 208 | Version 2.0 network load balancers (NLB) were updated to cleanup unnecessary IPVS rules. |
| {{site.data.keyword.openshiftshort}} | 4.3.18 | 4.3.19 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-19){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.18_1522_openshift" caption-side="top"}

### Changelog for master fix pack 4.3.18_1522_openshift, released 12 May 2020
{: #4318_1522}

The following table shows the changes that are included in the master fix pack update `4.3.18_1522_openshift`. Master patch updates are applied automatically. For more information, see [Update types](/docs/openshift?topic=openshift-openshift_versions#openshift_update_types).
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.0 | v1.1.4 | When cluster add-ons do not support the current cluster version, a warning is now returned in the cluster health state. |
| etcd | v3.4.3 | v3.4.7 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.7){: external}. |
| Gateway-enabled cluster controller | 1045 | 1082 | Updated image for [CVE-2020-1967](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1967){: external}. |
| IBM Calico extension | 320 | 349 | Updated image for [CVE-2020-1967](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1967){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.4-3 | v1.17.5-1 | Updated to support the Kubernetes 1.17.5 release and to use `Go` version `1.13.9`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 358 | 371 | Updated image for [CVE-2020-1967](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1967){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 177 | 206 | Improved application logging. Updated image for [CVE-2020-1967](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1967){: external}. |
| {{site.data.keyword.openshiftshort}} | 4.3.12-x86_64 | 4.3.18-x86_64 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html){: external}. |
| {{site.data.keyword.openshiftshort}} Console configuration | N/A | N/A | Fixed a problem that might leave the {{site.data.keyword.openshiftshort}} Console inaccessible after a cluster master operation. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | 3b3ff62 | bc493d4 | See the [{{site.data.keyword.openshiftshort}} HyperShift toolkit repository](https://github.com/openshift/hypershift-toolkit/commit/bc493d4b51ea7d3d8e60453dee2407baf03e1c6d){: external}. Removed incorrect notifications about available cluster updates that referred to OpenShift Container Platform versions instead of {{site.data.keyword.openshiftlong_notm}} versions. |
| {{site.data.keyword.openshiftshort}} HyperShift toolkit | 3b3ff62 | bc493d4 | See the [{{site.data.keyword.openshiftshort}} HyperShift toolkit repository](https://github.com/openshift/hypershift-toolkit/commit/bc493d4b51ea7d3d8e60453dee2407baf03e1c6d){: external}. Removed incorrect notifications about available cluster updates that referred to OpenShift Container Platform versions instead of {{site.data.keyword.openshiftlong_notm}} versions. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.13_1521_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.14_1522_openshift, released 11 May 2020
{: #4314_1522}

The following table shows the changes that are included in the worker node fix pack update `4.3.13_1522_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| CRI-O | 1.16.5 | 1.16.6 | See the [CRI-O changelogs](https://github.com/cri-o/cri-o/releases/tag/v1.16.6){: external}. |
| {{site.data.keyword.openshiftshort}} | 4.3.13 | 4.3.18 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-18){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.13_1521_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.3.13_1521_openshift, released 27 April 2020
{: #4313_1521}

The following table shows the changes that are included in the worker node fix pack update `4.3.13_1521_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| CRI-O | 1.16.4 | 1.16.5 | See the [CRI-O changelogs](https://github.com/cri-o/cri-o/releases/tag/v1.16.5){: external}. |
| HA proxy | 1.8.25-30b675 | 1.8.25-adb65d | Update addresses [CVE-2020-1967](https://nvd.nist.gov/vuln/detail/CVE-2020-1967){: external}. |
| {{site.data.keyword.openshiftshort}} | 4.3.10 | 4.3.13 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-13){: external}. |
| RHEL 7 Packages | N/A | N/A | Updated worker node images with package updates for [CVE-2019-19921](https://nvd.nist.gov/vuln/detail/CVE-2019-19921){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.10_1518_openshift" caption-side="top"}

### Changelog for master fix pack 4.3.12_1520_openshift and worker node fix pack 4.3.10_1518_openshift, released 20 April 2020
{: #4312_1520_master}

The following table shows the changes that are included in the master fix pack update `4.3.12_1520_openshift` and in worker node fix pack update `4.3.10_1518_openshift`. Master patch updates are applied automatically. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node. For more information, see [Update types](/docs/openshift?topic=openshift-openshift_versions#openshift_update_types).
{: shortdesc}

| Component | Location | Previous | Current | Description |
| --------- | -------- | ------- | -------- | ----------- |
| Calico | Master | v3.8.6 | v3.12.0 | See the [Calico release notes](https://docs.projectcalico.org/release-notes/){: external}. In addition, the Calico configuration was updated to use the [Kubernetes API datastore driver](https://docs.projectcalico.org/getting-started/kubernetes/hardway/the-calico-datastore){: external}. |
| Calico operator | Master | N/A | v1.1.1 | **New!:** Added the Calico operator to manage the lifecycle of the Calico installation. See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.1.1){: external}. |
| CRI-O | Worker | 1.11 | 1.16.4 | See the [CRI-O release notes](https://github.com/cri-o/cri-o/releases/tag/v1.16.4){: external}. |
| etcd | Master | v3.3.18 | v3.4.3 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.3){: external}. |
| Gateway-enabled cluster controller | Master | N/A | 1045 | **New!:** For [classic clusters with a gateway enabled](/docs/containers?topic=containers-clusters#gateway_cluster_cli), a `DaemonSet` is installed on each worker node to configure settings for routing network traffic to worker nodes. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | Master | 1.15.4 | 1.16 | Updated to `Go` version 1.13.8 and to set container resource requests and limits. |
| IBM Calico extension | Master | N/A | 320 | **New!:** Added a Calico node init container that creates Calico private host endpoints for worker nodes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | Master | v1.15.10-252 | v1.17.4-3 | The {{site.data.keyword.cloud_notm}} Controller Manager component replaces the {{site.data.keyword.cloud_notm}} Provider component by moving the {{site.data.keyword.cloud_notm}} controllers from the Kubernetes [kube-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#kube-controller-manager){: external} to the [cloud-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#cloud-controller-manager){: external}) component. The {{site.data.keyword.cloud_notm}} Controller Manager is updated to support the Kubernetes 1.17.4 release, to use `distroless/static` base image version `c6d59815`, `Go` version 1.13.8, and `calicoctl` version 3.12.1. Finally, the {{site.data.keyword.cloud_notm}} Controller Manager updated version 1.0 and 2.0 network load balancers (NLBs) to prefer scheduling NLB pods on worker nodes that do not currently run any NLB pods. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | Master | 169 | 177 | Version 2.0 network load balancers (NLBs) were updated to fix problems with long-lived network connections to endpoints that failed readiness probes. |
| {{site.data.keyword.openshiftshort}} | Master | 3.11.170 | 4.3.12 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html){: external}. |
| {{site.data.keyword.openshiftshort}} | Worker | 3.11.170 | 4.3.10 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | Master | N/A | 3b3ff62 | **New!:** Added a toolkit to enable running {{site.data.keyword.openshiftshort}} version 4 with a managed control plane. For more information, see the [{{site.data.keyword.openshiftshort}} HyperShift toolkit repository](https://github.com/openshift/hypershift-toolkit/commit/3b3ff6269b1c71ffa4a0598f7969aad6f7e4eb20). |
| {{site.data.keyword.openshiftshort}} HyperShift toolkit | Master | N/A | 3b3ff62 | **New!:** Added a toolkit to enable running {{site.data.keyword.openshiftshort}} version 4 with a managed control plane. For more information, see the [{{site.data.keyword.openshiftshort}} HyperShift toolkit repository](https://github.com/openshift/hypershift-toolkit/commit/3b3ff6269b1c71ffa4a0598f7969aad6f7e4eb20). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is where the component is located: the master, worker node, or both. The third column is the previous version number of the component. The fourth column is the current version number of the component. The fifth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.170" caption-side="top"}