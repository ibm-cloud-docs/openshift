---

copyright:
  years: 2023, 2024
lastupdated: "2024-09-03"


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


### Change log for master fix pack 4.13.46_1588_openshift, released 28 August 2024
{: #41346_1588_openshift_M}

The following table shows the changes that are in the master fix pack 4.13.46_1588_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.5.7 | v1.5.8 | New version contains updates and security fixes. |
| etcd | v3.5.14 | v3.5.15 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.15){: external}. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.23 | v2.4.24 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.26.15-27 | v1.26.15-29 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 312030f | 897f067 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.12 | v2.8.13 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2967 | 3022 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.17 | v0.13.18 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.18){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.13.45 | 4.13.46 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-46){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | 4.13.0+20240709 | 4.13.0+20240814 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.13.0+20240814){: external}. |
{: caption="Changes since version 4.13.45_1585_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.48_1589_openshift, released 26 August 2024
{: #41348_1589_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.48_1589_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages | N/A | N/A | Package updates for [RHSA-2024:5524](https://access.redhat.com/errata/RHSA-2024:5524){: external}, [CVE-2024-1737](https://nvd.nist.gov/vuln/detail/CVE-2024-1737){: external}, [CVE-2024-1975](https://nvd.nist.gov/vuln/detail/CVE-2024-1975){: external}, [RHSA-2024:5258](https://access.redhat.com/errata/RHSA-2024:5258){: external}, [CVE-2023-45290](https://nvd.nist.gov/vuln/detail/CVE-2023-45290){: external}, [CVE-2024-1394](https://nvd.nist.gov/vuln/detail/CVE-2024-1394){: external}, [CVE-2024-24783](https://nvd.nist.gov/vuln/detail/CVE-2024-24783){: external}, [CVE-2024-24784](https://nvd.nist.gov/vuln/detail/CVE-2024-24784){: external}, [CVE-2024-24789](https://nvd.nist.gov/vuln/detail/CVE-2024-24789){: external}, [CVE-2024-3727](https://nvd.nist.gov/vuln/detail/CVE-2024-3727){: external}, [CVE-2024-37298](https://nvd.nist.gov/vuln/detail/CVE-2024-37298){: external}, [CVE-2024-6104](https://nvd.nist.gov/vuln/detail/CVE-2024-6104){: external}, [RHSA-2024:5530](https://access.redhat.com/errata/RHSA-2024:5530){: external}, [CVE-2024-6345](https://nvd.nist.gov/vuln/detail/CVE-2024-6345){: external}, [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043){: external}, [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/CVE-2024-0690){: external}, [RHSA-2024:5654](https://access.redhat.com/errata/RHSA-2024:5654){: external}, [CVE-2024-2398](https://nvd.nist.gov/vuln/detail/CVE-2024-2398){: external}, [RHSA-2024:5312](https://access.redhat.com/errata/RHSA-2024:5312){: external}, [CVE-2024-37370](https://nvd.nist.gov/vuln/detail/CVE-2024-37370){: external}, [CVE-2024-37371](https://nvd.nist.gov/vuln/detail/CVE-2024-37371){: external}, [RHSA-2024:5309](https://access.redhat.com/errata/RHSA-2024:5309){: external}, [CVE-2024-37891](https://nvd.nist.gov/vuln/detail/CVE-2024-37891){: external}, [RHSA-2024:5299](https://access.redhat.com/errata/RHSA-2024:5299){: external}, [CVE-2024-38428](https://nvd.nist.gov/vuln/detail/CVE-2024-38428){: external}. |
| Haproxy | c91c765 | 546887a | Security fixes for [CVE-2024-2398](https://exchange.xforce.ibmcloud.com/vulnerabilities/286430){: external}, [CVE-2024-37370](https://exchange.xforce.ibmcloud.com/vulnerabilities/296012){: external}, [CVE-2024-37371](https://exchange.xforce.ibmcloud.com/vulnerabilities/296013){: external}, [CVE-2024-6345](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2024-6345){: external}. |
| {{site.data.keyword.openshiftshort}}. | 4.13.46 | 4.13.48 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-48){: external}. |
{: caption="Changes since version 4.13.46_1587_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.46_1587_openshift, released 12 August 2024
{: #41346_1587_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.46_1587_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages | 4.18.0-553.8.1.el8_10 | 4.18.0-553.16.1.el8_10 | Package updates for [RHSA-2024:5101](https://access.redhat.com/errata/RHSA-2024:5101){: external}, [CVE-2021-46939](https://nvd.nist.gov/vuln/detail/CVE-2021-46939){: external}, [CVE-2021-47018](https://nvd.nist.gov/vuln/detail/CVE-2021-47018){: external}, [CVE-2021-47257](https://nvd.nist.gov/vuln/detail/CVE-2021-47257){: external}, [CVE-2021-47284](https://nvd.nist.gov/vuln/detail/CVE-2021-47284){: external}, [CVE-2021-47304](https://nvd.nist.gov/vuln/detail/CVE-2021-47304){: external}, [CVE-2021-47373](https://nvd.nist.gov/vuln/detail/CVE-2021-47373){: external}, [CVE-2021-47408](https://nvd.nist.gov/vuln/detail/CVE-2021-47408){: external}, [CVE-2021-47461](https://nvd.nist.gov/vuln/detail/CVE-2021-47461){: external}, [CVE-2021-47468](https://nvd.nist.gov/vuln/detail/CVE-2021-47468){: external}, [CVE-2021-47491](https://nvd.nist.gov/vuln/detail/CVE-2021-47491){: external}, [CVE-2021-47548](https://nvd.nist.gov/vuln/detail/CVE-2021-47548){: external}, [CVE-2021-47579](https://nvd.nist.gov/vuln/detail/CVE-2021-47579){: external}, [CVE-2021-47624](https://nvd.nist.gov/vuln/detail/CVE-2021-47624){: external}, [CVE-2022-48632](https://nvd.nist.gov/vuln/detail/CVE-2022-48632){: external}, [CVE-2022-48743](https://nvd.nist.gov/vuln/detail/CVE-2022-48743){: external}, [CVE-2022-48747](https://nvd.nist.gov/vuln/detail/CVE-2022-48747){: external}, [CVE-2022-48757](https://nvd.nist.gov/vuln/detail/CVE-2022-48757){: external}, [CVE-2023-28746](https://nvd.nist.gov/vuln/detail/CVE-2023-28746){: external}, [CVE-2023-52451](https://nvd.nist.gov/vuln/detail/CVE-2023-52451){: external}, [CVE-2023-52463](https://nvd.nist.gov/vuln/detail/CVE-2023-52463){: external}, [CVE-2023-52469](https://nvd.nist.gov/vuln/detail/CVE-2023-52469){: external}, [CVE-2023-52471](https://nvd.nist.gov/vuln/detail/CVE-2023-52471){: external}, [CVE-2023-52486](https://nvd.nist.gov/vuln/detail/CVE-2023-52486){: external}, [CVE-2023-52530](https://nvd.nist.gov/vuln/detail/CVE-2023-52530){: external}, [CVE-2023-52619](https://nvd.nist.gov/vuln/detail/CVE-2023-52619){: external}, [CVE-2023-52622](https://nvd.nist.gov/vuln/detail/CVE-2023-52622){: external}, [CVE-2023-52623](https://nvd.nist.gov/vuln/detail/CVE-2023-52623){: external}, [CVE-2023-52648](https://nvd.nist.gov/vuln/detail/CVE-2023-52648){: external}, [CVE-2023-52653](https://nvd.nist.gov/vuln/detail/CVE-2023-52653){: external}, [CVE-2023-52658](https://nvd.nist.gov/vuln/detail/CVE-2023-52658){: external}, [CVE-2023-52662](https://nvd.nist.gov/vuln/detail/CVE-2023-52662){: external}, [CVE-2023-52679](https://nvd.nist.gov/vuln/detail/CVE-2023-52679){: external}, [CVE-2023-52707](https://nvd.nist.gov/vuln/detail/CVE-2023-52707){: external}, [CVE-2023-52730](https://nvd.nist.gov/vuln/detail/CVE-2023-52730){: external}, [CVE-2023-52756](https://nvd.nist.gov/vuln/detail/CVE-2023-52756){: external}, [CVE-2023-52762](https://nvd.nist.gov/vuln/detail/CVE-2023-52762){: external}, [CVE-2023-52764](https://nvd.nist.gov/vuln/detail/CVE-2023-52764){: external}, [CVE-2023-52775](https://nvd.nist.gov/vuln/detail/CVE-2023-52775){: external}, [CVE-2023-52777](https://nvd.nist.gov/vuln/detail/CVE-2023-52777){: external}, [CVE-2023-52784](https://nvd.nist.gov/vuln/detail/CVE-2023-52784){: external}, [CVE-2023-52791](https://nvd.nist.gov/vuln/detail/CVE-2023-52791){: external}, [CVE-2023-52796](https://nvd.nist.gov/vuln/detail/CVE-2023-52796){: external}, [CVE-2023-52803](https://nvd.nist.gov/vuln/detail/CVE-2023-52803){: external}, [CVE-2023-52811](https://nvd.nist.gov/vuln/detail/CVE-2023-52811){: external}, [CVE-2023-52832](https://nvd.nist.gov/vuln/detail/CVE-2023-52832){: external}, [CVE-2023-52834](https://nvd.nist.gov/vuln/detail/CVE-2023-52834){: external}, [CVE-2023-52845](https://nvd.nist.gov/vuln/detail/CVE-2023-52845){: external}, [CVE-2023-52847](https://nvd.nist.gov/vuln/detail/CVE-2023-52847){: external}, [CVE-2023-52864](https://nvd.nist.gov/vuln/detail/CVE-2023-52864){: external}, [CVE-2024-21823](https://nvd.nist.gov/vuln/detail/CVE-2024-21823){: external}, [CVE-2024-2201](https://nvd.nist.gov/vuln/detail/CVE-2024-2201){: external}, [CVE-2024-25739](https://nvd.nist.gov/vuln/detail/CVE-2024-25739){: external}, [CVE-2024-26586](https://nvd.nist.gov/vuln/detail/CVE-2024-26586){: external}, [CVE-2024-26614](https://nvd.nist.gov/vuln/detail/CVE-2024-26614){: external}, [CVE-2024-26640](https://nvd.nist.gov/vuln/detail/CVE-2024-26640){: external}, [CVE-2024-26660](https://nvd.nist.gov/vuln/detail/CVE-2024-26660){: external}, [CVE-2024-26669](https://nvd.nist.gov/vuln/detail/CVE-2024-26669){: external}, [CVE-2024-26686](https://nvd.nist.gov/vuln/detail/CVE-2024-26686){: external}, [CVE-2024-26698](https://nvd.nist.gov/vuln/detail/CVE-2024-26698){: external}, [CVE-2024-26704](https://nvd.nist.gov/vuln/detail/CVE-2024-26704){: external}, [CVE-2024-26733](https://nvd.nist.gov/vuln/detail/CVE-2024-26733){: external}, [CVE-2024-26740](https://nvd.nist.gov/vuln/detail/CVE-2024-26740){: external}, [CVE-2024-26772](https://nvd.nist.gov/vuln/detail/CVE-2024-26772){: external}, [CVE-2024-26773](https://nvd.nist.gov/vuln/detail/CVE-2024-26773){: external}, [CVE-2024-26802](https://nvd.nist.gov/vuln/detail/CVE-2024-26802){: external}, [CVE-2024-26810](https://nvd.nist.gov/vuln/detail/CVE-2024-26810){: external}, [CVE-2024-26837](https://nvd.nist.gov/vuln/detail/CVE-2024-26837){: external}, [CVE-2024-26840](https://nvd.nist.gov/vuln/detail/CVE-2024-26840){: external}, [CVE-2024-26843](https://nvd.nist.gov/vuln/detail/CVE-2024-26843){: external}, [CVE-2024-26852](https://nvd.nist.gov/vuln/detail/CVE-2024-26852){: external}, [CVE-2024-26853](https://nvd.nist.gov/vuln/detail/CVE-2024-26853){: external}, [CVE-2024-26870](https://nvd.nist.gov/vuln/detail/CVE-2024-26870){: external}, [CVE-2024-26878](https://nvd.nist.gov/vuln/detail/CVE-2024-26878){: external}, [CVE-2024-26908](https://nvd.nist.gov/vuln/detail/CVE-2024-26908){: external}, [CVE-2024-26921](https://nvd.nist.gov/vuln/detail/CVE-2024-26921){: external}, [CVE-2024-26925](https://nvd.nist.gov/vuln/detail/CVE-2024-26925){: external}, [CVE-2024-26940](https://nvd.nist.gov/vuln/detail/CVE-2024-26940){: external}, [CVE-2024-26958](https://nvd.nist.gov/vuln/detail/CVE-2024-26958){: external}, [CVE-2024-26960](https://nvd.nist.gov/vuln/detail/CVE-2024-26960){: external}, [CVE-2024-26961](https://nvd.nist.gov/vuln/detail/CVE-2024-26961){: external}, [CVE-2024-27010](https://nvd.nist.gov/vuln/detail/CVE-2024-27010){: external}, [CVE-2024-27011](https://nvd.nist.gov/vuln/detail/CVE-2024-27011){: external}, [CVE-2024-27019](https://nvd.nist.gov/vuln/detail/CVE-2024-27019){: external}, [CVE-2024-27020](https://nvd.nist.gov/vuln/detail/CVE-2024-27020){: external}, [CVE-2024-27025](https://nvd.nist.gov/vuln/detail/CVE-2024-27025){: external}, [CVE-2024-27065](https://nvd.nist.gov/vuln/detail/CVE-2024-27065){: external}, [CVE-2024-27388](https://nvd.nist.gov/vuln/detail/CVE-2024-27388){: external}, [CVE-2024-27395](https://nvd.nist.gov/vuln/detail/CVE-2024-27395){: external}, [CVE-2024-27434](https://nvd.nist.gov/vuln/detail/CVE-2024-27434){: external}, [CVE-2024-31076](https://nvd.nist.gov/vuln/detail/CVE-2024-31076){: external}, [CVE-2024-33621](https://nvd.nist.gov/vuln/detail/CVE-2024-33621){: external}, [CVE-2024-35790](https://nvd.nist.gov/vuln/detail/CVE-2024-35790){: external}, [CVE-2024-35801](https://nvd.nist.gov/vuln/detail/CVE-2024-35801){: external}, [CVE-2024-35807](https://nvd.nist.gov/vuln/detail/CVE-2024-35807){: external}, [CVE-2024-35810](https://nvd.nist.gov/vuln/detail/CVE-2024-35810){: external}, [CVE-2024-35814](https://nvd.nist.gov/vuln/detail/CVE-2024-35814){: external}, [CVE-2024-35823](https://nvd.nist.gov/vuln/detail/CVE-2024-35823){: external}, [CVE-2024-35824](https://nvd.nist.gov/vuln/detail/CVE-2024-35824){: external}, [CVE-2024-35847](https://nvd.nist.gov/vuln/detail/CVE-2024-35847){: external}, [CVE-2024-35876](https://nvd.nist.gov/vuln/detail/CVE-2024-35876){: external}, [CVE-2024-35893](https://nvd.nist.gov/vuln/detail/CVE-2024-35893){: external}, [CVE-2024-35896](https://nvd.nist.gov/vuln/detail/CVE-2024-35896){: external}, [CVE-2024-35897](https://nvd.nist.gov/vuln/detail/CVE-2024-35897){: external}, [CVE-2024-35899](https://nvd.nist.gov/vuln/detail/CVE-2024-35899){: external}, [CVE-2024-35900](https://nvd.nist.gov/vuln/detail/CVE-2024-35900){: external}, [CVE-2024-35910](https://nvd.nist.gov/vuln/detail/CVE-2024-35910){: external}, [CVE-2024-35912](https://nvd.nist.gov/vuln/detail/CVE-2024-35912){: external}, [CVE-2024-35924](https://nvd.nist.gov/vuln/detail/CVE-2024-35924){: external}, [CVE-2024-35925](https://nvd.nist.gov/vuln/detail/CVE-2024-35925){: external}, [CVE-2024-35930](https://nvd.nist.gov/vuln/detail/CVE-2024-35930){: external}, [CVE-2024-35937](https://nvd.nist.gov/vuln/detail/CVE-2024-35937){: external}, [CVE-2024-35938](https://nvd.nist.gov/vuln/detail/CVE-2024-35938){: external}, [CVE-2024-35946](https://nvd.nist.gov/vuln/detail/CVE-2024-35946){: external}, [CVE-2024-35947](https://nvd.nist.gov/vuln/detail/CVE-2024-35947){: external}, [CVE-2024-35952](https://nvd.nist.gov/vuln/detail/CVE-2024-35952){: external}, [CVE-2024-36000](https://nvd.nist.gov/vuln/detail/CVE-2024-36000){: external}, [CVE-2024-36005](https://nvd.nist.gov/vuln/detail/CVE-2024-36005){: external}, [CVE-2024-36006](https://nvd.nist.gov/vuln/detail/CVE-2024-36006){: external}, [CVE-2024-36010](https://nvd.nist.gov/vuln/detail/CVE-2024-36010){: external}, [CVE-2024-36016](https://nvd.nist.gov/vuln/detail/CVE-2024-36016){: external}, [CVE-2024-36017](https://nvd.nist.gov/vuln/detail/CVE-2024-36017){: external}, [CVE-2024-36020](https://nvd.nist.gov/vuln/detail/CVE-2024-36020){: external}, [CVE-2024-36025](https://nvd.nist.gov/vuln/detail/CVE-2024-36025){: external}, [CVE-2024-36270](https://nvd.nist.gov/vuln/detail/CVE-2024-36270){: external}, [CVE-2024-36286](https://nvd.nist.gov/vuln/detail/CVE-2024-36286){: external}, [CVE-2024-36489](https://nvd.nist.gov/vuln/detail/CVE-2024-36489){: external}, [CVE-2024-36886](https://nvd.nist.gov/vuln/detail/CVE-2024-36886){: external}, [CVE-2024-36889](https://nvd.nist.gov/vuln/detail/CVE-2024-36889){: external}, [CVE-2024-36896](https://nvd.nist.gov/vuln/detail/CVE-2024-36896){: external}, [CVE-2024-36904](https://nvd.nist.gov/vuln/detail/CVE-2024-36904){: external}, [CVE-2024-36905](https://nvd.nist.gov/vuln/detail/CVE-2024-36905){: external}, [CVE-2024-36917](https://nvd.nist.gov/vuln/detail/CVE-2024-36917){: external}, [CVE-2024-36921](https://nvd.nist.gov/vuln/detail/CVE-2024-36921){: external}, [CVE-2024-36927](https://nvd.nist.gov/vuln/detail/CVE-2024-36927){: external}, [CVE-2024-36929](https://nvd.nist.gov/vuln/detail/CVE-2024-36929){: external}, [CVE-2024-36933](https://nvd.nist.gov/vuln/detail/CVE-2024-36933){: external}, [CVE-2024-36940](https://nvd.nist.gov/vuln/detail/CVE-2024-36940){: external}, [CVE-2024-36941](https://nvd.nist.gov/vuln/detail/CVE-2024-36941){: external}, [CVE-2024-36945](https://nvd.nist.gov/vuln/detail/CVE-2024-36945){: external}, [CVE-2024-36950](https://nvd.nist.gov/vuln/detail/CVE-2024-36950){: external}, [CVE-2024-36954](https://nvd.nist.gov/vuln/detail/CVE-2024-36954){: external}, [CVE-2024-36960](https://nvd.nist.gov/vuln/detail/CVE-2024-36960){: external}, [CVE-2024-36971](https://nvd.nist.gov/vuln/detail/CVE-2024-36971){: external}, [CVE-2024-36978](https://nvd.nist.gov/vuln/detail/CVE-2024-36978){: external}, [CVE-2024-36979](https://nvd.nist.gov/vuln/detail/CVE-2024-36979){: external}, [CVE-2024-38538](https://nvd.nist.gov/vuln/detail/CVE-2024-38538){: external}, [CVE-2024-38555](https://nvd.nist.gov/vuln/detail/CVE-2024-38555){: external}, [CVE-2024-38573](https://nvd.nist.gov/vuln/detail/CVE-2024-38573){: external}, [CVE-2024-38575](https://nvd.nist.gov/vuln/detail/CVE-2024-38575){: external}, [CVE-2024-38596](https://nvd.nist.gov/vuln/detail/CVE-2024-38596){: external}, [CVE-2024-38598](https://nvd.nist.gov/vuln/detail/CVE-2024-38598){: external}, [CVE-2024-38615](https://nvd.nist.gov/vuln/detail/CVE-2024-38615){: external}, [CVE-2024-38627](https://nvd.nist.gov/vuln/detail/CVE-2024-38627){: external}, [CVE-2024-39276](https://nvd.nist.gov/vuln/detail/CVE-2024-39276){: external}, [CVE-2024-39472](https://nvd.nist.gov/vuln/detail/CVE-2024-39472){: external}, [CVE-2024-39476](https://nvd.nist.gov/vuln/detail/CVE-2024-39476){: external}, [CVE-2024-39487](https://nvd.nist.gov/vuln/detail/CVE-2024-39487){: external}, [CVE-2024-39502](https://nvd.nist.gov/vuln/detail/CVE-2024-39502){: external}, [CVE-2024-40927](https://nvd.nist.gov/vuln/detail/CVE-2024-40927){: external}, [CVE-2024-40974](https://nvd.nist.gov/vuln/detail/CVE-2024-40974){: external}, [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043){: external}, [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/CVE-2024-0690){: external}. |

{: caption="Changes since version 4.13.45_1586_openshift" caption-side="bottom"}


### Change log for master fix pack 4.13.45_1585_openshift, released 31 July 2024
{: #41345_1585_openshift_M}

The following table shows the changes that are in the master fix pack 4.13.45_1585_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.27.2 | v3.27.4 | See the [Calico release notes](https://docs.tigera.io/calico/3.27/release-notes/#v3.27.4){: external}. |
| Cluster health image | v1.5.6 | v1.5.7 | New version contains updates and security fixes. |
| etcd | v3.5.13 | v3.5.14 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.14){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1595 | 1598 | New version contains security fixes. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.20 | v2.4.23 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.26.15-20 | v1.26.15-27 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor | 443 | 445 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 14d0ab5 | 312030f | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.11 | v2.8.12 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2933 | 2967 | New version contains updates and security fixes. |
| OpenVPN client | 2.6.8-r0-IKS-130 | 2.6.11-r0-IKS-145 | New version contains updates and security fixes. |
| OpenVPN server | 2.6.8-r0-IKS-131 | 2.6.11-r0-IKS-144 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.5.16 | v1.5.18 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.16 | v0.13.17 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.17){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.13.43 | 4.13.45 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-45){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | 4.13.0+20240603 | 4.13.0+20240709 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.13.0+20240709){: external}. |
| Tigera Operator | v1.32.5 | v1.32.10 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.32.10){: external}. |
{: caption="Changes since version 4.13.43_1577_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.45_1586_openshift, released 29 July 2024
{: #41345_1586_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.45_1586_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages | N/A | N/A | Package updates for [RHSA-2024:4620](https://access.redhat.com/errata/RHSA-2024:4620){: external}, [CVE-2024-5564](https://nvd.nist.gov/vuln/detail/CVE-2024-5564){: external}, [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043){: external}, [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/CVE-2024-0690){: external}. |
| Haproxy | N/A | N/A | N/A |
| {{site.data.keyword.openshiftshort}}. | 4.13.44 | 4.13.45 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-45){: external}. |
{: caption="Changes since version 4.13.44_1580_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.44_1580_openshift, released 15 July 2024
{: #41344_1580_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.44_1580_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages | 4.18.0-553.5.1.el8_10 | 4.18.0-553.8.1.el8_10 | Worker node kernel & package updates for [RHSA-2024:4211](https://access.redhat.com/errata/RHSA-2024:4211){: external}, [CVE-2020-26555](https://nvd.nist.gov/vuln/detail/CVE-2020-26555){: external}, [CVE-2021-46909](https://nvd.nist.gov/vuln/detail/CVE-2021-46909){: external}, [CVE-2021-46972](https://nvd.nist.gov/vuln/detail/CVE-2021-46972){: external}, [CVE-2021-47069](https://nvd.nist.gov/vuln/detail/CVE-2021-47069){: external}, [CVE-2021-47073](https://nvd.nist.gov/vuln/detail/CVE-2021-47073){: external}, [CVE-2021-47236](https://nvd.nist.gov/vuln/detail/CVE-2021-47236){: external}, [CVE-2021-47310](https://nvd.nist.gov/vuln/detail/CVE-2021-47310){: external}, [CVE-2021-47311](https://nvd.nist.gov/vuln/detail/CVE-2021-47311){: external}, [CVE-2021-47353](https://nvd.nist.gov/vuln/detail/CVE-2021-47353){: external}, [CVE-2021-47356](https://nvd.nist.gov/vuln/detail/CVE-2021-47356){: external}, [CVE-2021-47456](https://nvd.nist.gov/vuln/detail/CVE-2021-47456){: external}, [CVE-2021-47495](https://nvd.nist.gov/vuln/detail/CVE-2021-47495){: external}, [CVE-2023-5090](https://nvd.nist.gov/vuln/detail/CVE-2023-5090){: external}, [CVE-2023-52464](https://nvd.nist.gov/vuln/detail/CVE-2023-52464){: external}, [CVE-2023-52560](https://nvd.nist.gov/vuln/detail/CVE-2023-52560){: external}, [CVE-2023-52615](https://nvd.nist.gov/vuln/detail/CVE-2023-52615){: external}, [CVE-2023-52626](https://nvd.nist.gov/vuln/detail/CVE-2023-52626){: external}, [CVE-2023-52667](https://nvd.nist.gov/vuln/detail/CVE-2023-52667){: external}, [CVE-2023-52669](https://nvd.nist.gov/vuln/detail/CVE-2023-52669){: external}, [CVE-2023-52675](https://nvd.nist.gov/vuln/detail/CVE-2023-52675){: external}, [CVE-2023-52686](https://nvd.nist.gov/vuln/detail/CVE-2023-52686){: external}, [CVE-2023-52700](https://nvd.nist.gov/vuln/detail/CVE-2023-52700){: external}, [CVE-2023-52703](https://nvd.nist.gov/vuln/detail/CVE-2023-52703){: external}, [CVE-2023-52781](https://nvd.nist.gov/vuln/detail/CVE-2023-52781){: external}, [CVE-2023-52813](https://nvd.nist.gov/vuln/detail/CVE-2023-52813){: external}, [CVE-2023-52835](https://nvd.nist.gov/vuln/detail/CVE-2023-52835){: external}, [CVE-2023-52877](https://nvd.nist.gov/vuln/detail/CVE-2023-52877){: external}, [CVE-2023-52878](https://nvd.nist.gov/vuln/detail/CVE-2023-52878){: external}, [CVE-2023-52881](https://nvd.nist.gov/vuln/detail/CVE-2023-52881){: external}, [CVE-2024-26583](https://nvd.nist.gov/vuln/detail/CVE-2024-26583){: external}, [CVE-2024-26584](https://nvd.nist.gov/vuln/detail/CVE-2024-26584){: external}, [CVE-2024-26585](https://nvd.nist.gov/vuln/detail/CVE-2024-26585){: external}, [CVE-2024-26656](https://nvd.nist.gov/vuln/detail/CVE-2024-26656){: external}, [CVE-2024-26675](https://nvd.nist.gov/vuln/detail/CVE-2024-26675){: external}, [CVE-2024-26735](https://nvd.nist.gov/vuln/detail/CVE-2024-26735){: external}, [CVE-2024-26759](https://nvd.nist.gov/vuln/detail/CVE-2024-26759){: external}, [CVE-2024-26801](https://nvd.nist.gov/vuln/detail/CVE-2024-26801){: external}, [CVE-2024-26804](https://nvd.nist.gov/vuln/detail/CVE-2024-26804){: external}, [CVE-2024-26826](https://nvd.nist.gov/vuln/detail/CVE-2024-26826){: external}, [CVE-2024-26859](https://nvd.nist.gov/vuln/detail/CVE-2024-26859){: external}, [CVE-2024-26906](https://nvd.nist.gov/vuln/detail/CVE-2024-26906){: external}, [CVE-2024-26907](https://nvd.nist.gov/vuln/detail/CVE-2024-26907){: external}, [CVE-2024-26974](https://nvd.nist.gov/vuln/detail/CVE-2024-26974){: external}, [CVE-2024-26982](https://nvd.nist.gov/vuln/detail/CVE-2024-26982){: external}, [CVE-2024-27397](https://nvd.nist.gov/vuln/detail/CVE-2024-27397){: external}, [CVE-2024-27410](https://nvd.nist.gov/vuln/detail/CVE-2024-27410){: external}, [CVE-2024-35789](https://nvd.nist.gov/vuln/detail/CVE-2024-35789){: external}, [CVE-2024-35835](https://nvd.nist.gov/vuln/detail/CVE-2024-35835){: external}, [CVE-2024-35838](https://nvd.nist.gov/vuln/detail/CVE-2024-35838){: external}, [CVE-2024-35845](https://nvd.nist.gov/vuln/detail/CVE-2024-35845){: external}, [CVE-2024-35852](https://nvd.nist.gov/vuln/detail/CVE-2024-35852){: external}, [CVE-2024-35853](https://nvd.nist.gov/vuln/detail/CVE-2024-35853){: external}, [CVE-2024-35854](https://nvd.nist.gov/vuln/detail/CVE-2024-35854){: external}, [CVE-2024-35855](https://nvd.nist.gov/vuln/detail/CVE-2024-35855){: external}, [CVE-2024-35888](https://nvd.nist.gov/vuln/detail/CVE-2024-35888){: external}, [CVE-2024-35890](https://nvd.nist.gov/vuln/detail/CVE-2024-35890){: external}, [CVE-2024-35958](https://nvd.nist.gov/vuln/detail/CVE-2024-35958){: external}, [CVE-2024-35959](https://nvd.nist.gov/vuln/detail/CVE-2024-35959){: external}, [CVE-2024-35960](https://nvd.nist.gov/vuln/detail/CVE-2024-35960){: external}, [CVE-2024-36004](https://nvd.nist.gov/vuln/detail/CVE-2024-36004){: external}, [CVE-2024-36007](https://nvd.nist.gov/vuln/detail/CVE-2024-36007){: external}, [RHSA-2024:4256](https://access.redhat.com/errata/RHSA-2024:4256){: external}, [CVE-2022-48624](https://nvd.nist.gov/vuln/detail/CVE-2022-48624){: external}, [CVE-2024-32487](https://nvd.nist.gov/vuln/detail/CVE-2024-32487){: external}, [RHSA-2024:4249](https://access.redhat.com/errata/RHSA-2024:4249){: external}, [CVE-2024-25629](https://nvd.nist.gov/vuln/detail/CVE-2024-25629){: external}, [RHSA-2024:4264](https://access.redhat.com/errata/RHSA-2024:4264){: external}, [CVE-2023-2953](https://nvd.nist.gov/vuln/detail/CVE-2023-2953){: external}, [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043){: external}, [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/CVE-2024-0690){: external}, [RHSA-2024:4262](https://access.redhat.com/errata/RHSA-2024:4262){: external}, [CVE-2023-31346](https://nvd.nist.gov/vuln/detail/CVE-2023-31346){: external}, [RHSA-2024:4252](https://access.redhat.com/errata/RHSA-2024:4252){: external}, [CVE-2024-28182](https://nvd.nist.gov/vuln/detail/CVE-2024-28182){: external}, [RHSA-2024:4260](https://access.redhat.com/errata/RHSA-2024:4260){: external}, [CVE-2024-3651](https://nvd.nist.gov/vuln/detail/CVE-2024-3651){: external}, [RHSA-2024:4231](https://access.redhat.com/errata/RHSA-2024:4231){: external}, [CVE-2024-34064](https://nvd.nist.gov/vuln/detail/CVE-2024-34064){: external}. |
| HAProxy | e77d4ca | c91c765 | Security fixes for [CVE-2024-28182](https://nvd.nist.gov/vuln/detail/CVE-2023-2953){: external},[CVE-2024-25062](https://nvd.nist.gov/vuln/detail/CVE-2024-28182){: external}. |
{: caption="Changes since version 4.13.44_1579_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.44_1579_openshift, released 09 July 2024
{: #41344_1579_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.44_1579_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.43 | 4.13.44 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-44){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-553.5.1.el8_10 | [RHSA-2024:3271](https://access.redhat.com/errata/RHSA-2024:3271){: external}, [CVE-2023-4408](https://nvd.nist.gov/vuln/detail/CVE-2023-4408){: external}, [CVE-2023-50387](https://nvd.nist.gov/vuln/detail/CVE-2023-50387){: external}, [CVE-2023-50868](https://nvd.nist.gov/vuln/detail/CVE-2023-50868){: external}, [RHSA-2024:3254](https://access.redhat.com/errata/RHSA-2024:3254){: external}, [CVE-2022-2880](https://nvd.nist.gov/vuln/detail/CVE-2022-2880){: external}, [CVE-2022-41715](https://nvd.nist.gov/vuln/detail/CVE-2022-41715){: external}, [CVE-2024-1753](https://nvd.nist.gov/vuln/detail/CVE-2024-1753){: external}, [CVE-2024-24786](https://nvd.nist.gov/vuln/detail/CVE-2024-24786){: external}, [CVE-2024-28180](https://nvd.nist.gov/vuln/detail/CVE-2024-28180){: external}, [RHSA-2024:4084](https://access.redhat.com/errata/RHSA-2024:4084){: external}, [CVE-2024-32002](https://nvd.nist.gov/vuln/detail/CVE-2024-32002){: external}, [CVE-2024-32004](https://nvd.nist.gov/vuln/detail/CVE-2024-32004){: external}, [CVE-2024-32020](https://nvd.nist.gov/vuln/detail/CVE-2024-32020){: external}, [CVE-2024-32021](https://nvd.nist.gov/vuln/detail/CVE-2024-32021){: external}, [CVE-2024-32465](https://nvd.nist.gov/vuln/detail/CVE-2024-32465){: external}, [RHSA-2024:3269](https://access.redhat.com/errata/RHSA-2024:3269){: external}, [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961){: external}, [RHSA-2024:3344](https://access.redhat.com/errata/RHSA-2024:3344){: external}, [CVE-2024-33599](https://nvd.nist.gov/vuln/detail/CVE-2024-33599){: external}, [CVE-2024-33600](https://nvd.nist.gov/vuln/detail/CVE-2024-33600){: external}, [CVE-2024-33601](https://nvd.nist.gov/vuln/detail/CVE-2024-33601){: external}, [CVE-2024-33602](https://nvd.nist.gov/vuln/detail/CVE-2024-33602){: external}, [RHSA-2024:3178](https://access.redhat.com/errata/RHSA-2024:3178){: external}, [CVE-2022-46329](https://nvd.nist.gov/vuln/detail/CVE-2022-46329){: external}, [CVE-2023-20592](https://nvd.nist.gov/vuln/detail/CVE-2023-20592){: external}, [RHSA-2024:3347](https://access.redhat.com/errata/RHSA-2024:3347){: external}, [CVE-2023-6597](https://nvd.nist.gov/vuln/detail/CVE-2023-6597){: external}, [CVE-2024-0450](https://nvd.nist.gov/vuln/detail/CVE-2024-0450){: external}, [RHSA-2024:3466](https://access.redhat.com/errata/RHSA-2024:3466){: external}, [CVE-2023-6597](https://nvd.nist.gov/vuln/detail/CVE-2023-6597){: external}, [CVE-2024-0450](https://nvd.nist.gov/vuln/detail/CVE-2024-0450){: external}, [CVE-2024-3651](https://nvd.nist.gov/vuln/detail/CVE-2024-3651){: external}, [RHSA-2024:3268](https://access.redhat.com/errata/RHSA-2024:3268){: external}, [CVE-2024-26458](https://nvd.nist.gov/vuln/detail/CVE-2024-26458){: external}, [CVE-2024-26461](https://nvd.nist.gov/vuln/detail/CVE-2024-26461){: external}, [RHSA-2024:3233](https://access.redhat.com/errata/RHSA-2024:3233){: external}, [CVE-2023-6004](https://nvd.nist.gov/vuln/detail/CVE-2023-6004){: external}, [CVE-2023-6918](https://nvd.nist.gov/vuln/detail/CVE-2023-6918){: external}, [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043){: external}, [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/CVE-2024-0690){: external}, [RHSA-2024:3968](https://access.redhat.com/errata/RHSA-2024:3968){: external}, [CVE-2024-28176](https://nvd.nist.gov/vuln/detail/CVE-2024-28176){: external}, [CVE-2024-28180](https://nvd.nist.gov/vuln/detail/CVE-2024-28180){: external}, [RHSA-2024:2988](https://access.redhat.com/errata/RHSA-2024:2988){: external}, [CVE-2018-25091](https://nvd.nist.gov/vuln/detail/CVE-2018-25091){: external}, [CVE-2021-33198](https://nvd.nist.gov/vuln/detail/CVE-2021-33198){: external}, [CVE-2021-34558](https://nvd.nist.gov/vuln/detail/CVE-2021-34558){: external}, [CVE-2022-2879](https://nvd.nist.gov/vuln/detail/CVE-2022-2879){: external}, [CVE-2022-2880](https://nvd.nist.gov/vuln/detail/CVE-2022-2880){: external}, [CVE-2022-41715](https://nvd.nist.gov/vuln/detail/CVE-2022-41715){: external}, [CVE-2023-29409](https://nvd.nist.gov/vuln/detail/CVE-2023-29409){: external}, [CVE-2023-39318](https://nvd.nist.gov/vuln/detail/CVE-2023-39318){: external}, [CVE-2023-39319](https://nvd.nist.gov/vuln/detail/CVE-2023-39319){: external}, [CVE-2023-39321](https://nvd.nist.gov/vuln/detail/CVE-2023-39321){: external}, [CVE-2023-39322](https://nvd.nist.gov/vuln/detail/CVE-2023-39322){: external}, [CVE-2023-39326](https://nvd.nist.gov/vuln/detail/CVE-2023-39326){: external}, [CVE-2023-45287](https://nvd.nist.gov/vuln/detail/CVE-2023-45287){: external}, [CVE-2023-45803](https://nvd.nist.gov/vuln/detail/CVE-2023-45803){: external}, [CVE-2023-48795](https://nvd.nist.gov/vuln/detail/CVE-2023-48795){: external}, [CVE-2024-23650](https://nvd.nist.gov/vuln/detail/CVE-2024-23650){: external}, [RHSA-2024:3214](https://access.redhat.com/errata/RHSA-2024:3214){: external}, [CVE-2021-43618](https://nvd.nist.gov/vuln/detail/CVE-2021-43618){: external}, [RHSA-2024:3184](https://access.redhat.com/errata/RHSA-2024:3184){: external}, [CVE-2023-4692](https://nvd.nist.gov/vuln/detail/CVE-2023-4692){: external}, [CVE-2023-4693](https://nvd.nist.gov/vuln/detail/CVE-2023-4693){: external}, [CVE-2024-1048](https://nvd.nist.gov/vuln/detail/CVE-2024-1048){: external}, [RHSA-2024:3138](https://access.redhat.com/errata/RHSA-2024:3138){: external}, [CVE-2019-13631](https://nvd.nist.gov/vuln/detail/CVE-2019-13631){: external}, [CVE-2019-15505](https://nvd.nist.gov/vuln/detail/CVE-2019-15505){: external}, [CVE-2020-25656](https://nvd.nist.gov/vuln/detail/CVE-2020-25656){: external}, [CVE-2021-3753](https://nvd.nist.gov/vuln/detail/CVE-2021-3753){: external}, [CVE-2021-4204](https://nvd.nist.gov/vuln/detail/CVE-2021-4204){: external}, [CVE-2022-0500](https://nvd.nist.gov/vuln/detail/CVE-2022-0500){: external}, [CVE-2022-23222](https://nvd.nist.gov/vuln/detail/CVE-2022-23222){: external}, [CVE-2022-3565](https://nvd.nist.gov/vuln/detail/CVE-2022-3565){: external}, [CVE-2022-45934](https://nvd.nist.gov/vuln/detail/CVE-2022-45934){: external}, [CVE-2023-1513](https://nvd.nist.gov/vuln/detail/CVE-2023-1513){: external}, [CVE-2023-24023](https://nvd.nist.gov/vuln/detail/CVE-2023-24023){: external}, [CVE-2023-25775](https://nvd.nist.gov/vuln/detail/CVE-2023-25775){: external}, [CVE-2023-28464](https://nvd.nist.gov/vuln/detail/CVE-2023-28464){: external}, [CVE-2023-31083](https://nvd.nist.gov/vuln/detail/CVE-2023-31083){: external}, [CVE-2023-3567](https://nvd.nist.gov/vuln/detail/CVE-2023-3567){: external}, [CVE-2023-37453](https://nvd.nist.gov/vuln/detail/CVE-2023-37453){: external}, [CVE-2023-38409](https://nvd.nist.gov/vuln/detail/CVE-2023-38409){: external}, [CVE-2023-39189](https://nvd.nist.gov/vuln/detail/CVE-2023-39189){: external}, [CVE-2023-39192](https://nvd.nist.gov/vuln/detail/CVE-2023-39192){: external}, [CVE-2023-39193](https://nvd.nist.gov/vuln/detail/CVE-2023-39193){: external}, [CVE-2023-39194](https://nvd.nist.gov/vuln/detail/CVE-2023-39194){: external}, [CVE-2023-39198](https://nvd.nist.gov/vuln/detail/CVE-2023-39198){: external}, [CVE-2023-4133](https://nvd.nist.gov/vuln/detail/CVE-2023-4133){: external}, [CVE-2023-4244](https://nvd.nist.gov/vuln/detail/CVE-2023-4244){: external}, [CVE-2023-42754](https://nvd.nist.gov/vuln/detail/CVE-2023-42754){: external}, [CVE-2023-42755](https://nvd.nist.gov/vuln/detail/CVE-2023-42755){: external}, [CVE-2023-45863](https://nvd.nist.gov/vuln/detail/CVE-2023-45863){: external}, [CVE-2023-51779](https://nvd.nist.gov/vuln/detail/CVE-2023-51779){: external}, [CVE-2023-51780](https://nvd.nist.gov/vuln/detail/CVE-2023-51780){: external}, [CVE-2023-52340](https://nvd.nist.gov/vuln/detail/CVE-2023-52340){: external}, [CVE-2023-52434](https://nvd.nist.gov/vuln/detail/CVE-2023-52434){: external}, [CVE-2023-52448](https://nvd.nist.gov/vuln/detail/CVE-2023-52448){: external}, [CVE-2023-52489](https://nvd.nist.gov/vuln/detail/CVE-2023-52489){: external}, [CVE-2023-52574](https://nvd.nist.gov/vuln/detail/CVE-2023-52574){: external}, [CVE-2023-52580](https://nvd.nist.gov/vuln/detail/CVE-2023-52580){: external}, [CVE-2023-52581](https://nvd.nist.gov/vuln/detail/CVE-2023-52581){: external}, [CVE-2023-52597](https://nvd.nist.gov/vuln/detail/CVE-2023-52597){: external}, [CVE-2023-52620](https://nvd.nist.gov/vuln/detail/CVE-2023-52620){: external}, [CVE-2023-6121](https://nvd.nist.gov/vuln/detail/CVE-2023-6121){: external}, [CVE-2023-6176](https://nvd.nist.gov/vuln/detail/CVE-2023-6176){: external}, [CVE-2023-6622](https://nvd.nist.gov/vuln/detail/CVE-2023-6622){: external}, [CVE-2023-6915](https://nvd.nist.gov/vuln/detail/CVE-2023-6915){: external}, [CVE-2023-6932](https://nvd.nist.gov/vuln/detail/CVE-2023-6932){: external}, [CVE-2024-0841](https://nvd.nist.gov/vuln/detail/CVE-2024-0841){: external}, [CVE-2024-25742](https://nvd.nist.gov/vuln/detail/CVE-2024-25742){: external}, [CVE-2024-25743](https://nvd.nist.gov/vuln/detail/CVE-2024-25743){: external}, [CVE-2024-26602](https://nvd.nist.gov/vuln/detail/CVE-2024-26602){: external}, [CVE-2024-26609](https://nvd.nist.gov/vuln/detail/CVE-2024-26609){: external}, [CVE-2024-26671](https://nvd.nist.gov/vuln/detail/CVE-2024-26671){: external}, [RHSA-2024:3618](https://access.redhat.com/errata/RHSA-2024:3618){: external}, [CVE-2019-25162](https://nvd.nist.gov/vuln/detail/CVE-2019-25162){: external}, [CVE-2020-36777](https://nvd.nist.gov/vuln/detail/CVE-2020-36777){: external}, [CVE-2021-46934](https://nvd.nist.gov/vuln/detail/CVE-2021-46934){: external}, [CVE-2021-47013](https://nvd.nist.gov/vuln/detail/CVE-2021-47013){: external}, [CVE-2021-47055](https://nvd.nist.gov/vuln/detail/CVE-2021-47055){: external}, [CVE-2021-47118](https://nvd.nist.gov/vuln/detail/CVE-2021-47118){: external}, [CVE-2021-47153](https://nvd.nist.gov/vuln/detail/CVE-2021-47153){: external}, [CVE-2021-47171](https://nvd.nist.gov/vuln/detail/CVE-2021-47171){: external}, [CVE-2021-47185](https://nvd.nist.gov/vuln/detail/CVE-2021-47185){: external}, [CVE-2022-48627](https://nvd.nist.gov/vuln/detail/CVE-2022-48627){: external}, [CVE-2022-48669](https://nvd.nist.gov/vuln/detail/CVE-2022-48669){: external}, [CVE-2023-52439](https://nvd.nist.gov/vuln/detail/CVE-2023-52439){: external}, [CVE-2023-52445](https://nvd.nist.gov/vuln/detail/CVE-2023-52445){: external}, [CVE-2023-52477](https://nvd.nist.gov/vuln/detail/CVE-2023-52477){: external}, [CVE-2023-52513](https://nvd.nist.gov/vuln/detail/CVE-2023-52513){: external}, [CVE-2023-52520](https://nvd.nist.gov/vuln/detail/CVE-2023-52520){: external}, [CVE-2023-52528](https://nvd.nist.gov/vuln/detail/CVE-2023-52528){: external}, [CVE-2023-52565](https://nvd.nist.gov/vuln/detail/CVE-2023-52565){: external}, [CVE-2023-52578](https://nvd.nist.gov/vuln/detail/CVE-2023-52578){: external}, [CVE-2023-52594](https://nvd.nist.gov/vuln/detail/CVE-2023-52594){: external}, [CVE-2023-52595](https://nvd.nist.gov/vuln/detail/CVE-2023-52595){: external}, [CVE-2023-52598](https://nvd.nist.gov/vuln/detail/CVE-2023-52598){: external}, [CVE-2023-52606](https://nvd.nist.gov/vuln/detail/CVE-2023-52606){: external}, [CVE-2023-52607](https://nvd.nist.gov/vuln/detail/CVE-2023-52607){: external}, [CVE-2023-52610](https://nvd.nist.gov/vuln/detail/CVE-2023-52610){: external}, [CVE-2023-6240](https://nvd.nist.gov/vuln/detail/CVE-2023-6240){: external}, [CVE-2024-0340](https://nvd.nist.gov/vuln/detail/CVE-2024-0340){: external}, [CVE-2024-23307](https://nvd.nist.gov/vuln/detail/CVE-2024-23307){: external}, [CVE-2024-25744](https://nvd.nist.gov/vuln/detail/CVE-2024-25744){: external}, [CVE-2024-26593](https://nvd.nist.gov/vuln/detail/CVE-2024-26593){: external}, [CVE-2024-26603](https://nvd.nist.gov/vuln/detail/CVE-2024-26603){: external}, [CVE-2024-26610](https://nvd.nist.gov/vuln/detail/CVE-2024-26610){: external}, [CVE-2024-26615](https://nvd.nist.gov/vuln/detail/CVE-2024-26615){: external}, [CVE-2024-26642](https://nvd.nist.gov/vuln/detail/CVE-2024-26642){: external}, [CVE-2024-26643](https://nvd.nist.gov/vuln/detail/CVE-2024-26643){: external}, [CVE-2024-26659](https://nvd.nist.gov/vuln/detail/CVE-2024-26659){: external}, [CVE-2024-26664](https://nvd.nist.gov/vuln/detail/CVE-2024-26664){: external}, [CVE-2024-26693](https://nvd.nist.gov/vuln/detail/CVE-2024-26693){: external}, [CVE-2024-26694](https://nvd.nist.gov/vuln/detail/CVE-2024-26694){: external}, [CVE-2024-26743](https://nvd.nist.gov/vuln/detail/CVE-2024-26743){: external}, [CVE-2024-26744](https://nvd.nist.gov/vuln/detail/CVE-2024-26744){: external}, [CVE-2024-26779](https://nvd.nist.gov/vuln/detail/CVE-2024-26779){: external}, [CVE-2024-26872](https://nvd.nist.gov/vuln/detail/CVE-2024-26872){: external}, [CVE-2024-26892](https://nvd.nist.gov/vuln/detail/CVE-2024-26892){: external}, [CVE-2024-26897](https://nvd.nist.gov/vuln/detail/CVE-2024-26897){: external}, [CVE-2024-26901](https://nvd.nist.gov/vuln/detail/CVE-2024-26901){: external}, [CVE-2024-26919](https://nvd.nist.gov/vuln/detail/CVE-2024-26919){: external}, [CVE-2024-26933](https://nvd.nist.gov/vuln/detail/CVE-2024-26933){: external}, [CVE-2024-26934](https://nvd.nist.gov/vuln/detail/CVE-2024-26934){: external}, [CVE-2024-26964](https://nvd.nist.gov/vuln/detail/CVE-2024-26964){: external}, [CVE-2024-26973](https://nvd.nist.gov/vuln/detail/CVE-2024-26973){: external}, [CVE-2024-26993](https://nvd.nist.gov/vuln/detail/CVE-2024-26993){: external}, [CVE-2024-27014](https://nvd.nist.gov/vuln/detail/CVE-2024-27014){: external}, [CVE-2024-27048](https://nvd.nist.gov/vuln/detail/CVE-2024-27048){: external}, [CVE-2024-27052](https://nvd.nist.gov/vuln/detail/CVE-2024-27052){: external}, [CVE-2024-27056](https://nvd.nist.gov/vuln/detail/CVE-2024-27056){: external}, [CVE-2024-27059](https://nvd.nist.gov/vuln/detail/CVE-2024-27059){: external}, [RHSA-2024:3626](https://access.redhat.com/errata/RHSA-2024:3626){: external}, [CVE-2024-25062](https://nvd.nist.gov/vuln/detail/CVE-2024-25062){: external}, [RHSA-2024:3166](https://access.redhat.com/errata/RHSA-2024:3166){: external}, [CVE-2020-15778](https://nvd.nist.gov/vuln/detail/CVE-2020-15778){: external}, [RHSA-2024:3163](https://access.redhat.com/errata/RHSA-2024:3163){: external}, [CVE-2024-22365](https://nvd.nist.gov/vuln/detail/CVE-2024-22365){: external}, [RHSA-2024:3102](https://access.redhat.com/errata/RHSA-2024:3102){: external}, [CVE-2024-22195](https://nvd.nist.gov/vuln/detail/CVE-2024-22195){: external}, [RHSA-2024:2985](https://access.redhat.com/errata/RHSA-2024:2985){: external}, [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/CVE-2022-40897){: external}, [CVE-2023-23931](https://nvd.nist.gov/vuln/detail/CVE-2023-23931){: external}, [CVE-2023-27043](https://nvd.nist.gov/vuln/detail/CVE-2023-27043){: external}, [CVE-2023-43804](https://nvd.nist.gov/vuln/detail/CVE-2023-43804){: external}, [RHSA-2024:3139](https://access.redhat.com/errata/RHSA-2024:3139){: external}, [CVE-2021-40153](https://nvd.nist.gov/vuln/detail/CVE-2021-40153){: external}, [CVE-2021-41072](https://nvd.nist.gov/vuln/detail/CVE-2021-41072){: external}, [RHSA-2024:3270](https://access.redhat.com/errata/RHSA-2024:3270){: external}, [CVE-2023-3758](https://nvd.nist.gov/vuln/detail/CVE-2023-3758){: external}, [RHSA-2024:3203](https://access.redhat.com/errata/RHSA-2024:3203){: external}, [CVE-2023-7008](https://nvd.nist.gov/vuln/detail/CVE-2023-7008){: external}. |
| HAProxy | 18889dd | e77d4ca | New version contains security fixes |
{: caption="Changes since version 4.13.43_1578_openshift" caption-side="bottom"}


### Change log for master fix pack 4.13.43_1577_openshift, released 19 June 2024
{: #41343_1577_openshift_M}

The following table shows the changes that are in the master fix pack 4.13.43_1577_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.5.5 | v1.5.6 | New version contains updates and security fixes. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1589 | 1595 | New version contains security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.26.15-16 | v1.26.15-20 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 4c5d156 | 14d0ab5 |New version contains updates and security fixes. |
| Key Management Service provider | v2.8.10 | v2.8.11 | New version contains updates and security fixes. |
| {{site.data.keyword.openshiftshort}}. | 4.13.41 | 4.13.43 | https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html |
| OpenVPN client | 2.6.8-r0-IKS-114-amd64 | 2.6.8-r0-IKS-130-amd64 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.5.15 | v1.5.16 | New version contains updates and security fixes. |
| OpenVPN server | 2.6.8-r0-IKS-113-amd64 | 2.6.8-r0-IKS-131-amd64 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.15 | v0.13.16 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.16){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | 4.13.0+20240514 | 4.13.0+20240603 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.13.0+20240603){: external}. |
{: caption="Changes since version 4.13.41_1573_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.43_1578_openshift, released 18 June 2024
{: #41343_1578_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.43_1578_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.42 | 4.13.43 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-43){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-513.24.1.el8_9 | N/A |
| HAProxy | 0062a3c | 18889dd | Security fixes for [CVE-2024-25062](https://nvd.nist.gov/vuln/detail/CVE-2024-25062){: external}. |
{: caption="Changes since version 4.13.42_1574_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.42_1574_openshift, released 03 June 2024
{: #41342_1574_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.42_1574_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.41 | 4.13.42 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-42){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-513.24.1.el8_9 | N/A |
| HAProxy | e88695e | 0062a3c | [CVE-2024-0450](https://nvd.nist.gov/vuln/detail/CVE-2024-0450){: external}, [CVE-2024-33599](https://nvd.nist.gov/vuln/detail/CVE-2024-33599){: external}, [CVE-2024-26461](https://nvd.nist.gov/vuln/detail/CVE-2024-26461){: external}, [CVE-2021-43618](https://nvd.nist.gov/vuln/detail/CVE-2021-43618){: external}, [CVE-2024-22365](https://nvd.nist.gov/vuln/detail/CVE-2024-22365){: external}, [CVE-2023-6597](https://nvd.nist.gov/vuln/detail/CVE-2023-6597){: external}, [CVE-2024-26458](https://nvd.nist.gov/vuln/detail/CVE-2024-26458){: external}, [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961){: external}, [CVE-2024-33601](https://nvd.nist.gov/vuln/detail/CVE-2024-33601){: external}, [CVE-2024-33602](https://nvd.nist.gov/vuln/detail/CVE-2024-33602){: external}, [CVE-2023-7008](https://nvd.nist.gov/vuln/detail/CVE-2023-7008){: external}, [CVE-2023-6004](https://nvd.nist.gov/vuln/detail/CVE-2023-6004){: external}, [CVE-2023-6918](https://nvd.nist.gov/vuln/detail/CVE-2023-6918){: external}, [CVE-2024-33600](https://nvd.nist.gov/vuln/detail/CVE-2024-33600){: external}. |
{: caption="Changes since version 4.13.41_1571_openshift" caption-side="bottom"}


### Change log for master fix pack 4.13.41_1573_openshift, released 29 May 2024
{: #41341_1573_openshift_M}

The following table shows the changes that are in the master fix pack 4.13.41_1573_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.26.4 | v3.27.2 | See the [Calico release notes](https://docs.tigera.io/calico/3.27/release-notes/#v3.27.2){: external}. |
| Cluster health image | v1.5.4 | v1.5.5 | New version contains updates and security fixes. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1537 | 1589 | New version contains security fixes. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.19 | v2.4.20 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.26.15-10 | v1.26.15-16 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor | 442 | 443 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.9 | v2.8.10 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2867 | 2933 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.5.14 | v1.5.15 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.13 | v0.13.15 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.15){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.13.39 | 4.13.41 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-41){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | 4.13.0+20240412 | 4.13.0+20240514 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.13.0+20240514){: external}. |
| Tigera Operator | v1.30.9 | v1.32.5 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.32.5){: external}. |
{: caption="Changes since version 4.13.39_1568_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.41_1571_openshift, released 23 May 2024
{: #41341_1571_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.41_1571_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.41 | 4.13.41 | N/A |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-513.24.1.el8_9 | Worker node package updates for [RHSA-2024:2722](https://access.redhat.com/errata/RHSA-2024:2722){: external}, [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961){: external}. |
| HAProxy | d225100 | 4e826da | [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961){: external}, [CVE-2024-28834](https://nvd.nist.gov/vuln/detail/CVE-2024-28834){: external}. |
{: caption="Changes since version 4.13.41_1570_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.41_1570_openshift, released 06 May 2024
{: #41341_1570_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.41_1570_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.40 | 4.13.41 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-41){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-513.24.1.el8_9 | Worker node package updates for [RHSA-2024:2098](https://access.redhat.com/errata/RHSA-2024:2098){: external}, [CVE-2024-1753](https://nvd.nist.gov/vuln/detail/CVE-2024-1753){: external}. |
| HAProxy | 295dba8 | 295dba8 | N/A |
{: caption="Changes since version 4.13.40_1569_openshift" caption-side="bottom"}


### Change log for master fix pack 4.13.39_1568_openshift, released 24 April 2024
{: #41339_1568_openshift_M}

The following table shows the changes that are in the master fix pack 4.13.39_1568_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.4.8 | v1.5.4 | New version contains updates and security fixes. |
| etcd | v3.5.12 | v3.5.13 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.13){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.26.15-1 | v1.26.15-10 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | bd30030 | 4c5d156 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.8 | v2.8.9 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2831 | 2867 | New version contains updates and security fixes. |
| OpenVPN client | 2.6.8-r0-IKS-110 | 2.6.8-r0-IKS-114 | New version contains updates and security fixes. |
| OpenVPN server | 2.6.8-r0-IKS-109 | 2.6.8-r0-IKS-113 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.5.13 | v1.5.14 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.12 | v0.13.13 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.13){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.13.36 | 4.13.39 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-39){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | 4.13.0+20240208 | 4.13.0+20240412 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.13.0+20240412){: external}. |
{: caption="Changes since version 4.13.36_1565_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.40_1569_openshift, released 22 April 2024
{: #41340_1569_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.40_1569_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.38 | 4.13.40 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-40){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-513.24.1.el8_9 | Worker node package updates for [RHSA-2024:1782](https://access.redhat.com/errata/RHSA-2024:1782){: external}, [CVE-2023-4408](https://nvd.nist.gov/vuln/detail/CVE-2023-4408){: external}, [CVE-2023-50387](https://nvd.nist.gov/vuln/detail/CVE-2023-50387){: external}, [CVE-2023-50868](https://nvd.nist.gov/vuln/detail/CVE-2023-50868){: external}, [RHSA-2024:1784](https://access.redhat.com/errata/RHSA-2024:1784){: external}, [CVE-2024-28834](https://nvd.nist.gov/vuln/detail/CVE-2024-28834){: external}. |
| HAProxy | 295dba8 | 4e826da | Security fixes for [CVE-2024-28834](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2024-28834){: external}. |
{: caption="Changes since version 4.13.38_1567_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.38_1567_openshift, released 8 April 2024
{: #41338_1567_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.38_1567_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.37 | 4.13.38 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-38){: external}. |
| RHEL 8 Packages | 4.18.0-513.18.1.el8_9 | 4.18.0-513.24.1.el8_9 | Worker node and kernel packages for [RHSA-2024:1607](https://access.redhat.com/errata/RHSA-2024:1607){: external}, [CVE-2021-33631](https://nvd.nist.gov/vuln/detail/CVE-2021-33631){: external}, [CVE-2022-38096](https://nvd.nist.gov/vuln/detail/CVE-2022-38096){: external}, [CVE-2023-51042](https://nvd.nist.gov/vuln/detail/CVE-2023-51042){: external}, [CVE-2023-6546](https://nvd.nist.gov/vuln/detail/CVE-2023-6546){: external}, [CVE-2023-6931](https://nvd.nist.gov/vuln/detail/CVE-2023-6931){: external}, [CVE-2024-0565](https://nvd.nist.gov/vuln/detail/CVE-2024-0565){: external}, [CVE-2024-1086](https://nvd.nist.gov/vuln/detail/CVE-2024-1086){: external}, [RHSA-2024:1601](https://access.redhat.com/errata/RHSA-2024:1601){: external}, [CVE-2023-28322](https://nvd.nist.gov/vuln/detail/CVE-2023-28322){: external}, [CVE-2023-38546](https://nvd.nist.gov/vuln/detail/CVE-2023-38546){: external}, [CVE-2023-46218](https://nvd.nist.gov/vuln/detail/CVE-2023-46218){: external}, [RHSA-2024:1615](https://access.redhat.com/errata/RHSA-2024:1615){: external}, [CVE-2023-52425](https://nvd.nist.gov/vuln/detail/CVE-2023-52425){: external}, [RHSA-2024:1610](https://access.redhat.com/errata/RHSA-2024:1610){: external}, [CVE-2022-48624](https://nvd.nist.gov/vuln/detail/CVE-2022-48624){: external}. |
| HAProxy | 512b32a | 295dba8 | Security fixes for [CVE-2023-28322](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-28322){: external}, [CVE-2023-38546](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-38546){: external}, [CVE-2023-46218](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-46218){: external}, [CVE-2023-52425](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-52425){: external}. |
| CRI-O | 1.26.5-2 | 1.26.5-2 | N/A |
{: caption="Changes since version 4.13.37_1566_openshift" caption-side="bottom"}


### Change log for master fix pack 4.13.36_1565_openshift, released 27 March 2024
{: #41336_1565_openshift_M}

The following table shows the changes that are in the master fix pack 4.13.36_1565_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.4.7 | v1.4.8 | New version contains updates and security fixes. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1534 | 1537 | New version contains security fixes. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.18 | v2.4.19 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.26.14-2 | v1.26.15-1 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 441 | 442 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.7 | v2.8.8 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2807 | 2831 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.5.12 | v1.5.13 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.11 | v0.13.12 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.12){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.13.33 | 4.13.36 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-36){: external}. |
{: caption="Changes since version 4.13.33_1562_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.37_1566_openshift, released 25 March 2024
{: #41337_1566_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.37_1566_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.36 | 4.13.37 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-13-37){: external}. |
| RHEL 8 Packages | 4.18.0-513.18.1.el8_9 | 4.18.0-513.18.1.el8_9 | N/A |
| CRI-O | 1.26.5-2 | 1.26.5-2 | N/A |
| HAProxy | 512b32 | 512b32 | N/A |
{: caption="Changes since version 4.13.36_1564_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.36_1564_openshift, released 13 March 2024
{: #41336_1564_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.36_1564_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.34 | 4.13.36 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-36){: external}. |
| RHEL 8 Packages | 4.18.0-513.18.1.el8_9 | 4.18.0-513.18.1.el8_9 | N/A |
| HAProxy | a13673 | 512b32 | N/A |
| CRI-O | 1.26.5-2 | 1.26.5-2 | N/A |
{: caption="Changes since version 4.13.34_1563_openshift" caption-side="bottom"}


### Change log for master fix pack 4.13.33_1562_openshift, released 28 February 2024
{: #41333_1562_openshift_M}

The following table shows the changes that are in the master fix pack 4.13.33_1562_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.4.6 | v1.4.7 | New version contains updates and security fixes. |
| etcd | v3.5.11 | v3.5.12 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.12){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1525 | 1534 | New version contains security fixes. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.14 | v2.4.18 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.26.13-3 | v1.26.14-2 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 439 | 441 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 7185ea1 | bd30030 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.6 | v2.8.7 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2789 | 2807 | New version contains updates and security fixes. |
| OpenVPN client | 2.6.8-r0-IKS-108 | 2.6.8-r0-IKS-110 | New version contains updates and security fixes. |
| OpenVPN server | 2.6.8-r0-IKS-107 | 2.6.8-r0-IKS-109 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.5.11 | v1.5.12 | New version contains updates and security fixes. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.13.28 | 4.13.33 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-33){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.13.0-20240104 | v4.13.0-20240208 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.13.0%2B20240208){: external}. |
{: caption="Changes since version 4.13.28_1555_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.34_1563_openshift, released 26 February 2024
{: #41334_1563_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.34_1563_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.32| 4.13.34 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-13-34){: external}. |
| RHEL 8 Packages| 4.18.0-513.11.1.el8_9 | 4.18.0-513.18.1.el8_9 | Package updates for [RHSA-2024:0897](https://access.redhat.com/errata/RHSA-2024:0897){: external}, [CVE-2022-3545](https://nvd.nist.gov/vuln/detail/CVE-2022-3545){: external}, [CVE-2022-41858](https://nvd.nist.gov/vuln/detail/CVE-2022-41858){: external}, [CVE-2023-1073](https://nvd.nist.gov/vuln/detail/CVE-2023-1073){: external}, [CVE-2023-1838](https://nvd.nist.gov/vuln/detail/CVE-2023-1838){: external}, [CVE-2023-2166](https://nvd.nist.gov/vuln/detail/CVE-2023-2166){: external}, [CVE-2023-2176](https://nvd.nist.gov/vuln/detail/CVE-2023-2176){: external}, [CVE-2023-40283](https://nvd.nist.gov/vuln/detail/CVE-2023-40283){: external}, [CVE-2023-45871](https://nvd.nist.gov/vuln/detail/CVE-2023-45871){: external}, [CVE-2023-4623](https://nvd.nist.gov/vuln/detail/CVE-2023-4623){: external}, [CVE-2023-46813](https://nvd.nist.gov/vuln/detail/CVE-2023-46813){: external}, [CVE-2023-4921](https://nvd.nist.gov/vuln/detail/CVE-2023-4921){: external}, [CVE-2023-5717](https://nvd.nist.gov/vuln/detail/CVE-2023-5717){: external}, [CVE-2023-6356](https://nvd.nist.gov/vuln/detail/CVE-2023-6356){: external}, [CVE-2023-6535](https://nvd.nist.gov/vuln/detail/CVE-2023-6535){: external}, [CVE-2023-6536](https://nvd.nist.gov/vuln/detail/CVE-2023-6536){: external}, [CVE-2023-6606](https://nvd.nist.gov/vuln/detail/CVE-2023-6606){: external}, [CVE-2023-6610](https://nvd.nist.gov/vuln/detail/CVE-2023-6610){: external}, [CVE-2023-6817](https://nvd.nist.gov/vuln/detail/CVE-2023-6817){: external}, [CVE-2024-0646](https://nvd.nist.gov/vuln/detail/CVE-2024-0646){: external}, [RHSA-2024:0768](https://access.redhat.com/errata/RHSA-2024:0768){: external}, [CVE-2020-28241](https://nvd.nist.gov/vuln/detail/CVE-2020-28241){: external}, [RHSA-2024:0889](https://access.redhat.com/errata/RHSA-2024:0889){: external}, [CVE-2019-13224](https://nvd.nist.gov/vuln/detail/CVE-2019-13224){: external}, [CVE-2019-16163](https://nvd.nist.gov/vuln/detail/CVE-2019-16163){: external}, [CVE-2019-19012](https://nvd.nist.gov/vuln/detail/CVE-2019-19012){: external}, [CVE-2019-19203](https://nvd.nist.gov/vuln/detail/CVE-2019-19203){: external}, [CVE-2019-19204](https://nvd.nist.gov/vuln/detail/CVE-2019-19204){: external}, [RHSA-2024:0811](https://access.redhat.com/errata/RHSA-2024:0811){: external}, [CVE-2023-28486](https://nvd.nist.gov/vuln/detail/CVE-2023-28486){: external}, [CVE-2023-28487](https://nvd.nist.gov/vuln/detail/CVE-2023-28487){: external}, [CVE-2023-42465](https://nvd.nist.gov/vuln/detail/CVE-2023-42465){: external}. |
{: caption="Changes since version 4.13.32_1557_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.32_1557_openshift, released 12 February 2024
{: #41332_1557_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.32_1557_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.30 | 4.13.32 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-32){: external}. |
| RHEL 8 Packages | 4.18.0-477.27.1.el8_8 | 4.18.0-513.11.1.el8_9 | Package updates for [RHSA-2024:0752](https://access.redhat.com/errata/RHSA-2024:0752){: external}, [CVE-2024-21626](https://nvd.nist.gov/vuln/detail/CVE-2024-21626){: external}, [RHSA-2023:7549](https://access.redhat.com/errata/RHSA-2023:7549){: external}, [CVE-2022-45884](https://nvd.nist.gov/vuln/detail/CVE-2022-45884){: external}, [CVE-2022-45886](https://nvd.nist.gov/vuln/detail/CVE-2022-45886){: external}, [CVE-2022-45919](https://nvd.nist.gov/vuln/detail/CVE-2022-45919){: external}, [CVE-2023-1192](https://nvd.nist.gov/vuln/detail/CVE-2023-1192){: external}, [CVE-2023-2163](https://nvd.nist.gov/vuln/detail/CVE-2023-2163){: external}, [CVE-2023-3812](https://nvd.nist.gov/vuln/detail/CVE-2023-3812){: external}, [CVE-2023-5178](https://nvd.nist.gov/vuln/detail/CVE-2023-5178){: external}, [RHSA-2024:0113](https://access.redhat.com/errata/RHSA-2024:0113){: external}, [CVE-2022-36402](https://nvd.nist.gov/vuln/detail/CVE-2022-36402){: external}, [CVE-2023-20569](https://nvd.nist.gov/vuln/detail/CVE-2023-20569){: external}, [CVE-2023-2162](https://nvd.nist.gov/vuln/detail/CVE-2023-2162){: external}, [CVE-2023-42753](https://nvd.nist.gov/vuln/detail/CVE-2023-42753){: external}, [CVE-2023-4622](https://nvd.nist.gov/vuln/detail/CVE-2023-4622){: external}, [CVE-2023-5633](https://nvd.nist.gov/vuln/detail/CVE-2023-5633){: external}, [RHSA-2023:7077](https://access.redhat.com/errata/RHSA-2023:7077){: external}, [CVE-2021-43975](https://nvd.nist.gov/vuln/detail/CVE-2021-43975){: external}, [CVE-2022-28388](https://nvd.nist.gov/vuln/detail/CVE-2022-28388){: external}, [CVE-2022-3594](https://nvd.nist.gov/vuln/detail/CVE-2022-3594){: external}, [CVE-2022-3640](https://nvd.nist.gov/vuln/detail/CVE-2022-3640){: external}, [CVE-2022-38457](https://nvd.nist.gov/vuln/detail/CVE-2022-38457){: external}, [CVE-2022-40133](https://nvd.nist.gov/vuln/detail/CVE-2022-40133){: external}, [CVE-2022-40982](https://nvd.nist.gov/vuln/detail/CVE-2022-40982){: external}, [CVE-2022-42895](https://nvd.nist.gov/vuln/detail/CVE-2022-42895){: external}, [CVE-2022-45869](https://nvd.nist.gov/vuln/detail/CVE-2022-45869){: external}, [CVE-2022-45887](https://nvd.nist.gov/vuln/detail/CVE-2022-45887){: external}, [CVE-2022-4744](https://nvd.nist.gov/vuln/detail/CVE-2022-4744){: external}, [CVE-2023-0458](https://nvd.nist.gov/vuln/detail/CVE-2023-0458){: external}, [CVE-2023-0590](https://nvd.nist.gov/vuln/detail/CVE-2023-0590){: external}, [CVE-2023-0597](https://nvd.nist.gov/vuln/detail/CVE-2023-0597){: external}, [CVE-2023-1073](https://nvd.nist.gov/vuln/detail/CVE-2023-1073){: external}, [CVE-2023-1074](https://nvd.nist.gov/vuln/detail/CVE-2023-1074){: external}, [CVE-2023-1075](https://nvd.nist.gov/vuln/detail/CVE-2023-1075){: external}, [CVE-2023-1079](https://nvd.nist.gov/vuln/detail/CVE-2023-1079){: external}, [CVE-2023-1118](https://nvd.nist.gov/vuln/detail/CVE-2023-1118){: external}, [CVE-2023-1206](https://nvd.nist.gov/vuln/detail/CVE-2023-1206){: external}, [CVE-2023-1252](https://nvd.nist.gov/vuln/detail/CVE-2023-1252){: external}, [CVE-2023-1382](https://nvd.nist.gov/vuln/detail/CVE-2023-1382){: external}, [CVE-2023-1855](https://nvd.nist.gov/vuln/detail/CVE-2023-1855){: external}, [CVE-2023-1989](https://nvd.nist.gov/vuln/detail/CVE-2023-1989){: external}, [CVE-2023-1998](https://nvd.nist.gov/vuln/detail/CVE-2023-1998){: external}, [CVE-2023-2269](https://nvd.nist.gov/vuln/detail/CVE-2023-2269){: external}, [CVE-2023-23455](https://nvd.nist.gov/vuln/detail/CVE-2023-23455){: external}, [CVE-2023-2513](https://nvd.nist.gov/vuln/detail/CVE-2023-2513){: external}, [CVE-2023-26545](https://nvd.nist.gov/vuln/detail/CVE-2023-26545){: external}, [CVE-2023-28328](https://nvd.nist.gov/vuln/detail/CVE-2023-28328){: external}, [CVE-2023-28772](https://nvd.nist.gov/vuln/detail/CVE-2023-28772){: external}, [CVE-2023-30456](https://nvd.nist.gov/vuln/detail/CVE-2023-30456){: external}, [CVE-2023-31084](https://nvd.nist.gov/vuln/detail/CVE-2023-31084){: external}, [CVE-2023-3141](https://nvd.nist.gov/vuln/detail/CVE-2023-3141){: external}, [CVE-2023-31436](https://nvd.nist.gov/vuln/detail/CVE-2023-31436){: external}, [CVE-2023-3161](https://nvd.nist.gov/vuln/detail/CVE-2023-3161){: external}, [CVE-2023-3212](https://nvd.nist.gov/vuln/detail/CVE-2023-3212){: external}, [CVE-2023-3268](https://nvd.nist.gov/vuln/detail/CVE-2023-3268){: external}, [CVE-2023-33203](https://nvd.nist.gov/vuln/detail/CVE-2023-33203){: external}, [CVE-2023-33951](https://nvd.nist.gov/vuln/detail/CVE-2023-33951){: external}, [CVE-2023-33952](https://nvd.nist.gov/vuln/detail/CVE-2023-33952){: external}, [CVE-2023-35823](https://nvd.nist.gov/vuln/detail/CVE-2023-35823){: external}, [CVE-2023-35824](https://nvd.nist.gov/vuln/detail/CVE-2023-35824){: external}, [CVE-2023-35825](https://nvd.nist.gov/vuln/detail/CVE-2023-35825){: external}, [CVE-2023-3609](https://nvd.nist.gov/vuln/detail/CVE-2023-3609){: external}, [CVE-2023-3611](https://nvd.nist.gov/vuln/detail/CVE-2023-3611){: external}, [CVE-2023-3772](https://nvd.nist.gov/vuln/detail/CVE-2023-3772){: external}, [CVE-2023-4128](https://nvd.nist.gov/vuln/detail/CVE-2023-4128){: external}, [CVE-2023-4132](https://nvd.nist.gov/vuln/detail/CVE-2023-4132){: external}, [CVE-2023-4155](https://nvd.nist.gov/vuln/detail/CVE-2023-4155){: external}, [CVE-2023-4206](https://nvd.nist.gov/vuln/detail/CVE-2023-4206){: external}, [CVE-2023-4207](https://nvd.nist.gov/vuln/detail/CVE-2023-4207){: external}, [CVE-2023-4208](https://nvd.nist.gov/vuln/detail/CVE-2023-4208){: external}, [CVE-2023-4732](https://nvd.nist.gov/vuln/detail/CVE-2023-4732){: external}, [CVE-2024-0443](https://nvd.nist.gov/vuln/detail/CVE-2024-0443){: external}, [RHSA-2023:7877](https://access.redhat.com/errata/RHSA-2023:7877){: external}, [CVE-2023-3446](https://nvd.nist.gov/vuln/detail/CVE-2023-3446){: external}, [CVE-2023-3817](https://nvd.nist.gov/vuln/detail/CVE-2023-3817){: external}, [CVE-2023-5678](https://nvd.nist.gov/vuln/detail/CVE-2023-5678){: external}, [RHSA-2023:7187](https://access.redhat.com/errata/RHSA-2023:7187){: external}, [CVE-2023-4016](https://nvd.nist.gov/vuln/detail/CVE-2023-4016){: external}, [RHSA-2023:7112](https://access.redhat.com/errata/RHSA-2023:7112){: external}, [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/CVE-2023-4641){: external}, [RHSA-2023:7166](https://access.redhat.com/errata/RHSA-2023:7166){: external}, [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/CVE-2023-22745){: external}, [RHSA-2023:7177](https://access.redhat.com/errata/RHSA-2023:7177){: external}, [CVE-2022-3094](https://nvd.nist.gov/vuln/detail/CVE-2022-3094){: external}, [RHSA-2023:7116](https://access.redhat.com/errata/RHSA-2023:7116){: external}, [CVE-2022-4904](https://nvd.nist.gov/vuln/detail/CVE-2022-4904){: external}, [RHSA-2023:7207](https://access.redhat.com/errata/RHSA-2023:7207){: external}, [CVE-2020-22217](https://nvd.nist.gov/vuln/detail/CVE-2020-22217){: external}, [CVE-2023-31130](https://nvd.nist.gov/vuln/detail/CVE-2023-31130){: external}, [RHSA-2023:6943](https://access.redhat.com/errata/RHSA-2023:6943){: external}, [CVE-2023-1786](https://nvd.nist.gov/vuln/detail/CVE-2023-1786){: external}, [RHSA-2023:6939](https://access.redhat.com/errata/RHSA-2023:6939){: external}, [CVE-2022-3064](https://nvd.nist.gov/vuln/detail/CVE-2022-3064){: external}, [CVE-2022-41723](https://nvd.nist.gov/vuln/detail/CVE-2022-41723){: external}, [CVE-2022-41724](https://nvd.nist.gov/vuln/detail/CVE-2022-41724){: external}, [CVE-2022-41725](https://nvd.nist.gov/vuln/detail/CVE-2022-41725){: external}, [CVE-2023-24534](https://nvd.nist.gov/vuln/detail/CVE-2023-24534){: external}, [CVE-2023-24536](https://nvd.nist.gov/vuln/detail/CVE-2023-24536){: external}, [CVE-2023-24537](https://nvd.nist.gov/vuln/detail/CVE-2023-24537){: external}, [CVE-2023-24538](https://nvd.nist.gov/vuln/detail/CVE-2023-24538){: external}, [CVE-2023-24539](https://nvd.nist.gov/vuln/detail/CVE-2023-24539){: external}, [CVE-2023-24540](https://nvd.nist.gov/vuln/detail/CVE-2023-24540){: external}, [CVE-2023-25173](https://nvd.nist.gov/vuln/detail/CVE-2023-25173){: external}, [CVE-2023-25809](https://nvd.nist.gov/vuln/detail/CVE-2023-25809){: external}, [CVE-2023-27561](https://nvd.nist.gov/vuln/detail/CVE-2023-27561){: external}, [CVE-2023-28642](https://nvd.nist.gov/vuln/detail/CVE-2023-28642){: external}, [CVE-2023-29400](https://nvd.nist.gov/vuln/detail/CVE-2023-29400){: external}, [CVE-2023-29406](https://nvd.nist.gov/vuln/detail/CVE-2023-29406){: external}, [CVE-2023-3978](https://nvd.nist.gov/vuln/detail/CVE-2023-3978){: external}, [RHSA-2024:0155](https://access.redhat.com/errata/RHSA-2024:0155){: external}, [CVE-2023-5981](https://nvd.nist.gov/vuln/detail/CVE-2023-5981){: external}, [RHSA-2024:0627](https://access.redhat.com/errata/RHSA-2024:0627){: external}, [CVE-2024-0553](https://nvd.nist.gov/vuln/detail/CVE-2024-0553){: external}, [RHSA-2023:6976](https://access.redhat.com/errata/RHSA-2023:6976){: external}, [CVE-2020-12762](https://nvd.nist.gov/vuln/detail/CVE-2020-12762){: external}, [RHSA-2024:0628](https://access.redhat.com/errata/RHSA-2024:0628){: external}, [CVE-2023-48795](https://nvd.nist.gov/vuln/detail/CVE-2023-48795){: external}, [RHSA-2024:0119](https://access.redhat.com/errata/RHSA-2024:0119){: external}, [CVE-2023-39615](https://nvd.nist.gov/vuln/detail/CVE-2023-39615){: external}, [RHSA-2023:7109](https://access.redhat.com/errata/RHSA-2023:7109){: external}, [CVE-2023-20569](https://nvd.nist.gov/vuln/detail/CVE-2023-20569){: external}, [RHSA-2024:0606](https://access.redhat.com/errata/RHSA-2024:0606){: external}, [CVE-2023-48795](https://nvd.nist.gov/vuln/detail/CVE-2023-48795){: external}, [CVE-2023-51385](https://nvd.nist.gov/vuln/detail/CVE-2023-51385){: external}, [RHSA-2023:7174](https://access.redhat.com/errata/RHSA-2023:7174){: external}, [CVE-2023-31486](https://nvd.nist.gov/vuln/detail/CVE-2023-31486){: external}, [RHSA-2023:6944](https://access.redhat.com/errata/RHSA-2023:6944){: external}, [CVE-2022-48468](https://nvd.nist.gov/vuln/detail/CVE-2022-48468){: external}, [RHSA-2023:7096](https://access.redhat.com/errata/RHSA-2023:7096){: external}, [CVE-2023-23931](https://nvd.nist.gov/vuln/detail/CVE-2023-23931){: external}, [RHSA-2023:7176](https://access.redhat.com/errata/RHSA-2023:7176){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [RHSA-2024:0116](https://access.redhat.com/errata/RHSA-2024:0116){: external}, [CVE-2023-43804](https://nvd.nist.gov/vuln/detail/CVE-2023-43804){: external}, [CVE-2023-45803](https://nvd.nist.gov/vuln/detail/CVE-2023-45803){: external}, [RHSA-2023:7151](https://access.redhat.com/errata/RHSA-2023:7151){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [RHSA-2024:0114](https://access.redhat.com/errata/RHSA-2024:0114){: external}, [CVE-2022-48560](https://nvd.nist.gov/vuln/detail/CVE-2022-48560){: external}, [CVE-2022-48564](https://nvd.nist.gov/vuln/detail/CVE-2022-48564){: external}, [RHSA-2024:0256](https://access.redhat.com/errata/RHSA-2024:0256){: external}, [CVE-2023-27043](https://nvd.nist.gov/vuln/detail/CVE-2023-27043){: external}, [RHSA-2023:7034](https://access.redhat.com/errata/RHSA-2023:7034){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [CVE-2023-32681](https://nvd.nist.gov/vuln/detail/CVE-2023-32681){: external}, [RHSA-2023:7058](https://access.redhat.com/errata/RHSA-2023:7058){: external}, [CVE-2022-41723](https://nvd.nist.gov/vuln/detail/CVE-2022-41723){: external}, [RHSA-2024:0647](https://access.redhat.com/errata/RHSA-2024:0647){: external}, [CVE-2021-35937](https://nvd.nist.gov/vuln/detail/CVE-2021-35937){: external}, [CVE-2021-35938](https://nvd.nist.gov/vuln/detail/CVE-2021-35938){: external}, [CVE-2021-35939](https://nvd.nist.gov/vuln/detail/CVE-2021-35939){: external}, [RHSA-2024:0253](https://access.redhat.com/errata/RHSA-2024:0253){: external}, [CVE-2023-7104](https://nvd.nist.gov/vuln/detail/CVE-2023-7104){: external}, [RHSA-2023:7057](https://access.redhat.com/errata/RHSA-2023:7057){: external}, [CVE-2023-33460](https://nvd.nist.gov/vuln/detail/CVE-2023-33460){: external}. | |
{: caption="Changes since version 4.13.30_1556_openshift" caption-side="bottom"}


### Change log for master fix pack 4.13.28_1555_openshift, released 31 January 2024
{: #41328_1555_openshift_M}

The following table shows the changes that are in the master fix pack 4.13.28_1555_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.26.3 | v3.26.4 | See the [Calico release notes](https://docs.tigera.io/calico/3.26/release-notes/#v3.26.4){: external}. |
| Tigera Operator | v1.30.7 | v1.30.9 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.30.9){: external}. |
| Cluster health image | v1.4.5 | v1.4.6 | New version contains security fixes. |
| etcd | v3.5.10 | v3.5.11 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.11){: external}. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1487 | 1525 | New version contains security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.26.11-6 | v1.26.13-3 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | e544e35 | 7185ea1 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.5 | v2.8.6 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2767 | 2789 | New version contains updates and security fixes. |
| OpenVPN client | 2.6.7-r0-IKS-93 | 2.6.8-r0-IKS-108 | New version contains updates and security fixes. |
| OpenVPN server | 2.6.7-r0-IKS-92 | 2.6.8-r0-IKS-107 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.5.10 | v1.5.11 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.10 | v0.13.11 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.11){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.13.23 | 4.13.28 | See the {{site.data.keyword.openshiftlong_notm}} [release notes](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-28){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit| v4.13.0-20231102 | v4.13.0-20240104 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.13.0%2B20240104){: external}. |
{: caption="Changes since version 4.13.23_1550_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.30_1556_openshift, released 29 January 2024
{: #41330_1556_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.30_1556_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.28 | 4.13.30 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-30){: external}. |
| Rhel8 Packages | 4.18.0-477.27.1.el8_8 | 4.18.0-477.27.1.el8_8 | N/A |
| HAProxy | e105dc | a13673 | Security fixes for [CVE-2023-7104](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-7104){: external}, [CVE-2023-27043](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2023-27043){: external}. |
{: caption="Changes since version 4.13.28_1554_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.28_1554_openshift, released 16 January 2024
{: #41328_1554_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.28_1554_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.13.26 | 4.13.28 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-28){: external}. |
| RHEL 8 Packages | N/A | N/A | N/A |
| Haproxy | 3060b0 | e105dc | [CVE-2023-39615](https://nvd.nist.gov/vuln/detail/CVE-2023-39615){: external}, [CVE-2023-5981](https://nvd.nist.gov/vuln/detail/CVE-2023-5981){: external}, [CVE-2022-48560](https://nvd.nist.gov/vuln/detail/CVE-2022-48560){: external}, [CVE-2022-48564](https://nvd.nist.gov/vuln/detail/CVE-2022-48564){: external}. |
{: caption="Changes since version 4.13.26_1553_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.26_1553_openshift, released 02 January 2024
{: #41326_1553_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.26_1553_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.13.26 | 4.13.26 | N/A |
| RHEL 8 Packages | 4.18.0-477.27.1.el8_8 | 4.18.0-477.27.1.el8_8 | N/A |
{: caption="Changes since version 4.13.26_1552_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.26_1552_openshift, released 18 December 2023
{: #41326_1552_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.26_1552_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}} | 4.13.24 |4.13.26|For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-26){: external}. |
| RHEL 8 Packages | N/A |N/A|N/A |
{: caption="Changes since version 4.13.24_1551_openshift" caption-side="bottom"}


### Change log for master fix pack 4.13.23_1550_openshift, released 06 December 2023
{: #41323_1550_openshift_M}

The following table shows the changes that are in the master fix pack 4.13.23_1550_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.12 | v2.4.14 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.26.10-4 | v1.26.11-6 | New version contains updates and security fixes. |
| Load balancer and Load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2731 | 2767 | New version contains updates and security fixes. |
| OpenVPN client | 2.6.5-r0-IKS-77 | 2.6.7-r0-IKS-93 | New version contains updates and security fixes. |
| OpenVPN server | 2.6.5-r0-IKS-76 | 2.6.7-r0-IKS-92 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.5.9 | v1.5.10 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 438 | 439 | New version contains updates and security fixes. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.13.19 | 4.13.23 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-23){: external}. |
{: caption="Changes since version 4.13.19_1546_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.24_1551_openshift, released 04 December 2023
{: #41324_1551_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.24_1551_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.22 | 4.13.24 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-24){: external}. |
| RHEL 8 Packages | N/A | N/A | N/A |
{: caption="Changes since version 4.13.22_1547_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.22_1547_openshift, released 29 November 2023
{: #41322_1547_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.22_1547_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.19 | 4.13.22 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-22){: external}. |
| CRI-O | 1.26.4 | 1.26.4 | Unqualified image registry aliases updated for `address-parsing-service`, `admin-site`, `apache-tika`, `auto-update-service`, `config-service`, `data-integration-service`, `dataprovider-manager-service`, `data-service`, `documents-service`, `gate-service`, `gateway-service`, `icij-db`, `identity-service`, `internet-access-service`, `mongo`, `notes-service`, `public-api-service`, `router`, and `search-service`.. However, using short names are not supported due to security risks, https://access.redhat.com/solutions/6178442. |
| RHEL 8 Packages |N/A|N/A|N/A|
{: caption="Changes since version 4.13.19_1545_openshift" caption-side="bottom"}


### Change log for master fix pack 4.13.19_1546_openshift, released 15 November 2023
{: #41319_1546_openshift_M}

The following table shows the changes that are in the master fix pack 4.13.19_1546_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.4.4 | v1.4.5 | New version contains updates and security fixes. |
| etcd | v3.5.9 | v3.5.10 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.10){: external}. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.26.9-8 | v1.26.10-4 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} plug-in and monitor | 435 | 438 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | f0d3265 | e544e35 | https://github.ibm.com/alchemy-containers/armada-rbac-sync/compare/f0d326565319e449efc1ace9347448b39c1c6800...e544e35d92bc34cf08ec7773a385ac2bfd3cbbbe |
| Key Management Service provider | v2.8.4 | v2.8.5 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2681 | 2731 | New version contains updates and security fixes. |
| OpenVPN client | 2.6.5-r0-IKS-66 | 2.6.5-r0-IKS-77 | New version contains updates and security fixes. |
| OpenVPN server | 2.6.5-r0-IKS-57 | 2.6.5-r0-IKS-76 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.5.7 | v1.5.9 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.8 | v0.13.10 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.10){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.13.15 | 4.13.19 | Review the changes in the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-19){: external}. Resolves [CVE-2023-39325](https://nvd.nist.gov/vuln/detail/CVE-2023-39325){: external}, [CVE-2023-5408](https://nvd.nist.gov/vuln/detail/CVE-2023-5408){: external}, and [CVE-2023-44487](https://nvd.nist.gov/vuln/detail/CVE-2023-44487). For more information, see IBM Security bulletin [7080059](https://www.ibm.com/support/pages/node/7080059){: external} and [7114006](https://www.ibm.com/support/pages/node/7114006). |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.13.0-20231010 | v4.13.0-20231102 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.13.0+20231102){: external}. |
{: caption="Changes since version 4.13.15_1543_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.19_1545_openshift, released 08 November 2023
{: #41319_1545_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.19_1545_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}| 4.13.17 | 4.13.19 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-13-19){: external}. |
{: caption="Changes since version 4.13.17_1544_openshift" caption-side="bottom"}


### Change log for master fix pack 4.13.15_1543_openshift, released 25 October 2023
{: #41315_1543_openshift_M}

The following table shows the changes that are in the master fix pack 4.13.15_1543_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.26.1 | v3.26.3 | See the [Calico release notes](https://docs.tigera.io/calico/latest/release-notes/#v3.26.3){: external}. |
| Tigera Operator | v1.30.5 | v1.30.7 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.30.7){: external}. |
| Cluster health image | v1.4.2 | v1.4.4 | New version contains updates and security fixes. |
| {{site.data.keyword.IBM_notm}} Calico extension | 1390 | 1487 | New version contains security fixes. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.4.10 | v2.4.12 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.26.8-3 | v1.26.9-8 | New version contains updates and security fixes. The logic for the `service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-idle-connection-timeout` annotation has changed. The default idle timeout is dependent on your account settings. Usually, this value is `50`. However, some allowlisted accounts have larger timeout settings. If you don't set the annotation, your load balancers use the timeout setting in your account. You can explicitly specify the timeout by setting this annotation. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 4e2f346 | f0d3265 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.2 | v2.8.4 | New version contains updates and security fixes. |
| OpenVPN Operator image | v1.5.6 | v1.5.7 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.6 | v0.13.8 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.8){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.13.11 | 4.13.15 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-15){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | v4.13.0-20230811 | v4.13.0-20231010 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.13.0%2B20231010){: external}. |
{: caption="Changes since version 4.13.11_1540_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.13.17_1544_openshift, released 23 October 2023
{: #41317_1544_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.13.17_1544_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.13.14 | 4.13.17 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-17){: external}. |
| RHEL 8 Packages |N/A|N/A| Worker node package update for [CVE-2023-44487](https://nvd.nist.gov/vuln/detail/CVE-2023-44487){: external}. |
{: caption="Changes since version 4.13.14_1542_openshift" caption-side="bottom"}


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
| Tigera Operator | v1.30.2 | v1.30.5 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.30.5){: external}. |
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
| {{site.data.keyword.openshiftshort}}. | 4.13.4 | 4.13.6 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-6){: external}. |
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
| {{site.data.keyword.openshiftshort}}. |4.13.1|4.13.3|For more information, see the [change logs](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-3){: external}. |
| RHEL 8 Packages | N/A | N/A | Worker node package updates for [CVE-2023-32067](https://nvd.nist.gov/vuln/detail/CVE-2023-32067){: external},[CVE-2023-24329](https://nvd.nist.gov/vuln/detail/CVE-2023-24329){: external}. |
{: caption="Changes since version 4.13.1_1521_openshift" caption-side="bottom"}


### Change log for master fix pack 4.13.0_1522_openshift and worker node fix pack 4.13.1_1521_openshift, released 14 June 2023
{: #4.13.0_1522_openshiftM_4.13.1_1521_openshiftW}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.25.1 | v3.26.0 | See the [Calico release notes](https://docs.tigera.io/archive){: external}. |
| Tigera Operator | v1.29.3 | v1.30.2 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.30.2){: external}. |
| etcd | v3.5.8 | v3.5.9 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.9){: external}. |
| IBM Cloud Controller Manager | v1.25.9-7 | v1.26.5-5 | Updated to support the Kubernetes `1.26.5` release. Updated `Go` dependencies and to `Go` version `1.19.9`. Updated `calicoctl` to version `v3.25.1` and `vpcctl` to version `v0.15.0`. |
| Key Management Service provider | v2.6.6 | v2.7.0 | Secret encryption support added for clusters in Satellite locations with CoreOS enabled. Updated `Go` dependencies. |
| Red Hat OpenShift (master) | 4.12.16 | 4.13.0 | See the [Red Hat OpenShift release notes](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-0-ga){: external}. |
| Red Hat OpenShift (worker node) | 4.12.19 | 4.13.1 | See the [Red Hat OpenShift release notes](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-1){: external}. |
| Red Hat OpenShift configuration | N/A | N/A | Updated the [feature gate configuration](/docs/openshift?topic=openshift-service-settings#feature-gates){: external}. |
| Red Hat OpenShift on IBM Cloud Control Plane Operator and Metrics Server | v4.12.0-20230417 | v4.13.0-20230515 | See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.13.0+20230515){: external}. |
| Red Hat OpenShift on IBM Cloud toolkit | 4.12.0+20230417 | 4.13.0+20230515 | See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.13.0+20230515){: external}. |
{: caption="Changes since master fix pack 4.12.16_1545_openshift and worker fix pack 4.12.19_1546_openshift." caption-side="bottom"}
