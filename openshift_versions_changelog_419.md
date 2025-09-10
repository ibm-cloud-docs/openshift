---

copyright:
  years: 2024, 2025

lastupdated: "2025-09-10"


keywords: change log, version history, 4.19_openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

<!-- The content in this topic is auto-generated except for reuse-snippets indicated with {[ ]}. -->


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
