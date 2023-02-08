---

copyright:
  years: 2022, 2023
lastupdated: "2023-02-08"

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

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security) for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_changelog).
{: tip}


## Change logs
{: #410_changelog}


Review the version 4.10 change log.
{: shortdesc}


### Change log for master fix pack 4.10.47_1553_openshift, released 30 January 2023
{: #41047_1553_openshift}

The following table shows the changes that are in the master fix pack 4.10.47_1553_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico Operator | v1.27.16 | v1.27.17 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.27.17){: external}. |
| Cluster health image | v1.3.14 | v1.3.15 | Updated `Go` dependencies and to `Go` version `1.19.4`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1257 | 1280 | Publish s390x image. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.4 | v2.3.6 | Updated `UBI images` to `8.7-1031` |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.14-2 | v1.23.16-3 | Updated to support the `Kubernetes 1.23.16` release. Updated `Go` dependencies and to `Go` version `1.19.5`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 421 | 425 | Fixes for Fixing [CVE-2022-40303](https://nvd.nist.gov/vuln/detail/CVE-2022-40303){: external} and [CVE-2022-40304](https://nvd.nist.gov/vuln/detail/CVE-2022-40303){: external}. |
| Key Management Service provider | v2.5.12 | v2.5.13 | Updated `Go` dependencies and to `Go` version `1.19.4`. |
| Red Hat {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.10.0-20221205 | v4.10.0-20230123 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20230123){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.10.43 | 4.10.47 | See the [{{site.data.keyword.openshiftlong_notm}} Release Notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-47){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.10.0-20221205 | v4.10.0-20230123 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20230123){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.10.0+20221205 | 4.10.0+20230123 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20230123){: external}. |
{: caption="Changes since version 4.10.43_1548_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.50_1554_openshift, released 30 January 2023
{: #41050_1554_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.50_1554_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.81 | 3.10.0-1160.83 | Worker node kernel & package updates for [CVE-2017-5715](https://nvd.nist.gov/vuln/detail/CVE-2017-5715){: external},[CVE-2021-25220](https://nvd.nist.gov/vuln/detail/CVE-2021-25220){: external},[CVE-2021-26401](https://nvd.nist.gov/vuln/detail/CVE-2021-26401){: external},[CVE-2022-2795](https://nvd.nist.gov/vuln/detail/CVE-2022-2795){: external},[CVE-2022-2964](https://nvd.nist.gov/vuln/detail/CVE-2022-2964){: external},[CVE-2023-22809](https://nvd.nist.gov/vuln/detail/CVE-2023-22809){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node kernel & package updates for [CVE-2022-40303](https://nvd.nist.gov/vuln/detail/CVE-2022-40303){: external},[CVE-2022-40304](https://nvd.nist.gov/vuln/detail/CVE-2022-40304){: external},[CVE-2023-22809](https://nvd.nist.gov/vuln/detail/CVE-2023-22809){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.47 | 4.10.50 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-50){: external}. |
| HAPROXY | 508bf6 | 8d6ea6 | [CVE-2022-42010](https://nvd.nist.gov/vuln/detail/CVE-2022-42010){: external},[CVE-2022-42011](https://nvd.nist.gov/vuln/detail/CVE-2022-42011){: external},[CVE-2022-42012](https://nvd.nist.gov/vuln/detail/CVE-2022-42012){: external},[CVE-2022-40303](https://nvd.nist.gov/vuln/detail/CVE-2022-40303){: external},[CVE-2022-40304](https://nvd.nist.gov/vuln/detail/CVE-2022-40304){: external},[CVE-2022-3821](https://nvd.nist.gov/vuln/detail/CVE-2022-3821){: external},[CVE-2022-35737](https://nvd.nist.gov/vuln/detail/CVE-2022-35737){: external},[CVE-2022-43680](https://nvd.nist.gov/vuln/detail/CVE-2022-43680){: external},[CVE-2021-46848](https://nvd.nist.gov/vuln/detail/CVE-2021-46848){: external}. |
{: caption="Changes since version 4.10.47_1551_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.47_1551_openshift, released 16 January 2023
{: #41047_1551_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.47_1551_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-425.3.1 | 4.18.0-425.10.1 | Worker node kernel & package updates for [CVE-2021-46848](https://nvd.nist.gov/vuln/detail/CVE-2021-46848){: external},[CVE-2022-2601](https://nvd.nist.gov/vuln/detail/CVE-2022-2601){: external},[CVE-2022-2964](https://nvd.nist.gov/vuln/detail/CVE-2022-2964){: external},[CVE-2022-35737](https://nvd.nist.gov/vuln/detail/CVE-2022-35737){: external},[CVE-2022-3775](https://nvd.nist.gov/vuln/detail/CVE-2022-3775){: external},[CVE-2022-3821](https://nvd.nist.gov/vuln/detail/CVE-2022-3821){: external},[CVE-2022-4139](https://nvd.nist.gov/vuln/detail/CVE-2022-4139){: external},[CVE-2022-42010](https://nvd.nist.gov/vuln/detail/CVE-2022-42010){: external},[CVE-2022-42011](https://nvd.nist.gov/vuln/detail/CVE-2022-42011){: external},[CVE-2022-42012](https://nvd.nist.gov/vuln/detail/CVE-2022-42012){: external},[CVE-2022-43680](https://nvd.nist.gov/vuln/detail/CVE-2022-43680){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.45 | 4.10.47 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-47){: external}. |
{: caption="Changes since version 4.10.45_1550_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.45_1550_openshift, released 02 January 2023
{: #41045_1550_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.45_1550_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}} |N/A|N/A|N/A|
{: caption="Changes since version 4.10.45_1549_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.45_1549_openshift, released 19 December 2022
{: #41045_1549_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.45_1549_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.80 | 3.10.0-1160.81 | Worker node kernel & package updates for [CVE-2022-28733](https://nvd.nist.gov/vuln/detail/CVE-2022-28733){: external}. |
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.10.43 | 4.10.45 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-45){: external}. |
{: caption="Changes since version 4.10.43_1547_openshift" caption-side="bottom"}


### Change log for master fix pack 4.10.43_1548_openshift, released 14 December 2022
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
| Red Hat {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.10.0-20221104 | v4.10.0-20221205 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20221205){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.10.39 | 4.10.43 | See the [{{site.data.keyword.openshiftlong_notm}} Release Notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-43){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server and toolkit | v4.10.0-20221104 | v4.10.0-20221205 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20221205){: external}. |
{: caption="Changes since version 4.10.39_1545_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.43_1547_openshift, released 05 December 2022
{: #41043_1547_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.43_1547_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-42898](https://nvd.nist.gov/vuln/detail/CVE-2022-42898){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node package updates for [CVE-2022-42898](https://nvd.nist.gov/vuln/detail/CVE-2022-42898){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.41 | 4.10.43 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-43){: external}. |
| HAPROXY | c619f4 | 508bf6 | [CVE-2016-3709](https://nvd.nist.gov/vuln/detail/CVE-2016-3709){: external}, [CVE-2022-42898](https://nvd.nist.gov/vuln/detail/CVE-2022-42898){: external}, [CVE-2022-1304](https://nvd.nist.gov/vuln/detail/CVE-2022-1304){: external}. |
{: caption="Changes since version 4.10.41_1546_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.41_1546_openshift, released 21 November 2022
{: #41041_1546_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.41_1546_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-21233](https://nvd.nist.gov/vuln/detail/CVE-2022-21233){: external},[CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external},[CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external},[CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external},[CVE-2022-26373](https://nvd.nist.gov/vuln/detail/CVE-2022-26373){: external},[CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external},[CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external},[CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node package updates for [CVE-2015-20107](https://nvd.nist.gov/vuln/detail/CVE-2015-20107){: external},[CVE-2016-3709](https://nvd.nist.gov/vuln/detail/CVE-2016-3709){: external},[CVE-2020-0256](https://nvd.nist.gov/vuln/detail/CVE-2020-0256){: external},[CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external},[CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external},[CVE-2020-36516](https://nvd.nist.gov/vuln/detail/CVE-2020-36516){: external},[CVE-2020-36558](https://nvd.nist.gov/vuln/detail/CVE-2020-36558){: external},[CVE-2021-0308](https://nvd.nist.gov/vuln/detail/CVE-2021-0308){: external},[CVE-2021-25220](https://nvd.nist.gov/vuln/detail/CVE-2021-25220){: external},[CVE-2021-30002](https://nvd.nist.gov/vuln/detail/CVE-2021-30002){: external},[CVE-2021-36221](https://nvd.nist.gov/vuln/detail/CVE-2021-36221){: external},[CVE-2021-3640](https://nvd.nist.gov/vuln/detail/CVE-2021-3640){: external},[CVE-2021-41190](https://nvd.nist.gov/vuln/detail/CVE-2021-41190){: external},[CVE-2022-0168](https://nvd.nist.gov/vuln/detail/CVE-2022-0168){: external},[CVE-2022-0494](https://nvd.nist.gov/vuln/detail/CVE-2022-0494){: external},[CVE-2022-0617](https://nvd.nist.gov/vuln/detail/CVE-2022-0617){: external},[CVE-2022-0854](https://nvd.nist.gov/vuln/detail/CVE-2022-0854){: external},[CVE-2022-1016](https://nvd.nist.gov/vuln/detail/CVE-2022-1016){: external},[CVE-2022-1048](https://nvd.nist.gov/vuln/detail/CVE-2022-1048){: external},[CVE-2022-1055](https://nvd.nist.gov/vuln/detail/CVE-2022-1055){: external},[CVE-2022-1184](https://nvd.nist.gov/vuln/detail/CVE-2022-1184){: external},[CVE-2022-1304](https://nvd.nist.gov/vuln/detail/CVE-2022-1304){: external},[CVE-2022-1353](https://nvd.nist.gov/vuln/detail/CVE-2022-1353){: external},[CVE-2022-1708](https://nvd.nist.gov/vuln/detail/CVE-2022-1708){: external},[CVE-2022-1852](https://nvd.nist.gov/vuln/detail/CVE-2022-1852){: external},[CVE-2022-20368](https://nvd.nist.gov/vuln/detail/CVE-2022-20368){: external},[CVE-2022-2078](https://nvd.nist.gov/vuln/detail/CVE-2022-2078){: external},[CVE-2022-21499](https://nvd.nist.gov/vuln/detail/CVE-2022-21499){: external},[CVE-2022-22624](https://nvd.nist.gov/vuln/detail/CVE-2022-22624){: external},[CVE-2022-22628](https://nvd.nist.gov/vuln/detail/CVE-2022-22628){: external},[CVE-2022-22629](https://nvd.nist.gov/vuln/detail/CVE-2022-22629){: external},[CVE-2022-22662](https://nvd.nist.gov/vuln/detail/CVE-2022-22662){: external},[CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external},[CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external},[CVE-2022-23960](https://nvd.nist.gov/vuln/detail/CVE-2022-23960){: external},[CVE-2022-24448](https://nvd.nist.gov/vuln/detail/CVE-2022-24448){: external},[CVE-2022-24795](https://nvd.nist.gov/vuln/detail/CVE-2022-24795){: external},[CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external},[CVE-2022-2586](https://nvd.nist.gov/vuln/detail/CVE-2022-2586){: external},[CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external},[CVE-2022-26373](https://nvd.nist.gov/vuln/detail/CVE-2022-26373){: external},[CVE-2022-2639](https://nvd.nist.gov/vuln/detail/CVE-2022-2639){: external},[CVE-2022-26700](https://nvd.nist.gov/vuln/detail/CVE-2022-26700){: external},[CVE-2022-26709](https://nvd.nist.gov/vuln/detail/CVE-2022-26709){: external},[CVE-2022-26710](https://nvd.nist.gov/vuln/detail/CVE-2022-26710){: external},[CVE-2022-26716](https://nvd.nist.gov/vuln/detail/CVE-2022-26716){: external},[CVE-2022-26717](https://nvd.nist.gov/vuln/detail/CVE-2022-26717){: external},[CVE-2022-26719](https://nvd.nist.gov/vuln/detail/CVE-2022-26719){: external},[CVE-2022-27191](https://nvd.nist.gov/vuln/detail/CVE-2022-27191){: external},[CVE-2022-27404](https://nvd.nist.gov/vuln/detail/CVE-2022-27404){: external},[CVE-2022-27405](https://nvd.nist.gov/vuln/detail/CVE-2022-27405){: external},[CVE-2022-27406](https://nvd.nist.gov/vuln/detail/CVE-2022-27406){: external},[CVE-2022-27950](https://nvd.nist.gov/vuln/detail/CVE-2022-27950){: external},[CVE-2022-28390](https://nvd.nist.gov/vuln/detail/CVE-2022-28390){: external},[CVE-2022-28893](https://nvd.nist.gov/vuln/detail/CVE-2022-28893){: external},[CVE-2022-29162](https://nvd.nist.gov/vuln/detail/CVE-2022-29162){: external},[CVE-2022-2938](https://nvd.nist.gov/vuln/detail/CVE-2022-2938){: external},[CVE-2022-29581](https://nvd.nist.gov/vuln/detail/CVE-2022-29581){: external},[CVE-2022-2989](https://nvd.nist.gov/vuln/detail/CVE-2022-2989){: external},[CVE-2022-2990](https://nvd.nist.gov/vuln/detail/CVE-2022-2990){: external},[CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external},[CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external},[CVE-2022-30293](https://nvd.nist.gov/vuln/detail/CVE-2022-30293){: external},[CVE-2022-32746](https://nvd.nist.gov/vuln/detail/CVE-2022-32746){: external},[CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external},[CVE-2022-36946](https://nvd.nist.gov/vuln/detail/CVE-2022-36946){: external},[CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external},[CVE-2022-3787](https://nvd.nist.gov/vuln/detail/CVE-2022-3787){: external},[CVE-2022-40674](https://nvd.nist.gov/vuln/detail/CVE-2022-40674){: external},[CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.39 | 4.10.41 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-41){: external}. |
{: caption="Changes since version 4.10.39_1543_openshift" caption-side="bottom"}


### Change log for master fix pack 4.10.39_1545_openshift, released 16 November 2022
{: #41039_1545_openshift}

The following table shows the changes that are in the master fix pack 4.10.39_1545_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.22.4 | v3.23.5 | See the [Calico release notes](https://projectcalico.docs.tigera.io/archive/v3.23/release-notes/#v3235){: external}. |
| Calico Operator | v1.25.11 | v1.27.16 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.27.16){: external}. |
| Cluster health image | v1.3.12 | v1.3.13 | Updated Go dependencies, golangci-lint, gosec, and to `Go` version 1.19.3. Updated base image version to 116. |
| etcd | v3.4.18 | v3.4.21 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.21){: external}. |
| Gateway-enabled cluster controller | 1823 | 1902 | `Go` module updates. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1096 | 1213 | Updated image to fix the following CVEs: [CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external}, [CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external}, [CVE-2022-3515](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-3515){: external}, [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}, [CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external}, [CVE-2022-32149](https://nvd.nist.gov/vuln/detail/CVE-2022-32149){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.3.1 | v2.3.3 | Updated universal base image (UBI) to version `8.7-923` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.13-1 | v1.23.13-5 | Key rotation and updated `Go` dependencies. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 416 | 420 | Updated universal base image (UBI) to version `8.7-923` to resolve CVEs. |
| Key Management Service provider | v2.5.10 | v2.5.11 | Updated `Go` dependencies and to `Go` version `1.19.3`. |
| OpenVPN Operator image | v1.4.10 | v1.4.11 | Updated `ansible operator base image` to `v1.24.0` to resolve CVEs. |
| Red Hat {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.10.0-20220920 | v4.10.0-20221104 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20221104){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.10.36 | 4.10.39 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-39){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server and toolkit | v4.10.0-20220920 | v4.10.0-20221104 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20221104){: external}. |
{: caption="Changes since version 4.10.36_1541_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.39_1544_openshift, released 11 November 2022
{: #41039_1544_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.39_1544_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-372.32.1.el8_6 | 4.18.0-425.3.1.el8 | Worker node kernel & package updates for [CVE-2021-36221](https://nvd.nist.gov/vuln/detail/CVE-2021-36221){: external}, [CVE-2022-1708](https://nvd.nist.gov/vuln/detail/CVE-2022-1708){: external}, [CVE-2022-27191](https://nvd.nist.gov/vuln/detail/CVE-2022-27191){: external}, [CVE-2021-41190](https://nvd.nist.gov/vuln/detail/CVE-2021-41190){: external}, [CVE-2022-2990](https://nvd.nist.gov/vuln/detail/CVE-2022-2990){: external}, [CVE-2022-29162](https://nvd.nist.gov/vuln/detail/CVE-2022-29162){: external}, [CVE-2022-2989](https://nvd.nist.gov/vuln/detail/CVE-2022-2989){: external}, [CVE-2022-2990](https://nvd.nist.gov/vuln/detail/CVE-2022-2990){: external}, [CVE-2020-36516](https://nvd.nist.gov/vuln/detail/CVE-2020-36516){: external}, [CVE-2020-36558](https://nvd.nist.gov/vuln/detail/CVE-2020-36558){: external}, [CVE-2021-3640](https://nvd.nist.gov/vuln/detail/CVE-2021-3640){: external}, [CVE-2021-30002](https://nvd.nist.gov/vuln/detail/CVE-2021-30002){: external}, [CVE-2022-0168](https://nvd.nist.gov/vuln/detail/CVE-2022-0168){: external}, [CVE-2022-0617](https://nvd.nist.gov/vuln/detail/CVE-2022-0617){: external}, [CVE-2022-0854](https://nvd.nist.gov/vuln/detail/CVE-2022-0854){: external}, [CVE-2022-1016](https://nvd.nist.gov/vuln/detail/CVE-2022-1016){: external}, [CVE-2022-1048](https://nvd.nist.gov/vuln/detail/CVE-2022-1048){: external}, [CVE-2022-1055](https://nvd.nist.gov/vuln/detail/CVE-2022-1055){: external}, [CVE-2022-1184](https://nvd.nist.gov/vuln/detail/CVE-2022-1184){: external}, [CVE-2022-1852](https://nvd.nist.gov/vuln/detail/CVE-2022-1852){: external}, [CVE-2022-2078](https://nvd.nist.gov/vuln/detail/CVE-2022-2078){: external}, [CVE-2022-2586](https://nvd.nist.gov/vuln/detail/CVE-2022-2586){: external}, [CVE-2022-2639](https://nvd.nist.gov/vuln/detail/CVE-2022-2639){: external}, [CVE-2022-2938](https://nvd.nist.gov/vuln/detail/CVE-2022-2938){: external}, [CVE-2022-20368](https://nvd.nist.gov/vuln/detail/CVE-2022-20368){: external}, [CVE-2022-21499](https://nvd.nist.gov/vuln/detail/CVE-2022-21499){: external}, [CVE-2022-23960](https://nvd.nist.gov/vuln/detail/CVE-2022-23960){: external}, [CVE-2022-26373](https://nvd.nist.gov/vuln/detail/CVE-2022-26373){: external}, [CVE-2022-27950](https://nvd.nist.gov/vuln/detail/CVE-2022-27950){: external}, [CVE-2022-28390](https://nvd.nist.gov/vuln/detail/CVE-2022-28390){: external}, [CVE-2022-28893](https://nvd.nist.gov/vuln/detail/CVE-2022-28893){: external}, [CVE-2022-29581](https://nvd.nist.gov/vuln/detail/CVE-2022-29581){: external}, [CVE-2022-36946](https://nvd.nist.gov/vuln/detail/CVE-2022-36946){: external}, [CVE-2022-24448](https://nvd.nist.gov/vuln/detail/CVE-2022-24448){: external}. |
{: caption="Changes since version 4.10.39_1543_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.39_1543_openshift, released 07 November 2022
{: #41039_1543_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.39_1543_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.76.1 | 3.10.0-1160.80.1 | Worker node kernel & package updates for [CVE-2022-21233](https://nvd.nist.gov/vuln/detail/CVE-2022-21233){: external},[CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external},[CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external},[CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external},[CVE-2022-26373](https://nvd.nist.gov/vuln/detail/CVE-2022-26373){: external},[CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external},[CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external},[CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| RHEL 8 Packages | 4.18.0-372.26.1 | 4.18.0-372.32.1 | Worker node kernel & package updates for [CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external},[CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external},[CVE-2022-0494](https://nvd.nist.gov/vuln/detail/CVE-2022-0494){: external},[CVE-2022-1353](https://nvd.nist.gov/vuln/detail/CVE-2022-1353){: external},[CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external},[CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external},[CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external},[CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external},[CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external},[CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external},[CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external},[CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external},[CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.37 | 4.10.39 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-39){: external}. |
| HAPROXY | b034b2 | 3a1392 | [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external},[CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external},[CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external},[CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external},[CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external},[CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external}. |
{: caption="Changes since version 4.10.37_1539_openshift" caption-side="bottom"}


### Change log for master fix pack 4.10.36_1541_openshift, released 27 October 2022
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
| {{site.data.keyword.openshiftlong_notm}}. | 4.10.32 | 4.10.36 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-36){: external}. |
{: caption="Changes since version 4.10.321536openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.37_1542_openshift, released 27 October 2022
{: #41037_1542_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.37_1542_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| VPC Gen 2 RHEL 8 worker image disk size | N/A | N/A | Fixed regression on previous version where root filesystem partition was 25 GB instead of 100GB for VPC Gen 2 |
{: caption="Changes since version 4.10.37_1539_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.37_1539_openshift, released 25 October 2022
{: #41037_1539_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.37_1539_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}} | 4.10.35 | 4.10.37 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-37){: external}. |
{: caption="Changes since version 4.10.35_1538_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.35_1538_openshift, released 10 October 2022
{: #41035_1538_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.35_1538_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.10.33 | 4.10.35 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-35){: external}. |
{: caption="Changes since version 4.10.33_1537_openshift" caption-side="bottom"}


### Change log for master fix pack 4.10.32_1536_openshift, released 26 September 2022
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
| {{site.data.keyword.openshiftshort}} | 4.10.26 | 4.10.32 | See the [{{site.data.keyword.openshiftshort}} Release Notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-32){: external}. |
| OpenVPN Operator image | v1.4.8 | v1.4.9 | Updated ansible operator base image to `v1.23.0` to resolve CVEs. |
| Red Hat {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.10.0-20220822 | v4.10.0-20220920 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220920){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.10.0-20220822 | v4.10.0-20220920 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220920){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.10.0+20220822 | 4.10.0+20220920 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220920){: external}. |
{: caption="Changes since version 4.10.261534openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.33_1537_openshift, released 26 September 2022
{: #41033_1537_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.33_1537_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| RHEL 8 Packages | 4.18.0-372.19.1 | 4.18.0-372.26.1 |N/A|
| {{site.data.keyword.openshiftshort}}. | 4.10.31 | 4.10.33 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-33){: external}. |
{: caption="Changes since version 4.10.31_1535_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.31_1535_openshift, released 12 September 2022
{: #41031_1535_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.31_1535_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.10.28 | 4.10.31 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-31){: external}. |
{: caption="Changes since version 4.10.28_1533_openshift" caption-side="bottom"}


### Change log for master fix pack 4.10.26_1534_openshift, released 1 September 2022
{: #41026_1534_openshift}

The following table shows the changes that are in the master fix pack 4.10.26_1534_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.22.2 | v3.22.4 | See the [Calico release notes](https://projectcalico.docs.tigera.io/archive/v3.22/release-notes/#v3224){: external}. Updated the Calico custom resource definitions to include `preserveUnknownFields: false`. |
| Calico Operator | v1.25.7 | v1.25.11 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.25.11){: external}. |
| Cluster health image | v1.3.9 | v1.3.10 | Updated `Go` dependencies and to `Go` version `1.18.5`. |
| Gateway-enabled cluster controller | 1792 | 1823 | Updated to `Go` version `1.17.13`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 997 | 1006 | Updated to `Go` version `1.17.13`. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.8 | v2.2.9 | Updated to `Go` version `1.18.5`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.8-7 | v1.23.9-3 | Updated `vpcctl` binary to version `3367`. Updated to support the Kubernetes `1.23.10` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 412 | 414 | Updated to `Go` version `1.18.5`. Updated universal base image (UBI) to version `8.6-902` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 0a187a4 | dc1725a | Updated `Go` dependencies and to `Go` version `1.18.3`. |
| Key Management Service provider | v2.5.7 | v2.5.8 | Updated `Go` dependencies. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2058 | 2110 | Updated `Go` dependencies and to `Go` version `1.17.13`. |
| {{site.data.keyword.openshiftshort}}. | 4.10.22 | 4.10.26 | See the [{{site.data.keyword.openshiftshort}} Release Notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-26){: external}. |
| OpenVPN client | 2.5.6-r1-IKS-629 | 2.5.6-r1-IKS-648 | Update image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external} and [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}. |
| OpenVPN Operator image | v1.4.7 | v1.4.8 | Updated Ansible operator base image to version `v1.22.2` to resolve CVEs. |
| OpenVPN server | 2.5.6-r1-IKS-628 | 2.5.6-r1-IKS-647 | Update image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external} and [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}. |
| Portieris admission controller | v0.12.5 | v0.12.6 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.12.6){: external}. |
| Red Hat {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.10.0-20220712 | v4.10.0-20220822 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0%2B20220822){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.10.0-20220712 | v4.10.0-20220822 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0%2B20220822){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.10.0+20220712 | 4.10.0+20220822 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220822){: external}. |
{: caption="Changes since version 4.10.22_1528_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.28_1533_openshift, released 29 August 2022
{: #41028_1533_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.28_1533_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-2526](https://nvd.nist.gov/vuln/detail/CVE-2022-2526){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.26 | 4.10.28 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-28){: external}. |
| HAPROXY | 6514a2 | c1634f | [CVE-2022-32206](https://nvd.nist.gov/vuln/detail/CVE-2022-32206){: external},[CVE-2022-32208](https://nvd.nist.gov/vuln/detail/CVE-2022-32208){: external}
{: caption="Changes since version 4.10.26_1530_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.26_1530_openshift, released 16 August 2022
{: #41026_1530_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.26_1530_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.71.1 | 3.10.0-1160.76.1 | Worker node package updates for [CVE-2022-0005](https://nvd.nist.gov/vuln/detail/CVE-2022-0005){: external},[CVE-2022-21123](https://nvd.nist.gov/vuln/detail/CVE-2022-21123){: external},[CVE-2022-21125](https://nvd.nist.gov/vuln/detail/CVE-2022-21125){: external},[CVE-2022-21127](https://nvd.nist.gov/vuln/detail/CVE-2022-21127){: external},[CVE-2022-21131](https://nvd.nist.gov/vuln/detail/CVE-2022-21131){: external},[CVE-2022-21136](https://nvd.nist.gov/vuln/detail/CVE-2022-21136){: external},[CVE-2022-21151](https://nvd.nist.gov/vuln/detail/CVE-2022-21151){: external},[CVE-2022-21166](https://nvd.nist.gov/vuln/detail/CVE-2022-21166){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.24 | 4.10.26 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-26){: external}. |
{: caption="Changes since version 4.10.24_1529_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.24_1529_openshift, released 01 August 2022
{: #41024_1529_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.24_1529_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.10.21 | 4.10.24 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-24){: external}. |
{: caption="Changes since version 4.10.21_1527_openshift" caption-side="bottom"}


### Change log for master fix pack 4.10.22_1528_openshift, released 26 July 2022
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
| {{site.data.keyword.openshiftshort}}. | 4.10.17 | 4.10.22 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-22){: external}. |
| OpenVPN client | 2.5.6-r0-IKS-592 | 2.5.6-r1-IKS-629 | Updated Alpine base image to version `3.16` to resolve CVEs. Updated OpenVPN to version `2.5.6-r1`. |
| OpenVPN Operator image | v1.4.6 | v1.4.7 | Updated Ansible operator base image to version `v1.22.1` to resolve CVEs. |
| OpenVPN server | 2.5.6-r0-IKS-591 | 2.5.6-r1-IKS-628 | Updated Alpine base image to version `3.16` to resolve CVEs. Updated OpenVPN to version `2.5.6-r1`. |
| Portieris admission controller | v0.12.4 | v0.12.5 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.12.5){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.10.0-20220614 | v4.10.0-20220712 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220712){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Metrics Server | v4.10.0-20220614 | v4.10.0-20220712 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220712){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} toolkit | 4.10.0+20220614 | 4.10.0+20220712 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220712){: external}. |
{: caption="Changes since version 4.10.17_1524_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.21_1527_openshift, released 18 July 2022
{: #41021_1527_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.21_1527_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.66.1 | 3.10.0-1160.71.1 | Worker node package updates for [CVE-2020-26116](https://nvd.nist.gov/vuln/detail/CVE-2020-26116){: external},[CVE-2020-26137](https://nvd.nist.gov/vuln/detail/CVE-2020-26137){: external},[CVE-2021-3177](https://nvd.nist.gov/vuln/detail/CVE-2021-3177){: external},[CVE-2022-0391](https://nvd.nist.gov/vuln/detail/CVE-2022-0391){: external},[CVE-2022-1729](https://nvd.nist.gov/vuln/detail/CVE-2022-1729){: external},[CVE-2022-1966](https://nvd.nist.gov/vuln/detail/CVE-2022-1966){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.20 | 4.10.21 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-21){: external}. |
{: caption="Changes since version 4.10.20_1526_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.20_1526_openshift, released 11 July 2022
{: #41020_1526_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.20_1526_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| General |N/A|N/A| Fix to address a bug that occurred if you used the persistent volume claim NFS v3 storage. |
{: caption="Changes since version 4.10.20_1525_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.20_1525_openshift, released 05 July 2022
{: #41020_1525_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.20_1525_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.10.18 | 4.10.20 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-20){: external}. |
{: caption="Changes since version 4.10.18_1523_openshift" caption-side="bottom"}


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
| {{site.data.keyword.openshiftshort}}. | 4.10.15 | 4.10.17 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-17){: external}. |
| {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.10.0-20220509 | v4.10.0-20220614 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0%2B20220614){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Metrics Server and toolkit | v4.10.0-20220509 | v4.10.0-20220614 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0%2B20220614){: external}. |
{: caption="Changes since version 4.10.15_1520_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.18_1523_openshift, released 20 June 2022
{: #41018_1523_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.18_1523_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}. |
| Haproxy | 468c09 | 04f862 | [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.16 | 4.10.18 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-18){: external}. |
{: caption="Changes since version 4.10.16_1521_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.16_1521_openshift, released 7 June 2022
{: #41016_1521_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.16_1521_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A| Worker node package updates for [CVE-2022-24903](https://nvd.nist.gov/vuln/detail/CVE-2022-24903){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.14 | 4.10.16 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-14){: external}. |
{: caption="Changes since version 4.10.14_1519_openshift" caption-side="bottom"}


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
| {{site.data.keyword.openshiftshort}}. | 4.10.12 | 4.10.15 | See the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-15){: external}. |
{: caption="Changes since version 4.10.9_1515_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.14_1519_openshift, released 23 May 2022
{: #41014_1519_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.14_1519_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
|RHEL 7 Packages | 3.10.0-1160.62.1 | 3.10.0-1160.66.1 | Worker node kernel & package updates for [CVE-2018-25032](https://nvd.nist.gov/vuln/detail/CVE-2018-25032){: external}, [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}, [CVE-2022-0492](https://nvd.nist.gov/vuln/detail/CVE-2022-0492){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.10.12 | 4.10.14 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-14){: external}. |
| HA proxy | 36b0307 | 468c09 | [CVE-2021-3634](https://nvd.nist.gov/vuln/detail/CVE-2021-3634){: external}. |
{: caption="Changes since version 4.10.12_1517_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.10.12_1517_openshift, released 09 May 2022
{: #41012_1517_openshift}

The following table shows the changes that are in the worker node fix pack 4.10.12_1517_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | N/A |
| {{site.data.keyword.openshiftshort}}. | 4.10.10 | 4.10.12 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-12){: external}. |
| Haproxy | f53b22 | 36b030 | [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}, [CVE-2022-1154](https://nvd.nist.gov/vuln/detail/CVE-2022-1154){: external}, [CVE-2018-25032](https://nvd.nist.gov/vuln/detail/CVE-2018-25032){: external}. |
{: caption="Changes since version 4.10.10_1516_openshift" caption-side="bottom"}


### Change log for fix pack 4.10.9_1515_openshift (master) and 4.10.10_1516_openshift (worker node), released 27 April 2022
{: #4109_1515_openshift_and_41010_1516_openshift}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.21.5 | v3.22.2 | See the [Calico release notes](https://docs.tigera.io/calico/latest/release-notes/){: external}. |
| Calico Operator | v1.23.7 | v1.25.7 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.25.7){: external}. |
| IBM Cloud Controller Manager | v1.22.8-7 | v1.23.5-9 | Updated to support the Kubernetes `1.23.5` release and to use Go version `1.17.8`. Classic load balancers are updated to improve availability during updates. In addition, creating a mixed protocol load balancer is not supported. |
| OpenShift (master) | 4.9.28 | 4.10.9 | See the [OpenShift release notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-9){: external}. |
| OpenShift (worker) | 4.9.29 | 4.10.10 | See the [OpenShift release notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-10){: external}. Worker nodes are configured to pull images in parallel. |
| Red Hat OpenShift Control Plane Operator | v4.9.0-20220412 | v4.10.0-20220420 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220420){: external}. |
| Red Hat OpenShift configuration | N/A | N/A | Updated the [feature gate configuration](/docs/openshift?topic=openshift-service-settings#feature-gates). |
| {{site.data.keyword.redhat_openshift_notm}} Metrics Server | v4.9.0-20220412 | v4.10.0-20220420 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220420){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} toolkit | 4.9.0+20220412 | 4.10.0+20220420 | See the [{{site.data.keyword.redhat_openshift_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220420){: external}. |
{: caption="Changes since version 4.9.28_1536_openshift master and 4.9.29_1537_openshift worker node" caption-side="bottom"}


