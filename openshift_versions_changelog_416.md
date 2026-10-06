---

copyright:
  years: 2024, 2026

lastupdated: "2026-10-06"


keywords: change log, version history, 4.16_openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}





# 4.16 version change log
{: #openshift_changelog_416}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run this version. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}



This version is no longer supported. Update your cluster to a [supported version](/docs/openshift?topic=openshift-openshift_versions) as soon as possible.
{: important}



## Overview
{: #changelog_overview_416}


Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security){: external} for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}

## Version 4.16
{: #416_components}


## 25 August 2026, Worker node fix pack 4.16.68_1629_openshift
{: #cl-boms-41668_1629_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.68_1629_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-687.39.1.el9_8
:   Resolves the following CVEs: RHSA-2026:54510, CVE-2026-10723, CVE-2026-11331, CVE-2026-11622, CVE-2026-11721, CVE-2026-13204, CVE-2026-13321, RHSA-2026:55439, CVE-2026-1965, CVE-2026-3783, CVE-2026-8286, CVE-2026-9547, RHSA-2026:54571, CVE-2026-15816, RHSA-2026:55772, CVE-2026-55203, CVE-2026-55204, RHSA-2026:53844, CVE-2026-44943, CVE-2026-44944, RHSA-2026:53847, CVE-2026-55995, RHSA-2026:53329, CVE-2025-54518, CVE-2026-31530, CVE-2026-64368, CVE-2026-64531, RHSA-2026:54443, CVE-2026-53202, CVE-2026-53264, RHSA-2026:54268, CVE-2026-11940, RHSA-2026:55440, CVE-2026-15588, CVE-2026-58010, CVE-2026-58011, CVE-2026-58012, CVE-2026-58013, CVE-2026-58014, CVE-2026-58015, RHSA-2026:57610, CVE-2026-72693, RHSA-2026:51035, CVE-2026-23415, CVE-2026-43450, RHSA-2026:52674, CVE-2026-14164, RHSA-2026:54662, CVE-2026-58055, RHSA-2026:54484, and CVE-2026-45409.


RHEL 9 (Satellite) 5.14.0-687.39.1.el9_8
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-687.39.1.el9_8
:   Resolves the following CVEs: RHSA-2026:54510, CVE-2026-10723, CVE-2026-11331, CVE-2026-11622, CVE-2026-11721, CVE-2026-13204, CVE-2026-13321, RHSA-2026:55439, CVE-2026-1965, CVE-2026-3783, CVE-2026-8286, CVE-2026-9547, RHSA-2026:54571, CVE-2026-15816, RHSA-2026:55772, CVE-2026-55203, CVE-2026-55204, RHSA-2026:53844, CVE-2026-44943, CVE-2026-44944, RHSA-2026:53847, CVE-2026-55995, RHSA-2026:53329, CVE-2025-54518, CVE-2026-31530, CVE-2026-64368, CVE-2026-64531, RHSA-2026:54443, CVE-2026-53202, CVE-2026-53264, RHSA-2026:54268, CVE-2026-11940, RHSA-2026:55440, CVE-2026-15588, CVE-2026-58010, CVE-2026-58011, CVE-2026-58012, CVE-2026-58013, CVE-2026-58014, CVE-2026-58015, RHSA-2026:57610, CVE-2026-72693, RHSA-2026:51035, CVE-2026-23415, CVE-2026-43450, RHSA-2026:52674, CVE-2026-14164, RHSA-2026:54662, CVE-2026-58055, RHSA-2026:54484, and CVE-2026-45409.


RHEL 8 (VPC) 4.18.0-553.156.1.el8_10
:   Resolves the following CVEs: RHSA-2026:54654, CVE-2026-10723, CVE-2026-11622, CVE-2026-11721, CVE-2026-13204, CVE-2026-13321, RHSA-2026:57462, CVE-2026-8286, RHSA-2026:54575, CVE-2026-15816, RHSA-2026:55859, CVE-2026-55204, RHSA-2026:53848, CVE-2026-55995, RHSA-2026:50978, CVE-2025-54518, RHSA-2026:55764, CVE-2025-39902, CVE-2026-17523, CVE-2026-43206, CVE-2026-53016, CVE-2026-53136, CVE-2026-53329, CVE-2026-53374, CVE-2026-63879, CVE-2026-63884, CVE-2026-64219, RHSA-2026:57253, CVE-2024-56602, CVE-2026-46120, CVE-2026-52991, CVE-2026-53189, CVE-2026-63887, CVE-2026-63888, CVE-2026-64048, CVE-2026-64379, CVE-2026-68388, RHSA-2026:56219, CVE-2026-11940, RHSA-2026:56130, CVE-2026-16313, RHSA-2026:55784, CVE-2026-44690, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:56133, CVE-2026-54371, RHSA-2026:52765, CVE-2026-64496, RHSA-2026:54246, CVE-2026-45991, CVE-2026-53009, RHSA-2026:55804, CVE-2026-58055, RHSA-2026:56131, CVE-2026-54411, RHSA-2026:54290, and CVE-2026-45409.


RHEL 8 (Classic) 4.18.0-553.156.1.el8_10
:   Resolves the following CVEs: RHSA-2026:54654, CVE-2026-10723, CVE-2026-11622, CVE-2026-11721, CVE-2026-13204, CVE-2026-13321, RHSA-2026:57462, CVE-2026-8286, RHSA-2026:54575, CVE-2026-15816, RHSA-2026:55859, CVE-2026-55204, RHSA-2026:53848, CVE-2026-55995, RHSA-2026:50978, CVE-2025-54518, RHSA-2026:55764, CVE-2025-39902, CVE-2026-17523, CVE-2026-43206, CVE-2026-53016, CVE-2026-53136, CVE-2026-53329, CVE-2026-53374, CVE-2026-63879, CVE-2026-63884, CVE-2026-64219, RHSA-2026:57253, CVE-2024-56602, CVE-2026-46120, CVE-2026-52991, CVE-2026-53189, CVE-2026-63887, CVE-2026-63888, CVE-2026-64048, CVE-2026-64379, CVE-2026-68388, RHSA-2026:56219, CVE-2026-11940, RHSA-2026:56130, CVE-2026-16313, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:56133, CVE-2026-54371, RHSA-2026:52765, CVE-2026-64496, RHSA-2026:54246, CVE-2026-45991, CVE-2026-53009, RHSA-2026:55804, CVE-2026-58055, RHSA-2026:56131, CVE-2026-54411, RHSA-2026:54290, and CVE-2026-45409.


Red Hat OpenShift 4.16.68
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-68_release-notes){: external}.


Red Hat CoreOS 4.16.68
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-68_release-notes){: external}.


HAProxy a70e8a8452c4d476687ad749df47b6f27a61851a
:   Resolves the following CVEs: CVE-2026-54411, CVE-2026-54371, CVE-2026-55204, and CVE-2026-58055.


## 12 August 2026, Worker node fix pack 4.16.67_1628_openshift
{: #cl-boms-41667_1628_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.67_1628_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-687.34.1.el9_8
:   Resolves the following CVEs: RHSA-2026:44385, CVE-2024-46738, CVE-2024-50076, CVE-2025-39982, CVE-2026-31488, CVE-2026-31613, CVE-2026-31684, CVE-2026-46116, CVE-2026-46209, RHSA-2026:49031, CVE-2025-10263, CVE-2025-40026, CVE-2026-52923, RHSA-2026:49839, CVE-2026-14474, CVE-2026-14476, RHSA-2026:48811, CVE-2026-48864, RHSA-2026:49910, and CVE-2026-29111.


RHEL 9 (Satellite) 5.14.0-687.34.1.el9_8
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-687.34.1.el9_8
:   Resolves the following CVEs: RHSA-2026:44385, CVE-2024-46738, CVE-2024-50076, CVE-2025-39982, CVE-2026-31488, CVE-2026-31613, CVE-2026-31684, CVE-2026-46116, CVE-2026-46209, RHSA-2026:49031, CVE-2025-10263, CVE-2025-40026, CVE-2026-52923, RHSA-2026:49839, CVE-2026-14474, CVE-2026-14476, RHSA-2026:48811, CVE-2026-48864, RHSA-2026:49910, and CVE-2026-29111.


RHEL 8 (VPC) 4.18.0-553.151.1.el8_10
:   Resolves the following CVEs: CVE-2026-56392, RHSA-2026:45115, CVE-2025-40026, CVE-2026-52993, CVE-2026-53059, RHSA-2026:47011, CVE-2026-53006, RHSA-2026:49214, CVE-2026-31692, CVE-2026-43116, CVE-2026-46150, CVE-2026-64530, RHSA-2026:42552, CVE-2026-46117, CVE-2026-53071, RHSA-2026:50978, CVE-2025-54518, RHSA-2026:46990, CVE-2026-14474, CVE-2026-14476, RHSA-2026:48703, CVE-2026-55693, CVE-2026-57455, CVE-2026-57456, CVE-2026-59858, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:49857, CVE-2026-52923, RHSA-2026:47117, CVE-2026-41989, RHSA-2026:47755, CVE-2026-55653, and CVE-2026-55655.


RHEL 8 (Classic) 4.18.0-553.151.1.el8_10
:   Resolves the following CVEs: CVE-2026-56392, RHSA-2026:45115, CVE-2025-40026, CVE-2026-52993, CVE-2026-53059, RHSA-2026:47011, CVE-2026-53006, RHSA-2026:49214, CVE-2026-31692, CVE-2026-43116, CVE-2026-46150, CVE-2026-64530, RHSA-2026:42552, CVE-2026-46117, CVE-2026-53071, RHSA-2026:50978, CVE-2025-54518, RHSA-2026:46990, CVE-2026-14474, CVE-2026-14476, RHSA-2026:48703, CVE-2026-55693, CVE-2026-57455, CVE-2026-57456, CVE-2026-59858, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:49857, CVE-2026-52923, RHSA-2026:47117, CVE-2026-41989, RHSA-2026:47755, CVE-2026-55653, and CVE-2026-55655.


Red Hat OpenShift 4.16.67
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-67_release-notes){: external}.


Red Hat CoreOS 4.16.67
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-67_release-notes){: external}.


HAProxy bd7e64ef86b90455535107263466d1825f3e7f9f
:   Resolves the following CVEs: CVE-2026-56391, and CVE-2026-56392.


## 07 August 2026, Master fix pack 4.16.68_1627_openshift
{: #cl-boms_master-41668_1627_openshift_M}

The following list shows the components that are in the master fix pack 4.16.68_1627_openshift. Master patch updates are applied automatically.
{: shortdesc}

etcd v3.5.32
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.32){: external}.


IBM Cloud Block Storage driver and plug-in v2.5.27
:   New version contains updates and security fixes.


IBM Cloud Controller Manager v1.29.15-63
:   New version contains updates and security fixes.


IBM Cloud File Storage for Classic plug-in and monitor v456
:   New version contains updates and security fixes.


Key Management Service provider 2.10.28
:   New version contains updates and security fixes.


Red Hat OpenShift on IBM Cloud 4.16.68
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-68_release-notes){: external}.Resolves the following CVEs: CVE-2026-16242.


## 28 July 2026, Worker node fix pack 4.16.66_1626_openshift
{: #cl-boms-41666_1626_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.66_1626_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.128.1.el9_6
:   Resolves the following CVEs: RHSA-2026:38902, CVE-2025-68183, CVE-2026-31408, CVE-2026-43074, CVE-2026-43279, CVE-2026-45984, CVE-2026-46135, CVE-2026-46152, CVE-2026-46189, CVE-2026-46242, CVE-2026-46316, CVE-2026-53359, RHSA-2026:44385, CVE-2024-46738, CVE-2024-50076, CVE-2025-39982, CVE-2026-31488, CVE-2026-31613, CVE-2026-31684, CVE-2026-46116, CVE-2026-46209, RHSA-2026:40425, CVE-2026-43499, CVE-2026-53166, and CVE-2026-64600.


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-570.128.1.el9_6
:   Resolves the following CVEs: RHSA-2026:38902, CVE-2025-68183, CVE-2026-31408, CVE-2026-43074, CVE-2026-43279, CVE-2026-45984, CVE-2026-46135, CVE-2026-46152, CVE-2026-46189, CVE-2026-46242, CVE-2026-46316, CVE-2026-53359, RHSA-2026:44385, CVE-2024-46738, CVE-2024-50076, CVE-2025-39982, CVE-2026-31488, CVE-2026-31613, CVE-2026-31684, CVE-2026-46116, CVE-2026-46209, RHSA-2026:40425, CVE-2026-43499, CVE-2026-53166, and CVE-2026-64600.


RHEL 8 (VPC) 4.18.0-553.144.1.el8_10
:   Resolves the following CVEs: RHSA-2026:43420, CVE-2026-54369, CVE-2026-54370, RHSA-2026:38504, CVE-2026-33811, CVE-2026-39835, CVE-2026-57231, RHSA-2026:42090, CVE-2026-58016, RHSA-2026:36366, CVE-2026-43112, RHSA-2026:39179, CVE-2026-46086, CVE-2026-46116, CVE-2026-64600, RHSA-2026:36349, CVE-2025-10263, CVE-2026-43198, CVE-2026-43450, CVE-2026-46209, CVE-2026-46227, CVE-2026-46259, RHSA-2026:42552, CVE-2026-46117, CVE-2026-53071, RHSA-2026:39083, CVE-2025-71066, CVE-2025-71089, CVE-2026-31411, CVE-2026-43499, CVE-2026-46113, CVE-2026-53166, CVE-2026-53266, CVE-2026-53359, RHSA-2026:39320, CVE-2026-15308, RHSA-2026:41930, CVE-2026-27145, CVE-2026-39821, RHSA-2026:38510, CVE-2026-46483, CVE-2026-47162, CVE-2026-47167, CVE-2026-52858, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:42733, CVE-2026-5435, CVE-2026-5928, CVE-2026-6238, RHSA-2026:38503, and CVE-2026-28390.


RHEL 8 (Classic) 4.18.0-553.144.1.el8_10
:   Resolves the following CVEs: RHSA-2026:43420, CVE-2026-54369, CVE-2026-54370, RHSA-2026:38504, CVE-2026-33811, CVE-2026-39835, CVE-2026-57231, RHSA-2026:42090, CVE-2026-58016, RHSA-2026:36366, CVE-2026-43112, RHSA-2026:39179, CVE-2026-46086, CVE-2026-46116, CVE-2026-64600, RHSA-2026:36349, CVE-2025-10263, CVE-2026-43198, CVE-2026-43450, CVE-2026-46209, CVE-2026-46227, CVE-2026-46259, RHSA-2026:42552, CVE-2026-46117, CVE-2026-53071, RHSA-2026:39083, CVE-2025-71066, CVE-2025-71089, CVE-2026-31411, CVE-2026-43499, CVE-2026-46113, CVE-2026-53166, CVE-2026-53266, CVE-2026-53359, RHSA-2026:39320, CVE-2026-15308, RHSA-2026:41930, CVE-2026-27145, CVE-2026-39821, RHSA-2026:38510, CVE-2026-46483, CVE-2026-47162, CVE-2026-47167, CVE-2026-52858, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:42733, CVE-2026-5435, CVE-2026-5928, CVE-2026-6238, RHSA-2026:38503, and CVE-2026-28390.


Red Hat OpenShift 4.16.66
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-66_release-notes){: external}.


Red Hat CoreOS 4.16.66
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-66_release-notes){: external}.


HAProxy 346c7130717ef7cc25d1dfbca7d57ca32396b692
:   Resolves the following CVEs: CVE-2026-6238, CVE-2026-5928, CVE-2026-48864, CVE-2026-54370, CVE-2026-28390, CVE-2026-5435, CVE-2025-13151, CVE-2026-54369, CVE-2026-58016, and CVE-2025-6170.


## 28 July 2026, Master fix pack 4.16.64_1624_openshift
{: #cl-boms_master-41664_1624_openshift_M}

The following list shows the components that are in the master fix pack 4.16.64_1624_openshift. Master patch updates are applied automatically.
{: shortdesc}

Calico v3.30.7
:   See the [Calico release notes](https://docs.tigera.io/calico/3.30/release-notes/#calico-open-source-3307-bug-fix-release){: external}.


Cluster health image v1.6.17
:   New version contains updates and security fixes.


etcd v3.5.30
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.30){: external}.


IBM Cloud Block Storage driver and plug-in v2.5.26
:   New version contains updates and security fixes.


IBM Cloud Controller Manager v1.29.15-61
:   New version contains updates and security fixes.


IBM Cloud File Storage for Classic plug-in and monitor v455
:   New version contains updates and security fixes.


IBM Cloud RBAC Operator 92ba7dd
:   New version contains updates and security fixes.


Key Management Service provider 2.10.27
:   New version contains updates and security fixes.


Portieris admission controller v0.14.2
:   See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.14.2){: external}


Red Hat OpenShift on IBM Cloud 4.16.64
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-64_release-notes){: external}.


Red Hat OpenShift on IBM Cloud Control Plane Operator, Metrics Server, and toolkit v4.16.0+20260707
:   See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.16.0+20260707){: external}.


Tigera Operator v1.38.13
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.38.13){: external}.


