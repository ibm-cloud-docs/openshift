---

copyright:
  years: 2014, 2020
lastupdated: "2020-11-09"

keywords: openshift, roks, rhoks, rhos, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
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
{:java: #java .ph data-hd-programlang='java'}
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
{:swift: #swift .ph data-hd-programlang='swift'}
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
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}



# Version changelog
{: #openshift_changelog}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters. Changes include updates to {{site.data.keyword.openshiftshort}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

Unless otherwise noted in the changelogs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.openshiftshort}} APIs and features that are at beta. {{site.data.keyword.openshiftshort}} alpha features, which are subject to change, are disabled.

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security) for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Changelog entries that address other security vulnerabilities but do not also refer to an IBM security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.openshiftshort}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}

## Version 4.5 changelog
{: #version-45}

Review the changelogs for {{site.data.keyword.openshiftlong_notm}} version 4.5 patch updates.
{: shortdesc}

### Changelog for worker node fix pack 4.5.17_1519_openshift, released 9 November 2020
{: #4517_1519}

The following table shows the changes that are included in the worker node fix pack update `4.5.17_1519_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.5.15 | 4.5.17 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-17){: external}.|
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates for [CVE-2020-15999](https://nvd.nist.gov/vuln/detail/CVE-2020-15999){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.5.15_1518_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.5.15_1518_openshift, released 26 October 2020
{: #4515_1518_worker}

The following table shows the changes that are included in the worker node fix pack update `4.5.15_1518_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.5.13 | 4.5.15 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-15){: external}.|
| RHEL 7 Packages | 3.10.0-1160.2.1.el7 | 3.10.0-1160.2.2.el7 | Updated worker node images with kernel and package updates for [CVE-2020-12351](https://nvd.nist.gov/vuln/detail/CVE-2020-12351){: external} and [CVE-2020-12352](https://nvd.nist.gov/vuln/detail/CVE-2020-12352){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.5.13_1515_openshift" caption-side="top"}

### Changelog for master fix pack 4.5.15_1518_openshift, released 26 October 2020
{: #4515_1518}

The following table shows the changes that are included in the master fix pack patch update `4.5.15_1518_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster health image | v1.2.1 | v1.2.2 | Fixed the cluster health status for when add-on customizations are used. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.18.9-2 | v1.18.10-1 | Updated to support the Kubernetes 1.18.10 release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 378 | 379 | Updated to use the universal base image (UBI) and to use `Go` version 1.15.2. |
| Kubernetes configuration | N/A | N/A | [Kubernetes service account token volume projection](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#service-account-token-volume-projection){: external} is enabled and issues tokens that use `https://kubernetes.default.svc` as the default API audience. |
| {{site.data.keyword.openshiftshort}} | 4.5.13 | 4.5.15 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-15){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.5.0-20201009 | v4.5.0-20201022 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201022){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.5.0-20201009 | v4.5.0-20201022 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201022){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.5.0+20201009 | 4.5.0+20201022 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201022){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.5.13_1515_openshift" caption-side="top"}

### Changelog for 4.5.13_1515_openshift, released 13 October 2020
{: #4513_1515}

The following table shows the changes that are included in the `4.5.13_1515_openshift` version update.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.13.3 | v3.16.1 | See the [Calico release notes](https://docs.projectcalico.org/releases){: external}. In addition, Calico pods in the `calico-system` namespace now set CPU and memory requests. |
| Calico Operator | v1.3.4 | v1.10.3 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.10.3){: external}. |
| Cluster health image | v1.1.11 | v1.2.1 | When a cluster has a Kubernetes key management service (KMS) provider enabled and a disabled [{{site.data.keyword.keymanagementserviceshort}}](/docs/containers?topic=containers-encryption#keyprotect) key, a warning is now returned in the cluster health state. Fixed check to determine if an add-on is unsupported. In addition, updated to use `Go` version 1.15.2.  |
| Cluster master HA configuration | N/A | N/A | Updated configuration to improve availability during cluster master operations. |
| Gateway-enabled cluster controller | 1082 | 1105 | Updated to use `Go` version 1.15.2. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | 1.17.1 | 1.17.2 | Updated to use `Go` version 1.13.15. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.12-1 | v1.18.9-2 | Updated to support the Kubernetes 1.18.9 release and to use `calicoctl` version 3.13.4. Updated network load balancer (NLB) events to use the latest {{site.data.keyword.cloud_notm}} troubleshooting documentation.  For VPC load balancers, the `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "proxy-protocol"` annotation was added to preserve the source IP address of requests to apps in your cluster. |
|{{site.data.keyword.cloud_notm}} RBAC Operator | 4b47693 | 31c794a | Updated to use `Go` version 1.15.2. |
| Key Management Service provider | v2.0.4 | v2.1.0 | Updated to use the key management service (KMS) provider secret to identify when a [{{site.data.keyword.keymanagementserviceshort}}](/docs/containers?topic=containers-encryption#keyprotect) key is enabled and disabled so that encryption and decryption requests are updated accordingly.  |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 208 | 234 | Improved startup performance of version 2.0 private network load balancers (NLBs). Updated to use `Go` version 1.15.2. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.4.0-20200821 | v4.5.0-20201009 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201009){: external}. |
| {{site.data.keyword.openshiftshort}} | 4.4.20 | 4.5.13 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-13){: external}. |
| {{site.data.keyword.openshiftshort}} configuration | N/A | N/A | New version 4.5 clusters that run on the VPC Gen 2 infrastructure provider and use {{site.data.keyword.cos_full_notm}} now proxy container image traffic through the internal registry pods directly to the {{site.data.keyword.cos_short}} endpoints. To configure this proxying for version 4.5 clusters that were updated from a previous version, see [the troubleshooting topic](/docs/openshift?topic=openshift-cs_troubleshoot_app#ts-app-ocr-vpc-push). |
| OpenVPN Operator image | v1.0.8 | v1.0.9 | Updated to improve OpenVPN availability. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | N/A | v4.5.0-20201009 | **New!**: {{site.data.keyword.openshiftlong_notm}} now provides custom cluster metrics. See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201009){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.4.0+20200821 | 4.5.0+20201009 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201009){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.4.20_1518_openshift" caption-side="top"}

## Version 4.4 changelog
{: #version-44}

Review the changelogs for {{site.data.keyword.openshiftlong_notm}} version 4.4 patch updates.
{: shortdesc}

### Changelog for worker node fix pack 4.4.29_1524_openshift, released 9 November 2020
{: #4429_1524}

The following table shows the changes that are included in the worker node fix pack update `4.4.29_1524_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.4.27 | 4.4.29 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-29){: external}.|
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates for [CVE-2020-15999](https://nvd.nist.gov/vuln/detail/CVE-2020-15999){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.4.27_1523_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.4.27_1523_openshift, released 26 October 2020
{: #4427_1523_worker}

The following table shows the changes that are included in the worker node fix pack update `4.4.27_1523_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.4.26 | 4.4.27 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-27){: external}.|
| RHEL 7 Packages | 3.10.0-1160.2.1.el7 | 3.10.0-1160.2.2.el7 | Updated worker node images with kernel and package updates for [CVE-2020-12351](https://nvd.nist.gov/vuln/detail/CVE-2020-12351){: external} and [CVE-2020-12352](https://nvd.nist.gov/vuln/detail/CVE-2020-12352){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.4.26_1521_openshift" caption-side="top"}

### Changelog for master fix pack 4.4.27_1523_openshift, released 26 October 2020
{: #4427_1523}

The following table shows the changes that are included in the master fix pack patch update `4.4.27_1523_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster health image | v1.1.11 | v1.1.12 | Fixed check for unsupported add-ons. Updated to use `Go` version 1.15.2. |
| Gateway-enabled cluster controller | 1082 | 1105 | Updated to use `Go` version 1.15.2. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | 1.17.1 | 1.17.2 | Updated to use `Go` version 1.13.15. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.12-1 | v1.17.13-1 | Updated to support the Kubernetes 1.17.13 release. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 4b47693 | 31c794a | Updated to use `Go` version 1.15.2. |
| {{site.data.keyword.openshiftshort}} | 4.4.20 | 4.4.27 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-27){: external}. |
| {{site.data.keyword.openshiftshort}} configuration | N/A | N/A | New version 4.4 clusters that run on the VPC Gen 2 infrastructure provider and use {{site.data.keyword.cos_full_notm}} now proxy container image traffic through the internal registry pods directly to the {{site.data.keyword.cos_short}} endpoints. To configure this proxying for existing version 4.4 clusters, see [the troubleshooting topic](/docs/openshift?topic=openshift-cs_troubleshoot_app#ts-app-ocr-vpc-push). |
| OpenVPN Operator image | v1.0.8 | v1.0.9 | Updated to improve OpenVPN availability. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.4.20_1518_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.4.26_1521_openshift, released 12 October 2020
{: #4426_1521}

The following table shows the changes that are included in the worker node fix pack update `4.4.26_1521_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.4.23 | 4.4.26 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-4-26){: external}. |
| RHEL 7 Packages | 3.10.0-1127.19.1.el7 | 3.10.0-1160.2.1.el7 | Updated worker node image with kernel and package updates for: [CVE-2019-12450](https://nvd.nist.gov/vuln/detail/CVE-2019-12450){: external}, [CVE-2019-14822](https://nvd.nist.gov/vuln/detail/CVE-2019-14822){: external}, [CVE-2020-12243](https://nvd.nist.gov/vuln/detail/CVE-2020-12243){: external}, [CVE-2019-14866](https://nvd.nist.gov/vuln/detail/CVE-2019-14866){: external}, [CVE-2017-12652](https://nvd.nist.gov/vuln/detail/CVE-2017-12652){: external}, [CVE-2017-18551](https://nvd.nist.gov/vuln/detail/CVE-2017-18551){: external}, [CVE-2018-20836](https://nvd.nist.gov/vuln/detail/CVE-2018-20836){: external}, [CVE-2019-9454](https://nvd.nist.gov/vuln/detail/CVE-2019-9454){: external}, [CVE-2019-9458](https://nvd.nist.gov/vuln/detail/CVE-2019-9458){: external}, [CVE-2019-12614](https://nvd.nist.gov/vuln/detail/CVE-2019-12614){: external}, [CVE-2019-15217](https://nvd.nist.gov/vuln/detail/CVE-2019-15217){: external}, [CVE-2019-15807](https://nvd.nist.gov/vuln/detail/CVE-2019-15807){: external}, [CVE-2019-15917](https://nvd.nist.gov/vuln/detail/CVE-2019-15917){: external}, [CVE-2019-16231](https://nvd.nist.gov/vuln/detail/CVE-2019-16231){: external}, [CVE-2019-16233](https://nvd.nist.gov/vuln/detail/CVE-2019-16233){: external}, [CVE-2019-16994](https://nvd.nist.gov/vuln/detail/CVE-2019-16994){: external}, [CVE-2019-17053](https://nvd.nist.gov/vuln/detail/CVE-2019-17053){: external}, [CVE-2019-17055](https://nvd.nist.gov/vuln/detail/CVE-2019-17055){: external}, [CVE-2019-18808](https://nvd.nist.gov/vuln/detail/CVE-2019-18808){: external}, [CVE-2019-19046](https://nvd.nist.gov/vuln/detail/CVE-2019-19046){: external}, [CVE-2019-19055](https://nvd.nist.gov/vuln/detail/CVE-2019-19055){: external}, [CVE-2019-19058](https://nvd.nist.gov/vuln/detail/CVE-2019-19058){: external}, [CVE-2019-19059](https://nvd.nist.gov/vuln/detail/CVE-2019-19059){: external}, [CVE-2019-19062](https://nvd.nist.gov/vuln/detail/CVE-2019-19062){: external}, [CVE-2019-19063](https://nvd.nist.gov/vuln/detail/CVE-2019-19063){: external}, [CVE-2019-19332](https://nvd.nist.gov/vuln/detail/CVE-2019-19332){: external}, [CVE-2019-19447](https://nvd.nist.gov/vuln/detail/CVE-2019-19447){: external}, [CVE-2019-19523](https://nvd.nist.gov/vuln/detail/CVE-2019-19523){: external}, [CVE-2019-19524](https://nvd.nist.gov/vuln/detail/CVE-2019-19524){: external}, [CVE-2019-19530](https://nvd.nist.gov/vuln/detail/CVE-2019-19530){: external}, [CVE-2019-19534](https://nvd.nist.gov/vuln/detail/CVE-2019-19534){: external}, [CVE-2019-19537](https://nvd.nist.gov/vuln/detail/CVE-2019-19537){: external}, [CVE-2019-19767](https://nvd.nist.gov/vuln/detail/CVE-2019-19767){: external}, [CVE-2019-19807](https://nvd.nist.gov/vuln/detail/CVE-2019-19807){: external}, [CVE-2019-20054](https://nvd.nist.gov/vuln/detail/CVE-2019-20054){: external}, [CVE-2019-20095](https://nvd.nist.gov/vuln/detail/CVE-2019-20095){: external}, [CVE-2019-20636](https://nvd.nist.gov/vuln/detail/CVE-2019-20636){: external}, [CVE-2020-1749](https://nvd.nist.gov/vuln/detail/CVE-2020-1749){: external}, [CVE-2020-2732](https://nvd.nist.gov/vuln/detail/CVE-2020-2732){: external}, [CVE-2020-8647](https://nvd.nist.gov/vuln/detail/CVE-2020-8647){: external}, [CVE-2020-8649](https://nvd.nist.gov/vuln/detail/CVE-2020-8649){: external}, [CVE-2020-9383](https://nvd.nist.gov/vuln/detail/CVE-2020-9383){: external}, [CVE-2020-10690](https://nvd.nist.gov/vuln/detail/CVE-2020-10690){: external}, [CVE-2020-10732](https://nvd.nist.gov/vuln/detail/CVE-2020-10732){: external}, [CVE-2020-10742](https://nvd.nist.gov/vuln/detail/CVE-2020-10742){: external}, [CVE-2020-10751](https://nvd.nist.gov/vuln/detail/CVE-2020-10751){: external}, [CVE-2020-10942](https://nvd.nist.gov/vuln/detail/CVE-2020-10942){: external}, [CVE-2020-11565](https://nvd.nist.gov/vuln/detail/CVE-2020-11565){: external}, [CVE-2020-12770](https://nvd.nist.gov/vuln/detail/CVE-2020-12770){: external}, [CVE-2020-12826](https://nvd.nist.gov/vuln/detail/CVE-2020-12826){: external}, [CVE-2020-14305](https://nvd.nist.gov/vuln/detail/CVE-2020-14305){: external}, [CVE-2019-5482](https://nvd.nist.gov/vuln/detail/CVE-2019-5482){: external}, [CVE-2019-19126](https://nvd.nist.gov/vuln/detail/CVE-2019-19126){: external}, [CVE-2020-12825](https://nvd.nist.gov/vuln/detail/CVE-2020-12825){: external}, [CVE-2019-5094](https://nvd.nist.gov/vuln/detail/CVE-2019-5094){: external}, [CVE-2019-5188](https://nvd.nist.gov/vuln/detail/CVE-2019-5188){: external}, [CVE-2019-2974](https://nvd.nist.gov/vuln/detail/CVE-2019-2974){: external}, [CVE-2020-2574](https://nvd.nist.gov/vuln/detail/CVE-2020-2574){: external}, [CVE-2020-2752](https://nvd.nist.gov/vuln/detail/CVE-2020-2752){: external}, [CVE-2020-2780](https://nvd.nist.gov/vuln/detail/CVE-2020-2780){: external}, [CVE-2020-2812](https://nvd.nist.gov/vuln/detail/CVE-2020-2812){: external}, [CVE-2019-12749](https://nvd.nist.gov/vuln/detail/CVE-2019-12749){: external}, [CVE-2019-19956](https://nvd.nist.gov/vuln/detail/CVE-2019-19956){: external}, [CVE-2019-20388](https://nvd.nist.gov/vuln/detail/CVE-2019-20388){: external}, [CVE-2020-7595](https://nvd.nist.gov/vuln/detail/CVE-2020-7595){: external}, [CVE-2020-10754](https://nvd.nist.gov/vuln/detail/CVE-2020-10754){: external}, [CVE-2019-11719](https://nvd.nist.gov/vuln/detail/CVE-2019-11719){: external}, [CVE-2019-11727](https://nvd.nist.gov/vuln/detail/CVE-2019-11727){: external}, [CVE-2019-11756](https://nvd.nist.gov/vuln/detail/CVE-2019-11756){: external}, [CVE-2019-17006](https://nvd.nist.gov/vuln/detail/CVE-2019-17006){: external}, [CVE-2019-17023](https://nvd.nist.gov/vuln/detail/CVE-2019-17023){: external}, [CVE-2020-6829](https://nvd.nist.gov/vuln/detail/CVE-2020-6829){: external}, [CVE-2020-12400](https://nvd.nist.gov/vuln/detail/CVE-2020-12400){: external}, [CVE-2020-12401](https://nvd.nist.gov/vuln/detail/CVE-2020-12401){: external}, [CVE-2020-12402](https://nvd.nist.gov/vuln/detail/CVE-2020-12402){: external}, [CVE-2020-12403](https://nvd.nist.gov/vuln/detail/CVE-2020-12403){: external}, [CVE-2018-20843](https://nvd.nist.gov/vuln/detail/CVE-2018-20843){: external}, [CVE-2019-15903](https://nvd.nist.gov/vuln/detail/CVE-2019-15903){: external}, [CVE-2019-14834](https://nvd.nist.gov/vuln/detail/CVE-2019-14834){: external}, [CVE-2019-11068](https://nvd.nist.gov/vuln/detail/CVE-2019-11068){: external}, [CVE-2019-18197](https://nvd.nist.gov/vuln/detail/CVE-2019-18197){: external}, [CVE-2019-16935](https://nvd.nist.gov/vuln/detail/CVE-2019-16935){: external}, [CVE-2019-20386](https://nvd.nist.gov/vuln/detail/CVE-2019-20386){: external}, [CVE-2019-17498](https://nvd.nist.gov/vuln/detail/CVE-2019-17498){: external}, and [CVE-2020-14365](https://nvd.nist.gov/vuln/detail/CVE-2020-14365){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.4.23_1520_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.4.23_1520_openshift, released 30 September 2020
{: #4423_1520}

The following table shows the changes that are included in the worker node fix pack update `4.4.23_1520_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Automation for provisioning and reloading | N/A	| N/A | Fixes an issue that prevented SDS worker nodes with unified extensible firmware interface (UEFI) bootstrapping from provisioning or reloading.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.4.23_1519_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.4.23_1519_openshift, released 28 September 2020
{: #4423_1519}

The following table shows the changes that are included in the worker node fix pack update `4.4.23_1519_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.4.20 | 4.4.23 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-23){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.4.20_1517_openshift" caption-side="top"}

### Changelog for master fix pack 4.4.20_1518_openshift, released 21 September 2020
{: #4420_1518}

The following table shows the changes that are included in the master fix pack patch update `4.4.20_1518_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster health image | v1.1.9 | v1.1.11 | Updated `Go` version for [CVE-2020-16845](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-16845){: external} and [CVE-2020-24553](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24553){: external}. |
| etcd | v3.4.10 | v3.4.13 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.13){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.11-1 | v1.17.12-1 | Updated to support the Kubernetes 1.17.12 release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 377 | 378 | Updated `Go` version for [CVE-2020-16845](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-16845){: external}. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | d80b738 | 4b47693 | Updated `Go` version for [CVE-2020-16845](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-16845){: external} and image for [CVE-2020-14352](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14352){: external}. |
| Key Management Service provider | v2.0.2 | v2.0.4 | Updated `Go` version for [CVE-2020-16845](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-16845){: external} and [CVE-2020-24553](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24553){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.4.0-20200805 | v4.4.0-20200821 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.4.0+20200821){: external}. |
| {{site.data.keyword.openshiftshort}} | 4.4.17 | 4.4.20 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-20){: external}. |
| OpenVPN Operator image | v1.0.7 | v1.0.8 | Updated image for [CVE-2020-14352](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14352){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.4.0+20200805 | 4.4.0+20200821 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.4.0+20200821){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.4.20_1517_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.4.20_1517_openshift, released 14 September 2020
{: #4420_1517}

The following table shows the changes that are included in the worker node fix pack update `4.4.20_1517_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| CRI-O | 1.17.4 | 1.17.5 | See the [CRI-O release notes](https://github.com/cri-o/cri-o/releases/tag/v1.17.5){: external}. |
| {{site.data.keyword.openshiftshort}} | 4.4.18 | 4.4.20 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-4-20){: external}. The update resolves CVE-2020-8557 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6343881){: external}).|
| RHEL 7 packages | N/A | N/A | Updated worker node image with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.4.18_1516_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.4.18_1516_openshift, released 31 August 2020
{: #4418_1516}

The following table shows the changes that are included in the worker node fix pack update `4.4.18_1516_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Master proxy | 1.8.25-384f42 | 1.8.26-561f1a | See the [HAProxy changelogs](https://www.haproxy.org/download/1.8/src/CHANGELOG){: external}. |
| {{site.data.keyword.openshiftshort}} | 4.4.16 | 4.4.18 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-4-18){: external}.|
| RHEL 7 packages | 3.10.0-1127.18.2.el7 | 3.10.0-1127.19.1.el7 | Updated worker node image with kernel and package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.4.16_1513_openshift" caption-side="top"}

### Changelog for master fix pack 4.4.17_1515_openshift, released 21 August 2020
{: #4417_1515}

The following table shows the changes that are included in the master fix pack patch update `4.4.17_1515_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster master operations | N/A | N/A | Fixed a problem that might cause cluster master operations to fail for clusters with a private service endpoint enabled. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.9-1 | v1.17.11-1 | Updated to support the Kubernetes 1.17.11 release and to use `Go` version 1.13.15. |
| {{site.data.keyword.openshiftshort}} | 4.4.16 | 4.4.17 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-17){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.4.16_1513_openshift" caption-side="top"}

### Changelog for master fix pack 4.4.16_1513_openshift, released 18 August 2020
{: #4416_1513_master}

The following table shows the changes that are included in the master fix pack patch update `4.4.16_1513_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster health image | v1.1.8 | v1.1.9 | Updated to use `Go` version 1.13.13. |
| Cluster master operations | N/A | N/A | Cluster master update operations are now canceled if a broken [Kubernetes admission webhook](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/){: external} is detected. |
| etcd | v3.4.9 | v3.4.10 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.10){: external}.|
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | 1.17 | 1.17.1 | Updated to use `Go` version 1.13.8. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 375 | 377 | Fixed a bug that prevents persistent volume claim (PVC) creation failures from being retried. Updated to use `Go` version 1.13.8. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 8882606 | d80b738 | Updated image for [CVE-2020-12049](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-12049){: external} and to use `Go` version 1.13.14. |
| Key Management Service provider | v1.0.0 | v2.0.2 | Updated image for [CVE-2020-15586](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-15586){: external}. |
| Kubernetes configuration | N/A | N/A | The Kubernetes API server audit policy configuration is updated to include auditing of all API groups except `apiregistration.k8s.io` and `coordination.k8s.io`. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.4.0-20200615 | v4.4.0-20200805 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.4.0+20200805){: external}. |
| {{site.data.keyword.openshiftshort}} | 4.4.11 | 4.4.16 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-16){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit |  v4.4.0+20200615 | v4.4.0+20200805| See the [{{site.data.keyword.openshiftlong_notm}}toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.4.0+20200805){: external}. |
| OpenVPN Operator image | v1.0.6 | v1.0.7 | Updated image for [CVE-2020-12049](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-12049){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.4.11_1511_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.4.16_1513_openshift, released 17 August 2020
{: #4416_1513}

The following table shows the changes that are included in the worker node fix pack update `4.4.16_1513_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.4.14 | 4.4.16 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-4-16){: external}.|
| RHEL 7 packages | N/A | N/A | Updated worker node images with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.4.14_1512_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.4.14_1512_openshift, released 3 August 2020
{: #4414_1512}

The following table shows the changes that are included in the worker node fix pack update `4.4.14_1512_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.4.11 | 4.4.14 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-4-14){: external}. The update resolves CVE-2020-8558 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6319989){: external}).|
| RHEL 7 Packages | 3.10.0-1127.13.1.el7 | 3.10.0-1127.18.2.el7 | Updated worker node images with package updates for [CVE-2020-10713](https://nvd.nist.gov/vuln/detail/CVE-2020-10713){: external}, [CVE-2020-14308](https://nvd.nist.gov/vuln/detail/CVE-2020-14308){: external}, [CVE-2020-14309](https://nvd.nist.gov/vuln/detail/CVE-2020-14309){: external}, [CVE-2020-14310](https://nvd.nist.gov/vuln/detail/CVE-2020-14310){: external}, [CVE-2020-14311](https://nvd.nist.gov/vuln/detail/CVE-2020-14311){: external}, [CVE-2020-15705](https://nvd.nist.gov/vuln/detail/CVE-2020-15705){: external}, [CVE-2020-15706](https://nvd.nist.gov/vuln/detail/CVE-2020-15706){: external}, [CVE-2020-15707](https://nvd.nist.gov/vuln/detail/CVE-2020-15707){: external}, [CVE-2019-19527](https://nvd.nist.gov/vuln/detail/CVE-2019-19527){: external}, [CVE-2020-10757](https://nvd.nist.gov/vuln/detail/CVE-2020-10757){: external}, [CVE-2020-12653](https://nvd.nist.gov/vuln/detail/CVE-2020-12653){: external}, and [CVE-2020-12654](https://nvd.nist.gov/vuln/detail/CVE-2020-12654){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.4.11_1511_openshift" caption-side="top"}

### Changelog for 4.4.11_1511_openshift, released 21 July 2020
{: #4411_1511}

The following table shows the changes that are included in the `4.4.11_1511_openshift` version update.
{: shortdesc}

| Component | Location | Previous | Current | Description |
| --- | --- | --- | --- | --- |
| CRI-O | Worker | 1.16.6 | 1.17.4 | See the [CRI-O changelogs](https://github.com/cri-o/cri-o/releases/tag/v1.17.4){: external}. |
| Master Proxy | Worker | 2.0.15-afe432 | 1.8.25-384f42 | See the [HAProxy changelogs](https://www.haproxy.org/download/1.8/src/CHANGELOG){: external}. Fixes a connection leak that happens when HAProxy is under high load. |
| Key Management Service provider | Master | N/A | v1.0.0 | **New!**: {{site.data.keyword.openshiftlong_notm}} version 4.4 clusters now support [Key Management Service (KMS) providers](/docs/openshift?topic=openshift-encryption#kms). |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | Master | v4.3.0-20200615 | v4.4.0-20200615 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.4.0+20200615){: external}. |
| {{site.data.keyword.openshiftshort}} | Both | Master 4.3.28<br>Worker 4.3.29 | 4.4.11 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-11){: external}. |
| RHEL 7 Packages | Worker | N/A | N/A | Updated worker node images with package updates for [CVE-2020-12049](https://nvd.nist.gov/vuln/detail/CVE-2020-12049){: external}.|
| {{site.data.keyword.openshiftlong_notm}} toolkit | Master | 4.3.0+20200615 | 4.4.0+20200615 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.4.0+20200615){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the location of the component, in the master, worker node, or both. The third column is the previous version number of the component. The fourth column is the current version number of the component. The fifth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.3.28_1532_openshift" caption-side="top"}

## Deprecated: Version 4.3 changelog
{: #version-43}

Review the changelogs for {{site.data.keyword.openshiftlong_notm}} version 4.3 patch updates.
{: shortdesc}

{{site.data.keyword.openshiftshort}} version 4.3 is deprecated, and becomes unsupported in February 2021 (date subject to change). [Update your clusters](/docs/openshift?topic=openshift-update) to at least {{site.data.keyword.openshiftshort}} version 4.4 as soon as possible.
{: deprecated}

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
| Cluster master operations | N/A | N/A | Fixed a problem that might cause cluster master operations to fail for clusters with a private service endpoint enabled. |
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
| {{site.data.keyword.cloud_notm}} RBAC Operator | Master | N/A | 08ce50e | **New!**: Added a control plane operator to synchronize [{{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) service roles](/docs/openshift?topic=openshift-access_reference#service) with Kubernetes role-based access control (RBAC) roles. |
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
| {{site.data.keyword.openshiftshort}} Control Plane Operator | Master | N/A | 3b3ff62 | **New!:** Added a toolkit to enable running {{site.data.keyword.openshiftshort}} version 4 with a managed control plane.  For more information, see the [{{site.data.keyword.openshiftshort}} HyperShift toolkit repository](https://github.com/openshift/hypershift-toolkit/commit/3b3ff6269b1c71ffa4a0598f7969aad6f7e4eb20). |
| {{site.data.keyword.openshiftshort}} HyperShift toolkit | Master | N/A | 3b3ff62 | **New!:** Added a toolkit to enable running {{site.data.keyword.openshiftshort}} version 4 with a managed control plane. For more information, see the [{{site.data.keyword.openshiftshort}} HyperShift toolkit repository](https://github.com/openshift/hypershift-toolkit/commit/3b3ff6269b1c71ffa4a0598f7969aad6f7e4eb20). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is where the component is located: the master, worker node, or both. The third column is the previous version number of the component. The fourth column is the current version number of the component. The fifth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.170" caption-side="top"}

## Deprecated: Version 3.11 changelog
{: #version-311}

Review the changelogs for {{site.data.keyword.openshiftlong_notm}} version 3.11 patch updates.
{: shortdesc}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> {{site.data.keyword.openshiftshort}} version 3.11 is deprecated, and becomes unsupported in June 2022 (date subject to change).
{: deprecated}

### Changelog for worker node fix pack 3.11.306_1572_openshift, released 9 November 2020
{: #311306_1572}

The following table shows the changes that are included in the worker node fix pack update `3.11.306_1572_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates for [CVE-2020-15999](https://nvd.nist.gov/vuln/detail/CVE-2020-15999){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.306_1571_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.306_1571_openshift, released 26 October 2020
{: #311306_1571}

The following table shows the changes that are included in the worker node fix pack update `3.11.306_1571_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} node | 3.11.286 | 3.11.306 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-306){: external}.|
| RHEL 7 Packages | 3.10.0-1160.2.1.el7 | 3.10.0-1160.2.2.el7 | Updated worker node images with kernel and package updates for [CVE-2020-12351](https://nvd.nist.gov/vuln/detail/CVE-2020-12351){: external} and [CVE-2020-12352](https://nvd.nist.gov/vuln/detail/CVE-2020-12352){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.286_1570_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.286_1571_openshift, released 26 October 2020
{: #311286_1571}

The following table shows the changes that are included in the master fix pack patch update `3.11.286_1571_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster health image | v1.1.11 | v1.1.12 | Updated to use `Go` version 1.15.2. |
| {{site.data.keyword.openshiftshort}} | 3.11.272 | 3.11.286 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-286){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.272_1567_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.286_1570_openshift, released 12 October 2020
{: #311286_1570}

The following table shows the changes that are included in the worker node fix pack update `3.11.286_1570_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1127.19.1.el7 | 3.10.0-1160.2.1.el7 | Updated worker node image with kernel and package updates for: [CVE-2019-12450](https://nvd.nist.gov/vuln/detail/CVE-2019-12450){: external}, [CVE-2019-14822](https://nvd.nist.gov/vuln/detail/CVE-2019-14822){: external}, [CVE-2020-12243](https://nvd.nist.gov/vuln/detail/CVE-2020-12243){: external}, [CVE-2019-14866](https://nvd.nist.gov/vuln/detail/CVE-2019-14866){: external}, [CVE-2017-12652](https://nvd.nist.gov/vuln/detail/CVE-2017-12652){: external}, [CVE-2017-18551](https://nvd.nist.gov/vuln/detail/CVE-2017-18551){: external}, [CVE-2018-20836](https://nvd.nist.gov/vuln/detail/CVE-2018-20836){: external}, [CVE-2019-9454](https://nvd.nist.gov/vuln/detail/CVE-2019-9454){: external}, [CVE-2019-9458](https://nvd.nist.gov/vuln/detail/CVE-2019-9458){: external}, [CVE-2019-12614](https://nvd.nist.gov/vuln/detail/CVE-2019-12614){: external}, [CVE-2019-15217](https://nvd.nist.gov/vuln/detail/CVE-2019-15217){: external}, [CVE-2019-15807](https://nvd.nist.gov/vuln/detail/CVE-2019-15807){: external}, [CVE-2019-15917](https://nvd.nist.gov/vuln/detail/CVE-2019-15917){: external}, [CVE-2019-16231](https://nvd.nist.gov/vuln/detail/CVE-2019-16231){: external}, [CVE-2019-16233](https://nvd.nist.gov/vuln/detail/CVE-2019-16233){: external}, [CVE-2019-16994](https://nvd.nist.gov/vuln/detail/CVE-2019-16994){: external}, [CVE-2019-17053](https://nvd.nist.gov/vuln/detail/CVE-2019-17053){: external}, [CVE-2019-17055](https://nvd.nist.gov/vuln/detail/CVE-2019-17055){: external}, [CVE-2019-18808](https://nvd.nist.gov/vuln/detail/CVE-2019-18808){: external}, [CVE-2019-19046](https://nvd.nist.gov/vuln/detail/CVE-2019-19046){: external}, [CVE-2019-19055](https://nvd.nist.gov/vuln/detail/CVE-2019-19055){: external}, [CVE-2019-19058](https://nvd.nist.gov/vuln/detail/CVE-2019-19058){: external}, [CVE-2019-19059](https://nvd.nist.gov/vuln/detail/CVE-2019-19059){: external}, [CVE-2019-19062](https://nvd.nist.gov/vuln/detail/CVE-2019-19062){: external}, [CVE-2019-19063](https://nvd.nist.gov/vuln/detail/CVE-2019-19063){: external}, [CVE-2019-19332](https://nvd.nist.gov/vuln/detail/CVE-2019-19332){: external}, [CVE-2019-19447](https://nvd.nist.gov/vuln/detail/CVE-2019-19447){: external}, [CVE-2019-19523](https://nvd.nist.gov/vuln/detail/CVE-2019-19523){: external}, [CVE-2019-19524](https://nvd.nist.gov/vuln/detail/CVE-2019-19524){: external}, [CVE-2019-19530](https://nvd.nist.gov/vuln/detail/CVE-2019-19530){: external}, [CVE-2019-19534](https://nvd.nist.gov/vuln/detail/CVE-2019-19534){: external}, [CVE-2019-19537](https://nvd.nist.gov/vuln/detail/CVE-2019-19537){: external}, [CVE-2019-19767](https://nvd.nist.gov/vuln/detail/CVE-2019-19767){: external}, [CVE-2019-19807](https://nvd.nist.gov/vuln/detail/CVE-2019-19807){: external}, [CVE-2019-20054](https://nvd.nist.gov/vuln/detail/CVE-2019-20054){: external}, [CVE-2019-20095](https://nvd.nist.gov/vuln/detail/CVE-2019-20095){: external}, [CVE-2019-20636](https://nvd.nist.gov/vuln/detail/CVE-2019-20636){: external}, [CVE-2020-1749](https://nvd.nist.gov/vuln/detail/CVE-2020-1749){: external}, [CVE-2020-2732](https://nvd.nist.gov/vuln/detail/CVE-2020-2732){: external}, [CVE-2020-8647](https://nvd.nist.gov/vuln/detail/CVE-2020-8647){: external}, [CVE-2020-8649](https://nvd.nist.gov/vuln/detail/CVE-2020-8649){: external}, [CVE-2020-9383](https://nvd.nist.gov/vuln/detail/CVE-2020-9383){: external}, [CVE-2020-10690](https://nvd.nist.gov/vuln/detail/CVE-2020-10690){: external}, [CVE-2020-10732](https://nvd.nist.gov/vuln/detail/CVE-2020-10732){: external}, [CVE-2020-10742](https://nvd.nist.gov/vuln/detail/CVE-2020-10742){: external}, [CVE-2020-10751](https://nvd.nist.gov/vuln/detail/CVE-2020-10751){: external}, [CVE-2020-10942](https://nvd.nist.gov/vuln/detail/CVE-2020-10942){: external}, [CVE-2020-11565](https://nvd.nist.gov/vuln/detail/CVE-2020-11565){: external}, [CVE-2020-12770](https://nvd.nist.gov/vuln/detail/CVE-2020-12770){: external}, [CVE-2020-12826](https://nvd.nist.gov/vuln/detail/CVE-2020-12826){: external}, [CVE-2020-14305](https://nvd.nist.gov/vuln/detail/CVE-2020-14305){: external}, [CVE-2019-5482](https://nvd.nist.gov/vuln/detail/CVE-2019-5482){: external}, [CVE-2019-19126](https://nvd.nist.gov/vuln/detail/CVE-2019-19126){: external}, [CVE-2020-12825](https://nvd.nist.gov/vuln/detail/CVE-2020-12825){: external}, [CVE-2019-5094](https://nvd.nist.gov/vuln/detail/CVE-2019-5094){: external}, [CVE-2019-5188](https://nvd.nist.gov/vuln/detail/CVE-2019-5188){: external}, [CVE-2019-2974](https://nvd.nist.gov/vuln/detail/CVE-2019-2974){: external}, [CVE-2020-2574](https://nvd.nist.gov/vuln/detail/CVE-2020-2574){: external}, [CVE-2020-2752](https://nvd.nist.gov/vuln/detail/CVE-2020-2752){: external}, [CVE-2020-2780](https://nvd.nist.gov/vuln/detail/CVE-2020-2780){: external}, [CVE-2020-2812](https://nvd.nist.gov/vuln/detail/CVE-2020-2812){: external}, [CVE-2019-12749](https://nvd.nist.gov/vuln/detail/CVE-2019-12749){: external}, [CVE-2019-19956](https://nvd.nist.gov/vuln/detail/CVE-2019-19956){: external}, [CVE-2019-20388](https://nvd.nist.gov/vuln/detail/CVE-2019-20388){: external}, [CVE-2020-7595](https://nvd.nist.gov/vuln/detail/CVE-2020-7595){: external}, [CVE-2020-10754](https://nvd.nist.gov/vuln/detail/CVE-2020-10754){: external}, [CVE-2019-11719](https://nvd.nist.gov/vuln/detail/CVE-2019-11719){: external}, [CVE-2019-11727](https://nvd.nist.gov/vuln/detail/CVE-2019-11727){: external}, [CVE-2019-11756](https://nvd.nist.gov/vuln/detail/CVE-2019-11756){: external}, [CVE-2019-17006](https://nvd.nist.gov/vuln/detail/CVE-2019-17006){: external}, [CVE-2019-17023](https://nvd.nist.gov/vuln/detail/CVE-2019-17023){: external}, [CVE-2020-6829](https://nvd.nist.gov/vuln/detail/CVE-2020-6829){: external}, [CVE-2020-12400](https://nvd.nist.gov/vuln/detail/CVE-2020-12400){: external}, [CVE-2020-12401](https://nvd.nist.gov/vuln/detail/CVE-2020-12401){: external}, [CVE-2020-12402](https://nvd.nist.gov/vuln/detail/CVE-2020-12402){: external}, [CVE-2020-12403](https://nvd.nist.gov/vuln/detail/CVE-2020-12403){: external}, [CVE-2018-20843](https://nvd.nist.gov/vuln/detail/CVE-2018-20843){: external}, [CVE-2019-15903](https://nvd.nist.gov/vuln/detail/CVE-2019-15903){: external}, [CVE-2019-14834](https://nvd.nist.gov/vuln/detail/CVE-2019-14834){: external}, [CVE-2019-11068](https://nvd.nist.gov/vuln/detail/CVE-2019-11068){: external}, [CVE-2019-18197](https://nvd.nist.gov/vuln/detail/CVE-2019-18197){: external}, [CVE-2019-16935](https://nvd.nist.gov/vuln/detail/CVE-2019-16935){: external}, [CVE-2019-20386](https://nvd.nist.gov/vuln/detail/CVE-2019-20386){: external}, [CVE-2019-17498](https://nvd.nist.gov/vuln/detail/CVE-2019-17498){: external}, and [CVE-2020-14365](https://nvd.nist.gov/vuln/detail/CVE-2020-14365){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.286_1569_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.286_1569_openshift, released 30 September 2020
{: #311286_1569}

The following table shows the changes that are included in the worker node fix pack update `3.11.286_1569_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Automation for provisioning and reloading | N/A	| N/A | Fixes an issue that prevented SDS worker nodes with unified extensible firmware interface (UEFI) bootstrapping from provisioning or reloading.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.286_1568_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.286_1568_openshift, released 28 September 2020
{: #311286_1568}

The following table shows the changes that are included in the worker node fix pack update `3.11.286_1568_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 3.11.272	| 3.11.286 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-286){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.272_1566_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.272_1567_openshift, released 21 September 2020
{: #311272_1567}

The following table shows the changes that are included in the master fix pack patch update `3.11.272_1567_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster health image | v1.1.9 | v1.1.11 | Updated `Go` version for [CVE-2020-16845](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-16845){: external} and [CVE-2020-24553](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24553){: external}. |
| etcd | v3.3.22 | v3.3.25 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.3.25){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 377 | 378 | Updated `Go` version for [CVE-2020-16845](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-16845){: external}. |
| Key Management Service provider | v1.0.1 | v1.0.3 | Updated `Go` version for [CVE-2020-16845](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-16845){: external} and [CVE-2020-24553](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24553){: external}. |
| {{site.data.keyword.openshiftshort}} | 3.11.248 | 3.11.272 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-272){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.272_1566_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.272_1566_openshift, released 14 September 2020
{: #311272_1566}

The following table shows the changes that are included in the worker node fix pack update `3.11.272_1566_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Master proxy | 1.8.25-384f42 | 1.8.26-561f1a | See the [HAProxy changelog](https://www.haproxy.org/download/1.8/src/CHANGELOG){: external}. |
| RHEL 7 packages | N/A | N/A | Updated worker node image with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.272_1565_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.272_1565_openshift, released 31 August 2020
{: #311272_1565}

The following table shows the changes that are included in the worker node fix pack update `3.11.272_1565_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 packages | 3.10.0-1127.18.2.el7 | 3.10.0-1127.19.1.el7 | Updated worker node image with kernel and package updates. |
| {{site.data.keyword.openshiftshort}} node | 3.11.248 | 3.11.272 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-272){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.248_1564_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.248_1564_openshift, released 18 August 2020
{: #311248_1564_master}

The following table shows the changes that are included in the master fix pack patch update `3.11.248_1564_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Calico node configuration | N/A | N/A | Disabled the pod readiness probe and removed the `felix` check from the pod liveness probe. |
| Cluster health image | v1.1.8 | v1.1.9 | Updated to use `Go` version 1.13.13. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 376 | 377 | Fixed a bug that prevents persistent volume claim (PVC) creation failures from being retried. |
| Key Management Service provider | v1.0.0 | v1.0.1 | Updated image for [CVE-2020-15586](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-15586){: external}. |
| {{site.data.keyword.openshiftshort}} | 3.11.232 | 3.11.248 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-248){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.232_1561_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.248_1564_openshift, released 17 August 2020
{: #311248_1564}

The following table shows the changes that are included in the worker node fix pack update `3.11.248_1564_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 packages | N/A | N/A | Updated worker node images with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.248_1561_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.248_1561_openshift, released 3 August 2020
{: #311248_1561}

The following table shows the changes that are included in the worker node fix pack update `3.11.248_1561_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} node | 3.11.232 | 3.11.248 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-248){: external}. The update resolves CVE-2020-8558 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6319989){: external}). |
| RHEL 7 Packages | 3.10.0-1127.13.1.el7 | 3.10.0-1127.18.2.el7 | Updated worker node images with package updates for [CVE-2020-10713](https://nvd.nist.gov/vuln/detail/CVE-2020-10713){: external}, [CVE-2020-14308](https://nvd.nist.gov/vuln/detail/CVE-2020-14308){: external}, [CVE-2020-14309](https://nvd.nist.gov/vuln/detail/CVE-2020-14309){: external}, [CVE-2020-14310](https://nvd.nist.gov/vuln/detail/CVE-2020-14310){: external}, [CVE-2020-14311](https://nvd.nist.gov/vuln/detail/CVE-2020-14311){: external}, [CVE-2020-15705](https://nvd.nist.gov/vuln/detail/CVE-2020-15705){: external}, [CVE-2020-15706](https://nvd.nist.gov/vuln/detail/CVE-2020-15706){: external}, [CVE-2020-15707](https://nvd.nist.gov/vuln/detail/CVE-2020-15707){: external}, [CVE-2019-19527](https://nvd.nist.gov/vuln/detail/CVE-2019-19527){: external}, [CVE-2020-10757](https://nvd.nist.gov/vuln/detail/CVE-2020-10757){: external}, [CVE-2020-12653](https://nvd.nist.gov/vuln/detail/CVE-2020-12653){: external}, and [CVE-2020-12654](https://nvd.nist.gov/vuln/detail/CVE-2020-12654){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.232_1558_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.232_1560_openshift, released 24 July 2020
{: #311232_1560}

The following table shows the changes that are included in the master fix pack update `3.11.232_1560_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Heapster configuration | N/A | N/A | Configuration changes now properly trigger a restart of the `heapster` pod in `kube-system` namespace. |
| Cluster master operations | N/A | N/A | Fixed a problem that might cause pods to fail authentication to the Kubernetes API server after a cluster master operation. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 375 | 376 | Updated to use `Go` version 1.13.8. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.232_1559_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.232_1559_openshift, released 20 July 2020
{: #311232_1559}

The following table shows the changes that are included in the master fix pack update `3.11.232_1559_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Block Storage driver configuration | N/A | N/A | Added a pod memory limit. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor configuration | N/A | N/A | Added a pod memory limit. |
| {{site.data.keyword.openshiftshort}} | 3.11.219 | 3.11.232 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-232){: external}. The update resolves CVE-2019-11254 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6249873){: external}) and CVE-2020-8555 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6249891){: external}). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.232_1555_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.232_1558_openshift, released 20 July 2020
{: #311232_1558}

The following table shows the changes that are included in the worker node fix pack update `3.11.232_1558_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Master Proxy | 2.0.15-afe432 | 1.8.25-384f42 | See the [HAProxy changelogs](https://www.haproxy.org/download/1.8/src/CHANGELOG){: external}. Fixes a connection leak that happens when HAProxy is under high load. |
| RHEL 7 Packages |  N/A | N/A | Updated worker node images with package updates for [CVE-2020-12049](https://nvd.nist.gov/vuln/detail/CVE-2020-12049){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.232_1555_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.232_1555_openshift, released 6 July 2020
{: #311232_1555}

The following table shows the changes that are included in the worker node fix pack update `3.11.232_1555_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Master Proxy | 1.8.25-30b675 | 2.0.15-afe432 | See the [HAProxy changelogs](https://www.haproxy.org/download/2.0/src/CHANGELOG){: external}. |
| RHEL 7 Packages | 3.10.0-1127.10.1.el7 | 3.10.0-1127.13.1.el7 | Updated worker node images with kernel package updates for [CVE-2020-10749](https://nvd.nist.gov/vuln/detail/CVE-2020-10749){: external}, [CVE-2020-1702](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1702){: external}, [CVE-2016-8867](https://nvd.nist.gov/vuln/detail/CVE-2016-8867){: external}, [CVE-2020-14298](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14298){: external}, [CVE-2020-14300](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14300){: external}, [CVE-2020-12888](https://nvd.nist.gov/vuln/detail/CVE-2020-12888){: external}, [CVE-2020-11868](https://nvd.nist.gov/vuln/detail/CVE-2020-11868){: external}, and [CVE-2020-13817](https://nvd.nist.gov/vuln/detail/CVE-2020-13817){: external}. |
| Worker node `drain` automation | N/A | N/A | Fixes a race condition that can cause worker node `drain` automation to fail. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.232_1554_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.219_1554_openshift and worker node fix pack 3.11.232_1554_openshift, released 22 June 2020
{: #311219_1554_master}

The following table shows the changes that are included in the master fix pack update `3.11.219_1554_openshift` and in worker node fix pack update `3.11.232_1554_openshift`. Master patch updates are applied automatically. Worker node patch updates can be applied by updating or reloading the worker node For more information, see [Update types](/docs/openshift?topic=openshift-openshift_versions#openshift_update_types).
{: shortdesc}

| Component | Location | Previous | Current | Description |
| --------- | -------- | ------- | -------- | ----------- |
| Calico | Master | v3.8.6 | v3.8.9 | See the [Calico release notes](https://docs.projectcalico.org/releases){: external}. |
| Cluster health image | Master | v1.1.5 | v1.1.8 | Additional status information is included when an add-on health state is `critical`. Improved performance when handling cluster status updates. |
| Cluster master operations | Master | N/A | N/A | Cluster master operations such as `refresh` or `update` are now canceled if a broken [Kubernetes admission webhook](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/){: external} is detected. |
| etcd | Master | v3.3.20 | v3.3.22 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.3.22){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | Master | v1.15.12-316 | v1.15.12-343 | Updated to use `calicoctl` version 3.8.9. |
| {{site.data.keyword.filestorage_full_notm}} plug-in | Master | 373 | 375 | Fixed a bug that might cause error handling to create additional persistent volumes. |
| {{site.data.keyword.openshiftshort}} | Master | 3.11.216 | 3.11.219 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-219){: external}. The master update resolves CVE-2020-8552 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6238260){: external}). |
| {{site.data.keyword.openshiftshort}} node | Worker | 3.11.219 | 3.11.232 | See the [{{site.data.keyword.openshiftshort}}  release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-232){: external}. |
| RHEL 7 packages | Worker | N/A | N/A | Updated worker node images with package updates for [CVE-2020-0543](https://nvd.nist.gov/vuln/detail/CVE-2020-0543){: external}, [CVE-2020-0548](https://nvd.nist.gov/vuln/detail/CVE-2020-0548){: external}, and [CVE-2020-0549](https://nvd.nist.gov/vuln/detail/CVE-2020-0549){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is where the component is located, the master, worker node, or both. The third column is the previous version number of the component. The fourth column is the current version number of the component. The fifth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.219_1552_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.219_1552_openshift, released 8 June 2020
{: #311219_1552}

The following table shows the changes that are included in the worker node fix pack update `3.11.219_1552_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} node | 3.11.216 | 3.11.219 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-219){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.216_1551_openshift" caption-side="top"}

### Changelog for 3.11.216_1551_openshift, released 26 May 2020
{: #311216_1551}

The following table shows the changes that are included in the master and worker node update `3.11.216_1551_openshift`. Master patch updates are applied automatically. Worker node patch updates can be applied by updating or reloading the worker node For more information, see [Update types](/docs/containers?topic=containers-cs_versions#update_types).
{: shortdesc}

| Component | Location | Previous | Current | Description |
| --------- | -------- | ------- | -------- | ----------- |
| Cluster health image | Master | v1.1.1 | v1.1.5 | When cluster add-ons do not support the current cluster version, a warning is now returned in the cluster health state. |
| etcd | Master | v3.3.18 | v3.3.20 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.3.20){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | Master | v1.15.11-274 | v1.15.12-316 | Updated to support the Kubernetes 1.15.12 release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | Master | 358 | 373 | Updated image for [CVE-2020-1967](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1967){: external} and [CVE-2020-11655](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-11655){: external}. |
| {{site.data.keyword.cloud_notm}} Paks | Master | N/A | N/A | Removed duplicate repositories in `ClusterImagePolicies` resources that are installed by {{site.data.keyword.cloud_notm}} Paks. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | Master | 169 | 203 | Version 2.0 network load balancers (NLB) were updated to fix problems with long-lived network connections to endpoints that failed readiness probes. Updated image for [CVE-2020-1967](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1967){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane | Master | 3.11.200 | 3.11.216 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-216){: external}. |
| RHEL 7 Packages | Worker | 3.10.0-1127.el7 | 3.10.0-1127.8.2.el7 | Updated worker node images with kernel package updates for [CVE-2017-18595](https://nvd.nist.gov/vuln/detail/CVE-2017-18595){: external}, [CVE-2019-19768](https://nvd.nist.gov/vuln/detail/CVE-2019-19768){: external}, and [CVE-2020-10711](https://nvd.nist.gov/vuln/detail/CVE-2020-10711){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is where the component is located, the master, worker node, or both. The third column is the previous version number of the component. The fourth column is the current version number of the component. The fifth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.216_1550_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.216_1550_openshift, released 11 May 2020
{: #311216_1550}

The following table shows the changes that are included in the worker node fix pack update `3.11.216_1550_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} node | 3.11.200 | 3.11.216 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-216){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.200_1549_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.200_1549_openshift, released 27 April 2020
{: #311200_1549}

The following table shows the changes that are included in the worker node fix pack update `3.11.200_1549_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 1.8.25-30b675 | 1.8.25-adb65d | Update addresses [CVE-2020-1967](https://nvd.nist.gov/vuln/detail/CVE-2020-1967){: external}. |
| RHEL 7 Packages | N/A | N/A | Updated worker node images with package updates for [CVE-2019-19921](https://nvd.nist.gov/vuln/detail/CVE-2019-19921){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.200_1546_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.200_1548_openshift, released 23 April 2020
{: #311200_1548}

The following table shows the changes that are included in the master fix pack update `3.11.200_1548_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico configuration | N/A | N/A | Updated to allow egress from the worker nodes via the `allow-vrrp` `GlobalNetworkPolicy`. |
| Cluster health | N/A | v1.1.1 | Cluster health now includes more add-on status information. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.15.10-252 | v1.15.11-274 | Updated to support the Kubernetes 1.15.11 release and to use `Go` version 1.12.17. |
| {{site.data.keyword.cloud_notm}} Paks | N/A | N/A | Fixed `ClusterImagePolicies` resources that are installed by {{site.data.keyword.cloud_notm}} Paks which prevent cluster master operations from succeeding. |
| Key Management Service provider | 277 | v1.0.0 | Updated the {{site.data.keyword.keymanagementservicelong_notm}} `Go` client. |
| {{site.data.keyword.openshiftshort}} | 3.11.170 | 3.11.200 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-200){: external}. |
| OpenVPN client | N/A | N/A | Fixed a problem that might cause the `vpn-config` secret in the `kube-system` project to be deleted during cluster master operations. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.200_1546_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.200_1546_openshift, released 13 April 2020
{: #311200_1546_worker}

The following table shows the changes that are included in the worker node fix pack update `3.11.200_1546_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 1.8.23 | 1.8.25 | See the [HA proxy changelogs](https://www.haproxy.org/download/1.8/src/CHANGELOG){: external}. Contains update for [CVE-2020-11100](https://nvd.nist.gov/vuln/detail/CVE-2020-11100){: external}. |
| {{site.data.keyword.openshiftshort}} node | 3.11.188 | 3.11.200 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-200){: external}. |
| RHEL 7 Packages | 3.10.0-1062.18.1.el7 | 3.10.0-1127.el7 | Updated worker node images with package and kernel updates for [CVE-2015-2716](https://nvd.nist.gov/vuln/detail/CVE-2015-2716){: external}, [CVE-2015-8035](https://nvd.nist.gov/vuln/detail/CVE-2015-8035){: external}, [CVE-2015-9289](https://nvd.nist.gov/vuln/detail/CVE-2015-9289){: external}, [CVE-2016-5131](https://nvd.nist.gov/vuln/detail/CVE-2016-5131){: external}, [CVE-2017-1000476](https://nvd.nist.gov/vuln/detail/CVE-2017-1000476){: external}, [CVE-2017-11166](https://nvd.nist.gov/vuln/detail/CVE-2017-11166){: external}, [CVE-2017-12805](https://nvd.nist.gov/vuln/detail/CVE-2017-12805){: external}, [CVE-2017-12806](https://nvd.nist.gov/vuln/detail/CVE-2017-12806){: external}, [CVE-2017-15412](https://nvd.nist.gov/vuln/detail/CVE-2017-15412){: external}, [CVE-2017-17807](https://nvd.nist.gov/vuln/detail/CVE-2017-17807){: external}, [CVE-2017-18251](https://nvd.nist.gov/vuln/detail/CVE-2017-18251){: external}, [CVE-2017-18252](https://nvd.nist.gov/vuln/detail/CVE-2017-18252){: external}, [CVE-2017-18254](https://nvd.nist.gov/vuln/detail/CVE-2017-18254){: external}, [CVE-2017-18258](https://nvd.nist.gov/vuln/detail/CVE-2017-18258){: external}, [CVE-2017-18271](https://nvd.nist.gov/vuln/detail/CVE-2017-18271){: external}, [CVE-2017-18273](https://nvd.nist.gov/vuln/detail/CVE-2017-18273){: external}, [CVE-2017-6519](https://nvd.nist.gov/vuln/detail/CVE-2017-6519){: external}, [CVE-2018-10177](https://nvd.nist.gov/vuln/detail/CVE-2018-10177){: external}, [CVE-2018-10360](https://nvd.nist.gov/vuln/detail/CVE-2018-10360){: external}, [CVE-2018-10804](https://nvd.nist.gov/vuln/detail/CVE-2018-10804){: external}, [CVE-2018-10805](https://nvd.nist.gov/vuln/detail/CVE-2018-10805){: external}, [CVE-2018-1116](https://nvd.nist.gov/vuln/detail/CVE-2018-1116){: external}, [CVE-2018-11656](https://nvd.nist.gov/vuln/detail/CVE-2018-11656){: external}, [CVE-2018-12599](https://nvd.nist.gov/vuln/detail/CVE-2018-12599){: external}, [CVE-2018-12600](https://nvd.nist.gov/vuln/detail/CVE-2018-12600){: external}, [CVE-2018-13153](https://nvd.nist.gov/vuln/detail/CVE-2018-13153){: external}, [CVE-2018-14404](https://nvd.nist.gov/vuln/detail/CVE-2018-14404){: external}, [CVE-2018-14434](https://nvd.nist.gov/vuln/detail/CVE-2018-14434){: external}, [CVE-2018-14435](https://nvd.nist.gov/vuln/detail/CVE-2018-14435){: external}, [CVE-2018-14436](https://nvd.nist.gov/vuln/detail/CVE-2018-14436){: external}, [CVE-2018-14437](https://nvd.nist.gov/vuln/detail/CVE-2018-14437){: external}, [CVE-2018-14567](https://nvd.nist.gov/vuln/detail/CVE-2018-14567){: external}, [CVE-2018-15607](https://nvd.nist.gov/vuln/detail/CVE-2018-15607){: external}, [CVE-2018-16328](https://nvd.nist.gov/vuln/detail/CVE-2018-16328){: external}, [CVE-2018-16749](https://nvd.nist.gov/vuln/detail/CVE-2018-16749){: external}, [CVE-2018-16750](https://nvd.nist.gov/vuln/detail/CVE-2018-16750){: external}, [CVE-2018-18544](https://nvd.nist.gov/vuln/detail/CVE-2018-18544){: external}, [CVE-2018-18751](https://nvd.nist.gov/vuln/detail/CVE-2018-18751){: external}, [CVE-2018-19985](https://nvd.nist.gov/vuln/detail/CVE-2018-19985){: external}, [CVE-2018-20169](https://nvd.nist.gov/vuln/detail/CVE-2018-20169){: external}, [CVE-2018-20467](https://nvd.nist.gov/vuln/detail/CVE-2018-20467){: external}, [CVE-2018-20852](https://nvd.nist.gov/vuln/detail/CVE-2018-20852){: external}, [CVE-2018-5745](https://nvd.nist.gov/vuln/detail/CVE-2018-5745){: external}, [CVE-2018-7191](https://nvd.nist.gov/vuln/detail/CVE-2018-7191){: external}, [CVE-2018-8804](https://nvd.nist.gov/vuln/detail/CVE-2018-8804){: external}, [CVE-2018-9133](https://nvd.nist.gov/vuln/detail/CVE-2018-9133){: external}, [CVE-2019-10131](https://nvd.nist.gov/vuln/detail/CVE-2019-10131){: external}, [CVE-2019-10207](https://nvd.nist.gov/vuln/detail/CVE-2019-10207){: external}, [CVE-2019-10638](https://nvd.nist.gov/vuln/detail/CVE-2019-10638){: external}, [CVE-2019-10639](https://nvd.nist.gov/vuln/detail/CVE-2019-10639){: external}, [CVE-2019-10650](https://nvd.nist.gov/vuln/detail/CVE-2019-10650){: external}, [CVE-2019-11190](https://nvd.nist.gov/vuln/detail/CVE-2019-11190){: external}, [CVE-2019-11470](https://nvd.nist.gov/vuln/detail/CVE-2019-11470){: external}, [CVE-2019-11472](https://nvd.nist.gov/vuln/detail/CVE-2019-11472){: external}, [CVE-2019-11597](https://nvd.nist.gov/vuln/detail/CVE-2019-11597){: external}, [CVE-2019-11598](https://nvd.nist.gov/vuln/detail/CVE-2019-11598){: external}, [CVE-2019-11884](https://nvd.nist.gov/vuln/detail/CVE-2019-11884){: external}, [CVE-2019-12382](https://nvd.nist.gov/vuln/detail/CVE-2019-12382){: external}, [CVE-2019-12974](https://nvd.nist.gov/vuln/detail/CVE-2019-12974){: external}, [CVE-2019-12975](https://nvd.nist.gov/vuln/detail/CVE-2019-12975){: external}, [CVE-2019-12976](https://nvd.nist.gov/vuln/detail/CVE-2019-12976){: external}, [CVE-2019-12978](https://nvd.nist.gov/vuln/detail/CVE-2019-12978){: external}, [CVE-2019-12979](https://nvd.nist.gov/vuln/detail/CVE-2019-12979){: external}, [CVE-2019-13133](https://nvd.nist.gov/vuln/detail/CVE-2019-13133){: external}, [CVE-2019-13134](https://nvd.nist.gov/vuln/detail/CVE-2019-13134){: external}, [CVE-2019-13135](https://nvd.nist.gov/vuln/detail/CVE-2019-13135){: external}, [CVE-2019-13233](https://nvd.nist.gov/vuln/detail/CVE-2019-13233){: external}, [CVE-2019-13295](https://nvd.nist.gov/vuln/detail/CVE-2019-13295){: external}, [CVE-2019-13297](https://nvd.nist.gov/vuln/detail/CVE-2019-13297){: external}, [CVE-2019-13300](https://nvd.nist.gov/vuln/detail/CVE-2019-13300){: external}, [CVE-2019-13301](https://nvd.nist.gov/vuln/detail/CVE-2019-13301){: external}, [CVE-2019-13304](https://nvd.nist.gov/vuln/detail/CVE-2019-13304){: external}, [CVE-2019-13305](https://nvd.nist.gov/vuln/detail/CVE-2019-13305){: external}, [CVE-2019-13306](https://nvd.nist.gov/vuln/detail/CVE-2019-13306){: external}, [CVE-2019-13307](https://nvd.nist.gov/vuln/detail/CVE-2019-13307){: external}, [CVE-2019-13309](https://nvd.nist.gov/vuln/detail/CVE-2019-13309){: external}, [CVE-2019-13310](https://nvd.nist.gov/vuln/detail/CVE-2019-13310){: external}, [CVE-2019-13311](https://nvd.nist.gov/vuln/detail/CVE-2019-13311){: external}, [CVE-2019-13454](https://nvd.nist.gov/vuln/detail/CVE-2019-13454){: external}, [CVE-2019-13648](https://nvd.nist.gov/vuln/detail/CVE-2019-13648){: external}, [CVE-2019-14283](https://nvd.nist.gov/vuln/detail/CVE-2019-14283){: external}, [CVE-2019-14980](https://nvd.nist.gov/vuln/detail/CVE-2019-14980){: external}, [CVE-2019-14981](https://nvd.nist.gov/vuln/detail/CVE-2019-14981){: external}, [CVE-2019-15139](https://nvd.nist.gov/vuln/detail/CVE-2019-15139){: external}, [CVE-2019-15140](https://nvd.nist.gov/vuln/detail/CVE-2019-15140){: external}, [CVE-2019-15141](https://nvd.nist.gov/vuln/detail/CVE-2019-15141){: external}, [CVE-2019-15221](https://nvd.nist.gov/vuln/detail/CVE-2019-15221){: external}, [CVE-2019-15916](https://nvd.nist.gov/vuln/detail/CVE-2019-15916){: external}, [CVE-2019-16056](https://nvd.nist.gov/vuln/detail/CVE-2019-16056){: external}, [CVE-2019-16708](https://nvd.nist.gov/vuln/detail/CVE-2019-16708){: external}, [CVE-2019-16709](https://nvd.nist.gov/vuln/detail/CVE-2019-16709){: external}, [CVE-2019-16710](https://nvd.nist.gov/vuln/detail/CVE-2019-16710){: external}, [CVE-2019-16711](https://nvd.nist.gov/vuln/detail/CVE-2019-16711){: external}, [CVE-2019-16712](https://nvd.nist.gov/vuln/detail/CVE-2019-16712){: external}, [CVE-2019-16713](https://nvd.nist.gov/vuln/detail/CVE-2019-16713){: external}, [CVE-2019-16746](https://nvd.nist.gov/vuln/detail/CVE-2019-16746){: external}, [CVE-2019-16884](https://nvd.nist.gov/vuln/detail/CVE-2019-16884){: external}, [CVE-2019-17041](https://nvd.nist.gov/vuln/detail/CVE-2019-17041){: external}, [CVE-2019-17042](https://nvd.nist.gov/vuln/detail/CVE-2019-17042){: external}, [CVE-2019-17540](https://nvd.nist.gov/vuln/detail/CVE-2019-17540){: external}, [CVE-2019-17541](https://nvd.nist.gov/vuln/detail/CVE-2019-17541){: external}, [CVE-2019-18660](https://nvd.nist.gov/vuln/detail/CVE-2019-18660){: external}, [CVE-2019-19948](https://nvd.nist.gov/vuln/detail/CVE-2019-19948){: external}, [CVE-2019-19949](https://nvd.nist.gov/vuln/detail/CVE-2019-19949){: external}, [CVE-2019-2737](https://nvd.nist.gov/vuln/detail/CVE-2019-2737){: external}, [CVE-2019-2739](https://nvd.nist.gov/vuln/detail/CVE-2019-2739){: external}, [CVE-2019-2740](https://nvd.nist.gov/vuln/detail/CVE-2019-2740){: external}, [CVE-2019-2805](https://nvd.nist.gov/vuln/detail/CVE-2019-2805){: external}, [CVE-2019-3820](https://nvd.nist.gov/vuln/detail/CVE-2019-3820){: external}, [CVE-2019-3901](https://nvd.nist.gov/vuln/detail/CVE-2019-3901){: external}, [CVE-2019-5436](https://nvd.nist.gov/vuln/detail/CVE-2019-5436){: external}, [CVE-2019-6465](https://nvd.nist.gov/vuln/detail/CVE-2019-6465){: external}, [CVE-2019-6477](https://nvd.nist.gov/vuln/detail/CVE-2019-6477){: external}, [CVE-2019-7175](https://nvd.nist.gov/vuln/detail/CVE-2019-7175){: external}, [CVE-2019-7397](https://nvd.nist.gov/vuln/detail/CVE-2019-7397){: external}, [CVE-2019-7398](https://nvd.nist.gov/vuln/detail/CVE-2019-7398){: external}, [CVE-2019-9503](https://nvd.nist.gov/vuln/detail/CVE-2019-9503){: external}, [CVE-2019-9924](https://nvd.nist.gov/vuln/detail/CVE-2019-9924){: external}, [CVE-2019-9956](https://nvd.nist.gov/vuln/detail/CVE-2019-9956){: external}, [CVE-2020-1702](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1702){: external}, and[CVE-2020-8945](https://nvd.nist.gov/vuln/detail/CVE-2020-8945){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.188_1545_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.188_1545_openshift, released 30 March 2020
{: #311188_1545_worker}

The following table shows the changes that are included in the worker node fix pack update `3.11.188_1545_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 packages | 3.10.0-1062.12.1.el7 | 3.10.0-1062.18.1.el7 | Updated worker node images with package and kernel updates for [CVE-2019-19921](https://nvd.nist.gov/vuln/detail/CVE-2019-19921){: external}, [CVE-2019-11487](https://nvd.nist.gov/vuln/detail/CVE-2019-11487){: external}, [CVE-2019-17666](https://nvd.nist.gov/vuln/detail/CVE-2019-17666){: external}, and [CVE-2019-19338](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19338){: external}. |
| {{site.data.keyword.openshiftshort}} node | 3.11.170 | 3.11.188 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-188){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.170_1544_openshift" caption-side="top"}

### Changelog for 3.11.170_1544_openshift, released 16 March 2020
{: #311170_1544}

The following table shows the changes that are included in the master and worker node update `3.11.170_1544_openshift`. Master patch updates are applied automatically. Worker node patch updates can be applied by updating or reloading the worker node For more information, see [Update types](/docs/openshift?topic=openshift-openshift_versions#openshift_update_types).
{: shortdesc}

| Component | Location | Previous | Current | Description |
| --------- | -------- | ------- | -------- | ----------- |
| Calico | Master | v3.6.5 | v3.8.6 | See the [Calico release notes](https://docs.projectcalico.org/archive/v3.8/release-notes/){: external}. |
| Cluster health | Master | N/A | N/A | Cluster health status now includes links to {{site.data.keyword.cloud_notm}} documentation. |
| {{site.data.keyword.openshiftshort}} | Both | 3.11.161 | 3.11.170 | See the [{{site.data.keyword.openshiftshort}}  release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-170){: external}. |
| RHEL 7 Packages | Worker | N/A | N/A | Updated worker node images with package updates for [CVE-2020-8597](https://nvd.nist.gov/vuln/detail/CVE-2020-8597){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is where the component is located: the master, worker node, or both. The third column is the previous version number of the component. The fourth column is the current version number of the component. The fifth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.170_1543" caption-side="top"}

### Changelog for worker node fix pack 3.11.170_1543_openshift, released 17 February 2020
{: #311170_1543_worker}

The following table shows the changes that are included in the worker node fix pack update `3.11.170_1543_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} node | 3.11.161 | 3.11.170 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-170){: external}. Fixes [CVE-2019-11244](https://nvd.nist.gov/vuln/detail/CVE-2019-11244){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.161_1542_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.161_1542_openshift, released 18 February 2020
{: #311161_1542_master}

The following table shows the changes that are included in the master fix pack update `3.11.161_1542_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster master HA configuration | N/A | N/A | Updated configuration to improve availability during cluster master operations. |
| Heapster | v1.5.4 | v3.11.161 | Replaces [Kubernetes Heapster](https://github.com/kubernetes-retired/heapster/releases/tag/v1.5.4){: external} with [{{site.data.keyword.openshiftshort}} Heapster](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-161){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.15.9-240 | v1.15.10-252 | Updated to support the Kubernetes 1.15.10 release. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.161_1540_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.161_1542_openshift, released 17 February 2020
{: #311161_1542_worker}

The following table shows the changes that are included in the worker node fix pack update `3.11.161_1542_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 packages | 3.10.0-1062.9.1.el7 | 3.10.0-1062.12.1.el7 | Updated worker node images with kernel and package updates for  [CVE-2019-18408](https://nvd.nist.gov/vuln/detail/CVE-2019-18408){: external}, [CVE-2019-13734](https://nvd.nist.gov/vuln/detail/CVE-2019-13734){: external}, [CVE-2019-14816](https://nvd.nist.gov/vuln/detail/CVE-2019-14816){: external}, [CVE-2019-14895](https://nvd.nist.gov/vuln/detail/CVE-2019-14895){: external}, [CVE-2019-14898](https://nvd.nist.gov/vuln/detail/CVE-2019-14898){: external}, [CVE-2019-14901](https://nvd.nist.gov/vuln/detail/CVE-2019-14901){: external}, and [CVE-2019-17133](https://nvd.nist.gov/vuln/detail/CVE-2019-17133). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.161_1540_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.161_1540_openshift, released 3 February 2020
{: #311161_1540}

The following table shows the changes that are included in the worker node fix pack `3.11.161_1540_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 packages | N/A | N/A | Updated worker node images with package updates for [CVE-2019-13734](https://nvd.nist.gov/vuln/detail/CVE-2019-13734){: external} and [CVE-2019-18408](https://nvd.nist.gov/vuln/detail/CVE-2019-18408){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.161_1538_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.161_1539_openshift, released 3 February 2020
{: #311161_1539}

The following table shows the changes that are included in the master fix pack `3.11.161_1539_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster ingress route configuration | N/A | N/A | Fixed a bug that reset ingress route configurations to the default subdomain in clusters that were created with version [3.11.141_1524](/docs/openshift?topic=openshift-openshift_changelog#311141_1524) or earlier. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.15.7-229 | v1.15.9-240 | Updated to support the Kubernetes 1.15.9 release. Updated to use `calicoctl` version 3.8.6. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 357 | 358 | Image updated for [CVE-2019-5188](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-5188){: external}. |
| OpenVPN server | N/A | N/A | OpenVPN server is now restarted during the [cluster master refresh](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_apiserver_refresh) operation. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.161_1538_openshift" caption-side="top"}

### Changelog for 3.11.161_1538_openshift, released 20 January 2020
{: #311161_1538}

The following table shows the changes that are included in the patch `3.11.161_1538_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster master HA Proxy | 1.8.21-alpine | 1.8.23-alpine | See the [HAProxy release notes](https://www.haproxy.org/download/1.8/src/CHANGELOG){: external}. Update resolves [CVE-2019-1551](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1551){: external}. |
| etcd | v3.3.17 | v3.3.18 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.3.18){: external}. Update resolves [CVE-2019-1551](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1551){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.15.6-200 | v1.15.7-229 | Updated to support the Kubernetes 1.15.7 release.|
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 354 | 357 | <ul><li>Made the `ibmc-block-gold` storage class the default storage class for new clusters only. The default storage class for existing clusters is unchanged. If you want to set your own default, see [Changing the default storage class](/docs/openshift?topic=openshift-kube_concepts#default_storageclass).</li><li>Added the following storage classes: `ibmc-file-bronze-gid`, `ibmc-file-silver-gid`, and `ibmc-file-gold-gid`.</li><li>Fixed bugs in support of [non-root user access to an NFS file share](/docs/openshift?topic=openshift-cs_troubleshoot_storage#cs_storage_nonroot).</li><li>Resolved [CVE-2019-1551](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1551){: external}.</li></ul> |
| Key Management Service provider | 270 | 277 | Updated the {{site.data.keyword.keymanagementservicelong_notm}} Go client. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 159 | 169 | Updated image for [CVE-2019-1551](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1551){: external}. |
| {{site.data.keyword.openshiftshort}} | 3.11.154 | 3.11.161 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-161){: external}. |
| {{site.data.keyword.openshiftshort}} router configuration | N/A | N/A | Improved general availability of the {{site.data.keyword.openshiftshort}} router and enhanced the configuration for multizone clusters. Now, the router runs 3 pods with a scheduling configuration that prefers running pods across worker nodes and zones. |
| OpenVPN server | 2.4.6-r3-IKS-121 | 2.4.6-r3-IKS-131 | Updated image for [CVE-2019-1551](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1551){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.154_1537" caption-side="top"}

### Changelog for worker node fix pack 3.11.157_1537_openshift, released 23 December 2019
{: #311157_1537}

The following table shows the changes that are included in the worker node fix pack `3.11.157_1537_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 packages | N/A | N/A | Updated worker node images with package updates for [CVE-2019-11729](https://nvd.nist.gov/vuln/detail/CVE-2019-11729){: external} and [CVE-2019-11745](https://nvd.nist.gov/vuln/detail/CVE-2019-11745){: external}. |
| {{site.data.keyword.openshiftshort}} node | 3.11.154 | 3.11.157 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-157){: external}. |
| Maximum process IDs (PIDs) for pods | N/A | N/A | Updated to support scaling the maximum allowed pod process IDs (PIDs) based on the [worker node machine type](/docs/openshift?topic=openshift-planning_worker_nodes#resource_limit_node). |
{: caption="Changes since version 3.11.154_1534" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for master fix pack 3.11.154_1536_openshift, released 17 December 2019
{: #311154_1536}

The following table shows the changes that are included in the master fix pack `3.11.154_1536_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | N/A | N/A | Fixed a bug that might prevent updating the driver and plug-in components. |
| {{site.data.keyword.cloud_notm}} File Storage plug-in and monitor | 353 | 354 | Updated to support [non-root user access to an NFS file share](/docs/openshift?topic=openshift-cs_troubleshoot_storage#cs_storage_nonroot) by allocating a group ID (GID) in the storage class. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.15.6-182 | v1.15.6-200 | Updated version 1.0 and 2.0 network load balancers (NLBs) to prefer scheduling NLB pods on worker nodes that do not currently run any NLB pods. In addition, the Virtual Private Cloud (VPC) load balancer plug-in is updated to use Go version 1.12.11. |
| Key Management Service provider | 254 | 270 | Improves performance of secret management by minimizing the number of data encryption keys (DEKs) that are used to unwrap secrets in the cluster. In addition, the {{site.data.keyword.keymanagementservicelong_notm}} Go client is updated. |
{: caption="Changes since version 3.11.154_1534" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for worker node fix pack 3.11.154_1534_openshift, released 9 December 2019
{: #311154_1534_worker}

The following table shows the changes that are included in the worker node fix pack `3.11.154_1534_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 kernel and packages | 3.10.0-1062.4.3.el7 | 3.10.0-1062.9.1.el7 | Updated worker node images with kernel and package updates for [CVE-2019-14821](https://nvd.nist.gov/vuln/detail/CVE-2019-14821){: external} and [CVE-2019-15239](https://nvd.nist.gov/vuln/detail/CVE-2019-15239){: external}.|
{: caption="Changes since version 3.11.153_1533" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for worker node fix pack 3.11.154_1533_openshift, released 25 November 2019
{: #311154_1533_worker}

The following table shows the changes that are included in the worker node fix pack `3.11.154_1533_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.openshiftshort}} node | 3.11.153 | 3.11.154 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-154){: external}.|
| RHEL 7 kernel and packages | 3.10.0-1062.4.1.el7 | 3.10.0-1062.4.3.el7 | Updated worker node images with kernel and package updates for [CVE-2018-12207](https://nvd.nist.gov/vuln/detail/CVE-2018-12207){: external}, [CVE-2019-0154](https://nvd.nist.gov/vuln/detail/CVE-2019-0154){: external}, [CVE-2019-11135](https://nvd.nist.gov/vuln/detail/CVE-2019-11135){: external}, and [CVE-2019-0155](https://nvd.nist.gov/vuln/detail/CVE-2019-0155).|
{: caption="Changes since version 3.11.153_1530" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for master fix pack 3.11.154_1533_openshift, released 21 November 2019
{: #311154_1533}

The following table shows the changes that are included in the master fix pack `3.11.154_1533_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | 1.15.2 | 1.15.4 | Updated to use `Go` version 1.13.4. |
| {{site.data.keyword.cloud_notm}} File Storage plug-in and monitor | 350 | 353 | Updated to use the `distroless/static` base image and to use `Go` version 1.12.11. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.15.5-119 | v1.15.6-182 | Updated to support the Kubernetes 1.15.6 release. Updated to use `Go` version 1.12.12 and `calicoctl` version v3.8.4. |
| Key Management Service provider | 237 | 254 | Updated to use `Go` version 1.12.13. |
| {{site.data.keyword.openshiftshort}} | 3.11.153 | 3.11.154 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-154){: external}. Update resolves [CVE-2019-11253](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-11253){: external} (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/1126071){: external}). |
{: caption="Changes since version 3.11.153_1530" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for worker node fix pack 3.11.153_1530_openshift, released 11 November 2019
{: #311153_1530}

The following table shows the changes that are included in the worker node fix pack `3.11.153_1530_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 packages | N/A | N/A | Updated worker node images with package updates. |
{: caption="Changes since version 3.11.146_1529" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for worker node fix pack 3.11.153_1529_openshift, released 28 October 2019
{: #311153_1529}

The following table shows the changes that are included in the worker node fix pack `3.11.153_1529_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.openshiftshort}} node | 3.11.146 | 3.11.153 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-153){: external}.|
| RHEL 7 packages and kernel |  3.10.0-1062.1.2.el7 | 3.10.0-1062.4.1.el7 | Updated worker node images with kernel and package updates for [CVE-2019-14835](https://nvd.nist.gov/vuln/detail/CVE-2019-14835){: external}, [CVE-2019-14287](https://nvd.nist.gov/vuln/detail/CVE-2019-14287){: external}, [CVE-2019-3846](https://nvd.nist.gov/vuln/detail/CVE-2019-3846) [CVE-2019-10126](https://nvd.nist.gov/vuln/detail/CVE-2019-10126){: external}, [CVE-2019-9506](https://nvd.nist.gov/vuln/detail/CVE-2019-9506){: external}, and [CVE-2018-20856](https://nvd.nist.gov/vuln/detail/CVE-2018-20856){: external}. |
{: caption="Changes since version 3.11.146_1528" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for master fix pack 3.11.146_1528_openshift, released 22 October 2019
{: #311146_1528}

The following table shows the changes that are included in the master fix pack `3.11.146_1528_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| etcd | v3.3.15 | v3.3.17 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.3.17){: external}. Update resolves [CVE-2019-1547](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1547){: external}, [CVE-2019-1549](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1549){: external}, and [CVE-2019-1563](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1563){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | N/A | N/A | Fixed a bug so that the driver and plug-in components can be updated. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.15.3-112 | v1.15.5-119 | Updated to support the Kubernetes 1.15.5 release. Update resolves [CVE-2019-16276](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16276){: external}. |
| {{site.data.keyword.cloud_notm}} File Storage plug-in and monitor | 349 | 350 | Updated image for [CVE-2019-1547](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1547){: external}, [CVE-2019-1549](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1549){: external}, and [CVE-2019-1563](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1563){: external}. |
| Key Management Service provider | 221 | 237 | Updated image for [CVE-2019-16276](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16276){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} provider | 153 | 159 | Updated image for [CVE-2019-1547](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1547){: external}, [CVE-2019-1549](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1549){: external}, [CVE-2019-1563](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1563){: external}, and [CVE-2019-16276](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16276){: external}. |
{: caption="Changes since version 3.11.146_1527" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for worker node fix pack 3.11.146_1527_openshift, released 14 October 2019
{: #311146_1527}

The following table shows the changes that are included in the worker node fix pack `3.11.146_1527_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 packages and kernel | N/A | N/A | Updated worker node images with package updates. |
{: caption="Changes since version 3.11.146_1525" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for master fix pack 3.11.146_1526_openshift, released 4 October 2019
{: #311146_1526}

The following table shows the changes that are included in the master fix pack `3.11.146_1526_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Default IBM security context constraints | N/A | N/A | To support [{{site.data.keyword.cloud_notm}} Paks](https://www.ibm.com/cloud/paks/){: external}, the `seLinuxContext` setting is changed from `MustRunAs` to `RunAsAny` for the following [default IBM security context constraints](/docs/openshift?topic=openshift-openshift_scc#ibm_sccs): `ibm-anyuid-hostaccess-scc`, `ibm-anyuid-hostpath-scc`, and `ibm-anyuid-scc`. |
{: caption="Changes since version 3.11.146_1525" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for 3.11.146_1525_openshift, released 3 October 2019
{: #311146_1525}

The following table shows the changes that are included in the patch `3.11.146_1525_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Calico | v3.6.4 | v3.6.4 | See the [Calico release notes](https://docs.projectcalico.org/archive/v3.6/release-notes/){: external}.|
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | 1.15.1 | 1.15.2 | Fixed an issue that might cause worker nodes to fail in a `NotReady` status or pods not to start because of networking errors. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.11.10-286 | v1.15.3-112 | Updated to support the Kubernetes 1.15.3 release. |
| {{site.data.keyword.openshiftshort}} | 3.11.141 | 3.11.146 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-146){: external}. Update resolves [CVE-2019-11247](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-11247){: external} (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/1101957){: external}) and [CVE-2019-11249](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-11249){: external} (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/1102029){: external}).|
| OpenVPN server | 2.4.6-r3-IKS-115 | 2.4.6-r3-IKS-121 | Image updated for [CVE-2019-1547](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1547){: external} and [CVE-2019-1563](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1563){: external}. |
| RHEL 7 packages and kernel | 3.10.0-1062.1.1 | 3.10.0-1062.1.2 | Updated worker node images with kernel and package updates for [CVE-2019-1125](https://nvd.nist.gov/vuln/detail/CVE-2019-14835){: external}. |
{: caption="Changes since version 3.11.141_1524" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for 3.11.141_1524_openshift, released 16 September 2019
{: #311141_1524}

The following table shows the changes that are included in the patch `3.11.141_1524_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Key Management Service provider | 212 | 216 | Improved Kubernetes [key management service provider](/docs/openshift?topic=openshift-encryption#keyprotect) caching of {{site.data.keyword.cloud_notm}} IAM tokens. In addition, fixed a problem with Kubernetes secret decryption when the cluster's root key is rotated.|
| {{site.data.keyword.openshiftshort}} | 3.11.135 | 3.11.141 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-141){: external}. |
| RHEL 7 packages and kernel | 3.10.0-1062 | 3.10.0-1062.1.1 | Updated worker node images with kernel and package updates for [CVE-2019-1125](https://nvd.nist.gov/vuln/detail/CVE-2019-1125){: external} and [CVE-2019-9500](https://nvd.nist.gov/vuln/detail/CVE-2019-9500){: external}. |
{: caption="Changes since version 3.11.135_1523" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for worker node fix pack 3.11.135_1523_openshift, released 3 September 2019
{: #311135_1523_worker}

The following table shows the changes that are included in the worker node fix pack `3.11.135_1523_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 packages | N/A | N/A | Updated worker node images with package updates.|
{: caption="Changes since version 3.11.135_1521" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for master fix pack 3.11.135_1522_openshift, released 28 August 2019
{: #311135_1522}

The following table shows the changes that are included in the master fix pack `3.11.135_1522_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Default IBM security context constraints | N/A | N/A | Added `ibm-restricted-scc` to [Default IBM security context constraints](/docs/openshift?topic=openshift-openshift_scc#ibm_sccs). |
| `etcd` | v3.3.13 | v3.3.15 | See the [`etcd` release notes](https://github.com/etcd-io/etcd/releases/v3.3.15){: external}. Update resolves [CVE-2019-9512](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9512){: external}, [CVE-2019-9514](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9514){: external}, and [CVE-2019-14809](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14809){: external}. |
| {{site.data.keyword.cloud_notm}} File Storage plug-in | 348 | 349 | Image updated for [CVE-2019-9512](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9512){: external}, [CVE-2019-9514](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9514){: external}, and [CVE-2019-14809](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14809){: external}. |
| Key Management Service provider | 207 | 212 | Image updated for [CVE-2019-9512](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9512){: external}, [CVE-2019-9514](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9514){: external}, and [CVE-2019-14809](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14809){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 147 | 148 | Image updated for [CVE-2019-9512](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9512){: external}, [CVE-2019-9514](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9514){: external}, and [CVE-2019-14809](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14809){: external}. |
{: caption="Changes since version 3.11.135_1521" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for worker node fix pack 3.11.135_1521_openshift, released 19 August 2019
{: #311135_1521_worker}

The following table shows the changes that are included in the worker node fix pack `3.11.135_1521_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster master HA Proxy | 2.0.1-alpine | 1.8.21-alpine | Moved to HA Proxy 1.8 to fix [socket leak in HA Proxy](https://github.com/haproxy/haproxy/issues/136){: external}. Added a liveliness check to monitor the health of HA Proxy. For more information about other changes, see [release notes](https://www.haproxy.org/download/1.8/src/CHANGELOG){: external}. |
| {{site.data.keyword.openshiftshort}} node | 3.11.129 | 3.11.135 | For more information, see the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-135){: external}. |
| RHEL 7 kernel | 3.10.0-957.21.3.el7 | 3.10.0-1062.el7 | Updated worker node images with kernel and package updates for [CVE-2018-16881](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-168810){: external}, [CVE-2019-6470](https://nvd.nist.gov/vuln/detail/CVE-2019-6470){: external}, [CVE-2018-14618](https://nvd.nist.gov/vuln/detail/CVE-2018-14618){: external}, [CVE-2018-16062](https://nvd.nist.gov/vuln/detail/CVE-2018-16062){: external}, [CVE-2018-16402](https://nvd.nist.gov/vuln/detail/CVE-2018-16402){: external}, [CVE-2018-16403](https://nvd.nist.gov/vuln/detail/CVE-2018-16403){: external}, [CVE-2018-18310](https://nvd.nist.gov/vuln/detail/CVE-2018-18310){: external}, [CVE-2018-18520](https://nvd.nist.gov/vuln/detail/CVE-2018-18520){: external}, [CVE-2018-18521](https://nvd.nist.gov/vuln/detail/CVE-2018-18521){: external}, [CVE-2019-7149](https://nvd.nist.gov/vuln/detail/CVE-2019-7149){: external}, [CVE-2019-7150](https://nvd.nist.gov/vuln/detail/CVE-2019-7150){: external}, [CVE-2019-7664](https://nvd.nist.gov/vuln/detail/CVE-2019-7664){: external}, [CVE-2019-7665](https://nvd.nist.gov/vuln/detail/CVE-2019-7665){: external}, [CVE-2016-10739](https://nvd.nist.gov/vuln/detail/CVE-2016-10739){: external}, [CVE-2018-16871](https://nvd.nist.gov/vuln/detail/CVE-2018-16871){: external}, [CVE-2018-16884](https://nvd.nist.gov/vuln/detail/CVE-2018-16884){: external}, [CVE-2019-11085](https://nvd.nist.gov/vuln/detail/CVE-2019-11085){: external}, [CVE-2019-11811](https://nvd.nist.gov/vuln/detail/CVE-2019-11811){: external}, [CVE-2018-15686](https://nvd.nist.gov/vuln/detail/CVE-2018-15686){: external}, [CVE-2018-16866](https://nvd.nist.gov/vuln/detail/CVE-2018-16866){: external}, [CVE-2018-16888](https://nvd.nist.gov/vuln/detail/CVE-2018-16888){: external}, [CVE-2018-12327](https://nvd.nist.gov/vuln/detail/CVE-2018-12327){: external}, [CVE-2018-12641](https://nvd.nist.gov/vuln/detail/CVE-2018-12641){: external}, [CVE-2018-12697](https://nvd.nist.gov/vuln/detail/CVE-2018-12697){: external}, [CVE-2018-1000876](https://nvd.nist.gov/vuln/detail/CVE-2018-1000876){: external}, [CVE-2018-16842](https://nvd.nist.gov/vuln/detail/CVE-2018-16842){: external}, [CVE-2018-5741](https://nvd.nist.gov/vuln/detail/CVE-2018-5741){: external}, [CVE-2018-0495](https://nvd.nist.gov/vuln/detail/CVE-2018-0495){: external}, [CVE-2018-12404](https://nvd.nist.gov/vuln/detail/CVE-2018-12404){: external}, [CVE-2018-1122](https://nvd.nist.gov/vuln/detail/CVE-2018-1122){: external}, [CVE-2018-7755](https://nvd.nist.gov/vuln/detail/CVE-2018-7755){: external}, [CVE-2018-8087](https://nvd.nist.gov/vuln/detail/CVE-2018-8087){: external}, [CVE-2018-9363](https://nvd.nist.gov/vuln/detail/CVE-2018-9363){: external}, [CVE-2018-9516](https://nvd.nist.gov/vuln/detail/CVE-2018-9516){: external}, [CVE-2018-9517](https://nvd.nist.gov/vuln/detail/CVE-2018-9517){: external}, [CVE-2018-10853](https://nvd.nist.gov/vuln/detail/CVE-2018-10853){: external}, [CVE-2018-13053](https://nvd.nist.gov/vuln/detail/CVE-2018-13053){: external}, [CVE-2018-13093](https://nvd.nist.gov/vuln/detail/CVE-2018-13093){: external}, [CVE-2018-13094](https://nvd.nist.gov/vuln/detail/CVE-2018-13094){: external}, [CVE-2018-13095](https://nvd.nist.gov/vuln/detail/CVE-2018-13095){: external}, [CVE-2018-14625](https://nvd.nist.gov/vuln/detail/CVE-2018-14625){: external}, [CVE-2018-14734](https://nvd.nist.gov/vuln/detail/CVE-2018-14734){: external}, [CVE-2018-15594](https://nvd.nist.gov/vuln/detail/CVE-2018-15594){: external}, [CVE-2018-16658](https://nvd.nist.gov/vuln/detail/CVE-2018-16658){: external}, [CVE-2018-16885](https://nvd.nist.gov/vuln/detail/CVE-2018-16885){: external}, [CVE-2018-18281](https://nvd.nist.gov/vuln/detail/CVE-2018-18281){: external}, [CVE-2019-3459](https://nvd.nist.gov/vuln/detail/CVE-2019-3459){: external}, [CVE-2019-3460](https://nvd.nist.gov/vuln/detail/CVE-2019-3460){: external}, [CVE-2019-3882](https://nvd.nist.gov/vuln/detail/CVE-2019-3882){: external}, [CVE-2019-3900](https://nvd.nist.gov/vuln/detail/CVE-2019-3900){: external}, [CVE-2019-5489](https://nvd.nist.gov/vuln/detail/CVE-2019-5489){: external}, [CVE-2018-18074](https://nvd.nist.gov/vuln/detail/CVE-2018-18074){: external}, [CVE-2019-3858](https://nvd.nist.gov/vuln/detail/CVE-2019-3858){: external}, [CVE-2019-3861](https://nvd.nist.gov/vuln/detail/CVE-2019-3861){: external}, [CVE-2019-3862](https://nvd.nist.gov/vuln/detail/CVE-2019-3862){: external}, [CVE-2018-14647](https://nvd.nist.gov/vuln/detail/CVE-2018-14647){: external}, [CVE-2019-5010](https://nvd.nist.gov/vuln/detail/CVE-2019-5010){: external}, [CVE-2019-9740](https://nvd.nist.gov/vuln/detail/CVE-2019-9740){: external}, [CVE-2019-9947](https://nvd.nist.gov/vuln/detail/CVE-2019-9947){: external}, [CVE-2019-9948](https://nvd.nist.gov/vuln/detail/CVE-2019-9948){: external}, [CVE-2017-14503](https://nvd.nist.gov/vuln/detail/CVE-2017-14503){: external}, [CVE-2018-1000877](https://nvd.nist.gov/vuln/detail/CVE-2018-1000877){: external}, [CVE-2018-1000878](https://nvd.nist.gov/vuln/detail/CVE-2018-1000878){: external}, [CVE-2019-1000019](https://nvd.nist.gov/vuln/detail/CVE-2019-1000019){: external}, [CVE-2019-1000020](https://nvd.nist.gov/vuln/detail/CVE-2019-1000020){: external}, [CVE-2018-3058](https://nvd.nist.gov/vuln/detail/CVE-2018-3058){: external}, [CVE-2018-3063](https://nvd.nist.gov/vuln/detail/CVE-2018-3063){: external}, [CVE-2018-3066](https://nvd.nist.gov/vuln/detail/CVE-2018-3066){: external}, [CVE-2018-3081](https://nvd.nist.gov/vuln/detail/CVE-2018-3081){: external}, [CVE-2018-3282](https://nvd.nist.gov/vuln/detail/CVE-2018-3282){: external}, [CVE-2019-2503](https://nvd.nist.gov/vuln/detail/CVE-2019-2503){: external}, [CVE-2019-2529](https://nvd.nist.gov/vuln/detail/CVE-2019-2529){: external}, [CVE-2019-2614](https://nvd.nist.gov/vuln/detail/CVE-2019-2614){: external}, [CVE-2019-2627](https://nvd.nist.gov/vuln/detail/CVE-2019-2627){: external}, [CVE-2018-14348](https://nvd.nist.gov/vuln/detail/CVE-2018-14348){: external}, [CVE-2018-15473](https://nvd.nist.gov/vuln/detail/CVE-2018-15473){: external}, [CVE-2018-5383](https://nvd.nist.gov/vuln/detail/CVE-2018-5383){: external}, [CVE-2018-19788](https://nvd.nist.gov/vuln/detail/CVE-2018-19788){: external}, [CVE-2018-0734](https://nvd.nist.gov/vuln/detail/CVE-2018-0734){: external}, [CVE-2019-1559](https://nvd.nist.gov/vuln/detail/CVE-2019-1559){: external}, [CVE-2018-20060](https://nvd.nist.gov/vuln/detail/CVE-2018-20060){: external}, and [CVE-2019-11236](https://nvd.nist.gov/vuln/detail/CVE-2019-11236){: external}. |
{: caption="Changes since version 3.11.129_1518" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for master fix pack 3.11.135_1521_openshift, released 17 August 2019
{: #311135_1521_master}

The following table shows the changes that are included in the master fix pack `3.11.135_1521_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Key Management Service provider | 167 | 207 | Fixed an issue that causes the Kubernetes key management service (KMS) provider to fail to manage Kubernetes secrets. |
{: caption="Changes since version 3.11.135_1520" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for master fix pack 3.11.135_1520_openshift, released 15 August 2019
{: #311135_1520_master}

The following table shows the changes that are included in the master fix pack `3.11.135_1520_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Calico configuration | N/A | N/A | Calico `calico-kube-controllers` deployment in the `kube-system` namespace sets a memory limit on the `calico-kube-controllers` container. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | 1.15 | 1.15.1 | Image updated for [CVE-2019-14697](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14697){: external}. |
| {{site.data.keyword.cloud_notm}} File Storage plug-in | 347 | 348 | Image updated for [CVE-2019-14697](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14697){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 146 | 147 | Image updated for [CVE-2019-14697](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14697){: external}. |
| {{site.data.keyword.openshiftshort}} | 3.11.129 | 3.11.135 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-135){: external}. |
| OpenVPN client | 2.4.6-r3-IKS-90 | 2.4.6-r3-IKS-116 | Image updated for [CVE-2019-14697](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14697){: external}. |
| OpenVPN server | 2.4.6-r3-IKS-25 | 2.4.6-r3-IKS-115 | Image updated for [CVE-2019-14697](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14697){: external}. |
{: caption="Changes since version 3.11.129_1517" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for worker node patch 3.11.129_1518_openshift, released 5 August 2019
{: #311129_1518_worker}

The following table shows the changes that are included in the worker node patch `3.11.129_1518_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 packages | N/A | N/A | Updated base packages in the worker node Red Hat Enterprise Linux image. |
{: caption="Changes since version 3.11.129_1517" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for 3.11.129_1517_openshift, released 2 August 2019
{: #311129_1517}

The following table shows the changes that are included in the patch `3.11.129_1517_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster DNS configuration| N/A | N/A | For security reasons, enhanced local `dnsmasq` cache to listen on only `localhost`. Changed the DNS `targetPort` for the `kubernetes` cluster service from `8053` to `53`. |
| Cluster master HA proxy| 1.9.7-alpine| 2.0.1-alpine | See the [HAProxy release notes](https://www.haproxy.org/download/2.0/src/CHANGELOG){: external}. |
| Cluster router configuration| N/A | N/A | Fixed bugs that might cause cluster master operations, such as `refresh` or `update`, to fail when the router configuration is updated. These fixes also improve master availability during such operations. |
{: caption="Changes since version 3.11.129_1515" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
