---

copyright:
  years: 2014, 2020
lastupdated: "2020-04-13"

keywords: kubernetes, openshift, roks, rhoks, rhos

subcollection: openshift

---

{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}



# IBM Cloud services and third-party integrations
{: #ibm-3rd-party-integrations}

You can use {{site.data.keyword.cloud}} platform and infrastructure services, and other third-party integrations to add extra capabilities to your cluster.
{: shortdesc}

## IBM Cloud services
{: #ibm-cloud-services}

Review the following information to see how {{site.data.keyword.cloud_notm}} platform and infrastructure services are integrated with Red Hat OpenShift on IBM Cloud and how you can use them in your cluster.
{: shortdesc}

### IBM Cloud platform services
{: #platform-services}

All {{site.data.keyword.cloud_notm}} platform services that support service keys can be integrated by using Red Hat OpenShift on IBM Cloud [service binding](/docs/openshift?topic=openshift-service-binding).
{: shortdesc}

Service binding is a quick way to create service credentials for an {{site.data.keyword.cloud_notm}} service and store these credentials in a Kubernetes secret in your cluster. The Kubernetes secret is automatically encrypted in etcd to protect your data. Your apps can use the credentials in the secret to access your {{site.data.keyword.cloud_notm}} service instance.

Services that do not support service keys usually provide an API that you can directly use in your app.

### IBM Cloud classic infrastructure services
{: #infrastructure-services}

Because Red Hat OpenShift on IBM Cloud lets you create a cluster on {{site.data.keyword.cloud_notm}} classic infrastructure, some classic infrastructure services, such as Virtual Servers, Bare Metal Servers, or VLANs are fully integrated into Red Hat OpenShift on IBM Cloud. You create and work with these service instances by using the Red Hat OpenShift on IBM Cloud API, CLI, or console.
{: shortdesc}

Supported persistent storage solutions, such as {{site.data.keyword.cloud_notm}} File Storage, {{site.data.keyword.cloud_notm}} Block Storage, or {{site.data.keyword.cos_full}} are integrated as Kubernetes flex drivers and can be set up by using [Helm charts](/docs/openshift?topic=openshift-helm). The Helm chart automatically sets up Kubernetes storage classes, the storage provider, and the storage driver in your cluster. You can use the storage classes to provision persistent storage by using persistent volume claims (PVCs). For more information, see [Planning highly available persistent storage](/docs/openshift?topic=openshift-storage_planning).

To secure your cluster network or connect to an on-prem data center, you can configure one of the following options:
- [strongSwan IPSec VPN Service](/docs/openshift?topic=openshift-vpn#vpn-setup)
- [{{site.data.keyword.BluDirectLink}}](/docs/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link)
- [Virtual Router Appliance (VRA)](/docs/openshift?topic=openshift-vpn#vyatta)
- [Fortigate Security Appliance (FSA)](/docs/vmwaresolutions/services?topic=vmware-solutions-fsa_considerations)



## Kubernetes community and open source integrations
{: #kube-community-tools}

Because you own the standard clusters that you create in Red Hat OpenShift on IBM Cloud, you can choose to install third-party solutions to add extra capabilities to your cluster.
{: shortdesc}

Some open source technologies, such as LogDNA, Sysdig, or Portworx are tested by IBM and provided as managed add-ons, Helm charts, or {{site.data.keyword.cloud_notm}} services that are operated by the service provider in partnership with IBM. These open source tools are fully integrated into the {{site.data.keyword.cloud_notm}} billing and support system.

You can install other open source tools in your cluster, but these tools might not be managed, supported, or verified to work in Red Hat OpenShift on IBM Cloud.

Supported integrations depend on the container platform, the infrastructure provider, and the cluster type that you choose. For more information, see [Supported {{site.data.keyword.cloud_notm}} and third-party integrations](/docs/openshift?topic=openshift-supported_integrations).
{: note}

### Integrations operated in partnership
{: #open-source-partners}

For more information about Red Hat OpenShift on IBM Cloud partners and the benefit of each solution that they provide, see [Red Hat OpenShift on IBM Cloud partners](/docs/openshift?topic=openshift-service-partners).

### Managed add-ons
{: #cluster-add-ons}
Red Hat OpenShift on IBM Cloud integrates popular open source integrations by using [managed add-ons](/docs/containers?topic=containers-managed-addons). Managed add-ons are an easy way to install an open source tool in your cluster that is tested by IBM and approved to be used in Red Hat OpenShift on IBM Cloud.

Managed add-ons are fully integrated into the {{site.data.keyword.cloud_notm}} support organization. If you have a question or an issue with using the managed add-ons, you can use one of the Red Hat OpenShift on IBM Cloud support channels. For more information, see [Getting help and support](/docs/openshift?topic=openshift-cs_troubleshoot#getting_help).

If the tool that you add to your cluster incurs costs, these costs are automatically integrated and listed as part of your monthly {{site.data.keyword.cloud_notm}} billing. The billing cycle is determined by {{site.data.keyword.cloud_notm}} depending on when you enabled the add-on in your cluster.

### Other third-party integrations
{: #kube-community-helm}

You can install any third-party open source tool that integrates with Kubernetes. For example, the Kubernetes community designates certain Helm charts `stable` or `incubator`. Note that these charts or tools are not verified to work in Red Hat OpenShift on IBM Cloud. If the tool requires a license, you must purchase a license before you use the tool. For an overview of available Helm charts from the Kubernetes community, see the `kubernetes` and `kubernetes-incubator` repositories in the [Helm charts ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/helm) catalog.
{: shortdesc}

Any costs that incur by using a third-party open source integration are not included in your monthly {{site.data.keyword.cloud_notm}} bill.

Installing third-party open source integrations or Helm charts from the Kubernetes community might change the default cluster configuration and can bring your cluster into an unsupported state. If you run into an issue with using any of these tools, consult the Kubernetes community or the service provider directly.
{: important}

### Extending OpenShift API and software with CRDs and Operators
{: #kube-crd-operators}

You might use custom resource definitions (CRDs) to extend the OpenShift API to create and orchestrate custom objects in your cluster. Operators combine custom resources and controllers to automate the lifecycle of app, such as installing and rolling out updates to a customized app from a catalog in your cluster. 

For more information, see [Operators](/docs/openshift?topic=openshift-operators).



