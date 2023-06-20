---

copyright:
  years: 2023, 2023
lastupdated: "2023-06-20"

keywords: openshift, 4.13, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# Version 4.13 change log
{: #openshift_changelog_413}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.13. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #openshift_changelog_overview_413}

Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security){: external} for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}


### Change log for worker node fix pack 4.13.3_1523_openshift, released 19 June 2023
{: #4133_1523_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.3_1523_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. |4.13.1|4.13.3|see [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-3){: external}. |
| RHEL 8 Packages | N/A | N/A | Worker node package updates for [CVE-2023-32067](https://nvd.nist.gov/vuln/detail/CVE-2023-32067){: external},[CVE-2023-24329](https://nvd.nist.gov/vuln/detail/CVE-2023-24329){: external}. |
{: caption="Changes since version 4.13.1_1521_openshift" caption-side="bottom"}


### Change log for master fix pack 4.13.0_1522_openshift and worker node fix pack 4.13.1_1521_openshift, released 14 June 2023
{: #4.13.0_1522_openshiftM_4.13.1_1521_openshiftW}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.25.1 | v3.26.0 | See the [Calico release notes](https://docs.tigera.io/archive){: external}. |
| Calico Operator | v1.29.3 | v1.30.2 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.30.2){: external}. |
| etcd | v3.5.8 | v3.5.9 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.9){: external}. |
| IBM Cloud Controller Manager | v1.25.9-7 | v1.26.5-5 | Updated to support the Kubernetes `1.26.5` release. Updated `Go` dependencies and to `Go` version `1.19.9`. Updated `calicoctl` to version `v3.25.1` and `vpcctl` to version `v0.15.0`. |
| Key Management Service provider | v2.6.6 | v2.7.0 | Secret encryption support added for clusters in Satellite locations with CoreOS enabled. Updated `Go` dependencies. |
| Red Hat OpenShift (master) | 4.12.16 | 4.13.0 | See the [Red Hat OpenShift release notes](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-0-ga){: external}. |
| Red Hat OpenShift (worker node) | 4.12.19 | 4.13.1 | See the [Red Hat OpenShift release notes](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-1){: external}. |
| Red Hat OpenShift configuration | N/A | N/A | Updated the [feature gate configuration](/docs/openshift?topic=openshift-service-settings#feature-gates){: external}. |
| Red Hat OpenShift on IBM Cloud Control Plane Operator and Metrics Server | v4.12.0-20230417 | v4.13.0-20230515 | See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.13.0+20230515){: external}. |
| Red Hat OpenShift on IBM Cloud toolkit | 4.12.0+20230417 | 4.13.0+20230515 | See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.13.0+20230515){: external}. |
{: caption="Changes since master fix pack 4.12.16_1545_openshift and worker fix pack 4.12.19_1546_openshift." caption-side="bottom"}


