---

copyright:
  years: 2024, 2026

lastupdated: "2026-02-10"


keywords: change log, version history, VPC Block CSI Driver

subcollection: "openshift"

---

{{site.data.keyword.attribute-definition-list}}




# VPC Block CSI Driver add-on version change log
{: #cl-add-ons-vpc-block-csi-driver}

Review the version history for VPC Block CSI Driver.
{: shortdesc}


## Version 5.2
{: #cl-add-ons-vpc-block-csi-driver-5.2}


### v5.2.44_316463149, released 10 February 2026
{: #cl-add-ons-vpc-block-csi-driver-v5244_316463149}

- Resolves the following CVEs: [CVE-2025-15467](https://nvd.nist.gov/vuln/detail/CVE-2025-15467){: external}, [CVE-2025-11187](https://nvd.nist.gov/vuln/detail/CVE-2025-11187){: external}, [CVE-2025-15468](https://nvd.nist.gov/vuln/detail/CVE-2025-15468){: external}, [CVE-2025-15469](https://nvd.nist.gov/vuln/detail/CVE-2025-15469){: external}, [CVE-2025-66199](https://nvd.nist.gov/vuln/detail/CVE-2025-66199){: external}, [CVE-2025-68160](https://nvd.nist.gov/vuln/detail/CVE-2025-68160){: external}, [CVE-2025-69418](https://nvd.nist.gov/vuln/detail/CVE-2025-69418){: external}, [CVE-2025-69419](https://nvd.nist.gov/vuln/detail/CVE-2025-69419){: external}, [CVE-2025-69420](https://nvd.nist.gov/vuln/detail/CVE-2025-69420){: external}, [CVE-2025-69421](https://nvd.nist.gov/vuln/detail/CVE-2025-69421){: external}, [CVE-2026-22795](https://nvd.nist.gov/vuln/detail/CVE-2026-22795){: external}, [CVE-2026-22796](https://nvd.nist.gov/vuln/detail/CVE-2026-22796){: external}, [CVE-2025-9086](https://nvd.nist.gov/vuln/detail/CVE-2025-9086){: external}, [CVE-2025-61726](https://nvd.nist.gov/vuln/detail/CVE-2025-61726){: external}, and [CVE-2025-61730](https://nvd.nist.gov/vuln/detail/CVE-2025-61730){: external}.
- `armada-storage-secret v1.3.40`


### v5.2.42_310488886, released 21 January 2026
{: #cl-add-ons-vpc-block-csi-driver-v5242_310488886}

- Resolves the following CVEs: [CVE-2025-61727](https://nvd.nist.gov/vuln/detail/CVE-2025-61727){: external}, [CVE-2025-61729](https://nvd.nist.gov/vuln/detail/CVE-2025-61729){: external}, [CVE-2025-4598](https://nvd.nist.gov/vuln/detail/CVE-2025-4598){: external}, and [CVE-2025-13281](https://nvd.nist.gov/vuln/detail/CVE-2025-13281){: external}.
- Updates K8s client libraries from 1.32.8 to 1.32.10 in iks-vpc-block-driver container 
- `armada-storage-secret v1.3.39`


### 5.2.41_296897820, released 12 November 2025
{: #cl-add-ons-vpc-block-csi-driver-5241_296897820}

- Resolves the following CVEs: [CVE-2025-61725](https://nvd.nist.gov/vuln/detail/CVE-2025-61725){: external}, [CVE-2025-61723](https://nvd.nist.gov/vuln/detail/CVE-2025-61723){: external}, [CVE-2025-58189](https://nvd.nist.gov/vuln/detail/CVE-2025-58189){: external}, and [CVE-2025-58185](https://nvd.nist.gov/vuln/detail/CVE-2025-58185){: external}.
- Updates Go to version `1.25.3`.
- `armada-storage-secret v1.3.36`


### 5.2.40_293222012, released 05 November 2025
{: #cl-add-ons-vpc-block-csi-driver-5240_293222012}

- Resolves the following CVEs: [CVE-2025-5187](https://nvd.nist.gov/vuln/detail/CVE-2025-5187){: external}, [CVE-2025-8058](https://nvd.nist.gov/vuln/detail/CVE-2025-8058){: external}, and [CVE-2025-47906](https://nvd.nist.gov/vuln/detail/CVE-2025-47906){: external}.
- Updates Go to version `1.23.12`.
- Updates k8s package to 1.32.8 in iks-vpc-block-driver container 
- `armada-storage-secret v1.3.35`


### 5.2.38_828, released 14 July 2025
{: #cl-add-ons-vpc-block-csi-driver-5238_828}

- Resolves the following CVEs: [CVE-2025-4563](https://nvd.nist.gov/vuln/detail/CVE-2025-4563){: external}, [CVE-2025-4673](https://nvd.nist.gov/vuln/detail/CVE-2025-4673){: external}, and [CVE-2020-8561](https://nvd.nist.gov/vuln/detail/CVE-2020-8561){: external}.
- Updates Go to version `1.23.10`.
- Updates k8s package to 1.32.6 in iks-vpc-block-driver container 
- Updates imagePullPolicy to IfNotPresent for all containers in the deployment. 
- `armada-storage-secret v1.3.30`


### 5.2.36_778, released 30 May 2025
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


### 5.2.33_735, released 09 May 2025
{: #cl-add-ons-vpc-block-csi-driver-5233_735}

- Resolves the following CVEs: [CVE-2020-11023](https://nvd.nist.gov/vuln/detail/CVE-2020-11023){: external}, and [CVE-2025-0395](https://nvd.nist.gov/vuln/detail/CVE-2025-0395){: external}.
- Updates the golang base image to 1.23.8. 
- Updates the armada-storage-secret to v1.3.26. 


### 5.2.31_687, released 17 February 2025
{: #cl-add-ons-vpc-block-csi-driver-5231_687}

- Resolves the following CVEs: [CVE-2024-45339](https://nvd.nist.gov/vuln/detail/CVE-2024-45339){: external}, and [CVE-2024-45338](https://nvd.nist.gov/vuln/detail/CVE-2024-45338){: external}.
- Resiliency improvement to use VPC Storage service API for tagging volumes. This doesn't impact existing or new PVCs. This reduces the number of Kubernetes service API calls. 
- Updates the golang base image to 1.22.12. 
- Updates the armada-storage-secret to v1.3.22. 


## Version 5.1
{: #cl-add-ons-vpc-block-csi-driver-5.1}


### v5.1.43_316462421, released 10 February 2026
{: #cl-add-ons-vpc-block-csi-driver-v5143_316462421}

- Resolves the following CVEs: [CVE-2025-15467](https://nvd.nist.gov/vuln/detail/CVE-2025-15467){: external}, [CVE-2025-11187](https://nvd.nist.gov/vuln/detail/CVE-2025-11187){: external}, [CVE-2025-15468](https://nvd.nist.gov/vuln/detail/CVE-2025-15468){: external}, [CVE-2025-15469](https://nvd.nist.gov/vuln/detail/CVE-2025-15469){: external}, [CVE-2025-66199](https://nvd.nist.gov/vuln/detail/CVE-2025-66199){: external}, [CVE-2025-68160](https://nvd.nist.gov/vuln/detail/CVE-2025-68160){: external}, [CVE-2025-69418](https://nvd.nist.gov/vuln/detail/CVE-2025-69418){: external}, [CVE-2025-69419](https://nvd.nist.gov/vuln/detail/CVE-2025-69419){: external}, [CVE-2025-69420](https://nvd.nist.gov/vuln/detail/CVE-2025-69420){: external}, [CVE-2025-69421](https://nvd.nist.gov/vuln/detail/CVE-2025-69421){: external}, [CVE-2026-22795](https://nvd.nist.gov/vuln/detail/CVE-2026-22795){: external}, [CVE-2026-22796](https://nvd.nist.gov/vuln/detail/CVE-2026-22796){: external}, and [CVE-2025-9086](https://nvd.nist.gov/vuln/detail/CVE-2025-9086){: external}.
- `armada-storage-secret v1.2.75`


### v5.1.41_310494703, released 21 January 2026
{: #cl-add-ons-vpc-block-csi-driver-v5141_310494703}

- Resolves the following CVEs: [CVE-2025-61727](https://nvd.nist.gov/vuln/detail/CVE-2025-61727){: external}, [CVE-2025-61729](https://nvd.nist.gov/vuln/detail/CVE-2025-61729){: external}, [CVE-2025-4598](https://nvd.nist.gov/vuln/detail/CVE-2025-4598){: external}, and [CVE-2025-13281](https://nvd.nist.gov/vuln/detail/CVE-2025-13281){: external}.
- Updates K8s client libraries from 1.32.8 to 1.32.10 in iks-vpc-block-driver container 
- `armada-storage-secret v1.2.74`


### 5.1.40_296898008, released 12 November 2025
{: #cl-add-ons-vpc-block-csi-driver-5140_296898008}

- Resolves the following CVEs: [CVE-2025-61725](https://nvd.nist.gov/vuln/detail/CVE-2025-61725){: external}, [CVE-2025-61723](https://nvd.nist.gov/vuln/detail/CVE-2025-61723){: external}, [CVE-2025-58189](https://nvd.nist.gov/vuln/detail/CVE-2025-58189){: external}, and [CVE-2025-58185](https://nvd.nist.gov/vuln/detail/CVE-2025-58185){: external}.
- Updates Go to version `1.25.3`.
- `armada-storage-secret v1.2.70`


### 5.1.39_293222093, released 05 November 2025
{: #cl-add-ons-vpc-block-csi-driver-5139_293222093}

- Resolves the following CVEs: [CVE-2025-5187](https://nvd.nist.gov/vuln/detail/CVE-2025-5187){: external}, [CVE-2025-8058](https://nvd.nist.gov/vuln/detail/CVE-2025-8058){: external}, and [CVE-2025-47906](https://nvd.nist.gov/vuln/detail/CVE-2025-47906){: external}.
- Updates Go to version `1.23.12`.
- Updates k8s package to 1.32.8 in iks-vpc-block-driver container 
- `armada-storage-secret v1.2.69`


### 5.1.37_827, released 14 July 2025
{: #cl-add-ons-vpc-block-csi-driver-5137_827}

[Default version]{: tag-green}

- Resolves the following CVEs: [CVE-2025-4563](https://nvd.nist.gov/vuln/detail/CVE-2025-4563){: external}, [CVE-2025-4673](https://nvd.nist.gov/vuln/detail/CVE-2025-4673){: external}, and [CVE-2020-8561](https://nvd.nist.gov/vuln/detail/CVE-2020-8561){: external}.
- Updates Go to version `1.23.10`.
- Updates k8s package to 1.32.6 in iks-vpc-block-driver container 
- Updates imagePullPolicy to IfNotPresent for all containers in the deployment. 
- `armada-storage-secret v1.2.64`


### 5.1.35_763, released 30 May 2025
{: #cl-add-ons-vpc-block-csi-driver-5135_763}

[Default version]{: tag-green}

- Resolves the following CVEs: [CVE-2024-9042](https://nvd.nist.gov/vuln/detail/CVE-2024-9042){: external}, [CVE-2025-0426](https://nvd.nist.gov/vuln/detail/CVE-2025-0426){: external}, [CVE-2025-22872](https://nvd.nist.gov/vuln/detail/CVE-2025-22872){: external}, and [CVE-2025-30204](https://nvd.nist.gov/vuln/detail/CVE-2025-30204){: external}.
- Updates k8s package to 1.32.3 in iks-vpc-block-driver container 
- `armada-storage-secret v1.2.61`
- `csi-provisioner v5.2.0`
- `csi-resizer v1.13.2`
- `csi-snapshotter v8.2.1`
- `csi-attacher v4.8.1`
- `livenessprobe:v2.15.0`
- `csi-node-driver-registrar v2.13.0`


### 5.1.34_740, released 09 May 2025
{: #cl-add-ons-vpc-block-csi-driver-5134_740}

- Resolves the following CVEs: [CVE-2020-11023](https://nvd.nist.gov/vuln/detail/CVE-2020-11023){: external}, and [CVE-2025-0395](https://nvd.nist.gov/vuln/detail/CVE-2025-0395){: external}.
- Updates the golang base image to 1.23.8. 
- Updates the armada-storage-secret to v1.2.60. 


### 5.1.33_685, released 17 February 2025
{: #cl-add-ons-vpc-block-csi-driver-5133_685}

- Resolves the following CVEs: [CVE-2024-45339](https://nvd.nist.gov/vuln/detail/CVE-2024-45339){: external}, and [CVE-2024-45338](https://nvd.nist.gov/vuln/detail/CVE-2024-45338){: external}.
- Resiliency improvement to use VPC Storage service API for tagging volumes. This doesn't impact existing or new PVCs. This reduces the number of Kubernetes service API calls. 
- Updates the golang base image to 1.22.12. 
- Updates the armada-storage-secret to v1.2.55. 


## Version 5.2 archive
{: #052_is_block_archive}


### Change log for version 5.2.26_657, released 11 December 2024
{: #5.2.26_657_is_block_relnote}

- Resolves [CVE-2024-51744](https://nvd.nist.gov/vuln/detail/CVE-2024-51744){: external}.
- Increases custom volume profile support to a maximum of 16TB.
- Removes IOPS and capacity validation for custom volume profile from CSI Driver. Now VPC IaaS performs validation and shows the following generic error in case of wrong user input: `The volume profile specified in the request is not valid for the provided capacity or IOPS`. Existing VPCs are not impacted.

### Change log for version 5.2.24_641, released 20 November 2024
{: #5.2.24_641_is_block_relnote}

- Updates the golang base image to `1.22.9`.
- Introduces an `init` container to clean up any leftover controller pods from the 5.1 release.



### Change log for version 5.2.21_602, released 3 October 2024
{: #5.2.21_602_is_block_relnote}

- Adds support for cross-account snapshot restoration.
- Updates the golang base image to `1.22.7`.
- Updates to Kubernetes 1.30 client libraries.
- Updates the CSI specification to version `1.9.0`.
- Fixes a security issue for the CSI sidecar liveness probe. The sidecar now runs as non-root in the Node Server pod.
- Adds the ability to set a default storage class. For more information, see [Setting the default storage class](/docs/openshift?topic=openshift-storage-file-vpc-apps#vpc-file-set-default-sc).
- Updates the following sidecar images: `csi-provisioner:v5.0.2`, `csi-resizer:v1.11.2`, `csi-snapshotter:v8.0.1`, `csi-attacher:v4.6.1`, `livenessprobe:v2.13.1`, and `csi-node-driver-registrar:v2.11.1`
- Resolves [CVE-2024-2398](https://nvd.nist.gov/vuln/detail/CVE-2024-2398){: external}, [CVE-2024-37370](https://nvd.nist.gov/vuln/detail/CVE-2024-37370){: external}, [CVE-2024-37371](https://nvd.nist.gov/vuln/detail/CVE-2024-37371){: external}.

### Change log for version 5.2.20_579, released 15 July 2024
{: #5.2.20_579_is_block_relnote}

- Updates the golang image to `1.21.12-community`.
- Updates the `armada-storage-secret` to `v1.3.10`.
- Resolves [CVE-2024-28182](https://nvd.nist.gov/vuln/detail/CVE-2024-28182){: external} and [CVE-2023-2953](https://nvd.nist.gov/vuln/detail/CVE-2023-2953){: external}.

### Change log for version 5.2.19_570, released 21 June 2024
{: #5.2.19_570_is_block_relnote}


- Updates `golang` to `1.21.11-community`.
- Updates the `armada-storage-secret` to `v1.3.9`.
- Resolves: [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961){: external}, [CVE-2024-33599](https://nvd.nist.gov/vuln/detail/CVE-2024-33599){: external}, [CVE-2024-33600](https://nvd.nist.gov/vuln/detail/CVE-2024-33600){: external}, [CVE-2024-33601](https://nvd.nist.gov/vuln/detail/CVE-2024-33601){: external}, [CVE-2024-33602](https://nvd.nist.gov/vuln/detail/CVE-2024-33602){: external}.

### Change log for version 5.2.18_539, released 10 May 2024
{: #5.2.18_539_is_block_relnote}


- Updates `golang` to `1.21.9-community`.
- Removes `curl` package from base image.
- Updates the `armada-storage-secret` to `v1.3.7`.
- Resolves [CVE-2023-46218](https://nvd.nist.gov/vuln/detail/CVE-2023-46218){: external}, [CVE-2023-28322](https://nvd.nist.gov/vuln/detail/CVE-2023-28322){: external}, and [CVE-2023-38546](https://nvd.nist.gov/vuln/detail/CVE-2023-38546){: external}.


### Change log for 5.2.17_535, released 08 March 2024
{: #5.2.17_535_is_block_relnote}

- Base image migrated from UBI to golang.


### Change log for version 5.2.15_501, released 08 February 2024
{: #5.2.15_501_is_block_relnote}

- Changes how the IAM endpoint is determined for VPC Gen2 clusters.
- Upgrades Kubernetes client library to 1.28.
- Upgrades CSI spec to 1.8.0.
- Resolves the following CVEs: [CVE-2022-48560](https://nvd.nist.gov/vuln/detail/CVE-2022-48560){: external}, [CVE-2022-48564](https://nvd.nist.gov/vuln/detail/CVE-2022-48564){: external}, [CVE-2023-39615](https://nvd.nist.gov/vuln/detail/CVE-2023-39615){: external}, [CVE-2023-43804](https://nvd.nist.gov/vuln/detail/CVE-2023-43804){: external}, [CVE-2023-45803](https://nvd.nist.gov/vuln/detail/CVE-2023-45803){: external}, and [CVE-2023-5981](https://nvd.nist.gov/vuln/detail/CVE-2023-5981){: external}.
- Updates the following sidecar images: 
    - `armada-storage-secret` to `v1.3.5`.
    - `csi-attacher` to `v4.4.3`.
    - `csi-node-driver-registrar` to `v2.9.3`.
    - `csi-provisioner` to `v3.6.3`.
    - `csi-resizer` to `v1.9.3`.
    - `csi-snapshotter` to `v6.3.3`.
    - `livenessprobe` to `v2.11.0`.


### Change log for version 5.2.14_485, released 10 January 2024
{: #5.2.14_485_is_block_relnote}

- Resolves [CVE-2023-3446](https://nvd.nist.gov/vuln/detail/CVE-2023-3446){: external}, [CVE-2023-3817](https://nvd.nist.gov/vuln/detail/CVE-2023-3817){: external}, and [CVE-2023-5678](https://nvd.nist.gov/vuln/detail/CVE-2023-5678){: external}.
- Applies a security fix to use the correct socket path following SElinux policy module changes and CSI recommendations to use `/var/lib/kubelet/plugins/`.

### Change log for version 5.2.11_447, released 27 November 2023
{: #5.2.11_447_is_block_relnote}

- Updates Golang to `1.20.11`.
- Updates the UBI image to `8.9.1029`.
- Updates `armada-storage-secret` to `v1.3.3`.
- Resolves the following CVEs: [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/CVE-2023-22745){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [CVE-2023-40217](https://nvd.nist.gov/vuln/detail/CVE-2023-40217){: external}, and [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/CVE-2023-4641){: external}.

### Change log for version 5.2.10_428, released 13 November 2023
{: #5.2.10_428_is_block_relnote}

- Updates Golang `1.20.10`. 
- Updates the `storage-secret-sidecar` image to `1.3.2`.
- The add-on tries to reach the IAM endpoint/token exchange URL for 5 minutes, in case of timeout.
- Resolves the following CVEs: [CVE-2023-44487](https://nvd.nist.gov/vuln/detail/CVE-2023-44487){: external}, [CVE-2023-4911](https://nvd.nist.gov/vuln/detail/CVE-2023-4911){: external}, [CVE-2023-4527](https://nvd.nist.gov/vuln/detail/CVE-2023-4527){: external}, [CVE-2023-4806](https://nvd.nist.gov/vuln/detail/CVE-2023-4806){: external}, [CVE-2023-4813](https://nvd.nist.gov/vuln/detail/CVE-2023-4813){: external}, and [CVE-2023-39325](https://nvd.nist.gov/vuln/detail/CVE-2023-39325){: external}.


### Change log for version 5.2, released 25 September 2023
{: #5.2_is_block_relnote}


- Adds support for Z system. Multi-architecture images are supported on both `s390x` and `amd64` based clusters.
- Adds a new configurable flag `VolumeAttachmentLimit` in `addon-vpc-block-csi-driver-configmap` configMap that allows users to edit the maximum number of volumes that can be attached per node. The default value is set to `12`.
- Deploys controller pods as `Deployments`. Previous releases were deployed as `Satefulsets`.
- Resolves an issue where logs showed incorrect completion duration of some CSI operations.
- Pulls sidecars from `registry.k8s.io`.
- Adds support for 2 volume snapshot classes with delete and retain policies.
- Updates `k8s` package from `1.26.1` to `1.26.6`.



## Version 5.1 archive
{: #051_is_block_archive}

### Change log for version 5.1.31_656, released 11 December 2024
{: #5.1.31_656_is_block_relnote}

- Resolves [CVE-2024-51744](https://nvd.nist.gov/vuln/detail/CVE-2024-51744){: external}.

### Change log for version 5.1.29_642, released 20 November 2024
{: #5.1.29_642_is_block_relnote}

- Updates the golang base image to `1.22.9`.
- Introduces an `init` container to clean up any leftover controller pods from 5.2 release.


### Change log for version 5.1.26_601, released 3 October 2024
{: #5.1.26_601_is_block_relnote}

- Updates the golang base image to `1.22.7`.
- Updates to Kubernetes 1.30 client libraries.
- Updates the CSI specification to version `1.9.0`.
- Fixes a security issue for the CSI sidecar liveness probe. The sidecar now runs as non-root in the Node Server pod.
- Adds the ability to set a default storage class. For more information, see [Setting the default storage class](/docs/openshift?topic=openshift-storage-file-vpc-apps#vpc-file-set-default-sc).
- Updates the following sidecar images: `csi-provisioner:v5.0.2`, `csi-resizer:v1.11.2`, `csi-snapshotter:v8.0.1`, `csi-attacher:v4.6.1`, `livenessprobe:v2.13.1`, and `csi-node-driver-registrar:v2.11.1`
- Resolves [CVE-2024-2398](https://nvd.nist.gov/vuln/detail/CVE-2024-2398){: external}, [CVE-2024-37370](https://nvd.nist.gov/vuln/detail/CVE-2024-37370){: external}, [CVE-2024-37371](https://nvd.nist.gov/vuln/detail/CVE-2024-37371){: external}.

### Change log for version 5.1.25_574, released 15 July 2024
{: #5.1.25_574_is_block_relnote}

- Updates the golang image to `1.21.12-community`.
- Updates the `armada-storage-secret` to `v1.2.40`.
- Resolves [CVE-2024-28182](https://nvd.nist.gov/vuln/detail/CVE-2024-28182){: external} and [CVE-2023-2953](https://nvd.nist.gov/vuln/detail/CVE-2023-2953){: external}.

### Change log for version 5.1.24_567, released 21 June 2024
{: #5.1.24_567_is_block_relnote}

- Updates `golang` to `1.21.11-community`.
- Updates the `armada-storage-secret` to `v1.3.8`.
- Resolves: [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961){: external}, [CVE-2024-33599](https://nvd.nist.gov/vuln/detail/CVE-2024-33599){: external}, [CVE-2024-33600](https://nvd.nist.gov/vuln/detail/CVE-2024-33600){: external}, [CVE-2024-33601](https://nvd.nist.gov/vuln/detail/CVE-2024-33601){: external}, [CVE-2024-33602](https://nvd.nist.gov/vuln/detail/CVE-2024-33602){: external}.

### Change log for version 5.1.23_543, released 10 May 2024
{: #5.1.23_543_is_block_relnote}

- Updates `golang` to `1.21.9-community`.
- Removes `curl` package from base image.
- Updates the `armada-storage-secret` to `v1.2.35`.
- Resolves [CVE-2023-46218](https://nvd.nist.gov/vuln/detail/CVE-2023-46218){: external}, [CVE-2023-28322](https://nvd.nist.gov/vuln/detail/CVE-2023-28322){: external}, and [CVE-2023-38546](https://nvd.nist.gov/vuln/detail/CVE-2023-38546){: external}.

### Change log for 5.1.22_522, released 08 March 2024
{: #5.1.22_522_is_block_relnote}

- Base image migrated from UBI to golang.

### Change log for version 5.1.21_506, released 08 February 2024
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


### Change log for version 5.1.19_486, released 10 January 2024
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

### Change log for version 5.1.13_345, released 14 September 2023
{: #5.1.13_345_is_block_relnote}

- Updated the UBI image to `8.8-860`.
- Updated the Golang updated to `1.19.12`.
- Resolves the following CVEs: [CVE-2023-34969](https://nvd.nist.gov/vuln/detail/CVE-2023-34969){: external}, [CVE-2023-28321](https://nvd.nist.gov/vuln/detail/CVE-2023-28321){: external}, [CVE-2023-2602](https://nvd.nist.gov/vuln/detail/CVE-2023-2602){: external}, [CVE-2023-2603](https://nvd.nist.gov/vuln/detail/CVE-2023-2603){: external}, [CVE-2023-28484](https://nvd.nist.gov/vuln/detail/CVE-2023-28484){: external}, [CVE-2023-29469](https://nvd.nist.gov/vuln/detail/CVE-2023-29469){: external}, [CVE-2023-27536](https://nvd.nist.gov/vuln/detail/CVE-2023-27536){: external}, [CVE-2023-3899](https://nvd.nist.gov/vuln/detail/CVE-2023-3899){: external}, and [CVE-2023-32681](https://nvd.nist.gov/vuln/detail/CVE-2023-32681){: external}.

### Change log for version 5.1.12_285, released 01 August 2023
{: #5.1.12_285_is_block_relnote}

- Node affinity added for controller server and node server, so that pods do not crash on Z system (s390x) based clusters.
- Resolves the following CVEs: [CVE-2023-26604](https://nvd.nist.gov/vuln/detail/CVE-2023-26604){: external}, [CVE-2020-24736](https://nvd.nist.gov/vuln/detail/CVE-2020-24736){: external}, [CVE-2023-1667](https://nvd.nist.gov/vuln/detail/CVE-2023-1667){: external}, and [CVE-2023-2283](https://nvd.nist.gov/vuln/detail/CVE-2023-2283){: external}.

### Change log for version 5.1.11_126, released 21 June 2023
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
    - [CVE-2022-43552](https://nvd.nist.gov/vuln/detail/CVE-2022-43552){: external}, [CVE-2022-3204](https://nvd.nist.gov/vuln/detail/CVE-2022-3204){: external}, [CVE-2023-27535](https://nvd.nist.gov/vuln/detail/CVE-2023-27535){: external},[CVE-2022-36227], [CVE-2022-35252](https://nvd.nist.gov/vuln/detail/CVE-2022-35252){: external}, [CVE-2023-29403](https://nvd.nist.gov/vuln/detail/CVE-2023-29403){: external}, [CVE-2023-29404](https://nvd.nist.gov/vuln/detail/CVE-2023-29404){: external}, [CVE-2023-29405](https://nvd.nist.gov/vuln/detail/CVE-2023-29405){: external}, [CVE-2023-29402](https://nvd.nist.gov/vuln/detail/CVE-2023-29402){: external}, [CVE-2023-29400](https://nvd.nist.gov/vuln/detail/CVE-2023-29400){: external}, [CVE-2023-24540](https://nvd.nist.gov/vuln/detail/CVE-2023-24540){: external}, [CVE-2023-24539](https://nvd.nist.gov/vuln/detail/CVE-2023-24539){: external}.
- Introduced two new configurable flags in `addon-vpc-block-csi-driver-configmap` configMap to enable/disable and edit the retry interval for Snapshot Creation.
    - `IsSnapshotEnabled` allows users to disable or enable snapshot functionality. By default, this parameter is set to `true`
    - `CustomSnapshotCreateDelay` allows users to edit the maximum delay (in seconds) for snapshot calls in case the source volume is not found and the volume is not attached. The maximum delay allowed is 15 minutes and the default is 5 minutes.

### Change log for version 5.1.8_1970, released 15 May 2023
{: #5.1.8_1970_is_block_relnote}

- Updates UBI image to `8.7-1107` 
- Updates Golang to `1.19.8`
- Users must determine token exchange URL based on cluster provider. For {{site.data.keyword.satelliteshort}} clusters, always use the provided token exchange URL. If the URL is not provided, use public IAM endpoint.
- Resolves the following CVEs: 
    - [CVE-2023-0361](https://nvd.nist.gov/vuln/detail/CVE-2023-0361){: external}, [CVE-2023-24536](https://nvd.nist.gov/vuln/detail/CVE-2023-24536){: external}, [CVE-2023-24537](https://nvd.nist.gov/vuln/detail/CVE-2023-24537), [CVE-2023-24538](https://nvd.nist.gov/vuln/detail/CVE-2023-24538){: external}


### Change log for version 5.1.6_1872, released 05 April 2023
{: #5.1.6_1872_is_block_relnote}

- Updates the storage-secret-sidecar image to `v1.2.20`.
- Updates Golang to `v1.19.7`.
- Updates the UBI image to `8.7-1085.1679482090`
- Resolves the following CVEs:
    - [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-2250){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}, and [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}

### Change log for version 5.1.5_1857, released 29 March 2023
{: #5.1.5_1857_is_block_relnote}

- Updates the storage-secret-sidecar image to `v1.2.19`.
- Resolves [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}

### Change log for version 5.1.4_1852, released 07 March 2023
{: #5.1.4_1852_is_block_relnote}

- Upgrades Kubernetes packages to version `1.26`.
- Updates the storage-secret-sidecar image to `v1.2.18`.
- Resolves the following CVEs: [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}, [CVE-2022-4415](https://nvd.nist.gov/vuln/detail/CVE-2022-4415){: external}, [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/CVE-2022-40897){: external}.

### Change log for version 5.1.2_1828, released 21 February 2023
{: #5.1.2-1828_is_block_relnote}

- Resolves [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}.

### Change log for version 5.1, released 9 February 2023
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

## Version 5.0 archive
{: #050_is_block_archive}

### Change log for version 5.0.23_437, released 27 November 2023
{: #5.0.23_437_is_block_relnote}

- Updates Golang to `1.20.11`.
- Updates the UBI image to `8.9.1029`.
- Updates `armada-storage-secret` to `v1.2.29`.
- Resolves the following CVEs: [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/CVE-2023-22745){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [CVE-2023-40217](https://nvd.nist.gov/vuln/detail/CVE-2023-40217){: external}, and [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/CVE-2023-4641){: external}.

### Change log for version 5.0.21_401, released 13 November 2023
{: #5.0.21_401_is_block_relnote}

- Updates Golang to `1.20.10`. 
- Updates the `storage-secret-sidecar` image to `1.2.28`.
- Resolves the following CVEs: [CVE-2023-44487](https://nvd.nist.gov/vuln/detail/CVE-2023-44487){: external}, [CVE-2023-4911](https://nvd.nist.gov/vuln/detail/CVE-2023-4911){: external}, [CVE-2023-4527](https://nvd.nist.gov/vuln/detail/CVE-2023-4527){: external}, [CVE-2023-4806](https://nvd.nist.gov/vuln/detail/CVE-2023-4806){: external}, [CVE-2023-4813](https://nvd.nist.gov/vuln/detail/CVE-2023-4813){: external}, and [CVE-2023-39325](https://nvd.nist.gov/vuln/detail/CVE-2023-39325){: external}.

### Change log for version 5.0.19_358, released 14 September 2023
{: #5.0.19_358_is_block_relnote}

- Updated the UBI image to `8.8-860`.
- Updated the Golang updated to `1.19.12`.
- Resolves the following CVEs: [CVE-2023-34969](https://nvd.nist.gov/vuln/detail/CVE-2023-34969){: external}, [CVE-2023-28321](https://nvd.nist.gov/vuln/detail/CVE-2023-28321){: external}, [CVE-2023-2602](https://nvd.nist.gov/vuln/detail/CVE-2023-2602){: external}, [CVE-2023-2603](https://nvd.nist.gov/vuln/detail/CVE-2023-2603){: external}, [CVE-2023-28484](https://nvd.nist.gov/vuln/detail/CVE-2023-28484){: external}, [CVE-2023-29469](https://nvd.nist.gov/vuln/detail/CVE-2023-29469){: external}, [CVE-2023-27536](https://nvd.nist.gov/vuln/detail/CVE-2023-27536){: external}, [CVE-2023-3899](https://nvd.nist.gov/vuln/detail/CVE-2023-3899){: external}, and [CVE-2023-32681](https://nvd.nist.gov/vuln/detail/CVE-2023-32681){: external}.

### Change log for version 5.0.17_266, released 01 August 2023
{: #5.0.17_266_is_block_relnote}

- Node affinity added for controller server and node server, so that pods do not crash on Z system (s390x) based clusters.
- Resolves the following CVEs: [CVE-2023-26604](https://nvd.nist.gov/vuln/detail/CVE-2023-26604){: external}, [CVE-2020-24736](https://nvd.nist.gov/vuln/detail/CVE-2020-24736){: external}, [CVE-2023-1667](https://nvd.nist.gov/vuln/detail/CVE-2023-1667){: external}, and [CVE-2023-2283](https://nvd.nist.gov/vuln/detail/CVE-2023-2283){: external}.


### Change log for version 5.0.16_127, released 21 June 2023
{: #5.0.16_127_is_block_relnote}

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
- Resolves the following CVEs: [CVE-2022-43552](https://nvd.nist.gov/vuln/detail/CVE-2022-43552){: external}, [CVE-2022-3204](https://nvd.nist.gov/vuln/detail/CVE-2022-3204){: external}, [CVE-2023-27535](https://nvd.nist.gov/vuln/detail/CVE-2023-27535){: external},[CVE-2022-36227], [CVE-2022-35252](https://nvd.nist.gov/vuln/detail/CVE-2022-35252){: external}, [CVE-2023-29403](https://nvd.nist.gov/vuln/detail/CVE-2023-29403){: external}, [CVE-2023-29404](https://nvd.nist.gov/vuln/detail/CVE-2023-29404){: external}, [CVE-2023-29405](https://nvd.nist.gov/vuln/detail/CVE-2023-29405){: external}, [CVE-2023-29402](https://nvd.nist.gov/vuln/detail/CVE-2023-29402){: external}, [CVE-2023-29400](https://nvd.nist.gov/vuln/detail/CVE-2023-29400){: external}, [CVE-2023-24540](https://nvd.nist.gov/vuln/detail/CVE-2023-24540){: external}, [CVE-2023-24539](https://nvd.nist.gov/vuln/detail/CVE-2023-24539){: external}.
- Introduced two new configurable flags in `addon-vpc-block-csi-driver-configmap` configMap to enable/disable and edit the retry interval for Snapshot Creation.
    - `IsSnapshotEnabled` allows users to disable or enable snapshot functionality. By default, this parameter is set to `true`
    - `CustomSnapshotCreateDelay` allows users to edit the maximum delay (in seconds) for snapshot calls in case the source volume is not found and the volume is not attached. The maximum delay allowed is 15 minutes and the default is 5 minutes.



### Change log for version 5.0.12_1963, released 15 May 2023
{: #5.0.12_1963_is_block_relnote}

- Updates UBI image to `8.7-1107` 
- Updates Golang to `1.19.8`
- Users must determine token exchange URL based on cluster provider. For {{site.data.keyword.satelliteshort}} clusters, always use the provided token exchange URL. If the URL is not provided, use public IAM endpoint.
- Resolves the following CVEs: [CVE-2023-0361](https://nvd.nist.gov/vuln/detail/CVE-2023-0361){: external}, [CVE-2023-24536](https://nvd.nist.gov/vuln/detail/CVE-2023-24536){: external}, [CVE-2023-24537](https://nvd.nist.gov/vuln/detail/CVE-2023-24537), [CVE-2023-24538](https://nvd.nist.gov/vuln/detail/CVE-2023-24538){: external}.

### Change log for version 5.0.10_1869, released 05 April 2023
{: #5.0.10_1869_is_block_relnote}

- Updates the storage-secret-sidecar image to `v1.2.20`.
- Updates Golang to `v1.19.7`.
- Updates the UBI image to `8.7-1085.1679482090`
- Resolves the following CVEs: [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-2250){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}, and [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}.


### Change log for version 5.0.9_1862, released 29 March 2023
{: #5.0.9_1862_is_block_relnote}

- Updates the storage-secret-sidecar image to `v1.2.19`.
- Resolves [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}


### Change log for version 5.0.8_1841, released 07 March 2023
{: #5.0.8_1841_is_block_relnote}

- Updates the storage-secret-sidecar image to `v1.2.18`.
- Resolves the following CVEs: [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}, [CVE-2022-4415](https://nvd.nist.gov/vuln/detail/CVE-2022-4415){: external}, [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/CVE-2022-40897){: external}.


### Change log for version 5.0.7_1836, released 21 February 2023
{: #5.0.7-1836_is_block_relnote}

- Added `priorityClass` in the deployment file for controller and node pods.
- Removed `preStop hook` for the `csi-driver-registrar`.
- Resolves [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}.



### Change log for version 5.0.5_1784, released 24 January 2023
{: #5.0.5-1784_is_block_relnote}


- Updates the storage-secret-sidecar image to `v1.2.15`.
- Resolves [CVE-2022-43680](https://nvd.nist.gov/vuln/detail/CVE-2022-43680){: external}, [CVE-2022-42010](https://nvd.nist.gov/vuln/detail/CVE-2022-42010){: external}, [CVE-2022-42011](https://nvd.nist.gov/vuln/detail/CVE-2022-42011){: external}, [CVE-2022-42012](https://nvd.nist.gov/vuln/detail/CVE-2022-42012){: external}, [CVE-2022-3821](https://nvd.nist.gov/vuln/detail/CVE-2022-3821){: external}, [CVE-2022-35737](https://nvd.nist.gov/vuln/detail/CVE-2022-35737){: external}, and [CVE-2021-46848](https://nvd.nist.gov/vuln/detail/CVE-2021-46848){: external}.

### Change log for version 5.0.4_1773, released 10 January 2023
{: #5.0.4-1773_is_block_relnote}

- Updates Golang to `1.18.9`.
- Updates the `storage-secret-sidecar` image to `v1.2.14`.
- Fixed volume tagging issue related to multiple tags.
- Added Block storage volume health state in driver logs. Volume health gives a detailed description as mentioned in the [Managing block storage](/docs/vpc?topic=vpc-block-storage-vpc-monitoring&interface=ui#block-storage-vpc-health-states) doc.
- Resolves the following CVEs:
    - [CVE-2022-42898](https://nvd.nist.gov/vuln/detail/CVE-2022-42898){: external}
    - [CVE-2022-41717](https://nvd.nist.gov/vuln/detail/CVE-2022-41717){: external}
    - [CVE-2022-41720](https://nvd.nist.gov/vuln/detail/CVE-2022-41720){: external}

### Change log for version 5.0.2_1713, released 17 November 2022
{: #5.0.2-1713_is_block_relnote}

- Updates the `storage-secret-sidecar` image to `v1.2.12`
- Resolves the following CVEs: 
    - [CVE-2016-3709](https://nvd.nist.gov/vuln/detail/CVE-2016-3709){: external}
    - [CVE-2022-30698](https://nvd.nist.gov/vuln/detail/CVE-2022-30698){: external}
    - [CVE-2022-30699](https://nvd.nist.gov/vuln/detail/CVE-2022-30699){: external}
    - [CVE-2022-1304](https://nvd.nist.gov/vuln/detail/CVE-2022-1304){: external}


### Change log for version 5.0.1_1695, released 9 November 2022
{: #5.0.1-1695_is_block_relnote}

- Updates the `storage-secret-sidecar` image to `v1.2.10`
- Updates the `csi-node-driver-registrar` to `v2.5.0`
- Updates the `livenessprobe` to `v2.6.0`
- Updates the `csi-provisioner` to `v3.2.1` 
- Updates the `csi-attacher` to `v3.5.0` 
- Updates the `csi-resizer` to `v1.5.0`
- Resolves the following CVEs: 
    - [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}
    - [CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external}
    - [CVE-2022-40674](https://nvd.nist.gov/vuln/detail/CVE-2022-40674){: external}
    - [CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external}
    - [CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external}
    - [CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external}


### Change log for version 5.0, released 11 October 2022
{: #5.0_is_block_relnote}

- Adds snapshot support for cluster versions 4.9 and later.
- Makes the resource requests and limits of the `vpc-block-csi-driver` containers configurable. To view the config run `kubectl get cm -n kube-system addon-vpc-block-csi-driver-configmap -o yaml`
- Adds the following parameters for customizing the driver.
    - `AttachDetachMinRetryGAP: "3"`: The initial retry interval for checking Attach/Detach Status. The default is 3 seconds.
    - `AttachDetachMinRetryAttempt: "3"`: The number of attempts for AttachDetachMinRetryGAP. The default is 3 retries for 3 seconds retry gap.
    - `AttachDetachMaxRetryAttempt: "46"`: Total number of retries for checking Attach/Detach Status. Default is 46 times. For example,  ~7 minutes (3 secs * 3 times + 6 secs * 6 times + 10 secs * 10 times).
    - `AttacherWorkerThreads: "15"`: The number of `goroutines` for processing VolumeAttachments.
    - `AttacherKubeAPIBurst: "10"`: The number of requests to the Kubernetes API server, exceeding the QPS, that can be sent at any given time
    - `AttacherKubeAPIQPS: "5.0"`: The number of requests per second sent by a Kubernetes client to the Kubernetes API server.
- Disables the `handle-volume-inuse-error` option as this is applies to CSI drivers that support offline expansion only.



### Change log for version 5.0.4-beta_1566, released 14 July 2022
{: #5.0.4-beta_1556_is_block_relnote}

- Updates the storage-secret-sidecar image to `v1.1.12`.
- Updates Golang to version `1.18.3`.
- Updates UBI image to version `8.6-854`.
- Pushes community images to `icr.io`.
- Fixes a bug for `user_tags` and `service_tags` data types.
- Changes the `volumesnapshotclass` name.
- Fixes for format errors and mount failures.
- Resolves the following CVEs:
    - [CVE-2022-29824](https://nvd.nist.gov/vuln/detail/CVE-2022-29824){: external}
    - [CVE-2021-40528](https://nvd.nist.gov/vuln/detail/CVE-2021-40528){: external}
    - [CVE-2022-22576](https://nvd.nist.gov/vuln/detail/CVE-2022-22576){: external}
    - [CVE-2022-27774](https://nvd.nist.gov/vuln/detail/CVE-2022-27774){: external}
    - [CVE-2022-27776](https://nvd.nist.gov/vuln/detail/CVE-2022-27776){: external}
    - [CVE-2022-27782](https://nvd.nist.gov/vuln/detail/CVE-2022-27782){: external}
    - [CVE-2022-25313](https://nvd.nist.gov/vuln/detail/CVE-2022-25313){: external}
    - [CVE-2022-25314](https://nvd.nist.gov/vuln/detail/CVE-2022-25314){: external}


### Change log for version 5.0.1-beta_1411, released 15 June 2022
{: #5.0.1-beta_1411_is_block_relnote}

Fixes a bug where the resource group wasn't included in the snapshot creation request payload.


### Change log for version 5.0.0-beta_1125, released 10 June 2022
{: #5.0.0-beta_1125_is_block_relnote}

Adds snapshot support.
