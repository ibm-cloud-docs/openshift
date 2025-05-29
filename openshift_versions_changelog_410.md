---

copyright:
  years: 2022, 2025
lastupdated: "2025-05-29"


keywords: openshift, 4.10, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# Version 4.10 change log
{: #openshift_changelog_410}



This version is no longer supported. Update your cluster to a [supported version](/docs/openshift?topic=openshift-openshift_versions) as soon as possible.
{: important}



View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.10. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}



## Overview
{: #openshift_changelog_overview_410}

Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features, which are subject to change, are disabled.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security) for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}


## Change logs
{: #410_changelog}


Review the version 4.10 change log.
{: shortdesc}


### Worker node fix pack 4.10.67_1597_openshift, released 29 January 2024
{: #41067_1597_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.67_1597_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.10.67 | 4.10.67 | N/A |
| Rhel8 Packages | 4.18.0-477.27.1.el8_8 | 4.18.0-477.27.1.el8_8 | N/A |
| HAProxy | e105dc | a13673 | Security fixes for [CVE-2023-7104](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-7104){: external}, [CVE-2023-27043](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-27043){: external}. |
{: caption="Changes since version 4.10.67_1596_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.67_1596_openshift, released 16 January 2024
{: #41067_1596_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.67_1596_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.10.67 | 4.10.67 | N/A |
| RHEL 8 Packages | N/A | N/A | N/A |
| Haproxy | 3060b0 | e105dc | [CVE-2023-39615](https://nvd.nist.gov/vuln/detail/CVE-2023-39615){: external}, [CVE-2023-5981](https://nvd.nist.gov/vuln/detail/CVE-2023-5981){: external}, [CVE-2022-48560](https://nvd.nist.gov/vuln/detail/CVE-2022-48560){: external}, [CVE-2022-48564](https://nvd.nist.gov/vuln/detail/CVE-2022-48564){: external}. |
{: caption="Changes since version 4.10.67_1595_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.67_1595_openshift, released 02 January 2024
{: #41067_1595_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.67_1595_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.10.67 | 4.10.67 | N/A |
| RHEL 8 Packages | 4.18.0-477.27.1.el8_8 | 4.18.0-477.27.1.el8_8 | N/A |
{: caption="Changes since version 4.10.67_1594_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.67_1594_openshift, released 18 December 2023
{: #41067_1594_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.67_1594_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | N/A |N/A|N/A|
| RHEL 8 Packages | N/A |N/A|N/A |
{: caption="Changes since version 4.10.67_1593_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.67_1593_openshift, released 04 December 2023
{: #41067_1593_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.67_1593_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.10.67 | 4.10.67 | N/A |
| RHEL 8 Packages | N/A | N/A | N/A |
{: caption="Changes since version 4.10.67_1592_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.67_1592_openshift, released 29 November 2023
{: #41067_1592_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.67_1592_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.10.67 | 4.10.67 |N/A|
| CRI-O | 1.23.5 | 1.23.5 | Unqualified image registry aliases updated for `address-parsing-service`, `admin-site`, `apache-tika`, `auto-update-service`, `config-service`, `data-integration-service`, `dataprovider-manager-service`, `data-service`, `documents-service`, `gate-service`, `gateway-service`, `icij-db`, `identity-service`, `internet-access-service`, `mongo`, `notes-service`, `public-api-service`, `router`, and `search-service`. However, using short names are not supported due to security risks, https://access.redhat.com/solutions/6178442. |
| RHEL 8 Packages |N/A|N/A|N/A|
{: caption="Changes since version 4.10.67_1590_openshift" caption-side="bottom"}


### Master fix pack 4.10.67_1591_openshift, released 15 November 2023
{: #41067_1591_openshift_M}

The following table shows the changes that are in the master fix pack 4.10.67_1591_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 435 | 438 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | f0d3265 | e544e35 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2681 | 2731 | New version contains updates and security fixes. |
| OpenVPN client | 2.6.5-r0-IKS-66 | 2.6.5-r0-IKS-77 | New version contains updates and security fixes. |
| OpenVPN server | 2.6.5-r0-IKS-57 | 2.6.5-r0-IKS-76 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.4.28 | v1.4.30 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.8 | v0.13.10 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.10){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.10.0-20231010 | v4.10.0-20231102 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0%2B20231102){: external}. |
{: caption="Changes since version 4.10.67_1588_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.67_1590_openshift, released 08 November 2023
{: #41067_1590_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.67_1590_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}|N/A|N/A|N/A|
{: caption="Changes since version 4.10.67_1589_openshift" caption-side="bottom"}


### Master fix pack 4.10.67_1588_openshift, released 25 October 2023
{: #41067_1588_openshift_M}

The following table shows the changes that are in the master fix pack 4.10.67_1588_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.IBM_notm}} Calico extension | 1390 | 1487 | New version contains security fixes. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.10 | v2.4.12 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 4e2f346 | f0d3265 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.4.27 | v1.4.28 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.6 | v0.13.8 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.8){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.10.0-20230811 | v4.10.0-20231010 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0%2B20231010){: external}. |
{: caption="Changes since version 4.10.67_1585_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.67_1589_openshift, released 23 October 2023
{: #41067_1589_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.67_1589_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. |N/A|N/A|N/A|
| RHEL 8 Packages |N/A|N/A| Worker node package update for [CVE-2023-44487](https://nvd.nist.gov/vuln/detail/CVE-2023-44487){: external}. |
{: caption="Changes since version 4.10.67_1587_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.67_1587_openshift, released 9 October 2023
{: #41067_1587_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.67_1587_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. |N/A|N/A| N/A |
| RHEL 8 Packages | N/A | N/A | Worker node package updates for [CVE-2023-3341](https://nvd.nist.gov/vuln/detail/CVE-2023-3341){: external}, [CVE-2023-4527](https://nvd.nist.gov/vuln/detail/CVE-2023-4527){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [CVE-2023-4806](https://nvd.nist.gov/vuln/detail/CVE-2023-4806){: external}, [CVE-2023-4813](https://nvd.nist.gov/vuln/detail/CVE-2023-4813){: external}, [CVE-2023-4911](https://nvd.nist.gov/vuln/detail/CVE-2023-4911){: external}. |
{: caption="Changes since version 4.10.67_1586_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.67_1586_openshift, released 27 September 2023
{: #41067_1586_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.67_1586_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.10.67 | 4.10.67 | No Change |
| RHEL 8 Packages | 4.18.0-477.21.1.el8_8 | 4.18.0-477.27.1.el8_8 | Worker node kernel & package updates for [CVE-2023-2002](https://nvd.nist.gov/vuln/detail/CVE-2023-2002){: external}, [CVE-2023-3090](https://nvd.nist.gov/vuln/detail/CVE-2023-3090){: external}, [CVE-2023-3390](https://nvd.nist.gov/vuln/detail/CVE-2023-3390){: external}, [CVE-2023-3776](https://nvd.nist.gov/vuln/detail/CVE-2023-3776){: external}, [CVE-2023-4004](https://nvd.nist.gov/vuln/detail/CVE-2023-4004){: external}, [CVE-2023-20593](https://nvd.nist.gov/vuln/detail/CVE-2023-20593){: external}, [CVE-2023-29491](https://nvd.nist.gov/vuln/detail/CVE-2023-29491){: external}, [CVE-2023-30630](https://nvd.nist.gov/vuln/detail/CVE-2023-30630){: external}, [CVE-2023-35001](https://nvd.nist.gov/vuln/detail/CVE-2023-35001){: external}, [CVE-2023-35788](https://nvd.nist.gov/vuln/detail/CVE-2023-35788){: external}. |
{: caption="Changes since version 4.10.67_1582_openshift" caption-side="bottom"}


### Master fix pack 4.10.67_1585_openshift, released 20 September 2023
{: #41067_1585_openshift_M}

The following table shows the changes that are in the master fix pack 4.10.67_1585_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.25.1 | v3.25.2 | See the [Calico release notes](https://archive-os-3-25.netlify.app/calico/3.25/release-notes/){: external}. |
| Tigera Operator | v1.29.4 | v1.29.6 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.29.6){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.5 | v2.4.10 | Updated `Go dependencies`. Updated to newer UBI base image. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.17-25 | v1.23.17-26 | Updated `Go dependencies`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 434 | 435 | Updated `Go` to version `1.20.6` and updated dependencies. Updated to newer UBI base image. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2631 | 2681 | Updated `Go` to version `1.19.12` and updated `Go dependencies`. |
| {{site.data.keyword.openshiftlong_notm}} | 4.10.65 | 4.10.67 | Resolves [CVE-2023-1260](https://nvd.nist.gov/vuln/detail/CVE-2023-1260){: external}. For more information, see the [IBM security bulletin](https://www.ibm.com/support/pages/node/7052832){: external}. See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-67){: external}. |
{: caption="Changes since version 4.10.65_1580_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.67_1582_openshift, released 12 September 2023
{: #41067_1582_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.67_1582_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.10.66 | 4.10.67| For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-67){: external}. |
| RHEL 8 Packages | N/A | N/A | Package updates for [CVE-2022-40982](https://nvd.nist.gov/vuln/detail/CVE-2022-40982){: external}, [CVE-2022-41804](https://nvd.nist.gov/vuln/detail/CVE-2022-41804){: external}, [CVE-2023-23908](https://nvd.nist.gov/vuln/detail/CVE-2023-23908){: external}. |
{: caption="Changes since version 4.10.66_1581_openshift" caption-side="bottom"}


### Master fix pack 4.10.65_1580_openshift, released 30 August 2023
{: #41065_1580_openshift_M}

The following table shows the changes that are in the master fix pack 4.10.65_1580_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.23 | v1.3.24 | Updated `Go` to version `1.19.12` and updated dependencies. Updated base image version to 378. |
| etcd | v3.4.26 | v3.4.27 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.27){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.17-22 | v1.23.17-25 | Updated `Go` dependencies to resolve a CVE. Updates to Travis build. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 433 | 434 | Updated `Go` to version `1.20.6` and updated dependencies. Updated to newer UBI base image. |
| Key Management Service provider | v2.7.2 | v2.7.3 | Updated `Go` dependencies. |
| OpenVPN client | 2.6.5-r0-IKS-41-amd64 | 2.6.5-r0-IKS-66-amd64 | Updated `openvpn` components to fix CVEs. |
| OpenVPN server | 2.6.5-r0-IKS-40-amd64 | 2.6.5-r0-IKS-57-amd64 | Updated `openvpn` components to fix CVEs. |
| OpenVPN Operator image | v1.4.26 | v1.4.27 | Updated `ansible-operator` version to `1.30.0` |
| Portieris admission controller | v0.13.5 | v0.13.6 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.6){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.10.63 | 4.10.65 | https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-65 |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.10.0-20230710 | v4.10.0-20230811 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0%2B20230811){: external}. |
{: caption="Changes since version 4.10.63_1577_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.66_1581_openshift, released 28 August 2023
{: #41066_1581_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.66_1581_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.10.65 | 4.10.66| For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-66){: external}. |
{: caption="Changes since version 4.10.65_1579_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.65_1579_openshift, released 15 August 2023
{: #41065_1579_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.65_1579_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.10.64 | 4.10.65 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-65){: external}. |
| RHEL 7 Packages| 3.10.0-1160.92.1.el7 | 3.10.0-1160.95.1.el7 | Worker node kernel & package updates for [CVE-2023-38408](https://nvd.nist.gov/vuln/detail/CVE-2023-38408){: external}, [CVE-2022-3564](https://nvd.nist.gov/vuln/detail/CVE-2022-3564){: external}. |
| RHEL 8 Packages| 4.18.0-477.15.1.el8_8 | 4.18.0-477.21.1.el8_8 | Worker node kernel & package updates for [CVE-2022-42896](https://nvd.nist.gov/vuln/detail/CVE-2022-42896){: external}, [CVE-2023-1281](https://nvd.nist.gov/vuln/detail/CVE-2023-1281){: external}, [CVE-2023-1829](https://nvd.nist.gov/vuln/detail/CVE-2023-1829){: external}, [CVE-2023-2124](https://nvd.nist.gov/vuln/detail/CVE-2023-2124){: external}, [CVE-2023-2194](https://nvd.nist.gov/vuln/detail/CVE-2023-2194){: external}, [CVE-2023-2235](https://nvd.nist.gov/vuln/detail/CVE-2023-2235){: external}, [CVE-2023-2602](https://nvd.nist.gov/vuln/detail/CVE-2023-2602){: external}, [CVE-2023-2603](https://nvd.nist.gov/vuln/detail/CVE-2023-2603){: external}, [CVE-2023-27536](https://nvd.nist.gov/vuln/detail/CVE-2023-27536){: external}, [CVE-2023-28321](https://nvd.nist.gov/vuln/detail/CVE-2023-28321){: external}, [CVE-2023-28484](https://nvd.nist.gov/vuln/detail/CVE-2023-28484){: external}, [CVE-2023-29469](https://nvd.nist.gov/vuln/detail/CVE-2023-29469){: external}, [CVE-2023-32681](https://nvd.nist.gov/vuln/detail/CVE-2023-32681){: external}, [CVE-2023-34969](https://nvd.nist.gov/vuln/detail/CVE-2023-34969){: external}, [CVE-2023-38408](https://nvd.nist.gov/vuln/detail/CVE-2023-38408){: external}. |
{: caption="Changes since version 4.10.64_1578_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.64_1578_openshift, released 1 August 2023
{: #41064_1578_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.64_1578_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.10.63 | 4.10.64 | For more information, see the [change logs](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-64){: external}. |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-3564](https://nvd.nist.gov/vuln/detail/CVE-2022-3564){: external}, [CVE-2023-2828](https://nvd.nist.gov/vuln/detail/CVE-2023-2828){: external}, [CVE-2023-32233](https://nvd.nist.gov/vuln/detail/CVE-2023-32233){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node package update for [CVE-2023-2828](https://nvd.nist.gov/vuln/detail/CVE-2023-2828){: external}. |
{: caption="Changes since version 4.10.63_1576_openshift" caption-side="bottom"}


### Master fix pack 4.10.63_1577_openshift, released 28 July 2023
{: #41063_1577_openshift_M}

The following table shows the changes that are in the master fix pack 4.10.63_1577_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.21 | v1.3.23 | Updated `Go` to version `1.19.11` and updated `Go` dependencies. Updated UBI base image. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.17-19 | v1.23.17-22 | Updated `Go` dependencies. |
| Key Management Service provider | v2.6.7 | v2.7.2 | Updated `Go` to version `1.19.11` and updated `Go` dependencies. Updated UBI base image. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2584 | 2631 | Updated `Go` to version `1.19.10` and updated `Go` dependencies. Updated Alpine base image. |
| OpenVPN client | 2.6.4-r0-IKS-34-amd64 | 2.6.5-r0-IKS-41-amd64 | Updated `OpenVPN` to version `2.6.5`. |
| OpenVPN Operator image | v1.4.25 | v1.4.26 | Updated based image to resolve [CVE-2023-24329](https://nvd.nist.gov/vuln/detail/CVE-2023-24329){: external}, [CVE-2020-24736](https://nvd.nist.gov/vuln/detail/CVE-2020-24736){: external}, [CVE-2023-26604](https://nvd.nist.gov/vuln/detail/CVE-2023-26604){: external}, [CVE-2023-1667](https://nvd.nist.gov/vuln/detail/CVE-2023-1667){: external}, and [CVE-2023-2283](https://nvd.nist.gov/vuln/detail/CVE-2023-2283){: external}. |
| OpenVPN server | 2.6.4-r0-IKS-33-amd64 | 2.6.5-r0-IKS-40-amd64 | Updated `OpenVPN` to version `2.6.5`. |
| {{site.data.keyword.openshiftshort}}. | 4.10.61 | 4.10.63 | See the [{{site.data.keyword.openshiftshort}} release notes.](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator and Metrics Server | v4.10.0-20230417 | v4.10.0-20230710 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20230710){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.10.0+20230417 | 4.10.0+20230710 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20230710){: external}. |
{: caption="Changes since version 4.10.61_1574_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.63_1576_openshift, released 17 July 2023
{: #41063_1576_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.63_1576_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.10.62 |4.10.63| [See change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-63){: external}. |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages |N/A|N/A|N/A|
{: caption="Changes since version 4.10.62_1575_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.62_1575_openshift, released 03 July 2023
{: #41062_1575_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.62_1575_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.10.61 | 4.10.62 | see [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-62){: external}. |
{: caption="Changes since version 4.10.61_1572_openshift" caption-side="bottom"}


### Master fix pack 4.10.61_1574_openshift, released 27 June 2023
{: #41061_1574_openshift_M}

The following table shows the changes that are in the master fix pack 4.10.61_1574_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.23.5 | v3.25.1 | See the [Calico release notes](https://archive-os-3-25.netlify.app/calico/3.25/release-notes/){: external}. |
| Tigera Operator | v1.27.17 | v1.29.4 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.29.4){: external}. |
| Cluster health image | v1.3.20 | v1.3.21 | Updated `Go` dependencies and to `Go` version `1.19.10`. |
| etcd | v3.4.25 | v3.4.26 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.26){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.17-16 | v1.23.17-19 | Updated to support the `Kubernetes 1.23.17` release. Updated `Go` dependencies. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 431 | 433 | Updated `Go` to version `1.20.4`. Updated UBI base image. |
| Key Management Service provider | v2.6.6 | v2.6.7 | Updated `Go` dependencies and to `Go` version `1.19.10`. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2486 | 2584 | Updated `Go` dependencies and to `Go` version `1.19.9`. Updated base image. |
| {{site.data.keyword.openshiftshort}} | 4.10.59 | 4.10.61 | https://docs.openshift.com/container-platform/ |
| OpenVPN client | 2.5.8-r0-IKS-674-amd64 | 2.6.4-r0-IKS-34-amd64 | Upgrade `openvpn` to version `2.6.4-r0`. |
| OpenVPN server | 2.5.8-r0-IKS-673-amd64 | 2.6.4-r0-IKS-33-amd64 | Upgrade `openvpn` to version `2.6.4-r0`. |
| OpenVPN Operator image | v1.4.23 | v1.4.25 | Updated OpenVPN configuration to provide shutdown grace period before terminating connections. |
{: caption="Changes since version 4.10.59_1570_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.61_1572_openshift, released 19 June 2023
{: #41061_1572_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.61_1572_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. |4.10.60|4.10.61|For more information, see the [change logs](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-61){: external}. |
| RHEL 8 Packages | N/A | N/A | Worker node package updates for [CVE-2023-32067](https://nvd.nist.gov/vuln/detail/CVE-2023-32067){: external},[CVE-2023-24329](https://nvd.nist.gov/vuln/detail/CVE-2023-24329){: external}. |
{: caption="Changes since version 4.10.60_1571_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.60_1571_openshift, released 5 June 2023
{: #41060_1571_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.60_1571_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.10.59 | 4.10.60 | For more information, see the [change logs](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-60){: external}. |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-477.10.1.el8_8 | 4.18.0-477.13.1.el8_8 | Worker node kernel & package updates for [CVE-2023-22490](https://nvd.nist.gov/vuln/detail/CVE-2023-22490){: external}, [CVE-2023-23946](https://nvd.nist.gov/vuln/detail/CVE-2023-23946){: external}, [CVE-2023-25652](https://nvd.nist.gov/vuln/detail/CVE-2023-25652){: external}, [CVE-2023-25815](https://nvd.nist.gov/vuln/detail/CVE-2023-25815){: external}, [CVE-2023-29007](https://nvd.nist.gov/vuln/detail/CVE-2023-29007){: external}, [CVE-2023-32233](https://nvd.nist.gov/vuln/detail/CVE-2023-32233){: external}. |
{: caption="Changes since version 4.10.59_1569_openshift" caption-side="bottom"}


### Master fix pack 4.10.59_1570_openshift, released 25 May 2023
{: #41059_1570_openshift_M}

The following table shows the changes that are in the master fix pack 4.10.59_1570_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.19 | v1.3.20 | Updated `Go` to version `1.19.9` and updated dependencies. Updated the base image. Resolved add-on health bugs. |
| etcd | v3.4.24 | v3.4.25 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.25){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.17-10 | v1.23.17-16 | Updated support of the Kubernetes 1.23.17 release. Updated Go dependencies. Key rotation. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 778ef2b | 4e2f346 | Make armada-rbac-sync FIPS compliant |
| Key Management Service provider | v2.6.5 | v2.6.6 | Updated `Go` to version `1.19.9` and updated dependencies. |
| OpenVPN client | 2.6.4-r0-IKS-27 | 2.5.8-r0-IKS-674 | Reverted to previous version. |
| OpenVPN server | 2.6.4-r0-IKS-26 | 2.5.8-r0-IKS-673 | Reverted to previous version. |
| Portieris admission controller | v0.13.4 | v0.13.5 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.5){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.10.56 | 4.10.59 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-59){: external}. |
{: caption="Changes since version 4.10.56_1565_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.59_1569_openshift, released 23 May 2023
{: #41059_1569_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.59_1569_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | N/A |N/A|N/A|
| RHEL 8 Packages | 4.18.0-425.19.2.el8_7 | 4.18.0-477.10.1.el8_8 | Worker node kernel & package updates for [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-26341](https://nvd.nist.gov/vuln/detail/CVE-2021-26341){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2021-33655](https://nvd.nist.gov/vuln/detail/CVE-2021-33655){: external}, [CVE-2021-33656](https://nvd.nist.gov/vuln/detail/CVE-2021-33656){: external}, [CVE-2022-1462](https://nvd.nist.gov/vuln/detail/CVE-2022-1462){: external}, [CVE-2022-1679](https://nvd.nist.gov/vuln/detail/CVE-2022-1679){: external}, [CVE-2022-1705](https://nvd.nist.gov/vuln/detail/CVE-2022-1705){: external}, [CVE-2022-1789](https://nvd.nist.gov/vuln/detail/CVE-2022-1789){: external}, [CVE-2022-1962](https://nvd.nist.gov/vuln/detail/CVE-2022-1962){: external}, [CVE-2022-20141](https://nvd.nist.gov/vuln/detail/CVE-2022-20141){: external}, [CVE-2022-2196](https://nvd.nist.gov/vuln/detail/CVE-2022-2196){: external}, [CVE-2022-24765](https://nvd.nist.gov/vuln/detail/CVE-2022-24765){: external}, [CVE-2022-25265](https://nvd.nist.gov/vuln/detail/CVE-2022-25265){: external}, [CVE-2022-2663](https://nvd.nist.gov/vuln/detail/CVE-2022-2663){: external}, [CVE-2022-27664](https://nvd.nist.gov/vuln/detail/CVE-2022-27664){: external}, [CVE-2022-2795](https://nvd.nist.gov/vuln/detail/CVE-2022-2795){: external}, [CVE-2022-28131](https://nvd.nist.gov/vuln/detail/CVE-2022-28131){: external}, [CVE-2022-29187](https://nvd.nist.gov/vuln/detail/CVE-2022-29187){: external}, [CVE-2022-2928](https://nvd.nist.gov/vuln/detail/CVE-2022-2928){: external}, [CVE-2022-2929](https://nvd.nist.gov/vuln/detail/CVE-2022-2929){: external}, [CVE-2022-3028](https://nvd.nist.gov/vuln/detail/CVE-2022-3028){: external}, [CVE-2022-30594](https://nvd.nist.gov/vuln/detail/CVE-2022-30594){: external}, [CVE-2022-30629](https://nvd.nist.gov/vuln/detail/CVE-2022-30629){: external}, [CVE-2022-30630](https://nvd.nist.gov/vuln/detail/CVE-2022-30630){: external}, [CVE-2022-30631](https://nvd.nist.gov/vuln/detail/CVE-2022-30631){: external}, [CVE-2022-30632](https://nvd.nist.gov/vuln/detail/CVE-2022-30632){: external}, [CVE-2022-30633](https://nvd.nist.gov/vuln/detail/CVE-2022-30633){: external}, [CVE-2022-30635](https://nvd.nist.gov/vuln/detail/CVE-2022-30635){: external}, [CVE-2022-32148](https://nvd.nist.gov/vuln/detail/CVE-2022-32148){: external}, [CVE-2022-32189](https://nvd.nist.gov/vuln/detail/CVE-2022-32189){: external}, [CVE-2022-3239](https://nvd.nist.gov/vuln/detail/CVE-2022-3239){: external}, [CVE-2022-3522](https://nvd.nist.gov/vuln/detail/CVE-2022-3522){: external}, [CVE-2022-3524](https://nvd.nist.gov/vuln/detail/CVE-2022-3524){: external}, [CVE-2022-35252](https://nvd.nist.gov/vuln/detail/CVE-2022-35252){: external}, [CVE-2022-3564](https://nvd.nist.gov/vuln/detail/CVE-2022-3564){: external}, [CVE-2022-3566](https://nvd.nist.gov/vuln/detail/CVE-2022-3566){: external}, [CVE-2022-3567](https://nvd.nist.gov/vuln/detail/CVE-2022-3567){: external}, [CVE-2022-3619](https://nvd.nist.gov/vuln/detail/CVE-2022-3619){: external}, [CVE-2022-36227](https://nvd.nist.gov/vuln/detail/CVE-2022-36227){: external}, [CVE-2022-3623](https://nvd.nist.gov/vuln/detail/CVE-2022-3623){: external}, [CVE-2022-3625](https://nvd.nist.gov/vuln/detail/CVE-2022-3625){: external}, [CVE-2022-3628](https://nvd.nist.gov/vuln/detail/CVE-2022-3628){: external}, [CVE-2022-3707](https://nvd.nist.gov/vuln/detail/CVE-2022-3707){: external}, [CVE-2022-39188](https://nvd.nist.gov/vuln/detail/CVE-2022-39188){: external}, [CVE-2022-39189](https://nvd.nist.gov/vuln/detail/CVE-2022-39189){: external}, [CVE-2022-39253](https://nvd.nist.gov/vuln/detail/CVE-2022-39253){: external}, [CVE-2022-39260](https://nvd.nist.gov/vuln/detail/CVE-2022-39260){: external}, [CVE-2022-41218](https://nvd.nist.gov/vuln/detail/CVE-2022-41218){: external}, [CVE-2022-4129](https://nvd.nist.gov/vuln/detail/CVE-2022-4129){: external}, [CVE-2022-41674](https://nvd.nist.gov/vuln/detail/CVE-2022-41674){: external}, [CVE-2022-41717](https://nvd.nist.gov/vuln/detail/CVE-2022-41717){: external}, [CVE-2022-41973](https://nvd.nist.gov/vuln/detail/CVE-2022-41973){: external}, [CVE-2022-4269](https://nvd.nist.gov/vuln/detail/CVE-2022-4269){: external}, [CVE-2022-42703](https://nvd.nist.gov/vuln/detail/CVE-2022-42703){: external}, [CVE-2022-42720](https://nvd.nist.gov/vuln/detail/CVE-2022-42720){: external}, [CVE-2022-42721](https://nvd.nist.gov/vuln/detail/CVE-2022-42721){: external}, [CVE-2022-42722](https://nvd.nist.gov/vuln/detail/CVE-2022-42722){: external}, [CVE-2022-43552](https://nvd.nist.gov/vuln/detail/CVE-2022-43552){: external}, [CVE-2022-43750](https://nvd.nist.gov/vuln/detail/CVE-2022-43750){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}, [CVE-2022-47929](https://nvd.nist.gov/vuln/detail/CVE-2022-47929){: external}, [CVE-2023-0394](https://nvd.nist.gov/vuln/detail/CVE-2023-0394){: external}, [CVE-2023-0461](https://nvd.nist.gov/vuln/detail/CVE-2023-0461){: external}, [CVE-2023-0778](https://nvd.nist.gov/vuln/detail/CVE-2023-0778){: external}, [CVE-2023-1195](https://nvd.nist.gov/vuln/detail/CVE-2023-1195){: external}, [CVE-2023-1582](https://nvd.nist.gov/vuln/detail/CVE-2023-1582){: external}, [CVE-2023-23454](https://nvd.nist.gov/vuln/detail/CVE-2023-23454){: external}, [CVE-2023-27535](https://nvd.nist.gov/vuln/detail/CVE-2023-27535){: external}. |
| Haproxy | N/A |N/A|N/A|
{: caption="Changes since version 4.10.59_1566_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.59_1566_openshift, released 10 May 2023
{: #41059_1566_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.10.59_1566_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.10.57 | 4.10.59 | See [change logs](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-59){: external}. |
| Haproxy |N/A|N/A|N/A|
{: caption="Changes since version 4.10.57_1565_openshift" caption-side="bottom"}


### Master fix pack 4.10.56_1565_openshift, released 27 April 2023
{: #41056_1565_openshift}

The following table shows the changes that are in the master fix pack 4.10.56_1565_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.17 | v1.3.19 | Updated `Go` to version `1.19.8` and updated dependencies. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1366-amd64 | 1390-amd64 | Eliminate IP syscall. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.0 | v2.4.5 | Updated universal base image (UBI) to resolve CVEs. Updated `Go` to version `1.19.8` and updated dependencies. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.17-5 | v1.23.17-10 | Updated Go dependencies. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 429 | 431 | Updated `Go` to version `1.19.8` and updated dependencies. Update UBI base image. |
| Key Management Service provider | v2.6.4 | v2.6.5 | Updated `Go` to version `1.19.7` and updated dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2420 | 2486 | Updated `Go` to version `1.19.7` and updated dependencies. |
| {{site.data.keyword.openshiftshort}}. | 4.10.53 | 4.10.56 | See the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-56){: external}. Updated to resolve [CVE-2022-3172](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-3172){: external}. For more information, see the [Security bulletin](https://www.ibm.com/support/pages/node/6997115){: external}. |
| OpenVPN Operator image | v1.4.22 | v1.4.23 | Updated base image to resolve CVEs: [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}, [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2023-0361](https://nvd.nist.gov/vuln/detail/CVE-2023-0361){: external}. |
| Portieris admission controller | v0.13.3 | v0.13.4 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.4){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator and Metrics Server | 4.10.0-20230314 | 4.10.0-20230417 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20230417){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.10.0+20230314 | 4.10.0+20230417 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20230417){: external}. |
{: caption="Changes since version 4.10.53_1561_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.57_1565_openshift, released 24 April 2023
{: #41057_1565_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.57_1565_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.10.55 | 4.10.57 | See [change logs](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-57){: external}. |
| Haproxy |N/A|N/A|N/A|
{: caption="Changes since version 4.10.55_1563_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.55_1563_openshift, released 11 April 2023
{: #41055_1563_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.55_1563_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages | 4.18.0-425.13.1 | 4.18.0-425.19.2 | Worker node kernel & package updates for [CVE-2022-4269](https://nvd.nist.gov/vuln/detail/CVE-2022-4269){: external}, [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4378](https://nvd.nist.gov/vuln/detail/CVE-2022-4378){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}, [CVE-2023-0266](https://nvd.nist.gov/vuln/detail/CVE-2023-0266){: external}, [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2023-0361](https://nvd.nist.gov/vuln/detail/CVE-2023-0361){: external}, [CVE-2023-0386](https://nvd.nist.gov/vuln/detail/CVE-2023-0386){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.54 | 4.10.55 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-55){: external}. |
| Haproxy | 8398d1 | 8895ad | [CVE-2023-0361](https://nvd.nist.gov/vuln/detail/CVE-2023-0361){: external}. |
{: caption="Changes since version 4.10.54_1562_openshift" caption-side="bottom"}


### Master fix pack 4.10.53_1561_openshift, released 28 March 2023
{: #41053_1561_openshift}

The following table shows the changes that are in the master fix pack 4.10.53_1561_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.16 | v1.3.17 | Updated `Go` to version `1.19.7` and updated dependencies. |
| etcd | v3.4.23 | v3.4.24 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.24){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1308-amd64 | 1366-amd64 | Updated to resolve [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.7 | v2.4.0 | Removed ExpandInUsePersistentVolumes feature gate. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.16-11 | v1.23.17-5 | Updated to support the `Kubernetes 1.23.17` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 427 | 429 | Updated universal base image (UBI) to resolve CVEs. Updated `Go` to version `1.19.6` and updated dependencies. |
| Key Management Service provider | v2.6.3 | v2.6.4 | Updated `Go` to version `1.19.7` and updated dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2383 | 2420 | Updated the image to resolve CVEs. |
| OpenVPN Operator image | v1.4.20 | v1.4.22 | Updated `ansible-operator` to `v1.28.0` to fix CVEs. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.10.52 | 4.10.53 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-53){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.10.0-20230220 | v4.10.0-20230314 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20230314){: external}. |
{: caption="Changes since version 4.10.52_1558_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.54_1562_openshift, released 27 March 2023
{: #41054_1562_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.54_1562_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.10.53 | 4.10.54 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-54){: external}. |
| Haproxy | af5031 | 8398d1 | [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}. |
| CRI-O configuration | N/A | N/A | CRI-O configuration now sets container network `sysctl` tuning for `net.ipv4.tcp_keepalive_intvl` to `15`, `net.ipv4.tcp_keepalive_probes` to `6` and `net.ipv4.tcp_keepalive_time` to `40`. |
{: caption="Changes since version 4.10.53_1559_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.53_1559_openshift, released 13 March 2023
{: #41052_1559_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.53_1559_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages |N/A|N/A| Worker node package updates for [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.52 | 4.10.53 |  See the [change logs](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-53){: external} |
{: caption="Changes since version 4.10.52_1556_openshift" caption-side="bottom"}


### Master fix pack 4.10.52_1558_openshift, released 2 March 2023
{: #41052_1558_openshift}

The following table shows the changes that are in the master fix pack 4.10.52_1558_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.15 | v1.3.16 | Updated `Go` dependencies and to `Go` version `1.19.6`. Updated universal base image (UBI) to resolve CVEs. |
| etcd | v3.4.22 | v3.4.23 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.23){: external}. |
| Gateway-enabled cluster controller | 1902 | 1987 | Updated `armada-utils` to version `v1.9.35` |
| {{site.data.keyword.IBM_notm}} Calico extension | 1305-amd64 | 1308-amd64 | Updated universal base image (UBI) to resolve [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.6 | v2.3.7 | Updated universal base image (UBI) to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.16-3 | v1.23.16-11 | Updated `Go dependencies`. Updated `k8s.io/utils` digest to `a5ecb01`. Updated `vpcctl binary` to `3785`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 425 | 427 | Updated universal base image (UBI) to resolve CVEs. |
| Key Management Service provider | v2.5.13 | v2.6.3 | Updated `Go` dependencies and to `Go` version `1.19.6`. |
| Load balancer and Load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2325 | 2383 | Updated to `armada-utils` version `1.9.35`. |
| OpenVPN client | 2.5.6-r1-IKS-648 | 2.5.8-r0-IKS-674-amd64 | Remediate [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}. |
| OpenVPN server | 2.5.6-r1-IKS-647 | 2.5.8-r0-IKS-673-amd64 | Remediate [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}. |
| OpenVPN Operator image | v1.4.13 | v1.4.20 | Update `ansible-operator` to `v1.26.1` to fix CVEs. |
| Portieris admission controller | v0.12.6 | v0.13.3 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.3){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.47 | 4.10.52 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-52){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.10.0-20230123 | v4.10.0-20230220 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0%2B20230220){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.10.0-20230123 | v4.10.0-20230220 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0%2B20230220){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.10.0+20230123 | 4.10.0+20230220 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20230220){: external}. |
{: caption="Changes since version 4.10.47_1553_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.52_1556_openshift, released 27 February 2023
{: #41052_1556_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.52_1556_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages | 4.18.0-425.10.1 | 4.18.0-425.13.1 | Worker node & kernel package updates for [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2022-2873](https://nvd.nist.gov/vuln/detail/CVE-2022-2873){: external}, [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/CVE-2022-40897){: external}, [CVE-2022-41222](https://nvd.nist.gov/vuln/detail/CVE-2022-41222){: external}, [CVE-2022-43945](https://nvd.nist.gov/vuln/detail/CVE-2022-43945){: external}, [CVE-2022-4415](https://nvd.nist.gov/vuln/detail/CVE-2022-4415){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}, [CVE-2022-48303](https://nvd.nist.gov/vuln/detail/CVE-2022-48303){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.51 | 4.10.52 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-52){: external}. |
| HAProxy | d38f89 | af5031 | [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/CVE-2022-40897){: external}, [CVE-2022-4415](https://nvd.nist.gov/vuln/detail/CVE-2022-4415){: external}, [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}. |
{: caption="Changes since version 4.10.51_1555_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.51_1555_openshift, released 13 February 2023
{: #41051_1555_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.51_1555_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages |N/A|N/A| Worker node package updates for [CVE-2022-23521](https://nvd.nist.gov/vuln/detail/CVE-2022-23521){: external}, [CVE-2022-41903](https://nvd.nist.gov/vuln/detail/CVE-2022-41903){: external}, [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.50 | 4.10.51 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-51){: external}. |
| HAProxy | 8d6ea6 | 08c969 | [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}. |
{: caption="Changes since version 4.10.50_1554_openshift" caption-side="bottom"}


### Master fix pack 4.10.47_1553_openshift, released 30 January 2023
{: #41047_1553_openshift}

The following table shows the changes that are in the master fix pack 4.10.47_1553_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Tigera Operator | v1.27.16 | v1.27.17 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.27.17){: external}. |
| Cluster health image | v1.3.14 | v1.3.15 | Updated `Go` dependencies and to `Go` version `1.19.4`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1257 | 1280 | Publish s390x image. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.4 | v2.3.6 | Updated `UBI images` to `8.7-1031` |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.14-2 | v1.23.16-3 | Updated to support the `Kubernetes 1.23.16` release. Updated `Go` dependencies and to `Go` version `1.19.5`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 421 | 425 | Fixes for Fixing [CVE-2022-40303](https://nvd.nist.gov/vuln/detail/CVE-2022-40303){: external} and [CVE-2022-40304](https://nvd.nist.gov/vuln/detail/CVE-2022-40303){: external}. |
| Key Management Service provider | v2.5.12 | v2.5.13 | Updated `Go` dependencies and to `Go` version `1.19.4`. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.10.0-20221205 | v4.10.0-20230123 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20230123){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.10.43 | 4.10.47 | See the [{{site.data.keyword.openshiftlong_notm}} Release Notes](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-47){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.10.0-20221205 | v4.10.0-20230123 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20230123){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.10.0+20221205 | 4.10.0+20230123 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20230123){: external}. |
{: caption="Changes since version 4.10.43_1548_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.50_1554_openshift, released 30 January 2023
{: #41050_1554_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.50_1554_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.81 | 3.10.0-1160.83 | Worker node kernel & package updates for [CVE-2017-5715](https://nvd.nist.gov/vuln/detail/CVE-2017-5715){: external}, [CVE-2021-25220](https://nvd.nist.gov/vuln/detail/CVE-2021-25220){: external}, [CVE-2021-26401](https://nvd.nist.gov/vuln/detail/CVE-2021-26401){: external}, [CVE-2022-2795](https://nvd.nist.gov/vuln/detail/CVE-2022-2795){: external}, [CVE-2022-2964](https://nvd.nist.gov/vuln/detail/CVE-2022-2964){: external}, [CVE-2023-22809](https://nvd.nist.gov/vuln/detail/CVE-2023-22809){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node kernel & package updates for [CVE-2022-40303](https://nvd.nist.gov/vuln/detail/CVE-2022-40303){: external}, [CVE-2022-40304](https://nvd.nist.gov/vuln/detail/CVE-2022-40304){: external}, [CVE-2023-22809](https://nvd.nist.gov/vuln/detail/CVE-2023-22809){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.47 | 4.10.50 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-50){: external}. |
| HAProxy | 508bf6 | 8d6ea6 | [CVE-2022-42010](https://nvd.nist.gov/vuln/detail/CVE-2022-42010){: external}, [CVE-2022-42011](https://nvd.nist.gov/vuln/detail/CVE-2022-42011){: external}, [CVE-2022-42012](https://nvd.nist.gov/vuln/detail/CVE-2022-42012){: external}, [CVE-2022-40303](https://nvd.nist.gov/vuln/detail/CVE-2022-40303){: external}, [CVE-2022-40304](https://nvd.nist.gov/vuln/detail/CVE-2022-40304){: external}, [CVE-2022-3821](https://nvd.nist.gov/vuln/detail/CVE-2022-3821){: external}, [CVE-2022-35737](https://nvd.nist.gov/vuln/detail/CVE-2022-35737){: external}, [CVE-2022-43680](https://nvd.nist.gov/vuln/detail/CVE-2022-43680){: external}, [CVE-2021-46848](https://nvd.nist.gov/vuln/detail/CVE-2021-46848){: external}. |
{: caption="Changes since version 4.10.47_1551_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.47_1551_openshift, released 16 January 2023
{: #41047_1551_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.47_1551_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-425.3.1 | 4.18.0-425.10.1 | Worker node kernel & package updates for [CVE-2021-46848](https://nvd.nist.gov/vuln/detail/CVE-2021-46848){: external}, [CVE-2022-2601](https://nvd.nist.gov/vuln/detail/CVE-2022-2601){: external}, [CVE-2022-2964](https://nvd.nist.gov/vuln/detail/CVE-2022-2964){: external}, [CVE-2022-35737](https://nvd.nist.gov/vuln/detail/CVE-2022-35737){: external}, [CVE-2022-3775](https://nvd.nist.gov/vuln/detail/CVE-2022-3775){: external}, [CVE-2022-3821](https://nvd.nist.gov/vuln/detail/CVE-2022-3821){: external}, [CVE-2022-4139](https://nvd.nist.gov/vuln/detail/CVE-2022-4139){: external}, [CVE-2022-42010](https://nvd.nist.gov/vuln/detail/CVE-2022-42010){: external}, [CVE-2022-42011](https://nvd.nist.gov/vuln/detail/CVE-2022-42011){: external}, [CVE-2022-42012](https://nvd.nist.gov/vuln/detail/CVE-2022-42012){: external}, [CVE-2022-43680](https://nvd.nist.gov/vuln/detail/CVE-2022-43680){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.45 | 4.10.47 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-47){: external}. |
{: caption="Changes since version 4.10.45_1550_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.45_1550_openshift, released 02 January 2023
{: #41045_1550_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.45_1550_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}} |N/A|N/A|N/A|
{: caption="Changes since version 4.10.45_1549_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.45_1549_openshift, released 19 December 2022
{: #41045_1549_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.45_1549_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.80 | 3.10.0-1160.81 | Worker node kernel & package updates for [CVE-2022-28733](https://nvd.nist.gov/vuln/detail/CVE-2022-28733){: external}. |
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.10.43 | 4.10.45 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-45){: external}. |
{: caption="Changes since version 4.10.43_1547_openshift" caption-side="bottom"}


### Master fix pack 4.10.43_1548_openshift, released 14 December 2022
{: #41043_1548_openshift}

The following table shows the changes that are in the master fix pack 4.10.43_1548_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.13 | v1.3.14 | Updated `Go` dependencies. Exclude ingress status from cluster status aggregation. |
| etcd | v3.4.21 | v3.4.22 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.22){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1213 | 1257 | Updated universal base image (UBI) to resolve: [CVE-2022-1304](https://nvd.nist.gov/vuln/detail/cve-2022-1304){: external}, [CVE-2016-3709](https://nvd.nist.gov/vuln/detail/CVE-2016-3709){: external}, [CVE-2022-42898](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-42898){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.3 | v2.3.4 | Update `Go` to version `1.18.8` and updated universal base image (UBI) to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.13-5 | v1.23.14-2 | Updated to support the `Kubernetes 1.23.14` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 420 | 421 | Updated universal base image (UBI) to resolve [CVE-2022-42898](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-42898){: external}. Updated `Go` to version `1.18.8` |
| Key Management Service provider | v2.5.11 | v2.5.12 | Updated `Go` dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2110 | 2325 | Update `Go` to version `1.19.1` and update dependencies. |
| OpenVPN Operator image | v1.4.11 | v1.4.13 | Updated the `ansible operator base image` to `v1.25.2` to resolve CVEs. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.10.0-20221104 | v4.10.0-20221205 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20221205){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.10.39 | 4.10.43 | See the [{{site.data.keyword.openshiftlong_notm}} Release Notes](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-43){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server and toolkit | v4.10.0-20221104 | v4.10.0-20221205 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20221205){: external}. |
{: caption="Changes since version 4.10.39_1545_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.43_1547_openshift, released 05 December 2022
{: #41043_1547_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.43_1547_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-42898](https://nvd.nist.gov/vuln/detail/CVE-2022-42898){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node package updates for [CVE-2022-42898](https://nvd.nist.gov/vuln/detail/CVE-2022-42898){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.41 | 4.10.43 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-43){: external}. |
| HAProxy | c619f4 | 508bf6 | [CVE-2016-3709](https://nvd.nist.gov/vuln/detail/CVE-2016-3709){: external}, [CVE-2022-42898](https://nvd.nist.gov/vuln/detail/CVE-2022-42898){: external}, [CVE-2022-1304](https://nvd.nist.gov/vuln/detail/CVE-2022-1304){: external}. |
{: caption="Changes since version 4.10.41_1546_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.41_1546_openshift, released 21 November 2022
{: #41041_1546_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.41_1546_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-21233](https://nvd.nist.gov/vuln/detail/CVE-2022-21233){: external}, [CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external}, [CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external}, [CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external}, [CVE-2022-26373](https://nvd.nist.gov/vuln/detail/CVE-2022-26373){: external}, [CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external}, [CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external}, [CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node package updates for [CVE-2015-20107](https://nvd.nist.gov/vuln/detail/CVE-2015-20107){: external}, [CVE-2016-3709](https://nvd.nist.gov/vuln/detail/CVE-2016-3709){: external}, [CVE-2020-0256](https://nvd.nist.gov/vuln/detail/CVE-2020-0256){: external}, [CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external}, [CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external}, [CVE-2020-36516](https://nvd.nist.gov/vuln/detail/CVE-2020-36516){: external}, [CVE-2020-36558](https://nvd.nist.gov/vuln/detail/CVE-2020-36558){: external}, [CVE-2021-0308](https://nvd.nist.gov/vuln/detail/CVE-2021-0308){: external}, [CVE-2021-25220](https://nvd.nist.gov/vuln/detail/CVE-2021-25220){: external}, [CVE-2021-30002](https://nvd.nist.gov/vuln/detail/CVE-2021-30002){: external}, [CVE-2021-36221](https://nvd.nist.gov/vuln/detail/CVE-2021-36221){: external}, [CVE-2021-3640](https://nvd.nist.gov/vuln/detail/CVE-2021-3640){: external}, [CVE-2021-41190](https://nvd.nist.gov/vuln/detail/CVE-2021-41190){: external}, [CVE-2022-0168](https://nvd.nist.gov/vuln/detail/CVE-2022-0168){: external}, [CVE-2022-0494](https://nvd.nist.gov/vuln/detail/CVE-2022-0494){: external}, [CVE-2022-0617](https://nvd.nist.gov/vuln/detail/CVE-2022-0617){: external}, [CVE-2022-0854](https://nvd.nist.gov/vuln/detail/CVE-2022-0854){: external}, [CVE-2022-1016](https://nvd.nist.gov/vuln/detail/CVE-2022-1016){: external}, [CVE-2022-1048](https://nvd.nist.gov/vuln/detail/CVE-2022-1048){: external}, [CVE-2022-1055](https://nvd.nist.gov/vuln/detail/CVE-2022-1055){: external}, [CVE-2022-1184](https://nvd.nist.gov/vuln/detail/CVE-2022-1184){: external}, [CVE-2022-1304](https://nvd.nist.gov/vuln/detail/CVE-2022-1304){: external}, [CVE-2022-1353](https://nvd.nist.gov/vuln/detail/CVE-2022-1353){: external}, [CVE-2022-1708](https://nvd.nist.gov/vuln/detail/CVE-2022-1708){: external}, [CVE-2022-1852](https://nvd.nist.gov/vuln/detail/CVE-2022-1852){: external}, [CVE-2022-20368](https://nvd.nist.gov/vuln/detail/CVE-2022-20368){: external}, [CVE-2022-2078](https://nvd.nist.gov/vuln/detail/CVE-2022-2078){: external}, [CVE-2022-21499](https://nvd.nist.gov/vuln/detail/CVE-2022-21499){: external}, [CVE-2022-22624](https://nvd.nist.gov/vuln/detail/CVE-2022-22624){: external}, [CVE-2022-22628](https://nvd.nist.gov/vuln/detail/CVE-2022-22628){: external}, [CVE-2022-22629](https://nvd.nist.gov/vuln/detail/CVE-2022-22629){: external}, [CVE-2022-22662](https://nvd.nist.gov/vuln/detail/CVE-2022-22662){: external}, [CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external}, [CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external}, [CVE-2022-23960](https://nvd.nist.gov/vuln/detail/CVE-2022-23960){: external}, [CVE-2022-24448](https://nvd.nist.gov/vuln/detail/CVE-2022-24448){: external}, [CVE-2022-24795](https://nvd.nist.gov/vuln/detail/CVE-2022-24795){: external}, [CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external}, [CVE-2022-2586](https://nvd.nist.gov/vuln/detail/CVE-2022-2586){: external}, [CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external}, [CVE-2022-26373](https://nvd.nist.gov/vuln/detail/CVE-2022-26373){: external}, [CVE-2022-2639](https://nvd.nist.gov/vuln/detail/CVE-2022-2639){: external}, [CVE-2022-26700](https://nvd.nist.gov/vuln/detail/CVE-2022-26700){: external}, [CVE-2022-26709](https://nvd.nist.gov/vuln/detail/CVE-2022-26709){: external}, [CVE-2022-26710](https://nvd.nist.gov/vuln/detail/CVE-2022-26710){: external}, [CVE-2022-26716](https://nvd.nist.gov/vuln/detail/CVE-2022-26716){: external}, [CVE-2022-26717](https://nvd.nist.gov/vuln/detail/CVE-2022-26717){: external}, [CVE-2022-26719](https://nvd.nist.gov/vuln/detail/CVE-2022-26719){: external}, [CVE-2022-27191](https://nvd.nist.gov/vuln/detail/CVE-2022-27191){: external}, [CVE-2022-27404](https://nvd.nist.gov/vuln/detail/CVE-2022-27404){: external}, [CVE-2022-27405](https://nvd.nist.gov/vuln/detail/CVE-2022-27405){: external}, [CVE-2022-27406](https://nvd.nist.gov/vuln/detail/CVE-2022-27406){: external}, [CVE-2022-27950](https://nvd.nist.gov/vuln/detail/CVE-2022-27950){: external}, [CVE-2022-28390](https://nvd.nist.gov/vuln/detail/CVE-2022-28390){: external}, [CVE-2022-28893](https://nvd.nist.gov/vuln/detail/CVE-2022-28893){: external}, [CVE-2022-29162](https://nvd.nist.gov/vuln/detail/CVE-2022-29162){: external}, [CVE-2022-2938](https://nvd.nist.gov/vuln/detail/CVE-2022-2938){: external}, [CVE-2022-29581](https://nvd.nist.gov/vuln/detail/CVE-2022-29581){: external}, [CVE-2022-2989](https://nvd.nist.gov/vuln/detail/CVE-2022-2989){: external}, [CVE-2022-2990](https://nvd.nist.gov/vuln/detail/CVE-2022-2990){: external}, [CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external}, [CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external}, [CVE-2022-30293](https://nvd.nist.gov/vuln/detail/CVE-2022-30293){: external}, [CVE-2022-32746](https://nvd.nist.gov/vuln/detail/CVE-2022-32746){: external}, [CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external}, [CVE-2022-36946](https://nvd.nist.gov/vuln/detail/CVE-2022-36946){: external}, [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}, [CVE-2022-3787](https://nvd.nist.gov/vuln/detail/CVE-2022-3787){: external}, [CVE-2022-40674](https://nvd.nist.gov/vuln/detail/CVE-2022-40674){: external}, [CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.39 | 4.10.41 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-41){: external}. |
{: caption="Changes since version 4.10.39_1543_openshift" caption-side="bottom"}


### Master fix pack 4.10.39_1545_openshift, released 16 November 2022
{: #41039_1545_openshift}

The following table shows the changes that are in the master fix pack 4.10.39_1545_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.22.4 | v3.23.5 | See the [Calico release notes](https://docs.tigera.io/archive/v3.23/release-notes/#v3235){: external}. |
| Tigera Operator | v1.25.11 | v1.27.16 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.27.16){: external}. |
| Cluster health image | v1.3.12 | v1.3.13 | Updated Go dependencies, `golangci-lint`, `gosec`, and to `Go` version 1.19.3. Updated base image version to 116. |
| etcd | v3.4.18 | v3.4.21 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.21){: external}. |
| Gateway-enabled cluster controller | 1823 | 1902 | `Go` module updates. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1096 | 1213 | Updated image to fix the following CVEs: [CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external}, [CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external}, [CVE-2022-3515](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-3515){: external}, [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}, [CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external}, [CVE-2022-32149](https://nvd.nist.gov/vuln/detail/CVE-2022-32149){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.1 | v2.3.3 | Updated universal base image (UBI) to version `8.7-923` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.13-1 | v1.23.13-5 | Key rotation and updated `Go` dependencies. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 416 | 420 | Updated universal base image (UBI) to version `8.7-923` to resolve CVEs. |
| Key Management Service provider | v2.5.10 | v2.5.11 | Updated `Go` dependencies and to `Go` version `1.19.3`. |
| OpenVPN Operator image | v1.4.10 | v1.4.11 | Updated `ansible operator base image` to `v1.24.0` to resolve CVEs. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.10.0-20220920 | v4.10.0-20221104 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20221104){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.10.36 | 4.10.39 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-39){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server and toolkit | v4.10.0-20220920 | v4.10.0-20221104 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20221104){: external}. |
{: caption="Changes since version 4.10.36_1541_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.39_1544_openshift, released 11 November 2022
{: #41039_1544_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.39_1544_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-372.32.1.el8_6 | 4.18.0-425.3.1.el8 | Worker node kernel & package updates for [CVE-2021-36221](https://nvd.nist.gov/vuln/detail/CVE-2021-36221){: external}, [CVE-2022-1708](https://nvd.nist.gov/vuln/detail/CVE-2022-1708){: external}, [CVE-2022-27191](https://nvd.nist.gov/vuln/detail/CVE-2022-27191){: external}, [CVE-2021-41190](https://nvd.nist.gov/vuln/detail/CVE-2021-41190){: external}, [CVE-2022-2990](https://nvd.nist.gov/vuln/detail/CVE-2022-2990){: external}, [CVE-2022-29162](https://nvd.nist.gov/vuln/detail/CVE-2022-29162){: external}, [CVE-2022-2989](https://nvd.nist.gov/vuln/detail/CVE-2022-2989){: external}, [CVE-2022-2990](https://nvd.nist.gov/vuln/detail/CVE-2022-2990){: external}, [CVE-2020-36516](https://nvd.nist.gov/vuln/detail/CVE-2020-36516){: external}, [CVE-2020-36558](https://nvd.nist.gov/vuln/detail/CVE-2020-36558){: external}, [CVE-2021-3640](https://nvd.nist.gov/vuln/detail/CVE-2021-3640){: external}, [CVE-2021-30002](https://nvd.nist.gov/vuln/detail/CVE-2021-30002){: external}, [CVE-2022-0168](https://nvd.nist.gov/vuln/detail/CVE-2022-0168){: external}, [CVE-2022-0617](https://nvd.nist.gov/vuln/detail/CVE-2022-0617){: external}, [CVE-2022-0854](https://nvd.nist.gov/vuln/detail/CVE-2022-0854){: external}, [CVE-2022-1016](https://nvd.nist.gov/vuln/detail/CVE-2022-1016){: external}, [CVE-2022-1048](https://nvd.nist.gov/vuln/detail/CVE-2022-1048){: external}, [CVE-2022-1055](https://nvd.nist.gov/vuln/detail/CVE-2022-1055){: external}, [CVE-2022-1184](https://nvd.nist.gov/vuln/detail/CVE-2022-1184){: external}, [CVE-2022-1852](https://nvd.nist.gov/vuln/detail/CVE-2022-1852){: external}, [CVE-2022-2078](https://nvd.nist.gov/vuln/detail/CVE-2022-2078){: external}, [CVE-2022-2586](https://nvd.nist.gov/vuln/detail/CVE-2022-2586){: external}, [CVE-2022-2639](https://nvd.nist.gov/vuln/detail/CVE-2022-2639){: external}, [CVE-2022-2938](https://nvd.nist.gov/vuln/detail/CVE-2022-2938){: external}, [CVE-2022-20368](https://nvd.nist.gov/vuln/detail/CVE-2022-20368){: external}, [CVE-2022-21499](https://nvd.nist.gov/vuln/detail/CVE-2022-21499){: external}, [CVE-2022-23960](https://nvd.nist.gov/vuln/detail/CVE-2022-23960){: external}, [CVE-2022-26373](https://nvd.nist.gov/vuln/detail/CVE-2022-26373){: external}, [CVE-2022-27950](https://nvd.nist.gov/vuln/detail/CVE-2022-27950){: external}, [CVE-2022-28390](https://nvd.nist.gov/vuln/detail/CVE-2022-28390){: external}, [CVE-2022-28893](https://nvd.nist.gov/vuln/detail/CVE-2022-28893){: external}, [CVE-2022-29581](https://nvd.nist.gov/vuln/detail/CVE-2022-29581){: external}, [CVE-2022-36946](https://nvd.nist.gov/vuln/detail/CVE-2022-36946){: external}, [CVE-2022-24448](https://nvd.nist.gov/vuln/detail/CVE-2022-24448){: external}. |
{: caption="Changes since version 4.10.39_1543_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.39_1543_openshift, released 07 November 2022
{: #41039_1543_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.39_1543_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.76.1 | 3.10.0-1160.80.1 | Worker node kernel & package updates for [CVE-2022-21233](https://nvd.nist.gov/vuln/detail/CVE-2022-21233){: external}, [CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external}, [CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external}, [CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external}, [CVE-2022-26373](https://nvd.nist.gov/vuln/detail/CVE-2022-26373){: external}, [CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external}, [CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external}, [CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| RHEL 8 Packages | 4.18.0-372.26.1 | 4.18.0-372.32.1 | Worker node kernel & package updates for [CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external}, [CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external}, [CVE-2022-0494](https://nvd.nist.gov/vuln/detail/CVE-2022-0494){: external}, [CVE-2022-1353](https://nvd.nist.gov/vuln/detail/CVE-2022-1353){: external}, [CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external}, [CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external}, [CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external}, [CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external}, [CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external}, [CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external}, [CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external}, [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}, [CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.37 | 4.10.39 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-39){: external}. |
| HAProxy | b034b2 | 3a1392 | [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}, [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}, [CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external}, [CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external}, [CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external}, [CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external}. |
{: caption="Changes since version 4.10.37_1539_openshift" caption-side="bottom"}


### Master fix pack 4.10.36_1541_openshift, released 27 October 2022
{: #41036_1541_openshift}

The following table shows the changes that are in the master fix pack 4.10.36_1541_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.11 | v1.3.12 | Updated `Go` dependencies, golangci-lint, and to `Go` version 1.19.2. Updated base image version to 109. Excluded ingress status from cluster status calculation. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.11-1 | v1.23.13-1 | Updated to support the `Kubernetes 1.23.13` release. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | dc1725a | 778ef2b | Updated to `Go` version `1.18.6`. |
| Key Management Service provider | v2.5.9 | v2.5.10 | Updated `Go` dependencies and to `Go` version `1.19.2`. |
| OpenVPN Operator image | v1.4.9 | v1.4.10 | Updated ansible operator base image to v1.24.0 to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.10.32 | 4.10.36 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-36){: external}. |
{: caption="Changes since version 4.10.321536openshift" caption-side="bottom"}


### Worker node fix pack 4.10.37_1542_openshift, released 27 October 2022
{: #41037_1542_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.37_1542_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| VPC Gen 2 RHEL 8 worker image disk size | N/A | N/A | Fixed regression on previous version where root file system partition was 25 GB instead of 100GB for VPC Gen 2 |
{: caption="Changes since version 4.10.37_1539_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.37_1539_openshift, released 25 October 2022
{: #41037_1539_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.37_1539_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}} | 4.10.35 | 4.10.37 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-37){: external}. |
{: caption="Changes since version 4.10.35_1538_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.35_1538_openshift, released 10 October 2022
{: #41035_1538_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.35_1538_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.10.33 | 4.10.35 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-35){: external}. |
{: caption="Changes since version 4.10.33_1537_openshift" caption-side="bottom"}


### Master fix pack 4.10.32_1536_openshift, released 26 September 2022
{: #41032_1536_openshift}

The following table shows the changes that are in the master fix pack 4.10.32_1536_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.10 | v1.3.11 | Updated `Go` dependencies and to `Go` version `1.18.6`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1006 | 1096 | Updated image for [CVE-2022-2526](https://nvd.nist.gov/vuln/detail/CVE-2022-2526){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.9 | v2.3.1 | Updated to `Go` version `1.18.6`. Updated universal base image (UBI) to version `8.6-941` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.9-3 | v1.23.11-1 | Updated `Go` dependencies and to use `Go` version `1.17.13`. Updated to support the Kubernetes `1.23.11` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 414 | 416 | Updated to `Go` version `1.18.6`. Updated universal base image (UBI) to version `8.6-941` to resolve CVEs. |
| Key Management Service Provider | v2.5.8 | v2.5.9 | Updated `Go` dependencies and to `Go` version `1.18.6`. |
| {{site.data.keyword.openshiftshort}} | 4.10.26 | 4.10.32 | See the [{{site.data.keyword.openshiftshort}} Release Notes](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-32){: external}. |
| OpenVPN Operator image | v1.4.8 | v1.4.9 | Updated ansible operator base image to `v1.23.0` to resolve CVEs. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.10.0-20220822 | v4.10.0-20220920 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220920){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.10.0-20220822 | v4.10.0-20220920 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220920){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.10.0+20220822 | 4.10.0+20220920 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220920){: external}. |
{: caption="Changes since version 4.10.261534openshift" caption-side="bottom"}


### Worker node fix pack 4.10.33_1537_openshift, released 26 September 2022
{: #41033_1537_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.33_1537_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-372.19.1 | 4.18.0-372.26.1 |N/A|
| {{site.data.keyword.openshiftshort}}. | 4.10.31 | 4.10.33 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-33){: external}. |
{: caption="Changes since version 4.10.31_1535_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.31_1535_openshift, released 12 September 2022
{: #41031_1535_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.31_1535_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.10.28 | 4.10.31 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-31){: external}. |
{: caption="Changes since version 4.10.28_1533_openshift" caption-side="bottom"}


### Master fix pack 4.10.26_1534_openshift, released 1 September 2022
{: #41026_1534_openshift}

The following table shows the changes that are in the master fix pack 4.10.26_1534_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.22.2 | v3.22.4 | See the [Calico release notes](https://docs.tigera.io/archive/v3.22/release-notes/#v3224){: external}. Updated the Calico custom resource definitions to include `preserveUnknownFields: false`. |
| Tigera Operator | v1.25.7 | v1.25.11 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.25.11){: external}. |
| Cluster health image | v1.3.9 | v1.3.10 | Updated `Go` dependencies and to `Go` version `1.18.5`. |
| Gateway-enabled cluster controller | 1792 | 1823 | Updated to `Go` version `1.17.13`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 997 | 1006 | Updated to `Go` version `1.17.13`. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.8 | v2.2.9 | Updated to `Go` version `1.18.5`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.8-7 | v1.23.9-3 | Updated `vpcctl` binary to version `3367`. Updated to support the Kubernetes `1.23.10` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 412 | 414 | Updated to `Go` version `1.18.5`. Updated universal base image (UBI) to version `8.6-902` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 0a187a4 | dc1725a | Updated `Go` dependencies and to `Go` version `1.18.3`. |
| Key Management Service provider | v2.5.7 | v2.5.8 | Updated `Go` dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2058 | 2110 | Updated `Go` dependencies and to `Go` version `1.17.13`. |
| {{site.data.keyword.openshiftshort}}. | 4.10.22 | 4.10.26 | See the [{{site.data.keyword.openshiftshort}} Release Notes](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-26){: external}. |
| OpenVPN client | 2.5.6-r1-IKS-629 | 2.5.6-r1-IKS-648 | Update image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external} and [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}. |
| OpenVPN Operator image | v1.4.7 | v1.4.8 | Updated Ansible operator base image to version `v1.22.2` to resolve CVEs. |
| OpenVPN server | 2.5.6-r1-IKS-628 | 2.5.6-r1-IKS-647 | Update image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external} and [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}. |
| Portieris admission controller | v0.12.5 | v0.12.6 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.12.6){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.10.0-20220712 | v4.10.0-20220822 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0%2B20220822){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.10.0-20220712 | v4.10.0-20220822 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0%2B20220822){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.10.0+20220712 | 4.10.0+20220822 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220822){: external}. |
{: caption="Changes since version 4.10.22_1528_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.28_1533_openshift, released 29 August 2022
{: #41028_1533_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.28_1533_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-2526](https://nvd.nist.gov/vuln/detail/CVE-2022-2526){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.26 | 4.10.28 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-28){: external}. |
| HAProxy | 6514a2 | c1634f | [CVE-2022-32206](https://nvd.nist.gov/vuln/detail/CVE-2022-32206){: external}, [CVE-2022-32208](https://nvd.nist.gov/vuln/detail/CVE-2022-32208){: external}
{: caption="Changes since version 4.10.26_1530_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.26_1530_openshift, released 16 August 2022
{: #41026_1530_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.26_1530_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.71.1 | 3.10.0-1160.76.1 | Worker node package updates for [CVE-2022-0005](https://nvd.nist.gov/vuln/detail/CVE-2022-0005){: external}, [CVE-2022-21123](https://nvd.nist.gov/vuln/detail/CVE-2022-21123){: external}, [CVE-2022-21125](https://nvd.nist.gov/vuln/detail/CVE-2022-21125){: external}, [CVE-2022-21127](https://nvd.nist.gov/vuln/detail/CVE-2022-21127){: external}, [CVE-2022-21131](https://nvd.nist.gov/vuln/detail/CVE-2022-21131){: external}, [CVE-2022-21136](https://nvd.nist.gov/vuln/detail/CVE-2022-21136){: external}, [CVE-2022-21151](https://nvd.nist.gov/vuln/detail/CVE-2022-21151){: external}, [CVE-2022-21166](https://nvd.nist.gov/vuln/detail/CVE-2022-21166){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.24 | 4.10.26 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-26){: external}. |
{: caption="Changes since version 4.10.24_1529_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.24_1529_openshift, released 01 August 2022
{: #41024_1529_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.24_1529_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.10.21 | 4.10.24 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-24){: external}. |
{: caption="Changes since version 4.10.21_1527_openshift" caption-side="bottom"}


### Master fix pack 4.10.22_1528_openshift, released 26 July 2022
{: #41022_1528_openshift}

The following table shows the changes that are in the master fix pack 4.10.22_1528_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.8 | v1.3.9 | Updated `Go` dependencies and to use `Go` version `1.18.4`. Fixed minor typographical error in the add-on `daemonset not available` health status. |
| Gateway-enabled cluster controller | 1680 | 1792 | Updated to use `Go` version `1.17.11`. Updated image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external} and [CVE-2022-29458](https://nvd.nist.gov/vuln/detail/CVE-2022-29458){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 980 | 997 | Updated to use `Go` version `1.17.11`. Updated universal base image (UBI) to version `8.6-854` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.6 | v2.2.8 | Updated to use `Go` version `1.18.3`. Updated universal base image (UBI) to version `8.6-854` to resolve CVEs. Updated to support RHEL 8 worker nodes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.7-7 | v1.23.8-7 | Updated `Go` dependencies and to use `Go` version `1.17.11`. Updated to support the Kubernetes `1.23.8` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 410 | 412 | Updated to use `Go` version `1.18.3`. Updated universal base image (UBI) to version `8.6-854` to resolve CVEs. Improved Kubernetes resource watch configuration. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 8c96932 | 0a187a4 | Updated universal base image (UBI) to resolve CVEs. |
| Key Management Service provider | v2.5.6 | v2.5.7 | Updated `Go` dependencies and to use `Go` version `1.18.4`. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1998 | 2058 | Updated image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.17 | 4.10.22 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-22){: external}. |
| OpenVPN client | 2.5.6-r0-IKS-592 | 2.5.6-r1-IKS-629 | Updated Alpine base image to version `3.16` to resolve CVEs. Updated OpenVPN to version `2.5.6-r1`. |
| OpenVPN Operator image | v1.4.6 | v1.4.7 | Updated Ansible operator base image to version `v1.22.1` to resolve CVEs. |
| OpenVPN server | 2.5.6-r0-IKS-591 | 2.5.6-r1-IKS-628 | Updated Alpine base image to version `3.16` to resolve CVEs. Updated OpenVPN to version `2.5.6-r1`. |
| Portieris admission controller | v0.12.4 | v0.12.5 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.12.5){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.10.0-20220614 | v4.10.0-20220712 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220712){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Metrics Server | v4.10.0-20220614 | v4.10.0-20220712 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220712){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} toolkit | 4.10.0+20220614 | 4.10.0+20220712 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220712){: external}. |
{: caption="Changes since version 4.10.17_1524_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.21_1527_openshift, released 18 July 2022
{: #41021_1527_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.21_1527_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.66.1 | 3.10.0-1160.71.1 | Worker node package updates for [CVE-2020-26116](https://nvd.nist.gov/vuln/detail/CVE-2020-26116){: external}, [CVE-2020-26137](https://nvd.nist.gov/vuln/detail/CVE-2020-26137){: external}, [CVE-2021-3177](https://nvd.nist.gov/vuln/detail/CVE-2021-3177){: external}, [CVE-2022-0391](https://nvd.nist.gov/vuln/detail/CVE-2022-0391){: external}, [CVE-2022-1729](https://nvd.nist.gov/vuln/detail/CVE-2022-1729){: external}, [CVE-2022-1966](https://nvd.nist.gov/vuln/detail/CVE-2022-1966){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.20 | 4.10.21 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-21){: external}. |
{: caption="Changes since version 4.10.20_1526_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.20_1526_openshift, released 11 July 2022
{: #41020_1526_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.20_1526_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| General |N/A|N/A| Fix to address a bug that occurred if you used the persistent volume claim NFS v3 storage. |
{: caption="Changes since version 4.10.20_1525_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.20_1525_openshift, released 05 July 2022
{: #41020_1525_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.20_1525_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.10.18 | 4.10.20 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-20){: external}. |
{: caption="Changes since version 4.10.18_1523_openshift" caption-side="bottom"}


### Master fix pack 4.10.17_1524_openshift, released 22 June 2022
{: #41017_1524_openshift}

The following table shows the changes that are in the master fix pack 4.10.17_1524_openshift. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.7 | v1.3.8 | Updated `Go` to version `1.17.11` and also updated the dependencies. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.4 | v2.2.6 | Bug fixes for the driver installation. Block plug-in base images were updated to `ubi`: `8.6-751.1655117800` for CVE-2022-1271 |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.7-4 | v1.23.7-7 | Update module github.com/{{site.data.keyword.IBM_notm}}/vpc-go-sdk to `v0.20.0`. Update module github.com/stretchr/testify to `v1.7.2`. |
| Key Management Service provider | v2.5.5 | v2.5.6 | Updated `Go` to version `1.17.11` and also updated the dependencies. |
| OpenVPN Operator image | v1.4.5 | v1.4.6 | Update base image to version `v1.22.0` to resolve CVEs. |
| {{site.data.keyword.openshiftshort}}. | 4.10.15 | 4.10.17 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-17){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.10.0-20220509 | v4.10.0-20220614 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0%2B20220614){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Metrics Server and toolkit | v4.10.0-20220509 | v4.10.0-20220614 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0%2B20220614){: external}. |
{: caption="Changes since version 4.10.15_1520_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.18_1523_openshift, released 20 June 2022
{: #41018_1523_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.18_1523_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}. |
| HAProxy | 468c09 | 04f862 | [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.16 | 4.10.18 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-18){: external}. |
{: caption="Changes since version 4.10.16_1521_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.16_1521_openshift, released 7 June 2022
{: #41016_1521_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.16_1521_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-24903](https://nvd.nist.gov/vuln/detail/CVE-2022-24903){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.14 | 4.10.16 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-14){: external}. |
{: caption="Changes since version 4.10.14_1519_openshift" caption-side="bottom"}


### Master fix pack 4.10.15_1520_openshift, released 3 June 2022
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
| {{site.data.keyword.openshiftshort}}. | 4.10.12 | 4.10.15 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-15){: external}. |
{: caption="Changes since version 4.10.9_1515_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.14_1519_openshift, released 23 May 2022
{: #41014_1519_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.14_1519_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
|RHEL 7 Packages | 3.10.0-1160.62.1 | 3.10.0-1160.66.1 | Worker node kernel & package updates for [CVE-2018-25032](https://nvd.nist.gov/vuln/detail/CVE-2018-25032){: external}, [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}, [CVE-2022-0492](https://nvd.nist.gov/vuln/detail/CVE-2022-0492){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.12 | 4.10.14 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-14){: external}. |
| HA proxy | 36b0307 | 468c09 | [CVE-2021-3634](https://nvd.nist.gov/vuln/detail/CVE-2021-3634){: external}. |
{: caption="Changes since version 4.10.12_1517_openshift" caption-side="bottom"}


### Worker node fix pack 4.10.12_1517_openshift, released 09 May 2022
{: #41012_1517_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.12_1517_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | N/A |
| {{site.data.keyword.openshiftshort}}. | 4.10.10 | 4.10.12 | For more information, see the [change log](https://docs.redhat.com/documentation/openshift_container_platform/4.10/html/release_notes/ocp-4-10-release-notes#ocp-4-10-12){: external}. |
| HAProxy | f53b22 | 36b030 | [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}, [CVE-2022-1154](https://nvd.nist.gov/vuln/detail/CVE-2022-1154){: external}, [CVE-2018-25032](https://nvd.nist.gov/vuln/detail/CVE-2018-25032){: external}. |
{: caption="Changes since version 4.10.10_1516_openshift" caption-side="bottom"}
