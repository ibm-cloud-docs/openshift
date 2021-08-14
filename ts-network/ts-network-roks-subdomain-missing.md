---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-14"

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
  

# Why is my cluster missing the public `containers.appdomain.cloud` subdomain?
{: #roks_ts_subdomain}
{: troubleshoot}
{: support}

**Infrastructure provider**:
* <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

{: tsSymptoms}
When you expose an app through a router subdomain, you get a local subdomain instead of a public route, in the format: `<service_name>-<project_name>.router.default.svc.cluster.local`.

When you try to open the {{site.data.keyword.openshiftshort}} web console or another app route in your browser, you might see an error similar to the following.

```
Application is not available
The application is currently not serving requests on this endpoint.
```
{: screen}

{: tsCauses}
After the cluster is created and enters a **normal** state, the router subdomain networking and load balancing components still take some time to deploy. If you expose your app before the networking components fully provision, or if the components experience an error, your apps can only be exposed internally with the default router's `svc.cluster.local` domain.

When the components fully provision, a public router subdomain is available for your apps, in the format `<cluster-name>-<accountID-hashed>-<ssll>.<region>.containers.appdomain.cloud`.

{: tsResolve}
1. After you create a cluster, wait some time before you expose your apps, even after the cluster enters a **normal** state.
2. Check the **Master Status**. If the **Master Status** is not **Ready**, [review its status](/docs/openshift?topic=openshift-debug_master) and follow any troubleshooting information to resolve the issue.   
    ```
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}

3. Check that your cluster has public connectivity so that the networking components can talk to the master as they deploy.
    * <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC clusters with public and private cloud service endpoints enabled: [Ensure that a public gateway is enabled on each subnet](/docs/openshift?topic=openshift-vpc-subnets#create_vpc_subnet) that your cluster is attached to. Public gateway are required for default components such as the web console and OperatorHub to use a secure, public connection to complete actions such as pulling images from remote, private registries. Note that if only the private service endpoint is enabled for your cluster, no public gateway is required because the private cloud service endpoint is used by default to access OpenShift components such as the OpenShift web console or OperatorHub.
    * <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic clusters:
        * In the output of Step 2, check that your cluster has a **Public Service Endpoint URL**. If your cluster does not have a public cloud service endpoint, [enable it](/docs/openshift?topic=openshift-cs_network_cluster#set-up-public-se).
        * Check that at least some of the worker nodes in your cluster have a **Public IP** address. If no worker node does, you must [set up public VLANs for at least one worker pool](/docs/openshift?topic=openshift-cs_network_cluster#change-vlans).
          ```
          ibmcloud oc workers -c <cluster_name_or_ID>
          ```
          {: pre}

4. In the output of Step 2, check that the **Ingress Subdomain** is available. The Ingress components in your cluster must provision before the router components can be created. If the **Ingress Subdomain** and **Ingress Secret** are not available, see [Why does no Ingress subdomain exist after cluster creation?](/docs/openshift?topic=openshift-ingress_subdomain).
5. Check that the **Hostname** of the router subdomain is in the format: `<cluster-name>-<accountID-hashed>-<ssll>.<region>.containers.appdomain.cloud`.
    ```
    ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>
    ```
    {: pre}

    *  If the router subdomain is not updated after two hours of creating the cluster, review the **Master Status** of the cluster again, and follow any troubleshooting steps to resolve the issue.

If the troubleshooting steps do not resolve the issue, see [Getting help](/docs/openshift?topic=openshift-get-help).


