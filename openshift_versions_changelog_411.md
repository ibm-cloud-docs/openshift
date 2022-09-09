---

copyright:
  years: 2022, 2022
lastupdated: "2022-09-09"

keywords: openshift, 4.11, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Version 4.11 change log
{: #openshift_changelog_411}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.11. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #openshift_changelog_overview_411}

Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security) for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include a {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_changelog).
{: tip}


## Change logs
{: #411_changelog}

Review the version 4.11 change log.
{: shortdesc}

### Change log for master fix pack 4.11.0_1519_openshift and worker node fix pack 4.11.1_1520_openshift, released 31 August 2022
{: #4.11.0_1519_openshift-and-4.11.1_1520_openshift}

The following table shows the changes that are in the master fix pack 4.11.0_1519_openshift and worker node fix pack 4.11.1_1520_openshift. Master patch updates are applied automatically. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.22.2 | v3.23.3 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases){: external}. |
| Calico Operator | v1.25.7 | v1.27.12 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.27.12){: external}. |
| Cluster health image | v1.3.9 | v1.3.10 | Updated `Go` dependencies and to `Go` version `1.18.5`. |
| etcd | v3.4.18 | v3.5.4 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.4){: external}. |
| IBM Calico extension | 997 | 1006 | Updated to `Go` version `1.17.13`. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.8 | v2.2.9 | Updated to `Go` version `1.18.5`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.8-7 | v1.24.4-1 | Updated `Go` dependencies and to `Go` version `1.18.5`. Updated to support the Kubernetes `1.24.4` release. [Disabling load balancer NodePort allocation](https://kubernetes.io/docs/concepts/services-networking/service/#load-balancer-nodeport-allocation){: external} is now prevented for VPC load balancers. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 412 | 414 | Updated to `Go` version `1.18.5`. Updated universal base image (UBI) to version `8.6-902` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 0a187a4 | dc1725a | Updated `Go` dependencies and to `Go` version `1.18.3`. |
| Key Management Service provider | v2.5.7 | v2.5.8 | Updated `Go` dependencies. |
| Load balancer and load balancer monitor for IBM Cloud Provider | 2058 | 2110 | Updated `Go` dependencies and to `Go` version `1.17.13`. |
| Red Hat OpenShift (master) | 4.10.22 | 4.11.0 | See the [OpenShift release notes](https://docs.openshift.com/container-platform/4.11/release_notes/ocp-4-11-release-notes.html#ocp-4-11-0-ga){: external}. |
| Red Hat OpenShift (worker) | 4.10.26 | 4.11.1 | See the [OpenShift release notes](https://docs.openshift.com/container-platform/4.11/release_notes/ocp-4-11-release-notes.html){: external}. |
| OpenVPN client | 2.5.6-r1-IKS-629 | 2.5.6-r1-IKS-648 | Update image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097) and [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}. |
| OpenVPN Operator image | v1.4.7 | v1.4.8 | Updated Ansible operator base image to version `v1.22.2` to resolve CVEs. |
| OpenVPN server | 2.5.6-r1-IKS-628 | 2.5.6-r1-IKS-647 | Update image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external} and [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}. |
| Pause container image | 3.7 | 3.8 | See the [pause container image release notes](https://github.com/kubernetes/kubernetes/blob/master/build/pause/CHANGELOG.md){: external}. |
| Portieris admission controller | v0.12.5 | v0.12.6 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.12.6){: external} |
| Red Hat OpenShift configuration | N/A | N/A | Updated the [feature gate configuration](/docs/openshift?topic=openshift-service-settings#feature-gates) |
| Red Hat OpenShift Control Plane Operator | v4.10.0-20220712 | v4.11.0-20220824 | See the [{{site.data.keyword.openshiftshort}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.11.0+20220824){: external}. |
| Red Hat OpenShift on IBM Cloud Metrics Server | v4.10.0-20220712 | v4.11.0-20220824 | See the [{{site.data.keyword.openshiftshort}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.11.0+20220824){: external}. |
| Red Hat OpenShift on IBM Cloud toolkit | 4.10.0+20220712 | 4.11.0+20220824 | See the [{{site.data.keyword.openshiftshort}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.11.0+20220824){: external}. |
| RHEL Packages | RHEL 7 | RHEL 8 | Red Hat OpenShift on IBM Cloud version 4.11 supports RHEL 8 worker nodes. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.10.22_1528_openshift" caption-side="top"}
