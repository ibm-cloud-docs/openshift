---

copyright:
  years: 2024, 2025

lastupdated: "2025-10-17"


keywords: change log, version history, 4.19_openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# 4.19 version change log
{: #openshift_changelog_419}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run this version. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #changelog_overview_419}


Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security){: external} for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}

## Version 4.19
{: #419_components}


### Worker node fix pack 4.19.14_1549_openshift, released 08 October 2025
{: #cl-boms-41914_1549_openshift_W}

The following table shows the components included in the worker node fix pack 4.19.14_1549_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-503.40.1.el9_5|N/A|
|Red Hat OpenShift and Red Hat CoreOS|4.19.14|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/release_notes/ocp-4-19-release-notes.html#ocp-4-19-14_release-notes).|
|HAProxy|e0a48fcf355d98dc769ea048d2fd02044b11ed62|N/A|
{: caption="4.19.14_1549_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41914_1549_openshift_W-component-table}



### Master fix pack 4.19.13_1548_openshift, released 07 October 2025
{: #41913_1548_openshift_M}

The following table shows the changes that are in the master fix pack 4.19.13_1548_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.29.4 | v3.29.5 | See the [Calico release notes](https://docs.tigera.io/calico/3.29/release-notes/#v3.29.5){: external}. |
| etcd | v3.5.22 | v3.5.23 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.23){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.32.8-1 | v1.32.9-2 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor | 451 | 452 | New version contains updates and security fixes. |
| Key Management Service provider | v2.10.16 | v2.10.17 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.29 | v0.13.30 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.30){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.19.9 | 4.19.13 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19#ocp-4-19-13){: external}. |
| Tigera Operator | v1.36.11 | v1.36.13 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.36.13){: external}. |
{: caption="Changes since version 4.19.9_1541_openshift" caption-side="bottom"}



### Worker node fix pack 4.19.12_1545_openshift, released 23 September 2025
{: #cl-boms-41912_1545_openshift_W}

The following table shows the components included in the worker node fix pack 4.19.12_1545_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-503.40.1.el9_5|N/A|
|Red Hat OpenShift and Red Hat CoreOS|4.19.12|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/release_notes/ocp-4-19-release-notes.html#ocp-4-19-12_release-notes).|
|HAProxy|e0a48fcf355d98dc769ea048d2fd02044b11ed62|N/A|
{: caption="4.19.12_1545_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41912_1545_openshift_W-component-table}



### Worker node fix pack 4.19.10_1543_openshift, released 15 September 2025
{: #cl-boms-41910_1543_openshift_W}

The following table shows the components included in the worker node fix pack 4.19.10_1543_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-503.40.1.el9_5|SELinux policy update for container runtime BPF execution to allow workloads like GPU Operators to run successfully|
|Red Hat OpenShift and Red Hat CoreOS|4.19.10|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/release_notes/ocp-4-19-release-notes.html#ocp-4-19-10_release-notes).|
|HAProxy|e0a48fcf355d98dc769ea048d2fd02044b11ed62|N/A|
{: caption="4.19.10_1543_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41910_1543_openshift_W-component-table}



### Worker node fix pack 4.19.10_1542_openshift, released 09 September 2025
{: #cl-boms-41910_1542_openshift_W}

The following table shows the components included in the worker node fix pack 4.19.10_1542_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|RHEL_9|5.14.0-503.40.1.el9_5|N/A|
|Red Hat OpenShift and Red Hat CoreOS|4.19.10|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/release_notes/ocp-4-19-release-notes.html#ocp-4-19-10_release-notes).|
|HAProxy|e0a48fcf355d98dc769ea048d2fd02044b11ed62|Resolves the following CVEs: [CVE-2025-6020](https://nvd.nist.gov/vuln/detail/CVE-2025-6020){: external}, and [CVE-2025-8941](https://nvd.nist.gov/vuln/detail/CVE-2025-8941){: external}.|
{: caption="4.19.10_1542_openshift fix pack." caption-side="bottom"}
{: #cl-boms-41910_1542_openshift_W-component-table}



### Master fix pack 4.19.9_1541_openshift and worker node fix pack 4.19.9_1540_openshift, released 03 September 2025
{: #4199_15411M_and_4199_1540W}

The following table shows the components included in master fix pack 4.19.9_1541_openshift and worker node fix pack 4.19.9_1540_openshift. Master patch updates are applied automatically. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| IBM Cloud Controller Manager | v1.31.11-2 | v1.32.8-1 | New version contains updates and security fixes. |
| Red Hat OpenShift (master) | 4.18.21 | 4.19.9 | See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/release_notes/ocp-4-19-release-notes#ocp-4-19-9_release-notes){: external}. |
| Red Hat OpenShift (worker) | 4.18.22 | 4.19.9 | See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/release_notes/ocp-4-19-release-notes#ocp-4-19-9_release-notes){: external}. |
{: caption="Changes since master fix pack 4.18.21_1555_openshift and worker fix pack 4.18.22_1556_openshift" caption-side="bottom"}
