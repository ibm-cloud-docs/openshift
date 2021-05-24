---

copyright:
  years: 2014, 2021
lastupdated: "2021-05-21"

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
  
  
# Block storage: Why does block storage change to read-only?
{: #readonly_block}

**Infrastructure provider**:
* <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

{: tsSymptoms}
You might see the following symptoms:
- When you run `oc get pods -o wide`, you see that multiple pods on the same worker node are stuck in the `ContainerCreating` or `CrashLoopBackOff` state. All these pods use the same block storage instance.
- When you run a `oc describe pod` command, you see the following error in the **Events** section: `MountVolume.SetUp failed for volume ... read-only`.

{: tsCauses}
If a network error occurs while a pod writes to a volume, IBM Cloud infrastructure protects the data on the volume from getting corrupted by changing the volume to a read-only mode. Pods that use this volume cannot continue to write to the volume and fail.

{: tsResolve}
1. Check the version of the {{site.data.keyword.cloud_notm}} Block Storage plug-in that is installed in your cluster.
   ```sh
   helm list --all-namespaces
   ```
   {: pre}

2. Verify that you use the [latest version of the {{site.data.keyword.cloud_notm}} Block Storage plug-in](https://cloud.ibm.com/kubernetes/helm/iks-charts/ibmcloud-block-storage-plugin). If not, [update your plug-in](/docs/containers?topic=containers-block_storage#update_block).
3. If you used a Kubernetes deployment for your pod, restart the pod that is failing by removing the pod and letting Kubernetes re-create it. If you did not use a deployment, retrieve the YAML file that was used to create your pod by running `oc get pod <pod_name> -o yaml >pod.yaml`. Then, delete and manually re-create the pod.
    ```sh
    oc delete pod <pod_name>
    ```
    {: pre}

4. Check whether re-creating your pod resolved the issue. If not, reload the worker node.
   1. Find the worker node where your pod runs and note the private IP address that is assigned to your worker node.
      ```sh
      oc describe pod <pod_name> | grep Node
      ```
      {: pre}

      **Example output**:
      ```sh
      Node:               10.75.XX.XXX/10.75.XX.XXX
      Node-Selectors:  <none>
      ```
      {: screen}

   2. Retrieve the **ID** of your worker node by using the private IP address from the previous step.
      ```sh
      ibmcloud oc worker ls --cluster <cluster_name_or_ID>
      ```
      {: pre}

   3. Gracefully [reload the worker node](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_reload).



