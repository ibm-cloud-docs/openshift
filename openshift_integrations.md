---

copyright:
  years: 2014, 2020
lastupdated: "2020-01-08"

keywords: openshift, roks, rhoks, rhos, cloud pak, cloud pack, cloudpak, cloudpack, icp, cloud paks, cloudpaks, cloud packs, cloudpacks, icd, icp4d

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

You can add services to your {{site.data.keyword.openshiftlong_notm}} cluster in various ways, including service binding, Helm charts, and operators. If you want to install open source software apps, make sure that these apps are compatible with your {{site.data.keyword.openshiftshort}} cluster and Kubernetes version. For example, you might need to [update the app](/docs/openshift?topic=openshift-openshift_apps) for the installation to succeed.
{: shortdesc}


## Adding IBM Cloud Paks
{: #oc_cloud_paks}

You can add [IBM Cloud Paks ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/paks/) to your {{site.data.keyword.openshiftshort}} clusters.
{: shortdesc}

<div class = "solutionBoxContainer">
    <a href = "/docs/openshift?topic=openshift-openshift_cloud_paks">
    <div class = "solutionBox">
        <div class = "solutionBoxContent">
                Adding Cloud Paks
          <div class="solutionBoxDescription">
                <div class="descriptionContainer">
                  </br> <p>Learn more about the different IBM Cloud Paks and how to install them in your to {{site.data.keyword.openshiftshort}} clusters.</p></br>
                </div>
                <div class="architectureDiagramContainer">
                    <img class="architectureDiagram" src="/images/oc-cloud-paks.png" alt="IBM Cloud Paks icons" />
                </div>
            </div>
        </div>
    </div>
    </a>
</div>

## Binding {{site.data.keyword.cloud_notm}} services to your cluster
{: #oc_service_binding}

To access {{site.data.keyword.cloud_notm}} services in your account, you can create service credentials and store these credentials in a Kubernetes secret in your cluster. For more information, see [Adding services by using {{site.data.keyword.cloud_notm}} service binding](/docs/containers?topic=containers-service-binding).

<br />


## Deploying apps with Helm charts
{: #oc_helm}

[Helm ![External link icon](../icons/launch-glyph.svg "External link icon")](https://helm.sh) is a Kubernetes package manager that uses Helm charts to define, install, and upgrade complex Kubernetes apps in your cluster. Helm charts package the specifications to generate YAML files for Kubernetes resources that build your app. Because {{site.data.keyword.openshiftshort}} sets stricter security context constraints the community Kubernetes, you might need to modify your Helm deployment before you install the chart. To install Helm, see the [{{site.data.keyword.containershort_notm}} docs](/docs/containers?topic=containers-helm).
{: shortdesc}

<br />


## Using Operators
{: #oc_operators}

Instead of Helm, you might use [Operators ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/4.1/applications/operators/olm-what-operators-are.html) to package, deploy, and update your apps. Operators are available for only {{site.data.keyword.openshiftshort}} 4.x versions. In the meantime, you can try out the [experimental {{site.data.keyword.cloud_notm}} Operator ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.ibm.com/seed/olm/blob/master/pocs/openshift-ibmcloud/README.md) and the following tutorial.
{: shortdesc}

<div class = "solutionBoxContainer">
    <a href = "https://developer.ibm.com/tutorials/simplify-lifecycle-management-kubernetes-OpenShift-ibm-cloud-operator/">
    <div class = "solutionBox">
        <div class = "solutionBoxContent">
                App lifecycle management with {{site.data.keyword.cloud_notm}} Operator
          <div class="solutionBoxDescription">
                <div class="descriptionContainer">
                  </br> <p>Use the Operator Lifecycle Manager (OLM) and the {{site.data.keyword.cloud_notm}} Operator to simplify your app lifecycle management approach for {{site.data.keyword.cloud_notm}} services, third-party apps, and your own custom-built, cloud-native apps in your {{site.data.keyword.openshiftshort}} cluster.</p></br>
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


<!--specific to ROKS 3.11-->
## Using the service catalog
{: #service_catalog}

You can extend your app's capabilities by binding a service from the [{{site.data.keyword.openshiftshort}} service catalog](https://docs.openshift.com/container-platform/3.11/architecture/service_catalog/index.html){: external}. The service catalog is enabled in your cluster by default. For an example of how to use the service catalog, see [Deploying an app with the {{site.data.keyword.openshiftshort}} service catalog](/docs/openshift?topic=openshift-getting-started#deploy-app).
{: shortdesc}

The catalog services and related [templates](https://docs.openshift.com/container-platform/3.11/dev_guide/templates.html#dev-guide-templates){: external} are extensions that you choose to add to your cluster and are not maintained, updated, or supported by IBM. To review the images or maintenance guidelines, follow the `readme` files or other documentation of each service.
{: note}

<br />


## Available integrations
{: #openshift_available_integrations}

Learn more about the following {{site.data.keyword.cloud_notm}} and third-party integrations for {{site.data.keyword.openshiftshort}} clusters.
{: shortdesc}

<dl>
  <dt>{{site.data.keyword.cloud_notm}} platform services</dt>
  <dd>{{site.data.keyword.cloud_notm}} platform services that support service keys can be integrated by using [service binding](#oc_service_binding).</dd>

  <dt>{{site.data.keyword.cloud_notm}} classic infrastructure services</dt>
  <dd>Your {{site.data.keyword.openshiftshort}} cluster is based on fully-integrated {{site.data.keyword.cloud_notm}} classic infrastructure services such as Virtual Servers, Bare Metal Servers, or VLANs. You create and work with these services instances by using the {{site.data.keyword.containerlong_notm}} API, CLI, or console.<br><br>
  To secure your cluster network or connect to an on-prem data center, you can configure one of the following options:
    <ul><li>[strongSwan IPSec VPN Service](/docs/openshift?topic=openshift-vpn#vpn-setup)</li>
    <li>[{{site.data.keyword.BluDirectLink}}](/docs/infrastructure/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link)</li>
    <li>[Virtual Router Appliance (VRA)](/docs/openshift?topic=openshift-vpn#vyatta)</li>
    <li>[Fortigate Security Appliance (FSA)](/docs/services/vmwaresolutions/services?topic=vmware-solutions-fsa_considerations)</li></ul></dd>

  <dt>{{site.data.keyword.cloud_notm}} storage</dt>
  <dd>Supported persistent storage solutions, such as {{site.data.keyword.cloud_notm}} File Storage, {{site.data.keyword.cloud_notm}} Block Storage, or {{site.data.keyword.cos_full_notm}} are integrated as Kubernetes flex drivers and can be set up by using [Helm charts](#oc_helm). The storage documentation for each solution includes instructions to install and manage storage. For more information about choosing a persistent storage solution, see [Planning highly available persistent storage](/docs/openshift?topic=openshift-storage_planning).</dd>

  <dt>Cluster autoscaler</dt>
  <dd>With the `ibm-iks-cluster-autoscaler` plug-in, you can scale the worker pools in your cluster automatically to increase or decrease the number of worker nodes in the worker pool based on the sizing requests of your scheduled workloads. For more information, see [Scaling clusters](/docs/openshift?topic=openshift-ca).</dd>

  <dt>Diagnostics and debug tool</dt>
  <dd>While you troubleshoot, you can use the [{{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool add-on](/docs/containers?topic=containers-cs_troubleshoot#debug_utility) to run tests and gather pertinent information from your cluster.</dd>

  <dt>Istio for service mesh</dt>
  <dd>Unlike for community Kubernetes clusters, <a href="https://www.ibm.com/cloud/istio" target="_blank">Istio <img src="../icons/launch-glyph.svg" alt="External link icon"></a> is not available as a managed add-on for {{site.data.keyword.openshiftshort}} clusters. Instead, use the Red Hat {{site.data.keyword.openshiftshort}} Service Mesh project. For more information, see [the {{site.data.keyword.openshiftshort}} installation docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/servicemesh-install/servicemesh-install.html).</dd>

  <dt>Knative for serverless apps</dt>
  <dd>Unlike for community Kubernetes clusters, <a href="https://github.com/knative/docs" target="_blank">Knative <img src="../icons/launch-glyph.svg" alt="External link icon"></a> is not available as a managed add-on for {{site.data.keyword.openshiftshort}} clusters. Instead, try out the Knative on {{site.data.keyword.openshiftshort}} developer preview. For more information, see [the {{site.data.keyword.openshiftshort}} installation docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/openshift-knative/docs).</dd>

  <dt>Kubernetes Terminal</dt>
  <dd>Use the [Kubernetes Terminal add-on](/docs/openshift?topic=openshift-openshift-cli#cli_web) to use the {{site.data.keyword.cloud_notm}} CLI to manage your cluster directly from your web browser.</dd>

  <dt>{{site.data.keyword.la_full_notm}}</dt>
  <dd>Add log management capabilities to your cluster by deploying LogDNA as a third-party service to your worker nodes to manage logs from your pod containers. For more information, see the following docs.<ul>
    <li>[About the LogDNA partnership](/docs/containers?topic=containers-service-partners#logdna-partner).</li>
    <li>[Setting up LogDNA in an {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-health#openshift_logdna).</li>
    <li>[Tutorial: Managing Kubernetes cluster logs with {{site.data.keyword.la_full_notm}}](/docs/services/Log-Analysis-with-LogDNA/tutorials?topic=LogDNA-kube#kube).</li></ul></dd>

  <dt>Portworx</dt>
  <dd>[Portworx ![External link icon](../icons/launch-glyph.svg "External link icon")](https://portworx.com/products/introduction/) is a highly available software-defined storage solution that you can use to manage persistent storage for your containerized databases and other stateful apps, or to share data between pods across multiple zones. You can [install Portworx with a Helm chart](/docs/containers?topic=containers-portworx#portworx) and provision storage for your apps by using Kubernetes persistent volumes. However, the default configuration requires that you modify the security context constraints, similar to [LogDNA](/docs/openshift?topic=openshift-health#openshift_logdna).</dd>

  <dt>Razee</dt>
  <dd>[Razee ![External link icon](../icons/launch-glyph.svg "External link icon")](https://razee.io/) is an open-source project that automates and manages the deployment of Kubernetes resources across clusters, environments, and cloud providers, and helps you to visualize deployment information for your resources so that you can monitor the rollout process and find deployment issues more quickly. For more information about Razee and how to set up Razee in your cluster to automate your deployment process, see the [Razee documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/razee-io/Razee).</dd>

  <dt>{{site.data.keyword.mon_full_notm}}</dt>
  <dd>Gain operational visibility into the performance and health of your apps by deploying Sysdig as a third-party service to your worker nodes to forward metrics to {{site.data.keyword.mon_full}}. For more information, see the following docs.<ul>
    <li>[About the Sysdig partnership](/docs/containers?topic=containers-service-partners#sydig-partner).</li>
    <li>[Setting up Sysdig in an {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-health#openshift_sysdig).</li>
    <li>[Tutorial: Analyzing metrics for an app that is deployed in a Kubernetes cluster](/docs/services/Monitoring-with-Sysdig/tutorials?topic=Sysdig-kubernetes_cluster#kubernetes_cluster).</li></ul></dd>

  <dt>Other third-party integrations</dt>
  <dd>You can install many other integrations into your {{site.data.keyword.openshiftshort}} cluster, such as through the {{site.data.keyword.openshiftshort}} catalog, Operators, Helm charts, or do-it-yourself open source software installations. Make sure that these apps are compatible with your {{site.data.keyword.openshiftshort}} cluster and Kubernetes version. For example, you might need to [update the app](/docs/openshift?topic=openshift-openshift_apps) for the installation to succeed.</dd>

</dl>
