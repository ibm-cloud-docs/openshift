---

copyright:
  years: 2014, 2021
lastupdated: "2021-05-14"

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
  
  


# IBM Cloud services and third-party integrations
{: #ibm-3rd-party-integrations}

You can use {{site.data.keyword.cloud}} platform and infrastructure services, and other third-party integrations to add extra capabilities to your cluster.
{: shortdesc}

## IBM Cloud services
{: #ibm-cloud-services}

Review the following information to see how {{site.data.keyword.cloud_notm}} platform and infrastructure services are integrated with {{site.data.keyword.openshiftlong_notm}} and how you can use them in your cluster.
{: shortdesc}

### IBM Cloud platform services
{: #platform-services}

All {{site.data.keyword.cloud_notm}} platform services that support service keys can be integrated by using {{site.data.keyword.openshiftlong_notm}} [service binding](/docs/openshift?topic=openshift-service-binding).
{: shortdesc}

Service binding is a quick way to create service credentials for an {{site.data.keyword.cloud_notm}} service and store these credentials in a Kubernetes secret in your cluster. The Kubernetes secret is automatically encrypted in etcd to protect your data. Your apps can use the credentials in the secret to access your {{site.data.keyword.cloud_notm}} service instance.

Services that do not support service keys usually provide an API that you can directly use in your app.

### IBM Cloud classic infrastructure services
{: #infrastructure-services}

Because {{site.data.keyword.openshiftlong_notm}} lets you create a cluster on {{site.data.keyword.cloud_notm}} classic infrastructure, some classic infrastructure services, such as Virtual Servers, Bare Metal Servers, or VLANs are fully integrated into {{site.data.keyword.openshiftlong_notm}}. You create and work with these service instances by using the {{site.data.keyword.openshiftlong_notm}} API, CLI, or console.
{: shortdesc}

Supported persistent storage solutions, such as {{site.data.keyword.cloud_notm}} File Storage, {{site.data.keyword.cloud_notm}} Block Storage, or {{site.data.keyword.cos_full}} are integrated as Kubernetes flex drivers and can be set up by using [Helm charts](/docs/openshift?topic=openshift-helm). The Helm chart automatically sets up Kubernetes storage classes, the storage provider, and the storage driver in your cluster. You can use the storage classes to provision persistent storage by using persistent volume claims (PVCs). For more information, see [Planning highly available persistent storage](/docs/openshift?topic=openshift-storage_planning).

To secure your cluster network or connect to an on-prem data center, you can configure one of the following options:
- [strongSwan IPSec VPN Service](/docs/openshift?topic=openshift-vpn#vpn-setup)
- [{{site.data.keyword.BluDirectLink}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
- [Virtual Router Appliance (VRA)](/docs/openshift?topic=openshift-vpn#vyatta)
- [Fortigate Security Appliance (FSA)](/docs/vmwaresolutions/services?topic=vmwaresolutions-fsa_considerations)



### IBM Cloud VPC infrastructure services
{: #vpc-infrastructure-services}

With {{site.data.keyword.openshiftlong_notm}}, you can create a standard cluster in a [Virtual Private Cloud (VPC)](/docs/vpc?topic=vpc-getting-started). A VPC gives you the security of a private cloud environment with the dynamic scalability of a public cloud.
{: shortdesc}

Before you can create a VPC cluster, you must have a VPC and at least one VPC subnet that you provision by using the {{site.data.keyword.cloud_notm}} console, CLI, or API. You manage these resources in the VPC dashboard directly. When you create your cluster, worker nodes are automatically provisioned as [{{site.data.keyword.vsi_is_short}}](/docs/vpc?topic=vpc-about-advanced-virtual-servers) instances and you can view and manage these instances in {{site.data.keyword.openshiftlong_notm}} only.

To add persistent storage to your VPC cluster, you can use the [{{site.data.keyword.block_storage_is_short}} add-on](/docs/openshift?topic=openshift-vpc-block). The add-on sets up pre-defined Kubernetes storage classes, the storage provider, and the storage driver in your cluster so that you can provision {{site.data.keyword.block_storage_is_short}} by using Kubernetes persistent volume claims (PVCs).

To secure your cluster network traffic, you can modify the default security group for your worker nodes. For more information, see [Security in your {{site.data.keyword.vpc_short}}](/docs/vpc?topic=vpc-security-in-your-vpc).

To connect to a different VPC or to an on-prem data center, use the [VPN for VPC](/docs/vpc?topic=vpc-vpn-onprem-example) service.  



## Kubernetes community and open source integrations
{: #kube-community-tools}

Because you own the standard clusters that you create in {{site.data.keyword.openshiftlong_notm}}, you can choose to install third-party solutions to add extra capabilities to your cluster.
{: shortdesc}

Some open source technologies, such as Portworx are tested by IBM and provided as managed add-ons, Helm charts, or {{site.data.keyword.cloud_notm}} services that are operated by the service provider in partnership with IBM. These open source tools are fully integrated into the {{site.data.keyword.cloud_notm}} billing and support system.

You can install other open source tools in your cluster, but these tools might not be managed, supported, or verified to work in {{site.data.keyword.openshiftlong_notm}}.

Supported integrations depend on the container platform, the infrastructure provider, and the cluster type that you choose. For more information, see [Supported {{site.data.keyword.cloud_notm}} and third-party integrations](/docs/openshift?topic=openshift-supported_integrations).
{: note}

### Integrations operated in partnership
{: #open-source-partners}

For more information about {{site.data.keyword.openshiftlong_notm}} partners and the benefit of each solution that they provide, see [{{site.data.keyword.openshiftlong_notm}} partners](/docs/openshift?topic=openshift-service-partners).

### Managed add-ons
{: #cluster-add-ons}
{{site.data.keyword.openshiftlong_notm}} integrates popular open source integrations by using [managed add-ons](/docs/openshift?topic=openshift-managed-addons). Managed add-ons are an easy way to install an open source tool in your cluster that is tested by IBM and approved to be used in {{site.data.keyword.openshiftlong_notm}}.

Managed add-ons are fully integrated into the {{site.data.keyword.cloud_notm}} support organization. If you have a question or an issue with using the managed add-ons, you can use one of the {{site.data.keyword.openshiftlong_notm}} support channels. For more information, see [Getting help and support](/docs/openshift?topic=openshift-get-help).

If the tool that you add to your cluster incurs costs, these costs are automatically integrated and listed as part of your monthly {{site.data.keyword.cloud_notm}} billing. The billing cycle is determined by {{site.data.keyword.cloud_notm}} depending on when you enabled the add-on in your cluster.

### Other third-party integrations
{: #kube-community-helm}

You can install any third-party open source tool that integrates with Kubernetes. For example, the Kubernetes community designates certain Helm charts `stable` or `incubator`. Note that these charts or tools are not verified to work in {{site.data.keyword.openshiftlong_notm}}. If the tool requires a license, you must purchase a license before you use the tool. For an overview of available Helm charts from the Kubernetes community, see the `kubernetes` and `kubernetes-incubator` repositories in the [Helm charts ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/helm) catalog.
{: shortdesc}

Any costs that incur by using a third-party open source integration are not included in your monthly {{site.data.keyword.cloud_notm}} bill.

Installing third-party open source integrations or Helm charts from the Kubernetes community might change the default cluster configuration and can bring your cluster into an unsupported state. If you run into an issue with using any of these tools, consult the Kubernetes community or the service provider directly.
{: important}

### Extending {{site.data.keyword.openshiftshort}} API and software with CRDs and Operators
{: #kube-crd-operators}

You might use custom resource definitions (CRDs) to extend the {{site.data.keyword.openshiftshort}} API to create and orchestrate custom objects in your cluster. Operators combine custom resources and controllers to automate the lifecycle of app, such as installing and rolling out updates to a customized app from a catalog in your cluster. 

For more information, see [Operators](/docs/openshift?topic=openshift-operators).


