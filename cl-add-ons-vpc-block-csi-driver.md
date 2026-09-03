---

copyright:
  years: 2024, 2026

lastupdated: "2026-09-03"


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


## Version 5.1
{: #cl-add-ons-vpc-block-csi-driver-5.1}


### 10 January 2024, Version 5.1.19_486
{: #5.1.19_486_is_block_relnote}

- Resolves [CVE-2023-3446](https://nvd.nist.gov/vuln/detail/cve-2023-3446){: external}, [CVE-2023-3817](https://nvd.nist.gov/vuln/detail/cve-2023-3817){: external}, and [CVE-2023-5678](https://nvd.nist.gov/vuln/detail/cve-2023-5678){: external}.
- Applies a security fix to use the correct socket path following SElinux policy module changes and CSI recommendations to use `/var/lib/kubelet/plugins/`.

## Change log for version 5.1.16_446, released 27 November 2023
{: #5.1.16_446_is_block_relnote}

- Updates Golang to `1.20.11`.
- Updates the UBI image to `8.9.1029`.
- Updates `armada-storage-secret` to `v1.2.29`.
- Resolves the following CVEs: [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/cve-2023-22745){: external}, [CVE-2007-4559](https://access.redhat.com/security/cve/CVE-2007-4559){: external}, [CVE-2023-40217](https://nvd.nist.gov/vuln/detail/cve-2023-40217){: external}, and [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/cve-2023-4641){: external}.


### Change log for version 5.1.15_419 released 13 November 2023
{: #5.1.15_419_is_block_relnote}

- Updates Golang `1.20.10`. 
- Updates the `storage-secret-sidecar` image to `1.2.28`.
- The add-on tries reaching the IAM endpoint/token exchange URL for 5 minutes, in case of timeout.
- Resolves the following CVEs: [CVE-2023-44487](https://nvd.nist.gov/vuln/detail/cve-2023-44487){: external}, [CVE-2023-4911](https://nvd.nist.gov/vuln/detail/cve-2023-4911){: external}, [CVE-2023-4527](https://nvd.nist.gov/vuln/detail/cve-2023-4527){: external}, [CVE-2023-4806](https://nvd.nist.gov/vuln/detail/cve-2023-4806){: external}, [CVE-2023-4813](https://nvd.nist.gov/vuln/detail/cve-2023-4813){: external}, and [CVE-2023-39325](https://nvd.nist.gov/vuln/detail/cve-2023-39325){: external}.


### 19 August 2026, Version 5.1 - v5.1.59_362336122
{: #cl-add-ons-vpc-block-csi-driver-v5159_362336122}

- Resolves the following CVEs: [CVE-2026-13757](https://nvd.nist.gov/vuln/detail/cve-2026-13757){: external}, [CVE-2026-41989](https://nvd.nist.gov/vuln/detail/cve-2026-41989){: external}, and [CVE-2026-10846](https://nvd.nist.gov/vuln/detail/cve-2026-10846){: external}.
- `armada-storage-secret v1.3.62`
- `ibm-csi-init-container v1.0.31`


### 06 August 2026, Version 5.1 - v5.1.58_359720275
{: #cl-add-ons-vpc-block-csi-driver-v5158_359720275}

- Resolves the following CVEs: [CVE-2026-54369](https://nvd.nist.gov/vuln/detail/cve-2026-54369){: external}, [CVE-2026-54370](https://nvd.nist.gov/vuln/detail/cve-2026-54370){: external}, [CVE-2026-6238](https://nvd.nist.gov/vuln/detail/cve-2026-6238){: external}, [CVE-2026-5928](https://nvd.nist.gov/vuln/detail/cve-2026-5928){: external}, [GHSA-hrxh-6v49-42gf](https://github.com/advisories/GHSA-hrxh-6v49-42gf){: external}, and [CVE-2026-42505](https://nvd.nist.gov/vuln/detail/cve-2026-42505){: external}.
- `armada-storage-secret v1.3.60`
- `ibm-csi-init-container v1.0.29`


### 29 July 2026, Version 5.1 - v5.1.57_356951142
{: #cl-add-ons-vpc-block-csi-driver-v5157_356951142}

- Resolves the following CVEs: [CVE-2025-5278](https://nvd.nist.gov/vuln/detail/cve-2025-5278){: external}, [CVE-2026-2303](https://nvd.nist.gov/vuln/detail/cve-2026-2303){: external}, [CVE-2026-5450](https://nvd.nist.gov/vuln/detail/cve-2026-5450){: external}, [CVE-2025-58185](https://nvd.nist.gov/vuln/detail/cve-2025-58185){: external}, [CVE-2025-61727](https://nvd.nist.gov/vuln/detail/cve-2025-61727){: external}, [CVE-2025-61729](https://nvd.nist.gov/vuln/detail/cve-2025-61729){: external}, [CVE-2025-47912](https://nvd.nist.gov/vuln/detail/cve-2025-47912){: external}, [CVE-2025-58187](https://nvd.nist.gov/vuln/detail/cve-2025-58187){: external}, [CVE-2025-58188](https://nvd.nist.gov/vuln/detail/cve-2025-58188){: external}, [CVE-2025-58189](https://nvd.nist.gov/vuln/detail/cve-2025-58189){: external}, [CVE-2025-61723](https://nvd.nist.gov/vuln/detail/cve-2025-61723){: external}, [CVE-2025-61724](https://nvd.nist.gov/vuln/detail/cve-2025-61724){: external}, [CVE-2025-61726](https://nvd.nist.gov/vuln/detail/cve-2025-61726){: external}, [CVE-2025-61730](https://nvd.nist.gov/vuln/detail/cve-2025-61730){: external}, [CVE-2025-68121](https://nvd.nist.gov/vuln/detail/cve-2025-68121){: external}, [CVE-2025-47906](https://nvd.nist.gov/vuln/detail/cve-2025-47906){: external}, and [CVE-2025-22870](https://nvd.nist.gov/vuln/detail/cve-2025-22870){: external}.
- `armada-storage-secret v1.3.59`
- `ibm-csi-init-container v1.0.28`
- `csi-snapshotter v8.5.0`
- `csi-attacher v4.11.0`
- `csi-resizer v2.1.0`
- `csi-provisioner v6.2.0`
- `livenessprobe v2.18.0`
- `csi-node-driver-registrar v2.16.0`


### 25 June 2026, Version 5.1 - v5.1.55_349394898
{: #cl-add-ons-vpc-block-csi-driver-v5155_349394898}

- Resolves the following CVEs: [CVE-2026-28390](https://nvd.nist.gov/vuln/detail/cve-2026-28390){: external}, [CVE-2026-39821](https://nvd.nist.gov/vuln/detail/cve-2026-39821){: external}, [CVE-2026-34182](https://nvd.nist.gov/vuln/detail/cve-2026-34182){: external}, [CVE-2026-34183](https://nvd.nist.gov/vuln/detail/cve-2026-34183){: external}, [CVE-2026-45445](https://nvd.nist.gov/vuln/detail/cve-2026-45445){: external}, [CVE-2026-45447](https://nvd.nist.gov/vuln/detail/cve-2026-45447){: external}, [CVE-2026-34180](https://nvd.nist.gov/vuln/detail/cve-2026-34180){: external}, [CVE-2026-34181](https://nvd.nist.gov/vuln/detail/cve-2026-34181){: external}, [CVE-2026-42764](https://nvd.nist.gov/vuln/detail/cve-2026-42764){: external}, [CVE-2026-42766](https://nvd.nist.gov/vuln/detail/cve-2026-42766){: external}, [CVE-2026-42767](https://nvd.nist.gov/vuln/detail/cve-2026-42767){: external}, [CVE-2026-42768](https://nvd.nist.gov/vuln/detail/cve-2026-42768){: external}, [CVE-2026-42769](https://nvd.nist.gov/vuln/detail/cve-2026-42769){: external}, [CVE-2026-42770](https://nvd.nist.gov/vuln/detail/cve-2026-42770){: external}, [CVE-2026-7383](https://nvd.nist.gov/vuln/detail/cve-2026-7383){: external}, [CVE-2026-9076](https://nvd.nist.gov/vuln/detail/cve-2026-9076){: external}, and [CVE-2026-45446](https://nvd.nist.gov/vuln/detail/cve-2026-45446){: external}.
- `armada-storage-secret v1.3.56`
- `ibm-csi-init-container v1.0.26`


### 10 June 2026, Version 5.1 - v5.1.54_345553861
{: #cl-add-ons-vpc-block-csi-driver-v5154_345553861}

- Resolves the following CVEs: [CVE-2026-4438](https://nvd.nist.gov/vuln/detail/cve-2026-4438){: external}, [CVE-2026-4046](https://nvd.nist.gov/vuln/detail/cve-2026-4046){: external}, and [CVE-2026-4437](https://nvd.nist.gov/vuln/detail/cve-2026-4437){: external}.
- `armada-storage-secret v1.2.87`
- `ibm-csi-init-container v1.0.22`


### 28 May 2026, Version 5.1 - v5.1.52_342345162
{: #cl-add-ons-vpc-block-csi-driver-v5152_342345162}

- Resolves the following CVEs: [CVE-2026-33811](https://nvd.nist.gov/vuln/detail/cve-2026-33811){: external}, [CVE-2026-39820](https://nvd.nist.gov/vuln/detail/cve-2026-39820){: external}, [CVE-2026-33814](https://nvd.nist.gov/vuln/detail/cve-2026-33814){: external}, [CVE-2026-39836](https://nvd.nist.gov/vuln/detail/cve-2026-39836){: external}, [CVE-2026-42499](https://nvd.nist.gov/vuln/detail/cve-2026-42499){: external}, [CVE-2026-39823](https://nvd.nist.gov/vuln/detail/cve-2026-39823){: external}, and [CVE-2026-39826](https://nvd.nist.gov/vuln/detail/cve-2026-39826){: external}.
- `armada-storage-secret v1.2.85`
- `ibm-csi-init-container v1.0.20`


### 20 May 2026, Version 5.1 - v5.1.51_340196313
{: #cl-add-ons-vpc-block-csi-driver-v5151_340196313}

- Resolves the following CVEs: [CVE-2026-33186](https://nvd.nist.gov/vuln/detail/cve-2026-33186){: external}, [CVE-2026-29181](https://nvd.nist.gov/vuln/detail/cve-2026-29181){: external}, [CVE-2026-4878](https://nvd.nist.gov/vuln/detail/cve-2026-4878){: external}, and [CVE-2026-29111](https://nvd.nist.gov/vuln/detail/cve-2026-29111){: external}.
- `armada-storage-secret v1.2.83`
- `ibm-csi-init-container v1.0.18`


### 13 May 2026, Version 5.1 - v5.1.50_338876479
{: #cl-add-ons-vpc-block-csi-driver-v5150_338876479}

- Fixed udevadm trigger execution and added critical device existence validation to prevent data loss during volume formatting operations 
- `armada-storage-secret v1.2.82`
- `ibm-csi-init-container v1.0.15`


### 30 April 2026, Version 5.1 - v5.1.49_335379980
{: #cl-add-ons-vpc-block-csi-driver-v5149_335379980}

- Resolves the following CVEs: [CVE-2026-32281](https://nvd.nist.gov/vuln/detail/cve-2026-32281){: external}, [CVE-2026-32280](https://nvd.nist.gov/vuln/detail/cve-2026-32280){: external}, [CVE-2026-32283](https://nvd.nist.gov/vuln/detail/cve-2026-32283){: external}, and [CVE-2026-32289](https://nvd.nist.gov/vuln/detail/cve-2026-32289){: external}.
- `armada-storage-secret v1.2.80`
- `ibm-csi-init-container v1.0.15`


### 14 April 2026, Version 5.1 - v5.1.48_330814388
{: #cl-add-ons-vpc-block-csi-driver-v5148_330814388}

- Resolves the following CVEs: [CVE-2026-33186](https://nvd.nist.gov/vuln/detail/cve-2026-33186){: external}.
- `armada-storage-secret v1.2.79`
- `ibm-csi-init-container v1.0.14`


### 25 March 2026, Version 5.1 - v5.1.47_326491091
{: #cl-add-ons-vpc-block-csi-driver-v5147_326491091}

- Resolves the following CVEs: [CVE-2026-25679](https://nvd.nist.gov/vuln/detail/cve-2026-25679){: external}, [CVE-2026-27139](https://nvd.nist.gov/vuln/detail/cve-2026-27139){: external}, and [CVE-2026-27142](https://nvd.nist.gov/vuln/detail/cve-2026-27142){: external}.
- `armada-storage-secret v1.2.78`
- `ibm-csi-init-container v1.0.13`


### 02 March 2026, Version 5.1 - v5.1.46_321044176
{: #cl-add-ons-vpc-block-csi-driver-v5146_321044176}

- Resolves the following CVEs: [CVE-2026-0861](https://nvd.nist.gov/vuln/detail/cve-2026-0861){: external}, [CVE-2025-15281](https://nvd.nist.gov/vuln/detail/cve-2025-15281){: external}, and [CVE-2026-0915](https://nvd.nist.gov/vuln/detail/cve-2026-0915){: external}.
- `armada-storage-secret v1.2.77`


### 26 February 2026, Version 5.1 - v5.1.44_319682969
{: #cl-add-ons-vpc-block-csi-driver-v5144_319682969}

- Resolves the following CVEs: [CVE-2025-14104](https://nvd.nist.gov/vuln/detail/cve-2025-14104){: external}, [CVE-2025-47911](https://nvd.nist.gov/vuln/detail/cve-2025-47911){: external}, [CVE-2026-0915](https://nvd.nist.gov/vuln/detail/cve-2026-0915){: external}, [CVE-2025-68121](https://nvd.nist.gov/vuln/detail/cve-2025-68121){: external}, and [CVE-2025-58190](https://nvd.nist.gov/vuln/detail/cve-2025-58190){: external}.
- `armada-storage-secret v1.2.76`


### 10 February 2026, Version 5.1 - v5.1.43_316462421
{: #cl-add-ons-vpc-block-csi-driver-v5143_316462421}

- Resolves the following CVEs: [CVE-2025-15467](https://nvd.nist.gov/vuln/detail/cve-2025-15467){: external}, [CVE-2025-11187](https://nvd.nist.gov/vuln/detail/cve-2025-11187){: external}, [CVE-2025-15468](https://nvd.nist.gov/vuln/detail/cve-2025-15468){: external}, [CVE-2025-15469](https://nvd.nist.gov/vuln/detail/cve-2025-15469){: external}, [CVE-2025-66199](https://nvd.nist.gov/vuln/detail/cve-2025-66199){: external}, [CVE-2025-68160](https://nvd.nist.gov/vuln/detail/cve-2025-68160){: external}, [CVE-2025-69418](https://nvd.nist.gov/vuln/detail/cve-2025-69418){: external}, [CVE-2025-69419](https://nvd.nist.gov/vuln/detail/cve-2025-69419){: external}, [CVE-2025-69420](https://nvd.nist.gov/vuln/detail/cve-2025-69420){: external}, [CVE-2025-69421](https://nvd.nist.gov/vuln/detail/cve-2025-69421){: external}, [CVE-2026-22795](https://nvd.nist.gov/vuln/detail/cve-2026-22795){: external}, [CVE-2026-22796](https://nvd.nist.gov/vuln/detail/cve-2026-22796){: external}, and [CVE-2025-9086](https://nvd.nist.gov/vuln/detail/cve-2025-9086){: external}.
- `armada-storage-secret v1.2.75`


### 02 February 2026, Version 5.1 - v5.1.42_313460253
{: #cl-add-ons-vpc-block-csi-driver-v5142_313460253}

- Fixes xfs filesystem expansion failure during CSI volume resize operation 


### 21 January 2026, Version 5.1 - v5.1.41_310494703
{: #cl-add-ons-vpc-block-csi-driver-v5141_310494703}

- Resolves the following CVEs: [CVE-2025-61727](https://nvd.nist.gov/vuln/detail/cve-2025-61727){: external}, [CVE-2025-61729](https://nvd.nist.gov/vuln/detail/cve-2025-61729){: external}, [CVE-2025-4598](https://nvd.nist.gov/vuln/detail/cve-2025-4598){: external}, and [CVE-2025-13281](https://nvd.nist.gov/vuln/detail/cve-2025-13281){: external}.
- Updates K8s client libraries from 1.32.8 to 1.32.10 in iks-vpc-block-driver container 
- `armada-storage-secret v1.2.74`


### 12 November 2025, Version 5.1 - 5.1.40_296898008
{: #cl-add-ons-vpc-block-csi-driver-5140_296898008}

- Resolves the following CVEs: [CVE-2025-61725](https://nvd.nist.gov/vuln/detail/cve-2025-61725){: external}, [CVE-2025-61723](https://nvd.nist.gov/vuln/detail/cve-2025-61723){: external}, [CVE-2025-58189](https://nvd.nist.gov/vuln/detail/cve-2025-58189){: external}, and [CVE-2025-58185](https://nvd.nist.gov/vuln/detail/cve-2025-58185){: external}.
- Updates Go to version `1.25.3`.
- `armada-storage-secret v1.2.70`


### 05 November 2025, Version 5.1 - 5.1.39_293222093
{: #cl-add-ons-vpc-block-csi-driver-5139_293222093}

- Resolves the following CVEs: [CVE-2025-5187](https://nvd.nist.gov/vuln/detail/cve-2025-5187){: external}, [CVE-2025-8058](https://nvd.nist.gov/vuln/detail/cve-2025-8058){: external}, and [CVE-2025-47906](https://nvd.nist.gov/vuln/detail/cve-2025-47906){: external}.
- Updates Go to version `1.23.12`.
- Updates k8s package to 1.32.8 in iks-vpc-block-driver container 
- `armada-storage-secret v1.2.69`


### 14 July 2025, Version 5.1 - 5.1.37_827
{: #cl-add-ons-vpc-block-csi-driver-5137_827}

- Resolves the following CVEs: [CVE-2025-4563](https://nvd.nist.gov/vuln/detail/cve-2025-4563){: external}, [CVE-2025-4673](https://nvd.nist.gov/vuln/detail/cve-2025-4673){: external}, and [CVE-2020-8561](https://nvd.nist.gov/vuln/detail/cve-2020-8561){: external}.
- Updates Go to version `1.23.10`.
- Updates k8s package to 1.32.6 in iks-vpc-block-driver container 
- Updates imagePullPolicy to IfNotPresent for all containers in the deployment. 
- `armada-storage-secret v1.2.64`


### 30 May 2025, Version 5.1 - 5.1.35_763
{: #cl-add-ons-vpc-block-csi-driver-5135_763}

- Resolves the following CVEs: [CVE-2024-9042](https://nvd.nist.gov/vuln/detail/cve-2024-9042){: external}, [CVE-2025-0426](https://nvd.nist.gov/vuln/detail/cve-2025-0426){: external}, [CVE-2025-22872](https://nvd.nist.gov/vuln/detail/cve-2025-22872){: external}, and [CVE-2025-30204](https://nvd.nist.gov/vuln/detail/cve-2025-30204){: external}.
- Updates k8s package to 1.32.3 in iks-vpc-block-driver container 
- `armada-storage-secret v1.2.61`
- `csi-provisioner v5.2.0`
- `csi-resizer v1.13.2`
- `csi-snapshotter v8.2.1`
- `csi-attacher v4.8.1`
- `livenessprobe:v2.15.0`
- `csi-node-driver-registrar v2.13.0`


### 09 May 2025, Version 5.1 - 5.1.34_740
{: #cl-add-ons-vpc-block-csi-driver-5134_740}

- Resolves the following CVEs: [CVE-2020-11023](https://nvd.nist.gov/vuln/detail/cve-2020-11023){: external}, and [CVE-2025-0395](https://nvd.nist.gov/vuln/detail/cve-2025-0395){: external}.
- Updates the golang base image to 1.23.8. 
- Updates the armada-storage-secret to v1.2.60. 


### 17 February 2025, Version 5.1 - 5.1.33_685
{: #cl-add-ons-vpc-block-csi-driver-5133_685}

- Resolves the following CVEs: [CVE-2024-45339](https://nvd.nist.gov/vuln/detail/cve-2024-45339){: external}, and [CVE-2024-45338](https://nvd.nist.gov/vuln/detail/cve-2024-45338){: external}.
- Resiliency improvement to use VPC Storage service API for tagging volumes. This doesn't impact existing or new PVCs. This reduces the number of Kubernetes service API calls. 
- Updates the golang base image to 1.22.12. 
- Updates the armada-storage-secret to v1.2.55. 


### 11 December 2024, Version 5.1.31_656
{: #5.1.31_656_is_block_relnote}

- Resolves [CVE-2024-51744](https://nvd.nist.gov/vuln/detail/cve-2024-51744){: external}.


### 20 November 2024, Version 5.1.29_642
{: #5.1.29_642_is_block_relnote}

- Updates the golang base image to `1.22.9`.
- Introduces an `init` container to clean up any leftover controller pods from 5.2 release.


### 3 October 2024, Version 5.1.26_601
{: #5.1.26_601_is_block_relnote}

- Updates the golang base image to `1.22.7`.
- Updates to Kubernetes 1.30 client libraries.
- Updates the CSI specification to version `1.9.0`.
- Fixes a security issue for the CSI sidecar liveness probe. The sidecar now runs as non-root in the Node Server pod.
- Adds the ability to set a default storage class. For more information, see [Setting the default storage class](/docs/openshift?topic=openshift-storage-file-vpc-apps#vpc-file-set-default-sc).
- Updates the following sidecar images: `csi-provisioner:v5.0.2`, `csi-resizer:v1.11.2`, `csi-snapshotter:v8.0.1`, `csi-attacher:v4.6.1`, `livenessprobe:v2.13.1`, and `csi-node-driver-registrar:v2.11.1`
- Resolves [CVE-2024-2398](https://nvd.nist.gov/vuln/detail/cve-2024-2398){: external}, [CVE-2024-37370](https://nvd.nist.gov/vuln/detail/cve-2024-37370){: external}, [CVE-2024-37371](https://nvd.nist.gov/vuln/detail/cve-2024-37371){: external}.


### 15 July 2024, Version 5.1.25_574
{: #5.1.25_574_is_block_relnote}

- Updates the golang image to `1.21.12-community`.
- Updates the `armada-storage-secret` to `v1.2.40`.
- Resolves [CVE-2024-28182](https://nvd.nist.gov/vuln/detail/cve-2024-28182){: external} and [CVE-2023-2953](https://nvd.nist.gov/vuln/detail/cve-2023-2953){: external}.


### 21 June 2024, Version 5.1.24_567
{: #5.1.24_567_is_block_relnote}

- Updates `golang` to `1.21.11-community`.
- Updates the `armada-storage-secret` to `v1.3.8`.
- Resolves: [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/cve-2024-2961){: external}, [CVE-2024-33599](https://nvd.nist.gov/vuln/detail/cve-2024-33599){: external}, [CVE-2024-33600](https://nvd.nist.gov/vuln/detail/cve-2024-33600){: external}, [CVE-2024-33601](https://nvd.nist.gov/vuln/detail/cve-2024-33601){: external}, [CVE-2024-33602](https://nvd.nist.gov/vuln/detail/cve-2024-33602){: external}.


### 10 May 2024, Version 5.1.23_543
{: #5.1.23_543_is_block_relnote}

- Updates `golang` to `1.21.9-community`.
- Removes `curl` package from base image.
- Updates the `armada-storage-secret` to `v1.2.35`.
- Resolves [CVE-2023-46218](https://nvd.nist.gov/vuln/detail/cve-2023-46218){: external}, [CVE-2023-28322](https://nvd.nist.gov/vuln/detail/cve-2023-28322){: external}, and [CVE-2023-38546](https://nvd.nist.gov/vuln/detail/cve-2023-38546){: external}.


### 08 March 2024, Version 5.1.22_522
{: #5.1.22_522_is_block_relnote}

- Base image migrated from UBI to golang.


### 08 February 2024, Version 5.1.21_506
{: #5.1.21_506_is_block_relnote}

- Changes how the IAM endpoint is determined for VPC Gen2 clusters.
- Upgrades Kubernetes client library to 1.28.
- Upgrades CSI spec to 1.8.0.
- Resolves the following CVEs: [CVE-2022-48560](https://nvd.nist.gov/vuln/detail/cve-2022-48560){: external}, [CVE-2022-48564](https://nvd.nist.gov/vuln/detail/cve-2022-48564){: external}, [CVE-2023-39615](https://nvd.nist.gov/vuln/detail/cve-2023-39615){: external}, [CVE-2023-43804](https://nvd.nist.gov/vuln/detail/cve-2023-43804){: external}, [CVE-2023-45803](https://nvd.nist.gov/vuln/detail/cve-2023-45803){: external}, and [CVE-2023-5981](https://nvd.nist.gov/vuln/detail/cve-2023-5981){: external}.
- Updates the following sidecar images: 
    - `armada-storage-secret` to `v1.2.31`.
    - `csi-attacher` to `v4.4.3`.
    - `csi-node-driver-registrar` to `v2.9.3`.
    - `csi-provisioner` to `v3.6.3`.
    - `csi-resizer` to `v1.9.3`.
    - `csi-snapshotter` to `v6.3.3`.
    - `livenessprobe` to `v2.11.0`.


### 14 September 2023, Version 5.1.13_345
{: #5.1.13_345_is_block_relnote}

- Updated the UBI image to `8.8-860`.
- Updated the Golang updated to `1.19.12`.
- Resolves the following CVEs: [CVE-2023-34969](https://nvd.nist.gov/vuln/detail/cve-2023-34969){: external}, [CVE-2023-28321](https://nvd.nist.gov/vuln/detail/cve-2023-28321){: external}, [CVE-2023-2602](https://nvd.nist.gov/vuln/detail/cve-2023-2602){: external}, [CVE-2023-2603](https://nvd.nist.gov/vuln/detail/cve-2023-2603){: external}, [CVE-2023-28484](https://nvd.nist.gov/vuln/detail/cve-2023-28484){: external}, [CVE-2023-29469](https://nvd.nist.gov/vuln/detail/cve-2023-29469){: external}, [CVE-2023-27536](https://nvd.nist.gov/vuln/detail/cve-2023-27536){: external}, [CVE-2023-3899](https://nvd.nist.gov/vuln/detail/cve-2023-3899){: external}, and [CVE-2023-32681](https://nvd.nist.gov/vuln/detail/cve-2023-32681){: external}.


### 01 August 2023, Version 5.1.12_285
{: #5.1.12_285_is_block_relnote}

- Node affinity added for controller server and node server, so that pods do not crash on Z system (s390x) based clusters.
- Resolves the following CVEs: [CVE-2023-26604](https://nvd.nist.gov/vuln/detail/cve-2023-26604){: external}, [CVE-2020-24736](https://nvd.nist.gov/vuln/detail/cve-2020-24736){: external}, [CVE-2023-1667](https://nvd.nist.gov/vuln/detail/cve-2023-1667){: external}, and [CVE-2023-2283](https://nvd.nist.gov/vuln/detail/cve-2023-2283){: external}.


### 21 June 2023, Version 5.1.11_126
{: #5.1.11_126_is_block_relnote}

- Updates the following sidecar images: 
    - `storage-secret-sidecar` to `v1.2.24`.
    - `csi-node-driver-registrar` to `v2.7.0`.
    - `livenessprobe` to `v2.9.0`.
    - `csi-provisioner` to `v3.4.1`.
    - `csi-attacher` to `v4.2.0`.
    - `csi-resizer` to `v1.7.0`.
    - `csi-snapshotter` to `v6.2.1`.
- Updates the UBI image `8.8-860`.
- Updates Golang to `1.19.10`.
- Resolves the following CVEs: 
    - [CVE-2022-43552](https://nvd.nist.gov/vuln/detail/cve-2022-43552){: external}, [CVE-2022-3204](https://nvd.nist.gov/vuln/detail/cve-2022-3204){: external}, [CVE-2023-27535](https://nvd.nist.gov/vuln/detail/cve-2023-27535){: external},[CVE-2022-36227], [CVE-2022-35252](https://nvd.nist.gov/vuln/detail/cve-2022-35252){: external}, [CVE-2023-29403](https://nvd.nist.gov/vuln/detail/cve-2023-29403){: external}, [CVE-2023-29404](https://nvd.nist.gov/vuln/detail/cve-2023-29404){: external}, [CVE-2023-29405](https://nvd.nist.gov/vuln/detail/cve-2023-29405){: external}, [CVE-2023-29402](https://nvd.nist.gov/vuln/detail/cve-2023-29402){: external}, [CVE-2023-29400](https://nvd.nist.gov/vuln/detail/cve-2023-29400){: external}, [CVE-2023-24540](https://nvd.nist.gov/vuln/detail/cve-2023-24540){: external}, [CVE-2023-24539](https://nvd.nist.gov/vuln/detail/cve-2023-24539){: external}.
- Introduced two new configurable flags in `addon-vpc-block-csi-driver-configmap` configMap to enable/disable and edit the retry interval for Snapshot Creation.
    - `IsSnapshotEnabled` allows users to disable or enable snapshot functionality. By default, this parameter is set to `true`
    - `CustomSnapshotCreateDelay` allows users to edit the maximum delay (in seconds) for snapshot calls in case the source volume is not found and the volume is not attached. The maximum delay allowed is 15 minutes and the default is 5 minutes.


### 15 May 2023, Version 5.1.8_1970
{: #5.1.8_1970_is_block_relnote}

- Updates UBI image to `8.7-1107` 
- Updates Golang to `1.19.8`
- Users must determine token exchange URL based on cluster provider. For {{site.data.keyword.satelliteshort}} clusters, always use the provided token exchange URL. If the URL is not provided, use public IAM endpoint.
- Resolves the following CVEs: 
    - [CVE-2023-0361](https://nvd.nist.gov/vuln/detail/cve-2023-0361){: external}, [CVE-2023-24536](https://nvd.nist.gov/vuln/detail/cve-2023-24536){: external}, [CVE-2023-24537](https://nvd.nist.gov/vuln/detail/cve-2023-24537), [CVE-2023-24538](https://nvd.nist.gov/vuln/detail/cve-2023-24538){: external}


### 05 April 2023, Version 5.1.6_1872
{: #5.1.6_1872_is_block_relnote}

- Updates the storage-secret-sidecar image to `v1.2.20`.
- Updates Golang to `v1.19.7`.
- Updates the UBI image to `8.7-1085.1679482090`
- Resolves the following CVEs:
    - [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/cve-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/cve-2022-2250){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/cve-2023-0215){: external}, and [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/cve-2023-0286){: external}


### 29 March 2023, Version 5.1.5_1857
{: #5.1.5_1857_is_block_relnote}

- Updates the storage-secret-sidecar image to `v1.2.19`.
- Resolves [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/cve-2023-23916){: external}


### 07 March 2023, Version 5.1.4_1852
{: #5.1.4_1852_is_block_relnote}

- Upgrades Kubernetes packages to version `1.26`.
- Updates the storage-secret-sidecar image to `v1.2.18`.
- Resolves the following CVEs: [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/cve-2020-10735){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/cve-2021-28861){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/cve-2022-45061){: external}, [CVE-2022-4415](https://nvd.nist.gov/vuln/detail/cve-2022-4415){: external}, [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/cve-2022-40897){: external}.


### 21 February 2023, Version 5.1.2_1828
{: #5.1.2-1828_is_block_relnote}

- Resolves [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/cve-2022-47629){: external}.


### 9 February 2023, Version 5.1
{: #5.1_is_block_relnote}


- Updates the snapshot size to reflect actual source volume size.
- Improves the resize method when creating a volume from a snapshot.
- Updates the Kubernetes dependency to `1.25`.
- Adds support for configuring the log level for sidecars from the configmap.
- Makes the `ibmc-vpcblock-snapshot` class the default `Volumesnapshotclass`.
- Adds the `priorityClass` in the deployment file for controller and node pods.
- Updates the driver to read the node instance ID from the node spec provider ID instead of node labels.
- Fixes a bug in volume expansion for raw block volumes.
- Removes the `preStop` hook for the `csi-driver-registrar`. 


## Version 4.3
{: #043_is_block}
