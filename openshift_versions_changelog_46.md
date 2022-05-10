---

copyright:
  years: 2014, 2022
lastupdated: "2022-05-10"

keywords: openshift, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.redhat_openshift_notm}} version 4.6 changelog
{: #openshift_changelog_46}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.6. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #openshift_changelog_overview_46}

Unless otherwise noted in the changelogs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features, which are subject to change, are disabled.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security) for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Changelog entries that address other security vulnerabilities but don't also refer to an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_changelog).
{: tip}

## Change logs
{: #47_changelog}

Review the version 4.6 change log.
{: shortdesc}






### Change log for worker node fix pack 4.6.57_1582_openshift, released 09 May 2022
{: #4657_1582_openshift}

The following table shows the changes that are in the worker node fix pack 4.6.57_1582_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | N/A |
| {{site.data.keyword.openshiftshort}}. | 4.6.56 | 4.6.57 | For more information, see the [change log](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-57){: external}. |
| Haproxy | f53b22 | 36b030 | [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}, [CVE-2022-1154](https://nvd.nist.gov/vuln/detail/CVE-2022-1154){: external}, [CVE-2018-25032](https://nvd.nist.gov/vuln/detail/CVE-2018-25032){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.56_1581_openshift" caption-side="top"}

### Change log for master fix pack 4.6.56_1580_openshift, released 26 April 2022
{: #4656_1580_openshift}

The following table shows the changes that are in the master fix pack 4.6.56_1580_openshift. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.19.4 | v3.20.5 | See the [Calico release notes](https://projectcalico.docs.tigera.io/archive/v3.20/release-notes/#v3205){: external}. |
| Calico Operator | v1.17.9 | v1.20.8 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.20.8){: external}. |
| Cluster health image | v1.3.5 | v1.3.6 | Updated `Go` to version `1.17.9` and also updated the dependencies. Update `registry base image` version to `103`. |
| Gateway-enabled cluster controller | 1669 | 1680 | Updated metadata for a rotated key. |
| {{site.data.keyword.IBM_notm}} Calico extension | 950 | 954 | Updated to latest UBI-minimal image to resolve [CVE-2021-3999](https://nvd.nist.gov/vuln/detail/CVE-2021-3999){: external}, [CVE-2022-23218](https://nvd.nist.gov/vuln/detail/CVE-2022-23218){: external}, [CVE-2022-23219](https://nvd.nist.gov/vuln/detail/CVE-2022-23219){: external}, [CVE-2022-23308](https://nvd.nist.gov/vuln/detail/CVE-2022-23308){: external}, [CVE-2021-23177](https://nvd.nist.gov/vuln/detail/CVE-2021-23177){: external}, and [CVE-2021-31566](https://nvd.nist.gov/vuln/detail/CVE-2021-31566){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.2.1 | v2.2.2 | Updated `ubi images` to `8.5-240.1648458092` |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.16-10 | v1.19.16-11 | Updated `vpcctl` to the `3003` binary image. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 407 | 408 | Fixed [CVE-2022-0778](https://nvd.nist.gov/vuln/detail/CVE-2022-0778){: external}. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 6c43ef1 | 8c8c82b | Updated `Go` to version `1.17.8` |
| Key Management Service provider | v2.5.3 | v2.5.4 | Moved to a different base image, version `102`, to reduce CVE footprint. Resolved [CVE-2022-0778](https://nvd.nist.gov/vuln/detail/CVE-2022-0778){: external}. |
| Load balancer and Load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1866 | 1915 | Updated the image to resolve CVEs. |
| OpenVPN client | 2.5.4-r0-IKS-579 | 2.5.6-r0-IKS-592 | Upgrade openvpn to version `2.5.6-r0`. |
| OpenVPN server | 2.5.4-r0-IKS-578 | 2.5.6-r0-IKS-591 | Upgrade openvpn to version `2.5.6-r0`. |
| OpenVPN Operator image | v1.4.2 | v1.4.3 | Updated ansible operator base image to version v1.19.0 to resolve CVEs. |
| Red Hat {{site.data.keyword.openshiftshort}} Control Plane Operator | v4.6.0-20220308 | v4.6.0-20220411 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0%2B20220411){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20220308 | v4.6.0-20220411 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0%2B20220411){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20220308 | 4.6.0+20220411 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20220411){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.56_1578_openshift" caption-side="top"}



### Change log for worker node fix pack 4.6.56_1581_openshift, released 25 April 2022
{: #4656_1581_openshift}




| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | N/A | N/A | Package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.56_1579_openshift" caption-side="top"}







### Change log for worker node fix pack 4.6.56_1579_openshift, released 11 April 2022
{: #4656_1579_openshift}

The following table shows the changes that are in the worker node fix pack 4.6.56_1579_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL Packages | 3.10.0-1160.59.1 | 3.10.0-1160.62.1 | Kernel and package updates for [CVE-2021-45960](https://nvd.nist.gov/vuln/detail/CVE-2021-45960), [CVE-2021-46143](https://nvd.nist.gov/vuln/detail/CVE-2021-46143), [CVE-2022-22822](https://nvd.nist.gov/vuln/detail/CVE-2022-22822), [CVE-2022-22823](https://nvd.nist.gov/vuln/detail/CVE-2022-22823), [CVE-2022-22824](https://nvd.nist.gov/vuln/detail/CVE-2022-22824), [CVE-2022-22825](https://nvd.nist.gov/vuln/detail/CVE-2022-22825), [CVE-2022-22826](https://nvd.nist.gov/vuln/detail/CVE-2022-22826)   [CVE-2022-22827](https://nvd.nist.gov/vuln/detail/CVE-2022-22827), [CVE-2022-23852](https://nvd.nist.gov/vuln/detail/CVE-2022-23852), [CVE-2022-25235](https://nvd.nist.gov/vuln/detail/CVE-2022-25235), [CVE-2022-25236](https://nvd.nist.gov/vuln/detail/CVE-2022-25236), [CVE-2022-25315](https://nvd.nist.gov/vuln/detail/CVE-2022-25315), [CVE-2021-4028](https://nvd.nist.gov/vuln/detail/CVE-2021-4028), [CVE-2021-4083](https://nvd.nist.gov/vuln/detail/CVE-2021-4083)   [CVE-2022-0778](https://nvd.nist.gov/vuln/detail/CVE-2022-0778). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.56_1577_openshift" caption-side="top"}






### Change log for master fix pack 4.6.56_1578_openshift, released 6 April 2022
{: #4658_1578}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.17.6 | v3.19.4 | See the [Calico release notes](https://projectcalico.docs.tigera.io/archive/v3.19/release-notes/){: external}. |
| Calico Operator | v1.13.11 | v1.17.9 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.17.9){: external}. |
| Cluster health image | v1.3.3 | v1.3.5 | Update golang dependencies.  Update image to version 102 to fix CVEs [CVE-2021-3999](https://access.redhat.com/security/cve/cve-2021-3999){: external}, [CVE-2022-23218](https://nvd.nist.gov/vuln/detail/CVE-2022-23218){: external}, [CVE-2022-23219](https://nvd.nist.gov/vuln/detail/CVE-2022-23219){: external} |
| Gateway-enabled cluster controller | 1653 | 1669 | Updated to use `Go` version `1.17.8`. |
| IBM Calico extension | 929 | 950 | Updated to use `Go` version `1.17.8`. Updated universal base image (UBI) to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.1.7 | v2.2.1 | Bug fixes for driver installation issues. Updated ubi images to `8.5-240` and updated `Go` to version to `1.16.15`. Fixes for CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.16-9 | v1.19.16-10 | Changes to the build. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.filestorage_short}} plug-in and monitor | 405 | 407 | Updated `Go` to version `1.16.14`.  Updated `UBI` image to version `8.5-240`. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 0fc9949 | 6c43ef1 | Upgraded `Go` packages to resolve vulnerabilities |
| Key Management Service provider | v2.4.3 | v2.5.3 | Updated to use `Go` version `1.17.8`. Updated golang dependencies. Fixed CVE [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1748 | 1866 | Updated the image to resolve CVEs. Updated to use `Go` version `1.17.8`. |
| OpenVPN client | 2.5.4-r0-IKS-556 | 2.5.4-r0-IKS-579 | Updated `Go` to version `1.16.15`. |
| OpenVPN server | 2.5.4-r0-IKS-562 | 2.5.4-r0-IKS-578 | Updated `Go` to version `1.16.15`. |
| OpenVPN Operator image | v1.4.1 | v1.4.2 | Updated ansible operator base image to version `v1.18.0` to resolve CVEs. |
| Red Hat OpenShift | 4.6.48 | 4.6.56 | See the [Red Hat OpenShift release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-56){: external}. |
| Red Hat OpenShift Control Plane Operator | v4.6.0-20220222 | v4.6.0-20220308 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20220308){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20220222 | v4.6.0-20220308 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20220308){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20220222 | 4.6.0+20220308 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20220308){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.48_1573_openshift" caption-side="top"}







### Change log for worker node pack 4.6.56_1577_openshift, released 28 March 2022
{: #4656_1577}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL Packages | N/A | N/A | N/A |
| HA proxy | 15198f | b40c07 | [CVE-2021-45960](https://nvd.nist.gov/vuln/detail/CVE-2021-45960){: external}, [CVE-2021-46143](https://nvd.nist.gov/vuln/detail/CVE-2021-46143){: external}, [CVE-2022-22822](https://nvd.nist.gov/vuln/detail/CVE-2022-22822){: external}, [CVE-2022-22823](https://nvd.nist.gov/vuln/detail/CVE-2022-22823){: external}, [CVE-2022-22824](https://nvd.nist.gov/vuln/detail/CVE-2022-22824){: external}, [CVE-2022-22825](https://nvd.nist.gov/vuln/detail/CVE-2022-22825){: external}, [CVE-2022-22826](https://nvd.nist.gov/vuln/detail/CVE-2022-22826){: external}, [CVE-2022-22827](https://nvd.nist.gov/vuln/detail/CVE-2022-22827){: external}, [CVE-2022-23852](https://nvd.nist.gov/vuln/detail/CVE-2022-23852){: external}, [CVE-2022-25235](https://nvd.nist.gov/vuln/detail/CVE-2022-25235){: external}, [CVE-2022-25236](https://nvd.nist.gov/vuln/detail/CVE-2022-25236){: external}, [CVE-2022-25315](https://nvd.nist.gov/vuln/detail/CVE-2022-25315){: external}, [CVE-2021-3999](https://nvd.nist.gov/vuln/detail/CVE-2021-3999){: external}, [CVE-2022-23218](https://nvd.nist.gov/vuln/detail/CVE-2022-23218){: external}, [CVE-2022-23219](https://nvd.nist.gov/vuln/detail/CVE-2022-23219){: external}, [CVE-2022-23308](https://nvd.nist.gov/vuln/detail/CVE-2022-23308){: external}, [CVE-2021-23177](https://nvd.nist.gov/vuln/detail/CVE-2021-23177){: external}, [CVE-2021-31566](https://nvd.nist.gov/vuln/detail/CVE-2021-31566){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.55 | 4.6.56 | See [changelogs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-56){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.55_1575_openshift" caption-side="top"}





### Change log for worker node pack 4.6.55_1575_openshift, released 14 March 2022
{: #4655_1575}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL Packages | N/A | N/A | N/A |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.53 | 4.6.55 | See the [change log](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-55){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.53_1574_openshift" caption-side="top"}





### Change log for master fix pack 4.6.48_1573_openshift, released 3 March 2022
{: #4648_1573}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.21 | v1.3.3 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds fix for [CVE-2021-43565](https://www.whitesourcesoftware.com/vulnerability-database/CVE-2021-43565){: external}. Adds Golang dependency updates. |
| Gateway-enabled cluster controller | 1586 | 1653 | Updated to use `Go` version `1.17.7` and updated `Go` modules to fix CVEs. |
| IBM Calico extension | 923 | 929 | Updated universal base image (UBI) to the `8.5-230` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.1.6 | v2.1.7 | Adds fix for CVE-2021-3538](https://www.whitesourcesoftware.com/vulnerability-database/CVE-2021-3538){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.16-6 | v1.19.16-9 | Adds changes to the renovate rules. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.filestorage_short}} plug-in and monitor | 404 | 405 | Adds fix for [CVE-2021-3538](https://www.whitesourcesoftware.com/vulnerability-database/CVE-2021-3538){: external} and adds dependency updates. |
| Key Management Service provider | v2.3.13 | v2.4.3 | Updated `golang.org/x/crypto` to `v0.0.0-20220214200702-86341886e292`. Adds fix for [CVE-2021-43565](https://www.whitesourcesoftware.com/vulnerability-database/CVE-2021-43565){: external}. Adds Golang dependency updates. |
| OpenVPN server | 2.5.4-r0-IKS-555 | 2.5.4-r0-IKS-562 | Turns off CRL verification in the openvpn image. |
| OpenVPN Operator image | v1.4.0 | v1.4.1 | Turns off CRL verification in the opevpn-operator images. |
| Red Hat OpenShift Control Plane Operator | v4.6.0-20220107 | v4.6.0-20220222 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20220222){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20220107 | v4.6.0-20220222 | See the {{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20220222){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20220107 | 4.6.0+20220222 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20220222){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.48_1570_openshift" caption-side="top"}






### Change log for worker node fix pack 4.6.53_1574_openshift, released 28 February 2022
{: #4653_1574}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | 3.10.0-1160.53.1.el7 | 3.10.0-1160.59.1.el7 | Kernel and package updates for [CVE-2020-25709](https://nvd.nist.gov/vuln/detail/CVE-2020-25709){: external}, [CVE-2020-25710](https://nvd.nist.gov/vuln/detail/CVE-2020-25710){: external}, [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}, [CVE-2020-0465](https://nvd.nist.gov/vuln/detail/CVE-2020-0465){: external}, [CVE-2020-0466](https://nvd.nist.gov/vuln/detail/CVE-2020-0466){: external}, [CVE-2021-0920](https://nvd.nist.gov/vuln/detail/CVE-2021-0920){: external}, [CVE-2021-3564](https://nvd.nist.gov/vuln/detail/CVE-2021-3564){: external}, [CVE-2021-3573](https://nvd.nist.gov/vuln/detail/CVE-2021-3573){: external}, [CVE-2021-3752](https://nvd.nist.gov/vuln/detail/CVE-2021-3752){: external}, [CVE-2021-4155](https://nvd.nist.gov/vuln/detail/CVE-2021-4155){: external}, [CVE-2022-0330](https://nvd.nist.gov/vuln/detail/CVE-2022-0330){: external}, [CVE-2022-22942](https://nvd.nist.gov/vuln/detail/CVE-2022-22942){: external} | 
| HA proxy | f6a2b3 | 15198fb | Contains fixes for [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}. | 
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.53_1572_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.53_1572_openshift, released 14 February 2022
{: #4653_1572}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | N/A |
|  {{site.data.keyword.redhat_openshift_notm}}  | N/A | N/A | N/A |
| HA proxy | d38fa1 | f6a2b3 | [CVE-2021-3521](https://nvd.nist.gov/vuln/detail/CVE-2021-3521){: external}   [CVE-2021-4122](https://nvd.nist.gov/vuln/detail/CVE-2021-4122){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.53_1571_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.53_1571_openshift, released 31 January 2022
{: #4653_1571}

The following table shows the changes that are in the worker node fix pack `4.6.53_1571_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | Updated worker node images with package updates for [CVE-2021-4034](https://nvd.nist.gov/vuln/detail/CVE-2021-4034){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.53_1569_openshift" caption-side="top"}





### Change log for master fix pack 4.6.48_1570_openshift, released 26 January 2022
{: #4648_1570}

The following table shows the changes that are in the master fix pack patch update `4.6.48_1570_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | N/A | N/A | Changed to improve Calico availability during updates. |
| Cluster health image | v1.2.20 | v1.2.21 | Updated to use `Go` version `1.17.5`, updated Go dependencies and golangci-lint. |
| {{site.data.keyword.IBM_notm}} Calico extension | 900 | 923 | Updated universal base image (UBI) to the `8.5-218` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | v2.1.3 | v2.1.6 | Updated to use `Go` version `1.16.13`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.16-5 | v1.19.16-6 | Exclude `CVE-2020-14312` from scanning |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 402 | 404 | Updated universal base image (UBI) to the `8.5-218` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 3430e03 | 0fc9949 | Updated universal base image (UBI) to the `8.5-218` version to resolve CVEs. Updated to use `Go` version `1.16.13`. |
| Key Management Service provider | v2.3.12 | v2.3.13 | Updated `Go` dependencies and golangci-lint. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1660 | 1748 | Updated the Alpine base image to the `3.15` version to resolve CVEs. Updated to use `Go` version `1.17.6`. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.47 | 4.6.48 | Changed the duration of the Kubernetes API server certificate from 825 days to 730 days. Changed the duration of the cluster CA certificate from 30 years to 10 years. Updated to fix [CVE-2021-25735](https://www.ibm.com/support/pages/node/6549374){: external}.  See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-48){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20211201 | v4.6.0-20220107 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0%2B20220107){: external}. |
| OpenVPN client | 2.4.6-r3-IKS-463 | 2.5.4-r0-IKS-556 | Update base image to alpine `3.15` to address CVEs, no longer set the `--compress config` option, updated scripts. |
| OpenVPN server | 2.4.6-r3-IKS-462 | 2.5.4-r0-IKS-555 | Update base image to alpine `3.15` to address CVEs, no longer set the `--compress config` option, updated scripts. |
| OpenVPN Operator image | v1.3.9 | v1.4.0 | Updated `OpenVPN` to version `2.5.4-r0`.  Remove deprecated compression config option from VPN server. Sset cipher explicitly to default value to avoid warning message in logs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20211201 | v4.6.0-20220107 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0%2B20220107){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20211201 | 4.6.0+20220107 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0%2B20220107){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.47_1569_openshift" caption-side="top"}






### Change log for worker node fix pack 4.6.53_1569_openshift, released 18 January 2022
{: #4653_1569}

The following table shows the changes that are in the worker node fix pack `4.6.53_1569_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.49.1.el7 | 3.10.0-1160.53.1.el7 | Kernel and package updates for [CVE-2020-25704](https://nvd.nist.gov/vuln/detail/CVE-2020-25704){: external}, [CVE-2020-36322](https://nvd.nist.gov/vuln/detail/CVE-2020-36322){: external}, [CVE-2021-42739](https://nvd.nist.gov/vuln/detail/CVE-2021-42739){: external}, and [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.52 | 4.6.53 | See the [change logs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-53){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.52_1568_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.52_1568_openshift, released 4 January 2022
{: #4652_1568}

The following table shows the changes that are in the worker node fix pack patch update `4.6.52_1568_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 3b8663 | d38fa1 | Contains fixes for [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.52_1567_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.52_1567_openshift, released 20 December 2021
{: #4652_1567_openshift}

The following table shows the changes that are in the worker node fix pack patch update `4.6.52_1567_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} node | 4.6.49 | 4.6.52 | See the [change logs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-52){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.49_1566_openshift" caption-side="top"}





### Change log for master fix pack 4.6.47_1565_openshift, released 7 December 2021
{: #4647_1565}

The following table shows the changes that are in the master fix pack patch update `4.6.47_1565_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.17.5 | v3.17.6 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases){: external}. |
| Calico Operator | v1.13.9 | v1.13.11 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.13.11){: external}. |
| Cluster health image | v1.2.18 | v1.2.20 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| Gateway-enabled cluster controller | 1567 | 1586 | Updated Alpine base image to the latest `3.14` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.IBM_notm}} Calico extension | 864 | 900 | Updated universal base image (UBI) to the `8.5-204` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | v2.1.2 | v2.1.3 | Updated universal base image (UBI) to the `8.5-204` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 401 | 402 | Updated universal base image (UBI) to the `8.5-204` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 4ca5637 | 3430e03 | Updated universal base image (UBI) to the latest `8.5` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| Key Management Service provider | v2.3.10 | v2.3.12 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| Load balancer and load balancer monitor for {{site.data.keyword.IBM_notm}} Cloud Provider | 1589 | 1660 | Updated Alpine base image to the latest `3.14` version to resolve CVEs. Updated to use `Go` version `1.16.10`. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20211109 | v4.6.0-20211201 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20211201){: external}. |
| OpenVPN Operator image | v1.3.8 | v1.3.9 | Updated ansible operator base image to version `v1.14.0` to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20211109 | v4.6.0-20211201 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20211201){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20211109 | 4.6.0+20211201 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20211201){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.47_1563_openshift" caption-side="top"}






### Change log for worker node fix pack 4.6.49_1566_openshift, released 6 December 2021
{: #4649_1566}

The following table shows the changes that are in the worker node fix pack patch update `4.6.49_1566_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.45 | 3.10.0-1160.49 | Updated worker node images and kernel with package updates. Contains fixes for [CVE-2020-36385](https://nvd.nist.gov/vuln/detail/CVE-2020-36385){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-41617](https://nvd.nist.gov/vuln/detail/CVE-2021-41617){: external}, [CVE-2021-20271](https://nvd.nist.gov/vuln/detail/CVE-2021-20271){: external}"{: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.49_1564_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.49_1564_openshift, released 22 November 2021
{: #4649_1564}

The following table shows the changes that are in the worker node fix pack patch update `4.6.49_1564_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 07f1e9e | 3b8663 | Contains fixes for [CVE-2021-20231](https://nvd.nist.gov/vuln/detail/CVE-2021-20231){: external}, [CVE-2021-20232](https://nvd.nist.gov/vuln/detail/CVE-2021-20232){: external}, [CVE-2021-3580](https://nvd.nist.gov/vuln/detail/CVE-2021-3580){: external}, [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946){: external}, [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947){: external}, [CVE-2021-22876](https://nvd.nist.gov/vuln/detail/CVE-2021-22876){: external}, [CVE-2021-22898](https://nvd.nist.gov/vuln/detail/CVE-2021-22898){: external}, [CVE-2021-22925](https://nvd.nist.gov/vuln/detail/CVE-2021-22925){: external}, [CVE-2019-20838](https://nvd.nist.gov/vuln/detail/CVE-2019-20838){: external}, [CVE-2020-14155](https://nvd.nist.gov/vuln/detail/CVE-2020-14155){: external}, [CVE-2018-20673](https://nvd.nist.gov/vuln/detail/CVE-2018-20673){: external}, [CVE-2021-42574](https://nvd.nist.gov/vuln/detail/CVE-2021-42574){: external}, [CVE-2019-17594](https://nvd.nist.gov/vuln/detail/CVE-2019-17594){: external}, [CVE-2019-17595](https://nvd.nist.gov/vuln/detail/CVE-2019-17595){: external}, [CVE-2020-12762](https://nvd.nist.gov/vuln/detail/CVE-2020-12762){: external}, [CVE-2020-16135](https://nvd.nist.gov/vuln/detail/CVE-2020-16135){: external}, [CVE-2021-3445](https://nvd.nist.gov/vuln/detail/CVE-2021-3445){: external}, [CVE-2021-36084](https://nvd.nist.gov/vuln/detail/CVE-2021-36084){: external}, [CVE-2021-36085](https://nvd.nist.gov/vuln/detail/CVE-2021-36085){: external}, [CVE-2021-36086](https://nvd.nist.gov/vuln/detail/CVE-2021-36086){: external}, [CVE-2021-36087](https://nvd.nist.gov/vuln/detail/CVE-2021-36087){: external}, [CVE-2021-20266](https://nvd.nist.gov/vuln/detail/CVE-2021-20266){: external}, [CVE-2019-18218](https://nvd.nist.gov/vuln/detail/CVE-2019-18218){: external}, [CVE-2021-23840](https://nvd.nist.gov/vuln/detail/CVE-2021-23840){: external}, [CVE-2021-23841](https://nvd.nist.gov/vuln/detail/CVE-2021-23841){: external}, [CVE-2021-27645](https://nvd.nist.gov/vuln/detail/CVE-2021-27645){: external}, [CVE-2021-33574](https://nvd.nist.gov/vuln/detail/CVE-2021-33574){: external}, [CVE-2021-35942](https://nvd.nist.gov/vuln/detail/CVE-2021-35942){: external}, [CVE-2021-33560](https://nvd.nist.gov/vuln/detail/CVE-2021-33560){: external}, [CVE-2019-13750](https://nvd.nist.gov/vuln/detail/CVE-2019-13750){: external}, [CVE-2019-13751](https://nvd.nist.gov/vuln/detail/CVE-2019-13751){: external}, [CVE-2019-19603](https://nvd.nist.gov/vuln/detail/CVE-2019-19603){: external}, [CVE-2019-5827](https://nvd.nist.gov/vuln/detail/CVE-2019-5827){: external}, [CVE-2020-13435](https://nvd.nist.gov/vuln/detail/CVE-2020-13435){: external}, [CVE-2020-24370](https://nvd.nist.gov/vuln/detail/CVE-2020-24370){: external}, [CVE-2021-28153](https://nvd.nist.gov/vuln/detail/CVE-2021-28153){: external}, [CVE-2021-3800](https://nvd.nist.gov/vuln/detail/CVE-2021-3800){: external}, [CVE-2021-33928](https://nvd.nist.gov/vuln/detail/CVE-2021-33928){: external}, [CVE-2021-33929](https://nvd.nist.gov/vuln/detail/CVE-2021-33929){: external}, [CVE-2021-33930](https://nvd.nist.gov/vuln/detail/CVE-2021-33930){: external}, [CVE-2021-33938](https://nvd.nist.gov/vuln/detail/CVE-2021-33938){: external}, and[CVE-2021-3200](https://nvd.nist.gov/vuln/detail/CVE-2021-3200){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.49_1562_openshift" caption-side="top"}





### Change log for master fix pack 4.6.47_1563_openshift, released 17 November 2021
{: #4647_1563}

The following table shows the changes that are in the master fix pack patch update `4.6.47_1563_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.16 | v1.2.18 | Updated `Go` module dependencies and to use `Go` version `1.16.9`.  Updated image for [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946){: external}, [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947){: external}, [CVE-2021-33928](https://nvd.nist.gov/vuln/detail/CVE-2021-33928){: external}, [CVE-2021-33929](https://nvd.nist.gov/vuln/detail/CVE-2021-33929){: external} and [CVE-2021-33930](https://nvd.nist.gov/vuln/detail/CVE-2021-33930){: external}.  |
| etcd | v3.4.17 | v3.4.18 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.18){: external}. |
| Gateway-enabled cluster controller | 1510 | 1567 | Updated to use `Go` version `1.16.9`. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.15-3 | v1.19.16-3 | Updated to support the Kubernetes `1.19.16` release. Updated image for [DLA-2797-1](https://www.debian.org/lts/security/2021/dla-2797){: external}. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | e3cb629 | 4ca5637 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. |
| Key Management Service provider | v2.3.8 | v2.3.10 | Updated `Go` module dependencies and to use `Go` version `1.16.9`.  Updated image for [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1550 | 1589 | Updated to use `Go` version `1.16.9`. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20210923 | v4.6.0-20211109 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20211109){: external}. |
| OpenVPN client | 2.4.6-r3-IKS-386 | 2.4.6-r3-IKS-463 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN server | 2.4.6-r3-IKS-385 | 2.4.6-r3-IKS-462 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN Operator image | v1.3.7 | v1.3.8 | Updated ansible operator base image to version `v1.13.1` to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20210923 | v4.6.0-20211109 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20211109){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20210923 | 4.6.0+20211109 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20211109){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.47_1560_openshift" caption-side="top"}






### Change log for worker node fix pack 4.6.49_1562_openshift, released 10 November 2021
{: #4649_1562}

The following table shows the changes that are in the worker node fix pack patch update `4.6.49_1562_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages| N/A | N/A | Updated worker node image packages for [CVE-2021-42574](https://nvd.nist.gov/vuln/detail/CVE-2021-42574){: external} |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.48 | 4.6.49 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-49){: external} |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.46_1558_openshift" caption-side="top"}





### Change log for master fix pack 4.6.47_1560_openshift, released 29 October 2021
{: #4647_1560}

The following table shows the changes that are in the master fix pack patch update `4.6.47_1560_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.15 | v1.2.16 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs:  [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}, [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}, and [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}. |
| etcd | v3.4.16 | v3.4.17 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.17){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 763 | 864 | Updated to use `Go` version `1.16.9`. Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | v2.1.1 | v2.1.2 | Updated universal base image (UBI) to version `8.4-210` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.15-1 | v1.19.15-3 | Updated to ignore VPC load balancer (LB) state when a LB delete is requested. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.filestorage_short}} plug-in and monitor | 400 | 401 | Updated universal base image (UBI) to the latest `8.4-210` version to resolve CVEs. |
| Key Management Service provider | v2.3.7 | v2.3.8 | Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs:  [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}, [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}, [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}, [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}, and [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.44 | 4.6.47 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-47){: external}.{: external} |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20210917 | v4.6.0-20210923 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210923){: external}. |
| OpenVPN Operator image | v1.3.6 | v1.3.7 | Updated ansible operator base image to version `v1.12.0` to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20210917 | v4.6.0-20210923 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210923){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20210917 | 4.6.0+20210923 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210923){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.44_1556_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.48_1561_openshift, released 25 October 2021
{: #4648_1561}

The following table shows the changes that are in the worker node fix pack patch update `4.6.48_1561_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.46 | 4.6.48 | See [the {{site.data.keyword.redhat_openshift_notm}} changelogs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-48){: external}. |
| RHEL 7 Packages | 3.10.0-1160.42.2.el7 | 3.10.0-1160.45.1.el7 | Updated worker node images and kernel with package updates for [CVE-2021-3778](https://nvd.nist.gov/vuln/detail/CVE-2021-3778){: external} and [CVE-2021-3796](https://nvd.nist.gov/vuln/detail/CVE-2021-3796){: external}. |
| Worker-pool taint automation | N/A | N/A | Fixes known issue related to worker-pool taint automation that prevents workers from getting providerID. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.46_1558_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.46_1558_openshift, released 11 October 2021
{: #4646_1558_openshift}

The following table shows the changes that are in the worker node fix pack patch update `4.6.46_1558_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.45 | 4.6.46 | See the [change logs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-46){: external}. The update resolves CVE-2021-25741 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6515606){: external}). |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.45_1557_openshift" caption-side="top"}





### Change log for master fix pack 4.6.44_1556_openshift, released 28 September 2021
{: #4644_1556}

The following table shows the changes that are in the master fix pack patch update `4.6.44_1556_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.17.2 | v3.17.5 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases){: external}. |
| Calico Operator | v1.13.4 | v1.13.9 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.13.9){: external}. |
| Gateway-enabled cluster controller | 1444 | 1510 | Updated image for [CVE-2021-3711](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3711){: external} and [CVE-2021-3712](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3712){: external}. |
| {{site.data.keyword.IBM_notm}} Cloud Block Storage plug-in and driver | v2.0.9 | v2.1.1 | Updated to use `Go` version `1.16.7`. Updated universal base image (UBI) to the latest `8.4-208` version to resolve CVEs. |
| {{site.data.keyword.IBM_notm}} Cloud Controller Manager | v1.19.14-1 | v1.19.15-1 | Updated to support the Kubernetes `1.19.15` release. Fixed a bug that may cause node initialization to fail when a new node reuses the name of a deleted node. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.filestorage_short}} plug-in and monitor | 398 | 400 | Updated to use `Go` version `1.16.7`. Updated universal base image (UBI) to the latest `8.4-208` version to resolve CVEs. |
| {{site.data.keyword.IBM_notm}} Cloud RBAC Operator | 945df65 | e3cb629 | Updated to use `Go` version `1.16.7`. |
| Kubernetes API server auditing configuration | N/A | N/A| Updated to support `verbose` [Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit#audit-api-server). |
| Load balancer and load balancer monitor for {{site.data.keyword.IBM_notm}} Cloud Provider | 1510 | 1550 | Updated image for [CVE-2021-3711](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3711){: external} and [CVE-2021-3712](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3712){: external}. |
|OpenShift Container Platform| 4.6.42 | 4.6.44 | See the [OpenShift Container Platform release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-44){: external}. |
|OpenShift Container PlatformControl Plane Operator | v4.6.0-20210816 | v4.6.0-20210917 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210917){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20210816 | v4.6.0-20210917 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210917){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20210816 | 4.6.0+20210917 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210917){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.42_1553_openshift" caption-side="top"}







### Change log for worker node fix pack 4.6.45_1557_openshift, released 27 September 2021
{: #4645_1557}

The following table shows the changes that are in the worker node fix pack patch update `4.6.45_1557_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Disk identification | N/A | N/A | Enhanced the disk identification logic to handle the case of 2+ partitions. |
| HA proxy | 9c98dc5 | 07f1e9 | Updated image with fixes for [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}, [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}, [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}, [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}, and [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}. |
|OpenShift Container Platform| 4.6.44 | 4.6.45 | See [changelogs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-45){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.44_1555_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.44_1555_openshift, released 13 September 2021
{: #4644_1555}

The following table shows the changes that are in the worker node fix pack patch update `4.6.44_1555_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| OpenShift Container Platform | 4.6.43 | 4.6.44 |See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-44){: external}. |
| RHEL 7 Packages | 3.10.0-1160.36.2.el7 | 3.10.0-1160.42.2.el7 | Updated worker node image with package updates for [CVE-2021-25214](https://nvd.nist.gov/vuln/detail/CVE-2021-25214){: external}, [CVE-2020-27777](https://nvd.nist.gov/vuln/detail/CVE-2020-27777){: external}, [CVE-2021-22555](https://nvd.nist.gov/vuln/detail/CVE-2021-22555){: external}, [CVE-2021-29154](https://nvd.nist.gov/vuln/detail/CVE-2021-29154){: external}, [CVE-2021-29650](https://nvd.nist.gov/vuln/detail/CVE-2021-29650){: external}, [CVE-2021-32399](https://nvd.nist.gov/vuln/detail/CVE-2021-32399){: external}, and [CVE-2021-3715](https://nvd.nist.gov/vuln/detail/CVE-2021-3715){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.43_1554_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.43_1554_openshift, released 30 August 2021
{: #4643_1554}

The following table shows the changes that are in the worker node fix pack patch update `4.6.43_1554_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| OpenShift Container Platform | 4.6.42 | 4.6.43 | See [changelogs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-43){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.42_1552_openshift" caption-side="top"}





### Change log for master fix pack 4.6.42_1553_openshift, released 25 August 2021
{: #4642_1553}

The following table shows the changes that are in the master fix pack patch update `4.6.42_1553_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | N/A | N/A | Updated the rolling update configuration for the `calico-node` daemonset in the `calico-system` namespace.  The configuration is now the same regardless of the number of cluster worker nodes. |
| Cluster health image | v1.2.14 | v1.2.15 | Updated to use `Go` version `1.15.15`. Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. |
| Cluster master operations | N/A | N/A | Fixes DNS configuration problem that may block {{site.data.keyword.redhat_openshift_notm}} operator updates. |
| Gateway-enabled cluster controller | 1348 | 1444 | Updated image for [CVE-2021-36159](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-36159){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 747 | 763 | Updated to use `Go` version `1.16.6`. Updated universal base image (UBI) to the latest `8.4-205` version to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} plug-in and driver | v2.0.8 | v2.0.9 | Updated to use `Go` version `1.16.6`. Updated image for [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33910){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.13-1 | v1.19.14-1 | Updated to support the Kubernetes `1.19.14` release and to use `Go` version `1.15.15`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 395 | 398 | Updated to use `Go` version `1.16.6`. Updated image for [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33910){: external}. |
| Key Management Service provider | v2.3.6 | v2.3.7 | Updated to use `Go` version `1.15.15`. Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1328 | 1510 | Updated image for [CVE-2020-27780](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-27780){: external}. |
| {{site.data.keyword.redhat_openshift_notm}}| 4.6.38 | 4.6.42 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-42){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20210630 | v4.6.0-20210816 | See the [{{site.data.keyword.openshiftlong_notm}}toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210816){: external}. |
| OpenVPN Operator image | v1.3.4 | v1.3.6 | Updated image for [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33910){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20210630 | v4.6.0-20210816 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210816){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20210630 | 4.6.0+20210816 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210816){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.38_1550_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.42_1552_openshift, released 16 August 2021
{: #4642_1552}

The following table shows the changes that are in the worker node fix pack patch update `4.6.42_1552_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 68e6b3 | 9c98dc | Updated image with fixes for [CVE-2021-27218](https://nvd.nist.gov/vuln/detail/CVE-2021-27218){: external} |
| RHEL 7 Packages | N/A| N/A| Updated image with fixes for: [CVE-2020-0543](https://nvd.nist.gov/vuln/detail/CVE-2020-0543){: external}, [CVE-2020-0548](https://nvd.nist.gov/vuln/detail/CVE-2020-0548){: external}, [CVE-2020-0549](https://nvd.nist.gov/vuln/detail/CVE-2020-0549){: external}, [CVE-2020-8695](https://nvd.nist.gov/vuln/detail/CVE-2020-8695){: external}, [CVE-2020-8696](https://nvd.nist.gov/vuln/detail/CVE-2020-8696){: external}, [CVE-2020-8698](https://nvd.nist.gov/vuln/detail/CVE-2020-8698){: external}, [CVE-2020-24489](https://nvd.nist.gov/vuln/detail/CVE-2020-24489){: external}, [CVE-2020-24511](https://nvd.nist.gov/vuln/detail/CVE-2020-24511){: external}, and [CVE-2020-24512](https://nvd.nist.gov/vuln/detail/CVE-2020-24512){: external}. |
| OpenShift Container Platform | 4.6.40 | 4.6.42 | See [changelogs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-42){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.40_1551_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.40_1551_openshift, released 02 August 2021
{: #4640_1551}

The following table shows the changes that are in the worker node fix pack patch update `4.6.40_1551_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | aae810 | 68e6b3 | Updated image with fixes for [CVE-2021-33910](https://nvd.nist.gov/vuln/detail/CVE-2021-33910){: external}. |
| Registry endpoints | Added ability to access all global registries for private service enabled clusters through the public domain. Added zonal public registry endpoints for clusters with both private and public service endpoints enabled. |
| Read only disk self healing | For VPC Gen2 workers. Added automation to recover from disks going read only. |
| RHEL 7 Packages | 3.10.0-1160.31.1 | 3.10.0-1160.36.2 | Updated worker node images & Kernel with package updates: [CVE-2019-20934](https://nvd.nist.gov/vuln/detail/CVE-2019-20934){: external}, [CVE-2020-11668](https://nvd.nist.gov/vuln/detail/CVE-2020-11668){: external}, [CVE-2021-33033](https://nvd.nist.gov/vuln/detail/CVE-2021-33033){: external}, [CVE-2021-33034](https://nvd.nist.gov/vuln/detail/CVE-2021-33034){: external}, [CVE-2021-33909](https://nvd.nist.gov/vuln/detail/CVE-2021-33909){: external}. |
| OpenShift Container Platform | 4.6.38 |4.6.40 | See [changelogs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-40){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.38_1549_openshift" caption-side="top"}





### Change log for master fix pack 4.6.38_1550_openshift, released 27 July 2021
{: #4638_1550}

The following table shows the changes that are in the master fix pack patch update `4.6.38_1550_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.13 | v1.2.14 | Updated universal base image (UBI) to the latest version to resolve CVEs. |
| etcd | v3.4.14 | v3.4.16 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.16){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 730 | 747 | Updated universal base image (UBI) to version `8.4-205` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} plug-in and driver | v2.0.7 | v2.0.8 | Updated to use Go version `1.16.6`. Updated universal base image (UBI) to version `8.4-205` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.12-2 | v1.19.13-1 | Updated to support the Kubernetes `1.19.13` release and to use Go version `1.15.14`. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 394 | 395 | Updated universal base image (UBI) to version `8.4-205` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | b68ea92 | 945df65 | Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. |
| Key Management Service provider | v2.3.5 | v2.3.6 | Updated universal base image (UBI) to the latest version to resolve CVEs. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.34 | 4.6.38 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-38){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20210608 | v4.6.0-20210630 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210630){: external}. |
| OpenVPN Operator image | v1.3.3 | v1.3.4 | Updated Ansible operator base image to version `1.8.1` to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20210608 | v4.6.0-20210630 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210630){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20210608 | 4.6.0+20210630 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210630){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.34_1547_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.38_1549_openshift, released 19 July 2021
{: #4638_1549}

The following table shows the changes that are in the worker node fix pack `4.6.38_1549_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.36 | 4.6.38 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-38){: external}. |
| RHEL 7 Packages| N/A | N/A | Updated worker node image with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.36_1548_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.36_1548_openshift, released 6 July 2021
{: #4636_1548}

The following table shows the changes that are in the worker node fix pack `4.6.36_1548_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 700dc6 | aae810 | Updated image with fixes for [CVE-2021-3520](https://nvd.nist.gov/vuln/detail/CVE-2021-3520){: external}, [CVE-2021-20271](https://nvd.nist.gov/vuln/detail/CVE-2021-20271){: external}, [CVE-2021-3516](https://nvd.nist.gov/vuln/detail/CVE-2021-3516){: external}, [CVE-2021-3517](https://nvd.nist.gov/vuln/detail/CVE-2021-3517){: external}, [CVE-2021-3518](https://nvd.nist.gov/vuln/detail/CVE-2021-3518){: external}, [CVE-2021-3537](https://nvd.nist.gov/vuln/detail/CVE-2021-3537){: external}, and [CVE-2021-3541](https://nvd.nist.gov/vuln/detail/CVE-2021-3541){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} node | 4.6.34 | 4.6.36 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-36){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.34_1546_openshift" caption-side="top"}





### Change log for master fix pack 4.6.34_1547_openshift, released 28 June 2021
{: #4634_1547}

The following table shows the changes that are in the master fix pack patch update `4.6.34_1547_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.12 | v1.2.13 | Updated to use `Go` version `1.15.12`. Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. |
| Gateway-enabled cluster controller | 1352 | 1348 | Updated to run as a non-root user by default, with privileged escalation as needed. |
| {{site.data.keyword.IBM_notm}} Calico extension | 689 | 730 | Updated to use `Go` version `1.16.15`. Updated minimal universal base image (UBI) to version `8.4` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} plug-in and driver | v2.0.4 | v2.0.7 | Updated to use `Go` version `1.15.12`. Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. Updated minimal UBI to version 8.4 to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.11-3 | v1.19.12-2 | Updated to support the Kubernetes `1.19.12` release and to use `Go` version `1.15.13`. Updated Go dependencies to resolve CVEs. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 392 | 394 | Updated to use `Go` version `1.15.12`. Updated UBI to version `8.4` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 63cd064 | b68ea92 | Update to use `Go` version `1.16.4`. Updated UBI to version `8.4` to resolve CVEs. |
| Key Management Service provider | v2.3.4 | v2.3.5 | Updated to use `Go` version `1.15.12`. Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.28 | 4.6.34 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-34){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20210512 | v4.6.0-20210608 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210608){: external}. |
| OpenVPN Operator image | v1.3.1 | v1.3.3 | Updated ansible operator base image to version `1.8.0` to resolve CVEs and updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| Portieris admission controller | v0.10.2 | v0.10.3 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.10.3){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20210512 | v4.6.0-20210608 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210608){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20210512 | 4.6.0+20210608 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210608){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.28_1543_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.34_1546_openshift, released 22 June 2021
{: #4634_1546}

The following table shows the changes that are in the worker node fix pack `4.6.34_1546_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 26c5cc | d3dc33 | Updated image with fixes for [CVE-2020-24977](https://nvd.nist.gov/vuln/detail/CVE-2020-24977){: external}, [CVE-2020-13434](https://nvd.nist.gov/vuln/detail/CVE-2020-13434){: external}, [CVE-2020-15358](https://nvd.nist.gov/vuln/detail/CVE-2020-15358){: external}, [CVE-2020-29361](https://nvd.nist.gov/vuln/detail/CVE-2020-29361){: external}, [CVE-2020-29362](https://nvd.nist.gov/vuln/detail/CVE-2020-29362){: external}, [CVE-2020-29363](https://nvd.nist.gov/vuln/detail/CVE-2020-29363){: external}, [CVE-2019-2708](https://nvd.nist.gov/vuln/detail/CVE-2019-2708){: external}, [CVE-2019-13012](https://nvd.nist.gov/vuln/detail/CVE-2019-13012){: external}, [CVE-2020-13543](https://nvd.nist.gov/vuln/detail/CVE-2020-13543){: external}, [CVE-2020-13584](https://nvd.nist.gov/vuln/detail/CVE-2020-13584){: external}, [CVE-2020-9948](https://nvd.nist.gov/vuln/detail/CVE-2020-9948){: external}, [CVE-2020-9951](https://nvd.nist.gov/vuln/detail/CVE-2020-9951){: external}, [CVE-2020-9983](https://nvd.nist.gov/vuln/detail/CVE-2020-9983){: external}, [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}, [CVE-2020-8231](https://nvd.nist.gov/vuln/detail/CVE-2020-8231){: external}, [CVE-2020-8284](https://nvd.nist.gov/vuln/detail/CVE-2020-8284){: external}, [CVE-2020-8285](https://nvd.nist.gov/vuln/detail/CVE-2020-8285){: external}, [CVE-2020-8286](https://nvd.nist.gov/vuln/detail/CVE-2020-8286){: external}, [CVE-2016-10228](https://nvd.nist.gov/vuln/detail/CVE-2016-10228){: external}, [CVE-2019-25013](https://nvd.nist.gov/vuln/detail/CVE-2019-25013){: external}, [CVE-2019-9169](https://nvd.nist.gov/vuln/detail/CVE-2019-9169){: external}, [CVE-2020-27618](https://nvd.nist.gov/vuln/detail/CVE-2020-27618){: external}, [CVE-2021-3326](https://nvd.nist.gov/vuln/detail/CVE-2021-3326){: external}, [CVE-2020-26116](https://nvd.nist.gov/vuln/detail/CVE-2020-26116){: external}, [CVE-2020-27619](https://nvd.nist.gov/vuln/detail/CVE-2020-27619){: external}, [CVE-2021-23336](https://nvd.nist.gov/vuln/detail/CVE-2021-23336){: external}, [CVE-2021-3177](https://nvd.nist.gov/vuln/detail/CVE-2021-3177){: external}, [CVE-2019-3842](https://nvd.nist.gov/vuln/detail/CVE-2019-3842){: external}, [CVE-2020-13776](https://nvd.nist.gov/vuln/detail/CVE-2020-13776){: external}, [CVE-2020-24330](https://nvd.nist.gov/vuln/detail/CVE-2020-24330){: external}, [CVE-2020-24331](https://nvd.nist.gov/vuln/detail/CVE-2020-24331){: external}, [CVE-2020-24332](https://nvd.nist.gov/vuln/detail/CVE-2020-24332){: external}, [CVE-2017-14502](https://nvd.nist.gov/vuln/detail/CVE-2017-14502){: external}, [CVE-2020-8927](https://nvd.nist.gov/vuln/detail/CVE-2020-8927){: external} and [CVE-2020-28196](https://nvd.nist.gov/vuln/detail/CVE-2020-28196){: external}. |
| {{site.data.keyword.registrylong_notm}} | N/A | N/A | Added private-only registry support for `ca.icr.io`, `br.icr.io` and `jp2.icr.io`. | 
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.31 | 4.6.34 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-34){: external}. | 
| RHEL 7 Packages | 3.10.0-1160.25 | 3.10.0-1160.31 | Updated worker node image with kernel package updates for [CVE-2020-8648](https://nvd.nist.gov/vuln/detail/CVE-2020-8648){: external}, [CVE-2020-12362](https://nvd.nist.gov/vuln/detail/CVE-2020-12362){: external}[CVE-2020-12363](https://nvd.nist.gov/vuln/detail/CVE-2020-12363){: external}[CVE-2020-12364](https://nvd.nist.gov/vuln/detail/CVE-2020-12364){: external}[CVE-2020-27170](https://nvd.nist.gov/vuln/detail/CVE-2020-27170){: external}[CVE-2021-3347](https://nvd.nist.gov/vuln/detail/CVE-2021-3347){: external}, [CVE-2020-24489](https://nvd.nist.gov/vuln/detail/CVE-2020-24489){: external}, [CVE-2020-24511](https://nvd.nist.gov/vuln/detail/CVE-2020-24511){: external}[CVE-2020-24512](https://nvd.nist.gov/vuln/detail/CVE-2020-24512){: external}, [CVE-2020-24513](https://nvd.nist.gov/vuln/detail/CVE-2020-24513){: external} and [CVE-2021-25217](https://nvd.nist.gov/vuln/detail/CVE-2021-25217){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.5.40_1541_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.31_1545_openshift, released 7 June 2021
{: #4631_1545}

The following table shows the changes that are in the worker node fix pack `4.6.31_1545_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 26c5cc | 700dc6 | Updated the image for [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}.|
|{{site.data.keyword.redhat_openshift_notm}} | 4.6.29 | 4.6.31 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-31){: external}. The update resolves CVE-2021-30465 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6462567){: external}).|
| TCP `keepalive` optimization for VPC | N/A | N/A | Set the `net.ipv4.tcp_keepalive_time` setting to 180 seconds for compatibility with VPC gateways. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates for [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.29_1544_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.29_1544_openshift, released 24 May 2021
{: #4629_1544}

The following table shows the changes that are in the worker node fix pack `4.6.29_1544_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | e0fa2f | 26c5cc | Updated image with fixes for [CVE-2020-26116](https://nvd.nist.gov/vuln/detail/CVE-2020-26116){: external}, [CVE-2020-27619](https://nvd.nist.gov/vuln/detail/CVE-2020-27619){: external}, [CVE-2021-23336](https://nvd.nist.gov/vuln/detail/CVE-2021-23336){: external}, [CVE-2021-3177](https://nvd.nist.gov/vuln/detail/CVE-2021-3177){: external}, [CVE-2019-3842](https://nvd.nist.gov/vuln/detail/CVE-2019-3842){: external}, [CVE-2020-13776](https://nvd.nist.gov/vuln/detail/CVE-2020-13776){: external}, [CVE-2019-18276](https://nvd.nist.gov/vuln/detail/CVE-2019-18276){: external}, [CVE-2020-24977](https://nvd.nist.gov/vuln/detail/CVE-2020-24977){: external}, [CVE-2020-13434](https://nvd.nist.gov/vuln/detail/CVE-2020-13434){: external}, [CVE-2020-15358](https://nvd.nist.gov/vuln/detail/CVE-2020-15358){: external}, [CVE-2019-13012](https://nvd.nist.gov/vuln/detail/CVE-2019-13012){: external}, [CVE-2020-13543](https://nvd.nist.gov/vuln/detail/CVE-2020-13543){: external}, [CVE-2020-13584](https://nvd.nist.gov/vuln/detail/CVE-2020-13584){: external}, [CVE-2020-9948](https://nvd.nist.gov/vuln/detail/CVE-2020-9948){: external}, [CVE-2020-9951](https://nvd.nist.gov/vuln/detail/CVE-2020-9951){: external}, [CVE-2020-9983](https://nvd.nist.gov/vuln/detail/CVE-2020-9983){: external}, [CVE-2020-8231](https://nvd.nist.gov/vuln/detail/CVE-2020-8231){: external}, [CVE-2020-8284](https://nvd.nist.gov/vuln/detail/CVE-2020-8284){: external}, [CVE-2020-8285](https://nvd.nist.gov/vuln/detail/CVE-2020-8285){: external}, [CVE-2020-8286](https://nvd.nist.gov/vuln/detail/CVE-2020-8286){: external}, [CVE-2020-24330](https://nvd.nist.gov/vuln/detail/CVE-2020-24330){: external}, [CVE-2020-24331](https://nvd.nist.gov/vuln/detail/CVE-2020-24331){: external}, [CVE-2020-24332](https://nvd.nist.gov/vuln/detail/CVE-2020-24332){: external}, [CVE-2020-29361](https://nvd.nist.gov/vuln/detail/CVE-2020-29361){: external}, [CVE-2020-29362](https://nvd.nist.gov/vuln/detail/CVE-2020-29362){: external}, [CVE-2020-29363](https://nvd.nist.gov/vuln/detail/CVE-2020-29363){: external}, [CVE-2020-28196](https://nvd.nist.gov/vuln/detail/CVE-2020-28196){: external}, [CVE-2019-2708](https://nvd.nist.gov/vuln/detail/CVE-2019-2708){: external}, [CVE-2016-10228](https://nvd.nist.gov/vuln/detail/CVE-2016-10228){: external}, [CVE-2019-25013](https://nvd.nist.gov/vuln/detail/CVE-2019-25013){: external}, [CVE-2019-9169](https://nvd.nist.gov/vuln/detail/CVE-2019-9169){: external}, [CVE-2020-27618](https://nvd.nist.gov/vuln/detail/CVE-2020-27618){: external}, [CVE-2021-3326](https://nvd.nist.gov/vuln/detail/CVE-2021-3326){: external}, and [CVE-2020-8927](https://nvd.nist.gov/vuln/detail/CVE-2020-8927){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.27 | 4.6.29 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-29){: external}. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.27_1542_openshift" caption-side="top"}






### Change log for master fix pack 4.6.28_1543_openshift, released 24 May 2021
{: #4628_1543}

The following table shows the changes that are in the master fix pack patch update `4.6.28_1543_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.11 | v1.2.12 | Improved the add-on status information that displays when errors occur. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2020-26160](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-26160){: external}, [CVE-2020-28483](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28483){: external} and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| Gateway-enabled cluster controller | 1322 | 1352 | Updated to use `Go` version 1.15.11. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2021-28831](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-28831){: external}, [CVE-2021-30139](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-30139){: external}, [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 618 | 689 | Updated to use `Go` version 1.15.12. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2020-14391](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14391){: external}, [CVE-2020-25661](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-25661){: external} and [CVE-2020-25662](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-25662){: external}. |
| {{site.data.keyword.blockstoragefull}} driver and plug-in | v2.0.3 | v2.0.4 | Updated image for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
| {{site.data.keyword.IBM_notm}} Cloud Controller Manager | v1.19.10-1 | v1.19.11-3 | Updated to support the Kubernetes 1.19.11 release and to use `Go` version 1.15.12. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 390 | 392 | Improved the pre-requisite validation logic for provisioning persistent volume claims (PVCs). Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305{: external}). |
| {{site.data.keyword.IBM_notm}} Cloud RBAC Operator | b6a694b | 63cd064 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2020-28483](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28483){: external}. |
| Key Management Service provider | v2.3.3 | v2.3.4 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2020-28483](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28483){: external} and [CVE-2020-26160](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-26160){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.IBM_notm}} Cloud Provider | 1274 | 1328 | Updated to use Go version 1.15.11. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2021-28831](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-28831){: external}, [CVE-2021-30139](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-30139){: external}, [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.23 | 4.6.28 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-28){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20210331 | v4.6.0-20210512 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210512){: external}. |
| OpenVPN Operator image | v1.3.0 | v1.3.1 | Updated image for [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| Portieris admission controller | v0.10.1 | v0.10.2 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.10.2){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20210331 | v4.6.0-20210512 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210512){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20210331 | 4.6.0+20210512 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210512){: external}. |
{: caption="Changes since version 4.6.23_1540_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.27_1542_openshift, released 10 May 2021
{: #4627_1542}

The following table shows the changes that are in the worker node fix pack `4.6.27_1542_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.25 | 4.6.27 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-27){: external}.|
| RHEL 7 Packages | 3.10.0-1160.24 | 3.10.0-1160.25 | To increase resiliency, `rsyslog` no longer keeps old file descriptors. Updated worker node images with kernel and package updates for [CVE-2021-25215](https://nvd.nist.gov/vuln/detail/CVE-2021-25215){: external}, [CVE-2020-25692](https://nvd.nist.gov/vuln/detail/CVE-2020-25692){: external}, and [CVE-2020-25648](https://nvd.nist.gov/vuln/detail/CVE-2020-25648){: external}.|
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.25_1541_openshift" caption-side="top"}





### Change log for master fix pack 4.6.23_1540_openshift, released 27 April 2021
{: #4623_1540}

The following table shows the changes that are in the master fix pack patch update `4.6.23_1540_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.9 | v1.2.11 | Fixed {{site.data.keyword.redhat_openshift_notm}} version check for unsupported add-ons. Updated to use `Go` version 1.15.11. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external}, [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}, and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| Cluster master operations | N/A | N/A | Resolved an {{site.data.keyword.redhat_openshift_notm}} API server target down alert on clusters that are updated from version 4.4 or earlier. Fixed a bug that can cause `ibmcloud oc cluster config` to fail. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.9-1 | v1.19.10-1 | Updated to support the Kubernetes 1.19.10 release and to use `Go` version 1.15.10. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 389 | 390 | Updated to use `Go` version 1.15.9 and for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}, and [CVE-2021-3121](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3121){: external}. |
|{{site.data.keyword.cloud_notm}} RBAC Operator | 3dd6bbc | b6a694b | Updated image for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
| Key Management Service provider | v2.3.0 | v2.3.3 | Updated to use `Go` version 1.15.11 and for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external}, [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}, and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.22 | 4.6.23 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-23){: external}. |
| OpenVPN client | 2.4.6-r3-IKS-301 | 2.4.6-r3-IKS-386 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN Operator image | v1.2.0 | v1.3.0 | Added OpenVPN support to the {{site.data.keyword.redhat_openshift_notm}} API server to support webhooks. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls and for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external}, [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}, and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| OpenVPN server | 2.4.6-r3-IKS-301 | 2.4.6-r3-IKS-385 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.22_1538_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.25_1541_openshift, released 26 April 2021
{: #4625_1541}

The following table shows the changes that are in the worker node fix pack `4.6.25_1541_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | a3b1ff | e0fa2f | The update addresses [CVE-2021-20305](https://nvd.nist.gov/vuln/detail/CVE-2021-20305){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.23 | 4.6.25 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-25){: external}.<br><br>Configured worker nodes to integrate with a newer version of the NVIDIA GPU operator. Now when you create an instance of the `ClusterPolicy` for the GPU operator, you must enter `450.80.02` for the **Driver Config** version.|
| RHEL 7 Packages | N/A | N/A | Updated worker node images with package updates for [CVE-2021-20305](https://nvd.nist.gov/vuln/detail/CVE-2021-20305){: external}.  |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.23_1539_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.23_1539_openshift, released 12 April 2021
{: #4623_1539}

The following table shows the changes that are in the worker node fix pack `4.6.23_1539_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 9b2dca | a3b1ff | The update addresses [CVE-2021-3449](https://nvd.nist.gov/vuln/detail/CVE-2021-3449){: external} and [CVE-2021-3450](https://nvd.nist.gov/vuln/detail/CVE-2021-3450){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.22 | 4.6.23 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-23){: external}.|
| RHEL 7 Packages | 3.10.0-1160.21.1.el7 | 3.10.0-1160.24.1.el7 | Updated worker node images with kernel and package updates for [CVE-2021-27363](https://nvd.nist.gov/vuln/detail/CVE-2021-27363){: external}, [CVE-2021-27364](https://nvd.nist.gov/vuln/detail/CVE-2021-27364){: external}, and [CVE-2021-27365](https://nvd.nist.gov/vuln/detail/CVE-2021-27365){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.22_1536_openshift" caption-side="top"}





### Change log for master fix pack 4.6.22_1538_openshift, released 2 April 2021
{: #4622_1538}

The following table shows the changes that are in the master fix pack patch update `4.6.22_1538_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.0.1 | v2.0.3 | Updated to use `Go` version 1.15.9 and for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.6.0-20210126 | v4.6.0-20210331 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210331){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.21 | 4.6.22 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-22){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.6.0-20210126 | v4.6.0-20210331 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210331){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.6.0+20210126 | 4.6.0+20210331 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210331){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.21_1535_openshift" caption-side="top"}





### Change log for master fix pack 4.6.21_1535_openshift, released 30 March 2021
{: #4621_1535}

The following table shows the changes that are in the master fix pack patch update `4.6.21_1535_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.at_short}} event | N/A | N/A | Now, the `containers-kubernetes.version.update` event is sent to {{site.data.keyword.at_short}} when a master fix pack update is initiated for a cluster. |
| Cluster health image | v1.2.8 | v1.2.9 | Updated image for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}. |
| Gateway-enabled cluster controller | 1232 | 1322 | Updated to use `Go` version 1.15.10 and for [CVE-2021-23839](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-23839){: external}, [CVE-2021-23840](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-23840){: external}, and [CVE-2021-23841](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-23841){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.8-4 | v1.19.9-1 | Updated to support the Kubernetes 1.19.9 release. Fixed a bug that prevented VPC load balancers from supporting more than 50 subnets in an account. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 388 | 389 | Updated to use `Go` version 1.15.8. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 86de2b7 | 3dd6bbc | Updated image for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.17 | 4.6.21 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-21){: external}. |
| OpenVPN Operator image | v1.1.2 | v1.2.0 | Fixed a bug that could prevent worker node VPN updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.17_1533_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.22_1536_openshift, released 29 March 2021
{: #4622_1536}

The following table shows the changes that are in the worker node fix pack `4.6.22_1536_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.20 | 4.6.22 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-22){: external}.|
| RHEL 7 Packages | 3.10.0-1160.15.2.el7 | 3.10.0-1160.21.1.el7 | Updated worker node images with kernel and package updates for [CVE-2019-19532](https://nvd.nist.gov/vuln/detail/CVE-2019-19532){: external}, [CVE-2020-0427](https://nvd.nist.gov/vuln/detail/CVE-2020-0427){: external}, [CVE-2020-7053](https://nvd.nist.gov/vuln/detail/CVE-2020-7053){: external}, [CVE-2020-14351](https://nvd.nist.gov/vuln/detail/CVE-2020-14351){: external}, [CVE-2020-25211](https://nvd.nist.gov/vuln/detail/CVE-2020-25211){: external}, [CVE-2020-25645](https://nvd.nist.gov/vuln/detail/CVE-2020-25645){: external}, [CVE-2020-25656](https://nvd.nist.gov/vuln/detail/CVE-2020-25656){: external}, [CVE-2020-25705](https://nvd.nist.gov/vuln/detail/CVE-2020-25705){: external}, [CVE-2020-28374](https://nvd.nist.gov/vuln/detail/CVE-2020-28374){: external}, [CVE-2020-29661](https://nvd.nist.gov/vuln/detail/CVE-2020-29661){: external}, and [CVE-2021-20265](https://nvd.nist.gov/vuln/detail/CVE-2021-20265){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.20_1534_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.20_1534_openshift, released 12 March 2021
{: #4620_1534}

The following table shows the changes that are in the worker node fix pack `4.6.20_1534_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.18 | 4.6.20 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-20){: external}.|
| RHEL 7 Packages | N/A | N/A | Updated worker node with package updates for [CVE-2020-8625](https://nvd.nist.gov/vuln/detail/CVE-2020-8625){: external}, [CVE-2020-14372](https://nvd.nist.gov/vuln/detail/CVE-2020-14372){: external}, [CVE-2020-25632](https://nvd.nist.gov/vuln/detail/CVE-2020-25632){: external}, [CVE-2020-25647](https://nvd.nist.gov/vuln/detail/CVE-2020-25647){: external}, [CVE-2020-27749](https://nvd.nist.gov/vuln/detail/CVE-2020-27749){: external}, [CVE-2020-27779](https://nvd.nist.gov/vuln/detail/CVE-2020-27779){: external}, [CVE-2021-20225](https://nvd.nist.gov/vuln/detail/CVE-2021-20225){: external}, [CVE-2021-20233](https://nvd.nist.gov/vuln/detail/CVE-2021-20233){: external}, and [CVE-2021-27803](https://nvd.nist.gov/vuln/detail/CVE-2021-27803){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.18_1533_openshift" caption-side="top"}





### Change log for worker node fix pack 4.6.18_1533_openshift, released 1 March 2021
{: #4618_1533}

The following table shows the changes that are in the worker node fix pack `4.6.18_1533_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Image garbage collection | N/A | N/A | Fixed a race condition during the provisioning of worker nodes that might cause image garbage collection to fail.  |
| {{site.data.keyword.registrylong_notm}} private endpoints | N/A | N/A | **VPC worker nodes**: Fixed a bug where traffic to the private endpoints of {{site.data.keyword.registrylong_notm}} might fail after rebooting the worker node. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.16 | 4.6.18 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-18){: external}.|
| OpenShift Data Foundation | N/A | N/A | Fixed the worker node configuration to resolve an error with deploying ODF. |
| RHEL 7 Packages | N/A | N/A | Updated worker node with package updates. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.16_1529_openshift" caption-side="top"}





### Change log for master fix pack 4.6.17_1533_openshift, released 27 February 2021
{: #4617_1533}

The following table shows the changes that are in the master fix pack patch update `4.6.17_1533_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.8-1 | v1.19.8-4 | Updated to use `calicoctl` version 3.16.8. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1165 | 1274 | Fixed a bug that might cause version 2.0 network load balancers (NLBs) to crash and restart on load balancer updates. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.6.16 | 4.6.17 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-17){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.16_1532_openshift" caption-side="top"}





### Change log for master fix pack 4.6.16_1532_openshift, released 22 February 2021
{: #4616_1532}

The following table shows the changes that are in the master fix pack patch update `4.6.16_1532_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.19.7-13 | v1.19.8-1 | Updated to support the Kubernetes 1.19.8 release and to use `Go` version 1.15.8. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| Key Management Service provider | v2.2.4 | v2.3.0 | Updated to use `Go` version 1.15.7. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| OpenVPN Operator image | v1.1.0 | v1.1.2 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.6.16_1530_openshift" caption-side="top"}





### Change log for 4.6.16_1530_openshift (master) and 4.6.16_1529_openshift (worker node), released 17 February 2020
{: #4616_1530}

The following table shows the changes that are in the version updates for the `4.6.16_1530_openshift` master fix pack and `4.6.16_1529_openshift` worker node fix pack.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Calico | v3.16.5 | v3.17.2 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases){: external}. |
| Calico Operator | v1.10.9 | v1.13.4 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.13.4){: external}. |
| Cluster health image | v1.2.6 | v1.2.8 | Updated to use `Go` version 1.15.7. Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| Gateway-enabled cluster controller | 1195 | 1232 | Updated to use `Go` version 1.15.7. |
| {{site.data.keyword.IBM_notm}} Calico extension | 567 | 618 | Updated to use `Go` version 1.15.7. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.18.15-3 | v1.19.7-13 | Updated to support the Kubernetes 1.19.7 release and to use `Go` version 1.15.5 and `calicoctl` version 3.16.7. Classic network load balancers (NLBs) now set the `NET_RAW` security context. Added support for VPC network load balancers. Updated version 1.0 and 2.0 network load balancers (NLBs) to run as a non-root user by default, with privileged escalation as needed. Updated image for [DLA-2509-1](https://www.debian.org/lts/security/2020/dla-2509){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 385 | 388 | Improved the retry logic for provisioning persistent volume claims (PVCs). |
| {{site.data.keyword.cloud_notm}} RBAC Operator | f859228 | 86de2b7 | Updated to use `Go` version 1.15.7. |
| Key Management Service provider | v2.2.3 | v2.2.4 | Updated image to implement additional {{site.data.keyword.IBM_notm}} security controls. |
| {{site.data.keyword.redhat_openshift_notm}} configuration | N/A | N/A | Updated the [feature gate configuration](/docs/openshift?topic=openshift-service-settings#feature-gates). |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1078 | 1165 | Updated to run as a non-root user by default, with privileged escalation as needed. Updated to use `Go` version 1.15.7. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.5.0-20210112 | v4.6.0-20210126 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/v4.6.0+20210126){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.24 (master), 4.5.31 (worker) | 4.6.16 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-16){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.5.0-20210112 | v4.6.0-20210126 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/v4.6.0+20210126){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.5.0+20210112 | 4.6.0+20210126 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.6.0+20210126){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.5.24_1527_openshift (master) and 4.5.31_1529_openshift (worker node)" caption-side="top"}

