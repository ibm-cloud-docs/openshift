---

copyright:
  years: 2026, 2026

lastupdated: "2026-10-07"


keywords: change log, version history, 4.20_openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}





# 4.20 version change log
{: #openshift_changelog_420}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run this version. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #changelog_overview_420}


Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security){: external} for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}

## Version 4.20
{: #420_components}


## 21 September 2026, Worker node fix pack 4.20.38_1563_openshift
{: #cl-boms-42038_1563_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.38_1563_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-687.47.1.el9_8
:   Resolves the following CVEs: [RHSA-2026:69126](https://access.redhat.com/errata/RHSA-2026:69126), [CVE-2026-8927](https://nvd.nist.gov/vuln/detail/cve-2026-8927), [RHSA-2026:67910](https://access.redhat.com/errata/RHSA-2026:67910), [CVE-2026-63381](https://nvd.nist.gov/vuln/detail/cve-2026-63381), [CVE-2026-63382](https://nvd.nist.gov/vuln/detail/cve-2026-63382), [CVE-2026-63383](https://nvd.nist.gov/vuln/detail/cve-2026-63383), [CVE-2026-63384](https://nvd.nist.gov/vuln/detail/cve-2026-63384), [CVE-2026-63385](https://nvd.nist.gov/vuln/detail/cve-2026-63385), [CVE-2026-63387](https://nvd.nist.gov/vuln/detail/cve-2026-63387), [CVE-2026-63388](https://nvd.nist.gov/vuln/detail/cve-2026-63388), [RHSA-2026:68011](https://access.redhat.com/errata/RHSA-2026:68011), [CVE-2025-35973](https://nvd.nist.gov/vuln/detail/cve-2025-35973), [RHSA-2026:69130](https://access.redhat.com/errata/RHSA-2026:69130), [CVE-2026-59999](https://nvd.nist.gov/vuln/detail/cve-2026-59999), [CVE-2026-73281](https://nvd.nist.gov/vuln/detail/cve-2026-73281), [CVE-2026-73282](https://nvd.nist.gov/vuln/detail/cve-2026-73282), [CVE-2026-73283](https://nvd.nist.gov/vuln/detail/cve-2026-73283), [RHSA-2026:67165](https://access.redhat.com/errata/RHSA-2026:67165), [CVE-2026-14457](https://nvd.nist.gov/vuln/detail/cve-2026-14457), [CVE-2026-18798](https://nvd.nist.gov/vuln/detail/cve-2026-18798), [CVE-2026-54874](https://nvd.nist.gov/vuln/detail/cve-2026-54874), [CVE-2026-63072](https://nvd.nist.gov/vuln/detail/cve-2026-63072), [CVE-2026-63073](https://nvd.nist.gov/vuln/detail/cve-2026-63073), [CVE-2026-63074](https://nvd.nist.gov/vuln/detail/cve-2026-63074), [CVE-2026-63075](https://nvd.nist.gov/vuln/detail/cve-2026-63075), [CVE-2026-63076](https://nvd.nist.gov/vuln/detail/cve-2026-63076), [RHSA-2026:69540](https://access.redhat.com/errata/RHSA-2026:69540), [RHSA-2026:69123](https://access.redhat.com/errata/RHSA-2026:69123), [RHSA-2026:66366](https://access.redhat.com/errata/RHSA-2026:66366), [CVE-2026-52859](https://nvd.nist.gov/vuln/detail/cve-2026-52859), [CVE-2026-55892](https://nvd.nist.gov/vuln/detail/cve-2026-55892), [CVE-2026-59857](https://nvd.nist.gov/vuln/detail/cve-2026-59857), [CVE-2026-73072](https://nvd.nist.gov/vuln/detail/cve-2026-73072), [CVE-2026-73076](https://nvd.nist.gov/vuln/detail/cve-2026-73076), [CVE-2026-73077](https://nvd.nist.gov/vuln/detail/cve-2026-73077), [CVE-2026-73078](https://nvd.nist.gov/vuln/detail/cve-2026-73078), [RHSA-2026:67583](https://access.redhat.com/errata/RHSA-2026:67583), [RHSA-2026:66403](https://access.redhat.com/errata/RHSA-2026:66403), [RHSA-2026:64812](https://access.redhat.com/errata/RHSA-2026:64812), [CVE-2026-56132](https://nvd.nist.gov/vuln/detail/cve-2026-56132), [RHSA-2026:67585](https://access.redhat.com/errata/RHSA-2026:67585), [RHSA-2026:64800](https://access.redhat.com/errata/RHSA-2026:64800), [RHSA-2026:67265](https://access.redhat.com/errata/RHSA-2026:67265), [CVE-2026-71226](https://nvd.nist.gov/vuln/detail/cve-2026-71226), [CVE-2026-71227](https://nvd.nist.gov/vuln/detail/cve-2026-71227), [RHSA-2026:64815](https://access.redhat.com/errata/RHSA-2026:64815), [RHSA-2026:67155](https://access.redhat.com/errata/RHSA-2026:67155), [RHSA-2026:64808](https://access.redhat.com/errata/RHSA-2026:64808), [CVE-2026-52933](https://nvd.nist.gov/vuln/detail/cve-2026-52933), [CVE-2026-53000](https://nvd.nist.gov/vuln/detail/cve-2026-53000), [CVE-2026-64136](https://nvd.nist.gov/vuln/detail/cve-2026-64136), [CVE-2026-64287](https://nvd.nist.gov/vuln/detail/cve-2026-64287), [CVE-2026-64319](https://nvd.nist.gov/vuln/detail/cve-2026-64319), [CVE-2026-64320](https://nvd.nist.gov/vuln/detail/cve-2026-64320), [CVE-2026-64384](https://nvd.nist.gov/vuln/detail/cve-2026-64384), [RHSA-2026:63129](https://access.redhat.com/errata/RHSA-2026:63129), [CVE-2025-71147](https://nvd.nist.gov/vuln/detail/cve-2025-71147), [CVE-2026-45970](https://nvd.nist.gov/vuln/detail/cve-2026-45970), [CVE-2026-46185](https://nvd.nist.gov/vuln/detail/cve-2026-46185), [CVE-2026-53073](https://nvd.nist.gov/vuln/detail/cve-2026-53073), [CVE-2026-53391](https://nvd.nist.gov/vuln/detail/cve-2026-53391), [CVE-2026-53392](https://nvd.nist.gov/vuln/detail/cve-2026-53392), [CVE-2026-53397](https://nvd.nist.gov/vuln/detail/cve-2026-53397), [CVE-2026-53399](https://nvd.nist.gov/vuln/detail/cve-2026-53399), [CVE-2026-63800](https://nvd.nist.gov/vuln/detail/cve-2026-63800), [CVE-2026-63808](https://nvd.nist.gov/vuln/detail/cve-2026-63808), [CVE-2026-63824](https://nvd.nist.gov/vuln/detail/cve-2026-63824), [CVE-2026-63886](https://nvd.nist.gov/vuln/detail/cve-2026-63886), [CVE-2026-63887](https://nvd.nist.gov/vuln/detail/cve-2026-63887), [CVE-2026-64002](https://nvd.nist.gov/vuln/detail/cve-2026-64002), [CVE-2026-64018](https://nvd.nist.gov/vuln/detail/cve-2026-64018), [CVE-2026-64268](https://nvd.nist.gov/vuln/detail/cve-2026-64268), [CVE-2026-64298](https://nvd.nist.gov/vuln/detail/cve-2026-64298), [CVE-2026-64304](https://nvd.nist.gov/vuln/detail/cve-2026-64304), [CVE-2026-64387](https://nvd.nist.gov/vuln/detail/cve-2026-64387), [CVE-2026-64438](https://nvd.nist.gov/vuln/detail/cve-2026-64438), [CVE-2026-64490](https://nvd.nist.gov/vuln/detail/cve-2026-64490), [CVE-2026-68145](https://nvd.nist.gov/vuln/detail/cve-2026-68145), [CVE-2026-68166](https://nvd.nist.gov/vuln/detail/cve-2026-68166), [CVE-2026-68480](https://nvd.nist.gov/vuln/detail/cve-2026-68480), [CVE-2026-72069](https://nvd.nist.gov/vuln/detail/cve-2026-72069), [CVE-2026-72130](https://nvd.nist.gov/vuln/detail/cve-2026-72130), [RHSA-2026:66180](https://access.redhat.com/errata/RHSA-2026:66180), [CVE-2026-43339](https://nvd.nist.gov/vuln/detail/cve-2026-43339), [CVE-2026-43493](https://nvd.nist.gov/vuln/detail/cve-2026-43493), [CVE-2026-46015](https://nvd.nist.gov/vuln/detail/cve-2026-46015), [CVE-2026-46149](https://nvd.nist.gov/vuln/detail/cve-2026-46149), [CVE-2026-46266](https://nvd.nist.gov/vuln/detail/cve-2026-46266), [CVE-2026-46306](https://nvd.nist.gov/vuln/detail/cve-2026-46306), [CVE-2026-46330](https://nvd.nist.gov/vuln/detail/cve-2026-46330), [CVE-2026-53002](https://nvd.nist.gov/vuln/detail/cve-2026-53002), [CVE-2026-53223](https://nvd.nist.gov/vuln/detail/cve-2026-53223), [CVE-2026-53275](https://nvd.nist.gov/vuln/detail/cve-2026-53275), [CVE-2026-53366](https://nvd.nist.gov/vuln/detail/cve-2026-53366), [CVE-2026-64034](https://nvd.nist.gov/vuln/detail/cve-2026-64034), [CVE-2026-64563](https://nvd.nist.gov/vuln/detail/cve-2026-64563), [CVE-2026-64597](https://nvd.nist.gov/vuln/detail/cve-2026-64597), [CVE-2026-72129](https://nvd.nist.gov/vuln/detail/cve-2026-72129), [CVE-2026-74480](https://nvd.nist.gov/vuln/detail/cve-2026-74480), [RHSA-2026:67150](https://access.redhat.com/errata/RHSA-2026:67150), [CVE-2026-23466](https://nvd.nist.gov/vuln/detail/cve-2026-23466), [CVE-2026-31479](https://nvd.nist.gov/vuln/detail/cve-2026-31479), [CVE-2026-31566](https://nvd.nist.gov/vuln/detail/cve-2026-31566), [CVE-2026-31656](https://nvd.nist.gov/vuln/detail/cve-2026-31656), [CVE-2026-31692](https://nvd.nist.gov/vuln/detail/cve-2026-31692), [CVE-2026-43334](https://nvd.nist.gov/vuln/detail/cve-2026-43334), [CVE-2026-43368](https://nvd.nist.gov/vuln/detail/cve-2026-43368), [CVE-2026-43370](https://nvd.nist.gov/vuln/detail/cve-2026-43370), [CVE-2026-52917](https://nvd.nist.gov/vuln/detail/cve-2026-52917), [CVE-2026-52918](https://nvd.nist.gov/vuln/detail/cve-2026-52918), [CVE-2026-52947](https://nvd.nist.gov/vuln/detail/cve-2026-52947), [CVE-2026-53053](https://nvd.nist.gov/vuln/detail/cve-2026-53053), [CVE-2026-53072](https://nvd.nist.gov/vuln/detail/cve-2026-53072), [CVE-2026-53091](https://nvd.nist.gov/vuln/detail/cve-2026-53091), [CVE-2026-53182](https://nvd.nist.gov/vuln/detail/cve-2026-53182), [CVE-2026-53209](https://nvd.nist.gov/vuln/detail/cve-2026-53209), [CVE-2026-53246](https://nvd.nist.gov/vuln/detail/cve-2026-53246), [CVE-2026-53254](https://nvd.nist.gov/vuln/detail/cve-2026-53254), [CVE-2026-53256](https://nvd.nist.gov/vuln/detail/cve-2026-53256), [CVE-2026-63801](https://nvd.nist.gov/vuln/detail/cve-2026-63801), [CVE-2026-63889](https://nvd.nist.gov/vuln/detail/cve-2026-63889), [CVE-2026-63944](https://nvd.nist.gov/vuln/detail/cve-2026-63944), [CVE-2026-63945](https://nvd.nist.gov/vuln/detail/cve-2026-63945), [CVE-2026-63946](https://nvd.nist.gov/vuln/detail/cve-2026-63946), [CVE-2026-63947](https://nvd.nist.gov/vuln/detail/cve-2026-63947), [CVE-2026-63971](https://nvd.nist.gov/vuln/detail/cve-2026-63971), [CVE-2026-63975](https://nvd.nist.gov/vuln/detail/cve-2026-63975), [CVE-2026-64037](https://nvd.nist.gov/vuln/detail/cve-2026-64037), [CVE-2026-64113](https://nvd.nist.gov/vuln/detail/cve-2026-64113), [CVE-2026-64117](https://nvd.nist.gov/vuln/detail/cve-2026-64117), [CVE-2026-64255](https://nvd.nist.gov/vuln/detail/cve-2026-64255), [CVE-2026-64515](https://nvd.nist.gov/vuln/detail/cve-2026-64515), [CVE-2026-68086](https://nvd.nist.gov/vuln/detail/cve-2026-68086), [CVE-2026-68117](https://nvd.nist.gov/vuln/detail/cve-2026-68117), [CVE-2026-68264](https://nvd.nist.gov/vuln/detail/cve-2026-68264), [CVE-2026-68300](https://nvd.nist.gov/vuln/detail/cve-2026-68300), [CVE-2026-68315](https://nvd.nist.gov/vuln/detail/cve-2026-68315), [CVE-2026-68376](https://nvd.nist.gov/vuln/detail/cve-2026-68376), [CVE-2026-68402](https://nvd.nist.gov/vuln/detail/cve-2026-68402), [CVE-2026-68406](https://nvd.nist.gov/vuln/detail/cve-2026-68406), and [CVE-2026-72098](https://nvd.nist.gov/vuln/detail/cve-2026-72098).


RHEL 9 (Satellite) 5.14.0-687.47.1.el9_8
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-687.47.1.el9_8
:   Resolves the following CVEs: [RHSA-2026:69126](https://access.redhat.com/errata/RHSA-2026:69126), [CVE-2026-8927](https://nvd.nist.gov/vuln/detail/cve-2026-8927), [RHSA-2026:67910](https://access.redhat.com/errata/RHSA-2026:67910), [CVE-2026-63381](https://nvd.nist.gov/vuln/detail/cve-2026-63381), [CVE-2026-63382](https://nvd.nist.gov/vuln/detail/cve-2026-63382), [CVE-2026-63383](https://nvd.nist.gov/vuln/detail/cve-2026-63383), [CVE-2026-63384](https://nvd.nist.gov/vuln/detail/cve-2026-63384), [CVE-2026-63385](https://nvd.nist.gov/vuln/detail/cve-2026-63385), [CVE-2026-63387](https://nvd.nist.gov/vuln/detail/cve-2026-63387), [CVE-2026-63388](https://nvd.nist.gov/vuln/detail/cve-2026-63388), [RHSA-2026:68011](https://access.redhat.com/errata/RHSA-2026:68011), [CVE-2025-35973](https://nvd.nist.gov/vuln/detail/cve-2025-35973), [RHSA-2026:69130](https://access.redhat.com/errata/RHSA-2026:69130), [CVE-2026-59999](https://nvd.nist.gov/vuln/detail/cve-2026-59999), [CVE-2026-73281](https://nvd.nist.gov/vuln/detail/cve-2026-73281), [CVE-2026-73282](https://nvd.nist.gov/vuln/detail/cve-2026-73282), [CVE-2026-73283](https://nvd.nist.gov/vuln/detail/cve-2026-73283), [RHSA-2026:67165](https://access.redhat.com/errata/RHSA-2026:67165), [CVE-2026-14457](https://nvd.nist.gov/vuln/detail/cve-2026-14457), [CVE-2026-18798](https://nvd.nist.gov/vuln/detail/cve-2026-18798), [CVE-2026-54874](https://nvd.nist.gov/vuln/detail/cve-2026-54874), [CVE-2026-63072](https://nvd.nist.gov/vuln/detail/cve-2026-63072), [CVE-2026-63073](https://nvd.nist.gov/vuln/detail/cve-2026-63073), [CVE-2026-63074](https://nvd.nist.gov/vuln/detail/cve-2026-63074), [CVE-2026-63075](https://nvd.nist.gov/vuln/detail/cve-2026-63075), [CVE-2026-63076](https://nvd.nist.gov/vuln/detail/cve-2026-63076), [RHSA-2026:69540](https://access.redhat.com/errata/RHSA-2026:69540), [RHSA-2026:69123](https://access.redhat.com/errata/RHSA-2026:69123), [RHSA-2026:66366](https://access.redhat.com/errata/RHSA-2026:66366), [CVE-2026-52859](https://nvd.nist.gov/vuln/detail/cve-2026-52859), [CVE-2026-55892](https://nvd.nist.gov/vuln/detail/cve-2026-55892), [CVE-2026-59857](https://nvd.nist.gov/vuln/detail/cve-2026-59857), [CVE-2026-73072](https://nvd.nist.gov/vuln/detail/cve-2026-73072), [CVE-2026-73076](https://nvd.nist.gov/vuln/detail/cve-2026-73076), [CVE-2026-73077](https://nvd.nist.gov/vuln/detail/cve-2026-73077), [CVE-2026-73078](https://nvd.nist.gov/vuln/detail/cve-2026-73078), [RHSA-2026:67583](https://access.redhat.com/errata/RHSA-2026:67583), [RHSA-2026:66403](https://access.redhat.com/errata/RHSA-2026:66403), [RHSA-2026:64812](https://access.redhat.com/errata/RHSA-2026:64812), [CVE-2026-56132](https://nvd.nist.gov/vuln/detail/cve-2026-56132), [RHSA-2026:67585](https://access.redhat.com/errata/RHSA-2026:67585), [RHSA-2026:64800](https://access.redhat.com/errata/RHSA-2026:64800), [RHSA-2026:67265](https://access.redhat.com/errata/RHSA-2026:67265), [CVE-2026-71226](https://nvd.nist.gov/vuln/detail/cve-2026-71226), [CVE-2026-71227](https://nvd.nist.gov/vuln/detail/cve-2026-71227), [RHSA-2026:64815](https://access.redhat.com/errata/RHSA-2026:64815), [RHSA-2026:67155](https://access.redhat.com/errata/RHSA-2026:67155), [RHSA-2026:64808](https://access.redhat.com/errata/RHSA-2026:64808), [CVE-2026-52933](https://nvd.nist.gov/vuln/detail/cve-2026-52933), [CVE-2026-53000](https://nvd.nist.gov/vuln/detail/cve-2026-53000), [CVE-2026-64136](https://nvd.nist.gov/vuln/detail/cve-2026-64136), [CVE-2026-64287](https://nvd.nist.gov/vuln/detail/cve-2026-64287), [CVE-2026-64319](https://nvd.nist.gov/vuln/detail/cve-2026-64319), [CVE-2026-64320](https://nvd.nist.gov/vuln/detail/cve-2026-64320), [CVE-2026-64384](https://nvd.nist.gov/vuln/detail/cve-2026-64384), [RHSA-2026:63129](https://access.redhat.com/errata/RHSA-2026:63129), [CVE-2025-71147](https://nvd.nist.gov/vuln/detail/cve-2025-71147), [CVE-2026-45970](https://nvd.nist.gov/vuln/detail/cve-2026-45970), [CVE-2026-46185](https://nvd.nist.gov/vuln/detail/cve-2026-46185), [CVE-2026-53073](https://nvd.nist.gov/vuln/detail/cve-2026-53073), [CVE-2026-53391](https://nvd.nist.gov/vuln/detail/cve-2026-53391), [CVE-2026-53392](https://nvd.nist.gov/vuln/detail/cve-2026-53392), [CVE-2026-53397](https://nvd.nist.gov/vuln/detail/cve-2026-53397), [CVE-2026-53399](https://nvd.nist.gov/vuln/detail/cve-2026-53399), [CVE-2026-63800](https://nvd.nist.gov/vuln/detail/cve-2026-63800), [CVE-2026-63808](https://nvd.nist.gov/vuln/detail/cve-2026-63808), [CVE-2026-63824](https://nvd.nist.gov/vuln/detail/cve-2026-63824), [CVE-2026-63886](https://nvd.nist.gov/vuln/detail/cve-2026-63886), [CVE-2026-63887](https://nvd.nist.gov/vuln/detail/cve-2026-63887), [CVE-2026-64002](https://nvd.nist.gov/vuln/detail/cve-2026-64002), [CVE-2026-64018](https://nvd.nist.gov/vuln/detail/cve-2026-64018), [CVE-2026-64268](https://nvd.nist.gov/vuln/detail/cve-2026-64268), [CVE-2026-64298](https://nvd.nist.gov/vuln/detail/cve-2026-64298), [CVE-2026-64304](https://nvd.nist.gov/vuln/detail/cve-2026-64304), [CVE-2026-64387](https://nvd.nist.gov/vuln/detail/cve-2026-64387), [CVE-2026-64438](https://nvd.nist.gov/vuln/detail/cve-2026-64438), [CVE-2026-64490](https://nvd.nist.gov/vuln/detail/cve-2026-64490), [CVE-2026-68145](https://nvd.nist.gov/vuln/detail/cve-2026-68145), [CVE-2026-68166](https://nvd.nist.gov/vuln/detail/cve-2026-68166), [CVE-2026-68480](https://nvd.nist.gov/vuln/detail/cve-2026-68480), [CVE-2026-72069](https://nvd.nist.gov/vuln/detail/cve-2026-72069), [CVE-2026-72130](https://nvd.nist.gov/vuln/detail/cve-2026-72130), [RHSA-2026:66180](https://access.redhat.com/errata/RHSA-2026:66180), [CVE-2026-43339](https://nvd.nist.gov/vuln/detail/cve-2026-43339), [CVE-2026-43493](https://nvd.nist.gov/vuln/detail/cve-2026-43493), [CVE-2026-46015](https://nvd.nist.gov/vuln/detail/cve-2026-46015), [CVE-2026-46149](https://nvd.nist.gov/vuln/detail/cve-2026-46149), [CVE-2026-46266](https://nvd.nist.gov/vuln/detail/cve-2026-46266), [CVE-2026-46306](https://nvd.nist.gov/vuln/detail/cve-2026-46306), [CVE-2026-46330](https://nvd.nist.gov/vuln/detail/cve-2026-46330), [CVE-2026-53002](https://nvd.nist.gov/vuln/detail/cve-2026-53002), [CVE-2026-53223](https://nvd.nist.gov/vuln/detail/cve-2026-53223), [CVE-2026-53275](https://nvd.nist.gov/vuln/detail/cve-2026-53275), [CVE-2026-53366](https://nvd.nist.gov/vuln/detail/cve-2026-53366), [CVE-2026-64034](https://nvd.nist.gov/vuln/detail/cve-2026-64034), [CVE-2026-64563](https://nvd.nist.gov/vuln/detail/cve-2026-64563), [CVE-2026-64597](https://nvd.nist.gov/vuln/detail/cve-2026-64597), [CVE-2026-72129](https://nvd.nist.gov/vuln/detail/cve-2026-72129), [CVE-2026-74480](https://nvd.nist.gov/vuln/detail/cve-2026-74480), [RHSA-2026:67150](https://access.redhat.com/errata/RHSA-2026:67150), [CVE-2026-23466](https://nvd.nist.gov/vuln/detail/cve-2026-23466), [CVE-2026-31479](https://nvd.nist.gov/vuln/detail/cve-2026-31479), [CVE-2026-31566](https://nvd.nist.gov/vuln/detail/cve-2026-31566), [CVE-2026-31656](https://nvd.nist.gov/vuln/detail/cve-2026-31656), [CVE-2026-31692](https://nvd.nist.gov/vuln/detail/cve-2026-31692), [CVE-2026-43334](https://nvd.nist.gov/vuln/detail/cve-2026-43334), [CVE-2026-43368](https://nvd.nist.gov/vuln/detail/cve-2026-43368), [CVE-2026-43370](https://nvd.nist.gov/vuln/detail/cve-2026-43370), [CVE-2026-52917](https://nvd.nist.gov/vuln/detail/cve-2026-52917), [CVE-2026-52918](https://nvd.nist.gov/vuln/detail/cve-2026-52918), [CVE-2026-52947](https://nvd.nist.gov/vuln/detail/cve-2026-52947), [CVE-2026-53053](https://nvd.nist.gov/vuln/detail/cve-2026-53053), [CVE-2026-53072](https://nvd.nist.gov/vuln/detail/cve-2026-53072), [CVE-2026-53091](https://nvd.nist.gov/vuln/detail/cve-2026-53091), [CVE-2026-53182](https://nvd.nist.gov/vuln/detail/cve-2026-53182), [CVE-2026-53209](https://nvd.nist.gov/vuln/detail/cve-2026-53209), [CVE-2026-53246](https://nvd.nist.gov/vuln/detail/cve-2026-53246), [CVE-2026-53254](https://nvd.nist.gov/vuln/detail/cve-2026-53254), [CVE-2026-53256](https://nvd.nist.gov/vuln/detail/cve-2026-53256), [CVE-2026-63801](https://nvd.nist.gov/vuln/detail/cve-2026-63801), [CVE-2026-63889](https://nvd.nist.gov/vuln/detail/cve-2026-63889), [CVE-2026-63944](https://nvd.nist.gov/vuln/detail/cve-2026-63944), [CVE-2026-63945](https://nvd.nist.gov/vuln/detail/cve-2026-63945), [CVE-2026-63946](https://nvd.nist.gov/vuln/detail/cve-2026-63946), [CVE-2026-63947](https://nvd.nist.gov/vuln/detail/cve-2026-63947), [CVE-2026-63971](https://nvd.nist.gov/vuln/detail/cve-2026-63971), [CVE-2026-63975](https://nvd.nist.gov/vuln/detail/cve-2026-63975), [CVE-2026-64037](https://nvd.nist.gov/vuln/detail/cve-2026-64037), [CVE-2026-64113](https://nvd.nist.gov/vuln/detail/cve-2026-64113), [CVE-2026-64117](https://nvd.nist.gov/vuln/detail/cve-2026-64117), [CVE-2026-64255](https://nvd.nist.gov/vuln/detail/cve-2026-64255), [CVE-2026-64515](https://nvd.nist.gov/vuln/detail/cve-2026-64515), [CVE-2026-68086](https://nvd.nist.gov/vuln/detail/cve-2026-68086), [CVE-2026-68117](https://nvd.nist.gov/vuln/detail/cve-2026-68117), [CVE-2026-68264](https://nvd.nist.gov/vuln/detail/cve-2026-68264), [CVE-2026-68300](https://nvd.nist.gov/vuln/detail/cve-2026-68300), [CVE-2026-68315](https://nvd.nist.gov/vuln/detail/cve-2026-68315), [CVE-2026-68376](https://nvd.nist.gov/vuln/detail/cve-2026-68376), [CVE-2026-68402](https://nvd.nist.gov/vuln/detail/cve-2026-68402), [CVE-2026-68406](https://nvd.nist.gov/vuln/detail/cve-2026-68406), and [CVE-2026-72098](https://nvd.nist.gov/vuln/detail/cve-2026-72098).


Red Hat OpenShift 4.20.38
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-38_release-notes){: external}.


Red Hat CoreOS 4.20.38
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-38_release-notes){: external}.


HAProxy b08f074d475aeb8ba959b03272daab5d46deec0c
:   Resolves the following CVEs: [CVE-2026-41991](https://nvd.nist.gov/vuln/detail/cve-2026-41991), [CVE-2026-50219](https://nvd.nist.gov/vuln/detail/cve-2026-50219), [CVE-2026-16118](https://nvd.nist.gov/vuln/detail/cve-2026-16118), [CVE-2026-56132](https://nvd.nist.gov/vuln/detail/cve-2026-56132), and [CVE-2026-41992](https://nvd.nist.gov/vuln/detail/cve-2026-41992).


## 21 September 2026, Master fix pack 4.20.36_1562_openshift
{: #cl-boms_master-42036_1562_openshift_M}

The following list shows the components that are in the master fix pack 4.20.36_1562_openshift. Master patch updates are applied automatically.
{: shortdesc}

Cluster health image v1.6.19
:   New version contains updates and security fixes.


etcd v3.5.33
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.33){: external}.


IBM Cloud Block Storage driver and plug-in v2.5.28
:   New version contains updates and security fixes.


IBM Cloud Controller Manager v1.33.13-11
:   New version contains updates and security fixes.


IBM Cloud File Storage for Classic plug-in and monitor v457
:   New version contains updates and security fixes.


IBM Cloud RBAC Operator 109756b
:   New version contains updates and security fixes.


Key Management Service provider 2.10.30
:   New version contains updates and security fixes.


Portieris admission controller v0.14.3
:   See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.14.3){: external}


Red Hat OpenShift on IBM Cloud 4.20.36
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes#ocp-4-20-36_release-notes){: external}.


## 08 September 2026, Worker node fix pack 4.20.36_1561_openshift
{: #cl-boms-42036_1561_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.36_1561_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-687.42.1.el9_8
:   Resolves the following CVEs: [RHSA-2026:63130](https://access.redhat.com/errata/RHSA-2026:63130), [CVE-2026-33818](https://nvd.nist.gov/vuln/detail/cve-2026-33818), [CVE-2026-56858](https://nvd.nist.gov/vuln/detail/cve-2026-56858), [CVE-2026-56860](https://nvd.nist.gov/vuln/detail/cve-2026-56860), [CVE-2026-56862](https://nvd.nist.gov/vuln/detail/cve-2026-56862), [RHSA-2026:58936](https://access.redhat.com/errata/RHSA-2026:58936), [CVE-2026-11822](https://nvd.nist.gov/vuln/detail/cve-2026-11822), [CVE-2026-11824](https://nvd.nist.gov/vuln/detail/cve-2026-11824), [RHSA-2026:60226](https://access.redhat.com/errata/RHSA-2026:60226), [CVE-2026-54371](https://nvd.nist.gov/vuln/detail/cve-2026-54371), [RHSA-2026:61355](https://access.redhat.com/errata/RHSA-2026:61355), [CVE-2026-16730](https://nvd.nist.gov/vuln/detail/cve-2026-16730), [RHSA-2026:61623](https://access.redhat.com/errata/RHSA-2026:61623), [CVE-2026-41991](https://nvd.nist.gov/vuln/detail/cve-2026-41991), [CVE-2026-41992](https://nvd.nist.gov/vuln/detail/cve-2026-41992), [RHSA-2026:62217](https://access.redhat.com/errata/RHSA-2026:62217), [CVE-2026-59843](https://nvd.nist.gov/vuln/detail/cve-2026-59843), [CVE-2026-59844](https://nvd.nist.gov/vuln/detail/cve-2026-59844), [CVE-2026-59845](https://nvd.nist.gov/vuln/detail/cve-2026-59845), [CVE-2026-59846](https://nvd.nist.gov/vuln/detail/cve-2026-59846), [CVE-2026-59847](https://nvd.nist.gov/vuln/detail/cve-2026-59847), [CVE-2026-59848](https://nvd.nist.gov/vuln/detail/cve-2026-59848), [CVE-2026-59850](https://nvd.nist.gov/vuln/detail/cve-2026-59850), [RHSA-2026:61247](https://access.redhat.com/errata/RHSA-2026:61247), [CVE-2026-11979](https://nvd.nist.gov/vuln/detail/cve-2026-11979), [CVE-2026-6653](https://nvd.nist.gov/vuln/detail/cve-2026-6653), [RHSA-2026:58572](https://access.redhat.com/errata/RHSA-2026:58572), [CVE-2026-10805](https://nvd.nist.gov/vuln/detail/cve-2026-10805), [RHSA-2026:61581](https://access.redhat.com/errata/RHSA-2026:61581), [CVE-2026-18477](https://nvd.nist.gov/vuln/detail/cve-2026-18477), [CVE-2026-18508](https://nvd.nist.gov/vuln/detail/cve-2026-18508), [CVE-2026-5704](https://nvd.nist.gov/vuln/detail/cve-2026-5704), [RHSA-2026:62143](https://access.redhat.com/errata/RHSA-2026:62143), [CVE-2026-58471](https://nvd.nist.gov/vuln/detail/cve-2026-58471), [CVE-2026-58472](https://nvd.nist.gov/vuln/detail/cve-2026-58472), [RHSA-2026:57252](https://access.redhat.com/errata/RHSA-2026:57252), [CVE-2026-43206](https://nvd.nist.gov/vuln/detail/cve-2026-43206), [CVE-2026-43233](https://nvd.nist.gov/vuln/detail/cve-2026-43233), [CVE-2026-43237](https://nvd.nist.gov/vuln/detail/cve-2026-43237), [CVE-2026-45878](https://nvd.nist.gov/vuln/detail/cve-2026-45878), [CVE-2026-45991](https://nvd.nist.gov/vuln/detail/cve-2026-45991), [CVE-2026-46120](https://nvd.nist.gov/vuln/detail/cve-2026-46120), [CVE-2026-52991](https://nvd.nist.gov/vuln/detail/cve-2026-52991), [CVE-2026-53136](https://nvd.nist.gov/vuln/detail/cve-2026-53136), [CVE-2026-53143](https://nvd.nist.gov/vuln/detail/cve-2026-53143), [CVE-2026-53189](https://nvd.nist.gov/vuln/detail/cve-2026-53189), [CVE-2026-53329](https://nvd.nist.gov/vuln/detail/cve-2026-53329), [CVE-2026-53356](https://nvd.nist.gov/vuln/detail/cve-2026-53356), [CVE-2026-53374](https://nvd.nist.gov/vuln/detail/cve-2026-53374), [CVE-2026-63879](https://nvd.nist.gov/vuln/detail/cve-2026-63879), [CVE-2026-63884](https://nvd.nist.gov/vuln/detail/cve-2026-63884), [CVE-2026-63888](https://nvd.nist.gov/vuln/detail/cve-2026-63888), [CVE-2026-63952](https://nvd.nist.gov/vuln/detail/cve-2026-63952), [CVE-2026-64007](https://nvd.nist.gov/vuln/detail/cve-2026-64007), [CVE-2026-64048](https://nvd.nist.gov/vuln/detail/cve-2026-64048), [CVE-2026-64219](https://nvd.nist.gov/vuln/detail/cve-2026-64219), [CVE-2026-64379](https://nvd.nist.gov/vuln/detail/cve-2026-64379), [CVE-2026-64382](https://nvd.nist.gov/vuln/detail/cve-2026-64382), [CVE-2026-64386](https://nvd.nist.gov/vuln/detail/cve-2026-64386), [CVE-2026-64560](https://nvd.nist.gov/vuln/detail/cve-2026-64560), [CVE-2026-68343](https://nvd.nist.gov/vuln/detail/cve-2026-68343), [CVE-2026-68388](https://nvd.nist.gov/vuln/detail/cve-2026-68388), [RHSA-2026:59723](https://access.redhat.com/errata/RHSA-2026:59723), [CVE-2025-68211](https://nvd.nist.gov/vuln/detail/cve-2025-68211), [CVE-2026-23003](https://nvd.nist.gov/vuln/detail/cve-2026-23003), [CVE-2026-43114](https://nvd.nist.gov/vuln/detail/cve-2026-43114), [CVE-2026-52920](https://nvd.nist.gov/vuln/detail/cve-2026-52920), [CVE-2026-52924](https://nvd.nist.gov/vuln/detail/cve-2026-52924), [CVE-2026-53131](https://nvd.nist.gov/vuln/detail/cve-2026-53131), [CVE-2026-53185](https://nvd.nist.gov/vuln/detail/cve-2026-53185), [CVE-2026-53268](https://nvd.nist.gov/vuln/detail/cve-2026-53268), [CVE-2026-64189](https://nvd.nist.gov/vuln/detail/cve-2026-64189), [CVE-2026-64191](https://nvd.nist.gov/vuln/detail/cve-2026-64191), [CVE-2026-64276](https://nvd.nist.gov/vuln/detail/cve-2026-64276), [CVE-2026-64277](https://nvd.nist.gov/vuln/detail/cve-2026-64277), and [CVE-2026-74581](https://nvd.nist.gov/vuln/detail/cve-2026-74581).


RHEL 9 (Satellite) 5.14.0-687.42.1.el9_8
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-687.42.1.el9_8
:   Resolves the following CVEs: [RHSA-2026:63130](https://access.redhat.com/errata/RHSA-2026:63130), [CVE-2026-33818](https://nvd.nist.gov/vuln/detail/cve-2026-33818), [CVE-2026-56858](https://nvd.nist.gov/vuln/detail/cve-2026-56858), [CVE-2026-56860](https://nvd.nist.gov/vuln/detail/cve-2026-56860), [CVE-2026-56862](https://nvd.nist.gov/vuln/detail/cve-2026-56862), [RHSA-2026:58936](https://access.redhat.com/errata/RHSA-2026:58936), [CVE-2026-11822](https://nvd.nist.gov/vuln/detail/cve-2026-11822), [CVE-2026-11824](https://nvd.nist.gov/vuln/detail/cve-2026-11824), [RHSA-2026:60226](https://access.redhat.com/errata/RHSA-2026:60226), [CVE-2026-54371](https://nvd.nist.gov/vuln/detail/cve-2026-54371), [RHSA-2026:61355](https://access.redhat.com/errata/RHSA-2026:61355), [CVE-2026-16730](https://nvd.nist.gov/vuln/detail/cve-2026-16730), [RHSA-2026:61623](https://access.redhat.com/errata/RHSA-2026:61623), [CVE-2026-41991](https://nvd.nist.gov/vuln/detail/cve-2026-41991), [CVE-2026-41992](https://nvd.nist.gov/vuln/detail/cve-2026-41992), [RHSA-2026:62217](https://access.redhat.com/errata/RHSA-2026:62217), [CVE-2026-59843](https://nvd.nist.gov/vuln/detail/cve-2026-59843), [CVE-2026-59844](https://nvd.nist.gov/vuln/detail/cve-2026-59844), [CVE-2026-59845](https://nvd.nist.gov/vuln/detail/cve-2026-59845), [CVE-2026-59846](https://nvd.nist.gov/vuln/detail/cve-2026-59846), [CVE-2026-59847](https://nvd.nist.gov/vuln/detail/cve-2026-59847), [CVE-2026-59848](https://nvd.nist.gov/vuln/detail/cve-2026-59848), [CVE-2026-59850](https://nvd.nist.gov/vuln/detail/cve-2026-59850), [RHSA-2026:61247](https://access.redhat.com/errata/RHSA-2026:61247), [CVE-2026-11979](https://nvd.nist.gov/vuln/detail/cve-2026-11979), [CVE-2026-6653](https://nvd.nist.gov/vuln/detail/cve-2026-6653), [RHSA-2026:58572](https://access.redhat.com/errata/RHSA-2026:58572), [CVE-2026-10805](https://nvd.nist.gov/vuln/detail/cve-2026-10805), [RHSA-2026:61581](https://access.redhat.com/errata/RHSA-2026:61581), [CVE-2026-18477](https://nvd.nist.gov/vuln/detail/cve-2026-18477), [CVE-2026-18508](https://nvd.nist.gov/vuln/detail/cve-2026-18508), [CVE-2026-5704](https://nvd.nist.gov/vuln/detail/cve-2026-5704), [RHSA-2026:62143](https://access.redhat.com/errata/RHSA-2026:62143), [CVE-2026-58471](https://nvd.nist.gov/vuln/detail/cve-2026-58471), [CVE-2026-58472](https://nvd.nist.gov/vuln/detail/cve-2026-58472), [RHSA-2026:57252](https://access.redhat.com/errata/RHSA-2026:57252), [CVE-2026-43206](https://nvd.nist.gov/vuln/detail/cve-2026-43206), [CVE-2026-43233](https://nvd.nist.gov/vuln/detail/cve-2026-43233), [CVE-2026-43237](https://nvd.nist.gov/vuln/detail/cve-2026-43237), [CVE-2026-45878](https://nvd.nist.gov/vuln/detail/cve-2026-45878), [CVE-2026-45991](https://nvd.nist.gov/vuln/detail/cve-2026-45991), [CVE-2026-46120](https://nvd.nist.gov/vuln/detail/cve-2026-46120), [CVE-2026-52991](https://nvd.nist.gov/vuln/detail/cve-2026-52991), [CVE-2026-53136](https://nvd.nist.gov/vuln/detail/cve-2026-53136), [CVE-2026-53143](https://nvd.nist.gov/vuln/detail/cve-2026-53143), [CVE-2026-53189](https://nvd.nist.gov/vuln/detail/cve-2026-53189), [CVE-2026-53329](https://nvd.nist.gov/vuln/detail/cve-2026-53329), [CVE-2026-53356](https://nvd.nist.gov/vuln/detail/cve-2026-53356), [CVE-2026-53374](https://nvd.nist.gov/vuln/detail/cve-2026-53374), [CVE-2026-63879](https://nvd.nist.gov/vuln/detail/cve-2026-63879), [CVE-2026-63884](https://nvd.nist.gov/vuln/detail/cve-2026-63884), [CVE-2026-63888](https://nvd.nist.gov/vuln/detail/cve-2026-63888), [CVE-2026-63952](https://nvd.nist.gov/vuln/detail/cve-2026-63952), [CVE-2026-64007](https://nvd.nist.gov/vuln/detail/cve-2026-64007), [CVE-2026-64048](https://nvd.nist.gov/vuln/detail/cve-2026-64048), [CVE-2026-64219](https://nvd.nist.gov/vuln/detail/cve-2026-64219), [CVE-2026-64379](https://nvd.nist.gov/vuln/detail/cve-2026-64379), [CVE-2026-64382](https://nvd.nist.gov/vuln/detail/cve-2026-64382), [CVE-2026-64386](https://nvd.nist.gov/vuln/detail/cve-2026-64386), [CVE-2026-64560](https://nvd.nist.gov/vuln/detail/cve-2026-64560), [CVE-2026-68343](https://nvd.nist.gov/vuln/detail/cve-2026-68343), [CVE-2026-68388](https://nvd.nist.gov/vuln/detail/cve-2026-68388), [RHSA-2026:59723](https://access.redhat.com/errata/RHSA-2026:59723), [CVE-2025-68211](https://nvd.nist.gov/vuln/detail/cve-2025-68211), [CVE-2026-23003](https://nvd.nist.gov/vuln/detail/cve-2026-23003), [CVE-2026-43114](https://nvd.nist.gov/vuln/detail/cve-2026-43114), [CVE-2026-52920](https://nvd.nist.gov/vuln/detail/cve-2026-52920), [CVE-2026-52924](https://nvd.nist.gov/vuln/detail/cve-2026-52924), [CVE-2026-53131](https://nvd.nist.gov/vuln/detail/cve-2026-53131), [CVE-2026-53185](https://nvd.nist.gov/vuln/detail/cve-2026-53185), [CVE-2026-53268](https://nvd.nist.gov/vuln/detail/cve-2026-53268), [CVE-2026-64189](https://nvd.nist.gov/vuln/detail/cve-2026-64189), [CVE-2026-64191](https://nvd.nist.gov/vuln/detail/cve-2026-64191), [CVE-2026-64276](https://nvd.nist.gov/vuln/detail/cve-2026-64276), [CVE-2026-64277](https://nvd.nist.gov/vuln/detail/cve-2026-64277), and [CVE-2026-74581](https://nvd.nist.gov/vuln/detail/cve-2026-74581).


Red Hat OpenShift 4.20.36
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-36_release-notes){: external}.


Red Hat CoreOS 4.20.36
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-36_release-notes){: external}.


HAProxy 32e7011201fc5fceab21338da7c0a2dfead3b185
:   Resolves the following CVEs: [CVE-2026-11824](https://nvd.nist.gov/vuln/detail/cve-2026-11824), [CVE-2026-11979](https://nvd.nist.gov/vuln/detail/cve-2026-11979), [CVE-2026-8286](https://nvd.nist.gov/vuln/detail/cve-2026-8286), and [CVE-2026-11822](https://nvd.nist.gov/vuln/detail/cve-2026-11822).


## 25 August 2026, Worker node fix pack 4.20.34_1560_openshift
{: #cl-boms-42034_1560_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.34_1560_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-687.39.1.el9_8
:   Resolves the following CVEs: [RHSA-2026:54510](https://access.redhat.com/errata/RHSA-2026:54510), [CVE-2026-10723](https://nvd.nist.gov/vuln/detail/cve-2026-10723), [CVE-2026-11331](https://nvd.nist.gov/vuln/detail/cve-2026-11331), [CVE-2026-11622](https://nvd.nist.gov/vuln/detail/cve-2026-11622), [CVE-2026-11721](https://nvd.nist.gov/vuln/detail/cve-2026-11721), [CVE-2026-13204](https://nvd.nist.gov/vuln/detail/cve-2026-13204), [CVE-2026-13321](https://nvd.nist.gov/vuln/detail/cve-2026-13321), [RHSA-2026:55439](https://access.redhat.com/errata/RHSA-2026:55439), [CVE-2026-1965](https://nvd.nist.gov/vuln/detail/cve-2026-1965), [CVE-2026-3783](https://nvd.nist.gov/vuln/detail/cve-2026-3783), [CVE-2026-8286](https://nvd.nist.gov/vuln/detail/cve-2026-8286), [CVE-2026-9547](https://nvd.nist.gov/vuln/detail/cve-2026-9547), [RHSA-2026:54571](https://access.redhat.com/errata/RHSA-2026:54571), [CVE-2026-15816](https://nvd.nist.gov/vuln/detail/cve-2026-15816), [RHSA-2026:55772](https://access.redhat.com/errata/RHSA-2026:55772), [CVE-2026-55203](https://nvd.nist.gov/vuln/detail/cve-2026-55203), [CVE-2026-55204](https://nvd.nist.gov/vuln/detail/cve-2026-55204), [RHSA-2026:53844](https://access.redhat.com/errata/RHSA-2026:53844), [CVE-2026-44943](https://nvd.nist.gov/vuln/detail/cve-2026-44943), [CVE-2026-44944](https://nvd.nist.gov/vuln/detail/cve-2026-44944), [RHSA-2026:53847](https://access.redhat.com/errata/RHSA-2026:53847), [CVE-2026-55995](https://nvd.nist.gov/vuln/detail/cve-2026-55995), [RHSA-2026:53329](https://access.redhat.com/errata/RHSA-2026:53329), [CVE-2025-54518](https://nvd.nist.gov/vuln/detail/cve-2025-54518), [CVE-2026-31530](https://nvd.nist.gov/vuln/detail/cve-2026-31530), [CVE-2026-64368](https://nvd.nist.gov/vuln/detail/cve-2026-64368), [CVE-2026-64531](https://nvd.nist.gov/vuln/detail/cve-2026-64531), [RHSA-2026:54443](https://access.redhat.com/errata/RHSA-2026:54443), [CVE-2026-53202](https://nvd.nist.gov/vuln/detail/cve-2026-53202), [CVE-2026-53264](https://nvd.nist.gov/vuln/detail/cve-2026-53264), [RHSA-2026:54268](https://access.redhat.com/errata/RHSA-2026:54268), [CVE-2026-11940](https://nvd.nist.gov/vuln/detail/cve-2026-11940), [RHSA-2026:55440](https://access.redhat.com/errata/RHSA-2026:55440), [CVE-2026-15588](https://nvd.nist.gov/vuln/detail/cve-2026-15588), [CVE-2026-58010](https://nvd.nist.gov/vuln/detail/cve-2026-58010), [CVE-2026-58011](https://nvd.nist.gov/vuln/detail/cve-2026-58011), [CVE-2026-58012](https://nvd.nist.gov/vuln/detail/cve-2026-58012), [CVE-2026-58013](https://nvd.nist.gov/vuln/detail/cve-2026-58013), [CVE-2026-58014](https://nvd.nist.gov/vuln/detail/cve-2026-58014), [CVE-2026-58015](https://nvd.nist.gov/vuln/detail/cve-2026-58015), [RHSA-2026:57610](https://access.redhat.com/errata/RHSA-2026:57610), [CVE-2026-72693](https://nvd.nist.gov/vuln/detail/cve-2026-72693), [RHSA-2026:51035](https://access.redhat.com/errata/RHSA-2026:51035), [CVE-2026-23415](https://nvd.nist.gov/vuln/detail/cve-2026-23415), [CVE-2026-43450](https://nvd.nist.gov/vuln/detail/cve-2026-43450), [RHSA-2026:52674](https://access.redhat.com/errata/RHSA-2026:52674), [CVE-2026-14164](https://nvd.nist.gov/vuln/detail/cve-2026-14164), [RHSA-2026:54662](https://access.redhat.com/errata/RHSA-2026:54662), [CVE-2026-58055](https://nvd.nist.gov/vuln/detail/cve-2026-58055), [RHSA-2026:54484](https://access.redhat.com/errata/RHSA-2026:54484), and [CVE-2026-45409](https://nvd.nist.gov/vuln/detail/cve-2026-45409).


RHEL 9 (Satellite) 5.14.0-687.39.1.el9_8
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-687.39.1.el9_8
:   Resolves the following CVEs: [RHSA-2026:54510](https://access.redhat.com/errata/RHSA-2026:54510), [CVE-2026-10723](https://nvd.nist.gov/vuln/detail/cve-2026-10723), [CVE-2026-11331](https://nvd.nist.gov/vuln/detail/cve-2026-11331), [CVE-2026-11622](https://nvd.nist.gov/vuln/detail/cve-2026-11622), [CVE-2026-11721](https://nvd.nist.gov/vuln/detail/cve-2026-11721), [CVE-2026-13204](https://nvd.nist.gov/vuln/detail/cve-2026-13204), [CVE-2026-13321](https://nvd.nist.gov/vuln/detail/cve-2026-13321), [RHSA-2026:55439](https://access.redhat.com/errata/RHSA-2026:55439), [CVE-2026-1965](https://nvd.nist.gov/vuln/detail/cve-2026-1965), [CVE-2026-3783](https://nvd.nist.gov/vuln/detail/cve-2026-3783), [CVE-2026-8286](https://nvd.nist.gov/vuln/detail/cve-2026-8286), [CVE-2026-9547](https://nvd.nist.gov/vuln/detail/cve-2026-9547), [RHSA-2026:54571](https://access.redhat.com/errata/RHSA-2026:54571), [CVE-2026-15816](https://nvd.nist.gov/vuln/detail/cve-2026-15816), [RHSA-2026:55772](https://access.redhat.com/errata/RHSA-2026:55772), [CVE-2026-55203](https://nvd.nist.gov/vuln/detail/cve-2026-55203), [CVE-2026-55204](https://nvd.nist.gov/vuln/detail/cve-2026-55204), [RHSA-2026:53844](https://access.redhat.com/errata/RHSA-2026:53844), [CVE-2026-44943](https://nvd.nist.gov/vuln/detail/cve-2026-44943), [CVE-2026-44944](https://nvd.nist.gov/vuln/detail/cve-2026-44944), [RHSA-2026:53847](https://access.redhat.com/errata/RHSA-2026:53847), [CVE-2026-55995](https://nvd.nist.gov/vuln/detail/cve-2026-55995), [RHSA-2026:53329](https://access.redhat.com/errata/RHSA-2026:53329), [CVE-2025-54518](https://nvd.nist.gov/vuln/detail/cve-2025-54518), [CVE-2026-31530](https://nvd.nist.gov/vuln/detail/cve-2026-31530), [CVE-2026-64368](https://nvd.nist.gov/vuln/detail/cve-2026-64368), [CVE-2026-64531](https://nvd.nist.gov/vuln/detail/cve-2026-64531), [RHSA-2026:54443](https://access.redhat.com/errata/RHSA-2026:54443), [CVE-2026-53202](https://nvd.nist.gov/vuln/detail/cve-2026-53202), [CVE-2026-53264](https://nvd.nist.gov/vuln/detail/cve-2026-53264), [RHSA-2026:54268](https://access.redhat.com/errata/RHSA-2026:54268), [CVE-2026-11940](https://nvd.nist.gov/vuln/detail/cve-2026-11940), [RHSA-2026:55440](https://access.redhat.com/errata/RHSA-2026:55440), [CVE-2026-15588](https://nvd.nist.gov/vuln/detail/cve-2026-15588), [CVE-2026-58010](https://nvd.nist.gov/vuln/detail/cve-2026-58010), [CVE-2026-58011](https://nvd.nist.gov/vuln/detail/cve-2026-58011), [CVE-2026-58012](https://nvd.nist.gov/vuln/detail/cve-2026-58012), [CVE-2026-58013](https://nvd.nist.gov/vuln/detail/cve-2026-58013), [CVE-2026-58014](https://nvd.nist.gov/vuln/detail/cve-2026-58014), [CVE-2026-58015](https://nvd.nist.gov/vuln/detail/cve-2026-58015), [RHSA-2026:57610](https://access.redhat.com/errata/RHSA-2026:57610), [CVE-2026-72693](https://nvd.nist.gov/vuln/detail/cve-2026-72693), [RHSA-2026:51035](https://access.redhat.com/errata/RHSA-2026:51035), [CVE-2026-23415](https://nvd.nist.gov/vuln/detail/cve-2026-23415), [CVE-2026-43450](https://nvd.nist.gov/vuln/detail/cve-2026-43450), [RHSA-2026:52674](https://access.redhat.com/errata/RHSA-2026:52674), [CVE-2026-14164](https://nvd.nist.gov/vuln/detail/cve-2026-14164), [RHSA-2026:54662](https://access.redhat.com/errata/RHSA-2026:54662), [CVE-2026-58055](https://nvd.nist.gov/vuln/detail/cve-2026-58055), [RHSA-2026:54484](https://access.redhat.com/errata/RHSA-2026:54484), and [CVE-2026-45409](https://nvd.nist.gov/vuln/detail/cve-2026-45409).


Red Hat OpenShift 4.20.34
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-34_release-notes){: external}.


Red Hat CoreOS 4.20.34
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-34_release-notes){: external}.


HAProxy a70e8a8452c4d476687ad749df47b6f27a61851a
:   Resolves the following CVEs: [CVE-2026-54411](https://nvd.nist.gov/vuln/detail/cve-2026-54411), [CVE-2026-54371](https://nvd.nist.gov/vuln/detail/cve-2026-54371), [CVE-2026-55204](https://nvd.nist.gov/vuln/detail/cve-2026-55204), and [CVE-2026-58055](https://nvd.nist.gov/vuln/detail/cve-2026-58055).


## 12 August 2026, Worker node fix pack 4.20.32_1559_openshift
{: #cl-boms-42032_1559_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.32_1559_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-687.34.1.el9_8
:   Resolves the following CVEs: [RHSA-2026:44385](https://access.redhat.com/errata/RHSA-2026:44385), [CVE-2024-46738](https://nvd.nist.gov/vuln/detail/cve-2024-46738), [CVE-2024-50076](https://nvd.nist.gov/vuln/detail/cve-2024-50076), [CVE-2025-39982](https://nvd.nist.gov/vuln/detail/cve-2025-39982), [CVE-2026-31488](https://nvd.nist.gov/vuln/detail/cve-2026-31488), [CVE-2026-31613](https://nvd.nist.gov/vuln/detail/cve-2026-31613), [CVE-2026-31684](https://nvd.nist.gov/vuln/detail/cve-2026-31684), [CVE-2026-46116](https://nvd.nist.gov/vuln/detail/cve-2026-46116), [CVE-2026-46209](https://nvd.nist.gov/vuln/detail/cve-2026-46209), [RHSA-2026:49031](https://access.redhat.com/errata/RHSA-2026:49031), [CVE-2025-10263](https://nvd.nist.gov/vuln/detail/cve-2025-10263), [CVE-2025-40026](https://nvd.nist.gov/vuln/detail/cve-2025-40026), [CVE-2026-52923](https://nvd.nist.gov/vuln/detail/cve-2026-52923), [RHSA-2026:49839](https://access.redhat.com/errata/RHSA-2026:49839), [CVE-2026-14474](https://nvd.nist.gov/vuln/detail/cve-2026-14474), [CVE-2026-14476](https://nvd.nist.gov/vuln/detail/cve-2026-14476), [RHSA-2026:48811](https://access.redhat.com/errata/RHSA-2026:48811), [CVE-2026-48864](https://nvd.nist.gov/vuln/detail/cve-2026-48864), [RHSA-2026:49910](https://access.redhat.com/errata/RHSA-2026:49910), and [CVE-2026-29111](https://nvd.nist.gov/vuln/detail/cve-2026-29111).


RHEL 9 (Satellite) 5.14.0-687.34.1.el9_8
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-687.34.1.el9_8
:   Resolves the following CVEs: [RHSA-2026:44385](https://access.redhat.com/errata/RHSA-2026:44385), [CVE-2024-46738](https://nvd.nist.gov/vuln/detail/cve-2024-46738), [CVE-2024-50076](https://nvd.nist.gov/vuln/detail/cve-2024-50076), [CVE-2025-39982](https://nvd.nist.gov/vuln/detail/cve-2025-39982), [CVE-2026-31488](https://nvd.nist.gov/vuln/detail/cve-2026-31488), [CVE-2026-31613](https://nvd.nist.gov/vuln/detail/cve-2026-31613), [CVE-2026-31684](https://nvd.nist.gov/vuln/detail/cve-2026-31684), [CVE-2026-46116](https://nvd.nist.gov/vuln/detail/cve-2026-46116), [CVE-2026-46209](https://nvd.nist.gov/vuln/detail/cve-2026-46209), [RHSA-2026:49031](https://access.redhat.com/errata/RHSA-2026:49031), [CVE-2025-10263](https://nvd.nist.gov/vuln/detail/cve-2025-10263), [CVE-2025-40026](https://nvd.nist.gov/vuln/detail/cve-2025-40026), [CVE-2026-52923](https://nvd.nist.gov/vuln/detail/cve-2026-52923), [RHSA-2026:49839](https://access.redhat.com/errata/RHSA-2026:49839), [CVE-2026-14474](https://nvd.nist.gov/vuln/detail/cve-2026-14474), [CVE-2026-14476](https://nvd.nist.gov/vuln/detail/cve-2026-14476), [RHSA-2026:48811](https://access.redhat.com/errata/RHSA-2026:48811), [CVE-2026-48864](https://nvd.nist.gov/vuln/detail/cve-2026-48864), [RHSA-2026:49910](https://access.redhat.com/errata/RHSA-2026:49910), and [CVE-2026-29111](https://nvd.nist.gov/vuln/detail/cve-2026-29111).


Red Hat OpenShift 4.20.32
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-32_release-notes){: external}.


Red Hat CoreOS 4.20.32
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-32_release-notes){: external}.


HAProxy bd7e64ef86b90455535107263466d1825f3e7f9f
:   Resolves the following CVEs: [CVE-2026-56391](https://nvd.nist.gov/vuln/detail/cve-2026-56391), and [CVE-2026-56392](https://nvd.nist.gov/vuln/detail/cve-2026-56392).


## 05 August 2026, Master fix pack 4.20.32_1558_openshift
{: #cl-boms_master-42032_1558_openshift_M}

The following list shows the components that are in the master fix pack 4.20.32_1558_openshift. Master patch updates are applied automatically.
{: shortdesc}

etcd v3.5.32
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.32){: external}.


IBM Cloud Block Storage driver and plug-in v2.5.27
:   New version contains updates and security fixes.


IBM Cloud Controller Manager v1.33.13-6
:   New version contains updates and security fixes.


IBM Cloud File Storage for Classic plug-in and monitor v456
:   New version contains updates and security fixes.


Key Management Service provider 2.10.28
:   New version contains updates and security fixes.


Red Hat OpenShift on IBM Cloud 4.20.32
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes#ocp-4-20-32_release-notes){: external}.Resolves the following CVEs: [CVE-2026-16242](https://nvd.nist.gov/vuln/detail/cve-2026-16242).


## 28 July 2026, Worker node fix pack 4.20.30_1557_openshift
{: #cl-boms-42030_1557_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.30_1557_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.128.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:38902](https://access.redhat.com/errata/RHSA-2026:38902), [CVE-2025-68183](https://nvd.nist.gov/vuln/detail/cve-2025-68183), [CVE-2026-31408](https://nvd.nist.gov/vuln/detail/cve-2026-31408), [CVE-2026-43074](https://nvd.nist.gov/vuln/detail/cve-2026-43074), [CVE-2026-43279](https://nvd.nist.gov/vuln/detail/cve-2026-43279), [CVE-2026-45984](https://nvd.nist.gov/vuln/detail/cve-2026-45984), [CVE-2026-46135](https://nvd.nist.gov/vuln/detail/cve-2026-46135), [CVE-2026-46152](https://nvd.nist.gov/vuln/detail/cve-2026-46152), [CVE-2026-46189](https://nvd.nist.gov/vuln/detail/cve-2026-46189), [CVE-2026-46242](https://nvd.nist.gov/vuln/detail/cve-2026-46242), [CVE-2026-46316](https://nvd.nist.gov/vuln/detail/cve-2026-46316), [CVE-2026-53359](https://nvd.nist.gov/vuln/detail/cve-2026-53359), [RHSA-2026:44385](https://access.redhat.com/errata/RHSA-2026:44385), [CVE-2024-46738](https://nvd.nist.gov/vuln/detail/cve-2024-46738), [CVE-2024-50076](https://nvd.nist.gov/vuln/detail/cve-2024-50076), [CVE-2025-39982](https://nvd.nist.gov/vuln/detail/cve-2025-39982), [CVE-2026-31488](https://nvd.nist.gov/vuln/detail/cve-2026-31488), [CVE-2026-31613](https://nvd.nist.gov/vuln/detail/cve-2026-31613), [CVE-2026-31684](https://nvd.nist.gov/vuln/detail/cve-2026-31684), [CVE-2026-46116](https://nvd.nist.gov/vuln/detail/cve-2026-46116), [CVE-2026-46209](https://nvd.nist.gov/vuln/detail/cve-2026-46209), [RHSA-2026:40425](https://access.redhat.com/errata/RHSA-2026:40425), [CVE-2026-43499](https://nvd.nist.gov/vuln/detail/cve-2026-43499), [CVE-2026-53166](https://nvd.nist.gov/vuln/detail/cve-2026-53166), and [CVE-2026-64600](https://nvd.nist.gov/vuln/detail/cve-2026-64600).


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-570.128.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:38902](https://access.redhat.com/errata/RHSA-2026:38902), [CVE-2025-68183](https://nvd.nist.gov/vuln/detail/cve-2025-68183), [CVE-2026-31408](https://nvd.nist.gov/vuln/detail/cve-2026-31408), [CVE-2026-43074](https://nvd.nist.gov/vuln/detail/cve-2026-43074), [CVE-2026-43279](https://nvd.nist.gov/vuln/detail/cve-2026-43279), [CVE-2026-45984](https://nvd.nist.gov/vuln/detail/cve-2026-45984), [CVE-2026-46135](https://nvd.nist.gov/vuln/detail/cve-2026-46135), [CVE-2026-46152](https://nvd.nist.gov/vuln/detail/cve-2026-46152), [CVE-2026-46189](https://nvd.nist.gov/vuln/detail/cve-2026-46189), [CVE-2026-46242](https://nvd.nist.gov/vuln/detail/cve-2026-46242), [CVE-2026-46316](https://nvd.nist.gov/vuln/detail/cve-2026-46316), [CVE-2026-53359](https://nvd.nist.gov/vuln/detail/cve-2026-53359), [RHSA-2026:44385](https://access.redhat.com/errata/RHSA-2026:44385), [CVE-2024-46738](https://nvd.nist.gov/vuln/detail/cve-2024-46738), [CVE-2024-50076](https://nvd.nist.gov/vuln/detail/cve-2024-50076), [CVE-2025-39982](https://nvd.nist.gov/vuln/detail/cve-2025-39982), [CVE-2026-31488](https://nvd.nist.gov/vuln/detail/cve-2026-31488), [CVE-2026-31613](https://nvd.nist.gov/vuln/detail/cve-2026-31613), [CVE-2026-31684](https://nvd.nist.gov/vuln/detail/cve-2026-31684), [CVE-2026-46116](https://nvd.nist.gov/vuln/detail/cve-2026-46116), [CVE-2026-46209](https://nvd.nist.gov/vuln/detail/cve-2026-46209), [RHSA-2026:40425](https://access.redhat.com/errata/RHSA-2026:40425), [CVE-2026-43499](https://nvd.nist.gov/vuln/detail/cve-2026-43499), [CVE-2026-53166](https://nvd.nist.gov/vuln/detail/cve-2026-53166), and [CVE-2026-64600](https://nvd.nist.gov/vuln/detail/cve-2026-64600).


Red Hat OpenShift 4.20.30
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-30_release-notes){: external}.


Red Hat CoreOS 4.20.30
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-30_release-notes){: external}.


HAProxy 346c7130717ef7cc25d1dfbca7d57ca32396b692
:   Resolves the following CVEs: [CVE-2026-6238](https://nvd.nist.gov/vuln/detail/cve-2026-6238), [CVE-2026-5928](https://nvd.nist.gov/vuln/detail/cve-2026-5928), [CVE-2026-48864](https://nvd.nist.gov/vuln/detail/cve-2026-48864), [CVE-2026-54370](https://nvd.nist.gov/vuln/detail/cve-2026-54370), [CVE-2026-28390](https://nvd.nist.gov/vuln/detail/cve-2026-28390), [CVE-2026-5435](https://nvd.nist.gov/vuln/detail/cve-2026-5435), [CVE-2025-13151](https://nvd.nist.gov/vuln/detail/cve-2025-13151), [CVE-2026-54369](https://nvd.nist.gov/vuln/detail/cve-2026-54369), [CVE-2026-58016](https://nvd.nist.gov/vuln/detail/cve-2026-58016), and [CVE-2025-6170](https://nvd.nist.gov/vuln/detail/cve-2025-6170).


## 28 July 2026, Master fix pack 4.20.25_1556_openshift
{: #cl-boms_master-42025_1556_openshift_M}

The following list shows the components that are in the master fix pack 4.20.25_1556_openshift. Master patch updates are applied automatically.
{: shortdesc}

Cluster health image v1.6.17
:   New version contains updates and security fixes.


etcd v3.5.30
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.30){: external}.


IBM Cloud Block Storage driver and plug-in v2.5.26
:   New version contains updates and security fixes.


IBM Cloud Controller Manager v1.33.13-4
:   New version contains updates and security fixes.


IBM Cloud File Storage for Classic plug-in and monitor v455
:   New version contains updates and security fixes.


IBM Cloud RBAC Operator 92ba7dd
:   New version contains updates and security fixes.


Key Management Service provider 2.10.27
:   New version contains updates and security fixes.


Portieris admission controller v0.14.2
:   See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.14.2){: external}


Red Hat OpenShift on IBM Cloud 4.20.25
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes#ocp-4-20-25_release-notes){: external}.


## 13 July 2026, Worker node fix pack 4.20.28_1555_openshift
{: #cl-boms-42028_1555_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.28_1555_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.125.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:30004](https://access.redhat.com/errata/RHSA-2026:30004), [CVE-2026-33845](https://nvd.nist.gov/vuln/detail/cve-2026-33845), [CVE-2026-33846](https://nvd.nist.gov/vuln/detail/cve-2026-33846), [CVE-2026-3833](https://nvd.nist.gov/vuln/detail/cve-2026-3833), [CVE-2026-42009](https://nvd.nist.gov/vuln/detail/cve-2026-42009), [CVE-2026-42010](https://nvd.nist.gov/vuln/detail/cve-2026-42010), [CVE-2026-42011](https://nvd.nist.gov/vuln/detail/cve-2026-42011), [CVE-2026-42012](https://nvd.nist.gov/vuln/detail/cve-2026-42012), [CVE-2026-42013](https://nvd.nist.gov/vuln/detail/cve-2026-42013), [CVE-2026-42014](https://nvd.nist.gov/vuln/detail/cve-2026-42014), [CVE-2026-42015](https://nvd.nist.gov/vuln/detail/cve-2026-42015), [CVE-2026-5260](https://nvd.nist.gov/vuln/detail/cve-2026-5260), [CVE-2026-5419](https://nvd.nist.gov/vuln/detail/cve-2026-5419), [RHSA-2026:34094](https://access.redhat.com/errata/RHSA-2026:34094), [CVE-2025-21648](https://nvd.nist.gov/vuln/detail/cve-2025-21648), [CVE-2025-21691](https://nvd.nist.gov/vuln/detail/cve-2025-21691), [CVE-2026-23191](https://nvd.nist.gov/vuln/detail/cve-2026-23191), [CVE-2026-31669](https://nvd.nist.gov/vuln/detail/cve-2026-31669), [CVE-2026-43027](https://nvd.nist.gov/vuln/detail/cve-2026-43027), [CVE-2026-43125](https://nvd.nist.gov/vuln/detail/cve-2026-43125), [CVE-2026-43128](https://nvd.nist.gov/vuln/detail/cve-2026-43128), [CVE-2026-43198](https://nvd.nist.gov/vuln/detail/cve-2026-43198), [CVE-2026-43329](https://nvd.nist.gov/vuln/detail/cve-2026-43329), [CVE-2026-43414](https://nvd.nist.gov/vuln/detail/cve-2026-43414), [CVE-2026-43501](https://nvd.nist.gov/vuln/detail/cve-2026-43501), [CVE-2026-45852](https://nvd.nist.gov/vuln/detail/cve-2026-45852), [CVE-2026-46090](https://nvd.nist.gov/vuln/detail/cve-2026-46090), [CVE-2026-46173](https://nvd.nist.gov/vuln/detail/cve-2026-46173), [CVE-2026-46176](https://nvd.nist.gov/vuln/detail/cve-2026-46176), [CVE-2026-46181](https://nvd.nist.gov/vuln/detail/cve-2026-46181), [CVE-2026-46227](https://nvd.nist.gov/vuln/detail/cve-2026-46227), [CVE-2026-46244](https://nvd.nist.gov/vuln/detail/cve-2026-46244), [RHSA-2026:28147](https://access.redhat.com/errata/RHSA-2026:28147), [CVE-2026-28847](https://nvd.nist.gov/vuln/detail/cve-2026-28847), [CVE-2026-28883](https://nvd.nist.gov/vuln/detail/cve-2026-28883), [CVE-2026-28901](https://nvd.nist.gov/vuln/detail/cve-2026-28901), [CVE-2026-28902](https://nvd.nist.gov/vuln/detail/cve-2026-28902), [CVE-2026-28903](https://nvd.nist.gov/vuln/detail/cve-2026-28903), [CVE-2026-28904](https://nvd.nist.gov/vuln/detail/cve-2026-28904), [CVE-2026-28905](https://nvd.nist.gov/vuln/detail/cve-2026-28905), [CVE-2026-28907](https://nvd.nist.gov/vuln/detail/cve-2026-28907), [CVE-2026-28942](https://nvd.nist.gov/vuln/detail/cve-2026-28942), [CVE-2026-28946](https://nvd.nist.gov/vuln/detail/cve-2026-28946), [CVE-2026-28947](https://nvd.nist.gov/vuln/detail/cve-2026-28947), [CVE-2026-28953](https://nvd.nist.gov/vuln/detail/cve-2026-28953), [CVE-2026-28955](https://nvd.nist.gov/vuln/detail/cve-2026-28955), [CVE-2026-28958](https://nvd.nist.gov/vuln/detail/cve-2026-28958), [CVE-2026-43658](https://nvd.nist.gov/vuln/detail/cve-2026-43658), [CVE-2026-43660](https://nvd.nist.gov/vuln/detail/cve-2026-43660), [RHSA-2026:33634](https://access.redhat.com/errata/RHSA-2026:33634), [CVE-2024-34459](https://nvd.nist.gov/vuln/detail/cve-2024-34459), [RHSA-2026:33230](https://access.redhat.com/errata/RHSA-2026:33230), [CVE-2026-5450](https://nvd.nist.gov/vuln/detail/cve-2026-5450), [RHSA-2026:28832](https://access.redhat.com/errata/RHSA-2026:28832), and [CVE-2026-31790](https://nvd.nist.gov/vuln/detail/cve-2026-31790).


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-570.125.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:30004](https://access.redhat.com/errata/RHSA-2026:30004), [CVE-2026-33845](https://nvd.nist.gov/vuln/detail/cve-2026-33845), [CVE-2026-33846](https://nvd.nist.gov/vuln/detail/cve-2026-33846), [CVE-2026-3833](https://nvd.nist.gov/vuln/detail/cve-2026-3833), [CVE-2026-42009](https://nvd.nist.gov/vuln/detail/cve-2026-42009), [CVE-2026-42010](https://nvd.nist.gov/vuln/detail/cve-2026-42010), [CVE-2026-42011](https://nvd.nist.gov/vuln/detail/cve-2026-42011), [CVE-2026-42012](https://nvd.nist.gov/vuln/detail/cve-2026-42012), [CVE-2026-42013](https://nvd.nist.gov/vuln/detail/cve-2026-42013), [CVE-2026-42014](https://nvd.nist.gov/vuln/detail/cve-2026-42014), [CVE-2026-42015](https://nvd.nist.gov/vuln/detail/cve-2026-42015), [CVE-2026-5260](https://nvd.nist.gov/vuln/detail/cve-2026-5260), [CVE-2026-5419](https://nvd.nist.gov/vuln/detail/cve-2026-5419), [RHSA-2026:34094](https://access.redhat.com/errata/RHSA-2026:34094), [CVE-2025-21648](https://nvd.nist.gov/vuln/detail/cve-2025-21648), [CVE-2025-21691](https://nvd.nist.gov/vuln/detail/cve-2025-21691), [CVE-2026-23191](https://nvd.nist.gov/vuln/detail/cve-2026-23191), [CVE-2026-31669](https://nvd.nist.gov/vuln/detail/cve-2026-31669), [CVE-2026-43027](https://nvd.nist.gov/vuln/detail/cve-2026-43027), [CVE-2026-43125](https://nvd.nist.gov/vuln/detail/cve-2026-43125), [CVE-2026-43128](https://nvd.nist.gov/vuln/detail/cve-2026-43128), [CVE-2026-43198](https://nvd.nist.gov/vuln/detail/cve-2026-43198), [CVE-2026-43329](https://nvd.nist.gov/vuln/detail/cve-2026-43329), [CVE-2026-43414](https://nvd.nist.gov/vuln/detail/cve-2026-43414), [CVE-2026-43501](https://nvd.nist.gov/vuln/detail/cve-2026-43501), [CVE-2026-45852](https://nvd.nist.gov/vuln/detail/cve-2026-45852), [CVE-2026-46090](https://nvd.nist.gov/vuln/detail/cve-2026-46090), [CVE-2026-46173](https://nvd.nist.gov/vuln/detail/cve-2026-46173), [CVE-2026-46176](https://nvd.nist.gov/vuln/detail/cve-2026-46176), [CVE-2026-46181](https://nvd.nist.gov/vuln/detail/cve-2026-46181), [CVE-2026-46227](https://nvd.nist.gov/vuln/detail/cve-2026-46227), [CVE-2026-46244](https://nvd.nist.gov/vuln/detail/cve-2026-46244), [RHSA-2026:28147](https://access.redhat.com/errata/RHSA-2026:28147), [CVE-2026-28847](https://nvd.nist.gov/vuln/detail/cve-2026-28847), [CVE-2026-28883](https://nvd.nist.gov/vuln/detail/cve-2026-28883), [CVE-2026-28901](https://nvd.nist.gov/vuln/detail/cve-2026-28901), [CVE-2026-28902](https://nvd.nist.gov/vuln/detail/cve-2026-28902), [CVE-2026-28903](https://nvd.nist.gov/vuln/detail/cve-2026-28903), [CVE-2026-28904](https://nvd.nist.gov/vuln/detail/cve-2026-28904), [CVE-2026-28905](https://nvd.nist.gov/vuln/detail/cve-2026-28905), [CVE-2026-28907](https://nvd.nist.gov/vuln/detail/cve-2026-28907), [CVE-2026-28942](https://nvd.nist.gov/vuln/detail/cve-2026-28942), [CVE-2026-28946](https://nvd.nist.gov/vuln/detail/cve-2026-28946), [CVE-2026-28947](https://nvd.nist.gov/vuln/detail/cve-2026-28947), [CVE-2026-28953](https://nvd.nist.gov/vuln/detail/cve-2026-28953), [CVE-2026-28955](https://nvd.nist.gov/vuln/detail/cve-2026-28955), [CVE-2026-28958](https://nvd.nist.gov/vuln/detail/cve-2026-28958), [CVE-2026-43658](https://nvd.nist.gov/vuln/detail/cve-2026-43658), [CVE-2026-43660](https://nvd.nist.gov/vuln/detail/cve-2026-43660), [RHSA-2026:33634](https://access.redhat.com/errata/RHSA-2026:33634), [CVE-2024-34459](https://nvd.nist.gov/vuln/detail/cve-2024-34459), [RHSA-2026:33230](https://access.redhat.com/errata/RHSA-2026:33230), [CVE-2026-5450](https://nvd.nist.gov/vuln/detail/cve-2026-5450), [RHSA-2026:28832](https://access.redhat.com/errata/RHSA-2026:28832), and [CVE-2026-31790](https://nvd.nist.gov/vuln/detail/cve-2026-31790).


Red Hat OpenShift 4.20.28
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-28_release-notes){: external}.


Red Hat CoreOS 4.20.28
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-28_release-notes){: external}.


HAProxy 27f76d0c7626993cde6e1ff90fa42253718cc5fa
:   Resolves the following CVEs: [CVE-2026-5450](https://nvd.nist.gov/vuln/detail/cve-2026-5450).


## 01 July 2026, Worker node fix pack 4.20.26_1553_openshift
{: #cl-boms-42026_1553_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.26_1553_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.123.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:24500](https://access.redhat.com/errata/RHSA-2026:24500), [CVE-2026-1519](https://nvd.nist.gov/vuln/detail/cve-2026-1519), [RHSA-2026:23224](https://access.redhat.com/errata/RHSA-2026:23224), [CVE-2025-38653](https://nvd.nist.gov/vuln/detail/cve-2025-38653), [CVE-2025-39766](https://nvd.nist.gov/vuln/detail/cve-2025-39766), [CVE-2025-68366](https://nvd.nist.gov/vuln/detail/cve-2025-68366), [CVE-2026-23210](https://nvd.nist.gov/vuln/detail/cve-2026-23210), [CVE-2026-23270](https://nvd.nist.gov/vuln/detail/cve-2026-23270), [CVE-2026-23392](https://nvd.nist.gov/vuln/detail/cve-2026-23392), [CVE-2026-31419](https://nvd.nist.gov/vuln/detail/cve-2026-31419), [CVE-2026-31607](https://nvd.nist.gov/vuln/detail/cve-2026-31607), [CVE-2026-31685](https://nvd.nist.gov/vuln/detail/cve-2026-31685), [CVE-2026-31709](https://nvd.nist.gov/vuln/detail/cve-2026-31709), [CVE-2026-43037](https://nvd.nist.gov/vuln/detail/cve-2026-43037), [CVE-2026-43038](https://nvd.nist.gov/vuln/detail/cve-2026-43038), [CVE-2026-43163](https://nvd.nist.gov/vuln/detail/cve-2026-43163), [RHSA-2026:25218](https://access.redhat.com/errata/RHSA-2026:25218), [CVE-2025-40135](https://nvd.nist.gov/vuln/detail/cve-2025-40135), [CVE-2025-40158](https://nvd.nist.gov/vuln/detail/cve-2025-40158), [CVE-2025-40170](https://nvd.nist.gov/vuln/detail/cve-2025-40170), [CVE-2025-68724](https://nvd.nist.gov/vuln/detail/cve-2025-68724), [CVE-2025-71089](https://nvd.nist.gov/vuln/detail/cve-2025-71089), [CVE-2025-71116](https://nvd.nist.gov/vuln/detail/cve-2025-71116), [CVE-2026-22984](https://nvd.nist.gov/vuln/detail/cve-2026-22984), [CVE-2026-22990](https://nvd.nist.gov/vuln/detail/cve-2026-22990), [CVE-2026-23216](https://nvd.nist.gov/vuln/detail/cve-2026-23216), [CVE-2026-23455](https://nvd.nist.gov/vuln/detail/cve-2026-23455), [CVE-2026-31508](https://nvd.nist.gov/vuln/detail/cve-2026-31508), [CVE-2026-43110](https://nvd.nist.gov/vuln/detail/cve-2026-43110), [CVE-2026-43190](https://nvd.nist.gov/vuln/detail/cve-2026-43190), [RHSA-2026:27708](https://access.redhat.com/errata/RHSA-2026:27708), [CVE-2025-40064](https://nvd.nist.gov/vuln/detail/cve-2025-40064), [CVE-2025-40168](https://nvd.nist.gov/vuln/detail/cve-2025-40168), [CVE-2026-23136](https://nvd.nist.gov/vuln/detail/cve-2026-23136), [CVE-2026-43116](https://nvd.nist.gov/vuln/detail/cve-2026-43116), [CVE-2026-43158](https://nvd.nist.gov/vuln/detail/cve-2026-43158), [CVE-2026-43303](https://nvd.nist.gov/vuln/detail/cve-2026-43303), [CVE-2026-45898](https://nvd.nist.gov/vuln/detail/cve-2026-45898), [CVE-2026-46125](https://nvd.nist.gov/vuln/detail/cve-2026-46125), [CVE-2026-46166](https://nvd.nist.gov/vuln/detail/cve-2026-46166), [CVE-2026-46243](https://nvd.nist.gov/vuln/detail/cve-2026-46243), [CVE-2026-46323](https://nvd.nist.gov/vuln/detail/cve-2026-46323), [CVE-2026-46331](https://nvd.nist.gov/vuln/detail/cve-2026-46331), [RHSA-2026:24683](https://access.redhat.com/errata/RHSA-2026:24683), [CVE-2026-40356](https://nvd.nist.gov/vuln/detail/cve-2026-40356), [RHSA-2026:24337](https://access.redhat.com/errata/RHSA-2026:24337), [CVE-2026-32280](https://nvd.nist.gov/vuln/detail/cve-2026-32280), [CVE-2026-32281](https://nvd.nist.gov/vuln/detail/cve-2026-32281), [CVE-2026-32282](https://nvd.nist.gov/vuln/detail/cve-2026-32282), [CVE-2026-32283](https://nvd.nist.gov/vuln/detail/cve-2026-32283), [RHSA-2026:25979](https://access.redhat.com/errata/RHSA-2026:25979), [CVE-2026-1933](https://nvd.nist.gov/vuln/detail/cve-2026-1933), [CVE-2026-2340](https://nvd.nist.gov/vuln/detail/cve-2026-2340), [CVE-2026-3012](https://nvd.nist.gov/vuln/detail/cve-2026-3012), [CVE-2026-4408](https://nvd.nist.gov/vuln/detail/cve-2026-4408), [CVE-2026-4480](https://nvd.nist.gov/vuln/detail/cve-2026-4480), [RHSA-2026:28050](https://access.redhat.com/errata/RHSA-2026:28050), [CVE-2026-34982](https://nvd.nist.gov/vuln/detail/cve-2026-34982), [CVE-2026-35177](https://nvd.nist.gov/vuln/detail/cve-2026-35177), [CVE-2026-41411](https://nvd.nist.gov/vuln/detail/cve-2026-41411), and [CVE-2026-46483](https://nvd.nist.gov/vuln/detail/cve-2026-46483).


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-570.123.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:24500](https://access.redhat.com/errata/RHSA-2026:24500), [CVE-2026-1519](https://nvd.nist.gov/vuln/detail/cve-2026-1519), [RHSA-2026:23224](https://access.redhat.com/errata/RHSA-2026:23224), [CVE-2025-38653](https://nvd.nist.gov/vuln/detail/cve-2025-38653), [CVE-2025-39766](https://nvd.nist.gov/vuln/detail/cve-2025-39766), [CVE-2025-68366](https://nvd.nist.gov/vuln/detail/cve-2025-68366), [CVE-2026-23210](https://nvd.nist.gov/vuln/detail/cve-2026-23210), [CVE-2026-23270](https://nvd.nist.gov/vuln/detail/cve-2026-23270), [CVE-2026-23392](https://nvd.nist.gov/vuln/detail/cve-2026-23392), [CVE-2026-31419](https://nvd.nist.gov/vuln/detail/cve-2026-31419), [CVE-2026-31607](https://nvd.nist.gov/vuln/detail/cve-2026-31607), [CVE-2026-31685](https://nvd.nist.gov/vuln/detail/cve-2026-31685), [CVE-2026-31709](https://nvd.nist.gov/vuln/detail/cve-2026-31709), [CVE-2026-43037](https://nvd.nist.gov/vuln/detail/cve-2026-43037), [CVE-2026-43038](https://nvd.nist.gov/vuln/detail/cve-2026-43038), [CVE-2026-43163](https://nvd.nist.gov/vuln/detail/cve-2026-43163), [RHSA-2026:25218](https://access.redhat.com/errata/RHSA-2026:25218), [CVE-2025-40135](https://nvd.nist.gov/vuln/detail/cve-2025-40135), [CVE-2025-40158](https://nvd.nist.gov/vuln/detail/cve-2025-40158), [CVE-2025-40170](https://nvd.nist.gov/vuln/detail/cve-2025-40170), [CVE-2025-68724](https://nvd.nist.gov/vuln/detail/cve-2025-68724), [CVE-2025-71089](https://nvd.nist.gov/vuln/detail/cve-2025-71089), [CVE-2025-71116](https://nvd.nist.gov/vuln/detail/cve-2025-71116), [CVE-2026-22984](https://nvd.nist.gov/vuln/detail/cve-2026-22984), [CVE-2026-22990](https://nvd.nist.gov/vuln/detail/cve-2026-22990), [CVE-2026-23216](https://nvd.nist.gov/vuln/detail/cve-2026-23216), [CVE-2026-23455](https://nvd.nist.gov/vuln/detail/cve-2026-23455), [CVE-2026-31508](https://nvd.nist.gov/vuln/detail/cve-2026-31508), [CVE-2026-43110](https://nvd.nist.gov/vuln/detail/cve-2026-43110), [CVE-2026-43190](https://nvd.nist.gov/vuln/detail/cve-2026-43190), [RHSA-2026:27708](https://access.redhat.com/errata/RHSA-2026:27708), [CVE-2025-40064](https://nvd.nist.gov/vuln/detail/cve-2025-40064), [CVE-2025-40168](https://nvd.nist.gov/vuln/detail/cve-2025-40168), [CVE-2026-23136](https://nvd.nist.gov/vuln/detail/cve-2026-23136), [CVE-2026-43116](https://nvd.nist.gov/vuln/detail/cve-2026-43116), [CVE-2026-43158](https://nvd.nist.gov/vuln/detail/cve-2026-43158), [CVE-2026-43303](https://nvd.nist.gov/vuln/detail/cve-2026-43303), [CVE-2026-45898](https://nvd.nist.gov/vuln/detail/cve-2026-45898), [CVE-2026-46125](https://nvd.nist.gov/vuln/detail/cve-2026-46125), [CVE-2026-46166](https://nvd.nist.gov/vuln/detail/cve-2026-46166), [CVE-2026-46243](https://nvd.nist.gov/vuln/detail/cve-2026-46243), [CVE-2026-46323](https://nvd.nist.gov/vuln/detail/cve-2026-46323), [CVE-2026-46331](https://nvd.nist.gov/vuln/detail/cve-2026-46331), [RHSA-2026:24683](https://access.redhat.com/errata/RHSA-2026:24683), [CVE-2026-40356](https://nvd.nist.gov/vuln/detail/cve-2026-40356), [RHSA-2026:24337](https://access.redhat.com/errata/RHSA-2026:24337), [CVE-2026-32280](https://nvd.nist.gov/vuln/detail/cve-2026-32280), [CVE-2026-32281](https://nvd.nist.gov/vuln/detail/cve-2026-32281), [CVE-2026-32282](https://nvd.nist.gov/vuln/detail/cve-2026-32282), [CVE-2026-32283](https://nvd.nist.gov/vuln/detail/cve-2026-32283), [RHSA-2026:25979](https://access.redhat.com/errata/RHSA-2026:25979), [CVE-2026-1933](https://nvd.nist.gov/vuln/detail/cve-2026-1933), [CVE-2026-2340](https://nvd.nist.gov/vuln/detail/cve-2026-2340), [CVE-2026-3012](https://nvd.nist.gov/vuln/detail/cve-2026-3012), [CVE-2026-4408](https://nvd.nist.gov/vuln/detail/cve-2026-4408), [CVE-2026-4480](https://nvd.nist.gov/vuln/detail/cve-2026-4480), [RHSA-2026:28050](https://access.redhat.com/errata/RHSA-2026:28050), [CVE-2026-34982](https://nvd.nist.gov/vuln/detail/cve-2026-34982), [CVE-2026-35177](https://nvd.nist.gov/vuln/detail/cve-2026-35177), [CVE-2026-41411](https://nvd.nist.gov/vuln/detail/cve-2026-41411), and [CVE-2026-46483](https://nvd.nist.gov/vuln/detail/cve-2026-46483).


Red Hat OpenShift 4.20.26
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-26_release-notes){: external}.


Red Hat CoreOS 4.20.26
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-26_release-notes){: external}.


HAProxy 119de539a7da3c92449b38e1531722802988e50c
:   Resolves the following CVEs: [CVE-2026-45447](https://nvd.nist.gov/vuln/detail/cve-2026-45447), [CVE-2024-4741](https://nvd.nist.gov/vuln/detail/cve-2024-4741), and [CVE-2024-34459](https://nvd.nist.gov/vuln/detail/cve-2024-34459).


## 26 June 2026, Master fix pack 4.20.23_1551_openshift
{: #cl-boms_master-42023_1551_openshift_M}

The following list shows the components that are in the master fix pack 4.20.23_1551_openshift. Master patch updates are applied automatically.
{: shortdesc}

Cluster health image v1.6.16
:   New version contains updates and security fixes.


etcd v3.5.30
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.30){: external}.


IBM Cloud Block Storage driver and plug-in v2.5.26
:   New version contains updates and security fixes.


IBM Cloud Controller Manager v1.33.12-2
:   New version contains updates and security fixes.


IBM Cloud File Storage for Classic plug-in and monitor v455
:   New version contains updates and security fixes.


Key Management Service provider 2.10.25
:   New version contains updates and security fixes.


Portieris admission controller v0.14.0
:   See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.14.0){: external}


Red Hat OpenShift on IBM Cloud 4.20.23
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes#ocp-4-20-23_release-notes){: external}.


## 15 June 2026, Worker node fix pack 4.20.24_1552_openshift
{: #cl-boms-42024_1552_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.24_1552_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.116.1.el9_6
:   Resolves the following CVEs: [CVE-2026-5119](https://nvd.nist.gov/vuln/detail/cve-2026-5119).


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-570.116.1.el9_6
:   


Red Hat OpenShift 4.20.24
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-23_release-notes){: external}.


Red Hat CoreOS 4.20.24
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-23_release-notes){: external}.


HAProxy d4656f400ca14059e1b5b8ef8078b4903290791a
:   Resolves the following CVEs: [CVE-2026-45186](https://nvd.nist.gov/vuln/detail/cve-2026-45186).


## 03 June 2026, Worker node fix pack 4.20.23_1550_openshift
{: #cl-boms-42023_1550_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.23_1550_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.116.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:21392](https://access.redhat.com/errata/RHSA-2026:21392), [CVE-2026-4802](https://nvd.nist.gov/vuln/detail/cve-2026-4802), [RHSA-2026:18042](https://access.redhat.com/errata/RHSA-2026:18042), [CVE-2026-39979](https://nvd.nist.gov/vuln/detail/cve-2026-39979), [CVE-2026-40164](https://nvd.nist.gov/vuln/detail/cve-2026-40164), [RHSA-2026:16312](https://access.redhat.com/errata/RHSA-2026:16312), [CVE-2026-43284](https://nvd.nist.gov/vuln/detail/cve-2026-43284), [RHSA-2026:20129](https://access.redhat.com/errata/RHSA-2026:20129), [CVE-2026-46300](https://nvd.nist.gov/vuln/detail/cve-2026-46300), [CVE-2026-46333](https://nvd.nist.gov/vuln/detail/cve-2026-46333), [RHSA-2026:19458](https://access.redhat.com/errata/RHSA-2026:19458), [CVE-2026-4878](https://nvd.nist.gov/vuln/detail/cve-2026-4878), [RHSA-2026:18031](https://access.redhat.com/errata/RHSA-2026:18031), [CVE-2026-41651](https://nvd.nist.gov/vuln/detail/cve-2026-41651), [RHSA-2026:19576](https://access.redhat.com/errata/RHSA-2026:19576), [CVE-2026-4786](https://nvd.nist.gov/vuln/detail/cve-2026-4786), [CVE-2026-6100](https://nvd.nist.gov/vuln/detail/cve-2026-6100), [RHSA-2026:20603](https://access.redhat.com/errata/RHSA-2026:20603), [CVE-2024-12086](https://nvd.nist.gov/vuln/detail/cve-2024-12086), [CVE-2025-10158](https://nvd.nist.gov/vuln/detail/cve-2025-10158), [CVE-2026-41035](https://nvd.nist.gov/vuln/detail/cve-2026-41035), [RHSA-2026:19457](https://access.redhat.com/errata/RHSA-2026:19457), [CVE-2025-14087](https://nvd.nist.gov/vuln/detail/cve-2025-14087), [CVE-2025-14512](https://nvd.nist.gov/vuln/detail/cve-2025-14512), [RHSA-2026:20548](https://access.redhat.com/errata/RHSA-2026:20548), and [CVE-2026-33416](https://nvd.nist.gov/vuln/detail/cve-2026-33416).


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


RHEL 9 (Classic) 5.14.0-570.116.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:18042](https://access.redhat.com/errata/RHSA-2026:18042), [CVE-2026-39979](https://nvd.nist.gov/vuln/detail/cve-2026-39979), [CVE-2026-40164](https://nvd.nist.gov/vuln/detail/cve-2026-40164), [RHSA-2026:16312](https://access.redhat.com/errata/RHSA-2026:16312), [CVE-2026-43284](https://nvd.nist.gov/vuln/detail/cve-2026-43284), [RHSA-2026:20129](https://access.redhat.com/errata/RHSA-2026:20129), [CVE-2026-46300](https://nvd.nist.gov/vuln/detail/cve-2026-46300), [CVE-2026-46333](https://nvd.nist.gov/vuln/detail/cve-2026-46333), [RHSA-2026:19458](https://access.redhat.com/errata/RHSA-2026:19458), [CVE-2026-4878](https://nvd.nist.gov/vuln/detail/cve-2026-4878), [RHSA-2026:19576](https://access.redhat.com/errata/RHSA-2026:19576), [CVE-2026-4786](https://nvd.nist.gov/vuln/detail/cve-2026-4786), [CVE-2026-6100](https://nvd.nist.gov/vuln/detail/cve-2026-6100), [RHSA-2026:19457](https://access.redhat.com/errata/RHSA-2026:19457), [CVE-2025-14087](https://nvd.nist.gov/vuln/detail/cve-2025-14087), [CVE-2025-14512](https://nvd.nist.gov/vuln/detail/cve-2025-14512), [RHSA-2026:20548](https://access.redhat.com/errata/RHSA-2026:20548), and [CVE-2026-33416](https://nvd.nist.gov/vuln/detail/cve-2026-33416).


Red Hat OpenShift 4.20.23
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-23_release-notes){: external}.


Red Hat CoreOS 4.20.23
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-23_release-notes){: external}.


HAProxy 0e0730588ba21878845cdb0bee615a371a489a02
:   Resolves the following CVEs: [CVE-2026-4046](https://nvd.nist.gov/vuln/detail/cve-2026-4046), [CVE-2026-33846](https://nvd.nist.gov/vuln/detail/cve-2026-33846), [CVE-2026-42010](https://nvd.nist.gov/vuln/detail/cve-2026-42010), [CVE-2026-5260](https://nvd.nist.gov/vuln/detail/cve-2026-5260), [CVE-2026-42014](https://nvd.nist.gov/vuln/detail/cve-2026-42014), [CVE-2026-3833](https://nvd.nist.gov/vuln/detail/cve-2026-3833), [CVE-2026-42015](https://nvd.nist.gov/vuln/detail/cve-2026-42015), [CVE-2026-33845](https://nvd.nist.gov/vuln/detail/cve-2026-33845), [CVE-2026-42011](https://nvd.nist.gov/vuln/detail/cve-2026-42011), [CVE-2026-42009](https://nvd.nist.gov/vuln/detail/cve-2026-42009), [CVE-2026-42013](https://nvd.nist.gov/vuln/detail/cve-2026-42013), and [CVE-2026-42012](https://nvd.nist.gov/vuln/detail/cve-2026-42012).


## 22 May 2026, Master fix pack 4.20.21_1548_openshift
{: #cl-boms_master-42021_1548_openshift_M}

The following list shows the components that are in the master fix pack 4.20.21_1548_openshift. Master patch updates are applied automatically.
{: shortdesc}

Calico v3.30.7
:   See the [Calico release notes](https://docs.tigera.io/calico/3.30/release-notes/#calico-open-source-3307-bug-fix-release){: external}.


etcd v3.5.29
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.29){: external}.


IBM Cloud Controller Manager v1.33.11-3
:   New version contains updates and security fixes.


Key Management Service provider 2.10.24
:   New version contains updates and security fixes.


Portieris admission controller v0.13.38
:   See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.13.38){: external}


Red Hat OpenShift on IBM Cloud 4.20.21
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes#ocp-4-20-21_release-notes){: external}.


Tigera Operator v1.38.13
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.38.13){: external}.


## 20 May 2026, Worker node fix pack 4.20.22_1549_openshift
{: #cl-boms-42022_1549_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.22_1549_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) [5.14.0-570.112.1.el9_6](/docs/openshift?topic=openshift-openshift-relnotes#openshift-may2126)
:   Resolves the following CVEs: [RHSA-2025:22392](https://access.redhat.com/errata/RHSA-2025:22392), [CVE-2025-38724](https://nvd.nist.gov/vuln/detail/cve-2025-38724), [CVE-2025-39864](https://nvd.nist.gov/vuln/detail/cve-2025-39864), [CVE-2025-39881](https://nvd.nist.gov/vuln/detail/cve-2025-39881), [CVE-2025-39883](https://nvd.nist.gov/vuln/detail/cve-2025-39883), [CVE-2025-39918](https://nvd.nist.gov/vuln/detail/cve-2025-39918), [CVE-2025-39955](https://nvd.nist.gov/vuln/detail/cve-2025-39955), [CVE-2025-40186](https://nvd.nist.gov/vuln/detail/cve-2025-40186), [RHSA-2026:0457](https://access.redhat.com/errata/RHSA-2026:0457), [CVE-2025-23142](https://nvd.nist.gov/vuln/detail/cve-2025-23142), [CVE-2025-39806](https://nvd.nist.gov/vuln/detail/cve-2025-39806), [CVE-2025-39981](https://nvd.nist.gov/vuln/detail/cve-2025-39981), [CVE-2025-39983](https://nvd.nist.gov/vuln/detail/cve-2025-39983), [CVE-2025-40176](https://nvd.nist.gov/vuln/detail/cve-2025-40176), [CVE-2025-68287](https://nvd.nist.gov/vuln/detail/cve-2025-68287), [RHSA-2026:0804](https://access.redhat.com/errata/RHSA-2026:0804), [CVE-2025-21795](https://nvd.nist.gov/vuln/detail/cve-2025-21795), [CVE-2025-37849](https://nvd.nist.gov/vuln/detail/cve-2025-37849), [CVE-2025-37891](https://nvd.nist.gov/vuln/detail/cve-2025-37891), [CVE-2025-39697](https://nvd.nist.gov/vuln/detail/cve-2025-39697), [CVE-2025-40154](https://nvd.nist.gov/vuln/detail/cve-2025-40154), [CVE-2025-68285](https://nvd.nist.gov/vuln/detail/cve-2025-68285), [RHSA-2026:14339](https://access.redhat.com/errata/RHSA-2026:14339), [CVE-2024-53216](https://nvd.nist.gov/vuln/detail/cve-2024-53216), [CVE-2025-68741](https://nvd.nist.gov/vuln/detail/cve-2025-68741), [CVE-2026-23243](https://nvd.nist.gov/vuln/detail/cve-2026-23243), [CVE-2026-23401](https://nvd.nist.gov/vuln/detail/cve-2026-23401), [CVE-2026-31431](https://nvd.nist.gov/vuln/detail/cve-2026-31431), [CVE-2026-31532](https://nvd.nist.gov/vuln/detail/cve-2026-31532), [CVE-2026-43077](https://nvd.nist.gov/vuln/detail/cve-2026-43077), [RHSA-2026:16312](https://access.redhat.com/errata/RHSA-2026:16312), [CVE-2026-43284](https://nvd.nist.gov/vuln/detail/cve-2026-43284), [RHSA-2026:1703](https://access.redhat.com/errata/RHSA-2026:1703), [CVE-2025-21863](https://nvd.nist.gov/vuln/detail/cve-2025-21863), [CVE-2025-40248](https://nvd.nist.gov/vuln/detail/cve-2025-40248), [CVE-2025-68301](https://nvd.nist.gov/vuln/detail/cve-2025-68301), [RHSA-2026:16059](https://access.redhat.com/errata/RHSA-2026:16059), [CVE-2026-35385](https://nvd.nist.gov/vuln/detail/cve-2026-35385), [CVE-2026-35386](https://nvd.nist.gov/vuln/detail/cve-2026-35386), [CVE-2026-35387](https://nvd.nist.gov/vuln/detail/cve-2026-35387), [CVE-2026-35388](https://nvd.nist.gov/vuln/detail/cve-2026-35388), [CVE-2026-35414](https://nvd.nist.gov/vuln/detail/cve-2026-35414), [RHSA-2026:13889](https://access.redhat.com/errata/RHSA-2026:13889), [CVE-2026-35535](https://nvd.nist.gov/vuln/detail/cve-2026-35535), [RHSA-2025:21563](https://access.redhat.com/errata/RHSA-2025:21563), [CVE-2024-56690](https://nvd.nist.gov/vuln/detail/cve-2024-56690), [RHSA-2025:21933](https://access.redhat.com/errata/RHSA-2025:21933), [CVE-2025-39898](https://nvd.nist.gov/vuln/detail/cve-2025-39898), [CVE-2025-39971](https://nvd.nist.gov/vuln/detail/cve-2025-39971), [CVE-2025-39973](https://nvd.nist.gov/vuln/detail/cve-2025-39973), [CVE-2025-40047](https://nvd.nist.gov/vuln/detail/cve-2025-40047), [RHSA-2025:22802](https://access.redhat.com/errata/RHSA-2025:22802), [CVE-2025-39966](https://nvd.nist.gov/vuln/detail/cve-2025-39966), [RHSA-2025:23789](https://access.redhat.com/errata/RHSA-2025:23789), [CVE-2025-39843](https://nvd.nist.gov/vuln/detail/cve-2025-39843), [CVE-2025-39925](https://nvd.nist.gov/vuln/detail/cve-2025-39925), [RHSA-2026:11313](https://access.redhat.com/errata/RHSA-2026:11313), [CVE-2026-23097](https://nvd.nist.gov/vuln/detail/cve-2026-23097), [CVE-2026-31402](https://nvd.nist.gov/vuln/detail/cve-2026-31402), [RHSA-2026:1194](https://access.redhat.com/errata/RHSA-2026:1194), [CVE-2023-53034](https://nvd.nist.gov/vuln/detail/cve-2023-53034), [CVE-2025-37761](https://nvd.nist.gov/vuln/detail/cve-2025-37761), [CVE-2025-37789](https://nvd.nist.gov/vuln/detail/cve-2025-37789), [CVE-2025-37819](https://nvd.nist.gov/vuln/detail/cve-2025-37819), [CVE-2025-37869](https://nvd.nist.gov/vuln/detail/cve-2025-37869), [CVE-2025-38289](https://nvd.nist.gov/vuln/detail/cve-2025-38289), [CVE-2025-40141](https://nvd.nist.gov/vuln/detail/cve-2025-40141), [CVE-2025-40251](https://nvd.nist.gov/vuln/detail/cve-2025-40251), [CVE-2025-40258](https://nvd.nist.gov/vuln/detail/cve-2025-40258), [CVE-2025-40277](https://nvd.nist.gov/vuln/detail/cve-2025-40277), [CVE-2025-40318](https://nvd.nist.gov/vuln/detail/cve-2025-40318), [RHSA-2026:2352](https://access.redhat.com/errata/RHSA-2026:2352), [CVE-2024-54456](https://nvd.nist.gov/vuln/detail/cve-2024-54456), [CVE-2025-21647](https://nvd.nist.gov/vuln/detail/cve-2025-21647), [CVE-2025-21786](https://nvd.nist.gov/vuln/detail/cve-2025-21786), [CVE-2025-21791](https://nvd.nist.gov/vuln/detail/cve-2025-21791), [CVE-2025-38022](https://nvd.nist.gov/vuln/detail/cve-2025-38022), [CVE-2025-38051](https://nvd.nist.gov/vuln/detail/cve-2025-38051), [CVE-2025-38568](https://nvd.nist.gov/vuln/detail/cve-2025-38568), [CVE-2025-40294](https://nvd.nist.gov/vuln/detail/cve-2025-40294), [CVE-2025-40322](https://nvd.nist.gov/vuln/detail/cve-2025-40322), [CVE-2025-68349](https://nvd.nist.gov/vuln/detail/cve-2025-68349), [RHSA-2026:2759](https://access.redhat.com/errata/RHSA-2026:2759), [CVE-2025-37882](https://nvd.nist.gov/vuln/detail/cve-2025-37882), [CVE-2025-38349](https://nvd.nist.gov/vuln/detail/cve-2025-38349), [CVE-2025-38730](https://nvd.nist.gov/vuln/detail/cve-2025-38730), [CVE-2025-39760](https://nvd.nist.gov/vuln/detail/cve-2025-39760), [CVE-2025-39933](https://nvd.nist.gov/vuln/detail/cve-2025-39933), [CVE-2025-40269](https://nvd.nist.gov/vuln/detail/cve-2025-40269), [CVE-2025-40271](https://nvd.nist.gov/vuln/detail/cve-2025-40271), [CVE-2025-40304](https://nvd.nist.gov/vuln/detail/cve-2025-40304), [RHSA-2026:3088](https://access.redhat.com/errata/RHSA-2026:3088), [CVE-2025-37861](https://nvd.nist.gov/vuln/detail/cve-2025-37861), [CVE-2025-38106](https://nvd.nist.gov/vuln/detail/cve-2025-38106), [CVE-2025-38415](https://nvd.nist.gov/vuln/detail/cve-2025-38415), [RHSA-2026:3520](https://access.redhat.com/errata/RHSA-2026:3520), [CVE-2025-38154](https://nvd.nist.gov/vuln/detail/cve-2025-38154), [RHSA-2026:4011](https://access.redhat.com/errata/RHSA-2026:4011), [CVE-2024-47727](https://nvd.nist.gov/vuln/detail/cve-2024-47727), [CVE-2024-56603](https://nvd.nist.gov/vuln/detail/cve-2024-56603), [CVE-2025-22056](https://nvd.nist.gov/vuln/detail/cve-2025-22056), [CVE-2025-38024](https://nvd.nist.gov/vuln/detail/cve-2025-38024), [CVE-2025-38129](https://nvd.nist.gov/vuln/detail/cve-2025-38129), [CVE-2025-38141](https://nvd.nist.gov/vuln/detail/cve-2025-38141), [CVE-2025-38703](https://nvd.nist.gov/vuln/detail/cve-2025-38703), [RHSA-2026:4745](https://access.redhat.com/errata/RHSA-2026:4745), [CVE-2024-53229](https://nvd.nist.gov/vuln/detail/cve-2024-53229), [CVE-2025-38206](https://nvd.nist.gov/vuln/detail/cve-2025-38206), [CVE-2025-40240](https://nvd.nist.gov/vuln/detail/cve-2025-40240), [CVE-2025-68811](https://nvd.nist.gov/vuln/detail/cve-2025-68811), [CVE-2025-71085](https://nvd.nist.gov/vuln/detail/cve-2025-71085), [RHSA-2026:5197](https://access.redhat.com/errata/RHSA-2026:5197), [CVE-2025-38248](https://nvd.nist.gov/vuln/detail/cve-2025-38248), [CVE-2026-23001](https://nvd.nist.gov/vuln/detail/cve-2026-23001), [RHSA-2026:6164](https://access.redhat.com/errata/RHSA-2026:6164), [CVE-2024-56645](https://nvd.nist.gov/vuln/detail/cve-2024-56645), [CVE-2025-40096](https://nvd.nist.gov/vuln/detail/cve-2025-40096), [CVE-2025-68800](https://nvd.nist.gov/vuln/detail/cve-2025-68800), [CVE-2026-23209](https://nvd.nist.gov/vuln/detail/cve-2026-23209), [RHSA-2026:6940](https://access.redhat.com/errata/RHSA-2026:6940), [CVE-2025-38180](https://nvd.nist.gov/vuln/detail/cve-2025-38180), [CVE-2026-23231](https://nvd.nist.gov/vuln/detail/cve-2026-23231), [RHSA-2026:9112](https://access.redhat.com/errata/RHSA-2026:9112), [CVE-2026-23066](https://nvd.nist.gov/vuln/detail/cve-2026-23066), [CVE-2026-23111](https://nvd.nist.gov/vuln/detail/cve-2026-23111), [CVE-2026-23144](https://nvd.nist.gov/vuln/detail/cve-2026-23144), [CVE-2026-23171](https://nvd.nist.gov/vuln/detail/cve-2026-23171), [CVE-2026-23193](https://nvd.nist.gov/vuln/detail/cve-2026-23193), [CVE-2026-23204](https://nvd.nist.gov/vuln/detail/cve-2026-23204), [RHSA-2026:17524](https://access.redhat.com/errata/RHSA-2026:17524), and [CVE-2026-33636](https://nvd.nist.gov/vuln/detail/cve-2026-33636).


RHEL 9 (Classic) [5.14.0-570.112.1.el9_6](/docs/openshift?topic=openshift-openshift-relnotes#openshift-may2126)
:   Resolves the following CVEs: [RHSA-2026:2229](https://access.redhat.com/errata/RHSA-2026:2229), [CVE-2025-6176](https://nvd.nist.gov/vuln/detail/cve-2025-6176), [RHSA-2025:21773](https://access.redhat.com/errata/RHSA-2025:21773), [CVE-2025-59375](https://nvd.nist.gov/vuln/detail/cve-2025-59375), [RHSA-2026:1229](https://access.redhat.com/errata/RHSA-2026:1229), [CVE-2025-68973](https://nvd.nist.gov/vuln/detail/cve-2025-68973), [RHSA-2026:18042](https://access.redhat.com/errata/RHSA-2026:18042), [CVE-2026-39979](https://nvd.nist.gov/vuln/detail/cve-2026-39979), [CVE-2026-40164](https://nvd.nist.gov/vuln/detail/cve-2026-40164), [RHSA-2025:22392](https://access.redhat.com/errata/RHSA-2025:22392), [CVE-2025-38724](https://nvd.nist.gov/vuln/detail/cve-2025-38724), [CVE-2025-39864](https://nvd.nist.gov/vuln/detail/cve-2025-39864), [CVE-2025-39881](https://nvd.nist.gov/vuln/detail/cve-2025-39881), [CVE-2025-39883](https://nvd.nist.gov/vuln/detail/cve-2025-39883), [CVE-2025-39918](https://nvd.nist.gov/vuln/detail/cve-2025-39918), [CVE-2025-39955](https://nvd.nist.gov/vuln/detail/cve-2025-39955), [CVE-2025-40186](https://nvd.nist.gov/vuln/detail/cve-2025-40186), [RHSA-2026:0457](https://access.redhat.com/errata/RHSA-2026:0457), [CVE-2025-23142](https://nvd.nist.gov/vuln/detail/cve-2025-23142), [CVE-2025-39806](https://nvd.nist.gov/vuln/detail/cve-2025-39806), [CVE-2025-39981](https://nvd.nist.gov/vuln/detail/cve-2025-39981), [CVE-2025-39983](https://nvd.nist.gov/vuln/detail/cve-2025-39983), [CVE-2025-40176](https://nvd.nist.gov/vuln/detail/cve-2025-40176), [CVE-2025-68287](https://nvd.nist.gov/vuln/detail/cve-2025-68287), [RHSA-2026:0804](https://access.redhat.com/errata/RHSA-2026:0804), [CVE-2025-21795](https://nvd.nist.gov/vuln/detail/cve-2025-21795), [CVE-2025-37849](https://nvd.nist.gov/vuln/detail/cve-2025-37849), [CVE-2025-37891](https://nvd.nist.gov/vuln/detail/cve-2025-37891), [CVE-2025-39697](https://nvd.nist.gov/vuln/detail/cve-2025-39697), [CVE-2025-40154](https://nvd.nist.gov/vuln/detail/cve-2025-40154), [CVE-2025-68285](https://nvd.nist.gov/vuln/detail/cve-2025-68285), [RHSA-2026:14339](https://access.redhat.com/errata/RHSA-2026:14339), [CVE-2024-53216](https://nvd.nist.gov/vuln/detail/cve-2024-53216), [CVE-2025-68741](https://nvd.nist.gov/vuln/detail/cve-2025-68741), [CVE-2026-23243](https://nvd.nist.gov/vuln/detail/cve-2026-23243), [CVE-2026-23401](https://nvd.nist.gov/vuln/detail/cve-2026-23401), [CVE-2026-31431](https://nvd.nist.gov/vuln/detail/cve-2026-31431), [CVE-2026-31532](https://nvd.nist.gov/vuln/detail/cve-2026-31532), [CVE-2026-43077](https://nvd.nist.gov/vuln/detail/cve-2026-43077), [RHSA-2026:16312](https://access.redhat.com/errata/RHSA-2026:16312), [CVE-2026-43284](https://nvd.nist.gov/vuln/detail/cve-2026-43284), [RHSA-2026:1703](https://access.redhat.com/errata/RHSA-2026:1703), [CVE-2025-21863](https://nvd.nist.gov/vuln/detail/cve-2025-21863), [CVE-2025-40248](https://nvd.nist.gov/vuln/detail/cve-2025-40248), [CVE-2025-68301](https://nvd.nist.gov/vuln/detail/cve-2025-68301), [RHSA-2026:7105](https://access.redhat.com/errata/RHSA-2026:7105), [CVE-2026-4111](https://nvd.nist.gov/vuln/detail/cve-2026-4111), [RHSA-2026:8866](https://access.redhat.com/errata/RHSA-2026:8866), [CVE-2026-4424](https://nvd.nist.gov/vuln/detail/cve-2026-4424), [CVE-2026-5121](https://nvd.nist.gov/vuln/detail/cve-2026-5121), [RHSA-2026:19458](https://access.redhat.com/errata/RHSA-2026:19458), [CVE-2026-4878](https://nvd.nist.gov/vuln/detail/cve-2026-4878), [RHSA-2026:0210](https://access.redhat.com/errata/RHSA-2026:0210), [CVE-2025-64720](https://nvd.nist.gov/vuln/detail/cve-2025-64720), [CVE-2025-65018](https://nvd.nist.gov/vuln/detail/cve-2025-65018), [CVE-2025-66293](https://nvd.nist.gov/vuln/detail/cve-2025-66293), [RHSA-2026:3576](https://access.redhat.com/errata/RHSA-2026:3576), [CVE-2026-22695](https://nvd.nist.gov/vuln/detail/cve-2026-22695), [CVE-2026-22801](https://nvd.nist.gov/vuln/detail/cve-2026-22801), [CVE-2026-25646](https://nvd.nist.gov/vuln/detail/cve-2026-25646), [RHSA-2026:8548](https://access.redhat.com/errata/RHSA-2026:8548), [CVE-2026-27135](https://nvd.nist.gov/vuln/detail/cve-2026-27135), [RHSA-2026:16059](https://access.redhat.com/errata/RHSA-2026:16059), [CVE-2026-35385](https://nvd.nist.gov/vuln/detail/cve-2026-35385), [CVE-2026-35386](https://nvd.nist.gov/vuln/detail/cve-2026-35386), [CVE-2026-35387](https://nvd.nist.gov/vuln/detail/cve-2026-35387), [CVE-2026-35388](https://nvd.nist.gov/vuln/detail/cve-2026-35388), [CVE-2026-35414](https://nvd.nist.gov/vuln/detail/cve-2026-35414), [RHSA-2026:9415](https://access.redhat.com/errata/RHSA-2026:9415), [CVE-2026-3497](https://nvd.nist.gov/vuln/detail/cve-2026-3497), [RHSA-2026:1503](https://access.redhat.com/errata/RHSA-2026:1503), [CVE-2025-15467](https://nvd.nist.gov/vuln/detail/cve-2025-15467), [CVE-2025-69419](https://nvd.nist.gov/vuln/detail/cve-2025-69419), [RHSA-2026:1729](https://access.redhat.com/errata/RHSA-2026:1729), [CVE-2025-66418](https://nvd.nist.gov/vuln/detail/cve-2025-66418), [CVE-2025-66471](https://nvd.nist.gov/vuln/detail/cve-2025-66471), [CVE-2026-21441](https://nvd.nist.gov/vuln/detail/cve-2026-21441), [RHSA-2026:9354](https://access.redhat.com/errata/RHSA-2026:9354), [CVE-2026-4519](https://nvd.nist.gov/vuln/detail/cve-2026-4519), [RHSA-2025:21067](https://access.redhat.com/errata/RHSA-2025:21067), [CVE-2025-11561](https://nvd.nist.gov/vuln/detail/cve-2025-11561), [RHSA-2026:13889](https://access.redhat.com/errata/RHSA-2026:13889), [CVE-2026-35535](https://nvd.nist.gov/vuln/detail/cve-2026-35535), [RHSA-2026:6539](https://access.redhat.com/errata/RHSA-2026:6539), [CVE-2026-25749](https://nvd.nist.gov/vuln/detail/cve-2026-25749), [CVE-2026-28417](https://nvd.nist.gov/vuln/detail/cve-2026-28417), [CVE-2026-28421](https://nvd.nist.gov/vuln/detail/cve-2026-28421), [CVE-2026-33412](https://nvd.nist.gov/vuln/detail/cve-2026-33412), [RHSA-2025:23400](https://access.redhat.com/errata/RHSA-2025:23400), [CVE-2025-11083](https://nvd.nist.gov/vuln/detail/cve-2025-11083), [RHSA-2025:23043](https://access.redhat.com/errata/RHSA-2025:23043), [CVE-2025-9086](https://nvd.nist.gov/vuln/detail/cve-2025-9086), [RHSA-2026:1465](https://access.redhat.com/errata/RHSA-2026:1465), [CVE-2025-13601](https://nvd.nist.gov/vuln/detail/cve-2025-13601), [RHSA-2026:19457](https://access.redhat.com/errata/RHSA-2026:19457), [CVE-2025-14087](https://nvd.nist.gov/vuln/detail/cve-2025-14087), [CVE-2025-14512](https://nvd.nist.gov/vuln/detail/cve-2025-14512), [RHSA-2026:6630](https://access.redhat.com/errata/RHSA-2026:6630), [CVE-2025-14831](https://nvd.nist.gov/vuln/detail/cve-2025-14831), [RHSA-2026:4823](https://access.redhat.com/errata/RHSA-2026:4823), [CVE-2025-61662](https://nvd.nist.gov/vuln/detail/cve-2025-61662), [RHSA-2025:21563](https://access.redhat.com/errata/RHSA-2025:21563), [CVE-2024-56690](https://nvd.nist.gov/vuln/detail/cve-2024-56690), [RHSA-2025:21933](https://access.redhat.com/errata/RHSA-2025:21933), [CVE-2025-39898](https://nvd.nist.gov/vuln/detail/cve-2025-39898), [CVE-2025-39971](https://nvd.nist.gov/vuln/detail/cve-2025-39971), [CVE-2025-39973](https://nvd.nist.gov/vuln/detail/cve-2025-39973), [CVE-2025-40047](https://nvd.nist.gov/vuln/detail/cve-2025-40047), [RHSA-2025:22802](https://access.redhat.com/errata/RHSA-2025:22802), [CVE-2025-39966](https://nvd.nist.gov/vuln/detail/cve-2025-39966), [RHSA-2025:23789](https://access.redhat.com/errata/RHSA-2025:23789), [CVE-2025-39843](https://nvd.nist.gov/vuln/detail/cve-2025-39843), [CVE-2025-39925](https://nvd.nist.gov/vuln/detail/cve-2025-39925), [RHSA-2026:11313](https://access.redhat.com/errata/RHSA-2026:11313), [CVE-2026-23097](https://nvd.nist.gov/vuln/detail/cve-2026-23097), [CVE-2026-31402](https://nvd.nist.gov/vuln/detail/cve-2026-31402), [RHSA-2026:1194](https://access.redhat.com/errata/RHSA-2026:1194), [CVE-2023-53034](https://nvd.nist.gov/vuln/detail/cve-2023-53034), [CVE-2025-37761](https://nvd.nist.gov/vuln/detail/cve-2025-37761), [CVE-2025-37789](https://nvd.nist.gov/vuln/detail/cve-2025-37789), [CVE-2025-37819](https://nvd.nist.gov/vuln/detail/cve-2025-37819), [CVE-2025-37869](https://nvd.nist.gov/vuln/detail/cve-2025-37869), [CVE-2025-38289](https://nvd.nist.gov/vuln/detail/cve-2025-38289), [CVE-2025-40141](https://nvd.nist.gov/vuln/detail/cve-2025-40141), [CVE-2025-40251](https://nvd.nist.gov/vuln/detail/cve-2025-40251), [CVE-2025-40258](https://nvd.nist.gov/vuln/detail/cve-2025-40258), [CVE-2025-40277](https://nvd.nist.gov/vuln/detail/cve-2025-40277), [CVE-2025-40318](https://nvd.nist.gov/vuln/detail/cve-2025-40318), [RHSA-2026:2352](https://access.redhat.com/errata/RHSA-2026:2352), [CVE-2024-54456](https://nvd.nist.gov/vuln/detail/cve-2024-54456), [CVE-2025-21647](https://nvd.nist.gov/vuln/detail/cve-2025-21647), [CVE-2025-21786](https://nvd.nist.gov/vuln/detail/cve-2025-21786), [CVE-2025-21791](https://nvd.nist.gov/vuln/detail/cve-2025-21791), [CVE-2025-38022](https://nvd.nist.gov/vuln/detail/cve-2025-38022), [CVE-2025-38051](https://nvd.nist.gov/vuln/detail/cve-2025-38051), [CVE-2025-38568](https://nvd.nist.gov/vuln/detail/cve-2025-38568), [CVE-2025-40294](https://nvd.nist.gov/vuln/detail/cve-2025-40294), [CVE-2025-40322](https://nvd.nist.gov/vuln/detail/cve-2025-40322), [CVE-2025-68349](https://nvd.nist.gov/vuln/detail/cve-2025-68349), [RHSA-2026:2759](https://access.redhat.com/errata/RHSA-2026:2759), [CVE-2025-37882](https://nvd.nist.gov/vuln/detail/cve-2025-37882), [CVE-2025-38349](https://nvd.nist.gov/vuln/detail/cve-2025-38349), [CVE-2025-38730](https://nvd.nist.gov/vuln/detail/cve-2025-38730), [CVE-2025-39760](https://nvd.nist.gov/vuln/detail/cve-2025-39760), [CVE-2025-39933](https://nvd.nist.gov/vuln/detail/cve-2025-39933), [CVE-2025-40269](https://nvd.nist.gov/vuln/detail/cve-2025-40269), [CVE-2025-40271](https://nvd.nist.gov/vuln/detail/cve-2025-40271), [CVE-2025-40304](https://nvd.nist.gov/vuln/detail/cve-2025-40304), [RHSA-2026:3088](https://access.redhat.com/errata/RHSA-2026:3088), [CVE-2025-37861](https://nvd.nist.gov/vuln/detail/cve-2025-37861), [CVE-2025-38106](https://nvd.nist.gov/vuln/detail/cve-2025-38106), [CVE-2025-38415](https://nvd.nist.gov/vuln/detail/cve-2025-38415), [RHSA-2026:3520](https://access.redhat.com/errata/RHSA-2026:3520), [CVE-2025-38154](https://nvd.nist.gov/vuln/detail/cve-2025-38154), [RHSA-2026:4011](https://access.redhat.com/errata/RHSA-2026:4011), [CVE-2024-47727](https://nvd.nist.gov/vuln/detail/cve-2024-47727), [CVE-2024-56603](https://nvd.nist.gov/vuln/detail/cve-2024-56603), [CVE-2025-22056](https://nvd.nist.gov/vuln/detail/cve-2025-22056), [CVE-2025-38024](https://nvd.nist.gov/vuln/detail/cve-2025-38024), [CVE-2025-38129](https://nvd.nist.gov/vuln/detail/cve-2025-38129), [CVE-2025-38141](https://nvd.nist.gov/vuln/detail/cve-2025-38141), [CVE-2025-38703](https://nvd.nist.gov/vuln/detail/cve-2025-38703), [RHSA-2026:4745](https://access.redhat.com/errata/RHSA-2026:4745), [CVE-2024-53229](https://nvd.nist.gov/vuln/detail/cve-2024-53229), [CVE-2025-38206](https://nvd.nist.gov/vuln/detail/cve-2025-38206), [CVE-2025-40240](https://nvd.nist.gov/vuln/detail/cve-2025-40240), [CVE-2025-68811](https://nvd.nist.gov/vuln/detail/cve-2025-68811), [CVE-2025-71085](https://nvd.nist.gov/vuln/detail/cve-2025-71085), [RHSA-2026:5197](https://access.redhat.com/errata/RHSA-2026:5197), [CVE-2025-38248](https://nvd.nist.gov/vuln/detail/cve-2025-38248), [CVE-2026-23001](https://nvd.nist.gov/vuln/detail/cve-2026-23001), [RHSA-2026:6164](https://access.redhat.com/errata/RHSA-2026:6164), [CVE-2024-56645](https://nvd.nist.gov/vuln/detail/cve-2024-56645), [CVE-2025-40096](https://nvd.nist.gov/vuln/detail/cve-2025-40096), [CVE-2025-68800](https://nvd.nist.gov/vuln/detail/cve-2025-68800), [CVE-2026-23209](https://nvd.nist.gov/vuln/detail/cve-2026-23209), [RHSA-2026:6940](https://access.redhat.com/errata/RHSA-2026:6940), [CVE-2025-38180](https://nvd.nist.gov/vuln/detail/cve-2025-38180), [CVE-2026-23231](https://nvd.nist.gov/vuln/detail/cve-2026-23231), [RHSA-2026:9112](https://access.redhat.com/errata/RHSA-2026:9112), [CVE-2026-23066](https://nvd.nist.gov/vuln/detail/cve-2026-23066), [CVE-2026-23111](https://nvd.nist.gov/vuln/detail/cve-2026-23111), [CVE-2026-23144](https://nvd.nist.gov/vuln/detail/cve-2026-23144), [CVE-2026-23171](https://nvd.nist.gov/vuln/detail/cve-2026-23171), [CVE-2026-23193](https://nvd.nist.gov/vuln/detail/cve-2026-23193), [CVE-2026-23204](https://nvd.nist.gov/vuln/detail/cve-2026-23204), [RHSA-2026:17524](https://access.redhat.com/errata/RHSA-2026:17524), [CVE-2026-33636](https://nvd.nist.gov/vuln/detail/cve-2026-33636), [RHSA-2026:0428](https://access.redhat.com/errata/RHSA-2026:0428), [CVE-2025-5987](https://nvd.nist.gov/vuln/detail/cve-2025-5987), [RHSA-2025:22377](https://access.redhat.com/errata/RHSA-2025:22377), [CVE-2025-9714](https://nvd.nist.gov/vuln/detail/cve-2025-9714), [RHSA-2026:3941](https://access.redhat.com/errata/RHSA-2026:3941), [CVE-2025-12801](https://nvd.nist.gov/vuln/detail/cve-2025-12801), [RHSA-2026:0693](https://access.redhat.com/errata/RHSA-2026:0693), [CVE-2025-61984](https://nvd.nist.gov/vuln/detail/cve-2025-61984), [CVE-2025-61985](https://nvd.nist.gov/vuln/detail/cve-2025-61985), [RHSA-2025:21174](https://access.redhat.com/errata/RHSA-2025:21174), [CVE-2025-9230](https://nvd.nist.gov/vuln/detail/cve-2025-9230), [RHSA-2026:2275](https://access.redhat.com/errata/RHSA-2026:2275), [CVE-2025-12084](https://nvd.nist.gov/vuln/detail/cve-2025-12084), [RHSA-2026:5218](https://access.redhat.com/errata/RHSA-2026:5218), [CVE-2025-15366](https://nvd.nist.gov/vuln/detail/cve-2025-15366), [CVE-2025-15367](https://nvd.nist.gov/vuln/detail/cve-2025-15367), [CVE-2026-1299](https://nvd.nist.gov/vuln/detail/cve-2026-1299), [RHSA-2026:0435](https://access.redhat.com/errata/RHSA-2026:0435), and [CVE-2025-45582](https://nvd.nist.gov/vuln/detail/cve-2025-45582).


RHEL 9 (Satellite) 5.14.0-570.62.1.el9_6
:   Kernel updates.


Red Hat OpenShift 4.20.22
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-22_release-notes){: external}.


Red Hat CoreOS 4.20.22
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-22_release-notes){: external}.


HAProxy 6ba93946d8bd08ba581321189c719ab548cadf01
:   Resolves the following CVEs: [CVE-2025-9714](https://nvd.nist.gov/vuln/detail/cve-2025-9714), [CVE-2026-4424](https://nvd.nist.gov/vuln/detail/cve-2026-4424), [CVE-2026-40356](https://nvd.nist.gov/vuln/detail/cve-2026-40356), [CVE-2025-14512](https://nvd.nist.gov/vuln/detail/cve-2025-14512), [CVE-2026-4878](https://nvd.nist.gov/vuln/detail/cve-2026-4878), [CVE-2026-40355](https://nvd.nist.gov/vuln/detail/cve-2026-40355), [CVE-2026-5121](https://nvd.nist.gov/vuln/detail/cve-2026-5121), and [CVE-2025-14087](https://nvd.nist.gov/vuln/detail/cve-2025-14087).


## 04 May 2026, Worker node fix pack 4.20.19_1546_openshift
{: #cl-boms-42019_1546_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.19_1546_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:9415](https://access.redhat.com/errata/RHSA-2026:9415), [CVE-2026-3497](https://nvd.nist.gov/vuln/detail/cve-2026-3497), [RHSA-2026:11313](https://access.redhat.com/errata/RHSA-2026:11313), [CVE-2026-23097](https://nvd.nist.gov/vuln/detail/cve-2026-23097), [CVE-2026-31402](https://nvd.nist.gov/vuln/detail/cve-2026-31402), [RHSA-2026:11329](https://access.redhat.com/errata/RHSA-2026:11329), [CVE-2025-43213](https://nvd.nist.gov/vuln/detail/cve-2025-43213), [CVE-2025-43214](https://nvd.nist.gov/vuln/detail/cve-2025-43214), [CVE-2025-43457](https://nvd.nist.gov/vuln/detail/cve-2025-43457), [CVE-2025-43511](https://nvd.nist.gov/vuln/detail/cve-2025-43511), [CVE-2025-46299](https://nvd.nist.gov/vuln/detail/cve-2025-46299), [CVE-2026-20608](https://nvd.nist.gov/vuln/detail/cve-2026-20608), [CVE-2026-20635](https://nvd.nist.gov/vuln/detail/cve-2026-20635), [CVE-2026-20636](https://nvd.nist.gov/vuln/detail/cve-2026-20636), [CVE-2026-20643](https://nvd.nist.gov/vuln/detail/cve-2026-20643), [CVE-2026-20644](https://nvd.nist.gov/vuln/detail/cve-2026-20644), [CVE-2026-20652](https://nvd.nist.gov/vuln/detail/cve-2026-20652), [CVE-2026-20664](https://nvd.nist.gov/vuln/detail/cve-2026-20664), [CVE-2026-20665](https://nvd.nist.gov/vuln/detail/cve-2026-20665), [CVE-2026-20676](https://nvd.nist.gov/vuln/detail/cve-2026-20676), [CVE-2026-20691](https://nvd.nist.gov/vuln/detail/cve-2026-20691), [CVE-2026-28857](https://nvd.nist.gov/vuln/detail/cve-2026-28857), [CVE-2026-28859](https://nvd.nist.gov/vuln/detail/cve-2026-28859), [CVE-2026-28871](https://nvd.nist.gov/vuln/detail/cve-2026-28871), and mitigates [CVE-2026-31431](https://nvd.nist.gov/vuln/detail/cve-2026-31431).


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   Resolves the following CVEs: [RHSA-2026:9415](https://access.redhat.com/errata/RHSA-2026:9415), [CVE-2026-3497](https://nvd.nist.gov/vuln/detail/cve-2026-3497), [RHSA-2026:11313](https://access.redhat.com/errata/RHSA-2026:11313), [CVE-2026-23097](https://nvd.nist.gov/vuln/detail/cve-2026-23097), [CVE-2026-31402](https://nvd.nist.gov/vuln/detail/cve-2026-31402), [RHSA-2026:11329](https://access.redhat.com/errata/RHSA-2026:11329), [CVE-2025-43213](https://nvd.nist.gov/vuln/detail/cve-2025-43213), [CVE-2025-43214](https://nvd.nist.gov/vuln/detail/cve-2025-43214), [CVE-2025-43457](https://nvd.nist.gov/vuln/detail/cve-2025-43457), [CVE-2025-43511](https://nvd.nist.gov/vuln/detail/cve-2025-43511), [CVE-2025-46299](https://nvd.nist.gov/vuln/detail/cve-2025-46299), [CVE-2026-20608](https://nvd.nist.gov/vuln/detail/cve-2026-20608), [CVE-2026-20635](https://nvd.nist.gov/vuln/detail/cve-2026-20635), [CVE-2026-20636](https://nvd.nist.gov/vuln/detail/cve-2026-20636), [CVE-2026-20643](https://nvd.nist.gov/vuln/detail/cve-2026-20643), [CVE-2026-20644](https://nvd.nist.gov/vuln/detail/cve-2026-20644), [CVE-2026-20652](https://nvd.nist.gov/vuln/detail/cve-2026-20652), [CVE-2026-20664](https://nvd.nist.gov/vuln/detail/cve-2026-20664), [CVE-2026-20665](https://nvd.nist.gov/vuln/detail/cve-2026-20665), [CVE-2026-20676](https://nvd.nist.gov/vuln/detail/cve-2026-20676), [CVE-2026-20691](https://nvd.nist.gov/vuln/detail/cve-2026-20691), [CVE-2026-28857](https://nvd.nist.gov/vuln/detail/cve-2026-28857), [CVE-2026-28859](https://nvd.nist.gov/vuln/detail/cve-2026-28859), [CVE-2026-28871](https://nvd.nist.gov/vuln/detail/cve-2026-28871), and mitigates [CVE-2026-31431](https://nvd.nist.gov/vuln/detail/cve-2026-31431).


Red Hat OpenShift 4.20.19
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-19_release-notes){: external}.


Red Hat CoreOS 4.20.19
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-19_release-notes){: external}. Includes mitigation for [CVE-2026-31431](https://nvd.nist.gov/vuln/detail/cve-2026-31431){: external}.


HAProxy c7e825675cbd75e8433801c99f8aca3b207a5a46
:   Resolves the following CVEs: [CVE-2026-5121](https://nvd.nist.gov/vuln/detail/cve-2026-5121), [CVE-2025-9714](https://nvd.nist.gov/vuln/detail/cve-2025-9714), and [CVE-2026-4424](https://nvd.nist.gov/vuln/detail/cve-2026-4424).


## 27 April 2026, Master fix pack 4.20.18_1545_openshift
{: #cl-boms_master-42018_1545_openshift_M}

The following list shows the components that are in the master fix pack 4.20.18_1545_openshift. Master patch updates are applied automatically.
{: shortdesc}

Calico v3.30.7
:   See the [Calico release notes](https://docs.tigera.io/calico/3.30/release-notes/#calico-open-source-3307-bug-fix-release){: external}.


Cluster health image v1.6.15
:   New version contains updates and security fixes.


etcd v3.5.29
:   See the [etcd release notes](https://github.com/etcd-io/etcd/releases/v3.5.29){: external}.


IBM Cloud Block Storage driver and plug-in v2.5.25
:   New version contains updates and security fixes.


IBM Cloud Controller Manager v1.33.10-2
:   New version contains updates and security fixes.


IBM Cloud File Storage for Classic plug-in and monitor v454
:   New version contains updates and security fixes.


IBM Cloud RBAC Operator 6212368
:   New version contains updates and security fixes.


Key Management Service provider 2.10.23
:   New version contains updates and security fixes.


Load balancer and load balancer monitor for IBM Cloud Provider 3563
:   New version contains updates and security fixes.


Portieris admission controller v0.13.37
:   See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.13.37){: external}


Red Hat OpenShift on IBM Cloud 4.20.18
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes#ocp-4-20-18_release-notes){: external}.


Tigera Operator v1.38.13
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.38.13){: external}.


## 20 April 2026, Worker node fix pack 4.20.18_1544_openshift
{: #cl-boms-42018_1544_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.18_1544_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   


Red Hat OpenShift 4.20.18
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-18_release-notes){: external}.


Red Hat CoreOS 4.20.18
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-18_release-notes){: external}.


HAProxy c7e825675cbd75e8433801c99f8aca3b207a5a46
:   Resolves the following CVEs: [CVE-2026-27135](https://nvd.nist.gov/vuln/detail/cve-2026-27135).


## 06 April 2026, Worker node fix pack 4.20.17_1543_openshift
{: #cl-boms-42017_1543_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.17_1543_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [5.4.2.4](https://workbench.cisecurity.org/sections/2758938/recommendations/4466977){: external}


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [5.4.2.4](https://workbench.cisecurity.org/sections/2758938/recommendations/4466977){: external}


Red Hat OpenShift 4.20.17
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-17_release-notes){: external}.


Red Hat CoreOS 4.20.17
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-17_release-notes){: external}.


HAProxy 91cc06f4e0a123d06f5ee7c226df6fb83e1ca223
:   Resolves the following CVEs: [CVE-2025-14831](https://nvd.nist.gov/vuln/detail/cve-2025-14831), and [CVE-2025-9820](https://nvd.nist.gov/vuln/detail/cve-2025-9820).


## 24 March 2026, Worker node fix pack 4.20.16_1542_openshift
{: #cl-boms-42016_1542_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.16_1542_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   


Red Hat OpenShift 4.20.16
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-16_release-notes){: external}.


Red Hat CoreOS 4.20.16
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-16_release-notes){: external}. CIS benchmark compliance [3.4.2.3](https://workbench.cisecurity.org/sections/1594542/recommendations/2564568){: external}.


HAProxy 10c8639e6b5829d0af51a22755e13756f34630cf
:   Resolves the following CVEs: [CVE-2025-15281](https://nvd.nist.gov/vuln/detail/cve-2025-15281), and [CVE-2026-0915](https://nvd.nist.gov/vuln/detail/cve-2026-0915).


## 11 March 2026, Worker node fix pack 4.20.15_1540_openshift
{: #cl-boms-42015_1540_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.15_1540_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   


Red Hat OpenShift 4.20.15
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-15_release-notes){: external}.


Red Hat CoreOS 4.20.15
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-15_release-notes){: external}. CIS benchmark compliance [1.1.3.2](https://workbench.cisecurity.org/sections/1594516/recommendations/2564412){: external}, [1.1.3.3](https://workbench.cisecurity.org/sections/1594516/recommendations/2564414){: external}, [3.4.2](https://workbench.cisecurity.org/benchmarks/11478/sections/1594542){: external}, [4.2.2.3](https://workbench.cisecurity.org/sections/1594553/recommendations/2564633){: external}


HAProxy 965c403695b15b3410d87a3772002edbc5ed2569
:   Resolves the following CVEs: [CVE-2025-69419](https://nvd.nist.gov/vuln/detail/cve-2025-69419).


## 24 February 2026, Worker node fix pack 4.20.14_1539_openshift
{: #cl-boms-42014_1539_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.14_1539_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [1.6.3](https://workbench.cisecurity.org/sections/2758919/recommendations/4466876){: external}


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [1.6.3](https://workbench.cisecurity.org/sections/2758919/recommendations/4466876){: external}


Red Hat OpenShift 4.20.14
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-14_release-notes){: external}.


Red Hat CoreOS 4.20.14
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-14_release-notes){: external}. CIS benchmark compliance [5.2.2](https://workbench.cisecurity.org/sections/1594521/recommendations/2564440){: external}, [5.2.3](https://workbench.cisecurity.org/sections/1594521/recommendations/2564444){: external}, [5.2.4](https://workbench.cisecurity.org/sections/1594521/recommendations/2564446){: external}, [5.2.18](https://workbench.cisecurity.org/sections/1594521/recommendations/2564555){: external}


HAProxy 2bf1aebe51a37cd9b4661656ce21e53f918166ea
:   Resolves the following CVEs: [CVE-2025-6176](https://nvd.nist.gov/vuln/detail/cve-2025-6176).


## 09 February 2026, Worker node fix pack 4.20.13_1537_openshift
{: #cl-boms-42013_1537_openshift_W}

The following list shows the components included in the worker node fix pack 4.20.13_1537_openshift. Worker node patch updates can be applied by updating, reloading (in classic infrastructure), or replacing (in VPC infrastructure) the worker node.
{: shortdesc}

RHEL 9 (VPC) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [1.6.6](https://workbench.cisecurity.org/sections/2758919/recommendations/4466895){: external}, [3.1.3](https://workbench.cisecurity.org/sections/2758883/recommendations/4466704){: external}, [4.1.2](https://workbench.cisecurity.org/sections/2758898/recommendations/4466776){: external}, [4.3.4](https://workbench.cisecurity.org/sections/2758905/recommendations/4466822){: external}, [5.3.2.1](https://workbench.cisecurity.org/sections/2758922/recommendations/4466880){: external}, [5.3.3.2.4](https://workbench.cisecurity.org/sections/2758930/recommendations/4466941){: external}, [5.3.3.2.7](https://workbench.cisecurity.org/sections/2758930/recommendations/4466958){: external}, [5.3.3.3.1](https://workbench.cisecurity.org/sections/2758934/recommendations/4466960){: external}, [5.3.3.4.2](https://workbench.cisecurity.org/sections/2758935/recommendations/4466965){: external}, [5.4.1.5](https://workbench.cisecurity.org/sections/2758937/recommendations/4466972){: external}, [5.4.2.5](https://workbench.cisecurity.org/sections/2758938/recommendations/4466978){: external}Resolves the following CVEs: [RHSA-2025:19930](https://access.redhat.com/errata/RHSA-2025:19930), [CVE-2024-36350](https://nvd.nist.gov/vuln/detail/cve-2024-36350), [CVE-2024-36357](https://nvd.nist.gov/vuln/detail/cve-2024-36357), and [CVE-2025-40300](https://nvd.nist.gov/vuln/detail/cve-2025-40300).


RHEL 9 (Classic) 5.14.0-570.62.1.el9_6
:   CIS benchmark compliance [1.6.6](https://workbench.cisecurity.org/sections/2758919/recommendations/4466895){: external}, [3.1.3](https://workbench.cisecurity.org/sections/2758883/recommendations/4466704){: external}, [4.1.2](https://workbench.cisecurity.org/sections/2758898/recommendations/4466776){: external}, [4.3.4](https://workbench.cisecurity.org/sections/2758905/recommendations/4466822){: external}, [5.3.2.1](https://workbench.cisecurity.org/sections/2758922/recommendations/4466880){: external}, [5.3.3.2.4](https://workbench.cisecurity.org/sections/2758930/recommendations/4466941){: external}, [5.3.3.2.7](https://workbench.cisecurity.org/sections/2758930/recommendations/4466958){: external}, [5.3.3.3.1](https://workbench.cisecurity.org/sections/2758934/recommendations/4466960){: external}, [5.3.3.4.2](https://workbench.cisecurity.org/sections/2758935/recommendations/4466965){: external}, [5.4.1.5](https://workbench.cisecurity.org/sections/2758937/recommendations/4466972){: external}, [5.4.2.5](https://workbench.cisecurity.org/sections/2758938/recommendations/4466978){: external}Resolves the following CVEs: [RHSA-2025:19930](https://access.redhat.com/errata/RHSA-2025:19930), [CVE-2024-36350](https://nvd.nist.gov/vuln/detail/cve-2024-36350), [CVE-2024-36357](https://nvd.nist.gov/vuln/detail/cve-2024-36357), and [CVE-2025-40300](https://nvd.nist.gov/vuln/detail/cve-2025-40300).


Red Hat OpenShift 4.20.13
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-13_release-notes){: external}.


Red Hat CoreOS 4.20.13
:   For more information, see the [change logs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/release_notes/ocp-4-20-release-notes.html#ocp-4-20-13_release-notes){: external}.


HAProxy ace947f4ecf45f28effe8d125ffda48f9890223b
:   Resolves the following CVEs: [CVE-2025-14104](https://nvd.nist.gov/vuln/detail/cve-2025-14104).
