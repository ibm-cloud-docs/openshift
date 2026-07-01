---

copyright:
  years: 2024, 2026

lastupdated: "2026-07-01"


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


### Version 4.21 - v1.0.5_4.21_351283493, released 25 June 2026
{: #cl-add-ons-openshift-virtualization-v105_421_351283493}

[Default version]{: tag-green}

- Updates Go to version `1.26.4`.
- kubevirt-hyperconverged-operator.v4.21.10
- kubernetes-nmstate-operator.4.21.0-202606171653
- node-maintenance-operator.v5.6.1
- Resolves the following Prisma CVEs: [CVE-2026-39821](https://nvd.nist.gov/vuln/detail/CVE-2026-39821){: external}, [CVE-2026-41178](https://nvd.nist.gov/vuln/detail/CVE-2026-41178){: external}, [CVE-2026-47262](https://nvd.nist.gov/vuln/detail/CVE-2026-47262){: external}, and [CVE-2026-53488](https://nvd.nist.gov/vuln/detail/CVE-2026-53488){: external}.


### Version 4.21 - v1.0.4_4.21_347026591, released 15 June 2026
{: #cl-add-ons-openshift-virtualization-v104_421_347026591}

- Resolves the following CVEs: [CVE-2026-4438](https://nvd.nist.gov/vuln/detail/CVE-2026-4438){: external}, [CVE-2026-4046](https://nvd.nist.gov/vuln/detail/CVE-2026-4046){: external}, and [CVE-2026-4437](https://nvd.nist.gov/vuln/detail/CVE-2026-4437){: external}.
- Updates Go to version `1.26.4`.
- kubevirt-hyperconverged-operator.v4.21.8
- kubernetes-nmstate-operator.4.21.0-202605270323
- node-maintenance-operator.v5.6.1
- Resolves the following Prisma CVEs: [CVE-2026-33811](https://nvd.nist.gov/vuln/detail/CVE-2026-33811){: external}, [CVE-2026-33814](https://nvd.nist.gov/vuln/detail/CVE-2026-33814){: external}, [CVE-2026-39820](https://nvd.nist.gov/vuln/detail/CVE-2026-39820){: external}, [CVE-2026-39836](https://nvd.nist.gov/vuln/detail/CVE-2026-39836){: external}, [CVE-2026-42499](https://nvd.nist.gov/vuln/detail/CVE-2026-42499){: external}, [CVE-2026-39823](https://nvd.nist.gov/vuln/detail/CVE-2026-39823){: external}, and [CVE-2026-39826](https://nvd.nist.gov/vuln/detail/CVE-2026-39826){: external}.


## Version 4.20
{: #cl-add-ons-openshift-virtualization-4.20}


### Version 4.20 - v1.0.4_4.20_347026591, released 15 June 2026
{: #cl-add-ons-openshift-virtualization-v104_420_347026591}

- Resolves the following CVEs: [CVE-2026-4438](https://nvd.nist.gov/vuln/detail/CVE-2026-4438){: external}, [CVE-2026-4046](https://nvd.nist.gov/vuln/detail/CVE-2026-4046){: external}, and [CVE-2026-4437](https://nvd.nist.gov/vuln/detail/CVE-2026-4437){: external}.
- Updates Go to version `1.26.4`.
- kubevirt-hyperconverged-operator.v4.20.15
- kubernetes-nmstate-operator.4.20.0-202605130318
- node-maintenance-operator.v5.5.0
- Resolves the following Prisma CVEs: [CVE-2026-33811](https://nvd.nist.gov/vuln/detail/CVE-2026-33811){: external}, [CVE-2026-33814](https://nvd.nist.gov/vuln/detail/CVE-2026-33814){: external}, [CVE-2026-39820](https://nvd.nist.gov/vuln/detail/CVE-2026-39820){: external}, [CVE-2026-39836](https://nvd.nist.gov/vuln/detail/CVE-2026-39836){: external}, [CVE-2026-42499](https://nvd.nist.gov/vuln/detail/CVE-2026-42499){: external}, [CVE-2026-39823](https://nvd.nist.gov/vuln/detail/CVE-2026-39823){: external}, and [CVE-2026-39826](https://nvd.nist.gov/vuln/detail/CVE-2026-39826){: external}.
