---

copyright:
  years: 2026, 2026

lastupdated: "2026-03-29"


keywords: change log, version history, 4.20_openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# 4.20 version change log
{: #openshift_changelog_420}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run this version. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #changelog_overview_420}


Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security){: external} for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}

## Version 4.20
{: #420_components}


### Change log for Master fix pack 4.20.15_1542_openshift, released 25 March 2026
{: #42015_1542_openshift_M}

The following table shows the changes that are in the master fix pack 4.20.15_1542_openshift. Master patch updates are applied automatically. 


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.30.4 | v3.30.6 | See the [Calico release notes](https://docs.tigera.io/calico/3.30/release-notes/#calico-open-source-3306-bug-fix-release){: external}. |
| Cluster health image | v1.6.14 | v1.6.15 | New version contains updates and security fixes. |
| etcd | v3.5.26 | v3.5.27 | See the [etcd release notes](https://github.com/coreos/etcd/releases/v3.5.27){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.5.24 | v2.5.25 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.33.7-7 | v1.33.9-1 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor | 452 | v454 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 8a12251 | 6212368 | New version contains updates and security fixes. |
| Key Management Service provider | v2.10.20 | 2.10.22 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 3347 | 3563 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.33 | v0.13.36 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.36){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.20.12 | 4.20.15 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes#ocp-4-20-15_release-notes){: external}. |
| Tigera Operator | v1.38.8 | v1.38.11 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.38.11){: external}. |
{: caption="Changes since version 4.20.13-1538-openshift" caption-side="bottom"}


### Worker node fix pack 4.20.16_1542_openshift, released 24 March 2026
{: #cl-boms-42016_1542_openshift_W}

The following table shows the components included in the worker node fix pack 4.20.16_1542_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL 9 (VPC)|5.14.0-570.62.1.el9_6|N/A|
|RHEL 9 (Classic)|5.14.0-570.62.1.el9_6|N/A|
|Red Hat OpenShift|4.20.16|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-16_release-notes).|
|Red Hat CoreOS|4.20.16|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-16_release-notes). CIS benchmark compliance [3.4.2.3](https://workbench.cisecurity.org/sections/1594542/recommendations/2564568).|
|HAProxy|10c8639e6b5829d0af51a22755e13756f34630cf|Resolves the following CVEs: [CVE-2025-15281](https://nvd.nist.gov/vuln/detail/CVE-2025-15281){: external}, and [CVE-2026-0915](https://nvd.nist.gov/vuln/detail/CVE-2026-0915){: external}.|
{: caption="4.20.16_1542_openshift fix pack." caption-side="bottom"}
{: #cl-boms-42016_1542_openshift_W-component-table}


### Worker node fix pack 4.20.15_1540_openshift, released 11 March 2026
{: #cl-boms-42015_1540_openshift_W}

The following table shows the components included in the worker node fix pack 4.20.15_1540_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL 9 (VPC)|5.14.0-570.62.1.el9_6|N/A|
|RHEL 9 (Classic)|5.14.0-570.62.1.el9_6|N/A|
|Red Hat OpenShift|4.20.15|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-15_release-notes).|
|Red Hat CoreOS|4.20.15|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-15_release-notes). CIS benchmark compliance [1.1.3.2](https://workbench.cisecurity.org/sections/1594516/recommendations/2564412), [1.1.3.3](https://workbench.cisecurity.org/sections/1594516/recommendations/2564414), [3.4.2](https://workbench.cisecurity.org/benchmarks/11478/sections/1594542), [4.2.2.3](https://workbench.cisecurity.org/sections/1594553/recommendations/2564633)|
|HAProxy|965c403695b15b3410d87a3772002edbc5ed2569|Resolves the following CVEs: [CVE-2025-69419](https://nvd.nist.gov/vuln/detail/CVE-2025-69419){: external}.|
{: caption="4.20.15_1540_openshift fix pack." caption-side="bottom"}
{: #cl-boms-42015_1540_openshift_W-component-table}


### Worker node fix pack 4.20.14_1539_openshift, released 24 February 2026
{: #cl-boms-42014_1539_openshift_W}

The following table shows the components included in the worker node fix pack 4.20.14_1539_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL 9 (VPC)|5.14.0-570.62.1.el9_6|CIS benchmark compliance [1.6.3](https://workbench.cisecurity.org/sections/2758919/recommendations/4466876)|
|RHEL 9 (Classic)|5.14.0-570.62.1.el9_6|CIS benchmark compliance [1.6.3](https://workbench.cisecurity.org/sections/2758919/recommendations/4466876)|
|Red Hat OpenShift|4.20.14|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-14_release-notes).|
|Red Hat CoreOS|4.20.14|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-14_release-notes). CIS benchmark compliance [5.2.2](https://workbench.cisecurity.org/sections/1594521/recommendations/2564440), [5.2.3](https://workbench.cisecurity.org/sections/1594521/recommendations/2564444), [5.2.4](https://workbench.cisecurity.org/sections/1594521/recommendations/2564446), [5.2.18](https://workbench.cisecurity.org/sections/1594521/recommendations/2564555)|
|HAProxy|2bf1aebe51a37cd9b4661656ce21e53f918166ea|Resolves the following CVEs: [CVE-2025-6176](https://nvd.nist.gov/vuln/detail/CVE-2025-6176){: external}.|
{: caption="4.20.14_1539_openshift fix pack." caption-side="bottom"}
{: #cl-boms-42014_1539_openshift_W-component-table}


### Change log for Master fix pack 4.20.13_1538_openshift, released 18 February 2026
{: #42013_1538_openshift_M}

The following table shows the changes that are in the master fix pack 4.20.13_1538_openshift. Master patch updates are applied automatically. 


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.30.4 | v3.30.6 | See the [Calico release notes](https://docs.tigera.io/calico/3.30/release-notes/#calico-open-source-3306-bug-fix-release){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.33.7-4 | v1.33.7-8 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor | 452 | v453 | New version contains updates and security fixes. |
| Key Management Service provider | v2.10.20 | 2.10.21 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.33 | v0.13.35 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.35){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.20.12 | 4.20.13 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes#ocp-4-20-13_release-notes){: external}. |
| Tigera Operator | v1.38.8 | v1.38.11 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.38.11){: external}. |
{: caption="Changes since version 4.20.12-1536-openshift" caption-side="bottom"}


### Worker node fix pack 4.20.13_1537_openshift, released 09 February 2026
{: #cl-boms-42013_1537_openshift_W}

The following table shows the components included in the worker node fix pack 4.20.13_1537_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL 9 (VPC)|5.14.0-570.62.1.el9_6|CIS benchmark compliance [1.6.6](https://workbench.cisecurity.org/sections/2758919/recommendations/4466895), [3.1.3](https://workbench.cisecurity.org/sections/2758883/recommendations/4466704), [4.1.2](https://workbench.cisecurity.org/sections/2758898/recommendations/4466776), [4.3.4](https://workbench.cisecurity.org/sections/2758905/recommendations/4466822), [5.3.2.1](https://workbench.cisecurity.org/sections/2758922/recommendations/4466880), [5.3.3.2.4](https://workbench.cisecurity.org/sections/2758930/recommendations/4466941), [5.3.3.2.7](https://workbench.cisecurity.org/sections/2758930/recommendations/4466958), [5.3.3.3.1](https://workbench.cisecurity.org/sections/2758934/recommendations/4466960), [5.3.3.4.2](https://workbench.cisecurity.org/sections/2758935/recommendations/4466965), [5.4.1.5](https://workbench.cisecurity.org/sections/2758937/recommendations/4466972), [5.4.2.5](https://workbench.cisecurity.org/sections/2758938/recommendations/4466978)Resolves the following CVEs: [RHSA-2025:19930](https://access.redhat.com/errata/RHSA-2025:19930){: external}, [CVE-2024-36350](https://nvd.nist.gov/vuln/detail/CVE-2024-36350){: external}, [CVE-2024-36357](https://nvd.nist.gov/vuln/detail/CVE-2024-36357){: external}, and [CVE-2025-40300](https://nvd.nist.gov/vuln/detail/CVE-2025-40300){: external}.|
|RHEL 9 (Classic)|5.14.0-570.62.1.el9_6|CIS benchmark compliance [1.6.6](https://workbench.cisecurity.org/sections/2758919/recommendations/4466895), [3.1.3](https://workbench.cisecurity.org/sections/2758883/recommendations/4466704), [4.1.2](https://workbench.cisecurity.org/sections/2758898/recommendations/4466776), [4.3.4](https://workbench.cisecurity.org/sections/2758905/recommendations/4466822), [5.3.2.1](https://workbench.cisecurity.org/sections/2758922/recommendations/4466880), [5.3.3.2.4](https://workbench.cisecurity.org/sections/2758930/recommendations/4466941), [5.3.3.2.7](https://workbench.cisecurity.org/sections/2758930/recommendations/4466958), [5.3.3.3.1](https://workbench.cisecurity.org/sections/2758934/recommendations/4466960), [5.3.3.4.2](https://workbench.cisecurity.org/sections/2758935/recommendations/4466965), [5.4.1.5](https://workbench.cisecurity.org/sections/2758937/recommendations/4466972), [5.4.2.5](https://workbench.cisecurity.org/sections/2758938/recommendations/4466978)Resolves the following CVEs: [RHSA-2025:19930](https://access.redhat.com/errata/RHSA-2025:19930){: external}, [CVE-2024-36350](https://nvd.nist.gov/vuln/detail/CVE-2024-36350){: external}, [CVE-2024-36357](https://nvd.nist.gov/vuln/detail/CVE-2024-36357){: external}, and [CVE-2025-40300](https://nvd.nist.gov/vuln/detail/CVE-2025-40300){: external}.|
|Red Hat OpenShift|4.20.13|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-13_release-notes).|
|Red Hat CoreOS|4.20.13|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-13_release-notes).|
|HAProxy|ace947f4ecf45f28effe8d125ffda48f9890223b|Resolves the following CVEs: [CVE-2025-14104](https://nvd.nist.gov/vuln/detail/CVE-2025-14104){: external}.|
{: caption="4.20.13_1537_openshift fix pack." caption-side="bottom"}
{: #cl-boms-42013_1537_openshift_W-component-table}


### Master and worker fixpacks 4.20.12_1536_openshift and 4.20.10_1535_openshift, released 04 February 2026
{: #42012_1536M_and_42010_1535W}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.29.7 | v3.30.4 | See the [Calico release notes](https://docs.tigera.io/calico/3.30/release-notes/#calico-open-source-3304-bug-fix-release). |
| Cluster health image | v1.6.13 | v1.6.14 | New version contains updates and security fixes. |
| IBM Cloud Block Storage driver and plug-in | v2.5.22 | v2.5.24 | New version contains updates and security fixes. |
| IBM Cloud Controller Manager | v1.32.11-2 | v1.33.7-7 | New version contains updates and security fixes. |
| Red Hat OpenShift (master) | 4.19.21 | 4.20.12 | See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes#ocp-4-20-12_release-notes). |
| Red Hat OpenShift (worker node) | 4.19.21 | 4.20.10 | See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes#ocp-4-20-12_release-notes). |
| Tigera Operator | v1.36.16 | v1.38.8 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.38.8). |
{: caption="Changes since master version 4.19.21-1566-openshift and worker version 4.19.21_1565_openshift." caption-side="bottom"}
