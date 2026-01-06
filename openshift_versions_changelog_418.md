---

copyright:
  years: 2024, 2026

lastupdated: "2026-01-06"


keywords: change log, version history, 4.18_openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# 4.18 version change log
{: #openshift_changelog_418}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run this version. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #changelog_overview_418}


Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security){: external} for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}

## Version 4.18
{: #418_components}


### Worker node fix pack 4.18.30_1573_openshift, released 29 December 2025
{: #cl-boms-41830_1573_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.30_1573_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL 9|5.14.0-570.60.1.el9_6|N/A|
|Red Hat OpenShift|4.18.30|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-30_release-notes).|
|Red Hat CoreOS|4.18.30|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-30_release-notes).|
|HAProxy|d04e61c5b29aa5328bc72455edb95e08e8f6d85c|Resolves the following CVEs: [CVE-2025-9086](https://nvd.nist.gov/vuln/detail/CVE-2025-9086){: external}.|
{: caption="4.18.30_1573_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41830_1573_openshift_W-component-table}


### Worker node fix pack 4.18.30_1572_openshift, released 16 December 2025
{: #cl-boms-41830_1572_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.30_1572_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL 9|5.14.0-570.60.1.el9_6|N/A|
|Red Hat OpenShift|4.18.30|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-30_release-notes).|
|Red Hat CoreOS|4.18.30|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-30_release-notes).|
|HAProxy|03b74b82b63cd53403b6b587b84233c93edef18d|N/A|
{: caption="4.18.30_1572_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41830_1572_openshift_W-component-table}


### Change log for Master fix pack 4.18.28_1571_openshift, released 10 December 2025
{: #41828_1571_openshift_M}

The following table shows the changes that are in the master fix pack 4.18.28_1571_openshift. Master patch updates are applied automatically. 


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.6.10 | v1.6.13 | New version contains updates and security fixes. |
| etcd | v3.5.24 | v3.5.25 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.25){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.31.13-6 | v1.31.14-3 | New version contains updates and security fixes. |
| Key Management Service provider | v2.10.17 | 2.10.19 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.31 | v0.13.33 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.33){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.18.26 | 4.18.28 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes#ocp-4-18-28_release-notes){: external}. |
{: caption="Changes since version 4.18.27-1568-openshift" caption-side="bottom"}


### Worker node fix pack 4.18.29_1570_openshift, released 03 December 2025
{: #cl-boms-41829_1570_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.29_1570_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL 9|5.14.0-570.60.1.el9_6|N/A|
|Red Hat OpenShift|4.18.29|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-29_release-notes).|
|Red Hat CoreOS|4.18.29|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-29_release-notes).|
|HAProxy|03b74b82b63cd53403b6b587b84233c93edef18d|Resolves the following CVEs: [CVE-2025-59375](https://nvd.nist.gov/vuln/detail/CVE-2025-59375){: external}, [CVE-2025-5372](https://nvd.nist.gov/vuln/detail/CVE-2025-5372){: external}, [CVE-2024-28757](https://nvd.nist.gov/vuln/detail/CVE-2024-28757){: external}, and [CVE-2022-23990](https://nvd.nist.gov/vuln/detail/CVE-2022-23990){: external}.|
{: caption="4.18.29_1570_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41829_1570_openshift_W-component-table}


### Worker node fix pack 4.18.27_1569_openshift, released 17 November 2025
{: #cl-boms-41827_1569_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.27_1569_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL 9|5.14.0-570.60.1.el9_6|Resolves the following CVEs: [RHSA-2025:19951](https://access.redhat.com/errata/RHSA-2025:19951){: external}, [CVE-2025-40778](https://nvd.nist.gov/vuln/detail/CVE-2025-40778){: external}, [CVE-2025-40780](https://nvd.nist.gov/vuln/detail/CVE-2025-40780){: external}, [RHSA-2025:19105](https://access.redhat.com/errata/RHSA-2025:19105){: external}, [CVE-2023-53331](https://nvd.nist.gov/vuln/detail/CVE-2023-53331){: external}, [CVE-2025-39718](https://nvd.nist.gov/vuln/detail/CVE-2025-39718){: external}, [CVE-2025-39730](https://nvd.nist.gov/vuln/detail/CVE-2025-39730){: external}, [CVE-2025-39751](https://nvd.nist.gov/vuln/detail/CVE-2025-39751){: external}, [CVE-2025-39819](https://nvd.nist.gov/vuln/detail/CVE-2025-39819){: external}, [RHSA-2025:19409](https://access.redhat.com/errata/RHSA-2025:19409){: external}, [CVE-2022-50367](https://nvd.nist.gov/vuln/detail/CVE-2022-50367){: external}, [CVE-2023-53494](https://nvd.nist.gov/vuln/detail/CVE-2023-53494){: external}, and [CVE-2025-39702](https://nvd.nist.gov/vuln/detail/CVE-2025-39702){: external}.|
|Red Hat OpenShift|4.18.27|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-27_release-notes).|
|Red Hat CoreOS|4.18.27|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-27_release-notes).|
|HAProxy|fbe9b8146f23bbd12b2566a79fa897d5981e7273|N/A|
{: caption="4.18.27_1569_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41827_1569_openshift_W-component-table}


### Master fix pack 4.18.27_1568_openshift, released 15 November 2025
{: #41827_1568_openshift_M}

The following table shows the changes that are in the master fix pack 4.18.27_1568_openshift. Master patch updates are applied automatically. 


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.29.5 | v3.29.6 | See the [Calico release notes](https://docs.tigera.io/calico/3.29/release-notes/#calico-open-source-3296-bug-fix-release){: external}. |
| etcd | v3.5.23 | v3.5.24 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.24){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.5.20 | v2.5.22 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.31.13-2 | v1.31.13-6 | New version contains updates and security fixes. |
| Key Management Service provider | v2.10.17 | v2.10.18 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.30 | v0.13.31 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.31){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.18.24 | 4.18.27 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes#ocp-4-18-27_release-notes){: external}. |
| Tigera Operator | v1.36.13 | v1.36.14 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.36.14){: external}. |
{: caption="Changes since version 4.18.24_1563_openshift" caption-side="bottom"}


### Worker node fix pack 4.18.27_1566_openshift, released 06 November 2025
{: #cl-boms-41827_1566_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.27_1566_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-570.55.1.el9_6|Resolves the following CVEs: [RHSA-2025:17377](https://access.redhat.com/errata/RHSA-2025:17377){: external}, [CVE-2024-50301](https://nvd.nist.gov/vuln/detail/CVE-2024-50301){: external}, [CVE-2025-38351](https://nvd.nist.gov/vuln/detail/CVE-2025-38351){: external}, [CVE-2025-39761](https://nvd.nist.gov/vuln/detail/CVE-2025-39761){: external}, [RHSA-2025:17760](https://access.redhat.com/errata/RHSA-2025:17760){: external}, [CVE-2023-53373](https://nvd.nist.gov/vuln/detail/CVE-2023-53373){: external}, [CVE-2025-38556](https://nvd.nist.gov/vuln/detail/CVE-2025-38556){: external}, [CVE-2025-38614](https://nvd.nist.gov/vuln/detail/CVE-2025-38614){: external}, [CVE-2025-39757](https://nvd.nist.gov/vuln/detail/CVE-2025-39757){: external}, [RHSA-2025:18281](https://access.redhat.com/errata/RHSA-2025:18281){: external}, [CVE-2022-50087](https://nvd.nist.gov/vuln/detail/CVE-2022-50087){: external}, [CVE-2025-22026](https://nvd.nist.gov/vuln/detail/CVE-2025-22026){: external}, [CVE-2025-38566](https://nvd.nist.gov/vuln/detail/CVE-2025-38566){: external}, [CVE-2025-38571](https://nvd.nist.gov/vuln/detail/CVE-2025-38571){: external}, [CVE-2025-39817](https://nvd.nist.gov/vuln/detail/CVE-2025-39817){: external}, [CVE-2025-39841](https://nvd.nist.gov/vuln/detail/CVE-2025-39841){: external}, and [CVE-2025-39849](https://nvd.nist.gov/vuln/detail/CVE-2025-39849){: external}.|
|Red Hat OpenShift|4.18.27|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-27_release-notes).|
|Red Hat CoreOS|4.18.27|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-27_release-notes). CIS benchmark compliance [5.1.14](https://workbench.cisecurity.org/sections/2758876/recommendations/4466787), [1.5.2](https://workbench.cisecurity.org/sections/2758917/recommendations/4466863), [1.7.2](https://workbench.cisecurity.org/sections/2758925/recommendations/4466906), [1.7.3](https://workbench.cisecurity.org/sections/2758925/recommendations/4466909)|
|HAProxy|fbe9b8146f23bbd12b2566a79fa897d5981e7273|Resolves the following CVEs: [CVE-2025-5318](https://nvd.nist.gov/vuln/detail/CVE-2025-5318){: external}.|
{: caption="4.18.27_1566_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41827_1566_openshift_W-component-table}


### Worker node fix pack 4.18.26_1565_openshift, released 21 October 2025
{: #cl-boms-41826_1565_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.26_1565_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-570.49.1.el9_6|Resolves the following CVEs: [RHSA-2025:10848](https://access.redhat.com/errata/RHSA-2025:10848){: external}, [CVE-2024-6174](https://nvd.nist.gov/vuln/detail/CVE-2024-6174){: external}, [RHSA-2025:11462](https://access.redhat.com/errata/RHSA-2025:11462){: external}, [CVE-2024-50349](https://nvd.nist.gov/vuln/detail/CVE-2024-50349){: external}, [CVE-2024-52006](https://nvd.nist.gov/vuln/detail/CVE-2024-52006){: external}, [CVE-2025-27613](https://nvd.nist.gov/vuln/detail/CVE-2025-27613){: external}, [CVE-2025-27614](https://nvd.nist.gov/vuln/detail/CVE-2025-27614){: external}, [CVE-2025-46835](https://nvd.nist.gov/vuln/detail/CVE-2025-46835){: external}, [CVE-2025-48384](https://nvd.nist.gov/vuln/detail/CVE-2025-48384){: external}, [CVE-2025-48385](https://nvd.nist.gov/vuln/detail/CVE-2025-48385){: external}, [RHSA-2025:10379](https://access.redhat.com/errata/RHSA-2025:10379){: external}, [CVE-2022-49846](https://nvd.nist.gov/vuln/detail/CVE-2022-49846){: external}, [CVE-2025-21759](https://nvd.nist.gov/vuln/detail/CVE-2025-21759){: external}, [CVE-2025-21887](https://nvd.nist.gov/vuln/detail/CVE-2025-21887){: external}, [CVE-2025-22004](https://nvd.nist.gov/vuln/detail/CVE-2025-22004){: external}, [CVE-2025-37799](https://nvd.nist.gov/vuln/detail/CVE-2025-37799){: external}, [RHSA-2025:11411](https://access.redhat.com/errata/RHSA-2025:11411){: external}, [CVE-2024-58002](https://nvd.nist.gov/vuln/detail/CVE-2024-58002){: external}, [CVE-2025-38089](https://nvd.nist.gov/vuln/detail/CVE-2025-38089){: external}, [RHSA-2025:12746](https://access.redhat.com/errata/RHSA-2025:12746){: external}, [CVE-2022-49788](https://nvd.nist.gov/vuln/detail/CVE-2022-49788){: external}, [CVE-2025-21727](https://nvd.nist.gov/vuln/detail/CVE-2025-21727){: external}, [CVE-2025-21928](https://nvd.nist.gov/vuln/detail/CVE-2025-21928){: external}, [CVE-2025-21929](https://nvd.nist.gov/vuln/detail/CVE-2025-21929){: external}, [CVE-2025-21962](https://nvd.nist.gov/vuln/detail/CVE-2025-21962){: external}, [CVE-2025-22020](https://nvd.nist.gov/vuln/detail/CVE-2025-22020){: external}, [CVE-2025-37890](https://nvd.nist.gov/vuln/detail/CVE-2025-37890){: external}, [CVE-2025-38052](https://nvd.nist.gov/vuln/detail/CVE-2025-38052){: external}, [CVE-2025-38087](https://nvd.nist.gov/vuln/detail/CVE-2025-38087){: external}, [RHSA-2025:13962](https://access.redhat.com/errata/RHSA-2025:13962){: external}, [CVE-2024-28956](https://nvd.nist.gov/vuln/detail/CVE-2024-28956){: external}, [CVE-2025-21867](https://nvd.nist.gov/vuln/detail/CVE-2025-21867){: external}, [CVE-2025-38084](https://nvd.nist.gov/vuln/detail/CVE-2025-38084){: external}, [CVE-2025-38085](https://nvd.nist.gov/vuln/detail/CVE-2025-38085){: external}, [CVE-2025-38124](https://nvd.nist.gov/vuln/detail/CVE-2025-38124){: external}, [CVE-2025-38159](https://nvd.nist.gov/vuln/detail/CVE-2025-38159){: external}, [CVE-2025-38250](https://nvd.nist.gov/vuln/detail/CVE-2025-38250){: external}, [CVE-2025-38380](https://nvd.nist.gov/vuln/detail/CVE-2025-38380){: external}, [CVE-2025-38471](https://nvd.nist.gov/vuln/detail/CVE-2025-38471){: external}, [RHSA-2025:14420](https://access.redhat.com/errata/RHSA-2025:14420){: external}, [CVE-2025-22058](https://nvd.nist.gov/vuln/detail/CVE-2025-22058){: external}, [CVE-2025-37914](https://nvd.nist.gov/vuln/detail/CVE-2025-37914){: external}, [CVE-2025-38417](https://nvd.nist.gov/vuln/detail/CVE-2025-38417){: external}, [RHSA-2025:15011](https://access.redhat.com/errata/RHSA-2025:15011){: external}, [CVE-2025-37823](https://nvd.nist.gov/vuln/detail/CVE-2025-37823){: external}, [CVE-2025-38200](https://nvd.nist.gov/vuln/detail/CVE-2025-38200){: external}, [CVE-2025-38211](https://nvd.nist.gov/vuln/detail/CVE-2025-38211){: external}, [CVE-2025-38350](https://nvd.nist.gov/vuln/detail/CVE-2025-38350){: external}, [CVE-2025-38461](https://nvd.nist.gov/vuln/detail/CVE-2025-38461){: external}, [CVE-2025-38464](https://nvd.nist.gov/vuln/detail/CVE-2025-38464){: external}, [CVE-2025-38500](https://nvd.nist.gov/vuln/detail/CVE-2025-38500){: external}, [CVE-2025-38684](https://nvd.nist.gov/vuln/detail/CVE-2025-38684){: external}, [RHSA-2025:15429](https://access.redhat.com/errata/RHSA-2025:15429){: external}, [CVE-2025-37803](https://nvd.nist.gov/vuln/detail/CVE-2025-37803){: external}, [CVE-2025-38392](https://nvd.nist.gov/vuln/detail/CVE-2025-38392){: external}, [CVE-2025-39825](https://nvd.nist.gov/vuln/detail/CVE-2025-39825){: external}, [RHSA-2025:15661](https://access.redhat.com/errata/RHSA-2025:15661){: external}, [CVE-2025-22097](https://nvd.nist.gov/vuln/detail/CVE-2025-22097){: external}, [CVE-2025-38332](https://nvd.nist.gov/vuln/detail/CVE-2025-38332){: external}, [CVE-2025-38352](https://nvd.nist.gov/vuln/detail/CVE-2025-38352){: external}, [CVE-2025-38449](https://nvd.nist.gov/vuln/detail/CVE-2025-38449){: external}, [RHSA-2025:7423](https://access.redhat.com/errata/RHSA-2025:7423){: external}, [CVE-2024-58005](https://nvd.nist.gov/vuln/detail/CVE-2024-58005){: external}, [CVE-2024-58007](https://nvd.nist.gov/vuln/detail/CVE-2024-58007){: external}, [CVE-2024-58069](https://nvd.nist.gov/vuln/detail/CVE-2024-58069){: external}, [CVE-2025-21633](https://nvd.nist.gov/vuln/detail/CVE-2025-21633){: external}, [CVE-2025-21927](https://nvd.nist.gov/vuln/detail/CVE-2025-21927){: external}, [CVE-2025-21993](https://nvd.nist.gov/vuln/detail/CVE-2025-21993){: external}, [RHSA-2025:7903](https://access.redhat.com/errata/RHSA-2025:7903){: external}, [CVE-2025-21756](https://nvd.nist.gov/vuln/detail/CVE-2025-21756){: external}, [CVE-2025-21966](https://nvd.nist.gov/vuln/detail/CVE-2025-21966){: external}, [CVE-2025-37749](https://nvd.nist.gov/vuln/detail/CVE-2025-37749){: external}, [RHSA-2025:8643](https://access.redhat.com/errata/RHSA-2025:8643){: external}, [CVE-2025-21920](https://nvd.nist.gov/vuln/detail/CVE-2025-21920){: external}, [CVE-2025-21926](https://nvd.nist.gov/vuln/detail/CVE-2025-21926){: external}, [CVE-2025-21997](https://nvd.nist.gov/vuln/detail/CVE-2025-21997){: external}, [CVE-2025-22055](https://nvd.nist.gov/vuln/detail/CVE-2025-22055){: external}, [CVE-2025-37785](https://nvd.nist.gov/vuln/detail/CVE-2025-37785){: external}, [CVE-2025-37943](https://nvd.nist.gov/vuln/detail/CVE-2025-37943){: external}, [RHSA-2025:9080](https://access.redhat.com/errata/RHSA-2025:9080){: external}, [CVE-2025-21961](https://nvd.nist.gov/vuln/detail/CVE-2025-21961){: external}, [CVE-2025-21963](https://nvd.nist.gov/vuln/detail/CVE-2025-21963){: external}, [CVE-2025-21969](https://nvd.nist.gov/vuln/detail/CVE-2025-21969){: external}, [CVE-2025-21979](https://nvd.nist.gov/vuln/detail/CVE-2025-21979){: external}, [CVE-2025-21999](https://nvd.nist.gov/vuln/detail/CVE-2025-21999){: external}, [CVE-2025-22126](https://nvd.nist.gov/vuln/detail/CVE-2025-22126){: external}, [CVE-2025-37750](https://nvd.nist.gov/vuln/detail/CVE-2025-37750){: external}, [RHSA-2025:14130](https://access.redhat.com/errata/RHSA-2025:14130){: external}, [CVE-2025-5914](https://nvd.nist.gov/vuln/detail/CVE-2025-5914){: external}, [RHSA-2025:10699](https://access.redhat.com/errata/RHSA-2025:10699){: external}, [CVE-2025-49794](https://nvd.nist.gov/vuln/detail/CVE-2025-49794){: external}, [CVE-2025-49796](https://nvd.nist.gov/vuln/detail/CVE-2025-49796){: external}, [CVE-2025-6021](https://nvd.nist.gov/vuln/detail/CVE-2025-6021){: external}, [RHSA-2025:12447](https://access.redhat.com/errata/RHSA-2025:12447){: external}, [CVE-2025-7425](https://nvd.nist.gov/vuln/detail/CVE-2025-7425){: external}, [RHSA-2025:15099](https://access.redhat.com/errata/RHSA-2025:15099){: external}, [CVE-2025-6020](https://nvd.nist.gov/vuln/detail/CVE-2025-6020){: external}, [CVE-2025-8941](https://nvd.nist.gov/vuln/detail/CVE-2025-8941){: external}, [RHSA-2025:9526](https://access.redhat.com/errata/RHSA-2025:9526){: external}, [CVE-2025-6020](https://nvd.nist.gov/vuln/detail/CVE-2025-6020){: external}, [RHSA-2025:10136](https://access.redhat.com/errata/RHSA-2025:10136){: external}, [CVE-2024-12718](https://nvd.nist.gov/vuln/detail/CVE-2024-12718){: external}, [CVE-2025-4138](https://nvd.nist.gov/vuln/detail/CVE-2025-4138){: external}, [CVE-2025-4330](https://nvd.nist.gov/vuln/detail/CVE-2025-4330){: external}, [CVE-2025-4435](https://nvd.nist.gov/vuln/detail/CVE-2025-4435){: external}, [CVE-2025-4517](https://nvd.nist.gov/vuln/detail/CVE-2025-4517){: external}, [RHSA-2025:11992](https://access.redhat.com/errata/RHSA-2025:11992){: external}, [CVE-2025-6965](https://nvd.nist.gov/vuln/detail/CVE-2025-6965){: external}, [RHSA-2025:9978](https://access.redhat.com/errata/RHSA-2025:9978){: external}, [CVE-2025-32462](https://nvd.nist.gov/vuln/detail/CVE-2025-32462){: external}, [CVE-2024-36350](https://nvd.nist.gov/vuln/detail/CVE-2024-36350){: external}, [CVE-2024-36357](https://nvd.nist.gov/vuln/detail/CVE-2024-36357){: external}, [RHSA-2025:12876](https://access.redhat.com/errata/RHSA-2025:12876){: external}, [CVE-2022-29458](https://nvd.nist.gov/vuln/detail/CVE-2022-29458){: external}, [RHSA-2025:7440](https://access.redhat.com/errata/RHSA-2025:7440){: external}, [CVE-2023-4752](https://nvd.nist.gov/vuln/detail/CVE-2023-4752){: external}, [CVE-2024-28956](https://nvd.nist.gov/vuln/detail/CVE-2024-28956){: external}, [CVE-2024-43420](https://nvd.nist.gov/vuln/detail/CVE-2024-43420){: external}, [CVE-2024-45332](https://nvd.nist.gov/vuln/detail/CVE-2024-45332){: external}, [CVE-2025-20012](https://nvd.nist.gov/vuln/detail/CVE-2025-20012){: external}, [CVE-2025-20623](https://nvd.nist.gov/vuln/detail/CVE-2025-20623){: external}, [CVE-2025-24495](https://nvd.nist.gov/vuln/detail/CVE-2025-24495){: external}, [RHSA-2025:7444](https://access.redhat.com/errata/RHSA-2025:7444){: external}, [CVE-2024-8176](https://nvd.nist.gov/vuln/detail/CVE-2024-8176){: external}, [RHSA-2025:7409](https://access.redhat.com/errata/RHSA-2025:7409){: external}, [CVE-2024-52005](https://nvd.nist.gov/vuln/detail/CVE-2024-52005){: external}, [RHSA-2025:11140](https://access.redhat.com/errata/RHSA-2025:11140){: external}, [CVE-2024-52533](https://nvd.nist.gov/vuln/detail/CVE-2024-52533){: external}, [CVE-2025-4373](https://nvd.nist.gov/vuln/detail/CVE-2025-4373){: external}, [RHSA-2025:12748](https://access.redhat.com/errata/RHSA-2025:12748){: external}, [CVE-2025-8058](https://nvd.nist.gov/vuln/detail/CVE-2025-8058){: external}, [RHSA-2025:8655](https://access.redhat.com/errata/RHSA-2025:8655){: external}, [CVE-2025-4802](https://nvd.nist.gov/vuln/detail/CVE-2025-4802){: external}, [RHSA-2025:9877](https://access.redhat.com/errata/RHSA-2025:9877){: external}, [CVE-2025-5702](https://nvd.nist.gov/vuln/detail/CVE-2025-5702){: external}, [RHSA-2025:7076](https://access.redhat.com/errata/RHSA-2025:7076){: external}, [CVE-2024-12243](https://nvd.nist.gov/vuln/detail/CVE-2024-12243){: external}, [RHSA-2025:16116](https://access.redhat.com/errata/RHSA-2025:16116){: external}, [CVE-2025-32988](https://nvd.nist.gov/vuln/detail/CVE-2025-32988){: external}, [CVE-2025-32989](https://nvd.nist.gov/vuln/detail/CVE-2025-32989){: external}, [CVE-2025-32990](https://nvd.nist.gov/vuln/detail/CVE-2025-32990){: external}, [CVE-2025-6395](https://nvd.nist.gov/vuln/detail/CVE-2025-6395){: external}, [RHSA-2025:6990](https://access.redhat.com/errata/RHSA-2025:6990){: external}, [CVE-2024-45774](https://nvd.nist.gov/vuln/detail/CVE-2024-45774){: external}, [CVE-2024-45775](https://nvd.nist.gov/vuln/detail/CVE-2024-45775){: external}, [CVE-2024-45776](https://nvd.nist.gov/vuln/detail/CVE-2024-45776){: external}, [CVE-2024-45781](https://nvd.nist.gov/vuln/detail/CVE-2024-45781){: external}, [CVE-2024-45783](https://nvd.nist.gov/vuln/detail/CVE-2024-45783){: external}, [CVE-2025-0622](https://nvd.nist.gov/vuln/detail/CVE-2025-0622){: external}, [CVE-2025-0677](https://nvd.nist.gov/vuln/detail/CVE-2025-0677){: external}, [CVE-2025-0690](https://nvd.nist.gov/vuln/detail/CVE-2025-0690){: external}, [RHSA-2025:17558](https://access.redhat.com/errata/RHSA-2025:17558){: external}, [CVE-2025-48964](https://nvd.nist.gov/vuln/detail/CVE-2025-48964){: external}, [RHSA-2025:9432](https://access.redhat.com/errata/RHSA-2025:9432){: external}, [CVE-2025-47268](https://nvd.nist.gov/vuln/detail/CVE-2025-47268){: external}, [RHSA-2025:10585](https://access.redhat.com/errata/RHSA-2025:10585){: external}, [CVE-2024-23337](https://nvd.nist.gov/vuln/detail/CVE-2024-23337){: external}, [CVE-2025-48060](https://nvd.nist.gov/vuln/detail/CVE-2025-48060){: external}, [RHSA-2025:10837](https://access.redhat.com/errata/RHSA-2025:10837){: external}, [CVE-2025-21991](https://nvd.nist.gov/vuln/detail/CVE-2025-21991){: external}, [RHSA-2025:11861](https://access.redhat.com/errata/RHSA-2025:11861){: external}, [CVE-2024-57980](https://nvd.nist.gov/vuln/detail/CVE-2024-57980){: external}, [CVE-2025-21905](https://nvd.nist.gov/vuln/detail/CVE-2025-21905){: external}, [CVE-2025-22085](https://nvd.nist.gov/vuln/detail/CVE-2025-22085){: external}, [CVE-2025-22091](https://nvd.nist.gov/vuln/detail/CVE-2025-22091){: external}, [CVE-2025-22113](https://nvd.nist.gov/vuln/detail/CVE-2025-22113){: external}, [CVE-2025-22121](https://nvd.nist.gov/vuln/detail/CVE-2025-22121){: external}, [CVE-2025-37797](https://nvd.nist.gov/vuln/detail/CVE-2025-37797){: external}, [CVE-2025-37958](https://nvd.nist.gov/vuln/detail/CVE-2025-37958){: external}, [CVE-2025-38086](https://nvd.nist.gov/vuln/detail/CVE-2025-38086){: external}, [CVE-2025-38110](https://nvd.nist.gov/vuln/detail/CVE-2025-38110){: external}, [RHSA-2025:13602](https://access.redhat.com/errata/RHSA-2025:13602){: external}, [CVE-2025-38079](https://nvd.nist.gov/vuln/detail/CVE-2025-38079){: external}, [CVE-2025-38292](https://nvd.nist.gov/vuln/detail/CVE-2025-38292){: external}, [RHSA-2025:15740](https://access.redhat.com/errata/RHSA-2025:15740){: external}, [CVE-2025-38550](https://nvd.nist.gov/vuln/detail/CVE-2025-38550){: external}, [RHSA-2025:16398](https://access.redhat.com/errata/RHSA-2025:16398){: external}, [CVE-2023-53125](https://nvd.nist.gov/vuln/detail/CVE-2023-53125){: external}, [CVE-2025-37810](https://nvd.nist.gov/vuln/detail/CVE-2025-37810){: external}, [CVE-2025-38498](https://nvd.nist.gov/vuln/detail/CVE-2025-38498){: external}, [CVE-2025-39694](https://nvd.nist.gov/vuln/detail/CVE-2025-39694){: external}, [RHSA-2025:16880](https://access.redhat.com/errata/RHSA-2025:16880){: external}, [CVE-2025-38472](https://nvd.nist.gov/vuln/detail/CVE-2025-38472){: external}, [CVE-2025-38527](https://nvd.nist.gov/vuln/detail/CVE-2025-38527){: external}, [CVE-2025-38718](https://nvd.nist.gov/vuln/detail/CVE-2025-38718){: external}, [CVE-2025-39682](https://nvd.nist.gov/vuln/detail/CVE-2025-39682){: external}, [CVE-2025-39698](https://nvd.nist.gov/vuln/detail/CVE-2025-39698){: external}, [RHSA-2025:17377](https://access.redhat.com/errata/RHSA-2025:17377){: external}, [CVE-2024-50301](https://nvd.nist.gov/vuln/detail/CVE-2024-50301){: external}, [CVE-2025-38351](https://nvd.nist.gov/vuln/detail/CVE-2025-38351){: external}, [CVE-2025-39761](https://nvd.nist.gov/vuln/detail/CVE-2025-39761){: external}, [RHSA-2025:17760](https://access.redhat.com/errata/RHSA-2025:17760){: external}, [CVE-2023-53373](https://nvd.nist.gov/vuln/detail/CVE-2023-53373){: external}, [CVE-2025-38556](https://nvd.nist.gov/vuln/detail/CVE-2025-38556){: external}, [CVE-2025-38614](https://nvd.nist.gov/vuln/detail/CVE-2025-38614){: external}, [CVE-2025-39757](https://nvd.nist.gov/vuln/detail/CVE-2025-39757){: external}, [RHSA-2025:6966](https://access.redhat.com/errata/RHSA-2025:6966){: external}, [CVE-2022-48969](https://nvd.nist.gov/vuln/detail/CVE-2022-48969){: external}, [CVE-2022-48989](https://nvd.nist.gov/vuln/detail/CVE-2022-48989){: external}, [CVE-2022-49006](https://nvd.nist.gov/vuln/detail/CVE-2022-49006){: external}, [CVE-2022-49014](https://nvd.nist.gov/vuln/detail/CVE-2022-49014){: external}, [CVE-2022-49029](https://nvd.nist.gov/vuln/detail/CVE-2022-49029){: external}, [CVE-2022-49778](https://nvd.nist.gov/vuln/detail/CVE-2022-49778){: external}, [CVE-2022-49804](https://nvd.nist.gov/vuln/detail/CVE-2022-49804){: external}, [CVE-2022-49815](https://nvd.nist.gov/vuln/detail/CVE-2022-49815){: external}, [CVE-2022-50112](https://nvd.nist.gov/vuln/detail/CVE-2022-50112){: external}, [CVE-2022-50159](https://nvd.nist.gov/vuln/detail/CVE-2022-50159){: external}, [CVE-2022-50214](https://nvd.nist.gov/vuln/detail/CVE-2022-50214){: external}, [CVE-2022-50511](https://nvd.nist.gov/vuln/detail/CVE-2022-50511){: external}, [CVE-2023-52672](https://nvd.nist.gov/vuln/detail/CVE-2023-52672){: external}, [CVE-2023-52917](https://nvd.nist.gov/vuln/detail/CVE-2023-52917){: external}, [CVE-2023-53066](https://nvd.nist.gov/vuln/detail/CVE-2023-53066){: external}, [CVE-2023-53117](https://nvd.nist.gov/vuln/detail/CVE-2023-53117){: external}, [CVE-2023-53196](https://nvd.nist.gov/vuln/detail/CVE-2023-53196){: external}, [CVE-2023-53260](https://nvd.nist.gov/vuln/detail/CVE-2023-53260){: external}, [CVE-2023-53261](https://nvd.nist.gov/vuln/detail/CVE-2023-53261){: external}, [CVE-2023-53595](https://nvd.nist.gov/vuln/detail/CVE-2023-53595){: external}, [CVE-2024-27008](https://nvd.nist.gov/vuln/detail/CVE-2024-27008){: external}, [CVE-2024-27398](https://nvd.nist.gov/vuln/detail/CVE-2024-27398){: external}, [CVE-2024-35891](https://nvd.nist.gov/vuln/detail/CVE-2024-35891){: external}, [CVE-2024-35933](https://nvd.nist.gov/vuln/detail/CVE-2024-35933){: external}, [CVE-2024-35934](https://nvd.nist.gov/vuln/detail/CVE-2024-35934){: external}, [CVE-2024-35963](https://nvd.nist.gov/vuln/detail/CVE-2024-35963){: external}, [CVE-2024-35964](https://nvd.nist.gov/vuln/detail/CVE-2024-35964){: external}, [CVE-2024-35965](https://nvd.nist.gov/vuln/detail/CVE-2024-35965){: external}, [CVE-2024-35966](https://nvd.nist.gov/vuln/detail/CVE-2024-35966){: external}, [CVE-2024-35967](https://nvd.nist.gov/vuln/detail/CVE-2024-35967){: external}, [CVE-2024-35978](https://nvd.nist.gov/vuln/detail/CVE-2024-35978){: external}, [CVE-2024-36011](https://nvd.nist.gov/vuln/detail/CVE-2024-36011){: external}, [CVE-2024-36012](https://nvd.nist.gov/vuln/detail/CVE-2024-36012){: external}, [CVE-2024-36013](https://nvd.nist.gov/vuln/detail/CVE-2024-36013){: external}, [CVE-2024-36880](https://nvd.nist.gov/vuln/detail/CVE-2024-36880){: external}, [CVE-2024-36968](https://nvd.nist.gov/vuln/detail/CVE-2024-36968){: external}, [CVE-2024-38541](https://nvd.nist.gov/vuln/detail/CVE-2024-38541){: external}, [CVE-2024-39500](https://nvd.nist.gov/vuln/detail/CVE-2024-39500){: external}, [CVE-2024-40956](https://nvd.nist.gov/vuln/detail/CVE-2024-40956){: external}, [CVE-2024-41010](https://nvd.nist.gov/vuln/detail/CVE-2024-41010){: external}, [CVE-2024-41062](https://nvd.nist.gov/vuln/detail/CVE-2024-41062){: external}, [CVE-2024-42094](https://nvd.nist.gov/vuln/detail/CVE-2024-42094){: external}, [CVE-2024-42133](https://nvd.nist.gov/vuln/detail/CVE-2024-42133){: external}, [CVE-2024-42253](https://nvd.nist.gov/vuln/detail/CVE-2024-42253){: external}, [CVE-2024-42265](https://nvd.nist.gov/vuln/detail/CVE-2024-42265){: external}, [CVE-2024-42278](https://nvd.nist.gov/vuln/detail/CVE-2024-42278){: external}, [CVE-2024-42291](https://nvd.nist.gov/vuln/detail/CVE-2024-42291){: external}, [CVE-2024-42294](https://nvd.nist.gov/vuln/detail/CVE-2024-42294){: external}, [CVE-2024-42302](https://nvd.nist.gov/vuln/detail/CVE-2024-42302){: external}, [CVE-2024-42304](https://nvd.nist.gov/vuln/detail/CVE-2024-42304){: external}, [CVE-2024-42305](https://nvd.nist.gov/vuln/detail/CVE-2024-42305){: external}, [CVE-2024-42312](https://nvd.nist.gov/vuln/detail/CVE-2024-42312){: external}, [CVE-2024-42315](https://nvd.nist.gov/vuln/detail/CVE-2024-42315){: external}, [CVE-2024-42316](https://nvd.nist.gov/vuln/detail/CVE-2024-42316){: external}, [CVE-2024-42321](https://nvd.nist.gov/vuln/detail/CVE-2024-42321){: external}, [CVE-2024-43820](https://nvd.nist.gov/vuln/detail/CVE-2024-43820){: external}, [CVE-2024-43821](https://nvd.nist.gov/vuln/detail/CVE-2024-43821){: external}, [CVE-2024-43823](https://nvd.nist.gov/vuln/detail/CVE-2024-43823){: external}, [CVE-2024-43828](https://nvd.nist.gov/vuln/detail/CVE-2024-43828){: external}, [CVE-2024-43834](https://nvd.nist.gov/vuln/detail/CVE-2024-43834){: external}, [CVE-2024-43846](https://nvd.nist.gov/vuln/detail/CVE-2024-43846){: external}, [CVE-2024-43853](https://nvd.nist.gov/vuln/detail/CVE-2024-43853){: external}, [CVE-2024-43871](https://nvd.nist.gov/vuln/detail/CVE-2024-43871){: external}, [CVE-2024-43873](https://nvd.nist.gov/vuln/detail/CVE-2024-43873){: external}, [CVE-2024-43882](https://nvd.nist.gov/vuln/detail/CVE-2024-43882){: external}, [CVE-2024-43884](https://nvd.nist.gov/vuln/detail/CVE-2024-43884){: external}, [CVE-2024-43889](https://nvd.nist.gov/vuln/detail/CVE-2024-43889){: external}, [CVE-2024-43898](https://nvd.nist.gov/vuln/detail/CVE-2024-43898){: external}, [CVE-2024-43910](https://nvd.nist.gov/vuln/detail/CVE-2024-43910){: external}, [CVE-2024-43914](https://nvd.nist.gov/vuln/detail/CVE-2024-43914){: external}, [CVE-2024-44931](https://nvd.nist.gov/vuln/detail/CVE-2024-44931){: external}, [CVE-2024-44932](https://nvd.nist.gov/vuln/detail/CVE-2024-44932){: external}, [CVE-2024-44934](https://nvd.nist.gov/vuln/detail/CVE-2024-44934){: external}, [CVE-2024-44952](https://nvd.nist.gov/vuln/detail/CVE-2024-44952){: external}, [CVE-2024-44958](https://nvd.nist.gov/vuln/detail/CVE-2024-44958){: external}, [CVE-2024-44964](https://nvd.nist.gov/vuln/detail/CVE-2024-44964){: external}, [CVE-2024-44975](https://nvd.nist.gov/vuln/detail/CVE-2024-44975){: external}, [CVE-2024-44987](https://nvd.nist.gov/vuln/detail/CVE-2024-44987){: external}, [CVE-2024-44989](https://nvd.nist.gov/vuln/detail/CVE-2024-44989){: external}, [CVE-2024-45000](https://nvd.nist.gov/vuln/detail/CVE-2024-45000){: external}, [CVE-2024-45009](https://nvd.nist.gov/vuln/detail/CVE-2024-45009){: external}, [CVE-2024-45010](https://nvd.nist.gov/vuln/detail/CVE-2024-45010){: external}, [CVE-2024-45016](https://nvd.nist.gov/vuln/detail/CVE-2024-45016){: external}, [CVE-2024-45022](https://nvd.nist.gov/vuln/detail/CVE-2024-45022){: external}, [CVE-2024-46673](https://nvd.nist.gov/vuln/detail/CVE-2024-46673){: external}, [CVE-2024-46675](https://nvd.nist.gov/vuln/detail/CVE-2024-46675){: external}, [CVE-2024-46711](https://nvd.nist.gov/vuln/detail/CVE-2024-46711){: external}, [CVE-2024-46722](https://nvd.nist.gov/vuln/detail/CVE-2024-46722){: external}, [CVE-2024-46723](https://nvd.nist.gov/vuln/detail/CVE-2024-46723){: external}, [CVE-2024-46724](https://nvd.nist.gov/vuln/detail/CVE-2024-46724){: external}, [CVE-2024-46725](https://nvd.nist.gov/vuln/detail/CVE-2024-46725){: external}, [CVE-2024-46743](https://nvd.nist.gov/vuln/detail/CVE-2024-46743){: external}, [CVE-2024-46745](https://nvd.nist.gov/vuln/detail/CVE-2024-46745){: external}, [CVE-2024-46747](https://nvd.nist.gov/vuln/detail/CVE-2024-46747){: external}, [CVE-2024-46750](https://nvd.nist.gov/vuln/detail/CVE-2024-46750){: external}, [CVE-2024-46754](https://nvd.nist.gov/vuln/detail/CVE-2024-46754){: external}, [CVE-2024-46756](https://nvd.nist.gov/vuln/detail/CVE-2024-46756){: external}, [CVE-2024-46758](https://nvd.nist.gov/vuln/detail/CVE-2024-46758){: external}, [CVE-2024-46759](https://nvd.nist.gov/vuln/detail/CVE-2024-46759){: external}, [CVE-2024-46761](https://nvd.nist.gov/vuln/detail/CVE-2024-46761){: external}, [CVE-2024-46783](https://nvd.nist.gov/vuln/detail/CVE-2024-46783){: external}, [CVE-2024-46786](https://nvd.nist.gov/vuln/detail/CVE-2024-46786){: external}, [CVE-2024-46787](https://nvd.nist.gov/vuln/detail/CVE-2024-46787){: external}, [CVE-2024-46800](https://nvd.nist.gov/vuln/detail/CVE-2024-46800){: external}, [CVE-2024-46805](https://nvd.nist.gov/vuln/detail/CVE-2024-46805){: external}, [CVE-2024-46806](https://nvd.nist.gov/vuln/detail/CVE-2024-46806){: external}, [CVE-2024-46807](https://nvd.nist.gov/vuln/detail/CVE-2024-46807){: external}, [CVE-2024-46819](https://nvd.nist.gov/vuln/detail/CVE-2024-46819){: external}, [CVE-2024-46820](https://nvd.nist.gov/vuln/detail/CVE-2024-46820){: external}, [CVE-2024-46822](https://nvd.nist.gov/vuln/detail/CVE-2024-46822){: external}, [CVE-2024-46828](https://nvd.nist.gov/vuln/detail/CVE-2024-46828){: external}, [CVE-2024-46835](https://nvd.nist.gov/vuln/detail/CVE-2024-46835){: external}, [CVE-2024-46839](https://nvd.nist.gov/vuln/detail/CVE-2024-46839){: external}, [CVE-2024-46853](https://nvd.nist.gov/vuln/detail/CVE-2024-46853){: external}, [CVE-2024-46864](https://nvd.nist.gov/vuln/detail/CVE-2024-46864){: external}, [CVE-2024-46871](https://nvd.nist.gov/vuln/detail/CVE-2024-46871){: external}, [CVE-2024-47141](https://nvd.nist.gov/vuln/detail/CVE-2024-47141){: external}, [CVE-2024-47660](https://nvd.nist.gov/vuln/detail/CVE-2024-47660){: external}, [CVE-2024-47668](https://nvd.nist.gov/vuln/detail/CVE-2024-47668){: external}, [CVE-2024-47678](https://nvd.nist.gov/vuln/detail/CVE-2024-47678){: external}, [CVE-2024-47685](https://nvd.nist.gov/vuln/detail/CVE-2024-47685){: external}, [CVE-2024-47687](https://nvd.nist.gov/vuln/detail/CVE-2024-47687){: external}, [CVE-2024-47692](https://nvd.nist.gov/vuln/detail/CVE-2024-47692){: external}, [CVE-2024-47700](https://nvd.nist.gov/vuln/detail/CVE-2024-47700){: external}, [CVE-2024-47703](https://nvd.nist.gov/vuln/detail/CVE-2024-47703){: external}, [CVE-2024-47705](https://nvd.nist.gov/vuln/detail/CVE-2024-47705){: external}, [CVE-2024-47706](https://nvd.nist.gov/vuln/detail/CVE-2024-47706){: external}, [CVE-2024-47710](https://nvd.nist.gov/vuln/detail/CVE-2024-47710){: external}, [CVE-2024-47713](https://nvd.nist.gov/vuln/detail/CVE-2024-47713){: external}, [CVE-2024-47715](https://nvd.nist.gov/vuln/detail/CVE-2024-47715){: external}, [CVE-2024-47718](https://nvd.nist.gov/vuln/detail/CVE-2024-47718){: external}, [CVE-2024-47719](https://nvd.nist.gov/vuln/detail/CVE-2024-47719){: external}, [CVE-2024-47737](https://nvd.nist.gov/vuln/detail/CVE-2024-47737){: external}, [CVE-2024-47738](https://nvd.nist.gov/vuln/detail/CVE-2024-47738){: external}, [CVE-2024-47739](https://nvd.nist.gov/vuln/detail/CVE-2024-47739){: external}, [CVE-2024-47745](https://nvd.nist.gov/vuln/detail/CVE-2024-47745){: external}, [CVE-2024-47748](https://nvd.nist.gov/vuln/detail/CVE-2024-47748){: external}, [CVE-2024-48873](https://nvd.nist.gov/vuln/detail/CVE-2024-48873){: external}, [CVE-2024-49569](https://nvd.nist.gov/vuln/detail/CVE-2024-49569){: external}, [CVE-2024-49851](https://nvd.nist.gov/vuln/detail/CVE-2024-49851){: external}, [CVE-2024-49856](https://nvd.nist.gov/vuln/detail/CVE-2024-49856){: external}, [CVE-2024-49860](https://nvd.nist.gov/vuln/detail/CVE-2024-49860){: external}, [CVE-2024-49862](https://nvd.nist.gov/vuln/detail/CVE-2024-49862){: external}, [CVE-2024-49870](https://nvd.nist.gov/vuln/detail/CVE-2024-49870){: external}, [CVE-2024-49875](https://nvd.nist.gov/vuln/detail/CVE-2024-49875){: external}, [CVE-2024-49878](https://nvd.nist.gov/vuln/detail/CVE-2024-49878){: external}, [CVE-2024-49881](https://nvd.nist.gov/vuln/detail/CVE-2024-49881){: external}, [CVE-2024-49882](https://nvd.nist.gov/vuln/detail/CVE-2024-49882){: external}, [CVE-2024-49883](https://nvd.nist.gov/vuln/detail/CVE-2024-49883){: external}, [CVE-2024-49884](https://nvd.nist.gov/vuln/detail/CVE-2024-49884){: external}, [CVE-2024-49885](https://nvd.nist.gov/vuln/detail/CVE-2024-49885){: external}, [CVE-2024-49886](https://nvd.nist.gov/vuln/detail/CVE-2024-49886){: external}, [CVE-2024-49889](https://nvd.nist.gov/vuln/detail/CVE-2024-49889){: external}, [CVE-2024-49904](https://nvd.nist.gov/vuln/detail/CVE-2024-49904){: external}, [CVE-2024-49927](https://nvd.nist.gov/vuln/detail/CVE-2024-49927){: external}, [CVE-2024-49928](https://nvd.nist.gov/vuln/detail/CVE-2024-49928){: external}, [CVE-2024-49929](https://nvd.nist.gov/vuln/detail/CVE-2024-49929){: external}, [CVE-2024-49930](https://nvd.nist.gov/vuln/detail/CVE-2024-49930){: external}, [CVE-2024-49933](https://nvd.nist.gov/vuln/detail/CVE-2024-49933){: external}, [CVE-2024-49934](https://nvd.nist.gov/vuln/detail/CVE-2024-49934){: external}, [CVE-2024-49935](https://nvd.nist.gov/vuln/detail/CVE-2024-49935){: external}, [CVE-2024-49937](https://nvd.nist.gov/vuln/detail/CVE-2024-49937){: external}, [CVE-2024-49938](https://nvd.nist.gov/vuln/detail/CVE-2024-49938){: external}, [CVE-2024-49939](https://nvd.nist.gov/vuln/detail/CVE-2024-49939){: external}, [CVE-2024-49946](https://nvd.nist.gov/vuln/detail/CVE-2024-49946){: external}, [CVE-2024-49948](https://nvd.nist.gov/vuln/detail/CVE-2024-49948){: external}, [CVE-2024-49950](https://nvd.nist.gov/vuln/detail/CVE-2024-49950){: external}, [CVE-2024-49951](https://nvd.nist.gov/vuln/detail/CVE-2024-49951){: external}, [CVE-2024-49954](https://nvd.nist.gov/vuln/detail/CVE-2024-49954){: external}, [CVE-2024-49959](https://nvd.nist.gov/vuln/detail/CVE-2024-49959){: external}, [CVE-2024-49960](https://nvd.nist.gov/vuln/detail/CVE-2024-49960){: external}, [CVE-2024-49962](https://nvd.nist.gov/vuln/detail/CVE-2024-49962){: external}, [CVE-2024-49967](https://nvd.nist.gov/vuln/detail/CVE-2024-49967){: external}, [CVE-2024-49968](https://nvd.nist.gov/vuln/detail/CVE-2024-49968){: external}, [CVE-2024-49971](https://nvd.nist.gov/vuln/detail/CVE-2024-49971){: external}, [CVE-2024-49973](https://nvd.nist.gov/vuln/detail/CVE-2024-49973){: external}, [CVE-2024-49974](https://nvd.nist.gov/vuln/detail/CVE-2024-49974){: external}, [CVE-2024-49975](https://nvd.nist.gov/vuln/detail/CVE-2024-49975){: external}, [CVE-2024-49977](https://nvd.nist.gov/vuln/detail/CVE-2024-49977){: external}, [CVE-2024-49983](https://nvd.nist.gov/vuln/detail/CVE-2024-49983){: external}, [CVE-2024-49991](https://nvd.nist.gov/vuln/detail/CVE-2024-49991){: external}, [CVE-2024-49993](https://nvd.nist.gov/vuln/detail/CVE-2024-49993){: external}, [CVE-2024-49994](https://nvd.nist.gov/vuln/detail/CVE-2024-49994){: external}, [CVE-2024-49995](https://nvd.nist.gov/vuln/detail/CVE-2024-49995){: external}, [CVE-2024-49999](https://nvd.nist.gov/vuln/detail/CVE-2024-49999){: external}, [CVE-2024-50002](https://nvd.nist.gov/vuln/detail/CVE-2024-50002){: external}, [CVE-2024-50006](https://nvd.nist.gov/vuln/detail/CVE-2024-50006){: external}, [CVE-2024-50008](https://nvd.nist.gov/vuln/detail/CVE-2024-50008){: external}, [CVE-2024-50009](https://nvd.nist.gov/vuln/detail/CVE-2024-50009){: external}, [CVE-2024-50013](https://nvd.nist.gov/vuln/detail/CVE-2024-50013){: external}, [CVE-2024-50014](https://nvd.nist.gov/vuln/detail/CVE-2024-50014){: external}, [CVE-2024-50015](https://nvd.nist.gov/vuln/detail/CVE-2024-50015){: external}, [CVE-2024-50018](https://nvd.nist.gov/vuln/detail/CVE-2024-50018){: external}, [CVE-2024-50019](https://nvd.nist.gov/vuln/detail/CVE-2024-50019){: external}, [CVE-2024-50022](https://nvd.nist.gov/vuln/detail/CVE-2024-50022){: external}, [CVE-2024-50023](https://nvd.nist.gov/vuln/detail/CVE-2024-50023){: external}, [CVE-2024-50024](https://nvd.nist.gov/vuln/detail/CVE-2024-50024){: external}, [CVE-2024-50027](https://nvd.nist.gov/vuln/detail/CVE-2024-50027){: external}, [CVE-2024-50028](https://nvd.nist.gov/vuln/detail/CVE-2024-50028){: external}, [CVE-2024-50029](https://nvd.nist.gov/vuln/detail/CVE-2024-50029){: external}, [CVE-2024-50033](https://nvd.nist.gov/vuln/detail/CVE-2024-50033){: external}, [CVE-2024-50035](https://nvd.nist.gov/vuln/detail/CVE-2024-50035){: external}, [CVE-2024-50038](https://nvd.nist.gov/vuln/detail/CVE-2024-50038){: external}, [CVE-2024-50039](https://nvd.nist.gov/vuln/detail/CVE-2024-50039){: external}, [CVE-2024-50044](https://nvd.nist.gov/vuln/detail/CVE-2024-50044){: external}, [CVE-2024-50046](https://nvd.nist.gov/vuln/detail/CVE-2024-50046){: external}, [CVE-2024-50047](https://nvd.nist.gov/vuln/detail/CVE-2024-50047){: external}, [CVE-2024-50055](https://nvd.nist.gov/vuln/detail/CVE-2024-50055){: external}, [CVE-2024-50057](https://nvd.nist.gov/vuln/detail/CVE-2024-50057){: external}, [CVE-2024-50058](https://nvd.nist.gov/vuln/detail/CVE-2024-50058){: external}, [CVE-2024-50064](https://nvd.nist.gov/vuln/detail/CVE-2024-50064){: external}, [CVE-2024-50067](https://nvd.nist.gov/vuln/detail/CVE-2024-50067){: external}, [CVE-2024-50073](https://nvd.nist.gov/vuln/detail/CVE-2024-50073){: external}, [CVE-2024-50074](https://nvd.nist.gov/vuln/detail/CVE-2024-50074){: external}, [CVE-2024-50075](https://nvd.nist.gov/vuln/detail/CVE-2024-50075){: external}, [CVE-2024-50077](https://nvd.nist.gov/vuln/detail/CVE-2024-50077){: external}, [CVE-2024-50078](https://nvd.nist.gov/vuln/detail/CVE-2024-50078){: external}, [CVE-2024-50081](https://nvd.nist.gov/vuln/detail/CVE-2024-50081){: external}, [CVE-2024-50082](https://nvd.nist.gov/vuln/detail/CVE-2024-50082){: external}, [CVE-2024-50093](https://nvd.nist.gov/vuln/detail/CVE-2024-50093){: external}, [CVE-2024-50101](https://nvd.nist.gov/vuln/detail/CVE-2024-50101){: external}, [CVE-2024-50102](https://nvd.nist.gov/vuln/detail/CVE-2024-50102){: external}, [CVE-2024-50106](https://nvd.nist.gov/vuln/detail/CVE-2024-50106){: external}, [CVE-2024-50107](https://nvd.nist.gov/vuln/detail/CVE-2024-50107){: external}, [CVE-2024-50109](https://nvd.nist.gov/vuln/detail/CVE-2024-50109){: external}, [CVE-2024-50117](https://nvd.nist.gov/vuln/detail/CVE-2024-50117){: external}, [CVE-2024-50120](https://nvd.nist.gov/vuln/detail/CVE-2024-50120){: external}, [CVE-2024-50121](https://nvd.nist.gov/vuln/detail/CVE-2024-50121){: external}, [CVE-2024-50126](https://nvd.nist.gov/vuln/detail/CVE-2024-50126){: external}, [CVE-2024-50127](https://nvd.nist.gov/vuln/detail/CVE-2024-50127){: external}, [CVE-2024-50128](https://nvd.nist.gov/vuln/detail/CVE-2024-50128){: external}, [CVE-2024-50130](https://nvd.nist.gov/vuln/detail/CVE-2024-50130){: external}, [CVE-2024-50141](https://nvd.nist.gov/vuln/detail/CVE-2024-50141){: external}, [CVE-2024-50143](https://nvd.nist.gov/vuln/detail/CVE-2024-50143){: external}, [CVE-2024-50150](https://nvd.nist.gov/vuln/detail/CVE-2024-50150){: external}, [CVE-2024-50151](https://nvd.nist.gov/vuln/detail/CVE-2024-50151){: external}, [CVE-2024-50152](https://nvd.nist.gov/vuln/detail/CVE-2024-50152){: external}, [CVE-2024-50153](https://nvd.nist.gov/vuln/detail/CVE-2024-50153){: external}, [CVE-2024-50162](https://nvd.nist.gov/vuln/detail/CVE-2024-50162){: external}, [CVE-2024-50163](https://nvd.nist.gov/vuln/detail/CVE-2024-50163){: external}, [CVE-2024-50169](https://nvd.nist.gov/vuln/detail/CVE-2024-50169){: external}, [CVE-2024-50182](https://nvd.nist.gov/vuln/detail/CVE-2024-50182){: external}, [CVE-2024-50186](https://nvd.nist.gov/vuln/detail/CVE-2024-50186){: external}, [CVE-2024-50189](https://nvd.nist.gov/vuln/detail/CVE-2024-50189){: external}, [CVE-2024-50191](https://nvd.nist.gov/vuln/detail/CVE-2024-50191){: external}, [CVE-2024-50197](https://nvd.nist.gov/vuln/detail/CVE-2024-50197){: external}, [CVE-2024-50199](https://nvd.nist.gov/vuln/detail/CVE-2024-50199){: external}, [CVE-2024-50200](https://nvd.nist.gov/vuln/detail/CVE-2024-50200){: external}, [CVE-2024-50201](https://nvd.nist.gov/vuln/detail/CVE-2024-50201){: external}, [CVE-2024-50215](https://nvd.nist.gov/vuln/detail/CVE-2024-50215){: external}, [CVE-2024-50216](https://nvd.nist.gov/vuln/detail/CVE-2024-50216){: external}, [CVE-2024-50219](https://nvd.nist.gov/vuln/detail/CVE-2024-50219){: external}, [CVE-2024-50228](https://nvd.nist.gov/vuln/detail/CVE-2024-50228){: external}, [CVE-2024-50235](https://nvd.nist.gov/vuln/detail/CVE-2024-50235){: external}, [CVE-2024-50236](https://nvd.nist.gov/vuln/detail/CVE-2024-50236){: external}, [CVE-2024-50237](https://nvd.nist.gov/vuln/detail/CVE-2024-50237){: external}, [CVE-2024-50256](https://nvd.nist.gov/vuln/detail/CVE-2024-50256){: external}, [CVE-2024-50261](https://nvd.nist.gov/vuln/detail/CVE-2024-50261){: external}, [CVE-2024-50271](https://nvd.nist.gov/vuln/detail/CVE-2024-50271){: external}, [CVE-2024-50272](https://nvd.nist.gov/vuln/detail/CVE-2024-50272){: external}, [CVE-2024-50278](https://nvd.nist.gov/vuln/detail/CVE-2024-50278){: external}, [CVE-2024-50282](https://nvd.nist.gov/vuln/detail/CVE-2024-50282){: external}, [CVE-2024-50299](https://nvd.nist.gov/vuln/detail/CVE-2024-50299){: external}, [CVE-2024-50304](https://nvd.nist.gov/vuln/detail/CVE-2024-50304){: external}, [CVE-2024-53042](https://nvd.nist.gov/vuln/detail/CVE-2024-53042){: external}, [CVE-2024-53044](https://nvd.nist.gov/vuln/detail/CVE-2024-53044){: external}, [CVE-2024-53047](https://nvd.nist.gov/vuln/detail/CVE-2024-53047){: external}, [CVE-2024-53050](https://nvd.nist.gov/vuln/detail/CVE-2024-53050){: external}, [CVE-2024-53051](https://nvd.nist.gov/vuln/detail/CVE-2024-53051){: external}, [CVE-2024-53055](https://nvd.nist.gov/vuln/detail/CVE-2024-53055){: external}, [CVE-2024-53057](https://nvd.nist.gov/vuln/detail/CVE-2024-53057){: external}, [CVE-2024-53059](https://nvd.nist.gov/vuln/detail/CVE-2024-53059){: external}, [CVE-2024-53060](https://nvd.nist.gov/vuln/detail/CVE-2024-53060){: external}, [CVE-2024-53070](https://nvd.nist.gov/vuln/detail/CVE-2024-53070){: external}, [CVE-2024-53072](https://nvd.nist.gov/vuln/detail/CVE-2024-53072){: external}, [CVE-2024-53074](https://nvd.nist.gov/vuln/detail/CVE-2024-53074){: external}, [CVE-2024-53082](https://nvd.nist.gov/vuln/detail/CVE-2024-53082){: external}, [CVE-2024-53085](https://nvd.nist.gov/vuln/detail/CVE-2024-53085){: external}, [CVE-2024-53091](https://nvd.nist.gov/vuln/detail/CVE-2024-53091){: external}, [CVE-2024-53093](https://nvd.nist.gov/vuln/detail/CVE-2024-53093){: external}, [CVE-2024-53095](https://nvd.nist.gov/vuln/detail/CVE-2024-53095){: external}, [CVE-2024-53096](https://nvd.nist.gov/vuln/detail/CVE-2024-53096){: external}, [CVE-2024-53097](https://nvd.nist.gov/vuln/detail/CVE-2024-53097){: external}, [CVE-2024-53103](https://nvd.nist.gov/vuln/detail/CVE-2024-53103){: external}, [CVE-2024-53105](https://nvd.nist.gov/vuln/detail/CVE-2024-53105){: external}, [CVE-2024-53110](https://nvd.nist.gov/vuln/detail/CVE-2024-53110){: external}, [CVE-2024-53117](https://nvd.nist.gov/vuln/detail/CVE-2024-53117){: external}, [CVE-2024-53118](https://nvd.nist.gov/vuln/detail/CVE-2024-53118){: external}, [CVE-2024-53120](https://nvd.nist.gov/vuln/detail/CVE-2024-53120){: external}, [CVE-2024-53121](https://nvd.nist.gov/vuln/detail/CVE-2024-53121){: external}, [CVE-2024-53123](https://nvd.nist.gov/vuln/detail/CVE-2024-53123){: external}, [CVE-2024-53124](https://nvd.nist.gov/vuln/detail/CVE-2024-53124){: external}, [CVE-2024-53134](https://nvd.nist.gov/vuln/detail/CVE-2024-53134){: external}, [CVE-2024-53136](https://nvd.nist.gov/vuln/detail/CVE-2024-53136){: external}, [CVE-2024-53141](https://nvd.nist.gov/vuln/detail/CVE-2024-53141){: external}, [CVE-2024-53142](https://nvd.nist.gov/vuln/detail/CVE-2024-53142){: external}, [CVE-2024-53146](https://nvd.nist.gov/vuln/detail/CVE-2024-53146){: external}, [CVE-2024-53152](https://nvd.nist.gov/vuln/detail/CVE-2024-53152){: external}, [CVE-2024-53156](https://nvd.nist.gov/vuln/detail/CVE-2024-53156){: external}, [CVE-2024-53160](https://nvd.nist.gov/vuln/detail/CVE-2024-53160){: external}, [CVE-2024-53161](https://nvd.nist.gov/vuln/detail/CVE-2024-53161){: external}, [CVE-2024-53164](https://nvd.nist.gov/vuln/detail/CVE-2024-53164){: external}, [CVE-2024-53166](https://nvd.nist.gov/vuln/detail/CVE-2024-53166){: external}, [CVE-2024-53173](https://nvd.nist.gov/vuln/detail/CVE-2024-53173){: external}, [CVE-2024-53174](https://nvd.nist.gov/vuln/detail/CVE-2024-53174){: external}, [CVE-2024-53176](https://nvd.nist.gov/vuln/detail/CVE-2024-53176){: external}, [CVE-2024-53190](https://nvd.nist.gov/vuln/detail/CVE-2024-53190){: external}, [CVE-2024-53194](https://nvd.nist.gov/vuln/detail/CVE-2024-53194){: external}, [CVE-2024-53203](https://nvd.nist.gov/vuln/detail/CVE-2024-53203){: external}, [CVE-2024-53208](https://nvd.nist.gov/vuln/detail/CVE-2024-53208){: external}, [CVE-2024-53213](https://nvd.nist.gov/vuln/detail/CVE-2024-53213){: external}, [CVE-2024-53222](https://nvd.nist.gov/vuln/detail/CVE-2024-53222){: external}, [CVE-2024-53224](https://nvd.nist.gov/vuln/detail/CVE-2024-53224){: external}, [CVE-2024-53232](https://nvd.nist.gov/vuln/detail/CVE-2024-53232){: external}, [CVE-2024-53237](https://nvd.nist.gov/vuln/detail/CVE-2024-53237){: external}, [CVE-2024-53681](https://nvd.nist.gov/vuln/detail/CVE-2024-53681){: external}, [CVE-2024-54460](https://nvd.nist.gov/vuln/detail/CVE-2024-54460){: external}, [CVE-2024-54680](https://nvd.nist.gov/vuln/detail/CVE-2024-54680){: external}, [CVE-2024-56535](https://nvd.nist.gov/vuln/detail/CVE-2024-56535){: external}, [CVE-2024-56544](https://nvd.nist.gov/vuln/detail/CVE-2024-56544){: external}, [CVE-2024-56551](https://nvd.nist.gov/vuln/detail/CVE-2024-56551){: external}, [CVE-2024-56558](https://nvd.nist.gov/vuln/detail/CVE-2024-56558){: external}, [CVE-2024-56562](https://nvd.nist.gov/vuln/detail/CVE-2024-56562){: external}, [CVE-2024-56566](https://nvd.nist.gov/vuln/detail/CVE-2024-56566){: external}, [CVE-2024-56570](https://nvd.nist.gov/vuln/detail/CVE-2024-56570){: external}, [CVE-2024-56590](https://nvd.nist.gov/vuln/detail/CVE-2024-56590){: external}, [CVE-2024-56591](https://nvd.nist.gov/vuln/detail/CVE-2024-56591){: external}, [CVE-2024-56600](https://nvd.nist.gov/vuln/detail/CVE-2024-56600){: external}, [CVE-2024-56601](https://nvd.nist.gov/vuln/detail/CVE-2024-56601){: external}, [CVE-2024-56602](https://nvd.nist.gov/vuln/detail/CVE-2024-56602){: external}, [CVE-2024-56604](https://nvd.nist.gov/vuln/detail/CVE-2024-56604){: external}, [CVE-2024-56605](https://nvd.nist.gov/vuln/detail/CVE-2024-56605){: external}, [CVE-2024-56611](https://nvd.nist.gov/vuln/detail/CVE-2024-56611){: external}, [CVE-2024-56614](https://nvd.nist.gov/vuln/detail/CVE-2024-56614){: external}, [CVE-2024-56616](https://nvd.nist.gov/vuln/detail/CVE-2024-56616){: external}, [CVE-2024-56623](https://nvd.nist.gov/vuln/detail/CVE-2024-56623){: external}, [CVE-2024-56631](https://nvd.nist.gov/vuln/detail/CVE-2024-56631){: external}, [CVE-2024-56642](https://nvd.nist.gov/vuln/detail/CVE-2024-56642){: external}, [CVE-2024-56644](https://nvd.nist.gov/vuln/detail/CVE-2024-56644){: external}, [CVE-2024-56647](https://nvd.nist.gov/vuln/detail/CVE-2024-56647){: external}, [CVE-2024-56653](https://nvd.nist.gov/vuln/detail/CVE-2024-56653){: external}, [CVE-2024-56654](https://nvd.nist.gov/vuln/detail/CVE-2024-56654){: external}, [CVE-2024-56663](https://nvd.nist.gov/vuln/detail/CVE-2024-56663){: external}, [CVE-2024-56664](https://nvd.nist.gov/vuln/detail/CVE-2024-56664){: external}, [CVE-2024-56667](https://nvd.nist.gov/vuln/detail/CVE-2024-56667){: external}, [CVE-2024-56688](https://nvd.nist.gov/vuln/detail/CVE-2024-56688){: external}, [CVE-2024-56693](https://nvd.nist.gov/vuln/detail/CVE-2024-56693){: external}, [CVE-2024-56729](https://nvd.nist.gov/vuln/detail/CVE-2024-56729){: external}, [CVE-2024-56757](https://nvd.nist.gov/vuln/detail/CVE-2024-56757){: external}, [CVE-2024-56760](https://nvd.nist.gov/vuln/detail/CVE-2024-56760){: external}, [CVE-2024-56779](https://nvd.nist.gov/vuln/detail/CVE-2024-56779){: external}, [CVE-2024-56783](https://nvd.nist.gov/vuln/detail/CVE-2024-56783){: external}, [CVE-2024-57798](https://nvd.nist.gov/vuln/detail/CVE-2024-57798){: external}, [CVE-2024-57809](https://nvd.nist.gov/vuln/detail/CVE-2024-57809){: external}, [CVE-2024-57843](https://nvd.nist.gov/vuln/detail/CVE-2024-57843){: external}, [CVE-2024-57852](https://nvd.nist.gov/vuln/detail/CVE-2024-57852){: external}, [CVE-2024-57879](https://nvd.nist.gov/vuln/detail/CVE-2024-57879){: external}, [CVE-2024-57884](https://nvd.nist.gov/vuln/detail/CVE-2024-57884){: external}, [CVE-2024-57885](https://nvd.nist.gov/vuln/detail/CVE-2024-57885){: external}, [CVE-2024-57888](https://nvd.nist.gov/vuln/detail/CVE-2024-57888){: external}, [CVE-2024-57890](https://nvd.nist.gov/vuln/detail/CVE-2024-57890){: external}, [CVE-2024-57894](https://nvd.nist.gov/vuln/detail/CVE-2024-57894){: external}, [CVE-2024-57898](https://nvd.nist.gov/vuln/detail/CVE-2024-57898){: external}, [CVE-2024-57903](https://nvd.nist.gov/vuln/detail/CVE-2024-57903){: external}, [CVE-2024-57929](https://nvd.nist.gov/vuln/detail/CVE-2024-57929){: external}, [CVE-2024-57931](https://nvd.nist.gov/vuln/detail/CVE-2024-57931){: external}, [CVE-2024-57940](https://nvd.nist.gov/vuln/detail/CVE-2024-57940){: external}, [CVE-2024-58009](https://nvd.nist.gov/vuln/detail/CVE-2024-58009){: external}, [CVE-2024-58064](https://nvd.nist.gov/vuln/detail/CVE-2024-58064){: external}, [CVE-2024-58099](https://nvd.nist.gov/vuln/detail/CVE-2024-58099){: external}, [CVE-2025-1272](https://nvd.nist.gov/vuln/detail/CVE-2025-1272){: external}, [CVE-2025-21646](https://nvd.nist.gov/vuln/detail/CVE-2025-21646){: external}, [CVE-2025-21663](https://nvd.nist.gov/vuln/detail/CVE-2025-21663){: external}, [CVE-2025-21666](https://nvd.nist.gov/vuln/detail/CVE-2025-21666){: external}, [CVE-2025-21668](https://nvd.nist.gov/vuln/detail/CVE-2025-21668){: external}, [CVE-2025-21669](https://nvd.nist.gov/vuln/detail/CVE-2025-21669){: external}, [CVE-2025-21689](https://nvd.nist.gov/vuln/detail/CVE-2025-21689){: external}, [CVE-2025-21694](https://nvd.nist.gov/vuln/detail/CVE-2025-21694){: external}, [CVE-2025-22087](https://nvd.nist.gov/vuln/detail/CVE-2025-22087){: external}, [RHSA-2025:8142](https://access.redhat.com/errata/RHSA-2025:8142){: external}, [CVE-2025-21964](https://nvd.nist.gov/vuln/detail/CVE-2025-21964){: external}, [RHSA-2025:8333](https://access.redhat.com/errata/RHSA-2025:8333){: external}, [CVE-2022-3424](https://nvd.nist.gov/vuln/detail/CVE-2022-3424){: external}, [CVE-2025-21764](https://nvd.nist.gov/vuln/detail/CVE-2025-21764){: external}, [RHSA-2025:9302](https://access.redhat.com/errata/RHSA-2025:9302){: external}, [CVE-2025-21883](https://nvd.nist.gov/vuln/detail/CVE-2025-21883){: external}, [CVE-2025-21919](https://nvd.nist.gov/vuln/detail/CVE-2025-21919){: external}, [CVE-2025-22104](https://nvd.nist.gov/vuln/detail/CVE-2025-22104){: external}, [CVE-2025-23150](https://nvd.nist.gov/vuln/detail/CVE-2025-23150){: external}, [CVE-2025-37738](https://nvd.nist.gov/vuln/detail/CVE-2025-37738){: external}, [RHSA-2025:9880](https://access.redhat.com/errata/RHSA-2025:9880){: external}, [CVE-2023-52933](https://nvd.nist.gov/vuln/detail/CVE-2023-52933){: external}, [RHSA-2025:7067](https://access.redhat.com/errata/RHSA-2025:7067){: external}, [CVE-2025-24528](https://nvd.nist.gov/vuln/detail/CVE-2025-24528){: external}, [RHSA-2025:9430](https://access.redhat.com/errata/RHSA-2025:9430){: external}, [CVE-2025-3576](https://nvd.nist.gov/vuln/detail/CVE-2025-3576){: external}, [RHSA-2025:9431](https://access.redhat.com/errata/RHSA-2025:9431){: external}, [CVE-2025-25724](https://nvd.nist.gov/vuln/detail/CVE-2025-25724){: external}, [RHSA-2025:18275](https://access.redhat.com/errata/RHSA-2025:18275){: external}, [CVE-2025-5318](https://nvd.nist.gov/vuln/detail/CVE-2025-5318){: external}, [RHSA-2025:7077](https://access.redhat.com/errata/RHSA-2025:7077){: external}, [CVE-2024-12133](https://nvd.nist.gov/vuln/detail/CVE-2024-12133){: external}, [RHSA-2025:13428](https://access.redhat.com/errata/RHSA-2025:13428){: external}, [CVE-2025-32414](https://nvd.nist.gov/vuln/detail/CVE-2025-32414){: external}, [CVE-2025-32415](https://nvd.nist.gov/vuln/detail/CVE-2025-32415){: external}, [RHSA-2025:7043](https://access.redhat.com/errata/RHSA-2025:7043){: external}, [CVE-2024-28047](https://nvd.nist.gov/vuln/detail/CVE-2024-28047){: external}, [CVE-2024-31157](https://nvd.nist.gov/vuln/detail/CVE-2024-31157){: external}, [CVE-2024-39279](https://nvd.nist.gov/vuln/detail/CVE-2024-39279){: external}, [RHSA-2025:6993](https://access.redhat.com/errata/RHSA-2025:6993){: external}, [CVE-2025-26465](https://nvd.nist.gov/vuln/detail/CVE-2025-26465){: external}, [RHSA-2025:11804](https://access.redhat.com/errata/RHSA-2025:11804){: external}, [CVE-2025-40909](https://nvd.nist.gov/vuln/detail/CVE-2025-40909){: external}, [RHSA-2025:15874](https://access.redhat.com/errata/RHSA-2025:15874){: external}, [CVE-2023-49083](https://nvd.nist.gov/vuln/detail/CVE-2023-49083){: external}, [RHSA-2025:12519](https://access.redhat.com/errata/RHSA-2025:12519){: external}, [CVE-2024-47081](https://nvd.nist.gov/vuln/detail/CVE-2024-47081){: external}, [RHSA-2025:7049](https://access.redhat.com/errata/RHSA-2025:7049){: external}, [CVE-2024-35195](https://nvd.nist.gov/vuln/detail/CVE-2024-35195){: external}, [RHSA-2025:10407](https://access.redhat.com/errata/RHSA-2025:10407){: external}, [CVE-2025-47273](https://nvd.nist.gov/vuln/detail/CVE-2025-47273){: external}, [RHSA-2025:15019](https://access.redhat.com/errata/RHSA-2025:15019){: external}, [CVE-2025-8194](https://nvd.nist.gov/vuln/detail/CVE-2025-8194){: external}, [RHSA-2025:6977](https://access.redhat.com/errata/RHSA-2025:6977){: external}, [CVE-2025-0938](https://nvd.nist.gov/vuln/detail/CVE-2025-0938){: external}, [RHSA-2025:7326](https://access.redhat.com/errata/RHSA-2025:7326){: external}, [CVE-2024-45336](https://nvd.nist.gov/vuln/detail/CVE-2024-45336){: external}, [CVE-2025-22866](https://nvd.nist.gov/vuln/detail/CVE-2025-22866){: external}, [RHSA-2025:10353](https://access.redhat.com/errata/RHSA-2025:10353){: external}, [CVE-2024-54661](https://nvd.nist.gov/vuln/detail/CVE-2024-54661){: external}, [RHSA-2025:17742](https://access.redhat.com/errata/RHSA-2025:17742){: external}, [CVE-2025-53905](https://nvd.nist.gov/vuln/detail/CVE-2025-53905){: external}, and [CVE-2025-53906](https://nvd.nist.gov/vuln/detail/CVE-2025-53906){: external}.|
|Red Hat OpenShift and Red Hat CoreOS|4.18.26|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-26_release-notes).|
|HAProxy|c01cd5322cd5c284286c07fe9ad0cc0ef3ab5360|Resolves the following CVEs: [CVE-2025-32988](https://nvd.nist.gov/vuln/detail/CVE-2025-32988){: external}, [CVE-2025-6395](https://nvd.nist.gov/vuln/detail/CVE-2025-6395){: external}, and [CVE-2025-32990](https://nvd.nist.gov/vuln/detail/CVE-2025-32990){: external}.|
{: caption="4.18.26_1565_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41826_1565_openshift_W-component-table}


### Worker node fix pack 4.18.25_1564_openshift, released 08 October 2025
{: #cl-boms-41825_1564_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.25_1564_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-503.40.1.el9_5|N/A|
|Red Hat OpenShift and Red Hat CoreOS|4.18.25|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-25_release-notes).|
|HAProxy|e0a48fcf355d98dc769ea048d2fd02044b11ed62|N/A|
{: caption="4.18.25_1564_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41825_1564_openshift_W-component-table}


### Master fix pack 4.18.24_1563_openshift, released 07 October 2025
{: #41824_1563_openshift_M}

The following table shows the changes that are in the master fix pack 4.18.24_1563_openshift. Master patch updates are applied automatically. 


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.29.4 | v3.29.5 | See the [Calico release notes](https://docs.tigera.io/calico/3.29/release-notes/#v3.29.5){: external}. |
| etcd | v3.5.22 | v3.5.23 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.23){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.31.13-1 | v1.31.13-2 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor | 451 | 452 | New version contains updates and security fixes. |
| Key Management Service provider | v2.10.16 | v2.10.17 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.29 | v0.13.30 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.30){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.18.21 | 4.18.24 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes#ocp-4-18-24){: external}. |
| Tigera Operator | v1.36.11 | v1.36.13 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.36.13){: external}. |
{: caption="Changes since version 4.18.21_1555_openshift" caption-side="bottom"}


### Worker node fix pack 4.18.24_1560_openshift, released 23 September 2025
{: #cl-boms-41824_1560_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.24_1560_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-503.40.1.el9_5|N/A|
|Red Hat OpenShift and Red Hat CoreOS|4.18.24|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-24_release-notes).|
|HAProxy|e0a48fcf355d98dc769ea048d2fd02044b11ed62|N/A|
{: caption="4.18.24_1560_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41824_1560_openshift_W-component-table}


### Worker node fix pack 4.18.23_1558_openshift, released 15 September 2025
{: #cl-boms-41823_1558_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.23_1558_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-503.40.1.el9_5|SELinux policy update for container runtime BPF execution to allow workloads like GPU Operators to run successfully|
|Red Hat OpenShift and Red Hat CoreOS|4.18.23|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-23_release-notes).|
|HAProxy|e0a48fcf355d98dc769ea048d2fd02044b11ed62|N/A|
{: caption="4.18.23_1558_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41823_1558_openshift_W-component-table}


### Worker node fix pack 4.18.23_1557_openshift, released 09 September 2025
{: #cl-boms-41823_1557_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.23_1557_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-503.40.1.el9_5|N/A|
|Red Hat OpenShift and Red Hat CoreOS|4.18.23|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-23_release-notes).|
|HAProxy|e0a48fcf355d98dc769ea048d2fd02044b11ed62|Resolves the following CVEs: [CVE-2025-6020](https://nvd.nist.gov/vuln/detail/CVE-2025-6020){: external}, and [CVE-2025-8941](https://nvd.nist.gov/vuln/detail/CVE-2025-8941){: external}.|
{: caption="4.18.23_1557_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41823_1557_openshift_W-component-table}


### Worker node fix pack 4.18.22_1556_openshift, released 26 August 2025
{: #cl-boms-41822_1556_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.22_1556_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-503.40.1.el9_5|N/A|
|Red Hat OpenShift and Red Hat CoreOS|4.18.22|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-22_release-notes).|
|HAProxy|3293782c542587d0ce46be4d053036b75509f4ef|Resolves the following CVEs: [CVE-2025-5914](https://nvd.nist.gov/vuln/detail/CVE-2025-5914){: external}.|
{: caption="4.18.22_1556_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41822_1556_openshift_W-component-table}


### Master fix pack 4.18.21_1555_openshift, released 20 August 2025
{: #41821_1555_openshift_M}

The following table shows the changes that are in the master fix pack 4.18.21_1555_openshift. Master patch updates are applied automatically. 


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| etcd | v3.5.21 | v3.5.22 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.22){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.31.10-4 | v1.31.11-2 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 38dc95c | 8a12251 | New version contains updates and security fixes. |
| Key Management Service provider | v2.10.15 | v2.10.16 | New version contains updates and security fixes. |
| {{site.data.keyword.openshiftlong_notm}} | 4.18.19 | 4.18.21 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes#ocp-4-18-21_release-notes){: external}. |
{: caption="Changes since version 4.18.19_1552_openshift" caption-side="bottom"}


### Worker node fix pack 4.18.21_1554_openshift, released 12 August 2025
{: #cl-boms-41821_1554_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.21_1554_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-503.40.1.el9_5|N/A|
|Red Hat OpenShift and Red Hat CoreOS|4.18.21|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-21_release-notes).|
|HAProxy|3a9451f4782fa8e8e9ed60b060dc4393c7e1e31a|Resolves the following CVEs: [CVE-2025-6965](https://nvd.nist.gov/vuln/detail/CVE-2025-6965){: external}, [CVE-2025-8058](https://nvd.nist.gov/vuln/detail/CVE-2025-8058){: external}, and [CVE-2025-7425](https://nvd.nist.gov/vuln/detail/CVE-2025-7425){: external}.|
{: caption="4.18.21_1554_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41821_1554_openshift_W-component-table}


### Master fix pack 4.18.19_1552_openshift, released 30 July 2025
{: #41819_1552_openshift_M}

The following table shows the changes that are in the master fix pack 4.18.19_1552_openshift. Master patch updates are applied automatically. 


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.29.3 | v3.29.4 | See the [Calico release notes](https://docs.tigera.io/calico/3.29/release-notes/#calico-open-source-3294-bug-fix-release){: external}. |
| Calico API server | v3.29.2 | v3.29.4 | See the [Calico release notes](https://docs.tigera.io/archive){: external}. |
| Cluster health image | v1.6.8 | v1.6.10 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.5.19 | v2.5.20 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.31.9-4 | v1.31.10-4 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor | 450 | 451 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | d1545bd | 38dc95c | New version contains updates and security fixes. |
| Key Management Service provider | v2.10.13 | v2.10.15 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 3232 | 3347 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.26 | v0.13.29 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.29){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.18.12 | 4.18.19 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes#ocp-4-18-19){: external}. |
| Tigera Operator | v1.36.8 | v1.36.11 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.36.11){: external}. |
{: caption="Changes since version 4.18.11_1547_openshift" caption-side="bottom"}


### Worker node fix pack 4.18.20_1553_openshift, released 28 July 2025
{: #cl-boms-41820_1553_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.20_1553_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-503.40.1.el9_5|N/A|
|Red Hat OpenShift and Red Hat CoreOS|4.18.20|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-20_release-notes).|
|HAProxy|b19109a289be3a60985c14bfdaf2b48a472556c0|Resolves the following CVEs: [CVE-2024-54661](https://nvd.nist.gov/vuln/detail/CVE-2024-54661){: external}, [CVE-2024-34397](https://nvd.nist.gov/vuln/detail/CVE-2024-34397){: external}, [CVE-2019-17543](https://nvd.nist.gov/vuln/detail/CVE-2019-17543){: external}, [CVE-2024-52533](https://nvd.nist.gov/vuln/detail/CVE-2024-52533){: external}, and [CVE-2025-4373](https://nvd.nist.gov/vuln/detail/CVE-2025-4373){: external}.|
{: caption="4.18.20_1553_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41820_1553_openshift_W-component-table}


### Worker node fix pack 4.18.19_1539_openshift, released 14 July 2025
{: #cl-boms-41819_1539_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.19_1539_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-503.40.1.el9_5|N/A|
|Red Hat OpenShift and Red Hat CoreOS|4.18.19|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-19_release-notes).|
|HAProxy|3bb13ac682885a0885eacb7edd1ee7a36d54e2a8|Resolves the following CVEs: [CVE-2025-6021](https://nvd.nist.gov/vuln/detail/CVE-2025-6021){: external}, [CVE-2025-49796](https://nvd.nist.gov/vuln/detail/CVE-2025-49796){: external}, [CVE-2025-49794](https://nvd.nist.gov/vuln/detail/CVE-2025-49794){: external}, and [CVE-2025-6020](https://nvd.nist.gov/vuln/detail/CVE-2025-6020){: external}.|
{: caption="4.18.19_1539_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41819_1539_openshift_W-component-table}


### Worker node fix pack 4.18.18_1539_openshift, released 01 July 2025
{: #cl-boms-41818_1539_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.18_1539_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-503.40.1.el9_5|N/A|
|Red Hat OpenShift and Red Hat CoreOS|4.18.18|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-18_release-notes).|
|HAProxy|951efd90b46e95a54751966c644ac37c4c901f92|N/A|
{: caption="4.18.18_1539_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41818_1539_openshift_W-component-table}


### Master fix pack 4.18.11_1547_openshift, released 18 June 2025
{: #41811_1547_openshift_M}

The following table shows the changes that are in the master fix pack 4.18.11_1547_openshift. Master patch updates are applied automatically. 


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.29.2 | v3.29.3 | See the [Calico release notes](https://docs.tigera.io/calico/3.29/release-notes/#v3.29.3){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.5.17 | v2.5.19 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.31.9-1 | v1.31.9-4 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | d1545bd | 38dc95c | New version contains updates and security fixes. |
| Key Management Service provider | v2.10.13 | v2.10.14 | New version contains updates and security fixes. |
| Tigera Operator | v1.36.5 | v1.36.8 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.36.8){: external}. |
{: caption="Changes since version 4.18.11_1544_openshift" caption-side="bottom"}


### Worker node fix pack 4.18.17_1539_openshift, released 16 June 2025
{: #cl-boms-41817_1539_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.17_1539_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-503.40.1.el9_5|N/A|
|Red Hat OpenShift and Red Hat CoreOS|4.18.17|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-17_release-notes).|
|HAProxy|951efd90b46e95a54751966c644ac37c4c901f92|Resolves the following CVEs: [CVE-2025-4802](https://nvd.nist.gov/vuln/detail/CVE-2025-4802){: external}, [CVE-2025-32414](https://nvd.nist.gov/vuln/detail/CVE-2025-32414){: external}, and [CVE-2025-3576](https://nvd.nist.gov/vuln/detail/CVE-2025-3576){: external}.|
{: caption="4.18.17_1539_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41817_1539_openshift_W-component-table}


### Worker node fix pack 4.18.15_1539_openshift, released 04 June 2025
{: #cl-boms-41815_1539_openshift_W}

The following table shows the components included in the worker node fix pack 4.18.15_1539_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-503.40.1.el9_5|N/A|
|Red Hat OpenShift and Red Hat CoreOS|4.18.15|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes.html#ocp-4-18-15_release-notes).|
|HAProxy|978e3c26ee7634e39a940696aaf57d9e374db5ce|N/A|
{: caption="4.18.15_1539_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41815_1539_openshift_W-component-table}


### Master fix pack 4.18.11_1543_openshift, released 28 May 2025
{: #41811_1544_openshift_M}

The following table shows the changes that are in the master fix pack 4.18.11_1544_openshift. Master patch updates are applied automatically. 


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.31.8-3 | v1.31.9-1 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor | 449 | 450 | New version contains updates and security fixes. |
{: caption="Changes since version 4.18.11_1543_openshift" caption-side="bottom"}


### Master fix pack 4.18.11_1544_openshift and worker node fix pack 4.18.11_1541_openshift, released 27 May 2025
{: #openshift_changelog_41811_1544}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico API server, policy controller, and Typha | v3.28.3 | v3.29.2 | See the [Calico release notes](https://docs.tigera.io/calico/latest/release-notes/){: external}. |
| Cluster health image | v1.6.8 | v1.6.9 | New version contains updates and security fixes. |
| IBM Cloud Controller Manager | v1.30.11-6 | v1.31.8-3 | New version contains updates and security fixes. |
| Key Management Service provider | 2.10.12 | 2.10.13 | New version contains updates and security fixes. |
| Load balancer for IBM Cloud Provider | 3232 | 3293 | New version contains updates and security fixes. |
| OpenShift | 4.17.24-x86_64 | 4.18.11-x86_64 | [OpenShift docs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/){: external}. |
| Portieris admission controller | v0.13.26 | v0.13.28 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.13.28){: external}. |
| Red Hat OpenShift on IBM Cloud Control Plane Operator, Metrics Server, and toolkit | 4.17.0+20250414 | N/A | Red Hat OpenShift on IBM Cloud 4.18 now utilizes [Red Hat HyperShift](https://github.com/openshift/hypershift){: external} in place of the toolkit. Also, see the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases){: external}. |
| Tigera Operator | v1.34.8 | v1.36.5 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.36.5){: external}. |
{: caption="Changes since master fix pack 4.17.24_1537_openshift and worker fix pack 4.17.25_1536_openshift." caption-side="bottom"}