## 13 July 2026, Worker node fix pack 4.16.65_1625_openshift
{: #cl-boms-41665_1625_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.65_1625_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.125.1.el9_6
:   Resolves the following CVEs: RHSA-2026:30004, CVE-2026-33845, CVE-2026-33846, CVE-2026-3833, CVE-2026-42009, CVE-2026-42010, CVE-2026-42011, CVE-2026-42012, CVE-2026-42013, CVE-2026-42014, CVE-2026-42015, CVE-2026-5260, CVE-2026-5419, RHSA-2026:34094, CVE-2025-21648, CVE-2025-21691, CVE-2026-23191, CVE-2026-31669, CVE-2026-43027, CVE-2026-43125, CVE-2026-43128, CVE-2026-43198, CVE-2026-43329, CVE-2026-43414, CVE-2026-43501, CVE-2026-45852, CVE-2026-46090, CVE-2026-46173, CVE-2026-46176, CVE-2026-46181, CVE-2026-46227, CVE-2026-46244, RHSA-2026:28147, CVE-2026-28847, CVE-2026-28883, CVE-2026-28901, CVE-2026-28902, CVE-2026-28903, CVE-2026-28904, CVE-2026-28905, CVE-2026-28907, CVE-2026-28942, CVE-2026-28946, CVE-2026-28947, CVE-2026-28953, CVE-2026-28955, CVE-2026-28958, CVE-2026-43658, CVE-2026-43660, RHSA-2026:33634, CVE-2024-34459, RHSA-2026:33230, CVE-2026-5450, RHSA-2026:28832, and CVE-2026-31790.


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-570.125.1.el9_6
:   Resolves the following CVEs: RHSA-2026:30004, CVE-2026-33845, CVE-2026-33846, CVE-2026-3833, CVE-2026-42009, CVE-2026-42010, CVE-2026-42011, CVE-2026-42012, CVE-2026-42013, CVE-2026-42014, CVE-2026-42015, CVE-2026-5260, CVE-2026-5419, RHSA-2026:34094, CVE-2025-21648, CVE-2025-21691, CVE-2026-23191, CVE-2026-31669, CVE-2026-43027, CVE-2026-43125, CVE-2026-43128, CVE-2026-43198, CVE-2026-43329, CVE-2026-43414, CVE-2026-43501, CVE-2026-45852, CVE-2026-46090, CVE-2026-46173, CVE-2026-46176, CVE-2026-46181, CVE-2026-46227, CVE-2026-46244, RHSA-2026:28147, CVE-2026-28847, CVE-2026-28883, CVE-2026-28901, CVE-2026-28902, CVE-2026-28903, CVE-2026-28904, CVE-2026-28905, CVE-2026-28907, CVE-2026-28942, CVE-2026-28946, CVE-2026-28947, CVE-2026-28953, CVE-2026-28955, CVE-2026-28958, CVE-2026-43658, CVE-2026-43660, RHSA-2026:33634, CVE-2024-34459, RHSA-2026:33230, CVE-2026-5450, RHSA-2026:28832, and CVE-2026-31790.


RHEL 8 (VPC) 4.18.0-553.139.1.el8_10
:   Resolves the following CVEs: RHSA-2026:35833, CVE-2026-34986, CVE-2026-39829, CVE-2026-39830, CVE-2026-39832, CVE-2026-42508, RHSA-2026:33722, CVE-2026-25679, CVE-2026-32280, CVE-2026-32281, CVE-2026-32283, CVE-2026-34986, RHSA-2026:33743, CVE-2026-23216, CVE-2026-45984, CVE-2026-46189, RHSA-2026:36776, CVE-2026-33811, RHSA-2026:37282, CVE-2026-40622, CVE-2026-41292, CVE-2026-42534, CVE-2026-44390, RHSA-2026:36728, CVE-2025-13151, RHSA-2026:36734, CVE-2025-6170, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:33126, CVE-2026-5450, RHSA-2026:29898, CVE-2026-33416, RHSA-2026:36730, CVE-2026-48864, RHSA-2026:36732, and CVE-2026-44431.


RHEL 8 (Classic) 4.18.0-553.139.1.el8_10
:   Resolves the following CVEs: RHSA-2026:35833, CVE-2026-34986, CVE-2026-39829, CVE-2026-39830, CVE-2026-39832, CVE-2026-42508, RHSA-2026:33722, CVE-2026-25679, CVE-2026-32280, CVE-2026-32281, CVE-2026-32283, CVE-2026-34986, RHSA-2026:33743, CVE-2026-23216, CVE-2026-45984, CVE-2026-46189, RHSA-2026:36776, CVE-2026-33811, RHSA-2026:37282, CVE-2026-40622, CVE-2026-41292, CVE-2026-42534, CVE-2026-44390, RHSA-2026:36728, CVE-2025-13151, RHSA-2026:36734, CVE-2025-6170, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:33126, CVE-2026-5450, RHSA-2026:29898, CVE-2026-33416, RHSA-2026:36730, CVE-2026-48864, RHSA-2026:36732, and CVE-2026-44431.


Red Hat OpenShift 4.16.65
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-65_release-notes){: external}.


Red Hat CoreOS 4.16.65
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-65_release-notes){: external}.


HAProxy 27f76d0c7626993cde6e1ff90fa42253718cc5fa
:   Resolves the following CVEs: CVE-2026-5450.


## 01 July 2026, Worker node fix pack 4.16.64_1622_openshift
{: #cl-boms-41664_1622_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.64_1622_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.123.1.el9_6
:   Resolves the following CVEs: RHSA-2026:24500, CVE-2026-1519, RHSA-2026:23224, CVE-2025-38653, CVE-2025-39766, CVE-2025-68366, CVE-2026-23210, CVE-2026-23270, CVE-2026-23392, CVE-2026-31419, CVE-2026-31607, CVE-2026-31685, CVE-2026-31709, CVE-2026-43037, CVE-2026-43038, CVE-2026-43163, RHSA-2026:25218, CVE-2025-40135, CVE-2025-40158, CVE-2025-40170, CVE-2025-68724, CVE-2025-71089, CVE-2025-71116, CVE-2026-22984, CVE-2026-22990, CVE-2026-23216, CVE-2026-23455, CVE-2026-31508, CVE-2026-43110, CVE-2026-43190, RHSA-2026:27708, CVE-2025-40064, CVE-2025-40168, CVE-2026-23136, CVE-2026-43116, CVE-2026-43158, CVE-2026-43303, CVE-2026-45898, CVE-2026-46125, CVE-2026-46166, CVE-2026-46243, CVE-2026-46323, CVE-2026-46331, RHSA-2026:24683, CVE-2026-40356, RHSA-2026:24337, CVE-2026-32280, CVE-2026-32281, CVE-2026-32282, CVE-2026-32283, RHSA-2026:25979, CVE-2026-1933, CVE-2026-2340, CVE-2026-3012, CVE-2026-4408, CVE-2026-4480, RHSA-2026:28050, CVE-2026-34982, CVE-2026-35177, CVE-2026-41411, and CVE-2026-46483.


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-570.123.1.el9_6
:   Resolves the following CVEs: RHSA-2026:24500, CVE-2026-1519, RHSA-2026:23224, CVE-2025-38653, CVE-2025-39766, CVE-2025-68366, CVE-2026-23210, CVE-2026-23270, CVE-2026-23392, CVE-2026-31419, CVE-2026-31607, CVE-2026-31685, CVE-2026-31709, CVE-2026-43037, CVE-2026-43038, CVE-2026-43163, RHSA-2026:25218, CVE-2025-40135, CVE-2025-40158, CVE-2025-40170, CVE-2025-68724, CVE-2025-71089, CVE-2025-71116, CVE-2026-22984, CVE-2026-22990, CVE-2026-23216, CVE-2026-23455, CVE-2026-31508, CVE-2026-43110, CVE-2026-43190, RHSA-2026:27708, CVE-2025-40064, CVE-2025-40168, CVE-2026-23136, CVE-2026-43116, CVE-2026-43158, CVE-2026-43303, CVE-2026-45898, CVE-2026-46125, CVE-2026-46166, CVE-2026-46243, CVE-2026-46323, CVE-2026-46331, RHSA-2026:24683, CVE-2026-40356, RHSA-2026:24337, CVE-2026-32280, CVE-2026-32281, CVE-2026-32282, CVE-2026-32283, RHSA-2026:25979, CVE-2026-1933, CVE-2026-2340, CVE-2026-3012, CVE-2026-4408, CVE-2026-4480, RHSA-2026:28050, CVE-2026-34982, CVE-2026-35177, CVE-2026-41411, and CVE-2026-46483.


RHEL 8 (VPC) 4.18.0-553.137.1.el8_10
:   Resolves the following CVEs: RHSA-2026:25121, CVE-2023-53781, CVE-2025-21858, CVE-2025-68366, CVE-2026-22984, CVE-2026-22990, CVE-2026-23392, CVE-2026-31581, CVE-2026-31613, CVE-2026-43037, CVE-2026-43038, CVE-2026-43125, CVE-2026-45852, CVE-2026-46181, RHSA-2026:26534, CVE-2026-6893, RHSA-2026:26427, CVE-2026-31669, CVE-2026-31786, CVE-2026-31787, CVE-2026-43110, CVE-2026-43329, CVE-2026-46056, CVE-2026-46125, CVE-2026-46152, RHSA-2026:27811, CVE-2026-46054, RHSA-2026:27353, CVE-2026-31419, CVE-2026-31488, CVE-2026-43056, CVE-2026-43279, CVE-2026-46090, CVE-2026-46135, CVE-2026-46145, CVE-2026-46331, RHSA-2026:26275, CVE-2024-4741, CVE-2026-45447, RHSA-2026:26408, CVE-2026-29518, CVE-2026-43618, RHSA-2026:26354, CVE-2024-34459, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:29898, CVE-2026-33416, RHSA-2026:28553, and CVE-2026-41411.


RHEL 8 (Classic) 4.18.0-553.137.1.el8_10
:   Resolves the following CVEs: RHSA-2026:25121, CVE-2023-53781, CVE-2025-21858, CVE-2025-68366, CVE-2026-22984, CVE-2026-22990, CVE-2026-23392, CVE-2026-31581, CVE-2026-31613, CVE-2026-43037, CVE-2026-43038, CVE-2026-43125, CVE-2026-45852, CVE-2026-46181, RHSA-2026:26534, CVE-2026-6893, RHSA-2026:26427, CVE-2026-31669, CVE-2026-31786, CVE-2026-31787, CVE-2026-43110, CVE-2026-43329, CVE-2026-46056, CVE-2026-46125, CVE-2026-46152, RHSA-2026:27811, CVE-2026-46054, RHSA-2026:27353, CVE-2026-31419, CVE-2026-31488, CVE-2026-43056, CVE-2026-43279, CVE-2026-46090, CVE-2026-46135, CVE-2026-46145, CVE-2026-46331, RHSA-2026:26275, CVE-2024-4741, CVE-2026-45447, RHSA-2026:26408, CVE-2026-29518, CVE-2026-43618, RHSA-2026:26354, CVE-2024-34459, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:29898, CVE-2026-33416, RHSA-2026:28553, and CVE-2026-41411.


Red Hat OpenShift 4.16.64
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-64_release-notes){: external}.


Red Hat CoreOS 4.16.64
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-64_release-notes){: external}.


HAProxy 119de539a7da3c92449b38e1531722802988e50c
:   Resolves the following CVEs: CVE-2026-45447, CVE-2024-4741, and CVE-2024-34459.


## 26 June 2026, Master fix pack 4.16.63_1620_openshift
{: #cl-boms_master-41663_1620_openshift_M}

The following list shows the components that are in the master fix pack 4.16.63_1620_openshift. Master patch updates are applied automatically.
{: shortdesc}

Calico v3.30.7
:   See the [Calico release notes](https://docs.tigera.io/calico/3.30/release-notes/#calico-open-source-3307-bug-fix-release){: external}.


Cluster health image v1.6.16
:   New version contains updates and security fixes.


etcd v3.5.30
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.30){: external}.


IBM Cloud Block Storage driver and plug-in v2.5.26
:   New version contains updates and security fixes.


IBM Cloud Controller Manager v1.29.15-56
:   New version contains updates and security fixes.


IBM Cloud File Storage for Classic plug-in and monitor v455
:   New version contains updates and security fixes.


Key Management Service provider 2.10.25
:   New version contains updates and security fixes.


Portieris admission controller v0.14.0
:   See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.14.0){: external}


Red Hat OpenShift on IBM Cloud 4.16.63
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-63_release-notes){: external}.


Red Hat OpenShift on IBM Cloud Control Plane Operator, Metrics Server, and toolkit v4.16.0+20260601
:   See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.16.0+20260601){: external}.


Tigera Operator v1.38.13
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.38.13){: external}.


## 15 June 2026, Worker node fix pack 4.16.63_1621_openshift
{: #cl-boms-41663_1621_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.63_1621_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.116.1.el9_6
:   Resolves the following CVEs: CVE-2026-5119.


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-570.116.1.el9_6
:   


RHEL 8 (VPC) 4.18.0-553.129.1.el8_10
:   Resolves the following CVEs: RHSA-2026:25121, CVE-2023-53781, CVE-2025-21858, CVE-2025-68366, CVE-2026-22984, CVE-2026-22990, CVE-2026-23392, CVE-2026-31581, CVE-2026-31613, CVE-2026-43037, CVE-2026-43038, CVE-2026-43125, CVE-2026-45852, CVE-2026-46181, RHSA-2026:24339, CVE-2026-3039, CVE-2026-5946, RHSA-2026:22721, CVE-2026-45186, RHSA-2026:21706, CVE-2025-39981, CVE-2025-68183, CVE-2025-68347, CVE-2025-71116, CVE-2026-23243, CVE-2026-23270, CVE-2026-23455, CVE-2026-31408, CVE-2026-31532, CVE-2026-31684, CVE-2026-31685, CVE-2026-31709, CVE-2026-43020, CVE-2026-43027, CVE-2026-43051, CVE-2026-43158, CVE-2026-43163, CVE-2026-43190, RHSA-2026:23258, CVE-2026-46243, RHSA-2026:24365, CVE-2026-42944, CVE-2026-42959, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:22730, and CVE-2026-35177.


RHEL 8 (Classic) 4.18.0-553.129.1.el8_10
:   Resolves the following CVEs: RHSA-2026:25121, CVE-2023-53781, CVE-2025-21858, CVE-2025-68366, CVE-2026-22984, CVE-2026-22990, CVE-2026-23392, CVE-2026-31581, CVE-2026-31613, CVE-2026-43037, CVE-2026-43038, CVE-2026-43125, CVE-2026-45852, CVE-2026-46181, RHSA-2026:24339, CVE-2026-3039, CVE-2026-5946, RHSA-2026:22721, CVE-2026-45186, RHSA-2026:21706, CVE-2025-39981, CVE-2025-68183, CVE-2025-68347, CVE-2025-71116, CVE-2026-23243, CVE-2026-23270, CVE-2026-23455, CVE-2026-31408, CVE-2026-31532, CVE-2026-31684, CVE-2026-31685, CVE-2026-31709, CVE-2026-43020, CVE-2026-43027, CVE-2026-43051, CVE-2026-43158, CVE-2026-43163, CVE-2026-43190, RHSA-2026:23258, CVE-2026-46243, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:22730, and CVE-2026-35177.


Red Hat OpenShift 4.16.63
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-62_release-notes){: external}.


Red Hat CoreOS 4.16.63
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-62_release-notes){: external}.


HAProxy d4656f400ca14059e1b5b8ef8078b4903290791a
:   Resolves the following CVEs: CVE-2026-45186.


## 03 June 2026, Worker node fix pack 4.16.62_1619_openshift
{: #cl-boms-41662_1619_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.62_1619_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.116.1.el9_6
:   Resolves the following CVEs: RHSA-2026:21392, CVE-2026-4802, RHSA-2026:18042, CVE-2026-39979, CVE-2026-40164, RHSA-2026:16312, CVE-2026-43284, RHSA-2026:20129, CVE-2026-46300, CVE-2026-46333, RHSA-2026:19458, CVE-2026-4878, RHSA-2026:18031, CVE-2026-41651, RHSA-2026:19576, CVE-2026-4786, CVE-2026-6100, RHSA-2026:20603, CVE-2024-12086, CVE-2025-10158, CVE-2026-41035, RHSA-2026:19457, CVE-2025-14087, CVE-2025-14512, RHSA-2026:20548, and CVE-2026-33416.


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-570.116.1.el9_6
:   Resolves the following CVEs: RHSA-2026:18042, CVE-2026-39979, CVE-2026-40164, RHSA-2026:16312, CVE-2026-43284, RHSA-2026:20129, CVE-2026-46300, CVE-2026-46333, RHSA-2026:19458, CVE-2026-4878, RHSA-2026:19576, CVE-2026-4786, CVE-2026-6100, RHSA-2026:19457, CVE-2025-14087, CVE-2025-14512, RHSA-2026:20548, and CVE-2026-33416.


RHEL 8 (VPC) 4.18.0-553.125.1.el8_10
:   Resolves the following CVEs: RHSA-2026:21700, CVE-2026-4802, RHSA-2026:20611, CVE-2026-33845, CVE-2026-33846, CVE-2026-3833, CVE-2026-42009, CVE-2026-42010, CVE-2026-42011, CVE-2026-42012, CVE-2026-42013, CVE-2026-42014, CVE-2026-42015, CVE-2026-5260, RHSA-2026:16195, CVE-2026-43284, RHSA-2026:19666, CVE-2026-46300, CVE-2026-46333, RHSA-2026:21706, CVE-2025-39981, CVE-2025-68183, CVE-2025-68347, CVE-2025-71116, CVE-2026-23243, CVE-2026-23270, CVE-2026-23455, CVE-2026-31408, CVE-2026-31532, CVE-2026-31684, CVE-2026-31685, CVE-2026-31709, CVE-2026-43020, CVE-2026-43027, CVE-2026-43051, CVE-2026-43158, CVE-2026-43163, CVE-2026-43190, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:20587, and CVE-2026-4046.


RHEL 8 (Classic) 4.18.0-553.125.1.el8_10
:   Resolves the following CVEs: RHSA-2026:20611, CVE-2026-33845, CVE-2026-33846, CVE-2026-3833, CVE-2026-42009, CVE-2026-42010, CVE-2026-42011, CVE-2026-42012, CVE-2026-42013, CVE-2026-42014, CVE-2026-42015, CVE-2026-5260, RHSA-2026:16195, CVE-2026-43284, RHSA-2026:19666, CVE-2026-46300, CVE-2026-46333, RHSA-2026:21706, CVE-2025-39981, CVE-2025-68183, CVE-2025-68347, CVE-2025-71116, CVE-2026-23243, CVE-2026-23270, CVE-2026-23455, CVE-2026-31408, CVE-2026-31532, CVE-2026-31684, CVE-2026-31685, CVE-2026-31709, CVE-2026-43020, CVE-2026-43027, CVE-2026-43051, CVE-2026-43158, CVE-2026-43163, CVE-2026-43190, RHSA-2026:20587, and CVE-2026-4046.


Red Hat OpenShift 4.16.62
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-62_release-notes){: external}.


Red Hat CoreOS 4.16.62
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-62_release-notes){: external}.


HAProxy 0e0730588ba21878845cdb0bee615a371a489a02
:   Resolves the following CVEs: CVE-2026-4046, CVE-2026-33846, CVE-2026-42010, CVE-2026-5260, CVE-2026-42014, CVE-2026-3833, CVE-2026-42015, CVE-2026-33845, CVE-2026-42011, CVE-2026-42009, CVE-2026-42013, and CVE-2026-42012.


## 22 May 2026, Master fix pack 4.16.61_1617_openshift
{: #cl-boms_master-41661_1617_openshift_M}

The following list shows the components that are in the master fix pack 4.16.61_1617_openshift. Master patch updates are applied automatically.
{: shortdesc}

IBM Cloud Controller Manager v1.29.15-54
:   New version contains updates and security fixes.


Key Management Service provider 2.10.24
:   New version contains updates and security fixes.


Portieris admission controller v0.13.38
:   See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.13.38){: external}


Red Hat OpenShift on IBM Cloud 4.16.61
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-61_release-notes){: external}.


