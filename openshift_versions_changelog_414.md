---

copyright:
  years: 2023, 2024
lastupdated: "2024-02-01"


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

### Change log for master fix pack 4.14.8_1545_openshift, released 31 January 2024
{: #4148_1545_openshift_M}

The following table shows the changes that are in the master fix pack 4.14.8_1545_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.26.3 | v3.26.4 | See the [Calico release notes](https://docs.tigera.io/calico/3.26/release-notes/#v3.26.4){: external}. |
| Calico Operator | v1.30.7 | v1.30.9 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.30.9){: external}. |
| Calico policy controller | v3.26.3 | v3.26.4 | See the [Calico release notes](https://github.com/projectcalico/calico/blob/release-v3.26/release-notes/v3.26.4-release-notes.md){: external}. |
| Cluster health image | v1.5.0 | v1.5.1 | New version contains security fixes. |
| etcd | v3.5.10 | v3.5.11 | See the [etcd release notes](https://github.com/coreos/etcd/releases/v3.5.11){: external}. |
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







