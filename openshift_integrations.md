---

copyright:
  years: 2014, 2019
lastupdated: "2019-10-01"

keywords: openshift, roks, rhoks, rhos, cloud pak, cloud pack, cloudpak, cloudpack, icp, cloud paks, cloudpaks, cloud packs, cloudpacks, icd, icp4d

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
{:important: .important}
{:download: .download}
{:preview: .preview}

<style>
<!--
    #tutorials { /* hide the page header */
        display: none !important
    }
    .allCategories {
        display: flex !important;
        flex-direction: row !important;
        flex-wrap: wrap !important;
    }
    .solutionBoxContainer {}
    .solutionBoxContainer a {
        text-decoration: none !important;
        border: none !important;
    }
    .solutionBox {
        display: inline-block !important;
        width: 600px !important;
        margin: 0 10px 20px 0 !important;
        padding: 10px !important;
        border: 1px #dfe6eb solid !important;
        box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.2) !important;
    }
    @media screen and (min-width: 960px) {
        .solutionBox {
        width: 27% !important;
        }
        .solutionBoxContent {
        height: 320px !important;
        }
    }
    @media screen and (min-width: 1298px) {
        .solutionBox {
        width: calc(33% - 2%) !important;
        }
        .solutionBoxContent {
        min-height: 320px !important;
        }
    }
    .solutionBox:hover {
        border-color: rgb(136, 151, 162) !important;
    }
    .solutionBoxContent {
        display: flex !important;
        flex-direction: column !important;
    }
    .solutionBoxDescription {
        flex-grow: 1 !important;
        display: flex !important;
        flex-direction: column !important;
    }
    .descriptionContainer {
    }
    .descriptionContainer p {
        margin: 2px !important;
        overflow: hidden !important;
        display: -webkit-box !important;
        -webkit-line-clamp: 4 !important;
        -webkit-box-orient: vertical !important;
        font-size: 12px !important;
        font-weight: 400 !important;
        line-height: 1.5 !important;
        letter-spacing: 0 !important;
        max-height: 70px !important;
    }
    .architectureDiagramContainer {
        flex-grow: 1 !important;
        min-width: 200px !important;
        padding: 0 10px !important;
        text-align: center !important;
        display: flex !important;
        flex-direction: column !important;
        justify-content: center !important;
    }
    .architectureDiagram {
        max-height: 170px !important;
        padding: 5px !important;
        margin: 0 auto !important;
    }
-->
</style>

