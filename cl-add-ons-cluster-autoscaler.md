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




### 16 February 2024, Version patch update 1.1.0_362
{: #110362_ca}

- Image tags: `1.21.0 110-10`, `1.22.0 110-10`, `1.23.0 110-10`, `1.24.0 110-10`, `1.25.0 110-10`.
- Updates `golang` version to `1.20.11`.




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
