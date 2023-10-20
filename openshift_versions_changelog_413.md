---

copyright:
  years: 2023, 2023
lastupdated: "2023-10-20"

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



### Change log for worker node fix pack 4.13.14_1542_openshift, released 9 October 2023
{: #41314_1542_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.14_1542_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. |4.13.13|4.13.14| For more information, see the [change log](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-14){: external}. |
| RHEL 8 Packages | N/A | N/A | Worker node package updates for [CVE-2023-3341](https://nvd.nist.gov/vuln/detail/CVE-2023-3341){: external}, [CVE-2023-4527](https://nvd.nist.gov/vuln/detail/CVE-2023-4527){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [CVE-2023-4806](https://nvd.nist.gov/vuln/detail/CVE-2023-4806){: external}, [CVE-2023-4813](https://nvd.nist.gov/vuln/detail/CVE-2023-4813){: external}, [CVE-2023-4911](https://nvd.nist.gov/vuln/detail/CVE-2023-4911){: external}. |
{: caption="Changes since version 4.13.13_1541_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.13_1541_openshift, released 27 September 2023
{: #41313_1541_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.13_1541_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.11 | 4.13.13 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-13){: external}. |
| RHEL 8 Packages | 4.18.0-477.21.1.el8_8 | 4.18.0-477.27.1.el8_8 | Worker node kernel & package updates for [CVE-2023-2002](https://nvd.nist.gov/vuln/detail/CVE-2023-2002){: external}, [CVE-2023-3090](https://nvd.nist.gov/vuln/detail/CVE-2023-3090){: external}, [CVE-2023-3390](https://nvd.nist.gov/vuln/detail/CVE-2023-3390){: external}, [CVE-2023-3776](https://nvd.nist.gov/vuln/detail/CVE-2023-3776){: external}, [CVE-2023-4004](https://nvd.nist.gov/vuln/detail/CVE-2023-4004){: external}, [CVE-2023-20593](https://nvd.nist.gov/vuln/detail/CVE-2023-20593){: external}, [CVE-2023-29491](https://nvd.nist.gov/vuln/detail/CVE-2023-29491){: external}, [CVE-2023-30630](https://nvd.nist.gov/vuln/detail/CVE-2023-30630){: external}, [CVE-2023-35001](https://nvd.nist.gov/vuln/detail/CVE-2023-35001){: external}, [CVE-2023-35788](https://nvd.nist.gov/vuln/detail/CVE-2023-35788){: external}. |
{: caption="Changes since version 4.13.11_1534_openshift" caption-side="bottom"}


### Change log for master fix pack 4.13.11_1540_openshift, released 20 September 2023
{: #41311_1540_openshift_M}

The following table shows the changes that are in the master fix pack 4.13.11_1540_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.26.0 | v3.26.1 | See the [Calico release notes](https://docs.tigera.io/calico/latest/release-notes/#v3.26.1){: external}. |
| Calico Operator | v1.30.2 | v1.30.5 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.30.5){: external}. |
| Cluster health image | v1.4.1 | v1.4.2 | Updated `Go` to version `1.20.8` and updated dependencies. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.5 | v2.4.10 | Updated `Go dependencies`. Updated to newer UBI base image. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.26.7-4 | v1.26.8-3 | Updated to support the `Kubernetes 1.26.8` release. Updated `Go` to version `1.20.7` and updated `Go dependencies`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 434 | 435 | Updated `Go` to version `1.20.6` and updated dependencies. Updated to newer UBI base image. |
| Key Management Service provider | v2.8.1 | v2.8.2 | Updated `Go dependencies`. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2631 | 2681 | Updated `Go` to version `1.19.12` and updated `Go dependencies`. |
| {{site.data.keyword.openshiftlong_notm}} | 4.13.6 | 4.13.11 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-11){: external}. |
{: caption="Changes since version 4.13.6_1532_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.11_1534_openshift, released 12 September 2023
{: #41311_1534_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.11_1534_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.9 | 4.13.11 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-11){: external}. |
| RHEL 8 Packages | N/A | N/A | Package updates for [CVE-2022-40982](https://nvd.nist.gov/vuln/detail/CVE-2022-40982){: external}, [CVE-2022-41804](https://nvd.nist.gov/vuln/detail/CVE-2022-41804){: external}, [CVE-2023-23908](https://nvd.nist.gov/vuln/detail/CVE-2023-23908){: external}. |
{: caption="Changes since version 4.13.9_1533_openshift" caption-side="bottom"}


### Change log for master fix pack 4.13.6_1532_openshift, released 30 August 2023
{: #4136_1532_openshift_M}

The following table shows the changes that are in the master fix pack 4.13.6_1532_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.4.0 | v1.4.1 | Updated `Go` to version `1.19.12` and updated dependencies. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.26.7-1 | v1.26.7-4 | Updated `Go` dependencies to resolve a CVE. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 433 | 434 | Updated `Go` to version `1.20.6` and updated dependencies. Updated to newer UBI base image. |
| Key Management Service provider | v2.8.0 | v2.8.1 | Updated `Go` dependencies. |
| OpenVPN client | 2.6.5-r0-IKS-41-amd64 | 2.6.5-r0-IKS-66-amd64 | Updated `openvpn` components to fix CVEs. |
| OpenVPN server | 2.6.5-r0-IKS-40-amd64 | 2.6.5-r0-IKS-57-amd64 | Updated `openvpn` components to fix CVEs. |
| OpenVPN Operator image | v1.4.26 | v1.5.6 | Signal handler fix. |
| Portieris admission controller | v0.13.5 | v0.13.6 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.6){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.13.5 | 4.13.6 | See the [change log](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-6){: external} for more information. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.13.0-20230710 | v4.13.0-20230811 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.13.0%2B20230811){: external}. |
{: caption="Changes since version 4.13.5_1528_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.9_1533_openshift, released 28th August 2023
{: #4139_1533_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.9_1533_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.8 | 4.13.9 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-9){: external}. |
{: caption="Changes since version 4.13.8_1530_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.8_1530_openshift, released 15th August 2023
{: #4138_1530_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.8_1530_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.6 | 4.13.8 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-8){: external}. |
| RHEL 7 Packages| 3.10.0-1160.92.1.el7 | 3.10.0-1160.95.1.el7 | Worker node kernel & package updates for [CVE-2023-38408](https://nvd.nist.gov/vuln/detail/CVE-2023-38408){: external}, [CVE-2022-3564](https://nvd.nist.gov/vuln/detail/CVE-2022-3564){: external}. |
| RHEL 8 Packages| 4.18.0-477.15.1.el8_8 | 4.18.0-477.21.1.el8_8 | Worker node kernel & package updates for [CVE-2022-42896](https://nvd.nist.gov/vuln/detail/CVE-2022-42896){: external}, [CVE-2023-1281](https://nvd.nist.gov/vuln/detail/CVE-2023-1281){: external}, [CVE-2023-1829](https://nvd.nist.gov/vuln/detail/CVE-2023-1829){: external}, [CVE-2023-2124](https://nvd.nist.gov/vuln/detail/CVE-2023-2124){: external}, [CVE-2023-2194](https://nvd.nist.gov/vuln/detail/CVE-2023-2194){: external}, [CVE-2023-2235](https://nvd.nist.gov/vuln/detail/CVE-2023-2235){: external}, [CVE-2023-2602](https://nvd.nist.gov/vuln/detail/CVE-2023-2602){: external}, [CVE-2023-2603](https://nvd.nist.gov/vuln/detail/CVE-2023-2603){: external}, [CVE-2023-27536](https://nvd.nist.gov/vuln/detail/CVE-2023-27536){: external}, [CVE-2023-28321](https://nvd.nist.gov/vuln/detail/CVE-2023-28321){: external}, [CVE-2023-28484](https://nvd.nist.gov/vuln/detail/CVE-2023-28484){: external}, [CVE-2023-29469](https://nvd.nist.gov/vuln/detail/CVE-2023-29469){: external}, [CVE-2023-32681](https://nvd.nist.gov/vuln/detail/CVE-2023-32681){: external}, [CVE-2023-34969](https://nvd.nist.gov/vuln/detail/CVE-2023-34969){: external}, [CVE-2023-38408](https://nvd.nist.gov/vuln/detail/CVE-2023-38408){: external}. |
{: caption="Changes since version 4.13.6_1529_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.6_1529_openshift, released 1 August 2023
{: #4136_1529_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.6_1529_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.4 | 4.13.6 | see [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-6){: external}. |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-3564](https://nvd.nist.gov/vuln/detail/CVE-2022-3564){: external}, [CVE-2023-2828](https://nvd.nist.gov/vuln/detail/CVE-2023-2828){: external}, [CVE-2023-32233](https://nvd.nist.gov/vuln/detail/CVE-2023-32233){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node package update for [CVE-2023-2828](https://nvd.nist.gov/vuln/detail/CVE-2023-2828){: external}. |
{: caption="Changes since version 4.13.4_1526_openshift" caption-side="bottom"}


### Change log for master fix pack 4.13.5_1528_openshift, released 28 July 2023
{: #4135_1528_openshift_M}

The following table shows the changes that are in the master fix pack 4.13.5_1528_openshift. Master patch updates are applied automatically. 


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.21 | v1.4.0 | Updated `Go` to version `1.19.11` and updated `Go` dependencies. Updated UBI base image with FedRAMP enablement support. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.26.6-1 | v1.26.7-1 | Updated to support the Kubernetes `1.26.4` release. Updated `Go` dependencies and to `Go` version `1.20.6`. |
| Key Management Service provider | v2.6.7 | v2.8.0 | Updated `Go` to version `1.19.11` and updated `Go` dependencies. Updated UBI base image with FedRAMP enablement support. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2584 | 2631 | Updated `Go` to version `1.19.10` and updated `Go` dependencies. Updated Alpine base image. |
| OpenVPN client | 2.6.4-r0-IKS-34-amd64 | 2.6.5-r0-IKS-41-amd64 | Updated `OpenVPN` to version `2.6.5`. |
| OpenVPN Operator image | v1.4.25 | v1.4.26 | Updated based image to resolve [CVE-2023-24329](https://nvd.nist.gov/vuln/detail/CVE-2023-24329){: external}, [CVE-2020-24736](https://nvd.nist.gov/vuln/detail/CVE-2020-24736){: external}, [CVE-2023-26604](https://nvd.nist.gov/vuln/detail/CVE-2023-26604){: external}, [CVE-2023-1667](https://nvd.nist.gov/vuln/detail/CVE-2023-1667){: external}, and [CVE-2023-2283](https://nvd.nist.gov/vuln/detail/CVE-2023-2283){: external}. |
| OpenVPN server | 2.6.4-r0-IKS-33-amd64 | 2.6.5-r0-IKS-40-amd64 | Updated `OpenVPN` to version `2.6.5`. |
| {{site.data.keyword.openshiftshort}}. | 4.13.0 | 4.13.5 | Resolves [CVE-2023-1260](https://nvd.nist.gov/vuln/detail/CVE-2023-1260){: external}. For more information, see the [IBM security bulletin](https://www.ibm.com/support/pages/node/7052832){: external}. See the [{{site.data.keyword.openshiftshort}} release notes.](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator and Metrics Server | v4.13.0-20230515 | v4.13.0-20230710 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.13.0+20230710){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.13.0+20230515 | 4.13.0+20230710 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.13.0+20230710){: external}. |
{: caption="Changes since version 4.13.0_1524_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.4_1526_openshift, released 17th July 2023
{: #4134_1526_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.4_1526_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | N/A |N/A|N/A|
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages |N/A|N/A|N/A|
{: caption="Changes since version 4.13.4_1525_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.4_1525_openshift, released 03 July 2023
{: #4134_1525_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.4_1525_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.3 | 4.13.4 | see [change log](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-4){: external}. |
{: caption="Changes since version 4.13.3_1523_openshift" caption-side="bottom"}


### Change log for master fix pack 4.13.0_1524_openshift, released 27 June 2023
{: #4130_1524_openshift_M}

The following table shows the changes that are in the master fix pack 4.13.0_1524_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.20 | v1.3.21 | Updated `Go` dependencies and to `Go` version `1.19.10`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.26.5-5 | v1.26.6-1 | Updated to support the `Kubernetes 1.26.6` release. Updated `Go` dependencies and to `Go` version `1.19.10`. Updated `calicoctl` and `vpcctl`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 431 | 433 | Updated `Go` to version `1.20.4`. Updated UBI base image. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2486 | 2584 | Updated `Go` dependencies and to `Go` version `1.19.9`. Updated base image. |
| OpenVPN client | 2.5.8-r0-IKS-674-amd64 | 2.6.4-r0-IKS-34-amd64 | Upgrade `openvpn` to version `2.6.4-r0`. |
| OpenVPN server | 2.5.8-r0-IKS-673-amd64 | 2.6.4-r0-IKS-33-amd64 | Upgrade `openvpn` to version `2.6.4-r0`. |
| OpenVPN Operator image | v1.4.23 | v1.4.25 | Updated OpenVPN configuration to provide shutdown grace period before terminating connections. |
{: caption="Changes since version 4.13.0_1522_openshift" caption-side="bottom"}


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


