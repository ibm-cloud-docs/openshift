---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-13"

keywords: kubernetes, openshift, roks, rhoks, rhos

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



# Setting up the {{site.data.keyword.redhat_notm}} Marketplace
{: #rh-marketplace}

With [{{site.data.keyword.redhat_full}} Marketplace](https://marketplace.redhat.com/en-us){: external}, you can deploy certified {{site.data.keyword.redhat_notm}} software from an operator-based catalog to your OpenShift Container Platform clusters, including {{site.data.keyword.openshiftlong}}.
{: shortdesc}

**Supported infrastructure providers**:
* <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC
* <img src="images/icon-satellite.svg" alt="{{site.data.keyword.satelliteshort}} infrastructure provider icon" width="15" style="width:15px; border-style: none"/> {{site.data.keyword.satelliteshort}}

**Required permissions**:
* The IAM **Operator** platform access role for the cluster in {{site.data.keyword.containershort_notm}}.
* The IAM **Manager** service access role in all namespaces (`cluster-admin` RBAC) for the cluster in {{site.data.keyword.containershort_notm}}.

<img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> {{site.data.keyword.redhat_notm}} Marketplace is available for clusters that run {{site.data.keyword.openshiftshort}} version 4 only.
{: note}

**Before you begin**:
*   Register for a [{{site.data.keyword.redhat_notm}} Marketplace account](https://marketplace.redhat.com/en-us/registration/redhat-marketplace){: external}.
*   [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
*   Make sure that the Operator Lifecycle Manager (OLM) pods in the `openshift-operator-lifecycle-manager` project and marketplace pods in the `openshift-marketplace` project are ready and running. You might have to restart a pod to return the pod to a healthy state.
    ```
    oc get pods -n openshift-operator-lifecycle-manager
    ```
    {: pre}

    ```
    oc get pods -n openshift-marketplace
    ```
    {: pre}

**To set up your cluster with {{site.data.keyword.redhat_notm}} Marketplace**:
1.  Follow the [{{site.data.keyword.redhat_notm}} Marketplace instructions](https://marketplace.redhat.com/en-us/workspace/clusters/add/register){: external} to create a namespace, operator, and global pull secret for the {{site.data.keyword.redhat_notm}} Marketplace.
2.  Verify that the global pull secret for the cluster is updated with the `registry.marketplace.redhat.com` secret.
    ```
    oc get secret pull-secret -n openshift-config --output="jsonpath={.data.\.dockerconfigjson}" | base64 --decode | grep "marketplace" -A4
    ```
    {: pre}
3.  To pick up the global configuration changes, reload all of the worker nodes in your cluster.
    1.  Note the **ID** of the worker nodes in your cluster.
        ```
        ibmcloud oc worker ls -c <cluster_name_or_ID>
        ```
        {: pre}
    2.  Reload each classic worker node, or replace each VPC worker node. You can reload or replace multiple worker nodes by including multiple `-w` flags, but make sure to leave enough worker nodes running at the same time for your apps to avoid an outage because they are reloaded concurrently.

        **Classic**: Reload worker nodes.
        ```
        ibmcloud oc worker reload -c <cluster_name_or_ID> -w <workerID_1> -w <workerID_2>
        ```
        {: pre}

        **VPC**: Replace worker nodes.
        ```
        ibmcloud oc worker replace -c <cluster_name_or_ID> -w <workerID_1> -w <workerID_2>
        ```
        {: pre}
4.  After your worker nodes are reloaded, verify that your cluster is listed in your [{{site.data.keyword.redhat_notm}} Marketplace workspace](https://marketplace.redhat.com/en-us/workspace/clusters){: external}.

Now, you can install and manage software from {{site.data.keyword.redhat_notm}} Marketplace in your cluster. For more information, see the [{{site.data.keyword.redhat_notm}} Marketplace documentation](https://marketplace.redhat.com/en-us/documentation/){: external}.
