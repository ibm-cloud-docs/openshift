---

copyright:
  years: 2022, 2022
lastupdated: "2022-08-01"

keywords: openshift, 4.10, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Version 4.10 change log
{: #openshift_changelog_410}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.10. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #openshift_changelog_overview_410}

Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features, which are subject to change, are disabled.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security) for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include a {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_changelog).
{: tip}


## Change logs
{: #410_changelog}

Review the version 4.10 change log.
{: shortdesc}















### Change log for master fix pack 4.10.22_1528_openshift, released 26 July 2022
{: #41022_1528_openshift}

The following table shows the changes that are in the master fix pack 4.10.22_1528_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.8 | v1.3.9 | Updated `Go` dependencies and to use `Go` version `1.18.4`. Fixed minor typo in addon `daemonset not available` health status. |
| Gateway-enabled cluster controller | 1680 | 1792 | Updated to use `Go` version `1.17.11`. Updated image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external} and [CVE-2022-29458](https://nvd.nist.gov/vuln/detail/CVE-2022-29458){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 980 | 997 | Updated to use `Go` version `1.17.11`. Updated universal base image (UBI) to version `8.6-854` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.6 | v2.2.8 | Updated to use `Go` version `1.18.3`. Updated universal base image (UBI) to version `8.6-854` to resolve CVEs. Updated to support RHEL 8 worker nodes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.7-7 | v1.23.8-7 | Updated `Go` dependencies and to use `Go` version `1.17.11`. Updated to support the Kubernetes `1.23.8` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 410 | 412 | Updated to use `Go` version `1.18.3`. Updated universal base image (UBI) to version `8.6-854` to resolve CVEs. Improved Kubernetes resource watch configuration. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 8c96932 | 0a187a4 | Updated universal base image (UBI) to resolve CVEs. |
| Key Management Service provider | v2.5.6 | v2.5.7 | Updated `Go` dependencies and to use `Go` version `1.18.4`. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1998 | 2058 | Updated image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.17 | 4.10.22 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-22){: external}. |
| OpenVPN client | 2.5.6-r0-IKS-592 | 2.5.6-r1-IKS-629 | Updated Alpine base image to version `3.16` to resolve CVEs. Updated OpenVPN to version `2.5.6-r1`. |
| OpenVPN Operator image | v1.4.6 | v1.4.7 | Updated Ansible operator base image to version `v1.22.1` to resolve CVEs. |
| OpenVPN server | 2.5.6-r0-IKS-591 | 2.5.6-r1-IKS-628 | Updated Alpine base image to version `3.16` to resolve CVEs. Updated OpenVPN to version `2.5.6-r1`. |
| Portieris admission controller | v0.12.4 | v0.12.5 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.12.5){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator | v4.10.0-20220614 | v4.10.0-20220712 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220712){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.10.0-20220614 | v4.10.0-20220712 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220712){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.10.0+20220614 | 4.10.0+20220712 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220712){: external}. |