## 20 May 2026, Worker node fix pack 4.16.62_1618_openshift
{: #cl-boms-41662_1618_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.62_1618_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) [5.14.0-570.112.1.el9_6](/docs/openshift?topic=openshift-openshift-relnotes#openshift-may2126)
:   Resolves the following CVEs: RHSA-2025:22392, CVE-2025-38724, CVE-2025-39864, CVE-2025-39881, CVE-2025-39883, CVE-2025-39918, CVE-2025-39955, CVE-2025-40186, RHSA-2026:0457, CVE-2025-23142, CVE-2025-39806, CVE-2025-39981, CVE-2025-39983, CVE-2025-40176, CVE-2025-68287, RHSA-2026:0804, CVE-2025-21795, CVE-2025-37849, CVE-2025-37891, CVE-2025-39697, CVE-2025-40154, CVE-2025-68285, RHSA-2026:14339, CVE-2024-53216, CVE-2025-68741, CVE-2026-23243, CVE-2026-23401, CVE-2026-31431, CVE-2026-31532, CVE-2026-43077, RHSA-2026:16312, CVE-2026-43284, RHSA-2026:1703, CVE-2025-21863, CVE-2025-40248, CVE-2025-68301, RHSA-2026:16059, CVE-2026-35385, CVE-2026-35386, CVE-2026-35387, CVE-2026-35388, CVE-2026-35414, RHSA-2026:13889, CVE-2026-35535, RHSA-2025:21563, CVE-2024-56690, RHSA-2025:21933, CVE-2025-39898, CVE-2025-39971, CVE-2025-39973, CVE-2025-40047, RHSA-2025:22802, CVE-2025-39966, RHSA-2025:23789, CVE-2025-39843, CVE-2025-39925, RHSA-2026:11313, CVE-2026-23097, CVE-2026-31402, RHSA-2026:1194, CVE-2023-53034, CVE-2025-37761, CVE-2025-37789, CVE-2025-37819, CVE-2025-37869, CVE-2025-38289, CVE-2025-40141, CVE-2025-40251, CVE-2025-40258, CVE-2025-40277, CVE-2025-40318, RHSA-2026:2352, CVE-2024-54456, CVE-2025-21647, CVE-2025-21786, CVE-2025-21791, CVE-2025-38022, CVE-2025-38051, CVE-2025-38568, CVE-2025-40294, CVE-2025-40322, CVE-2025-68349, RHSA-2026:2759, CVE-2025-37882, CVE-2025-38349, CVE-2025-38730, CVE-2025-39760, CVE-2025-39933, CVE-2025-40269, CVE-2025-40271, CVE-2025-40304, RHSA-2026:3088, CVE-2025-37861, CVE-2025-38106, CVE-2025-38415, RHSA-2026:3520, CVE-2025-38154, RHSA-2026:4011, CVE-2024-47727, CVE-2024-56603, CVE-2025-22056, CVE-2025-38024, CVE-2025-38129, CVE-2025-38141, CVE-2025-38703, RHSA-2026:4745, CVE-2024-53229, CVE-2025-38206, CVE-2025-40240, CVE-2025-68811, CVE-2025-71085, RHSA-2026:5197, CVE-2025-38248, CVE-2026-23001, RHSA-2026:6164, CVE-2024-56645, CVE-2025-40096, CVE-2025-68800, CVE-2026-23209, RHSA-2026:6940, CVE-2025-38180, CVE-2026-23231, RHSA-2026:9112, CVE-2026-23066, CVE-2026-23111, CVE-2026-23144, CVE-2026-23171, CVE-2026-23193, CVE-2026-23204, RHSA-2026:17524, and CVE-2026-33636.


RHEL 9 (Classic) 5.14.0-570.112.1.el9_6
:   Resolves the following CVEs: RHSA-2026:2229, CVE-2025-6176, RHSA-2025:21773, CVE-2025-59375, RHSA-2026:1229, CVE-2025-68973, RHSA-2026:18042, CVE-2026-39979, CVE-2026-40164, RHSA-2025:22392, CVE-2025-38724, CVE-2025-39864, CVE-2025-39881, CVE-2025-39883, CVE-2025-39918, CVE-2025-39955, CVE-2025-40186, RHSA-2026:0457, CVE-2025-23142, CVE-2025-39806, CVE-2025-39981, CVE-2025-39983, CVE-2025-40176, CVE-2025-68287, RHSA-2026:0804, CVE-2025-21795, CVE-2025-37849, CVE-2025-37891, CVE-2025-39697, CVE-2025-40154, CVE-2025-68285, RHSA-2026:14339, CVE-2024-53216, CVE-2025-68741, CVE-2026-23243, CVE-2026-23401, CVE-2026-31431, CVE-2026-31532, CVE-2026-43077, RHSA-2026:16312, CVE-2026-43284, RHSA-2026:1703, CVE-2025-21863, CVE-2025-40248, CVE-2025-68301, RHSA-2026:7105, CVE-2026-4111, RHSA-2026:8866, CVE-2026-4424, CVE-2026-5121, RHSA-2026:19458, CVE-2026-4878, RHSA-2026:0210, CVE-2025-64720, CVE-2025-65018, CVE-2025-66293, RHSA-2026:3576, CVE-2026-22695, CVE-2026-22801, CVE-2026-25646, RHSA-2026:8548, CVE-2026-27135, RHSA-2026:16059, CVE-2026-35385, CVE-2026-35386, CVE-2026-35387, CVE-2026-35388, CVE-2026-35414, RHSA-2026:9415, CVE-2026-3497, RHSA-2026:1503, CVE-2025-15467, CVE-2025-69419, RHSA-2026:1729, CVE-2025-66418, CVE-2025-66471, CVE-2026-21441, RHSA-2026:9354, CVE-2026-4519, RHSA-2025:21067, CVE-2025-11561, RHSA-2026:13889, CVE-2026-35535, RHSA-2026:6539, CVE-2026-25749, CVE-2026-28417, CVE-2026-28421, CVE-2026-33412, RHSA-2025:23400, CVE-2025-11083, RHSA-2025:23043, CVE-2025-9086, RHSA-2026:1465, CVE-2025-13601, RHSA-2026:19457, CVE-2025-14087, CVE-2025-14512, RHSA-2026:6630, CVE-2025-14831, RHSA-2026:4823, CVE-2025-61662, RHSA-2025:21563, CVE-2024-56690, RHSA-2025:21933, CVE-2025-39898, CVE-2025-39971, CVE-2025-39973, CVE-2025-40047, RHSA-2025:22802, CVE-2025-39966, RHSA-2025:23789, CVE-2025-39843, CVE-2025-39925, RHSA-2026:11313, CVE-2026-23097, CVE-2026-31402, RHSA-2026:1194, CVE-2023-53034, CVE-2025-37761, CVE-2025-37789, CVE-2025-37819, CVE-2025-37869, CVE-2025-38289, CVE-2025-40141, CVE-2025-40251, CVE-2025-40258, CVE-2025-40277, CVE-2025-40318, RHSA-2026:2352, CVE-2024-54456, CVE-2025-21647, CVE-2025-21786, CVE-2025-21791, CVE-2025-38022, CVE-2025-38051, CVE-2025-38568, CVE-2025-40294, CVE-2025-40322, CVE-2025-68349, RHSA-2026:2759, CVE-2025-37882, CVE-2025-38349, CVE-2025-38730, CVE-2025-39760, CVE-2025-39933, CVE-2025-40269, CVE-2025-40271, CVE-2025-40304, RHSA-2026:3088, CVE-2025-37861, CVE-2025-38106, CVE-2025-38415, RHSA-2026:3520, CVE-2025-38154, RHSA-2026:4011, CVE-2024-47727, CVE-2024-56603, CVE-2025-22056, CVE-2025-38024, CVE-2025-38129, CVE-2025-38141, CVE-2025-38703, RHSA-2026:4745, CVE-2024-53229, CVE-2025-38206, CVE-2025-40240, CVE-2025-68811, CVE-2025-71085, RHSA-2026:5197, CVE-2025-38248, CVE-2026-23001, RHSA-2026:6164, CVE-2024-56645, CVE-2025-40096, CVE-2025-68800, CVE-2026-23209, RHSA-2026:6940, CVE-2025-38180, CVE-2026-23231, RHSA-2026:9112, CVE-2026-23066, CVE-2026-23111, CVE-2026-23144, CVE-2026-23171, CVE-2026-23193, CVE-2026-23204, RHSA-2026:17524, CVE-2026-33636, RHSA-2026:0428, CVE-2025-5987, RHSA-2025:22377, CVE-2025-9714, RHSA-2026:3941, CVE-2025-12801, RHSA-2026:0693, CVE-2025-61984, CVE-2025-61985, RHSA-2025:21174, CVE-2025-9230, RHSA-2026:2275, CVE-2025-12084, RHSA-2026:5218, CVE-2025-15366, CVE-2025-15367, CVE-2026-1299, RHSA-2026:0435, and CVE-2025-45582.


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 8 (VPC) 4.18.0-553.123.1.el8_10
:   Resolves the following CVEs: RHSA-2026:16252, CVE-2026-39979, CVE-2026-40164, RHSA-2026:13577, CVE-2024-41073, CVE-2025-40252, CVE-2025-68724, CVE-2026-23401, CVE-2026-31402, CVE-2026-31431, CVE-2026-43077, RHSA-2026:16799, CVE-2026-40355, CVE-2026-40356, RHSA-2026:13285, CVE-2026-4878, RHSA-2026:13383, CVE-2026-35385, CVE-2026-35386, CVE-2026-35387, CVE-2026-35388, CVE-2026-35414, RHSA-2026:15980, CVE-2026-32280, CVE-2026-32282, CVE-2026-32283, RHSA-2026:17481, CVE-2026-41035, RHSA-2026:15953, CVE-2025-14087, CVE-2025-14512, RHSA-2026:14087, and CVE-2026-5119.


RHEL 8 (Classic) 4.18.0-553.123.1.el8_10
:   Resolves the following CVEs: RHSA-2026:16252, CVE-2026-39979, CVE-2026-40164, RHSA-2026:13577, CVE-2024-41073, CVE-2025-40252, CVE-2025-68724, CVE-2026-23401, CVE-2026-31402, CVE-2026-31431, CVE-2026-43077, RHSA-2026:16799, CVE-2026-40355, CVE-2026-40356, RHSA-2026:13285, CVE-2026-4878, RHSA-2026:13383, CVE-2026-35385, CVE-2026-35386, CVE-2026-35387, CVE-2026-35388, CVE-2026-35414, RHSA-2026:15980, CVE-2026-32280, CVE-2026-32282, CVE-2026-32283, RHSA-2026:15953, CVE-2025-14087, and CVE-2025-14512.


Red Hat OpenShift 4.16.62
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-62_release-notes){: external}.


Red Hat CoreOS 4.16.62
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-62_release-notes){: external}.


HAProxy 6ba93946d8bd08ba581321189c719ab548cadf01
:   Resolves the following CVEs: CVE-2025-9714, CVE-2026-4424, CVE-2026-40356, CVE-2025-14512, CVE-2026-4878, CVE-2026-40355, CVE-2026-5121, and CVE-2025-14087.


## 04 May 2026, Worker node fix pack 4.16.60_1614_openshift
{: #cl-boms-41660_1614_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.60_1614_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   Resolves the following CVEs: RHSA-2026:9415, CVE-2026-3497, RHSA-2026:11313, CVE-2026-23097, CVE-2026-31402, RHSA-2026:11329, CVE-2025-43213, CVE-2025-43214, CVE-2025-43457, CVE-2025-43511, CVE-2025-46299, CVE-2026-20608, CVE-2026-20635, CVE-2026-20636, CVE-2026-20643, CVE-2026-20644, CVE-2026-20652, CVE-2026-20664, CVE-2026-20665, CVE-2026-20676, CVE-2026-20691, CVE-2026-28857, CVE-2026-28859, CVE-2026-28871, and mitigates CVE-2026-31431.


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   Resolves the following CVEs: RHSA-2026:9415, CVE-2026-3497, RHSA-2026:11313, CVE-2026-23097, CVE-2026-31402, RHSA-2026:11329, CVE-2025-43213, CVE-2025-43214, CVE-2025-43457, CVE-2025-43511, CVE-2025-46299, CVE-2026-20608, CVE-2026-20635, CVE-2026-20636, CVE-2026-20643, CVE-2026-20644, CVE-2026-20652, CVE-2026-20664, CVE-2026-20665, CVE-2026-20676, CVE-2026-20691, CVE-2026-28857, CVE-2026-28859, CVE-2026-28871, and mitigates CVE-2026-31431.


RHEL 8 (VPC) 4.18.0-553.120.1.el8_10
:   Resolves the following CVEs: RHSA-2026:10741, CVE-2026-5201, RHSA-2026:9131, CVE-2025-68741, CVE-2026-23191, RHSA-2026:8534, CVE-2026-4424, CVE-2026-5121, RHSA-2026:11635, CVE-2026-41651, RHSA-2026:11077, CVE-2026-4786, CVE-2026-6100, RHSA-2026:10107, CVE-2026-33186, RHSA-2026:11521, CVE-2026-35535, RHSA-2026:11509, CVE-2026-34982, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:11349, CVE-2025-9714, and mitigates CVE-2026-31431.


RHEL 8 (Classic) 4.18.0-553.120.1.el8_10
:   Resolves the following CVEs: RHSA-2026:8352, CVE-2026-1519, RHSA-2026:9131, CVE-2025-68741, CVE-2026-23191, RHSA-2026:8534, CVE-2026-4424, CVE-2026-5121, RHSA-2026:7667, CVE-2026-27135, RHSA-2026:11077, CVE-2026-4786, CVE-2026-6100, RHSA-2026:10107, CVE-2026-33186, RHSA-2026:7674, CVE-2026-25679, RHSA-2026:11521, CVE-2026-35535, RHSA-2026:11509, CVE-2026-34982, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:11349, CVE-2025-9714, and mitigates CVE-2026-31431.


Red Hat OpenShift 4.16.60
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-60_release-notes){: external}.


Red Hat CoreOS 4.16.60
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-60_release-notes){: external}. Includes mitigation for CVE-2026-31431.


HAProxy c7e825675cbd75e8433801c99f8aca3b207a5a46
:   Resolves the following CVEs: CVE-2026-5121, CVE-2025-9714, and CVE-2026-4424.


## 27 April 2026, Master fix pack 4.16.59_1613_openshift
{: #cl-boms_master-41659_1613_openshift_M}

The following list shows the components that are in the master fix pack 4.16.59_1613_openshift. Master patch updates are applied automatically.
{: shortdesc}

etcd v3.5.29
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.29){: external}.


IBM Cloud Controller Manager v1.29.15-49
:   New version contains updates and security fixes.


Key Management Service provider 2.10.23
:   New version contains updates and security fixes.


Portieris admission controller v0.13.37
:   See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.13.37){: external}


Red Hat OpenShift on IBM Cloud 4.16.59
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-59_release-notes){: external}.


## 20 April 2026, Worker node fix pack 4.16.59_1610_openshift
{: #cl-boms-41659_1610_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.59_1610_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   


RHEL 8 (VPC) 4.18.0-553.117.1.el8_10
:   Resolves the following CVEs: RHSA-2026:8352, CVE-2026-1519, RHSA-2026:8534, CVE-2026-4424, CVE-2026-5121, RHSA-2026:7667, CVE-2026-27135, RHSA-2026:6461, CVE-2026-3497, RHSA-2026:6473, CVE-2026-4519, RHSA-2026:7674, CVE-2026-25679, RHSA-2026:6915, CVE-2026-28417, CVE-2026-28421, CVE-2026-33412, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:6037, CVE-2025-38180, CVE-2026-23204, CVE-2026-23209, RHSA-2026:6571, CVE-2024-26984, CVE-2025-71238, CVE-2026-23193, CVE-2026-23231, RHSA-2026:6436, and CVE-2025-10158.


RHEL 8 (Classic) 4.18.0-553.117.1.el8_10
:   Resolves the following CVEs: RHSA-2026:8352, CVE-2026-1519, RHSA-2026:4728, CVE-2026-22695, CVE-2026-22801, CVE-2026-25646, RHSA-2026:7667, CVE-2026-27135, RHSA-2026:6461, CVE-2026-3497, RHSA-2026:6473, CVE-2026-4519, RHSA-2026:4952, CVE-2025-61726, CVE-2025-61729, CVE-2025-68121, RHSA-2026:7674, CVE-2026-25679, RHSA-2026:6915, CVE-2026-28417, CVE-2026-28421, CVE-2026-33412, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:4772, CVE-2025-15281, CVE-2026-0915, RHSA-2026:5585, CVE-2025-14831, CVE-2025-9820, RHSA-2026:4648, CVE-2025-61662, RHSA-2026:6037, CVE-2025-38180, CVE-2026-23204, CVE-2026-23209, RHSA-2026:6571, CVE-2024-26984, CVE-2025-71238, CVE-2026-23193, CVE-2026-23231, RHSA-2026:5588, CVE-2025-0938, RHSA-2026:4442, and CVE-2026-25749.


Red Hat OpenShift 4.16.59
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-59_release-notes){: external}.


Red Hat CoreOS 4.16.59
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-59_release-notes){: external}.


HAProxy c7e825675cbd75e8433801c99f8aca3b207a5a46
:   Resolves the following CVEs: CVE-2026-27135.


## 06 April 2026, Worker node fix pack 4.16.58_1609_openshift
{: #cl-boms-41658_1609_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.58_1609_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [5.4.2.4](https://workbench.cisecurity.org/sections/2758938/recommendations/4466977){: external}


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [5.4.2.4](https://workbench.cisecurity.org/sections/2758938/recommendations/4466977){: external}


RHEL 8 (VPC) 4.18.0-553.111.1.el8_10
:   Resolves the following CVEs: RHSA-2024:3043, CVE-2024-0690, RHSA-2026:5585, CVE-2025-14831, CVE-2025-9820, RHSA-2026:3963, CVE-2025-71085, CVE-2026-23001, RHSA-2026:5588, and CVE-2025-0938.


RHEL 8 (Classic) 4.18.0-553.111.1.el8_10
:   Resolves the following CVEs: RHSA-2024:3043, CVE-2024-0690, RHSA-2026:3963, CVE-2025-71085, CVE-2026-23001, RHSA-2026:4442, and CVE-2026-25749.


Red Hat OpenShift 4.16.58
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-58_release-notes){: external}.


Red Hat CoreOS 4.16.58
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-58_release-notes){: external}.


HAProxy 91cc06f4e0a123d06f5ee7c226df6fb83e1ca223
:   Resolves the following CVEs: CVE-2025-14831, and CVE-2025-9820.


