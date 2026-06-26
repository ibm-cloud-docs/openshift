---

copyright:
  years: 2024, 2026

lastupdated: "2026-06-26"


keywords: change log, version history, VPC Block CSI Driver

subcollection: "openshift"

---

{{site.data.keyword.attribute-definition-list}}




# VPC Block CSI Driver add-on version change log
{: #cl-add-ons-vpc-block-csi-driver}


Patch updates
:   Patch updates are delivered automatically by IBM and don't contain any feature updates or changes in the supported add-on and cluster versions.

Release updates
:   Release updates contain new features or changes in the supported add-on or cluster versions. You must manually apply release updates to your cluster autoscaler add-on.

To view a list of add-ons and the supported cluster versions, run the following command or see the [Supported cluster add-ons table](/docs/openshift?topic=openshift-supported-cluster-addon-versions).

```sh
ibmcloud oc cluster addon versions
```
{: pre}


Review the version history for VPC Block CSI Driver.
{: shortdesc}


## Version 5.2
{: #cl-add-ons-vpc-block-csi-driver-5.2}


### Version 5.2 - v5.2.54_345553805, released 10 June 2026
{: #cl-add-ons-vpc-block-csi-driver-v5254_345553805}

- Resolves the following CVEs: [CVE-2026-4438](https://nvd.nist.gov/vuln/detail/CVE-2026-4438){: external}, [CVE-2026-4046](https://nvd.nist.gov/vuln/detail/CVE-2026-4046){: external}, and [CVE-2026-4437](https://nvd.nist.gov/vuln/detail/CVE-2026-4437){: external}.
- `armada-storage-secret v1.3.51`
- `ibm-csi-init-container v1.0.22`


### Version 5.2 - v5.2.52_342345117, released 28 May 2026
{: #cl-add-ons-vpc-block-csi-driver-v5252_342345117}

- Resolves the following CVEs: [CVE-2026-33811](https://nvd.nist.gov/vuln/detail/CVE-2026-33811){: external}, [CVE-2026-39820](https://nvd.nist.gov/vuln/detail/CVE-2026-39820){: external}, [CVE-2026-33814](https://nvd.nist.gov/vuln/detail/CVE-2026-33814){: external}, [CVE-2026-39836](https://nvd.nist.gov/vuln/detail/CVE-2026-39836){: external}, [CVE-2026-42499](https://nvd.nist.gov/vuln/detail/CVE-2026-42499){: external}, [CVE-2026-39823](https://nvd.nist.gov/vuln/detail/CVE-2026-39823){: external}, and [CVE-2026-39826](https://nvd.nist.gov/vuln/detail/CVE-2026-39826){: external}.
- `armada-storage-secret v1.3.49`
- `ibm-csi-init-container v1.0.20`


### Version 5.2 - v5.2.51_340196278, released 20 May 2026
{: #cl-add-ons-vpc-block-csi-driver-v5251_340196278}

- Resolves the following CVEs: [CVE-2026-33186](https://nvd.nist.gov/vuln/detail/CVE-2026-33186){: external}, [CVE-2026-29181](https://nvd.nist.gov/vuln/detail/CVE-2026-29181){: external}, [CVE-2026-4878](https://nvd.nist.gov/vuln/detail/CVE-2026-4878){: external}, and [CVE-2026-29111](https://nvd.nist.gov/vuln/detail/CVE-2026-29111){: external}.
- `armada-storage-secret v1.3.48`
- `ibm-csi-init-container v1.0.18`


### Version 5.2 - v5.2.50_338659383, released 13 May 2026
{: #cl-add-ons-vpc-block-csi-driver-v5250_338659383}

- Fixed udevadm trigger execution and added critical device existence validation to prevent data loss during volume formatting operations 
- `armada-storage-secret v1.3.47`
- `ibm-csi-init-container v1.0.15`


### Version 5.2 - v5.2.49_335380306, released 30 April 2026
{: #cl-add-ons-vpc-block-csi-driver-v5249_335380306}

- Resolves the following CVEs: [CVE-2026-32281](https://nvd.nist.gov/vuln/detail/CVE-2026-32281){: external}, [CVE-2026-32280](https://nvd.nist.gov/vuln/detail/CVE-2026-32280){: external}, [CVE-2026-32283](https://nvd.nist.gov/vuln/detail/CVE-2026-32283){: external}, and [CVE-2026-32289](https://nvd.nist.gov/vuln/detail/CVE-2026-32289){: external}.
- `armada-storage-secret v1.3.45`
- `ibm-csi-init-container v1.0.15`


### Version 5.2 - v5.2.48_330814432, released 14 April 2026
{: #cl-add-ons-vpc-block-csi-driver-v5248_330814432}

- Resolves the following CVEs: [CVE-2026-33186](https://nvd.nist.gov/vuln/detail/CVE-2026-33186){: external}.
- `armada-storage-secret v1.3.44`
- `ibm-csi-init-container v1.0.14`


### Version 5.2 - v5.2.47_326490882, released 25 March 2026
{: #cl-add-ons-vpc-block-csi-driver-v5247_326490882}

- Resolves the following CVEs: [CVE-2026-25679](https://nvd.nist.gov/vuln/detail/CVE-2026-25679){: external}, [CVE-2026-27139](https://nvd.nist.gov/vuln/detail/CVE-2026-27139){: external}, and [CVE-2026-27142](https://nvd.nist.gov/vuln/detail/CVE-2026-27142){: external}.
- `armada-storage-secret v1.3.43`
- `ibm-csi-init-container v1.0.13`


### Version 5.2 - v5.2.46_321044202, released 02 March 2026
{: #cl-add-ons-vpc-block-csi-driver-v5246_321044202}

- Resolves the following CVEs: [CVE-2026-0861](https://nvd.nist.gov/vuln/detail/CVE-2026-0861){: external}, [CVE-2025-15281](https://nvd.nist.gov/vuln/detail/CVE-2025-15281){: external}, and [CVE-2026-0915](https://nvd.nist.gov/vuln/detail/CVE-2026-0915){: external}.
- Supports the creation of snapshot in the user defined resource group. 
- `armada-storage-secret v1.3.42`


### Version 5.2 - v5.2.45_319683178, released 26 February 2026
{: #cl-add-ons-vpc-block-csi-driver-v5245_319683178}

- Resolves the following CVEs: [CVE-2025-14104](https://nvd.nist.gov/vuln/detail/CVE-2025-14104){: external}, and [CVE-2025-68121](https://nvd.nist.gov/vuln/detail/CVE-2025-68121){: external}.
- `armada-storage-secret v1.3.41`


### Version 5.2 - v5.2.44_316463149, released 10 February 2026
{: #cl-add-ons-vpc-block-csi-driver-v5244_316463149}

- Resolves the following CVEs: [CVE-2025-15467](https://nvd.nist.gov/vuln/detail/CVE-2025-15467){: external}, [CVE-2025-11187](https://nvd.nist.gov/vuln/detail/CVE-2025-11187){: external}, [CVE-2025-15468](https://nvd.nist.gov/vuln/detail/CVE-2025-15468){: external}, [CVE-2025-15469](https://nvd.nist.gov/vuln/detail/CVE-2025-15469){: external}, [CVE-2025-66199](https://nvd.nist.gov/vuln/detail/CVE-2025-66199){: external}, [CVE-2025-68160](https://nvd.nist.gov/vuln/detail/CVE-2025-68160){: external}, [CVE-2025-69418](https://nvd.nist.gov/vuln/detail/CVE-2025-69418){: external}, [CVE-2025-69419](https://nvd.nist.gov/vuln/detail/CVE-2025-69419){: external}, [CVE-2025-69420](https://nvd.nist.gov/vuln/detail/CVE-2025-69420){: external}, [CVE-2025-69421](https://nvd.nist.gov/vuln/detail/CVE-2025-69421){: external}, [CVE-2026-22795](https://nvd.nist.gov/vuln/detail/CVE-2026-22795){: external}, [CVE-2026-22796](https://nvd.nist.gov/vuln/detail/CVE-2026-22796){: external}, [CVE-2025-9086](https://nvd.nist.gov/vuln/detail/CVE-2025-9086){: external}, [CVE-2025-61726](https://nvd.nist.gov/vuln/detail/CVE-2025-61726){: external}, and [CVE-2025-61730](https://nvd.nist.gov/vuln/detail/CVE-2025-61730){: external}.
- `armada-storage-secret v1.3.40`


### Version 5.2 - v5.2.43_313466999, released 02 February 2026
{: #cl-add-ons-vpc-block-csi-driver-v5243_313466999}

- Fixes xfs filesystem expansion failure during CSI volume resize operation 


### Version 5.2 - v5.2.42_310488886, released 21 January 2026
{: #cl-add-ons-vpc-block-csi-driver-v5242_310488886}

- Resolves the following CVEs: [CVE-2025-61727](https://nvd.nist.gov/vuln/detail/CVE-2025-61727){: external}, [CVE-2025-61729](https://nvd.nist.gov/vuln/detail/CVE-2025-61729){: external}, [CVE-2025-4598](https://nvd.nist.gov/vuln/detail/CVE-2025-4598){: external}, and [CVE-2025-13281](https://nvd.nist.gov/vuln/detail/CVE-2025-13281){: external}.
- Updates K8s client libraries from 1.32.8 to 1.32.10 in iks-vpc-block-driver container 
- `armada-storage-secret v1.3.39`


### Version 5.2 - 5.2.41_296897820, released 12 November 2025
{: #cl-add-ons-vpc-block-csi-driver-5241_296897820}

- Resolves the following CVEs: [CVE-2025-61725](https://nvd.nist.gov/vuln/detail/CVE-2025-61725){: external}, [CVE-2025-61723](https://nvd.nist.gov/vuln/detail/CVE-2025-61723){: external}, [CVE-2025-58189](https://nvd.nist.gov/vuln/detail/CVE-2025-58189){: external}, and [CVE-2025-58185](https://nvd.nist.gov/vuln/detail/CVE-2025-58185){: external}.
- Updates Go to version `1.25.3`.
- `armada-storage-secret v1.3.36`


### Version 5.2 - 5.2.40_293222012, released 05 November 2025
{: #cl-add-ons-vpc-block-csi-driver-5240_293222012}

- Resolves the following CVEs: [CVE-2025-5187](https://nvd.nist.gov/vuln/detail/CVE-2025-5187){: external}, [CVE-2025-8058](https://nvd.nist.gov/vuln/detail/CVE-2025-8058){: external}, and [CVE-2025-47906](https://nvd.nist.gov/vuln/detail/CVE-2025-47906){: external}.
- Updates Go to version `1.23.12`.
- Updates k8s package to 1.32.8 in iks-vpc-block-driver container 
- `armada-storage-secret v1.3.35`


### Version 5.2 - 5.2.38_828, released 14 July 2025
{: #cl-add-ons-vpc-block-csi-driver-5238_828}

- Resolves the following CVEs: [CVE-2025-4563](https://nvd.nist.gov/vuln/detail/CVE-2025-4563){: external}, [CVE-2025-4673](https://nvd.nist.gov/vuln/detail/CVE-2025-4673){: external}, and [CVE-2020-8561](https://nvd.nist.gov/vuln/detail/CVE-2020-8561){: external}.
- Updates Go to version `1.23.10`.
- Updates k8s package to 1.32.6 in iks-vpc-block-driver container 
- Updates imagePullPolicy to IfNotPresent for all containers in the deployment. 
- `armada-storage-secret v1.3.30`


### Version 5.2 - 5.2.36_778, released 30 May 2025
{: #cl-add-ons-vpc-block-csi-driver-5236_778}

- Resolves the following CVEs: [CVE-2024-9042](https://nvd.nist.gov/vuln/detail/CVE-2024-9042){: external}, and [CVE-2025-0426](https://nvd.nist.gov/vuln/detail/CVE-2025-0426){: external}.
- Updates k8s package to 1.32.3 in iks-vpc-block-driver container. 
- New storage classes ibmc-vpc-block-sdp
- ibmc-vpc-block-sdp-max-bandwidth
- and ibmc-vpc-block-sdp-max-bandwidth-sds supported based on new block storage SSD defined performance profile. These classes are available in allowlisted accounts only.
- `armada-storage-secret v1.3.27`
- `csi-provisioner v5.2.0`
- `csi-resizer v1.13.2`
- `csi-snapshotter v8.2.1`
- `csi-attacher v4.8.1`
- `livenessprobe:v2.15.0`
- `csi-node-driver-registrar v2.13.0`


### Version 5.2 - 5.2.33_735, released 09 May 2025
{: #cl-add-ons-vpc-block-csi-driver-5233_735}

- Resolves the following CVEs: [CVE-2020-11023](https://nvd.nist.gov/vuln/detail/CVE-2020-11023){: external}, and [CVE-2025-0395](https://nvd.nist.gov/vuln/detail/CVE-2025-0395){: external}.
- Updates the golang base image to 1.23.8. 
- Updates the armada-storage-secret to v1.3.26. 


### Version 5.2 - 5.2.31_687, released 17 February 2025
{: #cl-add-ons-vpc-block-csi-driver-5231_687}

- Resolves the following CVEs: [CVE-2024-45339](https://nvd.nist.gov/vuln/detail/CVE-2024-45339){: external}, and [CVE-2024-45338](https://nvd.nist.gov/vuln/detail/CVE-2024-45338){: external}.
- Resiliency improvement to use VPC Storage service API for tagging volumes. This doesn't impact existing or new PVCs. This reduces the number of Kubernetes service API calls. 
- Updates the golang base image to 1.22.12. 
- Updates the armada-storage-secret to v1.3.22. 


## Version 5.1
{: #cl-add-ons-vpc-block-csi-driver-5.1}


### Version 5.1 - v5.1.54_345553861, released 10 June 2026
{: #cl-add-ons-vpc-block-csi-driver-v5154_345553861}

- Resolves the following CVEs: [CVE-2026-4438](https://nvd.nist.gov/vuln/detail/CVE-2026-4438){: external}, [CVE-2026-4046](https://nvd.nist.gov/vuln/detail/CVE-2026-4046){: external}, and [CVE-2026-4437](https://nvd.nist.gov/vuln/detail/CVE-2026-4437){: external}.
- `armada-storage-secret v1.2.87`
- `ibm-csi-init-container v1.0.22`


### Version 5.1 - v5.1.52_342345162, released 28 May 2026
{: #cl-add-ons-vpc-block-csi-driver-v5152_342345162}

- Resolves the following CVEs: [CVE-2026-33811](https://nvd.nist.gov/vuln/detail/CVE-2026-33811){: external}, [CVE-2026-39820](https://nvd.nist.gov/vuln/detail/CVE-2026-39820){: external}, [CVE-2026-33814](https://nvd.nist.gov/vuln/detail/CVE-2026-33814){: external}, [CVE-2026-39836](https://nvd.nist.gov/vuln/detail/CVE-2026-39836){: external}, [CVE-2026-42499](https://nvd.nist.gov/vuln/detail/CVE-2026-42499){: external}, [CVE-2026-39823](https://nvd.nist.gov/vuln/detail/CVE-2026-39823){: external}, and [CVE-2026-39826](https://nvd.nist.gov/vuln/detail/CVE-2026-39826){: external}.
- `armada-storage-secret v1.2.85`
- `ibm-csi-init-container v1.0.20`


### Version 5.1 - v5.1.51_340196313, released 20 May 2026
{: #cl-add-ons-vpc-block-csi-driver-v5151_340196313}

- Resolves the following CVEs: [CVE-2026-33186](https://nvd.nist.gov/vuln/detail/CVE-2026-33186){: external}, [CVE-2026-29181](https://nvd.nist.gov/vuln/detail/CVE-2026-29181){: external}, [CVE-2026-4878](https://nvd.nist.gov/vuln/detail/CVE-2026-4878){: external}, and [CVE-2026-29111](https://nvd.nist.gov/vuln/detail/CVE-2026-29111){: external}.
- `armada-storage-secret v1.2.83`
- `ibm-csi-init-container v1.0.18`


### Version 5.1 - v5.1.50_338876479, released 13 May 2026
{: #cl-add-ons-vpc-block-csi-driver-v5150_338876479}

- Fixed udevadm trigger execution and added critical device existence validation to prevent data loss during volume formatting operations 
- `armada-storage-secret v1.2.82`
- `ibm-csi-init-container v1.0.15`


### Version 5.1 - v5.1.49_335379980, released 30 April 2026
{: #cl-add-ons-vpc-block-csi-driver-v5149_335379980}

- Resolves the following CVEs: [CVE-2026-32281](https://nvd.nist.gov/vuln/detail/CVE-2026-32281){: external}, [CVE-2026-32280](https://nvd.nist.gov/vuln/detail/CVE-2026-32280){: external}, [CVE-2026-32283](https://nvd.nist.gov/vuln/detail/CVE-2026-32283){: external}, and [CVE-2026-32289](https://nvd.nist.gov/vuln/detail/CVE-2026-32289){: external}.
- `armada-storage-secret v1.2.80`
- `ibm-csi-init-container v1.0.15`


### Version 5.1 - v5.1.48_330814388, released 14 April 2026
{: #cl-add-ons-vpc-block-csi-driver-v5148_330814388}

- Resolves the following CVEs: [CVE-2026-33186](https://nvd.nist.gov/vuln/detail/CVE-2026-33186){: external}.
- `armada-storage-secret v1.2.79`
- `ibm-csi-init-container v1.0.14`


### Version 5.1 - v5.1.47_326491091, released 25 March 2026
{: #cl-add-ons-vpc-block-csi-driver-v5147_326491091}

- Resolves the following CVEs: [CVE-2026-25679](https://nvd.nist.gov/vuln/detail/CVE-2026-25679){: external}, [CVE-2026-27139](https://nvd.nist.gov/vuln/detail/CVE-2026-27139){: external}, and [CVE-2026-27142](https://nvd.nist.gov/vuln/detail/CVE-2026-27142){: external}.
- `armada-storage-secret v1.2.78`
- `ibm-csi-init-container v1.0.13`


### Version 5.1 - v5.1.46_321044176, released 02 March 2026
{: #cl-add-ons-vpc-block-csi-driver-v5146_321044176}

- Resolves the following CVEs: [CVE-2026-0861](https://nvd.nist.gov/vuln/detail/CVE-2026-0861){: external}, [CVE-2025-15281](https://nvd.nist.gov/vuln/detail/CVE-2025-15281){: external}, and [CVE-2026-0915](https://nvd.nist.gov/vuln/detail/CVE-2026-0915){: external}.
- `armada-storage-secret v1.2.77`


### Version 5.1 - v5.1.44_319682969, released 26 February 2026
{: #cl-add-ons-vpc-block-csi-driver-v5144_319682969}

- Resolves the following CVEs: [CVE-2025-14104](https://nvd.nist.gov/vuln/detail/CVE-2025-14104){: external}, [CVE-2025-47911](https://nvd.nist.gov/vuln/detail/CVE-2025-47911){: external}, [CVE-2026-0915](https://nvd.nist.gov/vuln/detail/CVE-2026-0915){: external}, [CVE-2025-68121](https://nvd.nist.gov/vuln/detail/CVE-2025-68121){: external}, and [CVE-2025-58190](https://nvd.nist.gov/vuln/detail/CVE-2025-58190){: external}.
- `armada-storage-secret v1.2.76`


### Version 5.1 - v5.1.43_316462421, released 10 February 2026
{: #cl-add-ons-vpc-block-csi-driver-v5143_316462421}

- Resolves the following CVEs: [CVE-2025-15467](https://nvd.nist.gov/vuln/detail/CVE-2025-15467){: external}, [CVE-2025-11187](https://nvd.nist.gov/vuln/detail/CVE-2025-11187){: external}, [CVE-2025-15468](https://nvd.nist.gov/vuln/detail/CVE-2025-15468){: external}, [CVE-2025-15469](https://nvd.nist.gov/vuln/detail/CVE-2025-15469){: external}, [CVE-2025-66199](https://nvd.nist.gov/vuln/detail/CVE-2025-66199){: external}, [CVE-2025-68160](https://nvd.nist.gov/vuln/detail/CVE-2025-68160){: external}, [CVE-2025-69418](https://nvd.nist.gov/vuln/detail/CVE-2025-69418){: external}, [CVE-2025-69419](https://nvd.nist.gov/vuln/detail/CVE-2025-69419){: external}, [CVE-2025-69420](https://nvd.nist.gov/vuln/detail/CVE-2025-69420){: external}, [CVE-2025-69421](https://nvd.nist.gov/vuln/detail/CVE-2025-69421){: external}, [CVE-2026-22795](https://nvd.nist.gov/vuln/detail/CVE-2026-22795){: external}, [CVE-2026-22796](https://nvd.nist.gov/vuln/detail/CVE-2026-22796){: external}, and [CVE-2025-9086](https://nvd.nist.gov/vuln/detail/CVE-2025-9086){: external}.
- `armada-storage-secret v1.2.75`


### Version 5.1 - v5.1.42_313460253, released 02 February 2026
{: #cl-add-ons-vpc-block-csi-driver-v5142_313460253}

- Fixes xfs filesystem expansion failure during CSI volume resize operation 


### Version 5.1 - v5.1.41_310494703, released 21 January 2026
{: #cl-add-ons-vpc-block-csi-driver-v5141_310494703}

- Resolves the following CVEs: [CVE-2025-61727](https://nvd.nist.gov/vuln/detail/CVE-2025-61727){: external}, [CVE-2025-61729](https://nvd.nist.gov/vuln/detail/CVE-2025-61729){: external}, [CVE-2025-4598](https://nvd.nist.gov/vuln/detail/CVE-2025-4598){: external}, and [CVE-2025-13281](https://nvd.nist.gov/vuln/detail/CVE-2025-13281){: external}.
- Updates K8s client libraries from 1.32.8 to 1.32.10 in iks-vpc-block-driver container 
- `armada-storage-secret v1.2.74`


### Version 5.1 - 5.1.40_296898008, released 12 November 2025
{: #cl-add-ons-vpc-block-csi-driver-5140_296898008}

- Resolves the following CVEs: [CVE-2025-61725](https://nvd.nist.gov/vuln/detail/CVE-2025-61725){: external}, [CVE-2025-61723](https://nvd.nist.gov/vuln/detail/CVE-2025-61723){: external}, [CVE-2025-58189](https://nvd.nist.gov/vuln/detail/CVE-2025-58189){: external}, and [CVE-2025-58185](https://nvd.nist.gov/vuln/detail/CVE-2025-58185){: external}.
- Updates Go to version `1.25.3`.
- `armada-storage-secret v1.2.70`


### Version 5.1 - 5.1.39_293222093, released 05 November 2025
{: #cl-add-ons-vpc-block-csi-driver-5139_293222093}

- Resolves the following CVEs: [CVE-2025-5187](https://nvd.nist.gov/vuln/detail/CVE-2025-5187){: external}, [CVE-2025-8058](https://nvd.nist.gov/vuln/detail/CVE-2025-8058){: external}, and [CVE-2025-47906](https://nvd.nist.gov/vuln/detail/CVE-2025-47906){: external}.
- Updates Go to version `1.23.12`.
- Updates k8s package to 1.32.8 in iks-vpc-block-driver container 
- `armada-storage-secret v1.2.69`


### Version 5.1 - 5.1.37_827, released 14 July 2025
{: #cl-add-ons-vpc-block-csi-driver-5137_827}

- Resolves the following CVEs: [CVE-2025-4563](https://nvd.nist.gov/vuln/detail/CVE-2025-4563){: external}, [CVE-2025-4673](https://nvd.nist.gov/vuln/detail/CVE-2025-4673){: external}, and [CVE-2020-8561](https://nvd.nist.gov/vuln/detail/CVE-2020-8561){: external}.
- Updates Go to version `1.23.10`.
- Updates k8s package to 1.32.6 in iks-vpc-block-driver container 
- Updates imagePullPolicy to IfNotPresent for all containers in the deployment. 
- `armada-storage-secret v1.2.64`


### Version 5.1 - 5.1.35_763, released 30 May 2025
{: #cl-add-ons-vpc-block-csi-driver-5135_763}

- Resolves the following CVEs: [CVE-2024-9042](https://nvd.nist.gov/vuln/detail/CVE-2024-9042){: external}, [CVE-2025-0426](https://nvd.nist.gov/vuln/detail/CVE-2025-0426){: external}, [CVE-2025-22872](https://nvd.nist.gov/vuln/detail/CVE-2025-22872){: external}, and [CVE-2025-30204](https://nvd.nist.gov/vuln/detail/CVE-2025-30204){: external}.
- Updates k8s package to 1.32.3 in iks-vpc-block-driver container 
- `armada-storage-secret v1.2.61`
- `csi-provisioner v5.2.0`
- `csi-resizer v1.13.2`
- `csi-snapshotter v8.2.1`
- `csi-attacher v4.8.1`
- `livenessprobe:v2.15.0`
- `csi-node-driver-registrar v2.13.0`


### Version 5.1 - 5.1.34_740, released 09 May 2025
{: #cl-add-ons-vpc-block-csi-driver-5134_740}

- Resolves the following CVEs: [CVE-2020-11023](https://nvd.nist.gov/vuln/detail/CVE-2020-11023){: external}, and [CVE-2025-0395](https://nvd.nist.gov/vuln/detail/CVE-2025-0395){: external}.
- Updates the golang base image to 1.23.8. 
- Updates the armada-storage-secret to v1.2.60. 


### Version 5.1 - 5.1.33_685, released 17 February 2025
{: #cl-add-ons-vpc-block-csi-driver-5133_685}

- Resolves the following CVEs: [CVE-2024-45339](https://nvd.nist.gov/vuln/detail/CVE-2024-45339){: external}, and [CVE-2024-45338](https://nvd.nist.gov/vuln/detail/CVE-2024-45338){: external}.
- Resiliency improvement to use VPC Storage service API for tagging volumes. This doesn't impact existing or new PVCs. This reduces the number of Kubernetes service API calls. 
- Updates the golang base image to 1.22.12. 
- Updates the armada-storage-secret to v1.2.55. 


### Version 5.1.31_656, released 11 December 2024
{: #5.1.31_656_is_block_relnote}

- Resolves [CVE-2024-51744](https://nvd.nist.gov/vuln/detail/CVE-2024-51744){: external}.


### Version 5.1.29_642, released 20 November 2024
{: #5.1.29_642_is_block_relnote}

- Updates the golang base image to `1.22.9`.
- Introduces an `init` container to clean up any leftover controller pods from 5.2 release.


### Version 5.1.26_601, released 3 October 2024
{: #5.1.26_601_is_block_relnote}

- Updates the golang base image to `1.22.7`.
- Updates to Kubernetes 1.30 client libraries.
- Updates the CSI specification to version `1.9.0`.
- Fixes a security issue for the CSI sidecar liveness probe. The sidecar now runs as non-root in the Node Server pod.
- Adds the ability to set a default storage class. For more information, see [Setting the default storage class](/docs/openshift?topic=openshift-storage-file-vpc-apps#vpc-file-set-default-sc).
- Updates the following sidecar images: `csi-provisioner:v5.0.2`, `csi-resizer:v1.11.2`, `csi-snapshotter:v8.0.1`, `csi-attacher:v4.6.1`, `livenessprobe:v2.13.1`, and `csi-node-driver-registrar:v2.11.1`
- Resolves [CVE-2024-2398](https://nvd.nist.gov/vuln/detail/CVE-2024-2398){: external}, [CVE-2024-37370](https://nvd.nist.gov/vuln/detail/CVE-2024-37370){: external}, [CVE-2024-37371](https://nvd.nist.gov/vuln/detail/CVE-2024-37371){: external}.


### Version 5.1.25_574, released 15 July 2024
{: #5.1.25_574_is_block_relnote}

- Updates the golang image to `1.21.12-community`.
- Updates the `armada-storage-secret` to `v1.2.40`.
- Resolves [CVE-2024-28182](https://nvd.nist.gov/vuln/detail/CVE-2024-28182){: external} and [CVE-2023-2953](https://nvd.nist.gov/vuln/detail/CVE-2023-2953){: external}.


### Version 5.1.24_567, released 21 June 2024
{: #5.1.24_567_is_block_relnote}

- Updates `golang` to `1.21.11-community`.
- Updates the `armada-storage-secret` to `v1.3.8`.
- Resolves: [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961){: external}, [CVE-2024-33599](https://nvd.nist.gov/vuln/detail/CVE-2024-33599){: external}, [CVE-2024-33600](https://nvd.nist.gov/vuln/detail/CVE-2024-33600){: external}, [CVE-2024-33601](https://nvd.nist.gov/vuln/detail/CVE-2024-33601){: external}, [CVE-2024-33602](https://nvd.nist.gov/vuln/detail/CVE-2024-33602){: external}.


### Version 5.1.23_543, released 10 May 2024
{: #5.1.23_543_is_block_relnote}

- Updates `golang` to `1.21.9-community`.
- Removes `curl` package from base image.
- Updates the `armada-storage-secret` to `v1.2.35`.
- Resolves [CVE-2023-46218](https://nvd.nist.gov/vuln/detail/CVE-2023-46218){: external}, [CVE-2023-28322](https://nvd.nist.gov/vuln/detail/CVE-2023-28322){: external}, and [CVE-2023-38546](https://nvd.nist.gov/vuln/detail/CVE-2023-38546){: external}.


### Version 5.1.22_522, released 08 March 2024
{: #5.1.22_522_is_block_relnote}

- Base image migrated from UBI to golang.


### Version 5.1.21_506, released 08 February 2024
{: #5.1.21_506_is_block_relnote}

- Changes how the IAM endpoint is determined for VPC Gen2 clusters.
- Upgrades Kubernetes client library to 1.28.
- Upgrades CSI spec to 1.8.0.
- Resolves the following CVEs: [CVE-2022-48560](https://nvd.nist.gov/vuln/detail/CVE-2022-48560){: external}, [CVE-2022-48564](https://nvd.nist.gov/vuln/detail/CVE-2022-48564){: external}, [CVE-2023-39615](https://nvd.nist.gov/vuln/detail/CVE-2023-39615){: external}, [CVE-2023-43804](https://nvd.nist.gov/vuln/detail/CVE-2023-43804){: external}, [CVE-2023-45803](https://nvd.nist.gov/vuln/detail/CVE-2023-45803){: external}, and [CVE-2023-5981](https://nvd.nist.gov/vuln/detail/CVE-2023-5981){: external}.
- Updates the following sidecar images: 
    - `armada-storage-secret` to `v1.2.31`.
    - `csi-attacher` to `v4.4.3`.
    - `csi-node-driver-registrar` to `v2.9.3`.
    - `csi-provisioner` to `v3.6.3`.
    - `csi-resizer` to `v1.9.3`.
    - `csi-snapshotter` to `v6.3.3`.
    - `livenessprobe` to `v2.11.0`.


### Version 5.1.19_486, released 10 January 2024
{: #5.1.19_486_is_block_relnote}

- Resolves [CVE-2023-3446](https://nvd.nist.gov/vuln/detail/CVE-2023-3446){: external}, [CVE-2023-3817](https://nvd.nist.gov/vuln/detail/CVE-2023-3817){: external}, and [CVE-2023-5678](https://nvd.nist.gov/vuln/detail/CVE-2023-5678){: external}.
- Applies a security fix to use the correct socket path following SElinux policy module changes and CSI recommendations to use `/var/lib/kubelet/plugins/`.

## Change log for version 5.1.16_446, released 27 November 2023
{: #5.1.16_446_is_block_relnote}

- Updates Golang to `1.20.11`.
- Updates the UBI image to `8.9.1029`.
- Updates `armada-storage-secret` to `v1.2.29`.
- Resolves the following CVEs: [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/CVE-2023-22745){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [CVE-2023-40217](https://nvd.nist.gov/vuln/detail/CVE-2023-40217){: external}, and [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/CVE-2023-4641){: external}.


### Change log for version 5.1.15_419 released 13 November 2023
{: #5.1.15_419_is_block_relnote}

- Updates Golang `1.20.10`. 
- Updates the `storage-secret-sidecar` image to `1.2.28`.
- The add-on tries reaching the IAM endpoint/token exchange URL for 5 minutes, in case of timeout.
- Resolves the following CVEs: [CVE-2023-44487](https://nvd.nist.gov/vuln/detail/CVE-2023-44487){: external}, [CVE-2023-4911](https://nvd.nist.gov/vuln/detail/CVE-2023-4911){: external}, [CVE-2023-4527](https://nvd.nist.gov/vuln/detail/CVE-2023-4527){: external}, [CVE-2023-4806](https://nvd.nist.gov/vuln/detail/CVE-2023-4806){: external}, [CVE-2023-4813](https://nvd.nist.gov/vuln/detail/CVE-2023-4813){: external}, and [CVE-2023-39325](https://nvd.nist.gov/vuln/detail/CVE-2023-39325){: external}.


### Version 5.1.13_345, released 14 September 2023
{: #5.1.13_345_is_block_relnote}

- Updated the UBI image to `8.8-860`.
- Updated the Golang updated to `1.19.12`.
- Resolves the following CVEs: [CVE-2023-34969](https://nvd.nist.gov/vuln/detail/CVE-2023-34969){: external}, [CVE-2023-28321](https://nvd.nist.gov/vuln/detail/CVE-2023-28321){: external}, [CVE-2023-2602](https://nvd.nist.gov/vuln/detail/CVE-2023-2602){: external}, [CVE-2023-2603](https://nvd.nist.gov/vuln/detail/CVE-2023-2603){: external}, [CVE-2023-28484](https://nvd.nist.gov/vuln/detail/CVE-2023-28484){: external}, [CVE-2023-29469](https://nvd.nist.gov/vuln/detail/CVE-2023-29469){: external}, [CVE-2023-27536](https://nvd.nist.gov/vuln/detail/CVE-2023-27536){: external}, [CVE-2023-3899](https://nvd.nist.gov/vuln/detail/CVE-2023-3899){: external}, and [CVE-2023-32681](https://nvd.nist.gov/vuln/detail/CVE-2023-32681){: external}.


### Version 5.1.12_285, released 01 August 2023
{: #5.1.12_285_is_block_relnote}

- Node affinity added for controller server and node server, so that pods do not crash on Z system (s390x) based clusters.
- Resolves the following CVEs: [CVE-2023-26604](https://nvd.nist.gov/vuln/detail/CVE-2023-26604){: external}, [CVE-2020-24736](https://nvd.nist.gov/vuln/detail/CVE-2020-24736){: external}, [CVE-2023-1667](https://nvd.nist.gov/vuln/detail/CVE-2023-1667){: external}, and [CVE-2023-2283](https://nvd.nist.gov/vuln/detail/CVE-2023-2283){: external}.




### Version 5.0.23_437, released 27 November 2023
{: #5.0.23_437_is_block_relnote}

- Updates Golang to `1.20.11`.
- Updates the UBI image to `8.9.1029`.
- Updates `armada-storage-secret` to `v1.2.29`.
- Resolves the following CVEs: [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/CVE-2023-22745){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [CVE-2023-40217](https://nvd.nist.gov/vuln/detail/CVE-2023-40217){: external}, and [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/CVE-2023-4641){: external}.


### Version 5.0.21_401, released 13 November 2023
{: #5.0.21_401_is_block_relnote}

- Updates Golang to `1.20.10`. 
- Updates the `storage-secret-sidecar` image to `1.2.28`.
- Resolves the following CVEs: [CVE-2023-44487](https://nvd.nist.gov/vuln/detail/CVE-2023-44487){: external}, [CVE-2023-4911](https://nvd.nist.gov/vuln/detail/CVE-2023-4911){: external}, [CVE-2023-4527](https://nvd.nist.gov/vuln/detail/CVE-2023-4527){: external}, [CVE-2023-4806](https://nvd.nist.gov/vuln/detail/CVE-2023-4806){: external}, [CVE-2023-4813](https://nvd.nist.gov/vuln/detail/CVE-2023-4813){: external}, and [CVE-2023-39325](https://nvd.nist.gov/vuln/detail/CVE-2023-39325){: external}.


### Version 5.0.19_358, released 14 September 2023
{: #5.0.19_358_is_block_relnote}

- Updated the UBI image to `8.8-860`.
- Updated the Golang updated to `1.19.12`.
- Resolves the following CVEs: [CVE-2023-34969](https://nvd.nist.gov/vuln/detail/CVE-2023-34969){: external}, [CVE-2023-28321](https://nvd.nist.gov/vuln/detail/CVE-2023-28321){: external}, [CVE-2023-2602](https://nvd.nist.gov/vuln/detail/CVE-2023-2602){: external}, [CVE-2023-2603](https://nvd.nist.gov/vuln/detail/CVE-2023-2603){: external}, [CVE-2023-28484](https://nvd.nist.gov/vuln/detail/CVE-2023-28484){: external}, [CVE-2023-29469](https://nvd.nist.gov/vuln/detail/CVE-2023-29469){: external}, [CVE-2023-27536](https://nvd.nist.gov/vuln/detail/CVE-2023-27536){: external}, [CVE-2023-3899](https://nvd.nist.gov/vuln/detail/CVE-2023-3899){: external}, and [CVE-2023-32681](https://nvd.nist.gov/vuln/detail/CVE-2023-32681){: external}.


### Version 5.0.17_266, released 01 August 2023
{: #5.0.17_266_is_block_relnote}

- Node affinity added for controller server and node server, so that pods do not crash on Z system (s390x) based clusters.
- Resolves the following CVEs: [CVE-2023-26604](https://nvd.nist.gov/vuln/detail/CVE-2023-26604){: external}, [CVE-2020-24736](https://nvd.nist.gov/vuln/detail/CVE-2020-24736){: external}, [CVE-2023-1667](https://nvd.nist.gov/vuln/detail/CVE-2023-1667){: external}, and [CVE-2023-2283](https://nvd.nist.gov/vuln/detail/CVE-2023-2283){: external}.
