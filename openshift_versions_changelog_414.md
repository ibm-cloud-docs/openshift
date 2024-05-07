---

copyright:
  years: 2023, 2024
lastupdated: "2024-05-07"


keywords: openshift, 4.14, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# Version 4.14 change log
{: #openshift_changelog_414}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.14. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #openshift_changelog_overview_414}

Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security){: external} for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}

### Change log for worker node fix pack 4.14.23_1561_openshift, released 06 May 2024
{: #41423_1561_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.14.23_1561_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.14.21 | 4.14.23 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-23){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-513.24.1.el8_9 | Worker node package updates for [RHSA-2024:2098](https://access.redhat.com/errata/RHSA-2024:2098){: external}, [CVE-2024-1753](https://nvd.nist.gov/vuln/detail/CVE-2024-1753){: external}. |
| HAProxy | 295dba8 | 295dba8 | N/A |
{: caption="Changes since version 4.14.21_1559_openshift" caption-side="bottom"}


### Change log for master fix pack 4.14.20_1558_openshift, released 24 April 2024
{: #41420_1558_openshift_M}

The following table shows the changes that are in the master fix pack 4.14.20_1558_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.5.3 | v1.5.4 | New version contains updates and security fixes. |
| etcd | v3.5.12 | v3.5.13 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.13){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.27.12-1 | v1.27.12-10 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | bd30030 | 4c5d156 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.8 | v2.8.9 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2831 | 2867 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.12 | v0.13.13 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.13){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.14.16 | 4.14.20 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-20){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | 4.14.0+20240226 | 4.14.0+20240412 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.14.0+20240412){: external}. |
{: caption="Changes since version 4.14.16_1555_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.14.21_1559_openshift, released 22 April 2024
{: #41421_1559_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.14.21_1559_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.14.19 | 4.14.21 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-21){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-513.24.1.el8_9 | Worker node package updates for [RHSA-2024:1782](https://access.redhat.com/errata/RHSA-2024:1782){: external}, [CVE-2023-4408](https://nvd.nist.gov/vuln/detail/CVE-2023-4408){: external}, [CVE-2023-50387](https://nvd.nist.gov/vuln/detail/CVE-2023-50387){: external}, [CVE-2023-50868](https://nvd.nist.gov/vuln/detail/CVE-2023-50868){: external}, [RHSA-2024:1784](https://access.redhat.com/errata/RHSA-2024:1784){: external}, [CVE-2024-28834](https://nvd.nist.gov/vuln/detail/CVE-2024-28834){: external}. |
| HAProxy | 295dba8 | 4e826da | Security fixes for [CVE-2024-28834](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2024-28834){: external}. |
{: caption="Changes since version 4.14.19_1557_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.14.19_1557_openshift, released 8 April 2024
{: #41419_1557_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.14.19_1557_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.14.17 | 4.14.19 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-19){: external}. |
| RHEL 8 Packages | 4.18.0-513.18.1.el8_9 | 4.18.0-513.24.1.el8_9 | Worker node and kernel packages for [RHSA-2024:1607](https://access.redhat.com/errata/RHSA-2024:1607){: external}, [CVE-2021-33631](https://nvd.nist.gov/vuln/detail/CVE-2021-33631){: external}, [CVE-2022-38096](https://nvd.nist.gov/vuln/detail/CVE-2022-38096){: external}, [CVE-2023-51042](https://nvd.nist.gov/vuln/detail/CVE-2023-51042){: external}, [CVE-2023-6546](https://nvd.nist.gov/vuln/detail/CVE-2023-6546){: external}, [CVE-2023-6931](https://nvd.nist.gov/vuln/detail/CVE-2023-6931){: external}, [CVE-2024-0565](https://nvd.nist.gov/vuln/detail/CVE-2024-0565){: external}, [CVE-2024-1086](https://nvd.nist.gov/vuln/detail/CVE-2024-1086){: external}, [RHSA-2024:1601](https://access.redhat.com/errata/RHSA-2024:1601){: external}, [CVE-2023-28322](https://nvd.nist.gov/vuln/detail/CVE-2023-28322){: external}, [CVE-2023-38546](https://nvd.nist.gov/vuln/detail/CVE-2023-38546){: external}, [CVE-2023-46218](https://nvd.nist.gov/vuln/detail/CVE-2023-46218){: external}, [RHSA-2024:1615](https://access.redhat.com/errata/RHSA-2024:1615){: external}, [CVE-2023-52425](https://nvd.nist.gov/vuln/detail/CVE-2023-52425){: external}, [RHSA-2024:1610](https://access.redhat.com/errata/RHSA-2024:1610){: external}, [CVE-2022-48624](https://nvd.nist.gov/vuln/detail/CVE-2022-48624){: external}. |
| HAProxy | 512b32a | 295dba8 | Security fixes for [CVE-2023-28322](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-28322){: external}, [CVE-2023-38546](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-38546){: external}, [CVE-2023-46218](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-46218){: external}, [CVE-2023-52425](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-52425){: external}. |
{: caption="Changes since version 4.14.17_1556_openshift" caption-side="bottom"}


### Change log for master fix pack 4.14.16_1555_openshift, released 27 March 2024
{: #41416_1555_openshift_M}

The following table shows the changes that are in the master fix pack 4.14.16_1555_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.5.2 | v1.5.3 | New version contains updates and security fixes. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1534 | 1537 | New version contains security fixes. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.5.7 | v2.5.8 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.27.11-2 | v1.27.12-1 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 441 | 442 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.7 | v2.8.8 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2807 | 2831 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.11 | v0.13.12 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.12){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.14.12 | 4.14.16 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-16){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | 4.14.0+20240209 | 4.14.0+20240226 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.14.0+20240226){: external}. |
{: caption="Changes since version 4.14.12_1552_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.14.17_1556_openshift, released 25 March 2024
{: #41417_1556_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.14.17_1556_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.14.15 | 4.14.17 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-17){: external}. |
| RHEL 8 Packages | 4.18.0-513.18.1.el8_9 | 4.18.0-513.18.1.el8_9 | N/A |
| CRI-O | 1.27.4-2 | 1.27.4-3 | N/A |
| HAProxy | 512b32 | 512b32 | N/A |
{: caption="Changes since version 4.14.15_1554_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.14.15_1554_openshift, released 13 March 2024
{: #41415_1554_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.14.15_1554_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.14.13 | 4.14.15 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-15){: external}. |
| RHEL 8 Packages | 4.18.0-513.18.1.el8_9 | 4.18.0-513.18.1.el8_9 | N/A |
| HAProxy | a13673 | 512b32 | N/A |
{: caption="Changes since version 4.14.13_1553_openshift" caption-side="bottom"}


### Change log for master fix pack 4.14.12_1552_openshift, released 28 February 2024
{: #41412_1552_openshift_M}

The following table shows the changes that are in the master fix pack 4.14.12_1552_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.5.1 | v1.5.2 | New version contains updates and security fixes. |
| etcd | v3.5.11 | v3.5.12 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.12){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1525 | 1534 | New version contains security fixes. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.5.4 | v2.5.7 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.27.10-3 | v1.27.11-2 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 439 | 441 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 7185ea1 | bd30030 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.6 | v2.8.7 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2789 | 2807 | New version contains updates and security fixes. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.14.8 | 4.14.12 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-12){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.14.0-20240109 | v4.14.0-20240209 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.14.0%2B20240208){: external}. |
{: caption="Changes since version 4.14.8_1545_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.14.13_1553_openshift, released 26 February 2024
{: #41413_1553_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.14.13_1553_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.14.11| 4.14.13 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-13){: external}. |
| RHEL 8 Packages| 4.18.0-513.11.1.el8_9 | 4.18.0-513.18.1.el8_9 | Package updates for [RHSA-2024:0897](https://access.redhat.com/errata/RHSA-2024:0897){: external}, [CVE-2022-3545](https://nvd.nist.gov/vuln/detail/CVE-2022-3545){: external}, [CVE-2022-41858](https://nvd.nist.gov/vuln/detail/CVE-2022-41858){: external}, [CVE-2023-1073](https://nvd.nist.gov/vuln/detail/CVE-2023-1073){: external}, [CVE-2023-1838](https://nvd.nist.gov/vuln/detail/CVE-2023-1838){: external}, [CVE-2023-2166](https://nvd.nist.gov/vuln/detail/CVE-2023-2166){: external}, [CVE-2023-2176](https://nvd.nist.gov/vuln/detail/CVE-2023-2176){: external}, [CVE-2023-40283](https://nvd.nist.gov/vuln/detail/CVE-2023-40283){: external}, [CVE-2023-45871](https://nvd.nist.gov/vuln/detail/CVE-2023-45871){: external}, [CVE-2023-4623](https://nvd.nist.gov/vuln/detail/CVE-2023-4623){: external}, [CVE-2023-46813](https://nvd.nist.gov/vuln/detail/CVE-2023-46813){: external}, [CVE-2023-4921](https://nvd.nist.gov/vuln/detail/CVE-2023-4921){: external}, [CVE-2023-5717](https://nvd.nist.gov/vuln/detail/CVE-2023-5717){: external}, [CVE-2023-6356](https://nvd.nist.gov/vuln/detail/CVE-2023-6356){: external}, [CVE-2023-6535](https://nvd.nist.gov/vuln/detail/CVE-2023-6535){: external}, [CVE-2023-6536](https://nvd.nist.gov/vuln/detail/CVE-2023-6536){: external}, [CVE-2023-6606](https://nvd.nist.gov/vuln/detail/CVE-2023-6606){: external}, [CVE-2023-6610](https://nvd.nist.gov/vuln/detail/CVE-2023-6610){: external}, [CVE-2023-6817](https://nvd.nist.gov/vuln/detail/CVE-2023-6817){: external}, [CVE-2024-0646](https://nvd.nist.gov/vuln/detail/CVE-2024-0646){: external}, [RHSA-2024:0768](https://access.redhat.com/errata/RHSA-2024:0768){: external}, [CVE-2020-28241](https://nvd.nist.gov/vuln/detail/CVE-2020-28241){: external}, [RHSA-2024:0889](https://access.redhat.com/errata/RHSA-2024:0889){: external}, [CVE-2019-13224](https://nvd.nist.gov/vuln/detail/CVE-2019-13224){: external}, [CVE-2019-16163](https://nvd.nist.gov/vuln/detail/CVE-2019-16163){: external}, [CVE-2019-19012](https://nvd.nist.gov/vuln/detail/CVE-2019-19012){: external}, [CVE-2019-19203](https://nvd.nist.gov/vuln/detail/CVE-2019-19203){: external}, [CVE-2019-19204](https://nvd.nist.gov/vuln/detail/CVE-2019-19204){: external}, [RHSA-2024:0811](https://access.redhat.com/errata/RHSA-2024:0811){: external}, [CVE-2023-28486](https://nvd.nist.gov/vuln/detail/CVE-2023-28486){: external}, [CVE-2023-28487](https://nvd.nist.gov/vuln/detail/CVE-2023-28487){: external}, [CVE-2023-42465](https://nvd.nist.gov/vuln/detail/CVE-2023-42465){: external}. |
{: caption="Changes since version 4.14.11_1547_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.14.11_1547_openshift, released 12 February 2024
{: #41411_1547_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.14.11_1547_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.14.10 | 4.14.11 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-11){: external}. |
| RHEL 8 Packages | 4.18.0-477.27.1.el8_8 | 4.18.0-513.11.1.el8_9 | Package updates for [RHSA-2024:0752](https://access.redhat.com/errata/RHSA-2024:0752){: external}, [CVE-2024-21626](https://nvd.nist.gov/vuln/detail/CVE-2024-21626){: external}, [RHSA-2023:7549](https://access.redhat.com/errata/RHSA-2023:7549){: external}, [CVE-2022-45884](https://nvd.nist.gov/vuln/detail/CVE-2022-45884){: external}, [CVE-2022-45886](https://nvd.nist.gov/vuln/detail/CVE-2022-45886){: external}, [CVE-2022-45919](https://nvd.nist.gov/vuln/detail/CVE-2022-45919){: external}, [CVE-2023-1192](https://nvd.nist.gov/vuln/detail/CVE-2023-1192){: external}, [CVE-2023-2163](https://nvd.nist.gov/vuln/detail/CVE-2023-2163){: external}, [CVE-2023-3812](https://nvd.nist.gov/vuln/detail/CVE-2023-3812){: external}, [CVE-2023-5178](https://nvd.nist.gov/vuln/detail/CVE-2023-5178){: external}, [RHSA-2024:0113](https://access.redhat.com/errata/RHSA-2024:0113){: external}, [CVE-2022-36402](https://nvd.nist.gov/vuln/detail/CVE-2022-36402){: external}, [CVE-2023-20569](https://nvd.nist.gov/vuln/detail/CVE-2023-20569){: external}, [CVE-2023-2162](https://nvd.nist.gov/vuln/detail/CVE-2023-2162){: external}, [CVE-2023-42753](https://nvd.nist.gov/vuln/detail/CVE-2023-42753){: external}, [CVE-2023-4622](https://nvd.nist.gov/vuln/detail/CVE-2023-4622){: external}, [CVE-2023-5633](https://nvd.nist.gov/vuln/detail/CVE-2023-5633){: external}, [RHSA-2023:7077](https://access.redhat.com/errata/RHSA-2023:7077){: external}, [CVE-2021-43975](https://nvd.nist.gov/vuln/detail/CVE-2021-43975){: external}, [CVE-2022-28388](https://nvd.nist.gov/vuln/detail/CVE-2022-28388){: external}, [CVE-2022-3594](https://nvd.nist.gov/vuln/detail/CVE-2022-3594){: external}, [CVE-2022-3640](https://nvd.nist.gov/vuln/detail/CVE-2022-3640){: external}, [CVE-2022-38457](https://nvd.nist.gov/vuln/detail/CVE-2022-38457){: external}, [CVE-2022-40133](https://nvd.nist.gov/vuln/detail/CVE-2022-40133){: external}, [CVE-2022-40982](https://nvd.nist.gov/vuln/detail/CVE-2022-40982){: external}, [CVE-2022-42895](https://nvd.nist.gov/vuln/detail/CVE-2022-42895){: external}, [CVE-2022-45869](https://nvd.nist.gov/vuln/detail/CVE-2022-45869){: external}, [CVE-2022-45887](https://nvd.nist.gov/vuln/detail/CVE-2022-45887){: external}, [CVE-2022-4744](https://nvd.nist.gov/vuln/detail/CVE-2022-4744){: external}, [CVE-2023-0458](https://nvd.nist.gov/vuln/detail/CVE-2023-0458){: external}, [CVE-2023-0590](https://nvd.nist.gov/vuln/detail/CVE-2023-0590){: external}, [CVE-2023-0597](https://nvd.nist.gov/vuln/detail/CVE-2023-0597){: external}, [CVE-2023-1073](https://nvd.nist.gov/vuln/detail/CVE-2023-1073){: external}, [CVE-2023-1074](https://nvd.nist.gov/vuln/detail/CVE-2023-1074){: external}, [CVE-2023-1075](https://nvd.nist.gov/vuln/detail/CVE-2023-1075){: external}, [CVE-2023-1079](https://nvd.nist.gov/vuln/detail/CVE-2023-1079){: external}, [CVE-2023-1118](https://nvd.nist.gov/vuln/detail/CVE-2023-1118){: external}, [CVE-2023-1206](https://nvd.nist.gov/vuln/detail/CVE-2023-1206){: external}, [CVE-2023-1252](https://nvd.nist.gov/vuln/detail/CVE-2023-1252){: external}, [CVE-2023-1382](https://nvd.nist.gov/vuln/detail/CVE-2023-1382){: external}, [CVE-2023-1855](https://nvd.nist.gov/vuln/detail/CVE-2023-1855){: external}, [CVE-2023-1989](https://nvd.nist.gov/vuln/detail/CVE-2023-1989){: external}, [CVE-2023-1998](https://nvd.nist.gov/vuln/detail/CVE-2023-1998){: external}, [CVE-2023-2269](https://nvd.nist.gov/vuln/detail/CVE-2023-2269){: external}, [CVE-2023-23455](https://nvd.nist.gov/vuln/detail/CVE-2023-23455){: external}, [CVE-2023-2513](https://nvd.nist.gov/vuln/detail/CVE-2023-2513){: external}, [CVE-2023-26545](https://nvd.nist.gov/vuln/detail/CVE-2023-26545){: external}, [CVE-2023-28328](https://nvd.nist.gov/vuln/detail/CVE-2023-28328){: external}, [CVE-2023-28772](https://nvd.nist.gov/vuln/detail/CVE-2023-28772){: external}, [CVE-2023-30456](https://nvd.nist.gov/vuln/detail/CVE-2023-30456){: external}, [CVE-2023-31084](https://nvd.nist.gov/vuln/detail/CVE-2023-31084){: external}, [CVE-2023-3141](https://nvd.nist.gov/vuln/detail/CVE-2023-3141){: external}, [CVE-2023-31436](https://nvd.nist.gov/vuln/detail/CVE-2023-31436){: external}, [CVE-2023-3161](https://nvd.nist.gov/vuln/detail/CVE-2023-3161){: external}, [CVE-2023-3212](https://nvd.nist.gov/vuln/detail/CVE-2023-3212){: external}, [CVE-2023-3268](https://nvd.nist.gov/vuln/detail/CVE-2023-3268){: external}, [CVE-2023-33203](https://nvd.nist.gov/vuln/detail/CVE-2023-33203){: external}, [CVE-2023-33951](https://nvd.nist.gov/vuln/detail/CVE-2023-33951){: external}, [CVE-2023-33952](https://nvd.nist.gov/vuln/detail/CVE-2023-33952){: external}, [CVE-2023-35823](https://nvd.nist.gov/vuln/detail/CVE-2023-35823){: external}, [CVE-2023-35824](https://nvd.nist.gov/vuln/detail/CVE-2023-35824){: external}, [CVE-2023-35825](https://nvd.nist.gov/vuln/detail/CVE-2023-35825){: external}, [CVE-2023-3609](https://nvd.nist.gov/vuln/detail/CVE-2023-3609){: external}, [CVE-2023-3611](https://nvd.nist.gov/vuln/detail/CVE-2023-3611){: external}, [CVE-2023-3772](https://nvd.nist.gov/vuln/detail/CVE-2023-3772){: external}, [CVE-2023-4128](https://nvd.nist.gov/vuln/detail/CVE-2023-4128){: external}, [CVE-2023-4132](https://nvd.nist.gov/vuln/detail/CVE-2023-4132){: external}, [CVE-2023-4155](https://nvd.nist.gov/vuln/detail/CVE-2023-4155){: external}, [CVE-2023-4206](https://nvd.nist.gov/vuln/detail/CVE-2023-4206){: external}, [CVE-2023-4207](https://nvd.nist.gov/vuln/detail/CVE-2023-4207){: external}, [CVE-2023-4208](https://nvd.nist.gov/vuln/detail/CVE-2023-4208){: external}, [CVE-2023-4732](https://nvd.nist.gov/vuln/detail/CVE-2023-4732){: external}, [CVE-2024-0443](https://nvd.nist.gov/vuln/detail/CVE-2024-0443){: external}, [RHSA-2023:7877](https://access.redhat.com/errata/RHSA-2023:7877){: external}, [CVE-2023-3446](https://nvd.nist.gov/vuln/detail/CVE-2023-3446){: external}, [CVE-2023-3817](https://nvd.nist.gov/vuln/detail/CVE-2023-3817){: external}, [CVE-2023-5678](https://nvd.nist.gov/vuln/detail/CVE-2023-5678){: external}, [RHSA-2023:7187](https://access.redhat.com/errata/RHSA-2023:7187){: external}, [CVE-2023-4016](https://nvd.nist.gov/vuln/detail/CVE-2023-4016){: external}, [RHSA-2023:7112](https://access.redhat.com/errata/RHSA-2023:7112){: external}, [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/CVE-2023-4641){: external}, [RHSA-2023:7166](https://access.redhat.com/errata/RHSA-2023:7166){: external}, [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/CVE-2023-22745){: external}, [RHSA-2023:7177](https://access.redhat.com/errata/RHSA-2023:7177){: external}, [CVE-2022-3094](https://nvd.nist.gov/vuln/detail/CVE-2022-3094){: external}, [RHSA-2023:7116](https://access.redhat.com/errata/RHSA-2023:7116){: external}, [CVE-2022-4904](https://nvd.nist.gov/vuln/detail/CVE-2022-4904){: external}, [RHSA-2023:7207](https://access.redhat.com/errata/RHSA-2023:7207){: external}, [CVE-2020-22217](https://nvd.nist.gov/vuln/detail/CVE-2020-22217){: external}, [CVE-2023-31130](https://nvd.nist.gov/vuln/detail/CVE-2023-31130){: external}, [RHSA-2023:6943](https://access.redhat.com/errata/RHSA-2023:6943){: external}, [CVE-2023-1786](https://nvd.nist.gov/vuln/detail/CVE-2023-1786){: external}, [RHSA-2023:6939](https://access.redhat.com/errata/RHSA-2023:6939){: external}, [CVE-2022-3064](https://nvd.nist.gov/vuln/detail/CVE-2022-3064){: external}, [CVE-2022-41723](https://nvd.nist.gov/vuln/detail/CVE-2022-41723){: external}, [CVE-2022-41724](https://nvd.nist.gov/vuln/detail/CVE-2022-41724){: external}, [CVE-2022-41725](https://nvd.nist.gov/vuln/detail/CVE-2022-41725){: external}, [CVE-2023-24534](https://nvd.nist.gov/vuln/detail/CVE-2023-24534){: external}, [CVE-2023-24536](https://nvd.nist.gov/vuln/detail/CVE-2023-24536){: external}, [CVE-2023-24537](https://nvd.nist.gov/vuln/detail/CVE-2023-24537){: external}, [CVE-2023-24538](https://nvd.nist.gov/vuln/detail/CVE-2023-24538){: external}, [CVE-2023-24539](https://nvd.nist.gov/vuln/detail/CVE-2023-24539){: external}, [CVE-2023-24540](https://nvd.nist.gov/vuln/detail/CVE-2023-24540){: external}, [CVE-2023-25173](https://nvd.nist.gov/vuln/detail/CVE-2023-25173){: external}, [CVE-2023-25809](https://nvd.nist.gov/vuln/detail/CVE-2023-25809){: external}, [CVE-2023-27561](https://nvd.nist.gov/vuln/detail/CVE-2023-27561){: external}, [CVE-2023-28642](https://nvd.nist.gov/vuln/detail/CVE-2023-28642){: external}, [CVE-2023-29400](https://nvd.nist.gov/vuln/detail/CVE-2023-29400){: external}, [CVE-2023-29406](https://nvd.nist.gov/vuln/detail/CVE-2023-29406){: external}, [CVE-2023-3978](https://nvd.nist.gov/vuln/detail/CVE-2023-3978){: external}, [RHSA-2024:0155](https://access.redhat.com/errata/RHSA-2024:0155){: external}, [CVE-2023-5981](https://nvd.nist.gov/vuln/detail/CVE-2023-5981){: external}, [RHSA-2024:0627](https://access.redhat.com/errata/RHSA-2024:0627){: external}, [CVE-2024-0553](https://nvd.nist.gov/vuln/detail/CVE-2024-0553){: external}, [RHSA-2023:6976](https://access.redhat.com/errata/RHSA-2023:6976){: external}, [CVE-2020-12762](https://nvd.nist.gov/vuln/detail/CVE-2020-12762){: external}, [RHSA-2024:0628](https://access.redhat.com/errata/RHSA-2024:0628){: external}, [CVE-2023-48795](https://nvd.nist.gov/vuln/detail/CVE-2023-48795){: external}, [RHSA-2024:0119](https://access.redhat.com/errata/RHSA-2024:0119){: external}, [CVE-2023-39615](https://nvd.nist.gov/vuln/detail/CVE-2023-39615){: external}, [RHSA-2023:7109](https://access.redhat.com/errata/RHSA-2023:7109){: external}, [CVE-2023-20569](https://nvd.nist.gov/vuln/detail/CVE-2023-20569){: external}, [RHSA-2024:0606](https://access.redhat.com/errata/RHSA-2024:0606){: external}, [CVE-2023-48795](https://nvd.nist.gov/vuln/detail/CVE-2023-48795){: external}, [CVE-2023-51385](https://nvd.nist.gov/vuln/detail/CVE-2023-51385){: external}, [RHSA-2023:7174](https://access.redhat.com/errata/RHSA-2023:7174){: external}, [CVE-2023-31486](https://nvd.nist.gov/vuln/detail/CVE-2023-31486){: external}, [RHSA-2023:6944](https://access.redhat.com/errata/RHSA-2023:6944){: external}, [CVE-2022-48468](https://nvd.nist.gov/vuln/detail/CVE-2022-48468){: external}, [RHSA-2023:7096](https://access.redhat.com/errata/RHSA-2023:7096){: external}, [CVE-2023-23931](https://nvd.nist.gov/vuln/detail/CVE-2023-23931){: external}, [RHSA-2023:7176](https://access.redhat.com/errata/RHSA-2023:7176){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [RHSA-2024:0116](https://access.redhat.com/errata/RHSA-2024:0116){: external}, [CVE-2023-43804](https://nvd.nist.gov/vuln/detail/CVE-2023-43804){: external}, [CVE-2023-45803](https://nvd.nist.gov/vuln/detail/CVE-2023-45803){: external}, [RHSA-2023:7151](https://access.redhat.com/errata/RHSA-2023:7151){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [RHSA-2024:0114](https://access.redhat.com/errata/RHSA-2024:0114){: external}, [CVE-2022-48560](https://nvd.nist.gov/vuln/detail/CVE-2022-48560){: external}, [CVE-2022-48564](https://nvd.nist.gov/vuln/detail/CVE-2022-48564){: external}, [RHSA-2024:0256](https://access.redhat.com/errata/RHSA-2024:0256){: external}, [CVE-2023-27043](https://nvd.nist.gov/vuln/detail/CVE-2023-27043){: external}, [RHSA-2023:7034](https://access.redhat.com/errata/RHSA-2023:7034){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [CVE-2023-32681](https://nvd.nist.gov/vuln/detail/CVE-2023-32681){: external}, [RHSA-2023:7058](https://access.redhat.com/errata/RHSA-2023:7058){: external}, [CVE-2022-41723](https://nvd.nist.gov/vuln/detail/CVE-2022-41723){: external}, [RHSA-2024:0647](https://access.redhat.com/errata/RHSA-2024:0647){: external}, [CVE-2021-35937](https://nvd.nist.gov/vuln/detail/CVE-2021-35937){: external}, [CVE-2021-35938](https://nvd.nist.gov/vuln/detail/CVE-2021-35938){: external}, [CVE-2021-35939](https://nvd.nist.gov/vuln/detail/CVE-2021-35939){: external}, [RHSA-2024:0253](https://access.redhat.com/errata/RHSA-2024:0253){: external}, [CVE-2023-7104](https://nvd.nist.gov/vuln/detail/CVE-2023-7104){: external}, [RHSA-2023:7057](https://access.redhat.com/errata/RHSA-2023:7057){: external}, [CVE-2023-33460](https://nvd.nist.gov/vuln/detail/CVE-2023-33460){: external}. |
{: caption="Changes since version 4.14.10_1546_openshift" caption-side="bottom"}


### Change log for master fix pack 4.14.8_1545_openshift, released 31 January 2024
{: #4148_1545_openshift_M}

The following table shows the changes that are in the master fix pack 4.14.8_1545_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.26.3 | v3.26.4 | See the [Calico release notes](https://docs.tigera.io/calico/3.26/release-notes/#v3.26.4){: external}. |
| Tigera Operator | v1.30.7 | v1.30.9 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.30.9){: external}. |
| Calico policy controller | v3.26.3 | v3.26.4 | See the [Calico release notes](https://github.com/projectcalico/calico/blob/release-v3.26/release-notes/v3.26.4-release-notes.md){: external}. |
| Cluster health image | v1.5.0 | v1.5.1 | New version contains security fixes. |
| etcd | v3.5.10 | v3.5.11 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.11){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1512 | 1525 | New version contains security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.27.8-6 | v1.27.10-3 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | e544e35 | 7185ea1 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.5 | v2.8.6 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2767 | 2789 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.10 | v0.13.11 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.11){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.14.5 | 4.14.8 | See the {{site.data.keyword.openshiftlong_notm}} [release notes](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-8){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.14.0-20231128 | v4.14.0-20240109 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.14.0%2B20240109){: external}. |
{: caption="Changes since version 4.14.5_1539_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.14.10_1546_openshift, released 29 January 2024
{: #41410_1546_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.14.10_1546_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.14.8 | 4.14.10 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-10){: external}. |
| Rhel8 Packages | 4.18.0-477.27.1.el8_8 | 4.18.0-477.27.1.el8_8 | N/A |
| HAProxy | e105dc | a13673 | Security fixes for [CVE-2023-7104](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-7104){: external}, [CVE-2023-27043](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-27043){: external}. |
{: caption="Changes since version 4.14.8_1544_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.14.8_1544_openshift, released 16 January 2024
{: #4148_1544_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.14.8_1544_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.14.6 | 4.14.8 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-8){: external}. |
| RHEL 8 Packages | N/A | N/A | N/A |
| Haproxy | 3060b0 | e105dc | [CVE-2023-39615](https://nvd.nist.gov/vuln/detail/CVE-2023-39615){: external}, [CVE-2023-5981](https://nvd.nist.gov/vuln/detail/CVE-2023-5981){: external}, [CVE-2022-48560](https://nvd.nist.gov/vuln/detail/CVE-2022-48560){: external}, [CVE-2022-48564](https://nvd.nist.gov/vuln/detail/CVE-2022-48564){: external}. |
{: caption="Changes since version 4.14.6_1542_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.14.6_1542_openshift, released 02 January 2024
{: #4146_1542_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.14.6_1542_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.14.6 | 4.14.6 | N/A |
| RHEL 8 Packages | 4.18.0-477.27.1.el8_8 | 4.18.0-477.27.1.el8_8 | N/A |
{: caption="Changes since version 4.14.6_1541_openshift" caption-side="bottom"}


### Change log for master fix pack 4.14.5_1539_openshift and worker node fix pack 4.14.4_1538_openshift, released 13 December 2023
{: #4.14.5_1539_openshiftM_4.14.4_1538_openshiftW}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.4.5 | v1.5.0 | New version contains updates and security fixes. |
| etcd | N/A | N/A | etcd is now automatically defragmented when necessary. |
| HAProxy configuration | N/A | N/A | Updated master health probes to use the `/livez/ping` endpoint. |
| IBM Cloud Block Storage driver and plug-in | v2.4.14 | v2.5.4 | New version contains updates and security fixes. |
| IBM Cloud Controller Manager | v1.26.11-6 | v1.27.8-6 | New version contains updates and security fixes. |
| **Removed:** OpenVPN Operator, client, and server | N/A | N/A | Konnectivity components (part of Red Hat OpenShift) replace the OpenVPN components as the network proxy used to secure the communication of the Kubernetes API server master to worker nodes in the cluster. |
| Red Hat OpenShift (master) | 4.13.23 | 4.14.5 | See the [Red Hat OpenShift release notes](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-5). |
| Red Hat OpenShift (worker node) | 4.13.24 | 4.14.4 | See the [Red Hat OpenShift release notes](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-4). |
| Red Hat OpenShift on IBM Cloud Control Plane Operator, Metrics Server, and toolkit | 4.13.0+20231102 | 4.14.0+20231128 | See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.14.0+20231128). |
{: caption="Changes since master fix pack 4.13.23_1550_openshift and worker fix pack 4.13.24_1551_openshift." caption-side="bottom"}







