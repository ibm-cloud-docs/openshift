---

copyright:
  years: 2014, 2021
lastupdated: "2021-02-10"

keywords: openshift, roks, rhoks, rhos

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


# Managing security and compliance with {{site.data.keyword.openshiftshort}}
{: #manage-security-compliance}

{{site.data.keyword.openshiftlong}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

With the {{site.data.keyword.compliance_short}}, you can:

* Monitor for controls and goals that pertain to {{site.data.keyword.openshiftlong_notm}}.
* Define rules for {{site.data.keyword.openshiftlong_notm}} that can help to standardize resource configuration.

## Monitoring security and compliance posture with {{site.data.keyword.openshiftshort}}
{: #monitor-clusters}

As a security or compliance focal, you can use the {{site.data.keyword.openshiftlong_notm}} [goals](#x2117978){: term} to help ensure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](#x2034950){: term}, you can identify potential issues as they arise.
{: shortdesc}

All of the goals for {{site.data.keyword.openshiftlong_notm}} are added to the {{site.data.keyword.cloud_notm}} Best Practices Controls 1.0 profile but can also be mapped to other profiles.
{: note}

To start monitoring your resources, check out [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic=security-compliance-getting-started)

### Available goals for {{site.data.keyword.openshiftshort}}
{: #clusters-available-goals}

Review the following goals for {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

*   **Ensure that clusters are accessible by using the private service endpoint only.** You can [disable the public service endpoint](/docs/openshift?topic=openshift-cs_network_cluster#disable-public-se). For more information, see [Planning your cluster network setup](/docs/openshift?topic=openshift-plan_clusters).
*   **Ensure that inbound traffic to the cluster through Ingress uses allowed TLS versions only.** The default TLS versions are 1.2 or 1.3. For more information, see [About Ingress](/docs/openshift?topic=openshift-ingress-about-roks4).
*   **Ensure that data in cluster secrets are encrypted with keys that the customer manages.** You can enable a key management service (KMS) provider in your cluster. For more information, see [Protecting sensitive information in your cluster](/docs/openshift?topic=openshift-encryption).
*   **Ensure that data in cluster secrets are encrypted with keys that the customer manages that are controlled by a hardware security module that the customer manages.** You can enable {{site.data.keyword.hscrypto}} as the key management service (KMS) provider in your cluster. For more information, see [Protecting sensitive information in your cluster](/docs/openshift?topic=openshift-encryption).
*   **Ensure that the cluster has a logging service enabled.** For more information, see [Understanding options for logging and monitoring](/docs/openshift?topic=openshift-health#oc_logmet_options)..
*   **Ensure that the cluster has a monitoring service enabled.** For more information, see [Understanding options for logging and monitoring](/docs/openshift?topic=openshift-health#oc_logmet_options).
*   **Ensure that the cluster and worker node versions are up to date.** For more information, see [Version information and update actions](/docs/openshift?topic=openshift-openshift_versions).
*   **Ensure that the cluster can pull images from the private image repository that is provided by {{site.data.keyword.registrylong_notm}}.** For more information, see [Understanding how to authorize your cluster to pull images from a private registry](/docs/openshift?topic=openshift-registry#cluster_registry_auth).
