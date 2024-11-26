---

copyright:
  years: 2024, 2024
lastupdated: "2024-11-26"


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


### Change log for worker node fix pack 4.17.4_1516_openshift, released 21 November 2024
{: #4174_1516_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.17.4_1516_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}


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
