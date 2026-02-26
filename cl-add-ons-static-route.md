---

copyright:
  years: 2024, 2026

lastupdated: "2026-02-26"


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


### v1.0.0-1661, released 06 February 2025
{: #cl-add-ons-static-route-v100-1661}

- Resolves the following CVEs: [CVE-2024-45337](https://nvd.nist.gov/vuln/detail/CVE-2024-45337){: external}, and [CVE-2024-45338](https://nvd.nist.gov/vuln/detail/CVE-2024-45338){: external}.
- CVE-2024-45337 
- CVE-2024-45338 
- Fix CVE-2024-45337 and CVE-2024-45338


### 1.0.0_1581, released 14 November 2024
{: #cl-add-ons-static-route-100_1581}

- Updates to the latest `ubi-minimal` base image for the operator build. 
- `addon-static-route v1.0.0_1581`


### 1.0.0_1415, released 3 October 2024
{: #cl-add-ons-static-route-100_1415}

- Updates the Operator SDK version to `1.36.1`.
- Updates the Go builder version to `1.22`.
- Fixes a bug in `nodeSelector` that didn't properly select nodes on a multi-subnet cluster.


### 1.0.0_1122, released 17 July 2023
{: #cl-add-ons-static-route-100_1122}

Adds support for different worker node architectures.



### 1.0.0_649, released 8 September 2021
{: #cl-add-ons-static-route-100_649}

- Uses `apiextensions.k8s.io/v1` instead of `apiextensions.k8s.io/v1beta1`.
