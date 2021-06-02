---

copyright:
  years: 2014, 2021
lastupdated: "2021-06-02"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

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
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
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
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
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
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
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
  
  
# Object storage: Why do I see wrong s3fs or IAM API endpoints when I create a PVC?
{: #cos_api_endpoint_failure}

**Infrastructure provider**:
* <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC


<img src="../images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This troubleshooting topic applies only to {{site.data.keyword.openshiftshort}} clusters that run version 3.11.
{: note}


{: tsSymptoms}
When you create the PVC, the PVC remains in a pending state. After you run the `oc describe pvc <pvc_name>` command, you see one of the following error messages:

```sh
Bad value for ibm.io/object-store-endpoint XXXX: scheme is missing. Must be of the form http://<hostname> or https://<hostname>
```
{: screen}

```sh
Bad value for ibm.io/iam-endpoint XXXX: scheme is missing. Must be of the form http://<hostname> or https://<hostname>
```
{: screen}

{: tsCauses}
The s3fs API endpoint for the bucket that you want to use might have the wrong format, or your cluster is deployed in a location that is supported in {{site.data.keyword.openshiftlong_notm}} but is not yet supported by the {{site.data.keyword.cos_full_notm}} plug-in.

{: tsResolve}
1. Check the s3fs API endpoint that was automatically assigned by the `ibmc` Helm plug-in to your storage classes during the {{site.data.keyword.cos_full_notm}} plug-in installation. The endpoint is based on the location that your cluster is deployed to.  
   ```sh
   oc get sc ibmc-s3fs-standard-regional -o yaml | grep object-store-endpoint
   ```
   {: pre}

   If the command returns `ibm.io/object-store-endpoint: NA`, your cluster is deployed in a location that is supported in {{site.data.keyword.openshiftlong_notm}} but is not yet supported by the {{site.data.keyword.cos_full_notm}} plug-in. To add the location to the {{site.data.keyword.openshiftlong_notm}}, post a question in our public Slack or open an {{site.data.keyword.cloud_notm}} support case. For more information, see [Getting help and support](/docs/containers?topic=containers-getting_help_storage).

2. If you manually added the s3fs API endpoint with the `ibm.io/endpoint` annotation or the IAM API endpoint with the `ibm.io/iam-endpoint` annotation in your PVC, make sure that you added the endpoints in the format `https://<s3fs_api_endpoint>` and `https://<iam_api_endpoint>`. The annotation overwrites the API endpoints that are automatically set by the `ibmc` plug-in in the {{site.data.keyword.cos_full_notm}} storage classes.
   ```sh
   oc describe pvc <pvc_name>
   ```
   {: pre}


