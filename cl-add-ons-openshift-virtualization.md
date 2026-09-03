---

copyright:
  years: 2024, 2026

lastupdated: "2026-09-03"


keywords: change log, version history, OpenShift Virtualization

subcollection: "openshift"

---

{{site.data.keyword.attribute-definition-list}}




# OpenShift Virtualization add-on version change log
{: #cl-add-ons-openshift-virtualization}


Patch updates
:   Patch updates are delivered automatically by IBM and don't contain any feature updates or changes in the supported add-on and cluster versions.

Release updates
:   Release updates contain new features or changes in the supported add-on or cluster versions. You must manually apply release updates to your cluster autoscaler add-on.

To view a list of add-ons and the supported cluster versions, run the following command or see the [Supported cluster add-ons table](/docs/openshift?topic=openshift-supported-cluster-addon-versions).

```sh
ibmcloud oc cluster addon versions
```
{: pre}


Review the version history for OpenShift Virtualization.
{: shortdesc}


## Version 4.21
{: #cl-add-ons-openshift-virtualization-4.21}


### 31 August 2026, Version 4.21 - v1.0.9_4.21_366720299
{: #cl-add-ons-openshift-virtualization-v109_421_366720299}

[Default version]{: tag-green}

- Updates Go to version `1.26.6`.
- kubevirt-hyperconverged-operator.v4.21.16
- kubernetes-nmstate-operator.4.21.0-202608172306
- node-maintenance-operator.v5.6.1
- Resolves the following Prisma CVEs: [CVE-2026-33818](https://nvd.nist.gov/vuln/detail/cve-2026-33818){: external}, [CVE-2026-39821](https://nvd.nist.gov/vuln/detail/cve-2026-39821){: external}, [CVE-2026-46600](https://nvd.nist.gov/vuln/detail/cve-2026-46600){: external}, [CVE-2026-56853](https://nvd.nist.gov/vuln/detail/cve-2026-56853){: external}, [CVE-2026-56858](https://nvd.nist.gov/vuln/detail/cve-2026-56858){: external}, [CVE-2026-56859](https://nvd.nist.gov/vuln/detail/cve-2026-56859){: external}, [CVE-2026-56860](https://nvd.nist.gov/vuln/detail/cve-2026-56860){: external}, and [CVE-2026-56862](https://nvd.nist.gov/vuln/detail/cve-2026-56862){: external}.


### 10 August 2026, Version 4.21 - v1.0.8_4.21
{: #cl-add-ons-openshift-virtualization-v108_421}

- Updates Go to version `1.26.5`.
- Update cpu and memory requests/limits for ibm-openshift-virt-operator pods 
- kubevirt-hyperconverged-operator.v4.21.13
- kubernetes-nmstate-operator.4.21.0-202607221131
- node-maintenance-operator.v5.6.1


### 06 August 2026, Version 4.21 - v1.0.7_4.21_360518333
{: #cl-add-ons-openshift-virtualization-v107_421_360518333}

- Updates Go to version `1.26.5`.
- Populate RedHat operators version in IBMOpenShiftVirtualization CR 
- kubevirt-hyperconverged-operator.v4.21.13
- kubernetes-nmstate-operator.4.21.0-202607221131
- node-maintenance-operator.v5.6.1
- Resolves the following Prisma CVEs: [CVE-2026-25934](https://nvd.nist.gov/vuln/detail/cve-2026-25934){: external}, [CVE-2026-34165](https://nvd.nist.gov/vuln/detail/cve-2026-34165){: external}, [CVE-2026-44973](https://nvd.nist.gov/vuln/detail/cve-2026-44973){: external}, [CVE-2026-41506](https://nvd.nist.gov/vuln/detail/cve-2026-41506){: external}, [CVE-2026-45022](https://nvd.nist.gov/vuln/detail/cve-2026-45022){: external}, [CVE-2026-44740](https://nvd.nist.gov/vuln/detail/cve-2026-44740){: external}, [CVE-2026-45571](https://nvd.nist.gov/vuln/detail/cve-2026-45571){: external}, [CVE-2026-33762](https://nvd.nist.gov/vuln/detail/cve-2026-33762){: external}, [CVE-2026-53488](https://nvd.nist.gov/vuln/detail/cve-2026-53488){: external}, [CVE-2026-50163](https://nvd.nist.gov/vuln/detail/cve-2026-50163){: external}, [CVE-2026-45570](https://nvd.nist.gov/vuln/detail/cve-2026-45570){: external}, [CVE-2026-49478](https://nvd.nist.gov/vuln/detail/cve-2026-49478){: external}, [CVE-2026-39822](https://nvd.nist.gov/vuln/detail/cve-2026-39822){: external}, [CVE-2026-41178](https://nvd.nist.gov/vuln/detail/cve-2026-41178){: external}, [CVE-2026-47262](https://nvd.nist.gov/vuln/detail/cve-2026-47262){: external}, [CVE-2026-42505](https://nvd.nist.gov/vuln/detail/cve-2026-42505){: external}, [CVE-2026-5450](https://nvd.nist.gov/vuln/detail/cve-2026-5450){: external}, [CVE-2026-5928](https://nvd.nist.gov/vuln/detail/cve-2026-5928){: external}, [CVE-2026-6238](https://nvd.nist.gov/vuln/detail/cve-2026-6238){: external}, [CVE-2026-5435](https://nvd.nist.gov/vuln/detail/cve-2026-5435){: external}, [GHSA-gcjh-h69q-9w9g](https://github.com/advisories/GHSA-gcjh-h69q-9w9g){: external}, [GHSA-hrxh-6v49-42gf](https://github.com/advisories/GHSA-hrxh-6v49-42gf){: external}, and [GHSA-w5pp-99ch-qj29](https://github.com/advisories/GHSA-w5pp-99ch-qj29){: external}.


### 25 June 2026, Version 4.21 - v1.0.5_4.21_351283493
{: #cl-add-ons-openshift-virtualization-v105_421_351283493}

- Updates Go to version `1.26.4`.
- kubevirt-hyperconverged-operator.v4.21.10
- kubernetes-nmstate-operator.4.21.0-202606171653
- node-maintenance-operator.v5.6.1
- Resolves the following Prisma CVEs: [CVE-2026-39821](https://nvd.nist.gov/vuln/detail/cve-2026-39821){: external}, [CVE-2026-41178](https://nvd.nist.gov/vuln/detail/cve-2026-41178){: external}, [CVE-2026-47262](https://nvd.nist.gov/vuln/detail/cve-2026-47262){: external}, and [CVE-2026-53488](https://nvd.nist.gov/vuln/detail/cve-2026-53488){: external}.


### 15 June 2026, Version 4.21 - v1.0.4_4.21_347026591
{: #cl-add-ons-openshift-virtualization-v104_421_347026591}

- Resolves the following CVEs: [CVE-2026-4438](https://nvd.nist.gov/vuln/detail/cve-2026-4438){: external}, [CVE-2026-4046](https://nvd.nist.gov/vuln/detail/cve-2026-4046){: external}, and [CVE-2026-4437](https://nvd.nist.gov/vuln/detail/cve-2026-4437){: external}.
- Updates Go to version `1.26.4`.
- kubevirt-hyperconverged-operator.v4.21.8
- kubernetes-nmstate-operator.4.21.0-202605270323
- node-maintenance-operator.v5.6.1
- Resolves the following Prisma CVEs: [CVE-2026-33811](https://nvd.nist.gov/vuln/detail/cve-2026-33811){: external}, [CVE-2026-33814](https://nvd.nist.gov/vuln/detail/cve-2026-33814){: external}, [CVE-2026-39820](https://nvd.nist.gov/vuln/detail/cve-2026-39820){: external}, [CVE-2026-39836](https://nvd.nist.gov/vuln/detail/cve-2026-39836){: external}, [CVE-2026-42499](https://nvd.nist.gov/vuln/detail/cve-2026-42499){: external}, [CVE-2026-39823](https://nvd.nist.gov/vuln/detail/cve-2026-39823){: external}, and [CVE-2026-39826](https://nvd.nist.gov/vuln/detail/cve-2026-39826){: external}.


## Version 4.20
{: #cl-add-ons-openshift-virtualization-4.20}


### 15 June 2026, Version 4.20 - v1.0.4_4.20_347026591
{: #cl-add-ons-openshift-virtualization-v104_420_347026591}

- Resolves the following CVEs: [CVE-2026-4438](https://nvd.nist.gov/vuln/detail/cve-2026-4438){: external}, [CVE-2026-4046](https://nvd.nist.gov/vuln/detail/cve-2026-4046){: external}, and [CVE-2026-4437](https://nvd.nist.gov/vuln/detail/cve-2026-4437){: external}.
- Updates Go to version `1.26.4`.
- kubevirt-hyperconverged-operator.v4.20.15
- kubernetes-nmstate-operator.4.20.0-202605130318
- node-maintenance-operator.v5.5.0
- Resolves the following Prisma CVEs: [CVE-2026-33811](https://nvd.nist.gov/vuln/detail/cve-2026-33811){: external}, [CVE-2026-33814](https://nvd.nist.gov/vuln/detail/cve-2026-33814){: external}, [CVE-2026-39820](https://nvd.nist.gov/vuln/detail/cve-2026-39820){: external}, [CVE-2026-39836](https://nvd.nist.gov/vuln/detail/cve-2026-39836){: external}, [CVE-2026-42499](https://nvd.nist.gov/vuln/detail/cve-2026-42499){: external}, [CVE-2026-39823](https://nvd.nist.gov/vuln/detail/cve-2026-39823){: external}, and [CVE-2026-39826](https://nvd.nist.gov/vuln/detail/cve-2026-39826){: external}.
