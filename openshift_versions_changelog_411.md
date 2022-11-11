---

copyright:
  years: 2022, 2022
lastupdated: "2022-11-11"

keywords: openshift, 4.11, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Version 4.11 change log
{: #openshift_changelog_411}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.11. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #openshift_changelog_overview_411}

Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security) for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include a {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_changelog).
{: tip}


## Change logs
{: #411_changelog}

Review the version 4.11 change log.
{: shortdesc}


### Change log for worker node fix pack 4.11.12_1531_openshift, released 11 November 2022
{: #41112_1531_openshift}

The following table shows the changes that are in the worker node fix pack 4.11.12_1531_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8  Packages | 4.18.0-372.32.1.el8_6 | 4.18.0-425.3.1.el8 | Worker node kernel & package updates for [CVE-2021-36221](https://nvd.nist.gov/vuln/detail/CVE-2021-36221){: external}, [CVE-2022-1708](https://nvd.nist.gov/vuln/detail/CVE-2022-1708){: external}, [CVE-2022-27191](https://nvd.nist.gov/vuln/detail/CVE-2022-27191){: external}, [CVE-2021-41190](https://nvd.nist.gov/vuln/detail/CVE-2021-41190){: external}, [CVE-2022-2990](https://nvd.nist.gov/vuln/detail/CVE-2022-2990){: external}, [CVE-2022-29162](https://nvd.nist.gov/vuln/detail/CVE-2022-29162){: external}, [CVE-2022-2989](https://nvd.nist.gov/vuln/detail/CVE-2022-2989){: external}, [CVE-2022-2990](https://nvd.nist.gov/vuln/detail/CVE-2022-2990){: external}, [CVE-2020-36516](https://nvd.nist.gov/vuln/detail/CVE-2020-36516){: external}, [CVE-2020-36558](https://nvd.nist.gov/vuln/detail/CVE-2020-36558){: external}, [CVE-2021-3640](https://nvd.nist.gov/vuln/detail/CVE-2021-3640){: external}, [CVE-2021-30002](https://nvd.nist.gov/vuln/detail/CVE-2021-30002){: external}, [CVE-2022-0168](https://nvd.nist.gov/vuln/detail/CVE-2022-0168){: external}, [CVE-2022-0617](https://nvd.nist.gov/vuln/detail/CVE-2022-0617){: external}, [CVE-2022-0854](https://nvd.nist.gov/vuln/detail/CVE-2022-0854){: external}, [CVE-2022-1016](https://nvd.nist.gov/vuln/detail/CVE-2022-1016){: external}, [CVE-2022-1048](https://nvd.nist.gov/vuln/detail/CVE-2022-1048){: external}, [CVE-2022-1055](https://nvd.nist.gov/vuln/detail/CVE-2022-1055){: external}, [CVE-2022-1184](https://nvd.nist.gov/vuln/detail/CVE-2022-1184){: external}, [CVE-2022-1852](https://nvd.nist.gov/vuln/detail/CVE-2022-1852){: external}, [CVE-2022-2078](https://nvd.nist.gov/vuln/detail/CVE-2022-2078){: external}, [CVE-2022-2586](https://nvd.nist.gov/vuln/detail/CVE-2022-2586){: external}, [CVE-2022-2639](https://nvd.nist.gov/vuln/detail/CVE-2022-2639){: external}, [CVE-2022-2938](https://nvd.nist.gov/vuln/detail/CVE-2022-2938){: external}, [CVE-2022-20368](https://nvd.nist.gov/vuln/detail/CVE-2022-20368){: external}, [CVE-2022-21499](https://nvd.nist.gov/vuln/detail/CVE-2022-21499){: external}, [CVE-2022-23960](https://nvd.nist.gov/vuln/detail/CVE-2022-23960){: external}, [CVE-2022-26373](https://nvd.nist.gov/vuln/detail/CVE-2022-26373){: external}, [CVE-2022-27950](https://nvd.nist.gov/vuln/detail/CVE-2022-27950){: external}, [CVE-2022-28390](https://nvd.nist.gov/vuln/detail/CVE-2022-28390){: external}, [CVE-2022-28893](https://nvd.nist.gov/vuln/detail/CVE-2022-28893){: external}, [CVE-2022-29581](https://nvd.nist.gov/vuln/detail/CVE-2022-29581){: external}, [CVE-2022-36946](https://nvd.nist.gov/vuln/detail/CVE-2022-36946){: external}, [CVE-2022-24448](https://nvd.nist.gov/vuln/detail/CVE-2022-24448){: external}. |
{: caption="Changes since version 4.11.12_1530_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.11.12_1530_openshift, released 07 November 2022
{: #41112_1530_openshift}

The following table shows the changes that are in the worker node fix pack 4.11.12_1530_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages | 4.18.0-372.26.1 | 4.18.0-372.32.1 | Worker node kernel & package updates for [CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external},[CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external},[CVE-2022-0494](https://nvd.nist.gov/vuln/detail/CVE-2022-0494){: external},[CVE-2022-1353](https://nvd.nist.gov/vuln/detail/CVE-2022-1353){: external},[CVE-2022-23816](https://nvd.nist.gov/vuln/detail/CVE-2022-23816){: external},[CVE-2022-23825](https://nvd.nist.gov/vuln/detail/CVE-2022-23825){: external},[CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external},[CVE-2022-2588](https://nvd.nist.gov/vuln/detail/CVE-2022-2588){: external},[CVE-2022-29900](https://nvd.nist.gov/vuln/detail/CVE-2022-29900){: external},[CVE-2022-29901](https://nvd.nist.gov/vuln/detail/CVE-2022-29901){: external},[CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external},[CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external},[CVE-2022-41974](https://nvd.nist.gov/vuln/detail/CVE-2022-41974){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.11.9 | 4.11.12 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.11/release_notes/ocp-4-11-release-notes.html#ocp-4-11-12){: external}. |
| HAPROXY | b034b2 | 3a1392 | [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external},[CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external},[CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external},[CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external},[CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external},[CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external}. |
| CUDA | 3ea43b | 576234 | [CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external},[CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external},[CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external},[CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external},[CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external}. |
{: caption="Changes since version 4.11.9_1526_openshift" caption-side="top"}


### Change log for master fix pack 4.11.8_1528_openshift, released 27 October 2022
{: #4118_1528_openshift}

The following table shows the changes that are in the master fix pack 4.11.8_1528_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.3.11 | v1.3.12 | Updated `Go` dependencies, golangci-lint, and to `Go` version 1.19.2. Updated base image version to 109. Excluded ingress status from cluster status calculation. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.24.5-1 | v1.24.7-1 | Updated to support the `Kubernetes 1.24.7` release. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | dc1725a | 778ef2b | Updated to `Go` version `1.18.6`. |
| Key Management Service provider | v2.5.9 | v2.5.10 | Updated `Go` dependencies and to `Go` version `1.19.2`. |
| OpenVPN Operator image | v1.4.9 | v1.4.10 | Updated ansible operator base image to v1.24.0 to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.11.4 | 4.11.8 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.11/release_notes/ocp-4-11-release-notes.html#ocp-4-11-8){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server and toolkit | v4.11.0-20220920 | v4.11.0-20221004 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.11.0%2B20221004){: external}. |
{: caption="Changes since version 4.11.41523openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.11.9_1529_openshift, released 27 October 2022
{: #4119_1529_openshift}

The following table shows the changes that are in the worker node fix pack 4.11.9_1529_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| VPC Gen 2 RHEL 8 worker image disk size | N/A | N/A | Fixed regression on previous version where root filesystem partition was 25 GB instead of 100GB for VPC Gen 2 |
{: caption="Changes since version 4.11.9_1526_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.11.9_1526_openshift, released 25 October 2022
{: #4119_1526_openshift}

The following table shows the changes that are in the worker node fix pack 4.11.9_1526_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages |N/A|N/A|N/A|
| {{site.data.keyword.openshiftshort}}. | 4.11.7 | 4.11.9 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.11/release_notes/ocp-4-11-release-notes.html#ocp-4-11-9){: external}. |
{: caption="Changes since version 4.11.7_1525_openshift" caption-side="bottom"}


### Change log for master fix pack 4.11.4_1523_openshift, released 26 September 2022
{: #4114_1523_openshift}

The following table shows the changes that are in the master fix pack 4.11.4_1523_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | N/A | N/A | Add pod security labels to the `tigera-operator` and `calico-system` namespaces. |
| Cluster health image | v1.3.10 | v1.3.11 | Updated `Go` dependencies and to `Go` version `1.18.6`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1006 | 1096 | Updated image for [CVE-2022-2526](https://nvd.nist.gov/vuln/detail/CVE-2022-2526){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.9 | v2.3.1 | Updated to `Go` version `1.18.6`. Updated universal base image (UBI) to version `8.6-941` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.24.4-1 | v1.24.5-1 | Updated `Go` dependencies and to use `Go` version `1.18.6`. Updated to support the Kubernetes `1.24.5` release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 414 | 416 | Updated to `Go` version `1.18.6`. Updated universal base image (UBI) to version `8.6-941` to resolve CVEs. |
| Key Management Service Provider | v2.5.8 | v2.5.9 | Updated `Go` dependencies and to `Go` version `1.18.6`. |
| {{site.data.keyword.openshiftshort}} | 4.11.0 | 4.11.4 | See the [{{site.data.keyword.openshiftshort}} Release Notes](https://docs.openshift.com/container-platform/4.11/release_notes/ocp-4-11-release-notes.html#ocp-4-11-4){: external}. |
| OpenVPN Operator image | v1.4.8 | v1.4.9 | Updated ansible operator base image to `v1.23.0` to resolve CVEs. |
| Red Hat {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.11.0-20220829 | v4.11.0-20220920 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.11.0+20220920){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.11.0-20220829 | v4.11.0-20220920 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.11.0+20220920){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.11.0+20220829 | 4.11.0+20220920 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.11.0+20220920){: external}. |
{: caption="Changes since version 4.11.01521openshift" caption-side="bottom"}


### Change log for master fix pack 4.11.0_1521_openshift, released 1 September 2022
{: #4.11.0_1521_openshift}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Red Hat OpenShift Control Plane Operator | v4.11.0-20220824 | v4.11.0-20220829 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.11.0%2B20220829){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.11.0-20220824 | v4.11.0-20220829 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.11.0%2B20220829){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.11.0+20220824 | 4.11.0+20220829 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.11.0+20220829){: external}. |
{: caption="Changes since version 4.11.0_1519_openshift" caption-side="bottom"}


### Change log for master fix pack 4.11.0_1519_openshift and worker node fix pack 4.11.1_1520_openshift, released 31 August 2022
{: #4.11.0_1519_openshift-and-4.11.1_1520_openshift}

The following table shows the changes that are in the master fix pack 4.11.0_1519_openshift and worker node fix pack 4.11.1_1520_openshift. Master patch updates are applied automatically. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.22.2 | v3.23.3 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases){: external}. |
| Calico Operator | v1.25.7 | v1.27.12 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.27.12){: external}. |
| Cluster health image | v1.3.9 | v1.3.10 | Updated `Go` dependencies and to `Go` version `1.18.5`. |
| etcd | v3.4.18 | v3.5.4 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.4){: external}. |
| IBM Calico extension | 997 | 1006 | Updated to `Go` version `1.17.13`. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.8 | v2.2.9 | Updated to `Go` version `1.18.5`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.23.8-7 | v1.24.4-1 | Updated `Go` dependencies and to `Go` version `1.18.5`. Updated to support the Kubernetes `1.24.4` release. [Disabling load balancer NodePort allocation](https://kubernetes.io/docs/concepts/services-networking/service/#load-balancer-nodeport-allocation){: external} is now prevented for VPC load balancers. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 412 | 414 | Updated to `Go` version `1.18.5`. Updated universal base image (UBI) to version `8.6-902` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 0a187a4 | dc1725a | Updated `Go` dependencies and to `Go` version `1.18.3`. |
| Key Management Service provider | v2.5.7 | v2.5.8 | Updated `Go` dependencies. |
| Load balancer and load balancer monitor for IBM Cloud Provider | 2058 | 2110 | Updated `Go` dependencies and to `Go` version `1.17.13`. |
| Red Hat OpenShift (master) | 4.10.22 | 4.11.0 | See the [OpenShift release notes](https://docs.openshift.com/container-platform/4.11/release_notes/ocp-4-11-release-notes.html#ocp-4-11-0-ga){: external}. |
| Red Hat OpenShift (worker) | 4.10.26 | 4.11.1 | See the [OpenShift release notes](https://docs.openshift.com/container-platform/4.11/release_notes/ocp-4-11-release-notes.html){: external}. |
| OpenVPN client | 2.5.6-r1-IKS-629 | 2.5.6-r1-IKS-648 | Update image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097) and [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}. |
| OpenVPN Operator image | v1.4.7 | v1.4.8 | Updated Ansible operator base image to version `v1.22.2` to resolve CVEs. |
| OpenVPN server | 2.5.6-r1-IKS-628 | 2.5.6-r1-IKS-647 | Update image for [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external} and [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}. |
| Pause container image | 3.7 | 3.8 | See the [pause container image release notes](https://github.com/kubernetes/kubernetes/blob/master/build/pause/CHANGELOG.md){: external}. |
| Portieris admission controller | v0.12.5 | v0.12.6 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.12.6){: external} |
| Red Hat OpenShift configuration | N/A | N/A | Updated the [feature gate configuration](/docs/openshift?topic=openshift-service-settings#feature-gates) |
| Red Hat OpenShift Control Plane Operator | v4.10.0-20220712 | v4.11.0-20220824 | See the [{{site.data.keyword.openshiftshort}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.11.0+20220824){: external}. |
| Red Hat OpenShift on IBM Cloud Metrics Server | v4.10.0-20220712 | v4.11.0-20220824 | See the [{{site.data.keyword.openshiftshort}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.11.0+20220824){: external}. |
| Red Hat OpenShift on IBM Cloud toolkit | 4.10.0+20220712 | 4.11.0+20220824 | See the [{{site.data.keyword.openshiftshort}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.11.0+20220824){: external}. |
| RHEL Packages | RHEL 7 | RHEL 8 | Red Hat OpenShift on IBM Cloud version 4.11 supports RHEL 8 worker nodes. |
{: caption="Changes since version 4.10.22_1528_openshift" caption-side="bottom"}

