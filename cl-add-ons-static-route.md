---

copyright:
  years: 2024, 2025

lastupdated: "2025-01-17"


keywords: change log, version history, Static Route

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

<!-- The content in this topic is auto-generated except for reuse-snippets indicated with {[ ]}. -->


# Static Route add-on version change log
{: #cl-add-ons-static-route}

Review the version history for Static Route.
{: shortdesc}



## Version 1.0.0
{: #cl-add-ons-static-route-1.0.0}


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
