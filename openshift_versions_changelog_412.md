---

copyright:
  years: 2023, 2023
lastupdated: "2023-06-30"

keywords: openshift, 4.12, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# Version 4.12 change log
{: #openshift_changelog_412}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.12. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #openshift_changelog_overview_412}

Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security){: external} for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}


### Change log for master fix pack 4.12.20_1549_openshift, released 27 June 2023
{: #41220_1549_openshift_M}

The following table shows the changes that are in the master fix pack 4.12.20_1549_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico Operator | v1.29.3 | v1.29.4 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.29.4){: external}. |
| Cluster health image | v1.3.20 | v1.3.21 | Updated `Go` dependencies and to `Go` version `1.19.10`. |
| etcd | v3.5.8 | v3.5.9 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.9){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.9-7 | v1.25.11-1 | Updated to support the `Kubernetes 1.25.11` release. Updated `Go` dependencies and to `Go` version `1.19.10`. Updated `calicoctl` and `vpcctl`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 431 | 433 | Updated `Go` to version `1.20.4`. Updated UBI base image. |
| Key Management Service provider | v2.6.6 | v2.6.7 | Updated `Go` dependencies and to `Go` version `1.19.10`. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2486 | 2584 | Updated `Go` dependencies and to `Go` version `1.19.9`. Updated base image. |
| {{site.data.keyword.openshiftshort}} | 4.12.16 | 4.12.20 | https://docs.openshift.com/container-platform/ |
| OpenVPN client | 2.5.8-r0-IKS-674-amd64 | 2.6.4-r0-IKS-34-amd64 | Upgrade `openvpn` to version `2.6.4-r0`. |
| OpenVPN server | 2.5.8-r0-IKS-673-amd64 | 2.6.4-r0-IKS-33-amd64 | Upgrade `openvpn` to version `2.6.4-r0`. |
| OpenVPN Operator image | v1.4.23 | v1.4.25 | Updated OpenVPN configuration to provide shutdown grace period before terminating connections. |
{: caption="Changes since version 4.12.16_1545_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.21_1547_openshift, released 19 June 2023
{: #41221_1547_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.21_1547_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. |4.12.19|4.12.21|see [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-21){: external}. |
| RHEL 8 Packages | N/A | N/A | Worker node package updates for [CVE-2023-32067](https://nvd.nist.gov/vuln/detail/CVE-2023-32067){: external},[CVE-2023-24329](https://nvd.nist.gov/vuln/detail/CVE-2023-24329){: external}. |
{: caption="Changes since version 4.12.19_1546_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.19_1546_openshift, released 5 June 2023
{: #41219_1546_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.19_1546_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.16 | 4.12.19 | see [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-19){: external}. |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-477.10.1.el8_8 | 4.18.0-477.13.1.el8_8 | Worker node kernel & package updates for [CVE-2023-22490](https://nvd.nist.gov/vuln/detail/CVE-2023-22490){: external}, [CVE-2023-23946](https://nvd.nist.gov/vuln/detail/CVE-2023-23946){: external}, [CVE-2023-25652](https://nvd.nist.gov/vuln/detail/CVE-2023-25652){: external}, [CVE-2023-25815](https://nvd.nist.gov/vuln/detail/CVE-2023-25815){: external}, [CVE-2023-29007](https://nvd.nist.gov/vuln/detail/CVE-2023-29007){: external}, [CVE-2023-32233](https://nvd.nist.gov/vuln/detail/CVE-2023-32233){: external}. |
{: caption="Changes since version 4.12.16_1544_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.16_1545_openshift, released 25 May 2023
{: #41216_1545_openshift_M}

The following table shows the changes that are in the master fix pack 4.12.16_1545_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.19 | v1.3.20 | Updated `Go` to version `1.19.9` and updated dependencies. Updated the base image. Resolved add-on health bugs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.9-2 | v1.25.9-7 | Updated support of the Kubernetes 1.25.9 release. Updated Go dependencies. Key rotation. |
| Key Management Service provider | v2.6.5 | v2.6.6 | Updated `Go` to version `1.19.9` and updated dependencies. |
| OpenVPN client | 2.6.4-r0-IKS-27 | 2.5.8-r0-IKS-674 | Reverted to previous version. |
| OpenVPN server | 2.6.4-r0-IKS-26 | 2.5.8-r0-IKS-673 | Reverted to previous version. |
| Portieris admission controller | v0.13.4 | v0.13.5 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.5){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.12.13 | 4.12.16 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-16){: external}. |
{: caption="Changes since version 4.12.13_1541_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.16_1544_openshift, released 23 May 2023
{: #41216_1544_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.16_1544_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.12.15 | 4.12.16 | see [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-16){: external}. |
| RHEL 8 Packages | 4.18.0-425.19.2.el8_7 | 4.18.0-477.10.1.el8_8 | Worker node kernel & package updates for [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-26341](https://nvd.nist.gov/vuln/detail/CVE-2021-26341){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2021-33655](https://nvd.nist.gov/vuln/detail/CVE-2021-33655){: external}, [CVE-2021-33656](https://nvd.nist.gov/vuln/detail/CVE-2021-33656){: external}, [CVE-2022-1462](https://nvd.nist.gov/vuln/detail/CVE-2022-1462){: external}, [CVE-2022-1679](https://nvd.nist.gov/vuln/detail/CVE-2022-1679){: external}, [CVE-2022-1705](https://nvd.nist.gov/vuln/detail/CVE-2022-1705){: external}, [CVE-2022-1789](https://nvd.nist.gov/vuln/detail/CVE-2022-1789){: external}, [CVE-2022-1962](https://nvd.nist.gov/vuln/detail/CVE-2022-1962){: external}, [CVE-2022-20141](https://nvd.nist.gov/vuln/detail/CVE-2022-20141){: external}, [CVE-2022-2196](https://nvd.nist.gov/vuln/detail/CVE-2022-2196){: external}, [CVE-2022-24765](https://nvd.nist.gov/vuln/detail/CVE-2022-24765){: external}, [CVE-2022-25265](https://nvd.nist.gov/vuln/detail/CVE-2022-25265){: external}, [CVE-2022-2663](https://nvd.nist.gov/vuln/detail/CVE-2022-2663){: external}, [CVE-2022-27664](https://nvd.nist.gov/vuln/detail/CVE-2022-27664){: external}, [CVE-2022-2795](https://nvd.nist.gov/vuln/detail/CVE-2022-2795){: external}, [CVE-2022-28131](https://nvd.nist.gov/vuln/detail/CVE-2022-28131){: external}, [CVE-2022-29187](https://nvd.nist.gov/vuln/detail/CVE-2022-29187){: external}, [CVE-2022-2928](https://nvd.nist.gov/vuln/detail/CVE-2022-2928){: external}, [CVE-2022-2929](https://nvd.nist.gov/vuln/detail/CVE-2022-2929){: external}, [CVE-2022-3028](https://nvd.nist.gov/vuln/detail/CVE-2022-3028){: external}, [CVE-2022-30594](https://nvd.nist.gov/vuln/detail/CVE-2022-30594){: external}, [CVE-2022-30629](https://nvd.nist.gov/vuln/detail/CVE-2022-30629){: external}, [CVE-2022-30630](https://nvd.nist.gov/vuln/detail/CVE-2022-30630){: external}, [CVE-2022-30631](https://nvd.nist.gov/vuln/detail/CVE-2022-30631){: external}, [CVE-2022-30632](https://nvd.nist.gov/vuln/detail/CVE-2022-30632){: external}, [CVE-2022-30633](https://nvd.nist.gov/vuln/detail/CVE-2022-30633){: external}, [CVE-2022-30635](https://nvd.nist.gov/vuln/detail/CVE-2022-30635){: external}, [CVE-2022-32148](https://nvd.nist.gov/vuln/detail/CVE-2022-32148){: external}, [CVE-2022-32189](https://nvd.nist.gov/vuln/detail/CVE-2022-32189){: external}, [CVE-2022-3239](https://nvd.nist.gov/vuln/detail/CVE-2022-3239){: external}, [CVE-2022-3522](https://nvd.nist.gov/vuln/detail/CVE-2022-3522){: external}, [CVE-2022-3524](https://nvd.nist.gov/vuln/detail/CVE-2022-3524){: external}, [CVE-2022-35252](https://nvd.nist.gov/vuln/detail/CVE-2022-35252){: external}, [CVE-2022-3564](https://nvd.nist.gov/vuln/detail/CVE-2022-3564){: external}, [CVE-2022-3566](https://nvd.nist.gov/vuln/detail/CVE-2022-3566){: external}, [CVE-2022-3567](https://nvd.nist.gov/vuln/detail/CVE-2022-3567){: external}, [CVE-2022-3619](https://nvd.nist.gov/vuln/detail/CVE-2022-3619){: external}, [CVE-2022-36227](https://nvd.nist.gov/vuln/detail/CVE-2022-36227){: external}, [CVE-2022-3623](https://nvd.nist.gov/vuln/detail/CVE-2022-3623){: external}, [CVE-2022-3625](https://nvd.nist.gov/vuln/detail/CVE-2022-3625){: external}, [CVE-2022-3628](https://nvd.nist.gov/vuln/detail/CVE-2022-3628){: external}, [CVE-2022-3707](https://nvd.nist.gov/vuln/detail/CVE-2022-3707){: external}, [CVE-2022-39188](https://nvd.nist.gov/vuln/detail/CVE-2022-39188){: external}, [CVE-2022-39189](https://nvd.nist.gov/vuln/detail/CVE-2022-39189){: external}, [CVE-2022-39253](https://nvd.nist.gov/vuln/detail/CVE-2022-39253){: external}, [CVE-2022-39260](https://nvd.nist.gov/vuln/detail/CVE-2022-39260){: external}, [CVE-2022-41218](https://nvd.nist.gov/vuln/detail/CVE-2022-41218){: external}, [CVE-2022-4129](https://nvd.nist.gov/vuln/detail/CVE-2022-4129){: external}, [CVE-2022-41674](https://nvd.nist.gov/vuln/detail/CVE-2022-41674){: external}, [CVE-2022-41717](https://nvd.nist.gov/vuln/detail/CVE-2022-41717){: external}, [CVE-2022-41973](https://nvd.nist.gov/vuln/detail/CVE-2022-41973){: external}, [CVE-2022-4269](https://nvd.nist.gov/vuln/detail/CVE-2022-4269){: external}, [CVE-2022-42703](https://nvd.nist.gov/vuln/detail/CVE-2022-42703){: external}, [CVE-2022-42720](https://nvd.nist.gov/vuln/detail/CVE-2022-42720){: external}, [CVE-2022-42721](https://nvd.nist.gov/vuln/detail/CVE-2022-42721){: external}, [CVE-2022-42722](https://nvd.nist.gov/vuln/detail/CVE-2022-42722){: external}, [CVE-2022-43552](https://nvd.nist.gov/vuln/detail/CVE-2022-43552){: external}, [CVE-2022-43750](https://nvd.nist.gov/vuln/detail/CVE-2022-43750){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}, [CVE-2022-47929](https://nvd.nist.gov/vuln/detail/CVE-2022-47929){: external}, [CVE-2023-0394](https://nvd.nist.gov/vuln/detail/CVE-2023-0394){: external}, [CVE-2023-0461](https://nvd.nist.gov/vuln/detail/CVE-2023-0461){: external}, [CVE-2023-0778](https://nvd.nist.gov/vuln/detail/CVE-2023-0778){: external}, [CVE-2023-1195](https://nvd.nist.gov/vuln/detail/CVE-2023-1195){: external}, [CVE-2023-1582](https://nvd.nist.gov/vuln/detail/CVE-2023-1582){: external}, [CVE-2023-23454](https://nvd.nist.gov/vuln/detail/CVE-2023-23454){: external}, [CVE-2023-27535](https://nvd.nist.gov/vuln/detail/CVE-2023-27535){: external}. |
| Haproxy | N/A |N/A|N/A|
{: caption="Changes since version 4.12.15_1542_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.13_1541_openshift, released 2 May 2023
{: #41213_1541_openshift}

The following table shows the changes that are in the master fix pack 4.12.13_1540_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| etcd | v3.5.7 | v3.5.8 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.8){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.9-1 | v1.25.9-2 | Update `Go` dependencies |
| {{site.data.keyword.openshiftshort}}. | 4.12.11 | 4.12.13 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-13){: external}. |
{: caption="Changes since version 4.12.11_1538_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.11_1539_openshift, released 27 April 2023
{: #41211_1539_openshift}

The following table shows the changes that are in the master fix pack 4.12.11_1538_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.25.0 | v3.25.1 | See the [Calico release notes](https://docs.tigera.io/calico/latest/release-notes/#v3.25.1){: external}. |
| Calico Operator | v1.29.0 | v1.29.3 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.29.3){: external}. |
| Cluster health image | v1.3.17 | v1.3.19 | Updated `Go` to version `1.19.8` and updated dependencies. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1366-amd64 | 1390-amd64 | Eliminate IP syscall. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.0 | v2.4.5 | Updated universal base image (UBI) to resolve CVEs. Updated `Go` to version `1.19.8` and updated dependencies. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.8-1 | v1.25.9-1 | Updated to support the Kubernetes `1.25.9` release. Updated `Go` dependencies and to `Go` version `1.19.8`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 429 | 431 | Updated `Go` to version `1.19.8` and updated dependencies. Update UBI base image. |
| Key Management Service provider | v2.6.4 | v2.6.5 | Updated `Go` to version `1.19.7` and updated dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2420 | 2486 | Updated `Go` to version `1.19.7` and updated dependencies. |
| {{site.data.keyword.openshiftshort}}. | 4.12.7 | 4.12.11 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-11){: external}. |
| {{site.data.keyword.openshiftshort}} configuration | N/A | N/A | Set proper topology spread constraints for the default {{site.data.keyword.openshiftshort}} image registry configuration used by classic clusters. |
| OpenVPN Operator image | v1.4.22 | v1.4.23 | Updated base image to resolve CVEs: [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}, [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2023-0361](https://nvd.nist.gov/vuln/detail/CVE-2023-0361){: external}. |
| Portieris admission controller | v0.13.3 | v0.13.4 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.4){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator and Metrics Server | 4.12.0-20230314 | 4.12.0-20230417 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20230417){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.12.0+20230314 | 4.12.0+20230417 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20230417){: external}. |
{: caption="Changes since version 4.12.7_1534_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.15_1542_openshift, released 24 April 2023
{: #41215_1542_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.12.15_1542_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.12.13 | 4.12.15 | See [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-15){: external}. |
| Haproxy |N/A|N/A|N/A|
{: caption="Changes since version 4.12.13_1539_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.13_1539_openshift, released 24 April 2023
{: #41213_1539_openshift}

The following table shows the changes that are in the worker node fix pack 4.12.13_1539_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.12.10 | 4.12.13 | See [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-13){: external}. |
| Haproxy |N/A|N/A|N/A|
{: caption="Changes since version 4.12.10_1536_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.10_1536_openshift, released 11 April 2023
{: #41210_1536_openshift}

The following table shows the changes that are in the worker node fix pack 4.12.10_1536_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages | 4.18.0-425.13.1 | 4.18.0-425.19.2 | Worker node kernel & package updates for [CVE-2022-4269](https://nvd.nist.gov/vuln/detail/CVE-2022-4269){: external}, [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4378](https://nvd.nist.gov/vuln/detail/CVE-2022-4378){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}, [CVE-2023-0266](https://nvd.nist.gov/vuln/detail/CVE-2023-0266){: external}, [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2023-0361](https://nvd.nist.gov/vuln/detail/CVE-2023-0361){: external}, [CVE-2023-0386](https://nvd.nist.gov/vuln/detail/CVE-2023-0386){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.12.8 | 4.12.10 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-10){: external}. |
| Haproxy | 8398d1 | 8895ad | [CVE-2023-0361](https://nvd.nist.gov/vuln/detail/CVE-2023-0361){: external}. |
{: caption="Changes since version 4.12.8_1535_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.7_1534_openshift, released 28 March 2023
{: #4127_1534_openshift}

The following table shows the changes that are in the master fix pack 4.12.7_1534_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.16 | v1.3.17 | Updated `Go` to version `1.19.7` and updated dependencies. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1308-amd64 | 1366-amd64 | Updated to resolve [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.7 | v2.4.0 | Removed ExpandInUsePersistentVolumes feature gate. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.6-10 | v1.25.8-1 | Updated to support the `Kubernetes 1.25.8` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 427 | 429 | Updated universal base image (UBI) to resolve CVEs. Updated `Go` to version `1.19.6` and updated dependencies. |
| Key Management Service provider | v2.6.3 | v2.6.4 | Updated `Go` to version `1.19.7` and updated dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2383 | 2420 | Updated the image to resolve CVEs. |
| OpenVPN Operator image | v1.5.3 | v1.4.22 | Updated `ansible-operator` to `v1.28.0` to fix CVEs. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.12.3 | 4.12.7 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-7){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.12.0-20230220 | v4.12.0-20230314 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20230314){: external}. |
{: caption="Changes since version 4.12.3_1530_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.8_1535_openshift, released 27 March 2023
{: #4128_1535_openshift}

The following table shows the changes that are in the worker node fix pack 4.12.8_1535_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.12.6 | 4.12.8 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-8){: external}. |
| Haproxy | af5031 | 8398d1 | [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}. |
{: caption="Changes since version 4.12.6_1531_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.6_1531_openshift, released 13 March 2023
{: #4126_1531_openshift}

The following table shows the changes that are in the worker node fix pack 4.12.6_1531_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages |N/A|N/A| Worker node package updates for [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.12.4 | 4.12.6 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-6){: external}. |
{: caption="Changes since version 4.12.4_1528_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.3_1530_openshift, released 2 March 2023
{: #4123_1530_openshift}

The following table shows the changes that are in the master fix pack 4.12.3_1530_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.15 | v1.3.16 | Updated `Go` dependencies and to `Go` version `1.19.6`. Updated universal base image (UBI) to resolve CVEs. |
| etcd | v3.5.6 | v3.5.7 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.7){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1305-amd64 | 1308-amd64 | Updated universal base image (UBI) to resolve [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.25.6-8 | v1.25.6-10 | Updated `Go` dependencies. Updated `k8s.io/utils` digest to `a5ecb01`. |
| OpenVPN client | 2.5.6-r1-IKS-648 | 2.5.8-r0-IKS-674-amd64 | Remediate [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}. |
| OpenVPN server | 2.5.6-r1-IKS-647 | 2.5.8-r0-IKS-673-amd64 | Remediate [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}. |
| OpenVPN Operator image | v1.4.20 | v1.5.2 | Resolve issue with openvpn container restarts |
| {{site.data.keyword.openshiftshort}}. | 4.12.2 | 4.12.3 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-3){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.12.0-20230124 | v4.12.0-20230220 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0%2B20230220){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.12.0-20230124 | v4.12.0-20230220 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0%2B20230220){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.12.0+20230124 | 4.12.0+20230220 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20230220){: external}. |
{: caption="Changes since version 4.12.2_1527_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.12.4_1528_openshift, released 27 February 2023
{: #4124_1528_openshift}

The following table shows the changes that are in the worker node fix pack 4.12.4_1528_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages | 4.18.0-425.10.1 | 4.18.0-425.13.1 | Worker node & kernel package updates for [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2022-2873](https://nvd.nist.gov/vuln/detail/CVE-2022-2873){: external}, [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/CVE-2022-40897){: external}, [CVE-2022-41222](https://nvd.nist.gov/vuln/detail/CVE-2022-41222){: external}, [CVE-2022-43945](https://nvd.nist.gov/vuln/detail/CVE-2022-43945){: external}, [CVE-2022-4415](https://nvd.nist.gov/vuln/detail/CVE-2022-4415){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}, [CVE-2022-48303](https://nvd.nist.gov/vuln/detail/CVE-2022-48303){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.12.2 | 4.12.4 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-4){: external}. |
| HAProxy | d38f89 | af5031 | [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/CVE-2022-40897){: external}, [CVE-2022-4415](https://nvd.nist.gov/vuln/detail/CVE-2022-4415){: external}, [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}. |
{: caption="Changes since version 4.12.2_1526_openshift" caption-side="bottom"}


### Change log for master fix pack 4.12.2_1527_openshift and worker node fix pack 4.12.2_1526_openshift, released 23 February 2023
{: #4122_1527_openshift_4.12.2_1526_openshift}

The following table shows the changes that are in the master fix pack 4.12.2_1627_openshift and worker node fix pack 4.12.2_1526_openshift.  Master patch updates are applied automatically. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.23.5 | v3.25.0 | See the [Calico release notes](https://docs.tigera.io/archive){: external}. Calico configuration now sets a [BGP password](https://docs.tigera.io/calico/latest/reference/resources/bgppeer#bgppassword){: external}. In addition, the `default` `FelixConfiguration` resource is updated to set `natPortRange` to `32768:65535` if not already set. For more information, see [Why am I seeing SNAT port issues and egress connection failures?](/docs/openshift?topic=openshift-ts-network-snat-125). |
| Calico Operator | v1.27.17 | v1.29.0 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.29.0){: external}. |
| Gateway-enabled cluster controller | 1902 | 1987 | Image updated to resolve [CVE-2022-41721](https://nvd.nist.gov/vuln/detail/CVE-2022-41721){: external}, [CVE-2022-41717](https://nvd.nist.gov/vuln/detail/CVE-2022-41717){: external}, [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}, and [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}.  |
| {{site.data.keyword.IBM_notm}} Calico extension | 1280-amd64 | 1305-amd64 | Updated `Go` version to `1.19.5`. |
| {{site.data.keyword.IBM_notm}} Cloud Block Storage driver and plug-in | v2.3.6 | v2.3.7 | Updated `Go` version to `1.18.9`.  Updated universal base image (`UBI`) to version `8.7-1031.1675784874`. |
| {{site.data.keyword.IBM_notm}} Cloud Controller Manager | v1.24.10-2 | v1.25.6-8 | Updated to support the Kubernetes `1.25.6` release. Updated `Go` dependencies and to `Go` version `1.19.5`. |
| {{site.data.keyword.IBM_notm}} Cloud File Storage plug-in and monitor | 425 | 427 | Image updated to resolve [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}. |
| Key Management Service provider | v2.5.13 | v2.6.3 | Key Management Service (KMS) pod termination is delayed until the Kubernetes API server terminates. Updated `Go` dependencies and to `Go` version `1.19.6`. |
| Load balancer and load balancer monitor for {{site.data.keyword.IBM_notm}} Cloud Provider | 2325 | 2383 | Updated `Go` dependencies and to `Go` version `1.19.5`. |
| {{site.data.keyword.redhat_openshift_notm}} (master) | 4.11.22 | 4.12.2 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html){: external}. Updated to resolve [CVE-2022-3172](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-3172){: external}. For more information, see the [Security bulletin](https://www.ibm.com/support/pages/node/6997115){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} (worker node) | 4.11.26 | 4.12.2 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.11.0-20230123 | v4.12.0-20230124 | See the [{{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20230124){: external}. |
| OpenVPN Operator image | v1.4.13 | v1.4.20 | Updated `ansible-operator` base image to version `v1.26.1` to resolve CVEs. |
| Pause container image | 3.8 | 3.9 | See the [pause container image release notes](https://github.com/kubernetes/kubernetes/blob/master/build/pause/CHANGELOG.md){: external}. |
| Portieris admission controller | v0.12.6 | v0.13.3 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.13.3){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud Metrics Server | v4.11.0-20230123 | v4.12.0-20230124 | See the [{{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20230124){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud toolkit | 4.11.0+20230123 | 4.12.0+20230124 | See the [{{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.12.0+20230124){: external}. |
{: caption="Changes since master fix pack 4.11.22_1540_openshift and worker fix pack 4.11.26_1542_openshift" caption-side="bottom"}


