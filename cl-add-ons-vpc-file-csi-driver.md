---

copyright:
  years: 2024, 2025

lastupdated: "2025-07-01"


keywords: change log, version history, VPC File CSI Driver

subcollection: "openshift"

---

{{site.data.keyword.attribute-definition-list}}




# VPC File CSI Driver add-on version change log
{: #cl-add-ons-vpc-file-csi-driver}

Review the version history for VPC File CSI Driver.
{: shortdesc}



## Version 2.0
{: #cl-add-ons-vpc-file-csi-driver-2.0}


### 2.0.13_370, released 16 June 2025
{: #cl-add-ons-vpc-file-csi-driver-2013_370}

- Resolves the following CVEs: [CVE-2025-0395](https://nvd.nist.gov/vuln/detail/CVE-2025-0395){: external}, [CVE-2025-3576](https://nvd.nist.gov/vuln/detail/CVE-2025-3576){: external}, and [CVE-2025-24528](https://nvd.nist.gov/vuln/detail/CVE-2025-24528){: external}.
- Updates Go to version `1.23.9`.
- Adds support for users to configure CPU and memory limits and requests for all file containers. 
- Fixes an issue where the provisioner and resizer containers were restarting due to the client rate-limiter. 
- Enables leader-election for csi-resizer. 
- Fixes a warning shown in PVC during volume expansion. 
- Improves error messages. 
- Updates k8s client libraries to 1.32. 
- {'Note': 'Users might see unwanted messages in file-csi-driver-status configmap.'} 

### 2.0.10_334, released 19 February 2025
{: #cl-add-ons-vpc-file-csi-driver-2010_334}

- Resolves the following CVEs: [CVE-2024-45339](https://nvd.nist.gov/vuln/detail/CVE-2024-45339){: external}, and [CVE-2024-45338](https://nvd.nist.gov/vuln/detail/CVE-2024-45338){: external}.
- Resiliency improvement to use VPC Storage service API for tagging volumes. This doesn't impact existing or new PVCs. This reduces the number of Kubernetes service API calls. 
- Updates the golang base image to 1.22.12. 
- Updates the armada-storage-secret to v1.2.55. 



## Version 1.2
{: #cl-add-ons-vpc-file-csi-driver-1.2}


### 1.2.14_332, released 19 February 2025
{: #cl-add-ons-vpc-file-csi-driver-1214_332}

- Resolves the following CVEs: [CVE-2024-45339](https://nvd.nist.gov/vuln/detail/CVE-2024-45339){: external}, and [CVE-2024-45338](https://nvd.nist.gov/vuln/detail/CVE-2024-45338){: external}.
- Resiliency improvement to use VPC Storage service API for tagging volumes. This doesn't impact existing or new PVCs. This reduces the number of Kubernetes service API calls. 
- Updates the golang base image to 1.22.12. 
- Updates the armada-storage-secret to v1.2.55. 



### Change log for version 2.0.9_322, released 11 December 2024
{: #2.0.9_322_is_file_relnote}


- `region` support is now deprecated in the storage class settings. Continuing to provide a `region` in your storage classes does not cause any issues with either existing PVC or new PVC. The default behavior is now to get the region detail from worker node labels only.
- Fixes a bug where setting default storage class was not working in version 4.15 clusters.
- Fixes [CVE-2024-51744](https://nvd.nist.gov/vuln/detail/CVE-2024-51744){: external}.
- Updates the `storage-secret-sidecar` image to `v1.2.52`.


### Change log for version 2.0.8_311, released 3 October 2024
{: #2.0.8_311_is_file_relnote}

- Updates the golang base image to `1.22.7`.
- Updates to Kubernetes 1.30 client libraries.
- Updates the CSI specification to version `1.9.0`.
- Fixes a security issue for the CSI sidecar liveness probe. The sidecar now runs as non-root in the Node Server pod.
- Adds the ability to set a default storage class. For more information, see [Setting the default storage class](/docs/openshift?topic=openshift-storage-file-vpc-apps#vpc-file-set-default-sc).
- Updates the following sidecar images: `csi-provisioner:v5.0.2`, `csi-resizer:v1.11.2`, `livenessprobe:v2.13.1`, and `csi-node-driver-registrar:v2.11.1`.
- Resolves [CVE-2024-2398](https://nvd.nist.gov/vuln/detail/CVE-2024-2398){: external}, [CVE-2024-37370](https://nvd.nist.gov/vuln/detail/CVE-2024-37370){: external}, [CVE-2024-37371](https://nvd.nist.gov/vuln/detail/CVE-2024-37371){: external}.

### Change log for version 2.0.6_259, released 26 August 2024
{: #2.0.6_259_is_file_relnote}

- Updates the golang image to `1.21.13-community`.

### Change log for version 2.0.5_253, released 15 July 2024
{: #2.0.5_253_is_file_relnote}

- Updates the golang image to `1.21.12-community`.
- Updates the `armada-storage-secret` to `v1.2.40`.
- Resolves [CVE-2024-28182](https://nvd.nist.gov/vuln/detail/CVE-2024-28182){: external} and [CVE-2023-2953](https://nvd.nist.gov/vuln/detail/CVE-2023-2953){: external}.

### Change log for version 2.0.4_232, released 3 July 2024
{: #2.0.4_232_is_file_relnote}

- Version 2.0 and later is managed via the `storage-operator` add-on which is installed by default on new 4.16 and later clusters. To update your add-on, see [Updating the {{site.data.keyword.filestorage_vpc_full_notm}} cluster add-on](/docs/openshift?topic=openshift-storage-file-vpc-managing).
- Adds support for encryption in-transit (EIT). EIT is disabled by default. For more information, see [Setting up encryption in-transit](/docs/openshift?topic=openshift-storage-file-vpc-apps#storage-file-vpc-eit).
- Adds support for tagging. File shares can now be cleaned up when deleting clusters by using the `--force-delete-storage` option on the `ibmcloud oc cluster rm` command.
- Adds new pre-defined storage classes. The previous storage classes are deprecated. Update your apps to use the new storage classes. For more information, see the [Migrating to a new storage class](/docs/openshift?topic=openshift-storage-file-vpc-apps#storage-file-expansion-migration).
- Adds functionality to track CSI driver major events. You can the add-on status by reviewing the `file-csi-driver-status` configmap in the `kube-system` namespace.
- Adds more attributes to persistent volume objects (PV) `FileShareID`, `FileShareTargetID`, `ENISubnetID`, `ENISecurityGroupIDs`.
- Adds retries for fileShare target creation in case of partial failure during PVC creation.
- Updates RBAC policies to use minimal privileges required.
- Updates golang to `1.21.11-community`.
- Known issues: [StorageClassSecres](https://kubernetes-csi.github.io/docs/secrets-and-credentials-storage-class.html#storageclass-secrets){: external} are not supported.





## Version 1.2
{: #012_is_file}

### Change log for version 1.2.13_326, released 11 December 2024
{: #1.2.13_326_is_file_relnote}

- Fixes [CVE-2024-51744](https://nvd.nist.gov/vuln/detail/CVE-2024-51744){: external}.
- Updates the `storage-secret-sidecar` image to `v1.2.52`.


### Change log for version 1.2.12_312, released 3 October 2024
{: #1.2.12_312_is_file_relnote}

- Updates the golang base image to `1.22.7`.
- Updates to Kubernetes 1.30 client libraries.
- Updates the CSI specification to version `1.9.0`.
- Fixes a security issue for the CSI sidecar liveness probe. The sidecar now runs as non-root in the Node Server pod.
- Updates the following sidecar images: `csi-provisioner:v5.0.2`, `csi-resizer:v1.11.2`, `livenessprobe:v2.13.1`, and `csi-node-driver-registrar:v2.11.1`.
- Resolves [CVE-2024-2398](https://nvd.nist.gov/vuln/detail/CVE-2024-2398){: external}, [CVE-2024-37370](https://nvd.nist.gov/vuln/detail/CVE-2024-37370){: external}, [CVE-2024-37371](https://nvd.nist.gov/vuln/detail/CVE-2024-37371){: external}.


### Change log for version 1.2.10_254, released 15 July 2024
{: #1.2.10_254_is_file_relnote}

- Updates the golang image to `1.21.12-community`.
- Updates the `armada-storage-secret` to `v1.2.40`.
- Resolves [CVE-2024-28182](https://nvd.nist.gov/vuln/detail/CVE-2024-28182){: external} and [CVE-2023-2953](https://nvd.nist.gov/vuln/detail/CVE-2023-2953){: external}.

### Change log for version 1.2.9_245, released 21 June 2024
{: #1.2.9_245_is_file_relnote}

- Updates `golang` to `1.21.11-community`.
- Updates the `armada-storage-secret` to `v1.3.8`.
- Resolves: [CVE-2024-26458](https://nvd.nist.gov/vuln/detail/CVE-2024-26458){: external}, [CVE-2024-26461](https://nvd.nist.gov/vuln/detail/CVE-2024-26461){: external}, [CVE-2024-33600](https://nvd.nist.gov/vuln/detail/CVE-2024-33600){: external}, [CVE-2024-33601](https://nvd.nist.gov/vuln/detail/CVE-2024-33601){: external}, [CVE-2024-33602](https://nvd.nist.gov/vuln/detail/CVE-2024-33602){: external}, [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-33602){: external}, and [CVE-2024-33599](https://nvd.nist.gov/vuln/detail/CVE-2024-33599){: external}.


### Change log for 1.2.8_174, released 10 May 2024
{: #1.2.8_174_is_file_relnote}

- Updates `golang` to `1.21.9-community`.
- Removes `curl` package from base image.
- Updates the `armada-storage-secret` to `v1.2.35`.
- Sets `handle-volume-inuse-error` flag to `false` in the `csi-resizer` to reduce costs associated with watching all pods in the cluster which can cause `OOM Killed` errors for the `csi-resizer`.
- Resolves [CVE-2023-46218](https://nvd.nist.gov/vuln/detail/CVE-2023-46218){: external}, [CVE-2023-28322](https://nvd.nist.gov/vuln/detail/CVE-2023-28322){: external}, and [CVE-2023-38546](https://nvd.nist.gov/vuln/detail/CVE-2023-38546){: external}.

### Change log for 1.2.7_154, released 08 March 2024
{: #1.2.7_154_is_file_relnote}

- Base image migrated from UBI to golang.

### Change log for version 1.2.6_130, released 08 February 2024
{: #1.2.6_130_is_file_relnote}


- Fixes hanging issue related to mounting and unmounting after node server restart.
- Introduces granular locking mounting and unmounting at the `targetPath` level.
- Disables the CSI NodeExpansion method as it is not required for the file share. The PVC can still be expanded.
- Changes how the IAM endpoint is determined for VPC Gen2 clusters.
- Upgrades Kubernetes client library to 1.28.
- Upgrades CSI spec to 1.8.0.
- Resolves the following CVEs: [CVE-2022-48560](https://nvd.nist.gov/vuln/detail/CVE-2022-48560){: external}, [CVE-2022-48564](https://nvd.nist.gov/vuln/detail/CVE-2022-48564){: external}, [CVE-2023-39615](https://nvd.nist.gov/vuln/detail/CVE-2023-39615){: external}, [CVE-2023-43804](https://nvd.nist.gov/vuln/detail/CVE-2023-43804){: external}, [CVE-2023-45803](https://nvd.nist.gov/vuln/detail/CVE-2023-45803){: external}, and [CVE-2023-5981](https://nvd.nist.gov/vuln/detail/CVE-2023-5981){: external}.
- Updates the following sidecar images: 
    - `armada-storage-secret` to `v1.2.31`.
    - `csi-node-driver-registrar` to `v2.9.3`.
    - `csi-provisioner` to `v3.6.3`.
    - `csi-resizer` to `v1.9.3`.
    - `livenessprobe` to `v2.11.0`.


### Change log for version 1.2.5_107, released 10 January 2024
{: #1.2.5_107_is_file_relnote}

- Resolves [CVE-2023-3446](https://nvd.nist.gov/vuln/detail/CVE-2023-3446){: external}, [CVE-2023-3817](https://nvd.nist.gov/vuln/detail/CVE-2023-3817){: external}, and [CVE-2023-5678](https://nvd.nist.gov/vuln/detail/CVE-2023-5678){: external}.
- Applies a security fix to use the correct socket path following SElinux policy module changes and CSI recommendations to use `/var/lib/kubelet/plugins/`.


### Change log for version 1.2.3_97, released 27 November 2023
{: #1.2.3_97_is_file_relnote}

- Updates Golang to `1.20.11`.
- Updates UBI image to `8.9.1029`.
- Updates the `armada-storage-secret` to `v1.2.29`.
- Resolves the following CVEs: [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/CVE-2023-22745){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [CVE-2023-40217](https://nvd.nist.gov/vuln/detail/CVE-2023-40217){: external}, and [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/CVE-2023-4641){: external}.

### Change log for version version 1.2.0, released 31 October 2023
{: #0120_is_file}


- Tiered and custom profile storage classes are no longer supported. Update your PVCs to use a `dp2` storage classes.
- Adds support for granular authorization via the Virtual Network Interface VNI (Elastic Network Interface ENI).
- Adds support for cross zone mounting by default. Pods can now mount storage volumes across zones.
- Allows you to bring your own security group to control granular authorization at the worker node, zone, or worker pool level.
- Adds bring your own subnet support to control which subnet the virtual network interface (VNI) IP for storage is assigned and created in.
- Adds bring your own IP support existing `PrimaryIP` which the VNI will assign.
- Allows you to set a custom `PrimaryIPAddress` within the subnet range where the VNI IP is assigned and created.


## Version 1.1
{: #011_is_file}

### Change log for version 1.1.10_93, released 27 November 2023
{: #1.1.10_93_is_file_relnote}

- Updates Golang to `1.20.11`.
- Updates UBI image to `8.9.1029`.
- Updates the `armada-storage-secret` to `v1.2.29`.
- Resolves the following CVEs: [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/CVE-2023-22745){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [CVE-2023-40217](https://nvd.nist.gov/vuln/detail/CVE-2023-40217){: external}, and [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/CVE-2023-4641){: external}.


### Change log for version 1.1.9_87, released 13 November 2023
{: #1.1.9_87_is_file_relnote}

- Updates the `storage-secret-sidecar` image to `1.2.27`.
- Updates Golang to `1.20.10`.
- Resolves [CVE-2023-44487](https://nvd.nist.gov/vuln/detail/CVE-2023-44487){: external}, [CVE-2023-4911](https://nvd.nist.gov/vuln/detail/CVE-2023-4911){: external}, [CVE-2023-4527](https://nvd.nist.gov/vuln/detail/CVE-2023-4527){: external}, [CVE-2023-4806](https://nvd.nist.gov/vuln/detail/CVE-2023-4806){: external}, [CVE-2023-4813](https://nvd.nist.gov/vuln/detail/CVE-2023-4813){: external}.


### Change log for version 1.1.7_49, released 14 September 2023
{: #1.1.7_is_file_relnote}

- Updates UBI image to `8.8-1037`.
- Updates Golang to `1.19.12`.
- Resolves the following CVEs: 
    - [CVE-2023-34969](https://nvd.nist.gov/vuln/detail/CVE-2023-34969){: external}, [CVE-2023-28321](https://nvd.nist.gov/vuln/detail/CVE-2023-28321){: external}, [CVE-2023-2602](https://nvd.nist.gov/vuln/detail/CVE-2023-2602){: external}, [CVE-2023-2603](https://nvd.nist.gov/vuln/detail/CVE-2023-2603){: external}, [CVE-2023-28484](https://nvd.nist.gov/vuln/detail/CVE-2023-28484){: external}, [CVE-2023-29469](https://nvd.nist.gov/vuln/detail/CVE-2023-29469){: external}, [CVE-2023-27536](https://nvd.nist.gov/vuln/detail/CVE-2023-27536){: external}, [CVE-2023-3899](https://nvd.nist.gov/vuln/detail/CVE-2023-3899){: external}, and [CVE-2023-32681](https://nvd.nist.gov/vuln/detail/CVE-2023-32681){: external}.



### Change log for version 1.1.6_41, release 28 July 2023
{: #1.1.6_is_file_relnote}

- Tiered storage classes are deprecated and will be unsupported soon. To migrate, create new PVCs and that use a `dp2` storage class and redeploy your apps.
- Updates for the VPC API compatibility changes. For more information, see the [VPC REST API change log](/docs/vpc?topic=vpc-api-change-log-beta#23-may-2023-beta)
- Adds support for `dp2` profiles.
- Updates the UBI to version `8.8-1014` to resolve the following CVEs: [CVE-2023-1667](https://nvd.nist.gov/vuln/detail/CVE-2023-1667){: external}, [CVE-2023-2283](https://nvd.nist.gov/vuln/detail/CVE-2023-2283){: external}, [CVE-2023-26604](https://nvd.nist.gov/vuln/detail/CVE-2023-26604){: external}, and [CVE-2020-24736](https://nvd.nist.gov/vuln/detail/CVE-2020-24736){: external}.
- Updates Golang to version `1.19.11` to resolve [CVE-2023-29406](https://nvd.nist.gov/vuln/detail/CVE-2023-29406){: external}.

### Change log for version 1.1, released 3 July 2023
{: #1.1_is_file_relnote}

- Updates the following sidecar images: 
    - `storage-secret-sidecar` to `v1.2.24`.
    - `csi-node-driver-registrar` to `v2.7.0`.
    - `livenessprobe` to `v2.9.0`.
    - `csi-provisioner` to `v3.4.1`.
    - `csi-resizer` to `v1.7.0`.

- Updates the UBI image `8.8-860`.
- Updates Golang to `1.19.10`.
- Resolves the following CVEs: 
    - [CVE-2023-29403](https://nvd.nist.gov/vuln/detail/CVE-2023-29403){: external},
    - [CVE-2023-29404](https://nvd.nist.gov/vuln/detail/CVE-2023-29404){: external}
    - [CVE-2023-29405](https://nvd.nist.gov/vuln/detail/CVE-2023-29405){: external}
    - [CVE-2023-29402](https://nvd.nist.gov/vuln/detail/CVE-2023-29402){: external} 
    - [CVE-2023-29400](https://nvd.nist.gov/vuln/detail/CVE-2023-29400){: external}
    - [CVE-2023-24540](https://nvd.nist.gov/vuln/detail/CVE-2023-24540){: external}
    - [CVE-2023-24539](https://nvd.nist.gov/vuln/detail/CVE-2023-24539){: external} 
    - [CVE-2022-43552](https://nvd.nist.gov/vuln/detail/CVE-2022-43552){: external}
    - [CVE-2022-3204](https://nvd.nist.gov/vuln/detail/CVE-2022-3204){: external}
    - [CVE-2023-27535](https://nvd.nist.gov/vuln/detail/CVE-2023-27535){: external}
    - [CVE-2022-36227](https://nvd.nist.gov/vuln/detail/CVE-2022-36227){: external}
    - [CVE-2022-35252](https://nvd.nist.gov/vuln/detail/CVE-2022-35252){: external}




### Change log for version 1.1-beta, released 15 May 2023
{: #1.1_beta_is_file_relnote}

- Kubernetes dependencies upgraded to `1.26.4`.
- Controller pods are now deployed as `Deployment`, in previous releases pods were deployed as `Satefulsets`.
- Adds the `priorityClass` in the deployment file for controller and node pods.

## Version 1.0
{: #01_is_file}


### Change log for version 1.0, released 16 May 2023
{: #1.0_is_file_relnote}

- Updates the UBI image to `8.7-1107`.
- Updates Golang to `1.19.8`.
- Resolves the following CVEs: [CVE-2023-2453](https://nvd.nist.gov/vuln/detail/CVE-2023-2453){: external}, [CVE-2023-24537](https://nvd.nist.gov/vuln/detail/CVE-2023-24537){: external}, [CVE-2023-24538](https://nvd.nist.gov/vuln/detail/CVE-2023-24538){: external}.
