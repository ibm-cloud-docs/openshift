---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-09"

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
  
  
# Classic: Why can't I add worker nodes with an invalid VLAN ID?
{: #suspended}

**Infrastructure provider**: <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

{: tsSymptoms}
Your {{site.data.keyword.cloud_notm}} account was suspended, or all worker nodes in your cluster were deleted. After the account is reactivated, you cannot add worker nodes when you try to resize or rebalance your worker pool. You see an error message similar to the following:

```
SoftLayerAPIError(SoftLayer_Exception_Public): Could not obtain network VLAN with id #123456.
```
{: screen}

{: tsCauses}
When an account is suspended, the worker nodes within the account are deleted. If a cluster has no worker nodes, IBM Cloud infrastructure reclaims the associated public and private VLANs. However, the cluster worker pool still has the previous VLAN IDs in its metadata and uses these unavailable IDs when you rebalance or resize the pool. The nodes fail to create because the VLANs are no longer associated with the cluster.

{: tsResolve}

You can [delete your existing worker pool](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_rm), then [create a new worker pool](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_create).

Alternatively, you can keep your existing worker pool by ordering new VLANs and using these to create new worker nodes in the pool.

Before you begin: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1.  To get the zones that you need new VLAN IDs for, note the **Location** in the following command output. **Note**: If your cluster is a multizone, you need VLAN IDs for each zone.

    ```
    ibmcloud oc cluster ls
    ```
    {: pre}

2.  Get a new private and public VLAN for each zone that your cluster is in by [contacting {{site.data.keyword.cloud_notm}} support](/docs/vlans?topic=vlans-ordering-premium-vlans#ordering-premium-vlans).

3.  Note the new private and public VLAN IDs for each zone.

4.  Note the name of your worker pools.

    ```
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

5.  Use the `zone network-set` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_zone_network_set) to change the worker pool network metadata.

    ```
    ibmcloud oc zone network-set --zone <zone> --cluster <cluster_name_or_ID> -- worker-pool ls <worker-pool> --private-vlan <private_vlan_ID> --public-vlan <public_vlan_ID>
    ```
    {: pre}

6.  **Multizone cluster only**: Repeat **Step 5** for each zone in your cluster.

7.  Rebalance or resize your worker pool to add worker nodes that use the new VLAN IDs. For example:

    ```
    ibmcloud oc worker-pool resize --cluster <cluster_name_or_ID> --worker-pool <worker_pool> --size-per-zone <number_of_workers_per_zone>
    ```
    {: pre}

8.  Verify that your worker nodes are created.

    ```
    ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <worker_pool>
    ```
    {: pre}


