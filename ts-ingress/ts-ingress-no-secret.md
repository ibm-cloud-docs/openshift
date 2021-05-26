---

copyright:
  years: 2014, 2021
lastupdated: "2021-05-24"

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
  
  
# Why does no Ingress secret exist after cluster creation?
{: #ingress_secret}

**Infrastructure provider**:
* <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

{: tsSymptoms}
When you run `ibmcloud oc ingress status -c <cluster_name_or_ID>`, one of the following messages continues to be displayed:
```
Creating TLS certificate for Ingress subdomain, which might take several minutes. Ensure you have the correct IAM permissions.
```
{: screen}
```
Could not upload certificates to Certificate Manager instance. Ensure you have the correct IAM service permissions.
```
{: screen}
```
Could not create a Certificate Manager instance. Ensure you have the correct IAM platform permissions.
```
{: screen}

When you run `ibmcloud oc ingress secret ls`, no secrets are listed.

{: tsCauses}
As of 24 August 2020, an [{{site.data.keyword.cloudcerts_long}}](/docs/certificate-manager?topic=certificate-manager-about-certificate-manager) instance is automatically created for each cluster that you can use to manage the cluster's Ingress TLS certificates.

For a {{site.data.keyword.cloudcerts_short}} instance to be created for your new or existing cluster, the API key for the region and resource group that the cluster is created in must have the correct IAM permissions. The API key that your cluster uses does not have the correct IAM permissions to create and access a {{site.data.keyword.cloudcerts_short}} instance.

Also, if you used the same cluster name repeatedly, you might have a rate limiting issue. For more information, see [No Ingress subdomain exists after you create clusters of the same or similar name](/docs/openshift?topic=openshift-cs_rate_limit).

{: tsResolve}
1. Check the ID of the user or functional user who sets the API key for this cluster.
  ```
  ibmcloud oc api-key info -c <cluster_name_or_ID>
  ```
  {: pre}
2. [Assign the following IAM permissions](/docs/openshift?topic=openshift-users#add_users) to the user or functional user who sets the API key.
  * The **Administrator** or **Editor** platform access role for {{site.data.keyword.cloudcerts_short}} in **All resource groups**
  * The **Manager** service access role for {{site.data.keyword.cloudcerts_short}} in **All resource groups**
3. The user must [reset the API key for the region and resource group](/docs/openshift?topic=openshift-users#api_key_most_cases).

  When the API key is reset, the previous API key that was used for the region and resource group is deleted. Before you reset the API key, check whether you have other services that use the existing API key, such as a [key management service (KMS) provider](/docs/openshift?topic=openshift-encryption#keyprotect).
  {: important}
4. After the cluster has access to the updated permissions in the API key, the creation of the {{site.data.keyword.cloudcerts_short}} instance is automatically triggered. Note that the {{site.data.keyword.cloudcerts_short}} instance might take up to an hour to become visible in the {{site.data.keyword.cloud_notm}} console.
5. Verify that your cluster is automatically assigned a {{site.data.keyword.cloudcerts_short}} instance.
  1. In the {{site.data.keyword.cloud_notm}} console, navigate to your [{{site.data.keyword.cloud_notm}} resource list](https://cloud.ibm.com/resources){: external}.
  2. Expand the **Services** row.
  3. Look for a {{site.data.keyword.cloudcerts_short}} instance that is named in the format `kube-crtmgr-<cluster_ID>`. To find your cluster's ID, run `ibmcloud oc cluster ls`.
  4. Click the instance's name. The **Your certificates** details page opens.
6. Verify that the TLS secret for your cluster's Ingress subdomain is created and listed in your cluster.
  ```
  ibmcloud oc ingress secret ls -c <cluster_name_or_ID>
  ```
  {: pre}


For more information, see [Managing TLS certificates and secrets](/docs/openshift?topic=openshift-ingress-types#manage_certs).
