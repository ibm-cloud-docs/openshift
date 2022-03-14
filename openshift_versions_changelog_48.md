---

copyright:
  years: 2014, 2022
lastupdated: "2022-03-14"

keywords: openshift, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.redhat_openshift_notm}} version 4.8 changelog
{: #openshift_changelog_48}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.8. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #openshift_changelog_overview_48}

Unless otherwise noted in the changelogs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features, which are subject to change, are disabled.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security) for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Changelog entries that address other security vulnerabilities but don't also refer to an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}

## Change logs
{: 48_changelog}

Review the version 4.8 changelog.
{: shortdesc}


### Change log for worker node pack 4.8.32_1548_openshift, released 14 March 2022
{: #4832_1548}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | NA | NA | NA |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version  4.8.32_1547_openshift" caption-side="top"}

### Change log for master fix pack 4.8.29_1545_openshift, released 3 March 2022
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

### Change log for worker node fix pack 4.8.28_1543_openshift, released 31 January 2022
{: #4828_1543}

The following table shows the changes that are in the worker node fix pack `4.8.28_1543_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | Updated worker node images with package updates for [CVE-2021-4034](https://nvd.nist.gov/vuln/detail/CVE-2021-4034){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.26 | 4.8.28 | See the {{site.data.keyword.redhat_openshift_notm}} [changelogs](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-28){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.26_1541_openshift" caption-side="top"}

### Change log for master fix pack 4.8.26_1542_openshift, released 26 January 2022
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


### Change log for worker node fix pack 4.8.26_1541_openshift, released 18 January 2022
{: #4826_1541}

The following table shows the changes that are in the worker node fix pack `4.8.26_1541_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.49.1.el7 | 3.10.0-1160.53.1.el7 | Kernel and package updates for [CVE-2020-25704](https://nvd.nist.gov/vuln/detail/CVE-2020-25704){: external}, [CVE-2020-36322](https://nvd.nist.gov/vuln/detail/CVE-2020-36322){: external}, [CVE-2021-42739](https://nvd.nist.gov/vuln/detail/CVE-2021-42739){: external}, and [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.24 | 4.8.26 | See  the [change logs](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-26){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.24_1540_openshift" caption-side="top"}

### Change log for worker node fix pack 4.8.24_1540_openshift, released 4 January 2022
{: #4824_1540}

The following table shows the changes that are in the worker node fix pack patch update `4.8.24_1540_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 3b8663 | d38fa1 | Contains fixes for [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.24_1539_openshift" caption-side="top"}

### Change log for worker node fix pack 4.8.24_1539_openshift, released 20 December 2021
{: #4824_1539_openshift}

The following table shows the changes that are in the worker node fix pack patch update `4.8.24_1539_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} node | 4.8.20 | 4.8.22 | See [changelogs](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-22){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.22_1538_openshift" caption-side="top"}

### Change log for master fix pack 4.8.21_1537_openshift, released 7 December 2021
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


### Change log for worker node fix pack 4.8.22_1538_openshift, released 6 December 2021
{: #4822_1538}

The following table shows the changes that are in the worker node fix pack patch update `4.8.22_1538_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.45 | 3.10.0-1160.49 | Updated worker node images and kernel with package updates. [CVE-2020-36385](https://nvd.nist.gov/vuln/detail/CVE-2020-36385){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-41617](https://nvd.nist.gov/vuln/detail/CVE-2021-41617){: external}, [CVE-2021-20271](https://nvd.nist.gov/vuln/detail/CVE-2021-20271){: external} |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.20 | 4.8.22 | See the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-22){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.20_1536_openshift" caption-side="top"}

### Change log for worker node fix pack 4.8.20_1536_openshift, released 22 November 2021
{: #4820_1536}

The following table shows the changes that are in the worker node fix pack patch update `4.8.20_1536_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.18 | 4.8.20 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-20){: external}. | 
| Haproxy | 07f1e9e | 3b8663 | Contains fixes for [CVE-2021-20231](https://nvd.nist.gov/vuln/detail/CVE-2021-20231){: external}, [CVE-2021-20232](https://nvd.nist.gov/vuln/detail/CVE-2021-20232){: external}, [CVE-2021-3580](https://nvd.nist.gov/vuln/detail/CVE-2021-3580){: external}, [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946){: external}, [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947){: external}, [CVE-2021-22876](https://nvd.nist.gov/vuln/detail/CVE-2021-22876){: external}, [CVE-2021-22898](https://nvd.nist.gov/vuln/detail/CVE-2021-22898){: external}, [CVE-2021-22925](https://nvd.nist.gov/vuln/detail/CVE-2021-22925){: external}, [CVE-2019-20838](https://nvd.nist.gov/vuln/detail/CVE-2019-20838){: external}, [CVE-2020-14155](https://nvd.nist.gov/vuln/detail/CVE-2020-14155){: external}, [CVE-2018-20673](https://nvd.nist.gov/vuln/detail/CVE-2018-20673){: external}, [CVE-2021-42574](https://nvd.nist.gov/vuln/detail/CVE-2021-42574){: external}, [CVE-2019-17594](https://nvd.nist.gov/vuln/detail/CVE-2019-17594){: external}, [CVE-2019-17595](https://nvd.nist.gov/vuln/detail/CVE-2019-17595){: external}, [CVE-2020-12762](https://nvd.nist.gov/vuln/detail/CVE-2020-12762){: external}, [CVE-2020-16135](https://nvd.nist.gov/vuln/detail/CVE-2020-16135){: external}, [CVE-2021-3445](https://nvd.nist.gov/vuln/detail/CVE-2021-3445){: external}, [CVE-2021-36084](https://nvd.nist.gov/vuln/detail/CVE-2021-36084){: external}, [CVE-2021-36085](https://nvd.nist.gov/vuln/detail/CVE-2021-36085){: external}, [CVE-2021-36086](https://nvd.nist.gov/vuln/detail/CVE-2021-36086){: external}, [CVE-2021-36087](https://nvd.nist.gov/vuln/detail/CVE-2021-36087){: external}, [CVE-2021-20266](https://nvd.nist.gov/vuln/detail/CVE-2021-20266){: external}, [CVE-2019-18218](https://nvd.nist.gov/vuln/detail/CVE-2019-18218){: external}, [CVE-2021-23840](https://nvd.nist.gov/vuln/detail/CVE-2021-23840){: external}, [CVE-2021-23841](https://nvd.nist.gov/vuln/detail/CVE-2021-23841){: external}, [CVE-2021-27645](https://nvd.nist.gov/vuln/detail/CVE-2021-27645){: external}, [CVE-2021-33574](https://nvd.nist.gov/vuln/detail/CVE-2021-33574){: external}, [CVE-2021-35942](https://nvd.nist.gov/vuln/detail/CVE-2021-35942){: external}, [CVE-2021-33560](https://nvd.nist.gov/vuln/detail/CVE-2021-33560){: external}, [CVE-2019-13750](https://nvd.nist.gov/vuln/detail/CVE-2019-13750){: external}, [CVE-2019-13751](https://nvd.nist.gov/vuln/detail/CVE-2019-13751){: external}, [CVE-2019-19603](https://nvd.nist.gov/vuln/detail/CVE-2019-19603){: external}, [CVE-2019-5827](https://nvd.nist.gov/vuln/detail/CVE-2019-5827){: external}, [CVE-2020-13435](https://nvd.nist.gov/vuln/detail/CVE-2020-13435){: external}, [CVE-2020-24370](https://nvd.nist.gov/vuln/detail/CVE-2020-24370){: external}, [CVE-2021-28153](https://nvd.nist.gov/vuln/detail/CVE-2021-28153){: external}, [CVE-2021-3800](https://nvd.nist.gov/vuln/detail/CVE-2021-3800){: external}, [CVE-2021-33928](https://nvd.nist.gov/vuln/detail/CVE-2021-33928){: external}, [CVE-2021-33929](https://nvd.nist.gov/vuln/detail/CVE-2021-33929){: external}, [CVE-2021-33930](https://nvd.nist.gov/vuln/detail/CVE-2021-33930){: external}, [CVE-2021-33938](https://nvd.nist.gov/vuln/detail/CVE-2021-33938){: external}, and [CVE-2021-3200](https://nvd.nist.gov/vuln/detail/CVE-2021-3200){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.18_1533_openshift" caption-side="top"}

### Change log for master fix pack 4.8.18_1535_openshift, released 17 November 2021
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


### Change log for worker node fix pack 4.8.18_1533_openshift, released 10 November 2021
{: #4818_1533}

The following table shows the changes that are in the worker node fix pack patch update `4.8.18_1533_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages| N/A | N/A | Updated worker node image packages for [CVE-2021-42574](https://nvd.nist.gov/vuln/detail/CVE-2021-42574){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.15 | 4.8.18 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-8-18){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.15_1532_openshift" caption-side="top"}

### Change log for master fix pack 4.8.14_1531_openshift, released 29 October 2021
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

### Change log for worker node fix pack 4.8.15_1532_openshift, released 25 October 2021
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

### Change log for worker node fix pack 4.8.13_1528_openshift, released 11 October 2021
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


