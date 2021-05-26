---

copyright:
  years: 2014, 2021
lastupdated: "2021-05-18"

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
  
  
# VPC: Why is no VPC available when I create a cluster in the console?
{: #ts_no_vpc}

**Infrastructure provider**: <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

{: tsSymptoms}
You try to create a VPC cluster by using the [{{site.data.keyword.openshiftlong_notm}} console](https://cloud.ibm.com/kubernetes/catalog/create){: external}. You have an existing [VPC](https://cloud.ibm.com/vpc){: external} in your account, but when you try to select an existing **Virtual Private Cloud** to create the cluster in, you see the following error message:
```
No VPC is available. Create a VPC.
```
{: screen}

{: tsCauses}
During cluster creation, the {{site.data.keyword.openshiftlong_notm}} console uses the API key that is set for the `default` resource group to list the VPCs that are available in your {{site.data.keyword.cloud_notm}} account. If no API key is set for the `default` resource group, no VPCs are listed in the {{site.data.keyword.openshiftlong_notm}} console, even if your VPC exists in a different resource group and an API key is set for that resource group.

{: tsResolve}
To set an API key for the `default` resource group, use the {{site.data.keyword.openshiftlong_notm}} CLI.
1. Log in to the command line as the account owner. If you want a different user than the account owner to set the API key, first [ensure that the API key owner has the correct permissions](/docs/openshift?topic=openshift-users#owner_permissions).
    ```
    ibmcloud login [--sso]
    ```
    {: pre}

2. Target the `default` resource group.
    ```
    ibmcloud target -g default
    ```
    {:pre}

3. Set the API key for the region and resource group.
    ```
    ibmcloud oc api-key reset --region <region>
    ```
    {: pre}

4. In the [{{site.data.keyword.openshiftlong_notm}} console](https://cloud.ibm.com/kubernetes/catalog/create){: external}, click **Refresh VPCs**. Your available VPCs are now listed in a drop-down menu.
