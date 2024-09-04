---

copyright:
  years: 2023, 2024
lastupdated: "2024-09-04"


keywords: openshift, 4.16, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# Version 4.16 change log
{: #openshift_changelog_416}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.16. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #openshift_changelog_overview_416}

Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security){: external} for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}


### Change log for master fix pack 4.16.7_1532_openshift and worker node fix pack 4.16.6_1531_openshift, released 30 August 2024

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.27.4 | v3.28.1 | See the [Calico release notes](https://docs.tigera.io/calico/3.28/release-notes/){: external}. |
| Cluster health image | v1.5.8 | v1.6.2 | New version contains updates and security fixes. |
| IBM Cloud Controller Manager | v1.28.13-1 | v1.29.8-1 | New version contains updates and security fixes. |
| Key Management Service provider | v2.9.9 | v2.10.4 | New version contains updates and security fixes. In addition, only [KMS v2](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/){: external} is supported. KMS v1 instances were migrated to KMS v2 as part of the Red Hat OpenShift on IBM Cloud version 4.15 release. |
| Pause container image | 3.9 | 3.10 | See the [pause container image release notes](https://github.com/kubernetes/kubernetes/blob/master/build/pause/CHANGELOG.md){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} (master) | 4.15.25 | 4.16.7 | See the [Red Hat OpenShift release notes](https://docs.openshift.com/container-platform/4.16/release_notes/ocp-4-16-release-notes.html#ocp-4-16-7_release-notes){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} (worker node) | 4.15.28 | 4.16.6 | See the [Red Hat OpenShift release notes](https://docs.openshift.com/container-platform/4.16/release_notes/ocp-4-16-release-notes.html#ocp-4-16-6_release-notes){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud Control Plane Operator, Metrics Server, and toolkit | 4.15.0+20240814 | 4.16.0+20240814 | See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.16.0+20240814){: external}. |
| Tigera Operator | v1.32.10 | v1.34.3 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.34.3){: external}. |
{: caption="Changes since master fix pack 4.15.25_1556_openshift and worker fix pack 4.15.28_1557_openshift." caption-side="bottom"}