{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.10.17_1524_openshift" caption-side="top"}

### Change log for worker node fix pack 4.10.21_1527_openshift, released 18 July 2022
{: #41021_1527_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.21_1527_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.66.1 | 3.10.0-1160.71.1 | Worker node package updates for [CVE-2020-26116](https://nvd.nist.gov/vuln/detail/CVE-2020-26116){: external},[CVE-2020-26137](https://nvd.nist.gov/vuln/detail/CVE-2020-26137){: external},[CVE-2021-3177](https://nvd.nist.gov/vuln/detail/CVE-2021-3177){: external},[CVE-2022-0391](https://nvd.nist.gov/vuln/detail/CVE-2022-0391){: external},[CVE-2022-1729](https://nvd.nist.gov/vuln/detail/CVE-2022-1729){: external},[CVE-2022-1966](https://nvd.nist.gov/vuln/detail/CVE-2022-1966){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.20 | 4.10.21 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-21){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.10.20_1526_openshift" caption-side="top"}

### Change log for worker node fix pack 4.10.20_1526_openshift, released 11 July 2022
{: #41020_1526_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.20_1526_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| General |N/A|N/A| Fix to address a bug that occurred if you used the persistent volume claim NFS v3 storage. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.10.20_1525_openshift" caption-side="top"}

### Change log for worker node fix pack 4.10.20_1525_openshift, released 05 July 2022
{: #41020_1525_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.20_1525_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.10.18 | 4.10.20 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-20){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.10.18_1523_openshift" caption-side="top"}

### Change log for master fix pack 4.10.17_1524_openshift, released 22 June 2022
{: #41017_1524_openshift}

The following table shows the changes that are in the master fix pack 4.10.17_1524_openshift. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.7 | v1.3.8 | Updated `Go` to version `1.17.11` and also updated the dependencies. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.4 | v2.2.6 | Bug fixes for the driver installation. Block plugin base images were updated to `ubi`: `8.6-751.1655117800` for CVE-2022-1271 |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.7-4 | v1.23.7-7 | Update module github.com/{{site.data.keyword.IBM_notm}}/vpc-go-sdk to `v0.20.0`. Update module github.com/stretchr/testify to `v1.7.2`. |
| Key Management Service provider | v2.5.5 | v2.5.6 | Updated `Go` to version `1.17.11` and also updated the dependencies. |
| OpenVPN Operator image | v1.4.5 | v1.4.6 | Update base image to version `v1.22.0` to resolve CVEs. |
| Red Hat {{site.data.keyword.openshiftshort}}. | 4.10.15 | 4.10.17 | See the [Red Hat {{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-17){: external}. |
| Red Hat {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.10.0-20220509 | v4.10.0-20220614 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0%2B20220614){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server and toolkit | v4.10.0-20220509 | v4.10.0-20220614 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0%2B20220614){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.10.15_1520_openshift" caption-side="top"}

### Change log for worker node fix pack 4.10.18_1523_openshift, released 20 June 2022
{: #41018_1523_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.18_1523_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}. |
| Haproxy | 468c09 | 04f862 | [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.16 | 4.10.18 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-18){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.10.16_1521_openshift" caption-side="top"}

### Change log for worker node fix pack 4.10.16_1521_openshift, released 7 June 2022
{: #41016_1521_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.16_1521_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-24903](https://nvd.nist.gov/vuln/detail/CVE-2022-24903){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.14 | 4.10.16 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-14){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.10.14_1519_openshift" caption-side="top"}

### Change log for master fix pack 4.10.15_1520_openshift, released 3 June 2022
{: #41015_1520_openshift}

The following table shows the changes that are in the master fix pack 4.10.15_1520_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.6 | v1.3.7 | Updated `Go` to version `1.17.10` and also updated the dependencies. Update registry base image version to `104` |
| {{site.data.keyword.IBM_notm}} Calico extension | 976 | 980 | Updated to use `Go` version `1.17.10`. Updated minimal UBI to version `8.5`. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.3 | v2.2.4 | Updated universal base image (UBI) to version `8.6-751` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.6-2 | v1.23.7-4 | Updated to support the Kubernetes `1.23.7` release and `Go` version `1.17.10` |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 408 | 410 | Updated universal base image (UBI) to version `8.6-751` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 8c8c82b | 8c96932 | Updated `Go` to version `1.18.1` |
| Key Management Service provider | v2.5.4 | v2.5.5 | Updated `Go` to version `1.17.10` and updated the golang dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1916 | 1998 | Updated `Go` to version `1.17.10` and updated dependencies. |
| OpenVPN Operator image | v1.4.4 | v1.4.5 | Updated base image to `v1.21.0` for CVE remediation. |
| Red Hat {{site.data.keyword.openshiftshort}}. | 4.10.12 | 4.10.15 | See the [Red Hat {{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-15){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.10.9_1515_openshift" caption-side="top"}

### Change log for worker node fix pack 4.10.14_1519_openshift, released 23 May 2022
{: #41014_1519_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.14_1519_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
|RHEL 7 Packages | 3.10.0-1160.62.1 | 3.10.0-1160.66.1 | Worker node kernel & package updates for [CVE-2018-25032](https://nvd.nist.gov/vuln/detail/CVE-2018-25032){: external}, [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}, [CVE-2022-0492](https://nvd.nist.gov/vuln/detail/CVE-2022-0492){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.12 | 4.10.14 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-14){: external}. |
| HA proxy | 36b0307 | 468c09 | [CVE-2021-3634](https://nvd.nist.gov/vuln/detail/CVE-2021-3634){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.10.12_1517_openshift" caption-side="top"}

### Change log for worker node fix pack 4.10.12_1517_openshift, released 09 May 2022
{: #41012_1517_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.12_1517_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | N/A |
| {{site.data.keyword.openshiftshort}}. | 4.10.10 | 4.10.12 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-12){: external}. |
| Haproxy | f53b22 | 36b030 | [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}, [CVE-2022-1154](https://nvd.nist.gov/vuln/detail/CVE-2022-1154){: external}, [CVE-2018-25032](https://nvd.nist.gov/vuln/detail/CVE-2018-25032){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.10.10_1516_openshift" caption-side="top"}

### Change log for fix pack 4.10.9_1515_openshift (master) and 4.10.10_1516_openshift (worker node), released 27 April 2022
{: #4109_1515_openshift_and_41010_1516_openshift}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.21.5 | v3.22.2 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases){: external}. |
| Calico Operator | v1.23.7 | v1.25.7 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.25.7){: external}. |
| IBM Cloud Controller Manager | v1.22.8-7 | v1.23.5-9 | Updated to support the Kubernetes `1.23.5` release and to use Go version `1.17.8`. Classic load balancers are updated to improve availability during updates. In addition, creating a mixed protocol load balancer is not supported. |
| OpenShift (master) | 4.9.28 | 4.10.9 | See the [OpenShift release notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-9){: external}. |
| OpenShift (worker) | 4.9.29 | 4.10.10 | See the [OpenShift release notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-10){: external}. Worker nodes are configured to pull images in parallel. |
| Red Hat OpenShift Control Plane Operator | v4.9.0-20220412 | v4.10.0-20220420 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220420){: external}. |
| Red Hat OpenShift configuration | N/A | N/A | Updated the [feature gate configuration](/docs/openshift?topic=openshift-service-settings#feature-gates). |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.9.0-20220412 | v4.10.0-20220420 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220420){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.9.0+20220412 | 4.10.0+20220420 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220420){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.28_1536_openshift master and 4.9.29_1537_openshift worker node" caption-side="top"}
