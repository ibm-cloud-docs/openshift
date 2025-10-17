---

copyright:
  years: 2024, 2025

lastupdated: "2025-10-17"


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
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.31.13-1 | v1.31.13-2 | https://github.ibm.com/alchemy-containers/armada-lb/compare/v1.31.13-1...v1.31.13-2 |
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
|Red Hat OpenShift and Red Hat CoreOS|4.18.24|For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/release_notes/ocp-4-18-release-notes#ocp-4-18-24).|
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
| OpenShift | 4.17.24-x86_64 | 4.18.11-x86_64 | [OpenShift docs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/about/welcome-index){: external}. |
| Portieris admission controller | v0.13.26 | v0.13.28 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.13.28){: external}. |
| Red Hat OpenShift on IBM Cloud Control Plane Operator, Metrics Server, and toolkit | 4.17.0+20250414 | N/A | Red Hat OpenShift on IBM Cloud 4.18 now utilizes [Red Hat HyperShift](https://github.com/openshift/hypershift){: external} in place of the toolkit. Also, see the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases){: external}. |
| Tigera Operator | v1.34.8 | v1.36.5 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.36.5){: external}. |
{: caption="Changes since master fix pack 4.17.24_1537_openshift and worker fix pack 4.17.25_1536_openshift." caption-side="bottom"}
