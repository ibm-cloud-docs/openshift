---

copyright:
  years: 2023, 2024
lastupdated: "2024-04-25"


keywords: openshift, 4.12, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# Version 4.12 change log
{: #openshift_changelog_412}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.12. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #openshift_changelog_overview_412}

Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security){: external} for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}



### Change log for master fix pack 4.12.55_1588_openshift, released 24 April 2024
{: #41255_1588_openshift_M}

The following table shows the changes that are in the master fix pack 4.12.55_1588_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.4.8 | v1.5.4 | New version contains updates and security fixes. |
| etcd | v3.5.12 | v3.5.13 | See the [etcd release notes](https://github.com/coreos/etcd/releases/v3.5.13){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.16-33 | v1.25.16-42 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | bd30030 | 4c5d156 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.8 | v2.8.9 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2831 | 2867 | New version contains updates and security fixes. |
| OpenVPN client | 2.6.8-r0-IKS-110 | 2.6.8-r0-IKS-114 | New version contains updates and security fixes. |
| OpenVPN server | 2.6.8-r0-IKS-109 | 2.6.8-r0-IKS-113 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.5.13 | v1.5.14 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.12 | v0.13.13 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.13){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.12.51 | 4.12.55 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-55){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | 4.12.0+20240208 | 4.12.0+20240412 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20240412){: external}. |
{: caption="Changes since version 4.12.51_1585_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.55_1589_openshift, released 22 April 2024
{: #41255_1589_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.55_1589_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.54 | 4.12.55 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-55){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-513.24.1.el8_9 | Worker node package updates for [RHSA-2024:1782](https://access.redhat.com/errata/RHSA-2024:1782){: external}, [CVE-2023-4408](https://nvd.nist.gov/vuln/detail/CVE-2023-4408){: external}, [CVE-2023-50387](https://nvd.nist.gov/vuln/detail/CVE-2023-50387){: external}, [CVE-2023-50868](https://nvd.nist.gov/vuln/detail/CVE-2023-50868){: external}, [RHSA-2024:1784](https://access.redhat.com/errata/RHSA-2024:1784){: external}, [CVE-2024-28834](https://nvd.nist.gov/vuln/detail/CVE-2024-28834){: external}. |
| HAProxy | 295dba8 | 4e826da | Security fixes for [CVE-2024-28834](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2024-28834){: external}. |
{: caption="Changes since version 4.12.54_1587_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.54_1587_openshift, released 8 April 2024
{: #41254_1587_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.54_1587_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.53 | 4.12.54 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-54){: external}. |
| RHEL 8 Packages | 4.18.0-513.18.1.el8_9 | 4.18.0-513.24.1.el8_9 | Worker node and kernel packages for [RHSA-2024:1607](https://access.redhat.com/errata/RHSA-2024:1607){: external}, [CVE-2021-33631](https://nvd.nist.gov/vuln/detail/CVE-2021-33631){: external}, [CVE-2022-38096](https://nvd.nist.gov/vuln/detail/CVE-2022-38096){: external}, [CVE-2023-51042](https://nvd.nist.gov/vuln/detail/CVE-2023-51042){: external}, [CVE-2023-6546](https://nvd.nist.gov/vuln/detail/CVE-2023-6546){: external}, [CVE-2023-6931](https://nvd.nist.gov/vuln/detail/CVE-2023-6931){: external}, [CVE-2024-0565](https://nvd.nist.gov/vuln/detail/CVE-2024-0565){: external}, [CVE-2024-1086](https://nvd.nist.gov/vuln/detail/CVE-2024-1086){: external}, [RHSA-2024:1601](https://access.redhat.com/errata/RHSA-2024:1601){: external}, [CVE-2023-28322](https://nvd.nist.gov/vuln/detail/CVE-2023-28322){: external}, [CVE-2023-38546](https://nvd.nist.gov/vuln/detail/CVE-2023-38546){: external}, [CVE-2023-46218](https://nvd.nist.gov/vuln/detail/CVE-2023-46218){: external}, [RHSA-2024:1615](https://access.redhat.com/errata/RHSA-2024:1615){: external}, [CVE-2023-52425](https://nvd.nist.gov/vuln/detail/CVE-2023-52425){: external}, [RHSA-2024:1610](https://access.redhat.com/errata/RHSA-2024:1610){: external}, [CVE-2022-48624](https://nvd.nist.gov/vuln/detail/CVE-2022-48624){: external}. |
| HAProxy | 512b32a | 295dba8 | Security fixes for [CVE-2023-28322](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-28322){: external}, [CVE-2023-38546](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-38546){: external}, [CVE-2023-46218](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-46218){: external}, [CVE-2023-52425](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-52425){: external}. |
| CRI-O | 1.25.5-8 | 1.25.5-8 | N/A |
{: caption="Changes since version 4.12.53_1586_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.51_1585_openshift, released 27 March 2024
{: #41251_1585_openshift_M}

The following table shows the changes that are in the master fix pack 4.12.51_1585_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.18 | v2.4.19 | https://github.ibm.com/alchemy-containers/armada-storage-block-plugin |
| {{site.data.keyword.IBM_notm}} Calico extension | 1534 | 1537 | New version contains security fixes. |
| Cluster health image | v1.4.7 | v1.4.8 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.16-24 | v1.25.16-33 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.7 | v2.8.8 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2807 | 2831 | https://github.ibm.com/alchemy-containers/armada-keepalived |
| {{site.data.keyword.openshiftshort}}. | 4.12.49 | 4.12.51 | https://docs.openshift.com/container-platform/ |
| OpenVPN Operator image | v1.4.33 | v1.5.13 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.11 | v0.13.12 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.12){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 441 | 442 | New version contains updates and security fixes. |
{: caption="Changes since version 4.12.49_1581_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.53_1586_openshift, released 25 March 2024
{: #41253_1586_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.53_1586_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.51 | 4.12.53 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-53){: external}. |
| RHEL 8 Packages | 4.18.0-513.18.1.el8_9 | 4.18.0-513.18.1.el8_9 | N/A |
| CRI-O | 1.25.5-8 | 1.25.5-8 | N/A |
| HAProxy | 512b32 | 512b32 | N/A |
{: caption="Changes since version 4.12.51_1583_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.51_1583_openshift, released 13 March 2024
{: #41251_1583_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.51_1583_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.50 | 4.12.51 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-51){: external}. |
| RHEL 8 Packages | 4.18.0-513.18.1.el8_9 | 4.18.0-513.18.1.el8_9 | N/A |
| HAProxy | a13673 | 512b32 | N/A |
| CRI-O | 1.25.5-8 | 1.25.5-8 | N/A |
{: caption="Changes since version 4.12.50_1582_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.49_1581_openshift, released 28 February 2024
{: #41249_1581_openshift_M}

The following table shows the changes that are in the master fix pack 4.12.49_1581_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.4.6 | v1.4.7 | New version contains updates and security fixes. |
| etcd | v3.5.11 | v3.5.12 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.12){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1525 | 1534 | New version contains security fixes. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.14 | v2.4.18 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.16-17 | v1.25.16-24 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 439 | 441 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 7185ea1 | bd30030 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.6 | v2.8.7 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2789 | 2807 | New version contains updates and security fixes. |
| OpenVPN client | 2.6.8-r0-IKS-108 | 2.6.8-r0-IKS-110 | New version contains updates and security fixes. |
| OpenVPN server | 2.6.8-r0-IKS-107 | 2.6.8-r0-IKS-109 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.4.32 | v1.4.33 | New version contains updates and security fixes. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.12.46 | 4.12.49 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-49){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.12.0-20240104 | v4.12.0-20240208 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0%2B20240208){: external}. |
{: caption="Changes since version 4.12.46_1576_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.50_1582_openshift, released 26 February 2024
{: #41250_1582_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.50_1582_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.49| 4.12.50 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-50){: external}. |
| RHEL 8 Packages| 4.18.0-513.11.1.el8_9 | 4.18.0-513.18.1.el8_9 | Package updates for [RHSA-2024:0897](https://access.redhat.com/errata/RHSA-2024:0897){: external}, [CVE-2022-3545](https://nvd.nist.gov/vuln/detail/CVE-2022-3545){: external}, [CVE-2022-41858](https://nvd.nist.gov/vuln/detail/CVE-2022-41858){: external}, [CVE-2023-1073](https://nvd.nist.gov/vuln/detail/CVE-2023-1073){: external}, [CVE-2023-1838](https://nvd.nist.gov/vuln/detail/CVE-2023-1838){: external}, [CVE-2023-2166](https://nvd.nist.gov/vuln/detail/CVE-2023-2166){: external}, [CVE-2023-2176](https://nvd.nist.gov/vuln/detail/CVE-2023-2176){: external}, [CVE-2023-40283](https://nvd.nist.gov/vuln/detail/CVE-2023-40283){: external}, [CVE-2023-45871](https://nvd.nist.gov/vuln/detail/CVE-2023-45871){: external}, [CVE-2023-4623](https://nvd.nist.gov/vuln/detail/CVE-2023-4623){: external}, [CVE-2023-46813](https://nvd.nist.gov/vuln/detail/CVE-2023-46813){: external}, [CVE-2023-4921](https://nvd.nist.gov/vuln/detail/CVE-2023-4921){: external}, [CVE-2023-5717](https://nvd.nist.gov/vuln/detail/CVE-2023-5717){: external}, [CVE-2023-6356](https://nvd.nist.gov/vuln/detail/CVE-2023-6356){: external}, [CVE-2023-6535](https://nvd.nist.gov/vuln/detail/CVE-2023-6535){: external}, [CVE-2023-6536](https://nvd.nist.gov/vuln/detail/CVE-2023-6536){: external}, [CVE-2023-6606](https://nvd.nist.gov/vuln/detail/CVE-2023-6606){: external}, [CVE-2023-6610](https://nvd.nist.gov/vuln/detail/CVE-2023-6610){: external}, [CVE-2023-6817](https://nvd.nist.gov/vuln/detail/CVE-2023-6817){: external}, [CVE-2024-0646](https://nvd.nist.gov/vuln/detail/CVE-2024-0646){: external}, [RHSA-2024:0768](https://access.redhat.com/errata/RHSA-2024:0768){: external}, [CVE-2020-28241](https://nvd.nist.gov/vuln/detail/CVE-2020-28241){: external}, [RHSA-2024:0889](https://access.redhat.com/errata/RHSA-2024:0889){: external}, [CVE-2019-13224](https://nvd.nist.gov/vuln/detail/CVE-2019-13224){: external}, [CVE-2019-16163](https://nvd.nist.gov/vuln/detail/CVE-2019-16163){: external}, [CVE-2019-19012](https://nvd.nist.gov/vuln/detail/CVE-2019-19012){: external}, [CVE-2019-19203](https://nvd.nist.gov/vuln/detail/CVE-2019-19203){: external}, [CVE-2019-19204](https://nvd.nist.gov/vuln/detail/CVE-2019-19204){: external}, [RHSA-2024:0811](https://access.redhat.com/errata/RHSA-2024:0811){: external}, [CVE-2023-28486](https://nvd.nist.gov/vuln/detail/CVE-2023-28486){: external}, [CVE-2023-28487](https://nvd.nist.gov/vuln/detail/CVE-2023-28487){: external}, [CVE-2023-42465](https://nvd.nist.gov/vuln/detail/CVE-2023-42465){: external}. |
{: caption="Changes since version 4.12.49_1578_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.49_1578_openshift, released 12 February 2024
{: #41249_1578_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.49_1578_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.47 | 4.12.49 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-49){: external}. |
| RHEL 8 Packages | 4.18.0-477.27.1.el8_8 | 4.18.0-513.11.1.el8_9 | Package updates for [RHSA-2024:0752](https://access.redhat.com/errata/RHSA-2024:0752){: external}, [CVE-2024-21626](https://nvd.nist.gov/vuln/detail/CVE-2024-21626){: external}, [RHSA-2023:7549](https://access.redhat.com/errata/RHSA-2023:7549){: external}, [CVE-2022-45884](https://nvd.nist.gov/vuln/detail/CVE-2022-45884){: external}, [CVE-2022-45886](https://nvd.nist.gov/vuln/detail/CVE-2022-45886){: external}, [CVE-2022-45919](https://nvd.nist.gov/vuln/detail/CVE-2022-45919){: external}, [CVE-2023-1192](https://nvd.nist.gov/vuln/detail/CVE-2023-1192){: external}, [CVE-2023-2163](https://nvd.nist.gov/vuln/detail/CVE-2023-2163){: external}, [CVE-2023-3812](https://nvd.nist.gov/vuln/detail/CVE-2023-3812){: external}, [CVE-2023-5178](https://nvd.nist.gov/vuln/detail/CVE-2023-5178){: external}, [RHSA-2024:0113](https://access.redhat.com/errata/RHSA-2024:0113){: external}, [CVE-2022-36402](https://nvd.nist.gov/vuln/detail/CVE-2022-36402){: external}, [CVE-2023-20569](https://nvd.nist.gov/vuln/detail/CVE-2023-20569){: external}, [CVE-2023-2162](https://nvd.nist.gov/vuln/detail/CVE-2023-2162){: external}, [CVE-2023-42753](https://nvd.nist.gov/vuln/detail/CVE-2023-42753){: external}, [CVE-2023-4622](https://nvd.nist.gov/vuln/detail/CVE-2023-4622){: external}, [CVE-2023-5633](https://nvd.nist.gov/vuln/detail/CVE-2023-5633){: external}, [RHSA-2023:7077](https://access.redhat.com/errata/RHSA-2023:7077){: external}, [CVE-2021-43975](https://nvd.nist.gov/vuln/detail/CVE-2021-43975){: external}, [CVE-2022-28388](https://nvd.nist.gov/vuln/detail/CVE-2022-28388){: external}, [CVE-2022-3594](https://nvd.nist.gov/vuln/detail/CVE-2022-3594){: external}, [CVE-2022-3640](https://nvd.nist.gov/vuln/detail/CVE-2022-3640){: external}, [CVE-2022-38457](https://nvd.nist.gov/vuln/detail/CVE-2022-38457){: external}, [CVE-2022-40133](https://nvd.nist.gov/vuln/detail/CVE-2022-40133){: external}, [CVE-2022-40982](https://nvd.nist.gov/vuln/detail/CVE-2022-40982){: external}, [CVE-2022-42895](https://nvd.nist.gov/vuln/detail/CVE-2022-42895){: external}, [CVE-2022-45869](https://nvd.nist.gov/vuln/detail/CVE-2022-45869){: external}, [CVE-2022-45887](https://nvd.nist.gov/vuln/detail/CVE-2022-45887){: external}, [CVE-2022-4744](https://nvd.nist.gov/vuln/detail/CVE-2022-4744){: external}, [CVE-2023-0458](https://nvd.nist.gov/vuln/detail/CVE-2023-0458){: external}, [CVE-2023-0590](https://nvd.nist.gov/vuln/detail/CVE-2023-0590){: external}, [CVE-2023-0597](https://nvd.nist.gov/vuln/detail/CVE-2023-0597){: external}, [CVE-2023-1073](https://nvd.nist.gov/vuln/detail/CVE-2023-1073){: external}, [CVE-2023-1074](https://nvd.nist.gov/vuln/detail/CVE-2023-1074){: external}, [CVE-2023-1075](https://nvd.nist.gov/vuln/detail/CVE-2023-1075){: external}, [CVE-2023-1079](https://nvd.nist.gov/vuln/detail/CVE-2023-1079){: external}, [CVE-2023-1118](https://nvd.nist.gov/vuln/detail/CVE-2023-1118){: external}, [CVE-2023-1206](https://nvd.nist.gov/vuln/detail/CVE-2023-1206){: external}, [CVE-2023-1252](https://nvd.nist.gov/vuln/detail/CVE-2023-1252){: external}, [CVE-2023-1382](https://nvd.nist.gov/vuln/detail/CVE-2023-1382){: external}, [CVE-2023-1855](https://nvd.nist.gov/vuln/detail/CVE-2023-1855){: external}, [CVE-2023-1989](https://nvd.nist.gov/vuln/detail/CVE-2023-1989){: external}, [CVE-2023-1998](https://nvd.nist.gov/vuln/detail/CVE-2023-1998){: external}, [CVE-2023-2269](https://nvd.nist.gov/vuln/detail/CVE-2023-2269){: external}, [CVE-2023-23455](https://nvd.nist.gov/vuln/detail/CVE-2023-23455){: external}, [CVE-2023-2513](https://nvd.nist.gov/vuln/detail/CVE-2023-2513){: external}, [CVE-2023-26545](https://nvd.nist.gov/vuln/detail/CVE-2023-26545){: external}, [CVE-2023-28328](https://nvd.nist.gov/vuln/detail/CVE-2023-28328){: external}, [CVE-2023-28772](https://nvd.nist.gov/vuln/detail/CVE-2023-28772){: external}, [CVE-2023-30456](https://nvd.nist.gov/vuln/detail/CVE-2023-30456){: external}, [CVE-2023-31084](https://nvd.nist.gov/vuln/detail/CVE-2023-31084){: external}, [CVE-2023-3141](https://nvd.nist.gov/vuln/detail/CVE-2023-3141){: external}, [CVE-2023-31436](https://nvd.nist.gov/vuln/detail/CVE-2023-31436){: external}, [CVE-2023-3161](https://nvd.nist.gov/vuln/detail/CVE-2023-3161){: external}, [CVE-2023-3212](https://nvd.nist.gov/vuln/detail/CVE-2023-3212){: external}, [CVE-2023-3268](https://nvd.nist.gov/vuln/detail/CVE-2023-3268){: external}, [CVE-2023-33203](https://nvd.nist.gov/vuln/detail/CVE-2023-33203){: external}, [CVE-2023-33951](https://nvd.nist.gov/vuln/detail/CVE-2023-33951){: external}, [CVE-2023-33952](https://nvd.nist.gov/vuln/detail/CVE-2023-33952){: external}, [CVE-2023-35823](https://nvd.nist.gov/vuln/detail/CVE-2023-35823){: external}, [CVE-2023-35824](https://nvd.nist.gov/vuln/detail/CVE-2023-35824){: external}, [CVE-2023-35825](https://nvd.nist.gov/vuln/detail/CVE-2023-35825){: external}, [CVE-2023-3609](https://nvd.nist.gov/vuln/detail/CVE-2023-3609){: external}, [CVE-2023-3611](https://nvd.nist.gov/vuln/detail/CVE-2023-3611){: external}, [CVE-2023-3772](https://nvd.nist.gov/vuln/detail/CVE-2023-3772){: external}, [CVE-2023-4128](https://nvd.nist.gov/vuln/detail/CVE-2023-4128){: external}, [CVE-2023-4132](https://nvd.nist.gov/vuln/detail/CVE-2023-4132){: external}, [CVE-2023-4155](https://nvd.nist.gov/vuln/detail/CVE-2023-4155){: external}, [CVE-2023-4206](https://nvd.nist.gov/vuln/detail/CVE-2023-4206){: external}, [CVE-2023-4207](https://nvd.nist.gov/vuln/detail/CVE-2023-4207){: external}, [CVE-2023-4208](https://nvd.nist.gov/vuln/detail/CVE-2023-4208){: external}, [CVE-2023-4732](https://nvd.nist.gov/vuln/detail/CVE-2023-4732){: external}, [CVE-2024-0443](https://nvd.nist.gov/vuln/detail/CVE-2024-0443){: external}, [RHSA-2023:7877](https://access.redhat.com/errata/RHSA-2023:7877){: external}, [CVE-2023-3446](https://nvd.nist.gov/vuln/detail/CVE-2023-3446){: external}, [CVE-2023-3817](https://nvd.nist.gov/vuln/detail/CVE-2023-3817){: external}, [CVE-2023-5678](https://nvd.nist.gov/vuln/detail/CVE-2023-5678){: external}, [RHSA-2023:7187](https://access.redhat.com/errata/RHSA-2023:7187){: external}, [CVE-2023-4016](https://nvd.nist.gov/vuln/detail/CVE-2023-4016){: external}, [RHSA-2023:7112](https://access.redhat.com/errata/RHSA-2023:7112){: external}, [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/CVE-2023-4641){: external}, [RHSA-2023:7166](https://access.redhat.com/errata/RHSA-2023:7166){: external}, [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/CVE-2023-22745){: external}, [RHSA-2023:7177](https://access.redhat.com/errata/RHSA-2023:7177){: external}, [CVE-2022-3094](https://nvd.nist.gov/vuln/detail/CVE-2022-3094){: external}, [RHSA-2023:7116](https://access.redhat.com/errata/RHSA-2023:7116){: external}, [CVE-2022-4904](https://nvd.nist.gov/vuln/detail/CVE-2022-4904){: external}, [RHSA-2023:7207](https://access.redhat.com/errata/RHSA-2023:7207){: external}, [CVE-2020-22217](https://nvd.nist.gov/vuln/detail/CVE-2020-22217){: external}, [CVE-2023-31130](https://nvd.nist.gov/vuln/detail/CVE-2023-31130){: external}, [RHSA-2023:6943](https://access.redhat.com/errata/RHSA-2023:6943){: external}, [CVE-2023-1786](https://nvd.nist.gov/vuln/detail/CVE-2023-1786){: external}, [RHSA-2023:6939](https://access.redhat.com/errata/RHSA-2023:6939){: external}, [CVE-2022-3064](https://nvd.nist.gov/vuln/detail/CVE-2022-3064){: external}, [CVE-2022-41723](https://nvd.nist.gov/vuln/detail/CVE-2022-41723){: external}, [CVE-2022-41724](https://nvd.nist.gov/vuln/detail/CVE-2022-41724){: external}, [CVE-2022-41725](https://nvd.nist.gov/vuln/detail/CVE-2022-41725){: external}, [CVE-2023-24534](https://nvd.nist.gov/vuln/detail/CVE-2023-24534){: external}, [CVE-2023-24536](https://nvd.nist.gov/vuln/detail/CVE-2023-24536){: external}, [CVE-2023-24537](https://nvd.nist.gov/vuln/detail/CVE-2023-24537){: external}, [CVE-2023-24538](https://nvd.nist.gov/vuln/detail/CVE-2023-24538){: external}, [CVE-2023-24539](https://nvd.nist.gov/vuln/detail/CVE-2023-24539){: external}, [CVE-2023-24540](https://nvd.nist.gov/vuln/detail/CVE-2023-24540){: external}, [CVE-2023-25173](https://nvd.nist.gov/vuln/detail/CVE-2023-25173){: external}, [CVE-2023-25809](https://nvd.nist.gov/vuln/detail/CVE-2023-25809){: external}, [CVE-2023-27561](https://nvd.nist.gov/vuln/detail/CVE-2023-27561){: external}, [CVE-2023-28642](https://nvd.nist.gov/vuln/detail/CVE-2023-28642){: external}, [CVE-2023-29400](https://nvd.nist.gov/vuln/detail/CVE-2023-29400){: external}, [CVE-2023-29406](https://nvd.nist.gov/vuln/detail/CVE-2023-29406){: external}, [CVE-2023-3978](https://nvd.nist.gov/vuln/detail/CVE-2023-3978){: external}, [RHSA-2024:0155](https://access.redhat.com/errata/RHSA-2024:0155){: external}, [CVE-2023-5981](https://nvd.nist.gov/vuln/detail/CVE-2023-5981){: external}, [RHSA-2024:0627](https://access.redhat.com/errata/RHSA-2024:0627){: external}, [CVE-2024-0553](https://nvd.nist.gov/vuln/detail/CVE-2024-0553){: external}, [RHSA-2023:6976](https://access.redhat.com/errata/RHSA-2023:6976){: external}, [CVE-2020-12762](https://nvd.nist.gov/vuln/detail/CVE-2020-12762){: external}, [RHSA-2024:0628](https://access.redhat.com/errata/RHSA-2024:0628){: external}, [CVE-2023-48795](https://nvd.nist.gov/vuln/detail/CVE-2023-48795){: external}, [RHSA-2024:0119](https://access.redhat.com/errata/RHSA-2024:0119){: external}, [CVE-2023-39615](https://nvd.nist.gov/vuln/detail/CVE-2023-39615){: external}, [RHSA-2023:7109](https://access.redhat.com/errata/RHSA-2023:7109){: external}, [CVE-2023-20569](https://nvd.nist.gov/vuln/detail/CVE-2023-20569){: external}, [RHSA-2024:0606](https://access.redhat.com/errata/RHSA-2024:0606){: external}, [CVE-2023-48795](https://nvd.nist.gov/vuln/detail/CVE-2023-48795){: external}, [CVE-2023-51385](https://nvd.nist.gov/vuln/detail/CVE-2023-51385){: external}, [RHSA-2023:7174](https://access.redhat.com/errata/RHSA-2023:7174){: external}, [CVE-2023-31486](https://nvd.nist.gov/vuln/detail/CVE-2023-31486){: external}, [RHSA-2023:6944](https://access.redhat.com/errata/RHSA-2023:6944){: external}, [CVE-2022-48468](https://nvd.nist.gov/vuln/detail/CVE-2022-48468){: external}, [RHSA-2023:7096](https://access.redhat.com/errata/RHSA-2023:7096){: external}, [CVE-2023-23931](https://nvd.nist.gov/vuln/detail/CVE-2023-23931){: external}, [RHSA-2023:7176](https://access.redhat.com/errata/RHSA-2023:7176){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [RHSA-2024:0116](https://access.redhat.com/errata/RHSA-2024:0116){: external}, [CVE-2023-43804](https://nvd.nist.gov/vuln/detail/CVE-2023-43804){: external}, [CVE-2023-45803](https://nvd.nist.gov/vuln/detail/CVE-2023-45803){: external}, [RHSA-2023:7151](https://access.redhat.com/errata/RHSA-2023:7151){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [RHSA-2024:0114](https://access.redhat.com/errata/RHSA-2024:0114){: external}, [CVE-2022-48560](https://nvd.nist.gov/vuln/detail/CVE-2022-48560){: external}, [CVE-2022-48564](https://nvd.nist.gov/vuln/detail/CVE-2022-48564){: external}, [RHSA-2024:0256](https://access.redhat.com/errata/RHSA-2024:0256){: external}, [CVE-2023-27043](https://nvd.nist.gov/vuln/detail/CVE-2023-27043){: external}, [RHSA-2023:7034](https://access.redhat.com/errata/RHSA-2023:7034){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [CVE-2023-32681](https://nvd.nist.gov/vuln/detail/CVE-2023-32681){: external}, [RHSA-2023:7058](https://access.redhat.com/errata/RHSA-2023:7058){: external}, [CVE-2022-41723](https://nvd.nist.gov/vuln/detail/CVE-2022-41723){: external}, [RHSA-2024:0647](https://access.redhat.com/errata/RHSA-2024:0647){: external}, [CVE-2021-35937](https://nvd.nist.gov/vuln/detail/CVE-2021-35937){: external}, [CVE-2021-35938](https://nvd.nist.gov/vuln/detail/CVE-2021-35938){: external}, [CVE-2021-35939](https://nvd.nist.gov/vuln/detail/CVE-2021-35939){: external}, [RHSA-2024:0253](https://access.redhat.com/errata/RHSA-2024:0253){: external}, [CVE-2023-7104](https://nvd.nist.gov/vuln/detail/CVE-2023-7104){: external}, [RHSA-2023:7057](https://access.redhat.com/errata/RHSA-2023:7057){: external}, [CVE-2023-33460](https://nvd.nist.gov/vuln/detail/CVE-2023-33460){: external}. |
{: caption="Changes since version 4.12.47_1577_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.46_1576_openshift, released 31 January 2024
{: #41246_1576_openshift_M}

The following table shows the changes that are in the master fix pack 4.12.46_1576_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.26.3 | v3.26.4 | See the [Calico release notes](https://docs.tigera.io/calico/3.26/release-notes/#v3.26.4){: external}. |
| Tigera Operator | v1.30.7 | v1.30.9 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.30.9){: external}. |
| Cluster health image | v1.4.5 | v1.4.6 | New version contains security fixes. |
| etcd | v3.5.10 | v3.5.11 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.11){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1487 | 1525 | New version contains security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.16-4 | v1.25.16-17 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | e544e35 | 7185ea1 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.5 | v2.8.6 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2767 | 2789 | New version contains updates and security fixes. |
| OpenVPN client | 2.6.7-r0-IKS-93 | 2.6.8-r0-IKS-108 | New version contains updates and security fixes. |
| OpenVPN server | 2.6.7-r0-IKS-92 | 2.6.8-r0-IKS-107 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.4.31 | v1.4.32 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.10 | v0.13.11 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.11){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.12.44 | 4.12.46 | See the {{site.data.keyword.openshiftlong_notm}} [release notes](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-46){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.12.0-20231102 | v4.12.0-20240104 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0%2B20240104){: external}. |
{: caption="Changes since version 4.12.44_1571_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.47_1577_openshift, released 29 January 2024
{: #41247_1577_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.47_1577_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.46 | 4.12.47 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-47){: external}. |
| Rhel8 Packages | 4.18.0-477.27.1.el8_8 | 4.18.0-477.27.1.el8_8 | N/A |
| HAProxy | e105dc | a13673 | Security fixes for [CVE-2023-7104](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-7104){: external}, [CVE-2023-27043](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-27043){: external}. |
{: caption="Changes since version 4.12.46_1575_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.46_1575_openshift, released 16 January 2024
{: #41246_1575_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.46_1575_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.12.45 | 4.12.46 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-46){: external}. |
| RHEL 8 Packages | N/A | N/A | N/A |
| Haproxy | 3060b0 | e105dc | [CVE-2023-39615](https://nvd.nist.gov/vuln/detail/CVE-2023-39615){: external}, [CVE-2023-5981](https://nvd.nist.gov/vuln/detail/CVE-2023-5981){: external}, [CVE-2022-48560](https://nvd.nist.gov/vuln/detail/CVE-2022-48560){: external}, [CVE-2022-48564](https://nvd.nist.gov/vuln/detail/CVE-2022-48564){: external}. |
{: caption="Changes since version 4.12.45_1574_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.45_1574_openshift, released 02 January 2024
{: #41245_1574_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.45_1574_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.12.45 | 4.12.45 | N/A |
| RHEL 8 Packages | 4.18.0-477.27.1.el8_8 | 4.18.0-477.27.1.el8_8 | N/A |
{: caption="Changes since version 4.12.45_1573_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.45_1573_openshift, released 18 December 2023
{: #41245_1573_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.45_1573_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.12.44 |4.12.45|For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-45){: external}. |
| RHEL 8 Packages | N/A |N/A|N/A |
{: caption="Changes since version 4.12.44_1572_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.44_1571_openshift, released 06 December 2023
{: #41244_1571_openshift_M}

The following table shows the changes that are in the master fix pack 4.12.44_1571_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.12 | v2.4.14 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.15-4 | v1.25.16-4 | New version contains updates and security fixes. |
| Load balancer and Load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2731 | 2767 | New version contains updates and security fixes. |
| OpenVPN client | 2.6.5-r0-IKS-77 | 2.6.7-r0-IKS-93 | New version contains updates and security fixes. |
| OpenVPN server | 2.6.5-r0-IKS-76 | 2.6.7-r0-IKS-92 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.4.30 | v1.4.31 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 438 | 439 | New version contains updates and security fixes. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.12.40 | 4.12.44 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-44){: external}. Resolves [CVE-2023-5408](https://nvd.nist.gov/vuln/detail/CVE-2023-5408){: external}. For more information, see the [IBM security bulletin](https://www.ibm.com/support/pages/node/7114006). |
{: caption="Changes since version 4.12.40_1568_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.44_1572_openshift, released 04 December 2023
{: #41244_1572_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.44_1572_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.42 | 4.12.44 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-44){: external}. |
| RHEL 8 Packages | N/A | N/A | N/A |
{: caption="Changes since version 4.12.42_1569_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.42_1569_openshift, released 29 November 2023
{: #41242_1569_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.42_1569_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.41 | 4.12.42 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-42){: external}. |
| CRI-O | 1.25.4 | 1.25.4 | Unqualified image registry aliases updated for `address-parsing-service`, `admin-site`, `apache-tika`, `auto-update-service`, `config-service`, `data-integration-service`, `dataprovider-manager-service`, `data-service`, `documents-service`, `gate-service`, `gateway-service`, `icij-db`, `identity-service`, `internet-access-service`, `mongo`, `notes-service`, `public-api-service`, `router`, and `search-service`.. However, using short names are not supported due to security risks, https://access.redhat.com/solutions/6178442. |
| RHEL 8 Packages |N/A|N/A|N/A|
{: caption="Changes since version 4.12.41_1567_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.40_1568_openshift, released 15 November 2023
{: #41240_1568_openshift_M}

The following table shows the changes that are in the master fix pack 4.12.40_1568_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.4.4 | v1.4.5 | New version contains updates and security fixes. |
| etcd | v3.5.9 | v3.5.10 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.10){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.14-8 | v1.25.15-4 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 435 | 438 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | f0d3265 | e544e35 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.4 | v2.8.5 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2681 | 2731 | New version contains updates and security fixes. |
| OpenVPN client | 2.6.5-r0-IKS-66 | 2.6.5-r0-IKS-77 | New version contains updates and security fixes. |
| OpenVPN server | 2.6.5-r0-IKS-57 | 2.6.5-r0-IKS-76 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.4.28 | v1.4.30 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.8 | v0.13.10 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.10){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.12.37 | 4.12.40 | Resolves [CVE-2023-39325](https://nvd.nist.gov/vuln/detail/CVE-2023-39325){: external} and [CVE-2023-44487](https://nvd.nist.gov/vuln/detail/CVE-2023-44487). For more information, see the [IBM security bulletin](https://www.ibm.com/support/pages/node/7080059){: external}. See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-40){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.12.0-20231010 | v4.12.0-20231102 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0%2B20231010){: external}. |
{: caption="Changes since version 4.12.37_1565_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.41_1567_openshift, released 08 November 2023
{: #41241_1567_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.41_1567_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}| 4.12.39 | 4.12.41 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-41){: external}. |
{: caption="Changes since version 4.12.39_1566_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.37_1565_openshift, released 25 October 2023
{: #41237_1565_openshift_M}

The following table shows the changes that are in the master fix pack 4.12.37_1565_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.26.1 | v3.26.3 | See the [Calico release notes](https://docs.tigera.io/calico/latest/release-notes/#v3.26.3){: external}. |
| Tigera Operator | v1.30.5 | v1.30.7 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.30.7){: external}. |
| Cluster health image | v1.4.2 | v1.4.4 | New version contains updates and security fixes. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1390 | 1487 | New version contains security fixes. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.10 | v2.4.12 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.14-1 | v1.25.14-8 | New version contains updates and security fixes. The logic for the `service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-idle-connection-timeout` annotation has changed. The default idle timeout is dependent on your account settings. Usually, this value is `50`. However, some allowlisted accounts have larger timeout settings. If you don't set the annotation, your load balancers use the timeout setting in your account. You can explicitly specify the timeout by setting this annotation. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 4e2f346 | f0d3265 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.2 | v2.8.4 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.4.27 | v1.4.28 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.6 | v0.13.8 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.8){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.12.26 | 4.12.37 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-37){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.12.0-20230811 | v4.12.0-20231010 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0%2B20231010){: external}. |
{: caption="Changes since version 4.12.26_1562_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.39_1566_openshift, released 23 October 2023
{: #41239_1566_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.39_1566_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.36 | 4.12.39 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-39){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node package update for [CVE-2023-44487](https://nvd.nist.gov/vuln/detail/CVE-2023-44487){: external}. |
{: caption="Changes since version 4.12.36_1564_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.36_1564_openshift, released 9 October 2023
{: #41236_1564_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.36_1564_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. |4.12.34|4.12.36| For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-36){: external}. |
| RHEL 8 Packages | N/A | N/A | Worker node package updates for [CVE-2023-3341](https://nvd.nist.gov/vuln/detail/CVE-2023-3341){: external}, [CVE-2023-4527](https://nvd.nist.gov/vuln/detail/CVE-2023-4527){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [CVE-2023-4806](https://nvd.nist.gov/vuln/detail/CVE-2023-4806){: external}, [CVE-2023-4813](https://nvd.nist.gov/vuln/detail/CVE-2023-4813){: external}, [CVE-2023-4911](https://nvd.nist.gov/vuln/detail/CVE-2023-4911){: external}. |
{: caption="Changes since version 4.12.34_1563_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.34_1563_openshift, released 27 September 2023
{: #41234_1563_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.34_1563_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.34 | 4.12.34 | No Change |
| RHEL 8 Packages | 4.18.0-477.21.1.el8_8 | 4.18.0-477.27.1.el8_8 | Worker node kernel & package updates for [CVE-2023-2002](https://nvd.nist.gov/vuln/detail/CVE-2023-2002){: external}, [CVE-2023-3090](https://nvd.nist.gov/vuln/detail/CVE-2023-3090){: external}, [CVE-2023-3390](https://nvd.nist.gov/vuln/detail/CVE-2023-3390){: external}, [CVE-2023-3776](https://nvd.nist.gov/vuln/detail/CVE-2023-3776){: external}, [CVE-2023-4004](https://nvd.nist.gov/vuln/detail/CVE-2023-4004){: external}, [CVE-2023-20593](https://nvd.nist.gov/vuln/detail/CVE-2023-20593){: external}, [CVE-2023-29491](https://nvd.nist.gov/vuln/detail/CVE-2023-29491){: external}, [CVE-2023-30630](https://nvd.nist.gov/vuln/detail/CVE-2023-30630){: external}, [CVE-2023-35001](https://nvd.nist.gov/vuln/detail/CVE-2023-35001){: external}, [CVE-2023-35788](https://nvd.nist.gov/vuln/detail/CVE-2023-35788){: external}. |
{: caption="Changes since version 4.12.34_1557_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.26_1562_openshift, released 20 September 2023
{: #41226_1562_openshift_M}

The following table shows the changes that are in the master fix pack 4.12.26_1562_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.25.1 | v3.26.1 | See the [Calico release notes](https://docs.tigera.io/calico/latest/release-notes/#v3.26.1){: external}. |
| Tigera Operator | v1.29.4 | v1.30.5 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.30.5){: external}. |
| Cluster health image | v1.3.24 | v1.4.2 | Updated `Go` to version `1.20.8` and updated dependencies. Updated to new base image. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.5 | v2.4.10 | Updated `Go dependencies`. Updated to newer UBI base image. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.14-4 | v1.25.14-1 | Updated to support the `Kubernetes 1.25.14` release. Updated `Go` to version `1.20.8` and updated `Go dependencies`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 434 | 435 | Updated `Go` to version `1.20.6` and updated dependencies. Updated to newer UBI base image. |
| Key Management Service provider | v2.7.3 | v2.8.2 | Updated `Go dependencies`. Changed to new base image. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2631 | 2681 | Updated `Go` to version `1.19.12` and updated `Go dependencies`. |
{: caption="Changes since version 4.12.26_1555_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.32_1557_openshift, released 12 September 2023
{: #41232_1557_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.32_1557_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.30 | 4.12.32 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-32){: external}. |
| RHEL 8 Packages | N/A | N/A | Package updates for [CVE-2022-40982](https://nvd.nist.gov/vuln/detail/CVE-2022-40982){: external}, [CVE-2022-41804](https://nvd.nist.gov/vuln/detail/CVE-2022-41804){: external}, [CVE-2023-23908](https://nvd.nist.gov/vuln/detail/CVE-2023-23908){: external}. |
{: caption="Changes since version 4.12.30_1556_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.26_1555_openshift, released 30 August 2023
{: #41226_1555_openshift_M}

The following table shows the changes that are in the master fix pack 4.12.26_1555_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.23 | v1.3.24 | Updated `Go` to version `1.19.12` and updated dependencies. Updated base image version to 378. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.12-1 | v1.25.12-4 | Updated `Go` dependencies to resolve a CVE. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 433 | 434 | Updated `Go` to version `1.20.6` and updated dependencies. Updated to newer UBI base image. |
| Key Management Service provider | v2.7.2 | v2.7.3 | Updated `Go` dependencies. |
| OpenVPN client | 2.6.5-r0-IKS-41-amd64 | 2.6.5-r0-IKS-66-amd64 | Updated `openvpn` components to fix CVEs. |
| OpenVPN server | 2.6.5-r0-IKS-40-amd64 | 2.6.5-r0-IKS-57-amd64 | Updated `openvpn` components to fix CVEs. |
| OpenVPN Operator image | v1.4.26 | v1.4.27 | Updated `ansible-operator` version to `1.30.0` |
| Portieris admission controller | v0.13.5 | v0.13.6 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.6){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.12.24 | 4.12.26 | See the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-26){: external} for more information. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.12.0-20230710 | v4.12.0-20230811 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0%2B20230811){: external}. |
{: caption="Changes since version 4.12.24_1552_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.30_1556_openshift, released 28th August 2023
{: #41230_1556_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.30_1556_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.28 | 4.12.30 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-30){: external}. |
{: caption="Changes since version 4.12.28_1554_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.28_1554_openshift, released 15th August 2023
{: #41228_1554_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.28_1554_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.26 | 4.12.28 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-28){: external}. |
| RHEL 7 Packages| 3.10.0-1160.92.1.el7 | 3.10.0-1160.95.1.el7 | Worker node kernel & package updates for [CVE-2023-38408](https://nvd.nist.gov/vuln/detail/CVE-2023-38408){: external}, [CVE-2022-3564](https://nvd.nist.gov/vuln/detail/CVE-2022-3564){: external}. |
| RHEL 8 Packages| 4.18.0-477.15.1.el8_8 | 4.18.0-477.21.1.el8_8 | Worker node kernel & package updates for [CVE-2022-42896](https://nvd.nist.gov/vuln/detail/CVE-2022-42896){: external}, [CVE-2023-1281](https://nvd.nist.gov/vuln/detail/CVE-2023-1281){: external}, [CVE-2023-1829](https://nvd.nist.gov/vuln/detail/CVE-2023-1829){: external}, [CVE-2023-2124](https://nvd.nist.gov/vuln/detail/CVE-2023-2124){: external}, [CVE-2023-2194](https://nvd.nist.gov/vuln/detail/CVE-2023-2194){: external}, [CVE-2023-2235](https://nvd.nist.gov/vuln/detail/CVE-2023-2235){: external}, [CVE-2023-2602](https://nvd.nist.gov/vuln/detail/CVE-2023-2602){: external}, [CVE-2023-2603](https://nvd.nist.gov/vuln/detail/CVE-2023-2603){: external}, [CVE-2023-27536](https://nvd.nist.gov/vuln/detail/CVE-2023-27536){: external}, [CVE-2023-28321](https://nvd.nist.gov/vuln/detail/CVE-2023-28321){: external}, [CVE-2023-28484](https://nvd.nist.gov/vuln/detail/CVE-2023-28484){: external}, [CVE-2023-29469](https://nvd.nist.gov/vuln/detail/CVE-2023-29469){: external}, [CVE-2023-32681](https://nvd.nist.gov/vuln/detail/CVE-2023-32681){: external}, [CVE-2023-34969](https://nvd.nist.gov/vuln/detail/CVE-2023-34969){: external}, [CVE-2023-38408](https://nvd.nist.gov/vuln/detail/CVE-2023-38408){: external}. |
{: caption="Changes since version 4.12.26_1553_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.26_1553_openshift, released 1 August 2023
{: #41226_1553_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.26_1553_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.24 | 4.12.26 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-26){: external}. |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-3564](https://nvd.nist.gov/vuln/detail/CVE-2022-3564){: external}, [CVE-2023-2828](https://nvd.nist.gov/vuln/detail/CVE-2023-2828){: external}, [CVE-2023-32233](https://nvd.nist.gov/vuln/detail/CVE-2023-32233){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node package update for [CVE-2023-2828](https://nvd.nist.gov/vuln/detail/CVE-2023-2828){: external}. |
{: caption="Changes since version 4.12.24_1551_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.24_1552_openshift, released 28 July 2023
{: #41224_1552_openshift_M}

The following table shows the changes that are in the master fix pack 4.12.24_1552_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.21 | v1.3.23 | Updated `Go` to version `1.19.11` and updated `Go` dependencies. Updated UBI base image. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.11-1 | v1.25.12-1 | Updated to support the Kubernetes `1.25.12` release. Updated `Go` dependencies and to `Go` version `1.20.6`. |
| Key Management Service provider | v2.6.7 | v2.7.2 | Updated `Go` to version `1.19.11` and updated `Go` dependencies. Updated UBI base image. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2584 | 2631 | Updated `Go` to version `1.19.10` and updated `Go` dependencies. Updated Alpine base image. |
| OpenVPN client | 2.6.4-r0-IKS-34-amd64 | 2.6.5-r0-IKS-41-amd64 | Updated `OpenVPN` to version `2.6.5`. |
| OpenVPN Operator image | v1.4.25 | v1.4.26 | Updated based image to resolve [CVE-2023-24329](https://nvd.nist.gov/vuln/detail/CVE-2023-24329){: external}, [CVE-2020-24736](https://nvd.nist.gov/vuln/detail/CVE-2020-24736){: external}, [CVE-2023-26604](https://nvd.nist.gov/vuln/detail/CVE-2023-26604){: external}, [CVE-2023-1667](https://nvd.nist.gov/vuln/detail/CVE-2023-1667){: external}, and [CVE-2023-2283](https://nvd.nist.gov/vuln/detail/CVE-2023-2283){: external}. |
| OpenVPN server | 2.6.4-r0-IKS-33-amd64 | 2.6.5-r0-IKS-40-amd64 | Updated `OpenVPN` to version `2.6.5`. |
| {{site.data.keyword.openshiftshort}}. | 4.12.20 | 4.12.24 | Resolves [CVE-2023-1260](https://nvd.nist.gov/vuln/detail/CVE-2023-1260){: external}. For more information, see the [IBM security bulletin](https://www.ibm.com/support/pages/node/7052832){: external}. See the [{{site.data.keyword.openshiftshort}} release notes.](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator and Metrics Server | v4.12.0-20230417 | v4.12.0-20230710 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20230710){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.12.0+20230417 | 4.12.0+20230710 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20230710){: external}. |
{: caption="Changes since version 4.12.20_1549_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.24_1551_openshift, released 17th July 2023
{: #41224_1551_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.24_1551_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.12.22 |4.12.24|[See change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-24){: external}. |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages |N/A|N/A|N/A|
{: caption="Changes since version 4.12.22_1550_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.22_1550_openshift, released 03 July 2023
{: #41222_1550_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.22_1550_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.21 | 4.12.22 | see [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-22){: external}. |
{: caption="Changes since version 4.12.21_1547_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.20_1549_openshift, released 27 June 2023
{: #41220_1549_openshift_M}

The following table shows the changes that are in the master fix pack 4.12.20_1549_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Tigera Operator | v1.29.3 | v1.29.4 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.29.4){: external}. |
| Cluster health image | v1.3.20 | v1.3.21 | Updated `Go` dependencies and to `Go` version `1.19.10`. |
| etcd | v3.5.8 | v3.5.9 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.9){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.9-7 | v1.25.11-1 | Updated to support the `Kubernetes 1.25.11` release. Updated `Go` dependencies and to `Go` version `1.19.10`. Updated `calicoctl` and `vpcctl`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 431 | 433 | Updated `Go` to version `1.20.4`. Updated UBI base image. |
| Key Management Service provider | v2.6.6 | v2.6.7 | Updated `Go` dependencies and to `Go` version `1.19.10`. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2486 | 2584 | Updated `Go` dependencies and to `Go` version `1.19.9`. Updated base image. |
| {{site.data.keyword.openshiftshort}} | 4.12.16 | 4.12.20 | https://docs.openshift.com/container-platform/ |
| OpenVPN client | 2.5.8-r0-IKS-674-amd64 | 2.6.4-r0-IKS-34-amd64 | Upgrade `openvpn` to version `2.6.4-r0`. |
| OpenVPN server | 2.5.8-r0-IKS-673-amd64 | 2.6.4-r0-IKS-33-amd64 | Upgrade `openvpn` to version `2.6.4-r0`. |
| OpenVPN Operator image | v1.4.23 | v1.4.25 | Updated OpenVPN configuration to provide shutdown grace period before terminating connections. |
{: caption="Changes since version 4.12.16_1545_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.21_1547_openshift, released 19 June 2023
{: #41221_1547_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.21_1547_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. |4.12.19|4.12.21|For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-21){: external}. |
| RHEL 8 Packages | N/A | N/A | Worker node package updates for [CVE-2023-32067](https://nvd.nist.gov/vuln/detail/CVE-2023-32067){: external},[CVE-2023-24329](https://nvd.nist.gov/vuln/detail/CVE-2023-24329){: external}. |
{: caption="Changes since version 4.12.19_1546_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.19_1546_openshift, released 5 June 2023
{: #41219_1546_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.19_1546_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.16 | 4.12.19 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-19){: external}. |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-477.10.1.el8_8 | 4.18.0-477.13.1.el8_8 | Worker node kernel & package updates for [CVE-2023-22490](https://nvd.nist.gov/vuln/detail/CVE-2023-22490){: external}, [CVE-2023-23946](https://nvd.nist.gov/vuln/detail/CVE-2023-23946){: external}, [CVE-2023-25652](https://nvd.nist.gov/vuln/detail/CVE-2023-25652){: external}, [CVE-2023-25815](https://nvd.nist.gov/vuln/detail/CVE-2023-25815){: external}, [CVE-2023-29007](https://nvd.nist.gov/vuln/detail/CVE-2023-29007){: external}, [CVE-2023-32233](https://nvd.nist.gov/vuln/detail/CVE-2023-32233){: external}. |
{: caption="Changes since version 4.12.16_1544_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.16_1545_openshift, released 25 May 2023
{: #41216_1545_openshift_M}

The following table shows the changes that are in the master fix pack 4.12.16_1545_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.19 | v1.3.20 | Updated `Go` to version `1.19.9` and updated dependencies. Updated the base image. Resolved add-on health bugs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.9-2 | v1.25.9-7 | Updated support of the Kubernetes 1.25.9 release. Updated Go dependencies. Key rotation. |
| Key Management Service provider | v2.6.5 | v2.6.6 | Updated `Go` to version `1.19.9` and updated dependencies. |
| OpenVPN client | 2.6.4-r0-IKS-27 | 2.5.8-r0-IKS-674 | Reverted to previous version. |
| OpenVPN server | 2.6.4-r0-IKS-26 | 2.5.8-r0-IKS-673 | Reverted to previous version. |
| Portieris admission controller | v0.13.4 | v0.13.5 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.5){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.12.13 | 4.12.16 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-16){: external}. |
{: caption="Changes since version 4.12.13_1541_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.16_1544_openshift, released 23 May 2023
{: #41216_1544_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.16_1544_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.15 | 4.12.16 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-16){: external}. |
| RHEL 8 Packages | 4.18.0-425.19.2.el8_7 | 4.18.0-477.10.1.el8_8 | Worker node kernel & package updates for [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-26341](https://nvd.nist.gov/vuln/detail/CVE-2021-26341){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2021-33655](https://nvd.nist.gov/vuln/detail/CVE-2021-33655){: external}, [CVE-2021-33656](https://nvd.nist.gov/vuln/detail/CVE-2021-33656){: external}, [CVE-2022-1462](https://nvd.nist.gov/vuln/detail/CVE-2022-1462){: external}, [CVE-2022-1679](https://nvd.nist.gov/vuln/detail/CVE-2022-1679){: external}, [CVE-2022-1705](https://nvd.nist.gov/vuln/detail/CVE-2022-1705){: external}, [CVE-2022-1789](https://nvd.nist.gov/vuln/detail/CVE-2022-1789){: external}, [CVE-2022-1962](https://nvd.nist.gov/vuln/detail/CVE-2022-1962){: external}, [CVE-2022-20141](https://nvd.nist.gov/vuln/detail/CVE-2022-20141){: external}, [CVE-2022-2196](https://nvd.nist.gov/vuln/detail/CVE-2022-2196){: external}, [CVE-2022-24765](https://nvd.nist.gov/vuln/detail/CVE-2022-24765){: external}, [CVE-2022-25265](https://nvd.nist.gov/vuln/detail/CVE-2022-25265){: external}, [CVE-2022-2663](https://nvd.nist.gov/vuln/detail/CVE-2022-2663){: external}, [CVE-2022-27664](https://nvd.nist.gov/vuln/detail/CVE-2022-27664){: external}, [CVE-2022-2795](https://nvd.nist.gov/vuln/detail/CVE-2022-2795){: external}, [CVE-2022-28131](https://nvd.nist.gov/vuln/detail/CVE-2022-28131){: external}, [CVE-2022-29187](https://nvd.nist.gov/vuln/detail/CVE-2022-29187){: external}, [CVE-2022-2928](https://nvd.nist.gov/vuln/detail/CVE-2022-2928){: external}, [CVE-2022-2929](https://nvd.nist.gov/vuln/detail/CVE-2022-2929){: external}, [CVE-2022-3028](https://nvd.nist.gov/vuln/detail/CVE-2022-3028){: external}, [CVE-2022-30594](https://nvd.nist.gov/vuln/detail/CVE-2022-30594){: external}, [CVE-2022-30629](https://nvd.nist.gov/vuln/detail/CVE-2022-30629){: external}, [CVE-2022-30630](https://nvd.nist.gov/vuln/detail/CVE-2022-30630){: external}, [CVE-2022-30631](https://nvd.nist.gov/vuln/detail/CVE-2022-30631){: external}, [CVE-2022-30632](https://nvd.nist.gov/vuln/detail/CVE-2022-30632){: external}, [CVE-2022-30633](https://nvd.nist.gov/vuln/detail/CVE-2022-30633){: external}, [CVE-2022-30635](https://nvd.nist.gov/vuln/detail/CVE-2022-30635){: external}, [CVE-2022-32148](https://nvd.nist.gov/vuln/detail/CVE-2022-32148){: external}, [CVE-2022-32189](https://nvd.nist.gov/vuln/detail/CVE-2022-32189){: external}, [CVE-2022-3239](https://nvd.nist.gov/vuln/detail/CVE-2022-3239){: external}, [CVE-2022-3522](https://nvd.nist.gov/vuln/detail/CVE-2022-3522){: external}, [CVE-2022-3524](https://nvd.nist.gov/vuln/detail/CVE-2022-3524){: external}, [CVE-2022-35252](https://nvd.nist.gov/vuln/detail/CVE-2022-35252){: external}, [CVE-2022-3564](https://nvd.nist.gov/vuln/detail/CVE-2022-3564){: external}, [CVE-2022-3566](https://nvd.nist.gov/vuln/detail/CVE-2022-3566){: external}, [CVE-2022-3567](https://nvd.nist.gov/vuln/detail/CVE-2022-3567){: external}, [CVE-2022-3619](https://nvd.nist.gov/vuln/detail/CVE-2022-3619){: external}, [CVE-2022-36227](https://nvd.nist.gov/vuln/detail/CVE-2022-36227){: external}, [CVE-2022-3623](https://nvd.nist.gov/vuln/detail/CVE-2022-3623){: external}, [CVE-2022-3625](https://nvd.nist.gov/vuln/detail/CVE-2022-3625){: external}, [CVE-2022-3628](https://nvd.nist.gov/vuln/detail/CVE-2022-3628){: external}, [CVE-2022-3707](https://nvd.nist.gov/vuln/detail/CVE-2022-3707){: external}, [CVE-2022-39188](https://nvd.nist.gov/vuln/detail/CVE-2022-39188){: external}, [CVE-2022-39189](https://nvd.nist.gov/vuln/detail/CVE-2022-39189){: external}, [CVE-2022-39253](https://nvd.nist.gov/vuln/detail/CVE-2022-39253){: external}, [CVE-2022-39260](https://nvd.nist.gov/vuln/detail/CVE-2022-39260){: external}, [CVE-2022-41218](https://nvd.nist.gov/vuln/detail/CVE-2022-41218){: external}, [CVE-2022-4129](https://nvd.nist.gov/vuln/detail/CVE-2022-4129){: external}, [CVE-2022-41674](https://nvd.nist.gov/vuln/detail/CVE-2022-41674){: external}, [CVE-2022-41717](https://nvd.nist.gov/vuln/detail/CVE-2022-41717){: external}, [CVE-2022-41973](https://nvd.nist.gov/vuln/detail/CVE-2022-41973){: external}, [CVE-2022-4269](https://nvd.nist.gov/vuln/detail/CVE-2022-4269){: external}, [CVE-2022-42703](https://nvd.nist.gov/vuln/detail/CVE-2022-42703){: external}, [CVE-2022-42720](https://nvd.nist.gov/vuln/detail/CVE-2022-42720){: external}, [CVE-2022-42721](https://nvd.nist.gov/vuln/detail/CVE-2022-42721){: external}, [CVE-2022-42722](https://nvd.nist.gov/vuln/detail/CVE-2022-42722){: external}, [CVE-2022-43552](https://nvd.nist.gov/vuln/detail/CVE-2022-43552){: external}, [CVE-2022-43750](https://nvd.nist.gov/vuln/detail/CVE-2022-43750){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}, [CVE-2022-47929](https://nvd.nist.gov/vuln/detail/CVE-2022-47929){: external}, [CVE-2023-0394](https://nvd.nist.gov/vuln/detail/CVE-2023-0394){: external}, [CVE-2023-0461](https://nvd.nist.gov/vuln/detail/CVE-2023-0461){: external}, [CVE-2023-0778](https://nvd.nist.gov/vuln/detail/CVE-2023-0778){: external}, [CVE-2023-1195](https://nvd.nist.gov/vuln/detail/CVE-2023-1195){: external}, [CVE-2023-1582](https://nvd.nist.gov/vuln/detail/CVE-2023-1582){: external}, [CVE-2023-23454](https://nvd.nist.gov/vuln/detail/CVE-2023-23454){: external}, [CVE-2023-27535](https://nvd.nist.gov/vuln/detail/CVE-2023-27535){: external}. |
| Haproxy | N/A |N/A|N/A|
{: caption="Changes since version 4.12.15_1542_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.13_1541_openshift, released 2 May 2023
{: #41213_1541_openshift}

The following table shows the changes that are in the master fix pack 4.12.13_1540_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| etcd | v3.5.7 | v3.5.8 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.8){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.9-1 | v1.25.9-2 | Update `Go` dependencies |
| {{site.data.keyword.openshiftshort}}. | 4.12.11 | 4.12.13 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-13){: external}. |
{: caption="Changes since version 4.12.11_1538_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.11_1539_openshift, released 27 April 2023
{: #41211_1539_openshift}

The following table shows the changes that are in the master fix pack 4.12.11_1538_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.25.0 | v3.25.1 | See the [Calico release notes](https://docs.tigera.io/calico/latest/release-notes/#v3.25.1){: external}. |
| Tigera Operator | v1.29.0 | v1.29.3 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.29.3){: external}. |
| Cluster health image | v1.3.17 | v1.3.19 | Updated `Go` to version `1.19.8` and updated dependencies. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1366-amd64 | 1390-amd64 | Eliminate IP syscall. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.0 | v2.4.5 | Updated universal base image (UBI) to resolve CVEs. Updated `Go` to version `1.19.8` and updated dependencies. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.8-1 | v1.25.9-1 | Updated to support the Kubernetes `1.25.9` release. Updated `Go` dependencies and to `Go` version `1.19.8`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 429 | 431 | Updated `Go` to version `1.19.8` and updated dependencies. Update UBI base image. |
| Key Management Service provider | v2.6.4 | v2.6.5 | Updated `Go` to version `1.19.7` and updated dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2420 | 2486 | Updated `Go` to version `1.19.7` and updated dependencies. |
| {{site.data.keyword.openshiftshort}}. | 4.12.7 | 4.12.11 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-11){: external}. |
| {{site.data.keyword.openshiftshort}} configuration | N/A | N/A | Set proper topology spread constraints for the default {{site.data.keyword.openshiftshort}} image registry configuration used by classic clusters. |
| OpenVPN Operator image | v1.4.22 | v1.4.23 | Updated base image to resolve CVEs: [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}, [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2023-0361](https://nvd.nist.gov/vuln/detail/CVE-2023-0361){: external}. |
| Portieris admission controller | v0.13.3 | v0.13.4 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.4){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator and Metrics Server | 4.12.0-20230314 | 4.12.0-20230417 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20230417){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.12.0+20230314 | 4.12.0+20230417 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20230417){: external}. |
{: caption="Changes since version 4.12.7_1534_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.15_1542_openshift, released 24 April 2023
{: #41215_1542_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.15_1542_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.12.13 | 4.12.15 | See [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-15){: external}. |
| Haproxy |N/A|N/A|N/A|
{: caption="Changes since version 4.12.13_1539_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.13_1539_openshift, released 24 April 2023
{: #41213_1539_openshift}

The following table shows the changes that are in the worker node fix pack 4.12.13_1539_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.12.10 | 4.12.13 | See [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-13){: external}. |
| Haproxy |N/A|N/A|N/A|
{: caption="Changes since version 4.12.10_1536_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.10_1536_openshift, released 11 April 2023
{: #41210_1536_openshift}

The following table shows the changes that are in the worker node fix pack 4.12.10_1536_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages | 4.18.0-425.13.1 | 4.18.0-425.19.2 | Worker node kernel & package updates for [CVE-2022-4269](https://nvd.nist.gov/vuln/detail/CVE-2022-4269){: external}, [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4378](https://nvd.nist.gov/vuln/detail/CVE-2022-4378){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}, [CVE-2023-0266](https://nvd.nist.gov/vuln/detail/CVE-2023-0266){: external}, [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2023-0361](https://nvd.nist.gov/vuln/detail/CVE-2023-0361){: external}, [CVE-2023-0386](https://nvd.nist.gov/vuln/detail/CVE-2023-0386){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.12.8 | 4.12.10 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-10){: external}. |
| Haproxy | 8398d1 | 8895ad | [CVE-2023-0361](https://nvd.nist.gov/vuln/detail/CVE-2023-0361){: external}. |
{: caption="Changes since version 4.12.8_1535_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.7_1534_openshift, released 28 March 2023
{: #4127_1534_openshift}

The following table shows the changes that are in the master fix pack 4.12.7_1534_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.16 | v1.3.17 | Updated `Go` to version `1.19.7` and updated dependencies. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1308-amd64 | 1366-amd64 | Updated to resolve [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.7 | v2.4.0 | Removed ExpandInUsePersistentVolumes feature gate. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.6-10 | v1.25.8-1 | Updated to support the `Kubernetes 1.25.8` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 427 | 429 | Updated universal base image (UBI) to resolve CVEs. Updated `Go` to version `1.19.6` and updated dependencies. |
| Key Management Service provider | v2.6.3 | v2.6.4 | Updated `Go` to version `1.19.7` and updated dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2383 | 2420 | Updated the image to resolve CVEs. |
| OpenVPN Operator image | v1.5.3 | v1.4.22 | Updated `ansible-operator` to `v1.28.0` to fix CVEs. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.12.3 | 4.12.7 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-7){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.12.0-20230220 | v4.12.0-20230314 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20230314){: external}. |
{: caption="Changes since version 4.12.3_1530_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.8_1535_openshift, released 27 March 2023
{: #4128_1535_openshift}

The following table shows the changes that are in the worker node fix pack 4.12.8_1535_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.12.6 | 4.12.8 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-8){: external}. |
| Haproxy | af5031 | 8398d1 | [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}. |
{: caption="Changes since version 4.12.6_1531_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.6_1531_openshift, released 13 March 2023
{: #4126_1531_openshift}

The following table shows the changes that are in the worker node fix pack 4.12.6_1531_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages |N/A|N/A| Worker node package updates for [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.12.4 | 4.12.6 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-6){: external}. |
{: caption="Changes since version 4.12.4_1528_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.3_1530_openshift, released 2 March 2023
{: #4123_1530_openshift}

The following table shows the changes that are in the master fix pack 4.12.3_1530_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.15 | v1.3.16 | Updated `Go` dependencies and to `Go` version `1.19.6`. Updated universal base image (UBI) to resolve CVEs. |
| etcd | v3.5.6 | v3.5.7 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.7){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1305-amd64 | 1308-amd64 | Updated universal base image (UBI) to resolve [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.6-8 | v1.25.6-10 | Updated `Go` dependencies. Updated `k8s.io/utils` digest to `a5ecb01`. |
| OpenVPN client | 2.5.6-r1-IKS-648 | 2.5.8-r0-IKS-674-amd64 | Remediate [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}. |
| OpenVPN server | 2.5.6-r1-IKS-647 | 2.5.8-r0-IKS-673-amd64 | Remediate [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}. |
| OpenVPN Operator image | v1.4.20 | v1.5.2 | Resolve issue with openvpn container restarts |
| {{site.data.keyword.openshiftshort}}. | 4.12.2 | 4.12.3 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-3){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.12.0-20230124 | v4.12.0-20230220 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0%2B20230220){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.12.0-20230124 | v4.12.0-20230220 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0%2B20230220){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.12.0+20230124 | 4.12.0+20230220 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20230220){: external}. |
{: caption="Changes since version 4.12.2_1527_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.4_1528_openshift, released 27 February 2023
{: #4124_1528_openshift}

The following table shows the changes that are in the worker node fix pack 4.12.4_1528_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages | 4.18.0-425.10.1 | 4.18.0-425.13.1 | Worker node & kernel package updates for [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2022-2873](https://nvd.nist.gov/vuln/detail/CVE-2022-2873){: external}, [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/CVE-2022-40897){: external}, [CVE-2022-41222](https://nvd.nist.gov/vuln/detail/CVE-2022-41222){: external}, [CVE-2022-43945](https://nvd.nist.gov/vuln/detail/CVE-2022-43945){: external}, [CVE-2022-4415](https://nvd.nist.gov/vuln/detail/CVE-2022-4415){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}, [CVE-2022-48303](https://nvd.nist.gov/vuln/detail/CVE-2022-48303){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.12.2 | 4.12.4 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-4){: external}. |
| HAProxy | d38f89 | af5031 | [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/CVE-2022-40897){: external}, [CVE-2022-4415](https://nvd.nist.gov/vuln/detail/CVE-2022-4415){: external}, [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}. |
{: caption="Changes since version 4.12.2_1526_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.2_1527_openshift and worker node fix pack 4.12.2_1526_openshift, released 23 February 2023
{: #4122_1527_openshift_4.12.2_1526_openshift}

The following table shows the changes that are in the master fix pack 4.12.2_1627_openshift and worker node fix pack 4.12.2_1526_openshift.  Master patch updates are applied automatically. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.23.5 | v3.25.0 | See the [Calico release notes](https://docs.tigera.io/archive){: external}. Calico configuration now sets a [BGP password](https://docs.tigera.io/calico/latest/reference/resources/bgppeer#bgppassword){: external}. In addition, the `default` `FelixConfiguration` resource is updated to set `natPortRange` to `32768:65535` if not already set. For more information, see [Why am I seeing SNAT port issues and egress connection failures?](/docs/openshift?topic=openshift-ts-network-snat-125). |
| Tigera Operator | v1.27.17 | v1.29.0 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.29.0){: external}. |
| Gateway-enabled cluster controller | 1902 | 1987 | Image updated to resolve [CVE-2022-41721](https://nvd.nist.gov/vuln/detail/CVE-2022-41721){: external}, [CVE-2022-41717](https://nvd.nist.gov/vuln/detail/CVE-2022-41717){: external}, [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}, and [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}.  |
| {{site.data.keyword.IBM_notm}} Calico extension | 1280-amd64 | 1305-amd64 | Updated `Go` version to `1.19.5`. |
| {{site.data.keyword.IBM_notm}} Cloud Block Storage driver and plug-in | v2.3.6 | v2.3.7 | Updated `Go` version to `1.18.9`.  Updated universal base image (`UBI`) to version `8.7-1031.1675784874`. |
| {{site.data.keyword.IBM_notm}} Cloud Controller Manager | v1.24.10-2 | v1.25.6-8 | Updated to support the Kubernetes `1.25.6` release. Updated `Go` dependencies and to `Go` version `1.19.5`. |
| {{site.data.keyword.IBM_notm}} Cloud File Storage plug-in and monitor | 425 | 427 | Image updated to resolve [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}. |
| Key Management Service provider | v2.5.13 | v2.6.3 | Key Management Service (KMS) pod termination is delayed until the Kubernetes API server terminates. Updated `Go` dependencies and to `Go` version `1.19.6`. |
| Load balancer and load balancer monitor for {{site.data.keyword.IBM_notm}} Cloud Provider | 2325 | 2383 | Updated `Go` dependencies and to `Go` version `1.19.5`. |
| {{site.data.keyword.redhat_openshift_notm}} (master) | 4.11.22 | 4.12.2 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html){: external}. Updated to resolve [CVE-2022-3172](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-3172){: external}. For more information, see the [Security bulletin](https://www.ibm.com/support/pages/node/6997115){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} (worker node) | 4.11.26 | 4.12.2 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.11.0-20230123 | v4.12.0-20230124 | See the [{{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20230124){: external}. |
| OpenVPN Operator image | v1.4.13 | v1.4.20 | Updated `ansible-operator` base image to version `v1.26.1` to resolve CVEs. |
| Pause container image | 3.8 | 3.9 | See the [pause container image release notes](https://github.com/kubernetes/kubernetes/blob/master/build/pause/CHANGELOG.md){: external}. |
| Portieris admission controller | v0.12.6 | v0.13.3 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.13.3){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud Metrics Server | v4.11.0-20230123 | v4.12.0-20230124 | See the [{{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20230124){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud toolkit | 4.11.0+20230123 | 4.12.0+20230124 | See the [{{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20230124){: external}. |
{: caption="Changes since master fix pack 4.11.22_1540_openshift and worker fix pack 4.11.26_1542_openshift" caption-side="bottom"}


