---

copyright: 
  years: 2014, 2025
lastupdated: "2025-04-04"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, object storage, plug-in, change log

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# {{site.data.keyword.cos_full_notm}} plug-in 
{: #cos_plugin_changelog}


View information for updates to the {{site.data.keyword.cos_full_notm}} plug-in in your {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}


| {{site.data.keyword.cos_full_notm}} plug-in version | Supported? |
| --- | --- |
| 2.2.35 | Yes |
| 2.2.36 | Yes |
{: caption="{{site.data.keyword.cos_full_notm}} plug-in versions" caption-side="bottom"}

Versions are deprecated at n-2 or roughly 3 months after their release date. Plan to keep your add-on updated. For update steps, see [Updating the {{site.data.keyword.cos_full_notm}} plug-in](/docs/openshift?topic=openshift-storage_cos_install#update_cos_plugin).
{: important}


## Change log for version 2.2.36, released 10 March 2025
{: #02236_object_plugin}

- Updates golang to `1.23.6`.
- Resolves the following CVEs: [CVE-2020-11023](https://nvd.nist.gov/vuln/detail/CVE-2020-11023){: external}, [CVE-2024-45341](https://nvd.nist.gov/vuln/detail/CVE-2024-45341){: external}, [CVE-2025-22866](https://nvd.nist.gov/vuln/detail/CVE-2025-22866){: external}, and [CVE-2024-45336](https://nvd.nist.gov/vuln/detail/CVE-2024-45336){: external}.

## Change log for version 2.2.35, released 27 January 2025
{: #02235_object_plugin}

- Updates golang to `1.22.11`.
- Resolves the following CVEs: [CVE-2024-51744](https://nvd.nist.gov/vuln/detail/CVE-2024-51744){: external}, [CVE-2024-45337](https://nvd.nist.gov/vuln/detail/CVE-2024-45337){: external}.
- Adds support for version 4.18 clusters.

## Change log for version 2.2.33, released 21 November 2024
{: #02233_object_plugin}

- Updates golang to `1.22.9`.
- Resolves CVE-2024-3596.
- Adds support for version 4.17 clusters.


## Change log for version 2.2.32, released 26 September 2024
{: #02232_object_plugin}

- Fixes a mounting issue in clusters with RHCOS worker nodes.

## Change log for version 2.2.31, released 24 September 2024
{: #02231_object_plugin}

- Updates `s3fs-fuse` to `v1.94`.
- Updates golang to `1.22.7`.
- Resolves [CVE-2024-34158](https://nvd.nist.gov/vuln/detail/CVE-2024-34158){: external}, [CVE-2024-34155](https://nvd.nist.gov/vuln/detail/CVE-2024-34155){: external}, and [CVE-2024-34156](https://nvd.nist.gov/vuln/detail/CVE-2024-34156){: external}.



## Change log for version 2.2.30, released 29 August 2024
{: #02230_object_plugin}

- Updates golang to `1.21.13`.
- Resolves the following CVEs: [CVE-2024-6104](https://nvd.nist.gov/vuln/detail/CVE-2024-6104){: external}, [CVE-2024-24791](https://nvd.nist.gov/vuln/detail/CVE-2024-24791){: external}, [CVE-2023-45288](https://nvd.nist.gov/vuln/detail/CVE-2023-45288){: external}, [CVE-2024-2398](https://nvd.nist.gov/vuln/detail/CVE-2024-2398){: external}, [CVE-2024-37370](https://nvd.nist.gov/vuln/detail/CVE-2024-37370){: external}, and [CVE-2024-37371](https://nvd.nist.gov/vuln/detail/CVE-2024-37371){: external}.


## Change log for version 2.2.29, released 31 July 2024
{: #02229_object_plugin}

- Adds support for Ubuntu 24 worker nodes.

## Change log for version 2.2.28, released 17 July 2024
{: #02228_object_plugin}

- Resolves [CVE-2023-2953](https://nvd.nist.gov/vuln/detail/CVE-2023-2953){: external} and [CVE-2024-28182](https://nvd.nist.gov/vuln/detail/CVE-2024-28182){: external}

## Change log for version 2.2.27, released 17 July 2024
{: #02227_object_plugin}

- Resolves [CVE-2024-24789](https://nvd.nist.gov/vuln/detail/CVE-2024-24789){: external} and [CVE-2024-24790](https://nvd.nist.gov/vuln/detail/CVE-2024-24790){: external}

## Change log for version 2.2.26, released 5 June 2024
{: #02226_object_plugin}

- Adds HPCS support.
- Updates golang base image to fix vulnerabilities [CVE-2023-7008](https://nvd.nist.gov/vuln/detail/CVE-2023-7008){: external}, [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961){: external}, [CVE-2024-33599](https://nvd.nist.gov/vuln/detail/CVE-2024-33599){: external}, [CVE-2024-33600](https://nvd.nist.gov/vuln/detail/CVE-2024-33600){: external}, [CVE-2024-33601](https://nvd.nist.gov/vuln/detail/CVE-2024-33601){: external}, [CVE-2024-33602](https://nvd.nist.gov/vuln/detail/CVE-2024-33602){: external}.


## Change log for version 2.2.25, released 24 April 2024
{: #02225_object_plugin}

- Resolves [CVE-2023-45288](https://nvd.nist.gov/vuln/detail/CVE-2023-45288){: external}, [CVE-2024-24785](https://nvd.nist.gov/vuln/detail/CVE-2024-24785){: external}, [CVE-2023-44487](https://nvd.nist.gov/vuln/detail/CVE-2023-44487){: external}, and [CVE-2023-45288](https://nvd.nist.gov/vuln/detail/CVE-2023-45288){: external}

## Change log for version 2.2.24, released 22 February 2024
{: #02224_object_plugin}

- Fixes an installation issue on Satellite clusters with CoreOS worker nodes.

## Change log for version 2.2.23, released 29 January 2024
{: #02223_object_plugin}

- Replaces UBI image with scratch image.
- Resolves [CVE-2023-3446](https://nvd.nist.gov/vuln/detail/CVE-2023-3446){: external}, [CVE-2023-3817](https://nvd.nist.gov/vuln/detail/CVE-2023-3817){: external}, and [CVE-2023-5678](https://nvd.nist.gov/vuln/detail/CVE-2023-5678){: external}.


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

Because this update affects regional storage classes, you must uninstall and reinstall the `2.2.13` chart so the new storage classes are created in your cluster. This change primarily impacts single site clusters because the regional storage classes, such as `ibmc-s3fs-standard-regional`, now point to the single site COS endpoint instead of the regional endpoints. This change is not applied automatically to existing PVCs and pods. You must create new PVCs with the new storage classes for the changes to take effect. For more information on how to update your PVCs, refer to the [Adding object storage to apps](/docs/openshift?topic=openshift-storage_cos_apps) documentation.
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

- Adds support for the `--set allowCrossNsSecret=true/false` option when you install the {{site.data.keyword.cos_full_notm}} plug-in. For more information, see [Installing the {{site.data.keyword.cos_full_notm}} plug-in](/docs/openshift?topic=openshift-storage_cos_install).
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
