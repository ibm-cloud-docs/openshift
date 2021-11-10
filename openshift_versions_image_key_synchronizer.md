---

copyright:
  years: 2014, 2021
lastupdated: "2021-11-10"

keywords: openshift

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on changelog
{: #image-key-synchronizer-changelog}

View information for version updates to the [{{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on](/docs/openshift?topic=openshift-images#encrypted-images) in clusters that run {{site.data.keyword.openshiftshort}} version 4.5 and later.
{: shortdesc}

* **Patch updates**: {{site.data.keyword.cloud_notm}} keeps all your add-on components up-to-date by automatically rolling out patch updates to the most recent version of the Image Key Synchronizer that is offered by {{site.data.keyword.openshiftlong_notm}}.
* **Minor version updates**: To update your add-on components to the most recent minor version of the Image Key Synchronizer that is offered by {{site.data.keyword.openshiftlong_notm}}, follow the steps in [Updating managed add-ons](/docs/openshift?topic=openshift-managed-addons#updating-managed-add-ons).

Review the supported versions of {{site.data.keyword.openshiftlong_notm}} for each add-on version. In the CLI, you can run `ibmcloud oc cluster addon ls -c <cluster_name_or_ID>` to check the current version of your add-on, and `ibmcloud oc cluster get -c <cluster_name_or_ID>` to check the current version of your cluster.

| Image Key Synchronizer add-on version | Supported? | {{site.data.keyword.openshiftshort}} version support |
| -------------------------- | -----------|----------------------------------------------------- |
| 1.0.0 | Yes | 4.6, 4.5, 4.4 |
{: summary="The rows are read from left to right. The first column is the Image Key Synchronizer add-on version. The second column is the version's supported state. The third column is the {{site.data.keyword.openshiftshort}} version of your cluster that the add-on version is supported for."}
{: caption="Supported Image Key Synchronizer add-on versions" caption-side="top"}

## Version 1.0.0
{: #1_0_0}

Review the changes in version 1.0.0 of the {{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on plug-in.
{: shortdesc}

## Changelog for version 1.0.0_690, released 6 October 2021
{: #1_0_0690}

Review the changes in version 1.0.0_690 of the {{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on plug-in.
{: shortdesc}

Updates to address
- [CVE-2021-22922](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-22922){: external}
- [CVE-2021-22923](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-22923){: external}
- [CVE-2021-22924](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-22924){: external}
- [CVE-2021-36222](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-36222){: external}
- [CVE-2021-37750](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-37750){: external}

## Changelog for version 1.0.0_627, released 23 August 2021
{: #1_0_0627}

Review the changes in version 1.0.0_627 of the {{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on plug-in.
{: shortdesc}

Updates to address
- [CVE-2021-36221](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-36221){: external}

## Changelog for version 1.0.0_614, released 10 August 2021
{: #1_0_0614}

Review the changes in version 1.0.0_614 of the {{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on plug-in.
{: shortdesc}

Updates to address
- [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-33910){: external}
- [CVE-2021-34558](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-34558){: external}

## Changelog for version 1.0.0_575, released 23 July 2021
{: #1_0_0575}

Review the changes in version 1.0.0_575 of the {{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on plug-in.
{: shortdesc}

Updates to address
- [CVE-2021-20271](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-20271){: external}
- [CVE-2021-3516](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3516){: external}
- [CVE-2021-3517](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3517){: external}
- [CVE-2021-3518](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3518){: external}
- [CVE-2021-3537](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3537){: external}
- [CVE-2021-3541](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3541){: external}
- [CVE-2021-3520](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3520){: external}

## Changelog for version 1.0.0_549, released 17 June 2021
{: #1_0_0549}

Review the changes in version 1.0.0_549 of the {{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on plug-in.
{: shortdesc}

Updates to address
- [CVE-2021-31525](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-31525){: external}
- [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-33194){: external}

## Changelog for version 1.0.0_529, released 2 June 2021
{: #1_0_0529}

Review the changes in version 1.0.0_529 of the {{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on plug-in.
{: shortdesc}

Updates to address
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
- [RHSA-2021:1675](https://access.redhat.com/errata/RHSA-2021:1675){: external}
- [RHSA-2021:1679](https://access.redhat.com/errata/RHSA-2021:1679){: external}
- [RHSA-2021:1702](https://access.redhat.com/errata/RHSA-2021:1702){: external}

## Changelog for version 1.0.0_485, released 28 April 2021
{: #1_0_0485}

Review the changes in version 1.0.0_485 of the {{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on plug-in.
{: shortdesc}

Updates to address
- [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}

## Changelog for version 1.0.0_473, released 19 April 2021
{: #1_0_0473}

Review the changes in version 1.0.0_473 of the {{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on plug-in.
{: shortdesc}

Updates to address
- [CVE-2021-3121](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3121){: external}
- [CVE-2021-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-28851){: external}
- [CVE-2021-28852](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-28852){: external}

## Changelog for version 1.0.0_461, released 14 April 2021
{: #1_0_0461}

Review the changes in version 1.0.0_461 of the {{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on plug-in.
{: shortdesc}

Updates to address
- [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3449){: external}
- [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3450){: external}

## Changelog for version 1.0.0_438, released 30 March 2021
{: #1_0_0438}

Review the changes in version 1.0.0_438 of the {{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on plug-in.
{: shortdesc}

Updates the Go version to 1.15.10
- [CVE-2021-3114](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3114){: external}
- [CVE-2021-3115](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3115){: external}
