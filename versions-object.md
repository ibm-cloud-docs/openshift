---

copyright: 
  years: 2014, 2021
lastupdated: "2021-11-15"

keywords: object storage, plug-in, changelog

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Object storage plug-in 
{: #cos_plugin_changelog}

View information for updates to the {{site.data.keyword.cos_full_notm}} plug-in in your {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}


Refer to the following tables for a summary of changes for each version of the [Object Storage plug-in](/docs/containers?topic=containers-object_storage).

| Object Storage plug-in version | Supported? | {{site.data.keyword.openshiftshort}} version support | Supported architecture |
| --- | --- |--- | --- |
| 2.1.6 | Yes | Greater than or equal to 4.3 | x86 |
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
{: caption="Object Storage plug-in versions" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the Object Storage plug-in version. The second column is the version's supported state. The third column is the version of your cluster that the Object Storage plug-in version is supported for."}


## Changelog for version 2.1.6, released 22 October 2021
{: #0216_object_plugin}

Review the changes in version 2.1.6 of the {{site.data.keyword.cos_full_notm}} plug-in.
{: shortdesc}

- Image tags: `1.8.36`
- Updates s3fs fuse to version 1.90
- Updates dependencies


## Changelog for version 2.1.5, released 5 October 2021
{: #0215_object_plugin}

Review the changes in version 2.1.5 of the {{site.data.keyword.cos_full_notm}} plug-in.
{: shortdesc}

- Image tags: `1.8.34`
- Resolves [CVE-2021-36221](https://nvd.nist.gov/vuln/detail/CVE-2021-36221){: external}, [CVE-2021-29923](https://nvd.nist.gov/vuln/detail/CVE-2021-29923){: external}, and [CVE-2021-33196](https://nvd.nist.gov/vuln/detail/CVE-2021-33196){: external}.
- Updates the UBI to `8.4-210`.
- Includes the `ibmc` plug-in version `2.0.7`.
- Pulls the Golang base image from artifactory.
- Includes endpoint updates for `jp-tok` and `uk-south`. 
- Updates location constraints for Sao Paulo 01. New constraints are `br-sao-standard`, `br-sao-vault`, `br-sao-cold`, and `br-sao-smart`. For more information, see [Storage classes](/docs/cloud-object-storage?topic=cloud-object-storage-classes).
- Allows deployments to the `kube-system` namespace when `bucketAccessPolicy` is enabled.
- Supports dynamic provisioning for non-default regions in AWS s3 instance.

## Changelog for version 2.1.4, released 1 September 2021
{: #0214_object_plugin}

Review the changes in version 2.1.4 of the {{site.data.keyword.cos_full_notm}} plug-in.
{: shortdesc}

- Image tags: `1.8.33`
- Fixes a `timeoutSeconds` issue in the `livenessProbe` and `readinessProbe`.
- Updates the Golang version to `v1.17`.
- Updates the UBI image to `8.4-208`.
- Migrates the image from the `ibmcom` public registry to the `icr.io/cpopen` registry.
- Resolves [CVE-2021-36221](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-36221){: external}, [CVE-2021-29923](https://nvd.nist.gov/vuln/detail/CVE-2021-29923){: external}, and [CVE-2021-33196](https://nvd.nist.gov/vuln/detail/CVE-2021-33196){: external}.


## Changelog for version 2.1.3, released 25 August 2021
{: #0213_object_plugin}

Review the changes in version 2.1.3 of the {{site.data.keyword.cos_full_notm}} plug-in.
{: shortdesc}

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


## Changelog for version 2.1.2, released 22 June 2021 
{: #0212_object_plugin}

Review the changes in version 2.1.2 of the {{site.data.keyword.cos_full_notm}} plug-in.
{: shortdesc}

- Image tags: `1.8.30`  
- Updates in this version: Version `v2.0.5` of the `helm-ibmc` plug-in is available.  
- Fixes [`CVE-2021-31525`](https://nvd.nist.gov/vuln/detail/CVE-2021-31525){: external},[`CVE-2021-33194`](https://nvd.nist.gov/vuln/detail/CVE-2021-33194){: external}, and [`CVE-2021-27219`](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}.  


## Changelog for version 2.1.1, released 03 June 2021
{: #0211_object_plugin}

Review the changes in version 2.1.1 of the {{site.data.keyword.cos_full_notm}} plug-in.
{: shortdesc}

- Image tags: `1.8.29`  
- Fixes an upgrade issue in version `2.1.0`.  
- Includes a new version of the `helm ibmc` plug-in. For more information, see [Updating the {{site.data.keyword.cos_full_notm}} plug-in.](/docs/openshift?topic=openshift-object_storage#update_cos_plugin).  
- Users can now specify <code>default</code> in PVC configurations to use the default TLS cipher suite when a connection to {{site.data.keyword.cos_full_notm}} is established via the HTTPS endpoint. If your worker nodes run an Ubuntu operating system, your storage classes are set up to use the `AESGCM` cipher suite by default. For worker nodes that run a Red Hat operating system, the `ecdhe_rsa_aes_128_gcm_sha_256` cipher suite is used by default. For more information, see [Adding object storage to apps](/docs/openshift?topic=openshift-object_storage#add_cos).  
- Fixes [CVE-2020-28851](https://nvd.nist.gov/vuln/detail/CVE-2020-28851){: external}.  


## Changelog for version 2.1.0, released 26 May 2021
{: #0210_object_plugin}

Review the changes in version 2.1.0 of the {{site.data.keyword.cos_full_notm}} plug-in.
{: shortdesc}

- Image tags: `1.8.28`  
- Updates the UBI to `8.4-200`.  


## Changelog for version 2.0.9, 10 May 2021
{: #0209_object_plugin}

Review the changes in version 2.0.9 of the {{site.data.keyword.cos_full_notm}} plug-in.
{: shortdesc}

- Image tags: `1.8.27`  
- Updates the UBI to `8.3-298.1618432845`.  
- Replaces the Flex storage classes with Smart Tier storage classes.  
- Fixes [CVE-2021-20305](https://nvd.nist.gov/vuln/detail/CVE-2021-20305){: external}.  
- Updates IAM Endpoints.  
- Updates the `object-store-endpoint`.  
- Fixes a PVC mount issue in private-only VPC clusters.  
- Updates the `ResourceConfiguration` endpoint.  


## Changelog for version 2.0.8, 19 April 2021
{: #0208_object_plugin}

Review the changes in version 2.0.8 of the {{site.data.keyword.cos_full_notm}} plug-in.
{: shortdesc}

- Image tags: `1.8.25`  
- Updates the Go version to `1.15.9`.  
- Updates the UBI from `ubi-minimal:8.3-291` to `ubi-minimal:8.3-298`.  
- Fixes [CVE-2021-3449](https://nvd.nist.gov/vuln/detail/CVE-2021-3449){: external}, [CVE-2021-3450](https://nvd.nist.gov/vuln/detail/CVE-2021-3450){: external}, [CVE-2021-27919](https://nvd.nist.gov/vuln/detail/CVE-2021-27919){: external}, and [CVE-2021-27918](https://nvd.nist.gov/vuln/detail/CVE-2021-27918){: external}.  



## Changelog for version 2.0.7, 26 March 2021
{: #0207_object_plugin}

Review the changes in version 2.0.7 of the {{site.data.keyword.cos_full_notm}} plug-in.
{: shortdesc}

- Image tags: `1.8.24`  
- Updates the Go version to `1.15.8`.  
- The plug-in now uses a universal base image (UBI).  
- Fixes for [CVE-2021-3114](https://nvd.nist.gov/vuln/detail/CVE-2021-3114){: external}, [CVE-2021-3115](https://nvd.nist.gov/vuln/detail/CVE-2021-3115){: external}, [CVE-2020-28852](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28852){: external}, and [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}.  


## Changelog for version 2.0.6, 18 December 2020
{: #0206_object_plugin}

Review the changes in version 2.0.6 of the {{site.data.keyword.cos_full_notm}} plug-in.
{: shortdesc}

- Image tags: `1.8.23`  
- The `1.8.23` image is signed.  
- Updates the Go version to `1.15.5`.  
- Fixes `CVE-2020-28362`, `CVE-2020-28367`, and `CVE-2020-28366`.  
- Resources that are deployed by the Object Storage plug-in are now linked with the corresponding source code and build URLs.  
- Updates the Object Storage plug-in to pull the universal base image (UBI) from the proxy image registry.  




## Changelog for version 2.0.5, released 25 November 2020
{: #0205_object_plugin}

Review the changes that are included in version 2.0.5 of the Object Storage plug-in.
{: shortdesc}

- Fixes a `NilPointer` error.  
- Resolves the following CVEs: `CVE-2018-20843`, `CVE-2019-13050`, `CVE-2019-13627`, `CVE-2019-14889`, `CVE-2019-1551`, `CVE-2019-15903`, `,CVE-2019-16168`, `CVE-2019-16935`, `CVE-2019-19221`, `CVE-2019-19906`, `CVE-2019-19956`, `CVE-2019-20218`, `CVE-2019-20386`, `CVE-2019-20387`, `CVE-2019-20388`, `CVE-2019-20454`, `CVE-2019-20907`, `CVE-2019-5018`, `CVE-2020-10029`, `CVE-2020-13630`, `CVE-2020-13631`, `CVE-2020-13632`, `CVE-2020-14422`, `CVE-2020-1730`, `CVE-2020-1751`, `CVE-2020-1752`, `CVE-2020-6405`, `CVE-2020-7595`, and `CVE-2020-8177`.   




