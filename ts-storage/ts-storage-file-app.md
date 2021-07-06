---

copyright:
  years: 2014, 2021
lastupdated: "2021-07-01"

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
  
  
# Why can't my app access or write to PVCs?
{: #file_app_failures}

**Infrastructure provider**: <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

When you mount a PVC to your pod, you might experience errors when accessing or writing to the PVC.
{: shortdesc}

1. List the pods in your cluster and review the status of the pod.
   ```sh
   oc get pods
   ```
   {: pre}

2. Find the root cause for why your app cannot access or write to the PVC.
   ```sh
   oc describe pod <pod_name>
   ```
   {: pre}

   ```sh
   oc logs <pod_name>
   ```
   {: pre}

3. Review common errors that can occur when you mount a PVC to a pod.

| Symptom or error message | Description | Steps to resolve |
| --- | --- | --- |
| Your pod is stuck in a `ContainerCreating` state. `MountVolume.SetUp failed for volume ... read-only file system`. | The {{site.data.keyword.cloud_notm}} infrastructure back end experienced network problems. To protect your data and to avoid data corruption, {{site.data.keyword.cloud_notm}} automatically disconnected the file storage server to prevent write operations on NFS file shares. | See [File storage: File systems for worker nodes change to read-only](/docs/containers?topic=containers-readonly_nodes) |
| `write-permission` `do not have required permission` `cannot create directory '/bitnami/mariadb/data': Permission denied` | In your deployment, you specified a non-root user to own the NFS file storage mount path. By default, non-root users do not have write permission on the volume mount path for NFS-backed storage. | See [File storage: App fails when a non-root user owns the NFS file storage mount path](/docs/containers?topic=containers-nonroot) |
| After you specified a non-root user to own the NFS file storage mount path or deployed a Helm chart with a non-root user ID specified, the user cannot write to the mounted storage. | The deployment or Helm chart configuration specifies the security context for the pod's `fsGroup` (group ID) and `runAsUser` (user ID) | See [File storage: Adding non-root user access to persistent storage fails](/docs/containers?topic=containers-cs_storage_nonroot) |
{: caption="File Storage error messages" caption-side="top"}
{: summary="The columns are read from left to right. The first column has the symptom or error message. The second column describes the message. The third column provides steps to resolve the error."}


