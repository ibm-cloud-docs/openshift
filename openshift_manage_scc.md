---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-14"

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


*   **Check whether {{site.data.keyword.openshiftshort}} worker nodes are updated to the latest image to ensure patching of vulnerabilities.** You can review the worker node version by selecting your cluster in the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} or in the command line by running `ibmcloud oc worker ls -c <cluster_name_or_ID>`. For more information, see the [Version changelog](/docs/openshift?topic=openshift-openshift_changelog).
*   **Check whether {{site.data.keyword.openshiftshort}} clusters are accessible only by using private cloud service endpoints.** You can enable the private cloud service endpoint only for VPC clusters. Review which cloud service endpoints are enabled by selecting your cluster in the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} or in the command line by running `ibmcloud oc cluster get -c <cluster_name_or_ID>`. For more information, see the [Example scenarios for VPC cluster network setup](/docs/openshift?topic=openshift-plan_clusters#vpc-workeruser-master).
*   **Check whether your {{site.data.keyword.openshiftshort}} cluster has image pull secrets enabled.** To verify that your cluster has the default image pull secrets, [log in](/docs/openshift?topic=openshift-access_cluster), run `oc get secrets -n default` and look for the `all-icr-io` secret. To create the image pull images to {{site.data.keyword.registrylong_notm}} in your cluster, see [Updating existing clusters to use the API key image pull secret
](/docs/openshift?topic=openshift-registry#imagePullSecret_migrate_api_key).
*   **Check whether {{site.data.keyword.openshiftshort}} clusters are enabled with {{site.data.keyword.monitoringlong_notm}}.** For more information, see [Forwarding cluster and app metrics to {{site.data.keyword.monitoringlong_notm}}](/docs/openshift?topic=openshift-health-monitor#openshift_monitoring).
*   **Check whether {{site.data.keyword.openshiftshort}} clusters are enabled with {{site.data.keyword.la_full_notm}}.** For more information, see [Forwarding cluster and app logs to {{site.data.keyword.la_full_notm}}](/docs/openshift?topic=openshift-health#openshift_logging).
*   **Check whether {{site.data.keyword.openshiftshort}} Ingress is configured only with TLS v1.2 for all inbound traffic.** For more information, see [About Ingress](/docs/openshift?topic=openshift-ingress-about-roks4).
*   **Check whether the {{site.data.keyword.openshiftshort}} version is up-to-date.** You can review the cluster version by selecting your cluster in the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} or in the command line by running `ibmcloud oc cluster get -c <cluster_name_or_ID>`. For more information, see the [Version information and update actions](/docs/openshift?topic=openshift-openshift_versions).



