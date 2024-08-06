---

copyright:
 years: 2014, 2024
lastupdated: "2024-08-06"


keywords: openshift, change log, version, unsupported, supported, deprecated

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}





# Archived version change logs
{: #changelog_archive}

The following versions are no longer supported for {{site.data.keyword.openshiftlong}}. You can review the archive of the change logs.
{: shortdesc}

Unsupported versions: [Archived version history](/docs/openshift?topic=openshift-sitemap#sitemap_archived_version_history)

Looking for the change logs of supported versions? See [{{site.data.keyword.redhat_openshift_notm}} version change log](/docs/openshift?topic=openshift-openshift_versions).
{: tip}

## Version 4.5 change log (Unsupported as of 10 October 2021)
{: #version-45}

Version 4.5 is unsupported. You can review the following archive of the 4.5 change logs.
{: shortdesc}

### Change log for worker node fix pack 4.5.41_1553_openshift, released 27 September 2021
{: #4541_1553}

The following table shows the changes that are in the worker node fix pack patch update `4.5.41_1553_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Disk identification | N/A | N/A | Enhanced the disk identification logic to handle the case of 2+ partitions. |
| Haproxy | 9c98dc5 | 07f1e9 | Updated image with fixes for [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}, [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}, [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}, [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}, and [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}. |
{: caption="Changes since version 4.5.41_1551_openshift" caption-side="bottom"}

### Change log for master fix pack 4.5.41_1552_openshift, released 28 September 2021
{: #4541_1552}

The following table shows the changes that are in the master fix pack patch update `4.5.41_1552_openshift`. Master patch updates are applied automatically. 
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Gateway-enabled cluster controller | 1444 | 1510 | Updated image for [CVE-2021-3711](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3711){: external} and [CVE-2021-3712](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3712){: external}. |
| IBM Cloud Block Storage plug-in and driver | v2.0.9 | v2.1.1 | Updated to use `Go` version `1.16.7`. Updated universal base image (UBI) to the latest `8.4-208` version to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.filestorage_short}} plug-in and monitor | 398 | 400 | Updated to use `Go` version `1.16.7`. Updated universal base image (UBI) to the latest `8.4-208` version to resolve CVEs. |
| IBM Cloud RBAC Operator | 945df65 | e3cb629 | Updated to use `Go` version `1.16.7`. |
| Load balancer and load balancer monitor for IBM Cloud Provider | 1510 | 1550 | Updated image for [CVE-2021-3711](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3711){: external} and [CVE-2021-3712](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3712){: external}. |
| Kubernetes API server auditing configuration | N/A | N/A| Updated to support `verbose` [Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit#audit-api-server). |
|OpenShift Container PlatformControl Plane Operator | v4.5.0-20210816 | v4.5.0-20210830 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210830){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.5.0-20210816 | v4.5.0-20210830 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210830){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.5.0+20210816 | 4.5.0+20210830 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210830){: external}. |
{: caption="Changes since version 4.5.41_1549_openshift" caption-side="bottom"}



### Change log for worker node fix pack 4.5.41_1551_openshift, released 13 September 2021
{: #4541_1551}

The following table shows the changes that are in the worker node fix pack patch update `4.5.41_1551_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 7 Packages | 3.10.0-1160.36.2.el7 | 3.10.0-1160.42.2.el7 | Updated worker node image package updates for [CVE-2021-25214](https://nvd.nist.gov/vuln/detail/CVE-2021-25214){: external}, [CVE-2020-27777](https://nvd.nist.gov/vuln/detail/CVE-2020-27777){: external}, [CVE-2021-22555](https://nvd.nist.gov/vuln/detail/CVE-2021-22555){: external}, [CVE-2021-29154](https://nvd.nist.gov/vuln/detail/CVE-2021-29154){: external}, [CVE-2021-29650](https://nvd.nist.gov/vuln/detail/CVE-2021-29650){: external}, [CVE-2021-32399](https://nvd.nist.gov/vuln/detail/CVE-2021-32399){: external}, and [CVE-2021-3715](https://nvd.nist.gov/vuln/detail/CVE-2021-3715){: external}. |
{: caption="Changes since version 4.5.41_1549_openshift" caption-side="bottom"}

### Change log for master fix pack 4.5.41_1549_openshift, released 25 August 2021
{: #4541_1549}

The following table shows the changes that are in the master fix pack patch update `4.5.41_1549_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.14 | v1.2.15 | Updated to use `Go` version `1.15.15`. Updated universal base image (UBI) to the latest `8.4` version to resolve CVEs. |
| Gateway-enabled cluster controller | 1348 | 1444 | Updated image for [CVE-2021-36159](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-36159){: external}. |
| IBM Calico extension | 747 | 763 | Updated to use `Go` version `1.16.6`. Updated universal base image (UBI) to the latest `8.4-205` version to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} plug-in and driver | v2.0.8 | v2.0.9 | Updated to use `Go` version `1.16.6`. Updated image for [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33910){: external}. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.filestorage_short}} plug-in and monitor | 395 | 398 | Updated to use `Go` version `1.16.6`. Updated image for [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33910){: external}. |
| Key Management Service provider | v2.3.6 | v2.3.7 | Updated to use `Go` version `1.15.15`. Updated UBI to the latest `8.4` version to resolve CVEs. |
| Load balancer and load balancer monitor for IBM Cloud Provider | 1328 | 1510 | Updated image for [CVE-2020-27780](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-27780){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.5.0-20210630 | v4.5.0-20210816 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210816){: external}. |
| OpenVPN Operator image | v1.3.4 | v1.3.6 | Updated image for [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33910){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Cloud Metrics Server | v4.5.0-20210630 | v4.5.0-20210816 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210816){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.5.0+20210630 | 4.5.0+20210816 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210816){: external}. |
{: caption="Changes since version 4.5.41_1546_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.5.41_1548_openshift, released 16 August 2021
{: #4541_1548}

The following table shows the changes that are in the worker node fix pack patch update `4.5.41_1548_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}


| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | 68e6b3 | 9c98dc | Updated image with fixes for [CVE-2021-27218](https://nvd.nist.gov/vuln/detail/CVE-2021-27218){: external} |
| RHEL Packages | N/A| N/A| Updated image with fixes for: [CVE-2020-0543](https://nvd.nist.gov/vuln/detail/CVE-2020-0543){: external}, [CVE-2020-0548](https://nvd.nist.gov/vuln/detail/CVE-2020-0548){: external}, [CVE-2020-0549](https://nvd.nist.gov/vuln/detail/CVE-2020-0549){: external}, [CVE-2020-8695](https://nvd.nist.gov/vuln/detail/CVE-2020-8695){: external}, [CVE-2020-8696](https://nvd.nist.gov/vuln/detail/CVE-2020-8696){: external}, [CVE-2020-8698](https://nvd.nist.gov/vuln/detail/CVE-2020-8698){: external}, [CVE-2020-24489](https://nvd.nist.gov/vuln/detail/CVE-2020-24489){: external}, [CVE-2020-24511](https://nvd.nist.gov/vuln/detail/CVE-2020-24511){: external}, and [CVE-2020-24512](https://nvd.nist.gov/vuln/detail/CVE-2020-24512){: external}. |
{: caption="Changes since version 4.6.40_1551_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.41_1547_openshift, released 02 August 2021
{: #4541_1547}

The following table shows the changes that are in the worker node fix pack patch update `4.5.41_1547_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HA proxy | aae810 | 68e6b3 | Updated image with fixes for [CVE-2021-33910](https://nvd.nist.gov/vuln/detail/CVE-2021-33910){: external}. |
| Registry endpoints | Added ability to access all global registries for private service enabled clusters through the public domain. Added zonal public registry endpoints for clusters with both private and public service endpoints enabled. |
| Read only disk self healing | For VPC Gen2 workers. Added automation to recover from disks going read only. |
| RHEL 7 Packages | 3.10.0-1160.31.1 | 3.10.0-1160.36.2 | Updated worker node images & Kernel with package updates: [CVE-2019-20934](https://nvd.nist.gov/vuln/detail/CVE-2019-20934){: external}, [CVE-2020-11668](https://nvd.nist.gov/vuln/detail/CVE-2020-11668){: external}, [CVE-2021-33033](https://nvd.nist.gov/vuln/detail/CVE-2021-33033){: external}, [CVE-2021-33034](https://nvd.nist.gov/vuln/detail/CVE-2021-33034){: external}, [CVE-2021-33909](https://nvd.nist.gov/vuln/detail/CVE-2021-33909){: external}. |
| OpenShift Container Platform | 4.6.38 |4.6.40 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-40){: external}. |
{: caption="Changes since version 4.5.41_1545_openshift" caption-side="bottom"}

### Change log for fix pack 4.5.41_1546_openshift, released 27 July 2021
{: #4541_1546}

The following table shows the changes that are in the master fix pack patch update `4.5.41_1546_openshift`. Master patch updates are applied automatically. 
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.13 | v1.2.14 | Updated universal base image (UBI) to the latest version to resolve CVEs. |
| etcd | v3.4.14 | v3.4.16 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.16){: external}). |
| IBM Calico extension | 730 | 747 | Updated universal base image (UBI) to version `8.4-205` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} plug-in and driver | v2.0.7 | v2.0.8 | Updated to use Go version `1.16.6`. Updated universal base image (UBI) to version `8.4-205` to resolve CVEs. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 394 | 395 | Updated universal base image (UBI) to version `8.4-205` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | b68ea92 | 945df65 | Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. |
| Key Management Service provider | v2.3.5 | v2.3.6 | Updated universal base image (UBI) to the latest version to resolve CVEs. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.40 | 4.5.41 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-41){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.5.0-20210608 | v4.5.0-20210630 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210630){: external}. |
| OpenVPN Operator image | v1.3.3 | v1.3.4 | Updated Ansible operator base image to version `1.8.1` to resolve CVEs. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.5.0-20210608 | v4.5.0-20210630 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210630){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.5.0+20210608 | 4.5.0+20210630 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210630){: external}. |
{: caption="Changes since version 4.5.40_1543_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.41_1545_openshift, released 19 July 2021
{: #4541_1545}

The following table shows the changes that are in the worker node fix pack `4.5.41_1545_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.40 | 4.5.41 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-41){: external}. |
| RHEL 7 Packages| N/A | N/A | Updated worker node image with package updates. |
{: caption="Changes since version 4.5.40_1544_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.40_1544_openshift, released 6 July 2021
{: #4540_1544}

The following table shows the changes that are in the worker node fix pack `4.5.40_1544_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 700dc6 | aae810 | Updated image with fixes for [CVE-2021-3520](https://nvd.nist.gov/vuln/detail/CVE-2021-3520){: external}, [CVE-2021-20271](https://nvd.nist.gov/vuln/detail/CVE-2021-20271){: external}, [CVE-2021-3516](https://nvd.nist.gov/vuln/detail/CVE-2021-3516){: external}, [CVE-2021-3517](https://nvd.nist.gov/vuln/detail/CVE-2021-3517){: external}, [CVE-2021-3518](https://nvd.nist.gov/vuln/detail/CVE-2021-3518){: external}, [CVE-2021-3537](https://nvd.nist.gov/vuln/detail/CVE-2021-3537){: external}, and [CVE-2021-3541](https://nvd.nist.gov/vuln/detail/CVE-2021-3541){: external}. |
{: caption="Changes since version 4.5.40_1542_openshift" caption-side="bottom"}

### Change log for master fix pack 4.5.40_1543_openshift, released 28 June 2021
{: #4540_1543}

The following table shows the changes that are in the master fix pack patch update `4.5.40_1543_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.12 | v1.2.13 | Updated to use `Go` version `1.15.12`. Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. |
| Gateway-enabled cluster controller | 1352 | 1348 | Updated to run as a non-root user by default, with privileged escalation as needed. |
| IBM Calico extension | 689 | 730 | Updated to use `Go` version `1.16.15`. Updated minimal universal base image (UBI) to version `8.4` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} plug-in and driver | v2.0.4 | v2.0.7 | Updated to use `Go` version `1.15.12`. Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. Updated minimal UBI to version `8.4` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.18.19-2 | v1.18.20-1 | Updated to support the Kubernetes `1.18.20` release. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 392 | 394 | Updated to use `Go` version `1.15.12`. Updated UBI to version `8.4` to resolve CVEs. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 63cd064 | b68ea92 | Update to use `Go` version `1.16.4`. Updated UBI to version `8.4` to resolve CVEs. |
| Key Management Service provider | v2.3.4 | v2.3.5 | Updated to use `Go` version `1.15.12`. Updated image for [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33194){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.39 | 4.5.40 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-40){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.5.0-20210512 | v4.5.0-20210608 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210608){: external}. |
| OpenVPN Operator image | v1.3.1 | v1.3.3 | Updated ansible operator base image to version `1.8.0` to resolve CVEs and updated image to implement additional IBM security controls. |
| Portieris admission controller | v0.10.2 | v0.10.3 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.10.3){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.5.0-20210512 | v4.5.0-20210608 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210608){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.5.0+20210512 | 4.5.0+20210608 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210608){: external}. |
{: caption="Changes since version 4.5.39_1539_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.40_1542_openshift, released 22 June 2021
{: #4540_1542}

The following table shows the changes that are in the worker node fix pack `4.5.40_1542_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 26c5cc | d3dc33 | Updated image with fixes for [CVE-2020-24977](https://nvd.nist.gov/vuln/detail/CVE-2020-24977){: external}, [CVE-2020-13434](https://nvd.nist.gov/vuln/detail/CVE-2020-13434){: external}, [CVE-2020-15358](https://nvd.nist.gov/vuln/detail/CVE-2020-15358){: external}, [CVE-2020-29361](https://nvd.nist.gov/vuln/detail/CVE-2020-29361){: external}, [CVE-2020-29362](https://nvd.nist.gov/vuln/detail/CVE-2020-29362){: external}, [CVE-2020-29363](https://nvd.nist.gov/vuln/detail/CVE-2020-29363){: external}, [CVE-2019-2708](https://nvd.nist.gov/vuln/detail/CVE-2019-2708){: external}, [CVE-2019-13012](https://nvd.nist.gov/vuln/detail/CVE-2019-13012){: external}, [CVE-2020-13543](https://nvd.nist.gov/vuln/detail/CVE-2020-13543){: external}, [CVE-2020-13584](https://nvd.nist.gov/vuln/detail/CVE-2020-13584){: external}, [CVE-2020-9948](https://nvd.nist.gov/vuln/detail/CVE-2020-9948){: external}, [CVE-2020-9951](https://nvd.nist.gov/vuln/detail/CVE-2020-9951){: external}, [CVE-2020-9983](https://nvd.nist.gov/vuln/detail/CVE-2020-9983){: external}, [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}, [CVE-2020-8231](https://nvd.nist.gov/vuln/detail/CVE-2020-8231){: external}, [CVE-2020-8284](https://nvd.nist.gov/vuln/detail/CVE-2020-8284){: external}, [CVE-2020-8285](https://nvd.nist.gov/vuln/detail/CVE-2020-8285){: external}, [CVE-2020-8286](https://nvd.nist.gov/vuln/detail/CVE-2020-8286){: external}, [CVE-2016-10228](https://nvd.nist.gov/vuln/detail/CVE-2016-10228){: external}, [CVE-2019-25013](https://nvd.nist.gov/vuln/detail/CVE-2019-25013){: external}, [CVE-2019-9169](https://nvd.nist.gov/vuln/detail/CVE-2019-9169){: external}, [CVE-2020-27618](https://nvd.nist.gov/vuln/detail/CVE-2020-27618){: external}, [CVE-2021-3326](https://nvd.nist.gov/vuln/detail/CVE-2021-3326){: external}, [CVE-2020-26116](https://nvd.nist.gov/vuln/detail/CVE-2020-26116){: external}, [CVE-2020-27619](https://nvd.nist.gov/vuln/detail/CVE-2020-27619){: external}, [CVE-2021-23336](https://nvd.nist.gov/vuln/detail/CVE-2021-23336){: external}, [CVE-2021-3177](https://nvd.nist.gov/vuln/detail/CVE-2021-3177){: external}, [CVE-2019-3842](https://nvd.nist.gov/vuln/detail/CVE-2019-3842){: external}, [CVE-2020-13776](https://nvd.nist.gov/vuln/detail/CVE-2020-13776){: external}, [CVE-2020-24330](https://nvd.nist.gov/vuln/detail/CVE-2020-24330){: external}, [CVE-2020-24331](https://nvd.nist.gov/vuln/detail/CVE-2020-24331){: external}, [CVE-2020-24332](https://nvd.nist.gov/vuln/detail/CVE-2020-24332){: external}, [CVE-2017-14502](https://nvd.nist.gov/vuln/detail/CVE-2017-14502){: external}, [CVE-2020-8927](https://nvd.nist.gov/vuln/detail/CVE-2020-8927){: external} and [CVE-2020-28196](https://nvd.nist.gov/vuln/detail/CVE-2020-28196){: external}. |
| {{site.data.keyword.registrylong_notm}} | N/A | N/A | Added private-only registry support for `ca.icr.io`, `br.icr.io` and `jp2.icr.io`. | 
|RHEL 7 Packages | 3.10.0-1160.25 | 3.10.0-1160.31 | Updated worker node image with kernel package updates for [CVE-2020-8648](https://nvd.nist.gov/vuln/detail/CVE-2020-8648){: external}, [CVE-2020-12362](https://nvd.nist.gov/vuln/detail/CVE-2020-12362){: external}[CVE-2020-12363](https://nvd.nist.gov/vuln/detail/CVE-2020-12363){: external}[CVE-2020-12364](https://nvd.nist.gov/vuln/detail/CVE-2020-12364){: external}[CVE-2020-27170](https://nvd.nist.gov/vuln/detail/CVE-2020-27170){: external}[CVE-2021-3347](https://nvd.nist.gov/vuln/detail/CVE-2021-3347){: external}, [CVE-2020-24489](https://nvd.nist.gov/vuln/detail/CVE-2020-24489){: external}, [CVE-2020-24511](https://nvd.nist.gov/vuln/detail/CVE-2020-24511){: external}[CVE-2020-24512](https://nvd.nist.gov/vuln/detail/CVE-2020-24512){: external}, [CVE-2020-24513](https://nvd.nist.gov/vuln/detail/CVE-2020-24513){: external} and [CVE-2021-25217](https://nvd.nist.gov/vuln/detail/CVE-2021-25217){: external}.|
{: caption="Changes since version 4.5.40_1541_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.40_1541_openshift, released 7 June 2021
{: #4540_1541}

The following table shows the changes that are in the worker node fix pack `4.5.40_1541_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 26c5cc | 700dc6 | Updated the image for [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}.|
|{{site.data.keyword.redhat_openshift_notm}} | 4.5.39 | 4.5.40 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-40){: external}. The update resolves CVE-2021-30465 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6462567){: external}).|
| TCP `keepalive` optimization for VPC | N/A | N/A | Set the `net.ipv4.tcp_keepalive_time` setting to 180 seconds for compatibility with VPC gateways. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates for [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}.|
{: caption="Changes since version 4.5.39_1540_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.39_1540_openshift, released 24 May 2021
{: #4539_1540}

The following table shows the changes that are in the worker node fix pack `4.5.39_1540_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | e0fa2f | 26c5cc | Updated image with fixes for [CVE-2020-26116](https://nvd.nist.gov/vuln/detail/CVE-2020-26116){: external}, [CVE-2020-27619](https://nvd.nist.gov/vuln/detail/CVE-2020-27619){: external}, [CVE-2021-23336](https://nvd.nist.gov/vuln/detail/CVE-2021-23336){: external}, [CVE-2021-3177](https://nvd.nist.gov/vuln/detail/CVE-2021-3177){: external}, [CVE-2019-3842](https://nvd.nist.gov/vuln/detail/CVE-2019-3842){: external}, [CVE-2020-13776](https://nvd.nist.gov/vuln/detail/CVE-2020-13776){: external}, [CVE-2019-18276](https://nvd.nist.gov/vuln/detail/CVE-2019-18276){: external}, [CVE-2020-24977](https://nvd.nist.gov/vuln/detail/CVE-2020-24977){: external}, [CVE-2020-13434](https://nvd.nist.gov/vuln/detail/CVE-2020-13434){: external}, [CVE-2020-15358](https://nvd.nist.gov/vuln/detail/CVE-2020-15358){: external}, [CVE-2019-13012](https://nvd.nist.gov/vuln/detail/CVE-2019-13012){: external}, [CVE-2020-13543](https://nvd.nist.gov/vuln/detail/CVE-2020-13543){: external}, [CVE-2020-13584](https://nvd.nist.gov/vuln/detail/CVE-2020-13584){: external}, [CVE-2020-9948](https://nvd.nist.gov/vuln/detail/CVE-2020-9948){: external}, [CVE-2020-9951](https://nvd.nist.gov/vuln/detail/CVE-2020-9951){: external}, [CVE-2020-9983](https://nvd.nist.gov/vuln/detail/CVE-2020-9983){: external}, [CVE-2020-8231](https://nvd.nist.gov/vuln/detail/CVE-2020-8231){: external}, [CVE-2020-8284](https://nvd.nist.gov/vuln/detail/CVE-2020-8284){: external}, [CVE-2020-8285](https://nvd.nist.gov/vuln/detail/CVE-2020-8285){: external}, [CVE-2020-8286](https://nvd.nist.gov/vuln/detail/CVE-2020-8286){: external}, [CVE-2020-24330](https://nvd.nist.gov/vuln/detail/CVE-2020-24330){: external}, [CVE-2020-24331](https://nvd.nist.gov/vuln/detail/CVE-2020-24331){: external}, [CVE-2020-24332](https://nvd.nist.gov/vuln/detail/CVE-2020-24332){: external}, [CVE-2020-29361](https://nvd.nist.gov/vuln/detail/CVE-2020-29361){: external}, [CVE-2020-29362](https://nvd.nist.gov/vuln/detail/CVE-2020-29362){: external}, [CVE-2020-29363](https://nvd.nist.gov/vuln/detail/CVE-2020-29363){: external}, [CVE-2020-28196](https://nvd.nist.gov/vuln/detail/CVE-2020-28196){: external}, [CVE-2019-2708](https://nvd.nist.gov/vuln/detail/CVE-2019-2708){: external}, [CVE-2016-10228](https://nvd.nist.gov/vuln/detail/CVE-2016-10228){: external}, [CVE-2019-25013](https://nvd.nist.gov/vuln/detail/CVE-2019-25013){: external}, [CVE-2019-9169](https://nvd.nist.gov/vuln/detail/CVE-2019-9169){: external}, [CVE-2020-27618](https://nvd.nist.gov/vuln/detail/CVE-2020-27618){: external}, [CVE-2021-3326](https://nvd.nist.gov/vuln/detail/CVE-2021-3326){: external}, and [CVE-2020-8927](https://nvd.nist.gov/vuln/detail/CVE-2020-8927){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.38 | 4.5.39 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-39){: external}. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates.|
{: caption="Changes since version 4.5.38_1538_openshift" caption-side="bottom"}

### Change log for master fix pack 4.5.39_1539_openshift, released 24 May 2021
{: #4539_1539}

The following table shows the changes that are in the master fix pack patch update `4.5.39_1539_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.11 | v1.2.12 | Improved the add-on status information that displays when errors are occur. Updated image to implement additional IBM security controls and for [CVE-2020-26160](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-26160){: external}, [CVE-2020-28483](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28483){: external} and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| Gateway-enabled cluster controller | 1322 | 1352 | Updated to use `Go` version 1.15.11. Updated image to implement additional IBM security controls and for [CVE-2021-28831](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-28831){: external}, [CVE-2021-30139](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-30139){: external}, [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
| IBM Calico extension | 618 | 689 | Updated to use `Go` version 1.15.12. Updated image to implement additional IBM security controls and for [CVE-2020-14391](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14391){: external}, [CVE-2020-25661](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-25661){: external} and [CVE-2020-25662](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-25662){: external}. |
| {{site.data.keyword.blockstoragefull}} driver and plug-in | v2.0.3 | v2.0.4 | Updated image for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
| IBM Cloud Controller Manager | v1.18.18-1 | v1.18.19-2 | Updated to support the Kubernetes 1.18.19 release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 390 | 392 | Improved the prerequisite validation logic for provisioning persistent volume claims (PVCs). Updated image to implement additional IBM security controls and for [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| IBM Cloud RBAC Operator | b6a694b | 63cd064 | Updated image to implement additional IBM security controls and for [CVE-2020-28483](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28483){: external}. |
| Key Management Service provider | v2.3.3 | v2.3.4 | Updated image to implement additional IBM security controls and for [CVE-2020-28483](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28483){: external} and [CVE-2020-26160](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-26160){: external}. |
| Load balancer and load balancer monitor for IBM Cloud Provider | 1274 | 1328 | Updated to use Go version 1.15.11. Updated image to implement additional IBM security controls and for [CVE-2021-28831](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-28831){: external}, [CVE-2021-30139](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-30139){: external}, [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
| {{site.data.keyword.redhat_openshift_notm}}  | 4.5.37 | 4.5.39 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-39){: external}. |
| {{site.data.keyword.redhat_openshift_notm}}  Control Plane Operator | v4.5.0-20210329 | v4.5.0-20210512 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases){: external}. |
| OpenVPN Operator image | v1.3.0 | v1.3.1 | Updated image for [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| Portieris admission controller | v0.10.1 | v0.10.2 | See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.10.2){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.5.0-20210329 | v4.5.0-20210512 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210512){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.5.0+20210329 | 4.5.0+20210512 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210512){: external}). |
{: caption="Changes since version 4.5.37_1536_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.38_1538_openshift, released 10 May 2021
{: #4538_1538}

The following table shows the changes that are in the worker node fix pack `4.5.38_1538_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.37 | 4.5.38 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-38){: external}.  \n  \n Configured worker nodes to integrate with a newer version of the NVIDIA GPU operator. Now when you create an instance of the `ClusterPolicy` for the GPU operator, you must enter `450.80.02` for the **Driver Config** version.|
| RHEL 7 Packages | 3.10.0-1160.24 | 3.10.0-1160.25 | To increase resiliency, `rsyslog` no longer keeps old file descriptors. Updated worker node images with kernel and package updates for [CVE-2021-25215](https://nvd.nist.gov/vuln/detail/CVE-2021-25215){: external}, [CVE-2020-25692](https://nvd.nist.gov/vuln/detail/CVE-2020-25692){: external}, and [CVE-2020-25648](https://nvd.nist.gov/vuln/detail/CVE-2020-25648){: external}.|
{: caption="Changes since version 4.5.37_1537_openshift" caption-side="bottom"}

### Change log for master fix pack 4.5.37_1536_openshift, released 27 April 2021
{: #4537_1536}

The following table shows the changes that are in the master fix pack patch update `4.5.37_1536_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.9 | v1.2.11 | Fixed {{site.data.keyword.redhat_openshift_notm}} version check for unsupported add-ons. Updated to use `Go` version 1.15.11. Updated image to implement additional IBM security controls and for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external}, [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}, and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| Cluster master operations | N/A | N/A | Resolved a {{site.data.keyword.redhat_openshift_notm}} API server target down alert on clusters that are updated from version 4.4 or earlier. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | v2.0.1 | v2.0.3 | Updated to use `Go` version 1.15.9 and for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.18.17-1 | v1.18.18-1 | Updated to support the Kubernetes 1.18.18 release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 389 | 390 | Updated to use `Go` version 1.15.9 and for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}, and [CVE-2021-3121](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3121){: external}. |
|{{site.data.keyword.cloud_notm}} RBAC Operator | 3dd6bbc | b6a694b | Updated image for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
| Key Management Service provider | v2.2.5 | v2.3.3 | Updated to use `Go` version 1.15.11. Updated image to implement additional IBM security controls and for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external}, [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}, and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.35 | 4.5.37 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-37){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.5.0-20210301 | v4.5.0-20210329 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210329){: external}. |
| OpenVPN client | 2.4.6-r3-IKS-301 | 2.4.6-r3-IKS-386 | Updated image to implement additional IBM security controls. |
| OpenVPN Operator image | v1.2.0 | v1.3.0 | Added OpenVPN support to the {{site.data.keyword.redhat_openshift_notm}} API server to support webhooks. Updated image to implement additional IBM security controls and for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external}, [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}, and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| OpenVPN server | 2.4.6-r3-IKS-301 | 2.4.6-r3-IKS-385 | Updated image to implement additional IBM security controls. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.5.0-20210301 | v4.5.0-20210329 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210329){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.5.0+20210301 | 4.5.0+20210329 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210329){: external}. |
{: caption="Changes since version 4.5.35_1533_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.37_1537_openshift, released 26 April 2021
{: #4537_1537}

The following table shows the changes that are in the worker node fix pack `4.5.37_1537_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | a3b1ff | e0fa2f | The update addresses [CVE-2021-20305](https://nvd.nist.gov/vuln/detail/CVE-2021-20305){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.35 | 4.5.37 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-37){: external}.|
| RHEL 7 Packages | N/A | N/A | Updated worker node images with package updates for [CVE-2021-20305](https://nvd.nist.gov/vuln/detail/CVE-2021-20305){: external}.  |
{: caption="Changes since version 4.5.35_1535_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.35_1535_openshift, released 12 April 2021
{: #4535_1535}

The following table shows the changes that are in the worker node fix pack `4.5.35_1535_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 9b2dca | a3b1ff | The update addresses [CVE-2021-3449](https://nvd.nist.gov/vuln/detail/CVE-2021-3449){: external} and [CVE-2021-3450](https://nvd.nist.gov/vuln/detail/CVE-2021-3450){: external}. |
| RHEL 7 Packages | 3.10.0-1160.21.1.el7 | 3.10.0-1160.24.1.el7 | Updated worker node images with kernel and package updates for [CVE-2021-27363](https://nvd.nist.gov/vuln/detail/CVE-2021-27363){: external}, [CVE-2021-27364](https://nvd.nist.gov/vuln/detail/CVE-2021-27364){: external}, and [CVE-2021-27365](https://nvd.nist.gov/vuln/detail/CVE-2021-27365){: external}. |
{: caption="Changes since version 4.5.35_1534_openshift" caption-side="bottom"}

### Change log for master fix pack 4.5.35_1533_openshift, released 30 March 2021
{: #4535_1533}

The following table shows the changes that are in the master fix pack patch update `4.5.35_1533_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.at_short}} event | N/A | N/A | Now, the `containers-kubernetes.version.update` event is sent to {{site.data.keyword.at_short}} when a master fix pack update is initiated for a cluster. |
| Cluster health image | v1.2.8 | v1.2.9 | Updated image for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}. |
| Gateway-enabled cluster controller | 1232 | 1322 | Updated to use `Go` version 1.15.10 and for [CVE-2021-23839](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-23839){: external}, [CVE-2021-23840](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-23840){: external}, and [CVE-2021-23841](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-23841){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.18.16-2 | v1.18.17-1 | Updated to support the Kubernetes 1.18.17 release. Fixed a bug that prevented VPC load balancers from supporting more than 50 subnets in an account. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 388 | 389 | Updated to use `Go` version 1.15.8. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 86de2b7 | 3dd6bbc | Updated image for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.31 | 4.5.35 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-35){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.5.0-20210112 | v4.5.0-20210301 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210301){: external}. |
| OpenVPN Operator image | v1.1.2 | v1.2.0 | Fixed a bug that could prevent worker node VPN updates. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.5.0-20210112 | v4.5.0-20210301 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210301){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.5.0+20210112 | 4.5.0+20210301 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210301){: external}. |
{: caption="Changes since version 4.5.31_1531_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.35_1534_openshift, released 29 March 2021
{: #4535_1534}

The following table shows the changes that are in the worker node fix pack `4.5.35_1534_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.33 | 4.5.35 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-35){: external}.|
| RHEL 7 Packages | 3.10.0-1160.15.2.el7 | 3.10.0-1160.21.1.el7 | Updated worker node images with kernel and package updates for [CVE-2019-19532](https://nvd.nist.gov/vuln/detail/CVE-2019-19532){: external}, [CVE-2020-0427](https://nvd.nist.gov/vuln/detail/CVE-2020-0427){: external}, [CVE-2020-7053](https://nvd.nist.gov/vuln/detail/CVE-2020-7053){: external}, [CVE-2020-14351](https://nvd.nist.gov/vuln/detail/CVE-2020-14351){: external}, [CVE-2020-25211](https://nvd.nist.gov/vuln/detail/CVE-2020-25211){: external}, [CVE-2020-25645](https://nvd.nist.gov/vuln/detail/CVE-2020-25645){: external}, [CVE-2020-25656](https://nvd.nist.gov/vuln/detail/CVE-2020-25656){: external}, [CVE-2020-25705](https://nvd.nist.gov/vuln/detail/CVE-2020-25705){: external}, [CVE-2020-28374](https://nvd.nist.gov/vuln/detail/CVE-2020-28374){: external}, [CVE-2020-29661](https://nvd.nist.gov/vuln/detail/CVE-2020-29661){: external}, and [CVE-2021-20265](https://nvd.nist.gov/vuln/detail/CVE-2021-20265){: external}. |
{: caption="Changes since version 4.5.33_1532_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.33_1532_openshift, released 12 March 2021
{: #4533_1532}

The following table shows the changes that are in the worker node fix pack `4.5.33_1532_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.31 | 4.5.33 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-33){: external}.|
| RHEL 7 Packages | N/A | N/A | Updated worker node with package updates for [CVE-2020-8625](https://nvd.nist.gov/vuln/detail/CVE-2020-8625){: external}, [CVE-2020-14372](https://nvd.nist.gov/vuln/detail/CVE-2020-14372){: external}, [CVE-2020-25632](https://nvd.nist.gov/vuln/detail/CVE-2020-25632){: external}, [CVE-2020-25647](https://nvd.nist.gov/vuln/detail/CVE-2020-25647){: external}, [CVE-2020-27749](https://nvd.nist.gov/vuln/detail/CVE-2020-27749){: external}, [CVE-2020-27779](https://nvd.nist.gov/vuln/detail/CVE-2020-27779){: external}, [CVE-2021-20225](https://nvd.nist.gov/vuln/detail/CVE-2021-20225){: external}, [CVE-2021-20233](https://nvd.nist.gov/vuln/detail/CVE-2021-20233){: external}, and [CVE-2021-27803](https://nvd.nist.gov/vuln/detail/CVE-2021-27803){: external}. |
{: caption="Changes since version 4.5.31_1531_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.31_1531_openshift, released 1 March 2021
{: #4531_1531}

The following table shows the changes that are in the worker node fix pack `4.5.31_1531_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Image garbage collection | N/A | N/A | Fixed a race condition during the provisioning of worker nodes that might cause image garbage collection to fail.  |
| {{site.data.keyword.registrylong_notm}} private endpoints | N/A | N/A | **VPC worker nodes**: Fixed a bug where traffic to the private endpoints of {{site.data.keyword.registrylong_notm}} might fail after rebooting the worker node. |
| RHEL 7 Packages | N/A | N/A | Updated worker node with package updates. |
{: caption="Changes since version 4.5.31_1529_openshift" caption-side="bottom"}

### Change log for master fix pack 4.5.31_1531_openshift, released 27 February 2021
{: #4531_1531_master}

The following table shows the changes that are in the master fix pack patch update `4.5.31_1531_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1165 | 1274 | Fixed a bug that might cause version 2.0 network load balancers (NLBs) to crash and restart on load balancer updates. |
| OpenVPN Operator image | v1.1.0 | v1.1.2 | Updated image to implement additional IBM security controls. |
{: caption="Changes since version 4.5.31_1530_openshift" caption-side="bottom"}

### Change log for master fix pack 4.5.31_1530_openshift, released 22 February 2021
{: #4531_1530}

The following table shows the changes that are in the master fix pack patch update `4.5.31_1530_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.16.5 | v3.16.6 | See the [Calico release notes](https://docs.tigera.io/archive){: external}. |
| Tigera Operator | v1.10.9 | v1.10.10 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.10.10){: external}. |
| Cluster health image | v1.2.6 | v1.2.8 | Updated to use `Go` version 1.15.7. Updated image to implement additional IBM security controls. |
| Gateway-enabled cluster controller | 1195 | 1232 | Updated to use `Go` version 1.15.7. |
| IBM Calico extension | 567 | 618 | Updated to use `Go` version 1.15.7. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.18.15-3 | v1.18.16-1 | Updated to support the Kubernetes 1.18.16 release and to use `calicoctl` version 3.13.5. Updated image to implement additional IBM security controls and for [DLA-2509-1](https://lists.debian.org/debian-lts-announce/2020/12/msg00039.html){: external}. Updated version 1.0 and 2.0 network load balancers (NLBs) to run as a non-root user by default, with privileged escalation as needed. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 385 | 388 | Improved the retry logic for provisioning persistent volume claims (PVCs). |
| {{site.data.keyword.cloud_notm}} RBAC Operator | f859228 | 86de2b7 | Updated to use `Go` version 1.15.7. |
| Key Management Service provider | v2.2.3 | v2.2.5 | Updated to use `Go` version 1.15.7. Updated image to implement additional IBM security controls. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1078 | 1165 | Updated to run as a non-root user by default, with privileged escalation as needed. Updated to use `Go` version 1.15.7. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.24 | 4.5.31 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-31){: external}. |
{: caption="Changes since version 4.5.24_1527_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.31_1529_openshift, released 15 February 2021
{: #4531_1529}

The following table shows the changes that are in the worker node fix pack `4.5.31_1529_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.28 | 4.5.31 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-31){: external}. |
| RHEL 7 Packages | 3.10.0-1160.11.1.el7 | 3.10.0-1160.15.2.el7 | Updated worker node with image kernel and package updates for: [CVE-2020-10543](https://nvd.nist.gov/vuln/detail/CVE-2020-10543){: external}, [CVE-2020-10878](https://nvd.nist.gov/vuln/detail/CVE-2020-10878){: external}, [CVE-2020-12723](https://nvd.nist.gov/vuln/detail/CVE-2020-12723){: external}, [CVE-2020-15436](https://nvd.nist.gov/vuln/detail/CVE-2020-15436){: external}, [CVE-2020-35513](https://nvd.nist.gov/vuln/detail/CVE-2020-35513){: external}, [CVE-2019-25013](https://nvd.nist.gov/vuln/detail/CVE-2019-25013){: external}, [CVE-2020-10029](https://nvd.nist.gov/vuln/detail/CVE-2020-10029){: external}, [CVE-2020-29573](https://nvd.nist.gov/vuln/detail/CVE-2020-29573){: external}, and [CVE-2020-12321](https://nvd.nist.gov/vuln/detail/CVE-2020-12321){: external}){: external}. |
{: caption="Changes since version 4.5.28_1528_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.28_1528_openshift, released 1 February 2021
{: #4528_1528}

The following table shows the changes that are in the worker node fix pack `4.5.28_1528_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.24 | 4.5.28 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-28){: external}. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates for [CVE-2021-3156](https://nvd.nist.gov/vuln/detail/CVE-2021-3156){: external}, [CVE-2020-25684](https://nvd.nist.gov/vuln/detail/CVE-2020-25684){: external}, [CVE-2020-25685](https://nvd.nist.gov/vuln/detail/CVE-2020-25685){: external}, and [CVE-2020-25686](https://nvd.nist.gov/vuln/detail/CVE-2020-25686){: external}. |
{: caption="Changes since version 4.5.24_1526_openshift" caption-side="bottom"}

### Change log for master fix pack 4.5.24_1527_openshift, released 19 January 2021
{: #4524_1527}

The following table shows the changes that are in the master fix pack patch update `4.5.24_1527_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.4 | v1.2.6 | Updated image to implement additional IBM security controls. |
| Gateway-enabled cluster controller | 1184 | 1195 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external}. |
| IBM Calico extension | 556 | 567 | Updated image to implement additional IBM security controls and for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external} and [CVE-2020-24659](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24659){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.0.0 | v2.0.1 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external} and [CVE-2020-24659](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24659){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.18.14-1 | v1.18.15-3 | Updated to support the Kubernetes 1.18.15 release and to implement additional IBM security controls. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 384 | 385 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external} and [CVE-2020-24659](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24659){: external}. |
| Key Management Service provider | v2.2.2 | v2.2.3 | Fixed bug to ignore conflict errors during KMS secret re-encryption. Updated to use `Go` version 1.15.5. Updated image to implement additional IBM security controls and for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1004 | 1078 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | N/A | N/A | Updated to implement additional IBM security controls. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.5.0-20201210 | v4.5.0-20210112 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210112){: external}. Updated to implement additional IBM security controls. |
| OpenVPN Operator image | v1.0.12 | v1.1.0 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.5.0-20201210 | v4.5.0-20210112 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210112){: external}. Updated to implement additional IBM security controls. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.5.0+20201210 | 4.5.0+20210112 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20210112){: external}. |
{: caption="Changes since version 4.5.24_1525_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.24_1526_openshift, released 18 January 2021
{: #4524_1526}

The following table shows the changes that are in the worker node fix pack `4.5.24_1526_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.22 | 4.5.24 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-24){: external}. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates. |
{: caption="Changes since version 4.5.22_1524_openshift" caption-side="bottom"}

### Change log for master fix pack 4.5.24_1525_openshift, released 6 January 2021
{: #4524_1525}

The following table shows the changes that are in the master fix pack patch update `4.5.24_1525_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| IBM Calico extension | 538 | 556 | Updated image to include the `ip` command. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | 1.17.2 | v2.0.0 | Updated to use the universal base image (UBI), to use `Go` version 1.15.5, to run with a least privileged security context, and to improve logging. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.18.13-1 | v1.18.14-1 | Updated to support the Kubernetes 1.18.14 release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in | N/A | N/A | Updated to run with a privileged security context. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | c148a8a | f859228 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external} and [CVE-2020-24659](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24659){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.5.0-20201207 | v4.5.0-20201210 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201210){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.18 | 4.5.24 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-24){: external}. The update resolves CVE-2020-8559 (see the [IBM security bulletin](https://www.ibm.com/support/pages/node/6404296){: external}). |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.5.0-20201207 | v4.5.0-20201210 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201210){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.5.0+20201207 | 4.5.0+20201210 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201210){: external}. |
{: caption="Changes since version 4.5.18_1523_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.22_1524_openshift, released 21 December 2020
{: #4522_1524}

The following table shows the changes that are in the worker node fix pack update `4.5.21_1524_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HAProxy | db4e6d | 9b2dca | Image update for [CVE-2020-1971](https://nvd.nist.gov/vuln/detail/CVE-2020-1971){: external} and [CVE-2020-24659](https://nvd.nist.gov/vuln/detail/CVE-2020-24659){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.21 | 4.5.22 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-22){: external}. |
| RHEL 7 Packages | 3.10.0-1160.6.1.el7 | 3.10.0-1160.11.1.el7 | Updated worker node image with kernel and package updates for: [CVE-2019-18282](https://nvd.nist.gov/vuln/detail/CVE-2019-18282){: external}, [CVE-2020-10769](https://nvd.nist.gov/vuln/detail/CVE-2020-10769){: external}, [CVE-2020-14314](https://nvd.nist.gov/vuln/detail/CVE-2020-14314){: external}, [CVE-2020-14385](https://nvd.nist.gov/vuln/detail/CVE-2020-14385){: external}, [CVE-2020-24394](https://nvd.nist.gov/vuln/detail/CVE-2020-24394){: external}, [CVE-2020-25212](https://nvd.nist.gov/vuln/detail/CVE-2020-25212){: external}, [CVE-2020-25643](https://nvd.nist.gov/vuln/detail/CVE-2020-25643){: external}, and [CVE-2020-1971](https://nvd.nist.gov/vuln/detail/CVE-2020-1971){: external}. |
{: caption="Changes since version 4.5.18_1523_openshift" caption-side="bottom"}

### Change log for master fix pack 4.5.18_1523_openshift, released 14 December 2020
{: #4518_1523}

The following table shows the changes that are in the master fix pack patch update `4.5.18_1523_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.2.3 | v1.2.4 | Updated image to implement additional IBM security controls. |
| etcd | v3.4.13 | v3.4.14 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.14){: external}. |
| Gateway-enabled cluster controller | 1105 | 1184 | Updated to use `Go` version 1.15.5. Updated image to implement additional IBM security controls. |
| IBM Calico extension | 469 | 538 | Updated to use the universal base image (UBI), to run as a non-root user and to use `Go` version 1.15.5. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.18.12-1 | v1.18.13-1 | Updated to support the Kubernetes 1.18.13 release. Updated image to implement additional IBM security controls. Fixed a bug in VPC load balancer creation when the cluster, VPC or subnet are in a different resource group. |
| {{site.data.keyword.filestorage_full_notm}} monitor | 379 | 384 | Updated to use `Go` version 1.15.5 and to run as a non-root user. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.filestorage_full_notm}} plug-in | 379 | 384 | Updated to use `Go` version 1.15.5 and to run with a least privileged security context. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 197bc70 | c148a8a | Updated to use `Go` version 1.15.6 and updated image to implement additional IBM security controls. |
| Key management service (KMS) provider | v2.2.1 | v2.2.2 | Updated image to implement additional IBM security controls. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 234 | 1004 | Updated Alpine base image to version 3.12 and to use `Go` version 1.15.5. Updated image for [CVE-2020-8037](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8037){: external} and [CVE-2020-28928](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28928){: external}. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.5.0-20201113 | v4.5.0-20201207 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201207){: external}. |
| OpenVPN client | 2.4.6-r3-IKS-116 | 2.4.6-r3-IKS-301 | Updated image to implement additional IBM security controls. |
| OpenVPN Operator image | v1.0.10 | v1.0.12 | Updated image to implement additional IBM security controls. |
| OpenVPN server | 2.4.6-r3-IKS-131 | 2.4.6-r3-IKS-301 | Updated image to implement additional IBM security controls. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.5.0-20201113 | v4.5.0-20201207 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201207){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.5.0+20201113 | 4.5.0+20201207 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201207){: external}. |
{: caption="Changes since version 4.5.18_1521_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.21_1522_openshift, released 7 December 2020
{: #4521_1522}

The following table shows the changes that are in the worker node fix pack update `4.5.21_1522_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HAProxy | 1.8.26-384f42 | db4e6d | Added provenance labels for source tracking. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.19 | 4.5.21 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-5-21){: external}. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates.|
{: caption="Changes since version 4.5.19_1521_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.19_1521_openshift, released 23 November 2020
{: #4519_1521}

The following table shows the changes that are in the worker node fix pack update `4.5.19_1521_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Ephemeral storage reservations | N/A | N/A | Local ephemeral storage is reserved on the Kubernetes data disk for system components. |
| {{site.data.keyword.redhat_openshift_notm}} node | 4.5.17 | 4.5.19 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-19){: external}. |
| RHEL 7 Packages |  3.10.0-1160.2.2.el7 | 3.10.0-1160.6.1.el7 | Updated worker node image with kernel and package updates for [CVE-2020-8622](https://nvd.nist.gov/vuln/detail/CVE-2020-8622){: external}, [CVE-2020-8623](https://nvd.nist.gov/vuln/detail/CVE-2020-8623){: external}, [CVE-2020-8624](https://nvd.nist.gov/vuln/detail/CVE-2020-8624){: external}, [CVE-2019-20907](https://nvd.nist.gov/vuln/detail/CVE-2019-20907){: external}, [CVE-2020-15999](https://nvd.nist.gov/vuln/detail/CVE-2020-15999){: external}, [CVE-2020-8177](https://nvd.nist.gov/vuln/detail/CVE-2020-8177){: external}, [CVE-2019-20811](https://nvd.nist.gov/vuln/detail/CVE-2019-20811){: external}, [CVE-2020-14331](https://nvd.nist.gov/vuln/detail/CVE-2020-14331){: external}, [CVE-2020-8695](https://nvd.nist.gov/vuln/detail/CVE-2020-8695){: external}, [CVE-2020-8696](https://nvd.nist.gov/vuln/detail/CVE-2020-8696){: external}, and [CVE-2020-8698](https://nvd.nist.gov/vuln/detail/CVE-2020-8698){: external}.|
{: caption="Changes since version 4.5.17_1519_openshift" caption-side="bottom"}

### Change log for master fix pack 4.5.18_1521_openshift, released 16 November 2020
{: #4518_1521}

The following table shows the changes that are in the master fix pack patch update `4.5.18_1521_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Calico | v3.16.1 | v3.16.5 | See the [Calico release notes](https://docs.tigera.io/archive){: external}. |
| Tigera Operator | v1.10.3 | v1.10.9 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.10.9){: external}. In addition, Tigera Operator metrics are disabled. |
| Cluster health image | v1.2.2 | v1.2.3 | Added status codes to add-on health messages. Set add-on health state to `critical` and status to `unknown` when cluster health is `critical`. When a cluster has a Kubernetes key management service (KMS) provider enabled and a disabled [Key Protect](/docs/openshift?topic=openshift-encryption) key, the cluster health state is now set to `critical`. Updated image for [DLA-2424-1](https://lists.debian.org/debian-lts-announce/2020/10/msg00037.html){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.18.10-1 | v1.18.12-1 | Updated to support the Kubernetes 1.18.12 release. Updated image for [DLA-2424-1](https://lists.debian.org/debian-lts-announce/2020/10/msg00037.html){: external}. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 31c794a | 197bc70 | Updated image for [CVE-2019-20454](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20454){: external}, [CVE-2020-10029](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-10029){: external}, [CVE-2020-1751](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1751){: external}, [CVE-2020-1752](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1752){: external}, [CVE-2019-20807](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20807){: external}, [CVE-2019-16935](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16935){: external}, [CVE-2019-20907](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20907){: external}, [CVE-2020-14422](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14422){: external}, [CVE-2020-8492](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8492){: external}, [CVE-2019-15165](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-15165){: external}, [CVE-2019-16168](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16168){: external}, [CVE-2019-20218](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20218){: external}, [CVE-2019-5018](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-5018){: external}, [CVE-2020-13630](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13630){: external}, [CVE-2020-13631](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13631){: external}, [CVE-2020-13632](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13632){: external}, [CVE-2020-6405](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-6405){: external}, [CVE-2020-9327](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9327){: external}, [CVE-2020-8177](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8177){: external}, [CVE-2019-13050](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13050){: external}, [CVE-2018-20843](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-20843){: external}, [CVE-2019-15903](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-15903){: external}, [CVE-2019-14889](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14889){: external}, [CVE-2020-1730](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1730){: external}, [CVE-2019-1551](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1551){: external}, [CVE-2020-14382](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14382){: external}, [CVE-2019-13627](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13627){: external}, [CVE-2019-19956](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19956){: external}, [CVE-2019-20388](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20388){: external}, [CVE-2020-7595](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-7595){: external}, [CVE-2019-20386](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20386){: external}, [CVE-2019-19906](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19906){: external}, [CVE-2019-20387](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20387){: external}, and [CVE-2019-19221](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19221){: external}. |
| Key Management Service provider | v2.1.0 | v2.2.1 | Updated to support service-to-service authentication and to use `Go` version 1.15.2. Updated image for [DLA-2424-1](https://lists.debian.org/debian-lts-announce/2020/10/msg00037.html){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.5.0-20201022 | v4.5.0-20201113 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201113){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.15 | 4.5.18 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-18){: external}. |
| OpenVPN Operator image | v1.0.9 | v1.0.10 | Updated image for [CVE-2019-20454](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20454){: external}, [CVE-2020-10029](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-10029){: external}, [CVE-2020-1751](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1751){: external}, [CVE-2020-1752](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1752){: external}, [CVE-2019-20807](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20807){: external}, [CVE-2019-16935](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16935){: external}, [CVE-2019-20907](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20907){: external}, [CVE-2020-14422](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14422){: external}, [CVE-2020-8492](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8492){: external}, [CVE-2019-15165](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-15165){: external}, [CVE-2019-16168](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16168){: external}, [CVE-2019-20218](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20218){: external}, [CVE-2019-5018](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-5018){: external}, [CVE-2020-13630](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13630){: external}, [CVE-2020-13631](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13631){: external}, [CVE-2020-13632](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13632){: external}, [CVE-2020-6405](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-6405){: external}, [CVE-2020-9327](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9327){: external}, [CVE-2020-8177](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8177){: external}, [CVE-2019-13050](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13050){: external}, [CVE-2018-20843](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-20843){: external}, [CVE-2019-15903](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-15903){: external}, [CVE-2019-14889](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14889){: external}, [CVE-2020-1730](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1730){: external}, [CVE-2019-1551](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1551){: external}, [CVE-2020-14382](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14382){: external}, [CVE-2019-13627](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13627){: external}, [CVE-2019-19956](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19956){: external}, [CVE-2019-20388](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20388){: external}, [CVE-2020-7595](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-7595){: external}, [CVE-2019-20386](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20386){: external}, [CVE-2019-19906](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19906){: external}, [CVE-2019-20387](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20387){: external}, and [CVE-2019-19221](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19221){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Server | v4.5.0-20201022 | v4.5.0-20201113 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201113){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.5.0+20201022 | 4.5.0+20201113 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201113){: external}. |
{: caption="Changes since version 4.5.15_1518_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.17_1519_openshift, released 9 November 2020
{: #4517_1519}

The following table shows the changes that are in the worker node fix pack update `4.5.17_1519_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.15 | 4.5.17 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-17){: external}.|
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates for [CVE-2020-15999](https://nvd.nist.gov/vuln/detail/CVE-2020-15999){: external}.|
{: caption="Changes since version 4.5.15_1518_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.5.15_1518_openshift, released 26 October 2020
{: #4515_1518_worker}

The following table shows the changes that are in the worker node fix pack update `4.5.15_1518_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.13 | 4.5.15 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-15){: external}.|
| RHEL 7 Packages | 3.10.0-1160.2.1.el7 | 3.10.0-1160.2.2.el7 | Updated worker node images with kernel and package updates for [CVE-2020-12351](https://nvd.nist.gov/vuln/detail/CVE-2020-12351){: external} and [CVE-2020-12352](https://nvd.nist.gov/vuln/detail/CVE-2020-12352){: external}.|
{: caption="Changes since version 4.5.13_1515_openshift" caption-side="bottom"}

### Change log for master fix pack 4.5.15_1518_openshift, released 26 October 2020
{: #4515_1518}

The following table shows the changes that are in the master fix pack patch update `4.5.15_1518_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster health image | v1.2.1 | v1.2.2 | Fixed the cluster health status for when add-on customizations are used. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.18.9-2 | v1.18.10-1 | Updated to support the Kubernetes 1.18.10 release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 378 | 379 | Updated to use the universal base image (UBI) and to use `Go` version 1.15.2. |
| Kubernetes configuration | N/A | N/A | [Kubernetes service account token volume projection](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#service-account-token-volume-projection){: external} is enabled and issues tokens that use `https://kubernetes.default.svc` as the default API audience. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.5.13 | 4.5.15 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-15){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.5.0-20201009 | v4.5.0-20201022 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201022){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.5.0-20201009 | v4.5.0-20201022 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201022){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.5.0+20201009 | 4.5.0+20201022 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201022){: external}. |
{: caption="Changes since version 4.5.13_1515_openshift" caption-side="bottom"}

### Change log for 4.5.13_1515_openshift, released 13 October 2020
{: #4513_1515}

The following table shows the changes that are in the `4.5.13_1515_openshift` version update.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.13.3 | v3.16.1 | See the [Calico release notes](https://docs.tigera.io/archive){: external}. In addition, Calico pods in the `calico-system` namespace now set CPU and memory requests. |
| Tigera Operator | v1.3.4 | v1.10.3 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.10.3){: external}. |
| Cluster health image | v1.1.11 | v1.2.1 | When a cluster has a Kubernetes key management service (KMS) provider enabled and a disabled [{{site.data.keyword.keymanagementserviceshort}}](/docs/openshift?topic=openshift-encryption) key, a warning is now returned in the cluster health state. Fixed check to determine if an add-on is unsupported. In addition, updated to use `Go` version 1.15.2. |
| Cluster master HA configuration | N/A | N/A | Updated configuration to improve availability during cluster master operations. |
| Gateway-enabled cluster controller | 1082 | 1105 | Updated to use `Go` version 1.15.2. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | 1.17.1 | 1.17.2 | Updated to use `Go` version 1.13.15. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.12-1 | v1.18.9-2 | Updated to support the Kubernetes 1.18.9 release and to use `calicoctl` version 3.13.4. Updated network load balancer (NLB) events to use the latest {{site.data.keyword.cloud_notm}} troubleshooting documentation. For VPC load balancers, the `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "proxy-protocol"` annotation was added to preserve the source IP address of requests to apps in your cluster. |
|{{site.data.keyword.cloud_notm}} RBAC Operator | 4b47693 | 31c794a | Updated to use `Go` version 1.15.2. |
| Key Management Service provider | v2.0.4 | v2.1.0 | Updated to use the key management service (KMS) provider secret to identify when a [{{site.data.keyword.keymanagementserviceshort}}](/docs/openshift?topic=openshift-encryption) key is enabled and disabled so that encryption and decryption requests are updated accordingly. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 208 | 234 | Improved startup performance of version 2.0 private network load balancers (NLBs). Updated to use `Go` version 1.15.2. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.4.0-20200821 | v4.5.0-20201009 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201009){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.4.20 | 4.5.13 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-13){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} configuration | N/A | N/A | New version 4.5 clusters that run on the VPC infrastructure provider and use {{site.data.keyword.cos_full_notm}} now proxy container image traffic through the internal registry pods directly to the {{site.data.keyword.cos_short}} endpoints. To configure this proxy for version 4.5 clusters that were updated from a previous version, see [the troubleshooting topic](/docs/openshift?topic=openshift-ts-app-ocr-vpc-push). |
| OpenVPN Operator image | v1.0.8 | v1.0.9 | Updated to improve OpenVPN availability. |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | N/A | v4.5.0-20201009 | **New!**: {{site.data.keyword.openshiftlong_notm}} now provides custom cluster metrics. See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201009){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.4.0+20200821 | 4.5.0+20201009 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.5.0+20201009){: external}. |
{: caption="Changes since version 4.4.20_1518_openshift" caption-side="bottom"}

## Version 4.4 change log (unsupported as of 31 May 2021)
{: #version-44}

Version 4.4 is unsupported. You can review the following archive of the 4.4 change logs.
{: shortdesc}

### Change log for worker node fix pack 4.4.33_1544_openshift, released 24 May 2021
{: #4433_1544}

The following table shows the changes that are in the worker node fix pack `4.4.33_1544_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | e0fa2f | 26c5cc | Updated image with fixes for [CVE-2020-26116](https://nvd.nist.gov/vuln/detail/CVE-2020-26116){: external}, [CVE-2020-27619](https://nvd.nist.gov/vuln/detail/CVE-2020-27619){: external}, [CVE-2021-23336](https://nvd.nist.gov/vuln/detail/CVE-2021-23336){: external}, [CVE-2021-3177](https://nvd.nist.gov/vuln/detail/CVE-2021-3177){: external}, [CVE-2019-3842](https://nvd.nist.gov/vuln/detail/CVE-2019-3842){: external}, [CVE-2020-13776](https://nvd.nist.gov/vuln/detail/CVE-2020-13776){: external}, [CVE-2019-18276](https://nvd.nist.gov/vuln/detail/CVE-2019-18276){: external}, [CVE-2020-24977](https://nvd.nist.gov/vuln/detail/CVE-2020-24977){: external}, [CVE-2020-13434](https://nvd.nist.gov/vuln/detail/CVE-2020-13434){: external}, [CVE-2020-15358](https://nvd.nist.gov/vuln/detail/CVE-2020-15358){: external}, [CVE-2019-13012](https://nvd.nist.gov/vuln/detail/CVE-2019-13012){: external}, [CVE-2020-13543](https://nvd.nist.gov/vuln/detail/CVE-2020-13543){: external}, [CVE-2020-13584](https://nvd.nist.gov/vuln/detail/CVE-2020-13584){: external}, [CVE-2020-9948](https://nvd.nist.gov/vuln/detail/CVE-2020-9948){: external}, [CVE-2020-9951](https://nvd.nist.gov/vuln/detail/CVE-2020-9951){: external}, [CVE-2020-9983](https://nvd.nist.gov/vuln/detail/CVE-2020-9983){: external}, [CVE-2020-8231](https://nvd.nist.gov/vuln/detail/CVE-2020-8231){: external}, [CVE-2020-8284](https://nvd.nist.gov/vuln/detail/CVE-2020-8284){: external}, [CVE-2020-8285](https://nvd.nist.gov/vuln/detail/CVE-2020-8285){: external}, [CVE-2020-8286](https://nvd.nist.gov/vuln/detail/CVE-2020-8286){: external}, [CVE-2020-24330](https://nvd.nist.gov/vuln/detail/CVE-2020-24330){: external}, [CVE-2020-24331](https://nvd.nist.gov/vuln/detail/CVE-2020-24331){: external}, [CVE-2020-24332](https://nvd.nist.gov/vuln/detail/CVE-2020-24332){: external}, [CVE-2020-29361](https://nvd.nist.gov/vuln/detail/CVE-2020-29361){: external}, [CVE-2020-29362](https://nvd.nist.gov/vuln/detail/CVE-2020-29362){: external}, [CVE-2020-29363](https://nvd.nist.gov/vuln/detail/CVE-2020-29363){: external}, [CVE-2020-28196](https://nvd.nist.gov/vuln/detail/CVE-2020-28196){: external}, [CVE-2019-2708](https://nvd.nist.gov/vuln/detail/CVE-2019-2708){: external}, [CVE-2016-10228](https://nvd.nist.gov/vuln/detail/CVE-2016-10228){: external}, [CVE-2019-25013](https://nvd.nist.gov/vuln/detail/CVE-2019-25013){: external}, [CVE-2019-9169](https://nvd.nist.gov/vuln/detail/CVE-2019-9169){: external}, [CVE-2020-27618](https://nvd.nist.gov/vuln/detail/CVE-2020-27618){: external}, [CVE-2021-3326](https://nvd.nist.gov/vuln/detail/CVE-2021-3326){: external}, and [CVE-2020-8927](https://nvd.nist.gov/vuln/detail/CVE-2020-8927){: external}. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates.|
{: caption="Changes since version 4.4.33_1541_openshift" caption-side="bottom"}

### Change log for master fix pack 4.4.33_1543_openshift, released 24 May 2021
{: #4433_1543}

The following table shows the changes that are in the master fix pack patch update `4.4.33_1543_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.21 | v1.1.22 | Updated image to implement additional IBM security controls and for [CVE-2020-26160](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-26160){: external}, [CVE-2020-28483](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28483){: external} and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| Gateway-enabled cluster controller | 1322 | 1352 | Updated to use `Go` version 1.15.11. Updated image to implement additional IBM security controls and for [CVE-2021-28831](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-28831){: external}, [CVE-2021-30139](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-30139){: external}, [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
| IBM Calico extension | 618 | 689 | Updated to use `Go` version 1.15.12. Updated image to implement additional IBM security controls and for [CVE-2020-14391](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14391){: external}, [CVE-2020-25661](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-25661){: external} and [CVE-2020-25662](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-25662){: external}. |
| {{site.data.keyword.blockstoragefull}} driver and plug-in | v2.0.3 | v2.0.4 | Updated image for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 390 | 392 | Improved the prerequisite validation logic for provisioning persistent volume claims (PVCs). Updated image to implement additional IBM security controls and for [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| IBM Cloud RBAC Operator | b6a694b | 63cd064 | Updated image to implement additional IBM security controls and for [CVE-2020-28483](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28483){: external}. |
| Key Management Service provider | v2.3.3 | v2.3.4 | Updated image to implement additional IBM security controls and for [CVE-2020-28483](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28483){: external} and [CVE-2020-26160](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-26160){: external}. |
| Load balancer and load balancer monitor for IBM Cloud Provider | 1274 | 1328 | Updated to use Go version 1.15.11. Updated image to implement additional IBM security controls and for [CVE-2021-28831](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-28831){: external}, [CVE-2021-30139](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-30139){: external}, [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
| OpenVPN Operator image | v1.3.0 | v1.3.1 | Updated image for [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
{: caption="Changes since version 4.4.33_1539_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.4.33_1541_openshift, released 10 May 2021
{: #4433_1541}

The following table shows the changes that are in the worker node fix pack `4.4.33_1541_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | 3.10.0-1160.24 | 3.10.0-1160.25 | To increase resiliency, `rsyslog` no longer keeps old file descriptors. Updated worker node images with kernel and package updates for [CVE-2021-25215](https://nvd.nist.gov/vuln/detail/CVE-2021-25215){: external}, [CVE-2020-25692](https://nvd.nist.gov/vuln/detail/CVE-2020-25692){: external}, and [CVE-2020-25648](https://nvd.nist.gov/vuln/detail/CVE-2020-25648){: external}.|
{: caption="Changes since version 4.4.33_1540_openshift" caption-side="bottom"}

### Change log for master fix pack 4.4.33_1539_openshift, released 27 April 2021
{: #4433_1539}

The following table shows the changes that are in the master fix pack patch update `4.4.33_1539_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.19 | v1.1.21 | Updated to use `Go` version 1.15.11. Updated image to implement additional IBM security controls and for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external}, [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}, and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| IBM Cloud Block Storage driver and plug-in | v2.0.1 | v2.0.3 | Updated to use `Go` version 1.15.9 and for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 389 | 390 | Updated to use `Go` version 1.15.9 and for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external} and [CVE-2021-3121](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3121){: external}. |
|{{site.data.keyword.cloud_notm}} RBAC Operator | 3dd6bbc | b6a694b | Updated image for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}. |
| Key Management Service provider | v2.2.5 | v2.3.3 | Updated to use `Go` version 1.15.11. Updated image to implement additional IBM security controls and for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external}, [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}, and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| OpenVPN client | 2.4.6-r3-IKS-301 | 2.4.6-r3-IKS-386 | Updated image to implement additional IBM security controls. |
| OpenVPN Operator image | v1.2.0 | v1.3.0 | Added OpenVPN support to the {{site.data.keyword.redhat_openshift_notm}} API server to support webhooks. Updated image to implement additional IBM security controls and for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3449){: external}, [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3450){: external}, and [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}. |
| OpenVPN server | 2.4.6-r3-IKS-301 | 2.4.6-r3-IKS-385 | Updated image to implement additional IBM security controls. |
{: caption="Changes since version 4.4.33_1536_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.4.33_1540_openshift, released 26 April 2021
{: #4433_1540}

The following table shows the changes that are in the worker node fix pack `4.4.33_1540_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | a3b1ff | e0fa2f | The update addresses [CVE-2021-20305](https://nvd.nist.gov/vuln/detail/CVE-2021-20305){: external}. |
| RHEL 7 Packages | N/A | N/A | Updated worker node images with package updates for [CVE-2021-20305](https://nvd.nist.gov/vuln/detail/CVE-2021-20305){: external}.  |
{: caption="Changes since version 4.4.33_1538_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.4.33_1538_openshift, released 12 April 2021
{: #4433_1538}

The following table shows the changes that are in the worker node fix pack `4.4.33_1538_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| HA proxy | 9b2dca | a3b1ff | The update addresses [CVE-2021-3449](https://nvd.nist.gov/vuln/detail/CVE-2021-3449){: external} and [CVE-2021-3450](https://nvd.nist.gov/vuln/detail/CVE-2021-3450){: external}. |
| RHEL 7 Packages | 3.10.0-1160.21.1.el7 | 3.10.0-1160.24.1.el7 | Updated worker node images with kernel and package updates for [CVE-2021-27363](https://nvd.nist.gov/vuln/detail/CVE-2021-27363){: external}, [CVE-2021-27364](https://nvd.nist.gov/vuln/detail/CVE-2021-27364){: external}, and [CVE-2021-27365](https://nvd.nist.gov/vuln/detail/CVE-2021-27365){: external}. |
{: caption="Changes since version 4.4.33_1537_openshift" caption-side="bottom"}

### Change log for master fix pack 4.4.33_1536_openshift, released 30 March 2021
{: #4433_1536}

The following table shows the changes that are in the master fix pack patch update `4.4.33_1536_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.at_short}} event | N/A | N/A | Now, the `containers-kubernetes.version.update` event is sent to {{site.data.keyword.at_short}} when a master fix pack update is initiated for a cluster. |
| Cluster health image | v1.1.18 | v1.1.19 | Updated image for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}. |
| Gateway-enabled cluster controller | 1232 | 1322 | Updated to use `Go` version 1.15.10 and for [CVE-2021-23839](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-23839){: external}, [CVE-2021-23840](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-23840){: external}, and [CVE-2021-23841](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-23841){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 388 | 389 | Updated to use `Go` version 1.15.8. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 86de2b7 | 3dd6bbc | Updated image for [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1165 | 1274 | Fixed a bug that might cause version 2.0 network load balancers (NLBs) to crash and restart on load balancer updates. |
| OpenVPN Operator image | v1.1.0 | v1.2.0 | Fixed a bug that could prevent worker node VPN updates. |
{: caption="Changes since version 4.4.33_1534_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.4.33_1537_openshift, released 29 March 2021
{: #4433_1537}

The following table shows the changes that are in the worker node fix pack `4.4.33_1537_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | 3.10.0-1160.15.2.el7 | 3.10.0-1160.21.1.el7 | Updated worker node images with kernel and package updates for [CVE-2019-19532](https://nvd.nist.gov/vuln/detail/CVE-2019-19532){: external}, [CVE-2020-0427](https://nvd.nist.gov/vuln/detail/CVE-2020-0427){: external}, [CVE-2020-7053](https://nvd.nist.gov/vuln/detail/CVE-2020-7053){: external}, [CVE-2020-14351](https://nvd.nist.gov/vuln/detail/CVE-2020-14351){: external}, [CVE-2020-25211](https://nvd.nist.gov/vuln/detail/CVE-2020-25211){: external}, [CVE-2020-25645](https://nvd.nist.gov/vuln/detail/CVE-2020-25645){: external}, [CVE-2020-25656](https://nvd.nist.gov/vuln/detail/CVE-2020-25656){: external}, [CVE-2020-25705](https://nvd.nist.gov/vuln/detail/CVE-2020-25705){: external}, [CVE-2020-28374](https://nvd.nist.gov/vuln/detail/CVE-2020-28374){: external}, [CVE-2020-29661](https://nvd.nist.gov/vuln/detail/CVE-2020-29661){: external}, and [CVE-2021-20265](https://nvd.nist.gov/vuln/detail/CVE-2021-20265){: external}. |
{: caption="Changes since version 4.4.33_1535_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.4.33_1535_openshift, released 12 March 2021
{: #4433_1535}

The following table shows the changes that are in the worker node fix pack `4.4.33_1535_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | Updated worker node with package updates for [CVE-2020-8625](https://nvd.nist.gov/vuln/detail/CVE-2020-8625){: external}, [CVE-2020-14372](https://nvd.nist.gov/vuln/detail/CVE-2020-14372){: external}, [CVE-2020-25632](https://nvd.nist.gov/vuln/detail/CVE-2020-25632){: external}, [CVE-2020-25647](https://nvd.nist.gov/vuln/detail/CVE-2020-25647){: external}, [CVE-2020-27749](https://nvd.nist.gov/vuln/detail/CVE-2020-27749){: external}, [CVE-2020-27779](https://nvd.nist.gov/vuln/detail/CVE-2020-27779){: external}, [CVE-2021-20225](https://nvd.nist.gov/vuln/detail/CVE-2021-20225){: external}, [CVE-2021-20233](https://nvd.nist.gov/vuln/detail/CVE-2021-20233){: external}, and [CVE-2021-27803](https://nvd.nist.gov/vuln/detail/CVE-2021-27803){: external}. |
{: caption="Changes since version 4.4.33_1534_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.4.33_1534_openshift, released 1 March 2021
{: #4433_1534_worker}

The following table shows the changes that are in the worker node fix pack `4.4.33_1534_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Image garbage collection | N/A | N/A | Fixed a race condition during the provisioning of worker nodes that might cause image garbage collection to fail.  |
| {{site.data.keyword.registrylong_notm}} private endpoints | N/A | N/A | **VPC worker nodes**: Fixed a bug where traffic to the private endpoints of {{site.data.keyword.registrylong_notm}} might fail after rebooting the worker node. |
| RHEL 7 Packages | N/A | N/A | Updated worker node with package updates. |
{: caption="Changes since version 4.4.33_1533_openshift" caption-side="bottom"}

### Change log for master fix pack 4.4.33_1534_openshift, released 22 February 2021
{: #4433_1534}

The following table shows the changes that are in the master fix pack patch update `4.4.33_1534_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.13.3 | v3.13.5 | See the [Calico release notes](https://docs.tigera.io/archive){: external}. |
| Tigera Operator | v1.3.4 | v1.3.6 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.3.6){: external}. |
| Cluster health image | v1.1.16 | v1.1.18 | Updated to use `Go` version 1.15.7. Updated image to implement additional IBM security controls. |
| Gateway-enabled cluster controller | 1195 | 1232 | Updated to use `Go` version 1.15.7. |
| IBM Calico extension | 567 | 618 | Updated to use `Go` version 1.15.7. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.17-1 | v1.17.17-5 | Updated image for for [DLA-2509-1](https://lists.debian.org/debian-lts-announce/2020/12/msg00039.html){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 385 | 388 | Improved the retry logic for provisioning persistent volume claims (PVCs). |
| {{site.data.keyword.cloud_notm}} RBAC Operator | f859228 | 86de2b7 | Updated to use `Go` version 1.15.7. |
| Key Management Service provider | v2.2.3 | v2.2.5 | Updated to use `Go` version 1.15.7. Updated image to implement additional IBM security controls. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1078 | 1165 | Updated to use `Go` version 1.15.7. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.4.31 | 4.4.33 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-33){: external}. |
{: caption="Changes since version 4.4.31_1531_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.4.33_1533_openshift, released 15 February 2021
{: #4433_1533}

The following table shows the changes that are in the worker node fix pack `4.4.33_1533_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.4.31 | 4.4.33 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-33){: external}. |
| RHEL 7 Packages | 3.10.0-1160.11.1.el7 | 3.10.0-1160.15.2.el7 | Updated worker node with image kernel and package updates for: [CVE-2020-10543](https://nvd.nist.gov/vuln/detail/CVE-2020-10543){: external}, [CVE-2020-10878](https://nvd.nist.gov/vuln/detail/CVE-2020-10878){: external}, [CVE-2020-12723](https://nvd.nist.gov/vuln/detail/CVE-2020-12723){: external}, [CVE-2020-15436](https://nvd.nist.gov/vuln/detail/CVE-2020-15436){: external}, [CVE-2020-35513](https://nvd.nist.gov/vuln/detail/CVE-2020-35513){: external}, [CVE-2019-25013](https://nvd.nist.gov/vuln/detail/CVE-2019-25013){: external}, [CVE-2020-10029](https://nvd.nist.gov/vuln/detail/CVE-2020-10029){: external}, [CVE-2020-29573](https://nvd.nist.gov/vuln/detail/CVE-2020-29573){: external}, and [CVE-2020-12321](https://nvd.nist.gov/vuln/detail/CVE-2020-12321){: external}){: external}. |
{: caption="Changes since version 4.4.31_1532_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.4.31_1532_openshift, released 1 February 2021
{: #4431_1532}

The following table shows the changes that are in the worker node fix pack `4.4.31_1532_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates for [CVE-2021-3156](https://nvd.nist.gov/vuln/detail/CVE-2021-3156){: external}, [CVE-2020-25684](https://nvd.nist.gov/vuln/detail/CVE-2020-25684){: external}, [CVE-2020-25685](https://nvd.nist.gov/vuln/detail/CVE-2020-25685){: external}, and [CVE-2020-25686](https://nvd.nist.gov/vuln/detail/CVE-2020-25686){: external}. |
{: caption="Changes since version 4.4.31_1530_openshift" caption-side="bottom"}

### Change log for master fix pack 4.4.31_1531_openshift, released 19 January 2021
{: #4431_1531}

The following table shows the changes that are in the master fix pack patch update `4.4.31_1531_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.1.13 | v1.1.16 | Updated image to implement additional IBM security controls. |
| Gateway-enabled cluster controller | 1184 | 1195 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external}. |
| IBM Calico extension | 556 | 567 | Updated image to implement additional IBM security controls and for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external} and [CVE-2020-24659](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24659){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.0.0 | v2.0.1 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external} and [CVE-2020-24659](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24659){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.16-1 | v1.17.17-1 | Updated to support the Kubernetes 1.17.17 release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 384 | 385 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external} and [CVE-2020-24659](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24659){: external}. |
| Key Management Service provider | v2.2.2 | v2.2.3 | Fixed bug to ignore conflict errors during KMS secret re-encryption. Updated to use `Go` version 1.15.5. Updated image to implement additional IBM security controls and for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external}. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 1004 | 1078 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.4.0-20201210 | v4.4.0-20210112 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.4.0+20210112){: external}. |
| OpenVPN Operator image | v1.0.12 | v1.1.0 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.4.0+20201210 | 4.4.0+20210112 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.4.0+20210112){: external}. |
{: caption="Changes since version 4.4.31_1529_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.4.31_1530_openshift, released 18 January 2021
{: #4431_1530}

The following table shows the changes that are in the worker node fix pack `4.4.31_1530_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates. |
{: caption="Changes since version 4.4.31_1528_openshift" caption-side="bottom"}

### Change log for master fix pack 4.4.31_1529_openshift, released 6 January 2021
{: #4431_1529}

The following table shows the changes that are in the master fix pack patch update `4.4.31_1529_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| IBM Calico extension | 538 | 556 | Updated image to include the `ip` command. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | 1.17.2 | v2.0.0 | Updated to use the universal base image (UBI), to use `Go` version 1.15.5, to run with a least privileged security context, and to improve logging. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.15-1 | v1.17.16-1 | Updated to support the Kubernetes 1.17.16 release. |
| {{site.data.keyword.filestorage_full_notm}} plug-in | N/A | N/A | Updated to run with a privileged security context. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | c148a8a | f859228 | Updated image for [CVE-2020-1971](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1971){: external} and [CVE-2020-24659](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24659){: external}. |
| Key Management Service provider | v2.0.7 | v2.2.2 | Updated the key management service (KMS) provider support as follows. \n - Updated to use `Go` version 1.15.2. \n - Added support for [service-to-service authentication](/docs/account?topic=account-serviceauth). \n - Updated to use the KMS provider secret to identify when a [Key Protect](/docs/openshift?topic=openshift-encryption) key is enabled and disabled so that encryption and decryption requests are updated accordingly. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.4.0-20201207 | v4.4.0-20201210 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.4.0+20201210){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.4.29 | 4.4.31 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-31){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.4.0+20201207 | 4.4.0+20201210 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.4.0+20201210){: external}. |
{: caption="Changes since version 4.4.29_1527_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.4.31_1528_openshift, released 21 December 2020
{: #4431_1528}

The following table shows the changes that are in the worker node fix pack update `4.4.31_1528_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HAProxy | db4e6d | 9b2dca | Image update for [CVE-2020-1971](https://nvd.nist.gov/vuln/detail/CVE-2020-1971){: external} and [CVE-2020-24659](https://nvd.nist.gov/vuln/detail/CVE-2020-24659){: external}. |
| RHEL 7 Packages | 3.10.0-1160.6.1.el7 | 3.10.0-1160.11.1.el7 | Updated worker node image with kernel and package updates for: [CVE-2019-18282](https://nvd.nist.gov/vuln/detail/CVE-2019-18282){: external}, [CVE-2020-10769](https://nvd.nist.gov/vuln/detail/CVE-2020-10769){: external}, [CVE-2020-14314](https://nvd.nist.gov/vuln/detail/CVE-2020-14314){: external}, [CVE-2020-14385](https://nvd.nist.gov/vuln/detail/CVE-2020-14385){: external}, [CVE-2020-24394](https://nvd.nist.gov/vuln/detail/CVE-2020-24394){: external}, [CVE-2020-25212](https://nvd.nist.gov/vuln/detail/CVE-2020-25212){: external}, [CVE-2020-25643](https://nvd.nist.gov/vuln/detail/CVE-2020-25643){: external}, and [CVE-2020-1971](https://nvd.nist.gov/vuln/detail/CVE-2020-1971){: external}. |
{: caption="Changes since version 4.4.29_1527_openshift" caption-side="bottom"}

### Change log for master fix pack 4.4.29_1527_openshift, released 14 December 2020
{: #4429_1527}

The following table shows the changes that are in the master fix pack patch update `4.4.29_1527_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| etcd | v3.4.13 | v3.4.14 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.4.14){: external}. |
| Gateway-enabled cluster controller | 1105 | 1184 | Updated to use `Go` version 1.15.5. Updated image to implement additional IBM security controls. |
| IBM Calico extension | 378 | 538 | Updated to use the universal base image (UBI), to run as a non-root user and to use `Go` version 1.15.5. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.14-1 | v1.17.15-1 | Updated to support the Kubernetes 1.17.15 release. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.filestorage_full_notm}} monitor | 379 | 384 | Updated to use `Go` version 1.15.5 and to run as a non-root user. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.filestorage_full_notm}} plug-in | 379 | 384 | Updated to use `Go` version 1.15.5 and to run with a least privileged security context. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 197bc70 | c148a8a | Updated to use `Go` version 1.15.6 and updated image to implement additional IBM security controls. |
| Key management service (KMS) provider | v2.0.5 | v2.0.7 | Updated image to implement additional IBM security controls. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 208 | 1004 | Updated Alpine base image to version 3.12 and to use `Go` version 1.15.5. Updated image for [CVE-2020-8037](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8037){: external} and [CVE-2020-28928](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28928){: external}. Updated image to implement additional IBM security controls. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.4.0-20201110 | v4.4.0-20201207 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.4.0+20201207){: external}. |
| OpenVPN client | 2.4.6-r3-IKS-116 | 2.4.6-r3-IKS-301 | Updated image to implement additional IBM security controls. |
| OpenVPN Operator image | v1.0.10 | v1.0.12 | Updated image to implement additional IBM security controls. |
| OpenVPN server | 2.4.6-r3-IKS-131 | 2.4.6-r3-IKS-301 | Updated image to implement additional IBM security controls. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.4.0+20201110 | 4.4.0+20201207 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.4.0+20201207){: external}. |
{: caption="Changes since version 4.4.29_1525_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.4.31_1526_openshift, released 7 December 2020
{: #4431_1526}

The following table shows the changes that are in the worker node fix pack update `4.4.31_1526_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| HAProxy | 1.8.26-384f42 | db4e6d | Added provenance labels for source tracking. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.4.30 | 4.4.31 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-31){: external}. |
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates.|
{: caption="Changes since version 4.4.30_1525_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.4.30_1525_openshift, released 23 November 2020
{: #4430_1525}

The following table shows the changes that are in the worker node fix pack update `4.4.30_1525_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Ephemeral storage reservations | N/A | N/A | Local ephemeral storage is reserved on the Kubernetes data disk for system components. |
| {{site.data.keyword.redhat_openshift_notm}} node | 4.4.29 | 4.4.30 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-30){: external}. |
| RHEL 7 Packages |  3.10.0-1160.2.2.el7 | 3.10.0-1160.6.1.el7 | Updated worker node image with kernel and package updates for [CVE-2020-8622](https://nvd.nist.gov/vuln/detail/CVE-2020-8622){: external}, [CVE-2020-8623](https://nvd.nist.gov/vuln/detail/CVE-2020-8623){: external}, [CVE-2020-8624](https://nvd.nist.gov/vuln/detail/CVE-2020-8624){: external}, [CVE-2019-20907](https://nvd.nist.gov/vuln/detail/CVE-2019-20907){: external}, [CVE-2020-15999](https://nvd.nist.gov/vuln/detail/CVE-2020-15999){: external}, [CVE-2020-8177](https://nvd.nist.gov/vuln/detail/CVE-2020-8177){: external}, [CVE-2019-20811](https://nvd.nist.gov/vuln/detail/CVE-2019-20811){: external}, [CVE-2020-14331](https://nvd.nist.gov/vuln/detail/CVE-2020-14331){: external}, [CVE-2020-8695](https://nvd.nist.gov/vuln/detail/CVE-2020-8695){: external}, [CVE-2020-8696](https://nvd.nist.gov/vuln/detail/CVE-2020-8696){: external}, and [CVE-2020-8698](https://nvd.nist.gov/vuln/detail/CVE-2020-8698){: external}.|
{: caption="Changes since version 4.4.29_1524_openshift" caption-side="bottom"}

### Change log for master fix pack 4.4.29_1525_openshift, released 16 November 2020
{: #4429_1525}

The following table shows the changes that are in the master fix pack patch update `4.4.29_1525_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster health image | v1.1.12 | v1.1.13 | Updated image for [DLA-2424-1](https://lists.debian.org/debian-lts-announce/2020/10/msg00037.html){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.13-1 | v1.17.14-1 | Updated to support the Kubernetes 1.17.14 release. Updated image for [DLA-2424-1](https://lists.debian.org/debian-lts-announce/2020/10/msg00037.html){: external}. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 378 | 379 | Updated to use the universal base image (UBI) and to use `Go` version 1.15.2. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 31c794a | 197bc70 | Updated image for [CVE-2019-20454](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20454){: external}, [CVE-2020-10029](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-10029){: external}, [CVE-2020-1751](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1751){: external}, [CVE-2020-1752](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1752){: external}, [CVE-2019-20807](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20807){: external}, [CVE-2019-16935](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16935){: external}, [CVE-2019-20907](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20907){: external}, [CVE-2020-14422](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14422){: external}, [CVE-2020-8492](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8492){: external}, [CVE-2019-15165](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-15165){: external}, [CVE-2019-16168](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16168){: external}, [CVE-2019-20218](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20218){: external}, [CVE-2019-5018](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-5018){: external}, [CVE-2020-13630](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13630){: external}, [CVE-2020-13631](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13631){: external}, [CVE-2020-13632](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13632){: external}, [CVE-2020-6405](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-6405){: external}, [CVE-2020-9327](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9327){: external}, [CVE-2020-8177](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8177){: external}, [CVE-2019-13050](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13050){: external}, [CVE-2018-20843](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-20843){: external}, [CVE-2019-15903](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-15903){: external}, [CVE-2019-14889](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14889){: external}, [CVE-2020-1730](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1730){: external}, [CVE-2019-1551](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1551){: external}, [CVE-2020-14382](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14382){: external}, [CVE-2019-13627](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13627){: external}, [CVE-2019-19956](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19956){: external}, [CVE-2019-20388](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20388){: external}, [CVE-2020-7595](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-7595){: external}, [CVE-2019-20386](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20386){: external}, [CVE-2019-19906](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19906){: external}, [CVE-2019-20387](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20387){: external}, and [CVE-2019-19221](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19221){: external}. |
| Key Management Service provider | v2.0.4 | v2.0.5 | Updated image for [DLA-2424-1](https://lists.debian.org/debian-lts-announce/2020/10/msg00037.html){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} Control Plane Operator | v4.4.0-20200821 | v4.4.0-20201110  | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.4.0+20201110){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.4.27 | 4.4.29 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-29){: external}. |
| OpenVPN Operator image | v1.0.9 | v1.0.10 | Updated image for [CVE-2019-20454](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20454){: external}, [CVE-2020-10029](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-10029){: external}, [CVE-2020-1751](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1751){: external}, [CVE-2020-1752](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1752){: external}, [CVE-2019-20807](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20807){: external}, [CVE-2019-16935](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16935){: external}, [CVE-2019-20907](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20907){: external}, [CVE-2020-14422](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14422){: external}, [CVE-2020-8492](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8492){: external}, [CVE-2019-15165](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-15165){: external}, [CVE-2019-16168](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16168){: external}, [CVE-2019-20218](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20218){: external}, [CVE-2019-5018](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-5018){: external}, [CVE-2020-13630](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13630){: external}, [CVE-2020-13631](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13631){: external}, [CVE-2020-13632](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13632){: external}, [CVE-2020-6405](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-6405){: external}, [CVE-2020-9327](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9327){: external}, [CVE-2020-8177](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8177){: external}, [CVE-2019-13050](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13050){: external}, [CVE-2018-20843](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-20843){: external}, [CVE-2019-15903](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-15903){: external}, [CVE-2019-14889](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14889){: external}, [CVE-2020-1730](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1730){: external}, [CVE-2019-1551](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-1551){: external}, [CVE-2020-14382](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14382){: external}, [CVE-2019-13627](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13627){: external}, [CVE-2019-19956](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19956){: external}, [CVE-2019-20388](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20388){: external}, [CVE-2020-7595](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-7595){: external}, [CVE-2019-20386](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20386){: external}, [CVE-2019-19906](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19906){: external}, [CVE-2019-20387](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20387){: external}, and [CVE-2019-19221](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19221){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.4.0+20200821 | 4.4.0+20201110 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.4.0+20201110){: external}. |
{: caption="Changes since version 4.4.27_1523_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.4.29_1524_openshift, released 9 November 2020
{: #4429_1524}

The following table shows the changes that are in the worker node fix pack update `4.4.29_1524_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.4.27 | 4.4.29 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-29){: external}.|
| RHEL 7 Packages | N/A | N/A | Updated worker node image with package updates for [CVE-2020-15999](https://nvd.nist.gov/vuln/detail/CVE-2020-15999){: external}.|
{: caption="Changes since version 4.4.27_1523_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.4.27_1523_openshift, released 26 October 2020
{: #4427_1523_worker}

The following table shows the changes that are in the worker node fix pack update `4.4.27_1523_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.4.26 | 4.4.27 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-27){: external}.|
| RHEL 7 Packages | 3.10.0-1160.2.1.el7 | 3.10.0-1160.2.2.el7 | Updated worker node images with kernel and package updates for [CVE-2020-12351](https://nvd.nist.gov/vuln/detail/CVE-2020-12351){: external} and [CVE-2020-12352](https://nvd.nist.gov/vuln/detail/CVE-2020-12352){: external}.|
{: caption="Changes since version 4.4.26_1521_openshift" caption-side="bottom"}

### Change log for master fix pack 4.4.27_1523_openshift, released 26 October 2020
{: #4427_1523}

The following table shows the changes that are in the master fix pack patch update `4.4.27_1523_openshift`. Master patch updates are applied automatically.
{: shortdesc}

| Component | Previous | Current | Description |
| --------- | -------- | ------- | ----------- |
| Cluster health image | v1.1.11 | v1.1.12 | Fixed check for unsupported add-ons. Updated to use `Go` version 1.15.2. |
| Gateway-enabled cluster controller | 1082 | 1105 | Updated to use `Go` version 1.15.2. |
| {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} driver and plug-in | 1.17.1 | 1.17.2 | Updated to use `Go` version 1.13.15. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.17.12-1 | v1.17.13-1 | Updated to support the Kubernetes 1.17.13 release. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 4b47693 | 31c794a | Updated to use `Go` version 1.15.2. |
| {{site.data.keyword.redhat_openshift_notm}} | 4.4.20 | 4.4.27 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-27){: external}. |
| {{site.data.keyword.redhat_openshift_notm}} configuration | N/A | N/A | New version 4.4 clusters that run on the VPC infrastructure provider and use {{site.data.keyword.cos_full_notm}} now proxy container image traffic through the internal registry pods directly to the {{site.data.keyword.cos_short}} endpoints. To configure this proxy for existing version 4.4 clusters, see [the troubleshooting topic](/docs/openshift?topic=openshift-ts-app-ocr-vpc-push). |
| OpenVPN Operator image | v1.0.8 | v1.0.9 | Updated to improve OpenVPN availability. |
{: caption="Changes since version 4.4.20_1518_openshift" caption-side="bottom"}

### Change log for worker node fix pack 4.4.26_1521_openshift, released 12 October 2020
{: #4426_1521}

The following table shows the changes that are in the worker node fix pack update `4.4.26_1521_openshift`. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | 4.4.23 | 4.4.26 | See the [{{site.data.keyword.redhat_openshift_notm}} release notes](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-4-26){: external}. |
| RHEL 7 Packages | 3.10.0-1127.19.1.el7 | 3.10.0-1160.2.1.el7 | Updated worker node image with kernel and package updates for: [CVE-2019-12450](https://nvd.nist.gov/vuln/detail/CVE-2019-12450){: external}, [CVE-2019-14822](https://nvd.nist.gov/vuln/detail/CVE-2019-14822){: external}, [CVE-2020-12243](https://nvd.nist.gov/vuln/detail/CVE-2020-12243){: external}, [CVE-2019-14866](https://nvd.nist.gov/vuln/detail/CVE-2019-14866){: external}, [CVE-2017-12652](https://nvd.nist.gov/vuln/detail/CVE-2017-12652){: external}, [CVE-2017-18551](https://nvd.nist.gov/vuln/detail/CVE-2017-18551){: external}, [CVE-2018-20836](https://nvd.nist.gov/vuln/detail/CVE-2018-20836){: external}, [CVE-2019-9454](https://nvd.nist.gov/vuln/detail/CVE-2019-9454){: external}, [CVE-2019-9458](https://nvd.nist.gov/vuln/detail/CVE-2019-9458){: external}, [CVE-2019-12614](https://nvd.nist.gov/vuln/detail/CVE-2019-12614){: external}, [CVE-2019-15217](https://nvd.nist.gov/vuln/detail/CVE-2019-15217){: external}, [CVE-2019-15807](https://nvd.nist.gov/vuln/detail/CVE-2019-15807){: external}, [CVE-2019-15917](https://nvd.nist.gov/vuln/detail/CVE-2019-15917){: external}, [CVE-2019-16231](https://nvd.nist.gov/vuln/detail/CVE-2019-16231){: external}, [CVE-2019-16233](https://nvd.nist.gov/vuln/detail/CVE-2019-16233){: external}, [CVE-2019-16994](https://nvd.nist.gov/vuln/detail/CVE-2019-16994){: external}, [CVE-2019-17053](https://nvd.nist.gov/vuln/detail/CVE-2019-17053){: external}, [CVE-2019-17055](https://nvd.nist.gov/vuln/detail/CVE-2019-17055){: external}, [CVE-2019-18808](https://nvd.nist.gov/vuln/detail/CVE-2019-18808){: external}, [CVE-2019-19046](https://nvd.nist.gov/vuln/detail/CVE-2019-19046){: external}, [CVE-2019-19055](https://nvd.nist.gov/vuln/detail/CVE-2019-19055){: external}, [CVE-2019-19058](https://nvd.nist.gov/vuln/detail/CVE-2019-19058){: external}, [CVE-2019-19059](https://nvd.nist.gov/vuln/detail/CVE-2019-19059){: external}, [CVE-2019-19062](https://nvd.nist.gov/vuln/detail/CVE-2019-19062){: external}, [CVE-2019-19063](https://nvd.nist.gov/vuln/detail/CVE-2019-19063){: external}, [CVE-2019-19332](https://nvd.nist.gov/vuln/detail/CVE-2019-19332){: external}, [CVE-2019-19447](https://nvd.nist.gov/vuln/detail/CVE-2019-19447){: external}, [CVE-2019-19523](https://nvd.nist.gov/vuln/detail/CVE-2019-19523){: external}, [CVE-2019-19524](https://nvd.nist.gov/vuln/detail/CVE-2019-19524){: external}, [CVE-2019-19530](https://nvd.nist.gov/vuln/detail/CVE-2019-19530){: external}, [CVE-2019-19534](https://nvd.nist.gov/vuln/detail/CVE-2019-19534){: external}, [CVE-2019-19537](https://nvd.nist.gov/vuln/detail/CVE-2019-19537){: external}, [CVE-2019-19767](https://nvd.nist.gov/vuln/detail/CVE-2019-19767){: external}, [CVE-2019-19807](https://nvd.nist.gov/vuln/detail/CVE-2019-19807){: external}, [CVE-2019-20054](https://nvd.nist.gov/vuln/detail/CVE-2019-20054){: external}, [CVE-2019-20095](https://nvd.nist.gov/vuln/detail/CVE-2019-20095){: external}, [CVE-2019-20636](https://nvd.nist.gov/vuln/detail/CVE-2019-20636){: external}, [CVE-2020-1749](https://nvd.nist.gov/vuln/detail/CVE-2020-1749){: external}, [CVE-2020-2732](https://nvd.nist.gov/vuln/detail/CVE-2020-2732){: external}, [CVE-2020-8647](https://nvd.nist.gov/vuln/detail/CVE-2020-8647){: external}, [CVE-2020-8649](https://nvd.nist.gov/vuln/detail/CVE-2020-8649){: external}, [CVE-2020-9383](https://nvd.nist.gov/vuln/detail/CVE-2020-9383){: external}, [CVE-2020-10690](https://nvd.nist.gov/vuln/detail/CVE-2020-10690){: external}, [CVE-2020-10732](https://nvd.nist.gov/vuln/detail/CVE-2020-10732){: external}, [CVE-2020-10742](https://nvd.nist.gov/vuln/detail/CVE-2020-10742){: external}, [CVE-2020-10751](https://nvd.nist.gov/vuln/detail/CVE-2020-10751){: external}, [CVE-2020-10942](https://nvd.nist.gov/vuln/detail/CVE-2020-10942){: external}, [CVE-2020-11565](https://nvd.nist.gov/vuln/detail/CVE-2020-11565){: external}, [CVE-2020-12770](https://nvd.nist.gov/vuln/detail/CVE-2020-12770){: external}, [CVE-2020-12826](https://nvd.nist.gov/vuln/detail/CVE-2020-12826){: external}, [CVE-2020-14305](https://nvd.nist.gov/vuln/detail/CVE-2020-14305){: external}, [CVE-2019-5482](https://nvd.nist.gov/vuln/detail/CVE-2019-5482){: external}, [CVE-2019-19126](https://nvd.nist.gov/vuln/detail/CVE-2019-19126){: external}, [CVE-2020-12825](https://nvd.nist.gov/vuln/detail/CVE-2020-12825){: external}, [CVE-2019-5094](https://nvd.nist.gov/vuln/detail/CVE-2019-5094){: external}, [CVE-2019-5188](https://nvd.nist.gov/vuln/detail/CVE-2019-5188){: external}, [CVE-2019-2974](https://nvd.nist.gov/vuln/detail/CVE-2019-2974){: external}, [CVE-2020-2574](https://nvd.nist.gov/vuln/detail/CVE-2020-2574){: external}, [CVE-2020-2752](https://nvd.nist.gov/vuln/detail/CVE-2020-2752){: external}, [CVE-2020-2780](https://nvd.nist.gov/vuln/detail/CVE-2020-2780){: external}, [CVE-2020-2812](https://nvd.nist.gov/vuln/detail/CVE-2020-2812){: external}, [CVE-2019-12749](https://nvd.nist.gov/vuln/detail/CVE-2019-12749){: external}, [CVE-2019-19956](https://nvd.nist.gov/vuln/detail/CVE-2019-19956){: external}, [CVE-2019-20388](https://nvd.nist.gov/vuln/detail/CVE-2019-20388){: external}, [CVE-2020-7595](https://nvd.nist.gov/vuln/detail/CVE-2020-7595){: external}, [CVE-2020-10754](https://nvd.nist.gov/vuln/detail/CVE-2020-10754){: external}, [CVE-2019-11719](https://nvd.nist.gov/vuln/detail/CVE-2019-11719){: external}, [CVE-2019-11727](https://nvd.nist.gov/vuln/detail/CVE-2019-11727){: external}, [CVE-2019-11756](https://nvd.nist.gov/vuln/detail/CVE-2019-11756){: external}, [CVE-2019-17006](https://nvd.nist.gov/vuln/detail/CVE-2019-17006){: external}, [CVE-2019-17023](https://nvd.nist.gov/vuln/detail/CVE-2019-17023){: external}, [CVE-2020-6829](https://nvd.nist.gov/vuln/detail/CVE-2020-6829){: external}, [CVE-2020-12400](https://nvd.nist.gov/vuln/detail/CVE-2020-12400){: external}, [CVE-2020-12401](https://nvd.nist.gov/vuln/detail/CVE-2020-12401){: external}, [CVE-2020-12402](https://nvd.nist.gov/vuln/detail/CVE-2020-12402){: external}, [CVE-2020-12403](https://nvd.nist.gov/vuln/detail/CVE-2020-12403){: external}, [CVE-2018-20843](https://nvd.nist.gov/vuln/detail/CVE-2018-20843){: external}, [CVE-2019-15903](https://nvd.nist.gov/vuln/detail/CVE-2019-15903){: external}, [CVE-2019-14834](https://nvd.nist.gov/vuln/detail/CVE-2019-14834){: external}, [CVE-2019-11068](https://nvd.nist.gov/vuln/detail/CVE-2019-11068){: external}, [CVE-2019-18197](https://nvd.nist.gov/vuln/detail/CVE-2019-18197){: external}, [CVE-2019-16935](https://nvd.nist.gov/vuln/detail/CVE-2019-16935){: external}, [CVE-2019-20386](https://nvd.nist.gov/vuln/detail/CVE-2019-20386){: external}, [CVE-2019-17498](https://nvd.nist.gov/vuln/detail/CVE-2019-17498){: external}, and [CVE-2020-14365](https://nvd.nist.gov/vuln/detail/CVE-2020-14365){: external}.|
{: caption="Changes since version 4.4.23_1520_openshift" caption-side="bottom"}


