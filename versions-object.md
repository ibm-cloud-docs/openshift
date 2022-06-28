---

copyright: 
  years: 2014, 2022
lastupdated: "2022-06-28"

keywords: object storage, plug-in, changelog

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# {{site.data.keyword.cos_full_notm}} plug-in 
{: #cos_plugin_changelog}

View information for updates to the {{site.data.keyword.cos_full_notm}} plug-in in your {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}


Refer to the following tables for a summary of changes for each version of the [{{site.data.keyword.cos_full_notm}} plug-in](/docs/containers?topic=containers-storage-cos-understand).

| {{site.data.keyword.cos_full_notm}} plug-in version | Supported? | {{site.data.keyword.redhat_openshift_notm}} version support | Supported architecture |
| --- | --- |--- | --- |
| 2.1.16 | Yes | Greater than or equal to 4.6 | x86 |
| 2.1.15 | Yes | Greater than or equal to 4.6 | x86 |
| 2.1.14 | Deprecated | Greater than or equal to 4.6 | x86 |
| 2.1.13 | Deprecated | Greater than or equal to 4.6 | x86 |
| 2.1.12 | Deprecated | Greater than or equal to 4.3 | x86 |
| 2.1.11 | Deprecated | Greater than or equal to 4.3 | x86 |
| 2.1.10 | Deprecated | Greater than or equal to 4.3 | x86 |
| 2.1.9 | Deprecated | Greater than or equal to 4.3 | x86 |
| 2.1.8 | Deprecated | Greater than or equal to 4.3 | x86 |
| 2.1.7 | Deprecated | Greater than or equal to 4.3 | x86 |
| 2.1.6 | Deprecated | Greater than or equal to 4.3 | x86 |
| 2.1.5 | Deprecated | Greater than or equal to 4.3  | x86 |
| 2.1.4 | Deprecated | Greater than or equal to 4.3  | x86 |
| 2.1.3 | Deprecated | Greater than or equal to 4.3  | x86 |
| 2.1.2 | Deprecated | Greater than or equal to 4.3  | x86 |
| 2.1.1 | Deprecated | 4.3 to 4.6 | x86 |
| 2.1.0 | Deprecated | 4.3 to 4.6 | x86 |
| 2.0.9 | Deprecated | 4.3 to 4.6 | x86 |
| 2.0.8 | Deprecated | 4.3 to 4.6 | x86 |
| 2.0.7 | Deprecated | 4.3 to 4.6 | x86 |
| 2.0.6 | Deprecated | 4.3 - 4.6 | x86 | 
| 2.0.5 | Deprecated | 4.3 to 4.6 | x86 |
{: caption="{{site.data.keyword.cos_full_notm}} plug-in versions" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the {{site.data.keyword.cos_full_notm}} plug-in version. The second column is the version's supported state. The third column is the version of your cluster that the {{site.data.keyword.cos_full_notm}} plug-in version is supported for."}

## Change log for version 2.1.17, released 28 June 2022
{: #02117_object_plugin}

- Updates the UBI to `8.6-751.1655117800`.
- Updates `s3fs-fuse` fix a segfault issue.
- Adds support to configure ephemeral storage of plug-in and driver pods.

## Change log for version 2.1.16, released 25 May 2022
{: #02116_object_plugin}

- Updates the UBI to `8.6-751`
- Added support for adding ips via pvc annotation for `configBucketAccess`
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
- Added support for quota-limit option for COS buckets via s3fs plugin
- Includes the `ibmc` plug-in version `2.0.8`

## Change log for version 2.1.13, released 24 March 2022
{: #02113_object_plugin}

- Updates the UBI to `8.5-240`
- Updates Golang to `v1.16.15`
- Resolves [CVE-2022-24921](https://nvd.nist.gov/vuln/detail/CVE-2022-24921){: external}, and [CVE-2022-23852](https://nvd.nist.gov/vuln/detail/CVE-2022-23852){: external}.
- s3fs fuse updated to `v1.91`
- Added support for additional mount options `Ex: ibm.io/add-mount-param: "del_cache,retries=6"`


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


- Updates the univeral base image (UBI) to `ubi-minimal:8.5-230`.
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

**Notes:**
* The `ibm-object-s3fs` namespace is created during installation. Dynamic creation of namespaces is supported for Helm versions 3.2.0 and later. Before upgrading to version 2.1.3 of the `ibm-object-storage-plugin`, upgrade to Helm 3.2.0 or later.
* If you want to install the Helm chart without using the `ibmc` plug-in, you must manually create the `ibm-object-s3fs` namespace before installing the plug-in.


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
- Users can now specify `default` in PVC configurations to use the default TLS cipher suite when a connection to {{site.data.keyword.cos_full_notm}} is established via the HTTPS endpoint. If your worker nodes run an Ubuntu operating system, your storage classes are set up to use the `AESGCM` cipher suite by default. For worker nodes that run a Red Hat operating system, the `ecdhe_rsa_aes_128_gcm_sha_256` cipher suite is used by default. For more information, see [Adding object storage to apps](/docs/containers?topic=containers-storage_cos_apps).  
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
