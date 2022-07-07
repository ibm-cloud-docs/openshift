---

copyright:
  years: 2014, 2022
lastupdated: "2022-07-07"

keywords: openshift

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}



# {{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on changelog
{: #image-key-synchronizer-changelog}

View information for version updates to the [{{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on](/docs/openshift?topic=openshift-images#encrypted-images) in clusters that run {{site.data.keyword.redhat_openshift_notm}} version 4.5 and later.
{: shortdesc}

* **Patch updates**: {{site.data.keyword.cloud_notm}} keeps all your add-on components up-to-date by automatically rolling out patch updates to the most recent version of the Image Key Synchronizer that is offered by {{site.data.keyword.openshiftlong_notm}}.
* **Minor version updates**: To update your add-on components to the most recent minor version of the Image Key Synchronizer that is offered by {{site.data.keyword.openshiftlong_notm}}, follow the steps in [Updating managed add-ons](/docs/openshift?topic=openshift-managed-addons#updating-managed-add-ons).

Review the supported versions of {{site.data.keyword.openshiftlong_notm}} for each add-on version. In the CLI, you can run `ibmcloud oc cluster addon ls -c <cluster_name_or_ID>` to check the current version of your add-on, and `ibmcloud oc cluster get -c <cluster_name_or_ID>` to check the current version of your cluster.

| Image Key Synchronizer add-on version | Supported? | {{site.data.keyword.redhat_openshift_notm}} version support |
| -------------------------- | -----------|----------------------------------------------------- |
| 1.0.0 | Yes | 4.6, 4.7, 4.8 |
{: summary="The rows are read from left to right. The first column is the Image Key Synchronizer add-on version. The second column is the version's supported state. The third column is the {{site.data.keyword.redhat_openshift_notm}} version of your cluster that the add-on version is supported for."}
{: caption="Supported Image Key Synchronizer add-on versions" caption-side="top"}

## Version 1.0.0
{: #1_0_0}

Review the changes in version 1.0.0 of the {{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on plug-in.
{: shortdesc}

### Version 1.0.0_1061, released on 13 Jun 2022
{: #1_0_1022}

Resolves [CVE-2021-38561](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-38561){: external}.

### Version 1.0.0_1022, released on 13 Jun 2022
{: #1_0_1022}

Resolves [CVE-2021-3634](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3634){: external}.

### Version 1.0.0_956, released on 4 May 2022
{: #1_0_0956}

Resolves [CVE-2018-25032](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-25032){: external}.

### Version 1.0.0_927, released on 11 April 2022
{: #1_0_0927}

Resolves [CVE-2022-0778](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-0778){: external}.

### Version 1.0.0_906, released on 24 March 2022
{: #1_0_0906}

- [CVE-2021-3999](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3999){: external}.
- [CVE-2022-23218](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-23218){: external}.
- [CVE-2022-23219](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-23219){: external}.
- [CVE-2022-23308](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-23308){: external}.
- [CVE-2021-23177](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-23177){: external}.
- [CVE-2021-31566](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-31566){: external}.
- [CVE-2022-24921](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-24921){: external}.

### Version 1.0.0_883, released on 28 February 2022
{: #1_0_0883}

- [CVE-2022-23772](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-23772){: external}.
- [CVE-2022-23773](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-23773){: external}.
- [CVE-2022-23806](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-23806){: external}.

### Version 1.0.0_834, released on 25 January 2022
{: #1_0_0834}

- [CVE-2021-44716](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44716){: external}.
- [CVE-2021-44717](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44717){: external}.

### Version 1.0.0_804, released on 11 January 2022
{: #1_0_0804}

Resolves [CVE-2021-3712](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3712){: external}.

### Version 1.0.0_744, released on 19 November 2021
{: #1_0_0744}

- [CVE-2021-41771](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-41771){: external}
- [CVE-2021-41772](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-41772){: external}

### Version 1.0.0_734, released on 16 November 2021
{: #1_0_0734}

- [CVE-2019-17594](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-17594){: external}
- [CVE-2019-17595](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-17595){: external}
- [CVE-2021-33574](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33574){: external}
- [CVE-2021-35942](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-35942){: external}
- [CVE-2021-23840](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-23840){: external}
- [CVE-2021-23841](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-23841){: external}
- [CVE-2021-20231](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20231){: external}
- [CVE-2021-20232](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20232){: external}
- [CVE-2021-3580](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3580){: external}
- [CVE-2021-28153](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-28153){: external}
- [CVE-2021-3800](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3800){: external}
- [CVE-2019-18218](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-18218){: external}
- [CVE-2020-12762](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-12762){: external}
- [CVE-2020-16135](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-16135){: external}
- [CVE-2021-20266](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20266){: external}
- [CVE-2021-33928](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33928){: external}
- [CVE-2021-33929](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33929){: external}
- [CVE-2021-33930](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33930){: external}
- [CVE-2021-33938](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33938){: external}
- [CVE-2021-3200](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3200){: external}
- [CVE-2021-3445](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3445){: external}
- [CVE-2021-22946](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-22946){: external}
- [CVE-2021-22947](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-22947){: external}
- [CVE-2021-22876](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-22876){: external}
- [CVE-2021-22898](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-22898){: external}
- [CVE-2021-22925](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-22925){: external}
- [CVE-2018-20673](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-20673){: external}
- [CVE-2021-36084](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-36084){: external}
- [CVE-2021-36085](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-36085){: external}
- [CVE-2021-36086](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-36086){: external}
- [CVE-2021-36087](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-36087){: external}
- [CVE-2021-33560](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-33560){: external}
- [CVE-2019-13750](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13750){: external}
- [CVE-2019-13751](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13751){: external}
- [CVE-2019-19603](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19603){: external}
- [CVE-2019-5827](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-5827){: external}
- [CVE-2020-13435](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-13435){: external}
- [CVE-2020-24370](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-24370){: external}
- [CVE-2019-20838](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-20838){: external}
- [CVE-2020-14155](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14155){: external}

### Version 1.0.0_690, released on 6 October 2021
{: #1_0_0690}

- [CVE-2021-22922](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-22922){: external}
- [CVE-2021-22923](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-22923){: external}
- [CVE-2021-22924](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-22924){: external}
- [CVE-2021-36222](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-36222){: external}
- [CVE-2021-37750](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-37750){: external}

### Version 1.0.0_627, released on 23 August 2021
{: #1_0_0627}

- [CVE-2021-36221](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-36221){: external}

### Version 1.0.0_614, released on 10 August 2021
{: #1_0_0614}

- [CVE-2021-33910](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-33910){: external}
- [CVE-2021-34558](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-34558){: external}

### Version 1.0.0_575, released on 23 July 2021
{: #1_0_0575}

- [CVE-2021-20271](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-20271){: external}
- [CVE-2021-3516](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3516){: external}
- [CVE-2021-3517](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3517){: external}
- [CVE-2021-3518](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3518){: external}
- [CVE-2021-3537](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3537){: external}
- [CVE-2021-3541](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3541){: external}
- [CVE-2021-3520](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3520){: external}

### Version 1.0.0_549, released on 17 June 2021
{: #1_0_0549}

- [CVE-2021-31525](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-31525){: external}
- [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-33194){: external}

### Version 1.0.0_529, released on 2 June 2021
{: #1_0_0529}

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

### Version 1.0.0_485, released on 28 April 2021
{: #1_0_0485}

- [CVE-2021-20305](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-20305){: external}

### Version 1.0.0_473, released on 19 April 2021
{: #1_0_0473}

- [CVE-2021-3121](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3121){: external}
- [CVE-2021-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-28851){: external}
- [CVE-2021-28852](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-28852){: external}

### Version 1.0.0_461, released on 14 April 2021
{: #1_0_0461}

- [CVE-2021-3449](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3449){: external}
- [CVE-2021-3450](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3450){: external}

### Version 1.0.0_438, released on 30 March 2021
{: #1_0_0438}

- [CVE-2021-3114](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3114){: external}
- [CVE-2021-3115](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3115){: external}
