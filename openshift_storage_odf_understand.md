---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-26"

keywords: openshift, openshift data foundation, openshift container storage, vpc, roks, satellite

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
{:release-note: data-hd-content-type='release-note'}
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
  

# Understanding OpenShift Data Foundation
{: #ocs-storage-prep}

OpenShift Data Foundation is a storage solution that consists of open source technologies [Ceph](https://docs.ceph.com/en/latest/start/intro/){: external}, [Noobaa](https://www.noobaa.io/){: external}, and [Rook](https://rook.io/){: external}. ODF allows you to provision and manage File, Block, and Object storage for your containerized workloads in {{site.data.keyword.openshiftlong}} clusters. Unlike other storage solutions where you might need to configure separate drivers and operators for each type of storage, ODF is a unified solution capable of adapting or scaling to your storage needs. You can also deploy ODF on any OCP cluster.
{: shortdesc}

The OpenShift Data Foundation add-on is available as a technology preview and might change without prior notice. Don't use this add-on for production workloads.
{: preview}

For an overview of the features and benefits, see [OpenShift Data Foundation](https://www.redhat.com/en/technologies/cloud-computing/openshift-data-foundation){: external}.

<br />


## Architecture overview
{: #odf-ov}
Review the following diagram and table to learn more about OpenShift Data Foundation.
{: shortdesc}

![ODF Architecture](images/ODF_components.svg "ODF Architecture")


| Number | ODF component | Description |
| --- | --- | --- |
| 1 | OpenShift Data Foundation storage classes | When you deploy ODF, the ODF operator creates File, Block, and Object storage classes in your cluster. Reference these storage classes in your PVCs and to claim storage for your apps. |
| 2 | Object Storage Daemon (OSD) block storage device | The OSD devices provide application storage in your cluster. Each OSD is a raw block storage device that can be a local disk on your worker node or dynamically provisioned when you deploy ODF. In VPC clusters, your OSD block storage devices are dynamically provisioned by using the {{site.data.keyword.block_storage_is_short}} driver. In {{site.data.keyword.satelliteshort}} clusters, you can use local volumes on your worker nodes, or dynamically provision block storage devices by using a block storage driver that supports dynamic provisioning. In Classic clusters, the OSD block devices are local disks on your worker nodes. When you deploy ODF, each device is mounted by an OSD pod. The total storage that is available to your applications is equal to the `osdSize` multiplied by the `numOfOsd`. |
| 3 | Object Storage Daemon (OSD) pods | The OSD pods manage data placement and replication across your storage devices. |
| 4 | Monitor (Mon) pods | The Monitor pods keep a map of your OpenShift Data Foundation storage cluster and monitor storage cluster health. |
| 5 | Monitor (Mon) block storage device | The monitor storage devices are the underlying storage devices for the monitor pods. Each monitor device is a raw block storage device that can be a local disk on your worker node or dynamically provisioned when you deploy ODF. Each device provides storage to a monitor pod. |
{: caption="ODF architecture overview" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the diagram number of ODF resource. The second column is the name of the resource. The third column is a brief description of the resource."}




## Deploying OpenShift Data Foundation
{: #odf-deploy-options}

Review the following deployment options for your infrastructure provider.
{: shortdesc}


| Infrastructure provider | Disk type | Installation instructions |
| --- | --- | --- |
| Virtual Private Cloud (VPC) | Remote, dynamically provisioned disks | [Deploying OpenShift Data Foundation on VPC clusters](/docs/openshift?topic=openshift-deploy-odf-vpc) |
| {{site.data.keyword.satelliteshort}} | Remote, dynamically provisioned disks or local disks on the worker nodes | [Deploying OpenShift Data Foundation on {{site.data.keyword.satelliteshort}} clusters](/docs/openshift?topic=openshift-deploy-odf-sat) |
| Classic | Local disks on the worker nodes | [Deploying OpenShift Data Foundation on Classic clusters](/docs/openshift?topic=openshift-deploy-odf-classic) |
{: caption="ODF deployment options" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the infrastructure provider. The second column indicates the supported disk type. The third column is a link to the installation instructions."}




