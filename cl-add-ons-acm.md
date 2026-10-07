---

copyright:
  years: 2024, 2026

lastupdated: "2026-10-07"


keywords: change log, version history, ACM

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# ACM add-on version change log
{: #cl-add-ons-acm}


Patch updates
:   Patch updates are delivered automatically by IBM and don't contain any feature updates or changes in the supported add-on and cluster versions.

Release updates
:   Release updates contain new features or changes in the supported add-on or cluster versions. You must manually apply release updates to your cluster autoscaler add-on.

To view a list of add-ons and the supported cluster versions, run the following command or see the [Supported cluster add-ons table](/docs/openshift?topic=openshift-supported-cluster-addon-versions).

```sh
ibmcloud oc cluster addon versions
```
{: pre}


Review the version history for ACM.
{: shortdesc}


## Version 2.17.0
{: #cl-add-ons-acm-2.17.0}


### 06 October 2026, Version 2.17.0 - 2.17.7
{: #cl-add-ons-acm-2177}

- Updates Go to version `1.26.6`.
- Billing IAM API key fallback when Trusted Profile is unavailable.


### 30 September 2026, Version 2.17.0 - 2.17.6
{: #cl-add-ons-acm-2176}

- Resolves the following CVEs: [CVE-2026-84445](https://nvd.nist.gov/vuln/detail/cve-2026-84445){: external}, and [CVE-2026-63209](https://nvd.nist.gov/vuln/detail/cve-2026-63209){: external}.
- Updates Go to version `1.26.6`.
- VA fixes. Bumped builder image to v9.8.145. Removed shell and utility binaries from runtime image. 


### 29 September 2026, Version 2.17.0 - 2.17.4
{: #cl-add-ons-acm-2174}

- Resolves the following CVEs: [CVE-2026-88031](https://nvd.nist.gov/vuln/detail/cve-2026-88031){: external}, [CVE-2026-2303](https://nvd.nist.gov/vuln/detail/cve-2026-2303){: external}, [CVE-2026-78662](https://nvd.nist.gov/vuln/detail/cve-2026-78662){: external}, [CVE-2026-56855](https://nvd.nist.gov/vuln/detail/cve-2026-56855){: external}, [CVE-2026-56854](https://nvd.nist.gov/vuln/detail/cve-2026-56854){: external}, [CVE-2026-84445](https://nvd.nist.gov/vuln/detail/cve-2026-84445){: external}, [CVE-2026-84304](https://nvd.nist.gov/vuln/detail/cve-2026-84304){: external}, [CVE-2026-84303](https://nvd.nist.gov/vuln/detail/cve-2026-84303){: external}, and [CVE-2026-33186](https://nvd.nist.gov/vuln/detail/cve-2026-33186){: external}.
- Updates Go to version `1.26.6`.
- VA fixes. 


### 29 September 2026, Version 2.17.0 - 2.17.5
{: #cl-add-ons-acm-2175}

- Resolves the following CVEs: [CVE-2026-88031](https://nvd.nist.gov/vuln/detail/cve-2026-88031){: external}, [CVE-2026-2303](https://nvd.nist.gov/vuln/detail/cve-2026-2303){: external}, [CVE-2026-78662](https://nvd.nist.gov/vuln/detail/cve-2026-78662){: external}, [CVE-2026-56855](https://nvd.nist.gov/vuln/detail/cve-2026-56855){: external}, [CVE-2026-56854](https://nvd.nist.gov/vuln/detail/cve-2026-56854){: external}, [CVE-2026-84445](https://nvd.nist.gov/vuln/detail/cve-2026-84445){: external}, [CVE-2026-84304](https://nvd.nist.gov/vuln/detail/cve-2026-84304){: external}, [CVE-2026-84303](https://nvd.nist.gov/vuln/detail/cve-2026-84303){: external}, and [CVE-2026-33186](https://nvd.nist.gov/vuln/detail/cve-2026-33186){: external}.
- Updates Go to version `1.26.6`.
- VA fixes. 


### 01 September 2026, Version 2.17.0 - 2.17.3
{: #cl-add-ons-acm-2173}

- Updates Go to version `1.26.6`.
- VA fixes. Bumped Go to 1.26.6 and builder image to v9.8.88. 


### 04 August 2026, Version 2.17.0 - 2.17.1
{: #cl-add-ons-acm-2171}

- Updates Go to version `1.25.11`.
- Initial release of ACM 2.17.


### 04 August 2026, Version 2.17.0 - 2.17.2
{: #cl-add-ons-acm-2172}

- Updates Go to version `1.25.11`.
- VA fixes. 


## Version 2.16.0
{: #cl-add-ons-acm-2.16.0}


### 06 October 2026, Version 2.16.0 - 2.16.18
{: #cl-add-ons-acm-21618}

- Updates Go to version `1.26.6`.
- Billing IAM API key fallback when Trusted Profile is unavailable.


### 30 September 2026, Version 2.16.0 - 2.16.17
{: #cl-add-ons-acm-21617}

- Resolves the following CVEs: [CVE-2026-84445](https://nvd.nist.gov/vuln/detail/cve-2026-84445){: external}, and [CVE-2026-63209](https://nvd.nist.gov/vuln/detail/cve-2026-63209){: external}.
- Updates Go to version `1.26.6`.
- VA fixes. Bumped builder image to v9.8.145. Removed shell and utility binaries from runtime image. 


### 29 September 2026, Version 2.16.0 - 2.16.16
{: #cl-add-ons-acm-21616}

- Resolves the following CVEs: [CVE-2026-88031](https://nvd.nist.gov/vuln/detail/cve-2026-88031){: external}, [CVE-2026-2303](https://nvd.nist.gov/vuln/detail/cve-2026-2303){: external}, [CVE-2026-78662](https://nvd.nist.gov/vuln/detail/cve-2026-78662){: external}, [CVE-2026-56855](https://nvd.nist.gov/vuln/detail/cve-2026-56855){: external}, [CVE-2026-56854](https://nvd.nist.gov/vuln/detail/cve-2026-56854){: external}, [CVE-2026-84445](https://nvd.nist.gov/vuln/detail/cve-2026-84445){: external}, [CVE-2026-84304](https://nvd.nist.gov/vuln/detail/cve-2026-84304){: external}, [CVE-2026-84303](https://nvd.nist.gov/vuln/detail/cve-2026-84303){: external}, and [CVE-2026-33186](https://nvd.nist.gov/vuln/detail/cve-2026-33186){: external}.
- Updates Go to version `1.26.6`.
- VA fixes. 


### 01 September 2026, Version 2.16.0 - 2.16.15
{: #cl-add-ons-acm-21615}

- Updates Go to version `1.26.6`.
- VA fixes. Bumped Go to 1.26.6 and builder image to v9.8.88. 


### 16 June 2026, Version 2.16.0 - 2.16.12
{: #cl-add-ons-acm-21612}

- Updates Go to version `1.25.11`.
- VA fixes. Bumped Go to 1.25.11 and builder image to v9.8.37. 


### 16 June 2026, Version 2.16.0 - 2.16.13
{: #cl-add-ons-acm-21613}

- Updates Go to version `1.25.11`.
- VA fixes. Bumped Go to 1.25.11 and builder image to v9.8.37. 


### 03 June 2026, Version 2.16.0 - 2.16.10
{: #cl-add-ons-acm-21610}

- Updates Go to version `1.23.7`.
- Disabled plan change. 


### 03 June 2026, Version 2.16.0 - 2.16.11
{: #cl-add-ons-acm-21611}

- Updates Go to version `1.23.7`.
- Disabled plan change. 


### 02 June 2026, Version 2.16.0 - 2.16.7
{: #cl-add-ons-acm-2167}

- Updates Go to version `1.23.7`.
- Virtualisation support re-enabled. Upgrade blocked. 


### 02 June 2026, Version 2.16.0 - 2.16.8
{: #cl-add-ons-acm-2168}

- Updates Go to version `1.23.7`.
- Virtualisation support re-enabled. Upgrade blocked. 


### 02 June 2026, Version 2.16.0 - 2.16.9
{: #cl-add-ons-acm-2169}

- Updates Go to version `1.23.7`.
- VA fixes. 


### 11 May 2026, Version 2.16.0 - 2.16.4
{: #cl-add-ons-acm-2164}

- Updates Go to version `1.23.7`.
- Removed virtualisation support. 


### 11 May 2026, Version 2.16.0 - 2.16.5
{: #cl-add-ons-acm-2165}

- Updates Go to version `1.23.7`.
- Removed virtualisation support. 


### 11 May 2026, Version 2.16.0 - 2.16.6
{: #cl-add-ons-acm-2166}

- Updates Go to version `1.23.7`.
- Removed virtualisation support. 


### 07 May 2026, Version 2.16.0 - 2.16.3
{: #cl-add-ons-acm-2163}

- Updates Go to version `1.23.7`.
- BM naming changes and billing calculation fix. 


### 15 April 2026, Version 2.16.0 - 2.16.1
{: #cl-add-ons-acm-2161}

- Updates Go to version `1.23.7`.
- E2E fixes. 


### 15 April 2026, Version 2.16.0 - 2.16.2
{: #cl-add-ons-acm-2162}

- Updates Go to version `1.23.7`.
- E2E fixes. 


### 06 April 2026, Version 2.16.0
{: #cl-add-ons-acm-2160}

- Updates Go to version `1.23.7`.
- Initial release of ACM 2.16.

