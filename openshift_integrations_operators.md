---

copyright:
  years: 2014, 2020
lastupdated: "2020-09-16"

keywords: kubernetes, openshift, roks, rhoks, rhos

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
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
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
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
{:swift: #swift .ph data-hd-programlang='swift'}
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
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}



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

In {{site.data.keyword.openshiftshort}} clusters that run version 4, operators are available in your cluster by default. Use [Operators](https://docs.openshift.com/container-platform/4.1/applications/operators/olm-what-operators-are.html){: external} to package, deploy, and update the apps in your {{site.data.keyword.openshiftlong_notm}} clusters.
{: shortdesc}

1.  To use operators, follow the {{site.data.keyword.openshiftshort}} documentation.
    *   [Adding Operators to a cluster](https://docs.openshift.com/container-platform/4.1/applications/operators/olm-adding-operators-to-cluster.html){: external}
    *   [Deleting Operators from a cluster](https://docs.openshift.com/container-platform/4.1/applications/operators/olm-deleting-operators-from-cluster.html){: external}
    *   [Creating applications from installed Operators](https://docs.openshift.com/container-platform/4.1/applications/operators/olm-creating-apps-from-installed-operators.html){: external}
    *   [Making your own custom Operator](https://github.com/operator-framework/community-operators/blob/master/docs/testing-operators.md#testing-operator-deployment-on-openshift){: external}.
        *  For help creating custom Operators, see the [Operator SDK](https://docs.openshift.com/container-platform/4.2/operators/operator_sdk/osdk-getting-started.html){: external} documentation, which includes a guide to build an operator that is based on a [Helm chart](https://docs.openshift.com/container-platform/4.2/operators/operator_sdk/osdk-helm.html){: external}.
        *  To manage your custom Operator, see the [Operator Lifecycle Manager](http://docs.openshift.com/container-platform/4.2/operators/understanding_olm/olm-understanding-olm.html){: external} documentation.
2.  Review any custom steps to install an operator in your cluster.
    *   To set up an [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana (EFK) stack](https://docs.openshift.com/container-platform/4.3/logging/cluster-logging.html){: external}, see [installing the cluster logging operator](/docs/openshift?topic=openshift-health#oc_logging_operator).
3.  If the operator uses a template with a build component that must pull an image from a private registry, the build might fail with an authentication error. To resolve this error, see [Build error due to image pull authentication](/docs/openshift?topic=openshift-cs_troubleshoot_app#ts_build_img_pull).

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

