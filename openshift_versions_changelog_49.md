---

copyright:
  years: 2014, 2022
lastupdated: "2022-08-23"

keywords: openshift, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.redhat_openshift_notm}} version 4.9 change log
{: #openshift_changelog_49}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.9. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #openshift_changelog_overview_49}

Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features, which are subject to change, are disabled.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security) for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't also refer to an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_changelog).
{: tip}

## Change logs
{: #49_changelog}

Review the version 4.9 change log.
{: shortdesc}




























### Change log for worker node fix pack 4.9.45_1550_openshift, released 16 August 2022
{: #4945_1550_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.45_1550_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.71.1 | 3.10.0-1160.76.1 | Worker node package updates for [CVE-2022-0005](https://nvd.nist.gov/vuln/detail/CVE-2022-0005){: external},[CVE-2022-21123](https://nvd.nist.gov/vuln/detail/CVE-2022-21123){: external},[CVE-2022-21125](https://nvd.nist.gov/vuln/detail/CVE-2022-21125){: external},[CVE-2022-21127](https://nvd.nist.gov/vuln/detail/CVE-2022-21127){: external},[CVE-2022-21131](https://nvd.nist.gov/vuln/detail/CVE-2022-21131){: external},[CVE-2022-21136](https://nvd.nist.gov/vuln/detail/CVE-2022-21136){: external},[CVE-2022-21151](https://nvd.nist.gov/vuln/detail/CVE-2022-21151){: external},[CVE-2022-21166](https://nvd.nist.gov/vuln/detail/CVE-2022-21166){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.43 | 4.9.45 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-45){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.43_1549_openshift" caption-side="top"}

### Change log for worker node fix pack 4.9.43_1549_openshift, released 01 August 2022
{: #4943_1549_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.43_1549_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.9.42 | 4.9.43 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-43){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.42_1547_openshift" caption-side="top"}

### Change log for master fix pack 4.9.42_1548_openshift, released 26 July 2022
{: #4942_1548_openshift}

The following table shows the changes that are in the master fix pack 4.9.42_1548_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.8 | v1.3.9 | Updated `Go` dependencies and to use `Go` version `1.18.4`. Fixed minor typo in addon `daemonset not available` health status. |
| Gateway-enabled cluster controller | 1680 | 1792 | Updated to use `Go` version `1.17.11`. Updated image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external} and [CVE-2022-29458](https://nvd.nist.gov/vuln/detail/CVE-2022-29458){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 980 | 997 | Updated to use `Go` version `1.17.11`. Updated universal base image (UBI) to version `8.6-854` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.6 | v2.2.8 | Updated to use `Go` version `1.18.3`. Updated universal base image (UBI) to version `8.6-854` to resolve CVEs. Updated to support RHEL 8 worker nodes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.10-3 | v1.22.11-3 | Updated `Go` dependencies. Updated to support the Kubernetes `1.22.11` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 410 | 412 | Updated to use `Go` version `1.18.3`. Updated universal base image (UBI) to version `8.6-854` to resolve CVEs. Improved Kubernetes resource watch configuration. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 8c96932 | 0a187a4 | Updated universal base image (UBI) to resolve CVEs. |
| Key Management Service provider | v2.5.6 | v2.5.7 | Updated `Go` dependencies and to use `Go` version `1.18.4`. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1998 | 2058 | Updated image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.37 | 4.9.42 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-42){: external}. |
| OpenVPN client | 2.5.6-r0-IKS-592 | 2.5.6-r1-IKS-629 | Updated Alpine base image to version `3.16` to resolve CVEs. Updated OpenVPN to version `2.5.6-r1`. |
| OpenVPN Operator image | v1.4.6 | v1.4.7 | Updated Ansible operator base image to version `v1.22.1` to resolve CVEs. |
| OpenVPN server | 2.5.6-r0-IKS-591 | 2.5.6-r1-IKS-628 | Updated Alpine base image to version `3.16` to resolve CVEs. Updated OpenVPN to version `2.5.6-r1`. |
| Portieris admission controller | v0.12.4 | v0.12.5 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.12.5){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.9.0-20220614 | v4.9.0-20220712 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220712){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Metrics Server | v4.9.0-20220614 | v4.9.0-20220712 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220712){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} toolkit | 4.9.0+20220614 | 4.9.0+20220712 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220712){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.37_1544_openshift" caption-side="top"}

### Change log for worker node fix pack 4.9.42_1547_openshift, released 18 July 2022
{: #4942_1547_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.42_1547_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.66.1 | 3.10.0-1160.71.1 | Worker node package updates for [CVE-2020-26116](https://nvd.nist.gov/vuln/detail/CVE-2020-26116){: external},[CVE-2020-26137](https://nvd.nist.gov/vuln/detail/CVE-2020-26137){: external},[CVE-2021-3177](https://nvd.nist.gov/vuln/detail/CVE-2021-3177){: external},[CVE-2022-0391](https://nvd.nist.gov/vuln/detail/CVE-2022-0391){: external},[CVE-2022-1729](https://nvd.nist.gov/vuln/detail/CVE-2022-1729){: external},[CVE-2022-1966](https://nvd.nist.gov/vuln/detail/CVE-2022-1966){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.40 | 4.9.42 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-42){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.40_1546_openshift" caption-side="top"}

### Change log for worker node fix pack 4.9.40_1546_openshift, released 11 July 2022
{: #4940_1546_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.40_1546_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| General |N/A|N/A| Fix to address a bug that occurred if you used the persistent volume claim NFS v3 storage. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.40_1545_openshift" caption-side="top"}

### Change log for worker node fix pack 4.9.40_1545_openshift, released 05 July 2022
{: #4940_1545_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.40_1545_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.9.38 | 4.9.40 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-40){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.38_1543_openshift" caption-side="top"}

### Change log for master fix pack 4.9.37_1544_openshift, released 22 June 2022
{: #4937_1544_openshift}

The following table shows the changes that are in the master fix pack 4.9.37_1544_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.4 | v2.2.6 | Bug fixes for the driver installation. Block plugin base images were updated to `ubi`: `8.6-751.1655117800` for CVE-2022-1271 |
| Calico | v3.21.5 | v3.22.2 | See the [Calico release notes](https://projectcalico.docs.tigera.io/archive/v3.22/release-notes/#v3222){: external}. |
| Calico Operator | v1.23.7 | v1.25.7 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.25.7){: external}. |
| Cluster health image | v1.3.7 | v1.3.8 | Updated `Go` to version `1.17.11` and also updated the dependencies. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.10-1 | v1.22.10-3 | Update prometheus/client_golang@v1.11.0 to `v1.11.1`. |
| Key Management Service provider | v2.5.5 | v2.5.6 | Updated `Go` to version `1.17.11` and also updated the dependencies. |
| OpenVPN Operator image | v1.4.5 | v1.4.6 | Update base image to version `v1.22.0` to resolve CVEs. |
| {{site.data.keyword.openshiftshort}}. | 4.9.33 | 4.9.37 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-37){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.9.0-20220509 | v4.9.0-20220614 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0%2B20220614){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Metrics Server and toolkit | v4.9.0-20220509 | v4.9.0-20220614 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0%2B20220614){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.33_1540_openshift" caption-side="top"}

### Change log for worker node fix pack 4.9.38_1543_openshift, released 20 June 2022
{: #4938_1543_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.38_1543_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}. |
| Haproxy | 468c09 | 04f862 | [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.36 | 4.9.38 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-38){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.36_1541_openshift" caption-side="top"}

### Change log for worker node fix pack 4.9.36_1541_openshift, released 7 June 2022
{: #4936_1541_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.36_1541_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-24903](https://nvd.nist.gov/vuln/detail/CVE-2022-24903){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.33 | 4.9.36 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-36){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.33_1539_openshift" caption-side="top"}

### Change log for master fix pack 4.9.33_1540_openshift, released 3 June 2022
{: #4933_1540_openshift}

The following table shows the changes that are in the master fix pack 4.9.33_1540_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.6 | v1.3.7 | Updated `Go` to version `1.17.10` and also updated the dependencies. Update registry base image version to `104` |
| {{site.data.keyword.IBM_notm}} Calico extension | 954 | 980 | Updated to use `Go` version `1.17.10`. Updated minimal UBI to version `8.5`. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.2 | v2.2.4 | Updated universal base image (UBI) to version `8.6-751` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.8-7 | v1.22.10-1 | Updated to support the Kubernetes `1.22.10` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 408 | 410 | Updated universal base image (UBI) to version `8.6-751` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 8c8c82b | 8c96932 | Updated `Go` to version `1.18.1` |
| Key Management Service provider | v2.5.4 | v2.5.5 | Updated `Go` to version `1.17.10` and updated the golang dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1916 | 1998 | Updated `Go` to version `1.17.10` and updated dependencies. |
| OpenVPN Operator image | v1.4.3 | v1.4.5 | Updated base image to `v1.21.0` for CVE remediation. |
| {{site.data.keyword.openshiftshort}}. | 4.9.28 | 4.9.33 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-33){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.9.0-20220412 | v4.9.0-20220509 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220509){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Metrics Server | v4.9.0-20220412 | v4.9.0-20220509 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220509){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} toolkit | 4.9.0+20220412 | 4.9.0+20220509 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220509){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.28_1536_openshift" caption-side="top"}

### Change log for worker node fix pack 4.9.33_1539_openshift, released 23 May 2022
{: #4933_1539_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.33_1539_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.9.31 | 4.9.33 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-33){: external}. |
| RHEL 7 Packages | 3.10.0-1160.62.1 | 3.10.0-1160.66.1 | Worker node kernel & package updates for [CVE-2018-25032](https://nvd.nist.gov/vuln/detail/CVE-2018-25032){: external}, [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}, [CVE-2022-0492](https://nvd.nist.gov/vuln/detail/CVE-2022-0492){: external}. |
| HA proxy | 36b0307 | 468c09 | [CVE-2021-3634](https://nvd.nist.gov/vuln/detail/CVE-2021-3634){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.31_1538_openshift" caption-side="top"}

### Change log for worker node fix pack 4.9.31_1538_openshift, released 09 May 2022
{: #4931_1538_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.31_1538_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | N/A |
| {{site.data.keyword.openshiftshort}}. | 4.9.29 | 4.9.31 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-31){: external}. |
| Haproxy | f53b22 | 36b030 | [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}, [CVE-2022-1154](https://nvd.nist.gov/vuln/detail/CVE-2022-1154){: external}, [CVE-2018-25032](https://nvd.nist.gov/vuln/detail/CVE-2018-25032){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.29_1537_openshift" caption-side="top"}

### Change log for master fix pack 4.9.28_1536_openshift, released 26 April 2022
{: #4928_1536_openshift}

The following table shows the changes that are in the master fix pack 4.9.28_1536_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.21.4 | v3.21.5 | See the [Calico release notes](https://projectcalico.docs.tigera.io/archive/v3.21/release-notes/#v3215){: external}. |
| Calico Operator | v1.23.5 | v1.23.7 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.23.7){: external}. |
| Cluster health image | v1.3.5 | v1.3.6 | Updated `Go` to version `1.17.9` and also updated the dependencies. Update `registry base image` version to `103`. |
| Gateway-enabled cluster controller | 1669 | 1680 | Updated metadata for a rotated key. |
| {{site.data.keyword.IBM_notm}} Calico extension | 950 | 954 | Updated to latest UBI-minimal image to resolve [CVE-2021-3999](https://nvd.nist.gov/vuln/detail/CVE-2021-3999){: external}, [CVE-2022-23218](https://nvd.nist.gov/vuln/detail/CVE-2022-23218){: external}, [CVE-2022-23219](https://nvd.nist.gov/vuln/detail/CVE-2022-23219){: external}, [CVE-2022-23308](https://nvd.nist.gov/vuln/detail/CVE-2022-23308){: external}, [CVE-2021-23177](https://nvd.nist.gov/vuln/detail/CVE-2021-23177){: external}, and [CVE-2021-31566](https://nvd.nist.gov/vuln/detail/CVE-2021-31566){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.1 | v2.2.2 | Updated `ubi images` to `8.5-240.1648458092` |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.8-3 | v1.22.8-7 | Updated `vpcctl` to the `3003` binary image. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 407 | 408 | Fixed [CVE-2022-0778](https://nvd.nist.gov/vuln/detail/CVE-2022-0778){: external}. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 6c43ef1 | 8c8c82b | Updated `Go` to version `1.17.8` |
| Key Management Service provider | v2.5.3 | v2.5.4 | Moved to a different base image, version `102`, to reduce CVE footprint. Resolved [CVE-2022-0778](https://nvd.nist.gov/vuln/detail/CVE-2022-0778){: external}. |
| Load balancer and Load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1899 | 1916 | Updated the image to resolve CVEs. |
| OpenVPN client | 2.5.4-r0-IKS-579 | 2.5.6-r0-IKS-592 | Upgrade openvpn to version `2.5.6-r0`. |
| OpenVPN server | 2.5.4-r0-IKS-578 | 2.5.6-r0-IKS-591 | Upgrade openvpn to version `2.5.6-r0`. |
| OpenVPN Operator image | v1.4.2 | v1.4.3 | Updated ansible operator base image to version v1.19.0 to resolve CVEs. |
| Portieris admission controller | v0.12.3 | v0.12.4 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.12.4){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.25 | 4.9.28 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-28){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.9.0-20220322 | v4.9.0-20220412 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0%2B20220412){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Metrics Server | v4.9.0-20220322 | v4.9.0-20220412 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0%2B20220412){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} toolkit | 4.9.0+20220322 | 4.9.0+20220412 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0%2B20220412){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.25_1534_openshift" caption-side="top"}



### Change log for worker node fix pack 4.9.29_1537_openshift, released 25 April 2022
{: #4929_1537_openshift}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | Package updates. |
| {{site.data.keyword.openshiftshort}}. | 4.9.26 | 4.9.29 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-29){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.26_1535_openshift" caption-side="top"}





### Change log for worker node fix pack 4.9.26_1535_openshift, released 11 April 2022
{: #4926_1535_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.26_1535_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL Packages | 3.10.0-1160.59.1 | 3.10.0-1160.62.1 | Kernel and package updates for   [CVE-2021-45960](https://nvd.nist.gov/vuln/detail/CVE-2021-45960)   [CVE-2021-46143](https://nvd.nist.gov/vuln/detail/CVE-2021-46143)   [CVE-2022-22822](https://nvd.nist.gov/vuln/detail/CVE-2022-22822)   [CVE-2022-22823](https://nvd.nist.gov/vuln/detail/CVE-2022-22823)   [CVE-2022-22824](https://nvd.nist.gov/vuln/detail/CVE-2022-22824)   [CVE-2022-22825](https://nvd.nist.gov/vuln/detail/CVE-2022-22825)   [CVE-2022-22826](https://nvd.nist.gov/vuln/detail/CVE-2022-22826)   [CVE-2022-22827](https://nvd.nist.gov/vuln/detail/CVE-2022-22827)   [CVE-2022-23852](https://nvd.nist.gov/vuln/detail/CVE-2022-23852)   [CVE-2022-25235](https://nvd.nist.gov/vuln/detail/CVE-2022-25235)   [CVE-2022-25236](https://nvd.nist.gov/vuln/detail/CVE-2022-25236)   [CVE-2022-25315](https://nvd.nist.gov/vuln/detail/CVE-2022-25315)   [CVE-2021-4028](https://nvd.nist.gov/vuln/detail/CVE-2021-4028)   [CVE-2021-4083](https://nvd.nist.gov/vuln/detail/CVE-2021-4083)   [CVE-2022-0778](https://nvd.nist.gov/vuln/detail/CVE-2022-0778). |
| OpenShift | 4.9.25 | 4.9.26 | See [change logs](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-26){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.25_1532_openshift" caption-side="top"}





### Change log for master fix pack 4.9.25_1534_openshift, released 6 April 2022
{: #4.9.25_1534}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.3 | v1.3.5 | Update golang dependencies.  Update image to version 102 to fix CVEs [CVE-2021-3999](https://access.redhat.com/security/cve/cve-2021-3999){: external}, [CVE-2022-23218](https://nvd.nist.gov/vuln/detail/CVE-2022-23218){: external}, [CVE-2022-23219](https://nvd.nist.gov/vuln/detail/CVE-2022-23219){: external} |
| IBM Calico extension | 929 | 950 | Updated to use `Go` version `1.17.8`. Updated universal base image (UBI) to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.1.7 | v2.2.1 | Bug fixes for driver installation issues.  Updated ubi images to `8.5-240` and updated `Go` to version to `1.16.15`.  Fixes for CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.7-2 | v1.22.8-3 | Updated to support the Kubernetes 1.22.8 release and to use Go version 1.16.15. |
| {{site.data.keyword.cloud_notm}} File Storage plug-in and monitor | 405 | 407 | Updated `Go` to version `1.16.14`.  Updated `UBI` image to version `8.5-240`. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 0fc9949 | 6c43ef1 | Upgraded `Go` packages to resolve vulnerabilities |
| Gateway-enabled cluster controller | 1653 | 1669 | Updated to use `Go` version `1.17.8`. |
| Key Management Service provider | v2.5.2 | v2.5.3 | Updated to use `Go` version `1.17.8`. Updated golang dependencies.  Fixed CVE [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external} |
| Load balancer and Load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1747 | 1899 | Revert setting gratuitous arp on LBv1.  Updated the image to resolve CVEs. Updated to use `Go` version `1.17.8`. |
| Red Hat OpenShift | 4.9.21 | 4.9.25 | See the [Red Hat OpenShift release notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-25){: external} |
| Red hat OpenShift Control Plane Operator | v4.9.0-20220222 | v4.9.0-20220322 | See the [Red Hat OpenShift on {{site.data.keyword.cloud_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220322){: external}. |
| Red Hat OpenShift on {{site.data.keyword.cloud_notm}} Metrics Server | v4.9.0-20220222 | v4.9.0-20220322 | See the [Red Hat OpenShift on {{site.data.keyword.cloud_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220322){: external}. |
| Red Hat OpenShift on {{site.data.keyword.cloud_notm}} toolkit | 4.9.0+20220222 | 4.9.0+20220322 | See the [Red Hat OpenShift on {{site.data.keyword.cloud_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220322){: external}. |
| OpenVPN client | 2.5.4-r0-IKS-556 | 2.5.4-r0-IKS-579 | Updated `Go` to version `1.16.15`. |
| OpenVPN server | 2.5.4-r0-IKS-562 | 2.5.4-r0-IKS-578 | Updated `Go` to version `1.16.15`. |
| OpenVPN Operator image | v1.4.1 | v1.4.2 | Updated ansible operator base image to version `v1.18.0` to resolve CVEs. |
| Portieris admission controller | v0.12.2 | v0.12.3 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.12.3){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.21_1528_openshift" caption-side="top"}








### Change log for worker node pack 4.9.25_1532_openshift, released 28 March 2022
{: #4925_1532}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | N/A |
| HA proxy | 15198f | b40c07 | [CVE-2021-45960](https://nvd.nist.gov/vuln/detail/CVE-2021-45960){: external}, [CVE-2021-46143](https://nvd.nist.gov/vuln/detail/CVE-2021-46143){: external}, [CVE-2022-22822](https://nvd.nist.gov/vuln/detail/CVE-2022-22822){: external}, [CVE-2022-22823](https://nvd.nist.gov/vuln/detail/CVE-2022-22823){: external}, [CVE-2022-22824](https://nvd.nist.gov/vuln/detail/CVE-2022-22824){: external}, [CVE-2022-22825](https://nvd.nist.gov/vuln/detail/CVE-2022-22825){: external}, [CVE-2022-22826](https://nvd.nist.gov/vuln/detail/CVE-2022-22826){: external}, [CVE-2022-22827](https://nvd.nist.gov/vuln/detail/CVE-2022-22827){: external}, [CVE-2022-23852](https://nvd.nist.gov/vuln/detail/CVE-2022-23852){: external}, [CVE-2022-25235](https://nvd.nist.gov/vuln/detail/CVE-2022-25235){: external}, [CVE-2022-25236](https://nvd.nist.gov/vuln/detail/CVE-2022-25236){: external}, [CVE-2022-25315](https://nvd.nist.gov/vuln/detail/CVE-2022-25315){: external}, [CVE-2021-3999](https://nvd.nist.gov/vuln/detail/CVE-2021-3999){: external}, [CVE-2022-23218](https://nvd.nist.gov/vuln/detail/CVE-2022-23218){: external}, [CVE-2022-23219](https://nvd.nist.gov/vuln/detail/CVE-2022-23219){: external}, [CVE-2022-23308](https://nvd.nist.gov/vuln/detail/CVE-2022-23308){: external}, [CVE-2021-23177](https://nvd.nist.gov/vuln/detail/CVE-2021-23177){: external}, [CVE-2021-31566](https://nvd.nist.gov/vuln/detail/CVE-2021-31566){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.9.23 | 4.9.25 | See [change logs](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-25){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.23_1530_openshift_openshift" caption-side="top"}





### Change log for worker node pack 4.9.23_1530_openshift, released 14 March 2022
{: #4923_1530}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | N/A |
| {{site.data.keyword.redhat_openshift_notm}} | 4.9.22 | 4.9.23 | See the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-23){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.22_1529_openshift" caption-side="top"}






### Change log for master fix pack 4.9.21_1528_openshift, released 3 March 2022
{: #4921_1528}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.0 | v1.3.3 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds fix for [CVE-2021-43565](https://www.mend.io/vulnerability-database/CVE-2021-43565){: external}. Adds Golang dependency updates. |
| Gateway-enabled cluster controller | 1586 | 1653 | Updated to use `Go` version `1.17.7` and updated `Go` modules to fix CVEs. |
| {{site.data.keyword.IBM_notm}} Calico extension | 923 | 929 | Updated universal base image (UBI) to the `8.5-230` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | v2.1.6 | v2.1.7 | Fix for [CVE-2021-3538](https://www.mend.io/vulnerability-database/CVE-2021-3538){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.6-1 | v1.22.7-2 | Updated to support the Kubernetes `1.22.7` release and to use `Go` version `1.16.14`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 404 | 405 | Adds fix for [CVE-2021-3538](https://www.mend.io/vulnerability-database/CVE-2021-3538){: external} and adds dependency updates. |
| Key Management Service provider | v2.4.0 | v2.5.2 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds fix for [CVE-2021-43565](https://www.mend.io/vulnerability-database/CVE-2021-43565){: external}. Adds Golang dependency updates. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.9.17 | 4.9.21 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-21){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.9.0-20220201 | v4.9.0-20220222 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220222){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Metrics Server | v4.9.0-20220201 | v4.9.0-20220222 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220222){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} toolkit | 4.9.0+20220201 | 4.9.0+20220222 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220222){: external}. |
| OpenVPN server | 2.5.4-r0-IKS-555 | 2.5.4-r0-IKS-562 | Turns off CRL verification in the openvpn image. |
| OpenVPN Operator image | v1.4.0 | v1.4.1 | Turns off CRL verification in the opevpn-operator image. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.17_1525_openshift" caption-side="top"}






### Change log for worker node fix pack 4.9.22_1529_openshift, released 28 February 2022
{: #4922_1529}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.53.1.el7 | 3.10.0-1160.59.1.el7 | Kernel and package updates for [CVE-2020-25709](https://nvd.nist.gov/vuln/detail/CVE-2020-25709){: external}, [CVE-2020-25710](https://nvd.nist.gov/vuln/detail/CVE-2020-25710){: external}, [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}, [CVE-2020-0465](https://nvd.nist.gov/vuln/detail/CVE-2020-0465){: external}, [CVE-2020-0466](https://nvd.nist.gov/vuln/detail/CVE-2020-0466){: external}, [CVE-2021-0920](https://nvd.nist.gov/vuln/detail/CVE-2021-0920){: external}, [CVE-2021-3564](https://nvd.nist.gov/vuln/detail/CVE-2021-3564){: external}, [CVE-2021-3573](https://nvd.nist.gov/vuln/detail/CVE-2021-3573){: external}, [CVE-2021-3752](https://nvd.nist.gov/vuln/detail/CVE-2021-3752){: external}, [CVE-2021-4155](https://nvd.nist.gov/vuln/detail/CVE-2021-4155){: external}, [CVE-2022-0330](https://nvd.nist.gov/vuln/detail/CVE-2022-0330){: external}, [CVE-2022-22942](https://nvd.nist.gov/vuln/detail/CVE-2022-22942){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.9.19 | 4.9.22 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-22){: external} | 
| HA proxy | f6a2b3 | 15198fb | Contains fixes for [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}. | 
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.19_1526_openshift" caption-side="top"}






### Change log for worker node fix pack 4.9.19_1526_openshift, released 14 February 2022
{: #4919_1526}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | N/A |
| {{site.data.keyword.redhat_openshift_notm}} | N/A | 4.9.19 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-19){: external}. |
| HA proxy | d38fa1 | f6a2b3 | [CVE-2021-3521](https://nvd.nist.gov/vuln/detail/CVE-2021-3521){: external}, [CVE-2021-4122](https://nvd.nist.gov/vuln/detail/CVE-2021-4122){: external}. |
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
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.8.0-20220107 | v4.9.0-20220201 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220201){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} configuration | N/A | N/A | Updated the [feature gate configuration](/docs/openshift?topic=openshift-service-settings#feature-gates). Added new `ibm-admin` flow schema to default [Kubernetes API priority and fairness configuration](/docs/openshift?topic=openshift-kubeapi-priority). |
| Pause container image | 3.5 | 3.6 | See the [pause container image release notes](https://github.com/kubernetes/kubernetes/blob/master/build/pause/CHANGELOG.md){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Metrics Server | v4.8.0-20220107 | v4.9.0-20220201 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220201){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} toolkit | 4.8.0+20220107 | 4.9.0+20220201 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220201){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.8.26_1542_openshift master and 4.8.28_1543_openshift worker node." caption-side="top"}

