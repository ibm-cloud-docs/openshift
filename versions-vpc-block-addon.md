---

copyright: 
  years: 2014, 2024
lastupdated: "2024-03-08"


keywords: openshift, block, storage, add-on, changelog

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# {{site.data.keyword.block_storage_is_short}} add-on change log 
{: #vpc_bs_changelog}


View information for patch updates to the {{site.data.keyword.block_storage_is_short}} add-on in your {{site.data.keyword.openshiftlong_notm}} clusters.
{: shortdesc}

Patch updates
:   Patch updates are delivered automatically by IBM and don't contain any feature updates or changes in the supported add-on and cluster versions.

Release updates
:   Release updates contain new features for the {{site.data.keyword.block_storage_is_short}} or changes in the supported add-on or cluster versions. You must manually apply release updates to your {{site.data.keyword.block_storage_is_short}} add-on. To update your {{site.data.keyword.block_storage_is_short}} add-on, see [Updating the {{site.data.keyword.block_storage_is_short}} add-on](/docs/openshift?topic=openshift-vpc-block#vpc-addon-update).


To view a list of add-ons and the supported cluster versions in the CLI, run the following command.
```sh
ibmcloud oc cluster addon versions --addon vpc-block-csi-driver
```
{: pre}

To view a list of add-ons and the supported cluster versions, see the [Supported cluster add-ons table](/docs/openshift?topic=openshift-supported-cluster-addon-versions).

Before you migrate to a `5.x` release from a previous release, you must not have any volume snapshots in `failure` state. For more information, see [Why can't I delete my Block Storage for VPC volume snapshot resources?](/docs/openshift?topic=openshift-ts-storage-volumesnapshotdelete).
{: important}


## Version 5.2
{: #052_is_block}

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



## Version 5.1
{: #051_is_block}

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

## Version 5.0
{: #050_is_block}

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




## Version 4.4
{: #044_is_block}

### Change log for version 4.4.17_1829, released 21 February 2023
{: #4.4.17_1829_is_block_relnote}

- Resolves [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}.

### Change log for version 4.4.16_1779, released 24 January 2023
{: #4.4.16_1779_is_block_relnote}

- Updates the storage-secret-sidecar image to `v1.2.15`.
- Resolves [CVE-2022-43680](https://nvd.nist.gov/vuln/detail/CVE-2022-43680){: external}, [CVE-2022-42010](https://nvd.nist.gov/vuln/detail/CVE-2022-42010){: external}, [CVE-2022-42011](https://nvd.nist.gov/vuln/detail/CVE-2022-42011){: external}, [CVE-2022-42012](https://nvd.nist.gov/vuln/detail/CVE-2022-42012){: external}, [CVE-2022-3821](https://nvd.nist.gov/vuln/detail/CVE-2022-3821){: external}, [CVE-2022-35737](https://nvd.nist.gov/vuln/detail/CVE-2022-35737){: external}, and [CVE-2021-46848](https://nvd.nist.gov/vuln/detail/CVE-2021-46848){: external}.


### Change log for version 4.4.15_1764, released 10 January 2023
{: #4.4.15_1764_is_block_relnote}

- Updates Golang to `1.18.9`.
- Updates the `storage-secret-sidecar` image to `v1.2.14`.
- Fixed volume tagging issue related to multiple tags.
- Resolves the following CVEs:
    - [CVE-2022-42898](https://nvd.nist.gov/vuln/detail/CVE-2022-42898){: external}
    - [CVE-2022-41717](https://nvd.nist.gov/vuln/detail/CVE-2022-41717){: external}
    - [CVE-2022-41720](https://nvd.nist.gov/vuln/detail/CVE-2022-41720){: external}

### Change log for version 4.4.13_1712, released 17 November 2022
{: #4.4.13_1712_is_block_relnote}

- Updates the `storage-secret-sidecar` image to `v1.2.12`
- Resolves the following CVEs: 
    - [CVE-2016-3709](https://nvd.nist.gov/vuln/detail/CVE-2016-3709){: external}
    - [CVE-2022-30698](https://nvd.nist.gov/vuln/detail/CVE-2022-30698){: external}
    - [CVE-2022-30699](https://nvd.nist.gov/vuln/detail/CVE-2022-30699){: external}
    - [CVE-2022-1304](https://nvd.nist.gov/vuln/detail/CVE-2022-1304){: external}

### Change log for version 4.4.12_1700, released 9 November 2022
{: #4.4.12_1700_is_block_relnote}

- Updates the `storage-secret-sidecar` image to `v1.2.10`, 
- Updates the `csi-node-driver-registrar` to `v2.5.0`
- Updates the `livenessprobe` to `v2.6.0`
- Updates the `csi-provisioner` to `v3.2.1`
- Updates the `csi-attacher` to `v3.5.0`
- Updates the `csi-resizer` to `v1.5.0`
- Resolves the following CVEs: [CVE-2022-37434](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-37434){: external}, [CVE-2022-2509](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-2509){: external}, [CVE-2022-40674](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-40674){: external}, [CVE-2020-35525](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-35525){: external}, [CVE-2020-35527](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-35527){: external}, [CVE-2022-3515](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-3515){: external}.


### Change log for version 4.4.11_1614, released 23 September 2022
{: #4.4.11_1614_is_block_relnote}

- Updates the `storage-secret-sidecar` image to `v1.2.8`.
- Updates the golang version to `1.18.6`.
- Resolves the following CVEs: [CVE-2022-27664](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-27664){: external}, [CVE-2022-32190](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-32190){: external}.



### Change log for version 4.4.10_1578, released 13 September 2022
{: #4.4.10_1578_is_block_relnote}

- Updates the `storage-secret-sidecar` image to `v1.2.7`
- Resolves the following CVEs: [CVE-2022-32206](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-32206){: external}, [CVE-2022-32208](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-32208){: external}, [CVE-2022-2526](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-2526){: external}.


### Change log for version 4.4.9_1566, released 25 August 2022
{: #4.4.9_1566_is_block_relnote}

- Updates Golang to version `1.18.5`
- Updates the `storage-secret-sidecar` image to `v1.2.6`
- Resolves the following CVEs: [CVE-2022-1586](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-1586){: external}, [CVE-2022-2068](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-2068){: external}, [CVE-2022-1292](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-1292){: external}, [CVE-2022-2097](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-2097){: external}. 

### Change log for version 4.4.8_1550, released 18 July 2022
{: #4.4.8_1550_is_block_relnote}

- Updates the `storage-secret-sidecar` image to `v1.2.5`
- Updates Golang to version `1.18.3`
- Updates UBI image to version `8.6-854`
- Fixes an issue where volume mounting on node fails with already mounted error.
- Resolves the following CVEs: [CVE-2022-29824](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-29824){: external}, [CVE-2021-40528](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-40528){: external}, [CVE-2022-22576](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-22576){: external}, [CVE-2022-27774](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-27774){: external}, [CVE-2022-27776](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-27776){: external}, [CVE-2022-27782](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-27782){: external}, [CVE-2022-25313](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-25313){: external}, [CVE-2022-25314](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-25314){: external}. 


### Change log for version 4.4.6_1446, released 24 June 2022
{: #4.4.6_1446_is_block_relnote}

- Includes an update where volume creation or expansion isn't retried if the provided volume capacity is not supported by volume profile.
- Updates the `storage-secret-sidecar` image to `v1.2.4`
- Resolves [CVE-2022-1271](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-1271){: external}
- Adds a security fix related with image signing.


### Change log for version 4.4.5_1371, released 13 June 2022
{: #445_1371_is_block_relnote}

- Adds support for IAM trusted profiles.
- Adds IAM token caching in memory for up to 40 minutes which reduces the number of calls to IAM and improves driver performance.
- Updates the `storage-secret-sidecar` image to `v1.2.3`.
- Fixes a volume expansion error handling issue.



## Version 4.3
{: #043_is_block}

### Change log for version 4.3.8_1705 released 11 November 2022
{: #4.3.8_1705_is_block_relnote}

- Updates the `storage-secret-sidecar` image to `v1.2.10`
- Updates the `csi-node-driver-registrar` to `v2.5.0`
- Updates the `livenessprobe` to `v2.6.0`
- Updates the `csi-provisioner` to `v3.2.1` 
- Updates the `csi-attacher` to `v3.5.0` 
- Updates the `csi-resizer` to `v1.5.0`
- Resolves the following CVEs: [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}, [CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external}, [CVE-2022-40674](https://nvd.nist.gov/vuln/detail/CVE-2022-40674){: external}, [CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external}, [CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external}, [CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external}


### Change log for version 4.3.7_1613, released 22 September 2022
{: #4.3.7_1613_is_block_relnote}

- Updates the `storage-secret-sidecar` image to `v1.1.15`.
- Updates the golang version to `1.18.6`.
- Resolves the following CVEs: [CVE-2022-27664](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-27664){: external} and [CVE-2022-32190](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-32190){: external}.


### Change log for version 4.3.6_1579, released 12 September 2022
{: #436_1579_is_block_relnote}

- Updates the `storage-secret-sidecar` image to `v1.1.14`
- Resolves the following CVEs: [CVE-2022-32206](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-32206){: external}, [CVE-2022-32208](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-32208){: external}, [CVE-2022-2526](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-2526){: external}.

### Change log for version 4.3.5_1563, released 24 August 2022
{: #435_1563_is_block_relnote}

- Updates Golang to version `1.18.5`
- Updates the `storage-secret-sidecar` image to `v1.1.13`
- Resolves the following CVEs: [CVE-2022-1586](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-1586){: external}, [CVE-2022-2068](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-2068){: external}, [CVE-2022-1292](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-1292){: external}, [CVE-2022-2097](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-2097){: external}. 


### Change log for version 4.3.4_1551, released 18 July 2022
{: #434_1551_is_block_relnote}


- Updates the `storage-secret-sidecar` image to `v1.1.12`
- Updates Golang to version `1.18.3`
- Updates UBI image to version `8.6-854`
- Improves secret watcher in case of secret update.
- Fixes an issue where volume mounting on node fails with already mounted error.
- Resolves the following CVEs: [CVE-2022-29824](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-29824){: external}, [CVE-2021-40528](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-40528){: external}, [CVE-2022-22576](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-22576){: external}, [CVE-2022-27774](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-27774){: external}, [CVE-2022-27776](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-27776){: external}, [CVE-2022-27782](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-27782){: external}, [CVE-2022-25313](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-25313){: external}, [CVE-2022-25314](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-25314){: external}.




### Change log for version 4.3.2_1441, released 17 June 2022
{: #432_1441_is_block_relnote}

- Added security fix related to image signing
- Updates the `storage-secret-sidecar` image to `v1.1.11`
- Resolves [CVE-2022-1271](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-1271){: external}

### Change log for version 4.3.0_1163, released 25 May 2022
{: #430_1163_is_block_relnote}

- Resolves the following CVEs: [CVE-2021-3634](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3634){: external}, [CVE-2021-3737](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3737){: external}, [CVE-2021-4189]https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-4189){: external}.
- Updates the `storage-secret-sidecar` image to `v1.1.10`
- Fixes Volume provisioning failure when in StorageClass Region is provided without zone info
- Fixes an issue where volume creation fails if only `failure-domain.beta.kubernetes.io/zone` is given in `allowedTopologies`
- `Region` support is now *DEPRECATED* in the storage class. Providing "region" detail in storage classes is deprecated in this release, this will not cause any issues with either existing PVC or new PVC. For now the default behavior is to get the region detail from the node label only which is now mandatory for all cases.

## Version 4.2
{: #042_is_block}


### Change log for version 4.2.6_1161, released 12 May 2022
{: #426_1161_is_block_relnote}

- Updates armada-storage-secret to `v1.1.10`
- Resolves the following CVEs: [CVE-2021-3634](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3634){: external}, [CVE-2021-3737](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3737){: external}, [CVE-2021-4189](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-4189){: external}.


### Change log for version 4.2.5_1106, released 12 May 2022
{: #425_1106_is_block_relnote}

- Updates armada-storage-secret to `v1.1.9`
- Updates the UBI version to `8.5-243.1651231653` 
- Resolves [CVE-2022-1271](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-1271){: external}.


### Change log for version 4.2.3_983, released 11 April 2022
{: #423_983_is_block_relnote}

- Updates armada-storage-secret to `v1.1.8`
- Resolves [CVE-2022-0778](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-0778){: external}.


### Change log for version 4.2.2_900, released 24 March 2022
{: #422_900_is_block_relnote}

- Updates armada-storage-secret to `v1.1.7`
- Resolves [CVE-2022-24921](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-24921){: external}.
- Update Golang to `1.16.15`


### Change log for version 4.2.1_895, released 17 March 2022
{: #421_895_is_block_relnote}

- Resolves [CVE-2022-24407](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-24407){: external}.
- Updates the `armada-storage-secret` to v1.1.6.



### Change log for version 4.2.0_890, released 28 February 2022
{: #420_890_is_block_relnote}

Updates in this version:
- Volume expansion support is now generally available.
- Removes unused variables `sizeRange` and `sizeIOPSRange` from storage classes.
- Makes `ibmc-vpc-block-10iops-tier` the default storage class via the new `addon-vpc-block-csi-driver-configmap` in the `kube-system` namespace.
- Resolves the following CVEs: [CVE-2021-3712](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3712){: external} and [CVE-2021-3521](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3521){: external}, [CVE-2022-23772](https://nvd.nist.gov/vuln/detail/CVE-2022-23772){: external}, [CVE-2022-23773](https://nvd.nist.gov/vuln/detail/CVE-2022-23773){: external}, and [CVE-2022-23806](https://nvd.nist.gov/vuln/detail/CVE-2022-23806){: external}.
- Updates Golang to version 1.16.14.
- All the storage classes that are installed with the add-on now have `allowVolumeExpansion=true`.

After updating to version 4.2, you must complete the following steps.
{: important}

* [Delete and recreate](/docs/openshift?topic=openshift-vpc-block#vpc-addon-update) any custom storage classes that are using the `sizeRange` or `iopsRange` parameters.
* If you use a default storage class other than `ibmc-vpc-block-10iops-tier`, you must change the `isStorageClassDefault` setting to `false` in the `addon-vpc-block-csi-driver-configmap` configmap in the `kube-system` namespace. For more information, see [Changing the default storage class](/docs/openshift?topic=openshift-vpc-block#vpc-block-default-edit).
    



## Version 4.1
{: #041_is_block}

Review the changes in version `4.1` of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

### Change log for version 4.1.3_846, released 14 February 2022
{: #413_846_is_block_relnote}

Review the changes in version `4.1.3_846` of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}    

- Resolves the following CVEs. 
    - [CVE-2021-3538](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3538){: external}
    - [CVE-2020-26160](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-26160){: external}

    

### Change log for version 4.1.2_834, released 27 January 2022
{: #412_834_is_block_relnote}

- Fixes an issue where the persistent volume watcher was unable to handle non-{{site.data.keyword.cloud_notm}} VPC CSI driver PV updates which caused the controller pod to crash.



### Change log for version 4.1.1_827, released 20 January 2022
{: #0411837_is_block_relnote}

Review the changes in version `4.1.1_827` of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdisc}

- Resolves the following CVEs.
    - [CVE-2021-44716](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44716){: external}
    - [CVE-2021-44717](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44717){: external}
- Updates Golang to version `1.16.13`.
- Updates the UBI image to version `8.5-218`.



### Change log for version 4.1.0_807, released 06 January 2022
{: #41_is_block_relnote}

Review the changes in version `4.1.0_807` of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: v4.1
- Resolves [CVE-2021-3712](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3712){: external}.
- Updates the storage-secret-sidecar image to version 1.1.4.
- Upgrades Kubernetes packages to version 1.21.
- Updates how api-key rotation is handled so that restarting the driver is no longer required.

## Version 4.0
{: #0400_is_block}

Review the changes in version `4.0` of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}


### Change log for version 4.0.3_793, released 22 November 2021
{: #403793_is_block_relnote}

Review the changes in version `4.0.3_793` of the {{site.data.keyword.block_storage_is_short}} add-on. 
{: shortdesc}

- Image tags: v4.0.3
- Image tags: v4.0.2
- Resolves the following CVEs.
    - [CVE-2021-41772](https://nvd.nist.gov/vuln/detail/CVE-2021-41772){: external}
    - [CVE-2021-41771](https://nvd.nist.gov/vuln/detail/CVE-2021-41771){: external}
    - [CVE-2021-22946](https://nvd.nist.gov/vuln/detail/CVE-2021-22946){: external}
    - [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947){: external}
    - [CVE-2021-33928](https://nvd.nist.gov/vuln/detail/CVE-2021-33928){: external}
    - [CVE-2021-33929](https://nvd.nist.gov/vuln/detail/CVE-2021-33929){: external}
    - [CVE-2021-33930](https://nvd.nist.gov/vuln/detail/CVE-2021-33930){: external}
    - [CVE-2021-33938](https://nvd.nist.gov/vuln/detail/CVE-2021-33938){: external}
    - [CVE-2021-3733](https://nvd.nist.gov/vuln/detail/CVE-2021-3733){: external}
- Updates the `storage-secret-sidecar` image to `v1.1.3`.
- Updates the default class policy from `Reconcile` to `EnsureExists` for  the `ibmc-vpc-block-10iops-tier` storage class.
- Updates Golang to version `1.16.10`.
- Updates the UBI image to version `8.4-205`.
- Increases the timeout interval for receiving API keys.


### Change log for version 4.0.1_780, released 06 October 2021
{: #0400780_is_block_relnote}

Review the changes in version `4.0.1_780` of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v4.0.1`
- Resolves the following CVEs.
    - [CVE-2021-22922](https://nvd.nist.gov/vuln/detail/CVE-2021-22922){: external}
    - [CVE-2021-22923](https://nvd.nist.gov/vuln/detail/CVE-2021-22923){: external}
    - [CVE-2021-22924](https://nvd.nist.gov/vuln/detail/CVE-2021-22924){: external}
    - [CVE-2021-36222](https://nvd.nist.gov/vuln/detail/CVE-2021-36222){: external}
    - [CVE-2021-37750](https://nvd.nist.gov/vuln/detail/CVE-2021-37750){: external}
- Updates the `storage-secret-sidecar` image to `v1.1.2`.
- Improves error messaging if `iks_token_exchange_endpoint_private_url` is invalid or unreachable.
- Adds [new storage classes for OpenShift Data Foundation](/docs/openshift?topic=openshift-vpc-block#vpc-block-reference).
- Updates to improve the volume attach/detach performance by avoiding unnecessary retries.
- Fixes an issue where mounting failed with `already mounted` error.
- Improves logging when the device path for a volume is not present on worker node.
- Adds the image label `compliance.owner="ibm-armada-storage"`. 



### Change log for version 4.0.0_769, released 16 September 2021
{: #0400769_is_block_relnote}

Review the changes in version `4.0.0_769` of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v4.0.0`
- Resolves the following CVEs:
    - [CVE-2021-27218](https://nvd.nist.gov/vuln/detail/CVE-2021-27218){: external}  
    - [CVE-2021-3520](https://nvd.nist.gov/vuln/detail/CVE-2021-3520){: external}  
    - [CVE-2021-20271](https://nvd.nist.gov/vuln/detail/CVE-2021-20271){: external}  
    - [CVE-2021-3516](https://nvd.nist.gov/vuln/detail/CVE-2021-3516){: external}  
    - [CVE-2021-3517](https://nvd.nist.gov/vuln/detail/CVE-2021-3517){: external}  
    - [CVE-2021-3518](https://nvd.nist.gov/vuln/detail/CVE-2021-3518){: external}  
    - [CVE-2021-3537](https://nvd.nist.gov/vuln/detail/CVE-2021-3537){: external}  
    - [CVE-2021-3541](https://nvd.nist.gov/vuln/detail/CVE-2021-3541){: external}  
    - [CVE-2021-33910](https://nvd.nist.gov/vuln/detail/CVE-2021-33910){: external}  
- Updates the `storage-secret-sidecar` image to `v1.1.0`.



### Change log for version 4.0, released 1 September 2021
{: #0400_is_block_relnote}

Review the changes in version `4.0.0_764` of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v4.0.0`
- Resolves [CVE-2021-27218](https://nvd.nist.gov/vuln/detail/CVE-2021-27218){: external}.
- Updates CSI sidecar images to fix [DLA-2542-1](https://lists.debian.org/debian-lts-announce/2021/02/msg00003.html){: external}, [DLA-2509-1](https://lists.debian.org/debian-lts-announce/2020/12/msg00039.html){: external}, and [DLA-2424-1](https://lists.debian.org/debian-lts-announce/2020/10/msg00037.html){: external}.
- Updates the sidecar images to the following versions.      
    - `csi-provisioner`: `icr.io/ext/sig-storage/csi-provisioner:v2.2.2`
    - `csi-resizer`: `icr.io/ext/sig-storage/csi-resizer:v1.2.0`
    - `csi-attacher`: `icr.io/ext/sig-storage/csi-attacher:v3.2.1`
    - `liveness-probe`: `icr.io/ext/sig-storage/livenessprobe:v2.3.0`
    - `csi-node-driver-registrar`: `icr.io/ext/sig-storage/csi-node-driver-registrar:v2.2.0`
- Updates the Golang version from `1.15.12` to `1.16.7`
- Increases the resources to the `csi-attacher`, `csi-resizer`, `csi-provisioner`, `ibm-vpc-block-csi-controller`, and `ibm-vpc-block-csi-node` plug-ins to fix containers crashing due to OOM issues.
- Improves volume attach/detach performance by increasing the worker thread count for the `csi-attacher` sidecar.
- Improves error messaging
- Fixes a bug related to unexpected IAM behavior.
- Changes the version numbering system to `X.X.Y_YYY` where `X.X` is the major version number and `.Y_YYY` is the patch version number.



## Version 3.0.1
{: #0301_is_block}

Review the changes in version `3.0.1` of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

### Change log for version 3.0.1, released 15 July 2021
{: #301_init}

Review the change log for version `3.0.1` of the {{site.data.keyword.block_storage_is_short}} add-on.

Volume expansion in version `3.0.1` is available in beta for allowlisted accounts. Don't use this feature for production workloads.
{: beta}

- Image tags: `v3.0.7`  
- Includes beta support for volume expansion on allowlisted accounts.  
- Fixes vulnerability [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}.  
- Includes the `storage-secret-sidecar` container in the {{site.data.keyword.block_storage_is_short}} driver pods.  

## Version 3.0.0
{: #0300_is_block}

Review the changes in version 3.0.0 of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

### Change log for patch update 3.0.0_521, released 01 April 2021
{: #3.0.0_521}

Review the changes in version 3.0.0_521 of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v3.0.7`  
- Updates the Golang version from `1.15.5` to `1.15.9`.  


### Change log for version 3.0.0, released 26 February 2021
{: #0300_is_block_relnote}

Review the changes in version 3.0.0_521 of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v.3.0.0`   
- The `vpc-block-csi-driver` is now available for both managed clusters and unmanaged clusters.   
- No functional changes in this release.  

## Archive
{: #unsupported_versions}

Find an overview of {{site.data.keyword.block_storage_is_short}} add-ons that are unsupported in IBM Cloud Kubernetes Service.

### Version 2.0.3
{: #0203_is_block}

Review the changes in version 2.0.3 of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

Version 2.0.3 is unsupported.
{: important}

#### Change log for patch update 2.0.3_471, released 26 January 2021
{: #0203471_is_block}

Review the changes in version 2.0.3_471 of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v.2.0.9`  
- Supported cluster versions: 4.3 - 4.6  
- Updated he `openssl`, `openssl-libs`, `gnutls` packages to fix [CVE-2020-1971](https://nvd.nist.gov/vuln/detail/CVE-2020-1971){: external} and [CVE-2020-24659](https://nvd.nist.gov/vuln/detail/CVE-2020-24659){: external}.  

#### Change log for patch update 2.0.3_464, released 10 December 2020
{: #0203464_is_block}

Review the changes in version 2.0.3_464 of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v2.0.8`  
- **New!**: Metro storage classes with the `volumeBindingMode:WaitForFirstConsumer` specification.  
- Resources that are deployed by the add-on now contain a label which links the source code URL and the build URL.  
- The `v2.0.8` image is signed.  
- Updates the Go version from `1.15.2` to `1.15.5`.  

#### Change log for patch update 2.0.3_404, released 25 November 2020
{: #0203404_is_block}

Review the changes in version 2.0.3_404 of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v2.0.7`   
- Fixes vulnerability scan issues.  
- Updates the base image from `alpine` to `UBI`.  
- Pods and containers now run as `non-root` except for the `node-server` pod's containers.  

#### Change log for patch update 2.0.3_375, released 17 September 2020
{: #0203375_is_block}

Review the changes in version 2.0.3_375 of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v2.0.6`   
- Fixes an issue with volume attachment when replacing workers.  

#### Change log for patch update 2.0.3_374+, released 29 August 2020
{: #0203374_is_block}

Review the changes in version 2.0.3_374+ of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v2.0.5`   
- Adds the `/var/lib/kubelet` path for CSI driver calls on OCP 4.4.  

#### Change log for patch update 2.0.3_365, released 05 August 2020
{: #203365_is_block}

Review the changes in version 2.0.3_365 of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v2.0.4`   
- Updates sidecar container images.  
- Adds liveness probe.  
- Enables parallel attachment and detachment of volumes to worker nodes. Previously, worker nodes were attached and detached sequentially.  
