---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-25"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:download: .download}
{:preview: .preview}

# Enhancing cluster capabilities with integrations
{: #openshift_integrations}

With {{site.data.keyword.openshiftlong}}, you have many ways to enhance your cluster and app's capabilities with IBM and third-party content such as AI, security, databases, logging, monitoring, and more. Learn about what integrations are available and how to integrate these services with your cluster.
{: shortdesc}

## Available integrations
{: #openshift_available_integrations}

Learn more about the following {{site.data.keyword.cloud_notm}} and third-party integrations for OpenShift clusters.
{: shortdesc}

<dl>
  <dt>{{site.data.keyword.cloud_notm}} platform services</dt>
  <dd>{{site.data.keyword.cloud_notm}} platform services that support service keys can be integrated by using [service binding](#oc_service_binding). To find an overview of popular {{site.data.keyword.cloud_notm}} services, see [Popular integrations](/docs/containers?topic=containers-supported_integrations#popular_services).</dd>

  <dt>{{site.data.keyword.cloud_notm}} classic infrastructure services</dt>
  <dd>Your OpenShift cluster is based on fully-integrated {{site.data.keyword.cloud_notm}} classic infrastructure services such as Virtual Servers, Bare Metal Servers, or VLANs. You create and work with these services instances by using the {{site.data.keyword.containerlong_notm}} API, CLI, or console.<br><br>
  To secure your cluster network or connect to an on-prem data center, you can configure one of the following options:
    <ul><li>[strongSwan IPSec VPN Service](/docs/containers?topic=containers-vpn#vpn-setup)</li>
    <li>[{{site.data.keyword.BluDirectLink}}](/docs/infrastructure/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link)</li>
    <li>[Virtual Router Appliance (VRA)](/docs/containers?topic=containers-vpn#vyatta)</li>
    <li>[Fortigate Security Appliance (FSA)](/docs/services/vmwaresolutions/services?topic=vmware-solutions-fsa_considerations)</li></ul></dd>

  <dt>{{site.data.keyword.cloud_notm}} storage</dt>
  <dd>Supported persistent storage solutions, such as {{site.data.keyword.cloud_notm}} File Storage, {{site.data.keyword.cloud_notm}} Block Storage, or {{site.data.keyword.cos_full_notm}} are integrated as Kubernetes flex drivers and can be set up by using [Helm charts](#oc_helm). The storage documentation for each solution includes instructions to install and manage storage. For more information about choosing a persistent storage solution, see [Planning highly available persistent storage](/docs/openshift?topic=containers-storage_planning).</dd>

  <dt>Cluster autoscaler</dt>
  <dd>The cluster autoscaler is not supported because it requires Kubernetes version 1.12 or later. OpenShift 3.11 includes only Kubernetes version 1.11.</dd>

  <dt>Istio for service mesh</dt>
  <dd>Unlike for community Kubernetes clusters, <a href="https://www.ibm.com/cloud/info/istio" target="_blank">Istio <img src="../icons/launch-glyph.svg" alt="External link icon"></a> is not available as a managed add-on for OpenShift clusters. Instead, use the Red Hat OpenShift Servish Mesh project. For more information, see [the OpenShift installation docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/servicemesh-install/servicemesh-install.html).</dd>

  <dt>Knative for serverless apps</dt>
  <dd>Unlike for community Kubernetes clusters, <a href="https://github.com/knative/docs" target="_blank">Knative <img src="../icons/launch-glyph.svg" alt="External link icon"></a> is not available as a managed add-on for OpenShift clusters. Instead, try out the Knative on OpenShift developer preview. For more information, see [the OpenShift installation docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/openshift-knative/docs).</dd>

  <dt>Kubernetes Terminal</dt>
  <dd>The [Kubernetes Terminal add-on](/docs/containers?topic=containers-cs_cli_install#cli_web) is available for only community Kubernetes cluster, not OpenShift clusters.</dd>

  <dt>{{site.data.keyword.la_full_notm}}</dt>
  <dd>Add log management capabilities to your cluster by deploying LogDNA as a third-party service to your worker nodes to manage logs from your pod containers. For more information, see the following docs.<ul>
    <li>[About the LogDNA partnership](/docs/containers?topic=containers-service-partners#logdna-partner).</li>
    <li>[Setting up LogDNA in an OpenShift cluster](/docs/openshift?topic=openshift-openshift_health#openshift_logdna).</li>
    <li>[Tutorial: Managing Kubernetes cluster logs with {{site.data.keyword.loganalysisfull_notm}} with LogDNA](/docs/services/Log-Analysis-with-LogDNA/tutorials?topic=LogDNA-kube#kube).</li></ul></dd>

  <dt>Razee</dt>
  <dd>[Razee ![External link icon](../icons/launch-glyph.svg "External link icon")](https://razee.io/) is an open-source project that automates and manages the deployment of Kubernetes resources across clusters, environments, and cloud providers, and helps you to visualize deployment information for your resources so that you can monitor the rollout process and find deployment issues more quickly. For more information about Razee and how to set up Razee in your cluster to automate your deployment process, see the [Razee documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/razee-io/Razee).</dd>

  <dt>{{site.data.keyword.mon_full_notm}}</dt>
  <dd>Gain operational visibility into the performance and health of your apps by deploying Sysdig as a third-party service to your worker nodes to forward metrics to {{site.data.keyword.monitoringlong}}. For more information, see the following docs.<ul>
    <li>[About the Sysdig partnership](/docs/containers?topic=containers-service-partners#sydig-partner).</li>
    <li>[Setting up Sysdig in an OpenShift cluster](/docs/openshift?topic=openshift-openshift_health#openshift_sysdig).</li>
    <li>[Tutorial: Analyzing metrics for an app that is deployed in a Kubernetes cluster](/docs/services/Monitoring-with-Sysdig/tutorials?topic=Sysdig-kubernetes_cluster#kubernetes_cluster).</li></ul></dd>

  <dt>Other third-party integrations</dt>
  <dd>You can install many other integrations into your OpenShift cluster, such as through the OpenShift catalog, Operators, Helm charts, or do-it-yourself open source software installations. Make sure that these apps are compatible with your OpenShift cluster and Kubernetes version. For example, you might need to [update the app](/docs/openshift?topic=openshift-openshift_apps) for the installation to succeed.</dd>

</dl>

<br />


## Adding integrations to your OpenShift cluster
{: #openshift_adding_services}

You can add services to your Red Hat OpenShift on IBM Cloud cluster in various ways, including service binding, Helm charts, and operators. If you want to install open source software apps, make sure that these apps are compatible with your OpenShift cluster and Kubernetes version. For example, you might need to [update the app](/docs/openshift?topic=openshift-openshift_apps) for the installation to succeed.
{: shortdesc}

### IBM Cloud Paks
{: #oc_cloud_paks}

[IBM Cloud Paks&trade; ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/paks/) are containerized IBM middleware and open source software components that you are licensed to use in [IBM Passport Advantage]() as part of your hybrid cloud solution. IBM Cloud Paks run exclusively on OpenShift clusters, not community Kubernetes clusters. To use IBM Cloud Paks, you must set up your cluster environment as follows.
{: shortdesc}

1. In the project that you want to deploy the Cloud Pak to, make sure that you [set up the image pull secret to access images that are stored in {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-openshift-images#openshift_iccr).
2. Import the Cloud Pak from Passport Advantage to your registry. Methods vary depending on the Cloud Pak.
   * For public cloud environments, you can use the [`ibmcloud cr ppa-archive-load` CLI tool](/docs/services/Registry topic=registry-ts_index#ts_ppa_import).
   * If you have ICP Common Services installed in your cluster, then you can use the [`cloudctl catalog load-archive` CLI tool](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.2/app_center/add_package_offline.html).
   * Some Cloud Paks, such as {{site.data.keyword.icp4dfull_notm}}, push the image to the registry for you as part of their installation process.
3. Follow the instructions that are particular to each Cloud Pak installation, such as configuring the Helm chart values to work within OpenShift security context constraints.

### {{site.data.keyword.cloud_notm}} service binding
{: #oc_service_binding}

To access {{site.data.keyword.cloud_notm}} services in your account, you can create service credentials and store these credentials in a Kubernetes secret in your cluster. For more information, see [Adding services by using {{site.data.keyword.cloud_notm}} service binding](/docs/containers?topic=containers-service-binding).

### Helm charts
{: #oc_helm}

[Helm ![External link icon](../icons/launch-glyph.svg "External link icon")](https://helm.sh) is a Kubernetes package manager that uses Helm charts to define, install, and upgrade complex Kubernetes apps in your cluster. Helm charts package the specifications to generate YAML files for Kubernetes resources that build your app. Because OpenShift sets stricter security context constraints the community Kubernetes, you might need to modify your Helm deployment before you install the chart. To install Helm, see the [{{site.data.keyword.containershort_notm}} docs](/docs/containers?topic=containers-helm).
{: shortdesc}

### Operators
{: #oc_operators}

Instead of Helm, you might use [Operators ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/4.1/applications/operators/olm-what-operators-are.html) to package, deploy, and update your apps. Operators are available for only OpenShift 4.1 versions. In the meantime, you can try out the [experimental {{site.data.keyword.cloud_notm}} Operator ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.ibm.com/seed/olm/blob/master/pocs/openshift-ibmcloud/README.md).
{: shortdesc}
