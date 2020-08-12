---

copyright:
  years: 2014, 2020
lastupdated: "2020-08-12"

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
{:java: data-hd-programlang="java"}
{:javascript: data-hd-programlang="javascript"}
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



{[css-tiles.html]}

# Tutorial overview
{: #tutorials-ov}

Check out the following tutorials to learn how to make the most of your {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

## Create a cluster and deploy apps
{: #tutorials-create-cluster-deploy-app}

<div class = "solutionBoxContainer">
  <div class = "solutionBox">
  <a href = "/docs/openshift?topic=openshift-openshift_tutorial">
      <div class = "solutionBoxContent">
        <p><strong>Red Hat OpenShift on IBM Cloud cluster</strong></p>
        <div class="solutionBoxDescription">
              <div class="descriptionContainer">
                </br><p>Create a cluster with worker nodes that come installed with OpenShift container orchestration platform.</p></br>
                </div>
                <div class="architectureDiagramContainer">
                    <img class="architectureDiagram" src="images/roks_tutorial.png" alt="OpenShift tutorial diagram flow" /></br>
              </div>
          </div>
      </div>
  </a>
  </div>
    <div class = "solutionBox">
    <a href = "/docs/openshift?topic=openshift-vpc_rh_tutorial">
        <div class = "solutionBoxContent">
          <p><strong>OpenShift cluster on VPC Gen 2</strong></p>
          <div class="solutionBoxDescription">
                <div class="descriptionContainer">
                  </br><p>Create an OpenShift cluster in your Virtual Private Cloud with worker nodes on the next generation of compute infrastructure.</p></br>
                  </div>
                  <div class="architectureDiagramContainer">
                    <img class="architectureDiagram" src="images/vpc_roks_tutorial_lesson4_lb.png" alt="OpenShift tutorial diagram flow" /></br>
                </div>
            </div>
        </div>
    </a>
    </div>
    <div class = "solutionBox">
    <a href = "/docs/solution-tutorials?topic=solution-tutorials-scalable-webapp-openshift">
        <div class = "solutionBoxContent">
          <p><strong>Scalable web app on OpenShift</strong></p>
            <div class="solutionBoxDescription">
                <div class="descriptionContainer">
                  </br> <p>Scaffold a web app, deploy it to a cluster, and learn how to scale your app and monitor its health. </p></br>
                </div>
                <div class="architectureDiagramContainer">
                    <img class="architectureDiagram" src="https://raw.githubusercontent.com/ibm-cloud-docs/tutorials/master/images/solution50-scalable-webapp-openshift/Architecture.png" alt="Architecture diagram for deploying web apps with Red Hat OpenShift on IBM Cloud" />
                </div>
            </div>
        </div>
    </a>
    </div>
  <div class = "solutionBox">
  <a href = "/docs/terraform?topic=terraform-redhat">
      <div class = "solutionBoxContent">
            <p><strong>Automate version 3.11 cluster creation with Terraform</strong></p>
          <div class="solutionBoxDescription">
              <div class="descriptionContainer">
                </br><p>Use Terraform to automate the deployment of an OpenShift 3.11 cluster.</p></br>
              </div>
              <div class="architectureDiagramContainer">
                  <img class="architectureDiagram" src="images/terraform_roks_tutorial_ov.png" alt="Terraform deployment automation architecture" />
              </div>
          </div>
      </div>
  </a>
  </div>
</div>


## Dive deeper into OpenShift technology
{: #tutorials-deep-dive}

<div class = "solutionBoxContainer">
    <div class = "solutionBox">
    <a href = "https://developer.ibm.com/tutorials/automatic-security-certificate-renewal-OpenShift/">
        <div class = "solutionBoxContent">
            <p><strong>Security certificates for domains</strong></p>
          <div class="solutionBoxDescription">
                <div class="descriptionContainer">
                  </br> <p>Renew security certificates automatically for web domains with a DNS provider,Certificate Manager, and OpenShift cluster.</p></br>
                </div>
                <div class="architectureDiagramContainer">
                    <img class="architectureDiagram" src="images/dev_guides_certs.png" alt="Domain certifcate flowchart" />
                </div>
            </div>
        </div>
    </a>
    </div>
    <div class = "solutionBox">
    <a href = "https://developer.ibm.com/tutorials/simplify-lifecycle-management-kubernetes-OpenShift-ibm-cloud-operator/">
        <div class = "solutionBoxContent">
            <p><strong>App lifecycle management with {{site.data.keyword.cloud_notm}} Operator</strong></p>
          <div class="solutionBoxDescription">
                <div class="descriptionContainer">
                  </br> <p>Simplify your app lifecycle management approach for {{site.data.keyword.cloud_notm}} services, third-party apps, and your own custom-built, cloud-native apps in your OpenShift cluster.</p></br>
                </div>
                <div class="architectureDiagramContainer">
                    <img class="architectureDiagram" src="images/dev_guides_operators.png" alt="IBM Cloud operator flowchart" />
                </div>
            </div>
        </div>
    </a>
    </div>
    <div class = "solutionBox">
    <a href = "https://learn.openshift.com">
        <div class = "solutionBoxContent">
            <p><strong>Red Hat OpenShift interactive learning portal</strong></p>
          <div class="solutionBoxDescription">
                <div class="descriptionContainer">
                  </br> <p>Test out OpenShift concepts with a pre-configured OpenShift instance that is accessible from your browser.</p></br>
                </div>
                <div class="architectureDiagramContainer">
                    <img class="architectureDiagram" src="images/logo_openshift.svg" alt="Red Hat OpenShift logo for learning portal" />
                </div>
            </div>
        </div>
    </a>
    </div>
    <div class = "solutionBox">
    <a href = "https://www.katacoda.com/openshift">
        <div class = "solutionBoxContent">
            <p><strong>Katacoda site for learning OpenShift</strong></p>
          <div class="solutionBoxDescription">
                <div class="descriptionContainer">
                  </br> <p>Learn how to use OpenShift to build, run, and scale your apps in the cloud so that you can focus on writing code.</p></br>
                </div>
                <div class="architectureDiagramContainer">
                    <img class="architectureDiagram" src="https://katacoda.com/scenario-examples/scenarios/displaying-images/assets/logo-text-with-head.png" alt="Katacoda logo for learning platform" />
                </div>
            </div>
        </div>
    </a>
    </div>
</div>
