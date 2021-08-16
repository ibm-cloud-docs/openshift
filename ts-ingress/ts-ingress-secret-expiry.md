---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-13"

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
  

# Why isn't the Ingress secret expiration date updated?
{: #sync_cert_dates}

**Infrastructure provider**:
* <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC


When you run `ibmcloud oc cluster get -c <cluster_name_or_ID>` or `ibmcloud oc ingress status -c <cluster_name_or_ID>`, you see the following **Ingress Message**:
{: tsSymptoms}

```
The expiration dates reported by Ingress secrets are out of sync across namespaces. To resynchronize the expiration dates, see http://ibm.biz/ingress-secret-sync
```
{: screen}

When you run `ibmcloud oc ingress secret ls -c <cluster_name_or_ID>`, you notice that old expiration dates are listed for some certificates.

In some cases, the expiration date that is reported by the secrets in some namespaces in your cluster can become out of sync with the expiration date of secrets for the same certificate in other namespaces. Even though your actual certificate is renewed, a secret in your cluster can show an older expiration date that is not updated to the most recent expiration date for the certificate.
{: tsCauses}

However, a secret for this certificate in another namespace might show the correct expiration date.


To resynchronize the expiration dates, you can regenerate the secrets for your Ingress subdomain certificate.
{: tsResolve}

1. Get your **Ingress Subdomain**.
    ```
    ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep 'Ingress Subdomain'
    ```
    {: pre}

2. Regenerate the Ingress subdomain secret. The certificate is renewed, a new expiration date is generated, and the updates are synchronized across the secret in different namespaces. Secret regeneration is not disruptive, and traffic continues to flow while the secret regenerates.
    ```
    ibmcloud oc nlb-dns secret regenerate -c <cluster_name_or_ID> --nlb-subdomain <ingress_subdomain>
    ```
    {: pre}

    It might take 30 minutes or longer for the secret regeneration to complete.
    {: note}

3. List all secrets associated with the certificate for your Ingress subdomain. In the output, verify that the **Expiration date** for the secrets are more than 30 days later than today.
    ```
    ibmcloud oc ingress secret ls -c <cluster_name_or_ID> | grep <ingress_subdomain>
    ```
    {: pre}

    Example output:
    ```
    Name                                              Namespace        CRN                                                                                                                                                           Expires On                 Domain                                                                                  Status
    mycluster-35366fb2d3d90fd50548180f69e7d12a-0000   default          crn:v1:bluemix:public:cloudcerts:eu-de:a/6ef045fd2b43266cfe8e6388dd2ec098:4ebc1d51-8a74-4675-8c4c-b2922ceba2d4:certificate:70f08c8a0fc1eed1f147b28443ba6dcd   2020-12-10T18:00:58+0000   mycluster-35366fb2d3d90fd50548180f69e7d12a-0000.eu-de.containers.appdomain.cloud     created
    mycluster-35366fb2d3d90fd50548180f69e7d12a-0000   ibm-cert-store   crn:v1:bluemix:public:cloudcerts:eu-de:a/6ef045fd2b43266cfe8e6388dd2ec098:4ebc1d51-8a74-4675-8c4c-b2922ceba2d4:certificate:70f08c8a0fc1eed1f147b28443ba6dcd   2020-12-10T18:00:58+0000   *.mycluster-35366fb2d3d90fd50548180f69e7d12a-0000.eu-de.containers.appdomain.cloud   created
    mycluster-35366fb2d3d90fd50548180f69e7d12a-0000   kube-system      crn:v1:bluemix:public:cloudcerts:eu-de:a/6ef045fd2b43266cfe8e6388dd2ec098:4ebc1d51-8a74-4675-8c4c-b2922ceba2d4:certificate:70f08c8a0fc1eed1f147b28443ba6dcd   2020-12-10T18:00:58+0000   *.mycluster-35366fb2d3d90fd50548180f69e7d12a-0000.eu-de.containers.appdomain.cloud   created
    ```
    {: screen}

4. Optional: Other secrets for network load balancer (NLB) subdomains in your cluster might report expiration dates that are out of sync with the certificate's expiration date. You can run the following steps to resynchronize the expiration dates for other secrets in your cluster

    1. List all NLB subdomains in your cluster.
    ```
    ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>
    ```
    {: pre}

    2. For each subdomain besides the Ingress subdomain, regenerate its secret. The certificate is renewed, a new expiration date is generated, and the updates are synchronized across the secret in different namespaces. Secret regeneration is not disruptive, and traffic continues to flow while the secret regenerates. Note that it might take 30 minutes or longer for the secret regeneration to complete.
    ```
    ibmcloud oc nlb-dns secret regenerate -c <cluster_name_or_ID> --nlb-subdomain <NLB_DNS_subdomain>
    ```
    {: pre}

    3. List all secrets associated with the certificate for your Ingress subdomain. In the output, verify that the **Expiration date** for the secrets are more than 30 days later than today.
    ```
    ibmcloud oc ingress secret ls -c <cluster_name_or_ID> | grep <ingress_subdomain>
    ```
    {: pre}