## 24 March 2026, Worker node fix pack 4.16.58_1608_openshift
{: #cl-boms-41658_1608_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.58_1608_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   


RHEL 8 (VPC) 4.18.0-553.109.1.el8_10
:   Resolves the following CVEs: RHSA-2026:4672, CVE-2025-61726, CVE-2025-61728, CVE-2025-68121, RHSA-2026:4728, CVE-2026-22695, CVE-2026-22801, CVE-2026-25646, RHSA-2026:4952, CVE-2025-61726, CVE-2025-61729, CVE-2025-68121, RHSA-2026:4772, CVE-2025-15281, CVE-2026-0915, RHSA-2026:4648, CVE-2025-61662, RHSA-2026:3464, and CVE-2026-23097.


RHEL 8 (Classic) 4.18.0-553.109.1.el8_10
:   Resolves the following CVEs: RHSA-2026:4672, CVE-2025-61726, CVE-2025-61728, CVE-2025-68121, RHSA-2026:4728, CVE-2026-22695, CVE-2026-22801, CVE-2026-25646, RHSA-2026:4952, CVE-2025-61726, CVE-2025-61729, CVE-2025-68121, RHSA-2026:4772, CVE-2025-15281, CVE-2026-0915, RHSA-2026:4648, CVE-2025-61662, RHSA-2026:3464, and CVE-2026-23097.


Red Hat OpenShift 4.16.58
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-58_release-notes){: external}.


Red Hat CoreOS 4.16.58
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-58_release-notes){: external}.


HAProxy 10c8639e6b5829d0af51a22755e13756f34630cf
:   Resolves the following CVEs: CVE-2025-15281, and CVE-2026-0915.


## 11 March 2026, Worker node fix pack 4.16.57_1605_openshift
{: #cl-boms-41657_1605_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.57_1605_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   


RHEL 8 (VPC) 4.18.0-553.107.1.el8_10
:   Resolves the following CVEs: RHSA-2026:2264, CVE-2025-68349, CVE-2025-38403, CVE-2025-40158, CVE-2025-40135, CVE-2025-40170, CVE-2026-22998, CVE-2025-40269, CVE-2022-50673, RHSA-2026:2720, CVE-2025-40168, CVE-2025-40304, CVE-2023-53762, RHSA-2026:3083, CVE-2025-38129, CVE-2025-38248, CVE-2025-40064, CVE-2025-68800, and CVE-2026-23074.


RHEL 8 (Classic) 4.18.0-553.107.1.el8_10
:   Resolves the following CVEs: RHSA-2026:2264, CVE-2025-68349, CVE-2025-38403, CVE-2025-40158, CVE-2025-40135, CVE-2025-40170, CVE-2026-22998, CVE-2025-40269, CVE-2022-50673, RHSA-2026:2720, CVE-2025-40168, CVE-2025-40304, CVE-2023-53762, RHSA-2026:3083, CVE-2025-38129, CVE-2025-38248, CVE-2025-40064, CVE-2025-68800, and CVE-2026-23074.


Red Hat OpenShift 4.16.57
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-57_release-notes){: external}.


Red Hat CoreOS 4.16.57
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-57_release-notes){: external}.


HAProxy 965c403695b15b3410d87a3772002edbc5ed2569
:   Resolves the following CVEs: CVE-2025-69419.


## 24 February 2026, Worker node fix pack 4.16.57_1604_openshift
{: #cl-boms-41657_1604_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.57_1604_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [1.6.3](https://workbench.cisecurity.org/sections/2758919/recommendations/4466876){: external}


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [1.6.3](https://workbench.cisecurity.org/sections/2758919/recommendations/4466876){: external}


RHEL 8 (VPC) 4.18.0-553.100.1.el8_10
:   Resolves the following CVEs: RHSA-2026:2389, CVE-2025-6176, RHSA-2026:2215, CVE-2026-0719, CVE-2026-1761, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:1662, CVE-2022-50865, CVE-2024-26766, CVE-2025-38022, CVE-2025-38024, CVE-2025-38415, CVE-2025-38459, CVE-2025-39760, CVE-2025-40258, CVE-2025-40271, CVE-2025-40322, RHSA-2026:2264, CVE-2022-50673, CVE-2025-38403, CVE-2025-40135, CVE-2025-40158, CVE-2025-40170, CVE-2025-40269, CVE-2025-68349, CVE-2026-22998, RHSA-2026:2720, CVE-2023-53762, CVE-2025-40168, CVE-2025-40304, RHSA-2026:2128, CVE-2025-15366, CVE-2025-15367, CVE-2026-0865, and CVE-2026-1299.


RHEL 8 (Classic) 4.18.0-553.100.1.el8_10
:   Resolves the following CVEs: RHSA-2026:2389, CVE-2025-6176, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:1662, CVE-2022-50865, CVE-2024-26766, CVE-2025-38022, CVE-2025-38024, CVE-2025-38415, CVE-2025-38459, CVE-2025-39760, CVE-2025-40258, CVE-2025-40271, CVE-2025-40322, RHSA-2026:2264, CVE-2022-50673, CVE-2025-38403, CVE-2025-40135, CVE-2025-40158, CVE-2025-40170, CVE-2025-40269, CVE-2025-68349, CVE-2026-22998, RHSA-2026:2720, CVE-2023-53762, CVE-2025-40168, and CVE-2025-40304.


Red Hat OpenShift 4.16.57
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-57_release-notes){: external}.


Red Hat CoreOS 4.16.57
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-57_release-notes){: external}.


HAProxy 2bf1aebe51a37cd9b4661656ce21e53f918166ea
:   Resolves the following CVEs: CVE-2025-6176.


## 09 February 2026, Worker node fix pack 4.16.56_1602_openshift
{: #cl-boms-41656_1602_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.56_1602_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [1.6.6](https://workbench.cisecurity.org/sections/2758919/recommendations/4466895){: external}, [3.1.3](https://workbench.cisecurity.org/sections/2758883/recommendations/4466704){: external}, [4.1.2](https://workbench.cisecurity.org/sections/2758898/recommendations/4466776){: external}, [4.3.4](https://workbench.cisecurity.org/sections/2758905/recommendations/4466822){: external}, [5.3.2.1](https://workbench.cisecurity.org/sections/2758922/recommendations/4466880){: external}, [5.3.3.2.4](https://workbench.cisecurity.org/sections/2758930/recommendations/4466941){: external}, [5.3.3.2.7](https://workbench.cisecurity.org/sections/2758930/recommendations/4466958){: external}, [5.3.3.3.1](https://workbench.cisecurity.org/sections/2758934/recommendations/4466960){: external}, [5.3.3.4.2](https://workbench.cisecurity.org/sections/2758935/recommendations/4466965){: external}, [5.4.1.5](https://workbench.cisecurity.org/sections/2758937/recommendations/4466972){: external}, [5.4.2.5](https://workbench.cisecurity.org/sections/2758938/recommendations/4466978){: external}Resolves the following CVEs: RHSA-2025:19930, CVE-2024-36350, CVE-2024-36357, and CVE-2025-40300.


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [1.6.6](https://workbench.cisecurity.org/sections/2758919/recommendations/4466895){: external}, [3.1.3](https://workbench.cisecurity.org/sections/2758883/recommendations/4466704){: external}, [4.1.2](https://workbench.cisecurity.org/sections/2758898/recommendations/4466776){: external}, [4.3.4](https://workbench.cisecurity.org/sections/2758905/recommendations/4466822){: external}, [5.3.2.1](https://workbench.cisecurity.org/sections/2758922/recommendations/4466880){: external}, [5.3.3.2.4](https://workbench.cisecurity.org/sections/2758930/recommendations/4466941){: external}, [5.3.3.2.7](https://workbench.cisecurity.org/sections/2758930/recommendations/4466958){: external}, [5.3.3.3.1](https://workbench.cisecurity.org/sections/2758934/recommendations/4466960){: external}, [5.3.3.4.2](https://workbench.cisecurity.org/sections/2758935/recommendations/4466965){: external}, [5.4.1.5](https://workbench.cisecurity.org/sections/2758937/recommendations/4466972){: external}, [5.4.2.5](https://workbench.cisecurity.org/sections/2758938/recommendations/4466978){: external}Resolves the following CVEs: RHSA-2025:19930, CVE-2024-36350, CVE-2024-36357, and CVE-2025-40300.


RHEL 8 (VPC) 4.18.0-553.97.1.el8_10
:   Resolves the following CVEs: RHSA-2026:0444, CVE-2025-39993, CVE-2025-40240, CVE-2025-68285, RHSA-2026:0759, CVE-2023-53552, CVE-2025-38051, CVE-2025-39933, CVE-2025-40096, CVE-2025-68301, RHSA-2026:1142, CVE-2023-53673, CVE-2025-40154, CVE-2025-40248, CVE-2025-40277, RHSA-2026:1254, CVE-2025-66418, CVE-2025-66471, CVE-2026-21441, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:1662, CVE-2022-50865, CVE-2024-26766, CVE-2025-38022, CVE-2025-38024, CVE-2025-38415, CVE-2025-38459, CVE-2025-39760, CVE-2025-40258, CVE-2025-40271, CVE-2025-40322, RHSA-2026:1631, CVE-2025-12084, RHSA-2026:2128, CVE-2025-15366, CVE-2025-15367, CVE-2026-0865, CVE-2026-1299, RHSA-2026:1852, and CVE-2025-14104.


RHEL 8 (Classic) 4.18.0-553.97.1.el8_10
:   Resolves the following CVEs: RHSA-2025:23543, CVE-2025-52881, RHSA-2026:0753, CVE-2025-47913, RHSA-2026:0728, CVE-2025-68973, RHSA-2026:0444, CVE-2025-39993, CVE-2025-40240, CVE-2025-68285, RHSA-2026:0759, CVE-2023-53552, CVE-2025-38051, CVE-2025-39933, CVE-2025-40096, CVE-2025-68301, RHSA-2026:1142, CVE-2023-53673, CVE-2025-40154, CVE-2025-40248, CVE-2025-40277, RHSA-2026:0241, CVE-2025-64720, CVE-2025-65018, CVE-2025-66293, RHSA-2026:1254, CVE-2025-66418, CVE-2025-66471, CVE-2026-21441, RHSA-2025:23530, CVE-2024-11168, CVE-2024-5642, CVE-2024-9287, CVE-2025-0938, CVE-2025-4138, CVE-2025-4330, CVE-2025-4435, CVE-2025-4516, CVE-2025-4517, CVE-2025-6069, CVE-2025-6075, CVE-2025-8291, RHSA-2024:3043, CVE-2024-0690, RHSA-2025:23382, CVE-2025-11083, RHSA-2025:23374, CVE-2025-58183, RHSA-2025:23383, CVE-2025-9086, RHSA-2026:0991, CVE-2025-13601, RHSA-2026:1662, CVE-2022-50865, CVE-2024-26766, CVE-2025-38022, CVE-2025-38024, CVE-2025-38415, CVE-2025-38459, CVE-2025-39760, CVE-2025-40258, CVE-2025-40271, CVE-2025-40322, RHSA-2025:23481, CVE-2025-61984, CVE-2025-61985, RHSA-2026:0337, CVE-2025-9230, RHSA-2026:1631, CVE-2025-12084, RHSA-2026:2128, CVE-2025-15366, CVE-2025-15367, CVE-2026-0865, CVE-2026-1299, RHSA-2026:1852, and CVE-2025-14104.


Red Hat OpenShift 4.16.56
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-56_release-notes){: external}.


Red Hat CoreOS 4.16.56
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-56_release-notes){: external}.


HAProxy ace947f4ecf45f28effe8d125ffda48f9890223b
:   Resolves the following CVEs: CVE-2025-14104.


## 27 January 2026, Worker node fix pack 4.16.55_1601_openshift
{: #cl-boms-41655_1601_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.55_1601_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.60.1.el9_6
:   Beginning at this patch version, VPC worker nodes include the following changes: the local time is set to UTC, the root filesystem has changed from ext4 to XFS, and the boot mode has changed from BIOS to UEFI.


RHEL 9 (Classic) 5.14.0-570.60.1.el9_6
:   


RHEL 8 (VPC) 4.18.0-553.89.1.el8_10
:   Resolves the following CVEs: RHSA-2026:0753, CVE-2025-47913, RHSA-2026:0728, CVE-2025-68973, RHSA-2026:0444, CVE-2025-39993, CVE-2025-40240, CVE-2025-68285, RHSA-2026:0759, CVE-2023-53552, CVE-2025-38051, CVE-2025-39933, CVE-2025-40096, CVE-2025-68301, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:0991, and CVE-2025-13601.


RHEL 8 (Classic) 4.18.0-553.89.1.el8_10
:   Resolves the following CVEs: RHSA-2026:0753, CVE-2025-47913, RHSA-2026:0728, CVE-2025-68973, RHSA-2026:0444, CVE-2025-39993, CVE-2025-40240, CVE-2025-68285, RHSA-2026:0759, CVE-2023-53552, CVE-2025-38051, CVE-2025-39933, CVE-2025-40096, CVE-2025-68301, RHSA-2024:3043, CVE-2024-0690, RHSA-2026:0991, and CVE-2025-13601.


Red Hat OpenShift 4.16.55
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-55_release-notes){: external}.


Red Hat CoreOS 4.16.55
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-55_release-notes){: external}.


HAProxy c9cb5ad988e916d184d1c308d4f2e5c502d99523
:   Resolves the following CVEs: CVE-2025-68973, CVE-2025-13601, and CVE-2025-9230.


## Master fix pack 4.16.54_1600_openshift, released 21 January 2026
{: #41654_1600_openshift_M}

The following list shows the changes that are in the master fix pack 4.16.54_1600_openshift. Master patch updates are applied automatically. 


Calico v3.29.7
:   See the [Calico release notes](https://archive-os-3-29.netlify.app/calico/3.29/release-notes/#calico-open-source-3297-bug-fix-release){: external}.
Cluster health image v1.6.13
:   New version contains updates and security fixes.
etcd v3.5.26
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.26){: external}.
{{site.data.keyword.cloud_notm}} Controller Manager v1.29.15-38
:   New version contains updates and security fixes.
Key Management Service provider 2.10.20
:   New version contains updates and security fixes.
Portieris admission controller v0.13.33
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.33){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.16.54
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-54_release-notes){: external}.
Tigera Operator v1.36.16
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.36.16){: external}.


## 12 January 2026, Worker node fix pack 4.16.54_1598_openshift
{: #cl-boms-41654_1598_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.54_1598_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 5.14.0-570.60.1.el9_6
:   


RHEL 8 4.18.0-553.89.1.el8_10
:   Resolves the following CVEs: RHSA-2026:0241, CVE-2025-64720, CVE-2025-65018, CVE-2025-66293, RHSA-2024:3043, and CVE-2024-0690.


Red Hat OpenShift 4.16.54
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-54_release-notes){: external}.


Red Hat CoreOS 4.16.54
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-54_release-notes){: external}.


HAProxy d04e61c5b29aa5328bc72455edb95e08e8f6d85c
:   


## 29 December 2025, Worker node fix pack 4.16.54_1597_openshift
{: #cl-boms-41654_1597_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.54_1597_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 5.14.0-570.60.1.el9_6
:   


RHEL 8 4.18.0-553.89.1.el8_10
:   Resolves the following CVEs: RHSA-2025:23543, CVE-2025-52881, RHSA-2025:23530, CVE-2024-11168, CVE-2024-5642, CVE-2024-9287, CVE-2025-0938, CVE-2025-4138, CVE-2025-4330, CVE-2025-4435, CVE-2025-4516, CVE-2025-4517, CVE-2025-6069, CVE-2025-6075, CVE-2025-8291, RHSA-2024:3043, CVE-2024-0690, RHSA-2025:23382, CVE-2025-11083, RHSA-2025:23374, CVE-2025-58183, RHSA-2025:23383, CVE-2025-9086, RHSA-2025:21917, CVE-2025-39697, CVE-2025-39971, RHSA-2025:22388, CVE-2023-53513, CVE-2025-38724, CVE-2025-39825, CVE-2025-39883, CVE-2025-39898, CVE-2025-39955, RHSA-2025:22801, CVE-2022-50543, CVE-2023-53401, CVE-2023-53539, RHSA-2025:23481, CVE-2025-61984, and CVE-2025-61985.


Red Hat OpenShift 4.16.54
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-54_release-notes){: external}.


Red Hat CoreOS 4.16.54
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-54_release-notes){: external}.


HAProxy d04e61c5b29aa5328bc72455edb95e08e8f6d85c
:   Resolves the following CVEs: CVE-2025-9086.


## 16 December 2025, Worker node fix pack 4.16.54_1596_openshift
{: #cl-boms-41654_1596_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.54_1596_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 5.14.0-570.60.1.el9_6
:   


RHEL 8 4.18.0-553.84.1.el8_10
:   


Red Hat OpenShift 4.16.54
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-54_release-notes){: external}.


Red Hat CoreOS 4.16.54
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-54_release-notes){: external}.


HAProxy 03b74b82b63cd53403b6b587b84233c93edef18d
:   


## Master fix pack 4.16.52_1595_openshift, released 10 December 2025
{: #41652_1595_openshift_M}

The following list shows the changes that are in the master fix pack 4.16.52_1595_openshift. Master patch updates are applied automatically. 


Cluster health image v1.6.13
:   New version contains updates and security fixes.
etcd v3.5.25
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.25){: external}.
{{site.data.keyword.cloud_notm}} Controller Manager v1.29.15-33
:   New version contains updates and security fixes.
Key Management Service provider 2.10.19
:   New version contains updates and security fixes.
Portieris admission controller v0.13.33
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.33){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.16.52
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-52_release-notes){: external}.


## 03 December 2025, Worker node fix pack 4.16.52_1594_openshift
{: #cl-boms-41652_1594_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.52_1594_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 5.14.0-570.60.1.el9_6
:   


RHEL 8 4.18.0-553.84.1.el8_10
:   Resolves the following CVEs: RHSA-2025:21776, CVE-2025-59375, RHSA-2025:19931, CVE-2022-50367, CVE-2023-53178, CVE-2025-40300, RHSA-2025:21398, CVE-2025-39718, RHSA-2025:21977, and CVE-2025-5372.


Red Hat OpenShift 4.16.52
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-52_release-notes){: external}.


Red Hat CoreOS 4.16.52
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-52_release-notes){: external}.


HAProxy 03b74b82b63cd53403b6b587b84233c93edef18d
:   Resolves the following CVEs: CVE-2025-59375, CVE-2025-5372, CVE-2024-28757, and CVE-2022-23990.


## 17 November 2025, Worker node fix pack 4.16.52_1593_openshift
{: #cl-boms-41652_1593_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.52_1593_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 5.14.0-570.60.1.el9_6
:   Resolves the following CVEs: RHSA-2025:19951, CVE-2025-40778, CVE-2025-40780, RHSA-2025:19105, CVE-2023-53331, CVE-2025-39718, CVE-2025-39730, CVE-2025-39751, CVE-2025-39819, RHSA-2025:19409, CVE-2022-50367, CVE-2023-53494, and CVE-2025-39702.


RHEL 8 4.18.0-553.82.1.el8_10
:   Resolves the following CVEs: RHSA-2025:19835, CVE-2025-40778, CVE-2025-8677, RHSA-2025:21232, CVE-2025-31133, CVE-2025-52565, CVE-2025-52881, RHSA-2025:19610, CVE-2025-11561, RHSA-2024:3043, CVE-2024-0690, RHSA-2025:18297, CVE-2023-53373, CVE-2025-39751, CVE-2025-39757, RHSA-2025:19102, CVE-2022-50386, CVE-2023-53297, CVE-2023-53386, CVE-2025-39817, CVE-2025-39841, CVE-2025-39849, RHSA-2025:19447, CVE-2023-53226, CVE-2023-53257, and CVE-2025-39864.


Red Hat OpenShift 4.16.52
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-52_release-notes){: external}.


