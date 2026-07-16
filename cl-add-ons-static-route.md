---

copyright:
  years: 2024, 2026

lastupdated: "2026-07-16"


keywords: change log, version history, Static Route

subcollection: "openshift"

---

{{site.data.keyword.attribute-definition-list}}




# Static Route add-on version change log
{: #cl-add-ons-static-route}


Patch updates
:   Patch updates are delivered automatically by IBM and don't contain any feature updates or changes in the supported add-on and cluster versions.

Release updates
:   Release updates contain new features or changes in the supported add-on or cluster versions. You must manually apply release updates to your cluster autoscaler add-on.

To view a list of add-ons and the supported cluster versions, run the following command or see the [Supported cluster add-ons table](/docs/openshift?topic=openshift-supported-cluster-addon-versions).

```sh
ibmcloud oc cluster addon versions
```
{: pre}


Review the version history for Static Route.
{: shortdesc}


## Version 1.0.0
{: #cl-add-ons-static-route-1.0.0}


### Version 1.0.0 - v1.0.0-342645253, released 23 May 2026
{: #cl-add-ons-static-route-v100-342645253}

- Resolves the following CVEs: [CVE-2026-33814](https://nvd.nist.gov/vuln/detail/CVE-2026-33814){: external}, and [CVE-2026-39836](https://nvd.nist.gov/vuln/detail/CVE-2026-39836){: external}.
- CVE-2026-33814 
- CVE-2026-39836 
- Release the Static Route Operator with Go version 1.25.10
- Fix CVEs CVE-2026-33814, CVE-2026-39836


### Version 1.0.0 - v1.0.0-1661, released 06 February 2025
{: #cl-add-ons-static-route-v100-1661}

- Resolves the following CVEs: [CVE-2024-45337](https://nvd.nist.gov/vuln/detail/CVE-2024-45337){: external}, and [CVE-2024-45338](https://nvd.nist.gov/vuln/detail/CVE-2024-45338){: external}.
- CVE-2024-45337 
- CVE-2024-45338 
- Fix CVE-2024-45337 and CVE-2024-45338


### Version 1.0.0 - 1.0.0_1581, released 14 November 2024
{: #cl-add-ons-static-route-100_1581}

- Updates to the latest `ubi-minimal` base image for the operator build. 
- `addon-static-route v1.0.0_1581`
