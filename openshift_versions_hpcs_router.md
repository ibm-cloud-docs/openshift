---

copyright:
  years: 2014, 2022
lastupdated: "2022-03-14"

keywords: openshift, route, router

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.cloud_notm}} HPCS Router add-on changelog
{: #hpcs-router-changelog}

View information for version updates to the [{{site.data.keyword.cloud_notm}} HPCS Router add-on](/docs/openshift?topic=openshift-hpcs-router) in clusters that run {{site.data.keyword.redhat_openshift_notm}} version 4.5 and later.
{: shortdesc}

* **Patch updates**: {{site.data.keyword.cloud_notm}} keeps all your add-on components up-to-date by automatically rolling out patch updates to the most recent version of the HPCS Router that is offered by {{site.data.keyword.openshiftlong_notm}}.
* **Minor version updates**: The minor version of the HPCS Router add-on matches the minor version of your {{site.data.keyword.redhat_openshift_notm}} cluster. In the CLI, you can run `ibmcloud oc cluster addon ls -c <cluster_name_or_ID>` to check the current version of your add-on, and `ibmcloud oc cluster get -c <cluster_name_or_ID>` to check the current version of your cluster.

| HPCS Router add-on version | Supported? | {{site.data.keyword.redhat_openshift_notm}} version support |
| -------------------------- | -----------|----------------------------------------------------- |
| 4.9 | Yes | 4.9 |
| 4.8 | Yes | 4.8 |
| 4.7 | Yes | 4.7 |
| 4.6 | Yes | 4.6 |
| 4.5 | No | 4.5 |
{: summary="The rows are read from left to right. The first column is the HPCS Router add-on version. The second column is the version's supported state. The third column is the {{site.data.keyword.redhat_openshift_notm}} version of your cluster that the add-on version is supported for."}
{: caption="Supported HPCS Router add-on versions" caption-side="top"}

## Version 4.9.0
{: #4.9.0}

### Version 4.9.0_1364, released on 14 March 2022
{: #4_9_1364}

Resolves [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}.

### Version 4.9.0_1349, released on 28 February 2022
{: #4_9_0_1349}

- [CVE-2022-23772](https://nvd.nist.gov/vuln/detail/CVE-2022-23772){: external}.
- [CVE-2022-23773](https://nvd.nist.gov/vuln/detail/CVE-2022-23773){: external}.
- [CVE-2022-23806](https://nvd.nist.gov/vuln/detail/CVE-2022-23806){: external}.

### Version 4.9.0, released on 16 February 2022
{: #4_9_0}

Initial release of 4.9.0.

## Version 4.8.0
{: #4_8_0}

### Version 4.8.0_1363, released on 14 March 2022
{: #4_8_1363}

Resolves [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}.

### Version 4.8.0_1310, released on 28 February 2022
{: #4_8_0_1310}

- [CVE-2022-23772](https://nvd.nist.gov/vuln/detail/CVE-2022-23772){: external}.
- [CVE-2022-23773](https://nvd.nist.gov/vuln/detail/CVE-2022-23773){: external}.
- [CVE-2022-23806](https://nvd.nist.gov/vuln/detail/CVE-2022-23806){: external}.

### Version 4.8.0_1232, released on 25 January 2022
{: #4_8_1232}

- [CVE-2021-44716](https://nvd.nist.gov/vuln/detail/CVE-2021-44716){: external}.
- [CVE-2021-44717](https://nvd.nist.gov/vuln/detail/CVE-2021-44717){: external}.

### Version 4.8.0_1125, released on 11 January 2022
{: #4_8_1125}

Resolves [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}.

### Version 4.8.0_997, released on 16 November 2021
{: #4_8_0997}

Initial release of 4.8.0.

## Version 4.7.0
{: #4_7_0}

### Version 4.7.0_1362, released on 14 March 2022
{: #4_7_1362}

Resolves [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}.

### Version 4.7.0_1309, released on 28 February 2022
{: #4_7_0_1309}

- [CVE-2022-23772](https://nvd.nist.gov/vuln/detail/CVE-2022-23772){: external}.
- [CVE-2022-23773](https://nvd.nist.gov/vuln/detail/CVE-2022-23773){: external}.
- [CVE-2022-23806](https://nvd.nist.gov/vuln/detail/CVE-2022-23806){: external}.

### Version 4.7.0_1226, released on 25 January 2022
{: #4_7_1226}

- [CVE-2021-44716](https://nvd.nist.gov/vuln/detail/CVE-2021-44716){: external}.
- [CVE-2021-44717](https://nvd.nist.gov/vuln/detail/CVE-2021-44717){: external}.

### Version 4.7.0_1127, released on 11 January 2022
{: #4_7_1127}

Resolves [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}.

### Version 4.7.0_1013, released on 19 November 2021
{: #4_7_1013}

- [CVE-2021-41771](https://nvd.nist.gov/vuln/detail/CVE-2021-41771){: external}
- [CVE-2021-41772](https://nvd.nist.gov/vuln/detail/CVE-2021-41772){: external}

### Version 4.7.0_985, released on 16 November 2021
{: #4_7_0985}

- [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946){: external}
- [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947){: external}
- [CVE-2021-33928](https://nvd.nist.gov/vuln/detail/CVE-2021-33928){: external}
- [CVE-2021-33929](https://nvd.nist.gov/vuln/detail/CVE-2021-33929){: external}
- [CVE-2021-33930](https://nvd.nist.gov/vuln/detail/CVE-2021-33930){: external}
- [CVE-2021-33938](https://nvd.nist.gov/vuln/detail/CVE-2021-33938){: external}

### Version 4.7.0_854, released on 7 September 2021
{: #4_7_0854}

- [CVE-2021-3711](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3711){: external}
- [CVE-2021-3712](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3712){: external}

## Version 4.6.0
{: #4_6_0}

### Version 4.6.0_1360, released on 14 March 2022
{: #4_6_1360}

Resolves [CVE-2022-24407](https://nvd.nist.gov/vuln/detail/CVE-2022-24407){: external}.

### Version 4.6.0_1308, released on 28 February 2022
{: #4_6_0_1308}

- [CVE-2022-23772](https://nvd.nist.gov/vuln/detail/CVE-2022-23772){: external}.
- [CVE-2022-23773](https://nvd.nist.gov/vuln/detail/CVE-2022-23773){: external}.
- [CVE-2022-23806](https://nvd.nist.gov/vuln/detail/CVE-2022-23806){: external}.

### Version 4.6.0_1227, released on 25 January 2022
{: #4_6_1227}

- [CVE-2021-44716](https://nvd.nist.gov/vuln/detail/CVE-2021-44716){: external}.
- [CVE-2021-44717](https://nvd.nist.gov/vuln/detail/CVE-2021-44717){: external}.

### Version 4.6.0_1126, released on 11 January 2022
{: #4_6_1126}

Resolves [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}.

### Version 4.6.0_1012, released on 19 November 2021
{: #4_6_1012}

- [CVE-2021-41771](https://nvd.nist.gov/vuln/detail/CVE-2021-41771){: external}
- [CVE-2021-41772](https://nvd.nist.gov/vuln/detail/CVE-2021-41772){: external}

### Version 4.6.0_987, released on 16 November 2021
{: #4_6_0987}

- [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946){: external}
- [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947){: external}
- [CVE-2021-33928](https://nvd.nist.gov/vuln/detail/CVE-2021-33928){: external}
- [CVE-2021-33929](https://nvd.nist.gov/vuln/detail/CVE-2021-33929){: external}
- [CVE-2021-33930](https://nvd.nist.gov/vuln/detail/CVE-2021-33930){: external}
- [CVE-2021-33938](https://nvd.nist.gov/vuln/detail/CVE-2021-33938){: external}

### Version 4.6.0_860, released on 21 September 2021
{: #4_6_0860}

- [CVE-2021-3711](https://nvd.nist.gov/vuln/detail/CVE-2021-3711){: external}
- [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}

### Version 4.6.0_838, released on 23 August 2021
{: #4_6_0838}

- [CVE-2021-36221](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-36221){: external}
- [CVE-2021-3121](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3121){: external}

### Version 4.6.0_796, released on 10 August 2021
{: #4_6_0796}

- [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-33910){: external}

### Version 4.6.0_750, released on 26 Jul 2021
{: #4_6_0750}

- [CVE-2021-27219](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-27219){: external}
- [CVE-2021-31525](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-31525){: external}
- [CVE-2021-3516](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3516){: external}
- [CVE-2021-3517](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3517){: external}
- [CVE-2021-3518](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3518){: external}
- [CVE-2021-3520](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3520){: external}
- [CVE-2021-3537](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3537){: external}
- [CVE-2021-3541](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3541){: external}
- [CVE-2021-3520](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3520){: external}

### Version 4.6.0_696, released on 02 Jun 2021
{: #4_6_0696}

- [CVE-2016-10228](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-10228){: external}
- [CVE-2019-13012](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13012){: external}
- [CVE-2019-18276](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-18276){: external}
- [CVE-2019-25013](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-25013){: external}
- [CVE-2019-2708](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-2708){: external}
- [CVE-2019-3842](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-3842){: external}
- [CVE-2019-9169](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9169){: external}
- [CVE-2020-13434](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13434){: external}
- [CVE-2020-13543](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13543){: external}
- [CVE-2020-13584](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13584){: external}
- [CVE-2020-13776](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13776){: external}
- [CVE-2020-15358](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-15358){: external}
- [CVE-2020-24330](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24330){: external}
- [CVE-2020-24331](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24331){: external}
- [CVE-2020-24332](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24332){: external}
- [CVE-2020-24977](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24977){: external}
- [CVE-2020-27618](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-27618){: external}
- [CVE-2020-28196](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28196){: external}
- [CVE-2020-29361](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-29361){: external}
- [CVE-2020-29362](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-29362){: external}
- [CVE-2020-29363](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-29363){: external}
- [CVE-2020-8231](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8231){: external}
- [CVE-2020-8284](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8284){: external}
- [CVE-2020-8285](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8285){: external}
- [CVE-2020-8286](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8286){: external}
- [CVE-2020-8927](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8927){: external}
- [CVE-2020-9948](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9948){: external}
- [CVE-2020-9951](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9951){: external}
- [CVE-2020-9983](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9983){: external}
- [CVE-2021-3326](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3326){: external}
- [RHSA-2021:1581](https://access.redhat.com/errata/RHSA-2021:1581){: external}
- [RHSA-2021:1585](https://access.redhat.com/errata/RHSA-2021:1585){: external}
- [RHSA-2021:1586](https://access.redhat.com/errata/RHSA-2021:1586){: external}
- [RHSA-2021:1593](https://access.redhat.com/errata/RHSA-2021:1593){: external}
- [RHSA-2021:1597](https://access.redhat.com/errata/RHSA-2021:1597){: external}
- [RHSA-2021:1609](https://access.redhat.com/errata/RHSA-2021:1609){: external}
- [RHSA-2021:1610](https://access.redhat.com/errata/RHSA-2021:1610){: external}
- [RHSA-2021:1611](https://access.redhat.com/errata/RHSA-2021:1611){: external}
- [RHSA-2021:1627](https://access.redhat.com/errata/RHSA-2021:1627){: external}
- [RHSA-2021:1675](https://access.redhat.com/errata/RHSA-2021:1675){: external}
- [RHSA-2021:1679](https://access.redhat.com/errata/RHSA-2021:1679){: external}
- [RHSA-2021:1702](https://access.redhat.com/errata/RHSA-2021:1702){: external}

### Version 4.6.0_678, released on 22 Apr 2021
{: #4_6_0678}

- `Nettle` vulnerabilities for [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}

### Version 4.6.0_663, released on 19 Apr 2021
{: #4_6_0663}

- [CVE-2021-3121](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3121){: external}
- [CVE-2021-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-28851){: external}
- [CVE-2021-28852](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-28852){: external}

### Version 4.6.0_654, released on 14 Apr 2021
{: #4_6_0654}

- [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3449){: external}
- [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3450){: external}

### Version 4.6.0_646, released on 30 Mar 2021
{: #4_6_0646}

- [CVE-2021-3114](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3114){: external}
- [CVE-2021-3115](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3115){: external}

## Version 4.5.0 (Unsupported)
{: #4_5_0}

Version 4.5.0 is unsupported.

### Version 4.5.0_861, released on 21 September 2021
{: #4_5_0861}

- [CVE-2021-3711](https://nvd.nist.gov/vuln/detail/CVE-2021-3711){: external}
- [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}

### Version 4.5.0_837, released on 23 August 2021
{: #4_5_0837}

- [CVE-2021-36221](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-36221){: external}
- [CVE-2021-3121](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3121){: external}

### Version 4.5.0_790, released on 10 August 2021
{: #4_5_0790}

- [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-33910){: external}

### Version 4.5.0_749, released on 26 Jul 2021
{: #4_5_0749}

- [CVE-2021-27219](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-27219){: external}
- [CVE-2021-31525](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-31525){: external}
- [CVE-2021-3516](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3516){: external}
- [CVE-2021-3517](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3517){: external}
- [CVE-2021-3518](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3518){: external}
- [CVE-2021-3520](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3520){: external}
- [CVE-2021-3537](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3537){: external}
- [CVE-2021-3541](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3541){: external}
- [CVE-2021-3520](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3520){: external}

### Version 4.5.0_694, released on 02 Jun 2021
{: #4_5_0694}

- [CVE-2016-10228](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-10228){: external}
- [CVE-2019-13012](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13012){: external}
- [CVE-2019-18276](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-18276){: external}
- [CVE-2019-25013](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-25013){: external}
- [CVE-2019-2708](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-2708){: external}
- [CVE-2019-3842](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-3842){: external}
- [CVE-2019-9169](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9169){: external}
- [CVE-2020-13434](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13434){: external}
- [CVE-2020-13543](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13543){: external}
- [CVE-2020-13584](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13584){: external}
- [CVE-2020-13776](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13776){: external}
- [CVE-2020-15358](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-15358){: external}
- [CVE-2020-24977](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24977){: external}
- [CVE-2020-27618](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-27618){: external}
- [CVE-2020-28196](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28196){: external}
- [CVE-2020-29361](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-29361){: external}
- [CVE-2020-29362](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-29362){: external}
- [CVE-2020-29363](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-29363){: external}
- [CVE-2020-8231](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8231){: external}
- [CVE-2020-8284](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8284){: external}
- [CVE-2020-8285](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8285){: external}
- [CVE-2020-8286](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8286){: external}
- [CVE-2020-8927](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-8927){: external}
- [CVE-2020-9948](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9948){: external}
- [CVE-2020-9951](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9951){: external}
- [CVE-2020-9983](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-9983){: external}
- [CVE-2021-3326](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3326){: external}
- [RHSA-2021:1581](https://access.redhat.com/errata/RHSA-2021:1581){: external}
- [RHSA-2021:1585](https://access.redhat.com/errata/RHSA-2021:1585){: external}
- [RHSA-2021:1586](https://access.redhat.com/errata/RHSA-2021:1586){: external}
- [RHSA-2021:1593](https://access.redhat.com/errata/RHSA-2021:1593){: external}
- [RHSA-2021:1597](https://access.redhat.com/errata/RHSA-2021:1597){: external}
- [RHSA-2021:1609](https://access.redhat.com/errata/RHSA-2021:1609){: external}
- [RHSA-2021:1610](https://access.redhat.com/errata/RHSA-2021:1610){: external}
- [RHSA-2021:1611](https://access.redhat.com/errata/RHSA-2021:1611){: external}
- [RHSA-2021:1627](https://access.redhat.com/errata/RHSA-2021:1627){: external}
- [RHSA-2021:1675](https://access.redhat.com/errata/RHSA-2021:1675){: external}
- [RHSA-2021:1679](https://access.redhat.com/errata/RHSA-2021:1679){: external}
- [RHSA-2021:1702](https://access.redhat.com/errata/RHSA-2021:1702){: external}

### Version 4.5.0_679, released on 22 Apr 2021
{: #4_5_0679}

- `Nettle` vulnerabilities for [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}

### Version 4.5.0_662, released on 19 Apr 2021
{: #4_5_0662}

- [CVE-2021-23336](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-23336){: external}
- [CVE-2021-22890](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-22890){: external}

### Version 4.5.0_655, released on 14 Apr 2021
{: #4_5_0655}

- [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3449){: external}
- [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3450){: external}

### Version 4.5.0_647, released on 30 Mar 2021
{: #4_5_0647}

- [CVE-2021-3114](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3114){: external}
- [CVE-2021-3115](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3115){: external}

