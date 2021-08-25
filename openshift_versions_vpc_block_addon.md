---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-25"

keywords: vpc block, add-on, vpc block changelog

subcollection: openshift

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
  

# {{site.data.keyword.block_storage_is_short}} add-on changelog
{: #vpc_bs_changelog}

View information for patch updates to the {{site.data.keyword.block_storage_is_full}} add-on in your {{site.data.keyword.openshiftlong_notm}} clusters.
{: shortdesc}

* **Patch updates**: Patch updates are delivered automatically by IBM and do not contain any feature updates or changes in the supported add-on and cluster versions.
* **Release updates**: Release updates contain new features for the {{site.data.keyword.block_storage_is_full}} or changes in the supported add-on or cluster versions. You must manually apply release updates to your {{site.data.keyword.block_storage_is_full}} add-on. To update your {{site.data.keyword.block_storage_is_full}} add-on, see [Updating the {{site.data.keyword.block_storage_is_full}} add-on](/docs/openshift?topic=openshift-vpc-block#vpc-addon-update).


As of 26 July 2021, version 2.0.3 of the Block Storage for VPC add-on is unsupported. Version 3.0.0 is deprecated and becomes unsupported on or after 26 August 2021. Version 3.0.1, which adds beta support for volume expansion is now available. If you have a deprecated or unsupported version of the add-on installed in your cluster, update the add-on to version 3.0.1. If you have a deprecated or unsupported version of the add-on installed in your cluster, update the add-on to version 3.0.1. To update the Block Storage for VPC add-on in your cluster, disable the add-on and then re-enable the add-on. You might see a warning that resources or data might be deleted. For the {{site.data.keyword.block_storage_is_full}} add-on update, PVC creation and app deployment are not disrupted when the add-on is disabled and existing volumes are not impacted.
{: important}


To view a list of add-ons and the supported cluster versions, run the following command.
```sh
ibmcloud oc cluster addon versions --addon vpc-block-csi-driver
```
{: pre}

Refer to the following tables for a summary of changes for each version of the {{site.data.keyword.block_storage_is_full}} add-on.

| {{site.data.keyword.block_storage_is_full}} add-on version | Supported? | {{site.data.keyword.openshiftlong_notm}} version support |
| --- | --- | --- |
| 3.0.1 | Yes | >= 4.3 |
| 3.0.0 | Yes | >= 4.3 |
| 2.0.3 | No | >=4.3 |
{: summary="The rows are read from left to right. The first column is the {{site.data.keyword.block_storage_is_full}} add-on version. The second column is the version's supported state. The third column is the cluster version of your cluster that the {{site.data.keyword.block_storage_is_full}} version is supported for."}

## Version 3.0.1
{: #0301_is_block}

Review the changes in version `3.0.1` of the {{site.data.keyword.block_storage_is_full}} add-on.
{: shortdesc}

### Changelog for version 3.0.1, released 15 July 2021
{: #301_init}

Review the changlog for version `3.0.1` of the {{site.data.keyword.block_storage_is_full}} add-on.

Volume expansion in version `3.0.1` is available in beta for allowlisted accounts. Don't use this feature for production workloads.
{: beta}

- Image tags: `v3.0.7`  
- Supported cluster versions >=4.3  
- Includes beta support for volume expansion on allowlisted accounts.  
- Fixes vulnerability [CVE-2021-27219](https://nvd.nist.gov/vuln/detail/CVE-2021-27219){: external}.  
- Includes the `storage-secret-sidecar` container in the {{site.data.keyword.block_storage_is_full}} driver pods.  

## Version 3.0.0
{: #0300_is_block}

Review the changes in version 3.0.0 of the {{site.data.keyword.block_storage_is_full}} add-on.
{: shortdesc}

### Changelog for patch update 3.0.0_521, released 01 April 2021
{: #3.0.0_521}

Review the changes in version 3.0.0_521 of the {{site.data.keyword.block_storage_is_full}} add-on.
{: shortdesc}

- Image tags: `v3.0.7`  
- Supported cluster versions: >=4.3  
- Updates the Golang version from `1.15.5` to `1.15.9`.  


### Changelog for version 3.0.0, released 26 February 2021
{: #0300_is_block_relnote}

Review the changes in version 3.0.0_521 of the {{site.data.keyword.block_storage_is_full}} add-on.
{: shortdesc}

- Image tags: `v.3.0.0`   
- Supported cluster versions: >=4.3  
- The `vpc-block-csi-driver` is now available for both managed clusters and unmanaged clusters.   
- No functional changes in this release.  


## Version 2.0.3
{: #0203_is_block}

Review the changes in version 3.0.0_521 of the {{site.data.keyword.block_storage_is_full}} add-on.
{: shortdesc}

### Changelog for patch update 2.0.3_471, released 26 January 2021
{: #0203471_is_block}

Review the changes in version 3.0.0_521 of the {{site.data.keyword.block_storage_is_full}} add-on.
{: shortdesc}

- Image tags: `v.2.0.9`  
- Supported cluster versions: 4.3 - 4.6  
- Updated he `openssl`, `openssl-libs`, `gnutls` packages to fix [CVE-2020-1971](https://nvd.nist.gov/vuln/detail/CVE-2020-1971){: external} and [CVE-2020-24659](https://nvd.nist.gov/vuln/detail/CVE-2020-24659){: external}.  

### Changelog for patch update 2.0.3_464, released 10 December 2020
{: #0203464_is_block}

Review the changes in version 3.0.0_521 of the {{site.data.keyword.block_storage_is_full}} add-on.
{: shortdesc}

- Image tags: `v2.0.8`  
- Supported cluster versions: 4.3 - 4.6  
- **New!**: Metro storage classes with the `volumeBindingMode:WaitForFirstConsumer` specification.  
- Resources that are deployed by the add-on now contain a label which links the source code URL and the build URL.  
- The `v2.0.8` image is signed.  
- Updates the Go version from `1.15.2` to `1.15.5`.  

### Changelog for patch update 2.0.3_404, released 25 November 2020
{: #0203404_is_block}

Review the changes in version 2.0.3_404 of the {{site.data.keyword.block_storage_is_full}} add-on.
{: shortdesc}

- Image tags: `v2.0.7`  
- Supported cluster versions: 4.3 - 4.6  
- Fixes vulnerability scan issues.  
- Updates the base image from `alpine` to `UBI`.  
- Pods and containers now run as `non-root` except for the `node-server` pod's containers.  

### Changelog for patch update 2.0.3_375, released 17 September 2020
{: #0203375_is_block}

Review the changes in version 2.0.3_375 of the {{site.data.keyword.block_storage_is_full}} add-on.
{: shortdesc}

- Image tags: `v2.0.6`  
- Supported cluster versions: 4.3 - 4.5  
- Fixes an issue with volume attachment when replacing workers.  

### Changelog for patch update 2.0.3_374+, released 29 August 2020
{: #0203374_is_block}

Review the changes in version 2.0.3_374+ of the {{site.data.keyword.block_storage_is_full}} add-on.
{: shortdesc}

- Image tags: `v2.0.5`  
- Supported cluster versions: 4.3 - 4.5  
- Adds the `/var/lib/kubelet` path for CSI driver calls on OCP 4.4.  

### Changelog for patch update 2.0.3_365, released 05 August 2020
{: #203365_is_block}

Review the changes in version 2.0.3_365 of the {{site.data.keyword.block_storage_is_full}} add-on.
{: shortdesc}

- Image tags: `v2.0.4`  
- Supported versions: 4.3 - 4.5  
- Updates sidecar container images.  
- Adds liveness probe.  
- Enables parallel attachment and detachment of volumes to worker nodes. Previously, worker nodes were attached and detached sequentially.  


