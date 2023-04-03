---

copyright:
  years: 2014, 2023
lastupdated: "2023-04-03"

keywords: openshift, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}





# Version 4.8 change log
{: #openshift_changelog_48}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.8. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #openshift_changelog_overview_48}

Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features, which are subject to change, are disabled.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security) for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't also refer to an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_changelog).
{: tip}

## Change logs
{: #48_changelog}


Review the version 4.8 change log.
{: shortdesc}


### Change log for master fix pack 4.8.57_1596_openshift, released 28 March 2023
{: #4857_1596_openshift}

The following table shows the changes that are in the master fix pack 4.8.57_1596_openshift. Master patch updates are applied automatically. 



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
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.8.0-20230220 | v4.8.0-20230314 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20230314){: external}. |
{: caption="Changes since version 4.8.57_1593_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.57_1597_openshift, released 27 March 2023
{: #4857_1597_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.57_1597_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. |N/A|N/A|N/A|
| Haproxy | af5031 | 8398d1 | [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}. |
{: caption="Changes since version 4.8.57_1594_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.57_1594_openshift, released 13 March 2023
{: #4857_1594_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.57_1594_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.83.1 | 3.10.0-1160.87.1 | Worker node kernel & package updates for [CVE-2018-13405](https://nvd.nist.gov/vuln/detail/CVE-2018-13405){: external}, [CVE-2021-4037](https://nvd.nist.gov/vuln/detail/CVE-2021-4037){: external}, [CVE-2022-2639](https://nvd.nist.gov/vuln/detail/CVE-2022-2639){: external}, [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}, [CVE-2022-42703](https://nvd.nist.gov/vuln/detail/CVE-2022-42703){: external}, [CVE-2022-4378](https://nvd.nist.gov/vuln/detail/CVE-2022-4378){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node package updates for [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}. |
| {{site.data.keyword.openshiftshort}}. |N/A|N/A|N/A|
{: caption="Changes since version 4.8.57_1590_openshift" caption-side="bottom"}


### Change log for master fix pack 4.8.57_1593_openshift, released 2 March 2023
{: #4857_1593_openshift}

The following table shows the changes that are in the master fix pack 4.8.57_1593_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.15 | v1.3.16 | Updated `Go` dependencies and to `Go` version `1.19.6`. Updated universal base image (UBI) to resolve CVEs. |
| etcd | v3.4.22 | v3.4.23 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.23){: external}. |
| Gateway-enabled cluster controller | 1902 | 1987 | Updated `armada-utils` to version `v1.9.35` |
| {{site.data.keyword.IBM_notm}} Calico extension | 1305-amd64 | 1308-amd64 | Updated universal base image (UBI) to resolve [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.6 | v2.3.7 | Updated universal base image (UBI) to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.21.14-10 | v1.21.14-12 | Ignored Nancy dependency check failure. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 425 | 427 | Updated universal base image (UBI) to resolve CVEs. |
| Key Management Service provider | v2.5.13 | v2.6.3 | Updated `Go` dependencies and to `Go` version `1.19.6`. |
| Load balancer and Load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2325 | 2383 | Updated to `armada-utils` version `1.9.35`. |
| OpenVPN client | 2.5.6-r1-IKS-648 | 2.5.8-r0-IKS-674-amd64 | Remediate [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}. |
| OpenVPN server | 2.5.6-r1-IKS-647 | 2.5.8-r0-IKS-673-amd64 | Remediate [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}, [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}. |
| OpenVPN Operator image | v1.4.13 | v1.4.20 | Update `ansible-operator` to `v1.26.1` to fix CVEs. |
| Portieris admission controller | v0.12.6 | v0.13.3 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.3){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.8.55 | 4.8.57 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-57){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.8.0-20230123 | v4.8.0-20230220 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0%2B20230220){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.8.0-20230123 | v4.8.0-20230220 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0%2B20230220){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.8.0+20230123 | 4.8.0+20230220 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20230220){: external}. |
{: caption="Changes since version 4.8.55_1587_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.57_1590_openshift, released 27 February 2023
{: #4857_1590_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.57_1590_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-425.10.1 | 4.18.0-425.13.1 | Worker node & kernel package updates for [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2022-2873](https://nvd.nist.gov/vuln/detail/CVE-2022-2873){: external}, [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/CVE-2022-40897){: external}, [CVE-2022-41222](https://nvd.nist.gov/vuln/detail/CVE-2022-41222){: external}, [CVE-2022-43945](https://nvd.nist.gov/vuln/detail/CVE-2022-43945){: external}, [CVE-2022-4415](https://nvd.nist.gov/vuln/detail/CVE-2022-4415){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}, [CVE-2022-48303](https://nvd.nist.gov/vuln/detail/CVE-2022-48303){: external}. |
| {{site.data.keyword.openshiftshort}}. |N/A|N/A|N/A|
| HAProxy | d38f89 | af5031 | [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/CVE-2022-40897){: external}, [CVE-2022-4415](https://nvd.nist.gov/vuln/detail/CVE-2022-4415){: external}, [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}. |
{: caption="Changes since version 4.8.57_1589_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.57_1589_openshift, released 13 February 2023
{: #4857_1589_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.57_1589_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages |N/A|N/A| Worker node package updates for [CVE-2022-23521](https://nvd.nist.gov/vuln/detail/CVE-2022-23521){: external}, [CVE-2022-41903](https://nvd.nist.gov/vuln/detail/CVE-2022-41903){: external}, [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}. |
| {{site.data.keyword.openshiftshort}}. |N/A|N/A|N/A|
| HAProxy | 8d6ea6 | 08c969 | [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}. |
{: caption="Changes since version 4.8.57_1588_openshift" caption-side="bottom"}


### Change log for master fix pack 4.8.55_1587_openshift, released 30 January 2023
{: #4855_1587_openshift}

The following table shows the changes that are in the master fix pack 4.8.55_1587_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.22.5 | v3.23.5 | See the [Calico release notes](https://docs.tigera.io/archive/v3.23/release-notes/#v3235){: external}. |
| Calico Operator | v1.25.13 | v1.27.17 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.27.17){: external}. |
| Cluster health image | v1.3.14 | v1.3.15 | Updated `Go` dependencies and to `Go` version `1.19.4`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1257 | 1280 | Publish s390x image. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.4 | v2.3.6 | Updated universal base image (UBI) to `8.7-1031` |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 421 | 425 | Fixes for Fixing [CVE-2022-40303](https://nvd.nist.gov/vuln/detail/CVE-2022-40303){: external} and [CVE-2022-40304](https://nvd.nist.gov/vuln/detail/CVE-2022-40303){: external}. |
| Key Management Service provider | v2.5.12 | v2.5.13 | Updated `Go` dependencies and to `Go` version `1.19.4`. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.8.0-20221205 | v4.8.0-20230123 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20230123){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.8.54 | 4.8.55 | See the [{{site.data.keyword.openshiftlong_notm}} Release Notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-55){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.8.0-20221205 | v4.8.0-20230123 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20230123){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.8.0+20221205 | 4.8.0+20230123 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20230123){: external}. |
{: caption="Changes since version 4.8.54_1583_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.57_1588_openshift, released 30 January 2023
{: #4857_1588_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.57_1588_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.81 | 3.10.0-1160.83 | Worker node kernel & package updates for [CVE-2017-5715](https://nvd.nist.gov/vuln/detail/CVE-2017-5715){: external},[CVE-2021-25220](https://nvd.nist.gov/vuln/detail/CVE-2021-25220){: external},[CVE-2021-26401](https://nvd.nist.gov/vuln/detail/CVE-2021-26401){: external},[CVE-2022-2795](https://nvd.nist.gov/vuln/detail/CVE-2022-2795){: external},[CVE-2022-2964](https://nvd.nist.gov/vuln/detail/CVE-2022-2964){: external},[CVE-2023-22809](https://nvd.nist.gov/vuln/detail/CVE-2023-22809){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node kernel & package updates for [CVE-2022-40303](https://nvd.nist.gov/vuln/detail/CVE-2022-40303){: external},[CVE-2022-40304](https://nvd.nist.gov/vuln/detail/CVE-2022-40304){: external},[CVE-2023-22809](https://nvd.nist.gov/vuln/detail/CVE-2023-22809){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.8.55 | 4.8.57 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-57){: external}. |
| HAProxy | 508bf6 | 8d6ea6 | [CVE-2022-42010](https://nvd.nist.gov/vuln/detail/CVE-2022-42010){: external},[CVE-2022-42011](https://nvd.nist.gov/vuln/detail/CVE-2022-42011){: external},[CVE-2022-42012](https://nvd.nist.gov/vuln/detail/CVE-2022-42012){: external},[CVE-2022-40303](https://nvd.nist.gov/vuln/detail/CVE-2022-40303){: external},[CVE-2022-40304](https://nvd.nist.gov/vuln/detail/CVE-2022-40304){: external},[CVE-2022-3821](https://nvd.nist.gov/vuln/detail/CVE-2022-3821){: external},[CVE-2022-35737](https://nvd.nist.gov/vuln/detail/CVE-2022-35737){: external},[CVE-2022-43680](https://nvd.nist.gov/vuln/detail/CVE-2022-43680){: external},[CVE-2021-46848](https://nvd.nist.gov/vuln/detail/CVE-2021-46848){: external}. |
{: caption="Changes since version 4.8.55_1586_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.55_1586_openshift, released 16 January 2023
{: #4855_1586_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.55_1586_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-425.3.1 | 4.18.0-425.10.1 | Worker node kernel & package updates for [CVE-2021-46848](https://nvd.nist.gov/vuln/detail/CVE-2021-46848){: external},[CVE-2022-2601](https://nvd.nist.gov/vuln/detail/CVE-2022-2601){: external},[CVE-2022-2964](https://nvd.nist.gov/vuln/detail/CVE-2022-2964){: external},[CVE-2022-35737](https://nvd.nist.gov/vuln/detail/CVE-2022-35737){: external},[CVE-2022-3775](https://nvd.nist.gov/vuln/detail/CVE-2022-3775){: external},[CVE-2022-3821](https://nvd.nist.gov/vuln/detail/CVE-2022-3821){: external},[CVE-2022-4139](https://nvd.nist.gov/vuln/detail/CVE-2022-4139){: external},[CVE-2022-42010](https://nvd.nist.gov/vuln/detail/CVE-2022-42010){: external},[CVE-2022-42011](https://nvd.nist.gov/vuln/detail/CVE-2022-42011){: external},[CVE-2022-42012](https://nvd.nist.gov/vuln/detail/CVE-2022-42012){: external},[CVE-2022-43680](https://nvd.nist.gov/vuln/detail/CVE-2022-43680){: external}. |
| {{site.data.keyword.openshiftshort}}. |N/A|N/A|N/A|
{: caption="Changes since version 4.8.55_1585_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.55_1585_openshift, released 02 January 2023
{: #4855_1585_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.55_1585_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.8.54 | 4.8.55 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-55){: external}. |
{: caption="Changes since version 4.8.54_1584_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.54_1584_openshift, released 19 December 2022
{: #4854_1584_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.54_1584_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.80 | 3.10.0-1160.81 | Worker node kernel & package updates for [CVE-2022-28733](https://nvd.nist.gov/vuln/detail/CVE-2022-28733){: external}. |
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. |N/A|N/A|N/A|
{: caption="Changes since version 4.8.54_1582_openshift" caption-side="bottom"}


### Change log for master fix pack 4.8.54_1583_openshift, released 14 December 2022
{: #4854_1583_openshift}

The following table shows the changes that are in the master fix pack 4.8.54_1583_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.13 | v1.3.14 | Updated `Go` dependencies. Exclude ingress status from cluster status aggregation. |
| etcd | v3.4.21 | v3.4.22 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.22){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1213 | 1257 | Updated universal base image (UBI) to resolve: [CVE-2022-1304](https://nvd.nist.gov/vuln/detail/cve-2022-1304){: external}, [CVE-2016-3709](https://nvd.nist.gov/vuln/detail/CVE-2016-3709){: external}, [CVE-2022-42898](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-42898){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.3 | v2.3.4 | Update `Go` to version `1.18.8` and updated universal base image (UBI) to resolve CVEs. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 420 | 421 | Updated universal base image (UBI) to resolve [CVE-2022-42898](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-42898){: external}. Updated `Go` to version `1.18.8` |
| Key Management Service provider | v2.5.11 | v2.5.12 | Updated `Go` dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2110 | 2325 | Update `Go` to version `1.19.1` and update dependencies. |
| OpenVPN Operator image | v1.4.11 | v1.4.13 | Updated the `ansible operator base image` to `v1.25.2` to resolve CVEs. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.8.0-20221104 | v4.8.0-20221205 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20221205){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.8.52 | 4.8.54 | See the [{{site.data.keyword.openshiftlong_notm}} Release Notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-54){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server and toolkit | v4.8.0-20221104 | v4.8.0-20221205 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20221205){: external}. |
{: caption="Changes since version 4.8.52_1580_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.54_1582_openshift, released 05 December 2022
{: #4854_1582_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.54_1582_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-42898](https://nvd.nist.gov/vuln/detail/CVE-2022-42898){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node package updates for [CVE-2022-42898](https://nvd.nist.gov/vuln/detail/CVE-2022-42898){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.8.52 | 4.8.54 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-54){: external}. |
| HAProxy | c619f4 | 508bf6 | [CVE-2016-3709](https://nvd.nist.gov/vuln/detail/CVE-2016-3709){: external}, [CVE-2022-42898](https://nvd.nist.gov/vuln/detail/CVE-2022-42898){: external}, [CVE-2022-1304](https://nvd.nist.gov/vuln/detail/CVE-2022-1304){: external}. |
{: caption="Changes since version 4.8.52_1581_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.52_1581_openshift, released 21 November 2022
{: #4852_1581_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.52_1581_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-21233](https://nvd.nist.gov/vuln/detail/CVE-2022-21233){: external},[CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external},[CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external},[CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external},[CVE-2022-26373](https://nvd.nist.gov/vuln/detail/CVE-2022-26373){: external},[CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external},[CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external},[CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node package updates for [CVE-2015-20107](https://nvd.nist.gov/vuln/detail/CVE-2015-20107){: external},[CVE-2016-3709](https://nvd.nist.gov/vuln/detail/CVE-2016-3709){: external},[CVE-2020-0256](https://nvd.nist.gov/vuln/detail/CVE-2020-0256){: external},[CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external},[CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external},[CVE-2020-36516](https://nvd.nist.gov/vuln/detail/CVE-2020-36516){: external},[CVE-2020-36558](https://nvd.nist.gov/vuln/detail/CVE-2020-36558){: external},[CVE-2021-0308](https://nvd.nist.gov/vuln/detail/CVE-2021-0308){: external},[CVE-2021-25220](https://nvd.nist.gov/vuln/detail/CVE-2021-25220){: external},[CVE-2021-30002](https://nvd.nist.gov/vuln/detail/CVE-2021-30002){: external},[CVE-2021-36221](https://nvd.nist.gov/vuln/detail/CVE-2021-36221){: external},[CVE-2021-3640](https://nvd.nist.gov/vuln/detail/CVE-2021-3640){: external},[CVE-2021-41190](https://nvd.nist.gov/vuln/detail/CVE-2021-41190){: external},[CVE-2022-0168](https://nvd.nist.gov/vuln/detail/CVE-2022-0168){: external},[CVE-2022-0494](https://nvd.nist.gov/vuln/detail/CVE-2022-0494){: external},[CVE-2022-0617](https://nvd.nist.gov/vuln/detail/CVE-2022-0617){: external},[CVE-2022-0854](https://nvd.nist.gov/vuln/detail/CVE-2022-0854){: external},[CVE-2022-1016](https://nvd.nist.gov/vuln/detail/CVE-2022-1016){: external},[CVE-2022-1048](https://nvd.nist.gov/vuln/detail/CVE-2022-1048){: external},[CVE-2022-1055](https://nvd.nist.gov/vuln/detail/CVE-2022-1055){: external},[CVE-2022-1184](https://nvd.nist.gov/vuln/detail/CVE-2022-1184){: external},[CVE-2022-1304](https://nvd.nist.gov/vuln/detail/CVE-2022-1304){: external},[CVE-2022-1353](https://nvd.nist.gov/vuln/detail/CVE-2022-1353){: external},[CVE-2022-1708](https://nvd.nist.gov/vuln/detail/CVE-2022-1708){: external},[CVE-2022-1852](https://nvd.nist.gov/vuln/detail/CVE-2022-1852){: external},[CVE-2022-20368](https://nvd.nist.gov/vuln/detail/CVE-2022-20368){: external},[CVE-2022-2078](https://nvd.nist.gov/vuln/detail/CVE-2022-2078){: external},[CVE-2022-21499](https://nvd.nist.gov/vuln/detail/CVE-2022-21499){: external},[CVE-2022-22624](https://nvd.nist.gov/vuln/detail/CVE-2022-22624){: external},[CVE-2022-22628](https://nvd.nist.gov/vuln/detail/CVE-2022-22628){: external},[CVE-2022-22629](https://nvd.nist.gov/vuln/detail/CVE-2022-22629){: external},[CVE-2022-22662](https://nvd.nist.gov/vuln/detail/CVE-2022-22662){: external},[CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external},[CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external},[CVE-2022-23960](https://nvd.nist.gov/vuln/detail/CVE-2022-23960){: external},[CVE-2022-24448](https://nvd.nist.gov/vuln/detail/CVE-2022-24448){: external},[CVE-2022-24795](https://nvd.nist.gov/vuln/detail/CVE-2022-24795){: external},[CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external},[CVE-2022-2586](https://nvd.nist.gov/vuln/detail/CVE-2022-2586){: external},[CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external},[CVE-2022-26373](https://nvd.nist.gov/vuln/detail/CVE-2022-26373){: external},[CVE-2022-2639](https://nvd.nist.gov/vuln/detail/CVE-2022-2639){: external},[CVE-2022-26700](https://nvd.nist.gov/vuln/detail/CVE-2022-26700){: external},[CVE-2022-26709](https://nvd.nist.gov/vuln/detail/CVE-2022-26709){: external},[CVE-2022-26710](https://nvd.nist.gov/vuln/detail/CVE-2022-26710){: external},[CVE-2022-26716](https://nvd.nist.gov/vuln/detail/CVE-2022-26716){: external},[CVE-2022-26717](https://nvd.nist.gov/vuln/detail/CVE-2022-26717){: external},[CVE-2022-26719](https://nvd.nist.gov/vuln/detail/CVE-2022-26719){: external},[CVE-2022-27191](https://nvd.nist.gov/vuln/detail/CVE-2022-27191){: external},[CVE-2022-27404](https://nvd.nist.gov/vuln/detail/CVE-2022-27404){: external},[CVE-2022-27405](https://nvd.nist.gov/vuln/detail/CVE-2022-27405){: external},[CVE-2022-27406](https://nvd.nist.gov/vuln/detail/CVE-2022-27406){: external},[CVE-2022-27950](https://nvd.nist.gov/vuln/detail/CVE-2022-27950){: external},[CVE-2022-28390](https://nvd.nist.gov/vuln/detail/CVE-2022-28390){: external},[CVE-2022-28893](https://nvd.nist.gov/vuln/detail/CVE-2022-28893){: external},[CVE-2022-29162](https://nvd.nist.gov/vuln/detail/CVE-2022-29162){: external},[CVE-2022-2938](https://nvd.nist.gov/vuln/detail/CVE-2022-2938){: external},[CVE-2022-29581](https://nvd.nist.gov/vuln/detail/CVE-2022-29581){: external},[CVE-2022-2989](https://nvd.nist.gov/vuln/detail/CVE-2022-2989){: external},[CVE-2022-2990](https://nvd.nist.gov/vuln/detail/CVE-2022-2990){: external},[CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external},[CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external},[CVE-2022-30293](https://nvd.nist.gov/vuln/detail/CVE-2022-30293){: external},[CVE-2022-32746](https://nvd.nist.gov/vuln/detail/CVE-2022-32746){: external},[CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external},[CVE-2022-36946](https://nvd.nist.gov/vuln/detail/CVE-2022-36946){: external},[CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external},[CVE-2022-3787](https://nvd.nist.gov/vuln/detail/CVE-2022-3787){: external},[CVE-2022-40674](https://nvd.nist.gov/vuln/detail/CVE-2022-40674){: external},[CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| {{site.data.keyword.openshiftshort}}. |N/A|N/A|N/A|
{: caption="Changes since version 4.8.52_1579_openshift" caption-side="bottom"}


### Change log for master fix pack 4.8.52_1580_openshift, released 16 November 2022
{: #4852_1580_openshift}

The following table shows the changes that are in the master fix pack 4.8.52_1580_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.21.6 | v3.22.5 | See the [Calico release notes](https://docs.tigera.io/archive/v3.22/release-notes/#v3225){: external}. |
| Calico Operator | v1.23.8 | v1.25.13 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.25.13){: external}. |
| Cluster health image | v1.3.12 | v1.3.13 | Updated Go dependencies, `golangci-lint`, `gosec`, and to `Go` version 1.19.3. Updated base image version to 116. |
| etcd | v3.4.18 | v3.4.21 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.21){: external}. |
| Gateway-enabled cluster controller | 1823 | 1902 | `Go` module updates. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1096 | 1213 | Updated image to fix the following CVEs: [CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external}, [CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external}, [CVE-2022-3515](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-3515){: external}, [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}, [CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external}, [CVE-2022-32149](https://nvd.nist.gov/vuln/detail/CVE-2022-32149){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.1 | v2.3.3 | Updated universal base image (UBI) to version `8.7-923` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.21.14-6 | v1.21.14-10 | Key rotation and updated `Go` dependencies. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 416 | 420 | Updated universal base image (UBI) to version `8.7-923` to resolve CVEs. |
| Key Management Service provider | v2.5.10 | v2.5.11 | Updated `Go` dependencies and to `Go` version `1.19.3`. |
| OpenVPN Operator image | v1.4.10 | v1.4.11 | Updated `ansible operator base image` to `v1.24.0` to resolve CVEs. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.8.0-20220920 | v4.8.0-20221104 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20221104){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.8.51 | 4.8.52 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-52){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server and toolkit | v4.8.0-20220920 | v4.8.0-20221104 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20221104){: external}. |
{: caption="Changes since version 4.8.51_1578_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.52_1579_openshift, released 07 November 2022
{: #4852_1579_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.52_1579_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.76.1 | 3.10.0-1160.80.1 | Worker node kernel & package updates for [CVE-2022-21233](https://nvd.nist.gov/vuln/detail/CVE-2022-21233){: external},[CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external},[CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external},[CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external},[CVE-2022-26373](https://nvd.nist.gov/vuln/detail/CVE-2022-26373){: external},[CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external},[CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external},[CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| RHEL 8 Packages | 4.18.0-372.26.1 | 4.18.0-372.32.1 | Worker node kernel & package updates for [CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external},[CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external},[CVE-2022-0494](https://nvd.nist.gov/vuln/detail/CVE-2022-0494){: external},[CVE-2022-1353](https://nvd.nist.gov/vuln/detail/CVE-2022-1353){: external},[CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external},[CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external},[CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external},[CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external},[CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external},[CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external},[CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external},[CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external},[CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.8.51 | 4.8.52 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-52){: external}. |
| HAProxy | b034b2 | 3a1392 | [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external},[CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external},[CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external},[CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external},[CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external},[CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external}. |
{: caption="Changes since version 4.8.51_1576_openshift" caption-side="bottom"}


### Change log for master fix pack 4.8.51_1578_openshift, released 27 October 2022
{: #4851_1578_openshift}

The following table shows the changes that are in the master fix pack 4.8.51_1578_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.11 | v1.3.12 | Updated `Go` dependencies, golangci-lint, and to `Go` version 1.19.2. Updated base image version to 109. Excluded ingress status from cluster status calculation. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.21.14-4 | v1.21.14-6 | Updated to support the `Kubernetes 1.21.14` release. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | dc1725a | 778ef2b | Updated to `Go` version `1.18.6`. |
| Key Management Service provider | v2.5.9 | v2.5.10 | Updated `Go` dependencies and to `Go` version `1.19.2`. |
| OpenVPN Operator image | v1.4.9 | v1.4.10 | Updated ansible operator base image to v1.24.0 to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.8.49 | 4.8.51 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-51){: external}. |
{: caption="Changes since version 4.8.491573openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.51_1576_openshift, released 25 October 2022
{: #4851_1576_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.51_1576_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}} | 4.8.50 | 4.8.51 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-51){: external}. |
{: caption="Changes since version 4.8.50_1575_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.50_1575_openshift, released 10 October 2022
{: #4850_1575_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.50_1575_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}} |N/A|N/A|N/A|
{: caption="Changes since version 4.8.50_1574_openshift" caption-side="bottom"}


### Change log for master fix pack 4.8.49_1573_openshift, released 26 September 2022
{: #4849_1573_openshift}

The following table shows the changes that are in the master fix pack 4.8.49_1573_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.10 | v1.3.11 | Updated `Go` dependencies and to `Go` version `1.18.6`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1006 | 1096 | Updated image for [CVE-2022-2526](https://nvd.nist.gov/vuln/detail/CVE-2022-2526){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.9 | v2.3.1 | Updated to `Go` version `1.18.6`. Updated universal base image (UBI) to version `8.6-941` to resolve CVEs. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 414 | 416 | Updated to `Go` version `1.18.6`. Updated universal base image (UBI) to version `8.6-941` to resolve CVEs. |
| {{site.data.keyword.openshiftshort}} | 4.8.47 | 4.8.49 | See the [{{site.data.keyword.openshiftshort}} Release Notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-49){: external}. |
| OpenVPN Operator image | v1.4.8 | v1.4.9 | Updated ansible operator base image to `v1.23.0` to resolve CVEs. |
| Key Management Service Provider | v2.5.8 | v2.5.9 | Updated `Go` dependencies and to `Go` version `1.18.6`. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.8.0-20220816 | v4.8.0-20220920 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220920){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.8.0-20220816 | v4.8.0-20220920 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220920){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.8.0+20220816 | 4.8.0+20220920 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220920){: external}. |
{: caption="Changes since version 4.8.471571openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.50_1574_openshift, released 26 September 2022
{: #4850_1574_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.50_1574_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-372.19.1 | 4.18.0-372.26.1 |N/A|
| {{site.data.keyword.openshiftshort}}. | 4.8.48 | 4.8.50 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-50){: external}. |
{: caption="Changes since version 4.8.48_1572_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.48_1572_openshift, released 12 September 2022
{: #4848_1572_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.48_1572_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.8.47 | 4.8.48 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-48){: external}. |
{: caption="Changes since version 4.8.47_1570_openshift" caption-side="bottom"}


### Change log for master fix pack 4.8.47_1571_openshift, released 1 September 2022
{: #4847_1571_openshift}

The following table shows the changes that are in the master fix pack 4.8.47_1571_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.21.5 | v3.21.6 | See the [Calico release notes](https://docs.tigera.io/archive/v3.21/release-notes/.#v3216){: external}. Updated the Calico custom resource definitions to include `preserveUnknownFields: false`. |
| Calico Operator | v1.23.7 | v1.23.8 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.23.8){: external}. |
| Cluster health image | v1.3.9 | v1.3.10 | Updated `Go` dependencies and to `Go` version `1.18.5`. |
| Gateway-enabled cluster controller | 1792 | 1823 | Updated to `Go` version `1.17.13`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 997 | 1006 | Updated to `Go` version `1.17.13`. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.8 | v2.2.9 | Updated to `Go` version `1.18.5`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.21.14-3 | v1.21.14-4 | Updated `vpcctl` binary to version `3367`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 412 | 414 | Updated to `Go` version `1.18.5`. Updated universal base image (UBI) to version `8.6-902` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 0a187a4 | dc1725a | Updated `Go` dependencies and to `Go` version `1.18.3`. |
| Key Management Service provider | v2.5.7 | v2.5.8 | Updated `Go` dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2058 | 2110 | Updated `Go` dependencies and to `Go` version `1.17.13`. |
| {{site.data.keyword.openshiftshort}}. | 4.8.46 | 4.8.47 | See the [{{site.data.keyword.openshiftshort}} Release Notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-47){: external}. |
| OpenVPN client | 2.5.6-r1-IKS-629 | 2.5.6-r1-IKS-648 | Update image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external} and [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}. |
| OpenVPN Operator image | v1.4.7 | v1.4.8 | Updated Ansible operator base image to version `v1.22.2` to resolve CVEs. |
| OpenVPN server | 2.5.6-r1-IKS-628 | 2.5.6-r1-IKS-647 | Update image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external} and [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}. |
| Portieris admission controller | v0.12.5 | v0.12.6 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.12.6){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.8.0-20220712 | v4.8.0-20220816 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0%2B20220816){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.8.0-20220712 | v4.8.0-20220816 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0%2B20220816){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.8.0+20220712 | 4.8.0+20220816 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220816){: external}. |
{: caption="Changes since version 4.8.46_1566_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.47_1570_openshift, released 29 August 2022
{: #4847_1570_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.47_1570_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-2526](https://nvd.nist.gov/vuln/detail/CVE-2022-2526){: external}. |
| {{site.data.keyword.openshiftshort}}. |N/A|N/A|N/A|
| HAProxy | 6514a2 | c1634f | [CVE-2022-32206](https://nvd.nist.gov/vuln/detail/CVE-2022-32206){: external},[CVE-2022-32208](https://nvd.nist.gov/vuln/detail/CVE-2022-32208){: external}
{: caption="Changes since version 4.8.47_1568_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.47_1568_openshift, released 16 August 2022
{: #4847_1568_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.47_1568_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.71.1 | 3.10.0-1160.76.1 | Worker node package updates for [CVE-2022-0005](https://nvd.nist.gov/vuln/detail/CVE-2022-0005){: external},[CVE-2022-21123](https://nvd.nist.gov/vuln/detail/CVE-2022-21123){: external},[CVE-2022-21125](https://nvd.nist.gov/vuln/detail/CVE-2022-21125){: external},[CVE-2022-21127](https://nvd.nist.gov/vuln/detail/CVE-2022-21127){: external},[CVE-2022-21131](https://nvd.nist.gov/vuln/detail/CVE-2022-21131){: external},[CVE-2022-21136](https://nvd.nist.gov/vuln/detail/CVE-2022-21136){: external},[CVE-2022-21151](https://nvd.nist.gov/vuln/detail/CVE-2022-21151){: external},[CVE-2022-21166](https://nvd.nist.gov/vuln/detail/CVE-2022-21166){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.8.46 | 4.8.47 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-47){: external}. |
{: caption="Changes since version 4.8.46_1567_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.46_1567_openshift, released 01 August 2022
{: #4846_1567_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.46_1567_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}} |N/A|N/A|N/A|
{: caption="Changes since version 4.8.46_1565_openshift" caption-side="bottom"}


### Change log for master fix pack 4.8.46_1566_openshift, released 26 July 2022
{: #4846_1566_openshift}

The following table shows the changes that are in the master fix pack 4.8.46_1566_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.8 | v1.3.9 | Updated `Go` dependencies and to use `Go` version `1.18.4`. Fixed minor typographical error in the add-on `daemonset not available` health status. |
| Gateway-enabled cluster controller | 1680 | 1792 | Updated to use `Go` version `1.17.11`. Updated image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external} and [CVE-2022-29458](https://nvd.nist.gov/vuln/detail/CVE-2022-29458){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 980 | 997 | Updated to use `Go` version `1.17.11`. Updated universal base image (UBI) to version `8.6-854` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.6 | v2.2.8 | Updated to use `Go` version `1.18.3`. Updated universal base image (UBI) to version `8.6-854` to resolve CVEs. Updated to support RHEL 8 worker nodes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.21.13-5 | v1.21.14-3 | Updated `Go` dependencies. Updated to support the Kubernetes `1.21.14` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 410 | 412 | Updated to use `Go` version `1.18.3`. Updated universal base image (UBI) to version `8.6-854` to resolve CVEs. Improved Kubernetes resource watch configuration. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 8c96932 | 0a187a4 | Updated universal base image (UBI) to resolve CVEs. |
| Key Management Service provider | v2.5.6 | v2.5.7 | Updated `Go` dependencies and to use `Go` version `1.18.4`. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1998 | 2058 | Updated image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.8.42 | 4.8.46 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-46){: external}. |
| OpenVPN client | 2.5.6-r0-IKS-592 | 2.5.6-r1-IKS-629 | Updated Alpine base image to version `3.16` to resolve CVEs. Updated OpenVPN to version `2.5.6-r1`. |
| OpenVPN Operator image | v1.4.6 | v1.4.7 | Updated Ansible operator base image to version `v1.22.1` to resolve CVEs. |
| OpenVPN server | 2.5.6-r0-IKS-591 | 2.5.6-r1-IKS-628 | Updated Alpine base image to version `3.16` to resolve CVEs. Updated OpenVPN to version `2.5.6-r1`. |
| Portieris admission controller | v0.12.4 | v0.12.5 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.12.5){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator | v4.8.0-20220614 | v4.8.0-20220712 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220712){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.8.0-20220614 | v4.8.0-20220712 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220712){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.8.0+20220614 | 4.8.0+20220712 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220712){: external}. |
{: caption="Changes since version 4.8.42_1562_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.46_1565_openshift, released 18 July 2022
{: #4846_1565_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.46_1565_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.66.1 | 3.10.0-1160.71.1 | Worker node package updates for [CVE-2020-26116](https://nvd.nist.gov/vuln/detail/CVE-2020-26116){: external},[CVE-2020-26137](https://nvd.nist.gov/vuln/detail/CVE-2020-26137){: external},[CVE-2021-3177](https://nvd.nist.gov/vuln/detail/CVE-2021-3177){: external},[CVE-2022-0391](https://nvd.nist.gov/vuln/detail/CVE-2022-0391){: external},[CVE-2022-1729](https://nvd.nist.gov/vuln/detail/CVE-2022-1729){: external},[CVE-2022-1966](https://nvd.nist.gov/vuln/detail/CVE-2022-1966){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.8.44 | 4.8.46 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-46){: external}. |
{: caption="Changes since version 4.8.44_1564_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.44_1564_openshift, released 11 July 2022
{: #4844_1564_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.44_1564_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| General |N/A|N/A| Fix to address a bug that occurred if you used the persistent volume claim NFS v3 storage. |
{: caption="Changes since version 4.8.44_1563_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.44_1563_openshift, released 05 July 2022
{: #4844_1563_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.44_1563_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.8.42 | 4.8.44 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-44){: external}. |
{: caption="Changes since version 4.8.42_1561_openshift" caption-side="bottom"}


### Change log for master fix pack 4.8.42_1562_openshift, released 22 June 2022
{: #4842_1562_openshift}

The following table shows the changes that are in the master fix pack 4.8.42_1562_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.7 | v1.3.8 | Updated `Go` to version `1.17.11` and also updated the dependencies. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.4 | v2.2.6 | Bug fixes for the driver installation. Block plug-in base images were updated to universal base image (UBI) `8.6-751.1655117800` for CVE-2022-1271 |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.21.13-2 | v1.21.13-5 | Update prometheus/client_golang@v1.7.1 to `v1.11.1`. |
| Key Management Service provider | v2.5.5 | v2.5.6 | Updated `Go` to version `1.17.11` and also updated the dependencies. |
| OpenVPN Operator image | v1.4.5 | v1.4.6 | Update base image to version `v1.22.0` to resolve CVEs. |
| {{site.data.keyword.openshiftshort}}. | 4.8.39 | 4.8.42 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-42){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.8.0-20220509 | v4.8.0-20220614 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0%2B20220614){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server and toolkit | v4.8.0-20220509 | v4.8.0-20220614 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0%2B20220614){: external}. |
{: caption="Changes since version 4.8.39_1558_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.42_1561_openshift, released 20 June 2022
{: #4842_1561_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.42_1561_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}. |
| HAProxy | 468c09 | 04f862 | [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}. |
| {{site.data.keyword.openshiftshort}}. |N/A|N/A|N/A|
{: caption="Changes since version 4.8.42_1559_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.42_1559_openshift, released 7 June 2022
{: #4842_1559_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.42_1559_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-24903](https://nvd.nist.gov/vuln/detail/CVE-2022-24903){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.8.39 | 4.8.42 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-42){: external}. |
{: caption="Changes since version 4.8.39_1557_openshift" caption-side="bottom"}


### Change log for master fix pack 4.8.39_1558_openshift, released 3 June 2022
{: #4839_1558_openshift}

The following table shows the changes that are in the master fix pack 4.8.39_1558_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.6 | v1.3.7 | Updated `Go` to version `1.17.10` and also updated the dependencies. Update registry base image version to `104` |
| {{site.data.keyword.IBM_notm}} Calico extension | 954 | 980 | Updated to use `Go` version `1.17.10`. Updated minimal universal base image (UBI) to version `8.5`. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.2 | v2.2.4 | Updated universal base image (UBI) to version `8.6-751` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.21.11-6 | v1.21.13-2 | Updated to support the Kubernetes `1.21.13` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 408 | 410 | Updated universal base image (UBI) to version `8.6-751` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 8c8c82b | 8c96932 | Updated `Go` to version `1.18.1` |
| Key Management Service provider | v2.5.4 | v2.5.5 | Updated `Go` to version `1.17.10` and updated the golang dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1916 | 1998 | Updated `Go` to version `1.17.10` and updated dependencies. |
| OpenVPN Operator image | v1.4.3 | v1.4.5 | Updated base image to `v1.21.0` for CVE remediation. |
| {{site.data.keyword.openshiftshort}}. | 4.8.36 | 4.8.39 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-39){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.8.0-20220412 | v4.8.0-20220509 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220509){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.8.0-20220412 | v4.8.0-20220509 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220509){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.8.0+20220412 | 4.8.0+20220509 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220509){: external}. |
{: caption="Changes since version 4.8.36_1554_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.39_1557_openshift, released 23 May 2022
{: #4839_1557_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.39_1557_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.62.1 | 3.10.0-1160.66.1 | Worker node kernel & package updates for [CVE-2018-25032](https://nvd.nist.gov/vuln/detail/CVE-2018-25032){: external}, [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}, [CVE-2022-0492](https://nvd.nist.gov/vuln/detail/CVE-2022-0492){: external}. |
| HA proxy | 36b0307 | 468c09 | [CVE-2021-3634](https://nvd.nist.gov/vuln/detail/CVE-2021-3634){: external}. |
{: caption="Changes since version 4.8.39_1556_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.39_1556_openshift, released 09 May 2022
{: #4839_1556_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.39_1556_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | N/A |
| {{site.data.keyword.openshiftshort}}. | 4.8.37 | 4.8.39 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-39){: external}. |
| HAProxy | f53b22 | 36b030 | [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}, [CVE-2022-1154](https://nvd.nist.gov/vuln/detail/CVE-2022-1154){: external}, [CVE-2018-25032](https://nvd.nist.gov/vuln/detail/CVE-2018-25032){: external}. |
{: caption="Changes since version 4.8.37_1555_openshift" caption-side="bottom"}


### Change log for master fix pack 4.8.36_1554_openshift, released 26 April 2022
{: #4836_1554_openshift}

The following table shows the changes that are in the master fix pack 4.8.36_1554_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.20.4 | v3.21.5 | See the [Calico release notes](https://docs.tigera.io/archive/v3.21/release-notes/.#v3215){: external}. |
| Calico Operator | v1.20.6 | v1.23.7 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.23.7){: external}. |
| Cluster health image | v1.3.5 | v1.3.6 | Updated `Go` to version `1.17.9` and also updated the dependencies. Update `registry base image` version to `103`. |
| Gateway-enabled cluster controller | 1669 | 1680 | Updated metadata for a rotated key. |
| {{site.data.keyword.IBM_notm}} Calico extension | 950 | 954 | Updated to latest minimal universal base image (UBI) to resolve [CVE-2021-3999](https://nvd.nist.gov/vuln/detail/CVE-2021-3999){: external}, [CVE-2022-23218](https://nvd.nist.gov/vuln/detail/CVE-2022-23218){: external}, [CVE-2022-23219](https://nvd.nist.gov/vuln/detail/CVE-2022-23219){: external}, [CVE-2022-23308](https://nvd.nist.gov/vuln/detail/CVE-2022-23308){: external}, [CVE-2021-23177](https://nvd.nist.gov/vuln/detail/CVE-2021-23177){: external}, and [CVE-2021-31566](https://nvd.nist.gov/vuln/detail/CVE-2021-31566){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.1 | v2.2.2 | Updated universal base image (UBI) to `8.5-240.1648458092` |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.21.11-3 | v1.21.11-6 | Updated `vpcctl` to the `3003` binary image. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 407 | 408 | Fixed [CVE-2022-0778](https://nvd.nist.gov/vuln/detail/CVE-2022-0778){: external}. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 6c43ef1 | 8c8c82b | Updated `Go` to version `1.17.8` |
| Key Management Service provider | v2.5.3 | v2.5.4 | Moved to a different base image, version `102`, to reduce CVE footprint. Resolved [CVE-2022-0778](https://nvd.nist.gov/vuln/detail/CVE-2022-0778){: external}. |
| Load balancer and Load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1899 | 1916 | Updated the image to resolve CVEs. |
| OpenVPN client | 2.5.4-r0-IKS-579 | 2.5.6-r0-IKS-592 | Upgrade openvpn to version `2.5.6-r0`. |
| OpenVPN server | 2.5.4-r0-IKS-578 | 2.5.6-r0-IKS-591 | Upgrade openvpn to version `2.5.6-r0`. |
| OpenVPN Operator image | v1.4.2 | v1.4.3 | Updated ansible operator base image to version v1.19.0 to resolve CVEs. |
| Portieris admission controller | v0.12.3 | v0.12.4 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.12.4){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.8.35 | 4.8.36 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-36){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.8.0-20220322 | v4.8.0-20220412 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0%2B20220412){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.8.0-20220322 | v4.8.0-20220412 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0%2B20220412){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.8.0+20220322 | 4.8.0+20220412 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0%2B20220412){: external}. |
{: caption="Changes since version 4.8.35_1552_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.37_1555_openshift, released 25 April 2022
{: #4837_1555_openshift}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A  |  N/A | Package updates. |
| {{site.data.keyword.openshiftshort}}. | 4.8.35 | 4.8.37 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-37){: external}. |
{: caption="Changes since version 4.8.35_1553_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.35_1553_openshift, released 11 April 2022
{: #4835_1553_openshift}

The following table shows the changes that are in the worker node fix pack 4.8.35_1553_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL Packages | 3.10.0-1160.59.1 | 3.10.0-1160.62.1 | Kernel and package updates for [CVE-2021-45960](https://nvd.nist.gov/vuln/detail/CVE-2021-45960), [CVE-2021-46143](https://nvd.nist.gov/vuln/detail/CVE-2021-46143), [CVE-2022-22822](https://nvd.nist.gov/vuln/detail/CVE-2022-22822), [CVE-2022-22823](https://nvd.nist.gov/vuln/detail/CVE-2022-22823), [CVE-2022-22824](https://nvd.nist.gov/vuln/detail/CVE-2022-22824), [CVE-2022-22825](https://nvd.nist.gov/vuln/detail/CVE-2022-22825), [CVE-2022-22826](https://nvd.nist.gov/vuln/detail/CVE-2022-22826)   [CVE-2022-22827](https://nvd.nist.gov/vuln/detail/CVE-2022-22827), [CVE-2022-23852](https://nvd.nist.gov/vuln/detail/CVE-2022-23852), [CVE-2022-25235](https://nvd.nist.gov/vuln/detail/CVE-2022-25235), [CVE-2022-25236](https://nvd.nist.gov/vuln/detail/CVE-2022-25236), [CVE-2022-25315](https://nvd.nist.gov/vuln/detail/CVE-2022-25315), [CVE-2021-4028](https://nvd.nist.gov/vuln/detail/CVE-2021-4028), [CVE-2021-4083](https://nvd.nist.gov/vuln/detail/CVE-2021-4083)   [CVE-2022-0778](https://nvd.nist.gov/vuln/detail/CVE-2022-0778). |
{: caption="Changes since version 4.8.35_1550_openshift" caption-side="bottom"}


### Change log for master fix pack 4.8.35_1552_openshift, released 6 April 2022
{: #4835_1552}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.3 | v1.3.5 | Update golang dependencies.  Update image to version 102 to fix CVEs [CVE-2021-3999](https://access.redhat.com/security/cve/cve-2021-3999){: external}, [CVE-2022-23218](https://nvd.nist.gov/vuln/detail/CVE-2022-23218){: external}, [CVE-2022-23219](https://nvd.nist.gov/vuln/detail/CVE-2022-23219){: external} |
| IBM Calico extension | 929 | 950 | Updated to use `Go` version `1.17.8`. Updated universal base image (UBI) to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.1.7 | v2.2.1 | Bug fixes for driver installation issues.  Updated universal base image (UBI) to `8.5-240` and updated `Go` to version to `1.16.15`.  Fixes for CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.21.10-2 | v1.21.11-3 | Updated to support the Kubernetes 1.21.11 release and to use Go version 1.16.15. |
| {{site.data.keyword.cloud_notm}} File Storage plug-in and monitor | 405 | 407 | Updated `Go` to version `1.16.14`.  Updated universal base image (UBI)to version `8.5-240`. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 0fc9949 | 6c43ef1 | Upgraded `Go` packages to resolve vulnerabilities |
| Gateway-enabled cluster controller | 1653 | 1669 | Updated to use `Go` version `1.17.8`. |
| Key Management Service provider | v2.4.3 | v2.5.3 | Updated to use `Go` version `1.17.8`. Updated golang dependencies.  Fixed CVE [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external} |
| Load balancer and Load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1747 | 1899 | Revert setting gratuitous `ARP` on LBv1.  Updated the image to resolve CVEs. Updated to use `Go` version `1.17.8`. |
| OpenVPN client | 2.5.4-r0-IKS-556 | 2.5.4-r0-IKS-579 | Updated `Go` to version `1.16.15`. |
| OpenVPN server | 2.5.4-r0-IKS-562 | 2.5.4-r0-IKS-578 | Updated `Go` to version `1.16.15`. |
| OpenVPN Operator image | v1.4.1 | v1.4.2 | Updated ansible operator base image to version `v1.18.0` to resolve CVEs. |
| Portieris admission controller | v0.12.2 | v0.12.3 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.12.3){: external} |
| Red Hat OpenShift | 4.8.31 | 4.8.35 | See the [Red Hat OpenShift release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-35){: external} |
| Red Hat OpenShift Control Plane Operator | v4.8.0-20220222 | v4.8.0-20220322 | See the [Red Hat OpenShift on {{site.data.keyword.cloud_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220322){: external}. |
| Red Hat OpenShift on {{site.data.keyword.cloud_notm}} Metrics Server | v4.8.0-20220222 | v4.8.0-20220322 | See the [Red Hat OpenShift on {{site.data.keyword.cloud_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220322){: external}. |
| Red Hat OpenShift on {{site.data.keyword.cloud_notm}} toolkit | 4.8.0+20220222 | 4.8.0+20220322 | See the [Red Hat OpenShift on {{site.data.keyword.cloud_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220322){: external}. |
{: caption="Changes since version 4.8.31_1546_openshift" caption-side="bottom"}


### Change log for worker node pack 4.8.35_1550_openshift, released 28 March 2022
{: #4835_1550}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | N/A |
| HA proxy | 15198f | b40c07 | [CVE-2021-45960](https://nvd.nist.gov/vuln/detail/CVE-2021-45960){: external}, [CVE-2021-46143](https://nvd.nist.gov/vuln/detail/CVE-2021-46143){: external}, [CVE-2022-22822](https://nvd.nist.gov/vuln/detail/CVE-2022-22822){: external}, [CVE-2022-22823](https://nvd.nist.gov/vuln/detail/CVE-2022-22823){: external}, [CVE-2022-22824](https://nvd.nist.gov/vuln/detail/CVE-2022-22824){: external}, [CVE-2022-22825](https://nvd.nist.gov/vuln/detail/CVE-2022-22825){: external}, [CVE-2022-22826](https://nvd.nist.gov/vuln/detail/CVE-2022-22826){: external}, [CVE-2022-22827](https://nvd.nist.gov/vuln/detail/CVE-2022-22827){: external}, [CVE-2022-23852](https://nvd.nist.gov/vuln/detail/CVE-2022-23852){: external}, [CVE-2022-25235](https://nvd.nist.gov/vuln/detail/CVE-2022-25235){: external}, [CVE-2022-25236](https://nvd.nist.gov/vuln/detail/CVE-2022-25236){: external}, [CVE-2022-25315](https://nvd.nist.gov/vuln/detail/CVE-2022-25315){: external}, [CVE-2021-3999](https://nvd.nist.gov/vuln/detail/CVE-2021-3999){: external}, [CVE-2022-23218](https://nvd.nist.gov/vuln/detail/CVE-2022-23218){: external}, [CVE-2022-23219](https://nvd.nist.gov/vuln/detail/CVE-2022-23219){: external}, [CVE-2022-23308](https://nvd.nist.gov/vuln/detail/CVE-2022-23308){: external}, [CVE-2021-23177](https://nvd.nist.gov/vuln/detail/CVE-2021-23177){: external}, [CVE-2021-31566](https://nvd.nist.gov/vuln/detail/CVE-2021-31566){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.32 | 4.8.35 | See [change logs](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-35){: external}. |
{: caption="Changes since version 4.8.32_1548_openshift" caption-side="bottom"}


### Change log for worker node pack 4.8.32_1548_openshift, released 14 March 2022
{: #4832_1548}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | N/A |
{: caption="Changes since version 4.8.32_1547_openshift" caption-side="bottom"}


### Change log for master fix pack 4.8.31_1546_openshift, released 3 March 2022
{: #4831_1546}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.20.3 | v3.20.4 | See the [Calico release notes](https://docs.tigera.io/archive/v3.20/release-notes/.#v3204){: external}. |
| Calico Operator | v1.20.5 | v1.20.6 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.20.6){: external}. |
| Cluster health image | v1.2.21 | v1.3.3 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds fix for [CVE-2021-43565](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-43565){: external}. Adds Golang dependency updates. |
| Gateway-enabled cluster controller | 1586 | 1653 | Updated to use `Go` version `1.17.7` and updated `Go` modules to fix CVEs. |
| IBM Calico extension | 923 | 929 | Updated universal base image (UBI) to the `8.5-230` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.1.6 | v2.1.7 | Fix for [CVE-2021-3538](https://nvd.nist.gov/vuln/detail/CVE-2021-3538){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.21.9-1 | v1.21.10-2 | Updated to support the Kubernetes `1.21.10` release and to use `Go` version `1.16.14`. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.filestorage_short}} plug-in and monitor | 404 | 405 | Adds fix for [CVE-2021-3538](https://nvd.nist.gov/vuln/detail/CVE-2021-3538){: external} and adds dependency updates. |
| Key Management Service provider | v2.4.0 | v2.4.3 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds [CVE-2021-43565](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-43565){: external}. Adds Golang dependency updates. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.26 | 4.8.31 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-31){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.8.0-20220107 | v4.8.0-20220222 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220222){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.8.0-20220107 | v4.8.0-20220222 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220222){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.8.0+20220107 | 4.8.0+20220222 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220222){: external}. |
| OpenVPN server | 2.5.4-r0-IKS-555 | 2.5.4-r0-IKS-562 | Turns off CRL verification in the openvpn image. |
| OpenVPN Operator image | v1.4.0 | v1.4.1 | Turns off CRL verification in the opevpn-operator image. |
{: caption="Changes since version 4.8.26_1542_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.32_1547_openshift, released 28 February 2022
{: #4832_1547}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages |  3.10.0-1160.53.1.el7 | 3.10.0-1160.59.1.el7 | Kernel and package updates for [CVE-2020-25709](https://nvd.nist.gov/vuln/detail/CVE-2020-25709){: external}, [CVE-2020-25710](https://nvd.nist.gov/vuln/detail/CVE-2020-25710){: external}, [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}, [CVE-2020-0465](https://nvd.nist.gov/vuln/detail/CVE-2020-0465){: external}, [CVE-2020-0466](https://nvd.nist.gov/vuln/detail/CVE-2020-0466){: external}, [CVE-2021-0920](https://nvd.nist.gov/vuln/detail/CVE-2021-0920){: external}, [CVE-2021-3564](https://nvd.nist.gov/vuln/detail/CVE-2021-3564){: external}, [CVE-2021-3573](https://nvd.nist.gov/vuln/detail/CVE-2021-3573){: external}, [CVE-2021-3752](https://nvd.nist.gov/vuln/detail/CVE-2021-3752){: external}, [CVE-2021-4155](https://nvd.nist.gov/vuln/detail/CVE-2021-4155){: external}, [CVE-2022-0330](https://nvd.nist.gov/vuln/detail/CVE-2022-0330){: external}, [CVE-2022-22942](https://nvd.nist.gov/vuln/detail/CVE-2022-22942){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.29 | 4.8.32 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-32){: external} | 
| HA proxy | f6a2b3 | 15198fb | Contains fixes for [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}. |
{: caption="Changes since version 4.8.32_1547_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.29_1544_openshift, released 14 February 2022
{: #4829_1544}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | N/A |
|  {{site.data.keyword.redhat_openshift_notm}}  | 4.8.28 | 4.8.29 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-29){: external}. |
| HA proxy | d38fa1 | f6a2b3 | [CVE-2021-3521](https://nvd.nist.gov/vuln/detail/CVE-2021-3521){: external}   [CVE-2021-4122](https://nvd.nist.gov/vuln/detail/CVE-2021-4122){: external}. |
{: caption="Changes since version 4.8.28_1543_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.28_1543_openshift, released 31 January 2022
{: #4828_1543}

The following table shows the changes that are in the worker node fix pack `4.8.28_1543_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | Updated worker node images with package updates for [CVE-2021-4034](https://nvd.nist.gov/vuln/detail/CVE-2021-4034){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.26 | 4.8.28 | See the {{site.data.keyword.redhat_openshift_notm}} [change logs](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-28){: external}. |
{: caption="Changes since version 4.8.26_1541_openshift" caption-side="bottom"}


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
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.8.0-20211201 | v4.8.0-20220107 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220107){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.8.0-20211201 | v4.8.0-20220107 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220107){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.21 | 4.8.26 | Changed the duration of worker node certificates from 3 years to 2 years. See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-26){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.8.0+20211201 | 4.8.0+20220107 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20220107){: external}. |
| OpenVPN client | 2.4.6-r3-IKS-463 | 2.5.4-r0-IKS-556 | Update base image to alpine `3.15` to address CVEs, no longer set the `--compress config` option, updated scripts. |
| OpenVPN server | 2.4.6-r3-IKS-462 | 2.5.4-r0-IKS-555 | Update base image to alpine `3.15` to address CVEs, no longer set the `--compress config` option, updated scripts. |
| OpenVPN Operator image | v1.3.9 | v1.4.0 | Updated `OpenVPN` to version `2.5.4-r0`.  Remove deprecated compression config option from VPN server. Set cipher explicitly to default value to avoid warning message in logs. |
| Portieris admission controller | v0.12.1 | v0.12.2 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.12.2){: external} |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 3430e03 | 0fc9949 | Updated universal base image (UBI) to the `8.5-218` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 402 | 404 | Updated universal base image (UBI) to the `8.5-218` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
{: caption="Changes since version 4.8.21_1541_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.26_1541_openshift, released 18 January 2022
{: #4826_1541}

The following table shows the changes that are in the worker node fix pack `4.8.26_1541_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.49.1.el7 | 3.10.0-1160.53.1.el7 | Kernel and package updates for [CVE-2020-25704](https://nvd.nist.gov/vuln/detail/CVE-2020-25704){: external}, [CVE-2020-36322](https://nvd.nist.gov/vuln/detail/CVE-2020-36322){: external}, [CVE-2021-42739](https://nvd.nist.gov/vuln/detail/CVE-2021-42739){: external}, and [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.24 | 4.8.26 | See  the [change logs](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-26){: external}. |
{: caption="Changes since version 4.8.24_1540_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.24_1540_openshift, released 4 January 2022
{: #4824_1540}

The following table shows the changes that are in the worker node fix pack patch update `4.8.24_1540_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 3b8663 | d38fa1 | Contains fixes for [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}. |
{: caption="Changes since version 4.8.24_1539_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.24_1539_openshift, released 20 December 2021
{: #4824_1539_openshift}

The following table shows the changes that are in the worker node fix pack patch update `4.8.24_1539_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} node | 4.8.20 | 4.8.22 | See [change logs](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-22){: external} |
{: caption="Changes since version 4.8.22_1538_openshift" caption-side="bottom"}


### Change log for master fix pack 4.8.21_1537_openshift, released 7 December 2021
{: #4821_1537}

The following table shows the changes that are in the master fix pack patch update `4.8.21_1537_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.20.2 | v3.20.3 | See the [Calico release notes](https://docs.tigera.io/archive){: external}. |
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
|  {{site.data.keyword.redhat_openshift_notm}} | 4.8.18 | 4.8.21 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-21){: external}. |
|  {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.8.0-20211109 | v4.8.0-20211201 | See the [{{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211201){: external}. |
| OpenVPN Operator image | v1.3.8 | v1.3.9 | Updated ansible operator base image to version `v1.14.0` to resolve CVEs. |
| Portieris admission controller | v0.12.0 | v0.12.1 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.12.1){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud Metrics Server | v4.8.0-20211109 | v4.8.0-20211201 | See the [{{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211201){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud toolkit | 4.8.0+20211109 | 4.8.0+20211201 | See the [{{site.data.keyword.redhat_openshift_notm}} on {{site.data.keyword.IBM_notm}} Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211201){: external}. |
{: caption="Changes since version 4.8.18_1535_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.22_1538_openshift, released 6 December 2021
{: #4822_1538}

The following table shows the changes that are in the worker node fix pack patch update `4.8.22_1538_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.45 | 3.10.0-1160.49 | Updated worker node images and kernel with package updates. [CVE-2020-36385](https://nvd.nist.gov/vuln/detail/CVE-2020-36385){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-41617](https://nvd.nist.gov/vuln/detail/CVE-2021-41617){: external}, [CVE-2021-20271](https://nvd.nist.gov/vuln/detail/CVE-2021-20271){: external} |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.20 | 4.8.22 | See the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-22){: external} |
{: caption="Changes since version 4.8.20_1536_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.20_1536_openshift, released 22 November 2021
{: #4820_1536}

The following table shows the changes that are in the worker node fix pack patch update `4.8.20_1536_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.18 | 4.8.20 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-20){: external}. | 
| HA proxy | 07f1e9e | 3b8663 | Contains fixes for [CVE-2021-20231](https://nvd.nist.gov/vuln/detail/CVE-2021-20231){: external}, [CVE-2021-20232](https://nvd.nist.gov/vuln/detail/CVE-2021-20232){: external}, [CVE-2021-3580](https://nvd.nist.gov/vuln/detail/CVE-2021-3580){: external}, [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946){: external}, [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947){: external}, [CVE-2021-22876](https://nvd.nist.gov/vuln/detail/CVE-2021-22876){: external}, [CVE-2021-22898](https://nvd.nist.gov/vuln/detail/CVE-2021-22898){: external}, [CVE-2021-22925](https://nvd.nist.gov/vuln/detail/CVE-2021-22925){: external}, [CVE-2019-20838](https://nvd.nist.gov/vuln/detail/CVE-2019-20838){: external}, [CVE-2020-14155](https://nvd.nist.gov/vuln/detail/CVE-2020-14155){: external}, [CVE-2018-20673](https://nvd.nist.gov/vuln/detail/CVE-2018-20673){: external}, [CVE-2021-42574](https://nvd.nist.gov/vuln/detail/CVE-2021-42574){: external}, [CVE-2019-17594](https://nvd.nist.gov/vuln/detail/CVE-2019-17594){: external}, [CVE-2019-17595](https://nvd.nist.gov/vuln/detail/CVE-2019-17595){: external}, [CVE-2020-12762](https://nvd.nist.gov/vuln/detail/CVE-2020-12762){: external}, [CVE-2020-16135](https://nvd.nist.gov/vuln/detail/CVE-2020-16135){: external}, [CVE-2021-3445](https://nvd.nist.gov/vuln/detail/CVE-2021-3445){: external}, [CVE-2021-36084](https://nvd.nist.gov/vuln/detail/CVE-2021-36084){: external}, [CVE-2021-36085](https://nvd.nist.gov/vuln/detail/CVE-2021-36085){: external}, [CVE-2021-36086](https://nvd.nist.gov/vuln/detail/CVE-2021-36086){: external}, [CVE-2021-36087](https://nvd.nist.gov/vuln/detail/CVE-2021-36087){: external}, [CVE-2021-20266](https://nvd.nist.gov/vuln/detail/CVE-2021-20266){: external}, [CVE-2019-18218](https://nvd.nist.gov/vuln/detail/CVE-2019-18218){: external}, [CVE-2021-23840](https://nvd.nist.gov/vuln/detail/CVE-2021-23840){: external}, [CVE-2021-23841](https://nvd.nist.gov/vuln/detail/CVE-2021-23841){: external}, [CVE-2021-27645](https://nvd.nist.gov/vuln/detail/CVE-2021-27645){: external}, [CVE-2021-33574](https://nvd.nist.gov/vuln/detail/CVE-2021-33574){: external}, [CVE-2021-35942](https://nvd.nist.gov/vuln/detail/CVE-2021-35942){: external}, [CVE-2021-33560](https://nvd.nist.gov/vuln/detail/CVE-2021-33560){: external}, [CVE-2019-13750](https://nvd.nist.gov/vuln/detail/CVE-2019-13750){: external}, [CVE-2019-13751](https://nvd.nist.gov/vuln/detail/CVE-2019-13751){: external}, [CVE-2019-19603](https://nvd.nist.gov/vuln/detail/CVE-2019-19603){: external}, [CVE-2019-5827](https://nvd.nist.gov/vuln/detail/CVE-2019-5827){: external}, [CVE-2020-13435](https://nvd.nist.gov/vuln/detail/CVE-2020-13435){: external}, [CVE-2020-24370](https://nvd.nist.gov/vuln/detail/CVE-2020-24370){: external}, [CVE-2021-28153](https://nvd.nist.gov/vuln/detail/CVE-2021-28153){: external}, [CVE-2021-3800](https://nvd.nist.gov/vuln/detail/CVE-2021-3800){: external}, [CVE-2021-33928](https://nvd.nist.gov/vuln/detail/CVE-2021-33928){: external}, [CVE-2021-33929](https://nvd.nist.gov/vuln/detail/CVE-2021-33929){: external}, [CVE-2021-33930](https://nvd.nist.gov/vuln/detail/CVE-2021-33930){: external}, [CVE-2021-33938](https://nvd.nist.gov/vuln/detail/CVE-2021-33938){: external}, and [CVE-2021-3200](https://nvd.nist.gov/vuln/detail/CVE-2021-3200){: external} |
{: caption="Changes since version 4.8.18_1533_openshift" caption-side="bottom"}


### Change log for master fix pack 4.8.18_1535_openshift, released 17 November 2021
{: #4818_1535}

The following table shows the changes that are in the master fix pack patch update `4.8.18_1535_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.20.0 | v3.20.2 | See the [Calico release notes](https://docs.tigera.io/archive){: external}. |
| Calico Operator | v1.20.1 | v1.20.4 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.20.4){: external}. |
| Cluster health image | v1.2.16 | v1.2.18 | Updated `Go` module dependencies and to use `Go` version `1.16.9`.  Updated image for [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946){: external}, [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947){: external}, [CVE-2021-33928](https://nvd.nist.gov/vuln/detail/CVE-2021-33928){: external}, [CVE-2021-33929](https://nvd.nist.gov/vuln/detail/CVE-2021-33929){: external} and [CVE-2021-33930](https://nvd.nist.gov/vuln/detail/CVE-2021-33930){: external}.  |
| etcd | v3.4.17 | v3.4.18 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.18){: external}. |
| Gateway-enabled cluster controller | 1510 | 1567 | Updated to use `Go` version `1.16.9`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.21.5-2 | v1.21.6-2 | Updated to support the Kubernetes `1.21.6` release and to use `Go` version `1.16.9`. Updated image for [DLA-2797-1](https://www.debian.org/lts/security/2021/dla-2797){: external}. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | e3cb629 | 4ca5637 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. |
| Key Management Service provider | v2.3.8 | v2.3.10 | Updated `Go` module dependencies and to use `Go` version `1.16.9`.  Updated image for [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.IBM_notm}} Cloud Provider | 1547 | 1590 | Updated to use `Go` version `1.16.9`. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.14 | 4.8.18 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-18){: external}. Changed the duration of the Kubernetes API server certificate from 825 days to 365 days. Changed the duration of the cluster CA certificate from 30 to 10 years. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.8.0-20211004 | v4.8.0-20211109 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211109){: external}. |
| OpenVPN client | 2.4.6-r3-IKS-386 | 2.4.6-r3-IKS-463 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN server | 2.4.6-r3-IKS-385 | 2.4.6-r3-IKS-462 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN Operator image | v1.3.7 | v1.3.8 | Updated ansible operator base image to version `v1.13.1` to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.8.0-20211004 | v4.8.0-20211109 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211109){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.8.0+20211004 | 4.8.0+20211109 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211109){: external}. |
{: caption="Changes since version 4.8.14_1531_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.18_1533_openshift, released 10 November 2021
{: #4818_1533}

The following table shows the changes that are in the worker node fix pack patch update `4.8.18_1533_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages| N/A | N/A | Updated worker node image packages for [CVE-2021-42574](https://nvd.nist.gov/vuln/detail/CVE-2021-42574){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.15 | 4.8.18 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-8-18){: external}. |
{: caption="Changes since version 4.8.15_1532_openshift" caption-side="bottom"}


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
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.filestorage_short}} plug-in and monitor | 400 | 401 | Updated universal base image (UBI) to the latest `8.4-210` version to resolve CVEs. |
| Key Management Service provider | v2.3.7 | v2.3.8 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs:  [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}, [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}, and [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.11 | 4.8.14| See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-14){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.8.0-20210917 | v4.8.0-20211004 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211004){: external}. |
| OpenVPN Operator image | v1.3.6 | v1.3.7 | Updated ansible operator base image to version `v1.12.0` to resolve CVEs. |
| Portieris admission controller | v0.11.0 | v0.12.0 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.12.0){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.8.0-20210917 | v4.8.0-20211004 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211004){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.8.0+20210917 | 4.8.0+20211004 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.8.0+20211004){: external}. |
{: caption="Changes since version 4.8.11_1526_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.15_1532_openshift, released 25 October 2021
{: #4815_1532}

The following table shows the changes that are in the worker node fix pack patch update `4.8.15_1532_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.13 | 4.8.15 | See [the {{site.data.keyword.redhat_openshift_notm}} change logs](http://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html){: external}. |
| RHEL 7 Packages | 3.10.0-1160.42.2.el7 | 3.10.0-1160.45.1.el7 | Updated worker node images and kernel with package updates for [CVE-2021-3778](https://nvd.nist.gov/vuln/detail/CVE-2021-3778){: external} and [CVE-2021-3796](https://nvd.nist.gov/vuln/detail/CVE-2021-3796){: external}. |
| Worker-pool taint automation | N/A | N/A | Fixes known issue related to worker-pool taint automation that prevents workers from getting providerID. |
{: caption="Changes since version 4.8.13_1528_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.8.13_1528_openshift, released 11 October 2021
{: #48131528_openshift}

The following table shows the changes that are in the worker node fix pack patch update `4.8.13_1528_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.8.12 | 4.8.13 | See the [change logs](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-13){: external}. The update resolves CVE-2021-25741 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6515606){: external}).|
{: caption="Changes since version 4.8.12_1527_openshift" caption-side="bottom"}


