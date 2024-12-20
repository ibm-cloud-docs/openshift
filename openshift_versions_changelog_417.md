---

copyright:
  years: 2024, 2024
lastupdated: "2024-12-17"


keywords: openshift, 4.17, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# Version 4.17 change log
{: #openshift_changelog_417}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.17. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #openshift_changelog_overview_417}

Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security){: external} for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}


### Change log for worker node fix pack 4.17.8_1519_openshift, released 16 December 2024
{: #4178_1519_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.17.8_1519_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages | 4.18.0-553.30.1.el8_10 | 4.18.0-553.32.1.el8_10 | Worker node kernel & package updates for [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043){: external}, [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/CVE-2024-0690){: external}, [RHSA-2024:10943](https://access.redhat.com/errata/RHSA-2024:10943){: external}, [CVE-2024-46695](https://nvd.nist.gov/vuln/detail/CVE-2024-46695){: external}, [CVE-2024-49949](https://nvd.nist.gov/vuln/detail/CVE-2024-49949){: external}, [CVE-2024-50082](https://nvd.nist.gov/vuln/detail/CVE-2024-50082){: external}, [CVE-2024-50099](https://nvd.nist.gov/vuln/detail/CVE-2024-50099){: external}, [CVE-2024-50110](https://nvd.nist.gov/vuln/detail/CVE-2024-50110){: external}, [CVE-2024-50142](https://nvd.nist.gov/vuln/detail/CVE-2024-50142){: external}, [CVE-2024-50192](https://nvd.nist.gov/vuln/detail/CVE-2024-50192){: external}, [CVE-2024-50256](https://nvd.nist.gov/vuln/detail/CVE-2024-50256){: external}, [CVE-2024-50264](https://nvd.nist.gov/vuln/detail/CVE-2024-50264){: external}, [RHSA-2024:10779](https://access.redhat.com/errata/RHSA-2024:10779){: external}, [CVE-2024-11168](https://nvd.nist.gov/vuln/detail/CVE-2024-11168){: external}, [CVE-2024-9287](https://nvd.nist.gov/vuln/detail/CVE-2024-9287){: external}, [RHSA-2024:10784](https://access.redhat.com/errata/RHSA-2024:10784){: external}, [CVE-2022-3064](https://nvd.nist.gov/vuln/detail/CVE-2022-3064){: external}. |
| HAProxy | 55c1488 | 14daa78 | Security fixes for [CVE-2024-10963](https://nvd.nist.gov/vuln/detail/CVE-2024-10963){: external}, [CVE-2024-11168](https://nvd.nist.gov/vuln/detail/CVE-2024-11168){: external}, [CVE-2024-9287](https://nvd.nist.gov/vuln/detail/CVE-2024-9287){: external}, [CVE-2024-10041](https://nvd.nist.gov/vuln/detail/CVE-2024-10041){: external}. |
| {{site.data.keyword.openshiftshort}} | 4.17.5 | 4.17.8 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.17/release_notes/ocp-4-17-release-notes.html#ocp-4-17-8_release-notes){: external}.|
{: caption="Changes since version 4.17.5_1518_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.17.5_1518_openshift, released 05 December 2024
{: #4175_1518_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.17.5_1518_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages | 4.18.0-553.27.1.el8_10 | 4.18.0-553.30.1.el8_10 | Worker node kernel & package updates for [RHSA-2024:10379](https://access.redhat.com/errata/RHSA-2024:10379){: external}, [CVE-2024-10041](https://nvd.nist.gov/vuln/detail/CVE-2024-10041){: external}, [CVE-2024-10963](https://nvd.nist.gov/vuln/detail/CVE-2024-10963){: external}, [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043){: external}, [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/CVE-2024-0690){: external}, [RHSA-2024:10289](https://access.redhat.com/errata/RHSA-2024:10289){: external}, [CVE-2021-33198](https://nvd.nist.gov/vuln/detail/CVE-2021-33198){: external}, [CVE-2021-4024](https://nvd.nist.gov/vuln/detail/CVE-2021-4024){: external}, [CVE-2024-9676](https://nvd.nist.gov/vuln/detail/CVE-2024-9676){: external}, [RHSA-2024:10281](https://access.redhat.com/errata/RHSA-2024:10281){: external}, [CVE-2024-27043](https://nvd.nist.gov/vuln/detail/CVE-2024-27043){: external}, [CVE-2024-27399](https://nvd.nist.gov/vuln/detail/CVE-2024-27399){: external}, [CVE-2024-38564](https://nvd.nist.gov/vuln/detail/CVE-2024-38564){: external}, [CVE-2024-46858](https://nvd.nist.gov/vuln/detail/CVE-2024-46858){: external}. |
| RHEL 9 Packages | N/A | N/A | N/A |
| HAProxy | N/A | N/A | N/A |
| {{site.data.keyword.openshiftshort}} and Red Hat CoreOS | 4.17.4 | 4.17.5 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.17/release_notes/ocp-4-17-release-notes.html){: external}. |
{: caption="Changes since version 4.17.4_1516_openshift" caption-side="bottom"}


### Change log for master fix pack 4.17.5_1517_openshift, released 04 December 2024
{: #4175_1517_openshift_M}

The following table shows the changes that are in the master fix pack 4.17.5_1517_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.30.6-3 | v1.30.6-4 | New version contains updates and security fixes. |
| Key Management Service provider | v2.10.7 | v2.10.8 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 3051 | 3079 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.20 | v0.13.21 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.21){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.17.4 | 4.17.5 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.17/release_notes/ocp-4-17-release-notes.html#ocp-4-17-5){: external}. |
{: caption="Changes since version 4.17.4_1515_openshift" caption-side="bottom"}


### Change log for master fix pack 4.17.4_1515_openshift and worker node fix pack 4.17.4_1516_openshift, released 20 November 2024
{: #openshift_changelog_4174_1515}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| IBM Cloud Controller Manager | v1.29.10-2 | v1.30.6-3 | New version contains updates and security fixes. |
| IBM Cloud RBAC Operator | c4a05b0 | 743ed58 | New version contains updates and security fixes. |
| Red Hat OpenShift (master) | 4.16.19 | 4.17.4 | See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.openshift.com/container-platform/4.17/release_notes/ocp-4-17-release-notes.html#ocp-4-17-4_release-notes) |
| Red Hat OpenShift (worker node) | 4.16.21 | 4.17.4 | See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.openshift.com/container-platform/4.17/release_notes/ocp-4-17-release-notes.html#ocp-4-17-4_release-notes) |
| Red Hat OpenShift on IBM Cloud Control Plane Operator, Metrics Server, and toolkit | 4.16.0+20240913 | 4.17.0+20241112 | See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.17.0%2B20241112). |
{: caption="Changes since master fix pack 4.16.19_1543_openshift and worker fix pack 4.16.21_1544_openshift." caption-side="bottom"}