Red Hat CoreOS 4.16.52
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-52_release-notes){: external}.


HAProxy fbe9b8146f23bbd12b2566a79fa897d5981e7273
:   


## Master fix pack 4.16.51_1592_openshift, released 15 November 2025
{: #41651_1592_openshift_M}

The following list shows the changes that are in the master fix pack 4.16.51_1592_openshift. Master patch updates are applied automatically. 


Calico v3.29.6
:   See the [Calico release notes](https://archive-os-3-29.netlify.app/calico/3.29/release-notes/#calico-open-source-3296-bug-fix-release){: external}.
etcd v3.5.24
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.24){: external}.
{{site.data.keyword.cloud_notm}} Block Storage driver and plug-in v2.5.22
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} Controller Manager v1.29.15-28
:   New version contains updates and security fixes.
Key Management Service provider v2.10.18
:   New version contains updates and security fixes.
Portieris admission controller v0.13.31
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.31){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.16.51
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-51_release-notes){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit v4.16.0+20251015
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.16.0+20251015){: external}.
Tigera Operator v1.36.14
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.36.14){: external}.


## 06 November 2025, Worker node fix pack 4.16.51_1588_openshift
{: #cl-boms-41651_1588_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.51_1588_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-570.55.1.el9_6
:   Resolves the following CVEs: RHSA-2025:17377, CVE-2024-50301, CVE-2025-38351, CVE-2025-39761, RHSA-2025:17760, CVE-2023-53373, CVE-2025-38556, CVE-2025-38614, CVE-2025-39757, RHSA-2025:18281, CVE-2022-50087, CVE-2025-22026, CVE-2025-38566, CVE-2025-38571, CVE-2025-39817, CVE-2025-39841, and CVE-2025-39849.


RHEL_8 4.18.0-553.79.1.el8_10
:   Resolves the following CVEs: RHSA-2025:17397, CVE-2025-38527, CVE-2025-39730, RHSA-2025:17797, CVE-2022-50228, CVE-2023-53305, RHSA-2025:18286, and CVE-2025-5318.


Red Hat OpenShift 4.16.51
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-51_release-notes){: external}.


Red Hat CoreOS 4.16.51
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-51_release-notes){: external}.


HAProxy fbe9b8146f23bbd12b2566a79fa897d5981e7273
:   Resolves the following CVEs: CVE-2025-5318.


## 21 October 2025, Worker node fix pack 4.16.50_1587_openshift
{: #cl-boms-41650_1587_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.50_1587_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-570.49.1.el9_6
:   Resolves the following CVEs: RHSA-2025:10848, CVE-2024-6174, RHSA-2025:11462, CVE-2024-50349, CVE-2024-52006, CVE-2025-27613, CVE-2025-27614, CVE-2025-46835, CVE-2025-48384, CVE-2025-48385, RHSA-2025:10379, CVE-2022-49846, CVE-2025-21759, CVE-2025-21887, CVE-2025-22004, CVE-2025-37799, RHSA-2025:11411, CVE-2024-58002, CVE-2025-38089, RHSA-2025:12746, CVE-2022-49788, CVE-2025-21727, CVE-2025-21928, CVE-2025-21929, CVE-2025-21962, CVE-2025-22020, CVE-2025-37890, CVE-2025-38052, CVE-2025-38087, RHSA-2025:13962, CVE-2024-28956, CVE-2025-21867, CVE-2025-38084, CVE-2025-38085, CVE-2025-38124, CVE-2025-38159, CVE-2025-38250, CVE-2025-38380, CVE-2025-38471, RHSA-2025:14420, CVE-2025-22058, CVE-2025-37914, CVE-2025-38417, RHSA-2025:15011, CVE-2025-37823, CVE-2025-38200, CVE-2025-38211, CVE-2025-38350, CVE-2025-38461, CVE-2025-38464, CVE-2025-38500, CVE-2025-38684, RHSA-2025:15429, CVE-2025-37803, CVE-2025-38392, CVE-2025-39825, RHSA-2025:15661, CVE-2025-22097, CVE-2025-38332, CVE-2025-38352, CVE-2025-38449, RHSA-2025:7423, CVE-2024-58005, CVE-2024-58007, CVE-2024-58069, CVE-2025-21633, CVE-2025-21927, CVE-2025-21993, RHSA-2025:7903, CVE-2025-21756, CVE-2025-21966, CVE-2025-37749, RHSA-2025:8643, CVE-2025-21920, CVE-2025-21926, CVE-2025-21997, CVE-2025-22055, CVE-2025-37785, CVE-2025-37943, RHSA-2025:9080, CVE-2025-21961, CVE-2025-21963, CVE-2025-21969, CVE-2025-21979, CVE-2025-21999, CVE-2025-22126, CVE-2025-37750, RHSA-2025:14130, CVE-2025-5914, RHSA-2025:10699, CVE-2025-49794, CVE-2025-49796, CVE-2025-6021, RHSA-2025:12447, CVE-2025-7425, RHSA-2025:15099, CVE-2025-6020, CVE-2025-8941, RHSA-2025:9526, CVE-2025-6020, RHSA-2025:10136, CVE-2024-12718, CVE-2025-4138, CVE-2025-4330, CVE-2025-4435, CVE-2025-4517, RHSA-2025:11992, CVE-2025-6965, RHSA-2025:9978, CVE-2025-32462, CVE-2024-36350, CVE-2024-36357, RHSA-2025:12876, CVE-2022-29458, RHSA-2025:7440, CVE-2023-4752, CVE-2024-28956, CVE-2024-43420, CVE-2024-45332, CVE-2025-20012, CVE-2025-20623, CVE-2025-24495, RHSA-2025:7444, CVE-2024-8176, RHSA-2025:7409, CVE-2024-52005, RHSA-2025:11140, CVE-2024-52533, CVE-2025-4373, RHSA-2025:12748, CVE-2025-8058, RHSA-2025:8655, CVE-2025-4802, RHSA-2025:9877, CVE-2025-5702, RHSA-2025:7076, CVE-2024-12243, RHSA-2025:16116, CVE-2025-32988, CVE-2025-32989, CVE-2025-32990, CVE-2025-6395, RHSA-2025:6990, CVE-2024-45774, CVE-2024-45775, CVE-2024-45776, CVE-2024-45781, CVE-2024-45783, CVE-2025-0622, CVE-2025-0677, CVE-2025-0690, RHSA-2025:17558, CVE-2025-48964, RHSA-2025:9432, CVE-2025-47268, RHSA-2025:10585, CVE-2024-23337, CVE-2025-48060, RHSA-2025:10837, CVE-2025-21991, RHSA-2025:11861, CVE-2024-57980, CVE-2025-21905, CVE-2025-22085, CVE-2025-22091, CVE-2025-22113, CVE-2025-22121, CVE-2025-37797, CVE-2025-37958, CVE-2025-38086, CVE-2025-38110, RHSA-2025:13602, CVE-2025-38079, CVE-2025-38292, RHSA-2025:15740, CVE-2025-38550, RHSA-2025:16398, CVE-2023-53125, CVE-2025-37810, CVE-2025-38498, CVE-2025-39694, RHSA-2025:16880, CVE-2025-38472, CVE-2025-38527, CVE-2025-38718, CVE-2025-39682, CVE-2025-39698, RHSA-2025:17377, CVE-2024-50301, CVE-2025-38351, CVE-2025-39761, RHSA-2025:17760, CVE-2023-53373, CVE-2025-38556, CVE-2025-38614, CVE-2025-39757, RHSA-2025:6966, CVE-2022-48969, CVE-2022-48989, CVE-2022-49006, CVE-2022-49014, CVE-2022-49029, CVE-2022-49778, CVE-2022-49804, CVE-2022-49815, CVE-2022-50112, CVE-2022-50159, CVE-2022-50214, CVE-2022-50511, CVE-2023-52672, CVE-2023-52917, CVE-2023-53066, CVE-2023-53117, CVE-2023-53196, CVE-2023-53260, CVE-2023-53261, CVE-2023-53595, CVE-2024-27008, CVE-2024-27398, CVE-2024-35891, CVE-2024-35933, CVE-2024-35934, CVE-2024-35963, CVE-2024-35964, CVE-2024-35965, CVE-2024-35966, CVE-2024-35967, CVE-2024-35978, CVE-2024-36011, CVE-2024-36012, CVE-2024-36013, CVE-2024-36880, CVE-2024-36968, CVE-2024-38541, CVE-2024-39500, CVE-2024-40956, CVE-2024-41010, CVE-2024-41062, CVE-2024-42094, CVE-2024-42133, CVE-2024-42253, CVE-2024-42265, CVE-2024-42278, CVE-2024-42291, CVE-2024-42294, CVE-2024-42302, CVE-2024-42304, CVE-2024-42305, CVE-2024-42312, CVE-2024-42315, CVE-2024-42316, CVE-2024-42321, CVE-2024-43820, CVE-2024-43821, CVE-2024-43823, CVE-2024-43828, CVE-2024-43834, CVE-2024-43846, CVE-2024-43853, CVE-2024-43871, CVE-2024-43873, CVE-2024-43882, CVE-2024-43884, CVE-2024-43889, CVE-2024-43898, CVE-2024-43910, CVE-2024-43914, CVE-2024-44931, CVE-2024-44932, CVE-2024-44934, CVE-2024-44952, CVE-2024-44958, CVE-2024-44964, CVE-2024-44975, CVE-2024-44987, CVE-2024-44989, CVE-2024-45000, CVE-2024-45009, CVE-2024-45010, CVE-2024-45016, CVE-2024-45022, CVE-2024-46673, CVE-2024-46675, CVE-2024-46711, CVE-2024-46722, CVE-2024-46723, CVE-2024-46724, CVE-2024-46725, CVE-2024-46743, CVE-2024-46745, CVE-2024-46747, CVE-2024-46750, CVE-2024-46754, CVE-2024-46756, CVE-2024-46758, CVE-2024-46759, CVE-2024-46761, CVE-2024-46783, CVE-2024-46786, CVE-2024-46787, CVE-2024-46800, CVE-2024-46805, CVE-2024-46806, CVE-2024-46807, CVE-2024-46819, CVE-2024-46820, CVE-2024-46822, CVE-2024-46828, CVE-2024-46835, CVE-2024-46839, CVE-2024-46853, CVE-2024-46864, CVE-2024-46871, CVE-2024-47141, CVE-2024-47660, CVE-2024-47668, CVE-2024-47678, CVE-2024-47685, CVE-2024-47687, CVE-2024-47692, CVE-2024-47700, CVE-2024-47703, CVE-2024-47705, CVE-2024-47706, CVE-2024-47710, CVE-2024-47713, CVE-2024-47715, CVE-2024-47718, CVE-2024-47719, CVE-2024-47737, CVE-2024-47738, CVE-2024-47739, CVE-2024-47745, CVE-2024-47748, CVE-2024-48873, CVE-2024-49569, CVE-2024-49851, CVE-2024-49856, CVE-2024-49860, CVE-2024-49862, CVE-2024-49870, CVE-2024-49875, CVE-2024-49878, CVE-2024-49881, CVE-2024-49882, CVE-2024-49883, CVE-2024-49884, CVE-2024-49885, CVE-2024-49886, CVE-2024-49889, CVE-2024-49904, CVE-2024-49927, CVE-2024-49928, CVE-2024-49929, CVE-2024-49930, CVE-2024-49933, CVE-2024-49934, CVE-2024-49935, CVE-2024-49937, CVE-2024-49938, CVE-2024-49939, CVE-2024-49946, CVE-2024-49948, CVE-2024-49950, CVE-2024-49951, CVE-2024-49954, CVE-2024-49959, CVE-2024-49960, CVE-2024-49962, CVE-2024-49967, CVE-2024-49968, CVE-2024-49971, CVE-2024-49973, CVE-2024-49974, CVE-2024-49975, CVE-2024-49977, CVE-2024-49983, CVE-2024-49991, CVE-2024-49993, CVE-2024-49994, CVE-2024-49995, CVE-2024-49999, CVE-2024-50002, CVE-2024-50006, CVE-2024-50008, CVE-2024-50009, CVE-2024-50013, CVE-2024-50014, CVE-2024-50015, CVE-2024-50018, CVE-2024-50019, CVE-2024-50022, CVE-2024-50023, CVE-2024-50024, CVE-2024-50027, CVE-2024-50028, CVE-2024-50029, CVE-2024-50033, CVE-2024-50035, CVE-2024-50038, CVE-2024-50039, CVE-2024-50044, CVE-2024-50046, CVE-2024-50047, CVE-2024-50055, CVE-2024-50057, CVE-2024-50058, CVE-2024-50064, CVE-2024-50067, CVE-2024-50073, CVE-2024-50074, CVE-2024-50075, CVE-2024-50077, CVE-2024-50078, CVE-2024-50081, CVE-2024-50082, CVE-2024-50093, CVE-2024-50101, CVE-2024-50102, CVE-2024-50106, CVE-2024-50107, CVE-2024-50109, CVE-2024-50117, CVE-2024-50120, CVE-2024-50121, CVE-2024-50126, CVE-2024-50127, CVE-2024-50128, CVE-2024-50130, CVE-2024-50141, CVE-2024-50143, CVE-2024-50150, CVE-2024-50151, CVE-2024-50152, CVE-2024-50153, CVE-2024-50162, CVE-2024-50163, CVE-2024-50169, CVE-2024-50182, CVE-2024-50186, CVE-2024-50189, CVE-2024-50191, CVE-2024-50197, CVE-2024-50199, CVE-2024-50200, CVE-2024-50201, CVE-2024-50215, CVE-2024-50216, CVE-2024-50219, CVE-2024-50228, CVE-2024-50235, CVE-2024-50236, CVE-2024-50237, CVE-2024-50256, CVE-2024-50261, CVE-2024-50271, CVE-2024-50272, CVE-2024-50278, CVE-2024-50282, CVE-2024-50299, CVE-2024-50304, CVE-2024-53042, CVE-2024-53044, CVE-2024-53047, CVE-2024-53050, CVE-2024-53051, CVE-2024-53055, CVE-2024-53057, CVE-2024-53059, CVE-2024-53060, CVE-2024-53070, CVE-2024-53072, CVE-2024-53074, CVE-2024-53082, CVE-2024-53085, CVE-2024-53091, CVE-2024-53093, CVE-2024-53095, CVE-2024-53096, CVE-2024-53097, CVE-2024-53103, CVE-2024-53105, CVE-2024-53110, CVE-2024-53117, CVE-2024-53118, CVE-2024-53120, CVE-2024-53121, CVE-2024-53123, CVE-2024-53124, CVE-2024-53134, CVE-2024-53136, CVE-2024-53141, CVE-2024-53142, CVE-2024-53146, CVE-2024-53152, CVE-2024-53156, CVE-2024-53160, CVE-2024-53161, CVE-2024-53164, CVE-2024-53166, CVE-2024-53173, CVE-2024-53174, CVE-2024-53176, CVE-2024-53190, CVE-2024-53194, CVE-2024-53203, CVE-2024-53208, CVE-2024-53213, CVE-2024-53222, CVE-2024-53224, CVE-2024-53232, CVE-2024-53237, CVE-2024-53681, CVE-2024-54460, CVE-2024-54680, CVE-2024-56535, CVE-2024-56544, CVE-2024-56551, CVE-2024-56558, CVE-2024-56562, CVE-2024-56566, CVE-2024-56570, CVE-2024-56590, CVE-2024-56591, CVE-2024-56600, CVE-2024-56601, CVE-2024-56602, CVE-2024-56604, CVE-2024-56605, CVE-2024-56611, CVE-2024-56614, CVE-2024-56616, CVE-2024-56623, CVE-2024-56631, CVE-2024-56642, CVE-2024-56644, CVE-2024-56647, CVE-2024-56653, CVE-2024-56654, CVE-2024-56663, CVE-2024-56664, CVE-2024-56667, CVE-2024-56688, CVE-2024-56693, CVE-2024-56729, CVE-2024-56757, CVE-2024-56760, CVE-2024-56779, CVE-2024-56783, CVE-2024-57798, CVE-2024-57809, CVE-2024-57843, CVE-2024-57852, CVE-2024-57879, CVE-2024-57884, CVE-2024-57885, CVE-2024-57888, CVE-2024-57890, CVE-2024-57894, CVE-2024-57898, CVE-2024-57903, CVE-2024-57929, CVE-2024-57931, CVE-2024-57940, CVE-2024-58009, CVE-2024-58064, CVE-2024-58099, CVE-2025-1272, CVE-2025-21646, CVE-2025-21663, CVE-2025-21666, CVE-2025-21668, CVE-2025-21669, CVE-2025-21689, CVE-2025-21694, CVE-2025-22087, RHSA-2025:8142, CVE-2025-21964, RHSA-2025:8333, CVE-2022-3424, CVE-2025-21764, RHSA-2025:9302, CVE-2025-21883, CVE-2025-21919, CVE-2025-22104, CVE-2025-23150, CVE-2025-37738, RHSA-2025:9880, CVE-2023-52933, RHSA-2025:7067, CVE-2025-24528, RHSA-2025:9430, CVE-2025-3576, RHSA-2025:9431, CVE-2025-25724, RHSA-2025:18275, CVE-2025-5318, RHSA-2025:7077, CVE-2024-12133, RHSA-2025:13428, CVE-2025-32414, CVE-2025-32415, RHSA-2025:7043, CVE-2024-28047, CVE-2024-31157, CVE-2024-39279, RHSA-2025:6993, CVE-2025-26465, RHSA-2025:11804, CVE-2025-40909, RHSA-2025:15874, CVE-2023-49083, RHSA-2025:12519, CVE-2024-47081, RHSA-2025:7049, CVE-2024-35195, RHSA-2025:10407, CVE-2025-47273, RHSA-2025:15019, CVE-2025-8194, RHSA-2025:6977, CVE-2025-0938, RHSA-2025:7326, CVE-2024-45336, CVE-2025-22866, RHSA-2025:10353, CVE-2024-54661, RHSA-2025:17742, CVE-2025-53905, and CVE-2025-53906.


RHEL_8 4.18.0-553.77.1.el8_10
:   Resolves the following CVEs: RHSA-2024:3043, CVE-2024-0690, RHSA-2025:17415, CVE-2025-32988, CVE-2025-32990, CVE-2025-6395, RHSA-2025:17397, CVE-2025-38527, CVE-2025-39730, RHSA-2025:17797, CVE-2022-50228, CVE-2023-53305, RHSA-2025:17715, CVE-2025-53905, and CVE-2025-53906.


Red Hat OpenShift and Red Hat CoreOS 4.16.50
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-50_release-notes){: external}.


