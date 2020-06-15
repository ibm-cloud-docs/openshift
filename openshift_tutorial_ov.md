---

copyright:
  years: 2014, 2020
lastupdated: "2020-06-15"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---

{:beta: .beta}
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




# Tutorial overview
{: #tutorials-ov}

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


## Create a cluster and deploy apps
{: #tutorials-create-cluster-deploy-app}

<div class = "solutionBoxContainer">
  <a href = "/docs/openshift?topic=openshift-openshift_tutorial">
  <div class = "solutionBox">
      <div class = "solutionBoxContent">
        {{site.data.keyword.openshiftlong_notm}} cluster
        <div class="solutionBoxDescription">
              <div class="descriptionContainer">
                </br><p>Create an {{site.data.keyword.openshiftshort}} cluster with worker nodes that come installed with the {{site.data.keyword.openshiftshort}} container orchestration platform software.</p></br>
                </div>
                <div class="architectureDiagramContainer">
                    <img class="architectureDiagram" src="images/roks_tutorial.png" alt="OpenShift tutorial diagram flow" /></br>
              </div>
          </div>
      </div>
  </div>
  </a>
    <a href = "/docs/openshift?topic=openshift-openshift_tutorial_vpc">
    <div class = "solutionBox">
        <div class = "solutionBoxContent">
          {{site.data.keyword.openshiftshort}} cluster on VPC Gen 2
          <div class="solutionBoxDescription">
                <div class="descriptionContainer">
                  </br><p>Create an {{site.data.keyword.openshiftlong}} cluster in your Virtual Private Cloud with worker nodes on the next generation of compute infrastructure.</p></br>
                  </div>
                  <div class="architectureDiagramContainer">
                    <img class="architectureDiagram" src="images/vpc_roks_tutorial_lesson4_lb.png" alt="OpenShift tutorial diagram flow" /></br>
                </div>
            </div>
        </div>
    </div>
    </a>
  <a href = "/docs/tutorials?topic=solution-tutorials-scalable-webapp-openshift">
    <div class = "solutionBox">
        <div class = "solutionBoxContent">
          Scalable web app on {{site.data.keyword.openshiftshort}}
            <div class="solutionBoxDescription">
                <div class="descriptionContainer">
                  </br> <p>Scaffold a web app, deploy it to a cluster, and learn how to scale your app and monitor its health. </p></br>
                </div>
                <div class="architectureDiagramContainer">
                    <img class="architectureDiagram" src="https://raw.githubusercontent.com/ibm-cloud-docs/tutorials/master/images/solution50-scalable-webapp-openshift/Architecture.png" alt="Architecture diagram for deploying web apps with {{site.data.keyword.openshiftlong_notm}}" />
                </div>
            </div>
        </div>
    </div>
  </a>
  <a href = "/docs/terraform?topic=terraform-redhat">
  <div class = "solutionBox">
      <div class = "solutionBoxContent">
              Automate version 3.11 cluster creation with Terraform
          <div class="solutionBoxDescription">
              <div class="descriptionContainer">
                </br><p>Use Terraform to automate the deployment of an {{site.data.keyword.openshiftlong_notm}} cluster that runs {{site.data.keyword.openshiftshort}} version 3.11.</p></br>
              </div>
              <div class="architectureDiagramContainer">
                  <img class="architectureDiagram" src="images/terraform_roks_tutorial_ov.png" alt="Terraform deployment automation architecture" />
              </div>
          </div>
      </div>
  </div>
  </a>
</div>


## Dive deeper into {{site.data.keyword.openshiftshort}} technology
{: #tutorials-deep-dive}

<div class = "solutionBoxContainer">
    <a href = "https://developer.ibm.com/tutorials/automatic-security-certificate-renewal-OpenShift/">
    <div class = "solutionBox">
        <div class = "solutionBoxContent">
                Security certificates for domains
          <div class="solutionBoxDescription">
                <div class="descriptionContainer">
                  </br> <p>Renew security certificates automatically for web domains by using a DNS provider and IBM Cloud Certificate Manager with your Red Hat OpenShift on IBM Cloud cluster.</p></br>
                </div>
                <div class="architectureDiagramContainer">
                    <img class="architectureDiagram" src="images/dev_guides_certs.png" alt="Domain certifcate flowchart" />
                </div>
            </div>
        </div>
    </div>
    </a>
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
    <a href = "https://learn.openshift.com">
    <div class = "solutionBox">
        <div class = "solutionBoxContent">
                Red Hat OpenShift interactive learning portal
          <div class="solutionBoxDescription">
                <div class="descriptionContainer">
                  </br> <p>Complete the courses and test out OpenShift concepts with a pre-configured OpenShift instance that is accessible from your browser.</p></br>
                </div>
                <div class="architectureDiagramContainer">
                    <img class="architectureDiagram" src="images/logo_openshift.svg" alt="Red Hat OpenShift logo for learning portal" />
                </div>
            </div>
        </div>
    </div>
    </a>
    <a href = "https://www.katacoda.com/openshift">
    <div class = "solutionBox">
        <div class = "solutionBoxContent">
                Katacoda site for learning OpenShift
          <div class="solutionBoxDescription">
                <div class="descriptionContainer">
                  </br> <p>Learn how to use OpenShift to build, run, and scale your apps in the cloud so that you can focus on writing code.</p></br>
                </div>
                <div class="architectureDiagramContainer">
                    <img class="architectureDiagram" src="https://katacoda.com/scenario-examples/scenarios/displaying-images/assets/logo-text-with-head.png" alt="Katacoda logo for learning platform" />
                </div>
            </div>
        </div>
    </div>
    </a>
</div>
