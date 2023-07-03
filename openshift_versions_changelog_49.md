---

copyright:
  years: 2014, 2023
lastupdated: "2023-07-03"

keywords: openshift, update, upgrade, BOM, bill of materials, versions, patch, 4.9

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.redhat_openshift_notm}} version 4.9 change log
{: #openshift_changelog_49}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.9. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}


Version 4.9 becomes unsupported on 30 August 2023. Update your cluster to at least [version 4.10](/docs/openshift?topic=openshift-cs_versions_410&interface=ui) as soon as possible.
{: deprecated}

## Overview
{: #openshift_changelog_overview_49}

Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features, which are subject to change, are disabled.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security) for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't also refer to an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}

## Change logs
{: #49_changelog}


Review the version 4.9 change log.
{: shortdesc}


### Change log for worker node fix pack 4.9.59_1595_openshift, released 03 July 2023
{: #4959_1595_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.9.59_1595_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | N/A | N/A | N/A |
{: caption="Changes since version 4.9.59_1593_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.59_1594_openshift, released 27 June 2023
{: #4959_1594_openshift_M}

The following table shows the changes that are in the master fix pack 4.9.59_1594_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.20 | v1.3.21 | Updated `Go` dependencies and to `Go` version `1.19.10`. |
| etcd | v3.4.25 | v3.4.26 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.26){: external}. |
| Gateway-enabled cluster controller | 2106 | 2322 | Updated image to resolve [CVE-2023-2650](https://nvd.nist.gov/vuln/detail/CVE-2023-2650){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 431 | 433 | Updated `Go` to version `1.20.4`. Updated UBI base image. |
| Key Management Service provider | v2.6.6 | v2.6.7 | Updated `Go` dependencies and to `Go` version `1.19.10`. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2486 | 2584 | Updated `Go` dependencies and to `Go` version `1.19.9`. Updated base image. |
| OpenVPN client | 2.5.8-r0-IKS-674-amd64 | 2.6.4-r0-IKS-34-amd64 | Upgrade `openvpn` to version `2.6.4-r0`. |
| OpenVPN server | 2.5.8-r0-IKS-673-amd64 | 2.6.4-r0-IKS-33-amd64 | Upgrade `openvpn` to version `2.6.4-r0`. |
| OpenVPN Operator image | v1.4.23 | v1.4.25 | Updated OpenVPN configuration to provide shutdown grace period before terminating connections. |
{: caption="Changes since version 4.9.59_1591_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.59_1593_openshift, released 19 June 2023
{: #4959_1593_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.9.59_1593_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | N/A |N/A|N/A|
| RHEL 7 Packages |3.10.0-1160.90.1.el7|3.10.0-1160.92.1.el7|Worker node kernel & package updates for [CVE-2022-48339](https://nvd.nist.gov/vuln/detail/CVE-2022-48339){: external},[CVE-2023-24329](https://nvd.nist.gov/vuln/detail/CVE-2023-24329){: external}. |
| RHEL 8 Packages | N/A | N/A | Worker node package updates for [CVE-2023-32067](https://nvd.nist.gov/vuln/detail/CVE-2023-32067){: external},[CVE-2023-24329](https://nvd.nist.gov/vuln/detail/CVE-2023-24329){: external}. |
{: caption="Changes since version 4.9.59_1592_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.59_1592_openshift, released 5 June 2023
{: #4959_1592_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.9.59_1592_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | N/A |N/A|N/A|
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-477.10.1.el8_8 | 4.18.0-477.13.1.el8_8 | Worker node kernel & package updates for [CVE-2023-22490](https://nvd.nist.gov/vuln/detail/CVE-2023-22490){: external}, [CVE-2023-23946](https://nvd.nist.gov/vuln/detail/CVE-2023-23946){: external}, [CVE-2023-25652](https://nvd.nist.gov/vuln/detail/CVE-2023-25652){: external}, [CVE-2023-25815](https://nvd.nist.gov/vuln/detail/CVE-2023-25815){: external}, [CVE-2023-29007](https://nvd.nist.gov/vuln/detail/CVE-2023-29007){: external}, [CVE-2023-32233](https://nvd.nist.gov/vuln/detail/CVE-2023-32233){: external}. |
{: caption="Changes since version 4.9.59_1590_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.59_1591_openshift, released 25 May 2023
{: #4959_1591_openshift_M}

The following table shows the changes that are in the master fix pack 4.9.59_1591_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.19 | v1.3.20 | Updated `Go` to version `1.19.9` and updated dependencies. Updated the base image. Resolved add-on health bugs. |
| etcd | v3.4.24 | v3.4.25 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.25){: external}. |
| Gateway-enabled cluster controller | 2024 | 2106 | Updated to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.17-8 | v1.22.17-9 | Key rotation. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 778ef2b | 4e2f346 | Make armada-rbac-sync FIPS compliant |
| Key Management Service provider | v2.6.5 | v2.6.6 | Updated `Go` to version `1.19.9` and updated dependencies. |
| Portieris admission controller | v0.13.4 | v0.13.5 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.5){: external}. |
| OpenVPN client | 2.6.4-r0-IKS-27 | 2.5.8-r0-IKS-674 | Reverted to previous version. |
| OpenVPN server | 2.6.4-r0-IKS-26 | 2.5.8-r0-IKS-673 | Reverted to previous version. |
{: caption="Changes since version 4.9.59_1587_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.59_1590_openshift, released 23 May 2023
{: #4959_1590_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.9.59_1590_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | N/A |N/A|N/A|
| RHEL 7 Packages | 4.15.0-210-generic |4.15.0-211-generic|N/A
| RHEL 8 Packages | 4.18.0-425.19.2.el8_7 | 4.18.0-477.10.1.el8_8 | Worker node kernel & package updates for [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-26341](https://nvd.nist.gov/vuln/detail/CVE-2021-26341){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2021-33655](https://nvd.nist.gov/vuln/detail/CVE-2021-33655){: external}, [CVE-2021-33656](https://nvd.nist.gov/vuln/detail/CVE-2021-33656){: external}, [CVE-2022-1462](https://nvd.nist.gov/vuln/detail/CVE-2022-1462){: external}, [CVE-2022-1679](https://nvd.nist.gov/vuln/detail/CVE-2022-1679){: external}, [CVE-2022-1705](https://nvd.nist.gov/vuln/detail/CVE-2022-1705){: external}, [CVE-2022-1789](https://nvd.nist.gov/vuln/detail/CVE-2022-1789){: external}, [CVE-2022-1962](https://nvd.nist.gov/vuln/detail/CVE-2022-1962){: external}, [CVE-2022-20141](https://nvd.nist.gov/vuln/detail/CVE-2022-20141){: external}, [CVE-2022-2196](https://nvd.nist.gov/vuln/detail/CVE-2022-2196){: external}, [CVE-2022-24765](https://nvd.nist.gov/vuln/detail/CVE-2022-24765){: external}, [CVE-2022-25265](https://nvd.nist.gov/vuln/detail/CVE-2022-25265){: external}, [CVE-2022-2663](https://nvd.nist.gov/vuln/detail/CVE-2022-2663){: external}, [CVE-2022-27664](https://nvd.nist.gov/vuln/detail/CVE-2022-27664){: external}, [CVE-2022-2795](https://nvd.nist.gov/vuln/detail/CVE-2022-2795){: external}, [CVE-2022-28131](https://nvd.nist.gov/vuln/detail/CVE-2022-28131){: external}, [CVE-2022-29187](https://nvd.nist.gov/vuln/detail/CVE-2022-29187){: external}, [CVE-2022-2928](https://nvd.nist.gov/vuln/detail/CVE-2022-2928){: external}, [CVE-2022-2929](https://nvd.nist.gov/vuln/detail/CVE-2022-2929){: external}, [CVE-2022-3028](https://nvd.nist.gov/vuln/detail/CVE-2022-3028){: external}, [CVE-2022-30594](https://nvd.nist.gov/vuln/detail/CVE-2022-30594){: external}, [CVE-2022-30629](https://nvd.nist.gov/vuln/detail/CVE-2022-30629){: external}, [CVE-2022-30630](https://nvd.nist.gov/vuln/detail/CVE-2022-30630){: external}, [CVE-2022-30631](https://nvd.nist.gov/vuln/detail/CVE-2022-30631){: external}, [CVE-2022-30632](https://nvd.nist.gov/vuln/detail/CVE-2022-30632){: external}, [CVE-2022-30633](https://nvd.nist.gov/vuln/detail/CVE-2022-30633){: external}, [CVE-2022-30635](https://nvd.nist.gov/vuln/detail/CVE-2022-30635){: external}, [CVE-2022-32148](https://nvd.nist.gov/vuln/detail/CVE-2022-32148){: external}, [CVE-2022-32189](https://nvd.nist.gov/vuln/detail/CVE-2022-32189){: external}, [CVE-2022-3239](https://nvd.nist.gov/vuln/detail/CVE-2022-3239){: external}, [CVE-2022-3522](https://nvd.nist.gov/vuln/detail/CVE-2022-3522){: external}, [CVE-2022-3524](https://nvd.nist.gov/vuln/detail/CVE-2022-3524){: external}, [CVE-2022-35252](https://nvd.nist.gov/vuln/detail/CVE-2022-35252){: external}, [CVE-2022-3564](https://nvd.nist.gov/vuln/detail/CVE-2022-3564){: external}, [CVE-2022-3566](https://nvd.nist.gov/vuln/detail/CVE-2022-3566){: external}, [CVE-2022-3567](https://nvd.nist.gov/vuln/detail/CVE-2022-3567){: external}, [CVE-2022-3619](https://nvd.nist.gov/vuln/detail/CVE-2022-3619){: external}, [CVE-2022-36227](https://nvd.nist.gov/vuln/detail/CVE-2022-36227){: external}, [CVE-2022-3623](https://nvd.nist.gov/vuln/detail/CVE-2022-3623){: external}, [CVE-2022-3625](https://nvd.nist.gov/vuln/detail/CVE-2022-3625){: external}, [CVE-2022-3628](https://nvd.nist.gov/vuln/detail/CVE-2022-3628){: external}, [CVE-2022-3707](https://nvd.nist.gov/vuln/detail/CVE-2022-3707){: external}, [CVE-2022-39188](https://nvd.nist.gov/vuln/detail/CVE-2022-39188){: external}, [CVE-2022-39189](https://nvd.nist.gov/vuln/detail/CVE-2022-39189){: external}, [CVE-2022-39253](https://nvd.nist.gov/vuln/detail/CVE-2022-39253){: external}, [CVE-2022-39260](https://nvd.nist.gov/vuln/detail/CVE-2022-39260){: external}, [CVE-2022-41218](https://nvd.nist.gov/vuln/detail/CVE-2022-41218){: external}, [CVE-2022-4129](https://nvd.nist.gov/vuln/detail/CVE-2022-4129){: external}, [CVE-2022-41674](https://nvd.nist.gov/vuln/detail/CVE-2022-41674){: external}, [CVE-2022-41717](https://nvd.nist.gov/vuln/detail/CVE-2022-41717){: external}, [CVE-2022-41973](https://nvd.nist.gov/vuln/detail/CVE-2022-41973){: external}, [CVE-2022-4269](https://nvd.nist.gov/vuln/detail/CVE-2022-4269){: external}, [CVE-2022-42703](https://nvd.nist.gov/vuln/detail/CVE-2022-42703){: external}, [CVE-2022-42720](https://nvd.nist.gov/vuln/detail/CVE-2022-42720){: external}, [CVE-2022-42721](https://nvd.nist.gov/vuln/detail/CVE-2022-42721){: external}, [CVE-2022-42722](https://nvd.nist.gov/vuln/detail/CVE-2022-42722){: external}, [CVE-2022-43552](https://nvd.nist.gov/vuln/detail/CVE-2022-43552){: external}, [CVE-2022-43750](https://nvd.nist.gov/vuln/detail/CVE-2022-43750){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}, [CVE-2022-47929](https://nvd.nist.gov/vuln/detail/CVE-2022-47929){: external}, [CVE-2023-0394](https://nvd.nist.gov/vuln/detail/CVE-2023-0394){: external}, [CVE-2023-0461](https://nvd.nist.gov/vuln/detail/CVE-2023-0461){: external}, [CVE-2023-0778](https://nvd.nist.gov/vuln/detail/CVE-2023-0778){: external}, [CVE-2023-1195](https://nvd.nist.gov/vuln/detail/CVE-2023-1195){: external}, [CVE-2023-1582](https://nvd.nist.gov/vuln/detail/CVE-2023-1582){: external}, [CVE-2023-23454](https://nvd.nist.gov/vuln/detail/CVE-2023-23454){: external}, [CVE-2023-27535](https://nvd.nist.gov/vuln/detail/CVE-2023-27535){: external}. |
| Haproxy | N/A |N/A|N/A|
{: caption="Changes since version 4.9.59_1588_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.59_1588_openshift, released 10 May 2023
{: #4959_1588_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.9.59_1588_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|Package updates for [CVE-2022-43750](https://nvd.nist.gov/vuln/detail/CVE-2022-43750){: external}. |
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}} |N/A|N/A|N/A|
| Haproxy |N/A|N/A|N/A|
{: caption="Changes since version 4.9.59_1587_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.59_1587_openshift, released 27 April 2023
{: #4959_1587M_openshift}

The following table shows the changes that are in the master fix pack 4.9.59_1587_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.17 | v1.3.19 | Updated `Go` to version `1.19.8` and updated dependencies. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1366-amd64 | 1390-amd64 | Eliminate IP syscall. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.0 | v2.4.5 | Updated universal base image (UBI) to resolve CVEs. Updated `Go` to version `1.19.8` and updated dependencies. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.17-5 | v1.22.17-8 | Update `Go` dependencies. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 429 | 431 | Updated `Go` to version `1.19.8` and updated dependencies. Update UBI base image. |
| Key Management Service provider | v2.6.4 | v2.6.5 | Updated `Go` to version `1.19.7` and updated dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2420 | 2486 | Updated `Go` to version `1.19.7` and updated dependencies. |
| {{site.data.keyword.openshiftshort}}. | 4.9.57 | 4.9.59 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-59){: external}. |
| OpenVPN Operator image | v1.4.22 | v1.4.23 | Updated base image to resolve CVEs: [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}, [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2023-0361](https://nvd.nist.gov/vuln/detail/CVE-2023-0361){: external}. |
| Portieris admission controller | v0.13.3 | v0.13.4 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.4){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator and Metrics Server | 4.9.0-20230314 | 4.9.0-20230417 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20230417){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.9.0+20230314 | 4.9.0+20230417 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20230417){: external}. |
{: caption="Changes since version 4.9.57_1583_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.59_1587_openshift, released 24 April 2023
{: #4959_1587_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.59_1587_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}} |N/A|N/A|N/A|
| Haproxy |N/A|N/A|N/A|
{: caption="Changes since version 4.9.59_1585_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.59_1585_openshift, released 11 April 2023
{: #4959_1585_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.59_1585_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2023-0767](https://nvd.nist.gov/vuln/detail/CVE-2023-0767){: external}. |
| RHEL 8 Packages | 4.18.0-425.13.1 | 4.18.0-425.19.2 | Worker node kernel & package updates for [CVE-2022-4269](https://nvd.nist.gov/vuln/detail/CVE-2022-4269){: external}, [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4378](https://nvd.nist.gov/vuln/detail/CVE-2022-4378){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}, [CVE-2023-0266](https://nvd.nist.gov/vuln/detail/CVE-2023-0266){: external}, [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2023-0361](https://nvd.nist.gov/vuln/detail/CVE-2023-0361){: external}, [CVE-2023-0386](https://nvd.nist.gov/vuln/detail/CVE-2023-0386){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.57 | 4.9.59 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-59){: external}. |
| Haproxy | 8398d1 | 8895ad | [CVE-2023-0361](https://nvd.nist.gov/vuln/detail/CVE-2023-0361){: external}. |
{: caption="Changes since version 4.9.57_1584_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.57_1583_openshift, released 28 March 2023
{: #4957_1583_openshift}

The following table shows the changes that are in the master fix pack 4.9.57_1583_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.16 | v1.3.17 | Updated `Go` to version `1.19.7` and updated dependencies. |
| etcd | v3.4.23 | v3.4.24 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.24){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1308-amd64 | 1366-amd64 | Updated to resolve [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.7 | v2.4.0 | Removed ExpandInUsePersistentVolumes feature gate. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 427 | 429 | Updated universal base image (UBI) to resolve CVEs. Updated `Go` to version `1.19.6` and updated dependencies. |
| Key Management Service provider | v2.6.3 | v2.6.4 | Updated `Go` to version `1.19.7` and updated dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2383 | 2420 | Updated the image to resolve CVEs. |
| OpenVPN Operator image | v1.4.20 | v1.4.22 | Updated `ansible-operator` to `v1.28.0` to fix CVEs. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.9.55 | 4.9.57 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-57){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.9.0-20230220 | v4.9.0-20230314 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20230314){: external}. |
{: caption="Changes since version 4.9.55_1579_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.57_1584_openshift, released 27 March 2023
{: #4957_1584_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.57_1584_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. |N/A|N/A|N/A|
| Haproxy | af5031 | 8398d1 | [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}. |
{: caption="Changes since version 4.9.57_1580_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.57_1580_openshift, released 13 March 2023
{: #4957_1580_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.57_1580_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.83.1 | 3.10.0-1160.87.1 | Worker node kernel & package updates for [CVE-2018-13405](https://nvd.nist.gov/vuln/detail/CVE-2018-13405){: external}, [CVE-2021-4037](https://nvd.nist.gov/vuln/detail/CVE-2021-4037){: external}, [CVE-2022-2639](https://nvd.nist.gov/vuln/detail/CVE-2022-2639){: external}, [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}, [CVE-2022-42703](https://nvd.nist.gov/vuln/detail/CVE-2022-42703){: external}, [CVE-2022-4378](https://nvd.nist.gov/vuln/detail/CVE-2022-4378){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node package updates for [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.56 | 4.9.57 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-57){: external}. |
{: caption="Changes since version 4.9.56_1576_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.55_1579_openshift, released 2 March 2023
{: #4955_1579_openshift}

The following table shows the changes that are in the master fix pack 4.9.55_1579_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.15 | v1.3.16 | Updated `Go` dependencies and to `Go` version `1.19.6`. Updated universal base image (UBI) to resolve CVEs. |
| etcd | v3.4.22 | v3.4.23 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.23){: external}. |
| Gateway-enabled cluster controller | 1902 | 1987 | Updated `armada-utils` to version `v1.9.35` |
| {{site.data.keyword.IBM_notm}} Calico extension | 1305-amd64 | 1308-amd64 | Updated universal base image (UBI) to resolve [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.6 | v2.3.7 | Updated universal base image (UBI) to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.17-2 | v1.22.17-5 | Updated `vpcctl binary` to `3601`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 425 | 427 | Updated universal base image (UBI) to resolve CVEs. |
| Key Management Service provider | v2.5.13 | v2.6.3 | Updated `Go` dependencies and to `Go` version `1.19.6`. |
| Load balancer and Load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2325 | 2383 | Updated to `armada-utils` version `1.9.35`. |
| OpenVPN client | 2.5.6-r1-IKS-648 | 2.5.8-r0-IKS-674-amd64 | Remediate [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}. |
| OpenVPN server | 2.5.6-r1-IKS-647 | 2.5.8-r0-IKS-673-amd64 | Remediate [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}. |
| OpenVPN Operator image | v1.4.13 | v1.4.20 | Update `ansible-operator` to `v1.26.1` to fix CVEs. |
| Portieris admission controller | v0.12.6 | v0.13.3 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.3){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.54 | 4.9.55 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-55){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.9.0-20230123 | v4.9.0-20230220 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0%2B20230220){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.9.0-20230123 | v4.9.0-20230220 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0%2B20230220){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.9.0+20230123 | 4.9.0+20230220 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20230220){: external}. |
{: caption="Changes since version 4.9.54_1573_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.56_1576_openshift, released 27 February 2023
{: #4956_1576_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.56_1576_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-425.10.1 | 4.18.0-425.13.1 | Worker node & kernel package updates for [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2022-2873](https://nvd.nist.gov/vuln/detail/CVE-2022-2873){: external}, [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/CVE-2022-40897){: external}, [CVE-2022-41222](https://nvd.nist.gov/vuln/detail/CVE-2022-41222){: external}, [CVE-2022-43945](https://nvd.nist.gov/vuln/detail/CVE-2022-43945){: external}, [CVE-2022-4415](https://nvd.nist.gov/vuln/detail/CVE-2022-4415){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}, [CVE-2022-48303](https://nvd.nist.gov/vuln/detail/CVE-2022-48303){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.54 | 4.9.56 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-56){: external}. |
| HAProxy | d38f89 | af5031 | [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/CVE-2022-40897){: external}, [CVE-2022-4415](https://nvd.nist.gov/vuln/detail/CVE-2022-4415){: external}, [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}. |
{: caption="Changes since version 4.9.54_1575_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.54_1575_openshift, released 13 February 2023
{: #4954_1575_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.54_1575_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages |N/A|N/A| Worker node package updates for [CVE-2022-23521](https://nvd.nist.gov/vuln/detail/CVE-2022-23521){: external}, [CVE-2022-41903](https://nvd.nist.gov/vuln/detail/CVE-2022-41903){: external}, [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}. |
| {{site.data.keyword.openshiftshort}}. |N/A|N/A|N/A|
| HAProxy | 8d6ea6 | 08c969 | [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}. |
{: caption="Changes since version 4.9.54_1574_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.54_1573_openshift, released 30 January 2023
{: #4954_1573_openshift}

The following table shows the changes that are in the master fix pack 4.9.54_1573_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.22.5 | v3.23.5 | See the [Calico release notes](https://docs.tigera.io/archive/v3.23/release-notes/#v3235){: external}. |
| Calico Operator | v1.25.13 | v1.27.17 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.27.17){: external}. |
| Cluster health image | v1.3.14 | v1.3.15 | Updated `Go` dependencies and to `Go` version `1.19.4`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1257 | 1280 | Publish s390x image. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.4 | v2.3.6 | Updated universal base image (UBI) to `8.7-1031` |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.16-1 | v1.22.17-2 | Updated to support the `Kubernetes 1.22.17` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 421 | 425 | Fixes for Fixing [CVE-2022-40303](https://nvd.nist.gov/vuln/detail/CVE-2022-40303){: external} and [CVE-2022-40304](https://nvd.nist.gov/vuln/detail/CVE-2022-40303){: external}. |
| Key Management Service provider | v2.5.12 | v2.5.13 | Updated `Go` dependencies and to `Go` version `1.19.4`. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.9.0-20221205 | v4.9.0-20230123 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20230123){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.9.52 | 4.9.54 | See the [{{site.data.keyword.openshiftlong_notm}} Release Notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-54){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.9.0-20221205 | v4.9.0-20230123 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20230123){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.9.0+20221205 | 4.9.0+20230123 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20230123){: external}. |
{: caption="Changes since version 4.9.52_1568_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.54_1574_openshift, released 30 January 2023
{: #4954_1574_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.54_1574_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.81 | 3.10.0-1160.83 | Worker node kernel & package updates for [CVE-2017-5715](https://nvd.nist.gov/vuln/detail/CVE-2017-5715){: external}, [CVE-2021-25220](https://nvd.nist.gov/vuln/detail/CVE-2021-25220){: external}, [CVE-2021-26401](https://nvd.nist.gov/vuln/detail/CVE-2021-26401){: external}, [CVE-2022-2795](https://nvd.nist.gov/vuln/detail/CVE-2022-2795){: external}, [CVE-2022-2964](https://nvd.nist.gov/vuln/detail/CVE-2022-2964){: external}, [CVE-2023-22809](https://nvd.nist.gov/vuln/detail/CVE-2023-22809){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node kernel & package updates for [CVE-2022-40303](https://nvd.nist.gov/vuln/detail/CVE-2022-40303){: external}, [CVE-2022-40304](https://nvd.nist.gov/vuln/detail/CVE-2022-40304){: external}, [CVE-2023-22809](https://nvd.nist.gov/vuln/detail/CVE-2023-22809){: external}. |
| {{site.data.keyword.openshiftshort}}. |N/A|N/A|N/A|
| HAProxy | 508bf6 | 8d6ea6 | [CVE-2022-42010](https://nvd.nist.gov/vuln/detail/CVE-2022-42010){: external}, [CVE-2022-42011](https://nvd.nist.gov/vuln/detail/CVE-2022-42011){: external}, [CVE-2022-42012](https://nvd.nist.gov/vuln/detail/CVE-2022-42012){: external}, [CVE-2022-40303](https://nvd.nist.gov/vuln/detail/CVE-2022-40303){: external}, [CVE-2022-40304](https://nvd.nist.gov/vuln/detail/CVE-2022-40304){: external}, [CVE-2022-3821](https://nvd.nist.gov/vuln/detail/CVE-2022-3821){: external}, [CVE-2022-35737](https://nvd.nist.gov/vuln/detail/CVE-2022-35737){: external}, [CVE-2022-43680](https://nvd.nist.gov/vuln/detail/CVE-2022-43680){: external}, [CVE-2021-46848](https://nvd.nist.gov/vuln/detail/CVE-2021-46848){: external}. |
{: caption="Changes since version 4.9.54_1571_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.54_1571_openshift, released 16 January 2023
{: #4954_1571_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.54_1571_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-425.3.1 | 4.18.0-425.10.1 | Worker node kernel & package updates for [CVE-2021-46848](https://nvd.nist.gov/vuln/detail/CVE-2021-46848){: external}, [CVE-2022-2601](https://nvd.nist.gov/vuln/detail/CVE-2022-2601){: external}, [CVE-2022-2964](https://nvd.nist.gov/vuln/detail/CVE-2022-2964){: external}, [CVE-2022-35737](https://nvd.nist.gov/vuln/detail/CVE-2022-35737){: external}, [CVE-2022-3775](https://nvd.nist.gov/vuln/detail/CVE-2022-3775){: external}, [CVE-2022-3821](https://nvd.nist.gov/vuln/detail/CVE-2022-3821){: external}, [CVE-2022-4139](https://nvd.nist.gov/vuln/detail/CVE-2022-4139){: external}, [CVE-2022-42010](https://nvd.nist.gov/vuln/detail/CVE-2022-42010){: external}, [CVE-2022-42011](https://nvd.nist.gov/vuln/detail/CVE-2022-42011){: external}, [CVE-2022-42012](https://nvd.nist.gov/vuln/detail/CVE-2022-42012){: external}, [CVE-2022-43680](https://nvd.nist.gov/vuln/detail/CVE-2022-43680){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.53 | 4.9.54 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-54){: external}. |
{: caption="Changes since version 4.9.53_1570_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.53_1570_openshift, released 02 January 2023
{: #4953_1570_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.53_1570_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}} |N/A|N/A|N/A|
{: caption="Changes since version 4.9.53_1569_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.53_1569_openshift, released 19 December 2022
{: #4953_1569_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.53_1569_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.80 | 3.10.0-1160.81 | Worker node kernel & package updates for [CVE-2022-28733](https://nvd.nist.gov/vuln/detail/CVE-2022-28733){: external}. |
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.9.52 | 4.9.53 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-53){: external}. |
{: caption="Changes since version 4.9.52_1567_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.52_1568_openshift, released 14 December 2022
{: #4952_1568_openshift}

The following table shows the changes that are in the master fix pack 4.9.52_1568_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.13 | v1.3.14 | Updated `Go` dependencies. Exclude ingress status from cluster status aggregation. |
| etcd | v3.4.21 | v3.4.22 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.22){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1213 | 1257 | Updated universal base image (UBI) to resolve: [CVE-2022-1304](https://nvd.nist.gov/vuln/detail/cve-2022-1304){: external}, [CVE-2016-3709](https://nvd.nist.gov/vuln/detail/CVE-2016-3709){: external}, [CVE-2022-42898](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-42898){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.3 | v2.3.4 | Update `Go` to version `1.18.8` and updated universal base image (UBI) to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.15-7 | v1.22.16-1 | Updated to support the `Kubernetes 1.22.16` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 420 | 421 | Updated universal base image (UBI) to resolve [CVE-2022-42898](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-42898){: external}. Updated `Go` to version `1.18.8` |
| Key Management Service provider | v2.5.11 | v2.5.12 | Updated `Go` dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2110 | 2325 | Update `Go` to version `1.19.1` and update dependencies. |
| OpenVPN Operator image | v1.4.11 | v1.4.13 | Updated the `ansible operator base image` to `v1.25.2` to resolve CVEs. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.9.0-20221104 | v4.9.0-20221205 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20221205){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.9.51 | 4.9.52 | See the [{{site.data.keyword.openshiftlong_notm}} Release Notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-52){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server and toolkit | v4.9.0-20221104 | v4.9.0-20221205 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20221205){: external}. |
{: caption="Changes since version 4.9.51_1565_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.52_1567_openshift, released 05 December 2022
{: #4952_1567_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.52_1567_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-42898](https://nvd.nist.gov/vuln/detail/CVE-2022-42898){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node package updates for [CVE-2022-42898](https://nvd.nist.gov/vuln/detail/CVE-2022-42898){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.51 | 4.9.52 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-52){: external}. |
| HAProxy | c619f4 | 508bf6 | [CVE-2016-3709](https://nvd.nist.gov/vuln/detail/CVE-2016-3709){: external}, [CVE-2022-42898](https://nvd.nist.gov/vuln/detail/CVE-2022-42898){: external}, [CVE-2022-1304](https://nvd.nist.gov/vuln/detail/CVE-2022-1304){: external}. |
{: caption="Changes since version 4.9.51_1566_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.51_1566_openshift, released 21 November 2022
{: #4951_1566_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.51_1566_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-21233](https://nvd.nist.gov/vuln/detail/CVE-2022-21233){: external}, [CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external}, [CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external}, [CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external}, [CVE-2022-26373](https://nvd.nist.gov/vuln/detail/CVE-2022-26373){: external}, [CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external}, [CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external}, [CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node package updates for [CVE-2015-20107](https://nvd.nist.gov/vuln/detail/CVE-2015-20107){: external}, [CVE-2016-3709](https://nvd.nist.gov/vuln/detail/CVE-2016-3709){: external}, [CVE-2020-0256](https://nvd.nist.gov/vuln/detail/CVE-2020-0256){: external}, [CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external}, [CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external}, [CVE-2020-36516](https://nvd.nist.gov/vuln/detail/CVE-2020-36516){: external}, [CVE-2020-36558](https://nvd.nist.gov/vuln/detail/CVE-2020-36558){: external}, [CVE-2021-0308](https://nvd.nist.gov/vuln/detail/CVE-2021-0308){: external}, [CVE-2021-25220](https://nvd.nist.gov/vuln/detail/CVE-2021-25220){: external}, [CVE-2021-30002](https://nvd.nist.gov/vuln/detail/CVE-2021-30002){: external}, [CVE-2021-36221](https://nvd.nist.gov/vuln/detail/CVE-2021-36221){: external}, [CVE-2021-3640](https://nvd.nist.gov/vuln/detail/CVE-2021-3640){: external}, [CVE-2021-41190](https://nvd.nist.gov/vuln/detail/CVE-2021-41190){: external}, [CVE-2022-0168](https://nvd.nist.gov/vuln/detail/CVE-2022-0168){: external}, [CVE-2022-0494](https://nvd.nist.gov/vuln/detail/CVE-2022-0494){: external}, [CVE-2022-0617](https://nvd.nist.gov/vuln/detail/CVE-2022-0617){: external}, [CVE-2022-0854](https://nvd.nist.gov/vuln/detail/CVE-2022-0854){: external}, [CVE-2022-1016](https://nvd.nist.gov/vuln/detail/CVE-2022-1016){: external}, [CVE-2022-1048](https://nvd.nist.gov/vuln/detail/CVE-2022-1048){: external}, [CVE-2022-1055](https://nvd.nist.gov/vuln/detail/CVE-2022-1055){: external}, [CVE-2022-1184](https://nvd.nist.gov/vuln/detail/CVE-2022-1184){: external}, [CVE-2022-1304](https://nvd.nist.gov/vuln/detail/CVE-2022-1304){: external}, [CVE-2022-1353](https://nvd.nist.gov/vuln/detail/CVE-2022-1353){: external}, [CVE-2022-1708](https://nvd.nist.gov/vuln/detail/CVE-2022-1708){: external}, [CVE-2022-1852](https://nvd.nist.gov/vuln/detail/CVE-2022-1852){: external}, [CVE-2022-20368](https://nvd.nist.gov/vuln/detail/CVE-2022-20368){: external}, [CVE-2022-2078](https://nvd.nist.gov/vuln/detail/CVE-2022-2078){: external}, [CVE-2022-21499](https://nvd.nist.gov/vuln/detail/CVE-2022-21499){: external}, [CVE-2022-22624](https://nvd.nist.gov/vuln/detail/CVE-2022-22624){: external}, [CVE-2022-22628](https://nvd.nist.gov/vuln/detail/CVE-2022-22628){: external}, [CVE-2022-22629](https://nvd.nist.gov/vuln/detail/CVE-2022-22629){: external}, [CVE-2022-22662](https://nvd.nist.gov/vuln/detail/CVE-2022-22662){: external}, [CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external}, [CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external}, [CVE-2022-23960](https://nvd.nist.gov/vuln/detail/CVE-2022-23960){: external}, [CVE-2022-24448](https://nvd.nist.gov/vuln/detail/CVE-2022-24448){: external}, [CVE-2022-24795](https://nvd.nist.gov/vuln/detail/CVE-2022-24795){: external}, [CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external}, [CVE-2022-2586](https://nvd.nist.gov/vuln/detail/CVE-2022-2586){: external}, [CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external}, [CVE-2022-26373](https://nvd.nist.gov/vuln/detail/CVE-2022-26373){: external}, [CVE-2022-2639](https://nvd.nist.gov/vuln/detail/CVE-2022-2639){: external}, [CVE-2022-26700](https://nvd.nist.gov/vuln/detail/CVE-2022-26700){: external}, [CVE-2022-26709](https://nvd.nist.gov/vuln/detail/CVE-2022-26709){: external}, [CVE-2022-26710](https://nvd.nist.gov/vuln/detail/CVE-2022-26710){: external}, [CVE-2022-26716](https://nvd.nist.gov/vuln/detail/CVE-2022-26716){: external}, [CVE-2022-26717](https://nvd.nist.gov/vuln/detail/CVE-2022-26717){: external}, [CVE-2022-26719](https://nvd.nist.gov/vuln/detail/CVE-2022-26719){: external}, [CVE-2022-27191](https://nvd.nist.gov/vuln/detail/CVE-2022-27191){: external}, [CVE-2022-27404](https://nvd.nist.gov/vuln/detail/CVE-2022-27404){: external}, [CVE-2022-27405](https://nvd.nist.gov/vuln/detail/CVE-2022-27405){: external}, [CVE-2022-27406](https://nvd.nist.gov/vuln/detail/CVE-2022-27406){: external}, [CVE-2022-27950](https://nvd.nist.gov/vuln/detail/CVE-2022-27950){: external}, [CVE-2022-28390](https://nvd.nist.gov/vuln/detail/CVE-2022-28390){: external}, [CVE-2022-28893](https://nvd.nist.gov/vuln/detail/CVE-2022-28893){: external}, [CVE-2022-29162](https://nvd.nist.gov/vuln/detail/CVE-2022-29162){: external}, [CVE-2022-2938](https://nvd.nist.gov/vuln/detail/CVE-2022-2938){: external}, [CVE-2022-29581](https://nvd.nist.gov/vuln/detail/CVE-2022-29581){: external}, [CVE-2022-2989](https://nvd.nist.gov/vuln/detail/CVE-2022-2989){: external}, [CVE-2022-2990](https://nvd.nist.gov/vuln/detail/CVE-2022-2990){: external}, [CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external}, [CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external}, [CVE-2022-30293](https://nvd.nist.gov/vuln/detail/CVE-2022-30293){: external}, [CVE-2022-32746](https://nvd.nist.gov/vuln/detail/CVE-2022-32746){: external}, [CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external}, [CVE-2022-36946](https://nvd.nist.gov/vuln/detail/CVE-2022-36946){: external}, [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}, [CVE-2022-3787](https://nvd.nist.gov/vuln/detail/CVE-2022-3787){: external}, [CVE-2022-40674](https://nvd.nist.gov/vuln/detail/CVE-2022-40674){: external}, [CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| {{site.data.keyword.openshiftshort}}. |N/A|N/A|N/A|
{: caption="Changes since version 4.9.51_1563_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.51_1565_openshift, released 16 November 2022
{: #4951_1565_openshift}

The following table shows the changes that are in the master fix pack 4.9.51_1565_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.22.4 | v3.22.5 | See the [Calico release notes](https://docs.tigera.io/archive/v3.22/release-notes/#v3225){: external}. |
| Calico Operator | v1.25.11 | v1.25.13 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.25.13){: external}. |
| Cluster health image | v1.3.12 | v1.3.13 | Updated Go dependencies, `golangci-lint`, `gosec`, and to `Go` version 1.19.3. Updated base image version to 116. |
| etcd | v3.4.18 | v3.4.21 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.21){: external}. |
| Gateway-enabled cluster controller | 1823 | 1902 | `Go` module updates. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1096 | 1213 | Updated image to fix the following CVEs: [CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external}, [CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external}, [CVE-2022-3515](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-3515){: external}, [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}, [CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external}, [CVE-2022-32149](https://nvd.nist.gov/vuln/detail/CVE-2022-32149){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.1 | v2.3.3 | Updated universal base image (UBI) to version `8.7-923` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.15-3 | v1.22.15-7 | Key rotation and updated `Go` dependencies. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 416 | 420 | Updated universal base image (UBI) to version `8.7-923` to resolve CVEs. |
| Key Management Service provider | v2.5.10 | v2.5.11 | Updated `Go` dependencies and to `Go` version `1.19.3`. |
| OpenVPN Operator image | v1.4.10 | v1.4.11 | Updated `ansible operator base image` to `v1.24.0` to resolve CVEs. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.9.0-20220920 | v4.9.0-20221104 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20221104){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.9.49 | 4.9.51 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-51){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server and toolkit | v4.9.0-20220920 | v4.9.0-20221104 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20221104){: external}. |
{: caption="Changes since version 4.9.49_1561_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.51_1564_openshift, released 11 November 2022
{: #4951_1564_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.51_1564_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-372.32.1.el8_6 | 4.18.0-425.3.1.el8 | Worker node kernel & package updates for [CVE-2021-36221](https://nvd.nist.gov/vuln/detail/CVE-2021-36221){: external}, [CVE-2022-1708](https://nvd.nist.gov/vuln/detail/CVE-2022-1708){: external}, [CVE-2022-27191](https://nvd.nist.gov/vuln/detail/CVE-2022-27191){: external}, [CVE-2021-41190](https://nvd.nist.gov/vuln/detail/CVE-2021-41190){: external}, [CVE-2022-2990](https://nvd.nist.gov/vuln/detail/CVE-2022-2990){: external}, [CVE-2022-29162](https://nvd.nist.gov/vuln/detail/CVE-2022-29162){: external}, [CVE-2022-2989](https://nvd.nist.gov/vuln/detail/CVE-2022-2989){: external}, [CVE-2022-2990](https://nvd.nist.gov/vuln/detail/CVE-2022-2990){: external}, [CVE-2020-36516](https://nvd.nist.gov/vuln/detail/CVE-2020-36516){: external}, [CVE-2020-36558](https://nvd.nist.gov/vuln/detail/CVE-2020-36558){: external}, [CVE-2021-3640](https://nvd.nist.gov/vuln/detail/CVE-2021-3640){: external}, [CVE-2021-30002](https://nvd.nist.gov/vuln/detail/CVE-2021-30002){: external}, [CVE-2022-0168](https://nvd.nist.gov/vuln/detail/CVE-2022-0168){: external}, [CVE-2022-0617](https://nvd.nist.gov/vuln/detail/CVE-2022-0617){: external}, [CVE-2022-0854](https://nvd.nist.gov/vuln/detail/CVE-2022-0854){: external}, [CVE-2022-1016](https://nvd.nist.gov/vuln/detail/CVE-2022-1016){: external}, [CVE-2022-1048](https://nvd.nist.gov/vuln/detail/CVE-2022-1048){: external}, [CVE-2022-1055](https://nvd.nist.gov/vuln/detail/CVE-2022-1055){: external}, [CVE-2022-1184](https://nvd.nist.gov/vuln/detail/CVE-2022-1184){: external}, [CVE-2022-1852](https://nvd.nist.gov/vuln/detail/CVE-2022-1852){: external}, [CVE-2022-2078](https://nvd.nist.gov/vuln/detail/CVE-2022-2078){: external}, [CVE-2022-2586](https://nvd.nist.gov/vuln/detail/CVE-2022-2586){: external}, [CVE-2022-2639](https://nvd.nist.gov/vuln/detail/CVE-2022-2639){: external}, [CVE-2022-2938](https://nvd.nist.gov/vuln/detail/CVE-2022-2938){: external}, [CVE-2022-20368](https://nvd.nist.gov/vuln/detail/CVE-2022-20368){: external}, [CVE-2022-21499](https://nvd.nist.gov/vuln/detail/CVE-2022-21499){: external}, [CVE-2022-23960](https://nvd.nist.gov/vuln/detail/CVE-2022-23960){: external}, [CVE-2022-26373](https://nvd.nist.gov/vuln/detail/CVE-2022-26373){: external}, [CVE-2022-27950](https://nvd.nist.gov/vuln/detail/CVE-2022-27950){: external}, [CVE-2022-28390](https://nvd.nist.gov/vuln/detail/CVE-2022-28390){: external}, [CVE-2022-28893](https://nvd.nist.gov/vuln/detail/CVE-2022-28893){: external}, [CVE-2022-29581](https://nvd.nist.gov/vuln/detail/CVE-2022-29581){: external}, [CVE-2022-36946](https://nvd.nist.gov/vuln/detail/CVE-2022-36946){: external}, [CVE-2022-24448](https://nvd.nist.gov/vuln/detail/CVE-2022-24448){: external}. |
{: caption="Changes since version 4.9.51_1563_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.51_1563_openshift, released 07 November 2022
{: #4951_1563_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.51_1563_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.76.1 | 3.10.0-1160.80.1 | Worker node kernel & package updates for [CVE-2022-21233](https://nvd.nist.gov/vuln/detail/CVE-2022-21233){: external}, [CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external}, [CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external}, [CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external}, [CVE-2022-26373](https://nvd.nist.gov/vuln/detail/CVE-2022-26373){: external}, [CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external}, [CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external}, [CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| RHEL 8 Packages | 4.18.0-372.26.1 | 4.18.0-372.32.1 | Worker node kernel & package updates for [CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external}, [CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external}, [CVE-2022-0494](https://nvd.nist.gov/vuln/detail/CVE-2022-0494){: external}, [CVE-2022-1353](https://nvd.nist.gov/vuln/detail/CVE-2022-1353){: external}, [CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external}, [CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external}, [CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external}, [CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external}, [CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external}, [CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external}, [CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external}, [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}, [CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.50 | 4.9.51 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-51){: external}. |
| HAProxy | b034b2 | 3a1392 | [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}, [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}, [CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external}, [CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external}, [CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external}, [CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external}. |
{: caption="Changes since version 4.9.50_1559_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.49_1561_openshift, released 27 October 2022
{: #4949_1561_openshift}

The following table shows the changes that are in the master fix pack 4.9.49_1561_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.11 | v1.3.12 | Updated `Go` dependencies, golangci-lint, and to `Go` version 1.19.2. Updated base image version to 109. Excluded ingress status from cluster status calculation. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.14-2 | v1.22.15-3 | Updated to support the `Kubernetes 1.22.15` release. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | dc1725a | 778ef2b | Updated to `Go` version `1.18.6`. |
| Key Management Service provider | v2.5.9 | v2.5.10 | Updated `Go` dependencies and to `Go` version `1.19.2`. |
| OpenVPN Operator image | v1.4.9 | v1.4.10 | Updated ansible operator base image to v1.24.0 to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.9.48 | 4.9.49 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-49){: external}. |
{: caption="Changes since version 4.9.481556openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.50_1562_openshift, released 27 October 2022
{: #4950_1562_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.50_1562_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| VPC Gen 2 RHEL 8 worker image disk size | N/A | N/A | Fixed regression on previous version where root filesystem partition was 25 GB instead of 100GB for VPC Gen 2 |
{: caption="Changes since version 4.9.50_1559_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.50_1559_openshift, released 25 October 2022
{: #4950_1559_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.50_1559_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}} | 4.9.49 | 4.9.50 | See the [change logs](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-50){: external}. |
{: caption="Changes since version 4.9.49_1558_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.49_1558_openshift, released 10 October 2022
{: #4949_1558_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.49_1558_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.9.48 | 4.9.49 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-49){: external}. |
{: caption="Changes since version 4.9.48_1557_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.48_1556_openshift, released 26 September 2022
{: #4948_1556_openshift}

The following table shows the changes that are in the master fix pack 4.9.48_1556_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.10 | v1.3.11 | Updated `Go` dependencies and to `Go` version `1.18.6`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1006 | 1096 | Updated image for [CVE-2022-2526](https://nvd.nist.gov/vuln/detail/CVE-2022-2526){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.9 | v2.3.1 | Updated to `Go` version `1.18.6`. Updated universal base image (UBI) to version `8.6-941` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.13-1 | v1.22.14-2 | Updated to support the Kubernetes `1.22.14` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 414 | 416 | Updated to `Go` version `1.18.6`. Updated universal base image (UBI) to version `8.6-941` to resolve CVEs. |
| Key Management Service Provider | v2.5.8 | v2.5.9 | Updated `Go` dependencies and to `Go` version `1.18.6`. |
| {{site.data.keyword.openshiftshort}} | 4.9.46 | 4.9.48 | See the [{{site.data.keyword.openshiftshort}} Release Notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-48){: external}. |
| OpenVPN Operator image | v1.4.8 | v1.4.9 | Updated ansible operator base image to `v1.23.0` to resolve CVEs. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.9.0-20220816 | v4.9.0-20220920 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220920){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.9.0-20220816 | v4.9.0-20220920 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220920){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.9.0+20220816 | 4.9.0+20220920 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220920){: external}. |
{: caption="Changes since version 4.9.461554openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.48_1557_openshift, released 26 September 2022
{: #4948_1557_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.48_1557_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-372.19.1 | 4.18.0-372.26.1 |N/A|
| {{site.data.keyword.openshiftshort}}. | 4.9.47 | 4.9.48 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-48){: external}. |
{: caption="Changes since version 4.9.47_1555_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.47_1555_openshift, released 12 September 2022
{: #4947_1555_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.47_1555_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.9.46 | 4.9.47 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-47){: external}. |
{: caption="Changes since version 4.9.46_1553_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.46_1554_openshift, released 1 September 2022
{: #4946_1554_openshift}

The following table shows the changes that are in the master fix pack 4.9.46_1554_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.22.2 | v3.22.4 | See the [Calico release notes](https://docs.tigera.io/archive/v3.22/release-notes/#v3224){: external}. Updated the Calico custom resource definitions to include `preserveUnknownFields: false`. |
| Calico Operator | v1.25.7 | v1.25.11 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.25.11){: external}. |
| Cluster health image | v1.3.9 | v1.3.10 | Updated `Go` dependencies and to `Go` version `1.18.5`. |
| Gateway-enabled cluster controller | 1792 | 1823 | Updated to `Go` version `1.17.13`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 997 | 1006 | Updated to `Go` version `1.17.13`. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.8 | v2.2.9 | Updated to `Go` version `1.18.5`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.11-3 | v1.22.13-1 | Updated `vpcctl` binary to version `3367`. Updated to support the Kubernetes `1.22.13` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 412 | 414 | Updated to `Go` version `1.18.5`. Updated universal base image (UBI) to version `8.6-902` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 0a187a4 | dc1725a | Updated `Go` dependencies and to `Go` version `1.18.3`. |
| Key Management Service provider | v2.5.7 | v2.5.8 | Updated `Go` dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2058 | 2110 | Updated `Go` dependencies and to `Go` version `1.17.13`. |
| {{site.data.keyword.openshiftshort}}. | 4.9.42 | 4.9.46 | See the [{{site.data.keyword.openshiftshort}} Release Notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-46){: external}. |
| OpenVPN client | 2.5.6-r1-IKS-629 | 2.5.6-r1-IKS-648 | Update image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external} and [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}. |
| OpenVPN Operator image | v1.4.7 | v1.4.8 | Updated Ansible operator base image to version `v1.22.2` to resolve CVEs. |
| OpenVPN server | 2.5.6-r1-IKS-628 | 2.5.6-r1-IKS-647 | Update image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external} and [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}. |
| Portieris admission controller | v0.12.5 | v0.12.6 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.12.6){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.9.0-20220712 | v4.9.0-20220816 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0%2B20220816){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.9.0-20220712 | v4.9.0-20220816 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0%2B20220816){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.9.0+20220712 | 4.9.0+20220816 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220816){: external}. |
{: caption="Changes since version 4.9.42_1548_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.46_1553_openshift, released 29 August 2022
{: #4946_1553_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.46_1553_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-2526](https://nvd.nist.gov/vuln/detail/CVE-2022-2526){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.45 | 4.9.46 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-46){: external}. |
| HAProxy | 6514a2 | c1634f | [CVE-2022-32206](https://nvd.nist.gov/vuln/detail/CVE-2022-32206){: external}, [CVE-2022-32208](https://nvd.nist.gov/vuln/detail/CVE-2022-32208){: external}
{: caption="Changes since version 4.9.45_1550_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.45_1550_openshift, released 16 August 2022
{: #4945_1550_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.45_1550_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.71.1 | 3.10.0-1160.76.1 | Worker node package updates for [CVE-2022-0005](https://nvd.nist.gov/vuln/detail/CVE-2022-0005){: external}, [CVE-2022-21123](https://nvd.nist.gov/vuln/detail/CVE-2022-21123){: external}, [CVE-2022-21125](https://nvd.nist.gov/vuln/detail/CVE-2022-21125){: external}, [CVE-2022-21127](https://nvd.nist.gov/vuln/detail/CVE-2022-21127){: external}, [CVE-2022-21131](https://nvd.nist.gov/vuln/detail/CVE-2022-21131){: external}, [CVE-2022-21136](https://nvd.nist.gov/vuln/detail/CVE-2022-21136){: external}, [CVE-2022-21151](https://nvd.nist.gov/vuln/detail/CVE-2022-21151){: external}, [CVE-2022-21166](https://nvd.nist.gov/vuln/detail/CVE-2022-21166){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.43 | 4.9.45 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-45){: external}. |
{: caption="Changes since version 4.9.43_1549_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.43_1549_openshift, released 01 August 2022
{: #4943_1549_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.43_1549_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.9.42 | 4.9.43 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-43){: external}. |
{: caption="Changes since version 4.9.42_1547_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.42_1548_openshift, released 26 July 2022
{: #4942_1548_openshift}

The following table shows the changes that are in the master fix pack 4.9.42_1548_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.8 | v1.3.9 | Updated `Go` dependencies and to use `Go` version `1.18.4`. Fixed minor typographical error in the add-on `daemonset not available` health status. |
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
{: caption="Changes since version 4.9.37_1544_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.42_1547_openshift, released 18 July 2022
{: #4942_1547_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.42_1547_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.66.1 | 3.10.0-1160.71.1 | Worker node package updates for [CVE-2020-26116](https://nvd.nist.gov/vuln/detail/CVE-2020-26116){: external}, [CVE-2020-26137](https://nvd.nist.gov/vuln/detail/CVE-2020-26137){: external}, [CVE-2021-3177](https://nvd.nist.gov/vuln/detail/CVE-2021-3177){: external}, [CVE-2022-0391](https://nvd.nist.gov/vuln/detail/CVE-2022-0391){: external}, [CVE-2022-1729](https://nvd.nist.gov/vuln/detail/CVE-2022-1729){: external}, [CVE-2022-1966](https://nvd.nist.gov/vuln/detail/CVE-2022-1966){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.40 | 4.9.42 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-42){: external}. |
{: caption="Changes since version 4.9.40_1546_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.40_1546_openshift, released 11 July 2022
{: #4940_1546_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.40_1546_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| General |N/A|N/A| Fix to address a bug that occurred if you used the persistent volume claim NFS v3 storage. |
{: caption="Changes since version 4.9.40_1545_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.40_1545_openshift, released 05 July 2022
{: #4940_1545_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.40_1545_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.9.38 | 4.9.40 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-40){: external}. |
{: caption="Changes since version 4.9.38_1543_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.37_1544_openshift, released 22 June 2022
{: #4937_1544_openshift}

The following table shows the changes that are in the master fix pack 4.9.37_1544_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.4 | v2.2.6 | Bug fixes for the driver installation. Block plugin base images were updated to `ubi`: `8.6-751.1655117800` for CVE-2022-1271 |
| Calico | v3.21.5 | v3.22.2 | See the [Calico release notes](https://docs.tigera.io/archive/v3.22/release-notes/#v3222){: external}. |
| Calico Operator | v1.23.7 | v1.25.7 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.25.7){: external}. |
| Cluster health image | v1.3.7 | v1.3.8 | Updated `Go` to version `1.17.11` and also updated the dependencies. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.10-1 | v1.22.10-3 | Update prometheus/client_golang@v1.11.0 to `v1.11.1`. |
| Key Management Service provider | v2.5.5 | v2.5.6 | Updated `Go` to version `1.17.11` and also updated the dependencies. |
| OpenVPN Operator image | v1.4.5 | v1.4.6 | Update base image to version `v1.22.0` to resolve CVEs. |
| {{site.data.keyword.openshiftshort}}. | 4.9.33 | 4.9.37 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-37){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.9.0-20220509 | v4.9.0-20220614 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0%2B20220614){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Metrics Server and toolkit | v4.9.0-20220509 | v4.9.0-20220614 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0%2B20220614){: external}. |
{: caption="Changes since version 4.9.33_1540_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.38_1543_openshift, released 20 June 2022
{: #4938_1543_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.38_1543_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}. |
| HAProxy | 468c09 | 04f862 | [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.36 | 4.9.38 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-38){: external}. |
{: caption="Changes since version 4.9.36_1541_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.36_1541_openshift, released 7 June 2022
{: #4936_1541_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.36_1541_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-24903](https://nvd.nist.gov/vuln/detail/CVE-2022-24903){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.9.33 | 4.9.36 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-36){: external}. |
{: caption="Changes since version 4.9.33_1539_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.33_1540_openshift, released 3 June 2022
{: #4933_1540_openshift}

The following table shows the changes that are in the master fix pack 4.9.33_1540_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.6 | v1.3.7 | Updated `Go` to version `1.17.10` and also updated the dependencies. Update registry base image version to `104` |
| {{site.data.keyword.IBM_notm}} Calico extension | 954 | 980 | Updated to use `Go` version `1.17.10`. Updated minimal universal base image (UBI) to version `8.5`. |
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
{: caption="Changes since version 4.9.28_1536_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.33_1539_openshift, released 23 May 2022
{: #4933_1539_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.33_1539_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.9.31 | 4.9.33 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-33){: external}. |
| RHEL 7 Packages | 3.10.0-1160.62.1 | 3.10.0-1160.66.1 | Worker node kernel & package updates for [CVE-2018-25032](https://nvd.nist.gov/vuln/detail/CVE-2018-25032){: external}, [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}, [CVE-2022-0492](https://nvd.nist.gov/vuln/detail/CVE-2022-0492){: external}. |
| HA proxy | 36b0307 | 468c09 | [CVE-2021-3634](https://nvd.nist.gov/vuln/detail/CVE-2021-3634){: external}. |
{: caption="Changes since version 4.9.31_1538_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.31_1538_openshift, released 09 May 2022
{: #4931_1538_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.31_1538_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | N/A |
| {{site.data.keyword.openshiftshort}}. | 4.9.29 | 4.9.31 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-31){: external}. |
| HAProxy | f53b22 | 36b030 | [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}, [CVE-2022-1154](https://nvd.nist.gov/vuln/detail/CVE-2022-1154){: external}, [CVE-2018-25032](https://nvd.nist.gov/vuln/detail/CVE-2018-25032){: external}. |
{: caption="Changes since version 4.9.29_1537_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.28_1536_openshift, released 26 April 2022
{: #4928_1536_openshift}

The following table shows the changes that are in the master fix pack 4.9.28_1536_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.21.4 | v3.21.5 | See the [Calico release notes](https://docs.tigera.io/archive/v3.21/release-notes/.#v3215){: external}. |
| Calico Operator | v1.23.5 | v1.23.7 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.23.7){: external}. |
| Cluster health image | v1.3.5 | v1.3.6 | Updated `Go` to version `1.17.9` and also updated the dependencies. Update `registry base image` version to `103`. |
| Gateway-enabled cluster controller | 1669 | 1680 | Updated metadata for a rotated key. |
| {{site.data.keyword.IBM_notm}} Calico extension | 950 | 954 | Updated to latest minimal universal base image (UBI) to resolve [CVE-2021-3999](https://nvd.nist.gov/vuln/detail/CVE-2021-3999){: external}, [CVE-2022-23218](https://nvd.nist.gov/vuln/detail/CVE-2022-23218){: external}, [CVE-2022-23219](https://nvd.nist.gov/vuln/detail/CVE-2022-23219){: external}, [CVE-2022-23308](https://nvd.nist.gov/vuln/detail/CVE-2022-23308){: external}, [CVE-2021-23177](https://nvd.nist.gov/vuln/detail/CVE-2021-23177){: external}, and [CVE-2021-31566](https://nvd.nist.gov/vuln/detail/CVE-2021-31566){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.1 | v2.2.2 | Updated universal base image (UBI) to `8.5-240.1648458092` |
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
{: caption="Changes since version 4.9.25_1534_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.29_1537_openshift, released 25 April 2022
{: #4929_1537_openshift}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | Package updates. |
| {{site.data.keyword.openshiftshort}}. | 4.9.26 | 4.9.29 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-29){: external}. |
{: caption="Changes since version 4.9.26_1535_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.26_1535_openshift, released 11 April 2022
{: #4926_1535_openshift}

The following table shows the changes that are in the worker node fix pack 4.9.26_1535_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL Packages | 3.10.0-1160.59.1 | 3.10.0-1160.62.1 | Kernel and package updates for   [CVE-2021-45960](https://nvd.nist.gov/vuln/detail/CVE-2021-45960)   [CVE-2021-46143](https://nvd.nist.gov/vuln/detail/CVE-2021-46143)   [CVE-2022-22822](https://nvd.nist.gov/vuln/detail/CVE-2022-22822)   [CVE-2022-22823](https://nvd.nist.gov/vuln/detail/CVE-2022-22823)   [CVE-2022-22824](https://nvd.nist.gov/vuln/detail/CVE-2022-22824)   [CVE-2022-22825](https://nvd.nist.gov/vuln/detail/CVE-2022-22825)   [CVE-2022-22826](https://nvd.nist.gov/vuln/detail/CVE-2022-22826)   [CVE-2022-22827](https://nvd.nist.gov/vuln/detail/CVE-2022-22827)   [CVE-2022-23852](https://nvd.nist.gov/vuln/detail/CVE-2022-23852)   [CVE-2022-25235](https://nvd.nist.gov/vuln/detail/CVE-2022-25235)   [CVE-2022-25236](https://nvd.nist.gov/vuln/detail/CVE-2022-25236)   [CVE-2022-25315](https://nvd.nist.gov/vuln/detail/CVE-2022-25315)   [CVE-2021-4028](https://nvd.nist.gov/vuln/detail/CVE-2021-4028)   [CVE-2021-4083](https://nvd.nist.gov/vuln/detail/CVE-2021-4083)   [CVE-2022-0778](https://nvd.nist.gov/vuln/detail/CVE-2022-0778). |
| OpenShift | 4.9.25 | 4.9.26 | See [change logs](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-26){: external}. |
{: caption="Changes since version 4.9.25_1532_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.25_1534_openshift, released 6 April 2022
{: #4.9.25_1534}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.3 | v1.3.5 | Update golang dependencies.  Update image to version 102 to fix CVEs [CVE-2021-3999](https://access.redhat.com/security/cve/cve-2021-3999){: external}, [CVE-2022-23218](https://nvd.nist.gov/vuln/detail/CVE-2022-23218){: external}, [CVE-2022-23219](https://nvd.nist.gov/vuln/detail/CVE-2022-23219){: external} |
| IBM Calico extension | 929 | 950 | Updated to use `Go` version `1.17.8`. Updated universal base image (UBI) to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.1.7 | v2.2.1 | Bug fixes for driver installation issues.  Updated universal base image (UBI) to `8.5-240` and updated `Go` to version to `1.16.15`.  Fixes for CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.7-2 | v1.22.8-3 | Updated to support the Kubernetes 1.22.8 release and to use Go version 1.16.15. |
| {{site.data.keyword.cloud_notm}} File Storage plug-in and monitor | 405 | 407 | Updated `Go` to version `1.16.14`.  Updated universal base image (UBI) to version `8.5-240`. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 0fc9949 | 6c43ef1 | Upgraded `Go` packages to resolve vulnerabilities |
| Gateway-enabled cluster controller | 1653 | 1669 | Updated to use `Go` version `1.17.8`. |
| Key Management Service provider | v2.5.2 | v2.5.3 | Updated to use `Go` version `1.17.8`. Updated golang dependencies.  Fixed CVE [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external} |
| Load balancer and Load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1747 | 1899 | Revert setting gratuitous `ARP` on LBv1.  Updated the image to resolve CVEs. Updated to use `Go` version `1.17.8`. |
| Red Hat OpenShift | 4.9.21 | 4.9.25 | See the [Red Hat OpenShift release notes](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-25){: external} |
| Red hat OpenShift Control Plane Operator | v4.9.0-20220222 | v4.9.0-20220322 | See the [Red Hat OpenShift on {{site.data.keyword.cloud_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220322){: external}. |
| Red Hat OpenShift on {{site.data.keyword.cloud_notm}} Metrics Server | v4.9.0-20220222 | v4.9.0-20220322 | See the [Red Hat OpenShift on {{site.data.keyword.cloud_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220322){: external}. |
| Red Hat OpenShift on {{site.data.keyword.cloud_notm}} toolkit | 4.9.0+20220222 | 4.9.0+20220322 | See the [Red Hat OpenShift on {{site.data.keyword.cloud_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220322){: external}. |
| OpenVPN client | 2.5.4-r0-IKS-556 | 2.5.4-r0-IKS-579 | Updated `Go` to version `1.16.15`. |
| OpenVPN server | 2.5.4-r0-IKS-562 | 2.5.4-r0-IKS-578 | Updated `Go` to version `1.16.15`. |
| OpenVPN Operator image | v1.4.1 | v1.4.2 | Updated ansible operator base image to version `v1.18.0` to resolve CVEs. |
| Portieris admission controller | v0.12.2 | v0.12.3 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.12.3){: external} |
{: caption="Changes since version 4.9.21_1528_openshift" caption-side="bottom"}


### Change log for worker node pack 4.9.25_1532_openshift, released 28 March 2022
{: #4925_1532}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | N/A |
| HA proxy | 15198f | b40c07 | [CVE-2021-45960](https://nvd.nist.gov/vuln/detail/CVE-2021-45960){: external}, [CVE-2021-46143](https://nvd.nist.gov/vuln/detail/CVE-2021-46143){: external}, [CVE-2022-22822](https://nvd.nist.gov/vuln/detail/CVE-2022-22822){: external}, [CVE-2022-22823](https://nvd.nist.gov/vuln/detail/CVE-2022-22823){: external}, [CVE-2022-22824](https://nvd.nist.gov/vuln/detail/CVE-2022-22824){: external}, [CVE-2022-22825](https://nvd.nist.gov/vuln/detail/CVE-2022-22825){: external}, [CVE-2022-22826](https://nvd.nist.gov/vuln/detail/CVE-2022-22826){: external}, [CVE-2022-22827](https://nvd.nist.gov/vuln/detail/CVE-2022-22827){: external}, [CVE-2022-23852](https://nvd.nist.gov/vuln/detail/CVE-2022-23852){: external}, [CVE-2022-25235](https://nvd.nist.gov/vuln/detail/CVE-2022-25235){: external}, [CVE-2022-25236](https://nvd.nist.gov/vuln/detail/CVE-2022-25236){: external}, [CVE-2022-25315](https://nvd.nist.gov/vuln/detail/CVE-2022-25315){: external}, [CVE-2021-3999](https://nvd.nist.gov/vuln/detail/CVE-2021-3999){: external}, [CVE-2022-23218](https://nvd.nist.gov/vuln/detail/CVE-2022-23218){: external}, [CVE-2022-23219](https://nvd.nist.gov/vuln/detail/CVE-2022-23219){: external}, [CVE-2022-23308](https://nvd.nist.gov/vuln/detail/CVE-2022-23308){: external}, [CVE-2021-23177](https://nvd.nist.gov/vuln/detail/CVE-2021-23177){: external}, [CVE-2021-31566](https://nvd.nist.gov/vuln/detail/CVE-2021-31566){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.9.23 | 4.9.25 | See [change logs](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-25){: external}. |
{: caption="Changes since version 4.9.23_1530_openshift_openshift" caption-side="bottom"}


### Change log for worker node pack 4.9.23_1530_openshift, released 14 March 2022
{: #4923_1530}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | N/A |
| {{site.data.keyword.redhat_openshift_notm}} | 4.9.22 | 4.9.23 | See the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-23){: external}. |
{: caption="Changes since version 4.9.22_1529_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.21_1528_openshift, released 3 March 2022
{: #4921_1528}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.0 | v1.3.3 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds fix for [CVE-2021-43565](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-43565){: external}. Adds Golang dependency updates. |
| Gateway-enabled cluster controller | 1586 | 1653 | Updated to use `Go` version `1.17.7` and updated `Go` modules to fix CVEs. |
| {{site.data.keyword.IBM_notm}} Calico extension | 923 | 929 | Updated universal base image (UBI) to the `8.5-230` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | v2.1.6 | v2.1.7 | Fix for [CVE-2021-3538](https://nvd.nist.gov/vuln/detail/CVE-2021-3538){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.22.6-1 | v1.22.7-2 | Updated to support the Kubernetes `1.22.7` release and to use `Go` version `1.16.14`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 404 | 405 | Adds fix for [CVE-2021-3538](https://nvd.nist.gov/vuln/detail/CVE-2021-3538){: external} and adds dependency updates. |
| Key Management Service provider | v2.4.0 | v2.5.2 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds fix for [CVE-2021-43565](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-43565){: external}. Adds Golang dependency updates. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.9.17 | 4.9.21 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-21){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.9.0-20220201 | v4.9.0-20220222 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220222){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Metrics Server | v4.9.0-20220201 | v4.9.0-20220222 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220222){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} toolkit | 4.9.0+20220201 | 4.9.0+20220222 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.9.0+20220222){: external}. |
| OpenVPN server | 2.5.4-r0-IKS-555 | 2.5.4-r0-IKS-562 | Turns off CRL verification in the openvpn image. |
| OpenVPN Operator image | v1.4.0 | v1.4.1 | Turns off CRL verification in the opevpn-operator image. |
{: caption="Changes since version 4.9.17_1525_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.22_1529_openshift, released 28 February 2022
{: #4922_1529}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.53.1.el7 | 3.10.0-1160.59.1.el7 | Kernel and package updates for [CVE-2020-25709](https://nvd.nist.gov/vuln/detail/CVE-2020-25709){: external}, [CVE-2020-25710](https://nvd.nist.gov/vuln/detail/CVE-2020-25710){: external}, [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}, [CVE-2020-0465](https://nvd.nist.gov/vuln/detail/CVE-2020-0465){: external}, [CVE-2020-0466](https://nvd.nist.gov/vuln/detail/CVE-2020-0466){: external}, [CVE-2021-0920](https://nvd.nist.gov/vuln/detail/CVE-2021-0920){: external}, [CVE-2021-3564](https://nvd.nist.gov/vuln/detail/CVE-2021-3564){: external}, [CVE-2021-3573](https://nvd.nist.gov/vuln/detail/CVE-2021-3573){: external}, [CVE-2021-3752](https://nvd.nist.gov/vuln/detail/CVE-2021-3752){: external}, [CVE-2021-4155](https://nvd.nist.gov/vuln/detail/CVE-2021-4155){: external}, [CVE-2022-0330](https://nvd.nist.gov/vuln/detail/CVE-2022-0330){: external}, [CVE-2022-22942](https://nvd.nist.gov/vuln/detail/CVE-2022-22942){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.9.19 | 4.9.22 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-22){: external} | 
| HA proxy | f6a2b3 | 15198fb | Contains fixes for [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}. | 
{: caption="Changes since version 4.9.19_1526_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.9.19_1526_openshift, released 14 February 2022
{: #4919_1526}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | N/A |
| {{site.data.keyword.redhat_openshift_notm}} | N/A | 4.9.19 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-19){: external}. |
| HA proxy | d38fa1 | f6a2b3 | [CVE-2021-3521](https://nvd.nist.gov/vuln/detail/CVE-2021-3521){: external}, [CVE-2021-4122](https://nvd.nist.gov/vuln/detail/CVE-2021-4122){: external}. |
{: caption="Changes since version 4.9.17_1523_openshift" caption-side="bottom"}


### Change log for master fix pack 4.9.17_1525_openshift and worker node fix pack 4.9.17_1523_openshift, released 9 February 2022
{: #4917_1525}

The following table shows the changes that are in the master fix pack `4.9.17_1525_openshift` and worker node fix pack `4.9.17_1523_openshift`. Master patch updates are applied automatically. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.20.3 | v3.21.4 | See the [Calico release notes](https://docs.tigera.io/archive){: external}. |
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
{: caption="Changes since version 4.8.26_1542_openshift master and 4.8.28_1543_openshift worker node." caption-side="bottom"}


