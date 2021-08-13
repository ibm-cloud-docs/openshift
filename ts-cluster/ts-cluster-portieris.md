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
  

# Why is my Portieris cluster image security enforcement installation canceled?
{: #portieris_enable}

**Infrastructure provider**:
    * <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
    * <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC


Portieris image security enforcement add-on does not install.  You see a master status similar to the following:
{: tsSymptoms}

```
Image security enforcement update cancelled. CAE008: Cannot enable Portieris image security enforcement because the cluster already has a conflicting image admission controller installed. For more information, see the troubleshooting docs: 'https://ibm.biz/portieris_enable'
```
{: screen}


Your cluster has a conflicting image admission controller already installed, which prevents the image security enforcement cluster add-on from installing.
{: tsCauses}

When you have more than one image admission controller in your cluster, pods might not run.

Potential conflicting image admission controller sources include:
*   The deprecated [container image security enforcement Helm chart](/docs/Registry?topic=Registry-security_enforce).
*   A previous manual installation of the open source [Portieris](https://github.com/IBM/portieris){: external} project.


Identify and remove the conflicting image admission controller.
{: tsResolve}

1. Check for existing image admission controllers.
    *   Check if you have an existing container image security enforcement deployment in your cluster. If no output is returned, you do not have the deployment.
        ```
        oc get deploy cise-ibmcloud-image-enforcement -n ibm-system
        ```
        {: pre}

        Example output:
        ```
        NAME                              READY   UP-TO-DATE   AVAILABLE   AGE
        cise-ibmcloud-image-enforcement   3/3     3            3           129m
        ```
        {: pre}

    *   Check if you have an existing Portieris deployment in your cluster. If no output is returned, you do not have the deployment.
        ```
        oc get deployment --all-namespaces -l app=portieries
        ```
        {: pre}

        Example output:
        ```
        NAMESPACE     NAME        READY   UP-TO-DATE   AVAILABLE   AGE
        portieris     portieris   3/3     3            3           8m8s
        ```
        {: pre}

2. Uninstall the conflicting deployment.
    *   For container image security enforcement, see the [{{site.data.keyword.registrylong_notm}} documentation](/docs/Registry?topic=Registry-security_enforce#remove).
    *   For Portieris, see the [open source documentation](https://github.com/IBM/portieris#uninstalling-portieris){: external}.
3. Confirm that conflicting admission controllers are removed by checking that the cluster no longer has a mutating webhook configuration for an image admission controller.
    ```
    oc get MutatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Example output:
    ```
    Error from server (NotFound): mutatingwebhookconfigurations.admissionregistration.k8s.io "image-admission-config" not found
    ```
    {: pre}

4. Retry the installing the add-on by running the `ibmcloud oc cluster image-security enable` command.


