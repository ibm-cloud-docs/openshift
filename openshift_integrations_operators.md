---

copyright:
  years: 2014, 2020
lastupdated: "2020-03-11"

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

# Adding services by using Operators
{: #operators}

With operators, you can manage the lifecycle of the apps in your cluster, including third-party software and services that you integrate into your cluster from the [OperatorHub](https://operatorhub.io/){: external}. You can consistently install, update, and monitor system components by using operators or by making operators available to developers that work in specific projects or across projects.
{: shortdesc}

## Using Operators in 4.3 clusters
{: #operators_4}

In OpenShift clusters that run version 4.3 or later, operators are available in your cluster by default. Use [Operators](https://docs.openshift.com/container-platform/4.1/applications/operators/olm-what-operators-are.html){: external} to package, deploy, and update the apps in your Red Hat OpenShift on IBM Cloud clusters.
{: shortdesc}

1.  To use operators, follow the OpenShift documentation.
    *   [Adding Operators to a cluster](https://docs.openshift.com/container-platform/4.1/applications/operators/olm-adding-operators-to-cluster.html){: external}
    *   [Deleting Operators from a cluster](https://docs.openshift.com/container-platform/4.1/applications/operators/olm-deleting-operators-from-cluster.html){: external}
    *   [Creating applications from installed Operators](https://docs.openshift.com/container-platform/4.1/applications/operators/olm-creating-apps-from-installed-operators.html){: external}
    *   [Making your own custom Operator](https://github.com/operator-framework/community-operators/blob/master/docs/testing-operators.md#testing-operator-deployment-on-openshift){: external}.
        *  For help creating custom Operators, see the [Operator SDK](https://docs.openshift.com/container-platform/4.2/operators/operator_sdk/osdk-getting-started.html){: external} documentation, which includes a guide to build an operator that is based on a [Helm chart](https://docs.openshift.com/container-platform/4.2/operators/operator_sdk/osdk-helm.html){: external}.
        *  To manage your custom Operator, see the [Operator Lifecycle Manager](https://docs.openshift.com/container-platform/4.2/operators/understanding-olm/olm-understanding-olm.html){: external} documentation.
2.  Review any custom steps to install an operator in your cluster.
    *   To set up an [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana (EFK) stack](https://docs.openshift.com/container-platform/4.3/logging/cluster-logging.html){: external}, see [installing the cluster logging operator](/docs/openshift?topic=openshift-health#oc_logging_operator).

## Using Operators in 3.11 clusters
{: #operators_311}

Try out the [experimental {{site.data.keyword.cloud_notm}} Operator](https://github.ibm.com/seed/olm/blob/master/pocs/openshift-ibmcloud/README.md){: external} and the following tutorial.
{: shortdesc}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> The {{site.data.keyword.cloud_notm}} Operator and other Operators are experimental for version 3.11, and you are responsible for its maintenance and support. If you have a 4.x cluster, use the built-in [Operators and OperatorHub instead](#operators_4).
{: note}

<div class = "solutionBoxContainer">
    <a href = "https://developer.ibm.com/tutorials/simplify-lifecycle-management-kubernetes-OpenShift-ibm-cloud-operator/">
    <div class = "solutionBox">
        <div class = "solutionBoxContent">
                App lifecycle management with {{site.data.keyword.cloud_notm}} Operator
          <div class="solutionBoxDescription">
                <div class="descriptionContainer">
                  </br> <p>Use the Operator Lifecycle Manager (OLM) and the {{site.data.keyword.cloud_notm}} Operator to simplify your app lifecycle management approach for {{site.data.keyword.cloud_notm}} services, third-party apps, and your own custom-built, cloud-native apps in your OpenShift cluster.</p></br>
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


## Using the service catalog in 3.11 clusters
{: #service_catalog}

<img src="images/icon-version-43.png" alt="Version 4.3 icon" width="30" style="width:30px; border-style: none"/> The service catalog is not supported in clusters that run version 4.3 and later. Use [Operators](#operators_4) instead.
{: deprecated}

You can extend your app's capabilities by binding a service from the [OpenShift service catalog](https://docs.openshift.com/container-platform/3.11/architecture/service_catalog/index.html){: external}. The service catalog is enabled in your 3.11 cluster by default. For an example of how to use the service catalog, see [Deploying an app with the OpenShift service catalog](/docs/openshift?topic=openshift-getting-started#deploy-app).
{: shortdesc}

The catalog services and related [templates](https://docs.openshift.com/container-platform/3.11/dev_guide/templates.html#dev-guide-templates){: external} are extensions that you choose to add to your cluster and are not maintained, updated, or supported by IBM. To review the images or maintenance guidelines, follow the `readme` files or other documentation of each service.
{: note}

<br />