HAProxy c01cd5322cd5c284286c07fe9ad0cc0ef3ab5360
:   Resolves the following CVEs: CVE-2025-32988, CVE-2025-6395, and CVE-2025-32990.


## 08 October 2025, Worker node fix pack 4.16.49_1586_openshift
{: #cl-boms-41649_1586_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.49_1586_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.77.1.el8_10
:   Resolves the following CVEs: RHSA-2024:3043, CVE-2024-0690, RHSA-2025:16372, CVE-2025-38461, CVE-2025-38498, CVE-2025-38556, RHSA-2025:16919, CVE-2022-50087, CVE-2025-22026, CVE-2025-37797, CVE-2025-38718, RHSA-2025:16823, and CVE-2025-26465.


Red Hat OpenShift and Red Hat CoreOS 4.16.49
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-49_release-notes){: external}.


HAProxy e0a48fcf355d98dc769ea048d2fd02044b11ed62
:   


## Master fix pack 4.16.48_1585_openshift, released 07 October 2025
{: #41648_1585_openshift_M}

The following list shows the changes that are in the master fix pack 4.16.48_1585_openshift. Master patch updates are applied automatically. 


Calico v3.29.5
:   See the [Calico release notes](https://archive-os-3-29.netlify.app/calico/3.29/release-notes/#v3.29.5){: external}.
etcd v3.5.23
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.23){: external}.
{{site.data.keyword.cloud_notm}} Controller Manager v1.29.15-24
:   New version contains updates and security fixes.
{{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor 452
:   New version contains updates and security fixes.
Key Management Service provider v2.10.17
:   New version contains updates and security fixes.
Portieris admission controller v0.13.30
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.30){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.16.48
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-48){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.16.0+20250821
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.16.0+20250821){: external}.
Tigera Operator v1.36.13
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.36.13){: external}.


## 23 September 2025, Worker node fix pack 4.16.48_1582_openshift
{: #cl-boms-41648_1582_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.48_1582_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.75.1.el8_10
:   Resolves the following CVEs: RHSA-2025:15904, CVE-2025-9566, RHSA-2025:15471, CVE-2022-49985, CVE-2025-38352, RHSA-2025:15785, CVE-2023-53125, CVE-2025-38350, CVE-2025-38392, CVE-2025-38449, RHSA-2024:3043, and CVE-2024-0690.


Red Hat OpenShift and Red Hat CoreOS 4.16.48
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-48_release-notes){: external}.


HAProxy e0a48fcf355d98dc769ea048d2fd02044b11ed62
:   


## 09 September 2025, Worker node fix pack 4.16.47_1580_openshift
{: #cl-boms-41647_1580_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.47_1580_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.72.1.el8_10
:   Resolves the following CVEs: RHSA-2025:13960, CVE-2025-22097, CVE-2025-37914, CVE-2025-38250, CVE-2025-38380, RHSA-2025:14557, CVE-2025-6020, CVE-2025-8941, RHSA-2024:3043, CVE-2024-0690, RHSA-2025:13589, CVE-2021-47670, CVE-2024-56644, CVE-2025-21727, CVE-2025-21759, CVE-2025-38085, CVE-2025-38159, RHSA-2025:14438, CVE-2025-22058, CVE-2025-38200, RHSA-2025:15008, CVE-2025-38211, CVE-2025-38332, CVE-2025-38464, CVE-2025-38477, RHSA-2025:14553, CVE-2023-49083, RHSA-2025:14560, CVE-2025-8194, RHSA-2025:14900, CVE-2025-47273, and CVE-2025-8194.


Red Hat OpenShift and Red Hat CoreOS 4.16.47
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-47_release-notes){: external}.


HAProxy e0a48fcf355d98dc769ea048d2fd02044b11ed62
:   Resolves the following CVEs: CVE-2025-6020, and CVE-2025-8941.


## 26 August 2025, Worker node fix pack 4.16.46_1579_openshift
{: #cl-boms-41646_1579_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.46_1579_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.66.1.el8_10
:   Resolves the following CVEs: RHSA-2025:12752, CVE-2022-50020, CVE-2025-21928, CVE-2025-22020, CVE-2025-37890, CVE-2025-38052, CVE-2025-38079, RHSA-2025:14135, CVE-2025-5914, RHSA-2024:3043, CVE-2024-0690, RHSA-2025:11850, CVE-2022-49977, CVE-2025-21905, and CVE-2025-21919.


Red Hat OpenShift and Red Hat CoreOS 4.16.46
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-46_release-notes){: external}.


HAProxy 3293782c542587d0ce46be4d053036b75509f4ef
:   Resolves the following CVEs: CVE-2025-5914.


## Master fix pack 4.16.45_1578_openshift, released 20 August 2025
{: #41645_1578_openshift_M}

The following list shows the changes that are in the master fix pack 4.16.45_1578_openshift. Master patch updates are applied automatically. 


etcd v3.5.22
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.22){: external}.
{{site.data.keyword.cloud_notm}} Controller Manager v1.29.15-18
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} RBAC Operator 8a12251
:   New version contains updates and security fixes.
Key Management Service provider v2.10.16
:   New version contains updates and security fixes.
{{site.data.keyword.openshiftlong_notm}} 4.16.45
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-45_release-notes){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit v4.16.0+20250808
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.16.0+20250808){: external}.


## 12 August 2025, Worker node fix pack 4.16.45_1576_openshift
{: #cl-boms-41645_1576_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.45_1576_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.63.1.el8_10
:   Resolves the following CVEs: RHSA-2025:13589, CVE-2021-47670, CVE-2025-21727, CVE-2025-21759, CVE-2025-38085, and CVE-2025-38159.


Red Hat OpenShift and Red Hat CoreOS 4.16.45
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-45_release-notes){: external}.


HAProxy 3a9451f4782fa8e8e9ed60b060dc4393c7e1e31a
:   Resolves the following CVEs: CVE-2025-6965, CVE-2025-8058, and CVE-2025-7425.


## Master fix pack 4.16.43_1574_openshift, released 30 July 2025
{: #41643_1574_openshift_M}

The following list shows the changes that are in the master fix pack 4.16.43_1574_openshift. Master patch updates are applied automatically. 


Calico v3.28.5
:   See the [Calico release notes](https://archive-os-3-28.netlify.app/calico/3.28/release-notes/#calico-open-source-3285-bug-fix-update){: external}.
Calico API server v3.28.5
:   See the [Calico release notes](https://docs.tigera.io/archive){: external}.
Cluster health image v1.6.10
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} Block Storage driver and plug-in v2.5.20
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} Controller Manager v1.29.15-16
:   New version contains updates and security fixes.
{{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor 451
:   New version contains updates and security fixes.
Key Management Service provider v2.10.15
:   New version contains updates and security fixes.
Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider 3347
:   New version contains updates and security fixes.
Portieris admission controller v0.13.29
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.29){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.16.43
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16#ocp-4-16-43_release-notes){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.16.0+20250627
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.16.0+20250627){: external}.
Tigera Operator v1.34.13
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.34.13){: external}.


## 28 July 2025, Worker node fix pack 4.16.44_1575_openshift
{: #cl-boms-41644_1575_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.44_1575_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.63.1.el8_10
:   Resolves the following CVEs: RHSA-2025:11324, CVE-2024-6174, RHSA-2025:11534, CVE-2024-50349, CVE-2024-52006, CVE-2025-27613, CVE-2025-27614, CVE-2025-46835, CVE-2025-48384, CVE-2025-48385, RHSA-2024:3043, CVE-2024-0690, RHSA-2025:11327, CVE-2024-34397, CVE-2024-52533, CVE-2025-4373, RHSA-2025:11298, CVE-2022-49058, CVE-2022-49788, CVE-2024-57980, CVE-2024-58002, CVE-2025-21991, CVE-2025-22004, CVE-2025-23150, CVE-2025-37738, RHSA-2025:11455, CVE-2024-50154, CVE-2025-38086, RHSA-2025:11035, CVE-2019-17543, RHSA-2025:10991, CVE-2024-28956, CVE-2024-43420, CVE-2024-45332, CVE-2025-20012, CVE-2025-20623, CVE-2025-24495, RHSA-2025:11036, CVE-2025-47273, RHSA-2025:11042, and CVE-2024-54661.


Red Hat OpenShift and Red Hat CoreOS 4.16.44
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-44_release-notes){: external}.


HAProxy b19109a289be3a60985c14bfdaf2b48a472556c0
:   Resolves the following CVEs: CVE-2024-54661, CVE-2024-34397, CVE-2019-17543, CVE-2024-52533, and CVE-2025-4373.


## 14 July 2025, Worker node fix pack 4.16.43_1573_openshift
{: #cl-boms-41643_1573_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.43_1573_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.60.1.el8_10
:   Resolves the following CVEs: RHSA-2025:10551, CVE-2025-6032, RHSA-2025:10669, CVE-2022-49111, CVE-2022-49136, CVE-2022-49846, RHSA-2025:10698, CVE-2025-49794, CVE-2025-49796, CVE-2025-6021, RHSA-2025:10027, CVE-2025-6020, RHSA-2025:10128, CVE-2024-12718, CVE-2025-4138, CVE-2025-4330, CVE-2025-4435, CVE-2025-4517, RHSA-2025:10110, CVE-2025-32462, RHSA-2024:3043, CVE-2024-0690, RHSA-2025:10618, CVE-2024-23337, and CVE-2025-48060.


Red Hat OpenShift and Red Hat CoreOS 4.16.43
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-43_release-notes){: external}.


HAProxy 3bb13ac682885a0885eacb7edd1ee7a36d54e2a8
:   Resolves the following CVEs: CVE-2025-6021, CVE-2025-49796, CVE-2025-49794, and CVE-2025-6020.


## 01 July 2025, Worker node fix pack 4.16.42_1572_openshift
{: #cl-boms-41642_1572_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.42_1572_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.58.1.el8_10
:   Resolves the following CVEs: RHSA-2024:3043, CVE-2024-0690, RHSA-2025:9142, CVE-2025-22871, RHSA-2025:9580, CVE-2022-48919, CVE-2024-50301, CVE-2024-53064, and CVE-2025-21764.


Red Hat OpenShift and Red Hat CoreOS 4.16.42
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-42_release-notes){: external}.


HAProxy 951efd90b46e95a54751966c644ac37c4c901f92
:   


## Master fix pack 4.16.41_1570_openshift, released 18 June 2025
{: #41641_1570_openshift_M}

The following list shows the changes that are in the master fix pack 4.16.41_1570_openshift. Master patch updates are applied automatically. 


Calico v3.28.4
:   See the [Calico release notes](https://archive-os-3-28.netlify.app/calico/3.28/release-notes/#v3.28.4){: external}.
{{site.data.keyword.cloud_notm}} Block Storage driver and plug-in v2.5.19
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} Controller Manager v1.29.15-12
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} RBAC Operator 38dc95c
:   New version contains updates and security fixes.
Key Management Service provider v2.10.14
:   New version contains updates and security fixes.
{{site.data.keyword.openshiftlong_notm}}. 4.16.41
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-41){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.16.0+20250609
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.16.0+20250609){: external}.
Tigera Operator v1.34.11
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.34.11){: external}.


## 16 June 2025, Worker node fix pack 4.16.41_1571_openshift
{: #cl-boms-41641_1571_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.41_1571_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.56.1.el8_10
:   Resolves the following CVEs: RHSA-2024:3043, CVE-2024-0690, RHSA-2025:8414, CVE-2024-52005, RHSA-2025:8686, CVE-2025-4802, RHSA-2025:8743, CVE-2022-49395, RHSA-2025:8411, CVE-2025-3576, RHSA-2025:8958, and CVE-2025-32414.


Red Hat OpenShift and Red Hat CoreOS 4.16.41
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-41_release-notes){: external}.


HAProxy 951efd90b46e95a54751966c644ac37c4c901f92
:   Resolves the following CVEs: CVE-2025-4802, CVE-2025-32414, and CVE-2025-3576.


## 04 June 2025, Worker node fix pack 4.16.41_1568_openshift
{: #cl-boms-41641_1568_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.41_1568_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.54.1.el8_10
:   Resolves the following CVEs: RHSA-2025:8056, CVE-2024-40906, CVE-2024-44970, CVE-2025-21756, RHSA-2024:3043, CVE-2024-0690, RHSA-2025:8246, and CVE-2024-43842.


Red Hat OpenShift and Red Hat CoreOS 4.16.41
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-41_release-notes){: external}.


HAProxy 978e3c26ee7634e39a940696aaf57d9e374db5ce
:   


## Master fix pack 4.16.40_1567_openshift, released 28 May 2025
{: #41640_1567_openshift_M}

The following list shows the changes that are in the master fix pack 4.16.40_1567_openshift. Master patch updates are applied automatically. 


Cluster health image v1.6.9
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} Controller Manager v1.29.15-9
:   New version contains updates and security fixes.
{{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor 450
:   New version contains updates and security fixes.
Key Management Service provider v2.10.13
:   New version contains updates and security fixes.
Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider 3293
:   New version contains updates and security fixes.
Portieris admission controller v0.13.28
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.28){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.16.40
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-40_release-notes){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.16.0+20250509
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.16.0+20250509){: external}.


## 19 May 2025, Worker node fix pack 4.16.40_1566_openshift
{: #cl-boms-41640_1566_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.40_1566_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.52.1.el8_10
:   Resolves the following CVEs: RHSA-2025:7531, CVE-2022-49011, CVE-2024-53141, RHSA-2024:3043, and CVE-2024-0690.


Red Hat OpenShift and Red Hat CoreOS 4.16.40
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-40_release-notes){: external}.


HAProxy 978e3c26ee7634e39a940696aaf57d9e374db5ce
:   


## 07 May 2025, Worker node fix pack 4.16.39_1565_openshift
{: #cl-boms-41639_1565_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.39_1565_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   Resolves the following CVEs: RHSA-2025:4341, CVE-2024-42292, CVE-2024-42322, CVE-2024-44990, CVE-2024-46826, CVE-2025-21927, RHSA-2025:4244, and CVE-2025-0395.


RHEL_8 4.18.0-553.51.1.el8_10
:   Resolves the following CVEs: RHSA-2024:3043, CVE-2024-0690, RHSA-2025:4051, CVE-2024-12243, RHSA-2025:3893, CVE-2024-53150, CVE-2024-53241, RHSA-2025:4049, and CVE-2024-12133.


Red Hat OpenShift and Red Hat CoreOS 4.16.39
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes.html#ocp-4-16-39_release-notes){: external}.


HAProxy 978e3c26ee7634e39a940696aaf57d9e374db5ce
:   Resolves the following CVEs: CVE-2024-12243, and CVE-2024-12133.


## Master fix pack 4.16.38_1564_openshift, released 30 April 2025
{: #41638_1564_openshift_M}

The following list shows the changes that are in the master fix pack 4.16.38_1564_openshift. Master patch updates are applied automatically. 


Calico v3.28.3
:   See the [Calico release notes](https://archive-os-3-28.netlify.app/calico/3.28/release-notes/#v3.28.3){: external}.
Cluster health image v1.6.8
:   New version contains updates and security fixes.
etcd v3.5.21
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.21){: external}.
{{site.data.keyword.cloud_notm}} Controller Manager v1.29.15-6
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} RBAC Operator d1545bd
:   New version contains updates and security fixes.
Key Management Service provider v2.10.12
:   New version contains updates and security fixes.
Portieris admission controller v0.13.26
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.26){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.16.38
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-38){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.16.0+20250414
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.16.0+20250414){: external}.
Tigera Operator v1.34.8
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.34.8){: external}.


## 21 April 2025, Worker node fix pack 4.16.38_1563_openshift
{: #cl-boms-41638_1563_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.38_1563_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.38.1.el9_5
:   Resolves the following CVEs: RHSA-2025:3937, and CVE-2024-53150.


RHEL_8 4.18.0-553.47.1.el8_10
:   Resolves the following CVEs: RHSA-2024:3043, CVE-2024-0690, RHSA-2025:3913, CVE-2024-8176, RHSA-2025:3828, and CVE-2025-0395.


Red Hat OpenShift and Red Hat CoreOS 4.16.38
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-38_release-notes){: external}.


HAProxy bb0015364d95e0a2e7ab83d4a659d1541cee183e
:   Resolves the following CVEs: CVE-2025-0395, and CVE-2024-8176.


## 08 April 2025, Worker node fix pack 4.16.38_1562_openshift
{: #cl-boms-41638_1562_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.38_1562_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.35.1.el9_5
:   Resolves the following CVEs: RHSA-2025:3407, CVE-2025-27363, RHSA-2025:3208, CVE-2025-21785, RHSA-2025:3406, CVE-2025-27516, RHSA-2025:3531, CVE-2024-8176, RHSA-2025:3506, and CVE-2024-43855.


RHEL_8 4.18.0-553.47.1.el8_10
:   Resolves the following CVEs: RHSA-2025:3210, CVE-2025-22869, RHSA-2025:3421, CVE-2025-27363, RHSA-2025:3367, CVE-2025-0624, RHSA-2025:3260, CVE-2025-21785, RHSA-2025:3388, CVE-2025-27516, RHSA-2024:3043, and CVE-2024-0690.


Red Hat OpenShift and Red Hat CoreOS 4.16.38
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-38_release-notes){: external}.


HAProxy 997a4ab1e89a5c8ccf3a6823785d7ab5e34b0c83
:   


## Master fix pack 4.16.36_1560_openshift, released 26 March 2025
{: #41636_1560_openshift_M}

The following list shows the changes that are in the master fix pack 4.16.36_1560_openshift. Master patch updates are applied automatically. 


Cluster health image v1.6.7
:   New version contains updates and security fixes.
etcd v3.5.18
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.18){: external}.
{{site.data.keyword.cloud_notm}} Controller Manager v1.29.15-1
:   New version contains updates and security fixes.
Key Management Service provider v2.10.11
:   New version contains updates and security fixes.
Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider 3232
:   New version contains updates and security fixes.
Portieris admission controller v0.13.25
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.25){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.16.36
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-36){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.16.0+20250313
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.16.0+20250313){: external}.


