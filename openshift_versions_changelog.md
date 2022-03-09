---

copyright:
  years: 2014, 2022
lastupdated: "2022-03-09"

keywords: openshift, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

--- 



{{site.data.keyword.attribute-definition-list}}

# Version changelog
{: #openshift_changelog}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

Unless otherwise noted in the changelogs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features, which are subject to change, are disabled.

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security) for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Changelog entries that address other security vulnerabilities but don't also refer to an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}

## Version change logs
{: #change-logs-by-version}

Review the change logs in the following list. 

**Supported Kubernetes versions**:
- [4.9 change log](/docs/openshift?topic=openshift-openshift_changelog_49)
- [4.8 change log](/docs/openshift?topic=openshift-openshift_changelog_48)
- [4.7 change log](/docs/openshift?topic=openshift-openshift_changelog_47)
- [4.6 change log](/docs/openshift?topic=openshift-openshift_changelog_46)

**Deprecated Kubernetes versions**:
- [3.11 change log](/docs/openshift?topic=openshift-openshift_changelog_311) 

**Unsupported Kubernetes versions**: 
- [Archived change logs](/docs/openshift?topic=openshift-changelog_archive)

## Version 4.9 changelog
{: #version-49}


Review the changelogs for {{site.data.keyword.openshiftlong_notm}} version 4.9 patch updates.
{: shortdesc}

### Changelog for master fix pack 4.9.21_1527_openshift, released 3 March 2022
{: #4921_1527}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.0 | v1.3.3 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds fix for [CVE-2021-43565](https://www.whitesourcesoftware.com/vulnerability-database/CVE-2021-43565){: external}. Adds Golang dependency updates. |
| Gateway-enabled cluster controller | 1586 | 1653 | Updated to use `Go` version `1.17.7` and updated `Go` modules to fix CVEs. |
| IBM Calico extension | 923 | 929 | Updated universal base image (UBI) to the `8.5-230` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| IBM Cloud Block Storage driver and plug-in | v2.1.6 | v2.1.7 | Fix for [CVE-2021-3538](https://vuln.whitesourcesoftware.com/vulnerability/CVE-2021-3538){: external}. |
| IBM Cloud Controller Manager | v1.22.6-1 | v1.22.7-2 | Updated to support the Kubernetes `1.22.7` release and to use `Go` version `1.16.14`. |
| IBM Cloud File Storage plug-in and monitor | 404 | 405 | Adds fix for [CVE-2021-3538](https://vuln.whitesourcesoftware.com/vulnerability/CVE-2021-3538){: external} and adds dependency updates. |
| Key Management Service provider | v2.4.0 | v2.5.2 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds fix for [CVE-2021-43565](https://www.whitesourcesoftware.com/vulnerability-database/CVE-2021-43565){: external}. Adds Golang dependency updates. |
| Red Hat OpenShift | 4.9.17 | 4.9.21 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-21){: external}. |
| Red Hat OpenShift Control Plane Operator | v4.9.0-20220201 | v4.9.0-20220222 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220222){: external}. |
| Red Hat OpenShift on IBM Cloud Metrics Server | v4.9.0-20220201 | v4.9.0-20220222 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220222){: external}. |
| Red Hat OpenShift on IBM Cloud toolkit | 4.9.0+20220201 | 4.9.0+20220222 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220222){: external}. |
| OpenVPN server | 2.5.4-r0-IKS-555 | 2.5.4-r0-IKS-562 | Turns off CRL verification in the openvpn image. |
| OpenVPN Operator image | v1.4.0 | v1.4.1 | Turns off CRL verification in the opevpn-operator image. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.17_1525_openshift" caption-side="top"}

### Change log for worker node fix pack 4.9.22_1529_openshift, released 28 February 2022
{: #4922_1529}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.53.1.el7 | 3.10.0-1160.59.1.el7 | Kernel and package updates for [CVE-2020-25709](https://nvd.nist.gov/vuln/detail/CVE-2020-25709){: external}, [CVE-2020-25710](https://nvd.nist.gov/vuln/detail/CVE-2020-25710){: external}, [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}, [CVE-2020-0465](https://nvd.nist.gov/vuln/detail/CVE-2020-0465){: external}, [CVE-2020-0466](https://nvd.nist.gov/vuln/detail/CVE-2020-0466){: external}, [CVE-2021-0920](https://nvd.nist.gov/vuln/detail/CVE-2021-0920){: external}, [CVE-2021-3564](https://nvd.nist.gov/vuln/detail/CVE-2021-3564){: external}, [CVE-2021-3573](https://nvd.nist.gov/vuln/detail/CVE-2021-3573){: external}, [CVE-2021-3752](https://nvd.nist.gov/vuln/detail/CVE-2021-3752){: external}, [CVE-2021-4155](https://nvd.nist.gov/vuln/detail/CVE-2021-4155){: external}, [CVE-2022-0330](https://nvd.nist.gov/vuln/detail/CVE-2022-0330){: external}, [CVE-2022-22942](https://nvd.nist.gov/vuln/detail/CVE-2022-22942){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.9.19 | 4.9.22 | For more information, see the [changelogs](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-22){: external} | 
| HA proxy | f6a2b3 | 15198fb | Contains fixes for [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}. | 
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.19_1526_openshift" caption-side="top"}


### Change log for worker node fix pack 4.9.19_1526_openshift, released 14 February 2022
{: #4919_1526}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | N/A |
| {{site.data.keyword.redhat_openshift_notm}} | N/A | 4.9.19 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-19){: external}. |
| Haproxy | d38fa1 | f6a2b3 | [CVE-2021-3521](https://nvd.nist.gov/vuln/detail/CVE-2021-3521){: external}   [CVE-2021-4122](https://nvd.nist.gov/vuln/detail/CVE-2021-4122){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.17_1523_openshift" caption-side="top"}

### Change log for master fix pack 4.9.17_1525_openshift and worker node fix pack 4.9.17_1523_openshift, released 9 February 2022
{: #4917_1525}

The following table shows the changes that are in the master fix pack `4.9.17_1525_openshift` and worker node fix pack `4.9.17_1523_openshift`. Master patch updates are applied automatically. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.20.3 | v3.21.4 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases){: external}. |
| Calico Operator | v1.20.5 | v1.23.5 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.23.5){: external}. |
| Cluster health image | v1.2.21 | v1.3.0 | Added new health check for cluster autoscaler add-on. |
| etcd | N/A | N/A | Updated to support metrics collection for OpenShift. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.21.9-1 | v1.22.6-1 | Updated to support the Kubernetes `1.22.6` release and to use `Go` version `1.16.12`. In addition, the code for this component is now [open source](https://github.com/IBM-Cloud/cloud-provider-ibm){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} (master) | 4.8.26 | 4.9.17 | See the [OpenShift release notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-17){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} (worker node) | 4.8.28 | 4.9.17 | See the [OpenShift release notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-17){: external}. |
| OpenShift Control Plane Operator | v4.8.0-20220107 | v4.9.0-20220201 | See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220201){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} configuration | N/A | N/A | Updated the [feature gate configuration](/docs/openshift?topic=openshift-service-settings#feature-gates). Added new `ibm-admin` flow schema to default [Kubernetes API priority and fairness configuration](/docs/openshift?topic=openshift-kubeapi-priority). |
| Pause container image | 3.5 | 3.6 | See the [pause container image release notes](https://github.com/kubernetes/kubernetes/blob/master/build/pause/CHANGELOG.md){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.8.0-20220107 | v4.9.0-20220201 | See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220201){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.8.0+20220107 | 4.9.0+20220201 | See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220201){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.26_1542_openshift master and 4.8.28_1543_openshift worker node." caption-side="top"}


## Version 4.8 changelog
{: #version-48}


Review the changelogs for {{site.data.keyword.openshiftlong_notm}} version 4.8 patch updates.
{: shortdesc}

### Changelog for master fix pack 4.8.29_1545_openshift, released 3 March 2022
{: #4829_1545}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.20.3 | v3.20.4 | See the [Calico release notes](https://projectcalico.docs.tigera.io/archive/v3.20/release-notes/#v3204){: external}. |
| Calico Operator | v1.20.5 | v1.20.6 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.20.6){: external}. |
| Cluster health image | v1.2.21 | v1.3.3 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds fix for [CVE-2021-43565](https://www.whitesourcesoftware.com/vulnerability-database/CVE-2021-43565){: external}. Adds Golang dependency updates. |
| Gateway-enabled cluster controller | 1586 | 1653 | Updated to use `Go` version `1.17.7` and updated `Go` modules to fix CVEs. |
| IBM Calico extension | 923 | 929 | Updated universal base image (UBI) to the `8.5-230` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| IBM Cloud Block Storage driver and plug-in | v2.1.6 | v2.1.7 | Fix for [CVE-2021-3538](https://vuln.whitesourcesoftware.com/vulnerability/CVE-2021-3538){: external}. |
| IBM Cloud Controller Manager | v1.21.9-1 | v1.21.10-2 | Updated to support the Kubernetes `1.21.10` release and to use `Go` version `1.16.14`. |
| IBM Cloud File Storage plug-in and monitor | 404 | 405 | Adds fix for [CVE-2021-3538](https://vuln.whitesourcesoftware.com/vulnerability/CVE-2021-3538){: external} and adds dependency updates. |
| Key Management Service provider | v2.4.0 | v2.4.3 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds [CVE-2021-43565](https://www.whitesourcesoftware.com/vulnerability-database/CVE-2021-43565){: external}. Adds Golang dependency updates. |
| Red Hat OpenShift | 4.8.26 | 4.8.29 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-29){: external}. |
| Red Hat OpenShift Control Plane Operator | v4.8.0-20220107 | v4.8.0-20220222 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220222){: external}. |
| Red Hat OpenShift on IBM Cloud Metrics Server | v4.8.0-20220107 | v4.8.0-20220222 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220222){: external}. |
| Red Hat OpenShift on IBM Cloud toolkit | 4.8.0+20220107 | 4.8.0+20220222 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220222){: external}. |
| OpenVPN server | 2.5.4-r0-IKS-555 | 2.5.4-r0-IKS-562 | Turns off CRL verification in the openvpn image. |
| OpenVPN Operator image | v1.4.0 | v1.4.1 | Turns off CRL verification in the opevpn-operator image. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.26_1542_openshift" caption-side="top"}

### Change log for worker node fix pack 4.8.32_1547_openshift, released 28 February 2022
{: #4832_1547}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages |  3.10.0-1160.53.1.el7 | 3.10.0-1160.59.1.el7 | Kernel and package updates for [CVE-2020-25709](https://nvd.nist.gov/vuln/detail/CVE-2020-25709){: external}, [CVE-2020-25710](https://nvd.nist.gov/vuln/detail/CVE-2020-25710){: external}, [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}, [CVE-2020-0465](https://nvd.nist.gov/vuln/detail/CVE-2020-0465){: external}, [CVE-2020-0466](https://nvd.nist.gov/vuln/detail/CVE-2020-0466){: external}, [CVE-2021-0920](https://nvd.nist.gov/vuln/detail/CVE-2021-0920){: external}, [CVE-2021-3564](https://nvd.nist.gov/vuln/detail/CVE-2021-3564){: external}, [CVE-2021-3573](https://nvd.nist.gov/vuln/detail/CVE-2021-3573){: external}, [CVE-2021-3752](https://nvd.nist.gov/vuln/detail/CVE-2021-3752){: external}, [CVE-2021-4155](https://nvd.nist.gov/vuln/detail/CVE-2021-4155){: external}, [CVE-2022-0330](https://nvd.nist.gov/vuln/detail/CVE-2022-0330){: external}, [CVE-2022-22942](https://nvd.nist.gov/vuln/detail/CVE-2022-22942){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.29 | 4.8.32 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-32) | 
| HA proxy | f6a2b3 | 15198fb | Contains fixes for [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.32_1547_openshift" caption-side="top"}

### Change log for worker node fix pack 4.8.29_1544_openshift, released 14 February 2022
{: #4829_1544}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | N/A |
|  {{site.data.keyword.redhat_openshift_notm}}  | 4.8.28 | 4.8.29 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-29){: external}. |
| Haproxy | d38fa1 | f6a2b3 | [CVE-2021-3521](https://nvd.nist.gov/vuln/detail/CVE-2021-3521){: external}   [CVE-2021-4122](https://nvd.nist.gov/vuln/detail/CVE-2021-4122){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.28_1543_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.8.28_1543_openshift, released 31 January 2022
{: #4828_1543}

The following table shows the changes that are in the worker node fix pack `4.8.28_1543_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | Updated worker node images with package updates for [CVE-2021-4034](https://nvd.nist.gov/vuln/detail/CVE-2021-4034){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.26 | 4.8.28 | See the {{site.data.keyword.redhat_openshift_notm}} [changelogs](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-28){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.26_1541_openshift" caption-side="top"}

### Changelog for master fix pack 4.8.26_1542_openshift, released 26 January 2022
{: #4826_1542}

The following table shows the changes that are in the master fix pack patch update `4.8.26_1542_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | N/A | N/A | Changed to improve Calico availability during updates. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | v2.1.3 | v2.1.6 | Updated to use `Go` version `1.16.13`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 900 | 923 | Updated universal base image (UBI) to the `8.5-218` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| Cluster health image | v1.2.20 | v1.2.21 | Updated to use `Go` version `1.17.5`, updated Go dependencies and golangci-lint. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.21.7-3 | v1.21.9-1 | Updated to support the Kubernetes `1.21.9` release and to use `Go` version `1.16.12`. |
| Key Management Service provider | v2.3.12 | v2.4.0 | Decrypted data encryption key is persisted in memory until the root key is changed, disabled, or rotated. Update multiple go dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1659 | 1747 | Updated the Alpine base image to the `3.15` version to resolve CVEs. Updated to use `Go` version `1.17.6`. |
| {{site.data.keyword.redhat_openshift_notm}} configuration | N/A | N/A | Updated the [feature gate configuration](/docs/openshift?topic=openshift-service-settings#feature-gates). |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.8.0-20211201 | v4.8.0-20220107 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220107). |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.8.0-20211201 | v4.8.0-20220107 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220107). |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.21 | 4.8.26 | Changed the duration of worker node certificates from 3 years to 2 years. See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-26). |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.8.0+20211201 | 4.8.0+20220107 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220107). |
| OpenVPN client | 2.4.6-r3-IKS-463 | 2.5.4-r0-IKS-556 | Update base image to alpine `3.15` to address CVEs, no longer set the `--compress config` option, updated scripts. |
| OpenVPN server | 2.4.6-r3-IKS-462 | 2.5.4-r0-IKS-555 | Update base image to alpine `3.15` to address CVEs, no longer set the `--compress config` option, updated scripts. |
| OpenVPN Operator image | v1.3.9 | v1.4.0 | Updated `OpenVPN` to version `2.5.4-r0`.  Remove deprecated compression config option from VPN server. Sset cipher explicitly to default value to avoid warning message in logs. |
| Portieris admission controller | v0.12.1 | v0.12.2 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.12.2) |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 3430e03 | 0fc9949 | Updated universal base image (UBI) to the `8.5-218` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 402 | 404 | Updated universal base image (UBI) to the `8.5-218` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.21_1541_openshift" caption-side="top"}


### Changelog for worker node fix pack 4.8.26_1541_openshift, released 18 January 2022
{: #4826_1541}

The following table shows the changes that are in the worker node fix pack `4.8.26_1541_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.49.1.el7 | 3.10.0-1160.53.1.el7 | Kernel and package updates for [CVE-2020-25704](https://nvd.nist.gov/vuln/detail/CVE-2020-25704){: external}, [CVE-2020-36322](https://nvd.nist.gov/vuln/detail/CVE-2020-36322){: external}, [CVE-2021-42739](https://nvd.nist.gov/vuln/detail/CVE-2021-42739){: external}, and [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.24 | 4.8.26 | See  the [change logs](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-26){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.24_1540_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.8.24_1540_openshift, released 4 January 2022
{: #4824_1540}

The following table shows the changes that are in the worker node fix pack patch update `4.8.24_1540_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 3b8663 | d38fa1 | Contains fixes for [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.24_1539_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.8.24_1539_openshift, released 20 December 2021
{: #4824_1539_openshift}

The following table shows the changes that are in the worker node fix pack patch update `4.8.24_1539_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} node | 4.8.20 | 4.8.22 | See [changelogs](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-22){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.22_1538_openshift" caption-side="top"}

### Changelog for master fix pack 4.8.21_1537_openshift, released 7 December 2021
{: #4821_1537}

The following table shows the changes that are in the master fix pack patch update `4.8.21_1537_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.20.2 | v3.20.3 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases). |
| Calico Operator | v1.20.4 | v1.20.5 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.20.5){: external}. |
| Cluster health image | v1.2.18 | v1.2.20 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| Gateway-enabled cluster controller | 1567 | 1586 | Updated Alpine base image to the latest `3.14` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 864 | 900 | Updated universal base image (UBI) to the `8.5-204` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | v2.1.2 | v2.1.3 | Updated universal base image (UBI) to the `8.5-204` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.21.6-2 | v1.21.7-3 | Updated to support the Kubernetes `1.21.7` release and to use `Go` version `1.16.10`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 401 | 402 | Updated universal base image (UBI) to the `8.5-204` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 4ca5637 | 3430e03 | Updated universal base image (UBI) to the latest `8.5` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| Key Management Service provider | v2.3.10 | v2.3.12 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1590 | 1659 | Updated Alpine base image to the latest `3.14` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
|  {{site.data.keyword.redhat_openshift_notm}} | 4.8.18 | 4.8.21 | See the [ {{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-21){: external}. |
|  {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.8.0-20211109 | v4.8.0-20211201 | See the [Red Hat  {{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211201){: external}. |
| OpenVPN Operator image | v1.3.8 | v1.3.9 | Updated ansible operator base image to version `v1.14.0` to resolve CVEs. |
| Portieris admission controller | v0.12.0 | v0.12.1 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.12.1){: external}. |
| Red Hat  {{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud Metrics Server | v4.8.0-20211109 | v4.8.0-20211201 | See the [Red Hat  {{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211201){: external}. |
| Red Hat  {{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud toolkit | 4.8.0+20211109 | 4.8.0+20211201 | See the [Red Hat  {{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211201){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.18_1535_openshift" caption-side="top"}


### Changelog for worker node fix pack 4.8.22_1538_openshift, released 6 December 2021
{: #4822_1538}

The following table shows the changes that are in the worker node fix pack patch update `4.8.22_1538_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.45 | 3.10.0-1160.49 | Updated worker node images and kernel with package updates. [CVE-2020-36385](https://nvd.nist.gov/vuln/detail/CVE-2020-36385){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-41617](https://nvd.nist.gov/vuln/detail/CVE-2021-41617){: external}, [CVE-2021-20271](https://nvd.nist.gov/vuln/detail/CVE-2021-20271){: external} |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.20 | 4.8.22 | See the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-22){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.20_1536_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.8.20_1536_openshift, released 22 November 2021
{: #4820_1536}

The following table shows the changes that are in the worker node fix pack patch update `4.8.20_1536_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.18 | 4.8.20 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-20){: external}. | 
| Haproxy | 07f1e9e | 3b8663 | Contains fixes for [CVE-2021-20231](https://nvd.nist.gov/vuln/detail/CVE-2021-20231){: external}, [CVE-2021-20232](https://nvd.nist.gov/vuln/detail/CVE-2021-20232){: external}, [CVE-2021-3580](https://nvd.nist.gov/vuln/detail/CVE-2021-3580){: external}, [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946){: external}, [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947){: external}, [CVE-2021-22876](https://nvd.nist.gov/vuln/detail/CVE-2021-22876){: external}, [CVE-2021-22898](https://nvd.nist.gov/vuln/detail/CVE-2021-22898){: external}, [CVE-2021-22925](https://nvd.nist.gov/vuln/detail/CVE-2021-22925){: external}, [CVE-2019-20838](https://nvd.nist.gov/vuln/detail/CVE-2019-20838){: external}, [CVE-2020-14155](https://nvd.nist.gov/vuln/detail/CVE-2020-14155){: external}, [CVE-2018-20673](https://nvd.nist.gov/vuln/detail/CVE-2018-20673){: external}, [CVE-2021-42574](https://nvd.nist.gov/vuln/detail/CVE-2021-42574){: external}, [CVE-2019-17594](https://nvd.nist.gov/vuln/detail/CVE-2019-17594){: external}, [CVE-2019-17595](https://nvd.nist.gov/vuln/detail/CVE-2019-17595){: external}, [CVE-2020-12762](https://nvd.nist.gov/vuln/detail/CVE-2020-12762){: external}, [CVE-2020-16135](https://nvd.nist.gov/vuln/detail/CVE-2020-16135){: external}, [CVE-2021-3445](https://nvd.nist.gov/vuln/detail/CVE-2021-3445){: external}, [CVE-2021-36084](https://nvd.nist.gov/vuln/detail/CVE-2021-36084){: external}, [CVE-2021-36085](https://nvd.nist.gov/vuln/detail/CVE-2021-36085){: external}, [CVE-2021-36086](https://nvd.nist.gov/vuln/detail/CVE-2021-36086){: external}, [CVE-2021-36087](https://nvd.nist.gov/vuln/detail/CVE-2021-36087){: external}, [CVE-2021-20266](https://nvd.nist.gov/vuln/detail/CVE-2021-20266){: external}, [CVE-2019-18218](https://nvd.nist.gov/vuln/detail/CVE-2019-18218){: external}, [CVE-2021-23840](https://nvd.nist.gov/vuln/detail/CVE-2021-23840){: external}, [CVE-2021-23841](https://nvd.nist.gov/vuln/detail/CVE-2021-23841){: external}, [CVE-2021-27645](https://nvd.nist.gov/vuln/detail/CVE-2021-27645){: external}, [CVE-2021-33574](https://nvd.nist.gov/vuln/detail/CVE-2021-33574){: external}, [CVE-2021-35942](https://nvd.nist.gov/vuln/detail/CVE-2021-35942){: external}, [CVE-2021-33560](https://nvd.nist.gov/vuln/detail/CVE-2021-33560){: external}, [CVE-2019-13750](https://nvd.nist.gov/vuln/detail/CVE-2019-13750){: external}, [CVE-2019-13751](https://nvd.nist.gov/vuln/detail/CVE-2019-13751){: external}, [CVE-2019-19603](https://nvd.nist.gov/vuln/detail/CVE-2019-19603){: external}, [CVE-2019-5827](https://nvd.nist.gov/vuln/detail/CVE-2019-5827){: external}, [CVE-2020-13435](https://nvd.nist.gov/vuln/detail/CVE-2020-13435){: external}, [CVE-2020-24370](https://nvd.nist.gov/vuln/detail/CVE-2020-24370){: external}, [CVE-2021-28153](https://nvd.nist.gov/vuln/detail/CVE-2021-28153){: external}, [CVE-2021-3800](https://nvd.nist.gov/vuln/detail/CVE-2021-3800){: external}, [CVE-2021-33928](https://nvd.nist.gov/vuln/detail/CVE-2021-33928){: external}, [CVE-2021-33929](https://nvd.nist.gov/vuln/detail/CVE-2021-33929){: external}, [CVE-2021-33930](https://nvd.nist.gov/vuln/detail/CVE-2021-33930){: external}, [CVE-2021-33938](https://nvd.nist.gov/vuln/detail/CVE-2021-33938){: external}, and [CVE-2021-3200](https://nvd.nist.gov/vuln/detail/CVE-2021-3200){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.18_1533_openshift" caption-side="top"}

### Changelog for master fix pack 4.8.18_1535_openshift, released 17 November 2021
{: #4818_1535}

The following table shows the changes that are in the master fix pack patch update `4.8.18_1535_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.20.0 | v3.20.2 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases). |
| Calico Operator | v1.20.1 | v1.20.4 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.20.4). |
| Cluster health image | v1.2.16 | v1.2.18 | Updated `Go` module dependencies and to use `Go` version `1.16.9`.  Updated image for [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946), [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947), [CVE-2021-33928](https://nvd.nist.gov/vuln/detail/CVE-2021-33928), [CVE-2021-33929](https://nvd.nist.gov/vuln/detail/CVE-2021-33929) and [CVE-2021-33930](https://nvd.nist.gov/vuln/detail/CVE-2021-33930).  |
| etcd | v3.4.17 | v3.4.18 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.18). |
| Gateway-enabled cluster controller | 1510 | 1567 | Updated to use `Go` version `1.16.9`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.21.5-2 | v1.21.6-2 | Updated to support the Kubernetes `1.21.6` release and to use `Go` version `1.16.9`. Updated image for [DLA-2797-1](https://www.debian.org/lts/security/2021/dla-2797). |
| {{site.data.keyword.cloud_notm}} RBAC Operator | e3cb629 | 4ca5637 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. |
| Key Management Service provider | v2.3.8 | v2.3.10 | Updated `Go` module dependencies and to use `Go` version `1.16.9`.  Updated image for [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946). |
| Load balancer and load balancer monitor for {{site.data.keyword.IBM_notm}} Cloud Provider | 1547 | 1590 | Updated to use `Go` version `1.16.9`. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.14 | 4.8.18 | See the [Openshift release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-18). Changed the duration of the Kubernetes API server certificate from 825 days to 365 days. Changed the duration of the cluster CA certificate from 30 to 10 years. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.8.0-20211004 | v4.8.0-20211109 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211109). |
| OpenVPN client | 2.4.6-r3-IKS-386 | 2.4.6-r3-IKS-463 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN server | 2.4.6-r3-IKS-385 | 2.4.6-r3-IKS-462 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN Operator image | v1.3.7 | v1.3.8 | Updated ansible operator base image to version `v1.13.1` to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.8.0-20211004 | v4.8.0-20211109 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211109). |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.8.0+20211004 | 4.8.0+20211109 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211109). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.14_1531_openshift" caption-side="top"}


### Changelog for worker node fix pack 4.8.18_1533_openshift, released 10 November 2021
{: #4818_1533}

The following table shows the changes that are in the worker node fix pack patch update `4.8.18_1533_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages| N/A | N/A | Updated worker node image packages for [CVE-2021-42574](https://nvd.nist.gov/vuln/detail/CVE-2021-42574){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.15 | 4.8.18 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-8-18){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.15_1532_openshift" caption-side="top"}

### Changelog for master fix pack 4.8.14_1531_openshift, released 29 October 2021
{: #4814_1531}

The following table shows the changes that are in the master fix pack patch update `4.8.14_1531_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.15 | v1.2.16 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs:  [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}, [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}, and [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}. |
| etcd | v3.4.16 | v3.4.17 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.17){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 763 | 864 | Updated to use `Go` version `1.16.9`. Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.1.1 | v2.1.2 | Updated universal base image (UBI) to version `8.4-210` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.21.5-1 | v1.21.5-2 | Updated to ignore VPC load balancer (LB) state when a LB delete is requested. |
| {{site.data.keyword.cloud_notm}} File Storage plug-in and monitor | 400 | 401 | Updated universal base image (UBI) to the latest `8.4-210` version to resolve CVEs. |
| Key Management Service provider | v2.3.7 | v2.3.8 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs:  [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}, [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}, and [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.11 | 4.8.14| See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-14){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.8.0-20210917 | v4.8.0-20211004 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211004){: external}. |
| OpenVPN Operator image | v1.3.6 | v1.3.7 | Updated ansible operator base image to version `v1.12.0` to resolve CVEs. |
| Portieris admission controller | v0.11.0 | v0.12.0 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.12.0){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.8.0-20210917 | v4.8.0-20211004 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211004){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.8.0+20210917 | 4.8.0+20211004 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211004){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.11_1526_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.8.15_1532_openshift, released 25 October 2021
{: #4815_1532}

The following table shows the changes that are in the worker node fix pack patch update `4.8.15_1532_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.13 | 4.8.15 | See [the {{site.data.keyword.redhat_openshift_notm}} changelogs](http://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html){: external}. |
| RHEL 7 Packages | 3.10.0-1160.42.2.el7 | 3.10.0-1160.45.1.el7 | Updated worker node images and kernel with package updates for [CVE-2021-3778](https://nvd.nist.gov/vuln/detail/CVE-2021-3778){: external} and [CVE-2021-3796](https://nvd.nist.gov/vuln/detail/CVE-2021-3796){: external}. |
| Worker-pool taint automation | N/A | N/A | Fixes known issue related to worker-pool taint automation that prevents workers from getting providerID. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.13_1528_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.8.13_1528_openshift, released 11 October 2021
{: #48131528_openshift}

The following table shows the changes that are in the worker node fix pack patch update `4.8.13_1528_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.12 | 4.8.13 | See the [change logs](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-13){: external}. The update resolves CVE-2021-25741 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6515606){: external}).|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.12_1527_openshift" caption-side="top"}

### Change log for fix pack 4.8.11_1526_openshift (master) and 4.8.12_1527_openshift (worker node), released 29 Sept 2021
{: #4811_1526_and_4812_1527}

The following table shows the changes that are in the master fix pack `4.8.11_1526_openshift` and the worker node fix pack patch update `4.8.12_1527_openshift`. Master patch updates are applied automatically. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.19.3 | v3.20.0 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases){: external}. |
| Calico Operator | v1.17.8 | v1.20.1 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.20.1){: external}. Updated to use the `system-cluster-critical` priority class. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} plug-in and driver | N/A | N/A | Updated to use the `system-cluster-critical` and `system-node-critical` priority classes respectively. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.20.11-1 | v1.21.5-1 | Updated to support the Kubernetes `1.21.5` release. |
| {{site.data.keyword.redhat_openshift_notm}} (master) | 4.7.30 | 4.8.11 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-11){: external}. The update resolves [CVE-2021-3636](https://nvd.nist.gov/vuln/detail/CVE-2021-3636){: external} and [CVE-2021-25737](https://nvd.nist.gov/vuln/detail/CVE-2021-25737){: external}. For more infomration, see the [IBM security bulletin for CVE-2021-3636](https://www.ibm.com/support/pages/node/6517086){: external} and the [IBM security bulletin for CVE-2021-25737](https://www.ibm.com/support/pages/node/6517054){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} (worker node) | 4.7.30 | 4.8.12 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-12){: external}. The update resolves [CVE-2021-3636](https://nvd.nist.gov/vuln/detail/CVE-2021-3636){: external} and [CVE-2021-25737](https://nvd.nist.gov/vuln/detail/CVE-2021-25737){: external}. For more infomration, see the [IBM security bulletin for CVE-2021-3636](https://www.ibm.com/support/pages/node/6517086){: external} and the [IBM security bulletin for CVE-2021-25737](https://www.ibm.com/support/pages/node/6517054){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} configuration | N/A | N/A | Updated the [feature gate configuration](/docs/openshift?topic=openshift-service-settings#feature-gates). |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.7.0-20210917 | v4.8.0-20210917 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20210917){: external}. |
| Pause container image | 3.2 | 3.5 | See the [pause container image release notes](https://github.com/kubernetes/kubernetes/blob/master/build/pause/CHANGELOG.md){: external}. |
| Portieris admission controller | v0.10.3 | v0.11.0 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.11.0){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.7.0-20210917 | v4.8.0-20210917 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20210917){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.7.0+20210917 | 4.8.0+20210917 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20210917){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.30_1532_openshift master and 4.7.31_1533 worker node" caption-side="top"}

## Version 4.7 change log
{: #version-47}

Review the changelogs for {{site.data.keyword.openshiftlong_notm}} version 4.7 patch updates.
{: shortdesc}

### Changelog for master fix pack 4.7.42_1550_openshift, released 3 March 2022
{: #4742_1550}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.19.3 | v3.19.4 | See the [Calico release notes](https://projectcalico.docs.tigera.io/archive/v3.19/release-notes/#v3194){: external}. |
| Calico Operator | v1.17.8 | v1.17.9 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.17.9){: external}. |
| Cluster health image | v1.2.21 | v1.3.3 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds fix for [CVE-2021-43565](https://www.whitesourcesoftware.com/vulnerability-database/CVE-2021-43565){: external}. Golang dependency updates. |
| Gateway-enabled cluster controller | 1586 | 1653 | Updated to use `Go` version `1.17.7` and updated `Go` modules to fix CVEs. |
| IBM Calico extension | 923 | 929 | Updated universal base image (UBI) to the `8.5-230` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| IBM Cloud Block Storage driver and plug-in | v2.1.6 | v2.1.7 | Fix for [CVE-2021-3538](https://vuln.whitesourcesoftware.com/vulnerability/CVE-2021-3538){: external}. |
| IBM Cloud Controller Manager | v1.20.15-1 | v1.20.15-4 | Adds changes to the renovate rules. |
| IBM Cloud File Storage plug-in and monitor | 404 | 405 | Adds fix for [CVE-2021-3538](https://vuln.whitesourcesoftware.com/vulnerability/CVE-2021-3538){: external} and adds dependency updates. |
| Key Management Service provider | v2.3.13 | v2.4.3 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds fix for [CVE-2021-43565](https://www.whitesourcesoftware.com/vulnerability-database/CVE-2021-43565){: external}. Adds Golang dependency updates. |
| Red Hat OpenShift | 4.7.40 | 4.7.42 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-42){: external}. |
| Red Hat OpenShift Control Plane Operator | v4.7.0-20220107 | v4.7.0-20220222 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20220222){: external}. |
| Red Hat OpenShift on IBM Cloud Metrics Server | v4.7.0-20220107 | v4.7.0-20220222 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20220222){: external}. |
| Red Hat OpenShift on IBM Cloud toolkit | 4.7.0+20220107 | 4.7.0+20220222 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20220222){: external}. |
| OpenVPN server | 2.5.4-r0-IKS-555 | 2.5.4-r0-IKS-562 | Turns off CRL verification in the openvpn image. |
| OpenVPN Operator image | v1.4.0 | v1.4.1 | Turns off CRL verification in the opevpn-operator image. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.40_1547_openshift" caption-side="top"}

### Change log for worker node fix pack 4.7.42_1553_openshift, released 28 February 2022
{: #4742_1553}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| 4.7.42_1549_openshift |
| RHEL 7 Packages | 3.10.0-1160.53.1.el7 | 3.10.0-1160.59.1.el7 | Kernel and package updates for [CVE-2020-25709](https://nvd.nist.gov/vuln/detail/CVE-2020-25709){: external}, [CVE-2020-25710](https://nvd.nist.gov/vuln/detail/CVE-2020-25710){: external}, [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}, [CVE-2020-0465](https://nvd.nist.gov/vuln/detail/CVE-2020-0465){: external}, [CVE-2020-0466](https://nvd.nist.gov/vuln/detail/CVE-2020-0466){: external}, [CVE-2021-0920](https://nvd.nist.gov/vuln/detail/CVE-2021-0920){: external}, [CVE-2021-3564](https://nvd.nist.gov/vuln/detail/CVE-2021-3564){: external}, [CVE-2021-3573](https://nvd.nist.gov/vuln/detail/CVE-2021-3573){: external}, [CVE-2021-3752](https://nvd.nist.gov/vuln/detail/CVE-2021-3752){: external}, [CVE-2021-4155](https://nvd.nist.gov/vuln/detail/CVE-2021-4155){: external}, [CVE-2022-0330](https://nvd.nist.gov/vuln/detail/CVE-2022-0330){: external}, [CVE-2022-22942](https://nvd.nist.gov/vuln/detail/CVE-2022-22942) | 
| Haproxy | f6a2b3 | 15198fb | Contains fixes for [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external} | 
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.42_1549_openshift" caption-side="top"}

### Change log for worker node fix pack 4.7.42_1549_openshift, released 14 February 2022
{: #4742_1549}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| 4.7.42_1549_openshift |
| RHEL 7 Packages | N/A | N/A | N/A |
|  {{site.data.keyword.redhat_openshift_notm}}  | 4.7.41 | 4.7.42 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-42){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.41_1548_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.7.41_1548_openshift, released 31 January 2022
{: #4741_1548}

The following table shows the changes that are in the worker node fix pack `4.7.41_1548_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | Updated worker node images with package updates for [CVE-2021-4034](https://nvd.nist.gov/vuln/detail/CVE-2021-4034){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.7.40 | 4.7.41 | See the {{site.data.keyword.redhat_openshift_notm}} [changelogs](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-41){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.40_1546_openshift" caption-side="top"}

### Changelog for master fix pack 4.7.40_1547_openshift, released 26 January 2022
{: #4740_1547}

The following table shows the changes that are in the master fix pack patch update `4.7.40_1547_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | N/A | N/A | Changed to improve Calico availability during updates. |
| Cluster health image | v1.2.20 | v1.2.21 | Updated to use `Go` version `1.17.5`, updated Go dependencies and golangci-lint. |
| {{site.data.keyword.IBM_notm}} Calico extension | 900 | 923 | Updated universal base image (UBI) to the `8.5-218` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | v2.1.3 | v2.1.6 | Updated to use `Go` version `1.16.13`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.20.13-4 | v1.20.15-1 | Updated to support the Kubernetes 1.20.15 release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 402 | 404 | Updated universal base image (UBI) to the `8.5-218` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 3430e03 | 0fc9949 | Updated universal base image (UBI) to the `8.5-218` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| Key Management Service provider | v2.3.12 | v2.3.13 | Updated `Go` dependencies and golangci-lint. |
| Load balancer and load balancer monitor for IBM Cloud Provider | 1659 | 1747 | Updated the Alpine base image to the `3.15` version to resolve CVEs. Updated to use `Go` version `1.17.6`. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.7.37 | 4.7.40 | Changed the duration of the Kubernetes API server certificate from 825 days to 365 days. Changed the duration of the cluster CA certificate from 30 years to 10 years. Changed the duration of worker node certificates from 3 years to 2 years. See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-40). |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.7.0-20211201 | v4.7.0-20220107 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0%2B20220107). |
| OpenVPN client | 2.4.6-r3-IKS-463 | 2.5.4-r0-IKS-556 | Update base image to alpine `3.15` to address CVEs, no longer set the `--compress config` option, updated scripts. |
| OpenVPN server | 2.4.6-r3-IKS-462 | 2.5.4-r0-IKS-555 | Update base image to alpine `3.15` to address CVEs, no longer set the `--compress config` option, updated scripts|
| OpenVPN Operator image | v1.3.9 | v1.4.0 | Updated `OpenVPN` to version `2.5.4-r0`.  Remove deprecated compression config option from VPN server. Sset cipher explicitly to default value to avoid warning message in logs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.7.0-20211201 | v4.7.0-20220107 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0%2B20220107). |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.7.0+20211201 | 4.7.0+20220107 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20220107). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.37_1546_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.7.40_1546_openshift, released 18 January 2022
{: #4740_1546}

The following table shows the changes that are in the worker node fix pack `4.7.40_1546_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.49.1.el7 | 3.10.0-1160.53.1.el7 | Kernel and package updates for [CVE-2020-25704](https://nvd.nist.gov/vuln/detail/CVE-2020-25704){: external}, [CVE-2020-36322](https://nvd.nist.gov/vuln/detail/CVE-2020-36322){: external}, [CVE-2021-42739](https://nvd.nist.gov/vuln/detail/CVE-2021-42739){: external}, and [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.40_1545_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.7.40_1545_openshift, released 4 January 2022
{: #4740_1545}

The following table shows the changes that are in the worker node fix pack patch update `4.7.40_1545_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 3b8663 | d38fa1 | Contains fixes for [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.40_1544_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.7.40_1544_openshift, released 20 December 2021
{: #4740_1544_openshift}

The following table shows the changes that are in the worker node fix pack patch update `4.7.40_1544_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} node | 4.7.38 | 4.7.40 | See [changelogs](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-40){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.38_1543_openshift" caption-side="top"}

### Changelog for master fix pack 4.7.37_1542_openshift, released 7 December 2021
{: #4737_1542}

The following table shows the changes that are in the master fix pack patch update `4.7.37_1542_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.18 | v1.2.20 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| Gateway-enabled cluster controller | 1567 | 1586 | Updated Alpine base image to the latest `3.14` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 864 | 900 | Updated universal base image (UBI) to the `8.5-204` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | v2.1.2 | v2.1.3 | Updated universal base image (UBI) to the `8.5-204` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.20.12-3 | v1.20.13-4 | Updated to support the Kubernetes `1.20.13` release and to use `calicoctl` version `3.17.6`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 401 | 402 | Updated universal base image (UBI) to the `8.5-204` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 4ca5637 | 3430e03 | Updated universal base image (UBI) to the latest `8.5` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| Key Management Service provider | v2.3.10 | v2.3.12 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1590 | 1659 | Updated Alpine base image to the latest `3.14` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.7.36 | 4.7.37 | See the [ {{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-37){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.7.0-20211109 | v4.7.0-20211201 | See the [Red Hat  {{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20211201){: external}. |
| OpenVPN Operator image | v1.3.8 | v1.3.9 | Updated ansible operator base image to version `v1.14.0` to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.7.0-20211109 | v4.7.0-20211201 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20211201){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.7.0+20211109 | 4.7.0+20211201 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20211201){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.36_1539_openshift" caption-side="top"}


### Changelog for worker node fix pack 4.7.38_1543_openshift, released 6 December 2021
{: #4738_1543}

The following table shows the changes that are in the worker node fix pack patch update `4.7.38_1543_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.45 | 3.10.0-1160.49 | Updated worker node images and kernel with package updates. Contains fixes for [CVE-2020-36385](https://nvd.nist.gov/vuln/detail/CVE-2020-36385){: external},  [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-41617](https://nvd.nist.gov/vuln/detail/CVE-2021-41617){: external}, [CVE-2021-20271](https://nvd.nist.gov/vuln/detail/CVE-2021-20271){: external}. | 
| OpenShift Container Platform | 4.7.37 | 4.7.38 | See [changelogs](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-38){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.37_1540_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.7.37_1540_openshift, released 22 November 2021
{: #4737_1540}

The following table shows the changes that are in the worker node fix pack patch update `4.7.37_1540_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.7.36 | 4.7.37 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-37){: external}. | 
| Haproxy | 07f1e9e | 3b8663 | Contains fixes for [CVE-2021-20231](https://nvd.nist.gov/vuln/detail/CVE-2021-20231){: external}, [CVE-2021-20232](https://nvd.nist.gov/vuln/detail/CVE-2021-20232){: external}, [CVE-2021-3580](https://nvd.nist.gov/vuln/detail/CVE-2021-3580){: external}, [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946){: external}, [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947){: external}, [CVE-2021-22876](https://nvd.nist.gov/vuln/detail/CVE-2021-22876){: external}, [CVE-2021-22898](https://nvd.nist.gov/vuln/detail/CVE-2021-22898){: external}, [CVE-2021-22925](https://nvd.nist.gov/vuln/detail/CVE-2021-22925){: external}, [CVE-2019-20838](https://nvd.nist.gov/vuln/detail/CVE-2019-20838){: external}, [CVE-2020-14155](https://nvd.nist.gov/vuln/detail/CVE-2020-14155){: external}, [CVE-2018-20673](https://nvd.nist.gov/vuln/detail/CVE-2018-20673){: external}, [CVE-2021-42574](https://nvd.nist.gov/vuln/detail/CVE-2021-42574){: external}, [CVE-2019-17594](https://nvd.nist.gov/vuln/detail/CVE-2019-17594){: external}, [CVE-2019-17595](https://nvd.nist.gov/vuln/detail/CVE-2019-17595){: external}, [CVE-2020-12762](https://nvd.nist.gov/vuln/detail/CVE-2020-12762){: external}, [CVE-2020-16135](https://nvd.nist.gov/vuln/detail/CVE-2020-16135){: external}, [CVE-2021-3445](https://nvd.nist.gov/vuln/detail/CVE-2021-3445){: external}, [CVE-2021-36084](https://nvd.nist.gov/vuln/detail/CVE-2021-36084){: external}, [CVE-2021-36085](https://nvd.nist.gov/vuln/detail/CVE-2021-36085){: external}, [CVE-2021-36086](https://nvd.nist.gov/vuln/detail/CVE-2021-36086){: external}, [CVE-2021-36087](https://nvd.nist.gov/vuln/detail/CVE-2021-36087){: external}, [CVE-2021-20266](https://nvd.nist.gov/vuln/detail/CVE-2021-20266){: external}, [CVE-2019-18218](https://nvd.nist.gov/vuln/detail/CVE-2019-18218){: external}, [CVE-2021-23840](https://nvd.nist.gov/vuln/detail/CVE-2021-23840){: external}, [CVE-2021-23841](https://nvd.nist.gov/vuln/detail/CVE-2021-23841){: external}, [CVE-2021-27645](https://nvd.nist.gov/vuln/detail/CVE-2021-27645){: external}, [CVE-2021-33574](https://nvd.nist.gov/vuln/detail/CVE-2021-33574){: external}, [CVE-2021-35942](https://nvd.nist.gov/vuln/detail/CVE-2021-35942){: external}, [CVE-2021-33560](https://nvd.nist.gov/vuln/detail/CVE-2021-33560){: external}, [CVE-2019-13750](https://nvd.nist.gov/vuln/detail/CVE-2019-13750){: external}, [CVE-2019-13751](https://nvd.nist.gov/vuln/detail/CVE-2019-13751){: external}, [CVE-2019-19603](https://nvd.nist.gov/vuln/detail/CVE-2019-19603){: external}, [CVE-2019-5827](https://nvd.nist.gov/vuln/detail/CVE-2019-5827){: external}, [CVE-2020-13435](https://nvd.nist.gov/vuln/detail/CVE-2020-13435){: external}, [CVE-2020-24370](https://nvd.nist.gov/vuln/detail/CVE-2020-24370){: external}, [CVE-2021-28153](https://nvd.nist.gov/vuln/detail/CVE-2021-28153){: external}, [CVE-2021-3800](https://nvd.nist.gov/vuln/detail/CVE-2021-3800){: external}, [CVE-2021-33928](https://nvd.nist.gov/vuln/detail/CVE-2021-33928){: external}, [CVE-2021-33929](https://nvd.nist.gov/vuln/detail/CVE-2021-33929){: external}, [CVE-2021-33930](https://nvd.nist.gov/vuln/detail/CVE-2021-33930){: external}, [CVE-2021-33938](https://nvd.nist.gov/vuln/detail/CVE-2021-33938){: external}, and[CVE-2021-3200](https://nvd.nist.gov/vuln/detail/CVE-2021-3200){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.36_1538_openshift" caption-side="top"}

### Changelog for master fix pack 4.7.36_1539_openshift, released 17 November 2021
{: #4736_1539}

The following table shows the changes that are in the master fix pack patch update `4.7.36_1539_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.16 | v1.2.18 | Updated `Go` module dependencies and to use `Go` version `1.16.9`.  Updated image for [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946), [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947), [CVE-2021-33928](https://nvd.nist.gov/vuln/detail/CVE-2021-33928), [CVE-2021-33929](https://nvd.nist.gov/vuln/detail/CVE-2021-33929) and [CVE-2021-33930](https://nvd.nist.gov/vuln/detail/CVE-2021-33930).  |
| etcd | v3.4.17 | v3.4.18 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.18). |
| Gateway-enabled cluster controller | 1510 | 1567 | Updated to use `Go` version `1.16.9`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.20.11-2 | v1.20.12-3 | Updated to support the Kubernetes `1.20.12` release. Updated image for [DLA-2797-1](https://www.debian.org/lts/security/2021/dla-2797). |
| {{site.data.keyword.cloud_notm}} RBAC Operator | e3cb629 | 4ca5637 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. |
| Key Management Service provider | v2.3.8 | v2.3.10 | Updated `Go` module dependencies and to use `Go` version `1.16.9`.  Updated image for [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946). |
| Load balancer and load balancer monitor for {{site.data.keyword.IBM_notm}} Cloud Provider | 1547 | 1590 | Updated to use `Go` version `1.16.9`. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.7.33 | 4.7.36 | See the [Openshift release notes](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-36). |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.7.0-20210923 | v4.7.0-20211109 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20211109). |
| OpenVPN client | 2.4.6-r3-IKS-386 | 2.4.6-r3-IKS-463 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN server | 2.4.6-r3-IKS-385 | 2.4.6-r3-IKS-462 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN Operator image | v1.3.7 | v1.3.8 | Updated ansible operator base image to version `v1.13.1` to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.7.0-20210923 | v4.7.0-20211109 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20211109). |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.7.0+20210923 | 4.7.0+20211109 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20211109). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.33_1536_openshift" caption-side="top"}


### Changelog for worker node fix pack 4.7.36_1538_openshift, released 10 November 2021
{: #4736_1538}

The following table shows the changes that are in the worker node fix pack patch update `4.7.36_1538_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages| N/A | N/A | Updated worker node image packages for [CVE-2021-42574](https://nvd.nist.gov/vuln/detail/CVE-2021-42574){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.7.34 | 4.7.36 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-7-36){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.32_1534_openshift" caption-side="top"}

### Changelog for master fix pack 4.7.33_1536_openshift, released 29 October 2021
{: #4733_1536}

The following table shows the changes that are in the master fix pack patch update `4.7.33_1536_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.15 | v1.2.16 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs:  [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}, [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}, and [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}. |
| etcd | v3.4.16 | v3.4.17 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.17){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 763 | 864 | Updated to use `Go` version `1.16.9`. Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | v2.1.1 | v2.1.2 | Updated universal base image (UBI) to version `8.4-210` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager |  v1.20.11-1 | v1.20.11-2 | Updated to ignore VPC load balancer (LB) state when a LB delete is requested. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.filestorage_short}} plug-in and monitor | 400 | 401 | Updated universal base image (UBI) to the latest `8.4-210` version to resolve CVEs. |
| Key Management Service provider | v2.3.7 | v2.3.8 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs:  [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}, [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}, and [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.7.30 | 4.7.33 | Updated to fix [CVE-2021-25735](https://www.ibm.com/support/pages/node/6549374){: external}. See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-33){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.7.0-20210917 | v4.7.0-20210923 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210923){: external}. |
| OpenVPN Operator image | v1.3.6 | v1.3.7 | Updated ansible operator base image to version `v1.12.0` to resolve CVEs. |-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}, [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}, and [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.7.0-20210917 | v4.7.0-20210923 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210923). |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.7.0+20210917 | 4.7.0+20210923 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210923). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.30_1532_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.7.34_1537_openshift, released 25 October 2021
{: #4734_1537}

The following table shows the changes that are in the worker node fix pack patch update `4.7.34_1537_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.7.32 | 4.7.34 | See [the {{site.data.keyword.redhat_openshift_notm}} changelogs](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-34){: external}. |
| RHEL 7 Packages | 3.10.0-1160.42.2.el7 | 3.10.0-1160.45.1.el7 | Updated worker node images and kernel with package updates for [CVE-2021-3778](https://nvd.nist.gov/vuln/detail/CVE-2021-3778){: external} and [CVE-2021-3796](https://nvd.nist.gov/vuln/detail/CVE-2021-3796){: external}. |
| Worker-pool taint automation | N/A | N/A | Fixes known issue related to worker-pool taint automation that prevents workers from getting providerID. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.32_1534_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.7.32_1534_openshift, released 11 October 2021
{: #4732_1534_openshift}

The following table shows the changes that are in the worker node fix pack patch update `4.7.32_1534_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.7.31 | 4.7.32 | See the [change logs](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-32){: external}. The update resolves CVE-2021-25741 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6515606){: external}). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.31_1533_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.7.31_1533_openshift, released 27 September 2021
{: #4731_1533}

The following table shows the changes that are in the worker node fix pack patch update `4.7.31_1533_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Disk identification | NA | NA | Enhanced the disk identification logic to handle the case of 2+ partitions. |
| Haproxy | 9c98dc5 | 07f1e9 | Updated image with fixes for [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}, [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}, [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}, [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}, and [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}. |
|OpenShift Container Platform| 4.7.29 | 4.7.31 | See [changelogs](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-31){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.29_1531_openshift" caption-side="top"}

### Changelog for master fix pack 4.7.30_1532_openshift, released 28 September 2021
{: #4730_1532}

The following table shows the changes that are in the master fix pack patch update `4.7.30_1532_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.19.1 | v3.19.3 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases){: external}. |
| Calico Operator | v1.17.3 | v1.17.8 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.17.8){: external}. |
| Gateway-enabled cluster controller | 1444 | 1510 | Updated image for [CVE-2021-3711](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3711){: external} and [CVE-2021-3712](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3712){: external}. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} plug-in and driver | v2.0.9 | v2.1.1 | Updated to use `Go` version `1.16.7`. Updated universal base image (UBI) to the latest `8.4-208` version to resolve CVEs. |
| {{site.data.keyword.IBM_notm}} Cloud Controller Manager | v1.20.10-1 | v1.20.11-1 | Updated to support the Kubernetes `1.20.11` release. Fixed a bug that may cause node initialization to fail when a new node reuses the name of a deleted node. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.filestorage_short}} plug-in and monitor | 398 | 400 | Updated to use `Go` version `1.16.7`. Updated universal base image (UBI) to the latest `8.4-208` version to resolve CVEs. |
| {{site.data.keyword.IBM_notm}} Cloud RBAC Operator | 945df65 | e3cb629 | Updated to use `Go` version `1.16.7`. |
| Kubernetes API server auditing configuration | N/A | N/A| Updated to support `verbose` [Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit#audit-api-server){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.IBM_notm}} Cloud Provider | 1510 | 1547 | Updated image for [CVE-2021-3711](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3711) and [CVE-2021-3712](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3712){: external}. |
|OpenShift Container Platform| 4.7.23 | 4.7.30 | See the [OpenShift Container Platform release notes](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-30){: external}. |
|OpenShift Container PlatformControl Plane Operator | v4.7.0-20210816 | v4.7.0-20210917 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210917){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.7.0-20210816 | v4.7.0-20210917 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210917){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.7.0+20210816 | 4.7.0+20210917 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210917){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.23_1529_openshift" caption-side="top"}



### Changelog for worker node fix pack 4.7.29_1531_openshift, released 13 September 2021
{: #4729_1531}

The following table shows the changes that are in the worker node fix pack patch update `4.7.29_1531_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| OpenShift Container Platform | 4.7.24 | 4.7.29 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](http://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html){: external}. |
| RHEL 7 Packages | 3.10.0-1160.36.2.el7 | 3.10.0-1160.42.2.el7 | Updated worker node image with package updates for [CVE-2021-25214](https://nvd.nist.gov/vuln/detail/CVE-2021-25214){: external}, [CVE-2020-27777](https://nvd.nist.gov/vuln/detail/CVE-2020-27777){: external}, [CVE-2021-22555](https://nvd.nist.gov/vuln/detail/CVE-2021-22555){: external}, [CVE-2021-29154](https://nvd.nist.gov/vuln/detail/CVE-2021-29154){: external}, [CVE-2021-29650](https://nvd.nist.gov/vuln/detail/CVE-2021-29650){: external}, [CVE-2021-32399](https://nvd.nist.gov/vuln/detail/CVE-2021-32399){: external}, [CVE-2021-3715](https://nvd.nist.gov/vuln/detail/CVE-2021-3715){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.24_1530_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.7.24_1530_openshift, released 30 August 2021
{: #4724_1530}

The following table shows the changes that are in the worker node fix pack patch update `4.7.24_1530_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| OpenShift Container Platform | 4.7.23 | 4.7.24 | See [changelogs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-43){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.23_1528_openshift" caption-side="top"}

### Changelog for master fix pack 4.7.23_1529_openshift, released 25 August 2021
{: #4723_1529}

The following table shows the changes that are in the master fix pack patch update `4.7.23_1529_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | N/A | N/A | Updated the rolling update configuration for the `calico-node` daemonset in the `calico-system` namespace.  The configuration is now the same regardless of the number of cluster worker nodes. |
| Cluster health image | v1.2.14 | v1.2.15 | Updated to use `Go` version `1.15.15`. Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. |
| Cluster master operations | N/A | N/A | Fixes DNS configuration problem that may block {{site.data.keyword.redhat_openshift_notm}} operator updates. |
| Gateway-enabled cluster controller | 1348 | 1444 | Updated image for [CVE-2021-36159](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-36159){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 747 | 763 | Updated to use `Go` version `1.16.6`. Updated universal base image (UBI) to the latest `8.4-205` version to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} plug-in and driver | v2.0.8 | v2.0.9 | Updated to use `Go` version `1.16.6`. Updated image for [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33910){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.20.9-1 | v1.20.10-1 | Updated to support the Kubernetes `1.20.10` release and to use `Go` version `1.15.15`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 395 | 398 | Updated to use `Go` version `1.16.6`. Updated image for [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33910){: external}. |
| Key Management Service provider | v2.3.6 | v2.3.7 | Updated to use `Go` version `1.15.15`. Updated UBI to the latest `8.4` version to resolve CVEs. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1328 | 1510 | Updated image for [CVE-2020-27780](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-27780){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.7.19 | 4.7.23 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-23){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.7.0-20210630 | v4.7.0-20210816 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210816){: external}. |
| OpenVPN Operator image | v1.3.4 | v1.3.6 | Updated image for [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33910){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.7.0-20210630 | v4.7.0-20210816 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210816){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.7.0+20210630 | 4.7.0+20210816 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210816){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.19_1526_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.7.23_1528_openshift, released 16 August 2021
{: #4723_1528}

The following table shows the changes that are in the worker node fix pack patch update `4.7.23_1528_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 68e6b3 | 9c98dc | Updated image with fixes for [CVE-2021-27218](https://nvd.nist.gov/vuln/detail/CVE-2021-27218){: external} |
| RHEL 7 Packages | N/A| N/A| Updated image with fixes for: [CVE-2020-0543](https://nvd.nist.gov/vuln/detail/CVE-2020-0543){: external}, [CVE-2020-0548](https://nvd.nist.gov/vuln/detail/CVE-2020-0548){: external}, [CVE-2020-0549](https://nvd.nist.gov/vuln/detail/CVE-2020-0549){: external}, [CVE-2020-8695](https://nvd.nist.gov/vuln/detail/CVE-2020-8695){: external}, [CVE-2020-8696](https://nvd.nist.gov/vuln/detail/CVE-2020-8696){: external}, [CVE-2020-8698](https://nvd.nist.gov/vuln/detail/CVE-2020-8698){: external}, [CVE-2020-24489](https://nvd.nist.gov/vuln/detail/CVE-2020-24489){: external}, [CVE-2020-24511](https://nvd.nist.gov/vuln/detail/CVE-2020-24511){: external}, and [CVE-2020-24512](https://nvd.nist.gov/vuln/detail/CVE-2020-24512){: external}. |
| OpenShift Container Platform | 4.7.21 | 4.7.23 | See [changelogs](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.23_1527_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.7.21_1527_openshift, released 02 August 2021
{: #4721_1527}

The following table shows the changes that are in the worker node fix pack patch update `4.7.21_1527_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | aae810 | 68e6b3 | Updated image with fixes for [CVE-2021-33910](https://nvd.nist.gov/vuln/detail/CVE-2021-33910){: external}. |
| Registry endpoints | Added ability to access all global registries for private service enabled clusters through the public domain. Added zonal public registry endpoints for clusters with both private and public service endpoints enabled. |
| Read only disk self healing | For VPC Gen2 workers. Added automation to recover from disks going read only. |
| RHEL 7 Packages | 3.10.0-1160.31.1 | 3.10.0-1160.36.2 | Updated worker node images & Kernel with package updates: [CVE-2019-20934](https://nvd.nist.gov/vuln/detail/CVE-2019-20934){: external}, [CVE-2020-11668](https://nvd.nist.gov/vuln/detail/CVE-2020-11668){: external}, [CVE-2021-33033](https://nvd.nist.gov/vuln/detail/CVE-2021-33033){: external}, [CVE-2021-33034](https://nvd.nist.gov/vuln/detail/CVE-2021-33034){: external}, [CVE-2021-33909](https://nvd.nist.gov/vuln/detail/CVE-2021-33909){: external}. |
| OpenShift Container Platform | 4.7.19 |4.7.21 | See [changelogs](http://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.19_1525_openshift" caption-side="top"}

### Changelog for master fix pack 4.7.19_1526_openshift, released 27 July 2021
{: #4719_1526}

The following table shows the changes that are in the master fix pack patch update `4.7.19_1526_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.13 | v1.2.14 | Updated universal base image (UBI) to the latest version to resolve CVEs. |
| etcd | v3.4.14 | v3.4.16 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.16){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 730 | 747 | Updated universal base image (UBI) to version `8.4-205` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} plug-in and driver | v2.0.7 | v2.0.8 | Updated to use Go version `1.16.6`. Updated universal base image (UBI) to version `8.4-205` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.20.8-2 | v1.20.9-1 | Updated to support the Kubernetes `1.20.9` release and to use Go version `1.15.14`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 394 | 395 | Updated universal base image (UBI) to version `8.4-205` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | b68ea92 | 945df65 | Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. |
| Key Management Service provider | v2.3.5 | v2.3.6 | Updated universal base image (UBI) to the latest version to resolve CVEs. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.7.16 | 4.7.19 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-19){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.7.0-20210608 | v4.7.0-20210630 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210630){: external}. |
| OpenVPN Operator image | v1.3.3 | v1.3.4 | Updated Ansible operator base image to version `1.8.1` to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.7.0-20210608 | v4.7.0-20210630 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210630){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.7.0+20210608 | 4.7.0+20210630 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210630){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.16_1523_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.7.19_1525_openshift, released 19 July 2021
{: #4719_1525}

The following table shows the changes that are in the worker node fix pack `4.7.19_1525_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.7.18 | 4.7.19 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-19){: external}. |
| RHEL 7 Packages| N/A | N/A | Updated worker node image with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.18_1524_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.7.18_1524_openshift, released 6 July 2021
{: #4718_1524}

The following table shows the changes that are in the worker node fix pack `4.7.18_1524_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 700dc6 | aae810 | Updated image with fixes for [CVE-2021-3520](https://nvd.nist.gov/vuln/detail/CVE-2021-3520){: external}, [CVE-2021-20271](https://nvd.nist.gov/vuln/detail/CVE-2021-20271){: external}, [CVE-2021-3516](https://nvd.nist.gov/vuln/detail/CVE-2021-3516){: external}, [CVE-2021-3517](https://nvd.nist.gov/vuln/detail/CVE-2021-3517){: external}, [CVE-2021-3518](https://nvd.nist.gov/vuln/detail/CVE-2021-3518){: external}, [CVE-2021-3537](https://nvd.nist.gov/vuln/detail/CVE-2021-3537){: external}, and [CVE-2021-3541](https://nvd.nist.gov/vuln/detail/CVE-2021-3541). |
| {{site.data.keyword.redhat_openshift_notm}} node | 4.7.16 | 4.7.18 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](http://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.16_1522_openshift" caption-side="top"}


### Changelog for master fix pack 4.7.16_1523_openshift, released 28 June 2021
{: #4716_1523}

The following table shows the changes that are in the master fix pack patch update `4.7.16_1523_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.12 | v1.2.13 | Updated to use `Go` version `1.15.12`. Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 695 | 730 | Updated to use `Go` version `1.16.15`. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} plug-in and driver | v2.0.6 | v2.0.7 | Updated to use `Go` version `1.15.12`. Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.20.7-4 | v1.20.8-2 | Updated to support the Kubernetes `1.20.8` release and to use `Go` version `1.15.13`. Updated `Go` dependencies to resolve CVEs. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 393 | 394 | Updated to use `Go` version `1.15.12`. Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external} and [CVE-2021-27219](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-27219){: external}. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | cfd8ae9 | b68ea92 | Updated image for [CVE-2021-27219](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-27219){: external}. |
| Key Management Service provider | v2.3.4 | v2.3.5 | Updated to use `Go` version `1.15.12`. Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.7.12 | 4.7.16 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-16){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.7.0-20210512 | v4.7.0-20210608 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210608){: external}. |
| OpenVPN Operator image | v1.3.2 | v1.3.3 | Updated ansible operator base image to version `1.8.0` to resolve CVEs. |
| Portieris admission controller | v0.10.2 | v0.10.3 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.10.3){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.7.0-20210512 | v4.7.0-20210608 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210608){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.7.0+20210512 | 4.7.0+20210608 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210608){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.12_1520_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.7.16_1522_openshift, released 22 June 2021
{: #4716_1522}

The following table shows the changes that are in the worker node fix pack `4.7.16_1522_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 26c5cc | d3dc33 | Updated image with fixes for [CVE-2020-24977](https://nvd.nist.gov/vuln/detail/CVE-2020-24977){: external}, [CVE-2020-13434](https://nvd.nist.gov/vuln/detail/CVE-2020-13434){: external}, [CVE-2020-15358](https://nvd.nist.gov/vuln/detail/CVE-2020-15358){: external}, [CVE-2020-29361](https://nvd.nist.gov/vuln/detail/CVE-2020-29361){: external}, [CVE-2020-29362](https://nvd.nist.gov/vuln/detail/CVE-2020-29362){: external}, [CVE-2020-29363](https://nvd.nist.gov/vuln/detail/CVE-2020-29363){: external}, [CVE-2019-2708](https://nvd.nist.gov/vuln/detail/CVE-2019-2708){: external}, [CVE-2019-13012](https://nvd.nist.gov/vuln/detail/CVE-2019-13012){: external}, [CVE-2020-13543](https://nvd.nist.gov/vuln/detail/CVE-2020-13543){: external}, [CVE-2020-13584](https://nvd.nist.gov/vuln/detail/CVE-2020-13584){: external}, [CVE-2020-9948](https://nvd.nist.gov/vuln/detail/CVE-2020-9948){: external}, [CVE-2020-9951](https://nvd.nist.gov/vuln/detail/CVE-2020-9951){: external}, [CVE-2020-9983](https://nvd.nist.gov/vuln/detail/CVE-2020-9983){: external}, [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}, [CVE-2020-8231](https://nvd.nist.gov/vuln/detail/CVE-2020-8231){: external}, [CVE-2020-8284](https://nvd.nist.gov/vuln/detail/CVE-2020-8284){: external}, [CVE-2020-8285](https://nvd.nist.gov/vuln/detail/CVE-2020-8285){: external}, [CVE-2020-8286](https://nvd.nist.gov/vuln/detail/CVE-2020-8286){: external}, [CVE-2016-10228](https://nvd.nist.gov/vuln/detail/CVE-2016-10228){: external}, [CVE-2019-25013](https://nvd.nist.gov/vuln/detail/CVE-2019-25013){: external}, [CVE-2019-9169](https://nvd.nist.gov/vuln/detail/CVE-2019-9169){: external}, [CVE-2020-27618](https://nvd.nist.gov/vuln/detail/CVE-2020-27618){: external}, [CVE-2021-3326](https://nvd.nist.gov/vuln/detail/CVE-2021-3326){: external}, [CVE-2020-26116](https://nvd.nist.gov/vuln/detail/CVE-2020-26116){: external}, [CVE-2020-27619](https://nvd.nist.gov/vuln/detail/CVE-2020-27619){: external}, [CVE-2021-23336](https://nvd.nist.gov/vuln/detail/CVE-2021-23336){: external}, [CVE-2021-3177](https://nvd.nist.gov/vuln/detail/CVE-2021-3177){: external}, [CVE-2019-3842](https://nvd.nist.gov/vuln/detail/CVE-2019-3842){: external}, [CVE-2020-13776](https://nvd.nist.gov/vuln/detail/CVE-2020-13776){: external}, [CVE-2020-24330](https://nvd.nist.gov/vuln/detail/CVE-2020-24330){: external}, [CVE-2020-24331](https://nvd.nist.gov/vuln/detail/CVE-2020-24331){: external}, [CVE-2020-24332](https://nvd.nist.gov/vuln/detail/CVE-2020-24332){: external}, [CVE-2017-14502](https://nvd.nist.gov/vuln/detail/CVE-2017-14502){: external}, [CVE-2020-8927](https://nvd.nist.gov/vuln/detail/CVE-2020-8927){: external} and [CVE-2020-28196](https://nvd.nist.gov/vuln/detail/CVE-2020-28196){: external}. |
| {{site.data.keyword.registrylong_notm}} | N/A | N/A | Added private-only registry support for `ca.icr.io`, `br.icr.io` and `jp2.icr.io`. | 
| {{site.data.keyword.redhat_openshift_notm}} | 4.7.13 | 4.7.16 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](http://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html){: external}. | 
| RHEL 7 Packages | 3.10.0-1160.25 | 3.10.0-1160.31 | Updated worker node image with kernel package updates for [CVE-2020-8648](https://nvd.nist.gov/vuln/detail/CVE-2020-8648){: external}, [CVE-2020-12362](https://nvd.nist.gov/vuln/detail/CVE-2020-12362)[CVE-2020-12363](https://nvd.nist.gov/vuln/detail/CVE-2020-12363)[CVE-2020-12364](https://nvd.nist.gov/vuln/detail/CVE-2020-12364)[CVE-2020-27170](https://nvd.nist.gov/vuln/detail/CVE-2020-27170)[CVE-2021-3347](https://nvd.nist.gov/vuln/detail/CVE-2021-3347){: external}, [CVE-2020-24489](https://nvd.nist.gov/vuln/detail/CVE-2020-24489){: external}, [CVE-2020-24511](https://nvd.nist.gov/vuln/detail/CVE-2020-24511)[CVE-2020-24512](https://nvd.nist.gov/vuln/detail/CVE-2020-24512){: external}, [CVE-2020-24513](https://nvd.nist.gov/vuln/detail/CVE-2020-24513){: external} and [CVE-2021-25217](https://nvd.nist.gov/vuln/detail/CVE-2021-25217){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.7.13_1521_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.7.13_1521_openshift, released 9 June 2021
{: #4713_1521}

The following table shows the changes that are in the worker node fix pack `4.7.13_1521_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 26c5cc | 700dc6 | Updated the image for [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}.|
|{{site.data.keyword.redhat_openshift_notm}} | 4.6.31 | 4.7.13 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-13){: external}. The update resolves CVE-2021-30465 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6462567){: external}). |
| TCP `keepalive` optimization for VPC | N/A | N/A | Set the `net.ipv4.tcp_keepalive_time` setting to 180 seconds for compatibility with VPC gateways. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates for [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.31_1545_openshift" caption-side="top"}

### Changelog for master fix pack 4.7.12_1520_openshift, released 9 June 2021
{: #4712_1520}

The following table shows the changes that are in the master fix pack patch update `4.7.12_1520_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.17.2 | v3.19.1 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases){: external}. |
| Calico Operator | v1.13.4 | v1.17.3 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.17.3){: external}. |
| Gateway-enabled cluster controller | 1352 | 1348 | Updated to run as a non-root user by default, with privileged escalation as needed. |
| {{site.data.keyword.IBM_notm}} Calico extension | 689 | 695 | Updated the universal base image (UBI) to version 8.4 to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | v2.0.4 | v2.0.6 | Updated UBI minimal base image to version 8.4 to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.11-3 | v1.20.7-4 | Updated to support the Kubernetes 1.20.7 release, use `calicoctl` version 3.17.3 and implement additional {{site.data.keyword.IBM_notm}} security controls. **Unsupported**: Although the Kubernetes [SCTP protocol](https://kubernetes.io/docs/concepts/services-networking/service/#sctp){: external} and [application protocol](https://kubernetes.io/docs/concepts/services-networking/service/#application-protocol){: external} features are generally available in the community release, creating load balancers that use these protocols is not supported in {{site.data.keyword.openshiftlong_notm}} clusters. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 392 | 393 | Updated UBI base image to version 8.4 to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 63cd064 | cfd8ae9 | Update to use `Go` version 1.16.4. Updated UBI base image to version 8.4 to resolve CVEs. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.28 (master) | 4.7.12 (master) | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-12){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} configuration | N/A | N/A | Updated the [feature gate configuration](/docs/openshift?topic=openshift-service-settings#feature-gates). |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20210512 | v4.7.0-20210512 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210512){: external}. |
| OpenVPN Operator image | v1.3.1 | v1.3.2 | Updated ansible operator base image to version 1.7.2 to resolve CVEs and updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| {{site.data.keyword.openshiftlong_notm}}  Metrics Server | v4.6.0-20210512 | v4.7.0-20210512 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210512){: external}. |
| {{site.data.keyword.openshiftlong_notm}}  toolkit | 4.6.0+20210512 | 4.7.0+20210512 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.7.0+20210512){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.28_1543_openshift" caption-side="top"}

## Version 4.6 changelog
{: #version-46}

Review the changelogs for {{site.data.keyword.openshiftlong_notm}} version 4.6 patch updates.
{: shortdesc}

### Changelog for master fix pack 4.6.48_1573_openshift, released 3 March 2022
{: #4648_1573}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.21 | v1.3.3 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds fix for [CVE-2021-43565](https://www.whitesourcesoftware.com/vulnerability-database/CVE-2021-43565){: external}. Adds Golang dependency updates. |
| Gateway-enabled cluster controller | 1586 | 1653 | Updated to use `Go` version `1.17.7` and updated `Go` modules to fix CVEs. |
| IBM Calico extension | 923 | 929 | Updated universal base image (UBI) to the `8.5-230` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| IBM Cloud Block Storage driver and plug-in | v2.1.6 | v2.1.7 | Adds fix for CVE-2021-3538](https://vuln.whitesourcesoftware.com/vulnerability/CVE-2021-3538){: external}. |
| IBM Cloud Controller Manager | v1.19.16-6 | v1.19.16-9 | Adds changes to the renovate rules. |
| IBM Cloud File Storage plug-in and monitor | 404 | 405 | Adds fix for [CVE-2021-3538](https://vuln.whitesourcesoftware.com/vulnerability/CVE-2021-3538){: external} and adds dependency updates. |
| Key Management Service provider | v2.3.13 | v2.4.3 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds fix for [CVE-2021-43565](https://www.whitesourcesoftware.com/vulnerability-database/CVE-2021-43565){: external}. Adds Golang dependency updates. |
| OpenVPN server | 2.5.4-r0-IKS-555 | 2.5.4-r0-IKS-562 | Turns off CRL verification in the openvpn image. |
| OpenVPN Operator image | v1.4.0 | v1.4.1 | Turns off CRL verification in the opevpn-operator images. |
| Red Hat OpenShift Control Plane Operator | v4.6.0-20220107 | v4.6.0-20220222 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20220222){: external}. |
| Red Hat OpenShift on IBM Cloud Metrics Server | v4.6.0-20220107 | v4.6.0-20220222 | See the {{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20220222){: external}. |
| Red Hat OpenShift on IBM Cloud toolkit | 4.6.0+20220107 | 4.6.0+20220222 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20220222){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.48_1570_openshift" caption-side="top"}

### Change log for worker node fix pack 4.6.53_1574_openshift, released 28 February 2022
{: #4653_1574}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | 3.10.0-1160.53.1.el7 | 3.10.0-1160.59.1.el7 | Kernel and package updates for [CVE-2020-25709](https://nvd.nist.gov/vuln/detail/CVE-2020-25709){: external}, [CVE-2020-25710](https://nvd.nist.gov/vuln/detail/CVE-2020-25710){: external}, [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}, [CVE-2020-0465](https://nvd.nist.gov/vuln/detail/CVE-2020-0465){: external}, [CVE-2020-0466](https://nvd.nist.gov/vuln/detail/CVE-2020-0466){: external}, [CVE-2021-0920](https://nvd.nist.gov/vuln/detail/CVE-2021-0920){: external}, [CVE-2021-3564](https://nvd.nist.gov/vuln/detail/CVE-2021-3564){: external}, [CVE-2021-3573](https://nvd.nist.gov/vuln/detail/CVE-2021-3573){: external}, [CVE-2021-3752](https://nvd.nist.gov/vuln/detail/CVE-2021-3752){: external}, [CVE-2021-4155](https://nvd.nist.gov/vuln/detail/CVE-2021-4155){: external}, [CVE-2022-0330](https://nvd.nist.gov/vuln/detail/CVE-2022-0330){: external}, [CVE-2022-22942](https://nvd.nist.gov/vuln/detail/CVE-2022-22942) | 
| HA proxy | f6a2b3 | 15198fb | Contains fixes for [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}. | 
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.53_1572_openshift" caption-side="top"}

### Change log for worker node fix pack 4.6.53_1572_openshift, released 14 February 2022
{: #4653_1572}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | N/A |
|  {{site.data.keyword.redhat_openshift_notm}}  | N/A | N/A | N/A |
| Haproxy | d38fa1 | f6a2b3 | [CVE-2021-3521](https://nvd.nist.gov/vuln/detail/CVE-2021-3521){: external}   [CVE-2021-4122](https://nvd.nist.gov/vuln/detail/CVE-2021-4122){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.53_1571_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.53_1571_openshift, released 31 January 2022
{: #4653_1571}

The following table shows the changes that are in the worker node fix pack `4.6.53_1571_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | Updated worker node images with package updates for [CVE-2021-4034](https://nvd.nist.gov/vuln/detail/CVE-2021-4034){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.53_1569_openshift" caption-side="top"}

### Changelog for master fix pack 4.6.48_1570_openshift, released 26 January 2022
{: #4648_1570}

The following table shows the changes that are in the master fix pack patch update `4.6.48_1570_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | N/A | N/A | Changed to improve Calico availability during updates. |
| Cluster health image | v1.2.20 | v1.2.21 | Updated to use `Go` version `1.17.5`, updated Go dependencies and golangci-lint. |
| {{site.data.keyword.IBM_notm}} Calico extension | 900 | 923 | Updated universal base image (UBI) to the `8.5-218` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | v2.1.3 | v2.1.6 | Updated to use `Go` version `1.16.13`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.16-5 | v1.19.16-6 | Exclude `CVE-2020-14312` from scanning |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 402 | 404 | Updated universal base image (UBI) to the `8.5-218` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 3430e03 | 0fc9949 | Updated universal base image (UBI) to the `8.5-218` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| Key Management Service provider | v2.3.12 | v2.3.13 | Updated `Go` dependencies and golangci-lint. |
| Load balancer and load balancer monitor for IBM Cloud Provider | 1660 | 1748 | Updated the Alpine base image to the `3.15` version to resolve CVEs. Updated to use `Go` version `1.17.6`. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.47 | 4.6.48 | Changed the duration of the Kubernetes API server certificate from 825 days to 730 days. Changed the duration of the cluster CA certificate from 30 years to 10 years. Updated to fix [CVE-2021-25735](https://www.ibm.com/support/pages/node/6549374){: external}.  See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-48). |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20211201 | v4.6.0-20220107 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0%2B20220107). |
| OpenVPN client | 2.4.6-r3-IKS-463 | 2.5.4-r0-IKS-556 | Update base image to alpine `3.15` to address CVEs, no longer set the `--compress config` option, updated scripts. |
| OpenVPN server | 2.4.6-r3-IKS-462 | 2.5.4-r0-IKS-555 | Update base image to alpine `3.15` to address CVEs, no longer set the `--compress config` option, updated scripts. |
| OpenVPN Operator image | v1.3.9 | v1.4.0 | Updated `OpenVPN` to version `2.5.4-r0`.  Remove deprecated compression config option from VPN server. Sset cipher explicitly to default value to avoid warning message in logs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20211201 | v4.6.0-20220107 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0%2B20220107). |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20211201 | 4.6.0+20220107 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0%2B20220107). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.47_1569_openshift" caption-side="top"}


### Changelog for worker node fix pack 4.6.53_1569_openshift, released 18 January 2022
{: #4653_1569}

The following table shows the changes that are in the worker node fix pack `4.6.53_1569_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.49.1.el7 | 3.10.0-1160.53.1.el7 | Kernel and package updates for [CVE-2020-25704](https://nvd.nist.gov/vuln/detail/CVE-2020-25704){: external}, [CVE-2020-36322](https://nvd.nist.gov/vuln/detail/CVE-2020-36322){: external}, [CVE-2021-42739](https://nvd.nist.gov/vuln/detail/CVE-2021-42739){: external}, and [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.52 | 4.6.53 | See the [change logs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-53){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.52_1568_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.52_1568_openshift, released 4 January 2022
{: #4652_1568}

The following table shows the changes that are in the worker node fix pack patch update `4.6.52_1568_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 3b8663 | d38fa1 | Contains fixes for [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.52_1567_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.52_1567_openshift, released 20 December 2021
{: #4652_1567_openshift}

The following table shows the changes that are in the worker node fix pack patch update `4.6.52_1567_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} node | 4.6.49 | 4.6.52 | See the [change logs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-52){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.49_1566_openshift" caption-side="top"}

### Changelog for master fix pack 4.6.47_1565_openshift, released 7 December 2021
{: #4647_1565}

The following table shows the changes that are in the master fix pack patch update `4.6.47_1565_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.17.5 | v3.17.6 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases){: external}. |
| Calico Operator | v1.13.9 | v1.13.11 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.13.11){: external}. |
| Cluster health image | v1.2.18 | v1.2.20 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| Gateway-enabled cluster controller | 1567 | 1586 | Updated Alpine base image to the latest `3.14` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 864 | 900 | Updated universal base image (UBI) to the `8.5-204` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | v2.1.2 | v2.1.3 | Updated universal base image (UBI) to the `8.5-204` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 401 | 402 | Updated universal base image (UBI) to the `8.5-204` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 4ca5637 | 3430e03 | Updated universal base image (UBI) to the latest `8.5` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| Key Management Service provider | v2.3.10 | v2.3.12 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| Load balancer and load balancer monitor for {{site.data.keyword.IBM_notm}} Cloud Provider | 1589 | 1660 | Updated Alpine base image to the latest `3.14` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20211109 | v4.6.0-20211201 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20211201){: external}. |
| OpenVPN Operator image | v1.3.8 | v1.3.9 | Updated ansible operator base image to version `v1.14.0` to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20211109 | v4.6.0-20211201 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20211201){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20211109 | 4.6.0+20211201 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20211201){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.47_1563_openshift" caption-side="top"}


### Changelog for worker node fix pack 4.6.49_1566_openshift, released 6 December 2021
{: #4649_1566}

The following table shows the changes that are in the worker node fix pack patch update `4.6.49_1566_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.45 | 3.10.0-1160.49 | Updated worker node images and kernel with package updates. Contains fixes for [CVE-2020-36385](https://nvd.nist.gov/vuln/detail/CVE-2020-36385){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-41617](https://nvd.nist.gov/vuln/detail/CVE-2021-41617){: external}, [CVE-2021-20271](https://nvd.nist.gov/vuln/detail/CVE-2021-20271)"{: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.49_1564_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.49_1564_openshift, released 22 November 2021
{: #4649_1564}

The following table shows the changes that are in the worker node fix pack patch update `4.6.49_1564_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Haproxy | 07f1e9e | 3b8663 | Contains fixes for [CVE-2021-20231](https://nvd.nist.gov/vuln/detail/CVE-2021-20231){: external}, [CVE-2021-20232](https://nvd.nist.gov/vuln/detail/CVE-2021-20232){: external}, [CVE-2021-3580](https://nvd.nist.gov/vuln/detail/CVE-2021-3580){: external}, [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946){: external}, [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947){: external}, [CVE-2021-22876](https://nvd.nist.gov/vuln/detail/CVE-2021-22876){: external}, [CVE-2021-22898](https://nvd.nist.gov/vuln/detail/CVE-2021-22898){: external}, [CVE-2021-22925](https://nvd.nist.gov/vuln/detail/CVE-2021-22925){: external}, [CVE-2019-20838](https://nvd.nist.gov/vuln/detail/CVE-2019-20838){: external}, [CVE-2020-14155](https://nvd.nist.gov/vuln/detail/CVE-2020-14155){: external}, [CVE-2018-20673](https://nvd.nist.gov/vuln/detail/CVE-2018-20673){: external}, [CVE-2021-42574](https://nvd.nist.gov/vuln/detail/CVE-2021-42574){: external}, [CVE-2019-17594](https://nvd.nist.gov/vuln/detail/CVE-2019-17594){: external}, [CVE-2019-17595](https://nvd.nist.gov/vuln/detail/CVE-2019-17595){: external}, [CVE-2020-12762](https://nvd.nist.gov/vuln/detail/CVE-2020-12762){: external}, [CVE-2020-16135](https://nvd.nist.gov/vuln/detail/CVE-2020-16135){: external}, [CVE-2021-3445](https://nvd.nist.gov/vuln/detail/CVE-2021-3445){: external}, [CVE-2021-36084](https://nvd.nist.gov/vuln/detail/CVE-2021-36084){: external}, [CVE-2021-36085](https://nvd.nist.gov/vuln/detail/CVE-2021-36085){: external}, [CVE-2021-36086](https://nvd.nist.gov/vuln/detail/CVE-2021-36086){: external}, [CVE-2021-36087](https://nvd.nist.gov/vuln/detail/CVE-2021-36087){: external}, [CVE-2021-20266](https://nvd.nist.gov/vuln/detail/CVE-2021-20266){: external}, [CVE-2019-18218](https://nvd.nist.gov/vuln/detail/CVE-2019-18218){: external}, [CVE-2021-23840](https://nvd.nist.gov/vuln/detail/CVE-2021-23840){: external}, [CVE-2021-23841](https://nvd.nist.gov/vuln/detail/CVE-2021-23841){: external}, [CVE-2021-27645](https://nvd.nist.gov/vuln/detail/CVE-2021-27645){: external}, [CVE-2021-33574](https://nvd.nist.gov/vuln/detail/CVE-2021-33574){: external}, [CVE-2021-35942](https://nvd.nist.gov/vuln/detail/CVE-2021-35942){: external}, [CVE-2021-33560](https://nvd.nist.gov/vuln/detail/CVE-2021-33560){: external}, [CVE-2019-13750](https://nvd.nist.gov/vuln/detail/CVE-2019-13750){: external}, [CVE-2019-13751](https://nvd.nist.gov/vuln/detail/CVE-2019-13751){: external}, [CVE-2019-19603](https://nvd.nist.gov/vuln/detail/CVE-2019-19603){: external}, [CVE-2019-5827](https://nvd.nist.gov/vuln/detail/CVE-2019-5827){: external}, [CVE-2020-13435](https://nvd.nist.gov/vuln/detail/CVE-2020-13435){: external}, [CVE-2020-24370](https://nvd.nist.gov/vuln/detail/CVE-2020-24370){: external}, [CVE-2021-28153](https://nvd.nist.gov/vuln/detail/CVE-2021-28153){: external}, [CVE-2021-3800](https://nvd.nist.gov/vuln/detail/CVE-2021-3800){: external}, [CVE-2021-33928](https://nvd.nist.gov/vuln/detail/CVE-2021-33928){: external}, [CVE-2021-33929](https://nvd.nist.gov/vuln/detail/CVE-2021-33929){: external}, [CVE-2021-33930](https://nvd.nist.gov/vuln/detail/CVE-2021-33930){: external}, [CVE-2021-33938](https://nvd.nist.gov/vuln/detail/CVE-2021-33938){: external}, and[CVE-2021-3200](https://nvd.nist.gov/vuln/detail/CVE-2021-3200){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.49_1562_openshift" caption-side="top"}

### Changelog for master fix pack 4.6.47_1563_openshift, released 17 November 2021
{: #4647_1563}

The following table shows the changes that are in the master fix pack patch update `4.6.47_1563_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.16 | v1.2.18 | Updated `Go` module dependencies and to use `Go` version `1.16.9`.  Updated image for [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946), [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947), [CVE-2021-33928](https://nvd.nist.gov/vuln/detail/CVE-2021-33928), [CVE-2021-33929](https://nvd.nist.gov/vuln/detail/CVE-2021-33929) and [CVE-2021-33930](https://nvd.nist.gov/vuln/detail/CVE-2021-33930).  |
| etcd | v3.4.17 | v3.4.18 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.18). |
| Gateway-enabled cluster controller | 1510 | 1567 | Updated to use `Go` version `1.16.9`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.15-3 | v1.19.16-3 | Updated to support the Kubernetes `1.19.16` release. Updated image for [DLA-2797-1](https://www.debian.org/lts/security/2021/dla-2797). |
| {{site.data.keyword.cloud_notm}} RBAC Operator | e3cb629 | 4ca5637 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. |
| Key Management Service provider | v2.3.8 | v2.3.10 | Updated `Go` module dependencies and to use `Go` version `1.16.9`.  Updated image for [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946). |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1550 | 1589 | Updated to use `Go` version `1.16.9`. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20210923 | v4.6.0-20211109 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20211109). |
| OpenVPN client | 2.4.6-r3-IKS-386 | 2.4.6-r3-IKS-463 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN server | 2.4.6-r3-IKS-385 | 2.4.6-r3-IKS-462 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN Operator image | v1.3.7 | v1.3.8 | Updated ansible operator base image to version `v1.13.1` to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20210923 | v4.6.0-20211109 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20211109). |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20210923 | 4.6.0+20211109 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20211109). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.47_1560_openshift" caption-side="top"}


### Changelog for worker node fix pack 4.6.49_1562_openshift, released 10 November 2021
{: #4649_1562}

The following table shows the changes that are in the worker node fix pack patch update `4.6.49_1562_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages| N/A | N/A | Updated worker node image packages for [CVE-2021-42574](https://nvd.nist.gov/vuln/detail/CVE-2021-42574){: external} |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.48 | 4.6.49 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-49){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.46_1558_openshift" caption-side="top"}

### Changelog for master fix pack 4.6.47_1560_openshift, released 29 October 2021
{: #4647_1560}

The following table shows the changes that are in the master fix pack patch update `4.6.47_1560_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.15 | v1.2.16 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs:  [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}, [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}, and [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}. |
| etcd | v3.4.16 | v3.4.17 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.17){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 763 | 864 | Updated to use `Go` version `1.16.9`. Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | v2.1.1 | v2.1.2 | Updated universal base image (UBI) to version `8.4-210` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.15-1 | v1.19.15-3 | Updated to ignore VPC load balancer (LB) state when a LB delete is requested. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.filestorage_short}} plug-in and monitor | 400 | 401 | Updated universal base image (UBI) to the latest `8.4-210` version to resolve CVEs. |
| Key Management Service provider | v2.3.7 | v2.3.8 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs:  [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}, [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}, and [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.44 | 4.6.47 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-47).{: external} |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20210917 | v4.6.0-20210923 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210923){: external}. |
| OpenVPN Operator image | v1.3.6 | v1.3.7 | Updated ansible operator base image to version `v1.12.0` to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20210917 | v4.6.0-20210923 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210923){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20210917 | 4.6.0+20210923 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210923){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.44_1556_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.48_1561_openshift, released 25 October 2021
{: #4648_1561}

The following table shows the changes that are in the worker node fix pack patch update `4.6.48_1561_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.46 | 4.6.48 | See [the {{site.data.keyword.redhat_openshift_notm}} changelogs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-48){: external}. |
| RHEL 7 Packages | 3.10.0-1160.42.2.el7 | 3.10.0-1160.45.1.el7 | Updated worker node images and kernel with package updates for [CVE-2021-3778](https://nvd.nist.gov/vuln/detail/CVE-2021-3778){: external} and [CVE-2021-3796](https://nvd.nist.gov/vuln/detail/CVE-2021-3796){: external}. |
| Worker-pool taint automation | N/A | N/A | Fixes known issue related to worker-pool taint automation that prevents workers from getting providerID. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.46_1558_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.46_1558_openshift, released 11 October 2021
{: #4646_1558_openshift}

The following table shows the changes that are in the worker node fix pack patch update `4.6.46_1558_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.45 | 4.6.46 | See the [change logs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-46){: external}. The update resolves CVE-2021-25741 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6515606){: external}). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.45_1557_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.45_1557_openshift, released 27 September 2021
{: #4645_1557}

The following table shows the changes that are in the worker node fix pack patch update `4.6.45_1557_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Disk identification | NA | NA | Enhanced the disk identification logic to handle the case of 2+ partitions. |
| Haproxy | 9c98dc5 | 07f1e9 | Updated image with fixes for [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922), [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923), [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924), [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222), and [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750). |
|OpenShift Container Platform| 4.6.44 | 4.6.45 | See [changelogs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-45). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.44_1555_openshift" caption-side="top"}

### Changelog for master fix pack 4.6.44_1556_openshift, released 28 September 2021
{: #4644_1556}

The following table shows the changes that are in the master fix pack patch update `4.6.44_1556_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.17.2 | v3.17.5 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases). |
| Calico Operator | v1.13.4 | v1.13.9 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.13.9). |
| Gateway-enabled cluster controller | 1444 | 1510 | Updated image for [CVE-2021-3711](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3711) and [CVE-2021-3712](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3712). |
| {{site.data.keyword.IBM_notm}} Cloud Block Storage plug-in and driver | v2.0.9 | v2.1.1 | Updated to use `Go` version `1.16.7`. Updated universal base image (UBI) to the latest `8.4-208` version to resolve CVEs. |
| {{site.data.keyword.IBM_notm}} Cloud Controller Manager | v1.19.14-1 | v1.19.15-1 | Updated to support the Kubernetes `1.19.15` release. Fixed a bug that may cause node initialization to fail when a new node reuses the name of a deleted node. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.filestorage_short}} plug-in and monitor | 398 | 400 | Updated to use `Go` version `1.16.7`. Updated universal base image (UBI) to the latest `8.4-208` version to resolve CVEs. |
| {{site.data.keyword.IBM_notm}} Cloud RBAC Operator | 945df65 | e3cb629 | Updated to use `Go` version `1.16.7`. |
| Kubernetes API server auditing configuration | N/A | N/A| Updated to support `verbose` [Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit#audit-api-server). |
| Load balancer and load balancer monitor for {{site.data.keyword.IBM_notm}} Cloud Provider | 1510 | 1550 | Updated image for [CVE-2021-3711](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3711) and [CVE-2021-3712](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3712). |
|OpenShift Container Platform| 4.6.42 | 4.6.44 | See the [OpenShift Container Platform release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-44). |
|OpenShift Container PlatformControl Plane Operator | v4.6.0-20210816 | v4.6.0-20210917 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210917). |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20210816 | v4.6.0-20210917 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210917). |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20210816 | 4.6.0+20210917 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210917). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.42_1553_openshift" caption-side="top"}



### Changelog for worker node fix pack 4.6.44_1555_openshift, released 13 September 2021
{: #4644_1555}

The following table shows the changes that are in the worker node fix pack patch update `4.6.44_1555_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| OpenShift Container Platform | 4.6.43 | 4.6.44 |See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-44){: external}. |
| RHEL 7 Packages | 3.10.0-1160.36.2.el7 | 3.10.0-1160.42.2.el7 | Updated worker node image with package updates for [CVE-2021-25214](https://nvd.nist.gov/vuln/detail/CVE-2021-25214){: external}, [CVE-2020-27777](https://nvd.nist.gov/vuln/detail/CVE-2020-27777){: external}, [CVE-2021-22555](https://nvd.nist.gov/vuln/detail/CVE-2021-22555){: external}, [CVE-2021-29154](https://nvd.nist.gov/vuln/detail/CVE-2021-29154){: external}, [CVE-2021-29650](https://nvd.nist.gov/vuln/detail/CVE-2021-29650){: external}, [CVE-2021-32399](https://nvd.nist.gov/vuln/detail/CVE-2021-32399){: external}, and [CVE-2021-3715](https://nvd.nist.gov/vuln/detail/CVE-2021-3715){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.43_1554_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.43_1554_openshift, released 30 August 2021
{: #4643_1554}

The following table shows the changes that are in the worker node fix pack patch update `4.6.43_1554_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| OpenShift Container Platform | 4.6.42 | 4.6.43 | See [changelogs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-43){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.42_1552_openshift" caption-side="top"}

### Changelog for master fix pack 4.6.42_1553_openshift, released 25 August 2021
{: #4642_1553}

The following table shows the changes that are in the master fix pack patch update `4.6.42_1553_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | N/A | N/A | Updated the rolling update configuration for the `calico-node` daemonset in the `calico-system` namespace.  The configuration is now the same regardless of the number of cluster worker nodes. |
| Cluster health image | v1.2.14 | v1.2.15 | Updated to use `Go` version `1.15.15`. Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. |
| Cluster master operations | N/A | N/A | Fixes DNS configuration problem that may block {{site.data.keyword.redhat_openshift_notm}} operator updates. |
| Gateway-enabled cluster controller | 1348 | 1444 | Updated image for [CVE-2021-36159](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-36159){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 747 | 763 | Updated to use `Go` version `1.16.6`. Updated universal base image (UBI) to the latest `8.4-205` version to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} plug-in and driver | v2.0.8 | v2.0.9 | Updated to use `Go` version `1.16.6`. Updated image for [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33910){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.13-1 | v1.19.14-1 | Updated to support the Kubernetes `1.19.14` release and to use `Go` version `1.15.15`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 395 | 398 | Updated to use `Go` version `1.16.6`. Updated image for [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33910){: external}. |
| Key Management Service provider | v2.3.6 | v2.3.7 | Updated to use `Go` version `1.15.15`. Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1328 | 1510 | Updated image for [CVE-2020-27780](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-27780){: external}. |
| {{site.data.keyword.redhat_openshift_notm}}| 4.6.38 | 4.6.42 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-42){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20210630 | v4.6.0-20210816 | See the [{{site.data.keyword.openshiftlong_notm}}toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210816){: external}. |
| OpenVPN Operator image | v1.3.4 | v1.3.6 | Updated image for [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33910){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20210630 | v4.6.0-20210816 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210816){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20210630 | 4.6.0+20210816 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210816){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.38_1550_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.42_1552_openshift, released 16 August 2021
{: #4642_1552}

The following table shows the changes that are in the worker node fix pack patch update `4.6.42_1552_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 68e6b3 | 9c98dc | Updated image with fixes for [CVE-2021-27218](https://nvd.nist.gov/vuln/detail/CVE-2021-27218){: external} |
| RHEL 7 Packages | N/A| N/A| Updated image with fixes for: [CVE-2020-0543](https://nvd.nist.gov/vuln/detail/CVE-2020-0543){: external}, [CVE-2020-0548](https://nvd.nist.gov/vuln/detail/CVE-2020-0548){: external}, [CVE-2020-0549](https://nvd.nist.gov/vuln/detail/CVE-2020-0549){: external}, [CVE-2020-8695](https://nvd.nist.gov/vuln/detail/CVE-2020-8695){: external}, [CVE-2020-8696](https://nvd.nist.gov/vuln/detail/CVE-2020-8696){: external}, [CVE-2020-8698](https://nvd.nist.gov/vuln/detail/CVE-2020-8698){: external}, [CVE-2020-24489](https://nvd.nist.gov/vuln/detail/CVE-2020-24489){: external}, [CVE-2020-24511](https://nvd.nist.gov/vuln/detail/CVE-2020-24511){: external}, and [CVE-2020-24512](https://nvd.nist.gov/vuln/detail/CVE-2020-24512){: external}. |
| OpenShift Container Platform | 4.6.40 | 4.6.42 | See [changelogs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-42){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.40_1551_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.40_1551_openshift, released 02 August 2021
{: #4640_1551}

The following table shows the changes that are in the worker node fix pack patch update `4.6.40_1551_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | aae810 | 68e6b3 | Updated image with fixes for [CVE-2021-33910](https://nvd.nist.gov/vuln/detail/CVE-2021-33910){: external}. |
| Registry endpoints | Added ability to access all global registries for private service enabled clusters through the public domain. Added zonal public registry endpoints for clusters with both private and public service endpoints enabled. |
| Read only disk self healing | For VPC Gen2 workers. Added automation to recover from disks going read only. |
| RHEL 7 Packages | 3.10.0-1160.31.1 | 3.10.0-1160.36.2 | Updated worker node images & Kernel with package updates: [CVE-2019-20934](https://nvd.nist.gov/vuln/detail/CVE-2019-20934){: external}, [CVE-2020-11668](https://nvd.nist.gov/vuln/detail/CVE-2020-11668){: external}, [CVE-2021-33033](https://nvd.nist.gov/vuln/detail/CVE-2021-33033){: external}, [CVE-2021-33034](https://nvd.nist.gov/vuln/detail/CVE-2021-33034){: external}, [CVE-2021-33909](https://nvd.nist.gov/vuln/detail/CVE-2021-33909){: external}. |
| OpenShift Container Platform | 4.6.38 |4.6.40 | See [changelogs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-40){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.38_1549_openshift" caption-side="top"}

### Changelog for master fix pack 4.6.38_1550_openshift, released 27 July 2021
{: #4638_1550}

The following table shows the changes that are in the master fix pack patch update `4.6.38_1550_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.13 | v1.2.14 | Updated universal base image (UBI) to the latest version to resolve CVEs. |
| etcd | v3.4.14 | v3.4.16 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.16){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 730 | 747 | Updated universal base image (UBI) to version `8.4-205` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} plug-in and driver | v2.0.7 | v2.0.8 | Updated to use Go version `1.16.6`. Updated universal base image (UBI) to version `8.4-205` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.12-2 | v1.19.13-1 | Updated to support the Kubernetes `1.19.13` release and to use Go version `1.15.14`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 394 | 395 | Updated universal base image (UBI) to version `8.4-205` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | b68ea92 | 945df65 | Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. |
| Key Management Service provider | v2.3.5 | v2.3.6 | Updated universal base image (UBI) to the latest version to resolve CVEs. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.34 | 4.6.38 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-38){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20210608 | v4.6.0-20210630 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210630){: external}. |
| OpenVPN Operator image | v1.3.3 | v1.3.4 | Updated Ansible operator base image to version `1.8.1` to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20210608 | v4.6.0-20210630 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210630){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20210608 | 4.6.0+20210630 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210630){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.34_1547_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.38_1549_openshift, released 19 July 2021
{: #4638_1549}

The following table shows the changes that are in the worker node fix pack `4.6.38_1549_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.36 | 4.6.38 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-38){: external}. |
| RHEL 7 Packages| N/A | N/A | Updated worker node image with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.36_1548_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.36_1548_openshift, released 6 July 2021
{: #4636_1548}

The following table shows the changes that are in the worker node fix pack `4.6.36_1548_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 700dc6 | aae810 | Updated image with fixes for [CVE-2021-3520](https://nvd.nist.gov/vuln/detail/CVE-2021-3520){: external}, [CVE-2021-20271](https://nvd.nist.gov/vuln/detail/CVE-2021-20271){: external}, [CVE-2021-3516](https://nvd.nist.gov/vuln/detail/CVE-2021-3516){: external}, [CVE-2021-3517](https://nvd.nist.gov/vuln/detail/CVE-2021-3517){: external}, [CVE-2021-3518](https://nvd.nist.gov/vuln/detail/CVE-2021-3518){: external}, [CVE-2021-3537](https://nvd.nist.gov/vuln/detail/CVE-2021-3537){: external}, and [CVE-2021-3541](https://nvd.nist.gov/vuln/detail/CVE-2021-3541). |
| {{site.data.keyword.redhat_openshift_notm}} node | 4.6.34 | 4.6.36 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-36){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.34_1546_openshift" caption-side="top"}

### Changelog for master fix pack 4.6.34_1547_openshift, released 28 June 2021
{: #4634_1547}

The following table shows the changes that are in the master fix pack patch update `4.6.34_1547_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.12 | v1.2.13 | Updated to use `Go` version `1.15.12`. Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. |
| Gateway-enabled cluster controller | 1352 | 1348 | Updated to run as a non-root user by default, with privileged escalation as needed. |
| {{site.data.keyword.IBM_notm}} Calico extension | 689 | 730 | Updated to use `Go` version `1.16.15`. Updated minimal universal base image (UBI) to version `8.4` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} plug-in and driver | v2.0.4 | v2.0.7 | Updated to use `Go` version `1.15.12`. Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. Updated minimal UBI to version 8.4 to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.11-3 | v1.19.12-2 | Updated to support the Kubernetes `1.19.12` release and to use `Go` version `1.15.13`. Updated Go dependencies to resolve CVEs. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 392 | 394 | Updated to use `Go` version `1.15.12`. Updated UBI to version `8.4` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 63cd064 | b68ea92 | Update to use `Go` version `1.16.4`. Updated UBI to version `8.4` to resolve CVEs. |
| Key Management Service provider | v2.3.4 | v2.3.5 | Updated to use `Go` version `1.15.12`. Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.28 | 4.6.34 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-34){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20210512 | v4.6.0-20210608 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210608){: external}. |
| OpenVPN Operator image | v1.3.1 | v1.3.3 | Updated ansible operator base image to version `1.8.0` to resolve CVEs and updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| Portieris admission controller | v0.10.2 | v0.10.3 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.10.3){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20210512 | v4.6.0-20210608 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210608){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20210512 | 4.6.0+20210608 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210608){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.28_1543_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.34_1546_openshift, released 22 June 2021
{: #4634_1546}

The following table shows the changes that are in the worker node fix pack `4.6.34_1546_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 26c5cc | d3dc33 | Updated image with fixes for [CVE-2020-24977](https://nvd.nist.gov/vuln/detail/CVE-2020-24977){: external}, [CVE-2020-13434](https://nvd.nist.gov/vuln/detail/CVE-2020-13434){: external}, [CVE-2020-15358](https://nvd.nist.gov/vuln/detail/CVE-2020-15358){: external}, [CVE-2020-29361](https://nvd.nist.gov/vuln/detail/CVE-2020-29361){: external}, [CVE-2020-29362](https://nvd.nist.gov/vuln/detail/CVE-2020-29362){: external}, [CVE-2020-29363](https://nvd.nist.gov/vuln/detail/CVE-2020-29363){: external}, [CVE-2019-2708](https://nvd.nist.gov/vuln/detail/CVE-2019-2708){: external}, [CVE-2019-13012](https://nvd.nist.gov/vuln/detail/CVE-2019-13012){: external}, [CVE-2020-13543](https://nvd.nist.gov/vuln/detail/CVE-2020-13543){: external}, [CVE-2020-13584](https://nvd.nist.gov/vuln/detail/CVE-2020-13584){: external}, [CVE-2020-9948](https://nvd.nist.gov/vuln/detail/CVE-2020-9948){: external}, [CVE-2020-9951](https://nvd.nist.gov/vuln/detail/CVE-2020-9951){: external}, [CVE-2020-9983](https://nvd.nist.gov/vuln/detail/CVE-2020-9983){: external}, [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}, [CVE-2020-8231](https://nvd.nist.gov/vuln/detail/CVE-2020-8231){: external}, [CVE-2020-8284](https://nvd.nist.gov/vuln/detail/CVE-2020-8284){: external}, [CVE-2020-8285](https://nvd.nist.gov/vuln/detail/CVE-2020-8285){: external}, [CVE-2020-8286](https://nvd.nist.gov/vuln/detail/CVE-2020-8286){: external}, [CVE-2016-10228](https://nvd.nist.gov/vuln/detail/CVE-2016-10228){: external}, [CVE-2019-25013](https://nvd.nist.gov/vuln/detail/CVE-2019-25013){: external}, [CVE-2019-9169](https://nvd.nist.gov/vuln/detail/CVE-2019-9169){: external}, [CVE-2020-27618](https://nvd.nist.gov/vuln/detail/CVE-2020-27618){: external}, [CVE-2021-3326](https://nvd.nist.gov/vuln/detail/CVE-2021-3326){: external}, [CVE-2020-26116](https://nvd.nist.gov/vuln/detail/CVE-2020-26116){: external}, [CVE-2020-27619](https://nvd.nist.gov/vuln/detail/CVE-2020-27619){: external}, [CVE-2021-23336](https://nvd.nist.gov/vuln/detail/CVE-2021-23336){: external}, [CVE-2021-3177](https://nvd.nist.gov/vuln/detail/CVE-2021-3177){: external}, [CVE-2019-3842](https://nvd.nist.gov/vuln/detail/CVE-2019-3842){: external}, [CVE-2020-13776](https://nvd.nist.gov/vuln/detail/CVE-2020-13776){: external}, [CVE-2020-24330](https://nvd.nist.gov/vuln/detail/CVE-2020-24330){: external}, [CVE-2020-24331](https://nvd.nist.gov/vuln/detail/CVE-2020-24331){: external}, [CVE-2020-24332](https://nvd.nist.gov/vuln/detail/CVE-2020-24332){: external}, [CVE-2017-14502](https://nvd.nist.gov/vuln/detail/CVE-2017-14502){: external}, [CVE-2020-8927](https://nvd.nist.gov/vuln/detail/CVE-2020-8927){: external} and [CVE-2020-28196](https://nvd.nist.gov/vuln/detail/CVE-2020-28196){: external}. |
| {{site.data.keyword.registrylong_notm}} | N/A | N/A | Added private-only registry support for `ca.icr.io`, `br.icr.io` and `jp2.icr.io`. | 
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.31 | 4.6.34 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-34){: external}. | 
| RHEL 7 Packages | 3.10.0-1160.25 | 3.10.0-1160.31 | Updated worker node image with kernel package updates for [CVE-2020-8648](https://nvd.nist.gov/vuln/detail/CVE-2020-8648){: external}, [CVE-2020-12362](https://nvd.nist.gov/vuln/detail/CVE-2020-12362)[CVE-2020-12363](https://nvd.nist.gov/vuln/detail/CVE-2020-12363)[CVE-2020-12364](https://nvd.nist.gov/vuln/detail/CVE-2020-12364)[CVE-2020-27170](https://nvd.nist.gov/vuln/detail/CVE-2020-27170)[CVE-2021-3347](https://nvd.nist.gov/vuln/detail/CVE-2021-3347){: external}, [CVE-2020-24489](https://nvd.nist.gov/vuln/detail/CVE-2020-24489){: external}, [CVE-2020-24511](https://nvd.nist.gov/vuln/detail/CVE-2020-24511)[CVE-2020-24512](https://nvd.nist.gov/vuln/detail/CVE-2020-24512){: external}, [CVE-2020-24513](https://nvd.nist.gov/vuln/detail/CVE-2020-24513){: external} and [CVE-2021-25217](https://nvd.nist.gov/vuln/detail/CVE-2021-25217){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.5.40_1541_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.31_1545_openshift, released 7 June 2021
{: #4631_1545}

The following table shows the changes that are in the worker node fix pack `4.6.31_1545_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 26c5cc | 700dc6 | Updated the image for [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}.|
|{{site.data.keyword.redhat_openshift_notm}} | 4.6.29 | 4.6.31 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-31){: external}. The update resolves CVE-2021-30465 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6462567){: external}).|
| TCP `keepalive` optimization for VPC | N/A | N/A | Set the `net.ipv4.tcp_keepalive_time` setting to 180 seconds for compatibility with VPC gateways. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates for [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.29_1544_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.29_1544_openshift, released 24 May 2021
{: #4629_1544}

The following table shows the changes that are in the worker node fix pack `4.6.29_1544_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | e0fa2f | 26c5cc | Updated image with fixes for [CVE-2020-26116](https://nvd.nist.gov/vuln/detail/CVE-2020-26116){: external}, [CVE-2020-27619](https://nvd.nist.gov/vuln/detail/CVE-2020-27619){: external}, [CVE-2021-23336](https://nvd.nist.gov/vuln/detail/CVE-2021-23336){: external}, [CVE-2021-3177](https://nvd.nist.gov/vuln/detail/CVE-2021-3177){: external}, [CVE-2019-3842](https://nvd.nist.gov/vuln/detail/CVE-2019-3842){: external}, [CVE-2020-13776](https://nvd.nist.gov/vuln/detail/CVE-2020-13776){: external}, [CVE-2019-18276](https://nvd.nist.gov/vuln/detail/CVE-2019-18276){: external}, [CVE-2020-24977](https://nvd.nist.gov/vuln/detail/CVE-2020-24977){: external}, [CVE-2020-13434](https://nvd.nist.gov/vuln/detail/CVE-2020-13434){: external}, [CVE-2020-15358](https://nvd.nist.gov/vuln/detail/CVE-2020-15358){: external}, [CVE-2019-13012](https://nvd.nist.gov/vuln/detail/CVE-2019-13012){: external}, [CVE-2020-13543](https://nvd.nist.gov/vuln/detail/CVE-2020-13543){: external}, [CVE-2020-13584](https://nvd.nist.gov/vuln/detail/CVE-2020-13584){: external}, [CVE-2020-9948](https://nvd.nist.gov/vuln/detail/CVE-2020-9948){: external}, [CVE-2020-9951](https://nvd.nist.gov/vuln/detail/CVE-2020-9951){: external}, [CVE-2020-9983](https://nvd.nist.gov/vuln/detail/CVE-2020-9983){: external}, [CVE-2020-8231](https://nvd.nist.gov/vuln/detail/CVE-2020-8231){: external}, [CVE-2020-8284](https://nvd.nist.gov/vuln/detail/CVE-2020-8284){: external}, [CVE-2020-8285](https://nvd.nist.gov/vuln/detail/CVE-2020-8285){: external}, [CVE-2020-8286](https://nvd.nist.gov/vuln/detail/CVE-2020-8286){: external}, [CVE-2020-24330](https://nvd.nist.gov/vuln/detail/CVE-2020-24330){: external}, [CVE-2020-24331](https://nvd.nist.gov/vuln/detail/CVE-2020-24331){: external}, [CVE-2020-24332](https://nvd.nist.gov/vuln/detail/CVE-2020-24332){: external}, [CVE-2020-29361](https://nvd.nist.gov/vuln/detail/CVE-2020-29361){: external}, [CVE-2020-29362](https://nvd.nist.gov/vuln/detail/CVE-2020-29362){: external}, [CVE-2020-29363](https://nvd.nist.gov/vuln/detail/CVE-2020-29363){: external}, [CVE-2020-28196](https://nvd.nist.gov/vuln/detail/CVE-2020-28196){: external}, [CVE-2019-2708](https://nvd.nist.gov/vuln/detail/CVE-2019-2708){: external}, [CVE-2016-10228](https://nvd.nist.gov/vuln/detail/CVE-2016-10228){: external}, [CVE-2019-25013](https://nvd.nist.gov/vuln/detail/CVE-2019-25013){: external}, [CVE-2019-9169](https://nvd.nist.gov/vuln/detail/CVE-2019-9169){: external}, [CVE-2020-27618](https://nvd.nist.gov/vuln/detail/CVE-2020-27618){: external}, [CVE-2021-3326](https://nvd.nist.gov/vuln/detail/CVE-2021-3326){: external}, and [CVE-2020-8927](https://nvd.nist.gov/vuln/detail/CVE-2020-8927){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.27 | 4.6.29 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-29){: external}. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.27_1542_openshift" caption-side="top"}


### Changelog for master fix pack 4.6.28_1543_openshift, released 24 May 2021
{: #4628_1543}

The following table shows the changes that are in the master fix pack patch update `4.6.28_1543_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.11 | v1.2.12 | Improved the add-on status information that displays when errors occur. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2020-26160](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-26160){: external}, [CVE-2020-28483](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28483){: external} and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| Gateway-enabled cluster controller | 1322 | 1352 | Updated to use `Go` version 1.15.11. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2021-28831](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-28831){: external}, [CVE-2021-30139](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-30139){: external}, [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 618 | 689 | Updated to use `Go` version 1.15.12. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2020-14391](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14391){: external}, [CVE-2020-25661](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-25661){: external} and [CVE-2020-25662](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-25662){: external}. |
| {{site.data.keyword.blockstoragefull}} driver and plug-in | v2.0.3 | v2.0.4 | Updated image for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
| {{site.data.keyword.IBM_notm}} Cloud Controller Manager | v1.19.10-1 | v1.19.11-3 | Updated to support the Kubernetes 1.19.11 release and to use `Go` version 1.15.12. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 390 | 392 | Improved the pre-requisite validation logic for provisioning persistent volume claims (PVCs). Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305{: external}). |
| {{site.data.keyword.IBM_notm}} Cloud RBAC Operator | b6a694b | 63cd064 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2020-28483](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28483){: external}. |
| Key Management Service provider | v2.3.3 | v2.3.4 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2020-28483](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28483){: external} and [CVE-2020-26160](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-26160){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.IBM_notm}} Cloud Provider | 1274 | 1328 | Updated to use Go version 1.15.11. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2021-28831](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-28831){: external}, [CVE-2021-30139](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-30139){: external}, [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.23 | 4.6.28 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-28){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20210331 | v4.6.0-20210512 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210512){: external}. |
| OpenVPN Operator image | v1.3.0 | v1.3.1 | Updated image for [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| Portieris admission controller | v0.10.1 | v0.10.2 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.10.2){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20210331 | v4.6.0-20210512 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210512){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20210331 | 4.6.0+20210512 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210512){: external}. |
{: caption="Changes since version 4.6.23_1540_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.27_1542_openshift, released 10 May 2021
{: #4627_1542}

The following table shows the changes that are in the worker node fix pack `4.6.27_1542_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.25 | 4.6.27 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-27){: external}.|
| RHEL 7 Packages | 3.10.0-1160.24 | 3.10.0-1160.25 | To increase resiliency, `rsyslog` no longer keeps old file descriptors. Updated worker node images with kernel and package updates for [CVE-2021-25215](https://nvd.nist.gov/vuln/detail/CVE-2021-25215){: external}, [CVE-2020-25692](https://nvd.nist.gov/vuln/detail/CVE-2020-25692){: external}, and [CVE-2020-25648](https://nvd.nist.gov/vuln/detail/CVE-2020-25648){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.25_1541_openshift" caption-side="top"}

### Changelog for master fix pack 4.6.23_1540_openshift, released 27 April 2021
{: #4623_1540}

The following table shows the changes that are in the master fix pack patch update `4.6.23_1540_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.9 | v1.2.11 | Fixed {{site.data.keyword.redhat_openshift_notm}} version check for unsupported add-ons. Updated to use `Go` version 1.15.11. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external}, [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}, and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| Cluster master operations | N/A | N/A | Resolved an {{site.data.keyword.redhat_openshift_notm}} API server target down alert on clusters that are updated from version 4.4 or earlier. Fixed a bug that can cause `ibmcloud oc cluster config` to fail. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.9-1 | v1.19.10-1 | Updated to support the Kubernetes 1.19.10 release and to use `Go` version 1.15.10. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 389 | 390 | Updated to use `Go` version 1.15.9 and for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}, and [CVE-2021-3121](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3121){: external}. |
|{{site.data.keyword.cloud_notm}} RBAC Operator | 3dd6bbc | b6a694b | Updated image for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
| Key Management Service provider | v2.3.0 | v2.3.3 | Updated to use `Go` version 1.15.11 and for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external}, [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}, and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.22 | 4.6.23 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-23){: external}. |
| OpenVPN client | 2.4.6-r3-IKS-301 | 2.4.6-r3-IKS-386 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN Operator image | v1.2.0 | v1.3.0 | Added OpenVPN support to the {{site.data.keyword.redhat_openshift_notm}} API server to support webhooks. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external}, [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}, and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| OpenVPN server | 2.4.6-r3-IKS-301 | 2.4.6-r3-IKS-385 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.22_1538_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.25_1541_openshift, released 26 April 2021
{: #4625_1541}

The following table shows the changes that are in the worker node fix pack `4.6.25_1541_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | a3b1ff | e0fa2f | The update addresses [CVE-2021-20305](https://nvd.nist.gov/vuln/detail/CVE-2021-20305){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.23 | 4.6.25 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-25){: external}.<br><br>Configured worker nodes to integrate with a newer version of the NVIDIA GPU operator. Now when you create an instance of the `ClusterPolicy` for the GPU operator, you must enter `450.80.02` for the **Driver Config** version.|
| RHEL 7 Packages | N/A | N/A | Updated worker node images with package updates for [CVE-2021-20305](https://nvd.nist.gov/vuln/detail/CVE-2021-20305){: external}.  |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.23_1539_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.23_1539_openshift, released 12 April 2021
{: #4623_1539}

The following table shows the changes that are in the worker node fix pack `4.6.23_1539_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 9b2dca | a3b1ff | The update addresses [CVE-2021-3449](https://nvd.nist.gov/vuln/detail/CVE-2021-3449){: external} and [CVE-2021-3450](https://nvd.nist.gov/vuln/detail/CVE-2021-3450){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.22 | 4.6.23 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-23){: external}.|
| RHEL 7 Packages | 3.10.0-1160.21.1.el7 | 3.10.0-1160.24.1.el7 | Updated worker node images with kernel and package updates for [CVE-2021-27363](https://nvd.nist.gov/vuln/detail/CVE-2021-27363){: external}, [CVE-2021-27364](https://nvd.nist.gov/vuln/detail/CVE-2021-27364){: external}, and [CVE-2021-27365](https://nvd.nist.gov/vuln/detail/CVE-2021-27365){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.22_1536_openshift" caption-side="top"}

### Changelog for master fix pack 4.6.22_1538_openshift, released 2 April 2021
{: #4622_1538}

The following table shows the changes that are in the master fix pack patch update `4.6.22_1538_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.0.1 | v2.0.3 | Updated to use `Go` version 1.15.9 and for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20210126 | v4.6.0-20210331 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210331){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.21 | 4.6.22 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-22){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20210126 | v4.6.0-20210331 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210331){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20210126 | 4.6.0+20210331 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210331){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.21_1535_openshift" caption-side="top"}

### Changelog for master fix pack 4.6.21_1535_openshift, released 30 March 2021
{: #4621_1535}

The following table shows the changes that are in the master fix pack patch update `4.6.21_1535_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.at_short}} event | N/A | N/A | Now, the `containers-kubernetes.version.update` event is sent to {{site.data.keyword.at_short}} when a master fix pack update is initiated for a cluster. |
| Cluster health image | v1.2.8 | v1.2.9 | Updated image for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}. |
| Gateway-enabled cluster controller | 1232 | 1322 | Updated to use `Go` version 1.15.10 and for [CVE-2021-23839](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-23839){: external}, [CVE-2021-23840](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-23840){: external}, and [CVE-2021-23841](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-23841){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.8-4 | v1.19.9-1 | Updated to support the Kubernetes 1.19.9 release. Fixed a bug that prevented VPC load balancers from supporting more than 50 subnets in an account. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 388 | 389 | Updated to use `Go` version 1.15.8. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 86de2b7 | 3dd6bbc | Updated image for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.17 | 4.6.21 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-21){: external}. |
| OpenVPN Operator image | v1.1.2 | v1.2.0 | Fixed a bug that could prevent worker node VPN updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.17_1533_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.22_1536_openshift, released 29 March 2021
{: #4622_1536}

The following table shows the changes that are in the worker node fix pack `4.6.22_1536_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.20 | 4.6.22 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-22){: external}.|
| RHEL 7 Packages | 3.10.0-1160.15.2.el7 | 3.10.0-1160.21.1.el7 | Updated worker node images with kernel and package updates for [CVE-2019-19532](https://nvd.nist.gov/vuln/detail/CVE-2019-19532){: external}, [CVE-2020-0427](https://nvd.nist.gov/vuln/detail/CVE-2020-0427){: external}, [CVE-2020-7053](https://nvd.nist.gov/vuln/detail/CVE-2020-7053){: external}, [CVE-2020-14351](https://nvd.nist.gov/vuln/detail/CVE-2020-14351){: external}, [CVE-2020-25211](https://nvd.nist.gov/vuln/detail/CVE-2020-25211){: external}, [CVE-2020-25645](https://nvd.nist.gov/vuln/detail/CVE-2020-25645){: external}, [CVE-2020-25656](https://nvd.nist.gov/vuln/detail/CVE-2020-25656){: external}, [CVE-2020-25705](https://nvd.nist.gov/vuln/detail/CVE-2020-25705){: external}, [CVE-2020-28374](https://nvd.nist.gov/vuln/detail/CVE-2020-28374){: external}, [CVE-2020-29661](https://nvd.nist.gov/vuln/detail/CVE-2020-29661){: external}, and [CVE-2021-20265](https://nvd.nist.gov/vuln/detail/CVE-2021-20265){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.20_1534_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.20_1534_openshift, released 12 March 2021
{: #4620_1534}

The following table shows the changes that are in the worker node fix pack `4.6.20_1534_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.18 | 4.6.20 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-20){: external}.|
| RHEL 7 Packages | N/A | N/A | Updated worker node with package updates for [CVE-2020-8625](https://nvd.nist.gov/vuln/detail/CVE-2020-8625){: external}, [CVE-2020-14372](https://nvd.nist.gov/vuln/detail/CVE-2020-14372){: external}, [CVE-2020-25632](https://nvd.nist.gov/vuln/detail/CVE-2020-25632){: external}, [CVE-2020-25647](https://nvd.nist.gov/vuln/detail/CVE-2020-25647){: external}, [CVE-2020-27749](https://nvd.nist.gov/vuln/detail/CVE-2020-27749){: external}, [CVE-2020-27779](https://nvd.nist.gov/vuln/detail/CVE-2020-27779){: external}, [CVE-2021-20225](https://nvd.nist.gov/vuln/detail/CVE-2021-20225){: external}, [CVE-2021-20233](https://nvd.nist.gov/vuln/detail/CVE-2021-20233){: external}, and [CVE-2021-27803](https://nvd.nist.gov/vuln/detail/CVE-2021-27803){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.18_1533_openshift" caption-side="top"}

### Changelog for worker node fix pack 4.6.18_1533_openshift, released 1 March 2021
{: #4618_1533}

The following table shows the changes that are in the worker node fix pack `4.6.18_1533_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Image garbage collection | N/A | N/A | Fixed a race condition during the provisioning of worker nodes that might cause image garbage collection to fail.  |
| {{site.data.keyword.registrylong_notm}} private endpoints | N/A | N/A | **VPC worker nodes**: Fixed a bug where traffic to the private endpoints of {{site.data.keyword.registrylong_notm}} might fail after rebooting the worker node. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.16 | 4.6.18 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-18){: external}.|
| OpenShift Data Foundation | N/A | N/A | Fixed the worker node configuration to resolve an error with deploying ODF. |
| RHEL 7 Packages | N/A | N/A | Updated worker node with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.16_1529_openshift" caption-side="top"}

### Changelog for master fix pack 4.6.17_1533_openshift, released 27 February 2021
{: #4617_1533}

The following table shows the changes that are in the master fix pack patch update `4.6.17_1533_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.8-1 | v1.19.8-4 | Updated to use `calicoctl` version 3.16.8. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1165 | 1274 | Fixed a bug that might cause version 2.0 network load balancers (NLBs) to crash and restart on load balancer updates. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.16 | 4.6.17 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-17){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.16_1532_openshift" caption-side="top"}

### Changelog for master fix pack 4.6.16_1532_openshift, released 22 February 2021
{: #4616_1532}

The following table shows the changes that are in the master fix pack patch update `4.6.16_1532_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.7-13 | v1.19.8-1 | Updated to support the Kubernetes 1.19.8 release and to use `Go` version 1.15.8. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| Key Management Service provider | v2.2.4 | v2.3.0 | Updated to use `Go` version 1.15.7. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN Operator image | v1.1.0 | v1.1.2 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.16_1530_openshift" caption-side="top"}

### Changelog for 4.6.16_1530_openshift (master) and 4.6.16_1529_openshift (worker node), released 17 February 2020
{: #4616_1530}

The following table shows the changes that are in the version updates for the `4.6.16_1530_openshift` master fix pack and `4.6.16_1529_openshift` worker node fix pack.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Calico | v3.16.5 | v3.17.2 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases){: external}. |
| Calico Operator | v1.10.9 | v1.13.4 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.13.4){: external}. |
| Cluster health image | v1.2.6 | v1.2.8 | Updated to use `Go` version 1.15.7. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| Gateway-enabled cluster controller | 1195 | 1232 | Updated to use `Go` version 1.15.7. |
| {{site.data.keyword.IBM_notm}} Calico extension | 567 | 618 | Updated to use `Go` version 1.15.7. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.18.15-3 | v1.19.7-13 | Updated to support the Kubernetes 1.19.7 release and to use `Go` version 1.15.5 and `calicoctl` version 3.16.7. Classic network load balancers (NLBs) now set the `NET_RAW` security context. Added support for VPC network load balancers. Updated version 1.0 and 2.0 network load balancers (NLBs) to run as a non-root user by default, with privileged escalation as needed. Updated image for [DLA-2509-1](https://www.debian.org/lts/security/2020/dla-2509){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 385 | 388 | Improved the retry logic for provisioning persistent volume claims (PVCs). |
| {{site.data.keyword.cloud_notm}} RBAC Operator | f859228 | 86de2b7 | Updated to use `Go` version 1.15.7. |
| Key Management Service provider | v2.2.3 | v2.2.4 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| {{site.data.keyword.redhat_openshift_notm}} configuration | N/A | N/A | Updated the [feature gate configuration](/docs/openshift?topic=openshift-service-settings#feature-gates). |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1078 | 1165 | Updated to run as a non-root user by default, with privileged escalation as needed. Updated to use `Go` version 1.15.7. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.5.0-20210112 | v4.6.0-20210126 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/v4.6.0+20210126){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.24 (master), 4.5.31 (worker) | 4.6.16 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-16){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.5.0-20210112 | v4.6.0-20210126 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/v4.6.0+20210126){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.5.0+20210112 | 4.6.0+20210126 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210126){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.5.24_1527_openshift (master) and 4.5.31_1529_openshift (worker node)" caption-side="top"}

## Deprecated: Version 3.11 changelog
{: #version-311}

Review the changelogs for {{site.data.keyword.openshiftlong_notm}} version 3.11 patch updates.
{: shortdesc}

![Version 3.11 icon.](images/icon-version-311.png) {{site.data.keyword.redhat_openshift_notm}} version 3.11 is deprecated, and becomes unsupported on 6 June 2022 (date subject to change).
{: deprecated}

### Changelog for master fix pack 3.11.570_1623_openshift, released 3 March 2022
{: #311570_1623}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.30 | v1.1.32 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds fix for [CVE-2021-43565](https://www.whitesourcesoftware.com/vulnerability-database/CVE-2021-43565){: external}. Adds Golang dependency updates. |
| Key Management Service provider | v1.0.22 | v1.0.25 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds fix for [CVE-2021-43565](https://www.whitesourcesoftware.com/vulnerability-database/CVE-2021-43565). Adds Golang dependency updates.  |
| IBM Cloud File Storage plug-in and monitor | 404 | 405 | Adds fix for [CVE-2021-3538](https://vuln.whitesourcesoftware.com/vulnerability/CVE-2021-3538){: external} and adds dependency updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.570_1619_openshift" caption-side="top"}

### Change log for worker node fix pack 3.11.570_1624_openshift, released 28 February 2022
{: #311570_1624}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | 3.10.0-1160.53.1.el7 | 3.10.0-1160.59.1.el7 | Kernel and package updates for [CVE-2020-25709](https://nvd.nist.gov/vuln/detail/CVE-2020-25709){: external}, [CVE-2020-25710](https://nvd.nist.gov/vuln/detail/CVE-2020-25710){: external}, [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}, [CVE-2020-0465](https://nvd.nist.gov/vuln/detail/CVE-2020-0465){: external}, [CVE-2020-0466](https://nvd.nist.gov/vuln/detail/CVE-2020-0466){: external}, [CVE-2021-0920](https://nvd.nist.gov/vuln/detail/CVE-2021-0920){: external}, [CVE-2021-3564](https://nvd.nist.gov/vuln/detail/CVE-2021-3564){: external}, [CVE-2021-3573](https://nvd.nist.gov/vuln/detail/CVE-2021-3573){: external}, [CVE-2021-3752](https://nvd.nist.gov/vuln/detail/CVE-2021-3752){: external}, [CVE-2021-4155](https://nvd.nist.gov/vuln/detail/CVE-2021-4155){: external}, [CVE-2022-0330](https://nvd.nist.gov/vuln/detail/CVE-2022-0330){: external}, [CVE-2022-22942](https://nvd.nist.gov/vuln/detail/CVE-2022-22942){: external}. | 
| HA proxy | f6a2b3 | 15198fb | Contains fixes for [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external} | 
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.570_1621_openshift" caption-side="top"}


### Change log for worker node fix pack 3.11.570_1621_openshift, released 14 February 2022
{: #311570_1621}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A  | N/A  |
|  {{site.data.keyword.redhat_openshift_notm}} | N/A  | N/A  | N/A  |
| Haproxy | d38fa1 | f6a2b3 | [CVE-2021-3521](https://nvd.nist.gov/vuln/detail/CVE-2021-3521){: external}   [CVE-2021-4122](https://nvd.nist.gov/vuln/detail/CVE-2021-4122){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.570_1620_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.570_1620_openshift, released 31 January 2022
{: #311570_1620}

The following table shows the changes that are in the worker node fix pack `3.11.570_1620_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | Updated worker node images with package updates for [CVE-2021-4034](https://nvd.nist.gov/vuln/detail/CVE-2021-4034){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.570_1618_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.570_1619_openshift, released 26 January 2022
{: #311570_1619}

The following table shows the changes that are in the master fix pack patch update `3.11.570_1619_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.29 | v1.1.30 | Updated to use `Go` version `1.17.5`, updated Go dependencies and golangci-lint |
| Key Management Service provider | v1.0.21 | v1.0.22 | Updated `Go` dependencies and golangci-lint |
| Load balancer and load balancer monitor for IBM Cloud Provider | 1660 | 1748 | Updated the Alpine base image to the `3.15` version to resolve CVEs. Updated to use `Go` version `1.17.6`. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane | 3.11.542 | 3.11.570 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-570) |
| OpenVPN client | 2.4.6-r3-IKS-463 | 2.5.4-r0-IKS-556 | Update base image to alpine `3.15` to address CVEs, no longer set the `--compress config` option, updated scripts. |
| OpenVPN server | 2.4.6-r3-IKS-462 | 2.5.4-r0-IKS-555 | Update base image to alpine `3.15` to address CVEs, no longer set the `--compress config` option, updated scripts. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 402 | 404 | Updated universal base image (UBI) to the `8.5-218` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.542_1614_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.570_1618_openshift, released 18 January 2022
{: #311570_1618}

The following table shows the changes that are in the worker node fix pack `3.11.570_1618_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.49.1.el7 | 3.10.0-1160.53.1.el7 | Kernel and package updates for [CVE-2020-25704](https://nvd.nist.gov/vuln/detail/CVE-2020-25704){: external}, [CVE-2020-36322](https://nvd.nist.gov/vuln/detail/CVE-2020-36322){: external}, [CVE-2021-42739](https://nvd.nist.gov/vuln/detail/CVE-2021-42739){: external}, [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.570_1617_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.570_1617_openshift, released 4 January 2022
{: #311570_1617}

The following table shows the changes that are in the worker node fix pack patch update `3.11.570_1617_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 3b8663 | d38fa1 | Contains fixes for [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.570_1616_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.570_1616_openshift, released 20 December 2021
{: #311570_1616_openshift}

The following table shows the changes that are in the worker node fix pack patch update `3.11.570_1616_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.542 | 3.11.570 | See [change logs](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-570){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.542_1612_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.542_1614_openshift, released 7 December 2021
{: #311542_1614}

The following table shows the changes that are in the master fix pack patch update `3.11.542_1614_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.27 | v1.1.29 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| Key Management Service provider | v1.0.19 | v1.0.21 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| Load balancer and load balancer monitor for IBM Cloud Provider | 1589 | 1660 | Updated Alpine base image to the latest `3.14` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 401 | 402 | Updated universal base image (UBI) to the `8.5-204` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.542_1611_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.542_1615_openshift, released 6 December 2021
{: #311542_1615_openshift}

The following table shows the changes that are in the worker node fix pack patch update `3.11.542_1615_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| [{rhel_short}] 7 Packages | 3.10.0-1160.45 | 3.10.0-1160.49 | Updated worker node images and kernel with package updates. Contains fixes for [CVE-2020-36385](https://nvd.nist.gov/vuln/detail/CVE-2020-36385){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-41617](https://nvd.nist.gov/vuln/detail/CVE-2021-41617){: external}, [CVE-2021-20271](https://nvd.nist.gov/vuln/detail/CVE-2021-20271){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.542_1612_openshift" caption-side="top"}


### Changelog for worker node fix pack 3.11.542_1612_openshift, released 22 November 2021
{: #311542_1612_openshift}

The following table shows the changes that are in the worker node fix pack patch update `3.11.542_1612_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Haproxy | 07f1e9e | 3b8663 | Contains fixes for [CVE-2021-20231](https://nvd.nist.gov/vuln/detail/CVE-2021-20231){: external}, [CVE-2021-20232](https://nvd.nist.gov/vuln/detail/CVE-2021-20232){: external}, [CVE-2021-3580](https://nvd.nist.gov/vuln/detail/CVE-2021-3580){: external}, [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946){: external}, [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947){: external}, [CVE-2021-22876](https://nvd.nist.gov/vuln/detail/CVE-2021-22876){: external}, [CVE-2021-22898](https://nvd.nist.gov/vuln/detail/CVE-2021-22898){: external}, [CVE-2021-22925](https://nvd.nist.gov/vuln/detail/CVE-2021-22925){: external}, [CVE-2019-20838](https://nvd.nist.gov/vuln/detail/CVE-2019-20838){: external}, [CVE-2020-14155](https://nvd.nist.gov/vuln/detail/CVE-2020-14155){: external}, [CVE-2018-20673](https://nvd.nist.gov/vuln/detail/CVE-2018-20673){: external}, [CVE-2021-42574](https://nvd.nist.gov/vuln/detail/CVE-2021-42574){: external}, [CVE-2019-17594](https://nvd.nist.gov/vuln/detail/CVE-2019-17594){: external}, [CVE-2019-17595](https://nvd.nist.gov/vuln/detail/CVE-2019-17595){: external}, [CVE-2020-12762](https://nvd.nist.gov/vuln/detail/CVE-2020-12762){: external}, [CVE-2020-16135](https://nvd.nist.gov/vuln/detail/CVE-2020-16135){: external}, [CVE-2021-3445](https://nvd.nist.gov/vuln/detail/CVE-2021-3445){: external}, [CVE-2021-36084](https://nvd.nist.gov/vuln/detail/CVE-2021-36084){: external}, [CVE-2021-36085](https://nvd.nist.gov/vuln/detail/CVE-2021-36085){: external}, [CVE-2021-36086](https://nvd.nist.gov/vuln/detail/CVE-2021-36086){: external}, [CVE-2021-36087](https://nvd.nist.gov/vuln/detail/CVE-2021-36087){: external}, [CVE-2021-20266](https://nvd.nist.gov/vuln/detail/CVE-2021-20266){: external}, [CVE-2019-18218](https://nvd.nist.gov/vuln/detail/CVE-2019-18218){: external}, [CVE-2021-23840](https://nvd.nist.gov/vuln/detail/CVE-2021-23840){: external}, [CVE-2021-23841](https://nvd.nist.gov/vuln/detail/CVE-2021-23841){: external}, [CVE-2021-27645](https://nvd.nist.gov/vuln/detail/CVE-2021-27645){: external}, [CVE-2021-33574](https://nvd.nist.gov/vuln/detail/CVE-2021-33574){: external}, [CVE-2021-35942](https://nvd.nist.gov/vuln/detail/CVE-2021-35942){: external}, [CVE-2021-33560](https://nvd.nist.gov/vuln/detail/CVE-2021-33560){: external}, [CVE-2019-13750](https://nvd.nist.gov/vuln/detail/CVE-2019-13750){: external}, [CVE-2019-13751](https://nvd.nist.gov/vuln/detail/CVE-2019-13751){: external}, [CVE-2019-19603](https://nvd.nist.gov/vuln/detail/CVE-2019-19603){: external}, [CVE-2019-5827](https://nvd.nist.gov/vuln/detail/CVE-2019-5827){: external}, [CVE-2020-13435](https://nvd.nist.gov/vuln/detail/CVE-2020-13435){: external}, [CVE-2020-24370](https://nvd.nist.gov/vuln/detail/CVE-2020-24370){: external}, [CVE-2021-28153](https://nvd.nist.gov/vuln/detail/CVE-2021-28153){: external}, [CVE-2021-3800](https://nvd.nist.gov/vuln/detail/CVE-2021-3800){: external}, [CVE-2021-33928](https://nvd.nist.gov/vuln/detail/CVE-2021-33928){: external}, [CVE-2021-33929](https://nvd.nist.gov/vuln/detail/CVE-2021-33929){: external}, [CVE-2021-33930](https://nvd.nist.gov/vuln/detail/CVE-2021-33930){: external}, [CVE-2021-33938](https://nvd.nist.gov/vuln/detail/CVE-2021-33938){: external}, and[CVE-2021-3200](https://nvd.nist.gov/vuln/detail/CVE-2021-3200){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.542_1610_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.542_1611_openshift, released 17 November 2021
{: #311542_1611}

The following table shows the changes that are in the master fix pack patch update `3.11.542_1611_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.26 | v1.1.27 | Updated `Go` module dependencies and to use `Go` version `1.16.9`.  Updated image for [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946), [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947), [CVE-2021-33928](https://nvd.nist.gov/vuln/detail/CVE-2021-33928), [CVE-2021-33929](https://nvd.nist.gov/vuln/detail/CVE-2021-33929) and [CVE-2021-33930](https://nvd.nist.gov/vuln/detail/CVE-2021-33930). |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.15.12-404 | v1.15.12-407 | Updated image for [DLA-2797-1](https://www.debian.org/lts/security/2021/dla-2797). |
| Key Management Service provider | v1.0.18 | v1.0.19 | Updated `Go` module dependencies and to use `Go` version `1.16.9`.  Updated image for [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946). |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1550 | 1589 | Updated to use `Go` version `1.16.9`. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.524 | 3.11.542 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-542) |
| OpenVPN client | 2.4.6-r3-IKS-386 | 2.4.6-r3-IKS-463 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN server | 2.4.6-r3-IKS-385 | 2.4.6-r3-IKS-462 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.524_1608_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.542_1610_openshift, released 10 November 2021
{: #311542_1610}

The following table shows the changes that are in the worker node fix pack patch update `3.11.542_1610_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages| N/A | N/A | Updated worker node image packages for [CVE-2021-42574](https://nvd.nist.gov/vuln/detail/CVE-2021-42574){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.524 | 3.11.542 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-542){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.524_1609_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.524_1608_openshift, released 29 October 2021
{: #311524_1608}

The following table shows the changes that are in the master fix pack patch update `3.11.524_1608_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.25 | v1.1.26 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs:  [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}, [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}, and [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}.  |
| etcd | v3.3.25 | v3.3.26 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.3.26){: external}. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.filestorage_short}} plug-in and monitor | 400 | 401 | Updated universal base image (UBI) to the latest `8.4-210` version to resolve CVEs. |
| Key Management Service provider | v1.0.17 | v1.0.18 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs:  [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}, [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}, and [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}.  |
| {{site.data.keyword.redhat_openshift_notm}} Container Platform |  3.11.521 | 3.11.524 | See the [{{site.data.keyword.redhat_openshift_notm}} Container Platform release notes.](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-524){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.521_1604_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.524_1609_openshift, released 25 October 2021
{: #311524_1609}

The following table shows the changes that are in the worker node fix pack patch update `3.11.524_1609_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.521 | 3.11.524 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-524){: external}. |
| RHEL 7 Packages | 3.10.0-1160.42.2.el7 | 3.10.0-1160.45.1.el7 | Updated worker node images and kernel with package updates for [CVE-2021-3778](https://nvd.nist.gov/vuln/detail/CVE-2021-3778){: external} and [CVE-2021-3796](https://nvd.nist.gov/vuln/detail/CVE-2021-3796){: external}. |
| Worker-pool taint automation | N/A | N/A | Fixes known issue related to worker-pool taint automation that prevents workers from getting providerID. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.524_1606_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.524_1606_openshift, released 11 October 2021
{: #311524_1606_openshift}

The following table shows the changes that are in the worker node fix pack patch update `3.11.524_1606_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| OpenShift Container Platform node | 3.11.521 | 3.11.524 | See the [OpenShift Container Platform release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-524){: external}. The update resolves CVE-2021-25741 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6515606){: external}). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.521_1605_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.521_1605_openshift, released 27 September 2021
{: #311521_1605}

The following table shows the changes that are in the worker node fix pack patch update `3.11.521_1605_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Disk identification | NA | NA | Enhanced the disk identification logic to handle the case of 2+ partitions. |
| Haproxy | 9c98dc5 | 07f1e9 | Updated image with fixes for [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}, [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}, [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}, [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}, and [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}. |
|OpenShift Container Platform| 3.11.501 | 3.11.521 | See the [OpenShift Container Platform release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-521){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.501_1603_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.521_1604_openshift, released 28 September 2021
{: 311521_1604}

The following table shows the changes that are in the worker node fix pack patch update `3.11.521_1604_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.filestorage_short}} plug-in and monitor | 398 | 400 | Updated to use `Go` version `1.16.7`. Updated universal base image (UBI) to the latest `8.4-208` version to resolve CVEs. |
| Load balancer and load balancer monitor for {{site.data.keyword.IBM_notm}} Cloud Provider | 1510 | 1550 | Updated image for [CVE-2021-3711](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3711) and [CVE-2021-3712](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3712). |
|OpenShift Container Platform| 3.11.487 | 3.11.521 | See the [OpenShift Container Platform release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-521). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.487_1601_openshift" caption-side="top"}


### Changelog for worker node fix pack 3.11.501_1603_openshift, released 13 September 2021
{: #311501_1603}

The following table shows the changes that are in the worker node fix pack patch update `3.11.501_1603_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.36.2.el7 | 3.10.0-1160.42.2.el7 | Updated worker node image with package updates for [CVE-2021-25214](https://nvd.nist.gov/vuln/detail/CVE-2021-25214){: external}, [CVE-2020-27777](https://nvd.nist.gov/vuln/detail/CVE-2020-27777){: external}, [CVE-2021-22555](https://nvd.nist.gov/vuln/detail/CVE-2021-22555){: external}, [CVE-2021-29154](https://nvd.nist.gov/vuln/detail/CVE-2021-29154){: external}, [CVE-2021-29650](https://nvd.nist.gov/vuln/detail/CVE-2021-29650){: external}, [CVE-2021-32399](https://nvd.nist.gov/vuln/detail/CVE-2021-32399){: external}, and [CVE-2021-3715](https://nvd.nist.gov/vuln/detail/CVE-2021-3715){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.501_1602_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.501_1602_openshift, released 30 August 2021
{: #311501_1602}

The following table shows the changes that are in the worker node fix pack patch update `3.11.501_1602_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| OpenShift Container Platform | 3.11.487 |	3.11.501 | See [changelogs](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-501){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.487_1600_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.487_1601_openshift, released 25 August 2021
{: #311487_1601}

The following table shows the changes that are in the master fix pack patch update `3.11.487_1601`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.24 | v1.1.25 | Updated to use `Go` version `1.15.15`. Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. |
| Key Management Service provider | v1.0.16 | v1.0.17 | Updated to use `Go` version `1.15.15`. Updated UBI to the latest `8.4` version to resolve CVEs.|
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1328 | 1510 | Updated image for [CVE-2020-27780](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-27780){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.439 | 3.11.487 | See the [OpenShift Container Platform release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-487){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.465_1599_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.487_1600_openshift, released 16 August 2021
{: #311487_1600}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 68e6b3 | 9c98dc | Updated image with fixes for [CVE-2021-27218](https://nvd.nist.gov/vuln/detail/CVE-2021-27218){: external} |
| RHEL 7 Packages | N/A| N/A| Updated image with fixes for: [CVE-2020-0543](https://nvd.nist.gov/vuln/detail/CVE-2020-0543){: external}, [CVE-2020-0548](https://nvd.nist.gov/vuln/detail/CVE-2020-0548){: external}, [CVE-2020-0549](https://nvd.nist.gov/vuln/detail/CVE-2020-0549){: external}, [CVE-2020-8695](https://nvd.nist.gov/vuln/detail/CVE-2020-8695){: external}, [CVE-2020-8696](https://nvd.nist.gov/vuln/detail/CVE-2020-8696){: external}, [CVE-2020-8698](https://nvd.nist.gov/vuln/detail/CVE-2020-8698){: external}, [CVE-2020-24489](https://nvd.nist.gov/vuln/detail/CVE-2020-24489){: external}, [CVE-2020-24511](https://nvd.nist.gov/vuln/detail/CVE-2020-24511){: external}, and [CVE-2020-24512](https://nvd.nist.gov/vuln/detail/CVE-2020-24512){: external}. |
| OpenShift Container Platform |3.11.465 | 3.11.487 | See the [OpenShift Container Platform release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-487){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.465_1599_openshift" caption-side="top"}



### Changelog for worker node fix pack 3.11.465_1599_openshift, released 02 August 2021
{: #311465_1599}

The following table shows the changes that are in the worker node fix pack patch update `3.11.465_1599_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | aae810 | 68e6b3 | Updated image with fixes for [CVE-2021-33910](https://nvd.nist.gov/vuln/detail/CVE-2021-33910){: external}. |
| Registry endpoints | Added zonal public registry endpoints for clusters with both private and public service endpoints enabled. |
| Read only disk self healing | For VPC Gen2 workers. Added automation to recover from disks going read only. |
| RHEL 7 Packages | 3.10.0-1160.31.1 | 3.10.0-1160.36.2 | Updated worker node images & Kernel with package updates: [CVE-2019-20934](https://nvd.nist.gov/vuln/detail/CVE-2019-20934){: external}, [CVE-2020-11668](https://nvd.nist.gov/vuln/detail/CVE-2020-11668){: external}, [CVE-2021-33033](https://nvd.nist.gov/vuln/detail/CVE-2021-33033){: external}, [CVE-2021-33034](https://nvd.nist.gov/vuln/detail/CVE-2021-33034){: external}, [CVE-2021-33909](https://nvd.nist.gov/vuln/detail/CVE-2021-33909){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.465_1596_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.439_1598_openshift, released 27 July 2021
{: #311439_1598}

The following table shows the changes that are in the master fix pack patch update `311.439_1598_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.23 | v1.1.24 | Updated universal base image (UBI) to the latest version to resolve CVEs. |
| Key Management Service provider | v1.0.15 | v1.0.16 | Updated universal base image (UBI) to the latest version to resolve CVEs. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 394 | 395 | Updated universal base image (UBI) to version `8.4-205` to resolve CVEs. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.439_1594_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.465_1596_openshift, released 19 July 2021
{: #311465_1596}

The following table shows the changes that are in the worker node fix pack `3.11.465_1596_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.462 | 3.11.465 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-465){: external}. |
| RHEL 7 Packages| N/A | N/A | Updated worker node image with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.462_1595_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.462_1595_openshift, released 6 July 2021
{: #311462_1595}

The following table shows the changes that are in the worker node fix pack `3.11.462_1595_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 700dc6 | aae810 | Updated image with fixes for [CVE-2021-3520](https://nvd.nist.gov/vuln/detail/CVE-2021-3520){: external}, [CVE-2021-20271](https://nvd.nist.gov/vuln/detail/CVE-2021-20271){: external}, [CVE-2021-3516](https://nvd.nist.gov/vuln/detail/CVE-2021-3516){: external}, [CVE-2021-3517](https://nvd.nist.gov/vuln/detail/CVE-2021-3517){: external}, [CVE-2021-3518](https://nvd.nist.gov/vuln/detail/CVE-2021-3518){: external}, [CVE-2021-3537](https://nvd.nist.gov/vuln/detail/CVE-2021-3537){: external}, and [CVE-2021-3541](https://nvd.nist.gov/vuln/detail/CVE-2021-3541). |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.452 | 3.11.462 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-462){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.452_1593_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.439_1594_openshift, released 28 June 2021
{: #311439_1594}

The following table shows the changes that are in the master fix pack patch update `3.11.439_1594_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.22 | v1.1.23 | Updated to use `Go` version `1.15.12`. Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 392 | 394 | Updated to use `Go` version `1.15.12`. Updated universal base image (UBI) to version `8.4` to resolve CVEs. |
| Key Management Service provider | v1.0.14 | v1.0.15 | Updated to use `Go` version `1.15.12`. Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.420 | 3.11.439 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-439){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.420_1590_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.452_1593_openshift, released 22 June 2021
{: #311452_1593}

The following table shows the changes that are in the worker node fix pack `3.11.452_1593_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 26c5cc | d3dc33 | Updated image with fixes for [CVE-2020-24977](https://nvd.nist.gov/vuln/detail/CVE-2020-24977){: external}, [CVE-2020-13434](https://nvd.nist.gov/vuln/detail/CVE-2020-13434){: external}, [CVE-2020-15358](https://nvd.nist.gov/vuln/detail/CVE-2020-15358){: external}, [CVE-2020-29361](https://nvd.nist.gov/vuln/detail/CVE-2020-29361){: external}, [CVE-2020-29362](https://nvd.nist.gov/vuln/detail/CVE-2020-29362){: external}, [CVE-2020-29363](https://nvd.nist.gov/vuln/detail/CVE-2020-29363){: external}, [CVE-2019-2708](https://nvd.nist.gov/vuln/detail/CVE-2019-2708){: external}, [CVE-2019-13012](https://nvd.nist.gov/vuln/detail/CVE-2019-13012){: external}, [CVE-2020-13543](https://nvd.nist.gov/vuln/detail/CVE-2020-13543){: external}, [CVE-2020-13584](https://nvd.nist.gov/vuln/detail/CVE-2020-13584){: external}, [CVE-2020-9948](https://nvd.nist.gov/vuln/detail/CVE-2020-9948){: external}, [CVE-2020-9951](https://nvd.nist.gov/vuln/detail/CVE-2020-9951){: external}, [CVE-2020-9983](https://nvd.nist.gov/vuln/detail/CVE-2020-9983){: external}, [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}, [CVE-2020-8231](https://nvd.nist.gov/vuln/detail/CVE-2020-8231){: external}, [CVE-2020-8284](https://nvd.nist.gov/vuln/detail/CVE-2020-8284){: external}, [CVE-2020-8285](https://nvd.nist.gov/vuln/detail/CVE-2020-8285){: external}, [CVE-2020-8286](https://nvd.nist.gov/vuln/detail/CVE-2020-8286){: external}, [CVE-2016-10228](https://nvd.nist.gov/vuln/detail/CVE-2016-10228){: external}, [CVE-2019-25013](https://nvd.nist.gov/vuln/detail/CVE-2019-25013){: external}, [CVE-2019-9169](https://nvd.nist.gov/vuln/detail/CVE-2019-9169){: external}, [CVE-2020-27618](https://nvd.nist.gov/vuln/detail/CVE-2020-27618){: external}, [CVE-2021-3326](https://nvd.nist.gov/vuln/detail/CVE-2021-3326){: external}, [CVE-2020-26116](https://nvd.nist.gov/vuln/detail/CVE-2020-26116){: external}, [CVE-2020-27619](https://nvd.nist.gov/vuln/detail/CVE-2020-27619){: external}, [CVE-2021-23336](https://nvd.nist.gov/vuln/detail/CVE-2021-23336){: external}, [CVE-2021-3177](https://nvd.nist.gov/vuln/detail/CVE-2021-3177){: external}, [CVE-2019-3842](https://nvd.nist.gov/vuln/detail/CVE-2019-3842){: external}, [CVE-2020-13776](https://nvd.nist.gov/vuln/detail/CVE-2020-13776){: external}, [CVE-2020-24330](https://nvd.nist.gov/vuln/detail/CVE-2020-24330){: external}, [CVE-2020-24331](https://nvd.nist.gov/vuln/detail/CVE-2020-24331){: external}, [CVE-2020-24332](https://nvd.nist.gov/vuln/detail/CVE-2020-24332){: external}, [CVE-2017-14502](https://nvd.nist.gov/vuln/detail/CVE-2017-14502){: external}, [CVE-2020-8927](https://nvd.nist.gov/vuln/detail/CVE-2020-8927){: external} and [CVE-2020-28196](https://nvd.nist.gov/vuln/detail/CVE-2020-28196){: external}. |
| {{site.data.keyword.registrylong_notm}} | N/A | N/A | Added private-only registry support for `ca.icr.io`, `br.icr.io` and `jp2.icr.io`. | 
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.439 | 3.11.452 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-452){: external}.| 
| RHEL 7 Packages | 3.10.0-1160.25 | 3.10.0-1160.31 | Updated worker node image with kernel package updates for [CVE-2020-8648](https://nvd.nist.gov/vuln/detail/CVE-2020-8648){: external}, [CVE-2020-12362](https://nvd.nist.gov/vuln/detail/CVE-2020-12362)[CVE-2020-12363](https://nvd.nist.gov/vuln/detail/CVE-2020-12363)[CVE-2020-12364](https://nvd.nist.gov/vuln/detail/CVE-2020-12364)[CVE-2020-27170](https://nvd.nist.gov/vuln/detail/CVE-2020-27170)[CVE-2021-3347](https://nvd.nist.gov/vuln/detail/CVE-2021-3347){: external}, [CVE-2020-24489](https://nvd.nist.gov/vuln/detail/CVE-2020-24489){: external}, [CVE-2020-24511](https://nvd.nist.gov/vuln/detail/CVE-2020-24511)[CVE-2020-24512](https://nvd.nist.gov/vuln/detail/CVE-2020-24512){: external}, [CVE-2020-24513](https://nvd.nist.gov/vuln/detail/CVE-2020-24513){: external} and [CVE-2021-25217](https://nvd.nist.gov/vuln/detail/CVE-2021-25217){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.439_1592_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.439_1592_openshift, released 7 June 2021
{: #311439_1592}

The following table shows the changes that are in the worker node fix pack `3.11.439_1592_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 26c5cc | 700dc6 | Updated the image for [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}.|
| TCP `keepalive` optimization for VPC | N/A | N/A | Set the `net.ipv4.tcp_keepalive_time` setting to 180 seconds for compatibility with VPC gateways. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates for [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.439_1591_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.439_1591_openshift, released 24 May 2021
{: #311439_1591}

The following table shows the changes that are in the worker node fix pack `3.11.439_1591_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | e0fa2f | 26c5cc | Updated image with fixes for [CVE-2020-26116](https://nvd.nist.gov/vuln/detail/CVE-2020-26116){: external}, [CVE-2020-27619](https://nvd.nist.gov/vuln/detail/CVE-2020-27619){: external}, [CVE-2021-23336](https://nvd.nist.gov/vuln/detail/CVE-2021-23336){: external}, [CVE-2021-3177](https://nvd.nist.gov/vuln/detail/CVE-2021-3177){: external}, [CVE-2019-3842](https://nvd.nist.gov/vuln/detail/CVE-2019-3842){: external}, [CVE-2020-13776](https://nvd.nist.gov/vuln/detail/CVE-2020-13776){: external}, [CVE-2019-18276](https://nvd.nist.gov/vuln/detail/CVE-2019-18276){: external}, [CVE-2020-24977](https://nvd.nist.gov/vuln/detail/CVE-2020-24977){: external}, [CVE-2020-13434](https://nvd.nist.gov/vuln/detail/CVE-2020-13434){: external}, [CVE-2020-15358](https://nvd.nist.gov/vuln/detail/CVE-2020-15358){: external}, [CVE-2019-13012](https://nvd.nist.gov/vuln/detail/CVE-2019-13012){: external}, [CVE-2020-13543](https://nvd.nist.gov/vuln/detail/CVE-2020-13543){: external}, [CVE-2020-13584](https://nvd.nist.gov/vuln/detail/CVE-2020-13584){: external}, [CVE-2020-9948](https://nvd.nist.gov/vuln/detail/CVE-2020-9948){: external}, [CVE-2020-9951](https://nvd.nist.gov/vuln/detail/CVE-2020-9951){: external}, [CVE-2020-9983](https://nvd.nist.gov/vuln/detail/CVE-2020-9983){: external}, [CVE-2020-8231](https://nvd.nist.gov/vuln/detail/CVE-2020-8231){: external}, [CVE-2020-8284](https://nvd.nist.gov/vuln/detail/CVE-2020-8284){: external}, [CVE-2020-8285](https://nvd.nist.gov/vuln/detail/CVE-2020-8285){: external}, [CVE-2020-8286](https://nvd.nist.gov/vuln/detail/CVE-2020-8286){: external}, [CVE-2020-24330](https://nvd.nist.gov/vuln/detail/CVE-2020-24330){: external}, [CVE-2020-24331](https://nvd.nist.gov/vuln/detail/CVE-2020-24331){: external}, [CVE-2020-24332](https://nvd.nist.gov/vuln/detail/CVE-2020-24332){: external}, [CVE-2020-29361](https://nvd.nist.gov/vuln/detail/CVE-2020-29361){: external}, [CVE-2020-29362](https://nvd.nist.gov/vuln/detail/CVE-2020-29362){: external}, [CVE-2020-29363](https://nvd.nist.gov/vuln/detail/CVE-2020-29363){: external}, [CVE-2020-28196](https://nvd.nist.gov/vuln/detail/CVE-2020-28196){: external}, [CVE-2019-2708](https://nvd.nist.gov/vuln/detail/CVE-2019-2708){: external}, [CVE-2016-10228](https://nvd.nist.gov/vuln/detail/CVE-2016-10228){: external}, [CVE-2019-25013](https://nvd.nist.gov/vuln/detail/CVE-2019-25013){: external}, [CVE-2019-9169](https://nvd.nist.gov/vuln/detail/CVE-2019-9169){: external}, [CVE-2020-27618](https://nvd.nist.gov/vuln/detail/CVE-2020-27618){: external}, [CVE-2021-3326](https://nvd.nist.gov/vuln/detail/CVE-2021-3326){: external}, and [CVE-2020-8927](https://nvd.nist.gov/vuln/detail/CVE-2020-8927){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.420 | 3.11.439 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-439){: external}. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.420_1588_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.420_1590_openshift, released 24 May 2021
{: #311420_1590}

The following table shows the changes that are in the master fix pack patch update `3.11.420_1590_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.21 | v1.1.22 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2020-26160](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-26160){: external}, [CVE-2020-28483](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28483){: external} and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| {{site.keyword.data.filestorage_full_notm}} plug-in and monitor | 390 | 392 | Improved the pre-requisite validation logic for provisioning persistent volume claims (PVCs). Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| Key Management Service provider | v1.0.12 | v1.0.14 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2020-26160](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-26160){: external} and [CVE-2020-28483](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28483){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.IBM_notm}} Cloud Provider | 1274 | 1328 | Updated to use Go version 1.15.11. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2021-28831](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-28831){: external}, [CVE-2021-30139](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-30139){: external}, [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
{: caption="Changes since version 3.11.420_1586_openshift" caption-side="top"}


### Changelog for worker node fix pack 3.11.420_1588_openshift, released 10 May 2021
{: #311420_1588}

The following table shows the changes that are in the worker node fix pack `3.11.420_1588_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | 3.10.0-1160.24 | 3.10.0-1160.25 | To increase resiliency, `rsyslog` no longer keeps old file descriptors. Updated worker node images with kernel and package updates for [CVE-2021-25215](https://nvd.nist.gov/vuln/detail/CVE-2021-25215){: external}, [CVE-2020-25692](https://nvd.nist.gov/vuln/detail/CVE-2020-25692){: external}, and [CVE-2020-25648](https://nvd.nist.gov/vuln/detail/CVE-2020-25648){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.420_1587_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.420_1586_openshift, released 27 April 2021
{: #311420_1586}

The following table shows the changes that are in the master fix pack patch update `3.11.420_1586_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.19 | v1.1.21 | Updated to use `Go` version 1.15.11. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external}, [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}, and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 389 | 390 | Updated to use `Go` version 1.15.9 and for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external} and [CVE-2021-3121](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3121){: external}. |
| Key Management Service provider | v1.0.10 | v1.0.12 | Updated to use `Go` version 1.15.11 and for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external}, [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}, and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.394 | 3.11.420 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-420){: external}. |
| OpenVPN client | 2.4.6-r3-IKS-301 | 2.4.6-r3-IKS-386 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN server | 2.4.6-r3-IKS-301 | 2.4.6-r3-IKS-385 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.394_1583_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.420_1587_openshift, released 26 April 2021
{: #311420_1587}

The following table shows the changes that are in the worker node fix pack `3.11.420_1587_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | a3b1ff | e0fa2f | The update addresses [CVE-2021-20305](https://nvd.nist.gov/vuln/detail/CVE-2021-20305){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.404 | 3.11.420 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-420){: external}. |
| RHEL 7 Packages | N/A | N/A | Updated worker node images with package updates for [CVE-2021-20305](https://nvd.nist.gov/vuln/detail/CVE-2021-20305){: external}.  |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.404_1585_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.404_1585_openshift, released 12 April 2021
{: #311404_1585}

The following table shows the changes that are in the worker node fix pack `3.11.404_1585_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 9b2dca | a3b1ff | The update addresses [CVE-2021-3449](https://nvd.nist.gov/vuln/detail/CVE-2021-3449){: external} and [CVE-2021-3450](https://nvd.nist.gov/vuln/detail/CVE-2021-3450){: external}. |
| RHEL 7 Packages | 3.10.0-1160.21.1.el7 | 3.10.0-1160.24.1.el7 | Updated worker node images with kernel and package updates for [CVE-2021-27363](https://nvd.nist.gov/vuln/detail/CVE-2021-27363){: external}, [CVE-2021-27364](https://nvd.nist.gov/vuln/detail/CVE-2021-27364){: external}, and [CVE-2021-27365](https://nvd.nist.gov/vuln/detail/CVE-2021-27365){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.404_1584_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.394_1583_openshift, released 30 March 2021
{: #311394_1583}

The following table shows the changes that are in the master fix pack patch update `3.11.394_1583_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.at_short}} event | N/A | N/A | Now, the `containers-kubernetes.version.update` event is sent to {{site.data.keyword.at_short}} when a master fix pack update is initiated for a cluster. |
| Cluster health image | v1.1.18 | v1.1.19 | Updated image for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 388 | 389 | Updated to use `Go` version 1.15.8. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1165 | 1274 | Fixed a bug that might cause version 2.0 network load balancers (NLBs) to crash and restart on load balancer updates. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.380 | 3.11.394 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-394){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.380_1581_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.404_1584_openshift, released 29 March 2021
{: #311404_1584}

The following table shows the changes that are in the worker node fix pack `3.11.404_1584_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} node |     3.11.394 | 3.11.404 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-404){: external}.|
| RHEL 7 Packages | 3.10.0-1160.15.2.el7 | 3.10.0-1160.21.1.el7 | Updated worker node images with kernel and package updates for [CVE-2019-19532](https://nvd.nist.gov/vuln/detail/CVE-2019-19532){: external}, [CVE-2020-0427](https://nvd.nist.gov/vuln/detail/CVE-2020-0427){: external}, [CVE-2020-7053](https://nvd.nist.gov/vuln/detail/CVE-2020-7053){: external}, [CVE-2020-14351](https://nvd.nist.gov/vuln/detail/CVE-2020-14351){: external}, [CVE-2020-25211](https://nvd.nist.gov/vuln/detail/CVE-2020-25211){: external}, [CVE-2020-25645](https://nvd.nist.gov/vuln/detail/CVE-2020-25645){: external}, [CVE-2020-25656](https://nvd.nist.gov/vuln/detail/CVE-2020-25656){: external}, [CVE-2020-25705](https://nvd.nist.gov/vuln/detail/CVE-2020-25705){: external}, [CVE-2020-28374](https://nvd.nist.gov/vuln/detail/CVE-2020-28374){: external}, [CVE-2020-29661](https://nvd.nist.gov/vuln/detail/CVE-2020-29661){: external}, and [CVE-2021-20265](https://nvd.nist.gov/vuln/detail/CVE-2021-20265){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.394_1582_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.394_1582_openshift, released 12 March 2021
{: #311394_1582}

The following table shows the changes that are in the worker node fix pack `3.11.394_1582_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} node |     3.11.380 | 3.11.394 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-394){: external}.|
| RHEL 7 Packages | N/A | N/A | Updated worker node with package updates for [CVE-2020-8625](https://nvd.nist.gov/vuln/detail/CVE-2020-8625){: external}, [CVE-2020-14372](https://nvd.nist.gov/vuln/detail/CVE-2020-14372){: external}, [CVE-2020-25632](https://nvd.nist.gov/vuln/detail/CVE-2020-25632){: external}, [CVE-2020-25647](https://nvd.nist.gov/vuln/detail/CVE-2020-25647){: external}, [CVE-2020-27749](https://nvd.nist.gov/vuln/detail/CVE-2020-27749){: external}, [CVE-2020-27779](https://nvd.nist.gov/vuln/detail/CVE-2020-27779){: external}, [CVE-2021-20225](https://nvd.nist.gov/vuln/detail/CVE-2021-20225){: external}, [CVE-2021-20233](https://nvd.nist.gov/vuln/detail/CVE-2021-20233){: external}, and [CVE-2021-27803](https://nvd.nist.gov/vuln/detail/CVE-2021-27803){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.380_1581_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.380_1581_openshift, released 1 March 2021
{: #311380_1581_worker}

The following table shows the changes that are in the worker node fix pack `3.11.380_1581_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | Updated worker node with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.380_1580_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.380_1581_openshift, released 22 February 2021
{: #311380_1581}

The following table shows the changes that are in the master fix pack patch update `3.11.380_1581_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.16 | v1.1.18 | Updated to use `Go` version 1.15.7. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 385 | 388 | Improved the retry logic for provisioning persistent volume claims (PVCs). |
| Key Management Service provider | v1.0.7 | v1.0.10 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external} and [CVE-2020-24659](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24659){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1078 | 1165 | Updated to use `Go` version 1.15.7. |
| {{site.data.keyword.redhat_openshift_notm}}  | 3.11.346 | 3.11.380 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-380){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.346_1578_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.380_1580_openshift, released 15 February 2021
{: #311380_1580}

The following table shows the changes that are in the worker node fix pack `3.11.380_1580_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.374 | 3.11.380 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-380){: external}. |
| RHEL 7 Packages | 3.10.0-1160.11.1.el7 | 3.10.0-1160.15.2.el7 | Updated worker node with image kernel and package updates for: [CVE-2020-10543](https://nvd.nist.gov/vuln/detail/CVE-2020-10543){: external}, [CVE-2020-10878](https://nvd.nist.gov/vuln/detail/CVE-2020-10878){: external}, [CVE-2020-12723](https://nvd.nist.gov/vuln/detail/CVE-2020-12723){: external}, [CVE-2020-15436](https://nvd.nist.gov/vuln/detail/CVE-2020-15436){: external}, [CVE-2020-35513](https://nvd.nist.gov/vuln/detail/CVE-2020-35513){: external}, [CVE-2019-25013](https://nvd.nist.gov/vuln/detail/CVE-2019-25013){: external}, [CVE-2020-10029](https://nvd.nist.gov/vuln/detail/CVE-2020-10029){: external}, [CVE-2020-29573](https://nvd.nist.gov/vuln/detail/CVE-2020-29573){: external}, and [CVE-2020-12321](https://nvd.nist.gov/vuln/detail/CVE-2020-12321)){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.374_1579_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.374_1579_openshift, released 1 February 2021
{: #311347_1579}

The following table shows the changes that are in the worker node fix pack `3.11.374_1579_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.346 | 3.11.374 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-374){: external}. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates for [CVE-2021-3156](https://nvd.nist.gov/vuln/detail/CVE-2021-3156){: external}, [CVE-2020-25684](https://nvd.nist.gov/vuln/detail/CVE-2020-25684){: external}, [CVE-2020-25685](https://nvd.nist.gov/vuln/detail/CVE-2020-25685){: external}, and [CVE-2020-25686](https://nvd.nist.gov/vuln/detail/CVE-2020-25686){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.346_1578_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.346_1578_openshift, released 19 January 2021
{: #311346_1578_master}

The following table shows the changes that are in the master fix pack patch update `3.11.346_1578_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.13 | v1.1.16 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 384 | 385 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external} and [CVE-2020-24659](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24659){: external}. |
| Key Management Service provider | v1.0.5 | v1.0.7 | Fixed bug to ignore conflict errors during KMS secret reencryption. Updated to use `Go` version 1.15.5. Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1004 | 1078 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.346_1577_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.346_1578_openshift, released 18 January 2021
{: #311346_1578}

The following table shows the changes that are in the worker node fix pack `3.11.346_1578_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.346_1576_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.346_1577_openshift, released 6 January 2021
{: #311346_1577}

The following table shows the changes that are in the master fix pack patch update `3.11.346_1577_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.filestorage_full_notm}} plug-in | N/A | N/A | Updated to run as a root user. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.318 | 3.11.346 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-346){: external}. The update resolves CVE-2018-1002102 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6404300){: external}) and CVE-2020-8559 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6404296){: external}). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.318_1575_openshift" caption-side="top"}
### Changelog for worker node fix pack 3.11.346_1576_openshift, released 21 December 2020
{: #311346_1576_master}

The following table shows the changes that are in the worker node fix pack update `3.11.346_1576_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HAProxy | db4e6d | 9b2dca | Image update for [CVE-2020-1971](https://nvd.nist.gov/vuln/detail/CVE-2020-1971){: external} and [CVE-2020-24659](https://nvd.nist.gov/vuln/detail/CVE-2020-24659){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.318 | 3.11.346 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-346). |
| RHEL 7 Packages | 3.10.0-1160.6.1.el7 | 3.10.0-1160.11.1.el7 | Updated worker node image with kernel and package updates for: [CVE-2019-18282](https://nvd.nist.gov/vuln/detail/CVE-2019-18282){: external}, [CVE-2020-10769](https://nvd.nist.gov/vuln/detail/CVE-2020-10769){: external}, [CVE-2020-14314](https://nvd.nist.gov/vuln/detail/CVE-2020-14314){: external}, [CVE-2020-14385](https://nvd.nist.gov/vuln/detail/CVE-2020-14385){: external}, [CVE-2020-24394](https://nvd.nist.gov/vuln/detail/CVE-2020-24394){: external}, [CVE-2020-25212](https://nvd.nist.gov/vuln/detail/CVE-2020-25212){: external}, [CVE-2020-25643](https://nvd.nist.gov/vuln/detail/CVE-2020-25643){: external}, and [CVE-2020-1971](https://nvd.nist.gov/vuln/detail/CVE-2020-1971){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.318_1575_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.318_1575_openshift, released 14 December 2020
{: #311306_1573_master}

The following table shows the changes that are in the master fix pack patch update `3.11.318_1575_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 379 | 384 | Updated to use `Go` version 1.15.5. Updated image to run as a non-root user and to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| Key management service (KMS) provider | v1.0.4 | v1.0.5 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 203 | 1004 | Updated Alpine base image to version 3.12 and to use `Go` version 1.15.5. Updated image for [CVE-2020-8037](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8037){: external} and [CVE-2020-28928](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28928){: external}. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.306 | 3.11.318 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-318){: external}. |
| OpenVPN client | 2.4.6-r3-IKS-116 | 2.4.6-r3-IKS-301 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN server | 2.4.6-r3-IKS-131 | 2.4.6-r3-IKS-301 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.306_1573_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.318_1574_openshift, released 7 December 2020
{: #311318_1574}

The following table shows the changes that are in the worker node fix pack update `3.11.318_1574_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HAProxy | 1.8.26-384f42 | db4e6d | Added provenance labels for source tracking. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.318_1573_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.318_1573_openshift, released 23 November 2020
{: #311318_1573}

The following table shows the changes that are in the worker node fix pack update `3.11.318_1573_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.306 | 3.11.318 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-318){: external}. |
| RHEL 7 Packages |  3.10.0-1160.2.2.el7 | 3.10.0-1160.6.1.el7 | Updated worker node image with kernel and package updates for [CVE-2020-8622](https://nvd.nist.gov/vuln/detail/CVE-2020-8622){: external}, [CVE-2020-8623](https://nvd.nist.gov/vuln/detail/CVE-2020-8623){: external}, [CVE-2020-8624](https://nvd.nist.gov/vuln/detail/CVE-2020-8624){: external}, [CVE-2019-20907](https://nvd.nist.gov/vuln/detail/CVE-2019-20907){: external}, [CVE-2020-15999](https://nvd.nist.gov/vuln/detail/CVE-2020-15999){: external}, [CVE-2020-8177](https://nvd.nist.gov/vuln/detail/CVE-2020-8177){: external}, [CVE-2019-20811](https://nvd.nist.gov/vuln/detail/CVE-2019-20811){: external}, [CVE-2020-14331](https://nvd.nist.gov/vuln/detail/CVE-2020-14331){: external}, [CVE-2020-8695](https://nvd.nist.gov/vuln/detail/CVE-2020-8695){: external}, [CVE-2020-8696](https://nvd.nist.gov/vuln/detail/CVE-2020-8696){: external}, and [CVE-2020-8698](https://nvd.nist.gov/vuln/detail/CVE-2020-8698){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.306_1572_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.306_1573_openshift, released 16 November 2020
{: #311306_1573}

The following table shows the changes that are in the master fix pack patch update `3.11.306_1573_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster health image | v1.1.12 | v1.1.13 | Updated image for [DLA-2424-1](https://www.debian.org/lts/security/2020/dla-2424){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.15.12-343 | v1.15.12-404 | Updated image for [DLA-2424-1](https://www.debian.org/lts/security/2020/dla-2424){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 378 | 379 | Updated to use the universal base image (UBI) and to use `Go` version 1.15.2. |
| Key Management Service provider | v1.0.3 | v1.0.4 | Updated image for [DLA-2424-1](https://www.debian.org/lts/security/2020/dla-2424){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.286 | 3.11.306 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-306){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.286_1570_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.306_1572_openshift, released 9 November 2020
{: #311306_1572}

The following table shows the changes that are in the worker node fix pack update `3.11.306_1572_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates for [CVE-2020-15999](https://nvd.nist.gov/vuln/detail/CVE-2020-15999){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.306_1571_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.306_1571_openshift, released 26 October 2020
{: #311306_1571}

The following table shows the changes that are in the worker node fix pack update `3.11.306_1571_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.286 | 3.11.306 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-306){: external}.|
| RHEL 7 Packages | 3.10.0-1160.2.1.el7 | 3.10.0-1160.2.2.el7 | Updated worker node images with kernel and package updates for [CVE-2020-12351](https://nvd.nist.gov/vuln/detail/CVE-2020-12351){: external} and [CVE-2020-12352](https://nvd.nist.gov/vuln/detail/CVE-2020-12352){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.286_1570_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.286_1571_openshift, released 26 October 2020
{: #311286_1571}

The following table shows the changes that are in the master fix pack patch update `3.11.286_1571_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster health image | v1.1.11 | v1.1.12 | Updated to use `Go` version 1.15.2. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.272 | 3.11.286 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-286){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.272_1567_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.286_1570_openshift, released 12 October 2020
{: #311286_1570}

The following table shows the changes that are in the worker node fix pack update `3.11.286_1570_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1127.19.1.el7 | 3.10.0-1160.2.1.el7 | Updated worker node image with kernel and package updates for: [CVE-2019-12450](https://nvd.nist.gov/vuln/detail/CVE-2019-12450){: external}, [CVE-2019-14822](https://nvd.nist.gov/vuln/detail/CVE-2019-14822){: external}, [CVE-2020-12243](https://nvd.nist.gov/vuln/detail/CVE-2020-12243){: external}, [CVE-2019-14866](https://nvd.nist.gov/vuln/detail/CVE-2019-14866){: external}, [CVE-2017-12652](https://nvd.nist.gov/vuln/detail/CVE-2017-12652){: external}, [CVE-2017-18551](https://nvd.nist.gov/vuln/detail/CVE-2017-18551){: external}, [CVE-2018-20836](https://nvd.nist.gov/vuln/detail/CVE-2018-20836){: external}, [CVE-2019-9454](https://nvd.nist.gov/vuln/detail/CVE-2019-9454){: external}, [CVE-2019-9458](https://nvd.nist.gov/vuln/detail/CVE-2019-9458){: external}, [CVE-2019-12614](https://nvd.nist.gov/vuln/detail/CVE-2019-12614){: external}, [CVE-2019-15217](https://nvd.nist.gov/vuln/detail/CVE-2019-15217){: external}, [CVE-2019-15807](https://nvd.nist.gov/vuln/detail/CVE-2019-15807){: external}, [CVE-2019-15917](https://nvd.nist.gov/vuln/detail/CVE-2019-15917){: external}, [CVE-2019-16231](https://nvd.nist.gov/vuln/detail/CVE-2019-16231){: external}, [CVE-2019-16233](https://nvd.nist.gov/vuln/detail/CVE-2019-16233){: external}, [CVE-2019-16994](https://nvd.nist.gov/vuln/detail/CVE-2019-16994){: external}, [CVE-2019-17053](https://nvd.nist.gov/vuln/detail/CVE-2019-17053){: external}, [CVE-2019-17055](https://nvd.nist.gov/vuln/detail/CVE-2019-17055){: external}, [CVE-2019-18808](https://nvd.nist.gov/vuln/detail/CVE-2019-18808){: external}, [CVE-2019-19046](https://nvd.nist.gov/vuln/detail/CVE-2019-19046){: external}, [CVE-2019-19055](https://nvd.nist.gov/vuln/detail/CVE-2019-19055){: external}, [CVE-2019-19058](https://nvd.nist.gov/vuln/detail/CVE-2019-19058){: external}, [CVE-2019-19059](https://nvd.nist.gov/vuln/detail/CVE-2019-19059){: external}, [CVE-2019-19062](https://nvd.nist.gov/vuln/detail/CVE-2019-19062){: external}, [CVE-2019-19063](https://nvd.nist.gov/vuln/detail/CVE-2019-19063){: external}, [CVE-2019-19332](https://nvd.nist.gov/vuln/detail/CVE-2019-19332){: external}, [CVE-2019-19447](https://nvd.nist.gov/vuln/detail/CVE-2019-19447){: external}, [CVE-2019-19523](https://nvd.nist.gov/vuln/detail/CVE-2019-19523){: external}, [CVE-2019-19524](https://nvd.nist.gov/vuln/detail/CVE-2019-19524){: external}, [CVE-2019-19530](https://nvd.nist.gov/vuln/detail/CVE-2019-19530){: external}, [CVE-2019-19534](https://nvd.nist.gov/vuln/detail/CVE-2019-19534){: external}, [CVE-2019-19537](https://nvd.nist.gov/vuln/detail/CVE-2019-19537){: external}, [CVE-2019-19767](https://nvd.nist.gov/vuln/detail/CVE-2019-19767){: external}, [CVE-2019-19807](https://nvd.nist.gov/vuln/detail/CVE-2019-19807){: external}, [CVE-2019-20054](https://nvd.nist.gov/vuln/detail/CVE-2019-20054){: external}, [CVE-2019-20095](https://nvd.nist.gov/vuln/detail/CVE-2019-20095){: external}, [CVE-2019-20636](https://nvd.nist.gov/vuln/detail/CVE-2019-20636){: external}, [CVE-2020-1749](https://nvd.nist.gov/vuln/detail/CVE-2020-1749){: external}, [CVE-2020-2732](https://nvd.nist.gov/vuln/detail/CVE-2020-2732){: external}, [CVE-2020-8647](https://nvd.nist.gov/vuln/detail/CVE-2020-8647){: external}, [CVE-2020-8649](https://nvd.nist.gov/vuln/detail/CVE-2020-8649){: external}, [CVE-2020-9383](https://nvd.nist.gov/vuln/detail/CVE-2020-9383){: external}, [CVE-2020-10690](https://nvd.nist.gov/vuln/detail/CVE-2020-10690){: external}, [CVE-2020-10732](https://nvd.nist.gov/vuln/detail/CVE-2020-10732){: external}, [CVE-2020-10742](https://nvd.nist.gov/vuln/detail/CVE-2020-10742){: external}, [CVE-2020-10751](https://nvd.nist.gov/vuln/detail/CVE-2020-10751){: external}, [CVE-2020-10942](https://nvd.nist.gov/vuln/detail/CVE-2020-10942){: external}, [CVE-2020-11565](https://nvd.nist.gov/vuln/detail/CVE-2020-11565){: external}, [CVE-2020-12770](https://nvd.nist.gov/vuln/detail/CVE-2020-12770){: external}, [CVE-2020-12826](https://nvd.nist.gov/vuln/detail/CVE-2020-12826){: external}, [CVE-2020-14305](https://nvd.nist.gov/vuln/detail/CVE-2020-14305){: external}, [CVE-2019-5482](https://nvd.nist.gov/vuln/detail/CVE-2019-5482){: external}, [CVE-2019-19126](https://nvd.nist.gov/vuln/detail/CVE-2019-19126){: external}, [CVE-2020-12825](https://nvd.nist.gov/vuln/detail/CVE-2020-12825){: external}, [CVE-2019-5094](https://nvd.nist.gov/vuln/detail/CVE-2019-5094){: external}, [CVE-2019-5188](https://nvd.nist.gov/vuln/detail/CVE-2019-5188){: external}, [CVE-2019-2974](https://nvd.nist.gov/vuln/detail/CVE-2019-2974){: external}, [CVE-2020-2574](https://nvd.nist.gov/vuln/detail/CVE-2020-2574){: external}, [CVE-2020-2752](https://nvd.nist.gov/vuln/detail/CVE-2020-2752){: external}, [CVE-2020-2780](https://nvd.nist.gov/vuln/detail/CVE-2020-2780){: external}, [CVE-2020-2812](https://nvd.nist.gov/vuln/detail/CVE-2020-2812){: external}, [CVE-2019-12749](https://nvd.nist.gov/vuln/detail/CVE-2019-12749){: external}, [CVE-2019-19956](https://nvd.nist.gov/vuln/detail/CVE-2019-19956){: external}, [CVE-2019-20388](https://nvd.nist.gov/vuln/detail/CVE-2019-20388){: external}, [CVE-2020-7595](https://nvd.nist.gov/vuln/detail/CVE-2020-7595){: external}, [CVE-2020-10754](https://nvd.nist.gov/vuln/detail/CVE-2020-10754){: external}, [CVE-2019-11719](https://nvd.nist.gov/vuln/detail/CVE-2019-11719){: external}, [CVE-2019-11727](https://nvd.nist.gov/vuln/detail/CVE-2019-11727){: external}, [CVE-2019-11756](https://nvd.nist.gov/vuln/detail/CVE-2019-11756){: external}, [CVE-2019-17006](https://nvd.nist.gov/vuln/detail/CVE-2019-17006){: external}, [CVE-2019-17023](https://nvd.nist.gov/vuln/detail/CVE-2019-17023){: external}, [CVE-2020-6829](https://nvd.nist.gov/vuln/detail/CVE-2020-6829){: external}, [CVE-2020-12400](https://nvd.nist.gov/vuln/detail/CVE-2020-12400){: external}, [CVE-2020-12401](https://nvd.nist.gov/vuln/detail/CVE-2020-12401){: external}, [CVE-2020-12402](https://nvd.nist.gov/vuln/detail/CVE-2020-12402){: external}, [CVE-2020-12403](https://nvd.nist.gov/vuln/detail/CVE-2020-12403){: external}, [CVE-2018-20843](https://nvd.nist.gov/vuln/detail/CVE-2018-20843){: external}, [CVE-2019-15903](https://nvd.nist.gov/vuln/detail/CVE-2019-15903){: external}, [CVE-2019-14834](https://nvd.nist.gov/vuln/detail/CVE-2019-14834){: external}, [CVE-2019-11068](https://nvd.nist.gov/vuln/detail/CVE-2019-11068){: external}, [CVE-2019-18197](https://nvd.nist.gov/vuln/detail/CVE-2019-18197){: external}, [CVE-2019-16935](https://nvd.nist.gov/vuln/detail/CVE-2019-16935){: external}, [CVE-2019-20386](https://nvd.nist.gov/vuln/detail/CVE-2019-20386){: external}, [CVE-2019-17498](https://nvd.nist.gov/vuln/detail/CVE-2019-17498){: external}, and [CVE-2020-14365](https://nvd.nist.gov/vuln/detail/CVE-2020-14365){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.286_1569_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.286_1569_openshift, released 30 September 2020
{: #311286_1569}

The following table shows the changes that are in the worker node fix pack update `3.11.286_1569_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Automation for provisioning and reloading | N/A    | N/A | Fixes an issue that prevented SDS worker nodes with unified extensible firmware interface (UEFI) bootstrapping from provisioning or reloading.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.286_1568_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.286_1568_openshift, released 28 September 2020
{: #311286_1568}

The following table shows the changes that are in the worker node fix pack update `3.11.286_1568_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.272    | 3.11.286 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-286){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.272_1566_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.272_1567_openshift, released 21 September 2020
{: #311272_1567}

The following table shows the changes that are in the master fix pack patch update `3.11.272_1567_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster health image | v1.1.9 | v1.1.11 | Updated `Go` version for [CVE-2020-16845](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-16845){: external} and [CVE-2020-24553](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24553){: external}. |
| etcd | v3.3.22 | v3.3.25 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.3.25){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 377 | 378 | Updated `Go` version for [CVE-2020-16845](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-16845){: external}. |
| Key Management Service provider | v1.0.1 | v1.0.3 | Updated `Go` version for [CVE-2020-16845](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-16845){: external} and [CVE-2020-24553](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24553){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.248 | 3.11.272 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-272){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.272_1566_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.272_1566_openshift, released 14 September 2020
{: #311272_1566}

The following table shows the changes that are in the worker node fix pack update `3.11.272_1566_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Master proxy | 1.8.25-384f42 | 1.8.26-561f1a | See the [HAProxy changelog](https://www.haproxy.org/download/1.8/src/CHANGELOG){: external}. |
| RHEL 7 packages | N/A | N/A | Updated worker node image with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.272_1565_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.272_1565_openshift, released 31 August 2020
{: #311272_1565}

The following table shows the changes that are in the worker node fix pack update `3.11.272_1565_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 packages | 3.10.0-1127.18.2.el7 | 3.10.0-1127.19.1.el7 | Updated worker node image with kernel and package updates. |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.248 | 3.11.272 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-272){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.248_1564_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.248_1564_openshift, released 18 August 2020
{: #311248_1564_master}

The following table shows the changes that are in the master fix pack patch update `3.11.248_1564_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Calico node configuration | N/A | N/A | Disabled the pod readiness probe and removed the `felix` check from the pod liveness probe. |
| Cluster health image | v1.1.8 | v1.1.9 | Updated to use `Go` version 1.13.13. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 376 | 377 | Fixed a bug that prevents persistent volume claim (PVC) creation failures from being retried. |
| Key Management Service provider | v1.0.0 | v1.0.1 | Updated image for [CVE-2020-15586](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-15586){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.232 | 3.11.248 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-248){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.232_1561_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.248_1564_openshift, released 17 August 2020
{: #311248_1564}

The following table shows the changes that are in the worker node fix pack update `3.11.248_1564_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 packages | N/A | N/A | Updated worker node images with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.248_1561_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.248_1561_openshift, released 3 August 2020
{: #311248_1561}

The following table shows the changes that are in the worker node fix pack update `3.11.248_1561_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.232 | 3.11.248 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-248){: external}. The update resolves CVE-2020-8558 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6319989){: external}). |
| RHEL 7 Packages | 3.10.0-1127.13.1.el7 | 3.10.0-1127.18.2.el7 | Updated worker node images with package updates for [CVE-2020-10713](https://nvd.nist.gov/vuln/detail/CVE-2020-10713){: external}, [CVE-2020-14308](https://nvd.nist.gov/vuln/detail/CVE-2020-14308){: external}, [CVE-2020-14309](https://nvd.nist.gov/vuln/detail/CVE-2020-14309){: external}, [CVE-2020-14310](https://nvd.nist.gov/vuln/detail/CVE-2020-14310){: external}, [CVE-2020-14311](https://nvd.nist.gov/vuln/detail/CVE-2020-14311){: external}, [CVE-2020-15705](https://nvd.nist.gov/vuln/detail/CVE-2020-15705){: external}, [CVE-2020-15706](https://nvd.nist.gov/vuln/detail/CVE-2020-15706){: external}, [CVE-2020-15707](https://nvd.nist.gov/vuln/detail/CVE-2020-15707){: external}, [CVE-2019-19527](https://nvd.nist.gov/vuln/detail/CVE-2019-19527){: external}, [CVE-2020-10757](https://nvd.nist.gov/vuln/detail/CVE-2020-10757){: external}, [CVE-2020-12653](https://nvd.nist.gov/vuln/detail/CVE-2020-12653){: external}, and [CVE-2020-12654](https://nvd.nist.gov/vuln/detail/CVE-2020-12654){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.232_1558_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.232_1560_openshift, released 24 July 2020
{: #311232_1560}

The following table shows the changes that are in the master fix pack update `3.11.232_1560_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Heapster configuration | N/A | N/A | Configuration changes now properly trigger a restart of the `heapster` pod in `kube-system` namespace. |
| Cluster master operations | N/A | N/A | Fixed a problem that might cause pods to fail authentication to the Kubernetes API server after a cluster master operation. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 375 | 376 | Updated to use `Go` version 1.13.8. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.232_1559_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.232_1559_openshift, released 20 July 2020
{: #311232_1559}

The following table shows the changes that are in the master fix pack update `3.11.232_1559_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Block Storage driver configuration | N/A | N/A | Added a pod memory limit. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor configuration | N/A | N/A | Added a pod memory limit. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.219 | 3.11.232 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-232){: external}. The update resolves CVE-2019-11254 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6249873){: external}) and CVE-2020-8555 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6249891){: external}). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.232_1555_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.232_1558_openshift, released 20 July 2020
{: #311232_1558}

The following table shows the changes that are in the worker node fix pack update `3.11.232_1558_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Master Proxy | 2.0.15-afe432 | 1.8.25-384f42 | See the [HAProxy changelogs](https://www.haproxy.org/download/1.8/src/CHANGELOG){: external}. Fixes a connection leak that happens when HAProxy is under high load. |
| RHEL 7 Packages |  N/A | N/A | Updated worker node images with package updates for [CVE-2020-12049](https://nvd.nist.gov/vuln/detail/CVE-2020-12049){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.232_1555_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.232_1555_openshift, released 6 July 2020
{: #311232_1555}

The following table shows the changes that are in the worker node fix pack update `3.11.232_1555_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Master Proxy | 1.8.25-30b675 | 2.0.15-afe432 | See the [HAProxy changelogs](https://www.haproxy.org/download/2.0/src/CHANGELOG){: external}. |
| RHEL 7 Packages | 3.10.0-1127.10.1.el7 | 3.10.0-1127.13.1.el7 | Updated worker node images with kernel package updates for [CVE-2020-10749](https://nvd.nist.gov/vuln/detail/CVE-2020-10749){: external}, [CVE-2020-1702](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1702){: external}, [CVE-2016-8867](https://nvd.nist.gov/vuln/detail/CVE-2016-8867){: external}, [CVE-2020-14298](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14298){: external}, [CVE-2020-14300](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14300){: external}, [CVE-2020-12888](https://nvd.nist.gov/vuln/detail/CVE-2020-12888){: external}, [CVE-2020-11868](https://nvd.nist.gov/vuln/detail/CVE-2020-11868){: external}, and [CVE-2020-13817](https://nvd.nist.gov/vuln/detail/CVE-2020-13817){: external}. |
| Worker node `drain` automation | N/A | N/A | Fixes a race condition that can cause worker node `drain` automation to fail. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.232_1554_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.219_1554_openshift and worker node fix pack 3.11.232_1554_openshift, released 22 June 2020
{: #311219_1554_master}

The following table shows the changes that are in the master fix pack update `3.11.219_1554_openshift` and in worker node fix pack update `3.11.232_1554_openshift`. Master patch updates are applied automatically. Worker node patch updates can be applied by updating or reloading the worker node For more information, see [Update types](/docs/openshift?topic=openshift-openshift_versions#openshift_update_types).
{: shortdesc}

| Component | Location | Previous | Current | Description |
| --------- | -------- | ------- | -------- | ----------- |
| Calico | Master | v3.8.6 | v3.8.9 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases){: external}. |
| Cluster health image | Master | v1.1.5 | v1.1.8 | Additional status information is included when an add-on health state is `critical`. Improved performance when handling cluster status updates. |
| Cluster master operations | Master | N/A | N/A | Cluster master operations such as `refresh` or `update` are now canceled if a broken [Kubernetes admission webhook](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/){: external} is detected. |
| etcd | Master | v3.3.20 | v3.3.22 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.3.22){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | Master | v1.15.12-316 | v1.15.12-343 | Updated to use `calicoctl` version 3.8.9. |
| {{site.data.keyword.filestorage_full_notm}} plug-in | Master | 373 | 375 | Fixed a bug that might cause error handling to create additional persistent volumes. |
| {{site.data.keyword.redhat_openshift_notm}} | Master | 3.11.216 | 3.11.219 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-219){: external}. The master update resolves CVE-2020-8552 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6238260){: external}). |
| {{site.data.keyword.redhat_openshift_notm}} node | Worker | 3.11.219 | 3.11.232 | See the [{{site.data.keyword.redhat_openshift_notm}}  release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-232){: external}. |
| RHEL 7 packages | Worker | N/A | N/A | Updated worker node images with package updates for [CVE-2020-0543](https://nvd.nist.gov/vuln/detail/CVE-2020-0543){: external}, [CVE-2020-0548](https://nvd.nist.gov/vuln/detail/CVE-2020-0548){: external}, and [CVE-2020-0549](https://nvd.nist.gov/vuln/detail/CVE-2020-0549){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is where the component is located, the master, worker node, or both. The third column is the previous version number of the component. The fourth column is the current version number of the component. The fifth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.219_1552_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.219_1552_openshift, released 8 June 2020
{: #311219_1552}

The following table shows the changes that are in the worker node fix pack update `3.11.219_1552_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.216 | 3.11.219 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-219){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.216_1551_openshift" caption-side="top"}

### Changelog for 3.11.216_1551_openshift, released 26 May 2020
{: #311216_1551}

The following table shows the changes that are in the master and worker node update `3.11.216_1551_openshift`. Master patch updates are applied automatically. Worker node patch updates can be applied by updating or reloading the worker node For more information, see [Update types](/docs/openshift?topic=openshift-openshift_versions#openshift_update_types).
{: shortdesc}

| Component | Location | Previous | Current | Description |
| --------- | -------- | ------- | -------- | ----------- |
| Cluster health image | Master | v1.1.1 | v1.1.5 | When cluster add-ons don't support the current cluster version, a warning is now returned in the cluster health state. |
| etcd | Master | v3.3.18 | v3.3.20 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.3.20){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | Master | v1.15.11-274 | v1.15.12-316 | Updated to support the Kubernetes 1.15.12 release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | Master | 358 | 373 | Updated image for [CVE-2020-1967](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1967){: external} and [CVE-2020-11655](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-11655){: external}. |
| {{site.data.keyword.cloud_notm}} Paks | Master | N/A | N/A | Removed duplicate repositories in `ClusterImagePolicies` resources that are installed by {{site.data.keyword.cloud_notm}} Paks. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | Master | 169 | 203 | Version 2.0 network load balancers (NLB) were updated to fix problems with long-lived network connections to endpoints that failed readiness probes. Updated image for [CVE-2020-1967](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1967){: external}. |
| {{site.data.keyword.redhat_openshift_notm}}  | Master | 3.11.200 | 3.11.216 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-216){: external}. |
| RHEL 7 Packages | Worker | 3.10.0-1127.el7 | 3.10.0-1127.8.2.el7 | Updated worker node images with kernel package updates for [CVE-2017-18595](https://nvd.nist.gov/vuln/detail/CVE-2017-18595){: external}, [CVE-2019-19768](https://nvd.nist.gov/vuln/detail/CVE-2019-19768){: external}, and [CVE-2020-10711](https://nvd.nist.gov/vuln/detail/CVE-2020-10711){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is where the component is located, the master, worker node, or both. The third column is the previous version number of the component. The fourth column is the current version number of the component. The fifth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.216_1550_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.216_1550_openshift, released 11 May 2020
{: #311216_1550}

The following table shows the changes that are in the worker node fix pack update `3.11.216_1550_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.200 | 3.11.216 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-216){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.200_1549_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.200_1549_openshift, released 27 April 2020
{: #311200_1549}

The following table shows the changes that are in the worker node fix pack update `3.11.200_1549_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 1.8.25-30b675 | 1.8.25-adb65d | Update addresses [CVE-2020-1967](https://nvd.nist.gov/vuln/detail/CVE-2020-1967){: external}. |
| RHEL 7 Packages | N/A | N/A | Updated worker node images with package updates for [CVE-2019-19921](https://nvd.nist.gov/vuln/detail/CVE-2019-19921){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.200_1546_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.200_1548_openshift, released 23 April 2020
{: #311200_1548}

The following table shows the changes that are in the master fix pack update `3.11.200_1548_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico configuration | N/A | N/A | Updated to allow egress from the worker nodes via the `allow-vrrp` `GlobalNetworkPolicy`. |
| Cluster health | N/A | v1.1.1 | Cluster health now includes more add-on status information. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.15.10-252 | v1.15.11-274 | Updated to support the Kubernetes 1.15.11 release and to use `Go` version 1.12.17. |
| {{site.data.keyword.cloud_notm}} Paks | N/A | N/A | Fixed `ClusterImagePolicies` resources that are installed by {{site.data.keyword.cloud_notm}} Paks which prevent cluster master operations from succeeding. |
| Key Management Service provider | 277 | v1.0.0 | Updated the {{site.data.keyword.keymanagementservicelong_notm}} `Go` client. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.170 | 3.11.200 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-200){: external}. |
| OpenVPN client | N/A | N/A | Fixed a problem that might cause the `vpn-config` secret in the `kube-system` project to be deleted during cluster master operations. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.200_1546_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.200_1546_openshift, released 13 April 2020
{: #311200_1546_worker}

The following table shows the changes that are in the worker node fix pack update `3.11.200_1546_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 1.8.23 | 1.8.25 | See the [HA proxy changelogs](https://www.haproxy.org/download/1.8/src/CHANGELOG){: external}. Contains update for [CVE-2020-11100](https://nvd.nist.gov/vuln/detail/CVE-2020-11100){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.188 | 3.11.200 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-200){: external}. |
| RHEL 7 Packages | 3.10.0-1062.18.1.el7 | 3.10.0-1127.el7 | Updated worker node images with package and kernel updates for [CVE-2015-2716](https://nvd.nist.gov/vuln/detail/CVE-2015-2716){: external}, [CVE-2015-8035](https://nvd.nist.gov/vuln/detail/CVE-2015-8035){: external}, [CVE-2015-9289](https://nvd.nist.gov/vuln/detail/CVE-2015-9289){: external}, [CVE-2016-5131](https://nvd.nist.gov/vuln/detail/CVE-2016-5131){: external}, [CVE-2017-1000476](https://nvd.nist.gov/vuln/detail/CVE-2017-1000476){: external}, [CVE-2017-11166](https://nvd.nist.gov/vuln/detail/CVE-2017-11166){: external}, [CVE-2017-12805](https://nvd.nist.gov/vuln/detail/CVE-2017-12805){: external}, [CVE-2017-12806](https://nvd.nist.gov/vuln/detail/CVE-2017-12806){: external}, [CVE-2017-15412](https://nvd.nist.gov/vuln/detail/CVE-2017-15412){: external}, [CVE-2017-17807](https://nvd.nist.gov/vuln/detail/CVE-2017-17807){: external}, [CVE-2017-18251](https://nvd.nist.gov/vuln/detail/CVE-2017-18251){: external}, [CVE-2017-18252](https://nvd.nist.gov/vuln/detail/CVE-2017-18252){: external}, [CVE-2017-18254](https://nvd.nist.gov/vuln/detail/CVE-2017-18254){: external}, [CVE-2017-18258](https://nvd.nist.gov/vuln/detail/CVE-2017-18258){: external}, [CVE-2017-18271](https://nvd.nist.gov/vuln/detail/CVE-2017-18271){: external}, [CVE-2017-18273](https://nvd.nist.gov/vuln/detail/CVE-2017-18273){: external}, [CVE-2017-6519](https://nvd.nist.gov/vuln/detail/CVE-2017-6519){: external}, [CVE-2018-10177](https://nvd.nist.gov/vuln/detail/CVE-2018-10177){: external}, [CVE-2018-10360](https://nvd.nist.gov/vuln/detail/CVE-2018-10360){: external}, [CVE-2018-10804](https://nvd.nist.gov/vuln/detail/CVE-2018-10804){: external}, [CVE-2018-10805](https://nvd.nist.gov/vuln/detail/CVE-2018-10805){: external}, [CVE-2018-1116](https://nvd.nist.gov/vuln/detail/CVE-2018-1116){: external}, [CVE-2018-11656](https://nvd.nist.gov/vuln/detail/CVE-2018-11656){: external}, [CVE-2018-12599](https://nvd.nist.gov/vuln/detail/CVE-2018-12599){: external}, [CVE-2018-12600](https://nvd.nist.gov/vuln/detail/CVE-2018-12600){: external}, [CVE-2018-13153](https://nvd.nist.gov/vuln/detail/CVE-2018-13153){: external}, [CVE-2018-14404](https://nvd.nist.gov/vuln/detail/CVE-2018-14404){: external}, [CVE-2018-14434](https://nvd.nist.gov/vuln/detail/CVE-2018-14434){: external}, [CVE-2018-14435](https://nvd.nist.gov/vuln/detail/CVE-2018-14435){: external}, [CVE-2018-14436](https://nvd.nist.gov/vuln/detail/CVE-2018-14436){: external}, [CVE-2018-14437](https://nvd.nist.gov/vuln/detail/CVE-2018-14437){: external}, [CVE-2018-14567](https://nvd.nist.gov/vuln/detail/CVE-2018-14567){: external}, [CVE-2018-15607](https://nvd.nist.gov/vuln/detail/CVE-2018-15607){: external}, [CVE-2018-16328](https://nvd.nist.gov/vuln/detail/CVE-2018-16328){: external}, [CVE-2018-16749](https://nvd.nist.gov/vuln/detail/CVE-2018-16749){: external}, [CVE-2018-16750](https://nvd.nist.gov/vuln/detail/CVE-2018-16750){: external}, [CVE-2018-18544](https://nvd.nist.gov/vuln/detail/CVE-2018-18544){: external}, [CVE-2018-18751](https://nvd.nist.gov/vuln/detail/CVE-2018-18751){: external}, [CVE-2018-19985](https://nvd.nist.gov/vuln/detail/CVE-2018-19985){: external}, [CVE-2018-20169](https://nvd.nist.gov/vuln/detail/CVE-2018-20169){: external}, [CVE-2018-20467](https://nvd.nist.gov/vuln/detail/CVE-2018-20467){: external}, [CVE-2018-20852](https://nvd.nist.gov/vuln/detail/CVE-2018-20852){: external}, [CVE-2018-5745](https://nvd.nist.gov/vuln/detail/CVE-2018-5745){: external}, [CVE-2018-7191](https://nvd.nist.gov/vuln/detail/CVE-2018-7191){: external}, [CVE-2018-8804](https://nvd.nist.gov/vuln/detail/CVE-2018-8804){: external}, [CVE-2018-9133](https://nvd.nist.gov/vuln/detail/CVE-2018-9133){: external}, [CVE-2019-10131](https://nvd.nist.gov/vuln/detail/CVE-2019-10131){: external}, [CVE-2019-10207](https://nvd.nist.gov/vuln/detail/CVE-2019-10207){: external}, [CVE-2019-10638](https://nvd.nist.gov/vuln/detail/CVE-2019-10638){: external}, [CVE-2019-10639](https://nvd.nist.gov/vuln/detail/CVE-2019-10639){: external}, [CVE-2019-10650](https://nvd.nist.gov/vuln/detail/CVE-2019-10650){: external}, [CVE-2019-11190](https://nvd.nist.gov/vuln/detail/CVE-2019-11190){: external}, [CVE-2019-11470](https://nvd.nist.gov/vuln/detail/CVE-2019-11470){: external}, [CVE-2019-11472](https://nvd.nist.gov/vuln/detail/CVE-2019-11472){: external}, [CVE-2019-11597](https://nvd.nist.gov/vuln/detail/CVE-2019-11597){: external}, [CVE-2019-11598](https://nvd.nist.gov/vuln/detail/CVE-2019-11598){: external}, [CVE-2019-11884](https://nvd.nist.gov/vuln/detail/CVE-2019-11884){: external}, [CVE-2019-12382](https://nvd.nist.gov/vuln/detail/CVE-2019-12382){: external}, [CVE-2019-12974](https://nvd.nist.gov/vuln/detail/CVE-2019-12974){: external}, [CVE-2019-12975](https://nvd.nist.gov/vuln/detail/CVE-2019-12975){: external}, [CVE-2019-12976](https://nvd.nist.gov/vuln/detail/CVE-2019-12976){: external}, [CVE-2019-12978](https://nvd.nist.gov/vuln/detail/CVE-2019-12978){: external}, [CVE-2019-12979](https://nvd.nist.gov/vuln/detail/CVE-2019-12979){: external}, [CVE-2019-13133](https://nvd.nist.gov/vuln/detail/CVE-2019-13133){: external}, [CVE-2019-13134](https://nvd.nist.gov/vuln/detail/CVE-2019-13134){: external}, [CVE-2019-13135](https://nvd.nist.gov/vuln/detail/CVE-2019-13135){: external}, [CVE-2019-13233](https://nvd.nist.gov/vuln/detail/CVE-2019-13233){: external}, [CVE-2019-13295](https://nvd.nist.gov/vuln/detail/CVE-2019-13295){: external}, [CVE-2019-13297](https://nvd.nist.gov/vuln/detail/CVE-2019-13297){: external}, [CVE-2019-13300](https://nvd.nist.gov/vuln/detail/CVE-2019-13300){: external}, [CVE-2019-13301](https://nvd.nist.gov/vuln/detail/CVE-2019-13301){: external}, [CVE-2019-13304](https://nvd.nist.gov/vuln/detail/CVE-2019-13304){: external}, [CVE-2019-13305](https://nvd.nist.gov/vuln/detail/CVE-2019-13305){: external}, [CVE-2019-13306](https://nvd.nist.gov/vuln/detail/CVE-2019-13306){: external}, [CVE-2019-13307](https://nvd.nist.gov/vuln/detail/CVE-2019-13307){: external}, [CVE-2019-13309](https://nvd.nist.gov/vuln/detail/CVE-2019-13309){: external}, [CVE-2019-13310](https://nvd.nist.gov/vuln/detail/CVE-2019-13310){: external}, [CVE-2019-13311](https://nvd.nist.gov/vuln/detail/CVE-2019-13311){: external}, [CVE-2019-13454](https://nvd.nist.gov/vuln/detail/CVE-2019-13454){: external}, [CVE-2019-13648](https://nvd.nist.gov/vuln/detail/CVE-2019-13648){: external}, [CVE-2019-14283](https://nvd.nist.gov/vuln/detail/CVE-2019-14283){: external}, [CVE-2019-14980](https://nvd.nist.gov/vuln/detail/CVE-2019-14980){: external}, [CVE-2019-14981](https://nvd.nist.gov/vuln/detail/CVE-2019-14981){: external}, [CVE-2019-15139](https://nvd.nist.gov/vuln/detail/CVE-2019-15139){: external}, [CVE-2019-15140](https://nvd.nist.gov/vuln/detail/CVE-2019-15140){: external}, [CVE-2019-15141](https://nvd.nist.gov/vuln/detail/CVE-2019-15141){: external}, [CVE-2019-15221](https://nvd.nist.gov/vuln/detail/CVE-2019-15221){: external}, [CVE-2019-15916](https://nvd.nist.gov/vuln/detail/CVE-2019-15916){: external}, [CVE-2019-16056](https://nvd.nist.gov/vuln/detail/CVE-2019-16056){: external}, [CVE-2019-16708](https://nvd.nist.gov/vuln/detail/CVE-2019-16708){: external}, [CVE-2019-16709](https://nvd.nist.gov/vuln/detail/CVE-2019-16709){: external}, [CVE-2019-16710](https://nvd.nist.gov/vuln/detail/CVE-2019-16710){: external}, [CVE-2019-16711](https://nvd.nist.gov/vuln/detail/CVE-2019-16711){: external}, [CVE-2019-16712](https://nvd.nist.gov/vuln/detail/CVE-2019-16712){: external}, [CVE-2019-16713](https://nvd.nist.gov/vuln/detail/CVE-2019-16713){: external}, [CVE-2019-16746](https://nvd.nist.gov/vuln/detail/CVE-2019-16746){: external}, [CVE-2019-16884](https://nvd.nist.gov/vuln/detail/CVE-2019-16884){: external}, [CVE-2019-17041](https://nvd.nist.gov/vuln/detail/CVE-2019-17041){: external}, [CVE-2019-17042](https://nvd.nist.gov/vuln/detail/CVE-2019-17042){: external}, [CVE-2019-17540](https://nvd.nist.gov/vuln/detail/CVE-2019-17540){: external}, [CVE-2019-17541](https://nvd.nist.gov/vuln/detail/CVE-2019-17541){: external}, [CVE-2019-18660](https://nvd.nist.gov/vuln/detail/CVE-2019-18660){: external}, [CVE-2019-19948](https://nvd.nist.gov/vuln/detail/CVE-2019-19948){: external}, [CVE-2019-19949](https://nvd.nist.gov/vuln/detail/CVE-2019-19949){: external}, [CVE-2019-2737](https://nvd.nist.gov/vuln/detail/CVE-2019-2737){: external}, [CVE-2019-2739](https://nvd.nist.gov/vuln/detail/CVE-2019-2739){: external}, [CVE-2019-2740](https://nvd.nist.gov/vuln/detail/CVE-2019-2740){: external}, [CVE-2019-2805](https://nvd.nist.gov/vuln/detail/CVE-2019-2805){: external}, [CVE-2019-3820](https://nvd.nist.gov/vuln/detail/CVE-2019-3820){: external}, [CVE-2019-3901](https://nvd.nist.gov/vuln/detail/CVE-2019-3901){: external}, [CVE-2019-5436](https://nvd.nist.gov/vuln/detail/CVE-2019-5436){: external}, [CVE-2019-6465](https://nvd.nist.gov/vuln/detail/CVE-2019-6465){: external}, [CVE-2019-6477](https://nvd.nist.gov/vuln/detail/CVE-2019-6477){: external}, [CVE-2019-7175](https://nvd.nist.gov/vuln/detail/CVE-2019-7175){: external}, [CVE-2019-7397](https://nvd.nist.gov/vuln/detail/CVE-2019-7397){: external}, [CVE-2019-7398](https://nvd.nist.gov/vuln/detail/CVE-2019-7398){: external}, [CVE-2019-9503](https://nvd.nist.gov/vuln/detail/CVE-2019-9503){: external}, [CVE-2019-9924](https://nvd.nist.gov/vuln/detail/CVE-2019-9924){: external}, [CVE-2019-9956](https://nvd.nist.gov/vuln/detail/CVE-2019-9956){: external}, [CVE-2020-1702](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1702){: external}, and[CVE-2020-8945](https://nvd.nist.gov/vuln/detail/CVE-2020-8945){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.188_1545_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.188_1545_openshift, released 30 March 2020
{: #311188_1545_worker}

The following table shows the changes that are in the worker node fix pack update `3.11.188_1545_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 packages | 3.10.0-1062.12.1.el7 | 3.10.0-1062.18.1.el7 | Updated worker node images with package and kernel updates for [CVE-2019-19921](https://nvd.nist.gov/vuln/detail/CVE-2019-19921){: external}, [CVE-2019-11487](https://nvd.nist.gov/vuln/detail/CVE-2019-11487){: external}, [CVE-2019-17666](https://nvd.nist.gov/vuln/detail/CVE-2019-17666){: external}, and [CVE-2019-19338](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19338){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.170 | 3.11.188 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-188){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.170_1544_openshift" caption-side="top"}

### Changelog for 3.11.170_1544_openshift, released 16 March 2020
{: #311170_1544}

The following table shows the changes that are in the master and worker node update `3.11.170_1544_openshift`. Master patch updates are applied automatically. Worker node patch updates can be applied by updating or reloading the worker node For more information, see [Update types](/docs/openshift?topic=openshift-openshift_versions#openshift_update_types).
{: shortdesc}

| Component | Location | Previous | Current | Description |
| --------- | -------- | ------- | -------- | ----------- |
| Calico | Master | v3.6.5 | v3.8.6 | See the [Calico release notes](https://projectcalico.docs.tigera.io/archive/v3.8/release-notes/){: external}. |
| Cluster health | Master | N/A | N/A | Cluster health status now includes links to {{site.data.keyword.cloud_notm}} documentation. |
| {{site.data.keyword.redhat_openshift_notm}} | Both | 3.11.161 | 3.11.170 | See the [{{site.data.keyword.redhat_openshift_notm}}  release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-170){: external}. |
| RHEL 7 Packages | Worker | N/A | N/A | Updated worker node images with package updates for [CVE-2020-8597](https://nvd.nist.gov/vuln/detail/CVE-2020-8597){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is where the component is located: the master, worker node, or both. The third column is the previous version number of the component. The fourth column is the current version number of the component. The fifth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.170_1543" caption-side="top"}

### Changelog for worker node fix pack 3.11.170_1543_openshift, released 17 February 2020
{: #311170_1543_worker}

The following table shows the changes that are in the worker node fix pack update `3.11.170_1543_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.161 | 3.11.170 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-170){: external}. Fixes [CVE-2019-11244](https://nvd.nist.gov/vuln/detail/CVE-2019-11244){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.161_1542_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.161_1542_openshift, released 18 February 2020
{: #311161_1542_master}

The following table shows the changes that are in the master fix pack update `3.11.161_1542_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster master HA configuration | N/A | N/A | Updated configuration to improve availability during cluster master operations. |
| Heapster | v1.5.4 | v3.11.161 | Replaces [Kubernetes Heapster](https://github.com/kubernetes-retired/heapster/releases/tag/v1.5.4){: external} with [{{site.data.keyword.redhat_openshift_notm}} Heapster](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-161){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.15.9-240 | v1.15.10-252 | Updated to support the Kubernetes 1.15.10 release. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.161_1540_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.161_1542_openshift, released 17 February 2020
{: #311161_1542_worker}

The following table shows the changes that are in the worker node fix pack update `3.11.161_1542_openshift`. Worker node patch updates can be applied by updating or reloading the worker node
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 packages | 3.10.0-1062.9.1.el7 | 3.10.0-1062.12.1.el7 | Updated worker node images with kernel and package updates for  [CVE-2019-18408](https://nvd.nist.gov/vuln/detail/CVE-2019-18408){: external}, [CVE-2019-13734](https://nvd.nist.gov/vuln/detail/CVE-2019-13734){: external}, [CVE-2019-14816](https://nvd.nist.gov/vuln/detail/CVE-2019-14816){: external}, [CVE-2019-14895](https://nvd.nist.gov/vuln/detail/CVE-2019-14895){: external}, [CVE-2019-14898](https://nvd.nist.gov/vuln/detail/CVE-2019-14898){: external}, [CVE-2019-14901](https://nvd.nist.gov/vuln/detail/CVE-2019-14901){: external}, and [CVE-2019-17133](https://nvd.nist.gov/vuln/detail/CVE-2019-17133). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.161_1540_openshift" caption-side="top"}

### Changelog for worker node fix pack 3.11.161_1540_openshift, released 3 February 2020
{: #311161_1540}

The following table shows the changes that are in the worker node fix pack `3.11.161_1540_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 packages | N/A | N/A | Updated worker node images with package updates for [CVE-2019-13734](https://nvd.nist.gov/vuln/detail/CVE-2019-13734){: external} and [CVE-2019-18408](https://nvd.nist.gov/vuln/detail/CVE-2019-18408){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.161_1538_openshift" caption-side="top"}

### Changelog for master fix pack 3.11.161_1539_openshift, released 3 February 2020
{: #311161_1539}

The following table shows the changes that are in the master fix pack `3.11.161_1539_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster ingress route configuration | N/A | N/A | Fixed a bug that reset ingress route configurations to the default subdomain in clusters that were created with version [3.11.141_1524](/docs/openshift?topic=openshift-openshift_changelog#311141_1524) or earlier. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.15.7-229 | v1.15.9-240 | Updated to support the Kubernetes 1.15.9 release. Updated to use `calicoctl` version 3.8.6. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 357 | 358 | Image updated for [CVE-2019-5188](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-5188){: external}. |
| OpenVPN server | N/A | N/A | OpenVPN server is now restarted during the [cluster master refresh](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_apiserver_refresh) operation. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.161_1538_openshift" caption-side="top"}

### Changelog for 3.11.161_1538_openshift, released 20 January 2020
{: #311161_1538}

The following table shows the changes that are in the patch `3.11.161_1538_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster master HA Proxy | 1.8.21-alpine | 1.8.23-alpine | See the [HAProxy release notes](https://www.haproxy.org/download/1.8/src/CHANGELOG){: external}. Update resolves [CVE-2019-1551](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1551){: external}. |
| etcd | v3.3.17 | v3.3.18 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.3.18){: external}. Update resolves [CVE-2019-1551](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1551){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.15.6-200 | v1.15.7-229 | Updated to support the Kubernetes 1.15.7 release.|
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 354 | 357 | Made the `ibmc-block-gold` storage class the default storage class for new clusters only. The default storage class for existing clusters is unchanged. If you want to set your own default, see [Changing the default storage class](/docs/openshift?topic=openshift-kube_concepts#default_storageclass). Added the following storage classes: `ibmc-file-bronze-gid`, `ibmc-file-silver-gid`, and `ibmc-file-gold-gid`. Fixed bugs in support of [non-root user access to an NFS file share](/docs/openshift?topic=openshift-debug_storage_file){: external}. Resolved [CVE-2019-1551](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1551){: external}. |
| Key Management Service provider | 270 | 277 | Updated the {{site.data.keyword.keymanagementservicelong_notm}} Go client. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 159 | 169 | Updated image for [CVE-2019-1551](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1551){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.154 | 3.11.161 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-161){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} router configuration | N/A | N/A | Improved general availability of the {{site.data.keyword.redhat_openshift_notm}} router and enhanced the configuration for multizone clusters. Now, the router runs 3 pods with a scheduling configuration that prefers running pods across worker nodes and zones. |
| OpenVPN server | 2.4.6-r3-IKS-121 | 2.4.6-r3-IKS-131 | Updated image for [CVE-2019-1551](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1551){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 3.11.154_1537" caption-side="top"}

### Changelog for worker node fix pack 3.11.157_1537_openshift, released 23 December 2019
{: #311157_1537}

The following table shows the changes that are in the worker node fix pack `3.11.157_1537_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 packages | N/A | N/A | Updated worker node images with package updates for [CVE-2019-11729](https://nvd.nist.gov/vuln/detail/CVE-2019-11729){: external} and [CVE-2019-11745](https://nvd.nist.gov/vuln/detail/CVE-2019-11745){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.154 | 3.11.157 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-157){: external}. |
| Maximum process IDs (PIDs) for pods | N/A | N/A | Updated to support scaling the maximum allowed pod process IDs (PIDs) based on the [worker node machine type](/docs/openshift?topic=openshift-planning_worker_nodes#resource_limit_node). |
{: caption="Changes since version 3.11.154_1534" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for master fix pack 3.11.154_1536_openshift, released 17 December 2019
{: #311154_1536}

The following table shows the changes that are in the master fix pack `3.11.154_1536_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | N/A | N/A | Fixed a bug that might prevent updating the driver and plug-in components. |
| {{site.data.keyword.cloud_notm}} File Storage plug-in and monitor | 353 | 354 | Updated to support [non-root user access to an NFS file share](/docs/openshift?topic=openshift-debug_storage_file) by allocating a group ID (GID) in the storage class. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.15.6-182 | v1.15.6-200 | Updated version 1.0 and 2.0 network load balancers (NLBs) to prefer scheduling NLB pods on worker nodes that don't currently run any NLB pods. In addition, the Virtual Private Cloud (VPC) load balancer plug-in is updated to use Go version 1.12.11. |
| Key Management Service provider | 254 | 270 | Improves performance of secret management by minimizing the number of data encryption keys (DEKs) that are used to unwrap secrets in the cluster. In addition, the {{site.data.keyword.keymanagementservicelong_notm}} Go client is updated. |
{: caption="Changes since version 3.11.154_1534" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for worker node fix pack 3.11.154_1534_openshift, released 9 December 2019
{: #311154_1534_worker}

The following table shows the changes that are in the worker node fix pack `3.11.154_1534_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 kernel and packages | 3.10.0-1062.4.3.el7 | 3.10.0-1062.9.1.el7 | Updated worker node images with kernel and package updates for [CVE-2019-14821](https://nvd.nist.gov/vuln/detail/CVE-2019-14821){: external} and [CVE-2019-15239](https://nvd.nist.gov/vuln/detail/CVE-2019-15239){: external}.|
{: caption="Changes since version 3.11.153_1533" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for worker node fix pack 3.11.154_1533_openshift, released 25 November 2019
{: #311154_1533_worker}

The following table shows the changes that are in the worker node fix pack `3.11.154_1533_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.153 | 3.11.154 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-154){: external}.|
| RHEL 7 kernel and packages | 3.10.0-1062.4.1.el7 | 3.10.0-1062.4.3.el7 | Updated worker node images with kernel and package updates for [CVE-2018-12207](https://nvd.nist.gov/vuln/detail/CVE-2018-12207){: external}, [CVE-2019-0154](https://nvd.nist.gov/vuln/detail/CVE-2019-0154){: external}, [CVE-2019-11135](https://nvd.nist.gov/vuln/detail/CVE-2019-11135){: external}, and [CVE-2019-0155](https://nvd.nist.gov/vuln/detail/CVE-2019-0155).|
{: caption="Changes since version 3.11.153_1530" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for master fix pack 3.11.154_1533_openshift, released 21 November 2019
{: #311154_1533}

The following table shows the changes that are in the master fix pack `3.11.154_1533_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | 1.15.2 | 1.15.4 | Updated to use `Go` version 1.13.4. |
| {{site.data.keyword.cloud_notm}} File Storage plug-in and monitor | 350 | 353 | Updated to use the `distroless/static` base image and to use `Go` version 1.12.11. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.15.5-119 | v1.15.6-182 | Updated to support the Kubernetes 1.15.6 release. Updated to use `Go` version 1.12.12 and `calicoctl` version v3.8.4. |
| Key Management Service provider | 237 | 254 | Updated to use `Go` version 1.12.13. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.153 | 3.11.154 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-154){: external}. Update resolves [CVE-2019-11253](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-11253){: external} (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/1126071){: external}). |
{: caption="Changes since version 3.11.153_1530" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for worker node fix pack 3.11.153_1530_openshift, released 11 November 2019
{: #311153_1530}

The following table shows the changes that are in the worker node fix pack `3.11.153_1530_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 packages | N/A | N/A | Updated worker node images with package updates. |
{: caption="Changes since version 3.11.146_1529" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for worker node fix pack 3.11.153_1529_openshift, released 28 October 2019
{: #311153_1529}

The following table shows the changes that are in the worker node fix pack `3.11.153_1529_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.146 | 3.11.153 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-153){: external}.|
| RHEL 7 packages and kernel |  3.10.0-1062.1.2.el7 | 3.10.0-1062.4.1.el7 | Updated worker node images with kernel and package updates for [CVE-2019-14835](https://nvd.nist.gov/vuln/detail/CVE-2019-14835){: external}, [CVE-2019-14287](https://nvd.nist.gov/vuln/detail/CVE-2019-14287){: external}, [CVE-2019-3846](https://nvd.nist.gov/vuln/detail/CVE-2019-3846) [CVE-2019-10126](https://nvd.nist.gov/vuln/detail/CVE-2019-10126){: external}, [CVE-2019-9506](https://nvd.nist.gov/vuln/detail/CVE-2019-9506){: external}, and [CVE-2018-20856](https://nvd.nist.gov/vuln/detail/CVE-2018-20856){: external}. |
{: caption="Changes since version 3.11.146_1528" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for master fix pack 3.11.146_1528_openshift, released 22 October 2019
{: #311146_1528}

The following table shows the changes that are in the master fix pack `3.11.146_1528_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| etcd | v3.3.15 | v3.3.17 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.3.17){: external}. Update resolves [CVE-2019-1547](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1547){: external}, [CVE-2019-1549](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1549){: external}, and [CVE-2019-1563](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1563){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | N/A | N/A | Fixed a bug so that the driver and plug-in components can be updated. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.15.3-112 | v1.15.5-119 | Updated to support the Kubernetes 1.15.5 release. Update resolves [CVE-2019-16276](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16276){: external}. |
| {{site.data.keyword.cloud_notm}} File Storage plug-in and monitor | 349 | 350 | Updated image for [CVE-2019-1547](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1547){: external}, [CVE-2019-1549](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1549){: external}, and [CVE-2019-1563](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1563){: external}. |
| Key Management Service provider | 221 | 237 | Updated image for [CVE-2019-16276](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16276){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} provider | 153 | 159 | Updated image for [CVE-2019-1547](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1547){: external}, [CVE-2019-1549](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1549){: external}, [CVE-2019-1563](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1563){: external}, and [CVE-2019-16276](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16276){: external}. |
{: caption="Changes since version 3.11.146_1527" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for worker node fix pack 3.11.146_1527_openshift, released 14 October 2019
{: #311146_1527}

The following table shows the changes that are in the worker node fix pack `3.11.146_1527_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 packages and kernel | N/A | N/A | Updated worker node images with package updates. |
{: caption="Changes since version 3.11.146_1525" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for master fix pack 3.11.146_1526_openshift, released 4 October 2019
{: #311146_1526}

The following table shows the changes that are in the master fix pack `3.11.146_1526_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Default {{site.data.keyword.IBM_notm}} security context constraints | N/A | N/A | To support [{{site.data.keyword.cloud_notm}} Paks](https://www.ibm.com/cloud/paks/){: external}, the `seLinuxContext` setting is changed from `MustRunAs` to `RunAsAny` for the following [default {{site.data.keyword.IBM_notm}} security context constraints](/docs/openshift?topic=openshift-openshift_scc#ibm_sccs): `ibm-anyuid-hostaccess-scc`, `ibm-anyuid-hostpath-scc`, and `ibm-anyuid-scc`. |
{: caption="Changes since version 3.11.146_1525" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for 3.11.146_1525_openshift, released 3 October 2019
{: #311146_1525}

The following table shows the changes that are in the patch `3.11.146_1525_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Calico | v3.6.4 | v3.6.4 | See the [Calico release notes](https://projectcalico.docs.tigera.io/archive/v3.6/release-notes/){: external}.|
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | 1.15.1 | 1.15.2 | Fixed an issue that might cause worker nodes to fail in a `NotReady` status or pods not to start because of networking errors. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.11.10-286 | v1.15.3-112 | Updated to support the Kubernetes 1.15.3 release. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.141 | 3.11.146 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-146){: external}. Update resolves [CVE-2019-11247](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-11247){: external} (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/1101957){: external}) and [CVE-2019-11249](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-11249){: external} (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/1102029){: external}).|
| OpenVPN server | 2.4.6-r3-IKS-115 | 2.4.6-r3-IKS-121 | Image updated for [CVE-2019-1547](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1547){: external} and [CVE-2019-1563](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1563){: external}. |
| RHEL 7 packages and kernel | 3.10.0-1062.1.1 | 3.10.0-1062.1.2 | Updated worker node images with kernel and package updates for [CVE-2019-1125](https://nvd.nist.gov/vuln/detail/CVE-2019-14835){: external}. |
{: caption="Changes since version 3.11.141_1524" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for 3.11.141_1524_openshift, released 16 September 2019
{: #311141_1524}

The following table shows the changes that are in the patch `3.11.141_1524_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Key Management Service provider | 212 | 216 | Improved Kubernetes [key management service provider](/docs/openshift?topic=openshift-encryption#keyprotect) caching of {{site.data.keyword.cloud_notm}} IAM tokens. In addition, fixed a problem with Kubernetes secret decryption when the cluster's root key is rotated.|
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.135 | 3.11.141 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-141){: external}. |
| RHEL 7 packages and kernel | 3.10.0-1062 | 3.10.0-1062.1.1 | Updated worker node images with kernel and package updates for [CVE-2019-1125](https://nvd.nist.gov/vuln/detail/CVE-2019-1125){: external} and [CVE-2019-9500](https://nvd.nist.gov/vuln/detail/CVE-2019-9500){: external}. |
{: caption="Changes since version 3.11.135_1523" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for worker node fix pack 3.11.135_1523_openshift, released 3 September 2019
{: #311135_1523_worker}

The following table shows the changes that are in the worker node fix pack `3.11.135_1523_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 packages | N/A | N/A | Updated worker node images with package updates.|
{: caption="Changes since version 3.11.135_1521" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for master fix pack 3.11.135_1522_openshift, released 28 August 2019
{: #311135_1522}

The following table shows the changes that are in the master fix pack `3.11.135_1522_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Default {{site.data.keyword.IBM_notm}} security context constraints | N/A | N/A | Added `ibm-restricted-scc` to [Default {{site.data.keyword.IBM_notm}} security context constraints](/docs/openshift?topic=openshift-openshift_scc#ibm_sccs). |
| `etcd` | v3.3.13 | v3.3.15 | See the [`etcd` release notes](https://github.com/etcd-io/etcd/releases/v3.3.15){: external}. Update resolves [CVE-2019-9512](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9512){: external}, [CVE-2019-9514](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9514){: external}, and [CVE-2019-14809](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14809){: external}. |
| {{site.data.keyword.cloud_notm}} File Storage plug-in | 348 | 349 | Image updated for [CVE-2019-9512](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9512){: external}, [CVE-2019-9514](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9514){: external}, and [CVE-2019-14809](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14809){: external}. |
| Key Management Service provider | 207 | 212 | Image updated for [CVE-2019-9512](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9512){: external}, [CVE-2019-9514](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9514){: external}, and [CVE-2019-14809](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14809){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 147 | 148 | Image updated for [CVE-2019-9512](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9512){: external}, [CVE-2019-9514](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9514){: external}, and [CVE-2019-14809](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14809){: external}. |
{: caption="Changes since version 3.11.135_1521" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for worker node fix pack 3.11.135_1521_openshift, released 19 August 2019
{: #311135_1521_worker}

The following table shows the changes that are in the worker node fix pack `3.11.135_1521_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster master HA Proxy | 2.0.1-alpine | 1.8.21-alpine | Moved to HA Proxy 1.8 to fix [socket leak in HA Proxy](https://github.com/haproxy/haproxy/issues/136){: external}. Added a liveliness check to monitor the health of HA Proxy. For more information about other changes, see [release notes](https://www.haproxy.org/download/1.8/src/CHANGELOG){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} node | 3.11.129 | 3.11.135 | For more information, see the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-135){: external}. |
| RHEL 7 kernel | 3.10.0-957.21.3.el7 | 3.10.0-1062.el7 | Updated worker node images with kernel and package updates for [CVE-2018-16881](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-168810){: external}, [CVE-2019-6470](https://nvd.nist.gov/vuln/detail/CVE-2019-6470){: external}, [CVE-2018-14618](https://nvd.nist.gov/vuln/detail/CVE-2018-14618){: external}, [CVE-2018-16062](https://nvd.nist.gov/vuln/detail/CVE-2018-16062){: external}, [CVE-2018-16402](https://nvd.nist.gov/vuln/detail/CVE-2018-16402){: external}, [CVE-2018-16403](https://nvd.nist.gov/vuln/detail/CVE-2018-16403){: external}, [CVE-2018-18310](https://nvd.nist.gov/vuln/detail/CVE-2018-18310){: external}, [CVE-2018-18520](https://nvd.nist.gov/vuln/detail/CVE-2018-18520){: external}, [CVE-2018-18521](https://nvd.nist.gov/vuln/detail/CVE-2018-18521){: external}, [CVE-2019-7149](https://nvd.nist.gov/vuln/detail/CVE-2019-7149){: external}, [CVE-2019-7150](https://nvd.nist.gov/vuln/detail/CVE-2019-7150){: external}, [CVE-2019-7664](https://nvd.nist.gov/vuln/detail/CVE-2019-7664){: external}, [CVE-2019-7665](https://nvd.nist.gov/vuln/detail/CVE-2019-7665){: external}, [CVE-2016-10739](https://nvd.nist.gov/vuln/detail/CVE-2016-10739){: external}, [CVE-2018-16871](https://nvd.nist.gov/vuln/detail/CVE-2018-16871){: external}, [CVE-2018-16884](https://nvd.nist.gov/vuln/detail/CVE-2018-16884){: external}, [CVE-2019-11085](https://nvd.nist.gov/vuln/detail/CVE-2019-11085){: external}, [CVE-2019-11811](https://nvd.nist.gov/vuln/detail/CVE-2019-11811){: external}, [CVE-2018-15686](https://nvd.nist.gov/vuln/detail/CVE-2018-15686){: external}, [CVE-2018-16866](https://nvd.nist.gov/vuln/detail/CVE-2018-16866){: external}, [CVE-2018-16888](https://nvd.nist.gov/vuln/detail/CVE-2018-16888){: external}, [CVE-2018-12327](https://nvd.nist.gov/vuln/detail/CVE-2018-12327){: external}, [CVE-2018-12641](https://nvd.nist.gov/vuln/detail/CVE-2018-12641){: external}, [CVE-2018-12697](https://nvd.nist.gov/vuln/detail/CVE-2018-12697){: external}, [CVE-2018-1000876](https://nvd.nist.gov/vuln/detail/CVE-2018-1000876){: external}, [CVE-2018-16842](https://nvd.nist.gov/vuln/detail/CVE-2018-16842){: external}, [CVE-2018-5741](https://nvd.nist.gov/vuln/detail/CVE-2018-5741){: external}, [CVE-2018-0495](https://nvd.nist.gov/vuln/detail/CVE-2018-0495){: external}, [CVE-2018-12404](https://nvd.nist.gov/vuln/detail/CVE-2018-12404){: external}, [CVE-2018-1122](https://nvd.nist.gov/vuln/detail/CVE-2018-1122){: external}, [CVE-2018-7755](https://nvd.nist.gov/vuln/detail/CVE-2018-7755){: external}, [CVE-2018-8087](https://nvd.nist.gov/vuln/detail/CVE-2018-8087){: external}, [CVE-2018-9363](https://nvd.nist.gov/vuln/detail/CVE-2018-9363){: external}, [CVE-2018-9516](https://nvd.nist.gov/vuln/detail/CVE-2018-9516){: external}, [CVE-2018-9517](https://nvd.nist.gov/vuln/detail/CVE-2018-9517){: external}, [CVE-2018-10853](https://nvd.nist.gov/vuln/detail/CVE-2018-10853){: external}, [CVE-2018-13053](https://nvd.nist.gov/vuln/detail/CVE-2018-13053){: external}, [CVE-2018-13093](https://nvd.nist.gov/vuln/detail/CVE-2018-13093){: external}, [CVE-2018-13094](https://nvd.nist.gov/vuln/detail/CVE-2018-13094){: external}, [CVE-2018-13095](https://nvd.nist.gov/vuln/detail/CVE-2018-13095){: external}, [CVE-2018-14625](https://nvd.nist.gov/vuln/detail/CVE-2018-14625){: external}, [CVE-2018-14734](https://nvd.nist.gov/vuln/detail/CVE-2018-14734){: external}, [CVE-2018-15594](https://nvd.nist.gov/vuln/detail/CVE-2018-15594){: external}, [CVE-2018-16658](https://nvd.nist.gov/vuln/detail/CVE-2018-16658){: external}, [CVE-2018-16885](https://nvd.nist.gov/vuln/detail/CVE-2018-16885){: external}, [CVE-2018-18281](https://nvd.nist.gov/vuln/detail/CVE-2018-18281){: external}, [CVE-2019-3459](https://nvd.nist.gov/vuln/detail/CVE-2019-3459){: external}, [CVE-2019-3460](https://nvd.nist.gov/vuln/detail/CVE-2019-3460){: external}, [CVE-2019-3882](https://nvd.nist.gov/vuln/detail/CVE-2019-3882){: external}, [CVE-2019-3900](https://nvd.nist.gov/vuln/detail/CVE-2019-3900){: external}, [CVE-2019-5489](https://nvd.nist.gov/vuln/detail/CVE-2019-5489){: external}, [CVE-2018-18074](https://nvd.nist.gov/vuln/detail/CVE-2018-18074){: external}, [CVE-2019-3858](https://nvd.nist.gov/vuln/detail/CVE-2019-3858){: external}, [CVE-2019-3861](https://nvd.nist.gov/vuln/detail/CVE-2019-3861){: external}, [CVE-2019-3862](https://nvd.nist.gov/vuln/detail/CVE-2019-3862){: external}, [CVE-2018-14647](https://nvd.nist.gov/vuln/detail/CVE-2018-14647){: external}, [CVE-2019-5010](https://nvd.nist.gov/vuln/detail/CVE-2019-5010){: external}, [CVE-2019-9740](https://nvd.nist.gov/vuln/detail/CVE-2019-9740){: external}, [CVE-2019-9947](https://nvd.nist.gov/vuln/detail/CVE-2019-9947){: external}, [CVE-2019-9948](https://nvd.nist.gov/vuln/detail/CVE-2019-9948){: external}, [CVE-2017-14503](https://nvd.nist.gov/vuln/detail/CVE-2017-14503){: external}, [CVE-2018-1000877](https://nvd.nist.gov/vuln/detail/CVE-2018-1000877){: external}, [CVE-2018-1000878](https://nvd.nist.gov/vuln/detail/CVE-2018-1000878){: external}, [CVE-2019-1000019](https://nvd.nist.gov/vuln/detail/CVE-2019-1000019){: external}, [CVE-2019-1000020](https://nvd.nist.gov/vuln/detail/CVE-2019-1000020){: external}, [CVE-2018-3058](https://nvd.nist.gov/vuln/detail/CVE-2018-3058){: external}, [CVE-2018-3063](https://nvd.nist.gov/vuln/detail/CVE-2018-3063){: external}, [CVE-2018-3066](https://nvd.nist.gov/vuln/detail/CVE-2018-3066){: external}, [CVE-2018-3081](https://nvd.nist.gov/vuln/detail/CVE-2018-3081){: external}, [CVE-2018-3282](https://nvd.nist.gov/vuln/detail/CVE-2018-3282){: external}, [CVE-2019-2503](https://nvd.nist.gov/vuln/detail/CVE-2019-2503){: external}, [CVE-2019-2529](https://nvd.nist.gov/vuln/detail/CVE-2019-2529){: external}, [CVE-2019-2614](https://nvd.nist.gov/vuln/detail/CVE-2019-2614){: external}, [CVE-2019-2627](https://nvd.nist.gov/vuln/detail/CVE-2019-2627){: external}, [CVE-2018-14348](https://nvd.nist.gov/vuln/detail/CVE-2018-14348){: external}, [CVE-2018-15473](https://nvd.nist.gov/vuln/detail/CVE-2018-15473){: external}, [CVE-2018-5383](https://nvd.nist.gov/vuln/detail/CVE-2018-5383){: external}, [CVE-2018-19788](https://nvd.nist.gov/vuln/detail/CVE-2018-19788){: external}, [CVE-2018-0734](https://nvd.nist.gov/vuln/detail/CVE-2018-0734){: external}, [CVE-2019-1559](https://nvd.nist.gov/vuln/detail/CVE-2019-1559){: external}, [CVE-2018-20060](https://nvd.nist.gov/vuln/detail/CVE-2018-20060){: external}, and [CVE-2019-11236](https://nvd.nist.gov/vuln/detail/CVE-2019-11236){: external}. |
{: caption="Changes since version 3.11.129_1518" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for master fix pack 3.11.135_1521_openshift, released 17 August 2019
{: #311135_1521_master}

The following table shows the changes that are in the master fix pack `3.11.135_1521_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Key Management Service provider | 167 | 207 | Fixed an issue that causes the Kubernetes key management service (KMS) provider to fail to manage Kubernetes secrets. |
{: caption="Changes since version 3.11.135_1520" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for master fix pack 3.11.135_1520_openshift, released 15 August 2019
{: #311135_1520_master}

The following table shows the changes that are in the master fix pack `3.11.135_1520_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Calico configuration | N/A | N/A | Calico `calico-kube-controllers` deployment in the `kube-system` namespace sets a memory limit on the `calico-kube-controllers` container. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | 1.15 | 1.15.1 | Image updated for [CVE-2019-14697](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14697){: external}. |
| {{site.data.keyword.cloud_notm}} File Storage plug-in | 347 | 348 | Image updated for [CVE-2019-14697](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14697){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 146 | 147 | Image updated for [CVE-2019-14697](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14697){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 3.11.129 | 3.11.135 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/3.11/release_notes/ocp_3_11_release_notes.html#ocp-3-11-135){: external}. |
| OpenVPN client | 2.4.6-r3-IKS-90 | 2.4.6-r3-IKS-116 | Image updated for [CVE-2019-14697](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14697){: external}. |
| OpenVPN server | 2.4.6-r3-IKS-25 | 2.4.6-r3-IKS-115 | Image updated for [CVE-2019-14697](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14697){: external}. |
{: caption="Changes since version 3.11.129_1517" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for worker node patch 3.11.129_1518_openshift, released 5 August 2019
{: #311129_1518_worker}

The following table shows the changes that are in the worker node patch `3.11.129_1518_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 packages | N/A | N/A | Updated base packages in the worker node Red Hat Enterprise Linux image. |
{: caption="Changes since version 3.11.129_1517" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}

### Changelog for 3.11.129_1517_openshift, released 2 August 2019
{: #311129_1517}

The following table shows the changes that are in the patch `3.11.129_1517_openshift`.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster DNS configuration| N/A | N/A | For security reasons, enhanced local `dnsmasq` cache to listen on only `localhost`. Changed the DNS `targetPort` for the `kubernetes` cluster service from `8053` to `53`. |
| Cluster master HA proxy| 1.9.7-alpine| 2.0.1-alpine | See the [HAProxy release notes](https://www.haproxy.org/download/2.0/src/CHANGELOG){: external}. |
| Cluster router configuration| N/A | N/A | Fixed bugs that might cause cluster master operations, such as `refresh` or `update`, to fail when the router configuration is updated. These fixes also improve master availability during such operations. |
{: caption="Changes since version 3.11.129_1515" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}