# Enhancing cluster capabilities with integrations
{: #openshift_integrations}

With {{site.data.keyword.openshiftlong}}, you have many ways to enhance your cluster and app's capabilities with IBM and third-party content such as IBM Cloud Paks&trade;, AI, security, databases, logging, monitoring, and more. Learn about what integrations are available and how to integrate these services with your cluster.
{: shortdesc}

You can add services to your Red Hat OpenShift on IBM Cloud cluster in various ways, including service binding, Helm charts, and operators. If you want to install open source software apps, make sure that these apps are compatible with your OpenShift cluster and Kubernetes version. For example, you might need to [update the app](/docs/openshift?topic=openshift-openshift_apps) for the installation to succeed.
{: shortdesc}

## Adding IBM Cloud Paks
{: #oc_cloud_paks}

[IBM Cloud Paks ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/paks/) are containerized IBM middleware and open source software components that you are licensed to use in [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/) as part of your hybrid cloud solution. IBM Cloud Paks run exclusively on OpenShift clusters, not community Kubernetes clusters. To use IBM Cloud Paks, you must set up your cluster environment as follows.
{: shortdesc}

1. In the project that you want to deploy the Cloud Pak to, make sure that you [set up the image pull secret to access images that are stored in {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-openshift-images#openshift_iccr).
2. Import the Cloud Pak from Passport Advantage to your registry. Methods vary depending on the Cloud Pak.
   * For public cloud, you can use the [`ibmcloud cr ppa-archive-load` CLI tool](/docs/services/Registry?topic=registry-ts_index#ts_ppa_import).
   * If you have ICP Common Services installed in your cluster, then you can use the [`cloudctl catalog load-archive` CLI tool](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.2/app_center/add_package_offline.html). To push and pull these licensed images from ICP Common Services `load-archive` tool to your cluster's internal registry, you can [set up a secure external route for the internal registry](/docs/openshift?topic=openshift-openshift-images#route_internal_registry).
   * Some Cloud Paks, such as {{site.data.keyword.icp4dfull_notm}}, push the image to the registry for you as part of their installation process. To see if the image is pushed during installation, review the Cloud Pak installation information.
3. Follow the instructions that are particular to each Cloud Pak installation, such as configuring the Helm chart values to work within OpenShift security context constraints.

Now you can run your Cloud Pak on your OpenShift cluster!

When you set up your Cloud Pak, you might need to work with OpenShift-specific resources, such as security context constraints. Make sure that you use the [`oc` CLI or `kubectl` version 1.12 CLI](/docs/openshift?topic=openshift-openshift-cli#cli_oc) to interact with these resources, such as `oc get scc`. The `kubectl` CLI version 1.11 has a bug that yields an error when you run commands against OpenShift-specific resources, such as `kubectl get scc`.
{: important}

<br />


## Binding {{site.data.keyword.cloud_notm}} services to your cluster
{: #oc_service_binding}

To access {{site.data.keyword.cloud_notm}} services in your account, you can create service credentials and store these credentials in a Kubernetes secret in your cluster. For more information, see [Adding services by using {{site.data.keyword.cloud_notm}} service binding](/docs/containers?topic=containers-service-binding).

<br />


## Deploying apps with Helm charts
{: #oc_helm}

[Helm ![External link icon](../icons/launch-glyph.svg "External link icon")](https://helm.sh) is a Kubernetes package manager that uses Helm charts to define, install, and upgrade complex Kubernetes apps in your cluster. Helm charts package the specifications to generate YAML files for Kubernetes resources that build your app. Because OpenShift sets stricter security context constraints the community Kubernetes, you might need to modify your Helm deployment before you install the chart. To install Helm, see the [{{site.data.keyword.containershort_notm}} docs](/docs/containers?topic=containers-helm).
{: shortdesc}

<br />


## Using Operators
{: #oc_operators}

Instead of Helm, you might use [Operators ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/4.1/applications/operators/olm-what-operators-are.html) to package, deploy, and update your apps. Operators are available for only OpenShift 4.x versions. In the meantime, you can try out the [experimental {{site.data.keyword.cloud_notm}} Operator ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.ibm.com/seed/olm/blob/master/pocs/openshift-ibmcloud/README.md) and the following tutorial.
{: shortdesc}

<div class = "solutionBoxContainer">
    <a href = "https://developer.ibm.com/tutorials/simplify-lifecycle-management-kubernetes-OpenShift-ibm-cloud-operator/">
    <div class = "solutionBox">
        <div class = "solutionBoxContent">
                App lifecycle management with {{site.data.keyword.cloud_notm}} Operator
          <div class="solutionBoxDescription">
                <div class="descriptionContainer">
                  </br> <p>Use the Operator Lifecycle Manager (OLM) and the {{site.data.keyword.cloud_notm}} Operator to simplify your app lifecycle management approach for {{site.data.keyword.cloud_notm}} services, third-party apps, and your own custom-built, cloud-native apps in your {{site.data.keyword.openshifshort}} cluster.</p></br>
                </div>
                <div class="architectureDiagramContainer">
                    <img class="architectureDiagram" src="images/dev_guides_operators.png" alt="IBM Cloud operator flowchart" />
                </div>
            </div>
        </div>
    </div>
    </a>
</div>

<br />


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
  <dd>With the `ibm-iks-cluster-autoscaler` plug-in, you can scale the worker pools in your cluster automatically to increase or decrease the number of worker nodes in the worker pool based on the sizing requests of your scheduled workloads. For more information, see [Scaling clusters](/docs/containers?topic=containers-ca) in the {{site.data.keyword.containerlong_notm}} docs.</dd>

  <dt>Istio for service mesh</dt>
  <dd>Unlike for community Kubernetes clusters, <a href="https://www.ibm.com/cloud/istio" target="_blank">Istio <img src="../icons/launch-glyph.svg" alt="External link icon"></a> is not available as a managed add-on for OpenShift clusters. Instead, use the Red Hat OpenShift Service Mesh project. For more information, see [the OpenShift installation docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/servicemesh-install/servicemesh-install.html).</dd>

  <dt>Knative for serverless apps</dt>
  <dd>Unlike for community Kubernetes clusters, <a href="https://github.com/knative/docs" target="_blank">Knative <img src="../icons/launch-glyph.svg" alt="External link icon"></a> is not available as a managed add-on for OpenShift clusters. Instead, try out the Knative on OpenShift developer preview. For more information, see [the OpenShift installation docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/openshift-knative/docs).</dd>

  <dt>Kubernetes Terminal</dt>
  <dd>The [Kubernetes Terminal add-on](/docs/containers?topic=containers-cs_cli_install#cli_web) is available for only community Kubernetes cluster, not OpenShift clusters.</dd>

  <dt>{{site.data.keyword.la_full_notm}}</dt>
  <dd>Add log management capabilities to your cluster by deploying LogDNA as a third-party service to your worker nodes to manage logs from your pod containers. For more information, see the following docs.<ul>
    <li>[About the LogDNA partnership](/docs/containers?topic=containers-service-partners#logdna-partner).</li>
    <li>[Setting up LogDNA in an OpenShift cluster](/docs/openshift?topic=openshift-openshift_health#openshift_logdna).</li>
    <li>[Tutorial: Managing Kubernetes cluster logs with {{site.data.keyword.la_full_notm}}](/docs/services/Log-Analysis-with-LogDNA/tutorials?topic=LogDNA-kube#kube).</li></ul></dd>

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
