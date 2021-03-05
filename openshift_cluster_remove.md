---

copyright:
  years: 2014, 2021
lastupdated: "2021-03-05"

keywords: openshift, roks, rhos, rhoks, clusters, delete, remove

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



# Removing clusters
{: #remove}

Clusters that are created with a billable account must be removed manually when they are not needed anymore so that those clusters are no longer consuming resources.
{: shortdesc}

<p class="important">
No backups are created of your cluster or your data in your persistent storage. When you delete a cluster, you can choose to delete your persistent storage. Persistent storage that you provisioned by using a `delete` storage class is permanently deleted in IBM Cloud infrastructure if you choose to delete your persistent storage. If you provisioned your persistent storage by using a `retain` storage class and you choose to delete your storage, the cluster, the PV, and PVC are deleted, but the persistent storage instance in your IBM Cloud infrastructure account remains.</br>
</br><img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **Classic clusters only**: When you remove a cluster, you also remove any subnets that were automatically provisioned when you created the cluster and that you created by using the `ibmcloud oc cluster subnet create` command. However, if you manually added existing subnets to your cluster by using the `ibmcloud oc cluster subnet add` command, these subnets are not removed from your IBM Cloud infrastructure account and you can reuse them in other clusters.</br>
</br>When you delete your cluster, the default {{site.data.keyword.cloudcerts_short}} instance for your cluster, which is named in the format `kube-<cluster_ID>`, is also automatically deleted. Any certificates that are stored in the {{site.data.keyword.cloudcerts_short}} instance for your cluster are deleted when the {{site.data.keyword.cloudcerts_short}} instance is deleted.</p>

**Before you begin**:
* Note your cluster ID. You might need the cluster ID to investigate and remove related IBM Cloud infrastructure resources that are not automatically deleted with your cluster.
* Make sure that you have the [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-users#platform).
* If you want to delete the data in your persistent storage, review the delete options for the type of storage that you use.
  * [File storage](/docs/containers?topic=containers-file_storage#storage_delete_options)
  * [Block storage](/docs/containers?topic=containers-block_storage#cleanup) for classic clusters
  * [Block storage](/docs/containers?topic=containers-vpc-block#cleanup) for VPC clusters
  * [Object storage](/docs/cloud-object-storage?topic=cloud-object-storage-deleting-multiple-objects-patterns)
  * [Portworx](/docs/openshift?topic=openshift-portworx#portworx_cleanup)

**To remove a cluster**:

1. Optional: From the CLI, save a copy of all data in your cluster to a local YAML file.
  ```
  oc get all --all-namespaces -o yaml
  ```
  {: pre}

2. Remove the cluster.
  - From the {{site.data.keyword.cloud_notm}} console
    1.  Select your cluster and click **Delete** from the **More actions...** menu.

  - From the {{site.data.keyword.cloud_notm}} CLI
    1.  List the available clusters.

        ```
        ibmcloud oc cluster ls
        ```
        {: pre}

    2.  Delete the cluster.

        ```
        ibmcloud oc cluster rm --cluster <cluster_name_or_ID>
        ```
        {: pre}

    3.  Follow the prompts and choose whether to delete cluster resources, which include containers, pods, bound services, persistent storage, and secrets.
        - **Persistent storage**: If you [dynamically provisioned](/docs/openshift?topic=openshift-kube_concepts#dynamic_provisioning) storage with a storage class that sets `reclaimPolicy: Delete`, your persistent volume claim (PVC), persistent volume (PV), and the storage instance are automatically deleted when you delete the cluster. However, depending on when you delete the cluster, you might still see your storage instance in the {{site.data.keyword.cloud_notm}} console for up to 72 hours or until the new billing cycle begins. 

          For storage that was [statically provisioned](/docs/openshift?topic=openshift-kube_concepts#static_provisioning), or storage that you provisioned with a storage class that sets `reclaimPolicy: Retain`, the PVC and the PV are removed when you delete the cluster, but your storage instance and your data remain. You are still charged for your storage instance.

          To manually remove the storage and find frequently asked questions about storage removal, review the documentation for each storage type in the links in the **Before you begin** section.

Next steps:
- After it is no longer listed in the available clusters list when you run the `ibmcloud oc cluster ls` command, you can reuse the name of a removed cluster.
- <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **Classic clusters only**: If you kept the subnets, you can [reuse them in a new cluster](/docs/openshift?topic=openshift-subnets#subnets_custom) or manually delete them later from your IBM Cloud infrastructure portfolio.
- <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **VPC clusters only**: If you have infrastructure resources that you no longer want to use, such as the VPC or subnets, remove these resources in the VPC portal.
- If you kept the persistent storage, you can delete your storage later through the {{site.data.keyword.cloud_notm}} console for the corresponding storage service.


