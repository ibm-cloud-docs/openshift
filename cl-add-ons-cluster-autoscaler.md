---

copyright:
  years: 2024, 2026

lastupdated: "2026-09-03"


keywords: change log, version history, Cluster autoscaler

subcollection: "openshift"

---

{{site.data.keyword.attribute-definition-list}}




# Cluster autoscaler add-on version change log
{: #cl-add-ons-cluster-autoscaler}


Patch updates
:   Patch updates are delivered automatically by IBM and don't contain any feature updates or changes in the supported add-on and cluster versions.

Release updates
:   Release updates contain new features or changes in the supported add-on or cluster versions. You must manually apply release updates to your cluster autoscaler add-on.

To view a list of add-ons and the supported cluster versions, run the following command or see the [Supported cluster add-ons table](/docs/openshift?topic=openshift-supported-cluster-addon-versions).

```sh
ibmcloud oc cluster addon versions
```
{: pre}


Review the version history for Cluster autoscaler.
{: shortdesc}


## Version 2.0.0
{: #cl-add-ons-cluster-autoscaler-2.0.0}


### 07 July 2026, Version 2.0.0 - v200-12-0_351296784
{: #cl-add-ons-cluster-autoscaler-v200-12-0_351296784}

- Resolves the following CVEs: [CVE-2026-42507](https://nvd.nist.gov/vuln/detail/cve-2026-42507){: external}.
- Updates Go to version `1.25.11`.
- Update storage secret sidecar 1.3.56 
- `1.30.7 200-12`
- `1.31.5 200-12`
- `1.32.7 200-12`
- `1.33.4 200-12`
- `1.34.4 200-12`
- `1.35.0 200-12`


### 30 April 2026, Version 2.0.0 - v200-7-0_332133224
{: #cl-add-ons-cluster-autoscaler-v200-7-0_332133224}

- Update storage secret sidecar 1.3.44 
- `1.30.7 200-7`
- `1.31.5 200-7`
- `1.32.7 200-7`
- `1.33.4 200-7`
- `1.34.4 200-7`
- `1.35.0 200-7`


### 24 March 2026, Version 2.0.0 - v200-6-0_326846817
{: #cl-add-ons-cluster-autoscaler-v200-6-0_326846817}

- Update storage secret sidecar 1.3.43 
- Fix issue where scale down to 0 was not working in CA 1.34 
- `1.30.7 200-6`
- `1.31.5 200-6`
- `1.32.5 200-6`
- `1.33.3 200-6`
- `1.34.2 200-6.`


### 18 February 2026, Version 2.0.0 - v200-4_316755565
{: #cl-add-ons-cluster-autoscaler-v200-4_316755565}

- Resolves the following CVEs: [CVE-2025-13281](https://nvd.nist.gov/vuln/detail/cve-2025-13281){: external}.
- Update storage secret sidecar v1.3.40 
- `1.30.7 200-4`
- `1.31.5 200-4`
- `1.32.5 200-4`
- `1.33.3 200-4`
- `1.34.2 200-4.`


### 2 December 2025, Version patch update 2.0.0-2_302959219
{: #2.0.0-2_302959219_ca}

- Adds support for scale down to 0.
- Adds support for cluster version 1.34.
- Updates base golang version to `1.25.4`.
- Updates storage secret sidecar `1.3.37`.
- Image tags: `1.30.7-v200-2`, `1.31.5-v200-2`, `1.32.4-v200-2`, `1.33.2-v200-2`, `1.34.1-v200-2`.


## Version 1.2.4
{: #cl-add-ons-cluster-autoscaler-1.2.4}


### 07 July 2026, Version 1.2.4 - v124-13-0_351834855
{: #cl-add-ons-cluster-autoscaler-v124-13-0_351834855}

- Resolves the following CVEs: [CVE-2026-27145](https://nvd.nist.gov/vuln/detail/cve-2026-27145){: external}, and [CVE-2026-42507](https://nvd.nist.gov/vuln/detail/cve-2026-42507){: external}.
- Updates Go to version `1.25.11`.
- Update storage secret sidecar 1.3.56 
- `1.28.7 124-13`
- `1.29.5 124-13`
- `1.30.7 124-13`
- `1.31.5 124-13`
- `1.32.7 124-13`
- `1.33.4 124-13`
- `1.34.3 124-13.`


### 24 March 2026, Version 1.2.4 - v124-8-0_326847250
{: #cl-add-ons-cluster-autoscaler-v124-8-0_326847250}

- Update storage secret sidecar 1.3.43 
- `1.28.7 124-8`
- `1.29.5 124-8`
- `1.30.7 124-8`
- `1.31.5 124-8`
- `1.32.5 124-8`
- `1.33.3 124-8`
- `1.34.2 124-8.`


### 16 February 2026, Version 1.2.4 - v124-7_312863411
{: #cl-add-ons-cluster-autoscaler-v124-7_312863411}

- Resolves the following CVEs: [CVE-2025-4563](https://nvd.nist.gov/vuln/detail/cve-2025-4563){: external}, [CVE-2025-5187](https://nvd.nist.gov/vuln/detail/cve-2025-5187){: external}, [CVE-2025-13281](https://nvd.nist.gov/vuln/detail/cve-2025-13281){: external}, [CVE-2025-30204](https://nvd.nist.gov/vuln/detail/cve-2025-30204){: external}, and [CVE-2025-22872](https://nvd.nist.gov/vuln/detail/cve-2025-22872){: external}.
- Updates Go to version `1.25.4`.
- Update storage secret sidecar v1.3.39 
- Adds support for cluster version 1.34.
- 1.34 has functionality to cordon node before terminating via the `--cordon-node-before-terminating flag`.
- `1.28.7 124-7`
- `1.29.5 124-7`
- `1.30.7 124-7`
- `1.31.5 124-7`
- `1.32.5 124-7`
- `1.33.3 124-7`
- `1.34.2 124-7.`


### 18 July 2025, Version patch update 1.2.4_680.
{: #124_680_ca}

- Resolves the following CVEs: [CVE-2025-3576](https://exchange.xforce.ibmcloud.com/vulnerabilities/cve-2025-3576){: external}, [CVE-2025-4673](https://exchange.xforce.ibmcloud.com/vulnerabilities/cve-2025-4673){: external}, [CVE-2025-4802](https://exchange.xforce.ibmcloud.com/vulnerabilities/cve-2025-4802){: external}.   
- Updates Go to 1.23.10
- Updates the `storage-secret-sidecar` image to `v1.3.30`
- Image tags: `1.28.7 124-1`, `1.29.5 124-1`, `1.30.4 124-1`, `1.31.1 124-1`, `1.32.1 124-1`.


### 22 April 2025, Version patch update 1.2.4_629.
{: #124_629_ca}

- Adds support for version 1.32
- Updates golang version to 1.23.7
- Updates the `storage-secret-sidecar` image to `v1.3.26`
- Updates open source source cluster autoscaler code to latest versions for: `1.28.7`, `1.29.5`, `1.30.4`, `1.31.2`, `1.32.1`.
- Image tags: `1.28.7 124-0`, `1.29.5 124-0`, `1.30.4 124-0`, `1.31.1 124-0`, `1.32.1 124-0`.


Beginning in version 1.2.4 the `maxEmptyBulkDelete` option is no longer supported. Remove this option from your configmap by running `kubectl edit configmap iks-ca-configmap -n kube-system` command and deleting the option. As a replacement, you can use the `maxScaleDownParallelism` option which was added in version 1.2.4. For more information, see the [configmap reference](#ca-configmap).
{: important}


### Change log for patch update 1.2.4_793, released 18th September 2025
{: #124_793_ca}

- Adds support for cluster version 1.33.
- Updates Golang version to 1.24.0.
- Updates storage secret sidecar 1.3.32.
- Resolves the following CVEs: CVE-2025-4563.
- The `--max-empty-bulk-delete` option is no longer supported. Instead, use the `--max-scale-down-parallelism` option.
- Adds GPU support with the `--scale-down-gpu-utilization-threshold` option for Nvidia vendors.
- Image tags: `1.28.7 124-4`, `1.29.5 124-4`, `1.30.5 124-4`, `1.31.3 124-4`, `1.32.2 124-4`, `1.33.0 124-4`.


## Version 1.2.3
{: #0123_ca_addon}


### 25 July 2025, Version patch update 1.2.3_716.
{: #123_716_ca}

- Resolves the following CVEs: CVE-2025-3576, CVE-2025-4673, CVE-2025-4802, CVE-2025-0426, CVE-2024-9042, CVE-2025-0426, CVE-2024-9042.
- Updates Go to `1.23.10`.
- Updates storage secret sidecar to `1.3.30`.
- Image tags: `1.28.7 123-3`, `1.29.5 123-3`, `1.30.4 123-3`, `1.31.2 123-3`.
    


### 10 March 2025, Version patch update 1.2.3_540
{: #123_540_ca}

- Updates golang version to `1.22.11` for cluster version `1.28`, `1.29`, `1.30`, and `1.31`.
- Updates the `storage-secret-sidecar` image to `v1.3.23`.
- Updates source code to version `1.28.7`, `1.29.5`, `1.30.3`, and `1.31.1`.
- Image tags: `1.27.3 123-1`, `1.28.7 123-2`, `1.29.5 123-2`, `1.30.3 123-2`, `1.31.1 123-2`.
- Resolves [CVE-2024-24789](https://nvd.nist.gov/vuln/detail/cve-2024-24789){: external}, [CVE-2024-24790](https://nvd.nist.gov/vuln/detail/cve-2024-24790){: external}, [CVE-2024-34158](https://nvd.nist.gov/vuln/detail/cve-2024-34158){: external}, [CVE-2024-34155](https://nvd.nist.gov/vuln/detail/cve-2024-34155){: external}, [CVE-2024-34156](https://nvd.nist.gov/vuln/detail/cve-2024-34156){: external}, and [CVE-2024-43040](https://nvd.nist.gov/vuln/detail/cve-2024-43040){: external}.


### 31 October 2024, Version patch update 1.2.3_512
{: #123_512_ca}

- Adds support for version 1.31.
- Updates the storage-secret-sidecar image to v1.3.16.
- Image tags: `1.27.3 123-1`, `1.28.0 123-1`, `1.29.0 123-1`, `1.30.2 123-1`, `1.31.0 123-1`


## Version 1.2.2
{: #0122_ca_addon}


### 15 July 2024, Version patch update 1.2.2_466
{: #122_466_ca}

- Updates the `storage-secret-sidecar` image to `v1.3.10`.
- Resolves [CVE-2024-28182](https://nvd.nist.gov/vuln/detail/cve-2024-28182){: external} and [CVE-2023-2953](https://nvd.nist.gov/vuln/detail/cve-2023-2953){: external}
- Image tags: `1.24.0-122-0`, `1.25.0-122-0`, `1.26.4-122-0`, `1.27.3-122-0`, `1.28.0-122-0`, `1.29.0-122-0`.


### 20 June 2024, Version patch update 1.2.2_452
{: #122452_ca}

- Adds support for version 1.30.
- Changes the format of the `cluster-autoscaler-status` configmap. For more information, see the [Community Kubernetes pull request](https://github.com/kubernetes/autoscaler/pull/6375){: external}.
- Image tags: `1.22.0-122-0`, `1.23.0-122-0`, `1.24.0-122-0`, `1.25.0-122-0`, `1.26.4-122-0`, `1.27.3-122-0`, `1.28.0-122-0`, `1.29.0-122-0`, `1.30.0-122-0`.


## Version 1.2.1
{: #0121_ca_addon}


### 15 July 2024, Version patch update 1.2.1_467
{: #121_467_ca}

- Updates the `storage-secret-sidecar` image to `v1.3.10`.
- Resolves [CVE-2024-28182](https://nvd.nist.gov/vuln/detail/cve-2024-28182){: external} and [CVE-2023-2953](https://nvd.nist.gov/vuln/detail/cve-2023-2953){: external}
- Image tags: `1.24.0-121-2`, `1.25.0-121-2`, `1.26.4-121-2`, `1.27.3-121-2`, `1.28.0-121-2`, `1.29.0-121-2`.


### 21 June 2024, Version patch update 1.2.1_444
{: #121444_ca}

- Updates the `storage-secret-sidecar` image to `v1.3.9`.
- Updates golang version to `1.21.11`.
- Image tags: `1.24.0-121-2`, `1.25.0-121-2`, `1.26.4-121-2`, `1.27.3-121-2`, `1.28.0-121-2`, `1.29.0-121-2`.


### 05 May 2024, Version patch update 1.2.1_425
{: #121425_ca}

- Updates the `storage-secret-sidecar` image to `v1.3.7`
- Fixes a utilization calculation bug during scale down.
- Image tags: `1.22.0-121-1`, `1.23.0-121-1`, `1.24.0-121-1`, `1.25.0-121-1`, `1.26.4-121-1`, `1.27.3-121-1`, `1.28.0-121-1`, and `1.28.0-121-1`.


### 02 April 2024, Version patch update 1.2.1_418
{: #121418_ca}

- Updates the `storage-secret-sidecar` image to `v1.3.6`
- Adds support for `drainPriorityConfig`, `dynamicNodeDeleteDelayAfterTaintEnabled`, `loggingFormat`, `emitPerNodegroupMetrics`, `kubeApiContentType`, `featureGates` parameters.
- Image tags: `1.22.0-121-0`, `1.23.0-121-0`, `1.24.0-121-0`, `1.25.0-121-0`, `1.26.4-121-0`, `1.27.3-121-0`, `1.28.0-121-0`.


### 28 February 2024, Version patch update 1.2.1_395
{: #121395_ca}

- Adds support for cluster version 1.29.
- Image tags: `1.22.0-121-0`, `1.23.0-121-0`, `1.24.0-121-0`, `1.25.0-121-0`, `1.26.4-121-0`, `1.27.3-121-0`, `1.28.0-121-0`.


## Version 1.2.0
{: #0120_ca_addon}


### 15 July 2024, Version patch update 1.2.0_468
{: #120_468_ca}

- Updates the `storage-secret-sidecar` image to `v1.3.10`.
- Resolves [CVE-2024-28182](https://nvd.nist.gov/vuln/detail/cve-2024-28182){: external} and [CVE-2023-2953](https://nvd.nist.gov/vuln/detail/cve-2023-2953){: external}
- Image tags: `1.24.0-120-6`, `1.25.0-120-6`, `1.26.4-120-6`, `1.27.3-120-6`, `1.28.0-120-6`.


### 21 June 2024, Version patch update 1.2.0_443
{: #120443_ca}

- Updates the `storage-secret-sidecar` image to `v1.3.9`.
- Updates golang version to `1.21.11`.
- Image tags: `1.24.0-120-6`, `1.25.0-120-6`, `1.26.4-120-6`, `1.27.3-120-6`, `1.28.0-120-6`.


### 05 May 2024, Version patch update 1.2.0_426
{: #120426_ca}

- Updates the storage-secret-sidecar image to `v1.3.7`
- Fixes a utilization calculation bug during scale down.
- Image tags: `1.22.0-120-5`, `1.23.0-120-5`, `1.24.0-120-5`, `1.25.0-120-5`, `1.26.4-120-5`, `1.27.3-120-5`, and `1.28.0-120-5`.


### 02 April 2024, Version patch update 1.2.0_410
{: #120410_ca}

- Updates the `storage-secret-sidecar` image to `v1.3.6`
- Images tags: `1.22.0-120-4`, `1.23.0-120-4`, `1.24.0-120-4`, `1.25.0-120-4`, `1.26.4-120-4`, `1.27.3-120-4`, `1.28.0-120-4`.


### 21 February 2024, Version patch update 1.2.0_365
{: #120365_ca}

- Updated the storage-secret-sidecar image to `v1.3.5`.
- Image tags: `1.22.0-120-4`, `1.23.0-120-4`, `1.24.0-120-4`, `1.25.0-120-4`, `1.26.4-120-4`, `1.27.3-120-4`, and `1.28.0-120-4`.


### 16 January 2024, Version patch update 1.2.0_322
{: #120322_ca}

- Fixes [CVE-2007-4559](https://access.redhat.com/security/cve/CVE-2007-4559){: external}, [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/cve-2023-22745){: external}, [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/cve-2023-4641){: external}
- Updated the storage-secret-sidecar image to `v1.3.4`
- Fixes an issue while updating custom variables via add-on.
- Adds support for the `maxPodEvictionTime` parameter.
- Image tags: `1.22.0-120-3`, `1.23.0-120-3`, `1.24.0-120-3`, `1.25.0-120-3`, `1.26.4-120-3`, `1.27.3-120-3`, and `1.28.0-120-3`.


### 27 November 2023, Version patch update 1.2.0_290
{: #120290_ca}

- Fixes [CVE-2007-4559](https://access.redhat.com/security/cve/CVE-2007-4559){: external}, [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/cve-2023-22745){: external}, and [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/cve-2023-4641){: external}.
- Updated the storage-secret-sidecar image to `v1.3.3`.
- Image tags: `1.22.0-120-2`, `1.23.0-120-2`, `1.24.0-120-2`, `1.25.0-120-2`, `1.26.4-120-2`, `1.27.3-120-2`, and `1.28.0-120-2`.


### 15 November 2023, Version patch update 1.2.0_228
{: #120228_ca}

- Adds support for cluster version 1.28
- Image tags: `1.22.0-120-2`, `1.23.0-120-2`, `1.24.0-120-2`, `1.25.0-120-2`, `1.26.4-120-2`, `1.27.3-120-2`, and `1.28.0-120-2`.


## Version 1.0.9
{: #0109_ca_addon}


### 02 April 2024, Version patch update 1.0.9_411
{: #109411_ca}

- Updates the `storage-secret-sidecar` image to `v1.2.33`
- Images tags: `1.22.0-109-3`, `1.23.0-109-3`, `1.24.0-109-3`, `1.25.0-109-3`, `1.26.1-109-3`, `1.27.2-109-3`.


### 21 February 2024, Version patch update 1.0.9_377
{: #109377_ca}

- Updated the storage-secret-sidecar image to `v1.2.31`.
- Fixed naming issues with the `nodeDeleteDelayAfterTaint` and `maxNodesTotal` parameters.
- Image tags: `1.22.0-109-3`, `1.23.0-109-3`, `1.24.0-109-3`, `1.25.0-109-3`, `1.26.1-109-3`, `1.27.2-109-3`.


### 16 January 2024, Version patch update 1.0.9_328
{: #109328_ca}

- Fixes [CVE-2007-4559](https://access.redhat.com/security/cve/CVE-2007-4559){: external}, [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/cve-2023-22745){: external}, [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/cve-2023-4641){: external}
- Updates the storage-secret-sidecar image to `v1.2.30`.
- Fixes an issue while updating custom variables via add-on.


### 27 November 2023, Version patch update 1.0.9_290
{: #109290_ca}

- Fixes [CVE-2007-4559](https://access.redhat.com/security/cve/CVE-2007-4559){: external}, [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/cve-2023-22745){: external}, and [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/cve-2023-4641){: external}.
- Updated the storage-secret-sidecar image to `v1.2.29`.
- Image tags: `1.22.0-109-2`, `1.23.0-109-2`, `1.24.0-109-2`, `1.25.0-109-2`, `1.26.1-109-2`, `1.27.2-109-2`.


### 13 November 2023, Version patch update 1.0.9_195
{: #109195_ca}

- Updates the `storage-secret-sidecar` image to `v1.2.28`.
- Updates Golang to 1.20.10.
- Image tags: `1.22.0-109-2`, `1.23.0-109-2`, `1.24.0-109-2`, `1.25.0-109-2`, `1.26.1-109-2`, `1.27.2-109-2`.


### 04 October 2023, Version patch update 1.0.9_134
{: #109134_ca}

- Adds constraints to allow add-on deployment on `amd64` architecture only.
- Image tags: `1.22.0-109-1`, `1.23.0-109-1`, `1.24.0-109-1`, `1.25.0-109-1`, `1.26.1-109-1`, `1.27.2-109-1`.


### 15 September 2023, Version patch update 1.0.9_103
{: #109103_ca}

- Image tags: `1.22.0-109-3`, `1.23.0-109-3`, `1.24.0-109-3`, `1.25.0-109-3`, `1.26.1-109-3`, `1.27.2-109-3`.
- Updated the storage-secret-sidecar image to `v1.2.26`.
- Golang update to resolve [CVE-2023-29409](https://nvd.nist.gov/vuln/detail/cve-2023-29409){: external}.


### 07 August 2023, Version patch update 1.0.9_81
{: #10981_ca}

- Image tags: `1.22.0-109-0`, `1.23.0-109-0`, `1.24.0-109-0`, `1.25.0-109-0`,`1.26.1-109-0`,`1.27.2-109-0`.
- Updates the `storage-secret-sidecar` image to `v1.2.25`.
- Resolves the followings CVEs:[CVE-2023-2283](https://nvd.nist.gov/vuln/detail/cve-2023-2283){: external},[CVE-2023-26604](https://nvd.nist.gov/vuln/detail/cve-2023-26604){: external},[CVE-2020-24736](https://nvd.nist.gov/vuln/detail/cve-2020-24736){: external}, and [CVE-2023-1667](https://nvd.nist.gov/vuln/detail/cve-2023-1667){: external}.


### 24 July 2023, Version patch update 1.0.9_70
{: #10970_ca}

- Adds support for the `prometheusScrape` annotation.
- Image tags: `1.22.0-109-0`, `1.23.0-109-0`, `1.24.0-109-0`, `1.25.0-109-0`, `1.26.1-109-0`, `1.27.2-109-0`.


### 22 June 2023, Version patch update 1.0.9_44
{: #10944_ca}


- Adds support for cluster version 1.27.
- Adds the `scaleDownUnreadyEnabled`, `maxNodesPerScaleup`, `maxNodegroupBinpackingDuration`, `kubeClientBurst`, and `kubeClientQPS` parameters.
- Updates the `storage-secret-sidecar` image to `v1.2.24`.
- Updates Golang to `1.19.10` for `iks-cluster-autoscaler` `1.22-1.26` and Golang version `1.20.5` for `iks-cluster-autoscaler 1.27`.
- Image tags: `1.22.0 109-0`, `1.23.0 109-0`, `1.24.0 109-0`, `1.25.0 109-0`, `1.26.1 109-0`, `1.27.2 109-0`.


Version 1.0.9 version is deprecated and becomes unsupported on 30 April 2024.
{: note}


## Version 1.1.0 (Beta)
{: #0110_ca_addon}


### 16 February 2024, Version patch update 1.1.0_362
{: #110362_ca}

- Image tags: `1.21.0 110-10`, `1.22.0 110-10`, `1.23.0 110-10`, `1.24.0 110-10`, `1.25.0 110-10`.
- Updates `golang` version to `1.20.11`.


### 15 May 2023, Version patch update 1.1.0_1066
{: #111066_ca}

- Image tags: `1.21.0 110-9`, `1.22.0 110-9`, `1.23.0 110-9`, `1.24.0 110-9`, `1.25.0 110-9`
- Resolves issues while reading secrets. 


### 26 April 2023, Version patch update 1.1.0_1060
{: #111060_ca}

- Image tags: `1.19.1 110-8`, `1.20.0 110-8`, `1.21.0 110-8`, `1.22.0 110-8`, `1.23.0 110-8`.
- Updates `golang` version to `1.19.8`.
- Adds support for {{site.data.keyword.satelliteshort}} cluster versions 4.11 and 4.12.


### 16 March 2023, Version patch update 1.1.0_978
{: #110978_ca}

- Image tags: `1.19.1 110-6`, `1.20.0 110-6`, `1.21.0 110-6`, `1.22.0 110-6`, `1.23.0 110-6`.
- Updates `golang` version to `1.19.6`.


### 9 January 2023, Version patch update 1.1.0_897
{: #110897_ca}

- Image tags: `1.19.1 110-5`, `1.20.0 110-5`, `1.21.0 110-5`, `1.22.0 110-5`, `1.23.0 110-5`.
- Golang updated to `1.18.9`
- Updates the `storage-secret-sidecar` image to `v1.2.14`
- Resolves the following CVEs: [CVE-2022-42898](https://www.cve.org/cveRecord?id=cve-2022-42898){: external}, [CVE-2022-41717](https://www.cve.org/cveRecord?id=cve-2022-41717){: external}, [CVE-2022-41720](https://www.cve.org/cveRecord?id=cve-2022-41720){: external}


### 22 September 2022, Version patch update 1.1.0_798
{: #110798_ca}

- Image tags: `1.19.1-110-5`,`1.20.0-110-5`,`1.21.0-110-5`,`1.22.0-110-5`,`1.23.0-110-5`.
- Resolves [CVE-2022-27664](https://www.cve.org/cveRecord?id=cve-2022-27664){: external}, [CVE-2022-32190](https://www.cve.org/cveRecord?id=cve-2022-32190){: external}.


### 31 August 2022, Version patch update 1.1.0_776
{: #110776_ca}

- Image tags: `1.19.1-110-4`, `1.20.0-110-4`, `1.21.0-110-4`, `1.22.0-110-4`, `1.23.0-110-4`
- Resolves [CVE-2022-30630](https://nvd.nist.gov/vuln/detail/cve-2022-30630){: external}, [CVE-2022-30635](https://nvd.nist.gov/vuln/detail/cve-2022-30635){: external}, [CVE-2022-32148](https://nvd.nist.gov/vuln/detail/cve-2022-32148){: external}, [CVE-2022-30631](https://nvd.nist.gov/vuln/detail/cve-2022-30631){: external}, [CVE-2022-30632](https://nvd.nist.gov/vuln/detail/cve-2022-30632){: external}, [CVE-2022-32189](https://nvd.nist.gov/vuln/detail/cve-2022-32189){: external}, [CVE-2022-28131](https://nvd.nist.gov/vuln/detail/cve-2022-28131){: external}, [CVE-2022-30633](https://nvd.nist.gov/vuln/detail/cve-2022-30633){: external}, and [CVE-2022-1705](https://nvd.nist.gov/vuln/detail/cve-2022-1705){: external}.


### 21 July 2022, Version patch update 1.1.0_729
{: #110729_ca}

- Image tags: `1.19.1-101-2`, `1.20.0-101-2`, `1.21.0-101-2`, `1.22.0-101-2`, `1.23.0-101-2`
- Resolves [CVE-2022-29526](https://nvd.nist.gov/vuln/detail/cve-2022-29526){: external}.


### 30 June 2022, Version patch update 1.1.0_682
{: #110682_ca}

- Image tags: `1.19.1 110-1`, `1.20.0 110-1`, `1.21.0 110-1`, `1.22.0 110-1`, `1.23.0 110-1`
- Adds `storage-secret-store` compatibility fixes for {{site.data.keyword.satelliteshort}} clusters.
- Adds logging improvements.


### 16 May 2022, Version patch update 1.1.0_615
{: #110615_ca}

- Image tags: `1.19.1-110-0`, `1.20.0-110-0`, `1.21.0-110-0`, `1.22.0-110-0`, `1.23.0-110-0`
- Resolves [CVE-2022-28327](https://nvd.nist.gov/vuln/detail/cve-2022-28327){: external}, [CVE-2022-24675](https://nvd.nist.gov/vuln/detail/cve-2022-24675){: external}, and [CVE-2022-27536](https://nvd.nist.gov/vuln/detail/cve-2022-27536){: external}.
- Ignores label `ibm-cloud.kubernetes.io/vpc-instance-id` for zone balancing in satellite environments.
- Adds experimental option `balancingIgnoreLabelsFlag`. This option defines a node label that should be ignored when considering node group similarity. One label can be defined per option occurrence.


### 30 March 2022, Version patch update 1.1.0_475
{: #110475_ca}

- Image tags: `1.19.1-12`, `1.20.0-12`, `1.21.0-8`, `1.22.0-6`, `1.23.0-3`
- Resolves [CVE-2022-24921](https://nvd.nist.gov/vuln/detail/cve-2022-24921){: external}.
- Adds permissions for `cluster-autoscaler` to watch namespaces.


### 16 March 2022, Version patch update 1.1.0_429
{: #110429_ca}

- Image tags: `1.19.1-11`, `1.20.0-11`, `1.21.0-7`, `1.22.0-5`, `1.23.0-2`
- Adds Beta support for {{site.data.keyword.satelliteshort}} clusters in allowlisted accounts.


Version 1.1.0 is a {{site.data.keyword.satelliteshort}} Beta release. Patches might be slower on this version.
{: preview}


## Version 1.0.8
{: #0108_ca_addon}


### 27 November 2023, Version patch update 1.0.8_292
{: #108292_ca}

- Fixes [CVE-2007-4559](https://access.redhat.com/security/cve/CVE-2007-4559){: external}, [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/cve-2023-22745){: external}, and [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/cve-2023-4641){: external}.
- Updated the storage-secret-sidecar image to `v1.2.29`.
- Image tags: `1.20.0 108-5`, `1.21.0 108-5`, `1.22.0 108-5`, `1.23.0 108-5`, `1.24.0 108-5`, `1.25.0 108-5`, and `1.26.0 108-5`.


### 13 November 2023, Version patch update 1.0.8_233
{: #108233_ca}


- Updates the `storage-secret-sidecar` image to `v1.2.28`.
- Updates Golang to 1.20.10.
- Image tags: `1.20.0 108-5`, `1.21.0 108-5`, `1.22.0 108-5`, `1.23.0 108-5`, `1.24.0 108-5`, `1.25.0 108-5`, and `1.26.0 108-5`.


### 15 September 2023, Version patch update 1.0.8_104
{: #108104_ca}

- Image tags: `1.22.0-108-4`, `1.23.0-109-4`, `1.24.0-108-4`, `1.25.0-108-4`, `1.26.1-108-4`, `1.27.2-109-4`.
- Updated the storage-secret-sidecar image to `v1.2.26`.
- Golang update to resolve [CVE-2023-29409](https://nvd.nist.gov/vuln/detail/cve-2023-29409){: external}.


### 7 August 2023, Version patch update 1.0.8_82
{: #10882_ca}

- Image tags: `1.20.0 108-3`, `1.21.0 108-3`, `1.22.0 108-3`, `1.23.0 108-3`, `1.24.0 108-3`, `1.25.0 108-3`, `1.26.0 108-3`.
- Updates the `storage-secret-sidecar` image to `v1.2.25`.
- Resolves the followings CVEs:[CVE-2023-2283](https://nvd.nist.gov/vuln/detail/cve-2023-2283){: external},[CVE-2023-26604](https://nvd.nist.gov/vuln/detail/cve-2023-26604){: external},[CVE-2020-24736](https://nvd.nist.gov/vuln/detail/cve-2020-24736){: external}, and [CVE-2023-1667](https://nvd.nist.gov/vuln/detail/cve-2023-1667){: external}.


### 6 July 2023, Version patch update 1.0.8_56
{: #10856_ca}

- Image tags: `1.20.0 108-3`, `1.21.0 108-3`, `1.22.0 108-3`, `1.23.0 108-3`, `1.24.0 108-3`, `1.25.0 108-3`, `1.26.0 108-3`.
- Updates the `storage-secret-sidecar` image to `v1.2.21`.
- Updates the `golang` version to `1.19.8`.


### 15 May 2023, Version patch update 1.0.8_1078
{: #1081078_ca}

- Image tags: `1.20.0 108-2`, `1.21.0 108-2`, `1.22.0 108-2`, `1.23.0 108-2`, `1.24.0 108-2`, `1.25.0 108-2`, `1.26.0 108-2`.
- Updates `storage-secret-sidecar` image to `v1.2.21`.
- Golang updated to `1.19.8`.


### 5 April 2023, Version patch update 1.0.8_1016
{: #1081016_ca}

- Image tags: `1.20.0 108-1`, `1.21.0 108-1`, `1.22.0 108-1`, `1.23.0 108-1`, `1.24.0 108-1`, `1.25.0 108-1`, and `1.26.0 108-1`.
- Updates the `storage-secret-sidecar` image to `v1.2.20`.
- Updates the `golang` version to `1.19.7`.
- Resolves an issue where `cluster-autoscaler` stops retrying requests that return HTTP 401 codes.
- Logging improvements.


### 29 March 2023, Version patch update 1.0.8_987
{: #108987_ca}

- Image tags: `1.20.0 108-0`, `1.21.0 108-0`, `1.22.0 108-0`, `1.23.0 108-0`, `1.24.0 108-0`, `1.25.0 108-0`, and `1.26.0 108-0`.
- Resolves [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/cve-2023-23916){: external}.
- Updates the `storage-secret-sidecar` image to `v1.2.19`.


### 9 March 2023, Version patch update 1.0.8_968
{: #108968_ca}

- Image tags: `1.20.0 108-0`, `1.21.0 108-0`, `1.22.0 108-0`, `1.23.0 108-0`, `1.24.0 108-0`, `1.25.0 108-0`, and `1.26.0 108-0`
- Golang updated to `1.19.6`
- Adds support for cluster version 1.26 based on the Kubernetes community [cluster-autoscaler](https://github.com/kubernetes/autoscaler/releases/tag/cluster-autoscaler-1.26.0){: external}.


### Change log for patch update 1.0.8_346, released 01 February  2024
{: #108346_ca}

- Updates the `storage-secret-sidecar` image to `v1.2.30`.
- Image tags: `1.20.0 108-5`, `1.21.0 108-5`, `1.22.0 108-5`, `1.23.0 108-5`, `1.24.0 108-5`, `1.25.0 108-5`, and `1.26.0 108-5`.


## Version 1.0.7
{: #0107_ca_addon}


### 27 November 2023, Version patch update 1.0.7_291
{: #107291_ca}

- Fixes [CVE-2007-4559](https://access.redhat.com/security/cve/CVE-2007-4559){: external}, [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/cve-2023-22745){: external}, and [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/cve-2023-4641){: external}.
- Updated the storage-secret-sidecar image to `v1.2.29`.
- Image tags: `1.20.0 107-7`, `1.21.0 107-7`, `1.22.0 107-7`, `1.23.0 107-7`, `1.24.0 107-7`, and `1.25.0 107-7`.


### 13 November 2023, Version patch update 1.0.7_185
{: #107_185_ca}

- Updates the `storage-secret-sidecar` image to `v1.2.28`.
- Updates Golang to 1.20.10.
- Image tags: `1.20.0 107-7`, `1.21.0 107-7`, `1.22.0 107-7`, `1.23.0 107-7`, `1.24.0 107-7`, and `1.25.0 107-7`.


### 15 September 2023, Version patch update 1.0.7_102
{: #107102_ca}

- Image tags: `1.22.0-107-7`, `1.23.0-107-7`, `1.24.0-107-7`, `1.25.0-107-7`, `1.26.1-107-7`, `1.27.2-107-7`.
- Updated the storage-secret-sidecar image to `v1.2.26`.
- Golang update to resolve [CVE-2023-29409](https://nvd.nist.gov/vuln/detail/cve-2023-29409){: external}.


### 7 August 2023, Version patch update 1.0.7_83
{: #10783_ca}

- Image tags: `1.20.0 107-6`, `1.21.0 107-6`, `1.22.0 107-6`, `1.23.0 107-6`, `1.24.0 107-6`,`1.25.0 107-6`.
- Updates the `storage-secret-sidecar` image to `v1.2.25`.
- Resolves the followings CVEs:[CVE-2023-2283](https://nvd.nist.gov/vuln/detail/cve-2023-2283){: external},[CVE-2023-26604](https://nvd.nist.gov/vuln/detail/cve-2023-26604){: external},[CVE-2020-24736](https://nvd.nist.gov/vuln/detail/cve-2020-24736){: external}, and [CVE-2023-1667](https://nvd.nist.gov/vuln/detail/cve-2023-1667){: external}.


### 6 July 2023, Version patch update 1.0.7_57
{: #10757_ca}

- Image tags: `1.20.0 107-6`, `1.21.0 107-6`, `1.22.0 107-6`, `1.23.0 107-6`, `1.24.0 107-6`,`1.25.0 107-6`.
- Updates the `storage-secret-sidecar` image to `v1.2.21`.
- Updates the `golang` version to `1.19.8`.
- Fixes an issue where `cluster-autoscaler` stops retrying requests that return `HTTP401` code.


### 15 May 2023, Version patch update 1.0.7_1076
{: #1071076_ca}

- Image tags: `1.20.0 107-5`, `1.21.0 107-5`, `1.22.0 107-5`, `1.23.0 107-5`, `1.24.0 107-5`,`1.25.0 107-5`.
- Updates the `storage-secret-sidecar` image to `v1.2.21`
- Golang updated to `1.19.8`.
- Fixes issue where `cluster-autoscaler` stops retrying requests return `HTTP401` code.


### 5 April 2023, Version patch update 1.0.7_1021
{: #1071021_ca}

- Image tags: `1.20.0 107-4`, `1.21.0 107-4`,  `1.22.0 107-4`, `1.23.0 107-4`, `1.24.0 107-4`, and `1.25.0 107-4`.
- Updates the `storage-secret-sidecar` image to `v1.2.20`.
- Updates the `golang` version to `1.19.7`.


### 29 March 2023, Version patch update 1.0.7_988
{: #107988_ca}

- Image tags: `1.20.0 107-3`, `1.21.0 107-3`,  `1.22.0 107-3`, `1.23.0 107-3`, `1.24.0 107-3`, and `1.25.0 107-3`.
- Resolves [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/cve-2023-23916){: external}.
- Updates the `storage-secret-sidecar` image to `v1.2.19`.


### 7 March 2023, Version patch update 1.0.7_956
{: #107956_ca}

- Image tags: `1.20.0 107-3`, `1.21.0 107-3`,  `1.22.0 107-3`, `1.23.0 107-3`, `1.24.0 107-3`, and `1.25.0 107-3`.
- Updates the `golang` version to `1.19.6`.
- Updates the `storage-secret-sidecar` image to `v1.2.18`.
- Resolves the following CVEs: [CVE-2022-41724](https://nvd.nist.gov/vuln/detail/cve-2022-41724){: external}, [CVE-2022-41723](https://nvd.nist.gov/vuln/detail/cve-2022-41723){: external}, [CVE-2022-4415](https://nvd.nist.gov/vuln/detail/cve-2022-4415){: external}, [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/cve-2020-10735){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/cve-2021-28861){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/cve-2022-45061){: external}, and [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/cve-2022-40897){: external}.


### 17 February 2023, Version patch update 1.0.7_944
{: #107944_ca}

- Image tags: `1.20.0 107-2`, `1.21.0 107-2`,  `1.22.0 107-2`, `1.23.0 107-2`, `1.24.0 107-2`, and `1.25.0 107-2`.
- Updates the `storage-secret-sidecar` image to `v1.2.17`.
- Resolves [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/cve-2022-47629){: external}.


### 24 January 2023, Version patch update 1.0.7_940:
{: #107940_ca}

- Image tags: `1.20.0 107-2`, `1.21.0 107-2`,  `1.22.0 107-2`, `1.23.0 107-2`, `1.24.0 107-2`, and `1.25.0 107-2`.
- Updates the `storage-secret-sidecar` image to `v1.2.15`.
- Resolves the following [CVE-2022-40303](https://nvd.nist.gov/vuln/detail/cve-2022-40303){: external}, [CVE-2022-40304](https://nvd.nist.gov/vuln/detail/cve-2022-40304){: external}, [CVE-2022-35737](https://nvd.nist.gov/vuln/detail/cve-2022-35737){: external}, [CVE-2021-46848](https://nvd.nist.gov/vuln/detail/cve-2021-46848){: external}, [CVE-2022-3821](https://nvd.nist.gov/vuln/detail/cve-2022-3821){: external}.


### 9 January 2023, Version patch update 1.0.7_900
{: #107900_ca}

- Image tags: `1.20.0 107-2`, `1.21.0 107-2`, `1.22.0 107-2`, `1.23.0 107-2`, `1.24.0 107-2`, `1.25.0 107-2`.
- Golang updated to `1.18.9`
- Updates the `storage-secret-sidecar` image to `v1.2.14`
- Resolves the following CVEs: [CVE-2022-42898](https://www.cve.org/cveRecord?id=cve-2022-42898){: external}, [CVE-2022-41717](https://www.cve.org/cveRecord?id=cve-2022-41717){: external}, [CVE-2022-41720](https://www.cve.org/cveRecord?id=cve-2022-41720){: external}


### 3 November 2022, Version patch update 1.0.7_883
{: #107883_ca}

- Image tags: `1.20.0-107-1`, `1.21.0-107-1`, `1.22.0-107-1`, `1.23.0-107-1`, `1.24.0-107-1`, `1.25.0-107-1`.
- Adds compute identity support.
- Adds currency support for IKS [Cluster-autoscaler 1.25](https://github.com/kubernetes/autoscaler/releases/tag/cluster-autoscaler-1.25.0){: external}.


## Version 1.0.6
{: #0106_ca_addon}


### 15 May 2023, Version patch update 1.0.6_1077
{: #1061077_ca}

- Image tags: `1.19.1 106-8`, `1.20.0 106-8`, `1.21.0 106-8`, `1.22.0 106-8`, `1.23.0 106-8`, `1.24.0 106-8`.
- Updates the `storage-secret-sidecar` image to `v1.2.21`
- Golang updated to `1.19.8`.
- Fixes issue where `cluster-autoscaler` stops retrying requests return `HTTP401` code.


### 5 April 2023, Version patch update 1.0.6_1010
{: #1061010_ca}

- Image tags: `1.19.1 106-7`, `1.20.0 106-7`,  `1.21.0 106-7`, `1.22.0 106-7`, `1.23.0 106-7`, and `1.24.0 106-7`.
- Updates the `golang` version to `1.19.7`.


### 7 March 2023, Version patch update 1.0.6_955
{: #106955_ca}

- Image tags: `1.19.1 106-6`, `1.20.0 106-6`,  `1.21.0 106-6`, `1.22.0 106-6`, `1.23.0 106-6`, and `1.24.0 106-6`.
- Updates the `golang` version to `1.19.6`.
- Resolves the following CVEs: [CVE-2022-41724](https://nvd.nist.gov/vuln/detail/cve-2022-41724){: external}, [CVE-2022-41723](https://nvd.nist.gov/vuln/detail/cve-2022-41723){: external}, [CVE-2022-4415](https://nvd.nist.gov/vuln/detail/cve-2022-4415){: external}, [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/cve-2020-10735){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/cve-2021-28861){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/cve-2022-45061){: external}, and [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/cve-2022-40897){: external}.


### 9 January 2023, Version patch update 1.0.6_899
{: #106899_ca}

- Image tags: `1.19.1 106-5`, `1.20.0 106-5`, `1.21.0 106-5`, `1.22.0 106-5`, `1.23.0 106-5`, `1.24.0 106-5`.
- Golang updated to `1.18.9`
- Updates the `storage-secret-sidecar` image to `v1.2.14`
- Resolves the following CVEs: [CVE-2022-42898](https://www.cve.org/cveRecord?id=cve-2022-42898){: external}, [CVE-2022-41717](https://www.cve.org/cveRecord?id=cve-2022-41717){: external}, [CVE-2022-41720](https://www.cve.org/cveRecord?id=cve-2022-41720){: external}


### 10 October 2022, Version patch update 1.0.6_828
{: #106828_ca}

- Adds support for setting up to 5 additional ignore labels while balancing `balancingIgnoreLabel[1-5]`.
- `1.19.1 106-4`, `1.20.0 106-4`, `1.21.0 106-4`, `1.22.0 106-4`, `1.23.0 106-4`, `1.24.0 106-4`.


### 22 September 2022, Version patch update 1.0.6_800
{: #106800_ca}

- Image tags: `1.19.1-106-4`, `1.20.0-106-4`, `1.21.0-106-4`, `1.22.0-106-4`, `1.23.0 106-4`, `1.24.0 106-4`.
- Resolves [CVE-2022-27664](https://www.cve.org/cveRecord?id=cve-2022-27664){: external}, [CVE-2022-32190](https://www.cve.org/cveRecord?id=cve-2022-32190){: external}.


### 31 August 2022, Version patch update 1.0.6_774
{: #106774_ca}

- Image tags: `1.19.1-106-3`, `1.20.0-106-3`, `1.21.0-106-3`, `1.22.0-106-3`, `1.23.0-106-3`, `1.24.0-106-3`
- Resolves [CVE-2022-30630](https://nvd.nist.gov/vuln/detail/cve-2022-30630){: external}, [CVE-2022-30635](https://nvd.nist.gov/vuln/detail/cve-2022-30635){: external}, [CVE-2022-32148](https://nvd.nist.gov/vuln/detail/cve-2022-32148){: external}, [CVE-2022-30631](https://nvd.nist.gov/vuln/detail/cve-2022-30631){: external}, [CVE-2022-30632](https://nvd.nist.gov/vuln/detail/cve-2022-30632){: external}, [CVE-2022-32189](https://nvd.nist.gov/vuln/detail/cve-2022-32189){: external}, [CVE-2022-28131](https://nvd.nist.gov/vuln/detail/cve-2022-28131){: external}, [CVE-2022-30633](https://nvd.nist.gov/vuln/detail/cve-2022-30633){: external}, and [CVE-2022-1705](https://nvd.nist.gov/vuln/detail/cve-2022-1705){: external}.


### 17 August 2022, Version patch update 1.0.6_763
{: #106763_ca}

- Image tags: `1.19.1-106-1`, `1.20.0-106-1`, `1.21.0-106-2`, `1.22.0-106-2`, `1.23.0-106-2`, `1.24.0-106-2`
- All non-deleting workers are considered while scaling up.
- Worker deletion is not retried while scaling down.


### 15 July 2022, Version patch update 1.0.6_742
{: #106742_ca}

- Adds support for Kubernetes 1.24.
- Resolves [CVE-2022-29526](https://nvd.nist.gov/vuln/detail/cve-2022-29526){: external}.
- Image tags: `1.19.1-106-2`, `1.20.0-106-2`, `1.21.0 106-1`, `1.22.0 106-1`, `1.23.0 106-1`, `1.24.0 106-1`


## Version 1.0.5
{: #0105_ca_addon}


### 9 January 2023, Version patch update 1.0.5_898
{: #105898_ca}

- Image tags: `1.19.1 105-6`, `1.20.0 105-6`, `1.21.0 105-6`, `1.22.0 105-6`, `1.23.0 105-6`.
- Golang updated to `1.18.9`
- Updates the `storage-secret-sidecar` image to `v1.2.14`
- Resolves the following CVEs: [CVE-2022-42898](https://www.cve.org/cveRecord?id=cve-2022-42898){: external}, [CVE-2022-41717](https://www.cve.org/cveRecord?id=cve-2022-41717){: external}, [CVE-2022-41720](https://www.cve.org/cveRecord?id=cve-2022-41720){: external}


### 22 September 2022, Version patch update 1.0.5_779
{: #105779_ca}

- Image tags: `1.19.1-105-5`,`1.20.0-105-5`,`1.21.0-105-5`,`1.22.0-105-5`,`1.23.0-105-5`.
- Resolves [CVE-2022-27664](https://www.cve.org/cveRecord?id=cve-2022-27664){: external}, [CVE-2022-32190](https://www.cve.org/cveRecord?id=cve-2022-32190){: external}.


### 31 August 2022, Version patch update 1.0.5_775
{: #105775_ca}

- Image tags: `1.19.1-105-4`, `1.20.0-105-4`, `1.21.0-105-4`, `1.22.0-105-4`, `1.23.0-105-4`
- Resolves [CVE-2022-30630](https://nvd.nist.gov/vuln/detail/cve-2022-30630){: external}, [CVE-2022-30635](https://nvd.nist.gov/vuln/detail/cve-2022-30635){: external}, [CVE-2022-32148](https://nvd.nist.gov/vuln/detail/cve-2022-32148){: external}, [CVE-2022-30631](https://nvd.nist.gov/vuln/detail/cve-2022-30631){: external}, [CVE-2022-30632](https://nvd.nist.gov/vuln/detail/cve-2022-30632){: external}, [CVE-2022-32189](https://nvd.nist.gov/vuln/detail/cve-2022-32189){: external}, [CVE-2022-28131](https://nvd.nist.gov/vuln/detail/cve-2022-28131){: external}, [CVE-2022-30633](https://nvd.nist.gov/vuln/detail/cve-2022-30633){: external}, and [CVE-2022-1705](https://nvd.nist.gov/vuln/detail/cve-2022-1705){: external}.


### 17 August 2022, Version patch update 1.0.5_754
{: #105754_ca}

- Image tags: `1.19.1-105-3`, `1.20.0-105-3`, `1.21.0-105-3`, `1.22.0-105-3`, `1.23.0-105-3`
- All non-deleting workers are considered while scaling up.
- Worker deletion is not retried while scaling down.


### 19 July 2022, Version patch update 1.0.5_728
{: #105728_ca}

- Image tags: `1.19.1-105-2`, `1.20.0-105-2`, `1.21.0-105-2`, `1.22.0-105-2`, `1.23.0-105-2`
- Resolves [CVE-2022-29526](https://nvd.nist.gov/vuln/detail/cve-2022-29526){: external}.


### 30 June 2022, Version patch update 1.0.5_694
{: #105694_ca}

- Image tags: `1.19.1 105-1`, `1.20.0 105-1`, `1.21.0 105-1`, `1.22.0 105-1`, `1.23.0 105-1`
- Adds logging improvements.


### 16 May 2022, Version patch update 1.0.5_628
{: #105628_ca}

- Image tags: `1.19.1-105-0`, `1.20.0-105-0`, `1.21.0-105-0`, `1.22.0-105-0`, `1.23.0-105-0`
- Resolves [CVE-2022-28327](https://nvd.nist.gov/vuln/detail/cve-2022-28327){: external}, [CVE-2022-24675](https://nvd.nist.gov/vuln/detail/cve-2022-24675){: external}, and [CVE-2022-27536](https://nvd.nist.gov/vuln/detail/cve-2022-27536){: external}.
- Ignores label `ibm-cloud.kubernetes.io/vpc-instance-id` for zone balancing in satellite environments.
- Adds experimental option `balancingIgnoreLabelsFlag`. This option defines a node label that should be ignored when considering node group similarity. One label can be defined per option occurrence.


### 28 February 2022, Version patch update 1.0.5_415
{: #104415_ca}

Image tags: `1.19.1 9`, `1.20.0 9`, `1.21.0 5`, `1.22.0 3`
Adds support for Kubernetes 1.23


## Version 1.0.4
{: #0104_ca_addon}


### 23 February 2022, Version patch update 1.0.4_410
{: #104410_ca}

Image tags: `1.19.1 9`, `1.20.0 9`, `1.21.0 5`, `1.22.0 3`
Resolves the following CVEs: [CVE-2022-23772](https://nvd.nist.gov/vuln/detail/cve-2022-23772){: external}, [CVE-2022-23773](https://nvd.nist.gov/vuln/detail/cve-2022-23773){: external}, and [CVE-2022-23806](https://nvd.nist.gov/vuln/detail/cve-2022-23806){: external}.


### 20 January 2022, Version patch update 1.0.4_403
{: #104403_ca}

Review the changes in version `1.0.4_403` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.19.1-8`, `1.20.0-8`, `1.21.0-4`, and `1.22.0-2`.
- Supported cluster versions:  1.19.0 to 1.23.04.3
- Includes fixes for [CVE-2021-44716](https://nvd.nist.gov/vuln/detail/cve-2021-44716){: external} and [CVE-2021-44717](https://nvd.nist.gov/vuln/detail/cve-2021-44717){: external}. 


### 22 November 2021, Version patch update 1.0.4_387
{: #104387_ca}

Review the changes in version `1.0.4_387` of the cluster autoscaler add-on. 
{: shortdesc}

- Image tags: `1.19.1-7`, `1.20.0-7`, `1.21.0-3`, and `1.22.0-2`.
- Updates the Golang version to `1.16.10` which includes fixes for [CVE-2021-41772](https://nvd.nist.gov/vuln/detail/cve-2021-41772){: external} and [CVE-2021-41771](https://nvd.nist.gov/vuln/detail/cve-2021-41771){: external}.


### 7 October 2021, Version patch update 1.0.4_374
{: #104374_ca}

Review the changes in version `1.0.4_374` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.19.1-6`, `1.20.0-6`, `1.21.0-2`, and `1.22.0-1`.
- Adds support for Kubernetes version 1.22
- Pulls the base Golang image from a proxy registry.
- Adds an owner label to the `cluster-autoscaler` images.


Review the changes included in version 1.0.4 of the managed cluster autoscaler add-on.
{: shortdesc}


## Version 1.0.3
{: #0103_ca_addon}


### 26 August 2021, Version patch update 1.0.3_360
{: #103360_ca}

Review the changes in version `1.0.3_360` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags:  `1.17.4-5`, `1.18.3-5`, `1.19.1-5`, `1.20.0-5`, and `1.21.0-1`.  
- Supported cluster versions: 1.17 to 1.21>=4.3  
- Updates the Golang version to `1.16.6` which includes a fix for `PVR0281096`.  
- Increases the default resource requests and limits.
    - Previous values:
        ```yaml
        resourcesLimitsCPU: "600m"	    
        resourcesLimitsMemory: "600Mi"	     
        resourcesRequestsCPU: "200m"	      
        resourcesRequestsMemory: "200Mi"
        ```
        {: screen}	

    - Updated values:
        ```yaml
        resourcesLimitsCPU: "800m"
        resourcesLimitsMemory: "1000Mi"
        resourcesRequestsCPU: "200m"
        resourcesRequestsMemory: "400Mi"
        ```
        {: screen}


### 23 June 2021, Version patch update 1.0.3_352
{: #103352_ca}

Review the changes in version `1.0.3_352` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.17.4-4`, `1.18.3-4`, `1.19.1-4`, `1.20.0-4`, and `1.21.0-0`.   
- Supported cluster versions: 1.17 to 1.21>=4.3  
- Adds support for Kubernetes 1.21.  


Review the changes included in version 1.0.3 of the managed cluster autoscaler add-on.
{: shortdesc}


## Version 1.0.2
{: #0102_ca_addon}


### 10 May 2021, Version patch update 1.0.2_267
{: #102267_ca}

Review the changes in version `1.0.2_267` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.17.4-3`, `1.18.3-3`, `1.19.1-3`, and `1.20.0-3`.  
- Supported cluster versions: 1.17 <1.21.04.3 - 4.6  
- Includes a bug fix for the `worker replace` command on VPC clusters that caused worker creation to fail.  


### 19 April 2021, Version patch update 1.0.2_256 
{: #102256_ca}

Review the changes in version `1.0.2_256` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.17.4-2`, `1.18.3-2`, `1.19.1-2`, and `1.20.0-2`  
- Supported cluster versions: 1.17 - 1.204.3 - 4.6  
- Includes fixes for [CVE-2021-27919](https://nvd.nist.gov/vuln/detail/cve-2021-27919){: external} and [CVE-2021-27918](https://nvd.nist.gov/vuln/detail/cve-2021-27918){: external}.  


### 01 April 2021, Version patch update 1.0.2_249
{: #102249_ca}

Review the changes in version `1.0.2_249` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.16.7-1`, `1.17.4-1`, `1.18.3-1`, `1.19.1-1`, and `1.20.0-1`.  
- Supported cluster versions: 1.17 - 1.204.3 - 4.6  
- Includes fixes for [CVE-2021-3114](https://nvd.nist.gov/vuln/detail/cve-2021-3114){: external} and [CVE-2021-3115](https://nvd.nist.gov/vuln/detail/cve-2021-3114){: external}.  
- Removes the `init` container. In previous versions, the cluster autoscaler pods would remain in the `initContainer` state if the API key was missing or malformed. This update removes the `init` container so that if the API key is missing or malformed, the cluster autoscaler pod fails.  


### 09 March 2021, Version patch update 1.0.2_224
{: #10224_ca}

Review the changes in version `1.0.2_224` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.16.7-0`, `1.17.4-0`, `1.18.3-0`, `1.19.1-0`, and `1.20.0-0`.  
- Supported cluster versions: 1.17 - 1.204.3 - 4.6  
- Adds support for Kubernetes version 1.20.  


Review the changes that are in version 1.0.2 of the managed cluster autoscaler add-on.
{: shortdesc}


## Version 1.0.1
{: #0101_ca_addon}


### 16 February 2021, Version patch update 1.0.1_219
{: #101219_ca}

Review the changes in version `1.0.1_219` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.16.7-0` `1.17.4-0`, `1.18.3-0`, and `1.19.1-0`.  
- Supported cluster versions: 1.15.0 - 1.20.04.3 - 4.6  
- Updates the code base to synchronize with the community autoscaler. For more information, see the [Kubernetes autoscaler documentation](https://github.com/kubernetes/autoscaler/releases){: external}.  


### 13 January 2021, Version patch update 1.0.1_210
{: #101210_ca}

Review the changes in version `1.0.1_210` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.16.2-9`, `1.17.0-10`, `1.18.1-9`, and `1.19.0-4`.  
- Supported cluster versions: 1.15.0 - 1.20.04.3 - 4.6  
- Update addresses [`DLA-2509-1`](https://lists.debian.org/debian-lts-announce/2020/12/msg00039.html){: external}.  


### 15 December 2020, Version patch update 1.0.1_205
{: #101205_ca}

Review the changes in version `1.0.1_205` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.11.0-7`, `1.16.2-8`, `1.17.0-9`, `1.18.1-8`, and `1.19.0-3`.  
- Supported cluster versions: 1.15 - 1.194.3 - 4.6  
- Updates the `initContainer` to use the universal base image (UBI).  


### 10 December 2020, Version patch update 1.0.1_195
{: #101195_ca}

Review the changes in version `1.0.1_195` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.11.0-7`, `1.16.2-8`, `1.17.0-9`, `1.18.1-8`, and `1.19.0-3`.  
- Supported cluster versions: 1.15 - 1.194.3 - 4.6  
- Images are now signed.  
- Resources that are deployed by the cluster autoscaler add-on are now linked with the corresponding source code and build URLs.  
- Updates the Go version to `1.15.5`.  


### 03 December 2020, Version patch update 1.0.1_146
{: #101146_ca}

Review the changes in version `1.0.1_146` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.15.4-4`, `1.16.2-7`, `1.17.0-8`, `1.18.1-7`, and `1.19.0-2`.  
- Supported cluster versions: 1.15 - 1.194.3 - 4.6  
- Updates the cluster autoscaler to run as non-root.  
- Adds a feature to validate secrets before the autoscaler pods are initialized.  


### 27 October 2020, Version patch update 1.0.1_128
{: #101128_ca}

Review the changes in version `1.0.1_128` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.15.4-4`, `1.16.2-6`, `1.17.0-7`, `1.18.1-6`, and `1.19.0-1`.  
- Supported cluster versions: 1.15 - 1.194.3 - 4.5  
- Updates the Go version to `1.15.2`.  


### 16 October 2020, Version patch update 1.0.1_124
{: #101124_ca}

Review the changes in version `1.0.1_124` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.15.4-4`, `1.16.2-6`, `1.17.0-7`, `1.18.1-6`, and `1.19.0-1`.  
- Supported cluster versions: 1.15 - 1.194.3 - 4.5  
- Exposes the `--new-pod-scale-up-delay` option in the ConfigMap.  
- Adds support for Kubernetes 1.19.  


### 10 September 2020, Version patch update 1.0.1_114
{: #101114_ca}

Review the changes in version `1.0.1_114` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.15.4-4`, `1.16.2-5`, `1.17.0-6`, and `1.18.1-5`.  
- Supported cluster versions: 1.15 - 1.184.3 - 4.5  
- Includes fixes for `CVE-5188` and `CVE-3180`.  
- Unlike the previous Helm chart, you can modify all the add-on configuration settings via a single configmap.  


### 
Review the changes that are in version 1.0.1 of the managed cluster autoscaler add-on.  
{: shortdesc}
