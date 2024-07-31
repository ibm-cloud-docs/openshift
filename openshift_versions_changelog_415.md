---

copyright:
  years: 2023, 2024
lastupdated: "2024-07-31"


keywords: openshift, 4.15, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# Version 4.15 change log
{: #openshift_changelog_415}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.15. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #openshift_changelog_overview_415}

Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security){: external} for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}

### Change log for master fix pack 4.15.22_1554_openshift, released 31 July 2024
{: #41522_1554_openshift_M}

The following table shows the changes that are in the master fix pack 4.15.22_1554_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.27.2 | v3.27.4 | See the [Calico release notes](https://docs.tigera.io/calico/3.27/release-notes/#v3.27.4){: external}. |
| Cluster health image | v1.5.6 | v1.5.7 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.5.9 | v2.5.12 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.28.11-5 | v1.28.12-1 | New version contains updates and security fixes. |
| Key Management Service provider | v2.9.7 | v2.9.8 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.16 | v0.13.17 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.17){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.15.18 | 4.15.22 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-22){: external}. |
| {{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor | 443 | 445 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 14d0ab5 | 312030f | New version contains updates and security fixes. |
| Tigera Operator | v1.32.5 | v1.32.10 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.32.10){: external}. |
{: caption="Changes since version 4.15.18_1545_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.15.23_1553_openshift, released 29 July 2024
{: #41523_1553_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.15.23_1553_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| RHEL 8 Packages | N/A | N/A | Package updates for [RHSA-2024:4620](https://access.redhat.com/errata/RHSA-2024:4620){: external}, [CVE-2024-5564](https://nvd.nist.gov/vuln/detail/CVE-2024-5564){: external}, [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043){: external}, [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/CVE-2024-0690){: external}. |
| Haproxy | N/A | N/A | N/A |
| {{site.data.keyword.openshiftshort}}. | 4.15.21 | 4.15.23 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-23_release-notes){: external}. |
{: caption="Changes since version 4.15.21_1546_openshif" caption-side="bottom"}


### Change log for master fix pack 4.15.18_1545_openshift, released 15 July 2024
{: #41518_1545_openshift_M}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| etcd | v3.5.13 | v3.5.14 | See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.14). |
| IBM Cloud Controller Manager | v1.28.10-5 | v1.28.11-5 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for IBM Cloud Provider | 2933 | 2967 | New version contains updates and security fixes. |
| Red Hat OpenShift on IBM Cloud | 4.15.17 | 4.15.18 | See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-18) |
| Red Hat OpenShift on IBM Cloud Control Plane Operator, Metrics Server, and toolkit | 4.15.0+20240603 | 4.15.0+20240709 | See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.15.0+20240709). |
{: caption="Changes since version 4.15.17_1541_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.15.21_1546_openshift, released 15 July 2024
{: #41521_1546_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.15.21_1546_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.15.19 | 4.15.21 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-21){: external}. |
| RHEL 8 Packages | 4.18.0-553.5.1.el8_10 | 4.18.0-553.8.1.el8_10 | Worker node kernel & package updates for [RHSA-2024:4211](https://access.redhat.com/errata/RHSA-2024:4211){: external}, [CVE-2020-26555](https://nvd.nist.gov/vuln/detail/CVE-2020-26555){: external}, [CVE-2021-46909](https://nvd.nist.gov/vuln/detail/CVE-2021-46909){: external}, [CVE-2021-46972](https://nvd.nist.gov/vuln/detail/CVE-2021-46972){: external}, [CVE-2021-47069](https://nvd.nist.gov/vuln/detail/CVE-2021-47069){: external}, [CVE-2021-47073](https://nvd.nist.gov/vuln/detail/CVE-2021-47073){: external}, [CVE-2021-47236](https://nvd.nist.gov/vuln/detail/CVE-2021-47236){: external}, [CVE-2021-47310](https://nvd.nist.gov/vuln/detail/CVE-2021-47310){: external}, [CVE-2021-47311](https://nvd.nist.gov/vuln/detail/CVE-2021-47311){: external}, [CVE-2021-47353](https://nvd.nist.gov/vuln/detail/CVE-2021-47353){: external}, [CVE-2021-47356](https://nvd.nist.gov/vuln/detail/CVE-2021-47356){: external}, [CVE-2021-47456](https://nvd.nist.gov/vuln/detail/CVE-2021-47456){: external}, [CVE-2021-47495](https://nvd.nist.gov/vuln/detail/CVE-2021-47495){: external}, [CVE-2023-5090](https://nvd.nist.gov/vuln/detail/CVE-2023-5090){: external}, [CVE-2023-52464](https://nvd.nist.gov/vuln/detail/CVE-2023-52464){: external}, [CVE-2023-52560](https://nvd.nist.gov/vuln/detail/CVE-2023-52560){: external}, [CVE-2023-52615](https://nvd.nist.gov/vuln/detail/CVE-2023-52615){: external}, [CVE-2023-52626](https://nvd.nist.gov/vuln/detail/CVE-2023-52626){: external}, [CVE-2023-52667](https://nvd.nist.gov/vuln/detail/CVE-2023-52667){: external}, [CVE-2023-52669](https://nvd.nist.gov/vuln/detail/CVE-2023-52669){: external}, [CVE-2023-52675](https://nvd.nist.gov/vuln/detail/CVE-2023-52675){: external}, [CVE-2023-52686](https://nvd.nist.gov/vuln/detail/CVE-2023-52686){: external}, [CVE-2023-52700](https://nvd.nist.gov/vuln/detail/CVE-2023-52700){: external}, [CVE-2023-52703](https://nvd.nist.gov/vuln/detail/CVE-2023-52703){: external}, [CVE-2023-52781](https://nvd.nist.gov/vuln/detail/CVE-2023-52781){: external}, [CVE-2023-52813](https://nvd.nist.gov/vuln/detail/CVE-2023-52813){: external}, [CVE-2023-52835](https://nvd.nist.gov/vuln/detail/CVE-2023-52835){: external}, [CVE-2023-52877](https://nvd.nist.gov/vuln/detail/CVE-2023-52877){: external}, [CVE-2023-52878](https://nvd.nist.gov/vuln/detail/CVE-2023-52878){: external}, [CVE-2023-52881](https://nvd.nist.gov/vuln/detail/CVE-2023-52881){: external}, [CVE-2024-26583](https://nvd.nist.gov/vuln/detail/CVE-2024-26583){: external}, [CVE-2024-26584](https://nvd.nist.gov/vuln/detail/CVE-2024-26584){: external}, [CVE-2024-26585](https://nvd.nist.gov/vuln/detail/CVE-2024-26585){: external}, [CVE-2024-26656](https://nvd.nist.gov/vuln/detail/CVE-2024-26656){: external}, [CVE-2024-26675](https://nvd.nist.gov/vuln/detail/CVE-2024-26675){: external}, [CVE-2024-26735](https://nvd.nist.gov/vuln/detail/CVE-2024-26735){: external}, [CVE-2024-26759](https://nvd.nist.gov/vuln/detail/CVE-2024-26759){: external}, [CVE-2024-26801](https://nvd.nist.gov/vuln/detail/CVE-2024-26801){: external}, [CVE-2024-26804](https://nvd.nist.gov/vuln/detail/CVE-2024-26804){: external}, [CVE-2024-26826](https://nvd.nist.gov/vuln/detail/CVE-2024-26826){: external}, [CVE-2024-26859](https://nvd.nist.gov/vuln/detail/CVE-2024-26859){: external}, [CVE-2024-26906](https://nvd.nist.gov/vuln/detail/CVE-2024-26906){: external}, [CVE-2024-26907](https://nvd.nist.gov/vuln/detail/CVE-2024-26907){: external}, [CVE-2024-26974](https://nvd.nist.gov/vuln/detail/CVE-2024-26974){: external}, [CVE-2024-26982](https://nvd.nist.gov/vuln/detail/CVE-2024-26982){: external}, [CVE-2024-27397](https://nvd.nist.gov/vuln/detail/CVE-2024-27397){: external}, [CVE-2024-27410](https://nvd.nist.gov/vuln/detail/CVE-2024-27410){: external}, [CVE-2024-35789](https://nvd.nist.gov/vuln/detail/CVE-2024-35789){: external}, [CVE-2024-35835](https://nvd.nist.gov/vuln/detail/CVE-2024-35835){: external}, [CVE-2024-35838](https://nvd.nist.gov/vuln/detail/CVE-2024-35838){: external}, [CVE-2024-35845](https://nvd.nist.gov/vuln/detail/CVE-2024-35845){: external}, [CVE-2024-35852](https://nvd.nist.gov/vuln/detail/CVE-2024-35852){: external}, [CVE-2024-35853](https://nvd.nist.gov/vuln/detail/CVE-2024-35853){: external}, [CVE-2024-35854](https://nvd.nist.gov/vuln/detail/CVE-2024-35854){: external}, [CVE-2024-35855](https://nvd.nist.gov/vuln/detail/CVE-2024-35855){: external}, [CVE-2024-35888](https://nvd.nist.gov/vuln/detail/CVE-2024-35888){: external}, [CVE-2024-35890](https://nvd.nist.gov/vuln/detail/CVE-2024-35890){: external}, [CVE-2024-35958](https://nvd.nist.gov/vuln/detail/CVE-2024-35958){: external}, [CVE-2024-35959](https://nvd.nist.gov/vuln/detail/CVE-2024-35959){: external}, [CVE-2024-35960](https://nvd.nist.gov/vuln/detail/CVE-2024-35960){: external}, [CVE-2024-36004](https://nvd.nist.gov/vuln/detail/CVE-2024-36004){: external}, [CVE-2024-36007](https://nvd.nist.gov/vuln/detail/CVE-2024-36007){: external}, [RHSA-2024:4256](https://access.redhat.com/errata/RHSA-2024:4256){: external}, [CVE-2022-48624](https://nvd.nist.gov/vuln/detail/CVE-2022-48624){: external}, [CVE-2024-32487](https://nvd.nist.gov/vuln/detail/CVE-2024-32487){: external}, [RHSA-2024:4249](https://access.redhat.com/errata/RHSA-2024:4249){: external}, [CVE-2024-25629](https://nvd.nist.gov/vuln/detail/CVE-2024-25629){: external}, [RHSA-2024:4264](https://access.redhat.com/errata/RHSA-2024:4264){: external}, [CVE-2023-2953](https://nvd.nist.gov/vuln/detail/CVE-2023-2953){: external}, [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043){: external}, [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/CVE-2024-0690){: external}, [RHSA-2024:4262](https://access.redhat.com/errata/RHSA-2024:4262){: external}, [CVE-2023-31346](https://nvd.nist.gov/vuln/detail/CVE-2023-31346){: external}, [RHSA-2024:4252](https://access.redhat.com/errata/RHSA-2024:4252){: external}, [CVE-2024-28182](https://nvd.nist.gov/vuln/detail/CVE-2024-28182){: external}, [RHSA-2024:4260](https://access.redhat.com/errata/RHSA-2024:4260){: external}, [CVE-2024-3651](https://nvd.nist.gov/vuln/detail/CVE-2024-3651){: external}, [RHSA-2024:4231](https://access.redhat.com/errata/RHSA-2024:4231){: external}, [CVE-2024-34064](https://nvd.nist.gov/vuln/detail/CVE-2024-34064){: external}. |
| HAProxy | e77d4ca | c91c765 | Security fixes for [CVE-2024-28182](https://nvd.nist.gov/vuln/detail/CVE-2023-2953){: external},[CVE-2024-25062](https://nvd.nist.gov/vuln/detail/CVE-2024-28182){: external}. |
{: caption="Changes since version 4.15.19_1543_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.15.19_1543_openshift, released 09 July 2024
{: #41519_1543_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.15.19_1543_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.15.17 | 4.15.19 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-19){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-553.5.1.el8_10 | [RHSA-2024:3271](https://access.redhat.com/errata/RHSA-2024:3271){: external}, [CVE-2023-4408](https://nvd.nist.gov/vuln/detail/CVE-2023-4408){: external}, [CVE-2023-50387](https://nvd.nist.gov/vuln/detail/CVE-2023-50387){: external}, [CVE-2023-50868](https://nvd.nist.gov/vuln/detail/CVE-2023-50868){: external}, [RHSA-2024:3254](https://access.redhat.com/errata/RHSA-2024:3254){: external}, [CVE-2022-2880](https://nvd.nist.gov/vuln/detail/CVE-2022-2880){: external}, [CVE-2022-41715](https://nvd.nist.gov/vuln/detail/CVE-2022-41715){: external}, [CVE-2024-1753](https://nvd.nist.gov/vuln/detail/CVE-2024-1753){: external}, [CVE-2024-24786](https://nvd.nist.gov/vuln/detail/CVE-2024-24786){: external}, [CVE-2024-28180](https://nvd.nist.gov/vuln/detail/CVE-2024-28180){: external}, [RHSA-2024:4084](https://access.redhat.com/errata/RHSA-2024:4084){: external}, [CVE-2024-32002](https://nvd.nist.gov/vuln/detail/CVE-2024-32002){: external}, [CVE-2024-32004](https://nvd.nist.gov/vuln/detail/CVE-2024-32004){: external}, [CVE-2024-32020](https://nvd.nist.gov/vuln/detail/CVE-2024-32020){: external}, [CVE-2024-32021](https://nvd.nist.gov/vuln/detail/CVE-2024-32021){: external}, [CVE-2024-32465](https://nvd.nist.gov/vuln/detail/CVE-2024-32465){: external}, [RHSA-2024:3269](https://access.redhat.com/errata/RHSA-2024:3269){: external}, [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961){: external}, [RHSA-2024:3344](https://access.redhat.com/errata/RHSA-2024:3344){: external}, [CVE-2024-33599](https://nvd.nist.gov/vuln/detail/CVE-2024-33599){: external}, [CVE-2024-33600](https://nvd.nist.gov/vuln/detail/CVE-2024-33600){: external}, [CVE-2024-33601](https://nvd.nist.gov/vuln/detail/CVE-2024-33601){: external}, [CVE-2024-33602](https://nvd.nist.gov/vuln/detail/CVE-2024-33602){: external}, [RHSA-2024:3178](https://access.redhat.com/errata/RHSA-2024:3178){: external}, [CVE-2022-46329](https://nvd.nist.gov/vuln/detail/CVE-2022-46329){: external}, [CVE-2023-20592](https://nvd.nist.gov/vuln/detail/CVE-2023-20592){: external}, [RHSA-2024:3347](https://access.redhat.com/errata/RHSA-2024:3347){: external}, [CVE-2023-6597](https://nvd.nist.gov/vuln/detail/CVE-2023-6597){: external}, [CVE-2024-0450](https://nvd.nist.gov/vuln/detail/CVE-2024-0450){: external}, [RHSA-2024:3466](https://access.redhat.com/errata/RHSA-2024:3466){: external}, [CVE-2023-6597](https://nvd.nist.gov/vuln/detail/CVE-2023-6597){: external}, [CVE-2024-0450](https://nvd.nist.gov/vuln/detail/CVE-2024-0450){: external}, [CVE-2024-3651](https://nvd.nist.gov/vuln/detail/CVE-2024-3651){: external}, [RHSA-2024:3268](https://access.redhat.com/errata/RHSA-2024:3268){: external}, [CVE-2024-26458](https://nvd.nist.gov/vuln/detail/CVE-2024-26458){: external}, [CVE-2024-26461](https://nvd.nist.gov/vuln/detail/CVE-2024-26461){: external}, [RHSA-2024:3233](https://access.redhat.com/errata/RHSA-2024:3233){: external}, [CVE-2023-6004](https://nvd.nist.gov/vuln/detail/CVE-2023-6004){: external}, [CVE-2023-6918](https://nvd.nist.gov/vuln/detail/CVE-2023-6918){: external}, [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043){: external}, [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/CVE-2024-0690){: external}, [RHSA-2024:3968](https://access.redhat.com/errata/RHSA-2024:3968){: external}, [CVE-2024-28176](https://nvd.nist.gov/vuln/detail/CVE-2024-28176){: external}, [CVE-2024-28180](https://nvd.nist.gov/vuln/detail/CVE-2024-28180){: external}, [RHSA-2024:2988](https://access.redhat.com/errata/RHSA-2024:2988){: external}, [CVE-2018-25091](https://nvd.nist.gov/vuln/detail/CVE-2018-25091){: external}, [CVE-2021-33198](https://nvd.nist.gov/vuln/detail/CVE-2021-33198){: external}, [CVE-2021-34558](https://nvd.nist.gov/vuln/detail/CVE-2021-34558){: external}, [CVE-2022-2879](https://nvd.nist.gov/vuln/detail/CVE-2022-2879){: external}, [CVE-2022-2880](https://nvd.nist.gov/vuln/detail/CVE-2022-2880){: external}, [CVE-2022-41715](https://nvd.nist.gov/vuln/detail/CVE-2022-41715){: external}, [CVE-2023-29409](https://nvd.nist.gov/vuln/detail/CVE-2023-29409){: external}, [CVE-2023-39318](https://nvd.nist.gov/vuln/detail/CVE-2023-39318){: external}, [CVE-2023-39319](https://nvd.nist.gov/vuln/detail/CVE-2023-39319){: external}, [CVE-2023-39321](https://nvd.nist.gov/vuln/detail/CVE-2023-39321){: external}, [CVE-2023-39322](https://nvd.nist.gov/vuln/detail/CVE-2023-39322){: external}, [CVE-2023-39326](https://nvd.nist.gov/vuln/detail/CVE-2023-39326){: external}, [CVE-2023-45287](https://nvd.nist.gov/vuln/detail/CVE-2023-45287){: external}, [CVE-2023-45803](https://nvd.nist.gov/vuln/detail/CVE-2023-45803){: external}, [CVE-2023-48795](https://nvd.nist.gov/vuln/detail/CVE-2023-48795){: external}, [CVE-2024-23650](https://nvd.nist.gov/vuln/detail/CVE-2024-23650){: external}, [RHSA-2024:3214](https://access.redhat.com/errata/RHSA-2024:3214){: external}, [CVE-2021-43618](https://nvd.nist.gov/vuln/detail/CVE-2021-43618){: external}, [RHSA-2024:3184](https://access.redhat.com/errata/RHSA-2024:3184){: external}, [CVE-2023-4692](https://nvd.nist.gov/vuln/detail/CVE-2023-4692){: external}, [CVE-2023-4693](https://nvd.nist.gov/vuln/detail/CVE-2023-4693){: external}, [CVE-2024-1048](https://nvd.nist.gov/vuln/detail/CVE-2024-1048){: external}, [RHSA-2024:3138](https://access.redhat.com/errata/RHSA-2024:3138){: external}, [CVE-2019-13631](https://nvd.nist.gov/vuln/detail/CVE-2019-13631){: external}, [CVE-2019-15505](https://nvd.nist.gov/vuln/detail/CVE-2019-15505){: external}, [CVE-2020-25656](https://nvd.nist.gov/vuln/detail/CVE-2020-25656){: external}, [CVE-2021-3753](https://nvd.nist.gov/vuln/detail/CVE-2021-3753){: external}, [CVE-2021-4204](https://nvd.nist.gov/vuln/detail/CVE-2021-4204){: external}, [CVE-2022-0500](https://nvd.nist.gov/vuln/detail/CVE-2022-0500){: external}, [CVE-2022-23222](https://nvd.nist.gov/vuln/detail/CVE-2022-23222){: external}, [CVE-2022-3565](https://nvd.nist.gov/vuln/detail/CVE-2022-3565){: external}, [CVE-2022-45934](https://nvd.nist.gov/vuln/detail/CVE-2022-45934){: external}, [CVE-2023-1513](https://nvd.nist.gov/vuln/detail/CVE-2023-1513){: external}, [CVE-2023-24023](https://nvd.nist.gov/vuln/detail/CVE-2023-24023){: external}, [CVE-2023-25775](https://nvd.nist.gov/vuln/detail/CVE-2023-25775){: external}, [CVE-2023-28464](https://nvd.nist.gov/vuln/detail/CVE-2023-28464){: external}, [CVE-2023-31083](https://nvd.nist.gov/vuln/detail/CVE-2023-31083){: external}, [CVE-2023-3567](https://nvd.nist.gov/vuln/detail/CVE-2023-3567){: external}, [CVE-2023-37453](https://nvd.nist.gov/vuln/detail/CVE-2023-37453){: external}, [CVE-2023-38409](https://nvd.nist.gov/vuln/detail/CVE-2023-38409){: external}, [CVE-2023-39189](https://nvd.nist.gov/vuln/detail/CVE-2023-39189){: external}, [CVE-2023-39192](https://nvd.nist.gov/vuln/detail/CVE-2023-39192){: external}, [CVE-2023-39193](https://nvd.nist.gov/vuln/detail/CVE-2023-39193){: external}, [CVE-2023-39194](https://nvd.nist.gov/vuln/detail/CVE-2023-39194){: external}, [CVE-2023-39198](https://nvd.nist.gov/vuln/detail/CVE-2023-39198){: external}, [CVE-2023-4133](https://nvd.nist.gov/vuln/detail/CVE-2023-4133){: external}, [CVE-2023-4244](https://nvd.nist.gov/vuln/detail/CVE-2023-4244){: external}, [CVE-2023-42754](https://nvd.nist.gov/vuln/detail/CVE-2023-42754){: external}, [CVE-2023-42755](https://nvd.nist.gov/vuln/detail/CVE-2023-42755){: external}, [CVE-2023-45863](https://nvd.nist.gov/vuln/detail/CVE-2023-45863){: external}, [CVE-2023-51779](https://nvd.nist.gov/vuln/detail/CVE-2023-51779){: external}, [CVE-2023-51780](https://nvd.nist.gov/vuln/detail/CVE-2023-51780){: external}, [CVE-2023-52340](https://nvd.nist.gov/vuln/detail/CVE-2023-52340){: external}, [CVE-2023-52434](https://nvd.nist.gov/vuln/detail/CVE-2023-52434){: external}, [CVE-2023-52448](https://nvd.nist.gov/vuln/detail/CVE-2023-52448){: external}, [CVE-2023-52489](https://nvd.nist.gov/vuln/detail/CVE-2023-52489){: external}, [CVE-2023-52574](https://nvd.nist.gov/vuln/detail/CVE-2023-52574){: external}, [CVE-2023-52580](https://nvd.nist.gov/vuln/detail/CVE-2023-52580){: external}, [CVE-2023-52581](https://nvd.nist.gov/vuln/detail/CVE-2023-52581){: external}, [CVE-2023-52597](https://nvd.nist.gov/vuln/detail/CVE-2023-52597){: external}, [CVE-2023-52620](https://nvd.nist.gov/vuln/detail/CVE-2023-52620){: external}, [CVE-2023-6121](https://nvd.nist.gov/vuln/detail/CVE-2023-6121){: external}, [CVE-2023-6176](https://nvd.nist.gov/vuln/detail/CVE-2023-6176){: external}, [CVE-2023-6622](https://nvd.nist.gov/vuln/detail/CVE-2023-6622){: external}, [CVE-2023-6915](https://nvd.nist.gov/vuln/detail/CVE-2023-6915){: external}, [CVE-2023-6932](https://nvd.nist.gov/vuln/detail/CVE-2023-6932){: external}, [CVE-2024-0841](https://nvd.nist.gov/vuln/detail/CVE-2024-0841){: external}, [CVE-2024-25742](https://nvd.nist.gov/vuln/detail/CVE-2024-25742){: external}, [CVE-2024-25743](https://nvd.nist.gov/vuln/detail/CVE-2024-25743){: external}, [CVE-2024-26602](https://nvd.nist.gov/vuln/detail/CVE-2024-26602){: external}, [CVE-2024-26609](https://nvd.nist.gov/vuln/detail/CVE-2024-26609){: external}, [CVE-2024-26671](https://nvd.nist.gov/vuln/detail/CVE-2024-26671){: external}, [RHSA-2024:3618](https://access.redhat.com/errata/RHSA-2024:3618){: external}, [CVE-2019-25162](https://nvd.nist.gov/vuln/detail/CVE-2019-25162){: external}, [CVE-2020-36777](https://nvd.nist.gov/vuln/detail/CVE-2020-36777){: external}, [CVE-2021-46934](https://nvd.nist.gov/vuln/detail/CVE-2021-46934){: external}, [CVE-2021-47013](https://nvd.nist.gov/vuln/detail/CVE-2021-47013){: external}, [CVE-2021-47055](https://nvd.nist.gov/vuln/detail/CVE-2021-47055){: external}, [CVE-2021-47118](https://nvd.nist.gov/vuln/detail/CVE-2021-47118){: external}, [CVE-2021-47153](https://nvd.nist.gov/vuln/detail/CVE-2021-47153){: external}, [CVE-2021-47171](https://nvd.nist.gov/vuln/detail/CVE-2021-47171){: external}, [CVE-2021-47185](https://nvd.nist.gov/vuln/detail/CVE-2021-47185){: external}, [CVE-2022-48627](https://nvd.nist.gov/vuln/detail/CVE-2022-48627){: external}, [CVE-2022-48669](https://nvd.nist.gov/vuln/detail/CVE-2022-48669){: external}, [CVE-2023-52439](https://nvd.nist.gov/vuln/detail/CVE-2023-52439){: external}, [CVE-2023-52445](https://nvd.nist.gov/vuln/detail/CVE-2023-52445){: external}, [CVE-2023-52477](https://nvd.nist.gov/vuln/detail/CVE-2023-52477){: external}, [CVE-2023-52513](https://nvd.nist.gov/vuln/detail/CVE-2023-52513){: external}, [CVE-2023-52520](https://nvd.nist.gov/vuln/detail/CVE-2023-52520){: external}, [CVE-2023-52528](https://nvd.nist.gov/vuln/detail/CVE-2023-52528){: external}, [CVE-2023-52565](https://nvd.nist.gov/vuln/detail/CVE-2023-52565){: external}, [CVE-2023-52578](https://nvd.nist.gov/vuln/detail/CVE-2023-52578){: external}, [CVE-2023-52594](https://nvd.nist.gov/vuln/detail/CVE-2023-52594){: external}, [CVE-2023-52595](https://nvd.nist.gov/vuln/detail/CVE-2023-52595){: external}, [CVE-2023-52598](https://nvd.nist.gov/vuln/detail/CVE-2023-52598){: external}, [CVE-2023-52606](https://nvd.nist.gov/vuln/detail/CVE-2023-52606){: external}, [CVE-2023-52607](https://nvd.nist.gov/vuln/detail/CVE-2023-52607){: external}, [CVE-2023-52610](https://nvd.nist.gov/vuln/detail/CVE-2023-52610){: external}, [CVE-2023-6240](https://nvd.nist.gov/vuln/detail/CVE-2023-6240){: external}, [CVE-2024-0340](https://nvd.nist.gov/vuln/detail/CVE-2024-0340){: external}, [CVE-2024-23307](https://nvd.nist.gov/vuln/detail/CVE-2024-23307){: external}, [CVE-2024-25744](https://nvd.nist.gov/vuln/detail/CVE-2024-25744){: external}, [CVE-2024-26593](https://nvd.nist.gov/vuln/detail/CVE-2024-26593){: external}, [CVE-2024-26603](https://nvd.nist.gov/vuln/detail/CVE-2024-26603){: external}, [CVE-2024-26610](https://nvd.nist.gov/vuln/detail/CVE-2024-26610){: external}, [CVE-2024-26615](https://nvd.nist.gov/vuln/detail/CVE-2024-26615){: external}, [CVE-2024-26642](https://nvd.nist.gov/vuln/detail/CVE-2024-26642){: external}, [CVE-2024-26643](https://nvd.nist.gov/vuln/detail/CVE-2024-26643){: external}, [CVE-2024-26659](https://nvd.nist.gov/vuln/detail/CVE-2024-26659){: external}, [CVE-2024-26664](https://nvd.nist.gov/vuln/detail/CVE-2024-26664){: external}, [CVE-2024-26693](https://nvd.nist.gov/vuln/detail/CVE-2024-26693){: external}, [CVE-2024-26694](https://nvd.nist.gov/vuln/detail/CVE-2024-26694){: external}, [CVE-2024-26743](https://nvd.nist.gov/vuln/detail/CVE-2024-26743){: external}, [CVE-2024-26744](https://nvd.nist.gov/vuln/detail/CVE-2024-26744){: external}, [CVE-2024-26779](https://nvd.nist.gov/vuln/detail/CVE-2024-26779){: external}, [CVE-2024-26872](https://nvd.nist.gov/vuln/detail/CVE-2024-26872){: external}, [CVE-2024-26892](https://nvd.nist.gov/vuln/detail/CVE-2024-26892){: external}, [CVE-2024-26897](https://nvd.nist.gov/vuln/detail/CVE-2024-26897){: external}, [CVE-2024-26901](https://nvd.nist.gov/vuln/detail/CVE-2024-26901){: external}, [CVE-2024-26919](https://nvd.nist.gov/vuln/detail/CVE-2024-26919){: external}, [CVE-2024-26933](https://nvd.nist.gov/vuln/detail/CVE-2024-26933){: external}, [CVE-2024-26934](https://nvd.nist.gov/vuln/detail/CVE-2024-26934){: external}, [CVE-2024-26964](https://nvd.nist.gov/vuln/detail/CVE-2024-26964){: external}, [CVE-2024-26973](https://nvd.nist.gov/vuln/detail/CVE-2024-26973){: external}, [CVE-2024-26993](https://nvd.nist.gov/vuln/detail/CVE-2024-26993){: external}, [CVE-2024-27014](https://nvd.nist.gov/vuln/detail/CVE-2024-27014){: external}, [CVE-2024-27048](https://nvd.nist.gov/vuln/detail/CVE-2024-27048){: external}, [CVE-2024-27052](https://nvd.nist.gov/vuln/detail/CVE-2024-27052){: external}, [CVE-2024-27056](https://nvd.nist.gov/vuln/detail/CVE-2024-27056){: external}, [CVE-2024-27059](https://nvd.nist.gov/vuln/detail/CVE-2024-27059){: external}, [RHSA-2024:3626](https://access.redhat.com/errata/RHSA-2024:3626){: external}, [CVE-2024-25062](https://nvd.nist.gov/vuln/detail/CVE-2024-25062){: external}, [RHSA-2024:3166](https://access.redhat.com/errata/RHSA-2024:3166){: external}, [CVE-2020-15778](https://nvd.nist.gov/vuln/detail/CVE-2020-15778){: external}, [RHSA-2024:3163](https://access.redhat.com/errata/RHSA-2024:3163){: external}, [CVE-2024-22365](https://nvd.nist.gov/vuln/detail/CVE-2024-22365){: external}, [RHSA-2024:3102](https://access.redhat.com/errata/RHSA-2024:3102){: external}, [CVE-2024-22195](https://nvd.nist.gov/vuln/detail/CVE-2024-22195){: external}, [RHSA-2024:2985](https://access.redhat.com/errata/RHSA-2024:2985){: external}, [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/CVE-2022-40897){: external}, [CVE-2023-23931](https://nvd.nist.gov/vuln/detail/CVE-2023-23931){: external}, [CVE-2023-27043](https://nvd.nist.gov/vuln/detail/CVE-2023-27043){: external}, [CVE-2023-43804](https://nvd.nist.gov/vuln/detail/CVE-2023-43804){: external}, [RHSA-2024:3139](https://access.redhat.com/errata/RHSA-2024:3139){: external}, [CVE-2021-40153](https://nvd.nist.gov/vuln/detail/CVE-2021-40153){: external}, [CVE-2021-41072](https://nvd.nist.gov/vuln/detail/CVE-2021-41072){: external}, [RHSA-2024:3270](https://access.redhat.com/errata/RHSA-2024:3270){: external}, [CVE-2023-3758](https://nvd.nist.gov/vuln/detail/CVE-2023-3758){: external}, [RHSA-2024:3203](https://access.redhat.com/errata/RHSA-2024:3203){: external}, [CVE-2023-7008](https://nvd.nist.gov/vuln/detail/CVE-2023-7008){: external}. |
| HAProxy | 18889dd | e77d4ca | New version contains security fixes |
{: caption="Changes since version 4.15.17_1542_openshift" caption-side="bottom"}


### Change log for master fix pack 4.15.17_1541_openshift, released 19 June 2024
{: #41517_1541_openshift_M}

The following table shows the changes that are in the master fix pack 4.15.17_1541_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.5.5 | v1.5.6 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.28.10-1 | v1.28.10-5 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} RBAC Operator | 4c5d156 | 14d0ab5 | New version contains updates and security fixes. |
| Key Management Service provider | v2.9.6 | v2.9.7 | New version contains updates and security fixes. |
| {{site.data.keyword.openshiftshort}}. | 4.15.14 | 4.15.17 | https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html |
| Portieris admission controller | v0.13.15 | v0.13.16 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.16){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | 4.15.0+20240514 | 4.15.0+20240603 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.15.0+20240603){: external}. |
{: caption="Changes since version 4.15.14_1537_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.15.17_1542_openshift, released 18 June 2024
{: #41517_1542_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.15.17_1542_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.15.15 | 4.15.17 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-17){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-513.24.1.el8_9 | N/A |
| HAProxy | 0062a3c | 18889dd | Security fixes for [CVE-2024-25062](https://nvd.nist.gov/vuln/detail/CVE-2024-25062){: external}. |
{: caption="Changes since version 4.15.15_1538_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.15.15_1538_openshift, released 03 June 2024
{: #41515_1538_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.15.15_1538_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.15.13 | 4.15.15 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-15){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-513.24.1.el8_9 | N/A |
| HAProxy | e88695e | 0062a3c | [CVE-2024-0450](https://nvd.nist.gov/vuln/detail/CVE-2024-0450){: external}, [CVE-2024-33599](https://nvd.nist.gov/vuln/detail/CVE-2024-33599){: external}, [CVE-2024-26461](https://nvd.nist.gov/vuln/detail/CVE-2024-26461){: external}, [CVE-2021-43618](https://nvd.nist.gov/vuln/detail/CVE-2021-43618){: external}, [CVE-2024-22365](https://nvd.nist.gov/vuln/detail/CVE-2024-22365){: external}, [CVE-2023-6597](https://nvd.nist.gov/vuln/detail/CVE-2023-6597){: external}, [CVE-2024-26458](https://nvd.nist.gov/vuln/detail/CVE-2024-26458){: external}, [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961){: external}, [CVE-2024-33601](https://nvd.nist.gov/vuln/detail/CVE-2024-33601){: external}, [CVE-2024-33602](https://nvd.nist.gov/vuln/detail/CVE-2024-33602){: external}, [CVE-2023-7008](https://nvd.nist.gov/vuln/detail/CVE-2023-7008){: external}, [CVE-2023-6004](https://nvd.nist.gov/vuln/detail/CVE-2023-6004){: external}, [CVE-2023-6918](https://nvd.nist.gov/vuln/detail/CVE-2023-6918){: external}, [CVE-2024-33600](https://nvd.nist.gov/vuln/detail/CVE-2024-33600){: external}. |
{: caption="Changes since version 4.15.13_1535_openshift" caption-side="bottom"}


### Change log for master fix pack 4.15.14_1537_openshift, released 29 May 2024
{: #41514_1537_openshift_M}

The following table shows the changes that are in the master fix pack 4.15.14_1537_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Cluster health image | v1.5.4 | v1.5.5 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.28.9-4 | v1.28.10-1 | New version contains updates and security fixes. |
| Key Management Service provider | v2.9.5 | v2.9.6 | New version contains updates and security fixes. |
| Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider | 2867 | 2933 | New version contains updates and security fixes. |
| Portieris admission controller | v0.13.13 | v0.13.15 | See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.15){: external}. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.15.11 | 4.15.14 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-14){: external}. |
| {{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit | 4.15.0+20240415 | 4.15.0+20240514 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.15.0+20240514){: external}. |
{: caption="Changes since version 4.15.11_1534_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.15.13_1535_openshift, released 23 May 2024
{: #41513_1535_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.15.13_1535_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.15.11 | 4.15.13 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-13){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-513.24.1.el8_9 | Worker node package updates for [RHSA-2024:2722](https://access.redhat.com/errata/RHSA-2024:2722){: external}, [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961){: external}. |
| HAProxy | d225100 | 4e826da | [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961){: external}, [CVE-2024-28834](https://nvd.nist.gov/vuln/detail/CVE-2024-28834){: external}. |
{: caption="Changes since version 4.15.11_1533_openshift" caption-side="bottom"}


### Change log for master fix pack 4.15.11_1534_openshift, released 09 May 2024
{: #41511_1534_openshift_M}

The following table shows the changes that are in the master fix pack 4.15.11_1534_openshift. Master patch updates are applied automatically. 



| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.cloud_notm}} Block Storage driver and plug-in | v2.5.8 | v2.5.9 | New version contains updates and security fixes. |
| {{site.data.keyword.cloud_notm}} Controller Manager | v1.28.9-1 | v1.28.9-4 | New version contains updates and security fixes. |
| {{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor | 442 | 443 | New version contains updates and security fixes. |
| {{site.data.keyword.openshiftlong_notm}}. | 4.15.9 | 4.15.11 | See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-11){: external}. |
{: caption="Changes since version 4.15.9_1530_openshift" caption-side="bottom"}


### Change log for worker node fix pack 4.15.11_1533_openshift, released 06 May 2024
{: #41511_1533_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.15.11_1533_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.15.9 | 4.15.11 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-11){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-513.24.1.el8_9 | Worker node package updates for [RHSA-2024:2098](https://access.redhat.com/errata/RHSA-2024:2098){: external}, [CVE-2024-1753](https://nvd.nist.gov/vuln/detail/CVE-2024-1753){: external}. |
| HAProxy | 295dba8 | 295dba8 | N/A |
{: caption="Changes since version 4.15.9_1531_openshift" caption-side="bottom"}


### Change log for master fix pack 4.15.9_1530_openshift and worker node fix pack 4.15.6_1525_openshift, released 24 April 2024
{: #4.15.9_1530_openshiftM_4.15.6_1525_openshift_openshiftW}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.26.4 | v3.27.2 | See the [Calico release notes](https://docs.tigera.io/calico/3.27/release-notes/). |
| IBM Calico extension | 1537 | N/A | Component has been removed. |
| IBM Cloud Controller Manager | v1.27.12-10 | v1.28.9-1 | New version contains updates and security fixes. |
| Key Management Service provider | v2.8.9 | v2.9.5 | New version contains updates and security fixes. |
| Red Hat OpenShift (master) | 4.14.20 | 4.15.9 | See the [Red Hat OpenShift release notes](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-9). |
| Red Hat OpenShift (worker node) | 4.14.19 | 4.15.6 | See the [Red Hat OpenShift release notes](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-6). |
| Red Hat OpenShift on IBM Cloud Control Plane Operator, Metrics Server, and toolkit | 4.14.0+20240412 | 4.15.0+20240415 | See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.15.0+20240415). |
| Tigera Operator | v1.30.9 | v1.32.5 | See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.32.5). |
{: caption="Changes since master fix pack 4.14.20_1558_openshift and worker fix pack 4.14.19_1557_openshift." caption-side="bottom"}


### Change log for worker node fix pack 4.15.9_1531_openshift, released 22 April 2024
{: #4159_1531_openshift_W}

The following table shows the changes that are in the worker node fix pack 4.15.9_1531_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| {{site.data.keyword.openshiftshort}}. | 4.15.6 | 4.15.9 | For more information, see the [change logs](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-9){: external}. |
| RHEL 8 Packages | 4.18.0-513.24.1.el8_9 | 4.18.0-513.24.1.el8_9 | Worker node package updates for [RHSA-2024:1782](https://access.redhat.com/errata/RHSA-2024:1782){: external}, [CVE-2023-4408](https://nvd.nist.gov/vuln/detail/CVE-2023-4408){: external}, [CVE-2023-50387](https://nvd.nist.gov/vuln/detail/CVE-2023-50387){: external}, [CVE-2023-50868](https://nvd.nist.gov/vuln/detail/CVE-2023-50868){: external}, [RHSA-2024:1784](https://access.redhat.com/errata/RHSA-2024:1784){: external}, [CVE-2024-28834](https://nvd.nist.gov/vuln/detail/CVE-2024-28834){: external}. |
| HAProxy | 295dba8 | 4e826da | Security fixes for [CVE-2024-28834](https://exchange.xforce.ibmcloud.com/vulnerabilities/CVE-2024-28834){: external}. |
{: caption="Changes since version 4.15.6_1525_openshift" caption-side="bottom"}


