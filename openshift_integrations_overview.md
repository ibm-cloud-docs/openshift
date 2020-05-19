---

copyright:
  years: 2014, 2020
lastupdated: "2020-05-19"

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


# Supported IBM Cloud and third-party integrations
{: #supported_integrations}





Learn more about the following {{site.data.keyword.IBM}}, {{site.data.keyword.cloud}}, and third-party integrations for Red Hat OpenShift on IBM Cloud clusters.
{: shortdesc}

|Service|Description|
|----|----|
| {{site.data.keyword.cloud_notm}} platform services | {{site.data.keyword.cloud_notm}} platform services that support service keys can be integrated by using [service binding](/docs/openshift?topic=openshift-service-binding). |
| {{site.data.keyword.cloud_notm}} classic infrastructure services | Your OpenShift cluster is based on fully-integrated {{site.data.keyword.cloud_notm}} classic infrastructure services such as Virtual Servers, Bare Metal Servers, or VLANs. You create and work with these services instances by using the {{site.data.keyword.containerlong_notm}} API, CLI, or console.<br><br>To secure your cluster network or connect to an on-prem data center, you can configure one of the following options:<ul><li>[strongSwan IPSec VPN Service](/docs/openshift?topic=openshift-vpn#vpn-setup)</li><li>[{{site.data.keyword.BluDirectLink}}](/docs/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link)</li><li>[Virtual Router Appliance (VRA)](/docs/openshift?topic=openshift-vpn#vyatta)</li><li>[Fortigate Security Appliance (FSA)](/docs/vmwaresolutions/services?topic=vmwaresolutions-fsa_considerations)</li></ul> |
| {{site.data.keyword.cloud_notm}} storage | Supported persistent storage solutions, such as {{site.data.keyword.cloud_notm}} File Storage, {{site.data.keyword.cloud_notm}} Block Storage, or {{site.data.keyword.cos_full_notm}} are integrated as Kubernetes flex drivers and can be set up by using Helm charts. The storage documentation for each solution includes instructions to install and manage storage. For more information about choosing a persistent storage solution, see [Planning highly available persistent storage](/docs/openshift?topic=openshift-storage_planning). |
| Cluster autoscaler | With the `ibm-iks-cluster-autoscaler` plug-in, you can scale the worker pools in your cluster automatically to increase or decrease the number of worker nodes in the worker pool based on the sizing requests of your scheduled workloads. For more information, see [Scaling clusters](/docs/openshift?topic=openshift-ca). |
| Diagnostics and debug tool | While you troubleshoot, you can use the [{{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool add-on](/docs/openshift?topic=openshift-cs_troubleshoot#debug_utility) to run tests and gather pertinent information from your cluster. |
| Istio for service mesh | Unlike for community Kubernetes clusters, the Istio managed add-on is not supported. Instead, use the [Red Hat service mesh operator](https://docs.openshift.com/container-platform/4.3/service_mesh/servicemesh-release-notes.html){: external}. **Note**: The default {{site.data.keyword.cloud_notm}} configuration of the routers enables host networking, which is not compatible with the service mesh network policy. For the service mesh ingress to work, [apply a network policy](https://gist.githubusercontent.com/kitch/39c504a2ed9e381c2aadea436d5b52e4/raw/d8efa69f41d41425b16bb363a881a98d40d3708c/mesh-policy.yaml){: external}. |
| Knative for serverless apps | Unlike for community Kubernetes clusters, the Knative managed add-on is not supported. Instead, try out the tech preview for the [OpenShift Serverless operator](https://docs.openshift.com/container-platform/4.3/serverless/serverless-getting-started.html){: external}. |
| Kubernetes Terminal | Use the [Kubernetes Terminal add-on](/docs/openshift?topic=openshift-openshift-cli#cloud-shell) to use the {{site.data.keyword.cloud_notm}} CLI to manage your cluster directly from your web browser. |
| {{site.data.keyword.la_full_notm}} | Add log management capabilities to your cluster by deploying LogDNA as a third-party service to your worker nodes to manage logs from your pod containers. For more information, see the following docs.<ul><li>[About the LogDNA partnership](/docs/openshift?topic=openshift-service-partners#logdna-partner).</li><li>[Setting up LogDNA in an OpenShift cluster](/docs/openshift?topic=openshift-health#openshift_logdna).</li><li>[Tutorial: Managing Kubernetes cluster logs with {{site.data.keyword.la_full_notm}}](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-kube#kube).</li></ul> |
| Portworx | [Portworx](https://portworx.com/products/portworx-enterprise//){: external} is a highly available software-defined storage solution that you can use to manage persistent storage for your containerized databases and other stateful apps, or to share data between pods across multiple zones. You can [install Portworx with a Helm chart](/docs/openshift?topic=openshift-portworx#portworx) and provision storage for your apps by using Kubernetes persistent volumes. However, the default configuration requires that you modify the security context constraints, similar to [LogDNA](/docs/openshift?topic=openshift-health#openshift_logdna). |
| Razee | [Razee](https://razee.io/){: external} is an open-source project that automates and manages the deployment of Kubernetes resources across clusters, environments, and cloud providers, and helps you to visualize deployment information for your resources so that you can monitor the rollout process and find deployment issues more quickly. For more information about Razee and how to set up Razee in your cluster to automate your deployment process, see the [Razee documentation](https://github.com/razee-io/Razee){: external}. |
| {{site.data.keyword.mon_full_notm}} | Gain operational visibility into the performance and health of your apps by deploying Sysdig as a third-party service to your worker nodes to forward metrics to {{site.data.keyword.mon_full}}. For more information, see the following docs.<ul><li>[About the Sysdig partnership](/docs/openshift?topic=openshift-service-partners#sydig-partner).</li><li>[Setting up Sysdig in an OpenShift cluster](/docs/openshift?topic=openshift-health#openshift_sysdig).</li><li>[Tutorial: Analyzing metrics for an app that is deployed in a Kubernetes cluster](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-kubernetes_cluster#kubernetes_cluster).</li></ul> |
| Other third-party integrations | You can install many other integrations into your OpenShift cluster, such as through the OpenShift catalog, Operators, Helm charts, or do-it-yourself open source software installations. Make sure that these apps are compatible with your OpenShift cluster and Kubernetes version. For example, you might need to [update the app](/docs/openshift?topic=openshift-openshift_apps) for the installation to succeed. |
{: summary="The rows are read from left to right. The first column is the service that you might integrate with your cluster. The second column is the description of the service."}
{: caption="{{site.data.keyword.cloud_notm}} and third-party integrations for {{site.data.keyword.openshiftlong}} clusters"}
{: summary=""}




