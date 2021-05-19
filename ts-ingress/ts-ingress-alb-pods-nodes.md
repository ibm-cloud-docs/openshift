---

copyright:
  years: 2014, 2021
lastupdated: "2021-05-19"

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
  
  
# Version 3.11: Why do ALB pods not deploy to worker nodes?
{: #alb-pod-affinity}

**Infrastructure provider and version**:
* <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="../images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> {{site.data.keyword.openshiftshort}} version 3.11

{: tsSymptoms}
When you run `oc get pods -n kube-system | grep alb`, either no ALB pods or only some ALB pods successfully deployed to your worker nodes. When you describe an ALB pod by running `oc describe pod -n kube-system <pod_name>`, you see a message similar to the following in the **Events** section of the output.
```
0/3 nodes are available: 1 node(s) didn’t match pod affinity/anti-affinity, 2 node(s) didn’t match node selector.
```
{: screen}

{: tsCauses}
Ingress requires at least two worker nodes per zone to ensure high availability and apply periodic updates. By default, ALB pods have two replicas. However, ALB pods have anti-affinity rules to ensure that only one pod is scheduled to each worker node for high availability. When only one worker node exists per zone in a classic or VPC cluster, or if only one worker node exists on a VLAN that your classic cluster is attached to, ALB pods cannot deploy correctly.

{: tsResolve}

1. Check the number of worker nodes per zone in your cluster.
  ```
  ibmcloud oc worker ls -c <cluster_name_or_ID>
  ```
  {: pre}
  * Classic and VPC clusters: If only one worker node exists in a zone, increase the number of worker nodes in that zone.
    * **If you do not use edge nodes**: Ensure that at least two worker nodes exist in each zone by [resizing an existing worker pool](/docs/containers?topic=containers-add_workers#resize_pool), [creating a new worker pool in a VPC cluster](/docs/containers?topic=containers-add_workers#vpc_add_pool), or [creating a new worker pool in a classic cluster](/docs/containers?topic=containers-add_workers#add_pool).
    * **If you use edge nodes**: Ensure that at least two [edge worker nodes](/docs/containers?topic=containers-edge) are enabled in each zone.
  * Classic clusters only: If more than one worker node exists in each zone of your classic cluster, your worker nodes might be connected to different VLANs within one zone so that only one worker node exists on a private VLAN. Continue to the next step.

2. For each worker node in one zone, get the private VLAN that the worker node is attached to.
  ```
  ibmcloud oc worker get -w <worker_ID> -c <cluster_name_or_ID>
  ```
  {: pre}

3. If only one worker node exists on a private VLAN, and the other worker nodes in the zone are attached to a different private VLAN, [create a new worker pool](/docs/containers?topic=containers-add_workers#add_pool) with a size of at least one worker node. When you add a zone to the worker pool in step 6, specify the same zone and private VLAN as the worker node that you previously identified.

4. Repeat these steps for each zone in your cluster to ensure that more than one worker node exists on a private VLAN.

After the new worker nodes deploy, the ALB pods are automatically scheduled to deploy to those worker nodes.
