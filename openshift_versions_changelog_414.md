---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-03"


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







