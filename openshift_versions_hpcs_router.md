---

copyright:
  years: 2014, 2021
lastupdated: "2021-09-30"

keywords: openshift, roks, rhoks, rhos, route, router

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}

  


# {{site.data.keyword.cloud_notm}} HPCS Router add-on changelog
{: #hpcs-router-changelog}

View information for version updates to the [{{site.data.keyword.cloud_notm}} HPCS Router add-on](/docs/openshift?topic=openshift-hpcs-router) in clusters that run {{site.data.keyword.openshiftshort}} version 4.5 and later.
{: shortdesc}

* **Patch updates**: {{site.data.keyword.cloud_notm}} keeps all your add-on components up-to-date by automatically rolling out patch updates to the most recent version of the HPCS Router that is offered by {{site.data.keyword.openshiftlong_notm}}.
* **Minor version updates**: The minor version of the HPCS Router add-on matches the minor version of your {{site.data.keyword.openshiftshort}} cluster. In the CLI, you can run `ibmcloud oc cluster addon ls -c <cluster_name_or_ID>` to check the current version of your add-on, and `ibmcloud oc cluster get -c <cluster_name_or_ID>` to check the current version of your cluster.

| HPCS Router add-on version | Supported? | {{site.data.keyword.openshiftshort}} version support |
| -------------------------- | -----------|----------------------------------------------------- |
| 4.7 | Yes | 4.7 |
| 4.6 | Yes | 4.6 |
| 4.5 | Yes | 4.5 |
{: summary="The rows are read from left to right. The first column is the HPCS Router add-on version. The second column is the version's supported state. The third column is the {{site.data.keyword.openshiftshort}} version of your cluster that the add-on version is supported for."}
{: caption="Supported HPCS Router add-on versions" caption-side="top"}


## Version 4.7.0
{: #4_7_0}

|Version build|Release date|Changes|
|-------------|------------|-------|
| 4.7.0_854 | 7 September 2021 | Updates to address [CVE-2021-3711](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3711){: external} and [CVE-2021-3712](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3712){: external}. |
{: summary="The rows are read from left to right. The first column is the build of the image version. The second column is the build release date. The third column contains a brief description of the change made in the version build."}
{: caption="Changelog for version 4.7.0 of the HPCS Router add-on" caption-side="top"}

## Version 4.6.0
{: #4_6_0}

|Version build|Release date|Changes|
|-------------|------------|-------|
| 4.6.0_860 | 21 September 2021 | Updates to address [CVE-2021-3711](https://nvd.nist.gov/vuln/detail/CVE-2021-3711){: external} and [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}. |
| 4.6.0_838 | 23 August 2021 | Updates to address [CVE-2021-36221](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-36221){: external} and [CVE-2021-3121](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3121){: external}. |
| 4.6.0_796 | 10 August 2021 | Updates to address [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-33910){: external}. |
| 4.6.0-750 | 26 Jul 2021 | Updates to address [CVE-2021-27219](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-27219){: external}, [CVE-2021-31525](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-31525){: external}, [CVE-2021-3516](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3516){: external}, [CVE-2021-3517](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3517){: external}, [CVE-2021-3518](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3518){: external}, [CVE-2021-3520](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3520){: external}, [CVE-2021-3537](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3537){: external}, [CVE-2021-3541](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3541){: external}, and [CVE-2021-3520](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3520){: external}. |
| 4.6.0_696 | 02 Jun 2021 | Updates to address [CVE-2016-10228](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-10228){: external}, [CVE-2019-13012](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13012){: external}, [CVE-2019-18276](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-18276){: external}, [CVE-2019-25013](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-25013){: external}, [CVE-2019-2708](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-2708){: external}, [CVE-2019-3842](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-3842){: external}, [CVE-2019-9169](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9169){: external}, [CVE-2020-13434](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13434){: external}, [CVE-2020-13543](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13543){: external}, [CVE-2020-13584](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13584){: external}, [CVE-2020-13776](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13776){: external}, [CVE-2020-15358](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-15358){: external}, [CVE-2020-24330](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24330){: external}, [CVE-2020-24331](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24331){: external}, [CVE-2020-24332](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24332){: external}, [CVE-2020-24977](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24977){: external}, [CVE-2020-27618](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-27618){: external}, [CVE-2020-28196](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28196){: external}, [CVE-2020-29361](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-29361){: external}, [CVE-2020-29362](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-29362){: external}, [CVE-2020-29363](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-29363){: external}, [CVE-2020-8231](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8231){: external}, [CVE-2020-8284](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8284){: external}, [CVE-2020-8285](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8285){: external}, [CVE-2020-8286](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8286){: external}, [CVE-2020-8927](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8927){: external}, [CVE-2020-9948](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9948){: external}, [CVE-2020-9951](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9951){: external}, [CVE-2020-9983](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9983){: external}, [CVE-2021-3326](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3326){: external}, [RHSA-2021:1581](https://access.redhat.com/errata/RHSA-2021:1581){: external}, [RHSA-2021:1585](https://access.redhat.com/errata/RHSA-2021:1585){: external}, [RHSA-2021:1586](https://access.redhat.com/errata/RHSA-2021:1586){: external}, [RHSA-2021:1593](https://access.redhat.com/errata/RHSA-2021:1593){: external}, [RHSA-2021:1597](https://access.redhat.com/errata/RHSA-2021:1597){: external}, [RHSA-2021:1609](https://access.redhat.com/errata/RHSA-2021:1609){: external}, [RHSA-2021:1610](https://access.redhat.com/errata/RHSA-2021:1610){: external}, [RHSA-2021:1611](https://access.redhat.com/errata/RHSA-2021:1611){: external}, [RHSA-2021:1627](https://access.redhat.com/errata/RHSA-2021:1627){: external}, [RHSA-2021:1675](https://access.redhat.com/errata/RHSA-2021:1675){: external}, [RHSA-2021:1679](https://access.redhat.com/errata/RHSA-2021:1679){: external}, and [RHSA-2021:1702](https://access.redhat.com/errata/RHSA-2021:1702){: external}. |
| 4.6.0_678 | 22 Apr 2021 | Updates to address `Nettle` vulnerabilities for [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}.|
| 4.6.0_663 | 19 Apr 2021 | Updates to address [CVE-2021-3121](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3121){: external}, [CVE-2021-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-28851){: external}, and [CVE-2021-28852](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-28852){: external}.|
| 4.6.0_654 | 14 Apr 2021 | Fixes OpenSSL vulnerabilities for [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3450){: external}. |
|4.6.0_646|30 Mar 2021|Updates the Go version to 1.15.10 for [CVE-2021-3114](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3114){: external} and [CVE-2021-3115](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3115){: external}.|
{: summary="The rows are read from left to right. The first column is the build of the image version. The second column is the build release date. The third column contains a brief description of the change made in the version build."}
{: caption="Changelog for version 4.6.0 of the HPCS Router add-on" caption-side="top"}

## Version 4.5.0
{: #4_5_0}

|Version build|Release date|Changes|
|-------------|------------|-------|
| 4.5.0_861 | 21 September 2021 | Updates to address [CVE-2021-3711](https://nvd.nist.gov/vuln/detail/CVE-2021-3711){: external} and [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}. |
| 4.5.0_837 | 23 August 2021 | Updates to address [CVE-2021-36221](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-36221){: external} and [CVE-2021-3121](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3121){: external}. |
| 4.5.0_790 | 10 August 2021 | Updates to address [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-33910){: external}. |
| 4.5.0_749 | 26 Jul 2021 | Updates to address [CVE-2021-27219](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-27219){: external}, [CVE-2021-31525](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-31525){: external}, [CVE-2021-3516](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3516){: external}, [CVE-2021-3517](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3517){: external}, [CVE-2021-3518](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3518){: external}, [CVE-2021-3520](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3520){: external}, [CVE-2021-3537](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3537){: external}, [CVE-2021-3541](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3541){: external}, and [CVE-2021-3520](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3520){: external}. |
| 4.5.0_694 | 02 Jun 2021 | Updates to address [CVE-2016-10228](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-10228){: external}, [CVE-2019-13012](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13012){: external}, [CVE-2019-18276](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-18276){: external}, [CVE-2019-25013](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-25013){: external}, [CVE-2019-2708](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-2708){: external}, [CVE-2019-3842](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-3842){: external}, [CVE-2019-9169](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9169){: external}, [CVE-2020-13434](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13434){: external}, [CVE-2020-13543](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13543){: external}, [CVE-2020-13584](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13584){: external}, [CVE-2020-13776](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13776){: external}, [CVE-2020-15358](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-15358){: external}, [CVE-2020-24977](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24977){: external}, [CVE-2020-27618](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-27618){: external}, [CVE-2020-28196](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28196){: external}, [CVE-2020-29361](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-29361){: external}, [CVE-2020-29362](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-29362){: external}, [CVE-2020-29363](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-29363){: external}, [CVE-2020-8231](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8231){: external}, [CVE-2020-8284](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8284){: external}, [CVE-2020-8285](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8285){: external}, [CVE-2020-8286](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8286){: external}, [CVE-2020-8927](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8927){: external}, [CVE-2020-9948](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9948){: external}, [CVE-2020-9951](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9951){: external}, [CVE-2020-9983](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9983){: external}, [CVE-2021-3326](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3326){: external}, [RHSA-2021:1581](https://access.redhat.com/errata/RHSA-2021:1581){: external}, [RHSA-2021:1585](https://access.redhat.com/errata/RHSA-2021:1585){: external}, [RHSA-2021:1586](https://access.redhat.com/errata/RHSA-2021:1586){: external}, [RHSA-2021:1593](https://access.redhat.com/errata/RHSA-2021:1593){: external}, [RHSA-2021:1597](https://access.redhat.com/errata/RHSA-2021:1597){: external}, [RHSA-2021:1609](https://access.redhat.com/errata/RHSA-2021:1609){: external}, [RHSA-2021:1610](https://access.redhat.com/errata/RHSA-2021:1610){: external}, [RHSA-2021:1611](https://access.redhat.com/errata/RHSA-2021:1611){: external}, [RHSA-2021:1627](https://access.redhat.com/errata/RHSA-2021:1627){: external}, [RHSA-2021:1675](https://access.redhat.com/errata/RHSA-2021:1675){: external}, [RHSA-2021:1679](https://access.redhat.com/errata/RHSA-2021:1679){: external}, and [RHSA-2021:1702](https://access.redhat.com/errata/RHSA-2021:1702){: external}. |
| 4.5.0_679 | 22 Apr 2021 | Updates to address `Nettle` vulnerabilities for [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}.|
| 4.5.0_662 | 19 Apr 2021 | Updates to address [CVE-2021-23336](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-23336){: external} and [CVE-2021-22890](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-22890){: external}.|
| 4.5.0_655 | 14 Apr 2021 | Updates to address [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3449){: external} and [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3450){: external}. |
|4.5.0_647|30 Mar 2021|Updates the Go version to 1.15.10 for [CVE-2021-3114](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3114){: external} and [CVE-2021-3115](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3115){: external}.|
{: summary="The rows are read from left to right. The first column is the build of the image version. The second column is the build release date. The third column contains a brief description of the change made in the version build."}
{: caption="Changelog for version 4.5.0 of the HPCS Router add-on" caption-side="top"}






