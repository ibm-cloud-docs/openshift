---

copyright:
  years: 2026, 2026

lastupdated: "2026-05-13"


keywords: change log, version history, 4.21_openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# 4.21 version change log
{: #openshift_changelog_421}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run this version. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #changelog_overview_421}


Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security){: external} for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}

## Version 4.21
{: #421_components}

### Change log for master fix pack 4.21.13_1516_openshift, released 13 May 2026
{: #42113_1516_openshift_M}

The following table shows the changes that are in the master fix pack 4.21.13_1516_openshift. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| IBM Cloud Controller Manager | v1.33.10-2 | v1.34.7-1 | New version contains updates and security fixes. |
| Kubernetes pause container | 3.10.1 | 3.10.2 | New version contains updates and security fixes. |
| Red Hat OpenShift | 4.20.18 | 4.21.13 | See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/release_notes/ocp-4-21-release-notes#ocp-4-21-13_release-notes){: external}. |
{: caption="Changes since master version 4.20.18_1545_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.21.10_1514_openshift, released 13 May 2026
{: #42110_1514_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.21.10_1514_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Red Hat OpenShift | 4.20.15 | 4.21.10 | See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/release_notes/ocp-4-21-release-notes#ocp-4-21-10_release-notes){: external}. |
{: caption="Changes since worker node version 4.20.15_1544_openshift" caption-side="bottom"}