## 24 March 2025, Worker node fix pack 4.16.37_1561_openshift
{: #cl-boms-41637_1561_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.37_1561_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.33.1.el9_5
:   Resolves the following CVEs: RHSA-2025:2627, CVE-2023-52605, CVE-2023-52922, CVE-2024-50264, CVE-2024-50302, CVE-2024-53113, and CVE-2024-53197.


RHEL_8 4.18.0-553.45.1.el8_10
:   Resolves the following CVEs: RHSA-2025:2473, CVE-2024-50302, CVE-2024-53197, CVE-2024-57807, CVE-2024-57979, RHSA-2025:3026, CVE-2023-52922, RHSA-2025:2686, CVE-2024-56171, CVE-2025-24928, RHSA-2024:3043, CVE-2024-0690, RHSA-2025:2722, and CVE-2025-24528.


Red Hat OpenShift and Red Hat CoreOS 4.16.37
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-37_release-notes){: external}.


HAProxy 997a4ab1e89a5c8ccf3a6823785d7ab5e34b0c83
:   Resolves the following CVEs: CVE-2024-56171, CVE-2025-24528, and CVE-2025-24928.


## 11 March 2025, Worker node fix pack 4.16.37_1559_openshift
{: #cl-boms-41637_1559_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.37_1559_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.29.1.el9_5
:   


RHEL_8 4.18.0-553.42.1.el8_10
:   Resolves the following CVEs: RHSA-2024:3043, and CVE-2024-0690.


Red Hat OpenShift and Red Hat CoreOS 4.16.37
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-37_release-notes){: external}.


HAProxy 1d72cc8c7d02da6ba0340191fa8d9a86550e5090
:   


## 24 February 2025, Worker node fix pack 4.16.35_1558_openshift
{: #cl-boms-41635_1558_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.35_1558_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.26.1.el9_5
:   For more information, see [Release Notes for Red Hat Enterprise Linux 9.5](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/9.5_release_notes/index){: external}.Resolves the following CVEs: RHSA-2025:1681, CVE-2024-11187, RHSA-2025:0059, CVE-2024-46713, CVE-2024-50208, CVE-2024-50252, CVE-2024-53122, RHSA-2025:1262, CVE-2024-53104, RHSA-2024:9474, CVE-2024-3596, RHSA-2025:1350, CVE-2022-49043, RHSA-2025:1330, CVE-2024-12797, RHSA-2024:10244, CVE-2024-10963, RHSA-2025:0667, CVE-2024-56326, RHSA-2024:10759, CVE-2022-3064, CVE-2023-31315, RHSA-2024:9317, CVE-2024-6501, RHSA-2024:9333, CVE-2024-2511, CVE-2024-4603, CVE-2024-4741, CVE-2024-5535, RHSA-2024:9405, CVE-2021-3903, RHSA-2025:0925, CVE-2019-12900, RHSA-2024:9541, CVE-2024-50602, RHSA-2025:1346, CVE-2020-11023, RHSA-2024:10274, CVE-2024-41009, CVE-2024-42244, CVE-2024-50226, RHSA-2024:10939, CVE-2024-26615, CVE-2024-43854, CVE-2024-44994, CVE-2024-45018, CVE-2024-46695, CVE-2024-49949, CVE-2024-50251, RHSA-2024:11486, CVE-2024-27399, CVE-2024-38564, CVE-2024-45020, CVE-2024-46697, CVE-2024-47675, CVE-2024-49888, CVE-2024-50099, CVE-2024-50110, CVE-2024-50115, CVE-2024-50124, CVE-2024-50125, CVE-2024-50142, CVE-2024-50148, CVE-2024-50192, CVE-2024-50223, CVE-2024-50255, CVE-2024-50262, RHSA-2024:9315, CVE-2019-25162, CVE-2020-10135, CVE-2021-47098, CVE-2021-47101, CVE-2021-47185, CVE-2021-47384, CVE-2021-47386, CVE-2021-47428, CVE-2021-47429, CVE-2021-47432, CVE-2021-47454, CVE-2021-47457, CVE-2021-47495, CVE-2021-47497, CVE-2021-47505, CVE-2022-48669, CVE-2022-48672, CVE-2022-48703, CVE-2022-48804, CVE-2022-48929, CVE-2023-52445, CVE-2023-52451, CVE-2023-52455, CVE-2023-52462, CVE-2023-52464, CVE-2023-52466, CVE-2023-52467, CVE-2023-52473, CVE-2023-52475, CVE-2023-52477, CVE-2023-52482, CVE-2023-52486, CVE-2023-52492, CVE-2023-52498, CVE-2023-52501, CVE-2023-52513, CVE-2023-52520, CVE-2023-52528, CVE-2023-52560, CVE-2023-52565, CVE-2023-52585, CVE-2023-52594, CVE-2023-52595, CVE-2023-52606, CVE-2023-52614, CVE-2023-52615, CVE-2023-52619, CVE-2023-52621, CVE-2023-52622, CVE-2023-52624, CVE-2023-52625, CVE-2023-52632, CVE-2023-52634, CVE-2023-52635, CVE-2023-52637, CVE-2023-52643, CVE-2023-52648, CVE-2023-52649, CVE-2023-52650, CVE-2023-52656, CVE-2023-52659, CVE-2023-52661, CVE-2023-52662, CVE-2023-52663, CVE-2023-52664, CVE-2023-52674, CVE-2023-52676, CVE-2023-52679, CVE-2023-52680, CVE-2023-52683, CVE-2023-52686, CVE-2023-52689, CVE-2023-52690, CVE-2023-52696, CVE-2023-52697, CVE-2023-52698, CVE-2023-52703, CVE-2023-52730, CVE-2023-52731, CVE-2023-52740, CVE-2023-52749, CVE-2023-52751, CVE-2023-52756, CVE-2023-52757, CVE-2023-52758, CVE-2023-52762, CVE-2023-52775, CVE-2023-52784, CVE-2023-52788, CVE-2023-52791, CVE-2023-52811, CVE-2023-52813, CVE-2023-52814, CVE-2023-52817, CVE-2023-52819, CVE-2023-52831, CVE-2023-52833, CVE-2023-52834, CVE-2023-52837, CVE-2023-52840, CVE-2023-52859, CVE-2023-52867, CVE-2023-52869, CVE-2023-52878, CVE-2023-52902, CVE-2024-0340, CVE-2024-1151, CVE-2024-22099, CVE-2024-23307, CVE-2024-23848, CVE-2024-24857, CVE-2024-24858, CVE-2024-24859, CVE-2024-25739, CVE-2024-26589, CVE-2024-26591, CVE-2024-26601, CVE-2024-26603, CVE-2024-26605, CVE-2024-26611, CVE-2024-26612, CVE-2024-26614, CVE-2024-26618, CVE-2024-26631, CVE-2024-26638, CVE-2024-26641, CVE-2024-26645, CVE-2024-26646, CVE-2024-26650, CVE-2024-26656, CVE-2024-26660, CVE-2024-26661, CVE-2024-26662, CVE-2024-26663, CVE-2024-26664, CVE-2024-26669, CVE-2024-26670, CVE-2024-26672, CVE-2024-26674, CVE-2024-26675, CVE-2024-26678, CVE-2024-26679, CVE-2024-26680, CVE-2024-26686, CVE-2024-26691, CVE-2024-26700, CVE-2024-26704, CVE-2024-26707, CVE-2024-26708, CVE-2024-26712, CVE-2024-26717, CVE-2024-26719, CVE-2024-26725, CVE-2024-26733, CVE-2024-26734, CVE-2024-26740, CVE-2024-26743, CVE-2024-26744, CVE-2024-26746, CVE-2024-26757, CVE-2024-26758, CVE-2024-26759, CVE-2024-26761, CVE-2024-26767, CVE-2024-26772, CVE-2024-26774, CVE-2024-26782, CVE-2024-26785, CVE-2024-26786, CVE-2024-26803, CVE-2024-26812, CVE-2024-26815, CVE-2024-26835, CVE-2024-26837, CVE-2024-26838, CVE-2024-26840, CVE-2024-26843, CVE-2024-26846, CVE-2024-26857, CVE-2024-26861, CVE-2024-26862, CVE-2024-26863, CVE-2024-26870, CVE-2024-26872, CVE-2024-26878, CVE-2024-26882, CVE-2024-26889, CVE-2024-26890, CVE-2024-26892, CVE-2024-26894, CVE-2024-26899, CVE-2024-26900, CVE-2024-26901, CVE-2024-26903, CVE-2024-26906, CVE-2024-26907, CVE-2024-26915, CVE-2024-26920, CVE-2024-26921, CVE-2024-26922, CVE-2024-26924, CVE-2024-26927, CVE-2024-26928, CVE-2024-26933, CVE-2024-26934, CVE-2024-26937, CVE-2024-26938, CVE-2024-26939, CVE-2024-26940, CVE-2024-26950, CVE-2024-26951, CVE-2024-26953, CVE-2024-26958, CVE-2024-26960, CVE-2024-26962, CVE-2024-26964, CVE-2024-26973, CVE-2024-26975, CVE-2024-26976, CVE-2024-26984, CVE-2024-26987, CVE-2024-26988, CVE-2024-26989, CVE-2024-26990, CVE-2024-26992, CVE-2024-27003, CVE-2024-27004, CVE-2024-27010, CVE-2024-27011, CVE-2024-27012, CVE-2024-27013, CVE-2024-27014, CVE-2024-27015, CVE-2024-27017, CVE-2024-27023, CVE-2024-27025, CVE-2024-27038, CVE-2024-27042, CVE-2024-27048, CVE-2024-27057, CVE-2024-27062, CVE-2024-27079, CVE-2024-27389, CVE-2024-27395, CVE-2024-27404, CVE-2024-27410, CVE-2024-27414, CVE-2024-27431, CVE-2024-27436, CVE-2024-27437, CVE-2024-31076, CVE-2024-35787, CVE-2024-35794, CVE-2024-35795, CVE-2024-35801, CVE-2024-35805, CVE-2024-35807, CVE-2024-35808, CVE-2024-35809, CVE-2024-35810, CVE-2024-35812, CVE-2024-35814, CVE-2024-35817, CVE-2024-35822, CVE-2024-35824, CVE-2024-35827, CVE-2024-35831, CVE-2024-35835, CVE-2024-35838, CVE-2024-35840, CVE-2024-35843, CVE-2024-35847, CVE-2024-35853, CVE-2024-35854, CVE-2024-35855, CVE-2024-35859, CVE-2024-35861, CVE-2024-35862, CVE-2024-35863, CVE-2024-35864, CVE-2024-35865, CVE-2024-35866, CVE-2024-35867, CVE-2024-35869, CVE-2024-35872, CVE-2024-35876, CVE-2024-35877, CVE-2024-35878, CVE-2024-35880, CVE-2024-35886, CVE-2024-35888, CVE-2024-35892, CVE-2024-35894, CVE-2024-35900, CVE-2024-35904, CVE-2024-35905, CVE-2024-35908, CVE-2024-35912, CVE-2024-35913, CVE-2024-35918, CVE-2024-35923, CVE-2024-35924, CVE-2024-35925, CVE-2024-35927, CVE-2024-35928, CVE-2024-35930, CVE-2024-35931, CVE-2024-35938, CVE-2024-35939, CVE-2024-35942, CVE-2024-35944, CVE-2024-35946, CVE-2024-35947, CVE-2024-35950, CVE-2024-35952, CVE-2024-35954, CVE-2024-35957, CVE-2024-35959, CVE-2024-35973, CVE-2024-35976, CVE-2024-35979, CVE-2024-35983, CVE-2024-35991, CVE-2024-35995, CVE-2024-36002, CVE-2024-36006, CVE-2024-36010, CVE-2024-36015, CVE-2024-36022, CVE-2024-36028, CVE-2024-36030, CVE-2024-36031, CVE-2024-36477, CVE-2024-36881, CVE-2024-36882, CVE-2024-36884, CVE-2024-36885, CVE-2024-36891, CVE-2024-36896, CVE-2024-36901, CVE-2024-36902, CVE-2024-36905, CVE-2024-36917, CVE-2024-36920, CVE-2024-36926, CVE-2024-36927, CVE-2024-36928, CVE-2024-36930, CVE-2024-36932, CVE-2024-36933, CVE-2024-36936, CVE-2024-36939, CVE-2024-36940, CVE-2024-36944, CVE-2024-36945, CVE-2024-36955, CVE-2024-36956, CVE-2024-36960, CVE-2024-36961, CVE-2024-36967, CVE-2024-36974, CVE-2024-36977, CVE-2024-38388, CVE-2024-38555, CVE-2024-38581, CVE-2024-38596, CVE-2024-38598, CVE-2024-38600, CVE-2024-38604, CVE-2024-38605, CVE-2024-38618, CVE-2024-38627, CVE-2024-38629, CVE-2024-38632, CVE-2024-38635, CVE-2024-39276, CVE-2024-39291, CVE-2024-39298, CVE-2024-39471, CVE-2024-39473, CVE-2024-39474, CVE-2024-39479, CVE-2024-39486, CVE-2024-39488, CVE-2024-39491, CVE-2024-39497, CVE-2024-39498, CVE-2024-39499, CVE-2024-39501, CVE-2024-39503, CVE-2024-39507, CVE-2024-39508, CVE-2024-40901, CVE-2024-40903, CVE-2024-40906, CVE-2024-40907, CVE-2024-40913, CVE-2024-40919, CVE-2024-40922, CVE-2024-40923, CVE-2024-40924, CVE-2024-40925, CVE-2024-40930, CVE-2024-40940, CVE-2024-40945, CVE-2024-40948, CVE-2024-40965, CVE-2024-40966, CVE-2024-40967, CVE-2024-40988, CVE-2024-40989, CVE-2024-40997, CVE-2024-41001, CVE-2024-41007, CVE-2024-41008, CVE-2024-41012, CVE-2024-41020, CVE-2024-41032, CVE-2024-41038, CVE-2024-41039, CVE-2024-41042, CVE-2024-41049, CVE-2024-41056, CVE-2024-41057, CVE-2024-41058, CVE-2024-41060, CVE-2024-41063, CVE-2024-41065, CVE-2024-41077, CVE-2024-41079, CVE-2024-41082, CVE-2024-41084, CVE-2024-41085, CVE-2024-41089, CVE-2024-41092, CVE-2024-41093, CVE-2024-41094, CVE-2024-41095, CVE-2024-42070, CVE-2024-42078, CVE-2024-42084, CVE-2024-42090, CVE-2024-42101, CVE-2024-42114, CVE-2024-42123, CVE-2024-42124, CVE-2024-42125, CVE-2024-42132, CVE-2024-42141, CVE-2024-42154, CVE-2024-42159, CVE-2024-42226, CVE-2024-42228, CVE-2024-42237, CVE-2024-42238, CVE-2024-42240, CVE-2024-42245, CVE-2024-42258, CVE-2024-42268, CVE-2024-42271, CVE-2024-42276, CVE-2024-42301, CVE-2024-43817, CVE-2024-43826, CVE-2024-43830, CVE-2024-43842, CVE-2024-43856, CVE-2024-43865, CVE-2024-43866, CVE-2024-43869, CVE-2024-43870, CVE-2024-43879, CVE-2024-43888, CVE-2024-43892, CVE-2024-43911, CVE-2024-44947, CVE-2024-44960, CVE-2024-44965, CVE-2024-44970, CVE-2024-44984, CVE-2024-45005, RHSA-2024:9605, CVE-2024-42283, CVE-2024-46824, CVE-2024-46858, RHSA-2025:0578, CVE-2024-50154, CVE-2024-50275, CVE-2024-53088, RHSA-2025:1659, CVE-2023-52490, RHSA-2024:9331, CVE-2024-26458, CVE-2024-26461, CVE-2024-26462, RHSA-2024:9404, CVE-2024-2236, RHSA-2024:9401, CVE-2023-22655, CVE-2023-28746, CVE-2023-38575, CVE-2023-39368, CVE-2023-43490, CVE-2023-45733, CVE-2023-46103, RHSA-2024:11250, CVE-2024-10041, RHSA-2024:9150, CVE-2024-34064, RHSA-2024:9371, CVE-2024-8088, RHSA-2024:9468, CVE-2024-6232, RHSA-2024:10983, CVE-2024-11168, CVE-2024-9287, RHSA-2025:0377, and CVE-2024-3661.


RHEL_8 4.18.0-553.40.1.el8_10
:   Resolves the following CVEs: RHSA-2025:1675, CVE-2024-11187, RHSA-2025:1266, CVE-2024-53104, RHSA-2024:3043, CVE-2024-0690, RHSA-2025:1301, CVE-2020-11023, RHSA-2025:1517, and CVE-2022-49043.


Red Hat OpenShift and Red Hat CoreOS 4.16.35
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-35_release-notes){: external}.


HAProxy 1d72cc8c7d02da6ba0340191fa8d9a86550e5090
:   Resolves the following CVEs: CVE-2020-11023, and CVE-2022-49043.


## Master fix pack 4.16.32_1557_openshift, released 19 February 2025
{: #41632_1557_openshift_M}

The following list shows the changes that are in the master fix pack 4.16.32_1557_openshift. Master patch updates are applied automatically. 


{{site.data.keyword.cloud_notm}} Block Storage driver and plug-in v2.5.17
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} Controller Manager v1.29.13-3
:   New version contains updates and security fixes.
{{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor 449
:   New version contains updates and security fixes.
Key Management Service provider v2.10.10
:   New version contains updates and security fixes.
Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider 3178
:   New version contains updates and security fixes.
{{site.data.keyword.openshiftlong_notm}}. 4.16.32
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-32){: external}.


## 11 February 2025, Worker node fix pack 4.16.32_1556_openshift
{: #cl-boms-41632_1556_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.32_1556_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.23.2.el9_5
:   


RHEL_8 4.18.0-553.40.1.el8_10
:   Resolves the following CVEs: RHSA-2025:0711, CVE-2024-56326, RHSA-2024:3043, CVE-2024-0690, RHSA-2025:0733, CVE-2019-12900, RHSA-2025:1068, CVE-2024-26935, and CVE-2024-50275.


Red Hat OpenShift and Red Hat CoreOS 4.16.32
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-32_release-notes){: external}.


HAProxy 03d1ee01e9241d0e5ec93b9eb8986feb2771a01a
:   Resolves the following CVEs: CVE-2019-12900.


## 29 January 2025, Worker node fix pack 4.16.30_1554_openshift
{: #cl-boms-41630_1554_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.30_1554_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_8 4.18.0-553.36.1.el8_10
:   Resolves the following CVEs: RHSA-2024:3043, CVE-2024-0690, RHSA-2025:0288, and CVE-2024-3661.


RHEL_9 5.14.0-427.42.1.el9_4
:   


Red Hat OpenShift and Red Hat CoreOS 4.16.30
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-30_release-notes){: external}.


HAProxy 14daa781a66ca5ed5754656ce53c3cca4af580b5
:   


## Master fix pack 4.16.28_1550_openshift, released 22 January 2025
{: #41628_1550_openshift_M}

The following list shows the changes that are in the master fix pack 4.16.28_1550_openshift. Master patch updates are applied automatically. 


Cluster health image v1.6.4
:   New version contains updates and security fixes.
etcd v3.5.17
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.17){: external}.
{{site.data.keyword.cloud_notm}} Controller Manager v1.29.12-3
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} RBAC Operator cb4f333
:   New version contains updates and security fixes.
Key Management Service provider v2.10.9
:   New version contains updates and security fixes.
Portieris admission controller v0.13.23
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.23){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.16.28
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-28){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.16.0+20250102
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.16.0+20250102){: external}.


