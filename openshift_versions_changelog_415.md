---

copyright:
  years: 2023, 2024
lastupdated: "2024-05-30"


keywords: openshift, 4.15, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# Version 4.15 change log
{: #openshift_changelog_415}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.15. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #openshift_changelog_overview_415}

Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security){: external} for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}


### Change log for master fix pack 4.15.14_1537_openshift, released 29 May 2024
{: #41514_1537_openshift_M}

The following table shows the changes that are in the master fix pack 4.15.14_1537_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.5.4 | v1.5.5 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.28.9-4 | v1.28.10-1 | New version contains updates and security fixes. |
| Key Management Service provider | v2.9.5 | v2.9.6 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2867 | 2933 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.13 | v0.13.15 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.15){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.15.11 | 4.15.14 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-14){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | 4.15.0+20240415 | 4.15.0+20240514 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.15.0+20240514){: external}. |
{: caption="Changes since version 4.15.11_1534_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.15.13_1535_openshift, released 23 May 2024
{: #41513_1535_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.15.13_1535_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.15.11 | 4.15.13 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-13){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-513.24.1.el8_9 | Worker node package updates for [RHSA-2024:2722](https://access.redhat.com/errata/RHSA-2024:2722){: external}, [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961){: external}. |
| HAProxy | d225100 | 4e826da | [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961){: external}, [CVE-2024-28834](https://nvd.nist.gov/vuln/detail/CVE-2024-28834){: external}. |
{: caption="Changes since version 4.15.11_1533_openshift" caption-side="bottom"}


### Change log for master fix pack 4.15.11_1534_openshift, released 09 May 2024
{: #41511_1534_openshift_M}

The following table shows the changes that are in the master fix pack 4.15.11_1534_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.5.8 | v2.5.9 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.28.9-1 | v1.28.9-4 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor | 442 | 443 | New version contains updates and security fixes. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.15.9 | 4.15.11 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-11){: external}. |
{: caption="Changes since version 4.15.9_1530_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.15.11_1533_openshift, released 06 May 2024
{: #41511_1533_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.15.11_1533_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.15.9 | 4.15.11 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-11){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-513.24.1.el8_9 | Worker node package updates for [RHSA-2024:2098](https://access.redhat.com/errata/RHSA-2024:2098){: external}, [CVE-2024-1753](https://nvd.nist.gov/vuln/detail/CVE-2024-1753){: external}. |
| HAProxy | 295dba8 | 295dba8 | N/A |
{: caption="Changes since version 4.15.9_1531_openshift" caption-side="bottom"}


### Change log for master fix pack 4.15.9_1530_openshift and worker node fix pack 4.15.6_1525_openshift, released 24 April 2024
{: #4.15.9_1530_openshiftM_4.15.6_1525_openshift_openshiftW}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.26.4 | v3.27.2 | See the [Calico release notes](https://docs.tigera.io/calico/3.27/release-notes/). |
| IBM Calico extension | 1537 | N/A | Component has been removed. |
| IBM Cloud Controller Manager | v1.27.12-10 | v1.28.9-1 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.9 | v2.9.5 | New version contains updates and security fixes. |
| Red Hat OpenShift (master) | 4.14.20 | 4.15.9 | See the [Red Hat OpenShift release notes](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-9). |
| Red Hat OpenShift (worker node) | 4.14.19 | 4.15.6 | See the [Red Hat OpenShift release notes](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-6). |
| Red Hat OpenShift on IBM Cloud Control Plane Operator, Metrics Server, and toolkit | 4.14.0+20240412 | 4.15.0+20240415 | See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.15.0+20240415). |
| Tigera Operator | v1.30.9 | v1.32.5 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.32.5). |
{: caption="Changes since master fix pack 4.14.20_1558_openshift and worker fix pack 4.14.19_1557_openshift." caption-side="bottom"}






### Change log for worker node fix pack 4.15.9_1531_openshift, released 22 April 2024
{: #4159_1531_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.15.9_1531_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.15.6 | 4.15.9 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-9){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-513.24.1.el8_9 | Worker node package updates for [RHSA-2024:1782](https://access.redhat.com/errata/RHSA-2024:1782){: external}, [CVE-2023-4408](https://nvd.nist.gov/vuln/detail/CVE-2023-4408){: external}, [CVE-2023-50387](https://nvd.nist.gov/vuln/detail/CVE-2023-50387){: external}, [CVE-2023-50868](https://nvd.nist.gov/vuln/detail/CVE-2023-50868){: external}, [RHSA-2024:1784](https://access.redhat.com/errata/RHSA-2024:1784){: external}, [CVE-2024-28834](https://nvd.nist.gov/vuln/detail/CVE-2024-28834){: external}. |
| HAProxy | 295dba8 | 4e826da | Security fixes for [CVE-2024-28834](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2024-28834){: external}. |
{: caption="Changes since version 4.15.6_1525_openshift" caption-side="bottom"}


