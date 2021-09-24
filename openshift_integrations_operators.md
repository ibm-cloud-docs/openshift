---

copyright:
  years: 2014, 2021
lastupdated: "2021-09-24"

keywords: kubernetes, openshift, roks, rhoks, rhos

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}  

<style>
    <!--
        #tutorials { /* hide the page header */
            display: none !important;
        }
        .allCategories {
            display: flex !important;
            flex-direction: row !important;
            flex-wrap: wrap !important;
        }
        .categoryBox {
            flex-grow: 1 !important;
            width: calc(33% - 20px) !important;
            text-decoration: none !important;
            margin: 0 10px 20px 0 !important;
            padding: 16px !important;
            border: 1px #dfe6eb solid !important;
            box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.2) !important;
            text-align: center !important;
            text-overflow: ellipsis !important;
            overflow: hidden !important;
        }
        .solutionBoxContainer {}
        .solutionBoxContainer a {
            text-decoration: none !important;
            border: none !important;
        }
        .solutionBox {
            display: inline-block !important;
            width: 100% !important;
            margin: 0 10px 20px 0 !important;
            padding: 16px !important;
            background-color: #f4f4f4 !important;
        }
        @media screen and (min-width: 960px) {
            .solutionBox {
            width: calc(50% - 3%) !important;
            }
            .solutionBox.solutionBoxFeatured {
            width: calc(50% - 3%) !important;
            }
            .solutionBoxContent {
            height: 350px !important;
            }
        }
        @media screen and (min-width: 1298px) {
            .solutionBox {
            width: calc(33% - 2%) !important;
            }
            .solutionBoxContent {
            min-height: 350px !important;
            }
        }
        .solutionBox:hover {
            border: 1px rgb(136, 151, 162)solid !important;
            box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.2) !important;
        }
        .solutionBoxContent {
            display: flex !important;
            flex-direction: column !important;
        }
        .solutionBoxTitle {
            margin: 0rem !important;
            margin-bottom: 5px !important;
            font-size: 14px !important;
            font-weight: 900 !important;
            line-height: 16px !important;
            height: 37px !important;
            text-overflow: ellipsis !important;
            overflow: hidden !important;
            display: -webkit-box !important;
            -webkit-line-clamp: 2 !important;
            -webkit-box-orient: vertical !important;
            -webkit-box-align: inherit !important;
        }
        .solutionBoxDescription {
            flex-grow: 1 !important;
            display: flex !important;
            flex-direction: column !important;
        }
        .descriptionContainer {
        }
        .descriptionContainer p {
            margin: 0 !important;
            overflow: hidden !important;
            display: -webkit-box !important;
            -webkit-line-clamp: 4 !important;
            -webkit-box-orient: vertical !important;
            font-size: 14px !important;
            font-weight: 400 !important;
            line-height: 1.5 !important;
            letter-spacing: 0 !important;
            max-height: 70px !important;
        }
        .architectureDiagramContainer {
            flex-grow: 1 !important;
            min-width: calc(33% - 2%) !important;
            padding: 0 16px !important;
            text-align: center !important;
            display: flex !important;
            flex-direction: column !important;
            justify-content: center !important;
            background-color: #f4f4f4;
        }
        .architectureDiagram {
            max-height: 175px !important;
            padding: 5px !important;
            margin: 0 auto !important;
        }
    -->
    </style>

