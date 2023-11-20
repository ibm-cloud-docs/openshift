---

copyright: 
  years: 2014, 2023
lastupdated: "2023-11-20"

keywords: object storage, plug-in, change log

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# {{site.data.keyword.cos_full_notm}} plug-in 
{: #cos_plugin_changelog}


View information for updates to the {{site.data.keyword.cos_full_notm}} plug-in in your {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}


Refer to the following tables for a summary of changes for each version of the [{{site.data.keyword.cos_full_notm}} plug-in](/docs/openshift?topic=openshift-storage-cos-understand).

| {{site.data.keyword.cos_full_notm}} plug-in version | Supported? | {{site.data.keyword.redhat_openshift_notm}} version support | Supported architecture |
| --- | --- |--- | --- |
| 2.2.22 | Yes | Greater than or equal to 4.6 | x86 |
| 2.2.21 | Yes | Greater than or equal to 4.6 | x86 |
| 2.2.20 | Yes | Greater than or equal to 4.6 | x86 |
| 2.2.19 | Deprecated | Greater than or equal to 4.6 | x86 |
| 2.2.18 | Deprecated | Greater than or equal to 4.6 | x86 |
{: caption="{{site.data.keyword.cos_full_notm}} plug-in versions" caption-side="bottom"}

## Change log for version 2.2.22, released 20 November 2023
{: #02222_object_plugin}

- Updates Golang to `1.21.4`
- Updates UBI image to `8.9-1029`
- Resolves the following CVEs: [CVE-2023-22745](https://nvd.nist.gov/vuln/detail/CVE-2023-22745){: external}, [CVE-2007-4559](https://nvd.nist.gov/vuln/detail/CVE-2007-4559){: external}, [CVE-2023-40217](https://nvd.nist.gov/vuln/detail/CVE-2023-40217){: external}, [CVE-2023-4641](https://nvd.nist.gov/vuln/detail/CVE-2023-4641){: external}, [CVE-2023-45283](https://nvd.nist.gov/vuln/detail/CVE-2023-45283){: external}, and [CVE-2023-45284](https://nvd.nist.gov/vuln/detail/CVE-2023-45284){: external}.

## Change log for version 2.2.21, released 13 November 2023
{: #02221_object_plugin}


- Updates Golang to `1.21.3`
- Updates the `ibmc` plug-in to create the deployment namespace with privileged labels to enforce Pod Security Standards.
- Updates s3fs fuse to `v1.93`



## Change log for version 2.2.20, released 30 October 2023
{: #02220_object_plugin}

- Updates UBI to `8.8-1072.1697626218` to fix [CVE-2023-44487](https://nvd.nist.gov/vuln/detail/CVE-2023-44487){: external}.
- Updates to fix [CVE-2023-39325](https://nvd.nist.gov/vuln/detail/CVE-2023-39325){: external}.


## Change log for version 2.2.19, released 12 October 2023
{: #02219_object_plugin}

- Updates UBI image to `8.8-1072`
- Resolves the following CVEs: [CVE-2023-29491](https://nvd.nist.gov/vuln/detail/CVE-2023-29491){: external}, [CVE-2023-4911](https://nvd.nist.gov/vuln/detail/CVE-2023-4911){: external}, [CVE-2023-4527](https://nvd.nist.gov/vuln/detail/CVE-2023-4527){: external}, [CVE-2023-4806](https://nvd.nist.gov/vuln/detail/CVE-2023-4806){: external}, and [CVE-2023-4813](https://nvd.nist.gov/vuln/detail/CVE-2023-4813){: external}.


## Change log for version 2.2.18, released 7 September 2023
{: #02218_object_plugin}

- Adds support for RHCOS `4.13`.
- Updates Golang to `1.19.12`.
- Updates UBI image to `8.8-1037`.
- Resolves the following CVEs: [CVE-2023-29409](https://nvd.nist.gov/vuln/detail/CVE-2023-29409), [CVE-2023-27536](https://nvd.nist.gov/vuln/detail/CVE-2023-27536), [CVE-2023-2602](https://nvd.nist.gov/vuln/detail/CVE-2023-2602), [CVE-2023-2603](https://nvd.nist.gov/vuln/detail/CVE-2023-2603), [CVE-2023-34969](https://nvd.nist.gov/vuln/detail/CVE-2023-34969), [CVE-2023-28321](https://nvd.nist.gov/vuln/detail/CVE-2023-28321), [CVE-2023-28484](https://nvd.nist.gov/vuln/detail/CVE-2023-28484), and [CVE-2023-29469](https://nvd.nist.gov/vuln/detail/CVE-2023-29469).


## Change log for version 2.2.17, released 3 July 2023
{: #02217_object_plugin}

- Updates Golang to `1.19.11`.
- Updates UBI image to `8.8-1014`.
- Resolves the following CVEs: [CVE-2023-29406](https://nvd.nist.gov/vuln/detail/CVE-2023-29406){: external}, [CVE-2020-24736](https://nvd.nist.gov/vuln/detail/CVE-2020-24736){: external}, [CVE-2023-1667], [CVE-2023-2283](https://nvd.nist.gov/vuln/detail/CVE-2023-2283){: external}, and [CVE-2023-26604](https://nvd.nist.gov/vuln/detail/CVE-2023-26604){: external}.


## Change log for version 2.2.16, released 3 July 2023
{: #02216_object_plugin}

- Adds support for auto creation and deletion of user defined bucket names.

## Change log for version 2.2.15, released 19 June 2023
{: #02215_object_plugin}

- Updates UBI image to `8.8-860`.
- Updates Golang to `1.19.10`.
- Resolves the following CVEs: [CVE-2023-29401](https://nvd.nist.gov/vuln/detail/CVE-2023-29401){: external}, [CVE-2023-26125](https://nvd.nist.gov/vuln/detail/CVE-2023-26125){: external}, [CVE-2022-3172](https://nvd.nist.gov/vuln/detail/CVE-2022-3172){: external},[CVE-2023-29403](https://nvd.nist.gov/vuln/detail/CVE-2023-29403){: external}, [CVE-2023-29404](https://nvd.nist.gov/vuln/detail/CVE-2023-29404){: external}, [CVE-2023-29405](https://nvd.nist.gov/vuln/detail/CVE-2023-29405){: external}, [CVE-2023-29402](https://nvd.nist.gov/vuln/detail/CVE-2023-29402){: external}, [CVE-2023-29400](https://nvd.nist.gov/vuln/detail/CVE-2023-29400){: external}, [CVE-2023-24540](https://nvd.nist.gov/vuln/detail/CVE-2023-24540){: external}, [CVE-2023-24539](https://nvd.nist.gov/vuln/detail/CVE-2023-24539){: external}, [CVE-2022-43552](https://nvd.nist.gov/vuln/detail/CVE-2022-43552){: external}, [CVE-2022-3204](https://nvd.nist.gov/vuln/detail/CVE-2022-3204){: external}, [CVE-2023-27535](https://nvd.nist.gov/vuln/detail/CVE-2023-27535){: external}, [CVE-2022-36227](https://nvd.nist.gov/vuln/detail/CVE-2022-36227){: external}, and [CVE-2022-35252](https://nvd.nist.gov/vuln/detail/CVE-2022-35252){: external}.

## Change log for version 2.2.14, released 02 May 2023
{: #02214_object_plugin}

- Updates the UBI image to `8.7-1107`.
- Updates Golang to `1.19.8`.
- Resolves the following CVEs: [CVE-2023-0361](https://nvd.nist.gov/vuln/detail/CVE-2023-0361){: external}, [CVE-2023-24536](https://nvd.nist.gov/vuln/detail/CVE-2023-24536){: external}, [CVE-2023-24537](https://nvd.nist.gov/vuln/detail/CVE-2023-24537){: external}, [CVE-2023-24538](https://nvd.nist.gov/vuln/detail/CVE-2023-24538){: external}.

## Change log for version 2.2.13, released 03 April 2023
{: #02213_object_plugin}

- Updates the UBI image to `8.7-1085.1679482090`.
- Resolves the following CVEs: [CVE-2022-4304](https://nvd.nist.gov/vuln/detail/CVE-2022-4304){: external}, [CVE-2022-4450](https://nvd.nist.gov/vuln/detail/CVE-2022-4450){: external}, [CVE-2023-0215](https://nvd.nist.gov/vuln/detail/CVE-2023-0215){: external}, [CVE-2023-0286](https://nvd.nist.gov/vuln/detail/CVE-2023-0286){: external}.

Because this update affects regional storage classes, you must uninstall and reinstall the `2.2.13` chart so the new storage classes are created in your cluster. This change primarily impacts single site clusters because the regional storage classes, such as `ibmc-s3fs-standard-regional`, now point to the single site COS endpoint instead of the regional endpoints. This change is not applied automatically to existing PVCs and pods. You must create new PVCs with the new storage classes for the changes to take effect. For more information on how to update your PVCs, refer to the [Adding object storage to apps](/docs/containers?topic=containers-storage_cos_apps) documentation.
{: important}


## Change log for version 2.2.12, released 20 March 2023
{: #02212_object_plugin}

- Updates Golang to `1.19.7`.
- Resolves the following CVEs: [CVE-2023-24532](https://nvd.nist.gov/vuln/detail/CVE-2023-24532){: external}, [CVE-2022-41722](https://nvd.nist.gov/vuln/detail/CVE-2022-41722){: external}, [CVE-2022-41725](https://nvd.nist.gov/vuln/detail/CVE-2022-41725){: external}, [CVE-2023-23916](https://nvd.nist.gov/vuln/detail/CVE-2023-23916){: external}.

## Change log for version 2.2.11, released 03 March 2023
{: #02211_object_plugin}

- Updates Golang to `1.19.6`.
- Updates the UBI Image to `8.7-1085`.
- Updates s3fs fuse to [`d1388ff`](https://github.com/s3fs-fuse/s3fs-fuse/commit/d1388ff446b74e82483f8a09b1d576cd958d4d64){: external}.
- Resolves the following CVEs: [CVE-2022-41723](https://nvd.nist.gov/vuln/detail/CVE-2022-41723){: external}, [CVE-2022-41724](https://nvd.nist.gov/vuln/detail/CVE-2022-41724){: external}, [CVE-2022-4415](https://nvd.nist.gov/vuln/detail/CVE-2022-4415){: external}, [CVE-2020-10735](https://nvd.nist.gov/vuln/detail/CVE-2020-10735){: external}, [CVE-2021-28861](https://nvd.nist.gov/vuln/detail/CVE-2021-28861){: external}, [CVE-2022-45061](https://nvd.nist.gov/vuln/detail/CVE-2022-45061){: external}, [CVE-2022-40897](https://nvd.nist.gov/vuln/detail/CVE-2022-40897){: external}.

## Change log for version 2.2.10, released 21 February 2023
{: #02210_object_plugin}

- Updates the UBI Image to `8.7-1049.1675784874`.
- Updates the default values for `CPU request` and `CPU limit` to `100m` and `500m` respectively.
- Updates the default values for `Memory request` and `Memory limit1` to `128Mi` and `500Mi` respectively.
- Resolves [CVE-2022-47629](https://nvd.nist.gov/vuln/detail/CVE-2022-47629){: external}.


## Change log for version 2.2.9, released 13 February 2023
{: #0229_object_plugin}

- Adds support for the `--set allowCrossNsSecret=true/false` option when you install the {{site.data.keyword.cos_full_notm}} plug-in. For more information, see [Installing the {{site.data.keyword.cos_full_notm}} plug-in](/docs/containers?topic=containers-storage_cos_install).
- Adds support for `Wasabi` and `AWS` s3 providers on {{site.data.keyword.satelliteshort}} clusters.
- On {{site.data.keyword.satelliteshort}} clusters, the `object store endpoint` is now auto populated based on the `cos.storageClass` and `s3provider` options.


## Change log for version 2.2.8, released 23 January 2023
{: #0228_object_plugin}

- Updates the UBI Image to `8:8.7-1049`
- Adds `PriorityClasses` for driver and plug-in pods
- Updates tolerations for plug-in pod
- Adds support for encrypting buckets with {{site.data.keyword.keymanagementservicelong_notm}} by using your root key CRN when creating buckets.
- Resolves the following CVEs: [CVE-2022-43680](https://nvd.nist.gov/vuln/detail/CVE-2022-43680){: external}, [CVE-2022-42010](https://nvd.nist.gov/vuln/detail/CVE-2022-42010){: external}, [CVE-2022-42011](https://nvd.nist.gov/vuln/detail/CVE-2022-42011){: external}, [CVE-2022-42012](https://nvd.nist.gov/vuln/detail/CVE-2022-42012){: external}, [CVE-2022-3821](https://nvd.nist.gov/vuln/detail/CVE-2022-3821){: external}, [CVE-2022-35737](https://nvd.nist.gov/vuln/detail/CVE-2022-35737){: external}, [CVE-2021-46848](https://nvd.nist.gov/vuln/detail/CVE-2021-46848){: external}. 


## Change log for version 2.2.7, released 5 January 2023
{: #0227_object_plugin}

- Renames `flex` StorageClasses to `Smart` StorageClasses
- Updates GoLang to `1.18.9`
- Resolves [CVE-2022-41717](https://nvd.nist.gov/vuln/detail/CVE-2022-41717){: external} and [CVE-2022-41720](https://nvd.nist.gov/vuln/detail/CVE-2022-41720){: external}

Because this change affects storage classes, you must uninstall and reinstall the 2.2.7 chart so the new storage classes are created in your cluster. This change is not automatically applied to existing PVCs and pods. You must create new PVCs with the new storage classes for the changes to take effect.
{: important}

## Change log for version 2.2.6, released 15 December 2022
{: #0226_object_plugin}

- Updates the `tls-cipher-suite` value to `default` in all the s3fs storage classes for all {{site.data.keyword.redhat_openshift_notm}} clusters.
- Updates the `tls-cipher-suite` value to `AESGCM` for all Kubernetes clusters.
- If you want to overwrite the value from `default` to any other specific `tls-cipher-suite`, annotate your PVC with `ibm.io/tls-cipher-suite: "<cipher-suite-value>"`. 

Because this change affects storage classes, you must uninstall and reinstall the 2.2.6 chart so the new storage classes are created in your cluster. This change is not automatically applied to existing PVCs and pods. You must create new PVCs with the new storage classes for the changes to take effect.
{: important}

## Change log for version 2.2.5, released 9 December 2022
{: #0225_object_plugin}

- Updates the UBI image to `8.7-923.1669829893`

## Change log for version 2.2.4, released 5 December 2022
{: #0224_object_plugin}

- Updates Golang to `1.18.8`
- Resolves [CVE-2022-41715](https://nvd.nist.gov/vuln/detail/CVE-2022-41715){: external}, [CVE-2022-2879](https://nvd.nist.gov/vuln/detail/CVE-2022-2879){: external}, [CVE-2022-2880](https://nvd.nist.gov/vuln/detail/CVE-2022-2880){: external}

## Change log for version 2.2.3, released 15 November 2022
{: #0223_object_plugin}

- Updates the UBI image to `8.7-923`
- Resolves [CVE-2016-3709](https://nvd.nist.gov/vuln/detail/CVE-2016-3709){: external}, [CVE-2022-30698](https://nvd.nist.gov/vuln/detail/CVE-2022-30698){: external}, [CVE-2022-30699](https://nvd.nist.gov/vuln/detail/CVE-2022-30699){: external}, [CVE-2022-1304](https://nvd.nist.gov/vuln/detail/CVE-2022-1304){: external}.


## Change log for version 2.2.2, released 8 November 2022
{: #0222_object_plugin}

- Updates the UBI image to `8.6-994`.
- Resolves [CVE-2022-37434](https://nvd.nist.gov/vuln/detail/CVE-2022-37434){: external}, [CVE-2020-35525](https://nvd.nist.gov/vuln/detail/CVE-2020-35525){: external}, [CVE-2020-35527](https://nvd.nist.gov/vuln/detail/CVE-2020-35527){: external}, [CVE-2022-3515](https://nvd.nist.gov/vuln/detail/CVE-2022-3515){: external}, [CVE-2022-2509](https://nvd.nist.gov/vuln/detail/CVE-2022-2509){: external}, [CVE-2022-40674](https://nvd.nist.gov/vuln/detail/CVE-2022-40674){: external}.

## Change log for version 2.2.1, released 20 September 2022
{: #0221_object_plugin}

- Updates the UBI image to `8.6-941`
- Updates Golang `1.18.6` 
- Resolves [CVE-2022-27664](https://nvd.nist.gov/vuln/detail/CVE-2022-27664){: external}

## Change log for version 2.2.0, released 12 September 2022
{: #0220_object_plugin}

- Updates the UBI image to `8.6-902.1661794353`
- Resolves [CVE-2022-32206](https://nvd.nist.gov/vuln/detail/CVE-2022-32206){: external}, [CVE-2022-32208](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-32208){: external}, [CVE-2022-2526](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-2526){: external}.
- Cloud Pak certification renewed for the plug-in

## Change log for version 2.1.21, released 24 August 2022
{: #02121_object_plugin}

- Updates Golang to `1.18.5`
- Updates the UBI image to `8.6-902`
- Resolves [CVE-2022-1962](https://nvd.nist.gov/vuln/detail/CVE-2022-1962){: external}, [CVE-2022-1586](https://nvd.nist.gov/vuln/detail/CVE-2022-1586){: external}, [CVE-2022-2068](https://nvd.nist.gov/vuln/detail/CVE-2022-2068){: external}, [CVE-2022-1292](https://nvd.nist.gov/vuln/detail/CVE-2022-1292){: external}, [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external}.

## Change log for version 2.1.20, released 17 August 2022
{: #02120_object_plugin}

Adds support for RHEL 8.

## Change log for version 2.1.19, released 27 July 2022
{: #02119_object_plugin}

Updates the following mount paths for the driver pods.
    - Mounts `/etc/os-release` or `/etc/lsb-release` as read only.
    - Mounts `/etc/kubernetes` instead of `/etc` or `/usr/libexec/kubernetes` to install the `FlexVolume` binary.
    - Mounts `/usr/local/bin` instead of `/usr/local` to install the `s3fs` binary.

## Change log for version 2.1.18, released 14 July 2022
{: #02118_object_plugin}

- Updates the UBI Image to `8.6-854` 
- Resolves [CVE-2022-29824](https://nvd.nist.gov/vuln/detail/CVE-2022-29824){: external}, [CVE-2021-40528](https://nvd.nist.gov/vuln/detail/CVE-2021-40528){: external}, [CVE-2022-22576](https://nvd.nist.gov/vuln/detail/CVE-2022-22576){: external}, [CVE-2022-27774](https://nvd.nist.gov/vuln/detail/CVE-2022-27774){: external}, [CVE-2022-27776](https://nvd.nist.gov/vuln/detail/CVE-2022-27776){: external}, [CVE-2022-27782](https://nvd.nist.gov/vuln/detail/CVE-2022-27782){: external}, [CVE-2022-25313](https://nvd.nist.gov/vuln/detail/CVE-2022-25313){: external}, [CVE-2022-25314] (https://nvd.nist.gov/vuln/detail/CVE-2022-25314){: external}
- Updates Golang to `1.18.3`


## Change log for version 2.1.17, released 28 June 2022
{: #02117_object_plugin}

- Updates the UBI to `8.6-751.1655117800`
- Updates `s3fs-fuse` fix a `segfault` issue.
- Adds support to configure ephemeral storage of plug-in and driver pods.

## Change log for version 2.1.16, released 25 May 2022
{: #02116_object_plugin}

- Updates the UBI to `8.6-751`
- Added support for adding `ips` by using PVC annotation for `configBucketAccess`
- Added support for `crftoken` to be fetched from `storage-secret-store`

## Change log for version 2.1.15, released 6 May 2022
{: #02115_object_plugin}

- Updates the UBI to `8.5-243.1651231653`
- Resolves [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}
- Updates GoLang to `1.17.9`

## Change log for version 2.1.14, released 13 April 2022
{: #02114_object_plugin}

- Updates the UBI to `8.5-240.1648458092` 
- Resolves [CVE-2022-0778](https://nvd.nist.gov/vuln/detail/CVE-2022-0778){: external}
- Added support for two stable versions of s3fs fuse in one chart release
- Added support for quota-limit option for COS buckets by using s3fs plug-in
- Includes the `ibmc` plug-in version `2.0.8`

## Change log for version 2.1.13, released 24 March 2022
{: #02113_object_plugin}

- Updates the UBI to `8.5-240`
- Updates Golang to `v1.16.15`
- Resolves [CVE-2022-24921](https://nvd.nist.gov/vuln/detail/CVE-2022-24921){: external}, and [CVE-2022-23852](https://nvd.nist.gov/vuln/detail/CVE-2022-23852){: external}.
- Updates s3fs fuse to `v1.91`.
- Adds support for additional mount options `Ex: ibm.io/add-mount-param: "del_cache,retries=6"`.
- Fixes a bug where `mixupload` returns `EntityTooSmall` when a `copypart` is less than 5MB after split.


## Change log for version 2.1.12, released 11 March 2022
{: #02112_object_plugin}

- Updates the UBI to `8.5-230.1645809059`
- Resolves [CVE-2022-24407](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-24407){: external}


## Change log for version 2.1.11, released 1 March 2022
{: #02111_object_plugin}

- Update Go to version 1.16.14
- Resolves [CVE-2022-23772](https://nvd.nist.gov/vuln/detail/CVE-2022-23772){: external}, [CVE-2022-23773](https://nvd.nist.gov/vuln/detail/CVE-2022-23773){: external}, [CVE-2022-23806](https://nvd.nist.gov/vuln/detail/CVE-2022-23806){: external}



## Change log for version 2.1.10, released 17 February 2022
{: #02110_object_plugin}


- Updates the universal base image (UBI) to `ubi-minimal:8.5-230`.
- Resolves the following CVEs: [CVE-2021-3538](https://nvd.nist.gov/vuln/detail/CVE-2021-3538){: external}, [CVE-2018-14632](https://nvd.nist.gov/vuln/detail/CVE-2018-14632){: external}, [CVE-2020-26160](https://nvd.nist.gov/vuln/detail/CVE-2020-26160){: external}.
- Fixes a bug where the `kubernetes.io/secret/res-conf-apikey` was present in some logs.



## Change log for version 2.1.9, released 24 January 2022
{: #0219_object_plugin}

- [CVE-2021-44716](https://nvd.nist.gov/vuln/detail/CVE-2021-44716){: external}
- [CVE-2021-44717](https://nvd.nist.gov/vuln/detail/CVE-2021-44717){: external}



## Change log for version 2.1.8, released 17 January 2022
{: #0218_object_plugin}

- Updates the UBI to version `8.5-218`.
- Resolves [CVE-2021-3712](https://nvd.nist.gov/vuln/detail/CVE-2021-3712){: external}.
- Fixes an issue that prevented masking keys in the PVC logs.

## Change log for version 2.1.7, released 18 November 2021
{: #0217_object_plugin}

- Updates the UBI to version 8.5-204.
- Updates Golang to version 1.16.10.
- Resolves [CVE-2021-41772](https://nvd.nist.gov/vuln/detail/CVE-2021-41772){: external}, [CVE-2021-41771](https://nvd.nist.gov/vuln/detail/CVE-2021-41771){: external}, and [CVE-2021-22947](https://nvd.nist.gov/vuln/detail/CVE-2021-22947){: external}.


## Change log for version 2.1.6, released 22 October 2021
{: #0216_object_plugin}

- Image tags: `1.8.36`
- Updates s3fs fuse to version 1.90
- Updates dependencies


## Change log for version 2.1.5, released 5 October 2021
{: #0215_object_plugin}

- Image tags: `1.8.34`
- Resolves [CVE-2021-36221](https://nvd.nist.gov/vuln/detail/CVE-2021-36221){: external}, [CVE-2021-29923](https://nvd.nist.gov/vuln/detail/CVE-2021-29923){: external}, and [CVE-2021-33196](https://nvd.nist.gov/vuln/detail/CVE-2021-33196){: external}.
- Updates the UBI to `8.4-210`.
- Includes the `ibmc` plug-in version `2.0.7`.
- Pulls the Golang base image from artifactory.
- Includes endpoint updates for `jp-tok` and `uk-south`. 
- Updates location constraints for Sao Paulo 01. New constraints are `br-sao-standard`, `br-sao-vault`, `br-sao-cold`, and `br-sao-smart`. For more information, see [Storage classes](/docs/cloud-object-storage?topic=cloud-object-storage-classes).
- Allows deployments to the `kube-system` namespace when `bucketAccessPolicy` is enabled.
- Supports dynamic provisioning for non-default regions in AWS s3 instance.

## Change log for version 2.1.4, released 1 September 2021
{: #0214_object_plugin}

- Image tags: `1.8.33`
- Fixes a `timeoutSeconds` issue in the `livenessProbe` and `readinessProbe`.
- Updates the Golang version to `v1.17`.
- Updates the UBI image to `8.4-208`.
- Migrates the image from the `ibmcom` public registry to the `icr.io/cpopen` registry.
- Resolves [CVE-2021-36221](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-36221){: external}, [CVE-2021-29923](https://nvd.nist.gov/vuln/detail/CVE-2021-29923){: external}, and [CVE-2021-33196](https://nvd.nist.gov/vuln/detail/CVE-2021-33196){: external}.


## Change log for version 2.1.3, released 25 August 2021
{: #0213_object_plugin}

- Image tags: `1.8.32`
- Addresses the following CVEs: [CVE-2021-3520](https://nvd.nist.gov/vuln/detail/CVE-2021-3520){: external}, [CVE-2021-3516](https://nvd.nist.gov/vuln/detail/CVE-2021-3516){: external}, [CVE-2021-3517](https://nvd.nist.gov/vuln/detail/CVE-2021-3517){: external}, [CVE-2021-3518](https://nvd.nist.gov/vuln/detail/CVE-2021-3518){: external}, [CVE-2021-3537](https://nvd.nist.gov/vuln/detail/CVE-2021-3537){: external}, [CVE-2021-3541](https://nvd.nist.gov/vuln/detail/CVE-2021-3541){: external}, [CVE-2021-33195](https://nvd.nist.gov/vuln/detail/CVE-2021-33195){: external}, [CVE-2021-33196](https://nvd.nist.gov/vuln/detail/CVE-2021-33196){: external}, [CVE-2021-33198](https://nvd.nist.gov/vuln/detail/CVE-2021-33198){: external}, [CVE-2021-33197](https://nvd.nist.gov/vuln/detail/CVE-2021-33197){: external}, and [CVE-2021-34558](https://nvd.nist.gov/vuln/detail/CVE-2021-34558){: external}.  
- Includes a new version of the `ibmc` Helm plug-in. 
- Adds support for Satellite clusters.   
- Adds support for static provisioning of s3fs on AWS clusters.  
- Adds support for installing the `ibm-object-storage-plugin` in air-gapped environments.   
- Changes the default installation namespace from the `kube-system` namespace to the `ibm-object-s3fs` namespace.  
- Enables `ReadOnlyRootFilesystem` for the plug-in and driver pods.  
- Updates the Golang version to `v1.16.6`. 


The `ibm-object-s3fs` namespace is created during installation. Dynamic creation of namespaces is supported for Helm versions 3.2.0 and later. Before upgrading to version 2.1.3 of the `ibm-object-storage-plugin`, upgrade to Helm 3.2.0 or later. If you want to install the Helm chart without using the `ibmc` plug-in, you must manually create the `ibm-object-s3fs` namespace before installing the plug-in.
{: note}


## Change log for version 2.1.2, released 22 June 2021 
{: #0212_object_plugin}

- Image tags: `1.8.30`  
- Updates in this version: Version `v2.0.5` of the `helm-ibmc` plug-in is available.  
- Fixes [`CVE-2021-31525`](https://nvd.nist.gov/vuln/detail/CVE-2021-31525){: external},[`CVE-2021-33194`](https://nvd.nist.gov/vuln/detail/CVE-2021-33194){: external}, and [`CVE-2021-27219`](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}.  


## Change log for version 2.1.1, released 03 June 2021
{: #0211_object_plugin}

- Image tags: `1.8.29`  
- Fixes an upgrade issue in version `2.1.0`.  
- Includes a new version of the `helm ibmc` plug-in. For more information, see [Updating the {{site.data.keyword.cos_full_notm}} plug-in.](/docs/openshift?topic=openshift-storage_cos_install#update_cos_plugin).  
- Users can now specify `default` in PVC configurations to use the default TLS cipher suite when a connection to {{site.data.keyword.cos_full_notm}} is established via the HTTPS endpoint. If your worker nodes run an Ubuntu operating system, your storage classes are set up to use the `AESGCM` cipher suite by default. For worker nodes that run a Red Hat operating system, the `ecdhe_rsa_aes_128_gcm_sha_256` cipher suite is used by default. For more information, see [Adding object storage to apps](/docs/openshift?topic=openshift-storage_cos_apps).  
- Fixes [CVE-2020-28851](https://nvd.nist.gov/vuln/detail/CVE-2020-28851){: external}.  


## Change log for version 2.1.0, released 26 May 2021
{: #0210_object_plugin}

- Image tags: `1.8.28`  
- Updates the UBI to `8.4-200`.  


## Change log for version 2.0.9, 10 May 2021
{: #0209_object_plugin}

- Image tags: `1.8.27`  
- Updates the UBI to `8.3-298.1618432845`.  
- Replaces the Flex storage classes with Smart Tier storage classes.  
- Fixes [CVE-2021-20305](https://nvd.nist.gov/vuln/detail/CVE-2021-20305){: external}.  
- Updates IAM Endpoints.  
- Updates the `object-store-endpoint`.  
- Fixes a PVC mount issue in private-only VPC clusters.  
- Updates the `ResourceConfiguration` endpoint.  


## Change log for version 2.0.8, 19 April 2021
{: #0208_object_plugin}

- Image tags: `1.8.25`  
- Updates the Go version to `1.15.9`.  
- Updates the UBI from `ubi-minimal:8.3-291` to `ubi-minimal:8.3-298`.  
- Fixes [CVE-2021-3449](https://nvd.nist.gov/vuln/detail/CVE-2021-3449){: external}, [CVE-2021-3450](https://nvd.nist.gov/vuln/detail/CVE-2021-3450){: external}, [CVE-2021-27919](https://nvd.nist.gov/vuln/detail/CVE-2021-27919){: external}, and [CVE-2021-27918](https://nvd.nist.gov/vuln/detail/CVE-2021-27918){: external}.  



## Change log for version 2.0.7, 26 March 2021
{: #0207_object_plugin}


- Image tags: `1.8.24`  
- Updates the Go version to `1.15.8`.  
- The plug-in now uses a universal base image (UBI).  
- Fixes for [CVE-2021-3114](https://nvd.nist.gov/vuln/detail/CVE-2021-3114){: external}, [CVE-2021-3115](https://nvd.nist.gov/vuln/detail/CVE-2021-3115){: external}, [CVE-2020-28852](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28852){: external}, and [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}.  


## Change log for version 2.0.6, 18 December 2020
{: #0206_object_plugin}


- Image tags: `1.8.23`  
- The `1.8.23` image is signed.  
- Updates the Go version to `1.15.5`.  
- Fixes `CVE-2020-28362`, `CVE-2020-28367`, and `CVE-2020-28366`.  
- Resources that are deployed by the {{site.data.keyword.cos_full_notm}} plug-in are now linked with the corresponding source code and build URLs.  
- Updates the {{site.data.keyword.cos_full_notm}} plug-in to pull the universal base image (UBI) from the proxy image registry.  




## Change log for version 2.0.5, released 25 November 2020
{: #0205_object_plugin}

- Fixes a `NilPointer` error.  
- Resolves the following CVEs: `CVE-2018-20843`, `CVE-2019-13050`, `CVE-2019-13627`, `CVE-2019-14889`, `CVE-2019-1551`, `CVE-2019-15903`, `,CVE-2019-16168`, `CVE-2019-16935`, `CVE-2019-19221`, `CVE-2019-19906`, `CVE-2019-19956`, `CVE-2019-20218`, `CVE-2019-20386`, `CVE-2019-20387`, `CVE-2019-20388`, `CVE-2019-20454`, `CVE-2019-20907`, `CVE-2019-5018`, `CVE-2020-10029`, `CVE-2020-13630`, `CVE-2020-13631`, `CVE-2020-13632`, `CVE-2020-14422`, `CVE-2020-1730`, `CVE-2020-1751`, `CVE-2020-1752`, `CVE-2020-6405`, `CVE-2020-7595`, and `CVE-2020-8177`.   