## 13 January 2025, Worker node fix pack 4.16.29_1549_openshift
{: #cl-boms-41629_1549_openshift_W}

The following list shows the components included in the worker node fix pack 4.16.29_1549_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_8 4.18.0-553.34.1.el8_10
:   Resolves the following CVEs: RHSA-2025:0065, CVE-2024-53088, CVE-2024-53122, RHSA-2024:3043, CVE-2024-0690, RHSA-2025:0012, CVE-2024-35195, RHSA-2024:11161, and CVE-2024-52337.


RHEL_9 5.14.0-427.42.1.el9_4
:   


Red Hat OpenShift and Red Hat CoreOS 4.16.29
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-29_release-notes){: external}.


HAProxy 14daa781a66ca5ed5754656ce53c3cca4af580b5
:   


## Worker node fix pack 4.16.27_1548_openshift, released 30 December 2024
{: #41627_1548_openshift_W}

The following list shows the changes that are in the worker node fix pack 4.16.27_1548_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 8 Packages
:   Worker node package updates for RHSA-2024:3043, CVE-2024-0690, RHSA-2024:11161, CVE-2024-52337.
{{site.data.keyword.openshiftshort}} and Red Hat CoreOS 4.16.27
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-27_release-notes){: external}.


## Worker node fix pack 4.16.26_1547_openshift, released 16 December 2024
{: #41626_1547_openshift_W}

The following list shows the changes that are in the worker node fix pack 4.16.26_1547_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 8 Packages 4.18.0-553.32.1.el8_10
:   Worker node kernel & package updates for RHSA-2024:3043, CVE-2024-0690, RHSA-2024:10943, CVE-2024-46695, CVE-2024-49949, CVE-2024-50082, CVE-2024-50099, CVE-2024-50110, CVE-2024-50142, CVE-2024-50192, CVE-2024-50256, CVE-2024-50264, RHSA-2024:10779, CVE-2024-11168, CVE-2024-9287, RHSA-2024:10784, CVE-2022-3064.
HAProxy 14daa78
:   Security fixes for CVE-2024-10963, CVE-2024-11168, CVE-2024-9287, CVE-2024-10041.
{{site.data.keyword.openshiftshort}} 4.16.26
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-26_release-notes){: external}.


## Worker node fix pack 4.16.23_1546_openshift, released 05 December 2024
{: #41623_1546_openshift_W}

The following list shows the changes that are in the worker node fix pack 4.16.23_1546_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 8 Packages 4.18.0-553.30.1.el8_10
:   Worker node kernel & package updates for RHSA-2024:10379, CVE-2024-10041, CVE-2024-10963, RHSA-2024:3043, CVE-2024-0690, RHSA-2024:10289, CVE-2021-33198, CVE-2021-4024, CVE-2024-9676, RHSA-2024:10281, CVE-2024-27043, CVE-2024-27399, CVE-2024-38564, CVE-2024-46858.
RHEL 9 Packages
:   
HAProxy
:   
{{site.data.keyword.openshiftshort}} and Red Hat CoreOS 4.16.23
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes){: external}.


## Master fix pack 4.16.23_1545_openshift, released 04 December 2024
{: #41623_1545_openshift_M}

The following list shows the changes that are in the master fix pack 4.16.23_1545_openshift. Master patch updates are applied automatically. 


{{site.data.keyword.cloud_notm}} Controller Manager v1.29.10-4
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} RBAC Operator 743ed58
:   New version contains updates and security fixes.
Key Management Service provider v2.10.8
:   New version contains updates and security fixes.
Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider 3079
:   New version contains updates and security fixes.
Portieris admission controller v0.13.21
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.21){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.16.23
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-23){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.16.0+20241107
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.16.0+20241107){: external}.


## Worker node fix pack 4.16.21_1544_openshift, released 18 November 2024
{: #41621_1544_openshift_W}

The following list shows the changes that are in the worker node fix pack 4.16.21_1544_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 8 Packages 4.18.0-553.27.1.el8_10
:   Worker node kernel & package updates for RHSA-2024:8846, CVE-2024-9341, CVE-2024-9407, CVE-2024-9675, RHSA-2024:8860, CVE-2024-3596, RHSA-2024:9689, CVE-2018-12699, RHSA-2024:8922, CVE-2019-12900, RHSA-2024:3043, CVE-2024-0690, RHSA-2024:9502, CVE-2024-50602, RHSA-2024:8849, CVE-2023-45539, RHSA-2024:8856, CVE-2022-48773, CVE-2022-48936, CVE-2023-52492, CVE-2024-24857, CVE-2024-26851, CVE-2024-26924, CVE-2024-26976, CVE-2024-27017, CVE-2024-27062, CVE-2024-35839, CVE-2024-35898, CVE-2024-35939, CVE-2024-38540, CVE-2024-38541, CVE-2024-38586, CVE-2024-38608, CVE-2024-39503, CVE-2024-40924, CVE-2024-40961, CVE-2024-40983, CVE-2024-40984, CVE-2024-41009, CVE-2024-41042, CVE-2024-41066, CVE-2024-41092, CVE-2024-41093, CVE-2024-42070, CVE-2024-42079, CVE-2024-42244, CVE-2024-42284, CVE-2024-42292, CVE-2024-42301, CVE-2024-43854, CVE-2024-43880, CVE-2024-43889, CVE-2024-43892, CVE-2024-44935, CVE-2024-44989, CVE-2024-44990, CVE-2024-45018, CVE-2024-46826, CVE-2024-47668, CIS benchmark compliance: [1.4.3](https://workbench.cisecurity.org/sections/2250437/recommendations/3599694){: external}, [1.4.4](https://workbench.cisecurity.org/sections/2250437/recommendations/3599695){: external}, [1.6.2](https://workbench.cisecurity.org/sections/2250440/recommendations/3599717){: external}, [1.6.4](https://workbench.cisecurity.org/sections/2250440/recommendations/3599722){: external}.
{{site.data.keyword.openshiftshort}} and Red Hat CoreOS 4.16.21
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-21_release-notes){: external}.
HAProxy 55c148
:   Security fixes for CVE-2023-45539, CVE-2024-3596, CVE-2019-12900, CVE-2024-50602.


## Master fix pack 4.16.19_1543_openshift, released 13 November 2024
{: #41619_1543_openshift_M}

The following list shows the changes that are in the master fix pack 4.16.19_1543_openshift. Master patch updates are applied automatically. 


{{site.data.keyword.cloud_notm}} Block Storage driver and plug-in v2.5.16
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} Controller Manager v1.29.10-2
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} RBAC Operator c4a05b0
:   New version contains updates and security fixes.
{{site.data.keyword.openshiftlong_notm}}. 4.16.19
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-19){: external}.


## Worker node fix pack 4.16.19_1542_openshift, released 04 November 2024
{: #41619_1542_openshift_W}

The following list shows the changes that are in the worker node fix pack 4.16.19_1542_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 8 Packages
:   Package updates for RHSA-2024:3043, CVE-2024-0690, RHSA-2024:8359, CVE-2024-6232
RHEL 9 Packages 5.14.0-427.42.1.el9_4
:   Kernel and package updates for RHSA-2024:8617, CVE-2021-47383, CVE-2024-2201, CVE-2024-26640, CVE-2024-26826, CVE-2024-26923, CVE-2024-26935, CVE-2024-26961, CVE-2024-36244, CVE-2024-39472, CVE-2024-39504, CVE-2024-40904, CVE-2024-40931, CVE-2024-40960, CVE-2024-40972, CVE-2024-40977, CVE-2024-40995, CVE-2024-40998, CVE-2024-41005, CVE-2024-41013, CVE-2024-41014, CVE-2024-43854, CVE-2024-45018, RHSA-2024:8446, CVE-2024-6232
{{site.data.keyword.openshiftshort}} and Red Hat CoreOS 4.16.19
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-19_release-notes){: external}.
Haproxy
:   


## Master fix pack 4.16.16_1541_openshift, released 30 October 2024
{: #41616_1541_openshift_M}

The following list shows the changes that are in the master fix pack 4.16.16_1541_openshift. Master patch updates are applied automatically. 


Calico v3.28.2
:   See the [Calico release notes](https://archive-os-3-28.netlify.app/calico/3.28/release-notes/#v3.28.2){: external}.
Cluster health image v1.6.3
:   New version contains updates and security fixes.
etcd v3.5.16
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.16){: external}.
{{site.data.keyword.cloud_notm}} Controller Manager v1.29.9-6
:   New version contains updates and security fixes.
{{site.data.keyword.filestorage_full_notm}} plug-in and monitor 447
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} RBAC Operator 77dac6b
:   New version contains updates and security fixes.
Key Management Service provider v2.10.7
:   New version contains updates and security fixes.
Portieris admission controller v0.13.20
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.20){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.16.16
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-16){: external}.
Tigera Operator v1.34.5
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.34.5){: external}.


## Worker node fix pack 4.16.17_1540_openshift, released 21 October 2024
{: #41617_1540_openshift_W}

The following list shows the changes that are in the worker node fix pack 4.16.17_1540_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 8 Packages
:   Package updates for RHSA-2024:8038, CVE-2023-45290, CVE-2024-34155, CVE-2024-34156, CVE-2024-34158, RHSA-2024:7848, CVE-2024-5535, RHSA-2024:3043, CVE-2024-0690.
RHEL 9 Packages 5.14.0-427.40.1.el9_4
:   Kernel and package updates for RHSA-2024:8162, CVE-2021-47385, CVE-2023-28746, CVE-2023-52658, CVE-2024-27403, CVE-2024-35989, CVE-2024-36889, CVE-2024-36978, CVE-2024-38556, CVE-2024-39483, CVE-2024-39502, CVE-2024-40959, CVE-2024-42079, CVE-2024-42272, CVE-2024-42284. CIS benchmark compliance: [5.2.18.](https://workbench.cisecurity.org/sections/1594521/recommendations/2564555){: external},[2.1.2](https://workbench.cisecurity.org/sections/1594532/recommendations/2564483){: external}, [3.3.7](https://workbench.cisecurity.org/sections/1594530/recommendations/2564508){: external}, [2.2.14](https://workbench.cisecurity.org/sections/1594533/recommendations/2564557){: external}.
{{site.data.keyword.openshiftshort}} and Red Hat CoreOS 4.16.17
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-17_release-notes){: external}.
Haproxy 88598691
:   Security fixes for CVE-2024-5535.


## Worker node fix pack 4.16.15_1539_openshift, released 09 October 2024
{: #41615_1539_openshift_W}

The following list shows the changes that are in the worker node fix pack 4.16.15_1539_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 8 Packages 4.18.0-553.22.1.el8_10
:   CIS benchmark compliance: [1.4.2.](https://workbench.cisecurity.org/sections/2250437/recommendations/3599691){: external}. Kernel and package updates for RHSA-2024:7000, CVE-2021-46984, CVE-2021-47097, CVE-2021-47101, CVE-2021-47287, CVE-2021-47289, CVE-2021-47321, CVE-2021-47338, CVE-2021-47352, CVE-2021-47383, CVE-2021-47384, CVE-2021-47385, CVE-2021-47386, CVE-2021-47393, CVE-2021-47412, CVE-2021-47432, CVE-2021-47441, CVE-2021-47455, CVE-2021-47466, CVE-2021-47497, CVE-2021-47527, CVE-2021-47560, CVE-2021-47582, CVE-2021-47609, CVE-2022-48619, CVE-2022-48754, CVE-2022-48760, CVE-2022-48804, CVE-2022-48836, CVE-2022-48866, CVE-2023-52470, CVE-2023-52476, CVE-2023-52478, CVE-2023-52522, CVE-2023-52605, CVE-2023-52683, CVE-2023-52798, CVE-2023-52800, CVE-2023-52809, CVE-2023-52817, CVE-2023-52840, CVE-2023-6040, CVE-2024-23848, CVE-2024-26595, CVE-2024-26600, CVE-2024-26638, CVE-2024-26645, CVE-2024-26649, CVE-2024-26665, CVE-2024-26717, CVE-2024-26720, CVE-2024-26769, CVE-2024-26846, CVE-2024-26855, CVE-2024-26880, CVE-2024-26894, CVE-2024-26923, CVE-2024-26939, CVE-2024-27013, CVE-2024-27042, CVE-2024-35809, CVE-2024-35877, CVE-2024-35884, CVE-2024-35944, CVE-2024-35989, CVE-2024-36883, CVE-2024-36901, CVE-2024-36902, CVE-2024-36919, CVE-2024-36920, CVE-2024-36922, CVE-2024-36939, CVE-2024-36953, CVE-2024-37356, CVE-2024-38558, CVE-2024-38559, CVE-2024-38570, CVE-2024-38579, CVE-2024-38581, CVE-2024-38619, CVE-2024-39471, CVE-2024-39499, CVE-2024-39501, CVE-2024-39506, CVE-2024-40901, CVE-2024-40904, CVE-2024-40911, CVE-2024-40912, CVE-2024-40929, CVE-2024-40931, CVE-2024-40941, CVE-2024-40954, CVE-2024-40958, CVE-2024-40959, CVE-2024-40960, CVE-2024-40972, CVE-2024-40977, CVE-2024-40978, CVE-2024-40988, CVE-2024-40989, CVE-2024-40995, CVE-2024-40997, CVE-2024-40998, CVE-2024-41005, CVE-2024-41007, CVE-2024-41008, CVE-2024-41012, CVE-2024-41013, CVE-2024-41014, CVE-2024-41023, CVE-2024-41035, CVE-2024-41038, CVE-2024-41039, CVE-2024-41040, CVE-2024-41041, CVE-2024-41044, CVE-2024-41055, CVE-2024-41056, CVE-2024-41060, CVE-2024-41064, CVE-2024-41065, CVE-2024-41071, CVE-2024-41076, CVE-2024-41090, CVE-2024-41091, CVE-2024-41097, CVE-2024-42084, CVE-2024-42090, CVE-2024-42094, CVE-2024-42096, CVE-2024-42114, CVE-2024-42124, CVE-2024-42131, CVE-2024-42152, CVE-2024-42154, CVE-2024-42225, CVE-2024-42226, CVE-2024-42228, CVE-2024-42237, CVE-2024-42238, CVE-2024-42240, CVE-2024-42246, CVE-2024-42265, CVE-2024-42322, CVE-2024-43830, CVE-2024-43871, RHSA-2024:7481, CVE-2023-20584, CVE-2023-31315, CVE-2023-31356, RHSA-2024:3043, CVE-2024-0690, RHSA-2024:6969, CVE-2023-45290, CVE-2024-24783, CVE-2024-24784, CVE-2024-24788, CVE-2024-24791, RHSA-2024:6989, CVE-2024-45490, CVE-2024-45491, CVE-2024-45492, RHSA-2024:6975, CVE-2024-4032, CVE-2024-6232, CVE-2024-6923.
{{site.data.keyword.openshiftshort}} and Red Hat CoreOS 4.16.15
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-15_release-notes){: external}.
Haproxy 67d03375
:   Security fixes for CVE-2024-4032, CVE-2024-6232, CVE-2024-6923, CVE-2024-45490, CVE-2024-45491, CVE-2024-45492.


## Master fix pack 4.16.10_1537_openshift, released 25 September 2024
{: #41610_1537_openshift_M}

The following list shows the changes that are in the master fix pack 4.16.10_1537_openshift. Master patch updates are applied automatically. 


Calico API server v3.28.1
:   See the [Calico release notes](https://docs.tigera.io/archive){: external}.
{{site.data.keyword.cloud_notm}} Block Storage driver and plug-in v2.5.15
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} Controller Manager v1.29.9-1
:   New version contains updates and security fixes.
{{site.data.keyword.filestorage_full_notm}} plug-in and monitor 446
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} RBAC Operator 5b17dab
:   New version contains updates and security fixes.
Key Management Service provider v2.10.5
:   New version contains updates and security fixes.
Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider 3051
:   New version contains updates and security fixes.
{{site.data.keyword.openshiftlong_notm}}. 4.16.10
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-10){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.16.0+20240913
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.16.0+20240913){: external}.


## Worker node fix pack 4.16.13_1538_openshift, released 23 September 2024
{: #41613_1538_openshift_W}

The following list shows the changes that are in the worker node fix pack 4.16.13_1538_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 8 Packages
:   Package updates for RHSA-2024:3043, CVE-2024-0690.
{{site.data.keyword.openshiftshort}}. 4.16.13
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-13_release-notes){: external}.


## Worker node fix pack 4.16.10_1535_openshift, released 10 September 2024
{: #41610_1535_openshift_W}

The following list shows the changes that are in the worker node fix pack 4.16.10_1535_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

{{site.data.keyword.openshiftshort}}. 4.16.10
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-10_release-notes){: external}.
RHEL 8 Packages
:   Worker node package updates for RHSA-2024:3043, CVE-2024-0690, RHSA-2024:5962, CVE-2024-4032, CVE-2024-6345, CVE-2024-6923, CVE-2024-8088.


## Master fix pack 4.16.7_1532_openshift and worker node fix pack 4.16.6_1531_openshift, released 30 August 2024
{: #openshift_changelog_4167_1532}

Calico v3.28.1
:   See the [Calico release notes](https://archive-os-3-28.netlify.app/calico/3.28/release-notes/){: external}.
Cluster health image v1.6.2
:   New version contains updates and security fixes.
IBM Cloud Controller Manager v1.29.8-1
:   New version contains updates and security fixes.
Key Management Service provider v2.10.4
:   New version contains updates and security fixes. In addition, only [KMS v2](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/){: external} is supported. KMS v1 instances were migrated to KMS v2 as part of the Red Hat OpenShift on IBM Cloud version 4.15 release.
Pause container image 3.10
:   See the [pause container image release notes](https://github.com/kubernetes/kubernetes/blob/master/build/pause/CHANGELOG.md){: external}.
{{site.data.keyword.redhat_openshift_notm}} (master) 4.16.7
:   See the [Red Hat OpenShift release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-7_release-notes){: external}.
{{site.data.keyword.redhat_openshift_notm}} (worker node) 4.16.6
:   See the [Red Hat OpenShift release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/release_notes/ocp-4-16-release-notes#ocp-4-16-6_release-notes){: external}.
{{site.data.keyword.redhat_openshift_notm}} on IBM Cloud Control Plane Operator, Metrics Server, and toolkit 4.16.0+20240814
:   See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.16.0+20240814){: external}.
Tigera Operator v1.34.3
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.34.3){: external}.