# Adding services by using Operators
{: #operators}

With operators, you can manage the lifecycle of the apps in your cluster, including third-party software and services that you integrate into your cluster from the [OperatorHub](https://operatorhub.io/){: external}. You can consistently install, update, and monitor system components by using operators or by making operators available to developers that work in specific projects or across projects.
{: shortdesc}

Operators are a convenient way to add services to your cluster from community, third-party, your own, or other providers. Keep in mind that you are responsible for additional charges and how these services operate in your cluster, from deployment and maintenance to integration with your apps. If you have issues with an operator, work with the appropriate provider to troubleshoot the issue.
{: note}

## Using Operators in version 4 clusters
{: #operators_4}

In {{site.data.keyword.openshiftshort}} clusters that run version 4, operators are available in your cluster by default. Use [Operators](https://docs.openshift.com/container-platform/4.7/operators/understanding/olm-what-operators-are.html){: external} to package, deploy, and update the apps in your {{site.data.keyword.openshiftlong_notm}} clusters.
{: shortdesc}

1. To use operators, follow the {{site.data.keyword.openshiftshort}} documentation.
    *   [Adding Operators to a cluster](https://docs.openshift.com/container-platform/4.7/operators/admin/olm-adding-operators-to-cluster.html){: external}
    *   [Deleting Operators from a cluster](https://docs.openshift.com/container-platform/4.7/operators/admin/olm-deleting-operators-from-cluster.html){: external}
    *   [Creating applications from installed Operators](https://docs.openshift.com/container-platform/4.7/operators/user/olm-creating-apps-from-installed-operators.html){: external}
    *   [Making your own custom Operator](https://github.com/operator-framework/community-operators/blob/master/docs/testing-operators.md#testing-operator-deployment-on-openshift){: external}.
        *  For help creating custom Operators, see the [Operator SDK](https://docs.openshift.com/container-platform/4.7/operators/operator_sdk/osdk-getting-started.html){: external} documentation, which includes a guide to build an operator that is based on a [Helm chart](https://docs.openshift.com/container-platform/4.7/operators/operator_sdk/){: external}.
        *  To manage your custom Operator, see the [Operator Lifecycle Manager](http://docs.openshift.com/container-platform/4.7/operators/understanding/olm/olm-understanding-olm.html){: external} documentation.
2. Review any custom steps to install an operator in your cluster.
    *   To set up an [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana (EFK) stack](https://docs.openshift.com/container-platform/4.7/logging/cluster-logging.html){: external}, see [installing the cluster logging operator](/docs/openshift?topic=openshift-health#oc_logging_operator).
3. If the operator uses a template with a build component that must pull an image from a private registry, the build might fail with an authentication error. To resolve this error, see [Build error due to image pull authentication](/docs/openshift?topic=openshift-ts-app-build-img-pull).

<br />

## Disabling and mirroring OperatorHub catalog source images
{: #mirror-operatorhub}

You can disable and mirror the OperatorHub catalog source images by following the [Operator Lifecycle Manager (OLM) on restricted networks documentation from Red Hat](https://docs.openshift.com/container-platform/4.6/operators/admin/olm-restricted-networks.html){: external}. 
{: shortdesc}

To understand why you might disable and mirror the catalog, consider the following scenarios.
* For private clusters that run {{site.data.keyword.openshiftshort}} version 4.6 or later: The Red Hat-provided OperatorHub source images require access to the `registry.redhat.io` and `quay.io` registries. If your cluster runs on a restricted network, such as in a VPC without a public gateway or classic worker nodes on only a private VLAN, these images are not accessible
* You want to restrict the catalog content that is available to your cluster users in OperatorHub.

Before you begin:
* Make sure that you have the **Manager** service role to the cluster in all namespaces in {{site.data.keyword.cloud_notm}} IAM.
* [Install the `opm` command-line interface](https://docs.openshift.com/container-platform/4.6/cli_reference/opm-cli.html#opm-cli){: external}, including its prerequisite tools such as `podman`.
* Have a Red Hat account with credentials to pull images from the `registry.redhat.io` and `quay.io` registries, or use the [default global pull secret](/docs/openshift?topic=openshift-registry#cluster_global_pull_secret).

To disable and mirror the OperatorHub source images:
1. Disable the catalog sources as described in [Disabling the default OperatorHub sources](https://docs.openshift.com/container-platform/4.6/operators/admin/olm-restricted-networks.html#olm-restricted-networks-operatorhub_olm-restricted-networks){: external}.
2. **Optional**: Prune the catalog index to a select list of packages as described in [Pruning an index image](https://docs.openshift.com/container-platform/4.6/operators/admin/olm-restricted-networks.html#olm-pruning-index-image_olm-restricted-networks){: external}. You might prune the catalog to control what images your cluster users can install and to reduce the size of the images in your registry.
3. Mirror the catalog to your compatible registry, such as {{site.data.keyword.registrylong_notm}}, as described in [Mirroring an Operator catalog](https://docs.openshift.com/container-platform/4.6/operators/admin/olm-restricted-networks.html#olm-mirror-catalog_olm-restricted-networks){: external}.

<br />

## Using Operators in 3.11 clusters
{: #operators_311}

Try out the following tutorial.
{: shortdesc}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> The {{site.data.keyword.cloud_notm}} Operator and other Operators are experimental for version 3.11, and you are responsible for its maintenance and support. If you have a version 4 cluster, use the built-in [Operators and OperatorHub instead](#operators_4).
{: note}

<div class = "solutionBoxContainer">
    <div class = "solutionBox">
    <a href = "https://developer.ibm.com/tutorials/simplify-lifecycle-management-kubernetes-OpenShift-ibm-cloud-operator/">
        <div class = "solutionBoxContent">
                <p><strong>App lifecycle management with {{site.data.keyword.cloud_notm}} Operator</strong></p>
          <div class="solutionBoxDescription">
                <div class="descriptionContainer">
                  </br> <p>Use the Operator Lifecycle Manager (OLM) and the {{site.data.keyword.cloud_notm}} Operator to simplify your app lifecycle management approach for {{site.data.keyword.cloud_notm}} services, third-party apps, and your own custom-built, cloud-native apps in your {{site.data.keyword.openshiftshort}} cluster.</p></br>
                </div>
                <div class="architectureDiagramContainer">
                    <img class="architectureDiagram" src="images/dev_guides_operators.png" alt="IBM Cloud operator flowchart" />
                </div>
            </div>
        </div>
    </a>
    </div>
</div>

<br />

## Using the service catalog in 3.11 clusters
{: #service_catalog}

<img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> The service catalog is not supported in clusters that run version 4. Use [Operators](#operators_4) instead. Do not use the OperatorHub to install the service catalog.
{: important}

You can extend your app's capabilities by binding a service from the [{{site.data.keyword.openshiftshort}} service catalog](https://docs.openshift.com/container-platform/3.11/architecture/service_catalog/index.html){: external}. The service catalog is enabled in your 3.11 cluster by default. For an example of how to use the service catalog, see [Deploying an app with the {{site.data.keyword.openshiftshort}} service catalog](/docs/openshift?topic=openshift-getting-started#deploy-app).
{: shortdesc}

The catalog services and related [templates](https://docs.openshift.com/container-platform/3.11/dev_guide/templates.html#dev-guide-templates){: external} are extensions that you choose to add to your cluster and are not maintained, updated, or supported by IBM. To review the images or maintenance guidelines, follow the `readme` files or other documentation of each service.
{: note}

<br />






