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
  

# Why do pods remain in pending state?
{: #ts-app-pod-pending}

**Infrastructure provider**:
* <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC


When you run `oc get pods`, you can see pods that remain in a **Pending** state.
{: tsSymptoms}


If you just created the {{site.data.keyword.openshiftshort}} cluster, the worker nodes might still be configuring.
{: tsCauses}

If this cluster is an existing one:
*  You might not have enough capacity in your cluster to deploy the pod.
*  The pod might have exceeded a resource request or limit.


This task requires the {{site.data.keyword.cloud_notm}} IAM [**Administrator** platform access role](/docs/openshift?topic=openshift-users#checking-perms) for the cluster and the [**Manager** service access role](/docs/openshift?topic=openshift-users#checking-perms) for all namespaces.
{: tsResolve}

If you just created the {{site.data.keyword.openshiftshort}} cluster, run the following command and wait for the worker nodes to initialize.

```
oc get nodes
```
{: pre}

If this cluster is an existing one, check your cluster capacity.



1. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select your cluster.
2. Click **{{site.data.keyword.openshiftshort}} web console**.

3. Check if you have enough capacity in your cluster to deploy your pod.

4. If you don't have enough capacity in your cluster, resize your worker pool to add more nodes.

    1. Review the current sizes and flavors of your worker pools to decide which one to resize.

        ```
        ibmcloud oc worker-pool ls
        ```
        {: pre}

    2. Resize your worker pools to add more nodes to each zone that the pool spans.

        ```
        ibmcloud oc worker-pool resize --worker-pool <worker_pool> --cluster <cluster_name_or_ID> --size-per-zone <workers_per_zone>
        ```
        {: pre}

5. Optional: Check your pod resource requests.

    1. Confirm that the `resources.requests` values are not larger than the worker node's capacity. For example, if the pod request `cpu: 4000m`, or 4 cores, but the worker node size is only 2 cores, the pod cannot be deployed.

        ```
        oc get pod <pod_name> -o yaml
        ```
        {: pre}

    2. If the request exceeds the available capacity, [add a new worker pool](/docs/openshift?topic=openshift-add_workers#add_pool) with worker nodes that can fulfill the request.

6. If your pods still stay in a **pending** state after the worker node is fully deployed, review the [Kubernetes documentation](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-pod-replication-controller/#my-pod-stays-pending){: external} to further troubleshoot the pending state of your pod.




