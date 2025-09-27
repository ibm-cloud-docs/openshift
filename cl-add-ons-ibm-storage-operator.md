---

copyright:
  years: 2024, 2025

lastupdated: "2025-09-27"


keywords: change log, version history, IBM Storage Operator

subcollection: "openshift"

---

{{site.data.keyword.attribute-definition-list}}




# IBM Storage Operator add-on version change log
{: #cl-add-ons-ibm-storage-operator}

Review the version history for IBM Storage Operator.
{: shortdesc}



## Version 1.0
{: #cl-add-ons-ibm-storage-operator-1.0}


### 1.0.27_264, released 22 September 2025
{: #cl-add-ons-ibm-storage-operator-1027_264}

[Default version]{: tag-green}

- Resolves the following CVEs: [CVE-2025-8058](https://nvd.nist.gov/vuln/detail/CVE-2025-8058){: external}.
- Updates Go to version `1.23.12`.
- Adds EIT support for OpenShift clusters with RHEL worker nodes.
- {'Adds 3 new storage classes': 'ibmc-vpc-file-regional, ibmc-vpc-file-regional-max-bandwidth, and ibmc-vpc-file-regional-max-bandwidth-sds. These classes are based on VPC regional file share profiles and are available in Beta for allowlisted accounts.'}
- `ibm-vpc-package-deployer v1.0.5`

### 1.0.26_258, released 18 August 2025
{: #cl-add-ons-ibm-storage-operator-1026_258}

[Default version]{: tag-green}

- Updates Go to version `1.23.11`.
- Fixes an issue with setting the default storage class from the add-on configMap. 
- Added EIT support for RHEL 9.6 OS.
- `ibm-vpc-package-deployer v1.0.4`

### 1.0.25_248, released 18 July 2025
{: #cl-add-ons-ibm-storage-operator-1025_248}

[Default version]{: tag-green}

- Resolves the following CVEs: [CVE-2025-4802](https://nvd.nist.gov/vuln/detail/CVE-2025-4802){: external}, [CVE-2025-4673](https://nvd.nist.gov/vuln/detail/CVE-2025-4673){: external}, [CVE-2024-23337](https://nvd.nist.gov/vuln/detail/CVE-2024-23337){: external}, and [CVE-2025-48060](https://nvd.nist.gov/vuln/detail/CVE-2025-48060){: external}.
- Updates Go to version `1.23.10`.
- Updates the Kubernetes client libraries from 1.32.3 to 1.32.6, ensuring compatibility with newer clusters. 
- Updates imagePullPolicy to IfNotPresent for all containers in the deployment. 
- `armada-storage-secret v1.2.64`

### 1.0.23_230, released 16 June 2025
{: #cl-add-ons-ibm-storage-operator-1023_230}

- Resolves the following CVEs: [CVE-2025-0395](https://nvd.nist.gov/vuln/detail/CVE-2025-0395){: external}, and [CVE-2020-11023](https://nvd.nist.gov/vuln/detail/CVE-2020-11023){: external}.
- Updates Go to version `1.23.9`.
- Fixes issue with reconciliation of file resources. 
- Fixes an issue where updates to the storage operator no longer cause disruption to file resources. 
- Improves the events published in file-csi-driver-status configmap. 
- Updates rolling update strategy for operator controller pods to prevent reconciliation delays. 
- Updates to the EIT packages are now automatically applied if EIT is already installed. 
- Updates the Kubernetes 1.32 client libraries, ensuring compatibility with newer clusters. 
- Adds the capability in the operator to persist the `addon-vpc-file-csi-driver-configmap` and `file-csi-driver-status configmaps.

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
