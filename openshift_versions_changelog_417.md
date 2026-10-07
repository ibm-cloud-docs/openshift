---

copyright:
  years: 2024, 2026

lastupdated: "2026-10-07"


keywords: change log, version history, 4.17_openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}





# 4.17 version change log
{: #openshift_changelog_417}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run this version. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}



This version is deprecated. Update your cluster to a [supported version](/docs/openshift?topic=openshift-openshift_versions) as soon as possible.
{: deprecated}



## Overview
{: #changelog_overview_417}


Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security){: external} for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}

## Version 4.17
{: #417_components}


## 21 September 2026, Worker node fix pack 4.17.57_1600_openshift
{: #cl-boms-41757_1600_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.57_1600_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-687.47.1.el9_8
:   Resolves the following CVEs: [RHSA-2026:69126](https://access.redhat.com/errata/RHSA-2026:69126), [CVE-2026-8927](https://nvd.nist.gov/vuln/detail/cve-2026-8927), [RHSA-2026:67910](https://access.redhat.com/errata/RHSA-2026:67910), [CVE-2026-63381](https://nvd.nist.gov/vuln/detail/cve-2026-63381), [CVE-2026-63382](https://nvd.nist.gov/vuln/detail/cve-2026-63382), [CVE-2026-63383](https://nvd.nist.gov/vuln/detail/cve-2026-63383), [CVE-2026-63384](https://nvd.nist.gov/vuln/detail/cve-2026-63384), [CVE-2026-63385](https://nvd.nist.gov/vuln/detail/cve-2026-63385), [CVE-2026-63387](https://nvd.nist.gov/vuln/detail/cve-2026-63387), [CVE-2026-63388](https://nvd.nist.gov/vuln/detail/cve-2026-63388), [RHSA-2026:68011](https://access.redhat.com/errata/RHSA-2026:68011), [CVE-2025-35973](https://nvd.nist.gov/vuln/detail/cve-2025-35973), [RHSA-2026:69130](https://access.redhat.com/errata/RHSA-2026:69130), [CVE-2026-59999](https://nvd.nist.gov/vuln/detail/cve-2026-59999), [CVE-2026-73281](https://nvd.nist.gov/vuln/detail/cve-2026-73281), [CVE-2026-73282](https://nvd.nist.gov/vuln/detail/cve-2026-73282), [CVE-2026-73283](https://nvd.nist.gov/vuln/detail/cve-2026-73283), [RHSA-2026:67165](https://access.redhat.com/errata/RHSA-2026:67165), [CVE-2026-14457](https://nvd.nist.gov/vuln/detail/cve-2026-14457), [CVE-2026-18798](https://nvd.nist.gov/vuln/detail/cve-2026-18798), [CVE-2026-54874](https://nvd.nist.gov/vuln/detail/cve-2026-54874), [CVE-2026-63072](https://nvd.nist.gov/vuln/detail/cve-2026-63072), [CVE-2026-63073](https://nvd.nist.gov/vuln/detail/cve-2026-63073), [CVE-2026-63074](https://nvd.nist.gov/vuln/detail/cve-2026-63074), [CVE-2026-63075](https://nvd.nist.gov/vuln/detail/cve-2026-63075), [CVE-2026-63076](https://nvd.nist.gov/vuln/detail/cve-2026-63076), [RHSA-2026:69540](https://access.redhat.com/errata/RHSA-2026:69540), [RHSA-2026:69123](https://access.redhat.com/errata/RHSA-2026:69123), [RHSA-2026:66366](https://access.redhat.com/errata/RHSA-2026:66366), [CVE-2026-52859](https://nvd.nist.gov/vuln/detail/cve-2026-52859), [CVE-2026-55892](https://nvd.nist.gov/vuln/detail/cve-2026-55892), [CVE-2026-59857](https://nvd.nist.gov/vuln/detail/cve-2026-59857), [CVE-2026-73072](https://nvd.nist.gov/vuln/detail/cve-2026-73072), [CVE-2026-73076](https://nvd.nist.gov/vuln/detail/cve-2026-73076), [CVE-2026-73077](https://nvd.nist.gov/vuln/detail/cve-2026-73077), [CVE-2026-73078](https://nvd.nist.gov/vuln/detail/cve-2026-73078), [RHSA-2026:67583](https://access.redhat.com/errata/RHSA-2026:67583), [RHSA-2026:66403](https://access.redhat.com/errata/RHSA-2026:66403), [RHSA-2026:64812](https://access.redhat.com/errata/RHSA-2026:64812), [CVE-2026-56132](https://nvd.nist.gov/vuln/detail/cve-2026-56132), [RHSA-2026:67585](https://access.redhat.com/errata/RHSA-2026:67585), [RHSA-2026:64800](https://access.redhat.com/errata/RHSA-2026:64800), [RHSA-2026:67265](https://access.redhat.com/errata/RHSA-2026:67265), [CVE-2026-71226](https://nvd.nist.gov/vuln/detail/cve-2026-71226), [CVE-2026-71227](https://nvd.nist.gov/vuln/detail/cve-2026-71227), [RHSA-2026:64815](https://access.redhat.com/errata/RHSA-2026:64815), [RHSA-2026:67155](https://access.redhat.com/errata/RHSA-2026:67155), [RHSA-2026:64808](https://access.redhat.com/errata/RHSA-2026:64808), [CVE-2026-52933](https://nvd.nist.gov/vuln/detail/cve-2026-52933), [CVE-2026-53000](https://nvd.nist.gov/vuln/detail/cve-2026-53000), [CVE-2026-64136](https://nvd.nist.gov/vuln/detail/cve-2026-64136), [CVE-2026-64287](https://nvd.nist.gov/vuln/detail/cve-2026-64287), [CVE-2026-64319](https://nvd.nist.gov/vuln/detail/cve-2026-64319), [CVE-2026-64320](https://nvd.nist.gov/vuln/detail/cve-2026-64320), [CVE-2026-64384](https://nvd.nist.gov/vuln/detail/cve-2026-64384), [RHSA-2026:63129](https://access.redhat.com/errata/RHSA-2026:63129), [CVE-2025-71147](https://nvd.nist.gov/vuln/detail/cve-2025-71147), [CVE-2026-45970](https://nvd.nist.gov/vuln/detail/cve-2026-45970), [CVE-2026-46185](https://nvd.nist.gov/vuln/detail/cve-2026-46185), [CVE-2026-53073](https://nvd.nist.gov/vuln/detail/cve-2026-53073), [CVE-2026-53391](https://nvd.nist.gov/vuln/detail/cve-2026-53391), [CVE-2026-53392](https://nvd.nist.gov/vuln/detail/cve-2026-53392), [CVE-2026-53397](https://nvd.nist.gov/vuln/detail/cve-2026-53397), [CVE-2026-53399](https://nvd.nist.gov/vuln/detail/cve-2026-53399), [CVE-2026-63800](https://nvd.nist.gov/vuln/detail/cve-2026-63800), [CVE-2026-63808](https://nvd.nist.gov/vuln/detail/cve-2026-63808), [CVE-2026-63824](https://nvd.nist.gov/vuln/detail/cve-2026-63824), [CVE-2026-63886](https://nvd.nist.gov/vuln/detail/cve-2026-63886), [CVE-2026-63887](https://nvd.nist.gov/vuln/detail/cve-2026-63887), [CVE-2026-64002](https://nvd.nist.gov/vuln/detail/cve-2026-64002), [CVE-2026-64018](https://nvd.nist.gov/vuln/detail/cve-2026-64018), [CVE-2026-64268](https://nvd.nist.gov/vuln/detail/cve-2026-64268), [CVE-2026-64298](https://nvd.nist.gov/vuln/detail/cve-2026-64298), [CVE-2026-64304](https://nvd.nist.gov/vuln/detail/cve-2026-64304), [CVE-2026-64387](https://nvd.nist.gov/vuln/detail/cve-2026-64387), [CVE-2026-64438](https://nvd.nist.gov/vuln/detail/cve-2026-64438), [CVE-2026-64490](https://nvd.nist.gov/vuln/detail/cve-2026-64490), [CVE-2026-68145](https://nvd.nist.gov/vuln/detail/cve-2026-68145), [CVE-2026-68166](https://nvd.nist.gov/vuln/detail/cve-2026-68166), [CVE-2026-68480](https://nvd.nist.gov/vuln/detail/cve-2026-68480), [CVE-2026-72069](https://nvd.nist.gov/vuln/detail/cve-2026-72069), [CVE-2026-72130](https://nvd.nist.gov/vuln/detail/cve-2026-72130), [RHSA-2026:66180](https://access.redhat.com/errata/RHSA-2026:66180), [CVE-2026-43339](https://nvd.nist.gov/vuln/detail/cve-2026-43339), [CVE-2026-43493](https://nvd.nist.gov/vuln/detail/cve-2026-43493), [CVE-2026-46015](https://nvd.nist.gov/vuln/detail/cve-2026-46015), [CVE-2026-46149](https://nvd.nist.gov/vuln/detail/cve-2026-46149), [CVE-2026-46266](https://nvd.nist.gov/vuln/detail/cve-2026-46266), [CVE-2026-46306](https://nvd.nist.gov/vuln/detail/cve-2026-46306), [CVE-2026-46330](https://nvd.nist.gov/vuln/detail/cve-2026-46330), [CVE-2026-53002](https://nvd.nist.gov/vuln/detail/cve-2026-53002), [CVE-2026-53223](https://nvd.nist.gov/vuln/detail/cve-2026-53223), [CVE-2026-53275](https://nvd.nist.gov/vuln/detail/cve-2026-53275), [CVE-2026-53366](https://nvd.nist.gov/vuln/detail/cve-2026-53366), [CVE-2026-64034](https://nvd.nist.gov/vuln/detail/cve-2026-64034), [CVE-2026-64563](https://nvd.nist.gov/vuln/detail/cve-2026-64563), [CVE-2026-64597](https://nvd.nist.gov/vuln/detail/cve-2026-64597), [CVE-2026-72129](https://nvd.nist.gov/vuln/detail/cve-2026-72129), [CVE-2026-74480](https://nvd.nist.gov/vuln/detail/cve-2026-74480), [RHSA-2026:67150](https://access.redhat.com/errata/RHSA-2026:67150), [CVE-2026-23466](https://nvd.nist.gov/vuln/detail/cve-2026-23466), [CVE-2026-31479](https://nvd.nist.gov/vuln/detail/cve-2026-31479), [CVE-2026-31566](https://nvd.nist.gov/vuln/detail/cve-2026-31566), [CVE-2026-31656](https://nvd.nist.gov/vuln/detail/cve-2026-31656), [CVE-2026-31692](https://nvd.nist.gov/vuln/detail/cve-2026-31692), [CVE-2026-43334](https://nvd.nist.gov/vuln/detail/cve-2026-43334), [CVE-2026-43368](https://nvd.nist.gov/vuln/detail/cve-2026-43368), [CVE-2026-43370](https://nvd.nist.gov/vuln/detail/cve-2026-43370), [CVE-2026-52917](https://nvd.nist.gov/vuln/detail/cve-2026-52917), [CVE-2026-52918](https://nvd.nist.gov/vuln/detail/cve-2026-52918), [CVE-2026-52947](https://nvd.nist.gov/vuln/detail/cve-2026-52947), [CVE-2026-53053](https://nvd.nist.gov/vuln/detail/cve-2026-53053), [CVE-2026-53072](https://nvd.nist.gov/vuln/detail/cve-2026-53072), [CVE-2026-53091](https://nvd.nist.gov/vuln/detail/cve-2026-53091), [CVE-2026-53182](https://nvd.nist.gov/vuln/detail/cve-2026-53182), [CVE-2026-53209](https://nvd.nist.gov/vuln/detail/cve-2026-53209), [CVE-2026-53246](https://nvd.nist.gov/vuln/detail/cve-2026-53246), [CVE-2026-53254](https://nvd.nist.gov/vuln/detail/cve-2026-53254), [CVE-2026-53256](https://nvd.nist.gov/vuln/detail/cve-2026-53256), [CVE-2026-63801](https://nvd.nist.gov/vuln/detail/cve-2026-63801), [CVE-2026-63889](https://nvd.nist.gov/vuln/detail/cve-2026-63889), [CVE-2026-63944](https://nvd.nist.gov/vuln/detail/cve-2026-63944), [CVE-2026-63945](https://nvd.nist.gov/vuln/detail/cve-2026-63945), [CVE-2026-63946](https://nvd.nist.gov/vuln/detail/cve-2026-63946), [CVE-2026-63947](https://nvd.nist.gov/vuln/detail/cve-2026-63947), [CVE-2026-63971](https://nvd.nist.gov/vuln/detail/cve-2026-63971), [CVE-2026-63975](https://nvd.nist.gov/vuln/detail/cve-2026-63975), [CVE-2026-64037](https://nvd.nist.gov/vuln/detail/cve-2026-64037), [CVE-2026-64113](https://nvd.nist.gov/vuln/detail/cve-2026-64113), [CVE-2026-64117](https://nvd.nist.gov/vuln/detail/cve-2026-64117), [CVE-2026-64255](https://nvd.nist.gov/vuln/detail/cve-2026-64255), [CVE-2026-64515](https://nvd.nist.gov/vuln/detail/cve-2026-64515), [CVE-2026-68086](https://nvd.nist.gov/vuln/detail/cve-2026-68086), [CVE-2026-68117](https://nvd.nist.gov/vuln/detail/cve-2026-68117), [CVE-2026-68264](https://nvd.nist.gov/vuln/detail/cve-2026-68264), [CVE-2026-68300](https://nvd.nist.gov/vuln/detail/cve-2026-68300), [CVE-2026-68315](https://nvd.nist.gov/vuln/detail/cve-2026-68315), [CVE-2026-68376](https://nvd.nist.gov/vuln/detail/cve-2026-68376), [CVE-2026-68402](https://nvd.nist.gov/vuln/detail/cve-2026-68402), [CVE-2026-68406](https://nvd.nist.gov/vuln/detail/cve-2026-68406), and [CVE-2026-72098](https://nvd.nist.gov/vuln/detail/cve-2026-72098).


RHEL 9 (Satellite) 5.14.0-687.47.1.el9_8
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-687.47.1.el9_8
:   Resolves the following CVEs: [RHSA-2026:69126](https://access.redhat.com/errata/RHSA-2026:69126), [CVE-2026-8927](https://nvd.nist.gov/vuln/detail/cve-2026-8927), [RHSA-2026:67910](https://access.redhat.com/errata/RHSA-2026:67910), [CVE-2026-63381](https://nvd.nist.gov/vuln/detail/cve-2026-63381), [CVE-2026-63382](https://nvd.nist.gov/vuln/detail/cve-2026-63382), [CVE-2026-63383](https://nvd.nist.gov/vuln/detail/cve-2026-63383), [CVE-2026-63384](https://nvd.nist.gov/vuln/detail/cve-2026-63384), [CVE-2026-63385](https://nvd.nist.gov/vuln/detail/cve-2026-63385), [CVE-2026-63387](https://nvd.nist.gov/vuln/detail/cve-2026-63387), [CVE-2026-63388](https://nvd.nist.gov/vuln/detail/cve-2026-63388), [RHSA-2026:68011](https://access.redhat.com/errata/RHSA-2026:68011), [CVE-2025-35973](https://nvd.nist.gov/vuln/detail/cve-2025-35973), [RHSA-2026:69130](https://access.redhat.com/errata/RHSA-2026:69130), [CVE-2026-59999](https://nvd.nist.gov/vuln/detail/cve-2026-59999), [CVE-2026-73281](https://nvd.nist.gov/vuln/detail/cve-2026-73281), [CVE-2026-73282](https://nvd.nist.gov/vuln/detail/cve-2026-73282), [CVE-2026-73283](https://nvd.nist.gov/vuln/detail/cve-2026-73283), [RHSA-2026:67165](https://access.redhat.com/errata/RHSA-2026:67165), [CVE-2026-14457](https://nvd.nist.gov/vuln/detail/cve-2026-14457), [CVE-2026-18798](https://nvd.nist.gov/vuln/detail/cve-2026-18798), [CVE-2026-54874](https://nvd.nist.gov/vuln/detail/cve-2026-54874), [CVE-2026-63072](https://nvd.nist.gov/vuln/detail/cve-2026-63072), [CVE-2026-63073](https://nvd.nist.gov/vuln/detail/cve-2026-63073), [CVE-2026-63074](https://nvd.nist.gov/vuln/detail/cve-2026-63074), [CVE-2026-63075](https://nvd.nist.gov/vuln/detail/cve-2026-63075), [CVE-2026-63076](https://nvd.nist.gov/vuln/detail/cve-2026-63076), [RHSA-2026:69540](https://access.redhat.com/errata/RHSA-2026:69540), [RHSA-2026:69123](https://access.redhat.com/errata/RHSA-2026:69123), [RHSA-2026:66366](https://access.redhat.com/errata/RHSA-2026:66366), [CVE-2026-52859](https://nvd.nist.gov/vuln/detail/cve-2026-52859), [CVE-2026-55892](https://nvd.nist.gov/vuln/detail/cve-2026-55892), [CVE-2026-59857](https://nvd.nist.gov/vuln/detail/cve-2026-59857), [CVE-2026-73072](https://nvd.nist.gov/vuln/detail/cve-2026-73072), [CVE-2026-73076](https://nvd.nist.gov/vuln/detail/cve-2026-73076), [CVE-2026-73077](https://nvd.nist.gov/vuln/detail/cve-2026-73077), [CVE-2026-73078](https://nvd.nist.gov/vuln/detail/cve-2026-73078), [RHSA-2026:67583](https://access.redhat.com/errata/RHSA-2026:67583), [RHSA-2026:66403](https://access.redhat.com/errata/RHSA-2026:66403), [RHSA-2026:64812](https://access.redhat.com/errata/RHSA-2026:64812), [CVE-2026-56132](https://nvd.nist.gov/vuln/detail/cve-2026-56132), [RHSA-2026:67585](https://access.redhat.com/errata/RHSA-2026:67585), [RHSA-2026:64800](https://access.redhat.com/errata/RHSA-2026:64800), [RHSA-2026:67265](https://access.redhat.com/errata/RHSA-2026:67265), [CVE-2026-71226](https://nvd.nist.gov/vuln/detail/cve-2026-71226), [CVE-2026-71227](https://nvd.nist.gov/vuln/detail/cve-2026-71227), [RHSA-2026:64815](https://access.redhat.com/errata/RHSA-2026:64815), [RHSA-2026:67155](https://access.redhat.com/errata/RHSA-2026:67155), [RHSA-2026:64808](https://access.redhat.com/errata/RHSA-2026:64808), [CVE-2026-52933](https://nvd.nist.gov/vuln/detail/cve-2026-52933), [CVE-2026-53000](https://nvd.nist.gov/vuln/detail/cve-2026-53000), [CVE-2026-64136](https://nvd.nist.gov/vuln/detail/cve-2026-64136), [CVE-2026-64287](https://nvd.nist.gov/vuln/detail/cve-2026-64287), [CVE-2026-64319](https://nvd.nist.gov/vuln/detail/cve-2026-64319), [CVE-2026-64320](https://nvd.nist.gov/vuln/detail/cve-2026-64320), [CVE-2026-64384](https://nvd.nist.gov/vuln/detail/cve-2026-64384), [RHSA-2026:63129](https://access.redhat.com/errata/RHSA-2026:63129), [CVE-2025-71147](https://nvd.nist.gov/vuln/detail/cve-2025-71147), [CVE-2026-45970](https://nvd.nist.gov/vuln/detail/cve-2026-45970), [CVE-2026-46185](https://nvd.nist.gov/vuln/detail/cve-2026-46185), [CVE-2026-53073](https://nvd.nist.gov/vuln/detail/cve-2026-53073), [CVE-2026-53391](https://nvd.nist.gov/vuln/detail/cve-2026-53391), [CVE-2026-53392](https://nvd.nist.gov/vuln/detail/cve-2026-53392), [CVE-2026-53397](https://nvd.nist.gov/vuln/detail/cve-2026-53397), [CVE-2026-53399](https://nvd.nist.gov/vuln/detail/cve-2026-53399), [CVE-2026-63800](https://nvd.nist.gov/vuln/detail/cve-2026-63800), [CVE-2026-63808](https://nvd.nist.gov/vuln/detail/cve-2026-63808), [CVE-2026-63824](https://nvd.nist.gov/vuln/detail/cve-2026-63824), [CVE-2026-63886](https://nvd.nist.gov/vuln/detail/cve-2026-63886), [CVE-2026-63887](https://nvd.nist.gov/vuln/detail/cve-2026-63887), [CVE-2026-64002](https://nvd.nist.gov/vuln/detail/cve-2026-64002), [CVE-2026-64018](https://nvd.nist.gov/vuln/detail/cve-2026-64018), [CVE-2026-64268](https://nvd.nist.gov/vuln/detail/cve-2026-64268), [CVE-2026-64298](https://nvd.nist.gov/vuln/detail/cve-2026-64298), [CVE-2026-64304](https://nvd.nist.gov/vuln/detail/cve-2026-64304), [CVE-2026-64387](https://nvd.nist.gov/vuln/detail/cve-2026-64387), [CVE-2026-64438](https://nvd.nist.gov/vuln/detail/cve-2026-64438), [CVE-2026-64490](https://nvd.nist.gov/vuln/detail/cve-2026-64490), [CVE-2026-68145](https://nvd.nist.gov/vuln/detail/cve-2026-68145), [CVE-2026-68166](https://nvd.nist.gov/vuln/detail/cve-2026-68166), [CVE-2026-68480](https://nvd.nist.gov/vuln/detail/cve-2026-68480), [CVE-2026-72069](https://nvd.nist.gov/vuln/detail/cve-2026-72069), [CVE-2026-72130](https://nvd.nist.gov/vuln/detail/cve-2026-72130), [RHSA-2026:66180](https://access.redhat.com/errata/RHSA-2026:66180), [CVE-2026-43339](https://nvd.nist.gov/vuln/detail/cve-2026-43339), [CVE-2026-43493](https://nvd.nist.gov/vuln/detail/cve-2026-43493), [CVE-2026-46015](https://nvd.nist.gov/vuln/detail/cve-2026-46015), [CVE-2026-46149](https://nvd.nist.gov/vuln/detail/cve-2026-46149), [CVE-2026-46266](https://nvd.nist.gov/vuln/detail/cve-2026-46266), [CVE-2026-46306](https://nvd.nist.gov/vuln/detail/cve-2026-46306), [CVE-2026-46330](https://nvd.nist.gov/vuln/detail/cve-2026-46330), [CVE-2026-53002](https://nvd.nist.gov/vuln/detail/cve-2026-53002), [CVE-2026-53223](https://nvd.nist.gov/vuln/detail/cve-2026-53223), [CVE-2026-53275](https://nvd.nist.gov/vuln/detail/cve-2026-53275), [CVE-2026-53366](https://nvd.nist.gov/vuln/detail/cve-2026-53366), [CVE-2026-64034](https://nvd.nist.gov/vuln/detail/cve-2026-64034), [CVE-2026-64563](https://nvd.nist.gov/vuln/detail/cve-2026-64563), [CVE-2026-64597](https://nvd.nist.gov/vuln/detail/cve-2026-64597), [CVE-2026-72129](https://nvd.nist.gov/vuln/detail/cve-2026-72129), [CVE-2026-74480](https://nvd.nist.gov/vuln/detail/cve-2026-74480), [RHSA-2026:67150](https://access.redhat.com/errata/RHSA-2026:67150), [CVE-2026-23466](https://nvd.nist.gov/vuln/detail/cve-2026-23466), [CVE-2026-31479](https://nvd.nist.gov/vuln/detail/cve-2026-31479), [CVE-2026-31566](https://nvd.nist.gov/vuln/detail/cve-2026-31566), [CVE-2026-31656](https://nvd.nist.gov/vuln/detail/cve-2026-31656), [CVE-2026-31692](https://nvd.nist.gov/vuln/detail/cve-2026-31692), [CVE-2026-43334](https://nvd.nist.gov/vuln/detail/cve-2026-43334), [CVE-2026-43368](https://nvd.nist.gov/vuln/detail/cve-2026-43368), [CVE-2026-43370](https://nvd.nist.gov/vuln/detail/cve-2026-43370), [CVE-2026-52917](https://nvd.nist.gov/vuln/detail/cve-2026-52917), [CVE-2026-52918](https://nvd.nist.gov/vuln/detail/cve-2026-52918), [CVE-2026-52947](https://nvd.nist.gov/vuln/detail/cve-2026-52947), [CVE-2026-53053](https://nvd.nist.gov/vuln/detail/cve-2026-53053), [CVE-2026-53072](https://nvd.nist.gov/vuln/detail/cve-2026-53072), [CVE-2026-53091](https://nvd.nist.gov/vuln/detail/cve-2026-53091), [CVE-2026-53182](https://nvd.nist.gov/vuln/detail/cve-2026-53182), [CVE-2026-53209](https://nvd.nist.gov/vuln/detail/cve-2026-53209), [CVE-2026-53246](https://nvd.nist.gov/vuln/detail/cve-2026-53246), [CVE-2026-53254](https://nvd.nist.gov/vuln/detail/cve-2026-53254), [CVE-2026-53256](https://nvd.nist.gov/vuln/detail/cve-2026-53256), [CVE-2026-63801](https://nvd.nist.gov/vuln/detail/cve-2026-63801), [CVE-2026-63889](https://nvd.nist.gov/vuln/detail/cve-2026-63889), [CVE-2026-63944](https://nvd.nist.gov/vuln/detail/cve-2026-63944), [CVE-2026-63945](https://nvd.nist.gov/vuln/detail/cve-2026-63945), [CVE-2026-63946](https://nvd.nist.gov/vuln/detail/cve-2026-63946), [CVE-2026-63947](https://nvd.nist.gov/vuln/detail/cve-2026-63947), [CVE-2026-63971](https://nvd.nist.gov/vuln/detail/cve-2026-63971), [CVE-2026-63975](https://nvd.nist.gov/vuln/detail/cve-2026-63975), [CVE-2026-64037](https://nvd.nist.gov/vuln/detail/cve-2026-64037), [CVE-2026-64113](https://nvd.nist.gov/vuln/detail/cve-2026-64113), [CVE-2026-64117](https://nvd.nist.gov/vuln/detail/cve-2026-64117), [CVE-2026-64255](https://nvd.nist.gov/vuln/detail/cve-2026-64255), [CVE-2026-64515](https://nvd.nist.gov/vuln/detail/cve-2026-64515), [CVE-2026-68086](https://nvd.nist.gov/vuln/detail/cve-2026-68086), [CVE-2026-68117](https://nvd.nist.gov/vuln/detail/cve-2026-68117), [CVE-2026-68264](https://nvd.nist.gov/vuln/detail/cve-2026-68264), [CVE-2026-68300](https://nvd.nist.gov/vuln/detail/cve-2026-68300), [CVE-2026-68315](https://nvd.nist.gov/vuln/detail/cve-2026-68315), [CVE-2026-68376](https://nvd.nist.gov/vuln/detail/cve-2026-68376), [CVE-2026-68402](https://nvd.nist.gov/vuln/detail/cve-2026-68402), [CVE-2026-68406](https://nvd.nist.gov/vuln/detail/cve-2026-68406), and [CVE-2026-72098](https://nvd.nist.gov/vuln/detail/cve-2026-72098).


RHEL 8 (VPC) 4.18.0-553.162.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:63163](https://access.redhat.com/errata/RHSA-2026:63163), [CVE-2026-33818](https://nvd.nist.gov/vuln/detail/cve-2026-33818), [CVE-2026-42499](https://nvd.nist.gov/vuln/detail/cve-2026-42499), [CVE-2026-56853](https://nvd.nist.gov/vuln/detail/cve-2026-56853), [CVE-2026-56858](https://nvd.nist.gov/vuln/detail/cve-2026-56858), [CVE-2026-56859](https://nvd.nist.gov/vuln/detail/cve-2026-56859), [CVE-2026-56860](https://nvd.nist.gov/vuln/detail/cve-2026-56860), [CVE-2026-56862](https://nvd.nist.gov/vuln/detail/cve-2026-56862), [RHSA-2026:66000](https://access.redhat.com/errata/RHSA-2026:66000), [CVE-2026-43493](https://nvd.nist.gov/vuln/detail/cve-2026-43493), [CVE-2026-53002](https://nvd.nist.gov/vuln/detail/cve-2026-53002), [CVE-2026-64007](https://nvd.nist.gov/vuln/detail/cve-2026-64007), [CVE-2026-64563](https://nvd.nist.gov/vuln/detail/cve-2026-64563), [CVE-2026-68343](https://nvd.nist.gov/vuln/detail/cve-2026-68343), [CVE-2026-72129](https://nvd.nist.gov/vuln/detail/cve-2026-72129), [CVE-2026-74480](https://nvd.nist.gov/vuln/detail/cve-2026-74480), [RHSA-2026:63014](https://access.redhat.com/errata/RHSA-2026:63014), [CVE-2024-57849](https://nvd.nist.gov/vuln/detail/cve-2024-57849), [CVE-2025-71132](https://nvd.nist.gov/vuln/detail/cve-2025-71132), [CVE-2026-45970](https://nvd.nist.gov/vuln/detail/cve-2026-45970), [CVE-2026-53185](https://nvd.nist.gov/vuln/detail/cve-2026-53185), [CVE-2026-53391](https://nvd.nist.gov/vuln/detail/cve-2026-53391), [CVE-2026-53392](https://nvd.nist.gov/vuln/detail/cve-2026-53392), [CVE-2026-53397](https://nvd.nist.gov/vuln/detail/cve-2026-53397), [CVE-2026-53399](https://nvd.nist.gov/vuln/detail/cve-2026-53399), [CVE-2026-63800](https://nvd.nist.gov/vuln/detail/cve-2026-63800), [CVE-2026-64018](https://nvd.nist.gov/vuln/detail/cve-2026-64018), [CVE-2026-64268](https://nvd.nist.gov/vuln/detail/cve-2026-64268), [CVE-2026-64298](https://nvd.nist.gov/vuln/detail/cve-2026-64298), [CVE-2026-68480](https://nvd.nist.gov/vuln/detail/cve-2026-68480), [CVE-2026-74581](https://nvd.nist.gov/vuln/detail/cve-2026-74581), [RHSA-2026:66325](https://access.redhat.com/errata/RHSA-2026:66325), [CVE-2025-68745](https://nvd.nist.gov/vuln/detail/cve-2025-68745), [CVE-2026-46149](https://nvd.nist.gov/vuln/detail/cve-2026-46149), [CVE-2026-52917](https://nvd.nist.gov/vuln/detail/cve-2026-52917), [CVE-2026-52942](https://nvd.nist.gov/vuln/detail/cve-2026-52942), [CVE-2026-52986](https://nvd.nist.gov/vuln/detail/cve-2026-52986), [CVE-2026-53091](https://nvd.nist.gov/vuln/detail/cve-2026-53091), [CVE-2026-53246](https://nvd.nist.gov/vuln/detail/cve-2026-53246), [CVE-2026-63801](https://nvd.nist.gov/vuln/detail/cve-2026-63801), [CVE-2026-63971](https://nvd.nist.gov/vuln/detail/cve-2026-63971), [CVE-2026-64015](https://nvd.nist.gov/vuln/detail/cve-2026-64015), [CVE-2026-64113](https://nvd.nist.gov/vuln/detail/cve-2026-64113), [CVE-2026-68117](https://nvd.nist.gov/vuln/detail/cve-2026-68117), [CVE-2026-68300](https://nvd.nist.gov/vuln/detail/cve-2026-68300), [CVE-2026-68315](https://nvd.nist.gov/vuln/detail/cve-2026-68315), [CVE-2026-68376](https://nvd.nist.gov/vuln/detail/cve-2026-68376), [RHSA-2026:67908](https://access.redhat.com/errata/RHSA-2026:67908), [CVE-2026-63382](https://nvd.nist.gov/vuln/detail/cve-2026-63382), [CVE-2026-63383](https://nvd.nist.gov/vuln/detail/cve-2026-63383), [CVE-2026-63384](https://nvd.nist.gov/vuln/detail/cve-2026-63384), [CVE-2026-63385](https://nvd.nist.gov/vuln/detail/cve-2026-63385), [CVE-2026-63387](https://nvd.nist.gov/vuln/detail/cve-2026-63387), [CVE-2026-63388](https://nvd.nist.gov/vuln/detail/cve-2026-63388), [RHSA-2026:65147](https://access.redhat.com/errata/RHSA-2026:65147), [CVE-2025-31936](https://nvd.nist.gov/vuln/detail/cve-2025-31936), [CVE-2025-35973](https://nvd.nist.gov/vuln/detail/cve-2025-35973), [RHSA-2026:64786](https://access.redhat.com/errata/RHSA-2026:64786), [CVE-2026-33818](https://nvd.nist.gov/vuln/detail/cve-2026-33818), [CVE-2026-56853](https://nvd.nist.gov/vuln/detail/cve-2026-56853), [CVE-2026-56860](https://nvd.nist.gov/vuln/detail/cve-2026-56860), [CVE-2026-56862](https://nvd.nist.gov/vuln/detail/cve-2026-56862), [RHSA-2026:66348](https://access.redhat.com/errata/RHSA-2026:66348), [CVE-2026-28420](https://nvd.nist.gov/vuln/detail/cve-2026-28420), [CVE-2026-52859](https://nvd.nist.gov/vuln/detail/cve-2026-52859), [CVE-2026-55892](https://nvd.nist.gov/vuln/detail/cve-2026-55892), [CVE-2026-59857](https://nvd.nist.gov/vuln/detail/cve-2026-59857), [CVE-2026-73072](https://nvd.nist.gov/vuln/detail/cve-2026-73072), [CVE-2026-73076](https://nvd.nist.gov/vuln/detail/cve-2026-73076), [CVE-2026-73078](https://nvd.nist.gov/vuln/detail/cve-2026-73078), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:64809](https://access.redhat.com/errata/RHSA-2026:64809), [CVE-2026-50219](https://nvd.nist.gov/vuln/detail/cve-2026-50219), [CVE-2026-56132](https://nvd.nist.gov/vuln/detail/cve-2026-56132), [RHSA-2026:66451](https://access.redhat.com/errata/RHSA-2026:66451), [CVE-2026-16118](https://nvd.nist.gov/vuln/detail/cve-2026-16118), [RHSA-2026:65998](https://access.redhat.com/errata/RHSA-2026:65998), [CVE-2026-41991](https://nvd.nist.gov/vuln/detail/cve-2026-41991), [CVE-2026-41992](https://nvd.nist.gov/vuln/detail/cve-2026-41992), [RHSA-2026:67266](https://access.redhat.com/errata/RHSA-2026:67266), [CVE-2026-71225](https://nvd.nist.gov/vuln/detail/cve-2026-71225), [CVE-2026-71226](https://nvd.nist.gov/vuln/detail/cve-2026-71226), [CVE-2026-71227](https://nvd.nist.gov/vuln/detail/cve-2026-71227), [RHSA-2026:68266](https://access.redhat.com/errata/RHSA-2026:68266), [CVE-2026-15711](https://nvd.nist.gov/vuln/detail/cve-2026-15711), [RHSA-2026:67162](https://access.redhat.com/errata/RHSA-2026:67162), and [CVE-2026-13221](https://nvd.nist.gov/vuln/detail/cve-2026-13221).


RHEL 8 (Classic) 4.18.0-553.162.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:66000](https://access.redhat.com/errata/RHSA-2026:66000), [CVE-2026-43493](https://nvd.nist.gov/vuln/detail/cve-2026-43493), [CVE-2026-53002](https://nvd.nist.gov/vuln/detail/cve-2026-53002), [CVE-2026-64007](https://nvd.nist.gov/vuln/detail/cve-2026-64007), [CVE-2026-64563](https://nvd.nist.gov/vuln/detail/cve-2026-64563), [CVE-2026-68343](https://nvd.nist.gov/vuln/detail/cve-2026-68343), [CVE-2026-72129](https://nvd.nist.gov/vuln/detail/cve-2026-72129), [CVE-2026-74480](https://nvd.nist.gov/vuln/detail/cve-2026-74480), [RHSA-2026:63014](https://access.redhat.com/errata/RHSA-2026:63014), [CVE-2024-57849](https://nvd.nist.gov/vuln/detail/cve-2024-57849), [CVE-2025-71132](https://nvd.nist.gov/vuln/detail/cve-2025-71132), [CVE-2026-45970](https://nvd.nist.gov/vuln/detail/cve-2026-45970), [CVE-2026-53185](https://nvd.nist.gov/vuln/detail/cve-2026-53185), [CVE-2026-53391](https://nvd.nist.gov/vuln/detail/cve-2026-53391), [CVE-2026-53392](https://nvd.nist.gov/vuln/detail/cve-2026-53392), [CVE-2026-53397](https://nvd.nist.gov/vuln/detail/cve-2026-53397), [CVE-2026-53399](https://nvd.nist.gov/vuln/detail/cve-2026-53399), [CVE-2026-63800](https://nvd.nist.gov/vuln/detail/cve-2026-63800), [CVE-2026-64018](https://nvd.nist.gov/vuln/detail/cve-2026-64018), [CVE-2026-64268](https://nvd.nist.gov/vuln/detail/cve-2026-64268), [CVE-2026-64298](https://nvd.nist.gov/vuln/detail/cve-2026-64298), [CVE-2026-68480](https://nvd.nist.gov/vuln/detail/cve-2026-68480), [CVE-2026-74581](https://nvd.nist.gov/vuln/detail/cve-2026-74581), [RHSA-2026:66325](https://access.redhat.com/errata/RHSA-2026:66325), [CVE-2025-68745](https://nvd.nist.gov/vuln/detail/cve-2025-68745), [CVE-2026-46149](https://nvd.nist.gov/vuln/detail/cve-2026-46149), [CVE-2026-52917](https://nvd.nist.gov/vuln/detail/cve-2026-52917), [CVE-2026-52942](https://nvd.nist.gov/vuln/detail/cve-2026-52942), [CVE-2026-52986](https://nvd.nist.gov/vuln/detail/cve-2026-52986), [CVE-2026-53091](https://nvd.nist.gov/vuln/detail/cve-2026-53091), [CVE-2026-53246](https://nvd.nist.gov/vuln/detail/cve-2026-53246), [CVE-2026-63801](https://nvd.nist.gov/vuln/detail/cve-2026-63801), [CVE-2026-63971](https://nvd.nist.gov/vuln/detail/cve-2026-63971), [CVE-2026-64015](https://nvd.nist.gov/vuln/detail/cve-2026-64015), [CVE-2026-64113](https://nvd.nist.gov/vuln/detail/cve-2026-64113), [CVE-2026-68117](https://nvd.nist.gov/vuln/detail/cve-2026-68117), [CVE-2026-68300](https://nvd.nist.gov/vuln/detail/cve-2026-68300), [CVE-2026-68315](https://nvd.nist.gov/vuln/detail/cve-2026-68315), [CVE-2026-68376](https://nvd.nist.gov/vuln/detail/cve-2026-68376), [RHSA-2026:67908](https://access.redhat.com/errata/RHSA-2026:67908), [CVE-2026-63382](https://nvd.nist.gov/vuln/detail/cve-2026-63382), [CVE-2026-63383](https://nvd.nist.gov/vuln/detail/cve-2026-63383), [CVE-2026-63384](https://nvd.nist.gov/vuln/detail/cve-2026-63384), [CVE-2026-63385](https://nvd.nist.gov/vuln/detail/cve-2026-63385), [CVE-2026-63387](https://nvd.nist.gov/vuln/detail/cve-2026-63387), [CVE-2026-63388](https://nvd.nist.gov/vuln/detail/cve-2026-63388), [RHSA-2026:65147](https://access.redhat.com/errata/RHSA-2026:65147), [CVE-2025-31936](https://nvd.nist.gov/vuln/detail/cve-2025-31936), [CVE-2025-35973](https://nvd.nist.gov/vuln/detail/cve-2025-35973), [RHSA-2026:64786](https://access.redhat.com/errata/RHSA-2026:64786), [CVE-2026-33818](https://nvd.nist.gov/vuln/detail/cve-2026-33818), [CVE-2026-56853](https://nvd.nist.gov/vuln/detail/cve-2026-56853), [CVE-2026-56860](https://nvd.nist.gov/vuln/detail/cve-2026-56860), [CVE-2026-56862](https://nvd.nist.gov/vuln/detail/cve-2026-56862), [RHSA-2026:66348](https://access.redhat.com/errata/RHSA-2026:66348), [CVE-2026-28420](https://nvd.nist.gov/vuln/detail/cve-2026-28420), [CVE-2026-52859](https://nvd.nist.gov/vuln/detail/cve-2026-52859), [CVE-2026-55892](https://nvd.nist.gov/vuln/detail/cve-2026-55892), [CVE-2026-59857](https://nvd.nist.gov/vuln/detail/cve-2026-59857), [CVE-2026-73072](https://nvd.nist.gov/vuln/detail/cve-2026-73072), [CVE-2026-73076](https://nvd.nist.gov/vuln/detail/cve-2026-73076), [CVE-2026-73078](https://nvd.nist.gov/vuln/detail/cve-2026-73078), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:64809](https://access.redhat.com/errata/RHSA-2026:64809), [CVE-2026-50219](https://nvd.nist.gov/vuln/detail/cve-2026-50219), [CVE-2026-56132](https://nvd.nist.gov/vuln/detail/cve-2026-56132), [RHSA-2026:66451](https://access.redhat.com/errata/RHSA-2026:66451), [CVE-2026-16118](https://nvd.nist.gov/vuln/detail/cve-2026-16118), [RHSA-2026:65998](https://access.redhat.com/errata/RHSA-2026:65998), [CVE-2026-41991](https://nvd.nist.gov/vuln/detail/cve-2026-41991), [CVE-2026-41992](https://nvd.nist.gov/vuln/detail/cve-2026-41992), [RHSA-2026:67266](https://access.redhat.com/errata/RHSA-2026:67266), [CVE-2026-71225](https://nvd.nist.gov/vuln/detail/cve-2026-71225), [CVE-2026-71226](https://nvd.nist.gov/vuln/detail/cve-2026-71226), [CVE-2026-71227](https://nvd.nist.gov/vuln/detail/cve-2026-71227), [RHSA-2026:67162](https://access.redhat.com/errata/RHSA-2026:67162), and [CVE-2026-13221](https://nvd.nist.gov/vuln/detail/cve-2026-13221).


Red Hat OpenShift 4.17.57
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-57_release-notes){: external}.


Red Hat CoreOS 4.17.57
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-57_release-notes){: external}.


HAProxy b08f074d475aeb8ba959b03272daab5d46deec0c
:   Resolves the following CVEs: [CVE-2026-41991](https://nvd.nist.gov/vuln/detail/cve-2026-41991), [CVE-2026-50219](https://nvd.nist.gov/vuln/detail/cve-2026-50219), [CVE-2026-16118](https://nvd.nist.gov/vuln/detail/cve-2026-16118), [CVE-2026-56132](https://nvd.nist.gov/vuln/detail/cve-2026-56132), and [CVE-2026-41992](https://nvd.nist.gov/vuln/detail/cve-2026-41992).


## 21 September 2026, Master fix pack 4.17.56_1599_openshift
{: #cl-boms_master-41756_1599_openshift_M}

The following list shows the components that are in the master fix pack 4.17.56_1599_openshift. Master patch updates are applied automatically.
{: shortdesc}

Cluster health image v1.6.19
:   New version contains updates and security fixes.


etcd v3.5.33
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.33){: external}.


IBM Cloud Block Storage driver and plug-in v2.5.28
:   New version contains updates and security fixes.


IBM Cloud Controller Manager v1.30.14-55
:   New version contains updates and security fixes.


IBM Cloud File Storage for Classic plug-in and monitor v457
:   New version contains updates and security fixes.


IBM Cloud RBAC Operator 109756b
:   New version contains updates and security fixes.


Key Management Service provider 2.10.30
:   New version contains updates and security fixes.


Portieris admission controller v0.14.3
:   See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.14.3){: external}


Red Hat OpenShift on IBM Cloud 4.17.56
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-56_release-notes){: external}.


## 08 September 2026, Worker node fix pack 4.17.57_1598_openshift
{: #cl-boms-41757_1598_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.57_1598_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-687.42.1.el9_8
:   Resolves the following CVEs: [RHSA-2026:63130](https://access.redhat.com/errata/RHSA-2026:63130), [CVE-2026-33818](https://nvd.nist.gov/vuln/detail/cve-2026-33818), [CVE-2026-56858](https://nvd.nist.gov/vuln/detail/cve-2026-56858), [CVE-2026-56860](https://nvd.nist.gov/vuln/detail/cve-2026-56860), [CVE-2026-56862](https://nvd.nist.gov/vuln/detail/cve-2026-56862), [RHSA-2026:58936](https://access.redhat.com/errata/RHSA-2026:58936), [CVE-2026-11822](https://nvd.nist.gov/vuln/detail/cve-2026-11822), [CVE-2026-11824](https://nvd.nist.gov/vuln/detail/cve-2026-11824), [RHSA-2026:60226](https://access.redhat.com/errata/RHSA-2026:60226), [CVE-2026-54371](https://nvd.nist.gov/vuln/detail/cve-2026-54371), [RHSA-2026:61355](https://access.redhat.com/errata/RHSA-2026:61355), [CVE-2026-16730](https://nvd.nist.gov/vuln/detail/cve-2026-16730), [RHSA-2026:61623](https://access.redhat.com/errata/RHSA-2026:61623), [CVE-2026-41991](https://nvd.nist.gov/vuln/detail/cve-2026-41991), [CVE-2026-41992](https://nvd.nist.gov/vuln/detail/cve-2026-41992), [RHSA-2026:62217](https://access.redhat.com/errata/RHSA-2026:62217), [CVE-2026-59843](https://nvd.nist.gov/vuln/detail/cve-2026-59843), [CVE-2026-59844](https://nvd.nist.gov/vuln/detail/cve-2026-59844), [CVE-2026-59845](https://nvd.nist.gov/vuln/detail/cve-2026-59845), [CVE-2026-59846](https://nvd.nist.gov/vuln/detail/cve-2026-59846), [CVE-2026-59847](https://nvd.nist.gov/vuln/detail/cve-2026-59847), [CVE-2026-59848](https://nvd.nist.gov/vuln/detail/cve-2026-59848), [CVE-2026-59850](https://nvd.nist.gov/vuln/detail/cve-2026-59850), [RHSA-2026:61247](https://access.redhat.com/errata/RHSA-2026:61247), [CVE-2026-11979](https://nvd.nist.gov/vuln/detail/cve-2026-11979), [CVE-2026-6653](https://nvd.nist.gov/vuln/detail/cve-2026-6653), [RHSA-2026:58572](https://access.redhat.com/errata/RHSA-2026:58572), [CVE-2026-10805](https://nvd.nist.gov/vuln/detail/cve-2026-10805), [RHSA-2026:61581](https://access.redhat.com/errata/RHSA-2026:61581), [CVE-2026-18477](https://nvd.nist.gov/vuln/detail/cve-2026-18477), [CVE-2026-18508](https://nvd.nist.gov/vuln/detail/cve-2026-18508), [CVE-2026-5704](https://nvd.nist.gov/vuln/detail/cve-2026-5704), [RHSA-2026:62143](https://access.redhat.com/errata/RHSA-2026:62143), [CVE-2026-58471](https://nvd.nist.gov/vuln/detail/cve-2026-58471), [CVE-2026-58472](https://nvd.nist.gov/vuln/detail/cve-2026-58472), [RHSA-2026:57252](https://access.redhat.com/errata/RHSA-2026:57252), [CVE-2026-43206](https://nvd.nist.gov/vuln/detail/cve-2026-43206), [CVE-2026-43233](https://nvd.nist.gov/vuln/detail/cve-2026-43233), [CVE-2026-43237](https://nvd.nist.gov/vuln/detail/cve-2026-43237), [CVE-2026-45878](https://nvd.nist.gov/vuln/detail/cve-2026-45878), [CVE-2026-45991](https://nvd.nist.gov/vuln/detail/cve-2026-45991), [CVE-2026-46120](https://nvd.nist.gov/vuln/detail/cve-2026-46120), [CVE-2026-52991](https://nvd.nist.gov/vuln/detail/cve-2026-52991), [CVE-2026-53136](https://nvd.nist.gov/vuln/detail/cve-2026-53136), [CVE-2026-53143](https://nvd.nist.gov/vuln/detail/cve-2026-53143), [CVE-2026-53189](https://nvd.nist.gov/vuln/detail/cve-2026-53189), [CVE-2026-53329](https://nvd.nist.gov/vuln/detail/cve-2026-53329), [CVE-2026-53356](https://nvd.nist.gov/vuln/detail/cve-2026-53356), [CVE-2026-53374](https://nvd.nist.gov/vuln/detail/cve-2026-53374), [CVE-2026-63879](https://nvd.nist.gov/vuln/detail/cve-2026-63879), [CVE-2026-63884](https://nvd.nist.gov/vuln/detail/cve-2026-63884), [CVE-2026-63888](https://nvd.nist.gov/vuln/detail/cve-2026-63888), [CVE-2026-63952](https://nvd.nist.gov/vuln/detail/cve-2026-63952), [CVE-2026-64007](https://nvd.nist.gov/vuln/detail/cve-2026-64007), [CVE-2026-64048](https://nvd.nist.gov/vuln/detail/cve-2026-64048), [CVE-2026-64219](https://nvd.nist.gov/vuln/detail/cve-2026-64219), [CVE-2026-64379](https://nvd.nist.gov/vuln/detail/cve-2026-64379), [CVE-2026-64382](https://nvd.nist.gov/vuln/detail/cve-2026-64382), [CVE-2026-64386](https://nvd.nist.gov/vuln/detail/cve-2026-64386), [CVE-2026-64560](https://nvd.nist.gov/vuln/detail/cve-2026-64560), [CVE-2026-68343](https://nvd.nist.gov/vuln/detail/cve-2026-68343), [CVE-2026-68388](https://nvd.nist.gov/vuln/detail/cve-2026-68388), [RHSA-2026:59723](https://access.redhat.com/errata/RHSA-2026:59723), [CVE-2025-68211](https://nvd.nist.gov/vuln/detail/cve-2025-68211), [CVE-2026-23003](https://nvd.nist.gov/vuln/detail/cve-2026-23003), [CVE-2026-43114](https://nvd.nist.gov/vuln/detail/cve-2026-43114), [CVE-2026-52920](https://nvd.nist.gov/vuln/detail/cve-2026-52920), [CVE-2026-52924](https://nvd.nist.gov/vuln/detail/cve-2026-52924), [CVE-2026-53131](https://nvd.nist.gov/vuln/detail/cve-2026-53131), [CVE-2026-53185](https://nvd.nist.gov/vuln/detail/cve-2026-53185), [CVE-2026-53268](https://nvd.nist.gov/vuln/detail/cve-2026-53268), [CVE-2026-64189](https://nvd.nist.gov/vuln/detail/cve-2026-64189), [CVE-2026-64191](https://nvd.nist.gov/vuln/detail/cve-2026-64191), [CVE-2026-64276](https://nvd.nist.gov/vuln/detail/cve-2026-64276), [CVE-2026-64277](https://nvd.nist.gov/vuln/detail/cve-2026-64277), and [CVE-2026-74581](https://nvd.nist.gov/vuln/detail/cve-2026-74581).


RHEL 9 (Satellite) 5.14.0-687.42.1.el9_8
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-687.42.1.el9_8
:   Resolves the following CVEs: [RHSA-2026:63130](https://access.redhat.com/errata/RHSA-2026:63130), [CVE-2026-33818](https://nvd.nist.gov/vuln/detail/cve-2026-33818), [CVE-2026-56858](https://nvd.nist.gov/vuln/detail/cve-2026-56858), [CVE-2026-56860](https://nvd.nist.gov/vuln/detail/cve-2026-56860), [CVE-2026-56862](https://nvd.nist.gov/vuln/detail/cve-2026-56862), [RHSA-2026:58936](https://access.redhat.com/errata/RHSA-2026:58936), [CVE-2026-11822](https://nvd.nist.gov/vuln/detail/cve-2026-11822), [CVE-2026-11824](https://nvd.nist.gov/vuln/detail/cve-2026-11824), [RHSA-2026:60226](https://access.redhat.com/errata/RHSA-2026:60226), [CVE-2026-54371](https://nvd.nist.gov/vuln/detail/cve-2026-54371), [RHSA-2026:61355](https://access.redhat.com/errata/RHSA-2026:61355), [CVE-2026-16730](https://nvd.nist.gov/vuln/detail/cve-2026-16730), [RHSA-2026:61623](https://access.redhat.com/errata/RHSA-2026:61623), [CVE-2026-41991](https://nvd.nist.gov/vuln/detail/cve-2026-41991), [CVE-2026-41992](https://nvd.nist.gov/vuln/detail/cve-2026-41992), [RHSA-2026:62217](https://access.redhat.com/errata/RHSA-2026:62217), [CVE-2026-59843](https://nvd.nist.gov/vuln/detail/cve-2026-59843), [CVE-2026-59844](https://nvd.nist.gov/vuln/detail/cve-2026-59844), [CVE-2026-59845](https://nvd.nist.gov/vuln/detail/cve-2026-59845), [CVE-2026-59846](https://nvd.nist.gov/vuln/detail/cve-2026-59846), [CVE-2026-59847](https://nvd.nist.gov/vuln/detail/cve-2026-59847), [CVE-2026-59848](https://nvd.nist.gov/vuln/detail/cve-2026-59848), [CVE-2026-59850](https://nvd.nist.gov/vuln/detail/cve-2026-59850), [RHSA-2026:61247](https://access.redhat.com/errata/RHSA-2026:61247), [CVE-2026-11979](https://nvd.nist.gov/vuln/detail/cve-2026-11979), [CVE-2026-6653](https://nvd.nist.gov/vuln/detail/cve-2026-6653), [RHSA-2026:58572](https://access.redhat.com/errata/RHSA-2026:58572), [CVE-2026-10805](https://nvd.nist.gov/vuln/detail/cve-2026-10805), [RHSA-2026:61581](https://access.redhat.com/errata/RHSA-2026:61581), [CVE-2026-18477](https://nvd.nist.gov/vuln/detail/cve-2026-18477), [CVE-2026-18508](https://nvd.nist.gov/vuln/detail/cve-2026-18508), [CVE-2026-5704](https://nvd.nist.gov/vuln/detail/cve-2026-5704), [RHSA-2026:62143](https://access.redhat.com/errata/RHSA-2026:62143), [CVE-2026-58471](https://nvd.nist.gov/vuln/detail/cve-2026-58471), [CVE-2026-58472](https://nvd.nist.gov/vuln/detail/cve-2026-58472), [RHSA-2026:57252](https://access.redhat.com/errata/RHSA-2026:57252), [CVE-2026-43206](https://nvd.nist.gov/vuln/detail/cve-2026-43206), [CVE-2026-43233](https://nvd.nist.gov/vuln/detail/cve-2026-43233), [CVE-2026-43237](https://nvd.nist.gov/vuln/detail/cve-2026-43237), [CVE-2026-45878](https://nvd.nist.gov/vuln/detail/cve-2026-45878), [CVE-2026-45991](https://nvd.nist.gov/vuln/detail/cve-2026-45991), [CVE-2026-46120](https://nvd.nist.gov/vuln/detail/cve-2026-46120), [CVE-2026-52991](https://nvd.nist.gov/vuln/detail/cve-2026-52991), [CVE-2026-53136](https://nvd.nist.gov/vuln/detail/cve-2026-53136), [CVE-2026-53143](https://nvd.nist.gov/vuln/detail/cve-2026-53143), [CVE-2026-53189](https://nvd.nist.gov/vuln/detail/cve-2026-53189), [CVE-2026-53329](https://nvd.nist.gov/vuln/detail/cve-2026-53329), [CVE-2026-53356](https://nvd.nist.gov/vuln/detail/cve-2026-53356), [CVE-2026-53374](https://nvd.nist.gov/vuln/detail/cve-2026-53374), [CVE-2026-63879](https://nvd.nist.gov/vuln/detail/cve-2026-63879), [CVE-2026-63884](https://nvd.nist.gov/vuln/detail/cve-2026-63884), [CVE-2026-63888](https://nvd.nist.gov/vuln/detail/cve-2026-63888), [CVE-2026-63952](https://nvd.nist.gov/vuln/detail/cve-2026-63952), [CVE-2026-64007](https://nvd.nist.gov/vuln/detail/cve-2026-64007), [CVE-2026-64048](https://nvd.nist.gov/vuln/detail/cve-2026-64048), [CVE-2026-64219](https://nvd.nist.gov/vuln/detail/cve-2026-64219), [CVE-2026-64379](https://nvd.nist.gov/vuln/detail/cve-2026-64379), [CVE-2026-64382](https://nvd.nist.gov/vuln/detail/cve-2026-64382), [CVE-2026-64386](https://nvd.nist.gov/vuln/detail/cve-2026-64386), [CVE-2026-64560](https://nvd.nist.gov/vuln/detail/cve-2026-64560), [CVE-2026-68343](https://nvd.nist.gov/vuln/detail/cve-2026-68343), [CVE-2026-68388](https://nvd.nist.gov/vuln/detail/cve-2026-68388), [RHSA-2026:59723](https://access.redhat.com/errata/RHSA-2026:59723), [CVE-2025-68211](https://nvd.nist.gov/vuln/detail/cve-2025-68211), [CVE-2026-23003](https://nvd.nist.gov/vuln/detail/cve-2026-23003), [CVE-2026-43114](https://nvd.nist.gov/vuln/detail/cve-2026-43114), [CVE-2026-52920](https://nvd.nist.gov/vuln/detail/cve-2026-52920), [CVE-2026-52924](https://nvd.nist.gov/vuln/detail/cve-2026-52924), [CVE-2026-53131](https://nvd.nist.gov/vuln/detail/cve-2026-53131), [CVE-2026-53185](https://nvd.nist.gov/vuln/detail/cve-2026-53185), [CVE-2026-53268](https://nvd.nist.gov/vuln/detail/cve-2026-53268), [CVE-2026-64189](https://nvd.nist.gov/vuln/detail/cve-2026-64189), [CVE-2026-64191](https://nvd.nist.gov/vuln/detail/cve-2026-64191), [CVE-2026-64276](https://nvd.nist.gov/vuln/detail/cve-2026-64276), [CVE-2026-64277](https://nvd.nist.gov/vuln/detail/cve-2026-64277), and [CVE-2026-74581](https://nvd.nist.gov/vuln/detail/cve-2026-74581).


RHEL 8 (VPC) 4.18.0-553.158.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:57253](https://access.redhat.com/errata/RHSA-2026:57253), [CVE-2024-56602](https://nvd.nist.gov/vuln/detail/cve-2024-56602), [CVE-2026-46120](https://nvd.nist.gov/vuln/detail/cve-2026-46120), [CVE-2026-52991](https://nvd.nist.gov/vuln/detail/cve-2026-52991), [CVE-2026-53189](https://nvd.nist.gov/vuln/detail/cve-2026-53189), [CVE-2026-63887](https://nvd.nist.gov/vuln/detail/cve-2026-63887), [CVE-2026-63888](https://nvd.nist.gov/vuln/detail/cve-2026-63888), [CVE-2026-64048](https://nvd.nist.gov/vuln/detail/cve-2026-64048), [CVE-2026-64379](https://nvd.nist.gov/vuln/detail/cve-2026-64379), [CVE-2026-68388](https://nvd.nist.gov/vuln/detail/cve-2026-68388), [RHSA-2026:59821](https://access.redhat.com/errata/RHSA-2026:59821), [CVE-2026-52924](https://nvd.nist.gov/vuln/detail/cve-2026-52924), [CVE-2026-63886](https://nvd.nist.gov/vuln/detail/cve-2026-63886), [CVE-2026-63913](https://nvd.nist.gov/vuln/detail/cve-2026-63913), [CVE-2026-64189](https://nvd.nist.gov/vuln/detail/cve-2026-64189), [CVE-2026-64191](https://nvd.nist.gov/vuln/detail/cve-2026-64191), [CVE-2026-64276](https://nvd.nist.gov/vuln/detail/cve-2026-64276), [CVE-2026-64277](https://nvd.nist.gov/vuln/detail/cve-2026-64277), [CVE-2026-64320](https://nvd.nist.gov/vuln/detail/cve-2026-64320), [RHSA-2026:58938](https://access.redhat.com/errata/RHSA-2026:58938), [CVE-2026-11822](https://nvd.nist.gov/vuln/detail/cve-2026-11822), [CVE-2026-11824](https://nvd.nist.gov/vuln/detail/cve-2026-11824), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:61766](https://access.redhat.com/errata/RHSA-2026:61766), [CVE-2026-15588](https://nvd.nist.gov/vuln/detail/cve-2026-15588), [CVE-2026-58010](https://nvd.nist.gov/vuln/detail/cve-2026-58010), [CVE-2026-58011](https://nvd.nist.gov/vuln/detail/cve-2026-58011), [CVE-2026-58012](https://nvd.nist.gov/vuln/detail/cve-2026-58012), [CVE-2026-58013](https://nvd.nist.gov/vuln/detail/cve-2026-58013), [CVE-2026-58014](https://nvd.nist.gov/vuln/detail/cve-2026-58014), [CVE-2026-58015](https://nvd.nist.gov/vuln/detail/cve-2026-58015), [RHSA-2026:62218](https://access.redhat.com/errata/RHSA-2026:62218), [CVE-2026-59843](https://nvd.nist.gov/vuln/detail/cve-2026-59843), [CVE-2026-59844](https://nvd.nist.gov/vuln/detail/cve-2026-59844), [CVE-2026-59845](https://nvd.nist.gov/vuln/detail/cve-2026-59845), [CVE-2026-59846](https://nvd.nist.gov/vuln/detail/cve-2026-59846), [CVE-2026-59847](https://nvd.nist.gov/vuln/detail/cve-2026-59847), [CVE-2026-59848](https://nvd.nist.gov/vuln/detail/cve-2026-59848), [CVE-2026-59850](https://nvd.nist.gov/vuln/detail/cve-2026-59850), [RHSA-2026:61248](https://access.redhat.com/errata/RHSA-2026:61248), [CVE-2026-11979](https://nvd.nist.gov/vuln/detail/cve-2026-11979), [RHSA-2026:58555](https://access.redhat.com/errata/RHSA-2026:58555), and [CVE-2026-10805](https://nvd.nist.gov/vuln/detail/cve-2026-10805).


RHEL 8 (Classic) 4.18.0-553.158.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:57253](https://access.redhat.com/errata/RHSA-2026:57253), [CVE-2024-56602](https://nvd.nist.gov/vuln/detail/cve-2024-56602), [CVE-2026-46120](https://nvd.nist.gov/vuln/detail/cve-2026-46120), [CVE-2026-52991](https://nvd.nist.gov/vuln/detail/cve-2026-52991), [CVE-2026-53189](https://nvd.nist.gov/vuln/detail/cve-2026-53189), [CVE-2026-63887](https://nvd.nist.gov/vuln/detail/cve-2026-63887), [CVE-2026-63888](https://nvd.nist.gov/vuln/detail/cve-2026-63888), [CVE-2026-64048](https://nvd.nist.gov/vuln/detail/cve-2026-64048), [CVE-2026-64379](https://nvd.nist.gov/vuln/detail/cve-2026-64379), [CVE-2026-68388](https://nvd.nist.gov/vuln/detail/cve-2026-68388), [RHSA-2026:59821](https://access.redhat.com/errata/RHSA-2026:59821), [CVE-2026-52924](https://nvd.nist.gov/vuln/detail/cve-2026-52924), [CVE-2026-63886](https://nvd.nist.gov/vuln/detail/cve-2026-63886), [CVE-2026-63913](https://nvd.nist.gov/vuln/detail/cve-2026-63913), [CVE-2026-64189](https://nvd.nist.gov/vuln/detail/cve-2026-64189), [CVE-2026-64191](https://nvd.nist.gov/vuln/detail/cve-2026-64191), [CVE-2026-64276](https://nvd.nist.gov/vuln/detail/cve-2026-64276), [CVE-2026-64277](https://nvd.nist.gov/vuln/detail/cve-2026-64277), [CVE-2026-64320](https://nvd.nist.gov/vuln/detail/cve-2026-64320), [RHSA-2026:58938](https://access.redhat.com/errata/RHSA-2026:58938), [CVE-2026-11822](https://nvd.nist.gov/vuln/detail/cve-2026-11822), [CVE-2026-11824](https://nvd.nist.gov/vuln/detail/cve-2026-11824), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:61766](https://access.redhat.com/errata/RHSA-2026:61766), [CVE-2026-15588](https://nvd.nist.gov/vuln/detail/cve-2026-15588), [CVE-2026-58010](https://nvd.nist.gov/vuln/detail/cve-2026-58010), [CVE-2026-58011](https://nvd.nist.gov/vuln/detail/cve-2026-58011), [CVE-2026-58012](https://nvd.nist.gov/vuln/detail/cve-2026-58012), [CVE-2026-58013](https://nvd.nist.gov/vuln/detail/cve-2026-58013), [CVE-2026-58014](https://nvd.nist.gov/vuln/detail/cve-2026-58014), [CVE-2026-58015](https://nvd.nist.gov/vuln/detail/cve-2026-58015), [RHSA-2026:62218](https://access.redhat.com/errata/RHSA-2026:62218), [CVE-2026-59843](https://nvd.nist.gov/vuln/detail/cve-2026-59843), [CVE-2026-59844](https://nvd.nist.gov/vuln/detail/cve-2026-59844), [CVE-2026-59845](https://nvd.nist.gov/vuln/detail/cve-2026-59845), [CVE-2026-59846](https://nvd.nist.gov/vuln/detail/cve-2026-59846), [CVE-2026-59847](https://nvd.nist.gov/vuln/detail/cve-2026-59847), [CVE-2026-59848](https://nvd.nist.gov/vuln/detail/cve-2026-59848), [CVE-2026-59850](https://nvd.nist.gov/vuln/detail/cve-2026-59850), [RHSA-2026:61248](https://access.redhat.com/errata/RHSA-2026:61248), [CVE-2026-11979](https://nvd.nist.gov/vuln/detail/cve-2026-11979), [RHSA-2026:58555](https://access.redhat.com/errata/RHSA-2026:58555), [CVE-2026-10805](https://nvd.nist.gov/vuln/detail/cve-2026-10805), [RHSA-2026:62144](https://access.redhat.com/errata/RHSA-2026:62144), [CVE-2026-58469](https://nvd.nist.gov/vuln/detail/cve-2026-58469), [CVE-2026-58471](https://nvd.nist.gov/vuln/detail/cve-2026-58471), and [CVE-2026-58472](https://nvd.nist.gov/vuln/detail/cve-2026-58472).


Red Hat OpenShift 4.17.57
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-57_release-notes){: external}.


Red Hat CoreOS 4.17.57
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-57_release-notes){: external}.


HAProxy 32e7011201fc5fceab21338da7c0a2dfead3b185
:   Resolves the following CVEs: [CVE-2026-11824](https://nvd.nist.gov/vuln/detail/cve-2026-11824), [CVE-2026-11979](https://nvd.nist.gov/vuln/detail/cve-2026-11979), [CVE-2026-8286](https://nvd.nist.gov/vuln/detail/cve-2026-8286), and [CVE-2026-11822](https://nvd.nist.gov/vuln/detail/cve-2026-11822).


## 25 August 2026, Worker node fix pack 4.17.56_1597_openshift
{: #cl-boms-41756_1597_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.56_1597_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-687.39.1.el9_8
:   Resolves the following CVEs: [RHSA-2026:54510](https://access.redhat.com/errata/RHSA-2026:54510), [CVE-2026-10723](https://nvd.nist.gov/vuln/detail/cve-2026-10723), [CVE-2026-11331](https://nvd.nist.gov/vuln/detail/cve-2026-11331), [CVE-2026-11622](https://nvd.nist.gov/vuln/detail/cve-2026-11622), [CVE-2026-11721](https://nvd.nist.gov/vuln/detail/cve-2026-11721), [CVE-2026-13204](https://nvd.nist.gov/vuln/detail/cve-2026-13204), [CVE-2026-13321](https://nvd.nist.gov/vuln/detail/cve-2026-13321), [RHSA-2026:55439](https://access.redhat.com/errata/RHSA-2026:55439), [CVE-2026-1965](https://nvd.nist.gov/vuln/detail/cve-2026-1965), [CVE-2026-3783](https://nvd.nist.gov/vuln/detail/cve-2026-3783), [CVE-2026-8286](https://nvd.nist.gov/vuln/detail/cve-2026-8286), [CVE-2026-9547](https://nvd.nist.gov/vuln/detail/cve-2026-9547), [RHSA-2026:54571](https://access.redhat.com/errata/RHSA-2026:54571), [CVE-2026-15816](https://nvd.nist.gov/vuln/detail/cve-2026-15816), [RHSA-2026:55772](https://access.redhat.com/errata/RHSA-2026:55772), [CVE-2026-55203](https://nvd.nist.gov/vuln/detail/cve-2026-55203), [CVE-2026-55204](https://nvd.nist.gov/vuln/detail/cve-2026-55204), [RHSA-2026:53844](https://access.redhat.com/errata/RHSA-2026:53844), [CVE-2026-44943](https://nvd.nist.gov/vuln/detail/cve-2026-44943), [CVE-2026-44944](https://nvd.nist.gov/vuln/detail/cve-2026-44944), [RHSA-2026:53847](https://access.redhat.com/errata/RHSA-2026:53847), [CVE-2026-55995](https://nvd.nist.gov/vuln/detail/cve-2026-55995), [RHSA-2026:53329](https://access.redhat.com/errata/RHSA-2026:53329), [CVE-2025-54518](https://nvd.nist.gov/vuln/detail/cve-2025-54518), [CVE-2026-31530](https://nvd.nist.gov/vuln/detail/cve-2026-31530), [CVE-2026-64368](https://nvd.nist.gov/vuln/detail/cve-2026-64368), [CVE-2026-64531](https://nvd.nist.gov/vuln/detail/cve-2026-64531), [RHSA-2026:54443](https://access.redhat.com/errata/RHSA-2026:54443), [CVE-2026-53202](https://nvd.nist.gov/vuln/detail/cve-2026-53202), [CVE-2026-53264](https://nvd.nist.gov/vuln/detail/cve-2026-53264), [RHSA-2026:54268](https://access.redhat.com/errata/RHSA-2026:54268), [CVE-2026-11940](https://nvd.nist.gov/vuln/detail/cve-2026-11940), [RHSA-2026:55440](https://access.redhat.com/errata/RHSA-2026:55440), [CVE-2026-15588](https://nvd.nist.gov/vuln/detail/cve-2026-15588), [CVE-2026-58010](https://nvd.nist.gov/vuln/detail/cve-2026-58010), [CVE-2026-58011](https://nvd.nist.gov/vuln/detail/cve-2026-58011), [CVE-2026-58012](https://nvd.nist.gov/vuln/detail/cve-2026-58012), [CVE-2026-58013](https://nvd.nist.gov/vuln/detail/cve-2026-58013), [CVE-2026-58014](https://nvd.nist.gov/vuln/detail/cve-2026-58014), [CVE-2026-58015](https://nvd.nist.gov/vuln/detail/cve-2026-58015), [RHSA-2026:57610](https://access.redhat.com/errata/RHSA-2026:57610), [CVE-2026-72693](https://nvd.nist.gov/vuln/detail/cve-2026-72693), [RHSA-2026:51035](https://access.redhat.com/errata/RHSA-2026:51035), [CVE-2026-23415](https://nvd.nist.gov/vuln/detail/cve-2026-23415), [CVE-2026-43450](https://nvd.nist.gov/vuln/detail/cve-2026-43450), [RHSA-2026:52674](https://access.redhat.com/errata/RHSA-2026:52674), [CVE-2026-14164](https://nvd.nist.gov/vuln/detail/cve-2026-14164), [RHSA-2026:54662](https://access.redhat.com/errata/RHSA-2026:54662), [CVE-2026-58055](https://nvd.nist.gov/vuln/detail/cve-2026-58055), [RHSA-2026:54484](https://access.redhat.com/errata/RHSA-2026:54484), and [CVE-2026-45409](https://nvd.nist.gov/vuln/detail/cve-2026-45409).


RHEL 9 (Satellite) 5.14.0-687.39.1.el9_8
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-687.39.1.el9_8
:   Resolves the following CVEs: [RHSA-2026:54510](https://access.redhat.com/errata/RHSA-2026:54510), [CVE-2026-10723](https://nvd.nist.gov/vuln/detail/cve-2026-10723), [CVE-2026-11331](https://nvd.nist.gov/vuln/detail/cve-2026-11331), [CVE-2026-11622](https://nvd.nist.gov/vuln/detail/cve-2026-11622), [CVE-2026-11721](https://nvd.nist.gov/vuln/detail/cve-2026-11721), [CVE-2026-13204](https://nvd.nist.gov/vuln/detail/cve-2026-13204), [CVE-2026-13321](https://nvd.nist.gov/vuln/detail/cve-2026-13321), [RHSA-2026:55439](https://access.redhat.com/errata/RHSA-2026:55439), [CVE-2026-1965](https://nvd.nist.gov/vuln/detail/cve-2026-1965), [CVE-2026-3783](https://nvd.nist.gov/vuln/detail/cve-2026-3783), [CVE-2026-8286](https://nvd.nist.gov/vuln/detail/cve-2026-8286), [CVE-2026-9547](https://nvd.nist.gov/vuln/detail/cve-2026-9547), [RHSA-2026:54571](https://access.redhat.com/errata/RHSA-2026:54571), [CVE-2026-15816](https://nvd.nist.gov/vuln/detail/cve-2026-15816), [RHSA-2026:55772](https://access.redhat.com/errata/RHSA-2026:55772), [CVE-2026-55203](https://nvd.nist.gov/vuln/detail/cve-2026-55203), [CVE-2026-55204](https://nvd.nist.gov/vuln/detail/cve-2026-55204), [RHSA-2026:53844](https://access.redhat.com/errata/RHSA-2026:53844), [CVE-2026-44943](https://nvd.nist.gov/vuln/detail/cve-2026-44943), [CVE-2026-44944](https://nvd.nist.gov/vuln/detail/cve-2026-44944), [RHSA-2026:53847](https://access.redhat.com/errata/RHSA-2026:53847), [CVE-2026-55995](https://nvd.nist.gov/vuln/detail/cve-2026-55995), [RHSA-2026:53329](https://access.redhat.com/errata/RHSA-2026:53329), [CVE-2025-54518](https://nvd.nist.gov/vuln/detail/cve-2025-54518), [CVE-2026-31530](https://nvd.nist.gov/vuln/detail/cve-2026-31530), [CVE-2026-64368](https://nvd.nist.gov/vuln/detail/cve-2026-64368), [CVE-2026-64531](https://nvd.nist.gov/vuln/detail/cve-2026-64531), [RHSA-2026:54443](https://access.redhat.com/errata/RHSA-2026:54443), [CVE-2026-53202](https://nvd.nist.gov/vuln/detail/cve-2026-53202), [CVE-2026-53264](https://nvd.nist.gov/vuln/detail/cve-2026-53264), [RHSA-2026:54268](https://access.redhat.com/errata/RHSA-2026:54268), [CVE-2026-11940](https://nvd.nist.gov/vuln/detail/cve-2026-11940), [RHSA-2026:55440](https://access.redhat.com/errata/RHSA-2026:55440), [CVE-2026-15588](https://nvd.nist.gov/vuln/detail/cve-2026-15588), [CVE-2026-58010](https://nvd.nist.gov/vuln/detail/cve-2026-58010), [CVE-2026-58011](https://nvd.nist.gov/vuln/detail/cve-2026-58011), [CVE-2026-58012](https://nvd.nist.gov/vuln/detail/cve-2026-58012), [CVE-2026-58013](https://nvd.nist.gov/vuln/detail/cve-2026-58013), [CVE-2026-58014](https://nvd.nist.gov/vuln/detail/cve-2026-58014), [CVE-2026-58015](https://nvd.nist.gov/vuln/detail/cve-2026-58015), [RHSA-2026:57610](https://access.redhat.com/errata/RHSA-2026:57610), [CVE-2026-72693](https://nvd.nist.gov/vuln/detail/cve-2026-72693), [RHSA-2026:51035](https://access.redhat.com/errata/RHSA-2026:51035), [CVE-2026-23415](https://nvd.nist.gov/vuln/detail/cve-2026-23415), [CVE-2026-43450](https://nvd.nist.gov/vuln/detail/cve-2026-43450), [RHSA-2026:52674](https://access.redhat.com/errata/RHSA-2026:52674), [CVE-2026-14164](https://nvd.nist.gov/vuln/detail/cve-2026-14164), [RHSA-2026:54662](https://access.redhat.com/errata/RHSA-2026:54662), [CVE-2026-58055](https://nvd.nist.gov/vuln/detail/cve-2026-58055), [RHSA-2026:54484](https://access.redhat.com/errata/RHSA-2026:54484), and [CVE-2026-45409](https://nvd.nist.gov/vuln/detail/cve-2026-45409).


RHEL 8 (VPC) 4.18.0-553.156.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:54654](https://access.redhat.com/errata/RHSA-2026:54654), [CVE-2026-10723](https://nvd.nist.gov/vuln/detail/cve-2026-10723), [CVE-2026-11622](https://nvd.nist.gov/vuln/detail/cve-2026-11622), [CVE-2026-11721](https://nvd.nist.gov/vuln/detail/cve-2026-11721), [CVE-2026-13204](https://nvd.nist.gov/vuln/detail/cve-2026-13204), [CVE-2026-13321](https://nvd.nist.gov/vuln/detail/cve-2026-13321), [RHSA-2026:57462](https://access.redhat.com/errata/RHSA-2026:57462), [CVE-2026-8286](https://nvd.nist.gov/vuln/detail/cve-2026-8286), [RHSA-2026:54575](https://access.redhat.com/errata/RHSA-2026:54575), [CVE-2026-15816](https://nvd.nist.gov/vuln/detail/cve-2026-15816), [RHSA-2026:55859](https://access.redhat.com/errata/RHSA-2026:55859), [CVE-2026-55204](https://nvd.nist.gov/vuln/detail/cve-2026-55204), [RHSA-2026:53848](https://access.redhat.com/errata/RHSA-2026:53848), [CVE-2026-55995](https://nvd.nist.gov/vuln/detail/cve-2026-55995), [RHSA-2026:50978](https://access.redhat.com/errata/RHSA-2026:50978), [CVE-2025-54518](https://nvd.nist.gov/vuln/detail/cve-2025-54518), [RHSA-2026:55764](https://access.redhat.com/errata/RHSA-2026:55764), [CVE-2025-39902](https://nvd.nist.gov/vuln/detail/cve-2025-39902), [CVE-2026-17523](https://nvd.nist.gov/vuln/detail/cve-2026-17523), [CVE-2026-43206](https://nvd.nist.gov/vuln/detail/cve-2026-43206), [CVE-2026-53016](https://nvd.nist.gov/vuln/detail/cve-2026-53016), [CVE-2026-53136](https://nvd.nist.gov/vuln/detail/cve-2026-53136), [CVE-2026-53329](https://nvd.nist.gov/vuln/detail/cve-2026-53329), [CVE-2026-53374](https://nvd.nist.gov/vuln/detail/cve-2026-53374), [CVE-2026-63879](https://nvd.nist.gov/vuln/detail/cve-2026-63879), [CVE-2026-63884](https://nvd.nist.gov/vuln/detail/cve-2026-63884), [CVE-2026-64219](https://nvd.nist.gov/vuln/detail/cve-2026-64219), [RHSA-2026:57253](https://access.redhat.com/errata/RHSA-2026:57253), [CVE-2024-56602](https://nvd.nist.gov/vuln/detail/cve-2024-56602), [CVE-2026-46120](https://nvd.nist.gov/vuln/detail/cve-2026-46120), [CVE-2026-52991](https://nvd.nist.gov/vuln/detail/cve-2026-52991), [CVE-2026-53189](https://nvd.nist.gov/vuln/detail/cve-2026-53189), [CVE-2026-63887](https://nvd.nist.gov/vuln/detail/cve-2026-63887), [CVE-2026-63888](https://nvd.nist.gov/vuln/detail/cve-2026-63888), [CVE-2026-64048](https://nvd.nist.gov/vuln/detail/cve-2026-64048), [CVE-2026-64379](https://nvd.nist.gov/vuln/detail/cve-2026-64379), [CVE-2026-68388](https://nvd.nist.gov/vuln/detail/cve-2026-68388), [RHSA-2026:56219](https://access.redhat.com/errata/RHSA-2026:56219), [CVE-2026-11940](https://nvd.nist.gov/vuln/detail/cve-2026-11940), [RHSA-2026:56130](https://access.redhat.com/errata/RHSA-2026:56130), [CVE-2026-16313](https://nvd.nist.gov/vuln/detail/cve-2026-16313), [RHSA-2026:55784](https://access.redhat.com/errata/RHSA-2026:55784), [CVE-2026-44690](https://nvd.nist.gov/vuln/detail/cve-2026-44690), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:56133](https://access.redhat.com/errata/RHSA-2026:56133), [CVE-2026-54371](https://nvd.nist.gov/vuln/detail/cve-2026-54371), [RHSA-2026:52765](https://access.redhat.com/errata/RHSA-2026:52765), [CVE-2026-64496](https://nvd.nist.gov/vuln/detail/cve-2026-64496), [RHSA-2026:54246](https://access.redhat.com/errata/RHSA-2026:54246), [CVE-2026-45991](https://nvd.nist.gov/vuln/detail/cve-2026-45991), [CVE-2026-53009](https://nvd.nist.gov/vuln/detail/cve-2026-53009), [RHSA-2026:55804](https://access.redhat.com/errata/RHSA-2026:55804), [CVE-2026-58055](https://nvd.nist.gov/vuln/detail/cve-2026-58055), [RHSA-2026:56131](https://access.redhat.com/errata/RHSA-2026:56131), [CVE-2026-54411](https://nvd.nist.gov/vuln/detail/cve-2026-54411), [RHSA-2026:54290](https://access.redhat.com/errata/RHSA-2026:54290), and [CVE-2026-45409](https://nvd.nist.gov/vuln/detail/cve-2026-45409).


RHEL 8 (Classic) 4.18.0-553.156.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:54654](https://access.redhat.com/errata/RHSA-2026:54654), [CVE-2026-10723](https://nvd.nist.gov/vuln/detail/cve-2026-10723), [CVE-2026-11622](https://nvd.nist.gov/vuln/detail/cve-2026-11622), [CVE-2026-11721](https://nvd.nist.gov/vuln/detail/cve-2026-11721), [CVE-2026-13204](https://nvd.nist.gov/vuln/detail/cve-2026-13204), [CVE-2026-13321](https://nvd.nist.gov/vuln/detail/cve-2026-13321), [RHSA-2026:57462](https://access.redhat.com/errata/RHSA-2026:57462), [CVE-2026-8286](https://nvd.nist.gov/vuln/detail/cve-2026-8286), [RHSA-2026:54575](https://access.redhat.com/errata/RHSA-2026:54575), [CVE-2026-15816](https://nvd.nist.gov/vuln/detail/cve-2026-15816), [RHSA-2026:55859](https://access.redhat.com/errata/RHSA-2026:55859), [CVE-2026-55204](https://nvd.nist.gov/vuln/detail/cve-2026-55204), [RHSA-2026:53848](https://access.redhat.com/errata/RHSA-2026:53848), [CVE-2026-55995](https://nvd.nist.gov/vuln/detail/cve-2026-55995), [RHSA-2026:50978](https://access.redhat.com/errata/RHSA-2026:50978), [CVE-2025-54518](https://nvd.nist.gov/vuln/detail/cve-2025-54518), [RHSA-2026:55764](https://access.redhat.com/errata/RHSA-2026:55764), [CVE-2025-39902](https://nvd.nist.gov/vuln/detail/cve-2025-39902), [CVE-2026-17523](https://nvd.nist.gov/vuln/detail/cve-2026-17523), [CVE-2026-43206](https://nvd.nist.gov/vuln/detail/cve-2026-43206), [CVE-2026-53016](https://nvd.nist.gov/vuln/detail/cve-2026-53016), [CVE-2026-53136](https://nvd.nist.gov/vuln/detail/cve-2026-53136), [CVE-2026-53329](https://nvd.nist.gov/vuln/detail/cve-2026-53329), [CVE-2026-53374](https://nvd.nist.gov/vuln/detail/cve-2026-53374), [CVE-2026-63879](https://nvd.nist.gov/vuln/detail/cve-2026-63879), [CVE-2026-63884](https://nvd.nist.gov/vuln/detail/cve-2026-63884), [CVE-2026-64219](https://nvd.nist.gov/vuln/detail/cve-2026-64219), [RHSA-2026:57253](https://access.redhat.com/errata/RHSA-2026:57253), [CVE-2024-56602](https://nvd.nist.gov/vuln/detail/cve-2024-56602), [CVE-2026-46120](https://nvd.nist.gov/vuln/detail/cve-2026-46120), [CVE-2026-52991](https://nvd.nist.gov/vuln/detail/cve-2026-52991), [CVE-2026-53189](https://nvd.nist.gov/vuln/detail/cve-2026-53189), [CVE-2026-63887](https://nvd.nist.gov/vuln/detail/cve-2026-63887), [CVE-2026-63888](https://nvd.nist.gov/vuln/detail/cve-2026-63888), [CVE-2026-64048](https://nvd.nist.gov/vuln/detail/cve-2026-64048), [CVE-2026-64379](https://nvd.nist.gov/vuln/detail/cve-2026-64379), [CVE-2026-68388](https://nvd.nist.gov/vuln/detail/cve-2026-68388), [RHSA-2026:56219](https://access.redhat.com/errata/RHSA-2026:56219), [CVE-2026-11940](https://nvd.nist.gov/vuln/detail/cve-2026-11940), [RHSA-2026:56130](https://access.redhat.com/errata/RHSA-2026:56130), [CVE-2026-16313](https://nvd.nist.gov/vuln/detail/cve-2026-16313), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:56133](https://access.redhat.com/errata/RHSA-2026:56133), [CVE-2026-54371](https://nvd.nist.gov/vuln/detail/cve-2026-54371), [RHSA-2026:52765](https://access.redhat.com/errata/RHSA-2026:52765), [CVE-2026-64496](https://nvd.nist.gov/vuln/detail/cve-2026-64496), [RHSA-2026:54246](https://access.redhat.com/errata/RHSA-2026:54246), [CVE-2026-45991](https://nvd.nist.gov/vuln/detail/cve-2026-45991), [CVE-2026-53009](https://nvd.nist.gov/vuln/detail/cve-2026-53009), [RHSA-2026:55804](https://access.redhat.com/errata/RHSA-2026:55804), [CVE-2026-58055](https://nvd.nist.gov/vuln/detail/cve-2026-58055), [RHSA-2026:56131](https://access.redhat.com/errata/RHSA-2026:56131), [CVE-2026-54411](https://nvd.nist.gov/vuln/detail/cve-2026-54411), [RHSA-2026:54290](https://access.redhat.com/errata/RHSA-2026:54290), and [CVE-2026-45409](https://nvd.nist.gov/vuln/detail/cve-2026-45409).


Red Hat OpenShift 4.17.56
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-56_release-notes){: external}.


Red Hat CoreOS 4.17.56
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-56_release-notes){: external}.


HAProxy a70e8a8452c4d476687ad749df47b6f27a61851a
:   Resolves the following CVEs: [CVE-2026-54411](https://nvd.nist.gov/vuln/detail/cve-2026-54411), [CVE-2026-54371](https://nvd.nist.gov/vuln/detail/cve-2026-54371), [CVE-2026-55204](https://nvd.nist.gov/vuln/detail/cve-2026-55204), and [CVE-2026-58055](https://nvd.nist.gov/vuln/detail/cve-2026-58055).


## 12 August 2026, Worker node fix pack 4.17.56_1596_openshift
{: #cl-boms-41756_1596_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.56_1596_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-687.34.1.el9_8
:   Resolves the following CVEs: [RHSA-2026:44385](https://access.redhat.com/errata/RHSA-2026:44385), [CVE-2024-46738](https://nvd.nist.gov/vuln/detail/cve-2024-46738), [CVE-2024-50076](https://nvd.nist.gov/vuln/detail/cve-2024-50076), [CVE-2025-39982](https://nvd.nist.gov/vuln/detail/cve-2025-39982), [CVE-2026-31488](https://nvd.nist.gov/vuln/detail/cve-2026-31488), [CVE-2026-31613](https://nvd.nist.gov/vuln/detail/cve-2026-31613), [CVE-2026-31684](https://nvd.nist.gov/vuln/detail/cve-2026-31684), [CVE-2026-46116](https://nvd.nist.gov/vuln/detail/cve-2026-46116), [CVE-2026-46209](https://nvd.nist.gov/vuln/detail/cve-2026-46209), [RHSA-2026:49031](https://access.redhat.com/errata/RHSA-2026:49031), [CVE-2025-10263](https://nvd.nist.gov/vuln/detail/cve-2025-10263), [CVE-2025-40026](https://nvd.nist.gov/vuln/detail/cve-2025-40026), [CVE-2026-52923](https://nvd.nist.gov/vuln/detail/cve-2026-52923), [RHSA-2026:49839](https://access.redhat.com/errata/RHSA-2026:49839), [CVE-2026-14474](https://nvd.nist.gov/vuln/detail/cve-2026-14474), [CVE-2026-14476](https://nvd.nist.gov/vuln/detail/cve-2026-14476), [RHSA-2026:48811](https://access.redhat.com/errata/RHSA-2026:48811), [CVE-2026-48864](https://nvd.nist.gov/vuln/detail/cve-2026-48864), [RHSA-2026:49910](https://access.redhat.com/errata/RHSA-2026:49910), and [CVE-2026-29111](https://nvd.nist.gov/vuln/detail/cve-2026-29111).


RHEL 9 (Satellite) 5.14.0-687.34.1.el9_8
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-687.34.1.el9_8
:   Resolves the following CVEs: [RHSA-2026:44385](https://access.redhat.com/errata/RHSA-2026:44385), [CVE-2024-46738](https://nvd.nist.gov/vuln/detail/cve-2024-46738), [CVE-2024-50076](https://nvd.nist.gov/vuln/detail/cve-2024-50076), [CVE-2025-39982](https://nvd.nist.gov/vuln/detail/cve-2025-39982), [CVE-2026-31488](https://nvd.nist.gov/vuln/detail/cve-2026-31488), [CVE-2026-31613](https://nvd.nist.gov/vuln/detail/cve-2026-31613), [CVE-2026-31684](https://nvd.nist.gov/vuln/detail/cve-2026-31684), [CVE-2026-46116](https://nvd.nist.gov/vuln/detail/cve-2026-46116), [CVE-2026-46209](https://nvd.nist.gov/vuln/detail/cve-2026-46209), [RHSA-2026:49031](https://access.redhat.com/errata/RHSA-2026:49031), [CVE-2025-10263](https://nvd.nist.gov/vuln/detail/cve-2025-10263), [CVE-2025-40026](https://nvd.nist.gov/vuln/detail/cve-2025-40026), [CVE-2026-52923](https://nvd.nist.gov/vuln/detail/cve-2026-52923), [RHSA-2026:49839](https://access.redhat.com/errata/RHSA-2026:49839), [CVE-2026-14474](https://nvd.nist.gov/vuln/detail/cve-2026-14474), [CVE-2026-14476](https://nvd.nist.gov/vuln/detail/cve-2026-14476), [RHSA-2026:48811](https://access.redhat.com/errata/RHSA-2026:48811), [CVE-2026-48864](https://nvd.nist.gov/vuln/detail/cve-2026-48864), [RHSA-2026:49910](https://access.redhat.com/errata/RHSA-2026:49910), and [CVE-2026-29111](https://nvd.nist.gov/vuln/detail/cve-2026-29111).


RHEL 8 (VPC) 4.18.0-553.151.1.el8_10
:   Resolves the following CVEs: [CVE-2026-56392](https://nvd.nist.gov/vuln/detail/cve-2026-56392), [RHSA-2026:45115](https://access.redhat.com/errata/RHSA-2026:45115), [CVE-2025-40026](https://nvd.nist.gov/vuln/detail/cve-2025-40026), [CVE-2026-52993](https://nvd.nist.gov/vuln/detail/cve-2026-52993), [CVE-2026-53059](https://nvd.nist.gov/vuln/detail/cve-2026-53059), [RHSA-2026:47011](https://access.redhat.com/errata/RHSA-2026:47011), [CVE-2026-53006](https://nvd.nist.gov/vuln/detail/cve-2026-53006), [RHSA-2026:49214](https://access.redhat.com/errata/RHSA-2026:49214), [CVE-2026-31692](https://nvd.nist.gov/vuln/detail/cve-2026-31692), [CVE-2026-43116](https://nvd.nist.gov/vuln/detail/cve-2026-43116), [CVE-2026-46150](https://nvd.nist.gov/vuln/detail/cve-2026-46150), [CVE-2026-64530](https://nvd.nist.gov/vuln/detail/cve-2026-64530), [RHSA-2026:42552](https://access.redhat.com/errata/RHSA-2026:42552), [CVE-2026-46117](https://nvd.nist.gov/vuln/detail/cve-2026-46117), [CVE-2026-53071](https://nvd.nist.gov/vuln/detail/cve-2026-53071), [RHSA-2026:50978](https://access.redhat.com/errata/RHSA-2026:50978), [CVE-2025-54518](https://nvd.nist.gov/vuln/detail/cve-2025-54518), [RHSA-2026:46990](https://access.redhat.com/errata/RHSA-2026:46990), [CVE-2026-14474](https://nvd.nist.gov/vuln/detail/cve-2026-14474), [CVE-2026-14476](https://nvd.nist.gov/vuln/detail/cve-2026-14476), [RHSA-2026:48703](https://access.redhat.com/errata/RHSA-2026:48703), [CVE-2026-55693](https://nvd.nist.gov/vuln/detail/cve-2026-55693), [CVE-2026-57455](https://nvd.nist.gov/vuln/detail/cve-2026-57455), [CVE-2026-57456](https://nvd.nist.gov/vuln/detail/cve-2026-57456), [CVE-2026-59858](https://nvd.nist.gov/vuln/detail/cve-2026-59858), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:49857](https://access.redhat.com/errata/RHSA-2026:49857), [CVE-2026-52923](https://nvd.nist.gov/vuln/detail/cve-2026-52923), [RHSA-2026:47117](https://access.redhat.com/errata/RHSA-2026:47117), [CVE-2026-41989](https://nvd.nist.gov/vuln/detail/cve-2026-41989), [RHSA-2026:47755](https://access.redhat.com/errata/RHSA-2026:47755), [CVE-2026-55653](https://nvd.nist.gov/vuln/detail/cve-2026-55653), and [CVE-2026-55655](https://nvd.nist.gov/vuln/detail/cve-2026-55655).


RHEL 8 (Classic) 4.18.0-553.151.1.el8_10
:   Resolves the following CVEs: [CVE-2026-56392](https://nvd.nist.gov/vuln/detail/cve-2026-56392), [RHSA-2026:45115](https://access.redhat.com/errata/RHSA-2026:45115), [CVE-2025-40026](https://nvd.nist.gov/vuln/detail/cve-2025-40026), [CVE-2026-52993](https://nvd.nist.gov/vuln/detail/cve-2026-52993), [CVE-2026-53059](https://nvd.nist.gov/vuln/detail/cve-2026-53059), [RHSA-2026:47011](https://access.redhat.com/errata/RHSA-2026:47011), [CVE-2026-53006](https://nvd.nist.gov/vuln/detail/cve-2026-53006), [RHSA-2026:49214](https://access.redhat.com/errata/RHSA-2026:49214), [CVE-2026-31692](https://nvd.nist.gov/vuln/detail/cve-2026-31692), [CVE-2026-43116](https://nvd.nist.gov/vuln/detail/cve-2026-43116), [CVE-2026-46150](https://nvd.nist.gov/vuln/detail/cve-2026-46150), [CVE-2026-64530](https://nvd.nist.gov/vuln/detail/cve-2026-64530), [RHSA-2026:42552](https://access.redhat.com/errata/RHSA-2026:42552), [CVE-2026-46117](https://nvd.nist.gov/vuln/detail/cve-2026-46117), [CVE-2026-53071](https://nvd.nist.gov/vuln/detail/cve-2026-53071), [RHSA-2026:50978](https://access.redhat.com/errata/RHSA-2026:50978), [CVE-2025-54518](https://nvd.nist.gov/vuln/detail/cve-2025-54518), [RHSA-2026:46990](https://access.redhat.com/errata/RHSA-2026:46990), [CVE-2026-14474](https://nvd.nist.gov/vuln/detail/cve-2026-14474), [CVE-2026-14476](https://nvd.nist.gov/vuln/detail/cve-2026-14476), [RHSA-2026:48703](https://access.redhat.com/errata/RHSA-2026:48703), [CVE-2026-55693](https://nvd.nist.gov/vuln/detail/cve-2026-55693), [CVE-2026-57455](https://nvd.nist.gov/vuln/detail/cve-2026-57455), [CVE-2026-57456](https://nvd.nist.gov/vuln/detail/cve-2026-57456), [CVE-2026-59858](https://nvd.nist.gov/vuln/detail/cve-2026-59858), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:49857](https://access.redhat.com/errata/RHSA-2026:49857), [CVE-2026-52923](https://nvd.nist.gov/vuln/detail/cve-2026-52923), [RHSA-2026:47117](https://access.redhat.com/errata/RHSA-2026:47117), [CVE-2026-41989](https://nvd.nist.gov/vuln/detail/cve-2026-41989), [RHSA-2026:47755](https://access.redhat.com/errata/RHSA-2026:47755), [CVE-2026-55653](https://nvd.nist.gov/vuln/detail/cve-2026-55653), and [CVE-2026-55655](https://nvd.nist.gov/vuln/detail/cve-2026-55655).


Red Hat OpenShift 4.17.56
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-56_release-notes){: external}.


Red Hat CoreOS 4.17.56
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-56_release-notes){: external}.


HAProxy bd7e64ef86b90455535107263466d1825f3e7f9f
:   Resolves the following CVEs: [CVE-2026-56391](https://nvd.nist.gov/vuln/detail/cve-2026-56391), and [CVE-2026-56392](https://nvd.nist.gov/vuln/detail/cve-2026-56392).


## 05 August 2026, Master fix pack 4.17.56_1595_openshift
{: #cl-boms_master-41756_1595_openshift_M}

The following list shows the components that are in the master fix pack 4.17.56_1595_openshift. Master patch updates are applied automatically.
{: shortdesc}

Cluster health image v1.6.17
:   New version contains updates and security fixes.


etcd v3.5.32
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.32){: external}.


IBM Cloud Block Storage driver and plug-in v2.5.27
:   New version contains updates and security fixes.


IBM Cloud Controller Manager v1.30.14-51
:   New version contains updates and security fixes.


IBM Cloud File Storage for Classic plug-in and monitor v456
:   New version contains updates and security fixes.


IBM Cloud RBAC Operator 92ba7dd
:   New version contains updates and security fixes.


Key Management Service provider 2.10.28
:   New version contains updates and security fixes.


Portieris admission controller v0.14.2
:   See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.14.2){: external}


Red Hat OpenShift on IBM Cloud 4.17.56
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-56_release-notes){: external}.Resolves the following CVEs: [CVE-2026-16242](https://nvd.nist.gov/vuln/detail/cve-2026-16242).


Red Hat OpenShift on IBM Cloud Control Plane Operator, Metrics Server, and toolkit v4.17.0+20260707
:   See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.17.0+20260707){: external}.


## 28 July 2026, Worker node fix pack 4.17.55_1594_openshift
{: #cl-boms-41755_1594_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.55_1594_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.128.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:38902](https://access.redhat.com/errata/RHSA-2026:38902), [CVE-2025-68183](https://nvd.nist.gov/vuln/detail/cve-2025-68183), [CVE-2026-31408](https://nvd.nist.gov/vuln/detail/cve-2026-31408), [CVE-2026-43074](https://nvd.nist.gov/vuln/detail/cve-2026-43074), [CVE-2026-43279](https://nvd.nist.gov/vuln/detail/cve-2026-43279), [CVE-2026-45984](https://nvd.nist.gov/vuln/detail/cve-2026-45984), [CVE-2026-46135](https://nvd.nist.gov/vuln/detail/cve-2026-46135), [CVE-2026-46152](https://nvd.nist.gov/vuln/detail/cve-2026-46152), [CVE-2026-46189](https://nvd.nist.gov/vuln/detail/cve-2026-46189), [CVE-2026-46242](https://nvd.nist.gov/vuln/detail/cve-2026-46242), [CVE-2026-46316](https://nvd.nist.gov/vuln/detail/cve-2026-46316), [CVE-2026-53359](https://nvd.nist.gov/vuln/detail/cve-2026-53359), [RHSA-2026:44385](https://access.redhat.com/errata/RHSA-2026:44385), [CVE-2024-46738](https://nvd.nist.gov/vuln/detail/cve-2024-46738), [CVE-2024-50076](https://nvd.nist.gov/vuln/detail/cve-2024-50076), [CVE-2025-39982](https://nvd.nist.gov/vuln/detail/cve-2025-39982), [CVE-2026-31488](https://nvd.nist.gov/vuln/detail/cve-2026-31488), [CVE-2026-31613](https://nvd.nist.gov/vuln/detail/cve-2026-31613), [CVE-2026-31684](https://nvd.nist.gov/vuln/detail/cve-2026-31684), [CVE-2026-46116](https://nvd.nist.gov/vuln/detail/cve-2026-46116), [CVE-2026-46209](https://nvd.nist.gov/vuln/detail/cve-2026-46209), [RHSA-2026:40425](https://access.redhat.com/errata/RHSA-2026:40425), [CVE-2026-43499](https://nvd.nist.gov/vuln/detail/cve-2026-43499), [CVE-2026-53166](https://nvd.nist.gov/vuln/detail/cve-2026-53166), and [CVE-2026-64600](https://nvd.nist.gov/vuln/detail/cve-2026-64600).


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-570.128.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:38902](https://access.redhat.com/errata/RHSA-2026:38902), [CVE-2025-68183](https://nvd.nist.gov/vuln/detail/cve-2025-68183), [CVE-2026-31408](https://nvd.nist.gov/vuln/detail/cve-2026-31408), [CVE-2026-43074](https://nvd.nist.gov/vuln/detail/cve-2026-43074), [CVE-2026-43279](https://nvd.nist.gov/vuln/detail/cve-2026-43279), [CVE-2026-45984](https://nvd.nist.gov/vuln/detail/cve-2026-45984), [CVE-2026-46135](https://nvd.nist.gov/vuln/detail/cve-2026-46135), [CVE-2026-46152](https://nvd.nist.gov/vuln/detail/cve-2026-46152), [CVE-2026-46189](https://nvd.nist.gov/vuln/detail/cve-2026-46189), [CVE-2026-46242](https://nvd.nist.gov/vuln/detail/cve-2026-46242), [CVE-2026-46316](https://nvd.nist.gov/vuln/detail/cve-2026-46316), [CVE-2026-53359](https://nvd.nist.gov/vuln/detail/cve-2026-53359), [RHSA-2026:44385](https://access.redhat.com/errata/RHSA-2026:44385), [CVE-2024-46738](https://nvd.nist.gov/vuln/detail/cve-2024-46738), [CVE-2024-50076](https://nvd.nist.gov/vuln/detail/cve-2024-50076), [CVE-2025-39982](https://nvd.nist.gov/vuln/detail/cve-2025-39982), [CVE-2026-31488](https://nvd.nist.gov/vuln/detail/cve-2026-31488), [CVE-2026-31613](https://nvd.nist.gov/vuln/detail/cve-2026-31613), [CVE-2026-31684](https://nvd.nist.gov/vuln/detail/cve-2026-31684), [CVE-2026-46116](https://nvd.nist.gov/vuln/detail/cve-2026-46116), [CVE-2026-46209](https://nvd.nist.gov/vuln/detail/cve-2026-46209), [RHSA-2026:40425](https://access.redhat.com/errata/RHSA-2026:40425), [CVE-2026-43499](https://nvd.nist.gov/vuln/detail/cve-2026-43499), [CVE-2026-53166](https://nvd.nist.gov/vuln/detail/cve-2026-53166), and [CVE-2026-64600](https://nvd.nist.gov/vuln/detail/cve-2026-64600).


RHEL 8 (VPC) 4.18.0-553.144.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:43420](https://access.redhat.com/errata/RHSA-2026:43420), [CVE-2026-54369](https://nvd.nist.gov/vuln/detail/cve-2026-54369), [CVE-2026-54370](https://nvd.nist.gov/vuln/detail/cve-2026-54370), [RHSA-2026:38504](https://access.redhat.com/errata/RHSA-2026:38504), [CVE-2026-33811](https://nvd.nist.gov/vuln/detail/cve-2026-33811), [CVE-2026-39835](https://nvd.nist.gov/vuln/detail/cve-2026-39835), [CVE-2026-57231](https://nvd.nist.gov/vuln/detail/cve-2026-57231), [RHSA-2026:42090](https://access.redhat.com/errata/RHSA-2026:42090), [CVE-2026-58016](https://nvd.nist.gov/vuln/detail/cve-2026-58016), [RHSA-2026:36366](https://access.redhat.com/errata/RHSA-2026:36366), [CVE-2026-43112](https://nvd.nist.gov/vuln/detail/cve-2026-43112), [RHSA-2026:39179](https://access.redhat.com/errata/RHSA-2026:39179), [CVE-2026-46086](https://nvd.nist.gov/vuln/detail/cve-2026-46086), [CVE-2026-46116](https://nvd.nist.gov/vuln/detail/cve-2026-46116), [CVE-2026-64600](https://nvd.nist.gov/vuln/detail/cve-2026-64600), [RHSA-2026:36349](https://access.redhat.com/errata/RHSA-2026:36349), [CVE-2025-10263](https://nvd.nist.gov/vuln/detail/cve-2025-10263), [CVE-2026-43198](https://nvd.nist.gov/vuln/detail/cve-2026-43198), [CVE-2026-43450](https://nvd.nist.gov/vuln/detail/cve-2026-43450), [CVE-2026-46209](https://nvd.nist.gov/vuln/detail/cve-2026-46209), [CVE-2026-46227](https://nvd.nist.gov/vuln/detail/cve-2026-46227), [CVE-2026-46259](https://nvd.nist.gov/vuln/detail/cve-2026-46259), [RHSA-2026:42552](https://access.redhat.com/errata/RHSA-2026:42552), [CVE-2026-46117](https://nvd.nist.gov/vuln/detail/cve-2026-46117), [CVE-2026-53071](https://nvd.nist.gov/vuln/detail/cve-2026-53071), [RHSA-2026:39083](https://access.redhat.com/errata/RHSA-2026:39083), [CVE-2025-71066](https://nvd.nist.gov/vuln/detail/cve-2025-71066), [CVE-2025-71089](https://nvd.nist.gov/vuln/detail/cve-2025-71089), [CVE-2026-31411](https://nvd.nist.gov/vuln/detail/cve-2026-31411), [CVE-2026-43499](https://nvd.nist.gov/vuln/detail/cve-2026-43499), [CVE-2026-46113](https://nvd.nist.gov/vuln/detail/cve-2026-46113), [CVE-2026-53166](https://nvd.nist.gov/vuln/detail/cve-2026-53166), [CVE-2026-53266](https://nvd.nist.gov/vuln/detail/cve-2026-53266), [CVE-2026-53359](https://nvd.nist.gov/vuln/detail/cve-2026-53359), [RHSA-2026:39320](https://access.redhat.com/errata/RHSA-2026:39320), [CVE-2026-15308](https://nvd.nist.gov/vuln/detail/cve-2026-15308), [RHSA-2026:41930](https://access.redhat.com/errata/RHSA-2026:41930), [CVE-2026-27145](https://nvd.nist.gov/vuln/detail/cve-2026-27145), [CVE-2026-39821](https://nvd.nist.gov/vuln/detail/cve-2026-39821), [RHSA-2026:38510](https://access.redhat.com/errata/RHSA-2026:38510), [CVE-2026-46483](https://nvd.nist.gov/vuln/detail/cve-2026-46483), [CVE-2026-47162](https://nvd.nist.gov/vuln/detail/cve-2026-47162), [CVE-2026-47167](https://nvd.nist.gov/vuln/detail/cve-2026-47167), [CVE-2026-52858](https://nvd.nist.gov/vuln/detail/cve-2026-52858), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:42733](https://access.redhat.com/errata/RHSA-2026:42733), [CVE-2026-5435](https://nvd.nist.gov/vuln/detail/cve-2026-5435), [CVE-2026-5928](https://nvd.nist.gov/vuln/detail/cve-2026-5928), [CVE-2026-6238](https://nvd.nist.gov/vuln/detail/cve-2026-6238), [RHSA-2026:38503](https://access.redhat.com/errata/RHSA-2026:38503), and [CVE-2026-28390](https://nvd.nist.gov/vuln/detail/cve-2026-28390).


RHEL 8 (Classic) 4.18.0-553.144.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:43420](https://access.redhat.com/errata/RHSA-2026:43420), [CVE-2026-54369](https://nvd.nist.gov/vuln/detail/cve-2026-54369), [CVE-2026-54370](https://nvd.nist.gov/vuln/detail/cve-2026-54370), [RHSA-2026:38504](https://access.redhat.com/errata/RHSA-2026:38504), [CVE-2026-33811](https://nvd.nist.gov/vuln/detail/cve-2026-33811), [CVE-2026-39835](https://nvd.nist.gov/vuln/detail/cve-2026-39835), [CVE-2026-57231](https://nvd.nist.gov/vuln/detail/cve-2026-57231), [RHSA-2026:42090](https://access.redhat.com/errata/RHSA-2026:42090), [CVE-2026-58016](https://nvd.nist.gov/vuln/detail/cve-2026-58016), [RHSA-2026:36366](https://access.redhat.com/errata/RHSA-2026:36366), [CVE-2026-43112](https://nvd.nist.gov/vuln/detail/cve-2026-43112), [RHSA-2026:39179](https://access.redhat.com/errata/RHSA-2026:39179), [CVE-2026-46086](https://nvd.nist.gov/vuln/detail/cve-2026-46086), [CVE-2026-46116](https://nvd.nist.gov/vuln/detail/cve-2026-46116), [CVE-2026-64600](https://nvd.nist.gov/vuln/detail/cve-2026-64600), [RHSA-2026:36349](https://access.redhat.com/errata/RHSA-2026:36349), [CVE-2025-10263](https://nvd.nist.gov/vuln/detail/cve-2025-10263), [CVE-2026-43198](https://nvd.nist.gov/vuln/detail/cve-2026-43198), [CVE-2026-43450](https://nvd.nist.gov/vuln/detail/cve-2026-43450), [CVE-2026-46209](https://nvd.nist.gov/vuln/detail/cve-2026-46209), [CVE-2026-46227](https://nvd.nist.gov/vuln/detail/cve-2026-46227), [CVE-2026-46259](https://nvd.nist.gov/vuln/detail/cve-2026-46259), [RHSA-2026:42552](https://access.redhat.com/errata/RHSA-2026:42552), [CVE-2026-46117](https://nvd.nist.gov/vuln/detail/cve-2026-46117), [CVE-2026-53071](https://nvd.nist.gov/vuln/detail/cve-2026-53071), [RHSA-2026:39083](https://access.redhat.com/errata/RHSA-2026:39083), [CVE-2025-71066](https://nvd.nist.gov/vuln/detail/cve-2025-71066), [CVE-2025-71089](https://nvd.nist.gov/vuln/detail/cve-2025-71089), [CVE-2026-31411](https://nvd.nist.gov/vuln/detail/cve-2026-31411), [CVE-2026-43499](https://nvd.nist.gov/vuln/detail/cve-2026-43499), [CVE-2026-46113](https://nvd.nist.gov/vuln/detail/cve-2026-46113), [CVE-2026-53166](https://nvd.nist.gov/vuln/detail/cve-2026-53166), [CVE-2026-53266](https://nvd.nist.gov/vuln/detail/cve-2026-53266), [CVE-2026-53359](https://nvd.nist.gov/vuln/detail/cve-2026-53359), [RHSA-2026:39320](https://access.redhat.com/errata/RHSA-2026:39320), [CVE-2026-15308](https://nvd.nist.gov/vuln/detail/cve-2026-15308), [RHSA-2026:41930](https://access.redhat.com/errata/RHSA-2026:41930), [CVE-2026-27145](https://nvd.nist.gov/vuln/detail/cve-2026-27145), [CVE-2026-39821](https://nvd.nist.gov/vuln/detail/cve-2026-39821), [RHSA-2026:38510](https://access.redhat.com/errata/RHSA-2026:38510), [CVE-2026-46483](https://nvd.nist.gov/vuln/detail/cve-2026-46483), [CVE-2026-47162](https://nvd.nist.gov/vuln/detail/cve-2026-47162), [CVE-2026-47167](https://nvd.nist.gov/vuln/detail/cve-2026-47167), [CVE-2026-52858](https://nvd.nist.gov/vuln/detail/cve-2026-52858), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:42733](https://access.redhat.com/errata/RHSA-2026:42733), [CVE-2026-5435](https://nvd.nist.gov/vuln/detail/cve-2026-5435), [CVE-2026-5928](https://nvd.nist.gov/vuln/detail/cve-2026-5928), [CVE-2026-6238](https://nvd.nist.gov/vuln/detail/cve-2026-6238), [RHSA-2026:38503](https://access.redhat.com/errata/RHSA-2026:38503), and [CVE-2026-28390](https://nvd.nist.gov/vuln/detail/cve-2026-28390).


Red Hat OpenShift 4.17.55
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-55_release-notes){: external}.


Red Hat CoreOS 4.17.55
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-55_release-notes){: external}.


HAProxy 346c7130717ef7cc25d1dfbca7d57ca32396b692
:   Resolves the following CVEs: [CVE-2026-6238](https://nvd.nist.gov/vuln/detail/cve-2026-6238), [CVE-2026-5928](https://nvd.nist.gov/vuln/detail/cve-2026-5928), [CVE-2026-48864](https://nvd.nist.gov/vuln/detail/cve-2026-48864), [CVE-2026-54370](https://nvd.nist.gov/vuln/detail/cve-2026-54370), [CVE-2026-28390](https://nvd.nist.gov/vuln/detail/cve-2026-28390), [CVE-2026-5435](https://nvd.nist.gov/vuln/detail/cve-2026-5435), [CVE-2025-13151](https://nvd.nist.gov/vuln/detail/cve-2025-13151), [CVE-2026-54369](https://nvd.nist.gov/vuln/detail/cve-2026-54369), [CVE-2026-58016](https://nvd.nist.gov/vuln/detail/cve-2026-58016), and [CVE-2025-6170](https://nvd.nist.gov/vuln/detail/cve-2025-6170).


## 28 July 2026, Master fix pack 4.17.54_1592_openshift
{: #cl-boms_master-41754_1592_openshift_M}

The following list shows the components that are in the master fix pack 4.17.54_1592_openshift. Master patch updates are applied automatically.
{: shortdesc}

Cluster health image v1.6.17
:   New version contains updates and security fixes.


IBM Cloud Controller Manager v1.30.14-49
:   New version contains updates and security fixes.


IBM Cloud RBAC Operator 92ba7dd
:   New version contains updates and security fixes.


Key Management Service provider 2.10.27
:   New version contains updates and security fixes.


Portieris admission controller v0.14.2
:   See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.14.2){: external}


Red Hat OpenShift on IBM Cloud Control Plane Operator, Metrics Server, and toolkit v4.17.0+20260707
:   See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.17.0+20260707){: external}.


## 13 July 2026, Worker node fix pack 4.17.55_1593_openshift
{: #cl-boms-41755_1593_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.55_1593_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.125.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:30004](https://access.redhat.com/errata/RHSA-2026:30004), [CVE-2026-33845](https://nvd.nist.gov/vuln/detail/cve-2026-33845), [CVE-2026-33846](https://nvd.nist.gov/vuln/detail/cve-2026-33846), [CVE-2026-3833](https://nvd.nist.gov/vuln/detail/cve-2026-3833), [CVE-2026-42009](https://nvd.nist.gov/vuln/detail/cve-2026-42009), [CVE-2026-42010](https://nvd.nist.gov/vuln/detail/cve-2026-42010), [CVE-2026-42011](https://nvd.nist.gov/vuln/detail/cve-2026-42011), [CVE-2026-42012](https://nvd.nist.gov/vuln/detail/cve-2026-42012), [CVE-2026-42013](https://nvd.nist.gov/vuln/detail/cve-2026-42013), [CVE-2026-42014](https://nvd.nist.gov/vuln/detail/cve-2026-42014), [CVE-2026-42015](https://nvd.nist.gov/vuln/detail/cve-2026-42015), [CVE-2026-5260](https://nvd.nist.gov/vuln/detail/cve-2026-5260), [CVE-2026-5419](https://nvd.nist.gov/vuln/detail/cve-2026-5419), [RHSA-2026:34094](https://access.redhat.com/errata/RHSA-2026:34094), [CVE-2025-21648](https://nvd.nist.gov/vuln/detail/cve-2025-21648), [CVE-2025-21691](https://nvd.nist.gov/vuln/detail/cve-2025-21691), [CVE-2026-23191](https://nvd.nist.gov/vuln/detail/cve-2026-23191), [CVE-2026-31669](https://nvd.nist.gov/vuln/detail/cve-2026-31669), [CVE-2026-43027](https://nvd.nist.gov/vuln/detail/cve-2026-43027), [CVE-2026-43125](https://nvd.nist.gov/vuln/detail/cve-2026-43125), [CVE-2026-43128](https://nvd.nist.gov/vuln/detail/cve-2026-43128), [CVE-2026-43198](https://nvd.nist.gov/vuln/detail/cve-2026-43198), [CVE-2026-43329](https://nvd.nist.gov/vuln/detail/cve-2026-43329), [CVE-2026-43414](https://nvd.nist.gov/vuln/detail/cve-2026-43414), [CVE-2026-43501](https://nvd.nist.gov/vuln/detail/cve-2026-43501), [CVE-2026-45852](https://nvd.nist.gov/vuln/detail/cve-2026-45852), [CVE-2026-46090](https://nvd.nist.gov/vuln/detail/cve-2026-46090), [CVE-2026-46173](https://nvd.nist.gov/vuln/detail/cve-2026-46173), [CVE-2026-46176](https://nvd.nist.gov/vuln/detail/cve-2026-46176), [CVE-2026-46181](https://nvd.nist.gov/vuln/detail/cve-2026-46181), [CVE-2026-46227](https://nvd.nist.gov/vuln/detail/cve-2026-46227), [CVE-2026-46244](https://nvd.nist.gov/vuln/detail/cve-2026-46244), [RHSA-2026:28147](https://access.redhat.com/errata/RHSA-2026:28147), [CVE-2026-28847](https://nvd.nist.gov/vuln/detail/cve-2026-28847), [CVE-2026-28883](https://nvd.nist.gov/vuln/detail/cve-2026-28883), [CVE-2026-28901](https://nvd.nist.gov/vuln/detail/cve-2026-28901), [CVE-2026-28902](https://nvd.nist.gov/vuln/detail/cve-2026-28902), [CVE-2026-28903](https://nvd.nist.gov/vuln/detail/cve-2026-28903), [CVE-2026-28904](https://nvd.nist.gov/vuln/detail/cve-2026-28904), [CVE-2026-28905](https://nvd.nist.gov/vuln/detail/cve-2026-28905), [CVE-2026-28907](https://nvd.nist.gov/vuln/detail/cve-2026-28907), [CVE-2026-28942](https://nvd.nist.gov/vuln/detail/cve-2026-28942), [CVE-2026-28946](https://nvd.nist.gov/vuln/detail/cve-2026-28946), [CVE-2026-28947](https://nvd.nist.gov/vuln/detail/cve-2026-28947), [CVE-2026-28953](https://nvd.nist.gov/vuln/detail/cve-2026-28953), [CVE-2026-28955](https://nvd.nist.gov/vuln/detail/cve-2026-28955), [CVE-2026-28958](https://nvd.nist.gov/vuln/detail/cve-2026-28958), [CVE-2026-43658](https://nvd.nist.gov/vuln/detail/cve-2026-43658), [CVE-2026-43660](https://nvd.nist.gov/vuln/detail/cve-2026-43660), [RHSA-2026:33634](https://access.redhat.com/errata/RHSA-2026:33634), [CVE-2024-34459](https://nvd.nist.gov/vuln/detail/cve-2024-34459), [RHSA-2026:33230](https://access.redhat.com/errata/RHSA-2026:33230), [CVE-2026-5450](https://nvd.nist.gov/vuln/detail/cve-2026-5450), [RHSA-2026:28832](https://access.redhat.com/errata/RHSA-2026:28832), and [CVE-2026-31790](https://nvd.nist.gov/vuln/detail/cve-2026-31790).


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-570.125.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:30004](https://access.redhat.com/errata/RHSA-2026:30004), [CVE-2026-33845](https://nvd.nist.gov/vuln/detail/cve-2026-33845), [CVE-2026-33846](https://nvd.nist.gov/vuln/detail/cve-2026-33846), [CVE-2026-3833](https://nvd.nist.gov/vuln/detail/cve-2026-3833), [CVE-2026-42009](https://nvd.nist.gov/vuln/detail/cve-2026-42009), [CVE-2026-42010](https://nvd.nist.gov/vuln/detail/cve-2026-42010), [CVE-2026-42011](https://nvd.nist.gov/vuln/detail/cve-2026-42011), [CVE-2026-42012](https://nvd.nist.gov/vuln/detail/cve-2026-42012), [CVE-2026-42013](https://nvd.nist.gov/vuln/detail/cve-2026-42013), [CVE-2026-42014](https://nvd.nist.gov/vuln/detail/cve-2026-42014), [CVE-2026-42015](https://nvd.nist.gov/vuln/detail/cve-2026-42015), [CVE-2026-5260](https://nvd.nist.gov/vuln/detail/cve-2026-5260), [CVE-2026-5419](https://nvd.nist.gov/vuln/detail/cve-2026-5419), [RHSA-2026:34094](https://access.redhat.com/errata/RHSA-2026:34094), [CVE-2025-21648](https://nvd.nist.gov/vuln/detail/cve-2025-21648), [CVE-2025-21691](https://nvd.nist.gov/vuln/detail/cve-2025-21691), [CVE-2026-23191](https://nvd.nist.gov/vuln/detail/cve-2026-23191), [CVE-2026-31669](https://nvd.nist.gov/vuln/detail/cve-2026-31669), [CVE-2026-43027](https://nvd.nist.gov/vuln/detail/cve-2026-43027), [CVE-2026-43125](https://nvd.nist.gov/vuln/detail/cve-2026-43125), [CVE-2026-43128](https://nvd.nist.gov/vuln/detail/cve-2026-43128), [CVE-2026-43198](https://nvd.nist.gov/vuln/detail/cve-2026-43198), [CVE-2026-43329](https://nvd.nist.gov/vuln/detail/cve-2026-43329), [CVE-2026-43414](https://nvd.nist.gov/vuln/detail/cve-2026-43414), [CVE-2026-43501](https://nvd.nist.gov/vuln/detail/cve-2026-43501), [CVE-2026-45852](https://nvd.nist.gov/vuln/detail/cve-2026-45852), [CVE-2026-46090](https://nvd.nist.gov/vuln/detail/cve-2026-46090), [CVE-2026-46173](https://nvd.nist.gov/vuln/detail/cve-2026-46173), [CVE-2026-46176](https://nvd.nist.gov/vuln/detail/cve-2026-46176), [CVE-2026-46181](https://nvd.nist.gov/vuln/detail/cve-2026-46181), [CVE-2026-46227](https://nvd.nist.gov/vuln/detail/cve-2026-46227), [CVE-2026-46244](https://nvd.nist.gov/vuln/detail/cve-2026-46244), [RHSA-2026:28147](https://access.redhat.com/errata/RHSA-2026:28147), [CVE-2026-28847](https://nvd.nist.gov/vuln/detail/cve-2026-28847), [CVE-2026-28883](https://nvd.nist.gov/vuln/detail/cve-2026-28883), [CVE-2026-28901](https://nvd.nist.gov/vuln/detail/cve-2026-28901), [CVE-2026-28902](https://nvd.nist.gov/vuln/detail/cve-2026-28902), [CVE-2026-28903](https://nvd.nist.gov/vuln/detail/cve-2026-28903), [CVE-2026-28904](https://nvd.nist.gov/vuln/detail/cve-2026-28904), [CVE-2026-28905](https://nvd.nist.gov/vuln/detail/cve-2026-28905), [CVE-2026-28907](https://nvd.nist.gov/vuln/detail/cve-2026-28907), [CVE-2026-28942](https://nvd.nist.gov/vuln/detail/cve-2026-28942), [CVE-2026-28946](https://nvd.nist.gov/vuln/detail/cve-2026-28946), [CVE-2026-28947](https://nvd.nist.gov/vuln/detail/cve-2026-28947), [CVE-2026-28953](https://nvd.nist.gov/vuln/detail/cve-2026-28953), [CVE-2026-28955](https://nvd.nist.gov/vuln/detail/cve-2026-28955), [CVE-2026-28958](https://nvd.nist.gov/vuln/detail/cve-2026-28958), [CVE-2026-43658](https://nvd.nist.gov/vuln/detail/cve-2026-43658), [CVE-2026-43660](https://nvd.nist.gov/vuln/detail/cve-2026-43660), [RHSA-2026:33634](https://access.redhat.com/errata/RHSA-2026:33634), [CVE-2024-34459](https://nvd.nist.gov/vuln/detail/cve-2024-34459), [RHSA-2026:33230](https://access.redhat.com/errata/RHSA-2026:33230), [CVE-2026-5450](https://nvd.nist.gov/vuln/detail/cve-2026-5450), [RHSA-2026:28832](https://access.redhat.com/errata/RHSA-2026:28832), and [CVE-2026-31790](https://nvd.nist.gov/vuln/detail/cve-2026-31790).


RHEL 8 (VPC) 4.18.0-553.139.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:35833](https://access.redhat.com/errata/RHSA-2026:35833), [CVE-2026-34986](https://nvd.nist.gov/vuln/detail/cve-2026-34986), [CVE-2026-39829](https://nvd.nist.gov/vuln/detail/cve-2026-39829), [CVE-2026-39830](https://nvd.nist.gov/vuln/detail/cve-2026-39830), [CVE-2026-39832](https://nvd.nist.gov/vuln/detail/cve-2026-39832), [CVE-2026-42508](https://nvd.nist.gov/vuln/detail/cve-2026-42508), [RHSA-2026:33722](https://access.redhat.com/errata/RHSA-2026:33722), [CVE-2026-25679](https://access.redhat.com/security/cve/cve-2026-25679), [CVE-2026-32280](https://nvd.nist.gov/vuln/detail/cve-2026-32280), [CVE-2026-32281](https://nvd.nist.gov/vuln/detail/cve-2026-32281), [CVE-2026-32283](https://nvd.nist.gov/vuln/detail/cve-2026-32283), [CVE-2026-34986](https://nvd.nist.gov/vuln/detail/cve-2026-34986), [RHSA-2026:33743](https://access.redhat.com/errata/RHSA-2026:33743), [CVE-2026-23216](https://nvd.nist.gov/vuln/detail/cve-2026-23216), [CVE-2026-45984](https://nvd.nist.gov/vuln/detail/cve-2026-45984), [CVE-2026-46189](https://nvd.nist.gov/vuln/detail/cve-2026-46189), [RHSA-2026:36776](https://access.redhat.com/errata/RHSA-2026:36776), [CVE-2026-33811](https://nvd.nist.gov/vuln/detail/cve-2026-33811), [RHSA-2026:37282](https://access.redhat.com/errata/RHSA-2026:37282), [CVE-2026-40622](https://nvd.nist.gov/vuln/detail/cve-2026-40622), [CVE-2026-41292](https://nvd.nist.gov/vuln/detail/cve-2026-41292), [CVE-2026-42534](https://nvd.nist.gov/vuln/detail/cve-2026-42534), [CVE-2026-44390](https://nvd.nist.gov/vuln/detail/cve-2026-44390), [RHSA-2026:36728](https://access.redhat.com/errata/RHSA-2026:36728), [CVE-2025-13151](https://nvd.nist.gov/vuln/detail/cve-2025-13151), [RHSA-2026:36734](https://access.redhat.com/errata/RHSA-2026:36734), [CVE-2025-6170](https://nvd.nist.gov/vuln/detail/cve-2025-6170), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:33126](https://access.redhat.com/errata/RHSA-2026:33126), [CVE-2026-5450](https://nvd.nist.gov/vuln/detail/cve-2026-5450), [RHSA-2026:29898](https://access.redhat.com/errata/RHSA-2026:29898), [CVE-2026-33416](https://nvd.nist.gov/vuln/detail/cve-2026-33416), [RHSA-2026:36730](https://access.redhat.com/errata/RHSA-2026:36730), [CVE-2026-48864](https://nvd.nist.gov/vuln/detail/cve-2026-48864), [RHSA-2026:36732](https://access.redhat.com/errata/RHSA-2026:36732), and [CVE-2026-44431](https://nvd.nist.gov/vuln/detail/cve-2026-44431).


RHEL 8 (Classic) 4.18.0-553.139.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:35833](https://access.redhat.com/errata/RHSA-2026:35833), [CVE-2026-34986](https://nvd.nist.gov/vuln/detail/cve-2026-34986), [CVE-2026-39829](https://nvd.nist.gov/vuln/detail/cve-2026-39829), [CVE-2026-39830](https://nvd.nist.gov/vuln/detail/cve-2026-39830), [CVE-2026-39832](https://nvd.nist.gov/vuln/detail/cve-2026-39832), [CVE-2026-42508](https://nvd.nist.gov/vuln/detail/cve-2026-42508), [RHSA-2026:33722](https://access.redhat.com/errata/RHSA-2026:33722), [CVE-2026-25679](https://access.redhat.com/security/cve/cve-2026-25679), [CVE-2026-32280](https://nvd.nist.gov/vuln/detail/cve-2026-32280), [CVE-2026-32281](https://nvd.nist.gov/vuln/detail/cve-2026-32281), [CVE-2026-32283](https://nvd.nist.gov/vuln/detail/cve-2026-32283), [CVE-2026-34986](https://nvd.nist.gov/vuln/detail/cve-2026-34986), [RHSA-2026:33743](https://access.redhat.com/errata/RHSA-2026:33743), [CVE-2026-23216](https://nvd.nist.gov/vuln/detail/cve-2026-23216), [CVE-2026-45984](https://nvd.nist.gov/vuln/detail/cve-2026-45984), [CVE-2026-46189](https://nvd.nist.gov/vuln/detail/cve-2026-46189), [RHSA-2026:36776](https://access.redhat.com/errata/RHSA-2026:36776), [CVE-2026-33811](https://nvd.nist.gov/vuln/detail/cve-2026-33811), [RHSA-2026:37282](https://access.redhat.com/errata/RHSA-2026:37282), [CVE-2026-40622](https://nvd.nist.gov/vuln/detail/cve-2026-40622), [CVE-2026-41292](https://nvd.nist.gov/vuln/detail/cve-2026-41292), [CVE-2026-42534](https://nvd.nist.gov/vuln/detail/cve-2026-42534), [CVE-2026-44390](https://nvd.nist.gov/vuln/detail/cve-2026-44390), [RHSA-2026:36728](https://access.redhat.com/errata/RHSA-2026:36728), [CVE-2025-13151](https://nvd.nist.gov/vuln/detail/cve-2025-13151), [RHSA-2026:36734](https://access.redhat.com/errata/RHSA-2026:36734), [CVE-2025-6170](https://nvd.nist.gov/vuln/detail/cve-2025-6170), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:33126](https://access.redhat.com/errata/RHSA-2026:33126), [CVE-2026-5450](https://nvd.nist.gov/vuln/detail/cve-2026-5450), [RHSA-2026:29898](https://access.redhat.com/errata/RHSA-2026:29898), [CVE-2026-33416](https://nvd.nist.gov/vuln/detail/cve-2026-33416), [RHSA-2026:36730](https://access.redhat.com/errata/RHSA-2026:36730), [CVE-2026-48864](https://nvd.nist.gov/vuln/detail/cve-2026-48864), [RHSA-2026:36732](https://access.redhat.com/errata/RHSA-2026:36732), and [CVE-2026-44431](https://nvd.nist.gov/vuln/detail/cve-2026-44431).


Red Hat OpenShift 4.17.55
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-55_release-notes){: external}.


Red Hat CoreOS 4.17.55
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-55_release-notes){: external}.


HAProxy 27f76d0c7626993cde6e1ff90fa42253718cc5fa
:   Resolves the following CVEs: [CVE-2026-5450](https://nvd.nist.gov/vuln/detail/cve-2026-5450).


## 01 July 2026, Worker node fix pack 4.17.54_1591_openshift
{: #cl-boms-41754_1591_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.54_1591_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.123.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:24500](https://access.redhat.com/errata/RHSA-2026:24500), [CVE-2026-1519](https://nvd.nist.gov/vuln/detail/cve-2026-1519), [RHSA-2026:23224](https://access.redhat.com/errata/RHSA-2026:23224), [CVE-2025-38653](https://nvd.nist.gov/vuln/detail/cve-2025-38653), [CVE-2025-39766](https://nvd.nist.gov/vuln/detail/cve-2025-39766), [CVE-2025-68366](https://nvd.nist.gov/vuln/detail/cve-2025-68366), [CVE-2026-23210](https://nvd.nist.gov/vuln/detail/cve-2026-23210), [CVE-2026-23270](https://nvd.nist.gov/vuln/detail/cve-2026-23270), [CVE-2026-23392](https://nvd.nist.gov/vuln/detail/cve-2026-23392), [CVE-2026-31419](https://nvd.nist.gov/vuln/detail/cve-2026-31419), [CVE-2026-31607](https://nvd.nist.gov/vuln/detail/cve-2026-31607), [CVE-2026-31685](https://nvd.nist.gov/vuln/detail/cve-2026-31685), [CVE-2026-31709](https://nvd.nist.gov/vuln/detail/cve-2026-31709), [CVE-2026-43037](https://nvd.nist.gov/vuln/detail/cve-2026-43037), [CVE-2026-43038](https://nvd.nist.gov/vuln/detail/cve-2026-43038), [CVE-2026-43163](https://nvd.nist.gov/vuln/detail/cve-2026-43163), [RHSA-2026:25218](https://access.redhat.com/errata/RHSA-2026:25218), [CVE-2025-40135](https://nvd.nist.gov/vuln/detail/cve-2025-40135), [CVE-2025-40158](https://nvd.nist.gov/vuln/detail/cve-2025-40158), [CVE-2025-40170](https://nvd.nist.gov/vuln/detail/cve-2025-40170), [CVE-2025-68724](https://nvd.nist.gov/vuln/detail/cve-2025-68724), [CVE-2025-71089](https://nvd.nist.gov/vuln/detail/cve-2025-71089), [CVE-2025-71116](https://nvd.nist.gov/vuln/detail/cve-2025-71116), [CVE-2026-22984](https://nvd.nist.gov/vuln/detail/cve-2026-22984), [CVE-2026-22990](https://nvd.nist.gov/vuln/detail/cve-2026-22990), [CVE-2026-23216](https://nvd.nist.gov/vuln/detail/cve-2026-23216), [CVE-2026-23455](https://nvd.nist.gov/vuln/detail/cve-2026-23455), [CVE-2026-31508](https://nvd.nist.gov/vuln/detail/cve-2026-31508), [CVE-2026-43110](https://nvd.nist.gov/vuln/detail/cve-2026-43110), [CVE-2026-43190](https://nvd.nist.gov/vuln/detail/cve-2026-43190), [RHSA-2026:27708](https://access.redhat.com/errata/RHSA-2026:27708), [CVE-2025-40064](https://nvd.nist.gov/vuln/detail/cve-2025-40064), [CVE-2025-40168](https://nvd.nist.gov/vuln/detail/cve-2025-40168), [CVE-2026-23136](https://nvd.nist.gov/vuln/detail/cve-2026-23136), [CVE-2026-43116](https://nvd.nist.gov/vuln/detail/cve-2026-43116), [CVE-2026-43158](https://nvd.nist.gov/vuln/detail/cve-2026-43158), [CVE-2026-43303](https://nvd.nist.gov/vuln/detail/cve-2026-43303), [CVE-2026-45898](https://nvd.nist.gov/vuln/detail/cve-2026-45898), [CVE-2026-46125](https://nvd.nist.gov/vuln/detail/cve-2026-46125), [CVE-2026-46166](https://nvd.nist.gov/vuln/detail/cve-2026-46166), [CVE-2026-46243](https://nvd.nist.gov/vuln/detail/cve-2026-46243), [CVE-2026-46323](https://nvd.nist.gov/vuln/detail/cve-2026-46323), [CVE-2026-46331](https://nvd.nist.gov/vuln/detail/cve-2026-46331), [RHSA-2026:24683](https://access.redhat.com/errata/RHSA-2026:24683), [CVE-2026-40356](https://nvd.nist.gov/vuln/detail/cve-2026-40356), [RHSA-2026:24337](https://access.redhat.com/errata/RHSA-2026:24337), [CVE-2026-32280](https://nvd.nist.gov/vuln/detail/cve-2026-32280), [CVE-2026-32281](https://nvd.nist.gov/vuln/detail/cve-2026-32281), [CVE-2026-32282](https://nvd.nist.gov/vuln/detail/cve-2026-32282), [CVE-2026-32283](https://nvd.nist.gov/vuln/detail/cve-2026-32283), [RHSA-2026:25979](https://access.redhat.com/errata/RHSA-2026:25979), [CVE-2026-1933](https://nvd.nist.gov/vuln/detail/cve-2026-1933), [CVE-2026-2340](https://nvd.nist.gov/vuln/detail/cve-2026-2340), [CVE-2026-3012](https://nvd.nist.gov/vuln/detail/cve-2026-3012), [CVE-2026-4408](https://nvd.nist.gov/vuln/detail/cve-2026-4408), [CVE-2026-4480](https://nvd.nist.gov/vuln/detail/cve-2026-4480), [RHSA-2026:28050](https://access.redhat.com/errata/RHSA-2026:28050), [CVE-2026-34982](https://nvd.nist.gov/vuln/detail/cve-2026-34982), [CVE-2026-35177](https://nvd.nist.gov/vuln/detail/cve-2026-35177), [CVE-2026-41411](https://nvd.nist.gov/vuln/detail/cve-2026-41411), and [CVE-2026-46483](https://nvd.nist.gov/vuln/detail/cve-2026-46483).


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-570.123.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:24500](https://access.redhat.com/errata/RHSA-2026:24500), [CVE-2026-1519](https://nvd.nist.gov/vuln/detail/cve-2026-1519), [RHSA-2026:23224](https://access.redhat.com/errata/RHSA-2026:23224), [CVE-2025-38653](https://nvd.nist.gov/vuln/detail/cve-2025-38653), [CVE-2025-39766](https://nvd.nist.gov/vuln/detail/cve-2025-39766), [CVE-2025-68366](https://nvd.nist.gov/vuln/detail/cve-2025-68366), [CVE-2026-23210](https://nvd.nist.gov/vuln/detail/cve-2026-23210), [CVE-2026-23270](https://nvd.nist.gov/vuln/detail/cve-2026-23270), [CVE-2026-23392](https://nvd.nist.gov/vuln/detail/cve-2026-23392), [CVE-2026-31419](https://nvd.nist.gov/vuln/detail/cve-2026-31419), [CVE-2026-31607](https://nvd.nist.gov/vuln/detail/cve-2026-31607), [CVE-2026-31685](https://nvd.nist.gov/vuln/detail/cve-2026-31685), [CVE-2026-31709](https://nvd.nist.gov/vuln/detail/cve-2026-31709), [CVE-2026-43037](https://nvd.nist.gov/vuln/detail/cve-2026-43037), [CVE-2026-43038](https://nvd.nist.gov/vuln/detail/cve-2026-43038), [CVE-2026-43163](https://nvd.nist.gov/vuln/detail/cve-2026-43163), [RHSA-2026:25218](https://access.redhat.com/errata/RHSA-2026:25218), [CVE-2025-40135](https://nvd.nist.gov/vuln/detail/cve-2025-40135), [CVE-2025-40158](https://nvd.nist.gov/vuln/detail/cve-2025-40158), [CVE-2025-40170](https://nvd.nist.gov/vuln/detail/cve-2025-40170), [CVE-2025-68724](https://nvd.nist.gov/vuln/detail/cve-2025-68724), [CVE-2025-71089](https://nvd.nist.gov/vuln/detail/cve-2025-71089), [CVE-2025-71116](https://nvd.nist.gov/vuln/detail/cve-2025-71116), [CVE-2026-22984](https://nvd.nist.gov/vuln/detail/cve-2026-22984), [CVE-2026-22990](https://nvd.nist.gov/vuln/detail/cve-2026-22990), [CVE-2026-23216](https://nvd.nist.gov/vuln/detail/cve-2026-23216), [CVE-2026-23455](https://nvd.nist.gov/vuln/detail/cve-2026-23455), [CVE-2026-31508](https://nvd.nist.gov/vuln/detail/cve-2026-31508), [CVE-2026-43110](https://nvd.nist.gov/vuln/detail/cve-2026-43110), [CVE-2026-43190](https://nvd.nist.gov/vuln/detail/cve-2026-43190), [RHSA-2026:27708](https://access.redhat.com/errata/RHSA-2026:27708), [CVE-2025-40064](https://nvd.nist.gov/vuln/detail/cve-2025-40064), [CVE-2025-40168](https://nvd.nist.gov/vuln/detail/cve-2025-40168), [CVE-2026-23136](https://nvd.nist.gov/vuln/detail/cve-2026-23136), [CVE-2026-43116](https://nvd.nist.gov/vuln/detail/cve-2026-43116), [CVE-2026-43158](https://nvd.nist.gov/vuln/detail/cve-2026-43158), [CVE-2026-43303](https://nvd.nist.gov/vuln/detail/cve-2026-43303), [CVE-2026-45898](https://nvd.nist.gov/vuln/detail/cve-2026-45898), [CVE-2026-46125](https://nvd.nist.gov/vuln/detail/cve-2026-46125), [CVE-2026-46166](https://nvd.nist.gov/vuln/detail/cve-2026-46166), [CVE-2026-46243](https://nvd.nist.gov/vuln/detail/cve-2026-46243), [CVE-2026-46323](https://nvd.nist.gov/vuln/detail/cve-2026-46323), [CVE-2026-46331](https://nvd.nist.gov/vuln/detail/cve-2026-46331), [RHSA-2026:24683](https://access.redhat.com/errata/RHSA-2026:24683), [CVE-2026-40356](https://nvd.nist.gov/vuln/detail/cve-2026-40356), [RHSA-2026:24337](https://access.redhat.com/errata/RHSA-2026:24337), [CVE-2026-32280](https://nvd.nist.gov/vuln/detail/cve-2026-32280), [CVE-2026-32281](https://nvd.nist.gov/vuln/detail/cve-2026-32281), [CVE-2026-32282](https://nvd.nist.gov/vuln/detail/cve-2026-32282), [CVE-2026-32283](https://nvd.nist.gov/vuln/detail/cve-2026-32283), [RHSA-2026:25979](https://access.redhat.com/errata/RHSA-2026:25979), [CVE-2026-1933](https://nvd.nist.gov/vuln/detail/cve-2026-1933), [CVE-2026-2340](https://nvd.nist.gov/vuln/detail/cve-2026-2340), [CVE-2026-3012](https://nvd.nist.gov/vuln/detail/cve-2026-3012), [CVE-2026-4408](https://nvd.nist.gov/vuln/detail/cve-2026-4408), [CVE-2026-4480](https://nvd.nist.gov/vuln/detail/cve-2026-4480), [RHSA-2026:28050](https://access.redhat.com/errata/RHSA-2026:28050), [CVE-2026-34982](https://nvd.nist.gov/vuln/detail/cve-2026-34982), [CVE-2026-35177](https://nvd.nist.gov/vuln/detail/cve-2026-35177), [CVE-2026-41411](https://nvd.nist.gov/vuln/detail/cve-2026-41411), and [CVE-2026-46483](https://nvd.nist.gov/vuln/detail/cve-2026-46483).


RHEL 8 (VPC) 4.18.0-553.137.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:25121](https://access.redhat.com/errata/RHSA-2026:25121), [CVE-2023-53781](https://nvd.nist.gov/vuln/detail/cve-2023-53781), [CVE-2025-21858](https://nvd.nist.gov/vuln/detail/cve-2025-21858), [CVE-2025-68366](https://nvd.nist.gov/vuln/detail/cve-2025-68366), [CVE-2026-22984](https://nvd.nist.gov/vuln/detail/cve-2026-22984), [CVE-2026-22990](https://nvd.nist.gov/vuln/detail/cve-2026-22990), [CVE-2026-23392](https://nvd.nist.gov/vuln/detail/cve-2026-23392), [CVE-2026-31581](https://nvd.nist.gov/vuln/detail/cve-2026-31581), [CVE-2026-31613](https://nvd.nist.gov/vuln/detail/cve-2026-31613), [CVE-2026-43037](https://nvd.nist.gov/vuln/detail/cve-2026-43037), [CVE-2026-43038](https://nvd.nist.gov/vuln/detail/cve-2026-43038), [CVE-2026-43125](https://nvd.nist.gov/vuln/detail/cve-2026-43125), [CVE-2026-45852](https://nvd.nist.gov/vuln/detail/cve-2026-45852), [CVE-2026-46181](https://nvd.nist.gov/vuln/detail/cve-2026-46181), [RHSA-2026:26534](https://access.redhat.com/errata/RHSA-2026:26534), [CVE-2026-6893](https://nvd.nist.gov/vuln/detail/cve-2026-6893), [RHSA-2026:26427](https://access.redhat.com/errata/RHSA-2026:26427), [CVE-2026-31669](https://nvd.nist.gov/vuln/detail/cve-2026-31669), [CVE-2026-31786](https://nvd.nist.gov/vuln/detail/cve-2026-31786), [CVE-2026-31787](https://nvd.nist.gov/vuln/detail/cve-2026-31787), [CVE-2026-43110](https://nvd.nist.gov/vuln/detail/cve-2026-43110), [CVE-2026-43329](https://nvd.nist.gov/vuln/detail/cve-2026-43329), [CVE-2026-46056](https://nvd.nist.gov/vuln/detail/cve-2026-46056), [CVE-2026-46125](https://nvd.nist.gov/vuln/detail/cve-2026-46125), [CVE-2026-46152](https://nvd.nist.gov/vuln/detail/cve-2026-46152), [RHSA-2026:27811](https://access.redhat.com/errata/RHSA-2026:27811), [CVE-2026-46054](https://nvd.nist.gov/vuln/detail/cve-2026-46054), [RHSA-2026:27353](https://access.redhat.com/errata/RHSA-2026:27353), [CVE-2026-31419](https://nvd.nist.gov/vuln/detail/cve-2026-31419), [CVE-2026-31488](https://nvd.nist.gov/vuln/detail/cve-2026-31488), [CVE-2026-43056](https://nvd.nist.gov/vuln/detail/cve-2026-43056), [CVE-2026-43279](https://nvd.nist.gov/vuln/detail/cve-2026-43279), [CVE-2026-46090](https://nvd.nist.gov/vuln/detail/cve-2026-46090), [CVE-2026-46135](https://nvd.nist.gov/vuln/detail/cve-2026-46135), [CVE-2026-46145](https://nvd.nist.gov/vuln/detail/cve-2026-46145), [CVE-2026-46331](https://nvd.nist.gov/vuln/detail/cve-2026-46331), [RHSA-2026:26275](https://access.redhat.com/errata/RHSA-2026:26275), [CVE-2024-4741](https://nvd.nist.gov/vuln/detail/cve-2024-4741), [CVE-2026-45447](https://nvd.nist.gov/vuln/detail/cve-2026-45447), [RHSA-2026:26408](https://access.redhat.com/errata/RHSA-2026:26408), [CVE-2026-29518](https://nvd.nist.gov/vuln/detail/cve-2026-29518), [CVE-2026-43618](https://nvd.nist.gov/vuln/detail/cve-2026-43618), [RHSA-2026:26354](https://access.redhat.com/errata/RHSA-2026:26354), [CVE-2024-34459](https://nvd.nist.gov/vuln/detail/cve-2024-34459), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:29898](https://access.redhat.com/errata/RHSA-2026:29898), [CVE-2026-33416](https://nvd.nist.gov/vuln/detail/cve-2026-33416), [RHSA-2026:28553](https://access.redhat.com/errata/RHSA-2026:28553), and [CVE-2026-41411](https://nvd.nist.gov/vuln/detail/cve-2026-41411).


RHEL 8 (Classic) 4.18.0-553.137.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:25121](https://access.redhat.com/errata/RHSA-2026:25121), [CVE-2023-53781](https://nvd.nist.gov/vuln/detail/cve-2023-53781), [CVE-2025-21858](https://nvd.nist.gov/vuln/detail/cve-2025-21858), [CVE-2025-68366](https://nvd.nist.gov/vuln/detail/cve-2025-68366), [CVE-2026-22984](https://nvd.nist.gov/vuln/detail/cve-2026-22984), [CVE-2026-22990](https://nvd.nist.gov/vuln/detail/cve-2026-22990), [CVE-2026-23392](https://nvd.nist.gov/vuln/detail/cve-2026-23392), [CVE-2026-31581](https://nvd.nist.gov/vuln/detail/cve-2026-31581), [CVE-2026-31613](https://nvd.nist.gov/vuln/detail/cve-2026-31613), [CVE-2026-43037](https://nvd.nist.gov/vuln/detail/cve-2026-43037), [CVE-2026-43038](https://nvd.nist.gov/vuln/detail/cve-2026-43038), [CVE-2026-43125](https://nvd.nist.gov/vuln/detail/cve-2026-43125), [CVE-2026-45852](https://nvd.nist.gov/vuln/detail/cve-2026-45852), [CVE-2026-46181](https://nvd.nist.gov/vuln/detail/cve-2026-46181), [RHSA-2026:26534](https://access.redhat.com/errata/RHSA-2026:26534), [CVE-2026-6893](https://nvd.nist.gov/vuln/detail/cve-2026-6893), [RHSA-2026:26427](https://access.redhat.com/errata/RHSA-2026:26427), [CVE-2026-31669](https://nvd.nist.gov/vuln/detail/cve-2026-31669), [CVE-2026-31786](https://nvd.nist.gov/vuln/detail/cve-2026-31786), [CVE-2026-31787](https://nvd.nist.gov/vuln/detail/cve-2026-31787), [CVE-2026-43110](https://nvd.nist.gov/vuln/detail/cve-2026-43110), [CVE-2026-43329](https://nvd.nist.gov/vuln/detail/cve-2026-43329), [CVE-2026-46056](https://nvd.nist.gov/vuln/detail/cve-2026-46056), [CVE-2026-46125](https://nvd.nist.gov/vuln/detail/cve-2026-46125), [CVE-2026-46152](https://nvd.nist.gov/vuln/detail/cve-2026-46152), [RHSA-2026:27811](https://access.redhat.com/errata/RHSA-2026:27811), [CVE-2026-46054](https://nvd.nist.gov/vuln/detail/cve-2026-46054), [RHSA-2026:27353](https://access.redhat.com/errata/RHSA-2026:27353), [CVE-2026-31419](https://nvd.nist.gov/vuln/detail/cve-2026-31419), [CVE-2026-31488](https://nvd.nist.gov/vuln/detail/cve-2026-31488), [CVE-2026-43056](https://nvd.nist.gov/vuln/detail/cve-2026-43056), [CVE-2026-43279](https://nvd.nist.gov/vuln/detail/cve-2026-43279), [CVE-2026-46090](https://nvd.nist.gov/vuln/detail/cve-2026-46090), [CVE-2026-46135](https://nvd.nist.gov/vuln/detail/cve-2026-46135), [CVE-2026-46145](https://nvd.nist.gov/vuln/detail/cve-2026-46145), [CVE-2026-46331](https://nvd.nist.gov/vuln/detail/cve-2026-46331), [RHSA-2026:26275](https://access.redhat.com/errata/RHSA-2026:26275), [CVE-2024-4741](https://nvd.nist.gov/vuln/detail/cve-2024-4741), [CVE-2026-45447](https://nvd.nist.gov/vuln/detail/cve-2026-45447), [RHSA-2026:26408](https://access.redhat.com/errata/RHSA-2026:26408), [CVE-2026-29518](https://nvd.nist.gov/vuln/detail/cve-2026-29518), [CVE-2026-43618](https://nvd.nist.gov/vuln/detail/cve-2026-43618), [RHSA-2026:26354](https://access.redhat.com/errata/RHSA-2026:26354), [CVE-2024-34459](https://nvd.nist.gov/vuln/detail/cve-2024-34459), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:29898](https://access.redhat.com/errata/RHSA-2026:29898), [CVE-2026-33416](https://nvd.nist.gov/vuln/detail/cve-2026-33416), [RHSA-2026:28553](https://access.redhat.com/errata/RHSA-2026:28553), and [CVE-2026-41411](https://nvd.nist.gov/vuln/detail/cve-2026-41411).


Red Hat OpenShift 4.17.54
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-54_release-notes){: external}.


Red Hat CoreOS 4.17.54
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-54_release-notes){: external}.


HAProxy 119de539a7da3c92449b38e1531722802988e50c
:   Resolves the following CVEs: [CVE-2026-45447](https://nvd.nist.gov/vuln/detail/cve-2026-45447), [CVE-2024-4741](https://nvd.nist.gov/vuln/detail/cve-2024-4741), and [CVE-2024-34459](https://nvd.nist.gov/vuln/detail/cve-2024-34459).


## 26 June 2026, Master fix pack 4.17.54_1589_openshift
{: #cl-boms_master-41754_1589_openshift_M}

The following list shows the components that are in the master fix pack 4.17.54_1589_openshift. Master patch updates are applied automatically.
{: shortdesc}

Cluster health image v1.6.16
:   New version contains updates and security fixes.


etcd v3.5.30
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.30){: external}.


IBM Cloud Block Storage driver and plug-in v2.5.26
:   New version contains updates and security fixes.


IBM Cloud Controller Manager v1.30.14-44
:   New version contains updates and security fixes.


IBM Cloud File Storage for Classic plug-in and monitor v455
:   New version contains updates and security fixes.


Key Management Service provider 2.10.25
:   New version contains updates and security fixes.


Portieris admission controller v0.14.0
:   See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.14.0){: external}


Red Hat OpenShift on IBM Cloud 4.17.54
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-54_release-notes){: external}.


Red Hat OpenShift on IBM Cloud Control Plane Operator, Metrics Server, and toolkit v4.17.0+20260531
:   See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.17.0+20260531){: external}.


## 15 June 2026, Worker node fix pack 4.17.54_1590_openshift
{: #cl-boms-41754_1590_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.54_1590_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.116.1.el9_6
:   Resolves the following CVEs: [CVE-2026-5119](https://nvd.nist.gov/vuln/detail/cve-2026-5119).


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-570.116.1.el9_6
:   


RHEL 8 (VPC) 4.18.0-553.129.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:25121](https://access.redhat.com/errata/RHSA-2026:25121), [CVE-2023-53781](https://nvd.nist.gov/vuln/detail/cve-2023-53781), [CVE-2025-21858](https://nvd.nist.gov/vuln/detail/cve-2025-21858), [CVE-2025-68366](https://nvd.nist.gov/vuln/detail/cve-2025-68366), [CVE-2026-22984](https://nvd.nist.gov/vuln/detail/cve-2026-22984), [CVE-2026-22990](https://nvd.nist.gov/vuln/detail/cve-2026-22990), [CVE-2026-23392](https://nvd.nist.gov/vuln/detail/cve-2026-23392), [CVE-2026-31581](https://nvd.nist.gov/vuln/detail/cve-2026-31581), [CVE-2026-31613](https://nvd.nist.gov/vuln/detail/cve-2026-31613), [CVE-2026-43037](https://nvd.nist.gov/vuln/detail/cve-2026-43037), [CVE-2026-43038](https://nvd.nist.gov/vuln/detail/cve-2026-43038), [CVE-2026-43125](https://nvd.nist.gov/vuln/detail/cve-2026-43125), [CVE-2026-45852](https://nvd.nist.gov/vuln/detail/cve-2026-45852), [CVE-2026-46181](https://nvd.nist.gov/vuln/detail/cve-2026-46181), [RHSA-2026:24339](https://access.redhat.com/errata/RHSA-2026:24339), [CVE-2026-3039](https://nvd.nist.gov/vuln/detail/cve-2026-3039), [CVE-2026-5946](https://nvd.nist.gov/vuln/detail/cve-2026-5946), [RHSA-2026:22721](https://access.redhat.com/errata/RHSA-2026:22721), [CVE-2026-45186](https://nvd.nist.gov/vuln/detail/cve-2026-45186), [RHSA-2026:21706](https://access.redhat.com/errata/RHSA-2026:21706), [CVE-2025-39981](https://nvd.nist.gov/vuln/detail/cve-2025-39981), [CVE-2025-68183](https://nvd.nist.gov/vuln/detail/cve-2025-68183), [CVE-2025-68347](https://nvd.nist.gov/vuln/detail/cve-2025-68347), [CVE-2025-71116](https://nvd.nist.gov/vuln/detail/cve-2025-71116), [CVE-2026-23243](https://nvd.nist.gov/vuln/detail/cve-2026-23243), [CVE-2026-23270](https://nvd.nist.gov/vuln/detail/cve-2026-23270), [CVE-2026-23455](https://nvd.nist.gov/vuln/detail/cve-2026-23455), [CVE-2026-31408](https://nvd.nist.gov/vuln/detail/cve-2026-31408), [CVE-2026-31532](https://nvd.nist.gov/vuln/detail/cve-2026-31532), [CVE-2026-31684](https://nvd.nist.gov/vuln/detail/cve-2026-31684), [CVE-2026-31685](https://nvd.nist.gov/vuln/detail/cve-2026-31685), [CVE-2026-31709](https://nvd.nist.gov/vuln/detail/cve-2026-31709), [CVE-2026-43020](https://nvd.nist.gov/vuln/detail/cve-2026-43020), [CVE-2026-43027](https://nvd.nist.gov/vuln/detail/cve-2026-43027), [CVE-2026-43051](https://nvd.nist.gov/vuln/detail/cve-2026-43051), [CVE-2026-43158](https://nvd.nist.gov/vuln/detail/cve-2026-43158), [CVE-2026-43163](https://nvd.nist.gov/vuln/detail/cve-2026-43163), [CVE-2026-43190](https://nvd.nist.gov/vuln/detail/cve-2026-43190), [RHSA-2026:23258](https://access.redhat.com/errata/RHSA-2026:23258), [CVE-2026-46243](https://nvd.nist.gov/vuln/detail/cve-2026-46243), [RHSA-2026:24365](https://access.redhat.com/errata/RHSA-2026:24365), [CVE-2026-42944](https://nvd.nist.gov/vuln/detail/cve-2026-42944), [CVE-2026-42959](https://nvd.nist.gov/vuln/detail/cve-2026-42959), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:22730](https://access.redhat.com/errata/RHSA-2026:22730), and [CVE-2026-35177](https://nvd.nist.gov/vuln/detail/cve-2026-35177).


RHEL 8 (Classic) 4.18.0-553.129.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:25121](https://access.redhat.com/errata/RHSA-2026:25121), [CVE-2023-53781](https://nvd.nist.gov/vuln/detail/cve-2023-53781), [CVE-2025-21858](https://nvd.nist.gov/vuln/detail/cve-2025-21858), [CVE-2025-68366](https://nvd.nist.gov/vuln/detail/cve-2025-68366), [CVE-2026-22984](https://nvd.nist.gov/vuln/detail/cve-2026-22984), [CVE-2026-22990](https://nvd.nist.gov/vuln/detail/cve-2026-22990), [CVE-2026-23392](https://nvd.nist.gov/vuln/detail/cve-2026-23392), [CVE-2026-31581](https://nvd.nist.gov/vuln/detail/cve-2026-31581), [CVE-2026-31613](https://nvd.nist.gov/vuln/detail/cve-2026-31613), [CVE-2026-43037](https://nvd.nist.gov/vuln/detail/cve-2026-43037), [CVE-2026-43038](https://nvd.nist.gov/vuln/detail/cve-2026-43038), [CVE-2026-43125](https://nvd.nist.gov/vuln/detail/cve-2026-43125), [CVE-2026-45852](https://nvd.nist.gov/vuln/detail/cve-2026-45852), [CVE-2026-46181](https://nvd.nist.gov/vuln/detail/cve-2026-46181), [RHSA-2026:24339](https://access.redhat.com/errata/RHSA-2026:24339), [CVE-2026-3039](https://nvd.nist.gov/vuln/detail/cve-2026-3039), [CVE-2026-5946](https://nvd.nist.gov/vuln/detail/cve-2026-5946), [RHSA-2026:22721](https://access.redhat.com/errata/RHSA-2026:22721), [CVE-2026-45186](https://nvd.nist.gov/vuln/detail/cve-2026-45186), [RHSA-2026:21706](https://access.redhat.com/errata/RHSA-2026:21706), [CVE-2025-39981](https://nvd.nist.gov/vuln/detail/cve-2025-39981), [CVE-2025-68183](https://nvd.nist.gov/vuln/detail/cve-2025-68183), [CVE-2025-68347](https://nvd.nist.gov/vuln/detail/cve-2025-68347), [CVE-2025-71116](https://nvd.nist.gov/vuln/detail/cve-2025-71116), [CVE-2026-23243](https://nvd.nist.gov/vuln/detail/cve-2026-23243), [CVE-2026-23270](https://nvd.nist.gov/vuln/detail/cve-2026-23270), [CVE-2026-23455](https://nvd.nist.gov/vuln/detail/cve-2026-23455), [CVE-2026-31408](https://nvd.nist.gov/vuln/detail/cve-2026-31408), [CVE-2026-31532](https://nvd.nist.gov/vuln/detail/cve-2026-31532), [CVE-2026-31684](https://nvd.nist.gov/vuln/detail/cve-2026-31684), [CVE-2026-31685](https://nvd.nist.gov/vuln/detail/cve-2026-31685), [CVE-2026-31709](https://nvd.nist.gov/vuln/detail/cve-2026-31709), [CVE-2026-43020](https://nvd.nist.gov/vuln/detail/cve-2026-43020), [CVE-2026-43027](https://nvd.nist.gov/vuln/detail/cve-2026-43027), [CVE-2026-43051](https://nvd.nist.gov/vuln/detail/cve-2026-43051), [CVE-2026-43158](https://nvd.nist.gov/vuln/detail/cve-2026-43158), [CVE-2026-43163](https://nvd.nist.gov/vuln/detail/cve-2026-43163), [CVE-2026-43190](https://nvd.nist.gov/vuln/detail/cve-2026-43190), [RHSA-2026:23258](https://access.redhat.com/errata/RHSA-2026:23258), [CVE-2026-46243](https://nvd.nist.gov/vuln/detail/cve-2026-46243), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:22730](https://access.redhat.com/errata/RHSA-2026:22730), and [CVE-2026-35177](https://nvd.nist.gov/vuln/detail/cve-2026-35177).


Red Hat OpenShift 4.17.54
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-54_release-notes){: external}.


Red Hat CoreOS 4.17.54
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-54_release-notes){: external}.


HAProxy d4656f400ca14059e1b5b8ef8078b4903290791a
:   Resolves the following CVEs: [CVE-2026-45186](https://nvd.nist.gov/vuln/detail/cve-2026-45186).


## 03 June 2026, Worker node fix pack 4.17.54_1587_openshift
{: #cl-boms-41754_1587_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.54_1587_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.116.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:21392](https://access.redhat.com/errata/RHSA-2026:21392), [CVE-2026-4802](https://nvd.nist.gov/vuln/detail/cve-2026-4802), [RHSA-2026:18042](https://access.redhat.com/errata/RHSA-2026:18042), [CVE-2026-39979](https://nvd.nist.gov/vuln/detail/cve-2026-39979), [CVE-2026-40164](https://nvd.nist.gov/vuln/detail/cve-2026-40164), [RHSA-2026:16312](https://access.redhat.com/errata/RHSA-2026:16312), [CVE-2026-43284](https://nvd.nist.gov/vuln/detail/cve-2026-43284), [RHSA-2026:20129](https://access.redhat.com/errata/RHSA-2026:20129), [CVE-2026-46300](https://nvd.nist.gov/vuln/detail/cve-2026-46300), [CVE-2026-46333](https://nvd.nist.gov/vuln/detail/cve-2026-46333), [RHSA-2026:19458](https://access.redhat.com/errata/RHSA-2026:19458), [CVE-2026-4878](https://nvd.nist.gov/vuln/detail/cve-2026-4878), [RHSA-2026:18031](https://access.redhat.com/errata/RHSA-2026:18031), [CVE-2026-41651](https://nvd.nist.gov/vuln/detail/cve-2026-41651), [RHSA-2026:19576](https://access.redhat.com/errata/RHSA-2026:19576), [CVE-2026-4786](https://nvd.nist.gov/vuln/detail/cve-2026-4786), [CVE-2026-6100](https://nvd.nist.gov/vuln/detail/cve-2026-6100), [RHSA-2026:20603](https://access.redhat.com/errata/RHSA-2026:20603), [CVE-2024-12086](https://nvd.nist.gov/vuln/detail/cve-2024-12086), [CVE-2025-10158](https://nvd.nist.gov/vuln/detail/cve-2025-10158), [CVE-2026-41035](https://nvd.nist.gov/vuln/detail/cve-2026-41035), [RHSA-2026:19457](https://access.redhat.com/errata/RHSA-2026:19457), [CVE-2025-14087](https://nvd.nist.gov/vuln/detail/cve-2025-14087), [CVE-2025-14512](https://nvd.nist.gov/vuln/detail/cve-2025-14512), [RHSA-2026:20548](https://access.redhat.com/errata/RHSA-2026:20548), and [CVE-2026-33416](https://nvd.nist.gov/vuln/detail/cve-2026-33416).


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-570.116.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:18042](https://access.redhat.com/errata/RHSA-2026:18042), [CVE-2026-39979](https://nvd.nist.gov/vuln/detail/cve-2026-39979), [CVE-2026-40164](https://nvd.nist.gov/vuln/detail/cve-2026-40164), [RHSA-2026:16312](https://access.redhat.com/errata/RHSA-2026:16312), [CVE-2026-43284](https://nvd.nist.gov/vuln/detail/cve-2026-43284), [RHSA-2026:20129](https://access.redhat.com/errata/RHSA-2026:20129), [CVE-2026-46300](https://nvd.nist.gov/vuln/detail/cve-2026-46300), [CVE-2026-46333](https://nvd.nist.gov/vuln/detail/cve-2026-46333), [RHSA-2026:19458](https://access.redhat.com/errata/RHSA-2026:19458), [CVE-2026-4878](https://nvd.nist.gov/vuln/detail/cve-2026-4878), [RHSA-2026:19576](https://access.redhat.com/errata/RHSA-2026:19576), [CVE-2026-4786](https://nvd.nist.gov/vuln/detail/cve-2026-4786), [CVE-2026-6100](https://nvd.nist.gov/vuln/detail/cve-2026-6100), [RHSA-2026:19457](https://access.redhat.com/errata/RHSA-2026:19457), [CVE-2025-14087](https://nvd.nist.gov/vuln/detail/cve-2025-14087), [CVE-2025-14512](https://nvd.nist.gov/vuln/detail/cve-2025-14512), [RHSA-2026:20548](https://access.redhat.com/errata/RHSA-2026:20548), and [CVE-2026-33416](https://nvd.nist.gov/vuln/detail/cve-2026-33416).


RHEL 8 (VPC) 4.18.0-553.125.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:21700](https://access.redhat.com/errata/RHSA-2026:21700), [CVE-2026-4802](https://nvd.nist.gov/vuln/detail/cve-2026-4802), [RHSA-2026:20611](https://access.redhat.com/errata/RHSA-2026:20611), [CVE-2026-33845](https://nvd.nist.gov/vuln/detail/cve-2026-33845), [CVE-2026-33846](https://nvd.nist.gov/vuln/detail/cve-2026-33846), [CVE-2026-3833](https://nvd.nist.gov/vuln/detail/cve-2026-3833), [CVE-2026-42009](https://nvd.nist.gov/vuln/detail/cve-2026-42009), [CVE-2026-42010](https://nvd.nist.gov/vuln/detail/cve-2026-42010), [CVE-2026-42011](https://nvd.nist.gov/vuln/detail/cve-2026-42011), [CVE-2026-42012](https://nvd.nist.gov/vuln/detail/cve-2026-42012), [CVE-2026-42013](https://nvd.nist.gov/vuln/detail/cve-2026-42013), [CVE-2026-42014](https://nvd.nist.gov/vuln/detail/cve-2026-42014), [CVE-2026-42015](https://nvd.nist.gov/vuln/detail/cve-2026-42015), [CVE-2026-5260](https://nvd.nist.gov/vuln/detail/cve-2026-5260), [RHSA-2026:16195](https://access.redhat.com/errata/RHSA-2026:16195), [CVE-2026-43284](https://nvd.nist.gov/vuln/detail/cve-2026-43284), [RHSA-2026:19666](https://access.redhat.com/errata/RHSA-2026:19666), [CVE-2026-46300](https://nvd.nist.gov/vuln/detail/cve-2026-46300), [CVE-2026-46333](https://nvd.nist.gov/vuln/detail/cve-2026-46333), [RHSA-2026:21706](https://access.redhat.com/errata/RHSA-2026:21706), [CVE-2025-39981](https://nvd.nist.gov/vuln/detail/cve-2025-39981), [CVE-2025-68183](https://nvd.nist.gov/vuln/detail/cve-2025-68183), [CVE-2025-68347](https://nvd.nist.gov/vuln/detail/cve-2025-68347), [CVE-2025-71116](https://nvd.nist.gov/vuln/detail/cve-2025-71116), [CVE-2026-23243](https://nvd.nist.gov/vuln/detail/cve-2026-23243), [CVE-2026-23270](https://nvd.nist.gov/vuln/detail/cve-2026-23270), [CVE-2026-23455](https://nvd.nist.gov/vuln/detail/cve-2026-23455), [CVE-2026-31408](https://nvd.nist.gov/vuln/detail/cve-2026-31408), [CVE-2026-31532](https://nvd.nist.gov/vuln/detail/cve-2026-31532), [CVE-2026-31684](https://nvd.nist.gov/vuln/detail/cve-2026-31684), [CVE-2026-31685](https://nvd.nist.gov/vuln/detail/cve-2026-31685), [CVE-2026-31709](https://nvd.nist.gov/vuln/detail/cve-2026-31709), [CVE-2026-43020](https://nvd.nist.gov/vuln/detail/cve-2026-43020), [CVE-2026-43027](https://nvd.nist.gov/vuln/detail/cve-2026-43027), [CVE-2026-43051](https://nvd.nist.gov/vuln/detail/cve-2026-43051), [CVE-2026-43158](https://nvd.nist.gov/vuln/detail/cve-2026-43158), [CVE-2026-43163](https://nvd.nist.gov/vuln/detail/cve-2026-43163), [CVE-2026-43190](https://nvd.nist.gov/vuln/detail/cve-2026-43190), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:20587](https://access.redhat.com/errata/RHSA-2026:20587), and [CVE-2026-4046](https://nvd.nist.gov/vuln/detail/cve-2026-4046).


RHEL 8 (Classic) 4.18.0-553.125.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:20611](https://access.redhat.com/errata/RHSA-2026:20611), [CVE-2026-33845](https://nvd.nist.gov/vuln/detail/cve-2026-33845), [CVE-2026-33846](https://nvd.nist.gov/vuln/detail/cve-2026-33846), [CVE-2026-3833](https://nvd.nist.gov/vuln/detail/cve-2026-3833), [CVE-2026-42009](https://nvd.nist.gov/vuln/detail/cve-2026-42009), [CVE-2026-42010](https://nvd.nist.gov/vuln/detail/cve-2026-42010), [CVE-2026-42011](https://nvd.nist.gov/vuln/detail/cve-2026-42011), [CVE-2026-42012](https://nvd.nist.gov/vuln/detail/cve-2026-42012), [CVE-2026-42013](https://nvd.nist.gov/vuln/detail/cve-2026-42013), [CVE-2026-42014](https://nvd.nist.gov/vuln/detail/cve-2026-42014), [CVE-2026-42015](https://nvd.nist.gov/vuln/detail/cve-2026-42015), [CVE-2026-5260](https://nvd.nist.gov/vuln/detail/cve-2026-5260), [RHSA-2026:16195](https://access.redhat.com/errata/RHSA-2026:16195), [CVE-2026-43284](https://nvd.nist.gov/vuln/detail/cve-2026-43284), [RHSA-2026:19666](https://access.redhat.com/errata/RHSA-2026:19666), [CVE-2026-46300](https://nvd.nist.gov/vuln/detail/cve-2026-46300), [CVE-2026-46333](https://nvd.nist.gov/vuln/detail/cve-2026-46333), [RHSA-2026:21706](https://access.redhat.com/errata/RHSA-2026:21706), [CVE-2025-39981](https://nvd.nist.gov/vuln/detail/cve-2025-39981), [CVE-2025-68183](https://nvd.nist.gov/vuln/detail/cve-2025-68183), [CVE-2025-68347](https://nvd.nist.gov/vuln/detail/cve-2025-68347), [CVE-2025-71116](https://nvd.nist.gov/vuln/detail/cve-2025-71116), [CVE-2026-23243](https://nvd.nist.gov/vuln/detail/cve-2026-23243), [CVE-2026-23270](https://nvd.nist.gov/vuln/detail/cve-2026-23270), [CVE-2026-23455](https://nvd.nist.gov/vuln/detail/cve-2026-23455), [CVE-2026-31408](https://nvd.nist.gov/vuln/detail/cve-2026-31408), [CVE-2026-31532](https://nvd.nist.gov/vuln/detail/cve-2026-31532), [CVE-2026-31684](https://nvd.nist.gov/vuln/detail/cve-2026-31684), [CVE-2026-31685](https://nvd.nist.gov/vuln/detail/cve-2026-31685), [CVE-2026-31709](https://nvd.nist.gov/vuln/detail/cve-2026-31709), [CVE-2026-43020](https://nvd.nist.gov/vuln/detail/cve-2026-43020), [CVE-2026-43027](https://nvd.nist.gov/vuln/detail/cve-2026-43027), [CVE-2026-43051](https://nvd.nist.gov/vuln/detail/cve-2026-43051), [CVE-2026-43158](https://nvd.nist.gov/vuln/detail/cve-2026-43158), [CVE-2026-43163](https://nvd.nist.gov/vuln/detail/cve-2026-43163), [CVE-2026-43190](https://nvd.nist.gov/vuln/detail/cve-2026-43190), [RHSA-2026:20587](https://access.redhat.com/errata/RHSA-2026:20587), and [CVE-2026-4046](https://nvd.nist.gov/vuln/detail/cve-2026-4046).


Red Hat OpenShift 4.17.54
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-54_release-notes){: external}.


Red Hat CoreOS 4.17.54
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-54_release-notes){: external}.


HAProxy 0e0730588ba21878845cdb0bee615a371a489a02
:   Resolves the following CVEs: [CVE-2026-4046](https://nvd.nist.gov/vuln/detail/cve-2026-4046), [CVE-2026-33846](https://nvd.nist.gov/vuln/detail/cve-2026-33846), [CVE-2026-42010](https://nvd.nist.gov/vuln/detail/cve-2026-42010), [CVE-2026-5260](https://nvd.nist.gov/vuln/detail/cve-2026-5260), [CVE-2026-42014](https://nvd.nist.gov/vuln/detail/cve-2026-42014), [CVE-2026-3833](https://nvd.nist.gov/vuln/detail/cve-2026-3833), [CVE-2026-42015](https://nvd.nist.gov/vuln/detail/cve-2026-42015), [CVE-2026-33845](https://nvd.nist.gov/vuln/detail/cve-2026-33845), [CVE-2026-42011](https://nvd.nist.gov/vuln/detail/cve-2026-42011), [CVE-2026-42009](https://nvd.nist.gov/vuln/detail/cve-2026-42009), [CVE-2026-42013](https://nvd.nist.gov/vuln/detail/cve-2026-42013), and [CVE-2026-42012](https://nvd.nist.gov/vuln/detail/cve-2026-42012).


## 22 May 2026, Master fix pack 4.17.52_1585_openshift
{: #cl-boms_master-41752_1585_openshift_M}

The following list shows the components that are in the master fix pack 4.17.52_1585_openshift. Master patch updates are applied automatically.
{: shortdesc}

Calico v3.30.7
:   See the [Calico release notes](https://docs.tigera.io/calico/3.30/release-notes/#calico-open-source-3307-bug-fix-release){: external}.


IBM Cloud Controller Manager v1.30.14-42
:   New version contains updates and security fixes.


Key Management Service provider 2.10.24
:   New version contains updates and security fixes.


Portieris admission controller v0.13.38
:   See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.13.38){: external}


Tigera Operator v1.38.13
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.38.13){: external}.


## 20 May 2026, Worker node fix pack 4.17.53_1586_openshift
{: #cl-boms-41753_1586_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.53_1586_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) [5.14.0-570.112.1.el9_6](/docs/openshift?topic=openshift-openshift-relnotes#openshift-may2126)
:   Resolves the following CVEs: [RHSA-2025:22392](https://access.redhat.com/errata/RHSA-2025:22392), [CVE-2025-38724](https://nvd.nist.gov/vuln/detail/cve-2025-38724), [CVE-2025-39864](https://nvd.nist.gov/vuln/detail/cve-2025-39864), [CVE-2025-39881](https://nvd.nist.gov/vuln/detail/cve-2025-39881), [CVE-2025-39883](https://nvd.nist.gov/vuln/detail/cve-2025-39883), [CVE-2025-39918](https://nvd.nist.gov/vuln/detail/cve-2025-39918), [CVE-2025-39955](https://nvd.nist.gov/vuln/detail/cve-2025-39955), [CVE-2025-40186](https://nvd.nist.gov/vuln/detail/cve-2025-40186), [RHSA-2026:0457](https://access.redhat.com/errata/RHSA-2026:0457), [CVE-2025-23142](https://nvd.nist.gov/vuln/detail/cve-2025-23142), [CVE-2025-39806](https://nvd.nist.gov/vuln/detail/cve-2025-39806), [CVE-2025-39981](https://nvd.nist.gov/vuln/detail/cve-2025-39981), [CVE-2025-39983](https://nvd.nist.gov/vuln/detail/cve-2025-39983), [CVE-2025-40176](https://nvd.nist.gov/vuln/detail/cve-2025-40176), [CVE-2025-68287](https://nvd.nist.gov/vuln/detail/cve-2025-68287), [RHSA-2026:0804](https://access.redhat.com/errata/RHSA-2026:0804), [CVE-2025-21795](https://nvd.nist.gov/vuln/detail/cve-2025-21795), [CVE-2025-37849](https://nvd.nist.gov/vuln/detail/cve-2025-37849), [CVE-2025-37891](https://nvd.nist.gov/vuln/detail/cve-2025-37891), [CVE-2025-39697](https://nvd.nist.gov/vuln/detail/cve-2025-39697), [CVE-2025-40154](https://nvd.nist.gov/vuln/detail/cve-2025-40154), [CVE-2025-68285](https://nvd.nist.gov/vuln/detail/cve-2025-68285), [RHSA-2026:14339](https://access.redhat.com/errata/RHSA-2026:14339), [CVE-2024-53216](https://nvd.nist.gov/vuln/detail/cve-2024-53216), [CVE-2025-68741](https://nvd.nist.gov/vuln/detail/cve-2025-68741), [CVE-2026-23243](https://nvd.nist.gov/vuln/detail/cve-2026-23243), [CVE-2026-23401](https://nvd.nist.gov/vuln/detail/cve-2026-23401), [CVE-2026-31431](https://nvd.nist.gov/vuln/detail/cve-2026-31431), [CVE-2026-31532](https://nvd.nist.gov/vuln/detail/cve-2026-31532), [CVE-2026-43077](https://nvd.nist.gov/vuln/detail/cve-2026-43077), [RHSA-2026:16312](https://access.redhat.com/errata/RHSA-2026:16312), [CVE-2026-43284](https://nvd.nist.gov/vuln/detail/cve-2026-43284), [RHSA-2026:1703](https://access.redhat.com/errata/RHSA-2026:1703), [CVE-2025-21863](https://nvd.nist.gov/vuln/detail/cve-2025-21863), [CVE-2025-40248](https://nvd.nist.gov/vuln/detail/cve-2025-40248), [CVE-2025-68301](https://nvd.nist.gov/vuln/detail/cve-2025-68301), [RHSA-2026:16059](https://access.redhat.com/errata/RHSA-2026:16059), [CVE-2026-35385](https://nvd.nist.gov/vuln/detail/cve-2026-35385), [CVE-2026-35386](https://nvd.nist.gov/vuln/detail/cve-2026-35386), [CVE-2026-35387](https://nvd.nist.gov/vuln/detail/cve-2026-35387), [CVE-2026-35388](https://nvd.nist.gov/vuln/detail/cve-2026-35388), [CVE-2026-35414](https://nvd.nist.gov/vuln/detail/cve-2026-35414), [RHSA-2026:13889](https://access.redhat.com/errata/RHSA-2026:13889), [CVE-2026-35535](https://nvd.nist.gov/vuln/detail/cve-2026-35535), [RHSA-2025:21563](https://access.redhat.com/errata/RHSA-2025:21563), [CVE-2024-56690](https://nvd.nist.gov/vuln/detail/cve-2024-56690), [RHSA-2025:21933](https://access.redhat.com/errata/RHSA-2025:21933), [CVE-2025-39898](https://nvd.nist.gov/vuln/detail/cve-2025-39898), [CVE-2025-39971](https://nvd.nist.gov/vuln/detail/cve-2025-39971), [CVE-2025-39973](https://nvd.nist.gov/vuln/detail/cve-2025-39973), [CVE-2025-40047](https://nvd.nist.gov/vuln/detail/cve-2025-40047), [RHSA-2025:22802](https://access.redhat.com/errata/RHSA-2025:22802), [CVE-2025-39966](https://nvd.nist.gov/vuln/detail/cve-2025-39966), [RHSA-2025:23789](https://access.redhat.com/errata/RHSA-2025:23789), [CVE-2025-39843](https://nvd.nist.gov/vuln/detail/cve-2025-39843), [CVE-2025-39925](https://nvd.nist.gov/vuln/detail/cve-2025-39925), [RHSA-2026:11313](https://access.redhat.com/errata/RHSA-2026:11313), [CVE-2026-23097](https://nvd.nist.gov/vuln/detail/cve-2026-23097), [CVE-2026-31402](https://nvd.nist.gov/vuln/detail/cve-2026-31402), [RHSA-2026:1194](https://access.redhat.com/errata/RHSA-2026:1194), [CVE-2023-53034](https://nvd.nist.gov/vuln/detail/cve-2023-53034), [CVE-2025-37761](https://nvd.nist.gov/vuln/detail/cve-2025-37761), [CVE-2025-37789](https://nvd.nist.gov/vuln/detail/cve-2025-37789), [CVE-2025-37819](https://nvd.nist.gov/vuln/detail/cve-2025-37819), [CVE-2025-37869](https://nvd.nist.gov/vuln/detail/cve-2025-37869), [CVE-2025-38289](https://nvd.nist.gov/vuln/detail/cve-2025-38289), [CVE-2025-40141](https://nvd.nist.gov/vuln/detail/cve-2025-40141), [CVE-2025-40251](https://nvd.nist.gov/vuln/detail/cve-2025-40251), [CVE-2025-40258](https://nvd.nist.gov/vuln/detail/cve-2025-40258), [CVE-2025-40277](https://nvd.nist.gov/vuln/detail/cve-2025-40277), [CVE-2025-40318](https://nvd.nist.gov/vuln/detail/cve-2025-40318), [RHSA-2026:2352](https://access.redhat.com/errata/RHSA-2026:2352), [CVE-2024-54456](https://nvd.nist.gov/vuln/detail/cve-2024-54456), [CVE-2025-21647](https://nvd.nist.gov/vuln/detail/cve-2025-21647), [CVE-2025-21786](https://nvd.nist.gov/vuln/detail/cve-2025-21786), [CVE-2025-21791](https://nvd.nist.gov/vuln/detail/cve-2025-21791), [CVE-2025-38022](https://nvd.nist.gov/vuln/detail/cve-2025-38022), [CVE-2025-38051](https://nvd.nist.gov/vuln/detail/cve-2025-38051), [CVE-2025-38568](https://nvd.nist.gov/vuln/detail/cve-2025-38568), [CVE-2025-40294](https://nvd.nist.gov/vuln/detail/cve-2025-40294), [CVE-2025-40322](https://nvd.nist.gov/vuln/detail/cve-2025-40322), [CVE-2025-68349](https://nvd.nist.gov/vuln/detail/cve-2025-68349), [RHSA-2026:2759](https://access.redhat.com/errata/RHSA-2026:2759), [CVE-2025-37882](https://nvd.nist.gov/vuln/detail/cve-2025-37882), [CVE-2025-38349](https://nvd.nist.gov/vuln/detail/cve-2025-38349), [CVE-2025-38730](https://nvd.nist.gov/vuln/detail/cve-2025-38730), [CVE-2025-39760](https://nvd.nist.gov/vuln/detail/cve-2025-39760), [CVE-2025-39933](https://nvd.nist.gov/vuln/detail/cve-2025-39933), [CVE-2025-40269](https://nvd.nist.gov/vuln/detail/cve-2025-40269), [CVE-2025-40271](https://nvd.nist.gov/vuln/detail/cve-2025-40271), [CVE-2025-40304](https://nvd.nist.gov/vuln/detail/cve-2025-40304), [RHSA-2026:3088](https://access.redhat.com/errata/RHSA-2026:3088), [CVE-2025-37861](https://nvd.nist.gov/vuln/detail/cve-2025-37861), [CVE-2025-38106](https://nvd.nist.gov/vuln/detail/cve-2025-38106), [CVE-2025-38415](https://nvd.nist.gov/vuln/detail/cve-2025-38415), [RHSA-2026:3520](https://access.redhat.com/errata/RHSA-2026:3520), [CVE-2025-38154](https://nvd.nist.gov/vuln/detail/cve-2025-38154), [RHSA-2026:4011](https://access.redhat.com/errata/RHSA-2026:4011), [CVE-2024-47727](https://nvd.nist.gov/vuln/detail/cve-2024-47727), [CVE-2024-56603](https://nvd.nist.gov/vuln/detail/cve-2024-56603), [CVE-2025-22056](https://nvd.nist.gov/vuln/detail/cve-2025-22056), [CVE-2025-38024](https://nvd.nist.gov/vuln/detail/cve-2025-38024), [CVE-2025-38129](https://nvd.nist.gov/vuln/detail/cve-2025-38129), [CVE-2025-38141](https://nvd.nist.gov/vuln/detail/cve-2025-38141), [CVE-2025-38703](https://nvd.nist.gov/vuln/detail/cve-2025-38703), [RHSA-2026:4745](https://access.redhat.com/errata/RHSA-2026:4745), [CVE-2024-53229](https://nvd.nist.gov/vuln/detail/cve-2024-53229), [CVE-2025-38206](https://nvd.nist.gov/vuln/detail/cve-2025-38206), [CVE-2025-40240](https://nvd.nist.gov/vuln/detail/cve-2025-40240), [CVE-2025-68811](https://nvd.nist.gov/vuln/detail/cve-2025-68811), [CVE-2025-71085](https://nvd.nist.gov/vuln/detail/cve-2025-71085), [RHSA-2026:5197](https://access.redhat.com/errata/RHSA-2026:5197), [CVE-2025-38248](https://nvd.nist.gov/vuln/detail/cve-2025-38248), [CVE-2026-23001](https://nvd.nist.gov/vuln/detail/cve-2026-23001), [RHSA-2026:6164](https://access.redhat.com/errata/RHSA-2026:6164), [CVE-2024-56645](https://nvd.nist.gov/vuln/detail/cve-2024-56645), [CVE-2025-40096](https://nvd.nist.gov/vuln/detail/cve-2025-40096), [CVE-2025-68800](https://nvd.nist.gov/vuln/detail/cve-2025-68800), [CVE-2026-23209](https://nvd.nist.gov/vuln/detail/cve-2026-23209), [RHSA-2026:6940](https://access.redhat.com/errata/RHSA-2026:6940), [CVE-2025-38180](https://nvd.nist.gov/vuln/detail/cve-2025-38180), [CVE-2026-23231](https://nvd.nist.gov/vuln/detail/cve-2026-23231), [RHSA-2026:9112](https://access.redhat.com/errata/RHSA-2026:9112), [CVE-2026-23066](https://nvd.nist.gov/vuln/detail/cve-2026-23066), [CVE-2026-23111](https://nvd.nist.gov/vuln/detail/cve-2026-23111), [CVE-2026-23144](https://nvd.nist.gov/vuln/detail/cve-2026-23144), [CVE-2026-23171](https://nvd.nist.gov/vuln/detail/cve-2026-23171), [CVE-2026-23193](https://nvd.nist.gov/vuln/detail/cve-2026-23193), [CVE-2026-23204](https://nvd.nist.gov/vuln/detail/cve-2026-23204), [RHSA-2026:17524](https://access.redhat.com/errata/RHSA-2026:17524), and [CVE-2026-33636](https://nvd.nist.gov/vuln/detail/cve-2026-33636).


RHEL 9 (Classic) [5.14.0-570.112.1.el9_6](/docs/openshift?topic=openshift-openshift-relnotes#openshift-may2126)
:   Resolves the following CVEs: [RHSA-2026:2229](https://access.redhat.com/errata/RHSA-2026:2229), [CVE-2025-6176](https://nvd.nist.gov/vuln/detail/cve-2025-6176), [RHSA-2025:21773](https://access.redhat.com/errata/RHSA-2025:21773), [CVE-2025-59375](https://nvd.nist.gov/vuln/detail/cve-2025-59375), [RHSA-2026:1229](https://access.redhat.com/errata/RHSA-2026:1229), [CVE-2025-68973](https://nvd.nist.gov/vuln/detail/cve-2025-68973), [RHSA-2026:18042](https://access.redhat.com/errata/RHSA-2026:18042), [CVE-2026-39979](https://nvd.nist.gov/vuln/detail/cve-2026-39979), [CVE-2026-40164](https://nvd.nist.gov/vuln/detail/cve-2026-40164), [RHSA-2025:22392](https://access.redhat.com/errata/RHSA-2025:22392), [CVE-2025-38724](https://nvd.nist.gov/vuln/detail/cve-2025-38724), [CVE-2025-39864](https://nvd.nist.gov/vuln/detail/cve-2025-39864), [CVE-2025-39881](https://nvd.nist.gov/vuln/detail/cve-2025-39881), [CVE-2025-39883](https://nvd.nist.gov/vuln/detail/cve-2025-39883), [CVE-2025-39918](https://nvd.nist.gov/vuln/detail/cve-2025-39918), [CVE-2025-39955](https://nvd.nist.gov/vuln/detail/cve-2025-39955), [CVE-2025-40186](https://nvd.nist.gov/vuln/detail/cve-2025-40186), [RHSA-2026:0457](https://access.redhat.com/errata/RHSA-2026:0457), [CVE-2025-23142](https://nvd.nist.gov/vuln/detail/cve-2025-23142), [CVE-2025-39806](https://nvd.nist.gov/vuln/detail/cve-2025-39806), [CVE-2025-39981](https://nvd.nist.gov/vuln/detail/cve-2025-39981), [CVE-2025-39983](https://nvd.nist.gov/vuln/detail/cve-2025-39983), [CVE-2025-40176](https://nvd.nist.gov/vuln/detail/cve-2025-40176), [CVE-2025-68287](https://nvd.nist.gov/vuln/detail/cve-2025-68287), [RHSA-2026:0804](https://access.redhat.com/errata/RHSA-2026:0804), [CVE-2025-21795](https://nvd.nist.gov/vuln/detail/cve-2025-21795), [CVE-2025-37849](https://nvd.nist.gov/vuln/detail/cve-2025-37849), [CVE-2025-37891](https://nvd.nist.gov/vuln/detail/cve-2025-37891), [CVE-2025-39697](https://nvd.nist.gov/vuln/detail/cve-2025-39697), [CVE-2025-40154](https://nvd.nist.gov/vuln/detail/cve-2025-40154), [CVE-2025-68285](https://nvd.nist.gov/vuln/detail/cve-2025-68285), [RHSA-2026:14339](https://access.redhat.com/errata/RHSA-2026:14339), [CVE-2024-53216](https://nvd.nist.gov/vuln/detail/cve-2024-53216), [CVE-2025-68741](https://nvd.nist.gov/vuln/detail/cve-2025-68741), [CVE-2026-23243](https://nvd.nist.gov/vuln/detail/cve-2026-23243), [CVE-2026-23401](https://nvd.nist.gov/vuln/detail/cve-2026-23401), [CVE-2026-31431](https://nvd.nist.gov/vuln/detail/cve-2026-31431), [CVE-2026-31532](https://nvd.nist.gov/vuln/detail/cve-2026-31532), [CVE-2026-43077](https://nvd.nist.gov/vuln/detail/cve-2026-43077), [RHSA-2026:16312](https://access.redhat.com/errata/RHSA-2026:16312), [CVE-2026-43284](https://nvd.nist.gov/vuln/detail/cve-2026-43284), [RHSA-2026:1703](https://access.redhat.com/errata/RHSA-2026:1703), [CVE-2025-21863](https://nvd.nist.gov/vuln/detail/cve-2025-21863), [CVE-2025-40248](https://nvd.nist.gov/vuln/detail/cve-2025-40248), [CVE-2025-68301](https://nvd.nist.gov/vuln/detail/cve-2025-68301), [RHSA-2026:7105](https://access.redhat.com/errata/RHSA-2026:7105), [CVE-2026-4111](https://nvd.nist.gov/vuln/detail/cve-2026-4111), [RHSA-2026:8866](https://access.redhat.com/errata/RHSA-2026:8866), [CVE-2026-4424](https://nvd.nist.gov/vuln/detail/cve-2026-4424), [CVE-2026-5121](https://nvd.nist.gov/vuln/detail/cve-2026-5121), [RHSA-2026:19458](https://access.redhat.com/errata/RHSA-2026:19458), [CVE-2026-4878](https://nvd.nist.gov/vuln/detail/cve-2026-4878), [RHSA-2026:0210](https://access.redhat.com/errata/RHSA-2026:0210), [CVE-2025-64720](https://nvd.nist.gov/vuln/detail/cve-2025-64720), [CVE-2025-65018](https://nvd.nist.gov/vuln/detail/cve-2025-65018), [CVE-2025-66293](https://nvd.nist.gov/vuln/detail/cve-2025-66293), [RHSA-2026:3576](https://access.redhat.com/errata/RHSA-2026:3576), [CVE-2026-22695](https://nvd.nist.gov/vuln/detail/cve-2026-22695), [CVE-2026-22801](https://nvd.nist.gov/vuln/detail/cve-2026-22801), [CVE-2026-25646](https://nvd.nist.gov/vuln/detail/cve-2026-25646), [RHSA-2026:8548](https://access.redhat.com/errata/RHSA-2026:8548), [CVE-2026-27135](https://nvd.nist.gov/vuln/detail/cve-2026-27135), [RHSA-2026:16059](https://access.redhat.com/errata/RHSA-2026:16059), [CVE-2026-35385](https://nvd.nist.gov/vuln/detail/cve-2026-35385), [CVE-2026-35386](https://nvd.nist.gov/vuln/detail/cve-2026-35386), [CVE-2026-35387](https://nvd.nist.gov/vuln/detail/cve-2026-35387), [CVE-2026-35388](https://nvd.nist.gov/vuln/detail/cve-2026-35388), [CVE-2026-35414](https://nvd.nist.gov/vuln/detail/cve-2026-35414), [RHSA-2026:9415](https://access.redhat.com/errata/RHSA-2026:9415), [CVE-2026-3497](https://nvd.nist.gov/vuln/detail/cve-2026-3497), [RHSA-2026:1503](https://access.redhat.com/errata/RHSA-2026:1503), [CVE-2025-15467](https://nvd.nist.gov/vuln/detail/cve-2025-15467), [CVE-2025-69419](https://nvd.nist.gov/vuln/detail/cve-2025-69419), [RHSA-2026:1729](https://access.redhat.com/errata/RHSA-2026:1729), [CVE-2025-66418](https://nvd.nist.gov/vuln/detail/cve-2025-66418), [CVE-2025-66471](https://nvd.nist.gov/vuln/detail/cve-2025-66471), [CVE-2026-21441](https://nvd.nist.gov/vuln/detail/cve-2026-21441), [RHSA-2026:9354](https://access.redhat.com/errata/RHSA-2026:9354), [CVE-2026-4519](https://nvd.nist.gov/vuln/detail/cve-2026-4519), [RHSA-2025:21067](https://access.redhat.com/errata/RHSA-2025:21067), [CVE-2025-11561](https://nvd.nist.gov/vuln/detail/cve-2025-11561), [RHSA-2026:13889](https://access.redhat.com/errata/RHSA-2026:13889), [CVE-2026-35535](https://nvd.nist.gov/vuln/detail/cve-2026-35535), [RHSA-2026:6539](https://access.redhat.com/errata/RHSA-2026:6539), [CVE-2026-25749](https://nvd.nist.gov/vuln/detail/cve-2026-25749), [CVE-2026-28417](https://nvd.nist.gov/vuln/detail/cve-2026-28417), [CVE-2026-28421](https://nvd.nist.gov/vuln/detail/cve-2026-28421), [CVE-2026-33412](https://nvd.nist.gov/vuln/detail/cve-2026-33412), [RHSA-2025:23400](https://access.redhat.com/errata/RHSA-2025:23400), [CVE-2025-11083](https://nvd.nist.gov/vuln/detail/cve-2025-11083), [RHSA-2025:23043](https://access.redhat.com/errata/RHSA-2025:23043), [CVE-2025-9086](https://nvd.nist.gov/vuln/detail/cve-2025-9086), [RHSA-2026:1465](https://access.redhat.com/errata/RHSA-2026:1465), [CVE-2025-13601](https://nvd.nist.gov/vuln/detail/cve-2025-13601), [RHSA-2026:19457](https://access.redhat.com/errata/RHSA-2026:19457), [CVE-2025-14087](https://nvd.nist.gov/vuln/detail/cve-2025-14087), [CVE-2025-14512](https://nvd.nist.gov/vuln/detail/cve-2025-14512), [RHSA-2026:6630](https://access.redhat.com/errata/RHSA-2026:6630), [CVE-2025-14831](https://nvd.nist.gov/vuln/detail/cve-2025-14831), [RHSA-2026:4823](https://access.redhat.com/errata/RHSA-2026:4823), [CVE-2025-61662](https://nvd.nist.gov/vuln/detail/cve-2025-61662), [RHSA-2025:21563](https://access.redhat.com/errata/RHSA-2025:21563), [CVE-2024-56690](https://nvd.nist.gov/vuln/detail/cve-2024-56690), [RHSA-2025:21933](https://access.redhat.com/errata/RHSA-2025:21933), [CVE-2025-39898](https://nvd.nist.gov/vuln/detail/cve-2025-39898), [CVE-2025-39971](https://nvd.nist.gov/vuln/detail/cve-2025-39971), [CVE-2025-39973](https://nvd.nist.gov/vuln/detail/cve-2025-39973), [CVE-2025-40047](https://nvd.nist.gov/vuln/detail/cve-2025-40047), [RHSA-2025:22802](https://access.redhat.com/errata/RHSA-2025:22802), [CVE-2025-39966](https://nvd.nist.gov/vuln/detail/cve-2025-39966), [RHSA-2025:23789](https://access.redhat.com/errata/RHSA-2025:23789), [CVE-2025-39843](https://nvd.nist.gov/vuln/detail/cve-2025-39843), [CVE-2025-39925](https://nvd.nist.gov/vuln/detail/cve-2025-39925), [RHSA-2026:11313](https://access.redhat.com/errata/RHSA-2026:11313), [CVE-2026-23097](https://nvd.nist.gov/vuln/detail/cve-2026-23097), [CVE-2026-31402](https://nvd.nist.gov/vuln/detail/cve-2026-31402), [RHSA-2026:1194](https://access.redhat.com/errata/RHSA-2026:1194), [CVE-2023-53034](https://nvd.nist.gov/vuln/detail/cve-2023-53034), [CVE-2025-37761](https://nvd.nist.gov/vuln/detail/cve-2025-37761), [CVE-2025-37789](https://nvd.nist.gov/vuln/detail/cve-2025-37789), [CVE-2025-37819](https://nvd.nist.gov/vuln/detail/cve-2025-37819), [CVE-2025-37869](https://nvd.nist.gov/vuln/detail/cve-2025-37869), [CVE-2025-38289](https://nvd.nist.gov/vuln/detail/cve-2025-38289), [CVE-2025-40141](https://nvd.nist.gov/vuln/detail/cve-2025-40141), [CVE-2025-40251](https://nvd.nist.gov/vuln/detail/cve-2025-40251), [CVE-2025-40258](https://nvd.nist.gov/vuln/detail/cve-2025-40258), [CVE-2025-40277](https://nvd.nist.gov/vuln/detail/cve-2025-40277), [CVE-2025-40318](https://nvd.nist.gov/vuln/detail/cve-2025-40318), [RHSA-2026:2352](https://access.redhat.com/errata/RHSA-2026:2352), [CVE-2024-54456](https://nvd.nist.gov/vuln/detail/cve-2024-54456), [CVE-2025-21647](https://nvd.nist.gov/vuln/detail/cve-2025-21647), [CVE-2025-21786](https://nvd.nist.gov/vuln/detail/cve-2025-21786), [CVE-2025-21791](https://nvd.nist.gov/vuln/detail/cve-2025-21791), [CVE-2025-38022](https://nvd.nist.gov/vuln/detail/cve-2025-38022), [CVE-2025-38051](https://nvd.nist.gov/vuln/detail/cve-2025-38051), [CVE-2025-38568](https://nvd.nist.gov/vuln/detail/cve-2025-38568), [CVE-2025-40294](https://nvd.nist.gov/vuln/detail/cve-2025-40294), [CVE-2025-40322](https://nvd.nist.gov/vuln/detail/cve-2025-40322), [CVE-2025-68349](https://nvd.nist.gov/vuln/detail/cve-2025-68349), [RHSA-2026:2759](https://access.redhat.com/errata/RHSA-2026:2759), [CVE-2025-37882](https://nvd.nist.gov/vuln/detail/cve-2025-37882), [CVE-2025-38349](https://nvd.nist.gov/vuln/detail/cve-2025-38349), [CVE-2025-38730](https://nvd.nist.gov/vuln/detail/cve-2025-38730), [CVE-2025-39760](https://nvd.nist.gov/vuln/detail/cve-2025-39760), [CVE-2025-39933](https://nvd.nist.gov/vuln/detail/cve-2025-39933), [CVE-2025-40269](https://nvd.nist.gov/vuln/detail/cve-2025-40269), [CVE-2025-40271](https://nvd.nist.gov/vuln/detail/cve-2025-40271), [CVE-2025-40304](https://nvd.nist.gov/vuln/detail/cve-2025-40304), [RHSA-2026:3088](https://access.redhat.com/errata/RHSA-2026:3088), [CVE-2025-37861](https://nvd.nist.gov/vuln/detail/cve-2025-37861), [CVE-2025-38106](https://nvd.nist.gov/vuln/detail/cve-2025-38106), [CVE-2025-38415](https://nvd.nist.gov/vuln/detail/cve-2025-38415), [RHSA-2026:3520](https://access.redhat.com/errata/RHSA-2026:3520), [CVE-2025-38154](https://nvd.nist.gov/vuln/detail/cve-2025-38154), [RHSA-2026:4011](https://access.redhat.com/errata/RHSA-2026:4011), [CVE-2024-47727](https://nvd.nist.gov/vuln/detail/cve-2024-47727), [CVE-2024-56603](https://nvd.nist.gov/vuln/detail/cve-2024-56603), [CVE-2025-22056](https://nvd.nist.gov/vuln/detail/cve-2025-22056), [CVE-2025-38024](https://nvd.nist.gov/vuln/detail/cve-2025-38024), [CVE-2025-38129](https://nvd.nist.gov/vuln/detail/cve-2025-38129), [CVE-2025-38141](https://nvd.nist.gov/vuln/detail/cve-2025-38141), [CVE-2025-38703](https://nvd.nist.gov/vuln/detail/cve-2025-38703), [RHSA-2026:4745](https://access.redhat.com/errata/RHSA-2026:4745), [CVE-2024-53229](https://nvd.nist.gov/vuln/detail/cve-2024-53229), [CVE-2025-38206](https://nvd.nist.gov/vuln/detail/cve-2025-38206), [CVE-2025-40240](https://nvd.nist.gov/vuln/detail/cve-2025-40240), [CVE-2025-68811](https://nvd.nist.gov/vuln/detail/cve-2025-68811), [CVE-2025-71085](https://nvd.nist.gov/vuln/detail/cve-2025-71085), [RHSA-2026:5197](https://access.redhat.com/errata/RHSA-2026:5197), [CVE-2025-38248](https://nvd.nist.gov/vuln/detail/cve-2025-38248), [CVE-2026-23001](https://nvd.nist.gov/vuln/detail/cve-2026-23001), [RHSA-2026:6164](https://access.redhat.com/errata/RHSA-2026:6164), [CVE-2024-56645](https://nvd.nist.gov/vuln/detail/cve-2024-56645), [CVE-2025-40096](https://nvd.nist.gov/vuln/detail/cve-2025-40096), [CVE-2025-68800](https://nvd.nist.gov/vuln/detail/cve-2025-68800), [CVE-2026-23209](https://nvd.nist.gov/vuln/detail/cve-2026-23209), [RHSA-2026:6940](https://access.redhat.com/errata/RHSA-2026:6940), [CVE-2025-38180](https://nvd.nist.gov/vuln/detail/cve-2025-38180), [CVE-2026-23231](https://nvd.nist.gov/vuln/detail/cve-2026-23231), [RHSA-2026:9112](https://access.redhat.com/errata/RHSA-2026:9112), [CVE-2026-23066](https://nvd.nist.gov/vuln/detail/cve-2026-23066), [CVE-2026-23111](https://nvd.nist.gov/vuln/detail/cve-2026-23111), [CVE-2026-23144](https://nvd.nist.gov/vuln/detail/cve-2026-23144), [CVE-2026-23171](https://nvd.nist.gov/vuln/detail/cve-2026-23171), [CVE-2026-23193](https://nvd.nist.gov/vuln/detail/cve-2026-23193), [CVE-2026-23204](https://nvd.nist.gov/vuln/detail/cve-2026-23204), [RHSA-2026:17524](https://access.redhat.com/errata/RHSA-2026:17524), [CVE-2026-33636](https://nvd.nist.gov/vuln/detail/cve-2026-33636), [RHSA-2026:0428](https://access.redhat.com/errata/RHSA-2026:0428), [CVE-2025-5987](https://nvd.nist.gov/vuln/detail/cve-2025-5987), [RHSA-2025:22377](https://access.redhat.com/errata/RHSA-2025:22377), [CVE-2025-9714](https://nvd.nist.gov/vuln/detail/cve-2025-9714), [RHSA-2026:3941](https://access.redhat.com/errata/RHSA-2026:3941), [CVE-2025-12801](https://nvd.nist.gov/vuln/detail/cve-2025-12801), [RHSA-2026:0693](https://access.redhat.com/errata/RHSA-2026:0693), [CVE-2025-61984](https://nvd.nist.gov/vuln/detail/cve-2025-61984), [CVE-2025-61985](https://nvd.nist.gov/vuln/detail/cve-2025-61985), [RHSA-2025:21174](https://access.redhat.com/errata/RHSA-2025:21174), [CVE-2025-9230](https://nvd.nist.gov/vuln/detail/cve-2025-9230), [RHSA-2026:2275](https://access.redhat.com/errata/RHSA-2026:2275), [CVE-2025-12084](https://nvd.nist.gov/vuln/detail/cve-2025-12084), [RHSA-2026:5218](https://access.redhat.com/errata/RHSA-2026:5218), [CVE-2025-15366](https://nvd.nist.gov/vuln/detail/cve-2025-15366), [CVE-2025-15367](https://nvd.nist.gov/vuln/detail/cve-2025-15367), [CVE-2026-1299](https://nvd.nist.gov/vuln/detail/cve-2026-1299), [RHSA-2026:0435](https://access.redhat.com/errata/RHSA-2026:0435), and [CVE-2025-45582](https://nvd.nist.gov/vuln/detail/cve-2025-45582).


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 8 (VPC) 4.18.0-553.123.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:16252](https://access.redhat.com/errata/RHSA-2026:16252), [CVE-2026-39979](https://nvd.nist.gov/vuln/detail/cve-2026-39979), [CVE-2026-40164](https://nvd.nist.gov/vuln/detail/cve-2026-40164), [RHSA-2026:13577](https://access.redhat.com/errata/RHSA-2026:13577), [CVE-2024-41073](https://nvd.nist.gov/vuln/detail/cve-2024-41073), [CVE-2025-40252](https://nvd.nist.gov/vuln/detail/cve-2025-40252), [CVE-2025-68724](https://nvd.nist.gov/vuln/detail/cve-2025-68724), [CVE-2026-23401](https://nvd.nist.gov/vuln/detail/cve-2026-23401), [CVE-2026-31402](https://nvd.nist.gov/vuln/detail/cve-2026-31402), [CVE-2026-31431](https://nvd.nist.gov/vuln/detail/cve-2026-31431), [CVE-2026-43077](https://nvd.nist.gov/vuln/detail/cve-2026-43077), [RHSA-2026:16799](https://access.redhat.com/errata/RHSA-2026:16799), [CVE-2026-40355](https://nvd.nist.gov/vuln/detail/cve-2026-40355), [CVE-2026-40356](https://nvd.nist.gov/vuln/detail/cve-2026-40356), [RHSA-2026:13285](https://access.redhat.com/errata/RHSA-2026:13285), [CVE-2026-4878](https://nvd.nist.gov/vuln/detail/cve-2026-4878), [RHSA-2026:13383](https://access.redhat.com/errata/RHSA-2026:13383), [CVE-2026-35385](https://nvd.nist.gov/vuln/detail/cve-2026-35385), [CVE-2026-35386](https://nvd.nist.gov/vuln/detail/cve-2026-35386), [CVE-2026-35387](https://nvd.nist.gov/vuln/detail/cve-2026-35387), [CVE-2026-35388](https://nvd.nist.gov/vuln/detail/cve-2026-35388), [CVE-2026-35414](https://nvd.nist.gov/vuln/detail/cve-2026-35414), [RHSA-2026:15980](https://access.redhat.com/errata/RHSA-2026:15980), [CVE-2026-32280](https://nvd.nist.gov/vuln/detail/cve-2026-32280), [CVE-2026-32282](https://nvd.nist.gov/vuln/detail/cve-2026-32282), [CVE-2026-32283](https://nvd.nist.gov/vuln/detail/cve-2026-32283), [RHSA-2026:17481](https://access.redhat.com/errata/RHSA-2026:17481), [CVE-2026-41035](https://nvd.nist.gov/vuln/detail/cve-2026-41035), [RHSA-2026:15953](https://access.redhat.com/errata/RHSA-2026:15953), [CVE-2025-14087](https://nvd.nist.gov/vuln/detail/cve-2025-14087), [CVE-2025-14512](https://nvd.nist.gov/vuln/detail/cve-2025-14512), [RHSA-2026:14087](https://access.redhat.com/errata/RHSA-2026:14087), and [CVE-2026-5119](https://nvd.nist.gov/vuln/detail/cve-2026-5119).


RHEL 8 (Classic) 4.18.0-553.123.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:16252](https://access.redhat.com/errata/RHSA-2026:16252), [CVE-2026-39979](https://nvd.nist.gov/vuln/detail/cve-2026-39979), [CVE-2026-40164](https://nvd.nist.gov/vuln/detail/cve-2026-40164), [RHSA-2026:13577](https://access.redhat.com/errata/RHSA-2026:13577), [CVE-2024-41073](https://nvd.nist.gov/vuln/detail/cve-2024-41073), [CVE-2025-40252](https://nvd.nist.gov/vuln/detail/cve-2025-40252), [CVE-2025-68724](https://nvd.nist.gov/vuln/detail/cve-2025-68724), [CVE-2026-23401](https://nvd.nist.gov/vuln/detail/cve-2026-23401), [CVE-2026-31402](https://nvd.nist.gov/vuln/detail/cve-2026-31402), [CVE-2026-31431](https://nvd.nist.gov/vuln/detail/cve-2026-31431), [CVE-2026-43077](https://nvd.nist.gov/vuln/detail/cve-2026-43077), [RHSA-2026:16799](https://access.redhat.com/errata/RHSA-2026:16799), [CVE-2026-40355](https://nvd.nist.gov/vuln/detail/cve-2026-40355), [CVE-2026-40356](https://nvd.nist.gov/vuln/detail/cve-2026-40356), [RHSA-2026:13285](https://access.redhat.com/errata/RHSA-2026:13285), [CVE-2026-4878](https://nvd.nist.gov/vuln/detail/cve-2026-4878), [RHSA-2026:13383](https://access.redhat.com/errata/RHSA-2026:13383), [CVE-2026-35385](https://nvd.nist.gov/vuln/detail/cve-2026-35385), [CVE-2026-35386](https://nvd.nist.gov/vuln/detail/cve-2026-35386), [CVE-2026-35387](https://nvd.nist.gov/vuln/detail/cve-2026-35387), [CVE-2026-35388](https://nvd.nist.gov/vuln/detail/cve-2026-35388), [CVE-2026-35414](https://nvd.nist.gov/vuln/detail/cve-2026-35414), [RHSA-2026:15980](https://access.redhat.com/errata/RHSA-2026:15980), [CVE-2026-32280](https://nvd.nist.gov/vuln/detail/cve-2026-32280), [CVE-2026-32282](https://nvd.nist.gov/vuln/detail/cve-2026-32282), [CVE-2026-32283](https://nvd.nist.gov/vuln/detail/cve-2026-32283), [RHSA-2026:15953](https://access.redhat.com/errata/RHSA-2026:15953), [CVE-2025-14087](https://nvd.nist.gov/vuln/detail/cve-2025-14087), and [CVE-2025-14512](https://nvd.nist.gov/vuln/detail/cve-2025-14512).


Red Hat OpenShift 4.17.53
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-53_release-notes){: external}.


Red Hat CoreOS 4.17.53
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-53_release-notes){: external}.


HAProxy 6ba93946d8bd08ba581321189c719ab548cadf01
:   Resolves the following CVEs: [CVE-2025-9714](https://nvd.nist.gov/vuln/detail/cve-2025-9714), [CVE-2026-4424](https://nvd.nist.gov/vuln/detail/cve-2026-4424), [CVE-2026-40356](https://nvd.nist.gov/vuln/detail/cve-2026-40356), [CVE-2025-14512](https://nvd.nist.gov/vuln/detail/cve-2025-14512), [CVE-2026-4878](https://nvd.nist.gov/vuln/detail/cve-2026-4878), [CVE-2026-40355](https://nvd.nist.gov/vuln/detail/cve-2026-40355), [CVE-2026-5121](https://nvd.nist.gov/vuln/detail/cve-2026-5121), and [CVE-2025-14087](https://nvd.nist.gov/vuln/detail/cve-2025-14087).


## 04 May 2026, Worker node fix pack 4.17.52_1583_openshift
{: #cl-boms-41752_1583_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.52_1583_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:9415](https://access.redhat.com/errata/RHSA-2026:9415), [CVE-2026-3497](https://nvd.nist.gov/vuln/detail/cve-2026-3497), [RHSA-2026:11313](https://access.redhat.com/errata/RHSA-2026:11313), [CVE-2026-23097](https://nvd.nist.gov/vuln/detail/cve-2026-23097), [CVE-2026-31402](https://nvd.nist.gov/vuln/detail/cve-2026-31402), [RHSA-2026:11329](https://access.redhat.com/errata/RHSA-2026:11329), [CVE-2025-43213](https://nvd.nist.gov/vuln/detail/cve-2025-43213), [CVE-2025-43214](https://nvd.nist.gov/vuln/detail/cve-2025-43214), [CVE-2025-43457](https://nvd.nist.gov/vuln/detail/cve-2025-43457), [CVE-2025-43511](https://nvd.nist.gov/vuln/detail/cve-2025-43511), [CVE-2025-46299](https://nvd.nist.gov/vuln/detail/cve-2025-46299), [CVE-2026-20608](https://nvd.nist.gov/vuln/detail/cve-2026-20608), [CVE-2026-20635](https://nvd.nist.gov/vuln/detail/cve-2026-20635), [CVE-2026-20636](https://nvd.nist.gov/vuln/detail/cve-2026-20636), [CVE-2026-20643](https://nvd.nist.gov/vuln/detail/cve-2026-20643), [CVE-2026-20644](https://nvd.nist.gov/vuln/detail/cve-2026-20644), [CVE-2026-20652](https://nvd.nist.gov/vuln/detail/cve-2026-20652), [CVE-2026-20664](https://nvd.nist.gov/vuln/detail/cve-2026-20664), [CVE-2026-20665](https://nvd.nist.gov/vuln/detail/cve-2026-20665), [CVE-2026-20676](https://nvd.nist.gov/vuln/detail/cve-2026-20676), [CVE-2026-20691](https://nvd.nist.gov/vuln/detail/cve-2026-20691), [CVE-2026-28857](https://nvd.nist.gov/vuln/detail/cve-2026-28857), [CVE-2026-28859](https://nvd.nist.gov/vuln/detail/cve-2026-28859), [CVE-2026-28871](https://nvd.nist.gov/vuln/detail/cve-2026-28871), and mitigates [CVE-2026-31431](https://nvd.nist.gov/vuln/detail/cve-2026-31431).


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:9415](https://access.redhat.com/errata/RHSA-2026:9415), [CVE-2026-3497](https://nvd.nist.gov/vuln/detail/cve-2026-3497), [RHSA-2026:11313](https://access.redhat.com/errata/RHSA-2026:11313), [CVE-2026-23097](https://nvd.nist.gov/vuln/detail/cve-2026-23097), [CVE-2026-31402](https://nvd.nist.gov/vuln/detail/cve-2026-31402), [RHSA-2026:11329](https://access.redhat.com/errata/RHSA-2026:11329), [CVE-2025-43213](https://nvd.nist.gov/vuln/detail/cve-2025-43213), [CVE-2025-43214](https://nvd.nist.gov/vuln/detail/cve-2025-43214), [CVE-2025-43457](https://nvd.nist.gov/vuln/detail/cve-2025-43457), [CVE-2025-43511](https://nvd.nist.gov/vuln/detail/cve-2025-43511), [CVE-2025-46299](https://nvd.nist.gov/vuln/detail/cve-2025-46299), [CVE-2026-20608](https://nvd.nist.gov/vuln/detail/cve-2026-20608), [CVE-2026-20635](https://nvd.nist.gov/vuln/detail/cve-2026-20635), [CVE-2026-20636](https://nvd.nist.gov/vuln/detail/cve-2026-20636), [CVE-2026-20643](https://nvd.nist.gov/vuln/detail/cve-2026-20643), [CVE-2026-20644](https://nvd.nist.gov/vuln/detail/cve-2026-20644), [CVE-2026-20652](https://nvd.nist.gov/vuln/detail/cve-2026-20652), [CVE-2026-20664](https://nvd.nist.gov/vuln/detail/cve-2026-20664), [CVE-2026-20665](https://nvd.nist.gov/vuln/detail/cve-2026-20665), [CVE-2026-20676](https://nvd.nist.gov/vuln/detail/cve-2026-20676), [CVE-2026-20691](https://nvd.nist.gov/vuln/detail/cve-2026-20691), [CVE-2026-28857](https://nvd.nist.gov/vuln/detail/cve-2026-28857), [CVE-2026-28859](https://nvd.nist.gov/vuln/detail/cve-2026-28859), [CVE-2026-28871](https://nvd.nist.gov/vuln/detail/cve-2026-28871), and mitigates [CVE-2026-31431](https://nvd.nist.gov/vuln/detail/cve-2026-31431).


RHEL 8 (VPC) 4.18.0-553.120.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:10741](https://access.redhat.com/errata/RHSA-2026:10741), [CVE-2026-5201](https://nvd.nist.gov/vuln/detail/cve-2026-5201), [RHSA-2026:9131](https://access.redhat.com/errata/RHSA-2026:9131), [CVE-2025-68741](https://nvd.nist.gov/vuln/detail/cve-2025-68741), [CVE-2026-23191](https://nvd.nist.gov/vuln/detail/cve-2026-23191), [RHSA-2026:8534](https://access.redhat.com/errata/RHSA-2026:8534), [CVE-2026-4424](https://nvd.nist.gov/vuln/detail/cve-2026-4424), [CVE-2026-5121](https://nvd.nist.gov/vuln/detail/cve-2026-5121), [RHSA-2026:11635](https://access.redhat.com/errata/RHSA-2026:11635), [CVE-2026-41651](https://nvd.nist.gov/vuln/detail/cve-2026-41651), [RHSA-2026:11077](https://access.redhat.com/errata/RHSA-2026:11077), [CVE-2026-4786](https://nvd.nist.gov/vuln/detail/cve-2026-4786), [CVE-2026-6100](https://nvd.nist.gov/vuln/detail/cve-2026-6100), [RHSA-2026:10107](https://access.redhat.com/errata/RHSA-2026:10107), [CVE-2026-33186](https://nvd.nist.gov/vuln/detail/cve-2026-33186), [RHSA-2026:11521](https://access.redhat.com/errata/RHSA-2026:11521), [CVE-2026-35535](https://nvd.nist.gov/vuln/detail/cve-2026-35535), [RHSA-2026:11509](https://access.redhat.com/errata/RHSA-2026:11509), [CVE-2026-34982](https://nvd.nist.gov/vuln/detail/cve-2026-34982), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:11349](https://access.redhat.com/errata/RHSA-2026:11349), [CVE-2025-9714](https://nvd.nist.gov/vuln/detail/cve-2025-9714), and mitigates [CVE-2026-31431](https://nvd.nist.gov/vuln/detail/cve-2026-31431).


RHEL 8 (Classic) 4.18.0-553.120.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:8352](https://access.redhat.com/errata/RHSA-2026:8352), [CVE-2026-1519](https://nvd.nist.gov/vuln/detail/cve-2026-1519), [RHSA-2026:9131](https://access.redhat.com/errata/RHSA-2026:9131), [CVE-2025-68741](https://nvd.nist.gov/vuln/detail/cve-2025-68741), [CVE-2026-23191](https://nvd.nist.gov/vuln/detail/cve-2026-23191), [RHSA-2026:8534](https://access.redhat.com/errata/RHSA-2026:8534), [CVE-2026-4424](https://nvd.nist.gov/vuln/detail/cve-2026-4424), [CVE-2026-5121](https://nvd.nist.gov/vuln/detail/cve-2026-5121), [RHSA-2026:7667](https://access.redhat.com/errata/RHSA-2026:7667), [CVE-2026-27135](https://nvd.nist.gov/vuln/detail/cve-2026-27135), [RHSA-2026:11077](https://access.redhat.com/errata/RHSA-2026:11077), [CVE-2026-4786](https://nvd.nist.gov/vuln/detail/cve-2026-4786), [CVE-2026-6100](https://nvd.nist.gov/vuln/detail/cve-2026-6100), [RHSA-2026:10107](https://access.redhat.com/errata/RHSA-2026:10107), [CVE-2026-33186](https://nvd.nist.gov/vuln/detail/cve-2026-33186), [RHSA-2026:7674](https://access.redhat.com/errata/RHSA-2026:7674), [CVE-2026-25679](https://access.redhat.com/security/cve/cve-2026-25679), [RHSA-2026:11521](https://access.redhat.com/errata/RHSA-2026:11521), [CVE-2026-35535](https://nvd.nist.gov/vuln/detail/cve-2026-35535), [RHSA-2026:11509](https://access.redhat.com/errata/RHSA-2026:11509), [CVE-2026-34982](https://nvd.nist.gov/vuln/detail/cve-2026-34982), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:11349](https://access.redhat.com/errata/RHSA-2026:11349), [CVE-2025-9714](https://nvd.nist.gov/vuln/detail/cve-2025-9714), and mitigates [CVE-2026-31431](https://nvd.nist.gov/vuln/detail/cve-2026-31431).


Red Hat OpenShift 4.17.52
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-52_release-notes){: external}.


Red Hat CoreOS 4.17.52
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-52_release-notes){: external}. Includes mitigation for [CVE-2026-31431](https://nvd.nist.gov/vuln/detail/cve-2026-31431){: external}.


HAProxy c7e825675cbd75e8433801c99f8aca3b207a5a46
:   Resolves the following CVEs: [CVE-2026-5121](https://nvd.nist.gov/vuln/detail/cve-2026-5121), [CVE-2025-9714](https://nvd.nist.gov/vuln/detail/cve-2025-9714), and [CVE-2026-4424](https://nvd.nist.gov/vuln/detail/cve-2026-4424).


## 27 April 2026, Master fix pack 4.17.52_1582_openshift
{: #cl-boms_master-41752_1582_openshift_M}

The following list shows the components that are in the master fix pack 4.17.52_1582_openshift. Master patch updates are applied automatically.
{: shortdesc}

etcd v3.5.29
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.29){: external}.


IBM Cloud Controller Manager v1.30.14-37
:   New version contains updates and security fixes.


Key Management Service provider 2.10.23
:   New version contains updates and security fixes.


Portieris admission controller v0.13.37
:   See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.13.37){: external}


Red Hat OpenShift on IBM Cloud 4.17.52
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-52_release-notes){: external}.


## 20 April 2026, Worker node fix pack 4.17.52_1580_openshift
{: #cl-boms-41752_1580_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.52_1580_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   


RHEL 8 (VPC) 4.18.0-553.117.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:8352](https://access.redhat.com/errata/RHSA-2026:8352), [CVE-2026-1519](https://nvd.nist.gov/vuln/detail/cve-2026-1519), [RHSA-2026:8534](https://access.redhat.com/errata/RHSA-2026:8534), [CVE-2026-4424](https://nvd.nist.gov/vuln/detail/cve-2026-4424), [CVE-2026-5121](https://nvd.nist.gov/vuln/detail/cve-2026-5121), [RHSA-2026:7667](https://access.redhat.com/errata/RHSA-2026:7667), [CVE-2026-27135](https://nvd.nist.gov/vuln/detail/cve-2026-27135), [RHSA-2026:6461](https://access.redhat.com/errata/RHSA-2026:6461), [CVE-2026-3497](https://nvd.nist.gov/vuln/detail/cve-2026-3497), [RHSA-2026:6473](https://access.redhat.com/errata/RHSA-2026:6473), [CVE-2026-4519](https://nvd.nist.gov/vuln/detail/cve-2026-4519), [RHSA-2026:7674](https://access.redhat.com/errata/RHSA-2026:7674), [CVE-2026-25679](https://access.redhat.com/security/cve/cve-2026-25679), [RHSA-2026:6915](https://access.redhat.com/errata/RHSA-2026:6915), [CVE-2026-28417](https://nvd.nist.gov/vuln/detail/cve-2026-28417), [CVE-2026-28421](https://nvd.nist.gov/vuln/detail/cve-2026-28421), [CVE-2026-33412](https://nvd.nist.gov/vuln/detail/cve-2026-33412), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:6037](https://access.redhat.com/errata/RHSA-2026:6037), [CVE-2025-38180](https://nvd.nist.gov/vuln/detail/cve-2025-38180), [CVE-2026-23204](https://nvd.nist.gov/vuln/detail/cve-2026-23204), [CVE-2026-23209](https://nvd.nist.gov/vuln/detail/cve-2026-23209), [RHSA-2026:6571](https://access.redhat.com/errata/RHSA-2026:6571), [CVE-2024-26984](https://nvd.nist.gov/vuln/detail/cve-2024-26984), [CVE-2025-71238](https://nvd.nist.gov/vuln/detail/cve-2025-71238), [CVE-2026-23193](https://nvd.nist.gov/vuln/detail/cve-2026-23193), [CVE-2026-23231](https://nvd.nist.gov/vuln/detail/cve-2026-23231), [RHSA-2026:6436](https://access.redhat.com/errata/RHSA-2026:6436), and [CVE-2025-10158](https://nvd.nist.gov/vuln/detail/cve-2025-10158).


RHEL 8 (Classic) 4.18.0-553.117.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:8352](https://access.redhat.com/errata/RHSA-2026:8352), [CVE-2026-1519](https://nvd.nist.gov/vuln/detail/cve-2026-1519), [RHSA-2026:4728](https://access.redhat.com/errata/RHSA-2026:4728), [CVE-2026-22695](https://nvd.nist.gov/vuln/detail/cve-2026-22695), [CVE-2026-22801](https://nvd.nist.gov/vuln/detail/cve-2026-22801), [CVE-2026-25646](https://nvd.nist.gov/vuln/detail/cve-2026-25646), [RHSA-2026:7667](https://access.redhat.com/errata/RHSA-2026:7667), [CVE-2026-27135](https://nvd.nist.gov/vuln/detail/cve-2026-27135), [RHSA-2026:6461](https://access.redhat.com/errata/RHSA-2026:6461), [CVE-2026-3497](https://nvd.nist.gov/vuln/detail/cve-2026-3497), [RHSA-2026:6473](https://access.redhat.com/errata/RHSA-2026:6473), [CVE-2026-4519](https://nvd.nist.gov/vuln/detail/cve-2026-4519), [RHSA-2026:4952](https://access.redhat.com/errata/RHSA-2026:4952), [CVE-2025-61726](https://access.redhat.com/security/cve/cve-2025-61726), [CVE-2025-61729](https://nvd.nist.gov/vuln/detail/cve-2025-61729), [CVE-2025-68121](https://nvd.nist.gov/vuln/detail/cve-2025-68121), [RHSA-2026:7674](https://access.redhat.com/errata/RHSA-2026:7674), [CVE-2026-25679](https://access.redhat.com/security/cve/cve-2026-25679), [RHSA-2026:6915](https://access.redhat.com/errata/RHSA-2026:6915), [CVE-2026-28417](https://nvd.nist.gov/vuln/detail/cve-2026-28417), [CVE-2026-28421](https://nvd.nist.gov/vuln/detail/cve-2026-28421), [CVE-2026-33412](https://nvd.nist.gov/vuln/detail/cve-2026-33412), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:4772](https://access.redhat.com/errata/RHSA-2026:4772), [CVE-2025-15281](https://nvd.nist.gov/vuln/detail/cve-2025-15281), [CVE-2026-0915](https://nvd.nist.gov/vuln/detail/cve-2026-0915), [RHSA-2026:5585](https://access.redhat.com/errata/RHSA-2026:5585), [CVE-2025-14831](https://nvd.nist.gov/vuln/detail/cve-2025-14831), [CVE-2025-9820](https://nvd.nist.gov/vuln/detail/cve-2025-9820), [RHSA-2026:4648](https://access.redhat.com/errata/RHSA-2026:4648), [CVE-2025-61662](https://nvd.nist.gov/vuln/detail/cve-2025-61662), [RHSA-2026:6037](https://access.redhat.com/errata/RHSA-2026:6037), [CVE-2025-38180](https://nvd.nist.gov/vuln/detail/cve-2025-38180), [CVE-2026-23204](https://nvd.nist.gov/vuln/detail/cve-2026-23204), [CVE-2026-23209](https://nvd.nist.gov/vuln/detail/cve-2026-23209), [RHSA-2026:6571](https://access.redhat.com/errata/RHSA-2026:6571), [CVE-2024-26984](https://nvd.nist.gov/vuln/detail/cve-2024-26984), [CVE-2025-71238](https://nvd.nist.gov/vuln/detail/cve-2025-71238), [CVE-2026-23193](https://nvd.nist.gov/vuln/detail/cve-2026-23193), [CVE-2026-23231](https://nvd.nist.gov/vuln/detail/cve-2026-23231), [RHSA-2026:5588](https://access.redhat.com/errata/RHSA-2026:5588), [CVE-2025-0938](https://nvd.nist.gov/vuln/detail/cve-2025-0938), [RHSA-2026:4442](https://access.redhat.com/errata/RHSA-2026:4442), and [CVE-2026-25749](https://nvd.nist.gov/vuln/detail/cve-2026-25749).


Red Hat OpenShift 4.17.52
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-52_release-notes){: external}.


Red Hat CoreOS 4.17.52
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-52_release-notes){: external}.


HAProxy c7e825675cbd75e8433801c99f8aca3b207a5a46
:   Resolves the following CVEs: [CVE-2026-27135](https://nvd.nist.gov/vuln/detail/cve-2026-27135).


## 06 April 2026, Worker node fix pack 4.17.52_1579_openshift
{: #cl-boms-41752_1579_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.52_1579_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [5.4.2.4](https://workbench.cisecurity.org/sections/2758938/recommendations/4466977){: external}


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [5.4.2.4](https://workbench.cisecurity.org/sections/2758938/recommendations/4466977){: external}


RHEL 8 (VPC) 4.18.0-553.111.1.el8_10
:   Resolves the following CVEs: [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:5585](https://access.redhat.com/errata/RHSA-2026:5585), [CVE-2025-14831](https://nvd.nist.gov/vuln/detail/cve-2025-14831), [CVE-2025-9820](https://nvd.nist.gov/vuln/detail/cve-2025-9820), [RHSA-2026:3963](https://access.redhat.com/errata/RHSA-2026:3963), [CVE-2025-71085](https://nvd.nist.gov/vuln/detail/cve-2025-71085), [CVE-2026-23001](https://nvd.nist.gov/vuln/detail/cve-2026-23001), [RHSA-2026:5588](https://access.redhat.com/errata/RHSA-2026:5588), and [CVE-2025-0938](https://nvd.nist.gov/vuln/detail/cve-2025-0938).


RHEL 8 (Classic) 4.18.0-553.111.1.el8_10
:   Resolves the following CVEs: [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:3963](https://access.redhat.com/errata/RHSA-2026:3963), [CVE-2025-71085](https://nvd.nist.gov/vuln/detail/cve-2025-71085), [CVE-2026-23001](https://nvd.nist.gov/vuln/detail/cve-2026-23001), [RHSA-2026:4442](https://access.redhat.com/errata/RHSA-2026:4442), and [CVE-2026-25749](https://nvd.nist.gov/vuln/detail/cve-2026-25749).


Red Hat OpenShift 4.17.52
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-52_release-notes){: external}.


Red Hat CoreOS 4.17.52
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-52_release-notes){: external}.


HAProxy 91cc06f4e0a123d06f5ee7c226df6fb83e1ca223
:   Resolves the following CVEs: [CVE-2025-14831](https://nvd.nist.gov/vuln/detail/cve-2025-14831), and [CVE-2025-9820](https://nvd.nist.gov/vuln/detail/cve-2025-9820).


## 24 March 2026, Worker node fix pack 4.17.51_1578_openshift
{: #cl-boms-41751_1578_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.51_1578_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   


RHEL 8 (VPC) 4.18.0-553.109.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:4672](https://access.redhat.com/errata/RHSA-2026:4672), [CVE-2025-61726](https://access.redhat.com/security/cve/cve-2025-61726), [CVE-2025-61728](https://nvd.nist.gov/vuln/detail/cve-2025-61728), [CVE-2025-68121](https://nvd.nist.gov/vuln/detail/cve-2025-68121), [RHSA-2026:4728](https://access.redhat.com/errata/RHSA-2026:4728), [CVE-2026-22695](https://nvd.nist.gov/vuln/detail/cve-2026-22695), [CVE-2026-22801](https://nvd.nist.gov/vuln/detail/cve-2026-22801), [CVE-2026-25646](https://nvd.nist.gov/vuln/detail/cve-2026-25646), [RHSA-2026:4952](https://access.redhat.com/errata/RHSA-2026:4952), [CVE-2025-61726](https://access.redhat.com/security/cve/cve-2025-61726), [CVE-2025-61729](https://nvd.nist.gov/vuln/detail/cve-2025-61729), [CVE-2025-68121](https://nvd.nist.gov/vuln/detail/cve-2025-68121), [RHSA-2026:4772](https://access.redhat.com/errata/RHSA-2026:4772), [CVE-2025-15281](https://nvd.nist.gov/vuln/detail/cve-2025-15281), [CVE-2026-0915](https://nvd.nist.gov/vuln/detail/cve-2026-0915), [RHSA-2026:4648](https://access.redhat.com/errata/RHSA-2026:4648), [CVE-2025-61662](https://nvd.nist.gov/vuln/detail/cve-2025-61662), [RHSA-2026:3464](https://access.redhat.com/errata/RHSA-2026:3464), and [CVE-2026-23097](https://nvd.nist.gov/vuln/detail/cve-2026-23097).


RHEL 8 (Classic) 4.18.0-553.109.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:4672](https://access.redhat.com/errata/RHSA-2026:4672), [CVE-2025-61726](https://access.redhat.com/security/cve/cve-2025-61726), [CVE-2025-61728](https://nvd.nist.gov/vuln/detail/cve-2025-61728), [CVE-2025-68121](https://nvd.nist.gov/vuln/detail/cve-2025-68121), [RHSA-2026:4728](https://access.redhat.com/errata/RHSA-2026:4728), [CVE-2026-22695](https://nvd.nist.gov/vuln/detail/cve-2026-22695), [CVE-2026-22801](https://nvd.nist.gov/vuln/detail/cve-2026-22801), [CVE-2026-25646](https://nvd.nist.gov/vuln/detail/cve-2026-25646), [RHSA-2026:4952](https://access.redhat.com/errata/RHSA-2026:4952), [CVE-2025-61726](https://access.redhat.com/security/cve/cve-2025-61726), [CVE-2025-61729](https://nvd.nist.gov/vuln/detail/cve-2025-61729), [CVE-2025-68121](https://nvd.nist.gov/vuln/detail/cve-2025-68121), [RHSA-2026:4772](https://access.redhat.com/errata/RHSA-2026:4772), [CVE-2025-15281](https://nvd.nist.gov/vuln/detail/cve-2025-15281), [CVE-2026-0915](https://nvd.nist.gov/vuln/detail/cve-2026-0915), [RHSA-2026:4648](https://access.redhat.com/errata/RHSA-2026:4648), [CVE-2025-61662](https://nvd.nist.gov/vuln/detail/cve-2025-61662), [RHSA-2026:3464](https://access.redhat.com/errata/RHSA-2026:3464), and [CVE-2026-23097](https://nvd.nist.gov/vuln/detail/cve-2026-23097).


Red Hat OpenShift 4.17.51
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-51_release-notes){: external}.


Red Hat CoreOS 4.17.51
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-51_release-notes){: external}.


HAProxy 10c8639e6b5829d0af51a22755e13756f34630cf
:   Resolves the following CVEs: [CVE-2025-15281](https://nvd.nist.gov/vuln/detail/cve-2025-15281), and [CVE-2026-0915](https://nvd.nist.gov/vuln/detail/cve-2026-0915).


## 11 March 2026, Worker node fix pack 4.17.50_1575_openshift
{: #cl-boms-41750_1575_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.50_1575_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   


RHEL 8 (VPC) 4.18.0-553.107.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:2264](https://access.redhat.com/errata/RHSA-2026:2264), [CVE-2025-68349](https://nvd.nist.gov/vuln/detail/cve-2025-68349), [CVE-2025-38403](https://nvd.nist.gov/vuln/detail/cve-2025-38403), [CVE-2025-40158](https://nvd.nist.gov/vuln/detail/cve-2025-40158), [CVE-2025-40135](https://nvd.nist.gov/vuln/detail/cve-2025-40135), [CVE-2025-40170](https://nvd.nist.gov/vuln/detail/cve-2025-40170), [CVE-2026-22998](https://nvd.nist.gov/vuln/detail/cve-2026-22998), [CVE-2025-40269](https://nvd.nist.gov/vuln/detail/cve-2025-40269), [CVE-2022-50673](https://nvd.nist.gov/vuln/detail/cve-2022-50673), [RHSA-2026:2720](https://access.redhat.com/errata/RHSA-2026:2720), [CVE-2025-40168](https://nvd.nist.gov/vuln/detail/cve-2025-40168), [CVE-2025-40304](https://nvd.nist.gov/vuln/detail/cve-2025-40304), [CVE-2023-53762](https://nvd.nist.gov/vuln/detail/cve-2023-53762), [RHSA-2026:3083](https://access.redhat.com/errata/RHSA-2026:3083), [CVE-2025-38129](https://nvd.nist.gov/vuln/detail/cve-2025-38129), [CVE-2025-38248](https://nvd.nist.gov/vuln/detail/cve-2025-38248), [CVE-2025-40064](https://nvd.nist.gov/vuln/detail/cve-2025-40064), [CVE-2025-68800](https://nvd.nist.gov/vuln/detail/cve-2025-68800), and [CVE-2026-23074](https://nvd.nist.gov/vuln/detail/cve-2026-23074).


RHEL 8 (Classic) 4.18.0-553.107.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:2264](https://access.redhat.com/errata/RHSA-2026:2264), [CVE-2025-68349](https://nvd.nist.gov/vuln/detail/cve-2025-68349), [CVE-2025-38403](https://nvd.nist.gov/vuln/detail/cve-2025-38403), [CVE-2025-40158](https://nvd.nist.gov/vuln/detail/cve-2025-40158), [CVE-2025-40135](https://nvd.nist.gov/vuln/detail/cve-2025-40135), [CVE-2025-40170](https://nvd.nist.gov/vuln/detail/cve-2025-40170), [CVE-2026-22998](https://nvd.nist.gov/vuln/detail/cve-2026-22998), [CVE-2025-40269](https://nvd.nist.gov/vuln/detail/cve-2025-40269), [CVE-2022-50673](https://nvd.nist.gov/vuln/detail/cve-2022-50673), [RHSA-2026:2720](https://access.redhat.com/errata/RHSA-2026:2720), [CVE-2025-40168](https://nvd.nist.gov/vuln/detail/cve-2025-40168), [CVE-2025-40304](https://nvd.nist.gov/vuln/detail/cve-2025-40304), [CVE-2023-53762](https://nvd.nist.gov/vuln/detail/cve-2023-53762), [RHSA-2026:3083](https://access.redhat.com/errata/RHSA-2026:3083), [CVE-2025-38129](https://nvd.nist.gov/vuln/detail/cve-2025-38129), [CVE-2025-38248](https://nvd.nist.gov/vuln/detail/cve-2025-38248), [CVE-2025-40064](https://nvd.nist.gov/vuln/detail/cve-2025-40064), [CVE-2025-68800](https://nvd.nist.gov/vuln/detail/cve-2025-68800), and [CVE-2026-23074](https://nvd.nist.gov/vuln/detail/cve-2026-23074).


Red Hat OpenShift 4.17.50
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-50_release-notes){: external}.


Red Hat CoreOS 4.17.50
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-50_release-notes){: external}.


HAProxy 965c403695b15b3410d87a3772002edbc5ed2569
:   Resolves the following CVEs: [CVE-2025-69419](https://nvd.nist.gov/vuln/detail/cve-2025-69419).


## 24 February 2026, Worker node fix pack 4.17.49_1574_openshift
{: #cl-boms-41749_1574_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.49_1574_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [1.6.3](https://workbench.cisecurity.org/sections/2758919/recommendations/4466876){: external}


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [1.6.3](https://workbench.cisecurity.org/sections/2758919/recommendations/4466876){: external}


RHEL 8 (VPC) 4.18.0-553.100.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:2389](https://access.redhat.com/errata/RHSA-2026:2389), [CVE-2025-6176](https://nvd.nist.gov/vuln/detail/cve-2025-6176), [RHSA-2026:2215](https://access.redhat.com/errata/RHSA-2026:2215), [CVE-2026-0719](https://nvd.nist.gov/vuln/detail/cve-2026-0719), [CVE-2026-1761](https://nvd.nist.gov/vuln/detail/cve-2026-1761), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:1662](https://access.redhat.com/errata/RHSA-2026:1662), [CVE-2022-50865](https://nvd.nist.gov/vuln/detail/cve-2022-50865), [CVE-2024-26766](https://nvd.nist.gov/vuln/detail/cve-2024-26766), [CVE-2025-38022](https://nvd.nist.gov/vuln/detail/cve-2025-38022), [CVE-2025-38024](https://nvd.nist.gov/vuln/detail/cve-2025-38024), [CVE-2025-38415](https://nvd.nist.gov/vuln/detail/cve-2025-38415), [CVE-2025-38459](https://nvd.nist.gov/vuln/detail/cve-2025-38459), [CVE-2025-39760](https://nvd.nist.gov/vuln/detail/cve-2025-39760), [CVE-2025-40258](https://nvd.nist.gov/vuln/detail/cve-2025-40258), [CVE-2025-40271](https://nvd.nist.gov/vuln/detail/cve-2025-40271), [CVE-2025-40322](https://nvd.nist.gov/vuln/detail/cve-2025-40322), [RHSA-2026:2264](https://access.redhat.com/errata/RHSA-2026:2264), [CVE-2022-50673](https://nvd.nist.gov/vuln/detail/cve-2022-50673), [CVE-2025-38403](https://nvd.nist.gov/vuln/detail/cve-2025-38403), [CVE-2025-40135](https://nvd.nist.gov/vuln/detail/cve-2025-40135), [CVE-2025-40158](https://nvd.nist.gov/vuln/detail/cve-2025-40158), [CVE-2025-40170](https://nvd.nist.gov/vuln/detail/cve-2025-40170), [CVE-2025-40269](https://nvd.nist.gov/vuln/detail/cve-2025-40269), [CVE-2025-68349](https://nvd.nist.gov/vuln/detail/cve-2025-68349), [CVE-2026-22998](https://nvd.nist.gov/vuln/detail/cve-2026-22998), [RHSA-2026:2720](https://access.redhat.com/errata/RHSA-2026:2720), [CVE-2023-53762](https://nvd.nist.gov/vuln/detail/cve-2023-53762), [CVE-2025-40168](https://nvd.nist.gov/vuln/detail/cve-2025-40168), [CVE-2025-40304](https://nvd.nist.gov/vuln/detail/cve-2025-40304), [RHSA-2026:2128](https://access.redhat.com/errata/RHSA-2026:2128), [CVE-2025-15366](https://nvd.nist.gov/vuln/detail/cve-2025-15366), [CVE-2025-15367](https://nvd.nist.gov/vuln/detail/cve-2025-15367), [CVE-2026-0865](https://nvd.nist.gov/vuln/detail/cve-2026-0865), and [CVE-2026-1299](https://nvd.nist.gov/vuln/detail/cve-2026-1299).


RHEL 8 (Classic) 4.18.0-553.100.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:2389](https://access.redhat.com/errata/RHSA-2026:2389), [CVE-2025-6176](https://nvd.nist.gov/vuln/detail/cve-2025-6176), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:1662](https://access.redhat.com/errata/RHSA-2026:1662), [CVE-2022-50865](https://nvd.nist.gov/vuln/detail/cve-2022-50865), [CVE-2024-26766](https://nvd.nist.gov/vuln/detail/cve-2024-26766), [CVE-2025-38022](https://nvd.nist.gov/vuln/detail/cve-2025-38022), [CVE-2025-38024](https://nvd.nist.gov/vuln/detail/cve-2025-38024), [CVE-2025-38415](https://nvd.nist.gov/vuln/detail/cve-2025-38415), [CVE-2025-38459](https://nvd.nist.gov/vuln/detail/cve-2025-38459), [CVE-2025-39760](https://nvd.nist.gov/vuln/detail/cve-2025-39760), [CVE-2025-40258](https://nvd.nist.gov/vuln/detail/cve-2025-40258), [CVE-2025-40271](https://nvd.nist.gov/vuln/detail/cve-2025-40271), [CVE-2025-40322](https://nvd.nist.gov/vuln/detail/cve-2025-40322), [RHSA-2026:2264](https://access.redhat.com/errata/RHSA-2026:2264), [CVE-2022-50673](https://nvd.nist.gov/vuln/detail/cve-2022-50673), [CVE-2025-38403](https://nvd.nist.gov/vuln/detail/cve-2025-38403), [CVE-2025-40135](https://nvd.nist.gov/vuln/detail/cve-2025-40135), [CVE-2025-40158](https://nvd.nist.gov/vuln/detail/cve-2025-40158), [CVE-2025-40170](https://nvd.nist.gov/vuln/detail/cve-2025-40170), [CVE-2025-40269](https://nvd.nist.gov/vuln/detail/cve-2025-40269), [CVE-2025-68349](https://nvd.nist.gov/vuln/detail/cve-2025-68349), [CVE-2026-22998](https://nvd.nist.gov/vuln/detail/cve-2026-22998), [RHSA-2026:2720](https://access.redhat.com/errata/RHSA-2026:2720), [CVE-2023-53762](https://nvd.nist.gov/vuln/detail/cve-2023-53762), [CVE-2025-40168](https://nvd.nist.gov/vuln/detail/cve-2025-40168), and [CVE-2025-40304](https://nvd.nist.gov/vuln/detail/cve-2025-40304).


Red Hat OpenShift 4.17.49
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-49_release-notes){: external}.


Red Hat CoreOS 4.17.49
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-49_release-notes){: external}.


HAProxy 2bf1aebe51a37cd9b4661656ce21e53f918166ea
:   Resolves the following CVEs: [CVE-2025-6176](https://nvd.nist.gov/vuln/detail/cve-2025-6176).


## 09 February 2026, Worker node fix pack 4.17.48_1572_openshift
{: #cl-boms-41748_1572_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.48_1572_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [1.6.6](https://workbench.cisecurity.org/sections/2758919/recommendations/4466895){: external}, [3.1.3](https://workbench.cisecurity.org/sections/2758883/recommendations/4466704){: external}, [4.1.2](https://workbench.cisecurity.org/sections/2758898/recommendations/4466776){: external}, [4.3.4](https://workbench.cisecurity.org/sections/2758905/recommendations/4466822){: external}, [5.3.2.1](https://workbench.cisecurity.org/sections/2758922/recommendations/4466880){: external}, [5.3.3.2.4](https://workbench.cisecurity.org/sections/2758930/recommendations/4466941){: external}, [5.3.3.2.7](https://workbench.cisecurity.org/sections/2758930/recommendations/4466958){: external}, [5.3.3.3.1](https://workbench.cisecurity.org/sections/2758934/recommendations/4466960){: external}, [5.3.3.4.2](https://workbench.cisecurity.org/sections/2758935/recommendations/4466965){: external}, [5.4.1.5](https://workbench.cisecurity.org/sections/2758937/recommendations/4466972){: external}, [5.4.2.5](https://workbench.cisecurity.org/sections/2758938/recommendations/4466978){: external}Resolves the following CVEs: [RHSA-2025:19930](https://access.redhat.com/errata/RHSA-2025:19930), [CVE-2024-36350](https://nvd.nist.gov/vuln/detail/cve-2024-36350), [CVE-2024-36357](https://nvd.nist.gov/vuln/detail/cve-2024-36357), and [CVE-2025-40300](https://nvd.nist.gov/vuln/detail/cve-2025-40300).


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [1.6.6](https://workbench.cisecurity.org/sections/2758919/recommendations/4466895){: external}, [3.1.3](https://workbench.cisecurity.org/sections/2758883/recommendations/4466704){: external}, [4.1.2](https://workbench.cisecurity.org/sections/2758898/recommendations/4466776){: external}, [4.3.4](https://workbench.cisecurity.org/sections/2758905/recommendations/4466822){: external}, [5.3.2.1](https://workbench.cisecurity.org/sections/2758922/recommendations/4466880){: external}, [5.3.3.2.4](https://workbench.cisecurity.org/sections/2758930/recommendations/4466941){: external}, [5.3.3.2.7](https://workbench.cisecurity.org/sections/2758930/recommendations/4466958){: external}, [5.3.3.3.1](https://workbench.cisecurity.org/sections/2758934/recommendations/4466960){: external}, [5.3.3.4.2](https://workbench.cisecurity.org/sections/2758935/recommendations/4466965){: external}, [5.4.1.5](https://workbench.cisecurity.org/sections/2758937/recommendations/4466972){: external}, [5.4.2.5](https://workbench.cisecurity.org/sections/2758938/recommendations/4466978){: external}Resolves the following CVEs: [RHSA-2025:19930](https://access.redhat.com/errata/RHSA-2025:19930), [CVE-2024-36350](https://nvd.nist.gov/vuln/detail/cve-2024-36350), [CVE-2024-36357](https://nvd.nist.gov/vuln/detail/cve-2024-36357), and [CVE-2025-40300](https://nvd.nist.gov/vuln/detail/cve-2025-40300).


RHEL 8 (VPC) 4.18.0-553.97.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:0444](https://access.redhat.com/errata/RHSA-2026:0444), [CVE-2025-39993](https://nvd.nist.gov/vuln/detail/cve-2025-39993), [CVE-2025-40240](https://nvd.nist.gov/vuln/detail/cve-2025-40240), [CVE-2025-68285](https://nvd.nist.gov/vuln/detail/cve-2025-68285), [RHSA-2026:0759](https://access.redhat.com/errata/RHSA-2026:0759), [CVE-2023-53552](https://nvd.nist.gov/vuln/detail/cve-2023-53552), [CVE-2025-38051](https://nvd.nist.gov/vuln/detail/cve-2025-38051), [CVE-2025-39933](https://nvd.nist.gov/vuln/detail/cve-2025-39933), [CVE-2025-40096](https://nvd.nist.gov/vuln/detail/cve-2025-40096), [CVE-2025-68301](https://nvd.nist.gov/vuln/detail/cve-2025-68301), [RHSA-2026:1142](https://access.redhat.com/errata/RHSA-2026:1142), [CVE-2023-53673](https://nvd.nist.gov/vuln/detail/cve-2023-53673), [CVE-2025-40154](https://nvd.nist.gov/vuln/detail/cve-2025-40154), [CVE-2025-40248](https://nvd.nist.gov/vuln/detail/cve-2025-40248), [CVE-2025-40277](https://nvd.nist.gov/vuln/detail/cve-2025-40277), [RHSA-2026:1254](https://access.redhat.com/errata/RHSA-2026:1254), [CVE-2025-66418](https://nvd.nist.gov/vuln/detail/cve-2025-66418), [CVE-2025-66471](https://nvd.nist.gov/vuln/detail/cve-2025-66471), [CVE-2026-21441](https://nvd.nist.gov/vuln/detail/cve-2026-21441), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:1662](https://access.redhat.com/errata/RHSA-2026:1662), [CVE-2022-50865](https://nvd.nist.gov/vuln/detail/cve-2022-50865), [CVE-2024-26766](https://nvd.nist.gov/vuln/detail/cve-2024-26766), [CVE-2025-38022](https://nvd.nist.gov/vuln/detail/cve-2025-38022), [CVE-2025-38024](https://nvd.nist.gov/vuln/detail/cve-2025-38024), [CVE-2025-38415](https://nvd.nist.gov/vuln/detail/cve-2025-38415), [CVE-2025-38459](https://nvd.nist.gov/vuln/detail/cve-2025-38459), [CVE-2025-39760](https://nvd.nist.gov/vuln/detail/cve-2025-39760), [CVE-2025-40258](https://nvd.nist.gov/vuln/detail/cve-2025-40258), [CVE-2025-40271](https://nvd.nist.gov/vuln/detail/cve-2025-40271), [CVE-2025-40322](https://nvd.nist.gov/vuln/detail/cve-2025-40322), [RHSA-2026:1631](https://access.redhat.com/errata/RHSA-2026:1631), [CVE-2025-12084](https://nvd.nist.gov/vuln/detail/cve-2025-12084), [RHSA-2026:2128](https://access.redhat.com/errata/RHSA-2026:2128), [CVE-2025-15366](https://nvd.nist.gov/vuln/detail/cve-2025-15366), [CVE-2025-15367](https://nvd.nist.gov/vuln/detail/cve-2025-15367), [CVE-2026-0865](https://nvd.nist.gov/vuln/detail/cve-2026-0865), [CVE-2026-1299](https://nvd.nist.gov/vuln/detail/cve-2026-1299), [RHSA-2026:1852](https://access.redhat.com/errata/RHSA-2026:1852), and [CVE-2025-14104](https://nvd.nist.gov/vuln/detail/cve-2025-14104).


RHEL 8 (Classic) 4.18.0-553.97.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:23543](https://access.redhat.com/errata/RHSA-2025:23543), [CVE-2025-52881](https://nvd.nist.gov/vuln/detail/cve-2025-52881), [RHSA-2026:0753](https://access.redhat.com/errata/RHSA-2026:0753), [CVE-2025-47913](https://nvd.nist.gov/vuln/detail/cve-2025-47913), [RHSA-2026:0728](https://access.redhat.com/errata/RHSA-2026:0728), [CVE-2025-68973](https://nvd.nist.gov/vuln/detail/cve-2025-68973), [RHSA-2026:0444](https://access.redhat.com/errata/RHSA-2026:0444), [CVE-2025-39993](https://nvd.nist.gov/vuln/detail/cve-2025-39993), [CVE-2025-40240](https://nvd.nist.gov/vuln/detail/cve-2025-40240), [CVE-2025-68285](https://nvd.nist.gov/vuln/detail/cve-2025-68285), [RHSA-2026:0759](https://access.redhat.com/errata/RHSA-2026:0759), [CVE-2023-53552](https://nvd.nist.gov/vuln/detail/cve-2023-53552), [CVE-2025-38051](https://nvd.nist.gov/vuln/detail/cve-2025-38051), [CVE-2025-39933](https://nvd.nist.gov/vuln/detail/cve-2025-39933), [CVE-2025-40096](https://nvd.nist.gov/vuln/detail/cve-2025-40096), [CVE-2025-68301](https://nvd.nist.gov/vuln/detail/cve-2025-68301), [RHSA-2026:1142](https://access.redhat.com/errata/RHSA-2026:1142), [CVE-2023-53673](https://nvd.nist.gov/vuln/detail/cve-2023-53673), [CVE-2025-40154](https://nvd.nist.gov/vuln/detail/cve-2025-40154), [CVE-2025-40248](https://nvd.nist.gov/vuln/detail/cve-2025-40248), [CVE-2025-40277](https://nvd.nist.gov/vuln/detail/cve-2025-40277), [RHSA-2026:0241](https://access.redhat.com/errata/RHSA-2026:0241), [CVE-2025-64720](https://nvd.nist.gov/vuln/detail/cve-2025-64720), [CVE-2025-65018](https://nvd.nist.gov/vuln/detail/cve-2025-65018), [CVE-2025-66293](https://nvd.nist.gov/vuln/detail/cve-2025-66293), [RHSA-2026:1254](https://access.redhat.com/errata/RHSA-2026:1254), [CVE-2025-66418](https://nvd.nist.gov/vuln/detail/cve-2025-66418), [CVE-2025-66471](https://nvd.nist.gov/vuln/detail/cve-2025-66471), [CVE-2026-21441](https://nvd.nist.gov/vuln/detail/cve-2026-21441), [RHSA-2025:23530](https://access.redhat.com/errata/RHSA-2025:23530), [CVE-2024-11168](https://nvd.nist.gov/vuln/detail/cve-2024-11168), [CVE-2024-5642](https://nvd.nist.gov/vuln/detail/cve-2024-5642), [CVE-2024-9287](https://nvd.nist.gov/vuln/detail/cve-2024-9287), [CVE-2025-0938](https://nvd.nist.gov/vuln/detail/cve-2025-0938), [CVE-2025-4138](https://nvd.nist.gov/vuln/detail/cve-2025-4138), [CVE-2025-4330](https://nvd.nist.gov/vuln/detail/cve-2025-4330), [CVE-2025-4435](https://nvd.nist.gov/vuln/detail/cve-2025-4435), [CVE-2025-4516](https://nvd.nist.gov/vuln/detail/cve-2025-4516), [CVE-2025-4517](https://nvd.nist.gov/vuln/detail/cve-2025-4517), [CVE-2025-6069](https://nvd.nist.gov/vuln/detail/cve-2025-6069), [CVE-2025-6075](https://nvd.nist.gov/vuln/detail/cve-2025-6075), [CVE-2025-8291](https://nvd.nist.gov/vuln/detail/cve-2025-8291), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:23382](https://access.redhat.com/errata/RHSA-2025:23382), [CVE-2025-11083](https://nvd.nist.gov/vuln/detail/cve-2025-11083), [RHSA-2025:23374](https://access.redhat.com/errata/RHSA-2025:23374), [CVE-2025-58183](https://nvd.nist.gov/vuln/detail/cve-2025-58183), [RHSA-2025:23383](https://access.redhat.com/errata/RHSA-2025:23383), [CVE-2025-9086](https://nvd.nist.gov/vuln/detail/cve-2025-9086), [RHSA-2026:0991](https://access.redhat.com/errata/RHSA-2026:0991), [CVE-2025-13601](https://nvd.nist.gov/vuln/detail/cve-2025-13601), [RHSA-2026:1662](https://access.redhat.com/errata/RHSA-2026:1662), [CVE-2022-50865](https://nvd.nist.gov/vuln/detail/cve-2022-50865), [CVE-2024-26766](https://nvd.nist.gov/vuln/detail/cve-2024-26766), [CVE-2025-38022](https://nvd.nist.gov/vuln/detail/cve-2025-38022), [CVE-2025-38024](https://nvd.nist.gov/vuln/detail/cve-2025-38024), [CVE-2025-38415](https://nvd.nist.gov/vuln/detail/cve-2025-38415), [CVE-2025-38459](https://nvd.nist.gov/vuln/detail/cve-2025-38459), [CVE-2025-39760](https://nvd.nist.gov/vuln/detail/cve-2025-39760), [CVE-2025-40258](https://nvd.nist.gov/vuln/detail/cve-2025-40258), [CVE-2025-40271](https://nvd.nist.gov/vuln/detail/cve-2025-40271), [CVE-2025-40322](https://nvd.nist.gov/vuln/detail/cve-2025-40322), [RHSA-2025:23481](https://access.redhat.com/errata/RHSA-2025:23481), [CVE-2025-61984](https://nvd.nist.gov/vuln/detail/cve-2025-61984), [CVE-2025-61985](https://nvd.nist.gov/vuln/detail/cve-2025-61985), [RHSA-2026:0337](https://access.redhat.com/errata/RHSA-2026:0337), [CVE-2025-9230](https://nvd.nist.gov/vuln/detail/cve-2025-9230), [RHSA-2026:1631](https://access.redhat.com/errata/RHSA-2026:1631), [CVE-2025-12084](https://nvd.nist.gov/vuln/detail/cve-2025-12084), [RHSA-2026:2128](https://access.redhat.com/errata/RHSA-2026:2128), [CVE-2025-15366](https://nvd.nist.gov/vuln/detail/cve-2025-15366), [CVE-2025-15367](https://nvd.nist.gov/vuln/detail/cve-2025-15367), [CVE-2026-0865](https://nvd.nist.gov/vuln/detail/cve-2026-0865), [CVE-2026-1299](https://nvd.nist.gov/vuln/detail/cve-2026-1299), [RHSA-2026:1852](https://access.redhat.com/errata/RHSA-2026:1852), and [CVE-2025-14104](https://nvd.nist.gov/vuln/detail/cve-2025-14104).


Red Hat OpenShift 4.17.48
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-48_release-notes){: external}.


Red Hat CoreOS 4.17.48
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-48_release-notes){: external}.


HAProxy ace947f4ecf45f28effe8d125ffda48f9890223b
:   Resolves the following CVEs: [CVE-2025-14104](https://nvd.nist.gov/vuln/detail/cve-2025-14104).


## 27 January 2026, Worker node fix pack 4.17.47_1571_openshift
{: #cl-boms-41747_1571_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.47_1571_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.60.1.el9_6
:   Beginning at this patch version, VPC worker nodes include the following changes: the local time is set to UTC, the root filesystem has changed from ext4 to XFS, and the boot mode has changed from BIOS to UEFI.


RHEL 9 (Classic) 5.14.0-570.60.1.el9_6
:   


RHEL 8 (VPC) 4.18.0-553.89.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:0753](https://access.redhat.com/errata/RHSA-2026:0753), [CVE-2025-47913](https://nvd.nist.gov/vuln/detail/cve-2025-47913), [RHSA-2026:0728](https://access.redhat.com/errata/RHSA-2026:0728), [CVE-2025-68973](https://nvd.nist.gov/vuln/detail/cve-2025-68973), [RHSA-2026:0444](https://access.redhat.com/errata/RHSA-2026:0444), [CVE-2025-39993](https://nvd.nist.gov/vuln/detail/cve-2025-39993), [CVE-2025-40240](https://nvd.nist.gov/vuln/detail/cve-2025-40240), [CVE-2025-68285](https://nvd.nist.gov/vuln/detail/cve-2025-68285), [RHSA-2026:0759](https://access.redhat.com/errata/RHSA-2026:0759), [CVE-2023-53552](https://nvd.nist.gov/vuln/detail/cve-2023-53552), [CVE-2025-38051](https://nvd.nist.gov/vuln/detail/cve-2025-38051), [CVE-2025-39933](https://nvd.nist.gov/vuln/detail/cve-2025-39933), [CVE-2025-40096](https://nvd.nist.gov/vuln/detail/cve-2025-40096), [CVE-2025-68301](https://nvd.nist.gov/vuln/detail/cve-2025-68301), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:0991](https://access.redhat.com/errata/RHSA-2026:0991), and [CVE-2025-13601](https://nvd.nist.gov/vuln/detail/cve-2025-13601).


RHEL 8 (Classic) 4.18.0-553.89.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:0753](https://access.redhat.com/errata/RHSA-2026:0753), [CVE-2025-47913](https://nvd.nist.gov/vuln/detail/cve-2025-47913), [RHSA-2026:0728](https://access.redhat.com/errata/RHSA-2026:0728), [CVE-2025-68973](https://nvd.nist.gov/vuln/detail/cve-2025-68973), [RHSA-2026:0444](https://access.redhat.com/errata/RHSA-2026:0444), [CVE-2025-39993](https://nvd.nist.gov/vuln/detail/cve-2025-39993), [CVE-2025-40240](https://nvd.nist.gov/vuln/detail/cve-2025-40240), [CVE-2025-68285](https://nvd.nist.gov/vuln/detail/cve-2025-68285), [RHSA-2026:0759](https://access.redhat.com/errata/RHSA-2026:0759), [CVE-2023-53552](https://nvd.nist.gov/vuln/detail/cve-2023-53552), [CVE-2025-38051](https://nvd.nist.gov/vuln/detail/cve-2025-38051), [CVE-2025-39933](https://nvd.nist.gov/vuln/detail/cve-2025-39933), [CVE-2025-40096](https://nvd.nist.gov/vuln/detail/cve-2025-40096), [CVE-2025-68301](https://nvd.nist.gov/vuln/detail/cve-2025-68301), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2026:0991](https://access.redhat.com/errata/RHSA-2026:0991), and [CVE-2025-13601](https://nvd.nist.gov/vuln/detail/cve-2025-13601).


Red Hat OpenShift 4.17.47
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-47_release-notes){: external}.


Red Hat CoreOS 4.17.47
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-47_release-notes){: external}.


HAProxy c9cb5ad988e916d184d1c308d4f2e5c502d99523
:   Resolves the following CVEs: [CVE-2025-68973](https://nvd.nist.gov/vuln/detail/cve-2025-68973), [CVE-2025-13601](https://nvd.nist.gov/vuln/detail/cve-2025-13601), and [CVE-2025-9230](https://nvd.nist.gov/vuln/detail/cve-2025-9230).


## Master fix pack 4.17.45_1570_openshift, released 21 January 2026
{: #41745_1570_openshift_M}

The following list shows the changes that are in the master fix pack 4.17.45_1570_openshift. Master patch updates are applied automatically. 


Calico v3.29.7
:   See the [Calico release notes](https://archive-os-3-29.netlify.app/calico/3.29/release-notes/#calico-open-source-3297-bug-fix-release){: external}.
Cluster health image v1.6.13
:   New version contains updates and security fixes.
etcd v3.5.26
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.26){: external}.
{{site.data.keyword.cloud_notm}} Controller Manager v1.30.14-26
:   New version contains updates and security fixes.
Key Management Service provider 2.10.20
:   New version contains updates and security fixes.
Portieris admission controller v0.13.33
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.33){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.17.45
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-45_release-notes){: external}.
Tigera Operator v1.36.16
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.36.16){: external}.


## 12 January 2026, Worker node fix pack 4.17.46_1568_openshift
{: #cl-boms-41746_1568_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.46_1568_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 5.14.0-570.60.1.el9_6
:   


RHEL 8 4.18.0-553.89.1.el8_10
:   Resolves the following CVEs: [RHSA-2026:0241](https://access.redhat.com/errata/RHSA-2026:0241), [CVE-2025-64720](https://nvd.nist.gov/vuln/detail/cve-2025-64720), [CVE-2025-65018](https://nvd.nist.gov/vuln/detail/cve-2025-65018), [CVE-2025-66293](https://nvd.nist.gov/vuln/detail/cve-2025-66293), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), and [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690).


Red Hat OpenShift 4.17.46
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-46_release-notes){: external}.


Red Hat CoreOS 4.17.46
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-46_release-notes){: external}.


HAProxy d04e61c5b29aa5328bc72455edb95e08e8f6d85c
:   


## 29 December 2025, Worker node fix pack 4.17.45_1567_openshift
{: #cl-boms-41745_1567_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.45_1567_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 5.14.0-570.60.1.el9_6
:   


RHEL 8 4.18.0-553.89.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:23543](https://access.redhat.com/errata/RHSA-2025:23543), [CVE-2025-52881](https://nvd.nist.gov/vuln/detail/cve-2025-52881), [RHSA-2025:23530](https://access.redhat.com/errata/RHSA-2025:23530), [CVE-2024-11168](https://nvd.nist.gov/vuln/detail/cve-2024-11168), [CVE-2024-5642](https://nvd.nist.gov/vuln/detail/cve-2024-5642), [CVE-2024-9287](https://nvd.nist.gov/vuln/detail/cve-2024-9287), [CVE-2025-0938](https://nvd.nist.gov/vuln/detail/cve-2025-0938), [CVE-2025-4138](https://nvd.nist.gov/vuln/detail/cve-2025-4138), [CVE-2025-4330](https://nvd.nist.gov/vuln/detail/cve-2025-4330), [CVE-2025-4435](https://nvd.nist.gov/vuln/detail/cve-2025-4435), [CVE-2025-4516](https://nvd.nist.gov/vuln/detail/cve-2025-4516), [CVE-2025-4517](https://nvd.nist.gov/vuln/detail/cve-2025-4517), [CVE-2025-6069](https://nvd.nist.gov/vuln/detail/cve-2025-6069), [CVE-2025-6075](https://nvd.nist.gov/vuln/detail/cve-2025-6075), [CVE-2025-8291](https://nvd.nist.gov/vuln/detail/cve-2025-8291), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:23382](https://access.redhat.com/errata/RHSA-2025:23382), [CVE-2025-11083](https://nvd.nist.gov/vuln/detail/cve-2025-11083), [RHSA-2025:23374](https://access.redhat.com/errata/RHSA-2025:23374), [CVE-2025-58183](https://nvd.nist.gov/vuln/detail/cve-2025-58183), [RHSA-2025:23383](https://access.redhat.com/errata/RHSA-2025:23383), [CVE-2025-9086](https://nvd.nist.gov/vuln/detail/cve-2025-9086), [RHSA-2025:21917](https://access.redhat.com/errata/RHSA-2025:21917), [CVE-2025-39697](https://nvd.nist.gov/vuln/detail/cve-2025-39697), [CVE-2025-39971](https://nvd.nist.gov/vuln/detail/cve-2025-39971), [RHSA-2025:22388](https://access.redhat.com/errata/RHSA-2025:22388), [CVE-2023-53513](https://nvd.nist.gov/vuln/detail/cve-2023-53513), [CVE-2025-38724](https://nvd.nist.gov/vuln/detail/cve-2025-38724), [CVE-2025-39825](https://nvd.nist.gov/vuln/detail/cve-2025-39825), [CVE-2025-39883](https://nvd.nist.gov/vuln/detail/cve-2025-39883), [CVE-2025-39898](https://nvd.nist.gov/vuln/detail/cve-2025-39898), [CVE-2025-39955](https://nvd.nist.gov/vuln/detail/cve-2025-39955), [RHSA-2025:22801](https://access.redhat.com/errata/RHSA-2025:22801), [CVE-2022-50543](https://nvd.nist.gov/vuln/detail/cve-2022-50543), [CVE-2023-53401](https://nvd.nist.gov/vuln/detail/cve-2023-53401), [CVE-2023-53539](https://nvd.nist.gov/vuln/detail/cve-2023-53539), [RHSA-2025:23481](https://access.redhat.com/errata/RHSA-2025:23481), [CVE-2025-61984](https://nvd.nist.gov/vuln/detail/cve-2025-61984), and [CVE-2025-61985](https://nvd.nist.gov/vuln/detail/cve-2025-61985).


Red Hat OpenShift 4.17.45
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-45_release-notes){: external}.


Red Hat CoreOS 4.17.45
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-45_release-notes){: external}.


HAProxy d04e61c5b29aa5328bc72455edb95e08e8f6d85c
:   Resolves the following CVEs: [CVE-2025-9086](https://nvd.nist.gov/vuln/detail/cve-2025-9086).


## 16 December 2025, Worker node fix pack 4.17.45_1566_openshift
{: #cl-boms-41745_1566_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.45_1566_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 5.14.0-570.60.1.el9_6
:   


RHEL 8 4.18.0-553.84.1.el8_10
:   


Red Hat OpenShift 4.17.45
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-45_release-notes){: external}.


Red Hat CoreOS 4.17.45
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-45_release-notes){: external}.


HAProxy 03b74b82b63cd53403b6b587b84233c93edef18d
:   


## Master fix pack 4.17.44_1565_openshift, released 10 December 2025
{: #41744_1565_openshift_M}

The following list shows the changes that are in the master fix pack 4.17.44_1565_openshift. Master patch updates are applied automatically. 


Cluster health image v1.6.13
:   New version contains updates and security fixes.
etcd v3.5.25
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.25){: external}.
{{site.data.keyword.cloud_notm}} Controller Manager v1.30.14-22
:   New version contains updates and security fixes.
Key Management Service provider 2.10.19
:   New version contains updates and security fixes.
Portieris admission controller v0.13.33
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.33){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.17.44
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-44_release-notes){: external}.


## 03 December 2025, Worker node fix pack 4.17.43_1564_openshift
{: #cl-boms-41743_1564_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.43_1564_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 5.14.0-570.60.1.el9_6
:   


RHEL 8 4.18.0-553.84.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:21776](https://access.redhat.com/errata/RHSA-2025:21776), [CVE-2025-59375](https://nvd.nist.gov/vuln/detail/cve-2025-59375), [RHSA-2025:19931](https://access.redhat.com/errata/RHSA-2025:19931), [CVE-2022-50367](https://nvd.nist.gov/vuln/detail/cve-2022-50367), [CVE-2023-53178](https://nvd.nist.gov/vuln/detail/cve-2023-53178), [CVE-2025-40300](https://nvd.nist.gov/vuln/detail/cve-2025-40300), [RHSA-2025:21398](https://access.redhat.com/errata/RHSA-2025:21398), [CVE-2025-39718](https://nvd.nist.gov/vuln/detail/cve-2025-39718), [RHSA-2025:21977](https://access.redhat.com/errata/RHSA-2025:21977), and [CVE-2025-5372](https://nvd.nist.gov/vuln/detail/cve-2025-5372).


Red Hat OpenShift 4.17.43
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-43_release-notes){: external}.


Red Hat CoreOS 4.17.43
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-43_release-notes){: external}.


HAProxy 03b74b82b63cd53403b6b587b84233c93edef18d
:   Resolves the following CVEs: [CVE-2025-59375](https://nvd.nist.gov/vuln/detail/cve-2025-59375), [CVE-2025-5372](https://nvd.nist.gov/vuln/detail/cve-2025-5372), [CVE-2024-28757](https://nvd.nist.gov/vuln/detail/cve-2024-28757), and [CVE-2022-23990](https://nvd.nist.gov/vuln/detail/cve-2022-23990).


## 17 November 2025, Worker node fix pack 4.17.43_1563_openshift
{: #cl-boms-41743_1563_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.43_1563_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 5.14.0-570.60.1.el9_6
:   Resolves the following CVEs: [RHSA-2025:19951](https://access.redhat.com/errata/RHSA-2025:19951), [CVE-2025-40778](https://nvd.nist.gov/vuln/detail/cve-2025-40778), [CVE-2025-40780](https://nvd.nist.gov/vuln/detail/cve-2025-40780), [RHSA-2025:19105](https://access.redhat.com/errata/RHSA-2025:19105), [CVE-2023-53331](https://nvd.nist.gov/vuln/detail/cve-2023-53331), [CVE-2025-39718](https://nvd.nist.gov/vuln/detail/cve-2025-39718), [CVE-2025-39730](https://nvd.nist.gov/vuln/detail/cve-2025-39730), [CVE-2025-39751](https://nvd.nist.gov/vuln/detail/cve-2025-39751), [CVE-2025-39819](https://nvd.nist.gov/vuln/detail/cve-2025-39819), [RHSA-2025:19409](https://access.redhat.com/errata/RHSA-2025:19409), [CVE-2022-50367](https://nvd.nist.gov/vuln/detail/cve-2022-50367), [CVE-2023-53494](https://nvd.nist.gov/vuln/detail/cve-2023-53494), and [CVE-2025-39702](https://nvd.nist.gov/vuln/detail/cve-2025-39702).


RHEL 8 4.18.0-553.82.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:19835](https://access.redhat.com/errata/RHSA-2025:19835), [CVE-2025-40778](https://nvd.nist.gov/vuln/detail/cve-2025-40778), [CVE-2025-8677](https://nvd.nist.gov/vuln/detail/cve-2025-8677), [RHSA-2025:21232](https://access.redhat.com/errata/RHSA-2025:21232), [CVE-2025-31133](https://nvd.nist.gov/vuln/detail/cve-2025-31133), [CVE-2025-52565](https://nvd.nist.gov/vuln/detail/cve-2025-52565), [CVE-2025-52881](https://nvd.nist.gov/vuln/detail/cve-2025-52881), [RHSA-2025:19610](https://access.redhat.com/errata/RHSA-2025:19610), [CVE-2025-11561](https://nvd.nist.gov/vuln/detail/cve-2025-11561), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:18297](https://access.redhat.com/errata/RHSA-2025:18297), [CVE-2023-53373](https://nvd.nist.gov/vuln/detail/cve-2023-53373), [CVE-2025-39751](https://nvd.nist.gov/vuln/detail/cve-2025-39751), [CVE-2025-39757](https://nvd.nist.gov/vuln/detail/cve-2025-39757), [RHSA-2025:19102](https://access.redhat.com/errata/RHSA-2025:19102), [CVE-2022-50386](https://nvd.nist.gov/vuln/detail/cve-2022-50386), [CVE-2023-53297](https://nvd.nist.gov/vuln/detail/cve-2023-53297), [CVE-2023-53386](https://nvd.nist.gov/vuln/detail/cve-2023-53386), [CVE-2025-39817](https://nvd.nist.gov/vuln/detail/cve-2025-39817), [CVE-2025-39841](https://nvd.nist.gov/vuln/detail/cve-2025-39841), [CVE-2025-39849](https://nvd.nist.gov/vuln/detail/cve-2025-39849), [RHSA-2025:19447](https://access.redhat.com/errata/RHSA-2025:19447), [CVE-2023-53226](https://nvd.nist.gov/vuln/detail/cve-2023-53226), [CVE-2023-53257](https://nvd.nist.gov/vuln/detail/cve-2023-53257), and [CVE-2025-39864](https://nvd.nist.gov/vuln/detail/cve-2025-39864).


Red Hat OpenShift 4.17.43
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-43_release-notes){: external}.


Red Hat CoreOS 4.17.43
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-43_release-notes){: external}.


HAProxy fbe9b8146f23bbd12b2566a79fa897d5981e7273
:   


## Master fix pack 4.17.42_1562_openshift, released 15 November 2025
{: #41742_1562_openshift_M}

The following list shows the changes that are in the master fix pack 4.17.42_1562_openshift. Master patch updates are applied automatically. 


Calico v3.29.6
:   See the [Calico release notes](https://archive-os-3-29.netlify.app/calico/3.29/release-notes/#calico-open-source-3296-bug-fix-release){: external}.
etcd v3.5.24
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.24){: external}.
{{site.data.keyword.cloud_notm}} Block Storage driver and plug-in v2.5.22
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} Controller Manager v1.30.14-16
:   New version contains updates and security fixes.
Key Management Service provider v2.10.18
:   New version contains updates and security fixes.
Portieris admission controller v0.13.31
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.31){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.17.42
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-42_release-notes){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit v4.17.0+20251015
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.17.0+20251015){: external}.
Tigera Operator v1.36.14
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.36.14){: external}.


## 06 November 2025, Worker node fix pack 4.17.42_1560_openshift
{: #cl-boms-41742_1560_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.42_1560_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-570.55.1.el9_6
:   Resolves the following CVEs: [RHSA-2025:17377](https://access.redhat.com/errata/RHSA-2025:17377), [CVE-2024-50301](https://nvd.nist.gov/vuln/detail/cve-2024-50301), [CVE-2025-38351](https://nvd.nist.gov/vuln/detail/cve-2025-38351), [CVE-2025-39761](https://nvd.nist.gov/vuln/detail/cve-2025-39761), [RHSA-2025:17760](https://access.redhat.com/errata/RHSA-2025:17760), [CVE-2023-53373](https://nvd.nist.gov/vuln/detail/cve-2023-53373), [CVE-2025-38556](https://nvd.nist.gov/vuln/detail/cve-2025-38556), [CVE-2025-38614](https://nvd.nist.gov/vuln/detail/cve-2025-38614), [CVE-2025-39757](https://nvd.nist.gov/vuln/detail/cve-2025-39757), [RHSA-2025:18281](https://access.redhat.com/errata/RHSA-2025:18281), [CVE-2022-50087](https://nvd.nist.gov/vuln/detail/cve-2022-50087), [CVE-2025-22026](https://nvd.nist.gov/vuln/detail/cve-2025-22026), [CVE-2025-38566](https://nvd.nist.gov/vuln/detail/cve-2025-38566), [CVE-2025-38571](https://nvd.nist.gov/vuln/detail/cve-2025-38571), [CVE-2025-39817](https://nvd.nist.gov/vuln/detail/cve-2025-39817), [CVE-2025-39841](https://nvd.nist.gov/vuln/detail/cve-2025-39841), and [CVE-2025-39849](https://nvd.nist.gov/vuln/detail/cve-2025-39849).


RHEL_8 4.18.0-553.79.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:17397](https://access.redhat.com/errata/RHSA-2025:17397), [CVE-2025-38527](https://nvd.nist.gov/vuln/detail/cve-2025-38527), [CVE-2025-39730](https://nvd.nist.gov/vuln/detail/cve-2025-39730), [RHSA-2025:17797](https://access.redhat.com/errata/RHSA-2025:17797), [CVE-2022-50228](https://nvd.nist.gov/vuln/detail/cve-2022-50228), [CVE-2023-53305](https://nvd.nist.gov/vuln/detail/cve-2023-53305), [RHSA-2025:18286](https://access.redhat.com/errata/RHSA-2025:18286), and [CVE-2025-5318](https://nvd.nist.gov/vuln/detail/cve-2025-5318).


Red Hat OpenShift 4.17.42
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-42_release-notes){: external}.


Red Hat CoreOS 4.17.42
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-42_release-notes){: external}.


HAProxy fbe9b8146f23bbd12b2566a79fa897d5981e7273
:   Resolves the following CVEs: [CVE-2025-5318](https://nvd.nist.gov/vuln/detail/cve-2025-5318).


## 21 October 2025, Worker node fix pack 4.17.41_1559_openshift
{: #cl-boms-41741_1559_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.41_1559_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-570.49.1.el9_6
:   Resolves the following CVEs: [RHSA-2025:10848](https://access.redhat.com/errata/RHSA-2025:10848), [CVE-2024-6174](https://nvd.nist.gov/vuln/detail/cve-2024-6174), [RHSA-2025:11462](https://access.redhat.com/errata/RHSA-2025:11462), [CVE-2024-50349](https://nvd.nist.gov/vuln/detail/cve-2024-50349), [CVE-2024-52006](https://nvd.nist.gov/vuln/detail/cve-2024-52006), [CVE-2025-27613](https://nvd.nist.gov/vuln/detail/cve-2025-27613), [CVE-2025-27614](https://nvd.nist.gov/vuln/detail/cve-2025-27614), [CVE-2025-46835](https://nvd.nist.gov/vuln/detail/cve-2025-46835), [CVE-2025-48384](https://nvd.nist.gov/vuln/detail/cve-2025-48384), [CVE-2025-48385](https://nvd.nist.gov/vuln/detail/cve-2025-48385), [RHSA-2025:10379](https://access.redhat.com/errata/RHSA-2025:10379), [CVE-2022-49846](https://nvd.nist.gov/vuln/detail/cve-2022-49846), [CVE-2025-21759](https://nvd.nist.gov/vuln/detail/cve-2025-21759), [CVE-2025-21887](https://nvd.nist.gov/vuln/detail/cve-2025-21887), [CVE-2025-22004](https://nvd.nist.gov/vuln/detail/cve-2025-22004), [CVE-2025-37799](https://nvd.nist.gov/vuln/detail/cve-2025-37799), [RHSA-2025:11411](https://access.redhat.com/errata/RHSA-2025:11411), [CVE-2024-58002](https://nvd.nist.gov/vuln/detail/cve-2024-58002), [CVE-2025-38089](https://nvd.nist.gov/vuln/detail/cve-2025-38089), [RHSA-2025:12746](https://access.redhat.com/errata/RHSA-2025:12746), [CVE-2022-49788](https://nvd.nist.gov/vuln/detail/cve-2022-49788), [CVE-2025-21727](https://nvd.nist.gov/vuln/detail/cve-2025-21727), [CVE-2025-21928](https://nvd.nist.gov/vuln/detail/cve-2025-21928), [CVE-2025-21929](https://nvd.nist.gov/vuln/detail/cve-2025-21929), [CVE-2025-21962](https://nvd.nist.gov/vuln/detail/cve-2025-21962), [CVE-2025-22020](https://nvd.nist.gov/vuln/detail/cve-2025-22020), [CVE-2025-37890](https://nvd.nist.gov/vuln/detail/cve-2025-37890), [CVE-2025-38052](https://nvd.nist.gov/vuln/detail/cve-2025-38052), [CVE-2025-38087](https://nvd.nist.gov/vuln/detail/cve-2025-38087), [RHSA-2025:13962](https://access.redhat.com/errata/RHSA-2025:13962), [CVE-2024-28956](https://nvd.nist.gov/vuln/detail/cve-2024-28956), [CVE-2025-21867](https://nvd.nist.gov/vuln/detail/cve-2025-21867), [CVE-2025-38084](https://nvd.nist.gov/vuln/detail/cve-2025-38084), [CVE-2025-38085](https://nvd.nist.gov/vuln/detail/cve-2025-38085), [CVE-2025-38124](https://nvd.nist.gov/vuln/detail/cve-2025-38124), [CVE-2025-38159](https://nvd.nist.gov/vuln/detail/cve-2025-38159), [CVE-2025-38250](https://nvd.nist.gov/vuln/detail/cve-2025-38250), [CVE-2025-38380](https://nvd.nist.gov/vuln/detail/cve-2025-38380), [CVE-2025-38471](https://nvd.nist.gov/vuln/detail/cve-2025-38471), [RHSA-2025:14420](https://access.redhat.com/errata/RHSA-2025:14420), [CVE-2025-22058](https://nvd.nist.gov/vuln/detail/cve-2025-22058), [CVE-2025-37914](https://nvd.nist.gov/vuln/detail/cve-2025-37914), [CVE-2025-38417](https://nvd.nist.gov/vuln/detail/cve-2025-38417), [RHSA-2025:15011](https://access.redhat.com/errata/RHSA-2025:15011), [CVE-2025-37823](https://nvd.nist.gov/vuln/detail/cve-2025-37823), [CVE-2025-38200](https://nvd.nist.gov/vuln/detail/cve-2025-38200), [CVE-2025-38211](https://nvd.nist.gov/vuln/detail/cve-2025-38211), [CVE-2025-38350](https://nvd.nist.gov/vuln/detail/cve-2025-38350), [CVE-2025-38461](https://nvd.nist.gov/vuln/detail/cve-2025-38461), [CVE-2025-38464](https://nvd.nist.gov/vuln/detail/cve-2025-38464), [CVE-2025-38500](https://nvd.nist.gov/vuln/detail/cve-2025-38500), [CVE-2025-38684](https://nvd.nist.gov/vuln/detail/cve-2025-38684), [RHSA-2025:15429](https://access.redhat.com/errata/RHSA-2025:15429), [CVE-2025-37803](https://nvd.nist.gov/vuln/detail/cve-2025-37803), [CVE-2025-38392](https://nvd.nist.gov/vuln/detail/cve-2025-38392), [CVE-2025-39825](https://nvd.nist.gov/vuln/detail/cve-2025-39825), [RHSA-2025:15661](https://access.redhat.com/errata/RHSA-2025:15661), [CVE-2025-22097](https://nvd.nist.gov/vuln/detail/cve-2025-22097), [CVE-2025-38332](https://nvd.nist.gov/vuln/detail/cve-2025-38332), [CVE-2025-38352](https://nvd.nist.gov/vuln/detail/cve-2025-38352), [CVE-2025-38449](https://nvd.nist.gov/vuln/detail/cve-2025-38449), [RHSA-2025:7423](https://access.redhat.com/errata/RHSA-2025:7423), [CVE-2024-58005](https://nvd.nist.gov/vuln/detail/cve-2024-58005), [CVE-2024-58007](https://nvd.nist.gov/vuln/detail/cve-2024-58007), [CVE-2024-58069](https://nvd.nist.gov/vuln/detail/cve-2024-58069), [CVE-2025-21633](https://nvd.nist.gov/vuln/detail/cve-2025-21633), [CVE-2025-21927](https://nvd.nist.gov/vuln/detail/cve-2025-21927), [CVE-2025-21993](https://nvd.nist.gov/vuln/detail/cve-2025-21993), [RHSA-2025:7903](https://access.redhat.com/errata/RHSA-2025:7903), [CVE-2025-21756](https://nvd.nist.gov/vuln/detail/cve-2025-21756), [CVE-2025-21966](https://nvd.nist.gov/vuln/detail/cve-2025-21966), [CVE-2025-37749](https://nvd.nist.gov/vuln/detail/cve-2025-37749), [RHSA-2025:8643](https://access.redhat.com/errata/RHSA-2025:8643), [CVE-2025-21920](https://nvd.nist.gov/vuln/detail/cve-2025-21920), [CVE-2025-21926](https://nvd.nist.gov/vuln/detail/cve-2025-21926), [CVE-2025-21997](https://nvd.nist.gov/vuln/detail/cve-2025-21997), [CVE-2025-22055](https://nvd.nist.gov/vuln/detail/cve-2025-22055), [CVE-2025-37785](https://nvd.nist.gov/vuln/detail/cve-2025-37785), [CVE-2025-37943](https://nvd.nist.gov/vuln/detail/cve-2025-37943), [RHSA-2025:9080](https://access.redhat.com/errata/RHSA-2025:9080), [CVE-2025-21961](https://nvd.nist.gov/vuln/detail/cve-2025-21961), [CVE-2025-21963](https://nvd.nist.gov/vuln/detail/cve-2025-21963), [CVE-2025-21969](https://nvd.nist.gov/vuln/detail/cve-2025-21969), [CVE-2025-21979](https://nvd.nist.gov/vuln/detail/cve-2025-21979), [CVE-2025-21999](https://nvd.nist.gov/vuln/detail/cve-2025-21999), [CVE-2025-22126](https://nvd.nist.gov/vuln/detail/cve-2025-22126), [CVE-2025-37750](https://nvd.nist.gov/vuln/detail/cve-2025-37750), [RHSA-2025:14130](https://access.redhat.com/errata/RHSA-2025:14130), [CVE-2025-5914](https://nvd.nist.gov/vuln/detail/cve-2025-5914), [RHSA-2025:10699](https://access.redhat.com/errata/RHSA-2025:10699), [CVE-2025-49794](https://nvd.nist.gov/vuln/detail/cve-2025-49794), [CVE-2025-49796](https://nvd.nist.gov/vuln/detail/cve-2025-49796), [CVE-2025-6021](https://nvd.nist.gov/vuln/detail/cve-2025-6021), [RHSA-2025:12447](https://access.redhat.com/errata/RHSA-2025:12447), [CVE-2025-7425](https://nvd.nist.gov/vuln/detail/cve-2025-7425), [RHSA-2025:15099](https://access.redhat.com/errata/RHSA-2025:15099), [CVE-2025-6020](https://nvd.nist.gov/vuln/detail/cve-2025-6020), [CVE-2025-8941](https://nvd.nist.gov/vuln/detail/cve-2025-8941), [RHSA-2025:9526](https://access.redhat.com/errata/RHSA-2025:9526), [CVE-2025-6020](https://nvd.nist.gov/vuln/detail/cve-2025-6020), [RHSA-2025:10136](https://access.redhat.com/errata/RHSA-2025:10136), [CVE-2024-12718](https://nvd.nist.gov/vuln/detail/cve-2024-12718), [CVE-2025-4138](https://nvd.nist.gov/vuln/detail/cve-2025-4138), [CVE-2025-4330](https://nvd.nist.gov/vuln/detail/cve-2025-4330), [CVE-2025-4435](https://nvd.nist.gov/vuln/detail/cve-2025-4435), [CVE-2025-4517](https://nvd.nist.gov/vuln/detail/cve-2025-4517), [RHSA-2025:11992](https://access.redhat.com/errata/RHSA-2025:11992), [CVE-2025-6965](https://nvd.nist.gov/vuln/detail/cve-2025-6965), [RHSA-2025:9978](https://access.redhat.com/errata/RHSA-2025:9978), [CVE-2025-32462](https://nvd.nist.gov/vuln/detail/cve-2025-32462), [CVE-2024-36350](https://nvd.nist.gov/vuln/detail/cve-2024-36350), [CVE-2024-36357](https://nvd.nist.gov/vuln/detail/cve-2024-36357), [RHSA-2025:12876](https://access.redhat.com/errata/RHSA-2025:12876), [CVE-2022-29458](https://nvd.nist.gov/vuln/detail/cve-2022-29458), [RHSA-2025:7440](https://access.redhat.com/errata/RHSA-2025:7440), [CVE-2023-4752](https://nvd.nist.gov/vuln/detail/cve-2023-4752), [CVE-2024-28956](https://nvd.nist.gov/vuln/detail/cve-2024-28956), [CVE-2024-43420](https://nvd.nist.gov/vuln/detail/cve-2024-43420), [CVE-2024-45332](https://nvd.nist.gov/vuln/detail/cve-2024-45332), [CVE-2025-20012](https://nvd.nist.gov/vuln/detail/cve-2025-20012), [CVE-2025-20623](https://nvd.nist.gov/vuln/detail/cve-2025-20623), [CVE-2025-24495](https://nvd.nist.gov/vuln/detail/cve-2025-24495), [RHSA-2025:7444](https://access.redhat.com/errata/RHSA-2025:7444), [CVE-2024-8176](https://nvd.nist.gov/vuln/detail/cve-2024-8176), [RHSA-2025:7409](https://access.redhat.com/errata/RHSA-2025:7409), [CVE-2024-52005](https://nvd.nist.gov/vuln/detail/cve-2024-52005), [RHSA-2025:11140](https://access.redhat.com/errata/RHSA-2025:11140), [CVE-2024-52533](https://nvd.nist.gov/vuln/detail/cve-2024-52533), [CVE-2025-4373](https://nvd.nist.gov/vuln/detail/cve-2025-4373), [RHSA-2025:12748](https://access.redhat.com/errata/RHSA-2025:12748), [CVE-2025-8058](https://nvd.nist.gov/vuln/detail/cve-2025-8058), [RHSA-2025:8655](https://access.redhat.com/errata/RHSA-2025:8655), [CVE-2025-4802](https://nvd.nist.gov/vuln/detail/cve-2025-4802), [RHSA-2025:9877](https://access.redhat.com/errata/RHSA-2025:9877), [CVE-2025-5702](https://nvd.nist.gov/vuln/detail/cve-2025-5702), [RHSA-2025:7076](https://access.redhat.com/errata/RHSA-2025:7076), [CVE-2024-12243](https://nvd.nist.gov/vuln/detail/cve-2024-12243), [RHSA-2025:16116](https://access.redhat.com/errata/RHSA-2025:16116), [CVE-2025-32988](https://nvd.nist.gov/vuln/detail/cve-2025-32988), [CVE-2025-32989](https://nvd.nist.gov/vuln/detail/cve-2025-32989), [CVE-2025-32990](https://nvd.nist.gov/vuln/detail/cve-2025-32990), [CVE-2025-6395](https://nvd.nist.gov/vuln/detail/cve-2025-6395), [RHSA-2025:6990](https://access.redhat.com/errata/RHSA-2025:6990), [CVE-2024-45774](https://nvd.nist.gov/vuln/detail/cve-2024-45774), [CVE-2024-45775](https://nvd.nist.gov/vuln/detail/cve-2024-45775), [CVE-2024-45776](https://nvd.nist.gov/vuln/detail/cve-2024-45776), [CVE-2024-45781](https://nvd.nist.gov/vuln/detail/cve-2024-45781), [CVE-2024-45783](https://nvd.nist.gov/vuln/detail/cve-2024-45783), [CVE-2025-0622](https://nvd.nist.gov/vuln/detail/cve-2025-0622), [CVE-2025-0677](https://nvd.nist.gov/vuln/detail/cve-2025-0677), [CVE-2025-0690](https://nvd.nist.gov/vuln/detail/cve-2025-0690), [RHSA-2025:17558](https://access.redhat.com/errata/RHSA-2025:17558), [CVE-2025-48964](https://nvd.nist.gov/vuln/detail/cve-2025-48964), [RHSA-2025:9432](https://access.redhat.com/errata/RHSA-2025:9432), [CVE-2025-47268](https://nvd.nist.gov/vuln/detail/cve-2025-47268), [RHSA-2025:10585](https://access.redhat.com/errata/RHSA-2025:10585), [CVE-2024-23337](https://nvd.nist.gov/vuln/detail/cve-2024-23337), [CVE-2025-48060](https://nvd.nist.gov/vuln/detail/cve-2025-48060), [RHSA-2025:10837](https://access.redhat.com/errata/RHSA-2025:10837), [CVE-2025-21991](https://nvd.nist.gov/vuln/detail/cve-2025-21991), [RHSA-2025:11861](https://access.redhat.com/errata/RHSA-2025:11861), [CVE-2024-57980](https://nvd.nist.gov/vuln/detail/cve-2024-57980), [CVE-2025-21905](https://nvd.nist.gov/vuln/detail/cve-2025-21905), [CVE-2025-22085](https://nvd.nist.gov/vuln/detail/cve-2025-22085), [CVE-2025-22091](https://nvd.nist.gov/vuln/detail/cve-2025-22091), [CVE-2025-22113](https://nvd.nist.gov/vuln/detail/cve-2025-22113), [CVE-2025-22121](https://nvd.nist.gov/vuln/detail/cve-2025-22121), [CVE-2025-37797](https://nvd.nist.gov/vuln/detail/cve-2025-37797), [CVE-2025-37958](https://nvd.nist.gov/vuln/detail/cve-2025-37958), [CVE-2025-38086](https://nvd.nist.gov/vuln/detail/cve-2025-38086), [CVE-2025-38110](https://nvd.nist.gov/vuln/detail/cve-2025-38110), [RHSA-2025:13602](https://access.redhat.com/errata/RHSA-2025:13602), [CVE-2025-38079](https://nvd.nist.gov/vuln/detail/cve-2025-38079), [CVE-2025-38292](https://nvd.nist.gov/vuln/detail/cve-2025-38292), [RHSA-2025:15740](https://access.redhat.com/errata/RHSA-2025:15740), [CVE-2025-38550](https://nvd.nist.gov/vuln/detail/cve-2025-38550), [RHSA-2025:16398](https://access.redhat.com/errata/RHSA-2025:16398), [CVE-2023-53125](https://nvd.nist.gov/vuln/detail/cve-2023-53125), [CVE-2025-37810](https://nvd.nist.gov/vuln/detail/cve-2025-37810), [CVE-2025-38498](https://nvd.nist.gov/vuln/detail/cve-2025-38498), [CVE-2025-39694](https://nvd.nist.gov/vuln/detail/cve-2025-39694), [RHSA-2025:16880](https://access.redhat.com/errata/RHSA-2025:16880), [CVE-2025-38472](https://nvd.nist.gov/vuln/detail/cve-2025-38472), [CVE-2025-38527](https://nvd.nist.gov/vuln/detail/cve-2025-38527), [CVE-2025-38718](https://nvd.nist.gov/vuln/detail/cve-2025-38718), [CVE-2025-39682](https://nvd.nist.gov/vuln/detail/cve-2025-39682), [CVE-2025-39698](https://nvd.nist.gov/vuln/detail/cve-2025-39698), [RHSA-2025:17377](https://access.redhat.com/errata/RHSA-2025:17377), [CVE-2024-50301](https://nvd.nist.gov/vuln/detail/cve-2024-50301), [CVE-2025-38351](https://nvd.nist.gov/vuln/detail/cve-2025-38351), [CVE-2025-39761](https://nvd.nist.gov/vuln/detail/cve-2025-39761), [RHSA-2025:17760](https://access.redhat.com/errata/RHSA-2025:17760), [CVE-2023-53373](https://nvd.nist.gov/vuln/detail/cve-2023-53373), [CVE-2025-38556](https://nvd.nist.gov/vuln/detail/cve-2025-38556), [CVE-2025-38614](https://nvd.nist.gov/vuln/detail/cve-2025-38614), [CVE-2025-39757](https://nvd.nist.gov/vuln/detail/cve-2025-39757), [RHSA-2025:6966](https://access.redhat.com/errata/RHSA-2025:6966), [CVE-2022-48969](https://nvd.nist.gov/vuln/detail/cve-2022-48969), [CVE-2022-48989](https://nvd.nist.gov/vuln/detail/cve-2022-48989), [CVE-2022-49006](https://nvd.nist.gov/vuln/detail/cve-2022-49006), [CVE-2022-49014](https://nvd.nist.gov/vuln/detail/cve-2022-49014), [CVE-2022-49029](https://nvd.nist.gov/vuln/detail/cve-2022-49029), [CVE-2022-49778](https://nvd.nist.gov/vuln/detail/cve-2022-49778), [CVE-2022-49804](https://nvd.nist.gov/vuln/detail/cve-2022-49804), [CVE-2022-49815](https://nvd.nist.gov/vuln/detail/cve-2022-49815), [CVE-2022-50112](https://nvd.nist.gov/vuln/detail/cve-2022-50112), [CVE-2022-50159](https://nvd.nist.gov/vuln/detail/cve-2022-50159), [CVE-2022-50214](https://nvd.nist.gov/vuln/detail/cve-2022-50214), [CVE-2022-50511](https://nvd.nist.gov/vuln/detail/cve-2022-50511), [CVE-2023-52672](https://nvd.nist.gov/vuln/detail/cve-2023-52672), [CVE-2023-52917](https://nvd.nist.gov/vuln/detail/cve-2023-52917), [CVE-2023-53066](https://nvd.nist.gov/vuln/detail/cve-2023-53066), [CVE-2023-53117](https://nvd.nist.gov/vuln/detail/cve-2023-53117), [CVE-2023-53196](https://nvd.nist.gov/vuln/detail/cve-2023-53196), [CVE-2023-53260](https://nvd.nist.gov/vuln/detail/cve-2023-53260), [CVE-2023-53261](https://nvd.nist.gov/vuln/detail/cve-2023-53261), [CVE-2023-53595](https://nvd.nist.gov/vuln/detail/cve-2023-53595), [CVE-2024-27008](https://nvd.nist.gov/vuln/detail/cve-2024-27008), [CVE-2024-27398](https://nvd.nist.gov/vuln/detail/cve-2024-27398), [CVE-2024-35891](https://nvd.nist.gov/vuln/detail/cve-2024-35891), [CVE-2024-35933](https://nvd.nist.gov/vuln/detail/cve-2024-35933), [CVE-2024-35934](https://nvd.nist.gov/vuln/detail/cve-2024-35934), [CVE-2024-35963](https://nvd.nist.gov/vuln/detail/cve-2024-35963), [CVE-2024-35964](https://nvd.nist.gov/vuln/detail/cve-2024-35964), [CVE-2024-35965](https://nvd.nist.gov/vuln/detail/cve-2024-35965), [CVE-2024-35966](https://nvd.nist.gov/vuln/detail/cve-2024-35966), [CVE-2024-35967](https://nvd.nist.gov/vuln/detail/cve-2024-35967), [CVE-2024-35978](https://nvd.nist.gov/vuln/detail/cve-2024-35978), [CVE-2024-36011](https://nvd.nist.gov/vuln/detail/cve-2024-36011), [CVE-2024-36012](https://nvd.nist.gov/vuln/detail/cve-2024-36012), [CVE-2024-36013](https://nvd.nist.gov/vuln/detail/cve-2024-36013), [CVE-2024-36880](https://nvd.nist.gov/vuln/detail/cve-2024-36880), [CVE-2024-36968](https://nvd.nist.gov/vuln/detail/cve-2024-36968), [CVE-2024-38541](https://nvd.nist.gov/vuln/detail/cve-2024-38541), [CVE-2024-39500](https://nvd.nist.gov/vuln/detail/cve-2024-39500), [CVE-2024-40956](https://nvd.nist.gov/vuln/detail/cve-2024-40956), [CVE-2024-41010](https://nvd.nist.gov/vuln/detail/cve-2024-41010), [CVE-2024-41062](https://nvd.nist.gov/vuln/detail/cve-2024-41062), [CVE-2024-42094](https://nvd.nist.gov/vuln/detail/cve-2024-42094), [CVE-2024-42133](https://nvd.nist.gov/vuln/detail/cve-2024-42133), [CVE-2024-42253](https://nvd.nist.gov/vuln/detail/cve-2024-42253), [CVE-2024-42265](https://nvd.nist.gov/vuln/detail/cve-2024-42265), [CVE-2024-42278](https://nvd.nist.gov/vuln/detail/cve-2024-42278), [CVE-2024-42291](https://nvd.nist.gov/vuln/detail/cve-2024-42291), [CVE-2024-42294](https://nvd.nist.gov/vuln/detail/cve-2024-42294), [CVE-2024-42302](https://nvd.nist.gov/vuln/detail/cve-2024-42302), [CVE-2024-42304](https://nvd.nist.gov/vuln/detail/cve-2024-42304), [CVE-2024-42305](https://nvd.nist.gov/vuln/detail/cve-2024-42305), [CVE-2024-42312](https://nvd.nist.gov/vuln/detail/cve-2024-42312), [CVE-2024-42315](https://nvd.nist.gov/vuln/detail/cve-2024-42315), [CVE-2024-42316](https://nvd.nist.gov/vuln/detail/cve-2024-42316), [CVE-2024-42321](https://nvd.nist.gov/vuln/detail/cve-2024-42321), [CVE-2024-43820](https://nvd.nist.gov/vuln/detail/cve-2024-43820), [CVE-2024-43821](https://nvd.nist.gov/vuln/detail/cve-2024-43821), [CVE-2024-43823](https://nvd.nist.gov/vuln/detail/cve-2024-43823), [CVE-2024-43828](https://nvd.nist.gov/vuln/detail/cve-2024-43828), [CVE-2024-43834](https://nvd.nist.gov/vuln/detail/cve-2024-43834), [CVE-2024-43846](https://nvd.nist.gov/vuln/detail/cve-2024-43846), [CVE-2024-43853](https://nvd.nist.gov/vuln/detail/cve-2024-43853), [CVE-2024-43871](https://nvd.nist.gov/vuln/detail/cve-2024-43871), [CVE-2024-43873](https://nvd.nist.gov/vuln/detail/cve-2024-43873), [CVE-2024-43882](https://nvd.nist.gov/vuln/detail/cve-2024-43882), [CVE-2024-43884](https://nvd.nist.gov/vuln/detail/cve-2024-43884), [CVE-2024-43889](https://nvd.nist.gov/vuln/detail/cve-2024-43889), [CVE-2024-43898](https://nvd.nist.gov/vuln/detail/cve-2024-43898), [CVE-2024-43910](https://nvd.nist.gov/vuln/detail/cve-2024-43910), [CVE-2024-43914](https://nvd.nist.gov/vuln/detail/cve-2024-43914), [CVE-2024-44931](https://nvd.nist.gov/vuln/detail/cve-2024-44931), [CVE-2024-44932](https://nvd.nist.gov/vuln/detail/cve-2024-44932), [CVE-2024-44934](https://nvd.nist.gov/vuln/detail/cve-2024-44934), [CVE-2024-44952](https://nvd.nist.gov/vuln/detail/cve-2024-44952), [CVE-2024-44958](https://nvd.nist.gov/vuln/detail/cve-2024-44958), [CVE-2024-44964](https://nvd.nist.gov/vuln/detail/cve-2024-44964), [CVE-2024-44975](https://nvd.nist.gov/vuln/detail/cve-2024-44975), [CVE-2024-44987](https://nvd.nist.gov/vuln/detail/cve-2024-44987), [CVE-2024-44989](https://nvd.nist.gov/vuln/detail/cve-2024-44989), [CVE-2024-45000](https://nvd.nist.gov/vuln/detail/cve-2024-45000), [CVE-2024-45009](https://nvd.nist.gov/vuln/detail/cve-2024-45009), [CVE-2024-45010](https://nvd.nist.gov/vuln/detail/cve-2024-45010), [CVE-2024-45016](https://nvd.nist.gov/vuln/detail/cve-2024-45016), [CVE-2024-45022](https://nvd.nist.gov/vuln/detail/cve-2024-45022), [CVE-2024-46673](https://nvd.nist.gov/vuln/detail/cve-2024-46673), [CVE-2024-46675](https://nvd.nist.gov/vuln/detail/cve-2024-46675), [CVE-2024-46711](https://nvd.nist.gov/vuln/detail/cve-2024-46711), [CVE-2024-46722](https://nvd.nist.gov/vuln/detail/cve-2024-46722), [CVE-2024-46723](https://nvd.nist.gov/vuln/detail/cve-2024-46723), [CVE-2024-46724](https://nvd.nist.gov/vuln/detail/cve-2024-46724), [CVE-2024-46725](https://nvd.nist.gov/vuln/detail/cve-2024-46725), [CVE-2024-46743](https://nvd.nist.gov/vuln/detail/cve-2024-46743), [CVE-2024-46745](https://nvd.nist.gov/vuln/detail/cve-2024-46745), [CVE-2024-46747](https://nvd.nist.gov/vuln/detail/cve-2024-46747), [CVE-2024-46750](https://nvd.nist.gov/vuln/detail/cve-2024-46750), [CVE-2024-46754](https://nvd.nist.gov/vuln/detail/cve-2024-46754), [CVE-2024-46756](https://nvd.nist.gov/vuln/detail/cve-2024-46756), [CVE-2024-46758](https://nvd.nist.gov/vuln/detail/cve-2024-46758), [CVE-2024-46759](https://nvd.nist.gov/vuln/detail/cve-2024-46759), [CVE-2024-46761](https://nvd.nist.gov/vuln/detail/cve-2024-46761), [CVE-2024-46783](https://nvd.nist.gov/vuln/detail/cve-2024-46783), [CVE-2024-46786](https://nvd.nist.gov/vuln/detail/cve-2024-46786), [CVE-2024-46787](https://nvd.nist.gov/vuln/detail/cve-2024-46787), [CVE-2024-46800](https://nvd.nist.gov/vuln/detail/cve-2024-46800), [CVE-2024-46805](https://nvd.nist.gov/vuln/detail/cve-2024-46805), [CVE-2024-46806](https://nvd.nist.gov/vuln/detail/cve-2024-46806), [CVE-2024-46807](https://nvd.nist.gov/vuln/detail/cve-2024-46807), [CVE-2024-46819](https://nvd.nist.gov/vuln/detail/cve-2024-46819), [CVE-2024-46820](https://nvd.nist.gov/vuln/detail/cve-2024-46820), [CVE-2024-46822](https://nvd.nist.gov/vuln/detail/cve-2024-46822), [CVE-2024-46828](https://nvd.nist.gov/vuln/detail/cve-2024-46828), [CVE-2024-46835](https://nvd.nist.gov/vuln/detail/cve-2024-46835), [CVE-2024-46839](https://nvd.nist.gov/vuln/detail/cve-2024-46839), [CVE-2024-46853](https://nvd.nist.gov/vuln/detail/cve-2024-46853), [CVE-2024-46864](https://nvd.nist.gov/vuln/detail/cve-2024-46864), [CVE-2024-46871](https://nvd.nist.gov/vuln/detail/cve-2024-46871), [CVE-2024-47141](https://nvd.nist.gov/vuln/detail/cve-2024-47141), [CVE-2024-47660](https://nvd.nist.gov/vuln/detail/cve-2024-47660), [CVE-2024-47668](https://nvd.nist.gov/vuln/detail/cve-2024-47668), [CVE-2024-47678](https://nvd.nist.gov/vuln/detail/cve-2024-47678), [CVE-2024-47685](https://nvd.nist.gov/vuln/detail/cve-2024-47685), [CVE-2024-47687](https://nvd.nist.gov/vuln/detail/cve-2024-47687), [CVE-2024-47692](https://nvd.nist.gov/vuln/detail/cve-2024-47692), [CVE-2024-47700](https://nvd.nist.gov/vuln/detail/cve-2024-47700), [CVE-2024-47703](https://nvd.nist.gov/vuln/detail/cve-2024-47703), [CVE-2024-47705](https://nvd.nist.gov/vuln/detail/cve-2024-47705), [CVE-2024-47706](https://nvd.nist.gov/vuln/detail/cve-2024-47706), [CVE-2024-47710](https://nvd.nist.gov/vuln/detail/cve-2024-47710), [CVE-2024-47713](https://nvd.nist.gov/vuln/detail/cve-2024-47713), [CVE-2024-47715](https://nvd.nist.gov/vuln/detail/cve-2024-47715), [CVE-2024-47718](https://nvd.nist.gov/vuln/detail/cve-2024-47718), [CVE-2024-47719](https://nvd.nist.gov/vuln/detail/cve-2024-47719), [CVE-2024-47737](https://nvd.nist.gov/vuln/detail/cve-2024-47737), [CVE-2024-47738](https://nvd.nist.gov/vuln/detail/cve-2024-47738), [CVE-2024-47739](https://nvd.nist.gov/vuln/detail/cve-2024-47739), [CVE-2024-47745](https://nvd.nist.gov/vuln/detail/cve-2024-47745), [CVE-2024-47748](https://nvd.nist.gov/vuln/detail/cve-2024-47748), [CVE-2024-48873](https://nvd.nist.gov/vuln/detail/cve-2024-48873), [CVE-2024-49569](https://nvd.nist.gov/vuln/detail/cve-2024-49569), [CVE-2024-49851](https://nvd.nist.gov/vuln/detail/cve-2024-49851), [CVE-2024-49856](https://nvd.nist.gov/vuln/detail/cve-2024-49856), [CVE-2024-49860](https://nvd.nist.gov/vuln/detail/cve-2024-49860), [CVE-2024-49862](https://nvd.nist.gov/vuln/detail/cve-2024-49862), [CVE-2024-49870](https://nvd.nist.gov/vuln/detail/cve-2024-49870), [CVE-2024-49875](https://nvd.nist.gov/vuln/detail/cve-2024-49875), [CVE-2024-49878](https://nvd.nist.gov/vuln/detail/cve-2024-49878), [CVE-2024-49881](https://nvd.nist.gov/vuln/detail/cve-2024-49881), [CVE-2024-49882](https://nvd.nist.gov/vuln/detail/cve-2024-49882), [CVE-2024-49883](https://nvd.nist.gov/vuln/detail/cve-2024-49883), [CVE-2024-49884](https://nvd.nist.gov/vuln/detail/cve-2024-49884), [CVE-2024-49885](https://nvd.nist.gov/vuln/detail/cve-2024-49885), [CVE-2024-49886](https://nvd.nist.gov/vuln/detail/cve-2024-49886), [CVE-2024-49889](https://nvd.nist.gov/vuln/detail/cve-2024-49889), [CVE-2024-49904](https://nvd.nist.gov/vuln/detail/cve-2024-49904), [CVE-2024-49927](https://nvd.nist.gov/vuln/detail/cve-2024-49927), [CVE-2024-49928](https://nvd.nist.gov/vuln/detail/cve-2024-49928), [CVE-2024-49929](https://nvd.nist.gov/vuln/detail/cve-2024-49929), [CVE-2024-49930](https://nvd.nist.gov/vuln/detail/cve-2024-49930), [CVE-2024-49933](https://nvd.nist.gov/vuln/detail/cve-2024-49933), [CVE-2024-49934](https://nvd.nist.gov/vuln/detail/cve-2024-49934), [CVE-2024-49935](https://nvd.nist.gov/vuln/detail/cve-2024-49935), [CVE-2024-49937](https://nvd.nist.gov/vuln/detail/cve-2024-49937), [CVE-2024-49938](https://nvd.nist.gov/vuln/detail/cve-2024-49938), [CVE-2024-49939](https://nvd.nist.gov/vuln/detail/cve-2024-49939), [CVE-2024-49946](https://nvd.nist.gov/vuln/detail/cve-2024-49946), [CVE-2024-49948](https://nvd.nist.gov/vuln/detail/cve-2024-49948), [CVE-2024-49950](https://nvd.nist.gov/vuln/detail/cve-2024-49950), [CVE-2024-49951](https://nvd.nist.gov/vuln/detail/cve-2024-49951), [CVE-2024-49954](https://nvd.nist.gov/vuln/detail/cve-2024-49954), [CVE-2024-49959](https://nvd.nist.gov/vuln/detail/cve-2024-49959), [CVE-2024-49960](https://nvd.nist.gov/vuln/detail/cve-2024-49960), [CVE-2024-49962](https://nvd.nist.gov/vuln/detail/cve-2024-49962), [CVE-2024-49967](https://nvd.nist.gov/vuln/detail/cve-2024-49967), [CVE-2024-49968](https://nvd.nist.gov/vuln/detail/cve-2024-49968), [CVE-2024-49971](https://nvd.nist.gov/vuln/detail/cve-2024-49971), [CVE-2024-49973](https://nvd.nist.gov/vuln/detail/cve-2024-49973), [CVE-2024-49974](https://nvd.nist.gov/vuln/detail/cve-2024-49974), [CVE-2024-49975](https://nvd.nist.gov/vuln/detail/cve-2024-49975), [CVE-2024-49977](https://nvd.nist.gov/vuln/detail/cve-2024-49977), [CVE-2024-49983](https://nvd.nist.gov/vuln/detail/cve-2024-49983), [CVE-2024-49991](https://nvd.nist.gov/vuln/detail/cve-2024-49991), [CVE-2024-49993](https://nvd.nist.gov/vuln/detail/cve-2024-49993), [CVE-2024-49994](https://nvd.nist.gov/vuln/detail/cve-2024-49994), [CVE-2024-49995](https://nvd.nist.gov/vuln/detail/cve-2024-49995), [CVE-2024-49999](https://nvd.nist.gov/vuln/detail/cve-2024-49999), [CVE-2024-50002](https://nvd.nist.gov/vuln/detail/cve-2024-50002), [CVE-2024-50006](https://nvd.nist.gov/vuln/detail/cve-2024-50006), [CVE-2024-50008](https://nvd.nist.gov/vuln/detail/cve-2024-50008), [CVE-2024-50009](https://nvd.nist.gov/vuln/detail/cve-2024-50009), [CVE-2024-50013](https://nvd.nist.gov/vuln/detail/cve-2024-50013), [CVE-2024-50014](https://nvd.nist.gov/vuln/detail/cve-2024-50014), [CVE-2024-50015](https://nvd.nist.gov/vuln/detail/cve-2024-50015), [CVE-2024-50018](https://nvd.nist.gov/vuln/detail/cve-2024-50018), [CVE-2024-50019](https://nvd.nist.gov/vuln/detail/cve-2024-50019), [CVE-2024-50022](https://nvd.nist.gov/vuln/detail/cve-2024-50022), [CVE-2024-50023](https://nvd.nist.gov/vuln/detail/cve-2024-50023), [CVE-2024-50024](https://nvd.nist.gov/vuln/detail/cve-2024-50024), [CVE-2024-50027](https://nvd.nist.gov/vuln/detail/cve-2024-50027), [CVE-2024-50028](https://nvd.nist.gov/vuln/detail/cve-2024-50028), [CVE-2024-50029](https://nvd.nist.gov/vuln/detail/cve-2024-50029), [CVE-2024-50033](https://nvd.nist.gov/vuln/detail/cve-2024-50033), [CVE-2024-50035](https://nvd.nist.gov/vuln/detail/cve-2024-50035), [CVE-2024-50038](https://nvd.nist.gov/vuln/detail/cve-2024-50038), [CVE-2024-50039](https://nvd.nist.gov/vuln/detail/cve-2024-50039), [CVE-2024-50044](https://nvd.nist.gov/vuln/detail/cve-2024-50044), [CVE-2024-50046](https://nvd.nist.gov/vuln/detail/cve-2024-50046), [CVE-2024-50047](https://nvd.nist.gov/vuln/detail/cve-2024-50047), [CVE-2024-50055](https://nvd.nist.gov/vuln/detail/cve-2024-50055), [CVE-2024-50057](https://nvd.nist.gov/vuln/detail/cve-2024-50057), [CVE-2024-50058](https://nvd.nist.gov/vuln/detail/cve-2024-50058), [CVE-2024-50064](https://nvd.nist.gov/vuln/detail/cve-2024-50064), [CVE-2024-50067](https://nvd.nist.gov/vuln/detail/cve-2024-50067), [CVE-2024-50073](https://nvd.nist.gov/vuln/detail/cve-2024-50073), [CVE-2024-50074](https://nvd.nist.gov/vuln/detail/cve-2024-50074), [CVE-2024-50075](https://nvd.nist.gov/vuln/detail/cve-2024-50075), [CVE-2024-50077](https://nvd.nist.gov/vuln/detail/cve-2024-50077), [CVE-2024-50078](https://nvd.nist.gov/vuln/detail/cve-2024-50078), [CVE-2024-50081](https://nvd.nist.gov/vuln/detail/cve-2024-50081), [CVE-2024-50082](https://nvd.nist.gov/vuln/detail/cve-2024-50082), [CVE-2024-50093](https://nvd.nist.gov/vuln/detail/cve-2024-50093), [CVE-2024-50101](https://nvd.nist.gov/vuln/detail/cve-2024-50101), [CVE-2024-50102](https://nvd.nist.gov/vuln/detail/cve-2024-50102), [CVE-2024-50106](https://nvd.nist.gov/vuln/detail/cve-2024-50106), [CVE-2024-50107](https://nvd.nist.gov/vuln/detail/cve-2024-50107), [CVE-2024-50109](https://nvd.nist.gov/vuln/detail/cve-2024-50109), [CVE-2024-50117](https://nvd.nist.gov/vuln/detail/cve-2024-50117), [CVE-2024-50120](https://nvd.nist.gov/vuln/detail/cve-2024-50120), [CVE-2024-50121](https://nvd.nist.gov/vuln/detail/cve-2024-50121), [CVE-2024-50126](https://nvd.nist.gov/vuln/detail/cve-2024-50126), [CVE-2024-50127](https://nvd.nist.gov/vuln/detail/cve-2024-50127), [CVE-2024-50128](https://nvd.nist.gov/vuln/detail/cve-2024-50128), [CVE-2024-50130](https://nvd.nist.gov/vuln/detail/cve-2024-50130), [CVE-2024-50141](https://nvd.nist.gov/vuln/detail/cve-2024-50141), [CVE-2024-50143](https://nvd.nist.gov/vuln/detail/cve-2024-50143), [CVE-2024-50150](https://nvd.nist.gov/vuln/detail/cve-2024-50150), [CVE-2024-50151](https://nvd.nist.gov/vuln/detail/cve-2024-50151), [CVE-2024-50152](https://nvd.nist.gov/vuln/detail/cve-2024-50152), [CVE-2024-50153](https://nvd.nist.gov/vuln/detail/cve-2024-50153), [CVE-2024-50162](https://nvd.nist.gov/vuln/detail/cve-2024-50162), [CVE-2024-50163](https://nvd.nist.gov/vuln/detail/cve-2024-50163), [CVE-2024-50169](https://nvd.nist.gov/vuln/detail/cve-2024-50169), [CVE-2024-50182](https://nvd.nist.gov/vuln/detail/cve-2024-50182), [CVE-2024-50186](https://nvd.nist.gov/vuln/detail/cve-2024-50186), [CVE-2024-50189](https://nvd.nist.gov/vuln/detail/cve-2024-50189), [CVE-2024-50191](https://nvd.nist.gov/vuln/detail/cve-2024-50191), [CVE-2024-50197](https://nvd.nist.gov/vuln/detail/cve-2024-50197), [CVE-2024-50199](https://nvd.nist.gov/vuln/detail/cve-2024-50199), [CVE-2024-50200](https://nvd.nist.gov/vuln/detail/cve-2024-50200), [CVE-2024-50201](https://nvd.nist.gov/vuln/detail/cve-2024-50201), [CVE-2024-50215](https://nvd.nist.gov/vuln/detail/cve-2024-50215), [CVE-2024-50216](https://nvd.nist.gov/vuln/detail/cve-2024-50216), [CVE-2024-50219](https://nvd.nist.gov/vuln/detail/cve-2024-50219), [CVE-2024-50228](https://nvd.nist.gov/vuln/detail/cve-2024-50228), [CVE-2024-50235](https://nvd.nist.gov/vuln/detail/cve-2024-50235), [CVE-2024-50236](https://nvd.nist.gov/vuln/detail/cve-2024-50236), [CVE-2024-50237](https://nvd.nist.gov/vuln/detail/cve-2024-50237), [CVE-2024-50256](https://nvd.nist.gov/vuln/detail/cve-2024-50256), [CVE-2024-50261](https://nvd.nist.gov/vuln/detail/cve-2024-50261), [CVE-2024-50271](https://nvd.nist.gov/vuln/detail/cve-2024-50271), [CVE-2024-50272](https://nvd.nist.gov/vuln/detail/cve-2024-50272), [CVE-2024-50278](https://nvd.nist.gov/vuln/detail/cve-2024-50278), [CVE-2024-50282](https://nvd.nist.gov/vuln/detail/cve-2024-50282), [CVE-2024-50299](https://nvd.nist.gov/vuln/detail/cve-2024-50299), [CVE-2024-50304](https://nvd.nist.gov/vuln/detail/cve-2024-50304), [CVE-2024-53042](https://nvd.nist.gov/vuln/detail/cve-2024-53042), [CVE-2024-53044](https://nvd.nist.gov/vuln/detail/cve-2024-53044), [CVE-2024-53047](https://nvd.nist.gov/vuln/detail/cve-2024-53047), [CVE-2024-53050](https://nvd.nist.gov/vuln/detail/cve-2024-53050), [CVE-2024-53051](https://nvd.nist.gov/vuln/detail/cve-2024-53051), [CVE-2024-53055](https://nvd.nist.gov/vuln/detail/cve-2024-53055), [CVE-2024-53057](https://nvd.nist.gov/vuln/detail/cve-2024-53057), [CVE-2024-53059](https://nvd.nist.gov/vuln/detail/cve-2024-53059), [CVE-2024-53060](https://nvd.nist.gov/vuln/detail/cve-2024-53060), [CVE-2024-53070](https://nvd.nist.gov/vuln/detail/cve-2024-53070), [CVE-2024-53072](https://nvd.nist.gov/vuln/detail/cve-2024-53072), [CVE-2024-53074](https://nvd.nist.gov/vuln/detail/cve-2024-53074), [CVE-2024-53082](https://nvd.nist.gov/vuln/detail/cve-2024-53082), [CVE-2024-53085](https://nvd.nist.gov/vuln/detail/cve-2024-53085), [CVE-2024-53091](https://nvd.nist.gov/vuln/detail/cve-2024-53091), [CVE-2024-53093](https://nvd.nist.gov/vuln/detail/cve-2024-53093), [CVE-2024-53095](https://nvd.nist.gov/vuln/detail/cve-2024-53095), [CVE-2024-53096](https://nvd.nist.gov/vuln/detail/cve-2024-53096), [CVE-2024-53097](https://nvd.nist.gov/vuln/detail/cve-2024-53097), [CVE-2024-53103](https://nvd.nist.gov/vuln/detail/cve-2024-53103), [CVE-2024-53105](https://nvd.nist.gov/vuln/detail/cve-2024-53105), [CVE-2024-53110](https://nvd.nist.gov/vuln/detail/cve-2024-53110), [CVE-2024-53117](https://nvd.nist.gov/vuln/detail/cve-2024-53117), [CVE-2024-53118](https://nvd.nist.gov/vuln/detail/cve-2024-53118), [CVE-2024-53120](https://nvd.nist.gov/vuln/detail/cve-2024-53120), [CVE-2024-53121](https://nvd.nist.gov/vuln/detail/cve-2024-53121), [CVE-2024-53123](https://nvd.nist.gov/vuln/detail/cve-2024-53123), [CVE-2024-53124](https://nvd.nist.gov/vuln/detail/cve-2024-53124), [CVE-2024-53134](https://nvd.nist.gov/vuln/detail/cve-2024-53134), [CVE-2024-53136](https://nvd.nist.gov/vuln/detail/cve-2024-53136), [CVE-2024-53141](https://nvd.nist.gov/vuln/detail/cve-2024-53141), [CVE-2024-53142](https://nvd.nist.gov/vuln/detail/cve-2024-53142), [CVE-2024-53146](https://nvd.nist.gov/vuln/detail/cve-2024-53146), [CVE-2024-53152](https://nvd.nist.gov/vuln/detail/cve-2024-53152), [CVE-2024-53156](https://nvd.nist.gov/vuln/detail/cve-2024-53156), [CVE-2024-53160](https://nvd.nist.gov/vuln/detail/cve-2024-53160), [CVE-2024-53161](https://nvd.nist.gov/vuln/detail/cve-2024-53161), [CVE-2024-53164](https://nvd.nist.gov/vuln/detail/cve-2024-53164), [CVE-2024-53166](https://nvd.nist.gov/vuln/detail/cve-2024-53166), [CVE-2024-53173](https://nvd.nist.gov/vuln/detail/cve-2024-53173), [CVE-2024-53174](https://nvd.nist.gov/vuln/detail/cve-2024-53174), [CVE-2024-53176](https://nvd.nist.gov/vuln/detail/cve-2024-53176), [CVE-2024-53190](https://nvd.nist.gov/vuln/detail/cve-2024-53190), [CVE-2024-53194](https://nvd.nist.gov/vuln/detail/cve-2024-53194), [CVE-2024-53203](https://nvd.nist.gov/vuln/detail/cve-2024-53203), [CVE-2024-53208](https://nvd.nist.gov/vuln/detail/cve-2024-53208), [CVE-2024-53213](https://nvd.nist.gov/vuln/detail/cve-2024-53213), [CVE-2024-53222](https://nvd.nist.gov/vuln/detail/cve-2024-53222), [CVE-2024-53224](https://nvd.nist.gov/vuln/detail/cve-2024-53224), [CVE-2024-53232](https://nvd.nist.gov/vuln/detail/cve-2024-53232), [CVE-2024-53237](https://nvd.nist.gov/vuln/detail/cve-2024-53237), [CVE-2024-53681](https://nvd.nist.gov/vuln/detail/cve-2024-53681), [CVE-2024-54460](https://nvd.nist.gov/vuln/detail/cve-2024-54460), [CVE-2024-54680](https://nvd.nist.gov/vuln/detail/cve-2024-54680), [CVE-2024-56535](https://nvd.nist.gov/vuln/detail/cve-2024-56535), [CVE-2024-56544](https://nvd.nist.gov/vuln/detail/cve-2024-56544), [CVE-2024-56551](https://nvd.nist.gov/vuln/detail/cve-2024-56551), [CVE-2024-56558](https://nvd.nist.gov/vuln/detail/cve-2024-56558), [CVE-2024-56562](https://nvd.nist.gov/vuln/detail/cve-2024-56562), [CVE-2024-56566](https://nvd.nist.gov/vuln/detail/cve-2024-56566), [CVE-2024-56570](https://nvd.nist.gov/vuln/detail/cve-2024-56570), [CVE-2024-56590](https://nvd.nist.gov/vuln/detail/cve-2024-56590), [CVE-2024-56591](https://nvd.nist.gov/vuln/detail/cve-2024-56591), [CVE-2024-56600](https://nvd.nist.gov/vuln/detail/cve-2024-56600), [CVE-2024-56601](https://nvd.nist.gov/vuln/detail/cve-2024-56601), [CVE-2024-56602](https://nvd.nist.gov/vuln/detail/cve-2024-56602), [CVE-2024-56604](https://nvd.nist.gov/vuln/detail/cve-2024-56604), [CVE-2024-56605](https://nvd.nist.gov/vuln/detail/cve-2024-56605), [CVE-2024-56611](https://nvd.nist.gov/vuln/detail/cve-2024-56611), [CVE-2024-56614](https://nvd.nist.gov/vuln/detail/cve-2024-56614), [CVE-2024-56616](https://nvd.nist.gov/vuln/detail/cve-2024-56616), [CVE-2024-56623](https://nvd.nist.gov/vuln/detail/cve-2024-56623), [CVE-2024-56631](https://nvd.nist.gov/vuln/detail/cve-2024-56631), [CVE-2024-56642](https://nvd.nist.gov/vuln/detail/cve-2024-56642), [CVE-2024-56644](https://nvd.nist.gov/vuln/detail/cve-2024-56644), [CVE-2024-56647](https://nvd.nist.gov/vuln/detail/cve-2024-56647), [CVE-2024-56653](https://nvd.nist.gov/vuln/detail/cve-2024-56653), [CVE-2024-56654](https://nvd.nist.gov/vuln/detail/cve-2024-56654), [CVE-2024-56663](https://nvd.nist.gov/vuln/detail/cve-2024-56663), [CVE-2024-56664](https://nvd.nist.gov/vuln/detail/cve-2024-56664), [CVE-2024-56667](https://nvd.nist.gov/vuln/detail/cve-2024-56667), [CVE-2024-56688](https://nvd.nist.gov/vuln/detail/cve-2024-56688), [CVE-2024-56693](https://nvd.nist.gov/vuln/detail/cve-2024-56693), [CVE-2024-56729](https://nvd.nist.gov/vuln/detail/cve-2024-56729), [CVE-2024-56757](https://nvd.nist.gov/vuln/detail/cve-2024-56757), [CVE-2024-56760](https://nvd.nist.gov/vuln/detail/cve-2024-56760), [CVE-2024-56779](https://nvd.nist.gov/vuln/detail/cve-2024-56779), [CVE-2024-56783](https://nvd.nist.gov/vuln/detail/cve-2024-56783), [CVE-2024-57798](https://nvd.nist.gov/vuln/detail/cve-2024-57798), [CVE-2024-57809](https://nvd.nist.gov/vuln/detail/cve-2024-57809), [CVE-2024-57843](https://nvd.nist.gov/vuln/detail/cve-2024-57843), [CVE-2024-57852](https://nvd.nist.gov/vuln/detail/cve-2024-57852), [CVE-2024-57879](https://nvd.nist.gov/vuln/detail/cve-2024-57879), [CVE-2024-57884](https://nvd.nist.gov/vuln/detail/cve-2024-57884), [CVE-2024-57885](https://nvd.nist.gov/vuln/detail/cve-2024-57885), [CVE-2024-57888](https://nvd.nist.gov/vuln/detail/cve-2024-57888), [CVE-2024-57890](https://nvd.nist.gov/vuln/detail/cve-2024-57890), [CVE-2024-57894](https://nvd.nist.gov/vuln/detail/cve-2024-57894), [CVE-2024-57898](https://nvd.nist.gov/vuln/detail/cve-2024-57898), [CVE-2024-57903](https://nvd.nist.gov/vuln/detail/cve-2024-57903), [CVE-2024-57929](https://nvd.nist.gov/vuln/detail/cve-2024-57929), [CVE-2024-57931](https://nvd.nist.gov/vuln/detail/cve-2024-57931), [CVE-2024-57940](https://nvd.nist.gov/vuln/detail/cve-2024-57940), [CVE-2024-58009](https://nvd.nist.gov/vuln/detail/cve-2024-58009), [CVE-2024-58064](https://nvd.nist.gov/vuln/detail/cve-2024-58064), [CVE-2024-58099](https://nvd.nist.gov/vuln/detail/cve-2024-58099), [CVE-2025-1272](https://nvd.nist.gov/vuln/detail/cve-2025-1272), [CVE-2025-21646](https://nvd.nist.gov/vuln/detail/cve-2025-21646), [CVE-2025-21663](https://nvd.nist.gov/vuln/detail/cve-2025-21663), [CVE-2025-21666](https://nvd.nist.gov/vuln/detail/cve-2025-21666), [CVE-2025-21668](https://nvd.nist.gov/vuln/detail/cve-2025-21668), [CVE-2025-21669](https://nvd.nist.gov/vuln/detail/cve-2025-21669), [CVE-2025-21689](https://nvd.nist.gov/vuln/detail/cve-2025-21689), [CVE-2025-21694](https://nvd.nist.gov/vuln/detail/cve-2025-21694), [CVE-2025-22087](https://nvd.nist.gov/vuln/detail/cve-2025-22087), [RHSA-2025:8142](https://access.redhat.com/errata/RHSA-2025:8142), [CVE-2025-21964](https://nvd.nist.gov/vuln/detail/cve-2025-21964), [RHSA-2025:8333](https://access.redhat.com/errata/RHSA-2025:8333), [CVE-2022-3424](https://nvd.nist.gov/vuln/detail/cve-2022-3424), [CVE-2025-21764](https://nvd.nist.gov/vuln/detail/cve-2025-21764), [RHSA-2025:9302](https://access.redhat.com/errata/RHSA-2025:9302), [CVE-2025-21883](https://nvd.nist.gov/vuln/detail/cve-2025-21883), [CVE-2025-21919](https://nvd.nist.gov/vuln/detail/cve-2025-21919), [CVE-2025-22104](https://nvd.nist.gov/vuln/detail/cve-2025-22104), [CVE-2025-23150](https://nvd.nist.gov/vuln/detail/cve-2025-23150), [CVE-2025-37738](https://nvd.nist.gov/vuln/detail/cve-2025-37738), [RHSA-2025:9880](https://access.redhat.com/errata/RHSA-2025:9880), [CVE-2023-52933](https://nvd.nist.gov/vuln/detail/cve-2023-52933), [RHSA-2025:7067](https://access.redhat.com/errata/RHSA-2025:7067), [CVE-2025-24528](https://nvd.nist.gov/vuln/detail/cve-2025-24528), [RHSA-2025:9430](https://access.redhat.com/errata/RHSA-2025:9430), [CVE-2025-3576](https://nvd.nist.gov/vuln/detail/cve-2025-3576), [RHSA-2025:9431](https://access.redhat.com/errata/RHSA-2025:9431), [CVE-2025-25724](https://nvd.nist.gov/vuln/detail/cve-2025-25724), [RHSA-2025:18275](https://access.redhat.com/errata/RHSA-2025:18275), [CVE-2025-5318](https://nvd.nist.gov/vuln/detail/cve-2025-5318), [RHSA-2025:7077](https://access.redhat.com/errata/RHSA-2025:7077), [CVE-2024-12133](https://nvd.nist.gov/vuln/detail/cve-2024-12133), [RHSA-2025:13428](https://access.redhat.com/errata/RHSA-2025:13428), [CVE-2025-32414](https://nvd.nist.gov/vuln/detail/cve-2025-32414), [CVE-2025-32415](https://nvd.nist.gov/vuln/detail/cve-2025-32415), [RHSA-2025:7043](https://access.redhat.com/errata/RHSA-2025:7043), [CVE-2024-28047](https://nvd.nist.gov/vuln/detail/cve-2024-28047), [CVE-2024-31157](https://nvd.nist.gov/vuln/detail/cve-2024-31157), [CVE-2024-39279](https://nvd.nist.gov/vuln/detail/cve-2024-39279), [RHSA-2025:6993](https://access.redhat.com/errata/RHSA-2025:6993), [CVE-2025-26465](https://nvd.nist.gov/vuln/detail/cve-2025-26465), [RHSA-2025:11804](https://access.redhat.com/errata/RHSA-2025:11804), [CVE-2025-40909](https://nvd.nist.gov/vuln/detail/cve-2025-40909), [RHSA-2025:15874](https://access.redhat.com/errata/RHSA-2025:15874), [CVE-2023-49083](https://nvd.nist.gov/vuln/detail/cve-2023-49083), [RHSA-2025:12519](https://access.redhat.com/errata/RHSA-2025:12519), [CVE-2024-47081](https://nvd.nist.gov/vuln/detail/cve-2024-47081), [RHSA-2025:7049](https://access.redhat.com/errata/RHSA-2025:7049), [CVE-2024-35195](https://nvd.nist.gov/vuln/detail/cve-2024-35195), [RHSA-2025:10407](https://access.redhat.com/errata/RHSA-2025:10407), [CVE-2025-47273](https://nvd.nist.gov/vuln/detail/cve-2025-47273), [RHSA-2025:15019](https://access.redhat.com/errata/RHSA-2025:15019), [CVE-2025-8194](https://nvd.nist.gov/vuln/detail/cve-2025-8194), [RHSA-2025:6977](https://access.redhat.com/errata/RHSA-2025:6977), [CVE-2025-0938](https://nvd.nist.gov/vuln/detail/cve-2025-0938), [RHSA-2025:7326](https://access.redhat.com/errata/RHSA-2025:7326), [CVE-2024-45336](https://nvd.nist.gov/vuln/detail/cve-2024-45336), [CVE-2025-22866](https://nvd.nist.gov/vuln/detail/cve-2025-22866), [RHSA-2025:10353](https://access.redhat.com/errata/RHSA-2025:10353), [CVE-2024-54661](https://nvd.nist.gov/vuln/detail/cve-2024-54661), [RHSA-2025:17742](https://access.redhat.com/errata/RHSA-2025:17742), [CVE-2025-53905](https://nvd.nist.gov/vuln/detail/cve-2025-53905), and [CVE-2025-53906](https://nvd.nist.gov/vuln/detail/cve-2025-53906).


RHEL_8 4.18.0-553.77.1.el8_10
:   Resolves the following CVEs: [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:17415](https://access.redhat.com/errata/RHSA-2025:17415), [CVE-2025-32988](https://nvd.nist.gov/vuln/detail/cve-2025-32988), [CVE-2025-32990](https://nvd.nist.gov/vuln/detail/cve-2025-32990), [CVE-2025-6395](https://nvd.nist.gov/vuln/detail/cve-2025-6395), [RHSA-2025:17397](https://access.redhat.com/errata/RHSA-2025:17397), [CVE-2025-38527](https://nvd.nist.gov/vuln/detail/cve-2025-38527), [CVE-2025-39730](https://nvd.nist.gov/vuln/detail/cve-2025-39730), [RHSA-2025:17797](https://access.redhat.com/errata/RHSA-2025:17797), [CVE-2022-50228](https://nvd.nist.gov/vuln/detail/cve-2022-50228), [CVE-2023-53305](https://nvd.nist.gov/vuln/detail/cve-2023-53305), [RHSA-2025:17715](https://access.redhat.com/errata/RHSA-2025:17715), [CVE-2025-53905](https://nvd.nist.gov/vuln/detail/cve-2025-53905), and [CVE-2025-53906](https://nvd.nist.gov/vuln/detail/cve-2025-53906).


Red Hat OpenShift and Red Hat CoreOS 4.17.41
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-41_release-notes){: external}.


HAProxy c01cd5322cd5c284286c07fe9ad0cc0ef3ab5360
:   Resolves the following CVEs: [CVE-2025-32988](https://nvd.nist.gov/vuln/detail/cve-2025-32988), [CVE-2025-6395](https://nvd.nist.gov/vuln/detail/cve-2025-6395), and [CVE-2025-32990](https://nvd.nist.gov/vuln/detail/cve-2025-32990).


## 08 October 2025, Worker node fix pack 4.17.40_1558_openshift
{: #cl-boms-41740_1558_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.40_1558_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.77.1.el8_10
:   Resolves the following CVEs: [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:16372](https://access.redhat.com/errata/RHSA-2025:16372), [CVE-2025-38461](https://nvd.nist.gov/vuln/detail/cve-2025-38461), [CVE-2025-38498](https://nvd.nist.gov/vuln/detail/cve-2025-38498), [CVE-2025-38556](https://nvd.nist.gov/vuln/detail/cve-2025-38556), [RHSA-2025:16919](https://access.redhat.com/errata/RHSA-2025:16919), [CVE-2022-50087](https://nvd.nist.gov/vuln/detail/cve-2022-50087), [CVE-2025-22026](https://nvd.nist.gov/vuln/detail/cve-2025-22026), [CVE-2025-37797](https://nvd.nist.gov/vuln/detail/cve-2025-37797), [CVE-2025-38718](https://nvd.nist.gov/vuln/detail/cve-2025-38718), [RHSA-2025:16823](https://access.redhat.com/errata/RHSA-2025:16823), and [CVE-2025-26465](https://nvd.nist.gov/vuln/detail/cve-2025-26465).


Red Hat OpenShift and Red Hat CoreOS 4.17.40
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-40_release-notes){: external}.


HAProxy e0a48fcf355d98dc769ea048d2fd02044b11ed62
:   


## Master fix pack 4.17.40_1557_openshift, released 07 October 2025
{: #41740_1557_openshift_M}

The following list shows the changes that are in the master fix pack 4.17.40_1557_openshift. Master patch updates are applied automatically. 


Calico v3.29.5
:   See the [Calico release notes](https://archive-os-3-29.netlify.app/calico/3.29/release-notes/#v3.29.5){: external}.
etcd v3.5.23
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.23){: external}.
{{site.data.keyword.cloud_notm}} Controller Manager v1.30.14-12
:   New version contains updates and security fixes.
{{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor 452
:   New version contains updates and security fixes.
Key Management Service provider v2.10.17
:   New version contains updates and security fixes.
Portieris admission controller v0.13.30
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.30){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.17.40
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-40_release-notes){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.17.0+20250821
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.17.0+20250821){: external}.
Tigera Operator v1.36.13
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.36.13){: external}.


## 23 September 2025, Worker node fix pack 4.17.39_1554_openshift
{: #cl-boms-41739_1554_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.39_1554_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.75.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:15904](https://access.redhat.com/errata/RHSA-2025:15904), [CVE-2025-9566](https://nvd.nist.gov/vuln/detail/cve-2025-9566), [RHSA-2025:15471](https://access.redhat.com/errata/RHSA-2025:15471), [CVE-2022-49985](https://nvd.nist.gov/vuln/detail/cve-2022-49985), [CVE-2025-38352](https://nvd.nist.gov/vuln/detail/cve-2025-38352), [RHSA-2025:15785](https://access.redhat.com/errata/RHSA-2025:15785), [CVE-2023-53125](https://nvd.nist.gov/vuln/detail/cve-2023-53125), [CVE-2025-38350](https://nvd.nist.gov/vuln/detail/cve-2025-38350), [CVE-2025-38392](https://nvd.nist.gov/vuln/detail/cve-2025-38392), [CVE-2025-38449](https://nvd.nist.gov/vuln/detail/cve-2025-38449), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), and [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690).


Red Hat OpenShift and Red Hat CoreOS 4.17.39
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-39_release-notes){: external}.


HAProxy e0a48fcf355d98dc769ea048d2fd02044b11ed62
:   


## 09 September 2025, Worker node fix pack 4.17.38_1552_openshift
{: #cl-boms-41738_1552_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.38_1552_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.72.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:13960](https://access.redhat.com/errata/RHSA-2025:13960), [CVE-2025-22097](https://nvd.nist.gov/vuln/detail/cve-2025-22097), [CVE-2025-37914](https://nvd.nist.gov/vuln/detail/cve-2025-37914), [CVE-2025-38250](https://nvd.nist.gov/vuln/detail/cve-2025-38250), [CVE-2025-38380](https://nvd.nist.gov/vuln/detail/cve-2025-38380), [RHSA-2025:14557](https://access.redhat.com/errata/RHSA-2025:14557), [CVE-2025-6020](https://nvd.nist.gov/vuln/detail/cve-2025-6020), [CVE-2025-8941](https://nvd.nist.gov/vuln/detail/cve-2025-8941), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:13589](https://access.redhat.com/errata/RHSA-2025:13589), [CVE-2021-47670](https://nvd.nist.gov/vuln/detail/cve-2021-47670), [CVE-2024-56644](https://nvd.nist.gov/vuln/detail/cve-2024-56644), [CVE-2025-21727](https://nvd.nist.gov/vuln/detail/cve-2025-21727), [CVE-2025-21759](https://nvd.nist.gov/vuln/detail/cve-2025-21759), [CVE-2025-38085](https://nvd.nist.gov/vuln/detail/cve-2025-38085), [CVE-2025-38159](https://nvd.nist.gov/vuln/detail/cve-2025-38159), [RHSA-2025:14438](https://access.redhat.com/errata/RHSA-2025:14438), [CVE-2025-22058](https://nvd.nist.gov/vuln/detail/cve-2025-22058), [CVE-2025-38200](https://nvd.nist.gov/vuln/detail/cve-2025-38200), [RHSA-2025:15008](https://access.redhat.com/errata/RHSA-2025:15008), [CVE-2025-38211](https://nvd.nist.gov/vuln/detail/cve-2025-38211), [CVE-2025-38332](https://nvd.nist.gov/vuln/detail/cve-2025-38332), [CVE-2025-38464](https://nvd.nist.gov/vuln/detail/cve-2025-38464), [CVE-2025-38477](https://nvd.nist.gov/vuln/detail/cve-2025-38477), [RHSA-2025:14553](https://access.redhat.com/errata/RHSA-2025:14553), [CVE-2023-49083](https://nvd.nist.gov/vuln/detail/cve-2023-49083), [RHSA-2025:14560](https://access.redhat.com/errata/RHSA-2025:14560), [CVE-2025-8194](https://nvd.nist.gov/vuln/detail/cve-2025-8194), [RHSA-2025:14900](https://access.redhat.com/errata/RHSA-2025:14900), [CVE-2025-47273](https://nvd.nist.gov/vuln/detail/cve-2025-47273), and [CVE-2025-8194](https://nvd.nist.gov/vuln/detail/cve-2025-8194).


Red Hat OpenShift and Red Hat CoreOS 4.17.38
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-38_release-notes){: external}.


HAProxy e0a48fcf355d98dc769ea048d2fd02044b11ed62
:   Resolves the following CVEs: [CVE-2025-6020](https://nvd.nist.gov/vuln/detail/cve-2025-6020), and [CVE-2025-8941](https://nvd.nist.gov/vuln/detail/cve-2025-8941).


## 26 August 2025, Worker node fix pack 4.17.37_1551_openshift
{: #cl-boms-41737_1551_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.37_1551_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.66.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:12752](https://access.redhat.com/errata/RHSA-2025:12752), [CVE-2022-50020](https://nvd.nist.gov/vuln/detail/cve-2025-50020), [CVE-2025-21928](https://nvd.nist.gov/vuln/detail/cve-2025-21928), [CVE-2025-22020](https://nvd.nist.gov/vuln/detail/cve-2025-22020), [CVE-2025-37890](https://nvd.nist.gov/vuln/detail/cve-2025-37890), [CVE-2025-38052](https://nvd.nist.gov/vuln/detail/cve-2025-38052), [CVE-2025-38079](https://nvd.nist.gov/vuln/detail/cve-2025-38079), [RHSA-2025:14135](https://access.redhat.com/errata/RHSA-2025:14135), [CVE-2025-5914](https://nvd.nist.gov/vuln/detail/cve-2025-5914), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:11850](https://access.redhat.com/errata/RHSA-2025:11850), [CVE-2022-49977](https://nvd.nist.gov/vuln/detail/cve-2022-49977), [CVE-2025-21905](https://nvd.nist.gov/vuln/detail/cve-2025-21905), and [CVE-2025-21919](https://nvd.nist.gov/vuln/detail/cve-2025-21919).


Red Hat OpenShift and Red Hat CoreOS 4.17.37
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-37_release-notes){: external}.


HAProxy 3293782c542587d0ce46be4d053036b75509f4ef
:   Resolves the following CVEs: [CVE-2025-5914](https://nvd.nist.gov/vuln/detail/cve-2025-5914).


## Master fix pack 4.17.36_1550_openshift, released 20 August 2025
{: #41736_1550_openshift_M}

The following list shows the changes that are in the master fix pack 4.17.36_1550_openshift. Master patch updates are applied automatically. 


etcd v3.5.22
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.22){: external}.
{{site.data.keyword.cloud_notm}} Controller Manager v1.30.14-6
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} RBAC Operator 8a12251
:   New version contains updates and security fixes.
Key Management Service provider v2.10.16
:   New version contains updates and security fixes.
{{site.data.keyword.openshiftlong_notm}} 4.17.36
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-36_release-notes){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit v4.17.0+20250808
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.17.0+20250808){: external}.


## 12 August 2025, Worker node fix pack 4.17.37_1549_openshift
{: #cl-boms-41737_1549_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.37_1549_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.63.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:13589](https://access.redhat.com/errata/RHSA-2025:13589), [CVE-2021-47670](https://nvd.nist.gov/vuln/detail/cve-2021-47670), [CVE-2025-21727](https://nvd.nist.gov/vuln/detail/cve-2025-21727), [CVE-2025-21759](https://nvd.nist.gov/vuln/detail/cve-2025-21759), [CVE-2025-38085](https://nvd.nist.gov/vuln/detail/cve-2025-38085), and [CVE-2025-38159](https://nvd.nist.gov/vuln/detail/cve-2025-38159).


Red Hat OpenShift and Red Hat CoreOS 4.17.37
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-37_release-notes){: external}.


HAProxy 3a9451f4782fa8e8e9ed60b060dc4393c7e1e31a
:   Resolves the following CVEs: [CVE-2025-6965](https://nvd.nist.gov/vuln/detail/cve-2025-6965), [CVE-2025-8058](https://nvd.nist.gov/vuln/detail/cve-2025-8058), and [CVE-2025-7425](https://nvd.nist.gov/vuln/detail/cve-2025-7425).


## Master fix pack 4.17.35_1547_openshift, released 30 July 2025
{: #41735_1547_openshift_M}

The following list shows the changes that are in the master fix pack 4.17.35_1547_openshift. Master patch updates are applied automatically. 


Calico v3.29.4
:   See the [Calico release notes](https://archive-os-3-29.netlify.app/calico/3.29/release-notes/#calico-open-source-3294-bug-fix-release){: external}.
Calico API server v3.29.4
:   See the [Calico release notes](https://docs.tigera.io/archive){: external}.
Cluster health image v1.6.10
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} Block Storage driver and plug-in v2.5.20
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} Controller Manager v1.30.14-4
:   New version contains updates and security fixes.
{{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor 451
:   New version contains updates and security fixes.
Key Management Service provider v2.10.15
:   New version contains updates and security fixes.
Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider 3347
:   New version contains updates and security fixes.
Portieris admission controller v0.13.29
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.29){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.17.35
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-35_release-notes){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.17.0+20250627
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.17.0+20250627){: external}.
Tigera Operator v1.36.11
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.36.11){: external}.


## 28 July 2025, Worker node fix pack 4.17.36_1548_openshift
{: #cl-boms-41736_1548_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.36_1548_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.63.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:11324](https://access.redhat.com/errata/RHSA-2025:11324), [CVE-2024-6174](https://nvd.nist.gov/vuln/detail/cve-2024-6174), [RHSA-2025:11534](https://access.redhat.com/errata/RHSA-2025:11534), [CVE-2024-50349](https://nvd.nist.gov/vuln/detail/cve-2024-50349), [CVE-2024-52006](https://nvd.nist.gov/vuln/detail/cve-2024-52006), [CVE-2025-27613](https://nvd.nist.gov/vuln/detail/cve-2025-27613), [CVE-2025-27614](https://nvd.nist.gov/vuln/detail/cve-2025-27614), [CVE-2025-46835](https://nvd.nist.gov/vuln/detail/cve-2025-46835), [CVE-2025-48384](https://nvd.nist.gov/vuln/detail/cve-2025-48384), [CVE-2025-48385](https://nvd.nist.gov/vuln/detail/cve-2025-48385), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:11327](https://access.redhat.com/errata/RHSA-2025:11327), [CVE-2024-34397](https://nvd.nist.gov/vuln/detail/cve-2024-34397), [CVE-2024-52533](https://nvd.nist.gov/vuln/detail/cve-2024-52533), [CVE-2025-4373](https://nvd.nist.gov/vuln/detail/cve-2025-4373), [RHSA-2025:11298](https://access.redhat.com/errata/RHSA-2025:11298), [CVE-2022-49058](https://nvd.nist.gov/vuln/detail/cve-2022-49058), [CVE-2022-49788](https://nvd.nist.gov/vuln/detail/cve-2022-49788), [CVE-2024-57980](https://nvd.nist.gov/vuln/detail/cve-2024-57980), [CVE-2024-58002](https://nvd.nist.gov/vuln/detail/cve-2024-58002), [CVE-2025-21991](https://nvd.nist.gov/vuln/detail/cve-2025-21991), [CVE-2025-22004](https://nvd.nist.gov/vuln/detail/cve-2025-22004), [CVE-2025-23150](https://nvd.nist.gov/vuln/detail/cve-2025-23150), [CVE-2025-37738](https://nvd.nist.gov/vuln/detail/cve-2025-37738), [RHSA-2025:11455](https://access.redhat.com/errata/RHSA-2025:11455), [CVE-2024-50154](https://nvd.nist.gov/vuln/detail/cve-2024-50154), [CVE-2025-38086](https://nvd.nist.gov/vuln/detail/cve-2025-38086), [RHSA-2025:11035](https://access.redhat.com/errata/RHSA-2025:11035), [CVE-2019-17543](https://nvd.nist.gov/vuln/detail/cve-2019-17543), [RHSA-2025:10991](https://access.redhat.com/errata/RHSA-2025:10991), [CVE-2024-28956](https://nvd.nist.gov/vuln/detail/cve-2024-28956), [CVE-2024-43420](https://nvd.nist.gov/vuln/detail/cve-2024-43420), [CVE-2024-45332](https://nvd.nist.gov/vuln/detail/cve-2024-45332), [CVE-2025-20012](https://nvd.nist.gov/vuln/detail/cve-2025-20012), [CVE-2025-20623](https://nvd.nist.gov/vuln/detail/cve-2025-20623), [CVE-2025-24495](https://nvd.nist.gov/vuln/detail/cve-2025-24495), [RHSA-2025:11036](https://access.redhat.com/errata/RHSA-2025:11036), [CVE-2025-47273](https://nvd.nist.gov/vuln/detail/cve-2025-47273), [RHSA-2025:11042](https://access.redhat.com/errata/RHSA-2025:11042), and [CVE-2024-54661](https://nvd.nist.gov/vuln/detail/cve-2024-54661).


Red Hat OpenShift and Red Hat CoreOS 4.17.36
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-36_release-notes){: external}.


HAProxy b19109a289be3a60985c14bfdaf2b48a472556c0
:   Resolves the following CVEs: [CVE-2024-54661](https://nvd.nist.gov/vuln/detail/cve-2024-54661), [CVE-2024-34397](https://nvd.nist.gov/vuln/detail/cve-2024-34397), [CVE-2019-17543](https://nvd.nist.gov/vuln/detail/cve-2019-17543), [CVE-2024-52533](https://nvd.nist.gov/vuln/detail/cve-2024-52533), and [CVE-2025-4373](https://nvd.nist.gov/vuln/detail/cve-2025-4373).


## 14 July 2025, Worker node fix pack 4.17.35_1546_openshift
{: #cl-boms-41735_1546_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.35_1546_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.60.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:10551](https://access.redhat.com/errata/RHSA-2025:10551), [CVE-2025-6032](https://nvd.nist.gov/vuln/detail/cve-2025-6032), [RHSA-2025:10669](https://access.redhat.com/errata/RHSA-2025:10669), [CVE-2022-49111](https://nvd.nist.gov/vuln/detail/cve-2022-49111), [CVE-2022-49136](https://nvd.nist.gov/vuln/detail/cve-2022-49136), [CVE-2022-49846](https://nvd.nist.gov/vuln/detail/cve-2022-49846), [RHSA-2025:10698](https://access.redhat.com/errata/RHSA-2025:10698), [CVE-2025-49794](https://nvd.nist.gov/vuln/detail/cve-2025-49794), [CVE-2025-49796](https://nvd.nist.gov/vuln/detail/cve-2025-49796), [CVE-2025-6021](https://nvd.nist.gov/vuln/detail/cve-2025-6021), [RHSA-2025:10027](https://access.redhat.com/errata/RHSA-2025:10027), [CVE-2025-6020](https://nvd.nist.gov/vuln/detail/cve-2025-6020), [RHSA-2025:10128](https://access.redhat.com/errata/RHSA-2025:10128), [CVE-2024-12718](https://nvd.nist.gov/vuln/detail/cve-2024-12718), [CVE-2025-4138](https://nvd.nist.gov/vuln/detail/cve-2025-4138), [CVE-2025-4330](https://nvd.nist.gov/vuln/detail/cve-2025-4330), [CVE-2025-4435](https://nvd.nist.gov/vuln/detail/cve-2025-4435), [CVE-2025-4517](https://nvd.nist.gov/vuln/detail/cve-2025-4517), [RHSA-2025:10110](https://access.redhat.com/errata/RHSA-2025:10110), [CVE-2025-32462](https://nvd.nist.gov/vuln/detail/cve-2025-32462), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:10618](https://access.redhat.com/errata/RHSA-2025:10618), [CVE-2024-23337](https://nvd.nist.gov/vuln/detail/cve-2024-23337), and [CVE-2025-48060](https://nvd.nist.gov/vuln/detail/cve-2025-48060).


Red Hat OpenShift and Red Hat CoreOS 4.17.35
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-35_release-notes){: external}.


HAProxy 3bb13ac682885a0885eacb7edd1ee7a36d54e2a8
:   Resolves the following CVEs: [CVE-2025-6021](https://nvd.nist.gov/vuln/detail/cve-2025-6021), [CVE-2025-49796](https://nvd.nist.gov/vuln/detail/cve-2025-49796), [CVE-2025-49794](https://nvd.nist.gov/vuln/detail/cve-2025-49794), and [CVE-2025-6020](https://nvd.nist.gov/vuln/detail/cve-2025-6020).


## 01 July 2025, Worker node fix pack 4.17.34_1545_openshift
{: #cl-boms-41734_1545_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.34_1545_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.58.1.el8_10
:   Resolves the following CVEs: [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:9142](https://access.redhat.com/errata/RHSA-2025:9142), [CVE-2025-22871](https://nvd.nist.gov/vuln/detail/cve-2025-22871), [RHSA-2025:9580](https://access.redhat.com/errata/RHSA-2025:9580), [CVE-2022-48919](https://nvd.nist.gov/vuln/detail/cve-2022-48919), [CVE-2024-50301](https://nvd.nist.gov/vuln/detail/cve-2024-50301), [CVE-2024-53064](https://nvd.nist.gov/vuln/detail/cve-2024-53064), and [CVE-2025-21764](https://nvd.nist.gov/vuln/detail/cve-2025-21764).


Red Hat OpenShift and Red Hat CoreOS 4.17.34
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-34_release-notes){: external}.


HAProxy 951efd90b46e95a54751966c644ac37c4c901f92
:   


## Master fix pack 4.17.28_1543_openshift, released 18 June 2025
{: #41728_1543_openshift_M}

The following list shows the changes that are in the master fix pack 4.17.28_1543_openshift. Master patch updates are applied automatically. 


Calico v3.28.4
:   See the [Calico release notes](https://archive-os-3-28.netlify.app/calico/3.28/release-notes/#v3.28.4){: external}.
{{site.data.keyword.cloud_notm}} Block Storage driver and plug-in v2.5.19
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} Controller Manager v1.30.13-4
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} RBAC Operator 38dc95c
:   New version contains updates and security fixes.
Key Management Service provider v2.10.14
:   New version contains updates and security fixes.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.17.0+20250610
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.17.0+20250610){: external}.
Tigera Operator v1.34.11
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.34.11){: external}.


## 16 June 2025, Worker node fix pack 4.17.33_1544_openshift
{: #cl-boms-41733_1544_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.33_1544_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.56.1.el8_10
:   Resolves the following CVEs: [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:8414](https://access.redhat.com/errata/RHSA-2025:8414), [CVE-2024-52005](https://nvd.nist.gov/vuln/detail/cve-2024-52005), [RHSA-2025:8686](https://access.redhat.com/errata/RHSA-2025:8686), [CVE-2025-4802](https://nvd.nist.gov/vuln/detail/cve-2025-4802), [RHSA-2025:8743](https://access.redhat.com/errata/RHSA-2025:8743), [CVE-2022-49395](https://nvd.nist.gov/vuln/detail/cve-2022-49395), [RHSA-2025:8411](https://access.redhat.com/errata/RHSA-2025:8411), [CVE-2025-3576](https://nvd.nist.gov/vuln/detail/cve-2025-3576), [RHSA-2025:8958](https://access.redhat.com/errata/RHSA-2025:8958), and [CVE-2025-32414](https://nvd.nist.gov/vuln/detail/cve-2025-32414).


Red Hat OpenShift and Red Hat CoreOS 4.17.33
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-33_release-notes){: external}.


HAProxy 951efd90b46e95a54751966c644ac37c4c901f92
:   Resolves the following CVEs: [CVE-2025-4802](https://nvd.nist.gov/vuln/detail/cve-2025-4802), [CVE-2025-32414](https://nvd.nist.gov/vuln/detail/cve-2025-32414), and [CVE-2025-3576](https://nvd.nist.gov/vuln/detail/cve-2025-3576).


## 04 June 2025, Worker node fix pack 4.17.31_1541_openshift
{: #cl-boms-41731_1541_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.31_1541_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.54.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:8056](https://access.redhat.com/errata/RHSA-2025:8056), [CVE-2024-40906](https://nvd.nist.gov/vuln/detail/cve-2024-40906), [CVE-2024-44970](https://nvd.nist.gov/vuln/detail/cve-2024-44970), [CVE-2025-21756](https://nvd.nist.gov/vuln/detail/cve-2025-21756), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:8246](https://access.redhat.com/errata/RHSA-2025:8246), and [CVE-2024-43842](https://nvd.nist.gov/vuln/detail/cve-2024-43842).


Red Hat OpenShift and Red Hat CoreOS 4.17.31
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-31_release-notes){: external}.


HAProxy 978e3c26ee7634e39a940696aaf57d9e374db5ce
:   


## Master fix pack 4.17.28_1540_openshift, released 28 May 2025
{: #41728_1540_openshift_M}

The following list shows the changes that are in the master fix pack 4.17.28_1540_openshift. Master patch updates are applied automatically. 


Cluster health image v1.6.9
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} Controller Manager v1.30.13-1
:   New version contains updates and security fixes.
{{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor 450
:   New version contains updates and security fixes.
Key Management Service provider v2.10.13
:   New version contains updates and security fixes.
Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider 3293
:   New version contains updates and security fixes.
Portieris admission controller v0.13.28
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.28){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.17.28
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-28){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.17.0+20250509
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.17.0+20250509){: external}.


## 19 May 2025, Worker node fix pack 4.17.29_1539_openshift
{: #cl-boms-41729_1539_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.29_1539_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   


RHEL_8 4.18.0-553.52.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:7531](https://access.redhat.com/errata/RHSA-2025:7531), [CVE-2022-49011](https://nvd.nist.gov/vuln/detail/cve-2022-49011), [CVE-2024-53141](https://nvd.nist.gov/vuln/detail/cve-2024-53141), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), and [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690).


Red Hat OpenShift and Red Hat CoreOS 4.17.29
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-29_release-notes){: external}.


HAProxy 978e3c26ee7634e39a940696aaf57d9e374db5ce
:   


## 07 May 2025, Worker node fix pack 4.17.27_1538_openshift
{: #cl-boms-41727_1538_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.27_1538_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.40.1.el9_5
:   Resolves the following CVEs: [RHSA-2025:4341](https://access.redhat.com/errata/RHSA-2025:4341), [CVE-2024-42292](https://nvd.nist.gov/vuln/detail/cve-2024-42292), [CVE-2024-42322](https://nvd.nist.gov/vuln/detail/cve-2024-42322), [CVE-2024-44990](https://nvd.nist.gov/vuln/detail/cve-2024-44990), [CVE-2024-46826](https://nvd.nist.gov/vuln/detail/cve-2024-46826), [CVE-2025-21927](https://nvd.nist.gov/vuln/detail/cve-2025-21927), [RHSA-2025:4244](https://access.redhat.com/errata/RHSA-2025:4244), and [CVE-2025-0395](https://nvd.nist.gov/vuln/detail/cve-2025-0395).


RHEL_8 4.18.0-553.51.1.el8_10
:   Resolves the following CVEs: [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:4051](https://access.redhat.com/errata/RHSA-2025:4051), [CVE-2024-12243](https://nvd.nist.gov/vuln/detail/cve-2024-12243), [RHSA-2025:3893](https://access.redhat.com/errata/RHSA-2025:3893), [CVE-2024-53150](https://nvd.nist.gov/vuln/detail/cve-2024-53150), [CVE-2024-53241](https://nvd.nist.gov/vuln/detail/cve-2024-53241), [RHSA-2025:4049](https://access.redhat.com/errata/RHSA-2025:4049), and [CVE-2024-12133](https://nvd.nist.gov/vuln/detail/cve-2024-12133).


Red Hat OpenShift and Red Hat CoreOS 4.17.27
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes.html#ocp-4-17-27_release-notes){: external}.


HAProxy 978e3c26ee7634e39a940696aaf57d9e374db5ce
:   Resolves the following CVEs: [CVE-2024-12243](https://nvd.nist.gov/vuln/detail/cve-2024-12243), and [CVE-2024-12133](https://nvd.nist.gov/vuln/detail/cve-2024-12133).


## Master fix pack 4.17.24_1537_openshift, released 30 April 2025
{: #41724_1537_openshift_M}

The following list shows the changes that are in the master fix pack 4.17.24_1537_openshift. Master patch updates are applied automatically. 


Calico v3.28.3
:   See the [Calico release notes](https://archive-os-3-28.netlify.app/calico/3.28/release-notes/#v3.28.3){: external}.
Cluster health image v1.6.8
:   New version contains updates and security fixes.
etcd v3.5.21
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.21){: external}.
{{site.data.keyword.cloud_notm}} Controller Manager v1.30.11-6
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} RBAC Operator d1545bd
:   New version contains updates and security fixes.
Key Management Service provider v2.10.12
:   New version contains updates and security fixes.
Portieris admission controller v0.13.26
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.26){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.17.24
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-24){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.17.0+20250414
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.17.0+20250414){: external}.
Tigera Operator v1.34.8
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.34.8){: external}.


## 21 April 2025, Worker node fix pack 4.17.25_1536_openshift
{: #cl-boms-41725_1536_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.25_1536_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.38.1.el9_5
:   Resolves the following CVEs: [RHSA-2025:3937](https://access.redhat.com/errata/RHSA-2025:3937), and [CVE-2024-53150](https://nvd.nist.gov/vuln/detail/cve-2024-53150).


RHEL_8 4.18.0-553.47.1.el8_10
:   Resolves the following CVEs: [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:3913](https://access.redhat.com/errata/RHSA-2025:3913), [CVE-2024-8176](https://nvd.nist.gov/vuln/detail/cve-2024-8176), [RHSA-2025:3828](https://access.redhat.com/errata/RHSA-2025:3828), and [CVE-2025-0395](https://nvd.nist.gov/vuln/detail/cve-2025-0395).


Red Hat OpenShift and Red Hat CoreOS 4.17.25
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-25_release-notes){: external}.


HAProxy bb0015364d95e0a2e7ab83d4a659d1541cee183e
:   Resolves the following CVEs: [CVE-2025-0395](https://nvd.nist.gov/vuln/detail/cve-2025-0395), and [CVE-2024-8176](https://nvd.nist.gov/vuln/detail/cve-2024-8176).


## 08 April 2025, Worker node fix pack 4.17.23_1535_openshift
{: #cl-boms-41723_1535_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.23_1535_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.35.1.el9_5
:   Resolves the following CVEs: [RHSA-2025:3407](https://access.redhat.com/errata/RHSA-2025:3407), [CVE-2025-27363](https://nvd.nist.gov/vuln/detail/cve-2025-27363), [RHSA-2025:3208](https://access.redhat.com/errata/RHSA-2025:3208), [CVE-2025-21785](https://nvd.nist.gov/vuln/detail/cve-2025-21785), [RHSA-2025:3406](https://access.redhat.com/errata/RHSA-2025:3406), [CVE-2025-27516](https://nvd.nist.gov/vuln/detail/cve-2025-27516), [RHSA-2025:3531](https://access.redhat.com/errata/RHSA-2025:3531), [CVE-2024-8176](https://nvd.nist.gov/vuln/detail/cve-2024-8176), [RHSA-2025:3506](https://access.redhat.com/errata/RHSA-2025:3506), and [CVE-2024-43855](https://nvd.nist.gov/vuln/detail/cve-2024-43855).


RHEL_8 4.18.0-553.47.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:3210](https://access.redhat.com/errata/RHSA-2025:3210), [CVE-2025-22869](https://nvd.nist.gov/vuln/detail/cve-2025-22869), [RHSA-2025:3421](https://access.redhat.com/errata/RHSA-2025:3421), [CVE-2025-27363](https://nvd.nist.gov/vuln/detail/cve-2025-27363), [RHSA-2025:3367](https://access.redhat.com/errata/RHSA-2025:3367), [CVE-2025-0624](https://nvd.nist.gov/vuln/detail/cve-2025-0624), [RHSA-2025:3260](https://access.redhat.com/errata/RHSA-2025:3260), [CVE-2025-21785](https://nvd.nist.gov/vuln/detail/cve-2025-21785), [RHSA-2025:3388](https://access.redhat.com/errata/RHSA-2025:3388), [CVE-2025-27516](https://nvd.nist.gov/vuln/detail/cve-2025-27516), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), and [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690).


Red Hat OpenShift and Red Hat CoreOS 4.17.23
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-23_release-notes){: external}.


HAProxy 997a4ab1e89a5c8ccf3a6823785d7ab5e34b0c83
:   


## Master fix pack 4.17.18_1533_openshift, released 26 March 2025
{: #41718_1533_openshift_M}

The following list shows the changes that are in the master fix pack 4.17.18_1533_openshift. Master patch updates are applied automatically. 


Cluster health image v1.6.7
:   New version contains updates and security fixes.
etcd v3.5.18
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.18){: external}.
{{site.data.keyword.cloud_notm}} Controller Manager v1.30.11-1
:   New version contains updates and security fixes.
Key Management Service provider v2.10.11
:   New version contains updates and security fixes.
Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider 3232
:   New version contains updates and security fixes.
Portieris admission controller v0.13.25
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.25){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.17.18
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-18_release-notes){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.17.0+20250313
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.17.0+20250313){: external}.


## 24 March 2025, Worker node fix pack 4.17.21_1534_openshift
{: #cl-boms-41721_1534_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.21_1534_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.33.1.el9_5
:   Resolves the following CVEs: [RHSA-2025:2627](https://access.redhat.com/errata/RHSA-2025:2627), [CVE-2023-52605](https://nvd.nist.gov/vuln/detail/cve-2023-52605), [CVE-2023-52922](https://nvd.nist.gov/vuln/detail/cve-2023-52922), [CVE-2024-50264](https://nvd.nist.gov/vuln/detail/cve-2024-50264), [CVE-2024-50302](https://nvd.nist.gov/vuln/detail/cve-2024-50302), [CVE-2024-53113](https://nvd.nist.gov/vuln/detail/cve-2024-53113), and [CVE-2024-53197](https://nvd.nist.gov/vuln/detail/cve-2024-53197).


RHEL_8 4.18.0-553.45.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:2473](https://access.redhat.com/errata/RHSA-2025:2473), [CVE-2024-50302](https://nvd.nist.gov/vuln/detail/cve-2024-50302), [CVE-2024-53197](https://nvd.nist.gov/vuln/detail/cve-2024-53197), [CVE-2024-57807](https://nvd.nist.gov/vuln/detail/cve-2024-57807), [CVE-2024-57979](https://nvd.nist.gov/vuln/detail/cve-2024-57979), [RHSA-2025:3026](https://access.redhat.com/errata/RHSA-2025:3026), [CVE-2023-52922](https://nvd.nist.gov/vuln/detail/cve-2023-52922), [RHSA-2025:2686](https://access.redhat.com/errata/RHSA-2025:2686), [CVE-2024-56171](https://nvd.nist.gov/vuln/detail/cve-2024-56171), [CVE-2025-24928](https://nvd.nist.gov/vuln/detail/cve-2025-24928), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:2722](https://access.redhat.com/errata/RHSA-2025:2722), and [CVE-2025-24528](https://nvd.nist.gov/vuln/detail/cve-2025-24528).


Red Hat OpenShift and Red Hat CoreOS 4.17.21
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-21_release-notes){: external}.


HAProxy 997a4ab1e89a5c8ccf3a6823785d7ab5e34b0c83
:   Resolves the following CVEs: [CVE-2024-56171](https://nvd.nist.gov/vuln/detail/cve-2024-56171), [CVE-2025-24528](https://nvd.nist.gov/vuln/detail/cve-2025-24528), and [CVE-2025-24928](https://nvd.nist.gov/vuln/detail/cve-2025-24928).


## 11 March 2025, Worker node fix pack 4.17.19_1532_openshift
{: #cl-boms-41719_1532_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.19_1532_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.29.1.el9_5
:   


RHEL_8 4.18.0-553.42.1.el8_10
:   Resolves the following CVEs: [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), and [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690).


Red Hat OpenShift and Red Hat CoreOS 4.17.19
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-19_release-notes){: external}.


HAProxy 1d72cc8c7d02da6ba0340191fa8d9a86550e5090
:   


## 24 February 2025, Worker node fix pack 4.17.17_1531_openshift
{: #cl-boms-41717_1531_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.17_1531_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.26.1.el9_5
:   For more information, see [Release Notes for Red Hat Enterprise Linux 9.5](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/9.5_release_notes/index){: external}.Resolves the following CVEs: [RHSA-2025:1681](https://access.redhat.com/errata/RHSA-2025:1681), [CVE-2024-11187](https://nvd.nist.gov/vuln/detail/cve-2024-11187), [RHSA-2025:0059](https://access.redhat.com/errata/RHSA-2025:0059), [CVE-2024-46713](https://nvd.nist.gov/vuln/detail/cve-2024-46713), [CVE-2024-50208](https://nvd.nist.gov/vuln/detail/cve-2024-50208), [CVE-2024-50252](https://nvd.nist.gov/vuln/detail/cve-2024-50252), [CVE-2024-53122](https://nvd.nist.gov/vuln/detail/cve-2024-53122), [RHSA-2025:1262](https://access.redhat.com/errata/RHSA-2025:1262), [CVE-2024-53104](https://nvd.nist.gov/vuln/detail/cve-2024-53104), [RHSA-2024:9474](https://access.redhat.com/errata/RHSA-2024:9474), [CVE-2024-3596](https://nvd.nist.gov/vuln/detail/cve-2024-3596), [RHSA-2025:1350](https://access.redhat.com/errata/RHSA-2025:1350), [CVE-2022-49043](https://nvd.nist.gov/vuln/detail/cve-2022-49043), [RHSA-2025:1330](https://access.redhat.com/errata/RHSA-2025:1330), [CVE-2024-12797](https://nvd.nist.gov/vuln/detail/cve-2024-12797), [RHSA-2024:10244](https://access.redhat.com/errata/RHSA-2024:10244), [CVE-2024-10963](https://nvd.nist.gov/vuln/detail/cve-2024-10963), [RHSA-2025:0667](https://access.redhat.com/errata/RHSA-2025:0667), [CVE-2024-56326](https://nvd.nist.gov/vuln/detail/cve-2024-56326), [RHSA-2024:10759](https://access.redhat.com/errata/RHSA-2024:10759), [CVE-2022-3064](https://nvd.nist.gov/vuln/detail/cve-2022-3064), [CVE-2023-31315](https://nvd.nist.gov/vuln/detail/cve-2023-31315), [RHSA-2024:9317](https://access.redhat.com/errata/RHSA-2024:9317), [CVE-2024-6501](https://nvd.nist.gov/vuln/detail/cve-2024-6501), [RHSA-2024:9333](https://access.redhat.com/errata/RHSA-2024:9333), [CVE-2024-2511](https://nvd.nist.gov/vuln/detail/cve-2024-2511), [CVE-2024-4603](https://nvd.nist.gov/vuln/detail/cve-2024-4603), [CVE-2024-4741](https://nvd.nist.gov/vuln/detail/cve-2024-4741), [CVE-2024-5535](https://nvd.nist.gov/vuln/detail/cve-2024-5535), [RHSA-2024:9405](https://access.redhat.com/errata/RHSA-2024:9405), [CVE-2021-3903](https://nvd.nist.gov/vuln/detail/cve-2021-3903), [RHSA-2025:0925](https://access.redhat.com/errata/RHSA-2025:0925), [CVE-2019-12900](https://nvd.nist.gov/vuln/detail/cve-2019-12900), [RHSA-2024:9541](https://access.redhat.com/errata/RHSA-2024:9541), [CVE-2024-50602](https://nvd.nist.gov/vuln/detail/cve-2024-50602), [RHSA-2025:1346](https://access.redhat.com/errata/RHSA-2025:1346), [CVE-2020-11023](https://nvd.nist.gov/vuln/detail/cve-2020-11023), [RHSA-2024:10274](https://access.redhat.com/errata/RHSA-2024:10274), [CVE-2024-41009](https://nvd.nist.gov/vuln/detail/cve-2024-41009), [CVE-2024-42244](https://nvd.nist.gov/vuln/detail/cve-2024-42244), [CVE-2024-50226](https://nvd.nist.gov/vuln/detail/cve-2024-50226), [RHSA-2024:10939](https://access.redhat.com/errata/RHSA-2024:10939), [CVE-2024-26615](https://nvd.nist.gov/vuln/detail/cve-2024-26615), [CVE-2024-43854](https://nvd.nist.gov/vuln/detail/cve-2024-43854), [CVE-2024-44994](https://nvd.nist.gov/vuln/detail/cve-2024-44994), [CVE-2024-45018](https://nvd.nist.gov/vuln/detail/cve-2024-45018), [CVE-2024-46695](https://nvd.nist.gov/vuln/detail/cve-2024-46695), [CVE-2024-49949](https://nvd.nist.gov/vuln/detail/cve-2024-49949), [CVE-2024-50251](https://nvd.nist.gov/vuln/detail/cve-2024-50251), [RHSA-2024:11486](https://access.redhat.com/errata/RHSA-2024:11486), [CVE-2024-27399](https://nvd.nist.gov/vuln/detail/cve-2024-27399), [CVE-2024-38564](https://nvd.nist.gov/vuln/detail/cve-2024-38564), [CVE-2024-45020](https://nvd.nist.gov/vuln/detail/cve-2024-45020), [CVE-2024-46697](https://nvd.nist.gov/vuln/detail/cve-2024-46697), [CVE-2024-47675](https://nvd.nist.gov/vuln/detail/cve-2024-47675), [CVE-2024-49888](https://nvd.nist.gov/vuln/detail/cve-2024-49888), [CVE-2024-50099](https://nvd.nist.gov/vuln/detail/cve-2024-50099), [CVE-2024-50110](https://nvd.nist.gov/vuln/detail/cve-2024-50110), [CVE-2024-50115](https://nvd.nist.gov/vuln/detail/cve-2024-50115), [CVE-2024-50124](https://nvd.nist.gov/vuln/detail/cve-2024-50124), [CVE-2024-50125](https://nvd.nist.gov/vuln/detail/cve-2024-50125), [CVE-2024-50142](https://nvd.nist.gov/vuln/detail/cve-2024-50142), [CVE-2024-50148](https://nvd.nist.gov/vuln/detail/cve-2024-50148), [CVE-2024-50192](https://nvd.nist.gov/vuln/detail/cve-2024-50192), [CVE-2024-50223](https://nvd.nist.gov/vuln/detail/cve-2024-50223), [CVE-2024-50255](https://nvd.nist.gov/vuln/detail/cve-2024-50255), [CVE-2024-50262](https://nvd.nist.gov/vuln/detail/cve-2024-50262), [RHSA-2024:9315](https://access.redhat.com/errata/RHSA-2024:9315), [CVE-2019-25162](https://nvd.nist.gov/vuln/detail/cve-2019-25162), [CVE-2020-10135](https://nvd.nist.gov/vuln/detail/cve-2020-10135), [CVE-2021-47098](https://nvd.nist.gov/vuln/detail/cve-2021-47098), [CVE-2021-47101](https://nvd.nist.gov/vuln/detail/cve-2021-47101), [CVE-2021-47185](https://nvd.nist.gov/vuln/detail/cve-2021-47185), [CVE-2021-47384](https://nvd.nist.gov/vuln/detail/cve-2021-47384), [CVE-2021-47386](https://nvd.nist.gov/vuln/detail/cve-2021-47386), [CVE-2021-47428](https://nvd.nist.gov/vuln/detail/cve-2021-47428), [CVE-2021-47429](https://nvd.nist.gov/vuln/detail/cve-2021-47429), [CVE-2021-47432](https://nvd.nist.gov/vuln/detail/cve-2021-47432), [CVE-2021-47454](https://nvd.nist.gov/vuln/detail/cve-2021-47454), [CVE-2021-47457](https://nvd.nist.gov/vuln/detail/cve-2021-47457), [CVE-2021-47495](https://nvd.nist.gov/vuln/detail/cve-2021-47495), [CVE-2021-47497](https://nvd.nist.gov/vuln/detail/cve-2021-47497), [CVE-2021-47505](https://nvd.nist.gov/vuln/detail/cve-2021-47505), [CVE-2022-48669](https://nvd.nist.gov/vuln/detail/cve-2022-48669), [CVE-2022-48672](https://nvd.nist.gov/vuln/detail/cve-2022-48672), [CVE-2022-48703](https://nvd.nist.gov/vuln/detail/cve-2022-48703), [CVE-2022-48804](https://nvd.nist.gov/vuln/detail/cve-2022-48804), [CVE-2022-48929](https://nvd.nist.gov/vuln/detail/cve-2022-48929), [CVE-2023-52445](https://nvd.nist.gov/vuln/detail/cve-2023-52445), [CVE-2023-52451](https://nvd.nist.gov/vuln/detail/cve-2023-52451), [CVE-2023-52455](https://nvd.nist.gov/vuln/detail/cve-2023-52455), [CVE-2023-52462](https://nvd.nist.gov/vuln/detail/cve-2023-52462), [CVE-2023-52464](https://nvd.nist.gov/vuln/detail/cve-2023-52464), [CVE-2023-52466](https://nvd.nist.gov/vuln/detail/cve-2023-52466), [CVE-2023-52467](https://nvd.nist.gov/vuln/detail/cve-2023-52467), [CVE-2023-52473](https://nvd.nist.gov/vuln/detail/cve-2023-52473), [CVE-2023-52475](https://nvd.nist.gov/vuln/detail/cve-2023-52475), [CVE-2023-52477](https://nvd.nist.gov/vuln/detail/cve-2023-52477), [CVE-2023-52482](https://nvd.nist.gov/vuln/detail/cve-2023-52482), [CVE-2023-52486](https://nvd.nist.gov/vuln/detail/cve-2023-52486), [CVE-2023-52492](https://nvd.nist.gov/vuln/detail/cve-2023-52492), [CVE-2023-52498](https://nvd.nist.gov/vuln/detail/cve-2023-52498), [CVE-2023-52501](https://nvd.nist.gov/vuln/detail/cve-2023-52501), [CVE-2023-52513](https://nvd.nist.gov/vuln/detail/cve-2023-52513), [CVE-2023-52520](https://nvd.nist.gov/vuln/detail/cve-2023-52520), [CVE-2023-52528](https://nvd.nist.gov/vuln/detail/cve-2023-52528), [CVE-2023-52560](https://nvd.nist.gov/vuln/detail/cve-2023-52560), [CVE-2023-52565](https://nvd.nist.gov/vuln/detail/cve-2023-52565), [CVE-2023-52585](https://nvd.nist.gov/vuln/detail/cve-2023-52585), [CVE-2023-52594](https://nvd.nist.gov/vuln/detail/cve-2023-52594), [CVE-2023-52595](https://nvd.nist.gov/vuln/detail/cve-2023-52595), [CVE-2023-52606](https://nvd.nist.gov/vuln/detail/cve-2023-52606), [CVE-2023-52614](https://nvd.nist.gov/vuln/detail/cve-2023-52614), [CVE-2023-52615](https://nvd.nist.gov/vuln/detail/cve-2023-52615), [CVE-2023-52619](https://nvd.nist.gov/vuln/detail/cve-2023-52619), [CVE-2023-52621](https://nvd.nist.gov/vuln/detail/cve-2023-52621), [CVE-2023-52622](https://nvd.nist.gov/vuln/detail/cve-2023-52622), [CVE-2023-52624](https://nvd.nist.gov/vuln/detail/cve-2023-52624), [CVE-2023-52625](https://nvd.nist.gov/vuln/detail/cve-2023-52625), [CVE-2023-52632](https://nvd.nist.gov/vuln/detail/cve-2023-52632), [CVE-2023-52634](https://nvd.nist.gov/vuln/detail/cve-2023-52634), [CVE-2023-52635](https://nvd.nist.gov/vuln/detail/cve-2023-52635), [CVE-2023-52637](https://nvd.nist.gov/vuln/detail/cve-2023-52637), [CVE-2023-52643](https://nvd.nist.gov/vuln/detail/cve-2023-52643), [CVE-2023-52648](https://nvd.nist.gov/vuln/detail/cve-2023-52648), [CVE-2023-52649](https://nvd.nist.gov/vuln/detail/cve-2023-52649), [CVE-2023-52650](https://nvd.nist.gov/vuln/detail/cve-2023-52650), [CVE-2023-52656](https://nvd.nist.gov/vuln/detail/cve-2023-52656), [CVE-2023-52659](https://nvd.nist.gov/vuln/detail/cve-2023-52659), [CVE-2023-52661](https://nvd.nist.gov/vuln/detail/cve-2023-52661), [CVE-2023-52662](https://nvd.nist.gov/vuln/detail/cve-2023-52662), [CVE-2023-52663](https://nvd.nist.gov/vuln/detail/cve-2023-52663), [CVE-2023-52664](https://nvd.nist.gov/vuln/detail/cve-2023-52664), [CVE-2023-52674](https://nvd.nist.gov/vuln/detail/cve-2023-52674), [CVE-2023-52676](https://nvd.nist.gov/vuln/detail/cve-2023-52676), [CVE-2023-52679](https://nvd.nist.gov/vuln/detail/cve-2023-52679), [CVE-2023-52680](https://nvd.nist.gov/vuln/detail/cve-2023-52680), [CVE-2023-52683](https://nvd.nist.gov/vuln/detail/cve-2023-52683), [CVE-2023-52686](https://nvd.nist.gov/vuln/detail/cve-2023-52686), [CVE-2023-52689](https://nvd.nist.gov/vuln/detail/cve-2023-52689), [CVE-2023-52690](https://nvd.nist.gov/vuln/detail/cve-2023-52690), [CVE-2023-52696](https://nvd.nist.gov/vuln/detail/cve-2023-52696), [CVE-2023-52697](https://nvd.nist.gov/vuln/detail/cve-2023-52697), [CVE-2023-52698](https://nvd.nist.gov/vuln/detail/cve-2023-52698), [CVE-2023-52703](https://nvd.nist.gov/vuln/detail/cve-2023-52703), [CVE-2023-52730](https://nvd.nist.gov/vuln/detail/cve-2023-52730), [CVE-2023-52731](https://nvd.nist.gov/vuln/detail/cve-2023-52731), [CVE-2023-52740](https://nvd.nist.gov/vuln/detail/cve-2023-52740), [CVE-2023-52749](https://nvd.nist.gov/vuln/detail/cve-2023-52749), [CVE-2023-52751](https://nvd.nist.gov/vuln/detail/cve-2023-52751), [CVE-2023-52756](https://nvd.nist.gov/vuln/detail/cve-2023-52756), [CVE-2023-52757](https://nvd.nist.gov/vuln/detail/cve-2023-52757), [CVE-2023-52758](https://nvd.nist.gov/vuln/detail/cve-2023-52758), [CVE-2023-52762](https://nvd.nist.gov/vuln/detail/cve-2023-52762), [CVE-2023-52775](https://nvd.nist.gov/vuln/detail/cve-2023-52775), [CVE-2023-52784](https://nvd.nist.gov/vuln/detail/cve-2023-52784), [CVE-2023-52788](https://nvd.nist.gov/vuln/detail/cve-2023-52788), [CVE-2023-52791](https://nvd.nist.gov/vuln/detail/cve-2023-52791), [CVE-2023-52811](https://nvd.nist.gov/vuln/detail/cve-2023-52811), [CVE-2023-52813](https://nvd.nist.gov/vuln/detail/cve-2023-52813), [CVE-2023-52814](https://nvd.nist.gov/vuln/detail/cve-2023-52814), [CVE-2023-52817](https://nvd.nist.gov/vuln/detail/cve-2023-52817), [CVE-2023-52819](https://nvd.nist.gov/vuln/detail/cve-2023-52819), [CVE-2023-52831](https://nvd.nist.gov/vuln/detail/cve-2023-52831), [CVE-2023-52833](https://nvd.nist.gov/vuln/detail/cve-2023-52833), [CVE-2023-52834](https://nvd.nist.gov/vuln/detail/cve-2023-52834), [CVE-2023-52837](https://nvd.nist.gov/vuln/detail/cve-2023-52837), [CVE-2023-52840](https://nvd.nist.gov/vuln/detail/cve-2023-52840), [CVE-2023-52859](https://nvd.nist.gov/vuln/detail/cve-2023-52859), [CVE-2023-52867](https://nvd.nist.gov/vuln/detail/cve-2023-52867), [CVE-2023-52869](https://nvd.nist.gov/vuln/detail/cve-2023-52869), [CVE-2023-52878](https://nvd.nist.gov/vuln/detail/cve-2023-52878), [CVE-2023-52902](https://nvd.nist.gov/vuln/detail/cve-2023-52902), [CVE-2024-0340](https://nvd.nist.gov/vuln/detail/cve-2024-0340), [CVE-2024-1151](https://nvd.nist.gov/vuln/detail/cve-2024-1151), [CVE-2024-22099](https://nvd.nist.gov/vuln/detail/cve-2024-22099), [CVE-2024-23307](https://nvd.nist.gov/vuln/detail/cve-2024-23307), [CVE-2024-23848](https://nvd.nist.gov/vuln/detail/cve-2024-23848), [CVE-2024-24857](https://nvd.nist.gov/vuln/detail/cve-2024-24857), [CVE-2024-24858](https://nvd.nist.gov/vuln/detail/cve-2024-24858), [CVE-2024-24859](https://nvd.nist.gov/vuln/detail/cve-2024-24859), [CVE-2024-25739](https://nvd.nist.gov/vuln/detail/cve-2024-25739), [CVE-2024-26589](https://nvd.nist.gov/vuln/detail/cve-2024-26589), [CVE-2024-26591](https://nvd.nist.gov/vuln/detail/cve-2024-26591), [CVE-2024-26601](https://nvd.nist.gov/vuln/detail/cve-2024-26601), [CVE-2024-26603](https://nvd.nist.gov/vuln/detail/cve-2024-26603), [CVE-2024-26605](https://nvd.nist.gov/vuln/detail/cve-2024-26605), [CVE-2024-26611](https://nvd.nist.gov/vuln/detail/cve-2024-26611), [CVE-2024-26612](https://nvd.nist.gov/vuln/detail/cve-2024-26612), [CVE-2024-26614](https://nvd.nist.gov/vuln/detail/cve-2024-26614), [CVE-2024-26618](https://nvd.nist.gov/vuln/detail/cve-2024-26618), [CVE-2024-26631](https://nvd.nist.gov/vuln/detail/cve-2024-26631), [CVE-2024-26638](https://nvd.nist.gov/vuln/detail/cve-2024-26638), [CVE-2024-26641](https://nvd.nist.gov/vuln/detail/cve-2024-26641), [CVE-2024-26645](https://nvd.nist.gov/vuln/detail/cve-2024-26645), [CVE-2024-26646](https://nvd.nist.gov/vuln/detail/cve-2024-26646), [CVE-2024-26650](https://nvd.nist.gov/vuln/detail/cve-2024-26650), [CVE-2024-26656](https://nvd.nist.gov/vuln/detail/cve-2024-26656), [CVE-2024-26660](https://nvd.nist.gov/vuln/detail/cve-2024-26660), [CVE-2024-26661](https://nvd.nist.gov/vuln/detail/cve-2024-26661), [CVE-2024-26662](https://nvd.nist.gov/vuln/detail/cve-2024-26662), [CVE-2024-26663](https://nvd.nist.gov/vuln/detail/cve-2024-26663), [CVE-2024-26664](https://nvd.nist.gov/vuln/detail/cve-2024-26664), [CVE-2024-26669](https://nvd.nist.gov/vuln/detail/cve-2024-26669), [CVE-2024-26670](https://nvd.nist.gov/vuln/detail/cve-2024-26670), [CVE-2024-26672](https://nvd.nist.gov/vuln/detail/cve-2024-26672), [CVE-2024-26674](https://nvd.nist.gov/vuln/detail/cve-2024-26674), [CVE-2024-26675](https://nvd.nist.gov/vuln/detail/cve-2024-26675), [CVE-2024-26678](https://nvd.nist.gov/vuln/detail/cve-2024-26678), [CVE-2024-26679](https://nvd.nist.gov/vuln/detail/cve-2024-26679), [CVE-2024-26680](https://nvd.nist.gov/vuln/detail/cve-2024-26680), [CVE-2024-26686](https://nvd.nist.gov/vuln/detail/cve-2024-26686), [CVE-2024-26691](https://nvd.nist.gov/vuln/detail/cve-2024-26691), [CVE-2024-26700](https://nvd.nist.gov/vuln/detail/cve-2024-26700), [CVE-2024-26704](https://nvd.nist.gov/vuln/detail/cve-2024-26704), [CVE-2024-26707](https://nvd.nist.gov/vuln/detail/cve-2024-26707), [CVE-2024-26708](https://nvd.nist.gov/vuln/detail/cve-2024-26708), [CVE-2024-26712](https://nvd.nist.gov/vuln/detail/cve-2024-26712), [CVE-2024-26717](https://nvd.nist.gov/vuln/detail/cve-2024-26717), [CVE-2024-26719](https://nvd.nist.gov/vuln/detail/cve-2024-26719), [CVE-2024-26725](https://nvd.nist.gov/vuln/detail/cve-2024-26725), [CVE-2024-26733](https://nvd.nist.gov/vuln/detail/cve-2024-26733), [CVE-2024-26734](https://nvd.nist.gov/vuln/detail/cve-2024-26734), [CVE-2024-26740](https://nvd.nist.gov/vuln/detail/cve-2024-26740), [CVE-2024-26743](https://nvd.nist.gov/vuln/detail/cve-2024-26743), [CVE-2024-26744](https://nvd.nist.gov/vuln/detail/cve-2024-26744), [CVE-2024-26746](https://nvd.nist.gov/vuln/detail/cve-2024-26746), [CVE-2024-26757](https://nvd.nist.gov/vuln/detail/cve-2024-26757), [CVE-2024-26758](https://nvd.nist.gov/vuln/detail/cve-2024-26758), [CVE-2024-26759](https://nvd.nist.gov/vuln/detail/cve-2024-26759), [CVE-2024-26761](https://nvd.nist.gov/vuln/detail/cve-2024-26761), [CVE-2024-26767](https://nvd.nist.gov/vuln/detail/cve-2024-26767), [CVE-2024-26772](https://nvd.nist.gov/vuln/detail/cve-2024-26772), [CVE-2024-26774](https://nvd.nist.gov/vuln/detail/cve-2024-26774), [CVE-2024-26782](https://nvd.nist.gov/vuln/detail/cve-2024-26782), [CVE-2024-26785](https://nvd.nist.gov/vuln/detail/cve-2024-26785), [CVE-2024-26786](https://nvd.nist.gov/vuln/detail/cve-2024-26786), [CVE-2024-26803](https://nvd.nist.gov/vuln/detail/cve-2024-26803), [CVE-2024-26812](https://nvd.nist.gov/vuln/detail/cve-2024-26812), [CVE-2024-26815](https://nvd.nist.gov/vuln/detail/cve-2024-26815), [CVE-2024-26835](https://nvd.nist.gov/vuln/detail/cve-2024-26835), [CVE-2024-26837](https://nvd.nist.gov/vuln/detail/cve-2024-26837), [CVE-2024-26838](https://nvd.nist.gov/vuln/detail/cve-2024-26838), [CVE-2024-26840](https://nvd.nist.gov/vuln/detail/cve-2024-26840), [CVE-2024-26843](https://nvd.nist.gov/vuln/detail/cve-2024-26843), [CVE-2024-26846](https://nvd.nist.gov/vuln/detail/cve-2024-26846), [CVE-2024-26857](https://nvd.nist.gov/vuln/detail/cve-2024-26857), [CVE-2024-26861](https://nvd.nist.gov/vuln/detail/cve-2024-26861), [CVE-2024-26862](https://nvd.nist.gov/vuln/detail/cve-2024-26862), [CVE-2024-26863](https://nvd.nist.gov/vuln/detail/cve-2024-26863), [CVE-2024-26870](https://nvd.nist.gov/vuln/detail/cve-2024-26870), [CVE-2024-26872](https://nvd.nist.gov/vuln/detail/cve-2024-26872), [CVE-2024-26878](https://nvd.nist.gov/vuln/detail/cve-2024-26878), [CVE-2024-26882](https://nvd.nist.gov/vuln/detail/cve-2024-26882), [CVE-2024-26889](https://nvd.nist.gov/vuln/detail/cve-2024-26889), [CVE-2024-26890](https://nvd.nist.gov/vuln/detail/cve-2024-26890), [CVE-2024-26892](https://nvd.nist.gov/vuln/detail/cve-2024-26892), [CVE-2024-26894](https://nvd.nist.gov/vuln/detail/cve-2024-26894), [CVE-2024-26899](https://nvd.nist.gov/vuln/detail/cve-2024-26899), [CVE-2024-26900](https://nvd.nist.gov/vuln/detail/cve-2024-26900), [CVE-2024-26901](https://nvd.nist.gov/vuln/detail/cve-2024-26901), [CVE-2024-26903](https://nvd.nist.gov/vuln/detail/cve-2024-26903), [CVE-2024-26906](https://nvd.nist.gov/vuln/detail/cve-2024-26906), [CVE-2024-26907](https://nvd.nist.gov/vuln/detail/cve-2024-26907), [CVE-2024-26915](https://nvd.nist.gov/vuln/detail/cve-2024-26915), [CVE-2024-26920](https://nvd.nist.gov/vuln/detail/cve-2024-26920), [CVE-2024-26921](https://nvd.nist.gov/vuln/detail/cve-2024-26921), [CVE-2024-26922](https://nvd.nist.gov/vuln/detail/cve-2024-26922), [CVE-2024-26924](https://nvd.nist.gov/vuln/detail/cve-2024-26924), [CVE-2024-26927](https://nvd.nist.gov/vuln/detail/cve-2024-26927), [CVE-2024-26928](https://nvd.nist.gov/vuln/detail/cve-2024-26928), [CVE-2024-26933](https://nvd.nist.gov/vuln/detail/cve-2024-26933), [CVE-2024-26934](https://nvd.nist.gov/vuln/detail/cve-2024-26934), [CVE-2024-26937](https://nvd.nist.gov/vuln/detail/cve-2024-26937), [CVE-2024-26938](https://nvd.nist.gov/vuln/detail/cve-2024-26938), [CVE-2024-26939](https://nvd.nist.gov/vuln/detail/cve-2024-26939), [CVE-2024-26940](https://nvd.nist.gov/vuln/detail/cve-2024-26940), [CVE-2024-26950](https://nvd.nist.gov/vuln/detail/cve-2024-26950), [CVE-2024-26951](https://nvd.nist.gov/vuln/detail/cve-2024-26951), [CVE-2024-26953](https://nvd.nist.gov/vuln/detail/cve-2024-26953), [CVE-2024-26958](https://nvd.nist.gov/vuln/detail/cve-2024-26958), [CVE-2024-26960](https://nvd.nist.gov/vuln/detail/cve-2024-26960), [CVE-2024-26962](https://nvd.nist.gov/vuln/detail/cve-2024-26962), [CVE-2024-26964](https://nvd.nist.gov/vuln/detail/cve-2024-26964), [CVE-2024-26973](https://nvd.nist.gov/vuln/detail/cve-2024-26973), [CVE-2024-26975](https://nvd.nist.gov/vuln/detail/cve-2024-26975), [CVE-2024-26976](https://nvd.nist.gov/vuln/detail/cve-2024-26976), [CVE-2024-26984](https://nvd.nist.gov/vuln/detail/cve-2024-26984), [CVE-2024-26987](https://nvd.nist.gov/vuln/detail/cve-2024-26987), [CVE-2024-26988](https://nvd.nist.gov/vuln/detail/cve-2024-26988), [CVE-2024-26989](https://nvd.nist.gov/vuln/detail/cve-2024-26989), [CVE-2024-26990](https://nvd.nist.gov/vuln/detail/cve-2024-26990), [CVE-2024-26992](https://nvd.nist.gov/vuln/detail/cve-2024-26992), [CVE-2024-27003](https://nvd.nist.gov/vuln/detail/cve-2024-27003), [CVE-2024-27004](https://nvd.nist.gov/vuln/detail/cve-2024-27004), [CVE-2024-27010](https://nvd.nist.gov/vuln/detail/cve-2024-27010), [CVE-2024-27011](https://nvd.nist.gov/vuln/detail/cve-2024-27011), [CVE-2024-27012](https://nvd.nist.gov/vuln/detail/cve-2024-27012), [CVE-2024-27013](https://nvd.nist.gov/vuln/detail/cve-2024-27013), [CVE-2024-27014](https://nvd.nist.gov/vuln/detail/cve-2024-27014), [CVE-2024-27015](https://nvd.nist.gov/vuln/detail/cve-2024-27015), [CVE-2024-27017](https://nvd.nist.gov/vuln/detail/cve-2024-27017), [CVE-2024-27023](https://nvd.nist.gov/vuln/detail/cve-2024-27023), [CVE-2024-27025](https://nvd.nist.gov/vuln/detail/cve-2024-27025), [CVE-2024-27038](https://nvd.nist.gov/vuln/detail/cve-2024-27038), [CVE-2024-27042](https://nvd.nist.gov/vuln/detail/cve-2024-27042), [CVE-2024-27048](https://nvd.nist.gov/vuln/detail/cve-2024-27048), [CVE-2024-27057](https://nvd.nist.gov/vuln/detail/cve-2024-27057), [CVE-2024-27062](https://nvd.nist.gov/vuln/detail/cve-2024-27062), [CVE-2024-27079](https://nvd.nist.gov/vuln/detail/cve-2024-27079), [CVE-2024-27389](https://nvd.nist.gov/vuln/detail/cve-2024-27389), [CVE-2024-27395](https://nvd.nist.gov/vuln/detail/cve-2024-27395), [CVE-2024-27404](https://nvd.nist.gov/vuln/detail/cve-2024-27404), [CVE-2024-27410](https://nvd.nist.gov/vuln/detail/cve-2024-27410), [CVE-2024-27414](https://nvd.nist.gov/vuln/detail/cve-2024-27414), [CVE-2024-27431](https://nvd.nist.gov/vuln/detail/cve-2024-27431), [CVE-2024-27436](https://nvd.nist.gov/vuln/detail/cve-2024-27436), [CVE-2024-27437](https://nvd.nist.gov/vuln/detail/cve-2024-27437), [CVE-2024-31076](https://nvd.nist.gov/vuln/detail/cve-2024-31076), [CVE-2024-35787](https://nvd.nist.gov/vuln/detail/cve-2024-35787), [CVE-2024-35794](https://nvd.nist.gov/vuln/detail/cve-2024-35794), [CVE-2024-35795](https://nvd.nist.gov/vuln/detail/cve-2024-35795), [CVE-2024-35801](https://nvd.nist.gov/vuln/detail/cve-2024-35801), [CVE-2024-35805](https://nvd.nist.gov/vuln/detail/cve-2024-35805), [CVE-2024-35807](https://nvd.nist.gov/vuln/detail/cve-2024-35807), [CVE-2024-35808](https://nvd.nist.gov/vuln/detail/cve-2024-35808), [CVE-2024-35809](https://nvd.nist.gov/vuln/detail/cve-2024-35809), [CVE-2024-35810](https://nvd.nist.gov/vuln/detail/cve-2024-35810), [CVE-2024-35812](https://nvd.nist.gov/vuln/detail/cve-2024-35812), [CVE-2024-35814](https://nvd.nist.gov/vuln/detail/cve-2024-35814), [CVE-2024-35817](https://nvd.nist.gov/vuln/detail/cve-2024-35817), [CVE-2024-35822](https://nvd.nist.gov/vuln/detail/cve-2024-35822), [CVE-2024-35824](https://nvd.nist.gov/vuln/detail/cve-2024-35824), [CVE-2024-35827](https://nvd.nist.gov/vuln/detail/cve-2024-35827), [CVE-2024-35831](https://nvd.nist.gov/vuln/detail/cve-2024-35831), [CVE-2024-35835](https://nvd.nist.gov/vuln/detail/cve-2024-35835), [CVE-2024-35838](https://nvd.nist.gov/vuln/detail/cve-2024-35838), [CVE-2024-35840](https://nvd.nist.gov/vuln/detail/cve-2024-35840), [CVE-2024-35843](https://nvd.nist.gov/vuln/detail/cve-2024-35843), [CVE-2024-35847](https://nvd.nist.gov/vuln/detail/cve-2024-35847), [CVE-2024-35853](https://nvd.nist.gov/vuln/detail/cve-2024-35853), [CVE-2024-35854](https://nvd.nist.gov/vuln/detail/cve-2024-35854), [CVE-2024-35855](https://nvd.nist.gov/vuln/detail/cve-2024-35855), [CVE-2024-35859](https://nvd.nist.gov/vuln/detail/cve-2024-35859), [CVE-2024-35861](https://nvd.nist.gov/vuln/detail/cve-2024-35861), [CVE-2024-35862](https://nvd.nist.gov/vuln/detail/cve-2024-35862), [CVE-2024-35863](https://nvd.nist.gov/vuln/detail/cve-2024-35863), [CVE-2024-35864](https://nvd.nist.gov/vuln/detail/cve-2024-35864), [CVE-2024-35865](https://nvd.nist.gov/vuln/detail/cve-2024-35865), [CVE-2024-35866](https://nvd.nist.gov/vuln/detail/cve-2024-35866), [CVE-2024-35867](https://nvd.nist.gov/vuln/detail/cve-2024-35867), [CVE-2024-35869](https://nvd.nist.gov/vuln/detail/cve-2024-35869), [CVE-2024-35872](https://nvd.nist.gov/vuln/detail/cve-2024-35872), [CVE-2024-35876](https://nvd.nist.gov/vuln/detail/cve-2024-35876), [CVE-2024-35877](https://nvd.nist.gov/vuln/detail/cve-2024-35877), [CVE-2024-35878](https://nvd.nist.gov/vuln/detail/cve-2024-35878), [CVE-2024-35880](https://nvd.nist.gov/vuln/detail/cve-2024-35880), [CVE-2024-35886](https://nvd.nist.gov/vuln/detail/cve-2024-35886), [CVE-2024-35888](https://nvd.nist.gov/vuln/detail/cve-2024-35888), [CVE-2024-35892](https://nvd.nist.gov/vuln/detail/cve-2024-35892), [CVE-2024-35894](https://nvd.nist.gov/vuln/detail/cve-2024-35894), [CVE-2024-35900](https://nvd.nist.gov/vuln/detail/cve-2024-35900), [CVE-2024-35904](https://nvd.nist.gov/vuln/detail/cve-2024-35904), [CVE-2024-35905](https://nvd.nist.gov/vuln/detail/cve-2024-35905), [CVE-2024-35908](https://nvd.nist.gov/vuln/detail/cve-2024-35908), [CVE-2024-35912](https://nvd.nist.gov/vuln/detail/cve-2024-35912), [CVE-2024-35913](https://nvd.nist.gov/vuln/detail/cve-2024-35913), [CVE-2024-35918](https://nvd.nist.gov/vuln/detail/cve-2024-35918), [CVE-2024-35923](https://nvd.nist.gov/vuln/detail/cve-2024-35923), [CVE-2024-35924](https://nvd.nist.gov/vuln/detail/cve-2024-35924), [CVE-2024-35925](https://nvd.nist.gov/vuln/detail/cve-2024-35925), [CVE-2024-35927](https://nvd.nist.gov/vuln/detail/cve-2024-35927), [CVE-2024-35928](https://nvd.nist.gov/vuln/detail/cve-2024-35928), [CVE-2024-35930](https://nvd.nist.gov/vuln/detail/cve-2024-35930), [CVE-2024-35931](https://nvd.nist.gov/vuln/detail/cve-2024-35931), [CVE-2024-35938](https://nvd.nist.gov/vuln/detail/cve-2024-35938), [CVE-2024-35939](https://nvd.nist.gov/vuln/detail/cve-2024-35939), [CVE-2024-35942](https://nvd.nist.gov/vuln/detail/cve-2024-35942), [CVE-2024-35944](https://nvd.nist.gov/vuln/detail/cve-2024-35944), [CVE-2024-35946](https://nvd.nist.gov/vuln/detail/cve-2024-35946), [CVE-2024-35947](https://nvd.nist.gov/vuln/detail/cve-2024-35947), [CVE-2024-35950](https://nvd.nist.gov/vuln/detail/cve-2024-35950), [CVE-2024-35952](https://nvd.nist.gov/vuln/detail/cve-2024-35952), [CVE-2024-35954](https://nvd.nist.gov/vuln/detail/cve-2024-35954), [CVE-2024-35957](https://nvd.nist.gov/vuln/detail/cve-2024-35957), [CVE-2024-35959](https://nvd.nist.gov/vuln/detail/cve-2024-35959), [CVE-2024-35973](https://nvd.nist.gov/vuln/detail/cve-2024-35973), [CVE-2024-35976](https://nvd.nist.gov/vuln/detail/cve-2024-35976), [CVE-2024-35979](https://nvd.nist.gov/vuln/detail/cve-2024-35979), [CVE-2024-35983](https://nvd.nist.gov/vuln/detail/cve-2024-35983), [CVE-2024-35991](https://nvd.nist.gov/vuln/detail/cve-2024-35991), [CVE-2024-35995](https://nvd.nist.gov/vuln/detail/cve-2024-35995), [CVE-2024-36002](https://nvd.nist.gov/vuln/detail/cve-2024-36002), [CVE-2024-36006](https://nvd.nist.gov/vuln/detail/cve-2024-36006), [CVE-2024-36010](https://nvd.nist.gov/vuln/detail/cve-2024-36010), [CVE-2024-36015](https://nvd.nist.gov/vuln/detail/cve-2024-36015), [CVE-2024-36022](https://nvd.nist.gov/vuln/detail/cve-2024-36022), [CVE-2024-36028](https://nvd.nist.gov/vuln/detail/cve-2024-36028), [CVE-2024-36030](https://nvd.nist.gov/vuln/detail/cve-2024-36030), [CVE-2024-36031](https://nvd.nist.gov/vuln/detail/cve-2024-36031), [CVE-2024-36477](https://nvd.nist.gov/vuln/detail/cve-2024-36477), [CVE-2024-36881](https://nvd.nist.gov/vuln/detail/cve-2024-36881), [CVE-2024-36882](https://nvd.nist.gov/vuln/detail/cve-2024-36882), [CVE-2024-36884](https://nvd.nist.gov/vuln/detail/cve-2024-36884), [CVE-2024-36885](https://nvd.nist.gov/vuln/detail/cve-2024-36885), [CVE-2024-36891](https://nvd.nist.gov/vuln/detail/cve-2024-36891), [CVE-2024-36896](https://nvd.nist.gov/vuln/detail/cve-2024-36896), [CVE-2024-36901](https://nvd.nist.gov/vuln/detail/cve-2024-36901), [CVE-2024-36902](https://nvd.nist.gov/vuln/detail/cve-2024-36902), [CVE-2024-36905](https://nvd.nist.gov/vuln/detail/cve-2024-36905), [CVE-2024-36917](https://nvd.nist.gov/vuln/detail/cve-2024-36917), [CVE-2024-36920](https://nvd.nist.gov/vuln/detail/cve-2024-36920), [CVE-2024-36926](https://nvd.nist.gov/vuln/detail/cve-2024-36926), [CVE-2024-36927](https://nvd.nist.gov/vuln/detail/cve-2024-36927), [CVE-2024-36928](https://nvd.nist.gov/vuln/detail/cve-2024-36928), [CVE-2024-36930](https://nvd.nist.gov/vuln/detail/cve-2024-36930), [CVE-2024-36932](https://nvd.nist.gov/vuln/detail/cve-2024-36932), [CVE-2024-36933](https://nvd.nist.gov/vuln/detail/cve-2024-36933), [CVE-2024-36936](https://nvd.nist.gov/vuln/detail/cve-2024-36936), [CVE-2024-36939](https://nvd.nist.gov/vuln/detail/cve-2024-36939), [CVE-2024-36940](https://nvd.nist.gov/vuln/detail/cve-2024-36940), [CVE-2024-36944](https://nvd.nist.gov/vuln/detail/cve-2024-36944), [CVE-2024-36945](https://nvd.nist.gov/vuln/detail/cve-2024-36945), [CVE-2024-36955](https://nvd.nist.gov/vuln/detail/cve-2024-36955), [CVE-2024-36956](https://nvd.nist.gov/vuln/detail/cve-2024-36956), [CVE-2024-36960](https://nvd.nist.gov/vuln/detail/cve-2024-36960), [CVE-2024-36961](https://nvd.nist.gov/vuln/detail/cve-2024-36961), [CVE-2024-36967](https://nvd.nist.gov/vuln/detail/cve-2024-36967), [CVE-2024-36974](https://nvd.nist.gov/vuln/detail/cve-2024-36974), [CVE-2024-36977](https://nvd.nist.gov/vuln/detail/cve-2024-36977), [CVE-2024-38388](https://nvd.nist.gov/vuln/detail/cve-2024-38388), [CVE-2024-38555](https://nvd.nist.gov/vuln/detail/cve-2024-38555), [CVE-2024-38581](https://nvd.nist.gov/vuln/detail/cve-2024-38581), [CVE-2024-38596](https://nvd.nist.gov/vuln/detail/cve-2024-38596), [CVE-2024-38598](https://nvd.nist.gov/vuln/detail/cve-2024-38598), [CVE-2024-38600](https://nvd.nist.gov/vuln/detail/cve-2024-38600), [CVE-2024-38604](https://nvd.nist.gov/vuln/detail/cve-2024-38604), [CVE-2024-38605](https://nvd.nist.gov/vuln/detail/cve-2024-38605), [CVE-2024-38618](https://nvd.nist.gov/vuln/detail/cve-2024-38618), [CVE-2024-38627](https://nvd.nist.gov/vuln/detail/cve-2024-38627), [CVE-2024-38629](https://nvd.nist.gov/vuln/detail/cve-2024-38629), [CVE-2024-38632](https://nvd.nist.gov/vuln/detail/cve-2024-38632), [CVE-2024-38635](https://nvd.nist.gov/vuln/detail/cve-2024-38635), [CVE-2024-39276](https://nvd.nist.gov/vuln/detail/cve-2024-39276), [CVE-2024-39291](https://nvd.nist.gov/vuln/detail/cve-2024-39291), [CVE-2024-39298](https://nvd.nist.gov/vuln/detail/cve-2024-39298), [CVE-2024-39471](https://nvd.nist.gov/vuln/detail/cve-2024-39471), [CVE-2024-39473](https://nvd.nist.gov/vuln/detail/cve-2024-39473), [CVE-2024-39474](https://nvd.nist.gov/vuln/detail/cve-2024-39474), [CVE-2024-39479](https://nvd.nist.gov/vuln/detail/cve-2024-39479), [CVE-2024-39486](https://nvd.nist.gov/vuln/detail/cve-2024-39486), [CVE-2024-39488](https://nvd.nist.gov/vuln/detail/cve-2024-39488), [CVE-2024-39491](https://nvd.nist.gov/vuln/detail/cve-2024-39491), [CVE-2024-39497](https://nvd.nist.gov/vuln/detail/cve-2024-39497), [CVE-2024-39498](https://nvd.nist.gov/vuln/detail/cve-2024-39498), [CVE-2024-39499](https://nvd.nist.gov/vuln/detail/cve-2024-39499), [CVE-2024-39501](https://nvd.nist.gov/vuln/detail/cve-2024-39501), [CVE-2024-39503](https://nvd.nist.gov/vuln/detail/cve-2024-39503), [CVE-2024-39507](https://nvd.nist.gov/vuln/detail/cve-2024-39507), [CVE-2024-39508](https://nvd.nist.gov/vuln/detail/cve-2024-39508), [CVE-2024-40901](https://nvd.nist.gov/vuln/detail/cve-2024-40901), [CVE-2024-40903](https://nvd.nist.gov/vuln/detail/cve-2024-40903), [CVE-2024-40906](https://nvd.nist.gov/vuln/detail/cve-2024-40906), [CVE-2024-40907](https://nvd.nist.gov/vuln/detail/cve-2024-40907), [CVE-2024-40913](https://nvd.nist.gov/vuln/detail/cve-2024-40913), [CVE-2024-40919](https://nvd.nist.gov/vuln/detail/cve-2024-40919), [CVE-2024-40922](https://nvd.nist.gov/vuln/detail/cve-2024-40922), [CVE-2024-40923](https://nvd.nist.gov/vuln/detail/cve-2024-40923), [CVE-2024-40924](https://nvd.nist.gov/vuln/detail/cve-2024-40924), [CVE-2024-40925](https://nvd.nist.gov/vuln/detail/cve-2024-40925), [CVE-2024-40930](https://nvd.nist.gov/vuln/detail/cve-2024-40930), [CVE-2024-40940](https://nvd.nist.gov/vuln/detail/cve-2024-40940), [CVE-2024-40945](https://nvd.nist.gov/vuln/detail/cve-2024-40945), [CVE-2024-40948](https://nvd.nist.gov/vuln/detail/cve-2024-40948), [CVE-2024-40965](https://nvd.nist.gov/vuln/detail/cve-2024-40965), [CVE-2024-40966](https://nvd.nist.gov/vuln/detail/cve-2024-40966), [CVE-2024-40967](https://nvd.nist.gov/vuln/detail/cve-2024-40967), [CVE-2024-40988](https://nvd.nist.gov/vuln/detail/cve-2024-40988), [CVE-2024-40989](https://nvd.nist.gov/vuln/detail/cve-2024-40989), [CVE-2024-40997](https://nvd.nist.gov/vuln/detail/cve-2024-40997), [CVE-2024-41001](https://nvd.nist.gov/vuln/detail/cve-2024-41001), [CVE-2024-41007](https://nvd.nist.gov/vuln/detail/cve-2024-41007), [CVE-2024-41008](https://nvd.nist.gov/vuln/detail/cve-2024-41008), [CVE-2024-41012](https://nvd.nist.gov/vuln/detail/cve-2024-41012), [CVE-2024-41020](https://nvd.nist.gov/vuln/detail/cve-2024-41020), [CVE-2024-41032](https://nvd.nist.gov/vuln/detail/cve-2024-41032), [CVE-2024-41038](https://nvd.nist.gov/vuln/detail/cve-2024-41038), [CVE-2024-41039](https://nvd.nist.gov/vuln/detail/cve-2024-41039), [CVE-2024-41042](https://nvd.nist.gov/vuln/detail/cve-2024-41042), [CVE-2024-41049](https://nvd.nist.gov/vuln/detail/cve-2024-41049), [CVE-2024-41056](https://nvd.nist.gov/vuln/detail/cve-2024-41056), [CVE-2024-41057](https://nvd.nist.gov/vuln/detail/cve-2024-41057), [CVE-2024-41058](https://nvd.nist.gov/vuln/detail/cve-2024-41058), [CVE-2024-41060](https://nvd.nist.gov/vuln/detail/cve-2024-41060), [CVE-2024-41063](https://nvd.nist.gov/vuln/detail/cve-2024-41063), [CVE-2024-41065](https://nvd.nist.gov/vuln/detail/cve-2024-41065), [CVE-2024-41077](https://nvd.nist.gov/vuln/detail/cve-2024-41077), [CVE-2024-41079](https://nvd.nist.gov/vuln/detail/cve-2024-41079), [CVE-2024-41082](https://nvd.nist.gov/vuln/detail/cve-2024-41082), [CVE-2024-41084](https://nvd.nist.gov/vuln/detail/cve-2024-41084), [CVE-2024-41085](https://nvd.nist.gov/vuln/detail/cve-2024-41085), [CVE-2024-41089](https://nvd.nist.gov/vuln/detail/cve-2024-41089), [CVE-2024-41092](https://nvd.nist.gov/vuln/detail/cve-2024-41092), [CVE-2024-41093](https://nvd.nist.gov/vuln/detail/cve-2024-41093), [CVE-2024-41094](https://nvd.nist.gov/vuln/detail/cve-2024-41094), [CVE-2024-41095](https://nvd.nist.gov/vuln/detail/cve-2024-41095), [CVE-2024-42070](https://nvd.nist.gov/vuln/detail/cve-2024-42070), [CVE-2024-42078](https://nvd.nist.gov/vuln/detail/cve-2024-42078), [CVE-2024-42084](https://nvd.nist.gov/vuln/detail/cve-2024-42084), [CVE-2024-42090](https://nvd.nist.gov/vuln/detail/cve-2024-42090), [CVE-2024-42101](https://nvd.nist.gov/vuln/detail/cve-2024-42101), [CVE-2024-42114](https://nvd.nist.gov/vuln/detail/cve-2024-42114), [CVE-2024-42123](https://nvd.nist.gov/vuln/detail/cve-2024-42123), [CVE-2024-42124](https://nvd.nist.gov/vuln/detail/cve-2024-42124), [CVE-2024-42125](https://nvd.nist.gov/vuln/detail/cve-2024-42125), [CVE-2024-42132](https://nvd.nist.gov/vuln/detail/cve-2024-42132), [CVE-2024-42141](https://nvd.nist.gov/vuln/detail/cve-2024-42141), [CVE-2024-42154](https://nvd.nist.gov/vuln/detail/cve-2024-42154), [CVE-2024-42159](https://nvd.nist.gov/vuln/detail/cve-2024-42159), [CVE-2024-42226](https://nvd.nist.gov/vuln/detail/cve-2024-42226), [CVE-2024-42228](https://nvd.nist.gov/vuln/detail/cve-2024-42228), [CVE-2024-42237](https://nvd.nist.gov/vuln/detail/cve-2024-42237), [CVE-2024-42238](https://nvd.nist.gov/vuln/detail/cve-2024-42238), [CVE-2024-42240](https://nvd.nist.gov/vuln/detail/cve-2024-42240), [CVE-2024-42245](https://nvd.nist.gov/vuln/detail/cve-2024-42245), [CVE-2024-42258](https://nvd.nist.gov/vuln/detail/cve-2024-42258), [CVE-2024-42268](https://nvd.nist.gov/vuln/detail/cve-2024-42268), [CVE-2024-42271](https://nvd.nist.gov/vuln/detail/cve-2024-42271), [CVE-2024-42276](https://nvd.nist.gov/vuln/detail/cve-2024-42276), [CVE-2024-42301](https://nvd.nist.gov/vuln/detail/cve-2024-42301), [CVE-2024-43817](https://nvd.nist.gov/vuln/detail/cve-2024-43817), [CVE-2024-43826](https://nvd.nist.gov/vuln/detail/cve-2024-43826), [CVE-2024-43830](https://nvd.nist.gov/vuln/detail/cve-2024-43830), [CVE-2024-43842](https://nvd.nist.gov/vuln/detail/cve-2024-43842), [CVE-2024-43856](https://nvd.nist.gov/vuln/detail/cve-2024-43856), [CVE-2024-43865](https://nvd.nist.gov/vuln/detail/cve-2024-43865), [CVE-2024-43866](https://nvd.nist.gov/vuln/detail/cve-2024-43866), [CVE-2024-43869](https://nvd.nist.gov/vuln/detail/cve-2024-43869), [CVE-2024-43870](https://nvd.nist.gov/vuln/detail/cve-2024-43870), [CVE-2024-43879](https://nvd.nist.gov/vuln/detail/cve-2024-43879), [CVE-2024-43888](https://nvd.nist.gov/vuln/detail/cve-2024-43888), [CVE-2024-43892](https://nvd.nist.gov/vuln/detail/cve-2024-43892), [CVE-2024-43911](https://nvd.nist.gov/vuln/detail/cve-2024-43911), [CVE-2024-44947](https://nvd.nist.gov/vuln/detail/cve-2024-44947), [CVE-2024-44960](https://nvd.nist.gov/vuln/detail/cve-2024-44960), [CVE-2024-44965](https://nvd.nist.gov/vuln/detail/cve-2024-44965), [CVE-2024-44970](https://nvd.nist.gov/vuln/detail/cve-2024-44970), [CVE-2024-44984](https://nvd.nist.gov/vuln/detail/cve-2024-44984), [CVE-2024-45005](https://nvd.nist.gov/vuln/detail/cve-2024-45005), [RHSA-2024:9605](https://access.redhat.com/errata/RHSA-2024:9605), [CVE-2024-42283](https://nvd.nist.gov/vuln/detail/cve-2024-42283), [CVE-2024-46824](https://nvd.nist.gov/vuln/detail/cve-2024-46824), [CVE-2024-46858](https://nvd.nist.gov/vuln/detail/cve-2024-46858), [RHSA-2025:0578](https://access.redhat.com/errata/RHSA-2025:0578), [CVE-2024-50154](https://nvd.nist.gov/vuln/detail/cve-2024-50154), [CVE-2024-50275](https://nvd.nist.gov/vuln/detail/cve-2024-50275), [CVE-2024-53088](https://nvd.nist.gov/vuln/detail/cve-2024-53088), [RHSA-2025:1659](https://access.redhat.com/errata/RHSA-2025:1659), [CVE-2023-52490](https://nvd.nist.gov/vuln/detail/cve-2023-52490), [RHSA-2024:9331](https://access.redhat.com/errata/RHSA-2024:9331), [CVE-2024-26458](https://nvd.nist.gov/vuln/detail/cve-2024-26458), [CVE-2024-26461](https://nvd.nist.gov/vuln/detail/cve-2024-26461), [CVE-2024-26462](https://nvd.nist.gov/vuln/detail/cve-2024-26462), [RHSA-2024:9404](https://access.redhat.com/errata/RHSA-2024:9404), [CVE-2024-2236](https://nvd.nist.gov/vuln/detail/cve-2024-2236), [RHSA-2024:9401](https://access.redhat.com/errata/RHSA-2024:9401), [CVE-2023-22655](https://nvd.nist.gov/vuln/detail/cve-2023-22655), [CVE-2023-28746](https://nvd.nist.gov/vuln/detail/cve-2023-28746), [CVE-2023-38575](https://nvd.nist.gov/vuln/detail/cve-2023-38575), [CVE-2023-39368](https://nvd.nist.gov/vuln/detail/cve-2023-39368), [CVE-2023-43490](https://nvd.nist.gov/vuln/detail/cve-2023-43490), [CVE-2023-45733](https://nvd.nist.gov/vuln/detail/cve-2023-45733), [CVE-2023-46103](https://nvd.nist.gov/vuln/detail/cve-2023-46103), [RHSA-2024:11250](https://access.redhat.com/errata/RHSA-2024:11250), [CVE-2024-10041](https://nvd.nist.gov/vuln/detail/cve-2024-10041), [RHSA-2024:9150](https://access.redhat.com/errata/RHSA-2024:9150), [CVE-2024-34064](https://nvd.nist.gov/vuln/detail/cve-2024-34064), [RHSA-2024:9371](https://access.redhat.com/errata/RHSA-2024:9371), [CVE-2024-8088](https://nvd.nist.gov/vuln/detail/cve-2024-8088), [RHSA-2024:9468](https://access.redhat.com/errata/RHSA-2024:9468), [CVE-2024-6232](https://nvd.nist.gov/vuln/detail/cve-2024-6232), [RHSA-2024:10983](https://access.redhat.com/errata/RHSA-2024:10983), [CVE-2024-11168](https://nvd.nist.gov/vuln/detail/cve-2024-11168), [CVE-2024-9287](https://nvd.nist.gov/vuln/detail/cve-2024-9287), [RHSA-2025:0377](https://access.redhat.com/errata/RHSA-2025:0377), and [CVE-2024-3661](https://nvd.nist.gov/vuln/detail/cve-2024-3661).


RHEL_8 4.18.0-553.40.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:1675](https://access.redhat.com/errata/RHSA-2025:1675), [CVE-2024-11187](https://nvd.nist.gov/vuln/detail/cve-2024-11187), [RHSA-2025:1266](https://access.redhat.com/errata/RHSA-2025:1266), [CVE-2024-53104](https://nvd.nist.gov/vuln/detail/cve-2024-53104), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:1301](https://access.redhat.com/errata/RHSA-2025:1301), [CVE-2020-11023](https://nvd.nist.gov/vuln/detail/cve-2020-11023), [RHSA-2025:1517](https://access.redhat.com/errata/RHSA-2025:1517), and [CVE-2022-49043](https://nvd.nist.gov/vuln/detail/cve-2022-49043).


Red Hat OpenShift and Red Hat CoreOS 4.17.17
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-17_release-notes){: external}.


HAProxy 1d72cc8c7d02da6ba0340191fa8d9a86550e5090
:   Resolves the following CVEs: [CVE-2020-11023](https://nvd.nist.gov/vuln/detail/cve-2020-11023), and [CVE-2022-49043](https://nvd.nist.gov/vuln/detail/cve-2022-49043).


## Master fix pack 4.17.14_1530_openshift, released 19 February 2025
{: #41714_1530_openshift_M}

The following list shows the changes that are in the master fix pack 4.17.14_1530_openshift. Master patch updates are applied automatically. 


{{site.data.keyword.cloud_notm}} Block Storage driver and plug-in v2.5.17
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} Controller Manager v1.30.9-2
:   New version contains updates and security fixes.
{{site.data.keyword.filestorage_full_notm}} for Classic plug-in and monitor 449
:   New version contains updates and security fixes.
Key Management Service provider v2.10.10
:   New version contains updates and security fixes.
{{site.data.keyword.openshiftlong_notm}}. 4.17.14
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-14){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.17.0+20250207
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.17.0+20250207){: external}.
Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider 3178
:   New version contains updates and security fixes.
{{site.data.keyword.openshiftlong_notm}}. 4.17.12
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-12){: external}.


## 11 February 2025, Worker node fix pack 4.17.15_1527_openshift
{: #cl-boms-41715_1527_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.15_1527_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_9 5.14.0-503.23.2.el9_5
:   


RHEL_8 4.18.0-553.40.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:0711](https://access.redhat.com/errata/RHSA-2025:0711), [CVE-2024-56326](https://nvd.nist.gov/vuln/detail/cve-2024-56326), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:0733](https://access.redhat.com/errata/RHSA-2025:0733), [CVE-2019-12900](https://nvd.nist.gov/vuln/detail/cve-2019-12900), [RHSA-2025:1068](https://access.redhat.com/errata/RHSA-2025:1068), [CVE-2024-26935](https://nvd.nist.gov/vuln/detail/cve-2024-26935), and [CVE-2024-50275](https://nvd.nist.gov/vuln/detail/cve-2024-50275).


Red Hat OpenShift and Red Hat CoreOS 4.17.15
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-15_release-notes){: external}.


HAProxy 03d1ee01e9241d0e5ec93b9eb8986feb2771a01a
:   Resolves the following CVEs: [CVE-2019-12900](https://nvd.nist.gov/vuln/detail/cve-2019-12900).


## 29 January 2025, Worker node fix pack 4.17.12_1526_openshift
{: #cl-boms-41712_1526_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.12_1526_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_8 4.18.0-553.36.1.el8_10
:   Resolves the following CVEs: [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:0288](https://access.redhat.com/errata/RHSA-2025:0288), and [CVE-2024-3661](https://nvd.nist.gov/vuln/detail/cve-2024-3661).


RHEL_9 5.14.0-427.42.1.el9_4
:   


Red Hat OpenShift and Red Hat CoreOS 4.17.12
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-12_release-notes){: external}.


HAProxy 14daa781a66ca5ed5754656ce53c3cca4af580b5
:   


## Master fix pack 4.17.10_1522_openshift, released 22 January 2025
{: #41710_1522_openshift_M}

The following list shows the changes that are in the master fix pack 4.17.10_1522_openshift. Master patch updates are applied automatically. 


Cluster health image v1.6.4
:   New version contains updates and security fixes.
etcd v3.5.17
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.17){: external}.
{{site.data.keyword.cloud_notm}} Controller Manager v1.30.8-3
:   New version contains updates and security fixes.
{{site.data.keyword.cloud_notm}} RBAC Operator cb4f333
:   New version contains updates and security fixes.
Key Management Service provider v2.10.9
:   New version contains updates and security fixes.
Portieris admission controller v0.13.23
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.23){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.17.10
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-10){: external}.
{{site.data.keyword.openshiftlong_notm}} Control Plane Operator, Metrics Server, and toolkit 4.17.0+20250102
:   See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.17.0+20250102){: external}.


## 13 January 2025, Worker node fix pack 4.17.11_1521_openshift
{: #cl-boms-41711_1521_openshift_W}

The following list shows the components included in the worker node fix pack 4.17.11_1521_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL_8 4.18.0-553.34.1.el8_10
:   Resolves the following CVEs: [RHSA-2025:0065](https://access.redhat.com/errata/RHSA-2025:0065), [CVE-2024-53088](https://nvd.nist.gov/vuln/detail/cve-2024-53088), [CVE-2024-53122](https://nvd.nist.gov/vuln/detail/cve-2024-53122), [RHSA-2024:3043](https://access.redhat.com/errata/RHSA-2024:3043), [CVE-2024-0690](https://nvd.nist.gov/vuln/detail/cve-2024-0690), [RHSA-2025:0012](https://access.redhat.com/errata/RHSA-2025:0012), [CVE-2024-35195](https://nvd.nist.gov/vuln/detail/cve-2024-35195), [RHSA-2024:11161](https://access.redhat.com/errata/RHSA-2024:11161), and [CVE-2024-52337](https://nvd.nist.gov/vuln/detail/cve-2024-52337).


RHEL_9 5.14.0-427.42.1.el9_4
:   


Red Hat OpenShift and Red Hat CoreOS 4.17.11
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-11_release-notes){: external}.


HAProxy 14daa781a66ca5ed5754656ce53c3cca4af580b5
:   


## Worker node fix pack 4.17.9_1520_openshift, released 30 December 2024
{: #4179_1520_openshift_W}

The following list shows the changes that are in the worker node fix pack 4.17.9_1520_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 8 Packages
:   Worker node package updates for RHSA-2024:3043, CVE-2024-0690, RHSA-2024:11161, CVE-2024-52337.
{{site.data.keyword.openshiftshort}} and Red Hat CoreOS 4.17.9
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-9_release-notes){: external}.


## Worker node fix pack 4.17.8_1519_openshift, released 16 December 2024
{: #4178_1519_openshift_W}

The following list shows the changes that are in the worker node fix pack 4.17.8_1519_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 8 Packages 4.18.0-553.32.1.el8_10
:   Worker node kernel & package updates for RHSA-2024:3043, CVE-2024-0690, RHSA-2024:10943, CVE-2024-46695, CVE-2024-49949, CVE-2024-50082, CVE-2024-50099, CVE-2024-50110, CVE-2024-50142, CVE-2024-50192, CVE-2024-50256, CVE-2024-50264, RHSA-2024:10779, CVE-2024-11168, CVE-2024-9287, RHSA-2024:10784, CVE-2022-3064.
HAProxy 14daa78
:   Security fixes for CVE-2024-10963, CVE-2024-11168, CVE-2024-9287, CVE-2024-10041.
{{site.data.keyword.openshiftshort}} 4.17.8
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-8_release-notes){: external}.


## Worker node fix pack 4.17.5_1518_openshift, released 05 December 2024
{: #4175_1518_openshift_W}

The following list shows the changes that are in the worker node fix pack 4.17.5_1518_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 8 Packages 4.18.0-553.30.1.el8_10
:   Worker node kernel & package updates for RHSA-2024:10379, CVE-2024-10041, CVE-2024-10963, RHSA-2024:3043, CVE-2024-0690, RHSA-2024:10289, CVE-2021-33198, CVE-2021-4024, CVE-2024-9676, RHSA-2024:10281, CVE-2024-27043, CVE-2024-27399, CVE-2024-38564, CVE-2024-46858.
RHEL 9 Packages
:   
HAProxy
:   
{{site.data.keyword.openshiftshort}} and Red Hat CoreOS 4.17.5
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes){: external}.


## Master fix pack 4.17.5_1517_openshift, released 04 December 2024
{: #4175_1517_openshift_M}

The following list shows the changes that are in the master fix pack 4.17.5_1517_openshift. Master patch updates are applied automatically. 


{{site.data.keyword.cloud_notm}} Controller Manager v1.30.6-4
:   New version contains updates and security fixes.
Key Management Service provider v2.10.8
:   New version contains updates and security fixes.
Load balancer and load balancer monitor for {{site.data.keyword.cloud_notm}} Provider 3079
:   New version contains updates and security fixes.
Portieris admission controller v0.13.21
:   See the [Portieris admission controller release notes](https://github.com/{{site.data.keyword.IBM_notm}}/portieris/releases/tag/v0.13.21){: external}.
{{site.data.keyword.openshiftlong_notm}}. 4.17.5
:   See the [{{site.data.keyword.openshiftlong_notm}} release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-5_release-notes){: external}.


## Master fix pack 4.17.4_1515_openshift and worker node fix pack 4.17.4_1516_openshift, released 20 November 2024
{: #openshift_changelog_4174_1515}

IBM Cloud Controller Manager v1.30.6-3
:   New version contains updates and security fixes.
IBM Cloud RBAC Operator 743ed58
:   New version contains updates and security fixes.
Red Hat OpenShift (master) 4.17.4
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-4_release-notes){: external}
Red Hat OpenShift (worker node) 4.17.4
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/release_notes/ocp-4-17-release-notes#ocp-4-17-4_release-notes){: external}
Red Hat OpenShift on IBM Cloud Control Plane Operator, Metrics Server, and toolkit 4.17.0+20241112
:   See the [Red Hat OpenShift on IBM Cloud toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.17.0%2B20241112){: external}.
