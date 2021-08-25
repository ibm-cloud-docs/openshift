---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-25"

keywords: object storage, plug-in, changelog

subcollection: openshift, object storage

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}
  


# Object storage plug-in 
{: #cos_plugin_changelog}

View information for updates to the {{site.data.keyword.cos_full_notm}} plug-in in your {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

Version 2.1.3 includes a new version of the `ibmc` plug-in. To update the `ibmc` plug-in, uninstall and re-install the {{site.data.keyword.cos_full_notm}} plug-in. For more information, see [Updating the {{site.data.keyword.cos_full_notm}}](/docs/openshift?topic=openshift-object_storage#update_cos_plugin) plug-in.
{: note}

Refer to the following tables for a summary of changes for each version of the [Object Storage plug-in](/docs/openshift?topic=openshift-object_storage).

| Object Storage plug-in version | Supported? | {{site.data.keyword.openshiftshort}} version support | Supported architecture |
| -------------------- | -----------|--------------------------- |
| 2.1.3 | Yes | >= 4.3  | x86 |
| 2.1.2 | Yes | >= 4.3  | x86 |
| 2.1.1 | Yes | 4.3 to 4.6 | x86 |
| 2.1.0 | Yes | 4.3 to 4.6 | x86 |
| 2.0.9 | Yes | 4.3 to 4.6 | x86 |
| 2.0.8 | Yes | 4.3 to 4.6 | x86 |
| 2.0.7 | Yes | 4.3 to 4.6 | x86 |
| 2.0.6 | Yes | 4.3 - 4.6 | x86 | 
| 2.0.5 | Yes | 4.3 to 4.6 | x86 |
{: caption="Object Storage plug-in versions" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the Object Storage plug-in version. The second column is the version's supported state. The third column is the version of your cluster that the Object Storage plug-in version is supported for."}

## Changelog for version 2.1.3, released 25 August 2021
{: #0213_object_plugin}

- Image tags: `1.8.32`
- Addresses the following CVEs: [CVE-2021-3520](ttps://nvd.nist.gov/vuln/detail/CVE-2021-3520){: external}, [CVE-2021-3516](ttps://nvd.nist.gov/vuln/detail/CVE-2021-3516){: external}, [CVE-2021-3517](ttps://nvd.nist.gov/vuln/detail/CVE-2021-3517){: external}, [CVE-2021-3518](ttps://nvd.nist.gov/vuln/detail/CVE-2021-3518){: external}, [CVE-2021-3537](ttps://nvd.nist.gov/vuln/detail/CVE-2021-3537){: external}, [CVE-2021-3541](ttps://nvd.nist.gov/vuln/detail/CVE-2021-3541){: external}, [CVE-2021-33195](ttps://nvd.nist.gov/vuln/detail/CVE-2021-33195){: external}, [CVE-2021-33196](ttps://nvd.nist.gov/vuln/detail/CVE-2021-33196){: external}, [CVE-2021-33198](ttps://nvd.nist.gov/vuln/detail/CVE-2021-33198){: external}, [CVE-2021-33197](ttps://nvd.nist.gov/vuln/detail/CVE-2021-33197){: external}, and [CVE-2021-34558](ttps://nvd.nist.gov/vuln/detail/CVE-2021-34558){: external}.  
- Includes a new version of the `ibmc` Helm plug-in. 
- Adds support for Satellite clusters.   
- Adds support static provisioning s3fs on AWS clusters.  
- Adds support for installing the `ibm-object-storage-plugin` in air-gapped environments.   
- Changes the default installation namespace from the `kube-system` namespace to the `ibm-object-s3fs` namespace.  
- Enables `ReadOnlyRootFilesystem` for the plug-in and driver pods.  
- Updates the GoLang version to `v1.16.6`. 

**Notes:**
* The `ibm-object-s3fs` namespace is created during installation. Dynamic creation of namespaces is supported for Helm versions 3.2.0 and later. Before upgrading to version 2.1.3 of the `ibm-object-storage-plugin`, upgrade to Helm 3.2.0 or later.
* If you want to install the Helm chart without using the `ibmc` plug-in, you must manually create the `ibm-object-s3fs` namespace before installing the plug-in.


## Changelog for version 2.1.2, released 22 June 2021 
{: #0212_object_plugin}

- Image tags: `1.8.30`  
- Updates in this version: Version `v2.0.5` of the `helm-ibmc` plug-in is available.  
- Fixes [`CVE-2021-31525`](https://nvd.nist.gov/vuln/detail/CVE-2021-31525){: external},[`CVE-2021-33194`](https://nvd.nist.gov/vuln/detail/CVE-2021-33194){: external}, and [`CVE-2021-27219`](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}.  


## Changelog for version 2.1.1, released 03 June 2021
{: #0211_object_plugin}

- Image tags: `1.8.29`  
- Fixes an upgrade issue in version `2.1.0`.  
- Includes a new version of the `helm ibmc` plug-in. For more information, see [Updating the {{site.data.keyword.cos_full_notm}} plug-in.](/docs/openshift?topic=openshift-object_storage#update_cos_plugin).  
- Users can now specify <code>default</code> in PVC configurations to use the default TLS cipher suite when a connection to {{site.data.keyword.cos_full_notm}} is established via the HTTPS endpoint. If your worker nodes run an Ubuntu operating system, your storage classes are set up to use the `AESGCM` cipher suite by default. For worker nodes that run a Red Hat operating system, the `ecdhe_rsa_aes_128_gcm_sha_256` cipher suite is used by default. For more information, see [Adding object storage to apps](/docs/openshift?topic=openshift-object_storage#add_cos).  
- Fixes [CVE-2020-28851](https://nvd.nist.gov/vuln/detail/CVE-2020-28851){: external}.  


## Changelog for version 2.1.0, released 26 May 2021
{: #0210_object_plugin}

- Image tags: `1.8.28`  
- Updates the UBI to `8.4-200`.  


## Changelog for version 2.0.9, 10 May 2021
{: #0209_object_plugin}

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

- Image tags: `1.8.25`  
- Updates the Go version to `1.15.9`.  
- Updates the UBI from `ubi-minimal:8.3-291` to `ubi-minimal:8.3-298`.  
- Fixes [CVE-2021-3449](https://nvd.nist.gov/vuln/detail/CVE-2021-3449){: external}, [CVE-2021-3450](https://nvd.nist.gov/vuln/detail/CVE-2021-3450){: external}, [CVE-2021-27919](https://nvd.nist.gov/vuln/detail/CVE-2021-27919){: external}, and [CVE-2021-27918](https://nvd.nist.gov/vuln/detail/CVE-2021-27918){: external}.  



## Changelog for version 2.0.7, 26 March 2021
{: #0207_object_plugin}

- Image tags: `1.8.24`  
- Updates the Go version to `1.15.8`.  
- The plug-in now uses a universal base image (UBI).  
- Fixes for [CVE-2021-3114](https://nvd.nist.gov/vuln/detail/CVE-2021-3114){: external}, [CVE-2021-3115](https://nvd.nist.gov/vuln/detail/CVE-2021-3115){: external}, [CVE-2020-28852](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28852){: external}, and [CVE-2020-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28851){: external}.  


## Changelog for version 2.0.6, 18 December 2020
{: #0206_object_plugin}


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


