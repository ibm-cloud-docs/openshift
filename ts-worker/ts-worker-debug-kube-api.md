---

copyright:
  years: 2014, 2021
lastupdated: "2021-05-26"

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
{:terraform: .ph data-hd-interface='terraform'}
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
  
  
# Debugging worker nodes with Kubernetes API
{: #debug-kube-nodes}

If you have access to the cluster, you can debug the worker nodes by using the Kubernetes API on the `Node` resource.
{: shortdesc}

Before you begin, make sure that you have the **Manager** service access role in all namespaces for the cluster, which corresponds to the `cluster-admin` RBAC role.

1.  [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
2.  List the worker nodes in your cluster and note the **NAME** of the worker nodes that are not in a `Ready` **STATUS**. Note that the **NAME** is the private IP address of the worker node.
    ```
    oc get nodes
    ```
    {: pre}
3.  Describe the each worker node, and review the `Conditions` section in the output.
    * `Type`: The type of condition that might affect the worker node, such as memory or disk pressure.
    * `LastTransitionTime`: The most recent time that the status was updated. Use this time to identify when the issue with your worker node began, which can help you further troubleshoot the issue.
    
    ```
    oc describe node <name>
    ```
    {: pre}
4.  Check the usage of the worker nodes.
    1.  In the `Allocated resources` output of the previous command, review the workloads that use the worker node's CPU and memory resources. You might notice that some pods do not set resource limits, and are consuming more resources than you expected. If so, adjust the resource usage of the pods.
    2.  Review the percentage of usage of CPU and memory across the worker nodes in your cluster. If the usage is consistently over 80%, [add more worker nodes](/docs/openshift?topic=openshift-add_workers) to the cluster to support the workloads.
5.  Check for custom admission controllers that are installed in your cluster. Admission controllers often block required pods from running, which might make your worker nodes enter a critical state. If you have custom admission controllers, try removing them with `oc delete`. Then, check if the worker node issue resolves.
    ```
    kubectl get mutatingwebhookconfigurations --all-namespaces
    ```
    {: pre}

    ```
    kubectl get validatingwebhookconfigurations --all-namespaces
    ```
    {: pre}
6.  If you configured [log forwarding](/docs/openshift?topic=openshift-health), review the node-related logs from the following paths.
    ```
    /var/log/containerd.log
    /var/log/kubelet.log
    /var/log/kube-proxy.log
    /var/log/syslog
    ```
    {: screen}
7.  Check that a workload deployment does not cause the worker node issue.
    1.  Taint the worker node with the issue.
        ```
        oc taint node NODEIP ibm-cloud-debug-isolate-customer-workload=true:NoExecute
        ```
        {: pre}
    2.  Make sure that you deleted any custom admission controllers as described in step 5.
    3.  Restart the worker node.
        * **Classic**: Reload the worker node.
          ```
          ibmcloud oc worker reload -c <cluster_name_or_ID> --worker <worker_ID>
          ```
          {: pre}
        * **VPC**: Replace the worker node.
          ```
          ibmcloud oc worker replace -c <cluster_name_or_ID> --worker <worker_ID> --update
          ```
          {: pre}
    4.  Wait for the worker node to finish restarting. If the worker node enters a healthy state, the issue is likely caused by a workload.
    5.  Schedule one workload at a time onto the worker node to see which workload causes the issue. To schedule the workloads, add the following toleration.
        ```
        tolerations:
        - effect: NoExecute
          key: ibm-cloud-debug-isolate-customer-workload
          operator: Exists
        ```
        {: copyblock}
    6.  After you identify the workload that causes the issue, continue with [Debugging app deployments](/docs/openshift?topic=openshift-debug_apps).
