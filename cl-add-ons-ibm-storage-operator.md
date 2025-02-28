---

copyright:
  years: 2024, 2025

lastupdated: "2025-02-28"


keywords: change log, version history, IBM Storage Operator

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

<!-- The content in this topic is auto-generated except for reuse-snippets indicated with {[ ]}. -->


# IBM Storage Operator add-on version change log
{: #cl-add-ons-ibm-storage-operator}

Review the version history for IBM Storage Operator.
{: shortdesc}



## Version 1.0
{: #cl-add-ons-ibm-storage-operator-1.0}


### 1.0.17_173, released 19 February 2025
{: #cl-add-ons-ibm-storage-operator-1017_173}

- Resolves the following CVEs: [CVE-2024-5535](https://nvd.nist.gov/vuln/detail/CVE-2024-5535){: external}.
- Updates the golang base image to 1.22.12. 




## Version 1.0.0
{: #ibm-storage-operator-1.0.0}

### Change log for version 1.0.16_169, released 11 December 2024
{: #ibm-storage-operator-1.0.16_169}


- Resolves [CVE-2024-51744](https://nvd.nist.gov/vuln/detail/CVE-2024-51744){: external}.



### Change log for version 1.0.15_163, released 3 October 2024
{: #ibm-storage-operator-1.0.15_163}

- Fixes issue with reconciliation of the `file-csi-driver-status` and `addon-vpc-file-csi-driver-configmap` in case it is deleted.
- Updates the golang base image to `1.22.7`.
- Resolves [CVE-2024-2398](https://nvd.nist.gov/vuln/detail/CVE-2024-2398){: external}, [CVE-2024-37370](https://nvd.nist.gov/vuln/detail/CVE-2024-37370){: external}, [CVE-2024-37371](https://nvd.nist.gov/vuln/detail/CVE-2024-37371){: external}.


### Change log for version 1.0.13_151, released 26 August 2024
{: #ibm-storage-operator-1.0.13_151}

- Applies the `PACKAGE_DEPLOYER_VERSION` image automatically on the worker pools where EIT is enabled.
- Updates the golang image to `1.21.13-community`.


### Change log for version 1.0.12_147, released 15 July 2024
{: #ibm-storage-operator-1.0.12_147}

- Updates the golang image to `1.21.12-community`.
- Resolves [CVE-2024-28182](https://nvd.nist.gov/vuln/detail/CVE-2024-28182){: external} and [CVE-2023-2953](https://nvd.nist.gov/vuln/detail/CVE-2023-2953){: external}.


### 1.0.10_141, released 03 July 2024
{: #ibm-storage-operator-1.0.0-initial}

- Initial release.
