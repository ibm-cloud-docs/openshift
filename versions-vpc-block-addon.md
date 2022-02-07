---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-07"

keywords: block, add-on, changelog

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.block_storage_is_short}} add-on changelog
{: #vpc_bs_changelog}

View information for patch updates to the {{site.data.keyword.block_storage_is_short}} add-on in your {{site.data.keyword.openshiftlong_notm}} clusters.
{: shortdesc}

Patch updates
:   Patch updates are delivered automatically by IBM and don't contain any feature updates or changes in the supported add-on and cluster versions.

Release updates
:   Release updates contain new features for the {{site.data.keyword.block_storage_is_short}} or changes in the supported add-on or cluster versions. You must manually apply release updates to your {{site.data.keyword.block_storage_is_short}} add-on. To update your {{site.data.keyword.block_storage_is_short}} add-on, see [Updating the {{site.data.keyword.block_storage_is_short}} add-on](/docs/openshift?topic=openshift-vpc-block#vpc-addon-update).


To view a list of add-ons and the supported cluster versions, run the following command.
```sh
ibmcloud oc cluster addon versions --addon vpc-block-csi-driver
```
{: pre}

Refer to the following tables for a summary of changes for each version of the {{site.data.keyword.block_storage_is_short}} add-on.

| {{site.data.keyword.block_storage_is_short}} add-on version | {{site.data.keyword.openshiftlong_notm}} version support |
| --- | --- |
| 4.1 (default) | All supported versions of {{site.data.keyword.openshiftlong_notm}} and unsupported versions that are version 4.3 or higher. |
| 4.0 | All supported versions of {{site.data.keyword.openshiftlong_notm}} and unsupported versions that are version 4.3 or higher. |
| 3.0.1 | All supported versions of {{site.data.keyword.openshiftlong_notm}} and unsupported versions that are version 4.3 or higher. |
| 3.0.0 | All supported versions of {{site.data.keyword.openshiftlong_notm}} and unsupported versions that are version 4.3 or higher. |
| 2.0.3 | Unsupported as of Kubernetes version 1.20. |
{: summary="The rows are read from left to right. The first column is the {{site.data.keyword.block_storage_is_short}} add-on version. The second column is the version of your cluster that the {{site.data.keyword.block_storage_is_short}} version is supported for."}

## Version 4.1
{: #041_is_block}

Review the changes in version `4.1` of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

### Changelog for version 4.1.2_834, released 27 January 2022
{: #412_834_is_block_relnote}

- Fixes an issue where the persistent volume watcher was unable to handle non-{{site.data.keyword.cloud_notm}} VPC CSI driver PV updates which caused the controller pod to crash.



### Changelog for version 4.1.1_827, released 20 January 2022
{: #0411837_is_block_relnote}

Review the changes in version `4.1.1_827` of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdisc}

- Resolves the following CVEs.
    - [CVE-2021-44716](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44716{: external}
    - [CVE-2021-44717](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44717{: external}
- Updates Golang to version `1.16.13`.
- Updates the UBI image to version `8.5-218`.



### Changelog for version 4.1.0_807, released 06 January 2022
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


### Changelog for version 4.0.3_793, released 22 November 2021
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


### Changelog for version 4.0.1_780, released 06 October 2021
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



### Changelog for version 4.0.0_769, released 16 September 2021
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



### Changelog for version 4.0, released 1 September 2021
{: #0400_is_block_relnote}

Review the changes in version `4.0.0_764` of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v4.0.0`
- Resolves [CVE-2021-27218](https://nvd.nist.gov/vuln/detail/CVE-2021-27218).
- Updates CSI sidecar images to fix [DLA-2542-1](https://www.debian.org/lts/security/2021/dla-2542), [DLA-2509-1](https://www.debian.org/lts/security/2020/dla-2509), and [DLA-2424-1](https://security-tracker.debian.org/tracker/DLA-2424-1).
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

### Changelog for version 3.0.1, released 15 July 2021
{: #301_init}

Review the changelog for version `3.0.1` of the {{site.data.keyword.block_storage_is_short}} add-on.

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

### Changelog for patch update 3.0.0_521, released 01 April 2021
{: #3.0.0_521}

Review the changes in version 3.0.0_521 of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v3.0.7`  
- Updates the Golang version from `1.15.5` to `1.15.9`.  


### Changelog for version 3.0.0, released 26 February 2021
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

#### Changelog for patch update 2.0.3_471, released 26 January 2021
{: #0203471_is_block}

Review the changes in version 2.0.3_471 of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v.2.0.9`  
- Supported cluster versions: 4.3 - 4.6  
- Updated he `openssl`, `openssl-libs`, `gnutls` packages to fix [CVE-2020-1971](https://nvd.nist.gov/vuln/detail/CVE-2020-1971){: external} and [CVE-2020-24659](https://nvd.nist.gov/vuln/detail/CVE-2020-24659){: external}.  

#### Changelog for patch update 2.0.3_464, released 10 December 2020
{: #0203464_is_block}

Review the changes in version 2.0.3_464 of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v2.0.8`  
- **New!**: Metro storage classes with the `volumeBindingMode:WaitForFirstConsumer` specification.  
- Resources that are deployed by the add-on now contain a label which links the source code URL and the build URL.  
- The `v2.0.8` image is signed.  
- Updates the Go version from `1.15.2` to `1.15.5`.  

#### Changelog for patch update 2.0.3_404, released 25 November 2020
{: #0203404_is_block}

Review the changes in version 2.0.3_404 of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v2.0.7`   
- Fixes vulnerability scan issues.  
- Updates the base image from `alpine` to `UBI`.  
- Pods and containers now run as `non-root` except for the `node-server` pod's containers.  

#### Changelog for patch update 2.0.3_375, released 17 September 2020
{: #0203375_is_block}

Review the changes in version 2.0.3_375 of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v2.0.6`   
- Fixes an issue with volume attachment when replacing workers.  

#### Changelog for patch update 2.0.3_374+, released 29 August 2020
{: #0203374_is_block}

Review the changes in version 2.0.3_374+ of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v2.0.5`   
- Adds the `/var/lib/kubelet` path for CSI driver calls on OCP 4.4.  

#### Changelog for patch update 2.0.3_365, released 05 August 2020
{: #203365_is_block}

Review the changes in version 2.0.3_365 of the {{site.data.keyword.block_storage_is_short}} add-on.
{: shortdesc}

- Image tags: `v2.0.4`   
- Updates sidecar container images.  
- Adds liveness probe.  
- Enables parallel attachment and detachment of volumes to worker nodes. Previously, worker nodes were attached and detached sequentially.  

