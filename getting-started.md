---

copyright:
  years: 2014, 2020
lastupdated: "2020-01-02"

keywords: openshift, containers, clusters, roks, rhoks, rhos

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
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

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
    .icon {
        width: 1rem;
        height: 1rem;
    }
    .bx--tile-content {
        box-shadow: 0 1px 2px 0 rgba(0,0,0,0.2);
        background-color: #fff;
        border: 1px solid #dfe3e6;
    }
    .solutionBoxContainer {}
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
        height: 300px !important;
        }
    }
    @media screen and (min-width: 1298px) {
        .solutionBox {
        width: calc(33% - 2%) !important;
        }
        .solutionBoxContent {
        min-height: 300px !important;
        }
    }
    .solutionBox:hover {
        border-color: rgb(136, 151, 162) !important;
    }
    .solutionBoxDescription {
        flex-grow: 1 !important;
        display: flex !important;
        flex-direction: column !important;
    }
-->
</style>



# Getting started with Red Hat OpenShift on IBM Cloud
{: #getting-started}

With {{site.data.keyword.openshiftlong}}, you can deploy apps on highly available clusters that come installed with the [Red Hat OpenShift on IBM Cloud Container Platform![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/welcome/index.html) software installed on Red Hat Enterprise Linux.
{: shortdesc}

First, create a Red Hat OpenShift on IBM Cloud cluster. Then, deploy and expose a sample app in your cluster.
<br>

To complete the getting started tutorial, use a [Pay-As-You-Go or Subscription {{site.data.keyword.containerlong}} account](/docs/account?topic=account-upgrading-account) where you are the owner or have [full Administrator access](/docs/iam?topic=iam-iammanidaccser).
{: note}

  <div class=solutionBoxContainer>
  <div class="solutionBox">
   <a href = "#clusters_gs">
    <div>
         <h2><img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Create a cluster</h2>
         <p class="bx--type-caption">Create an OpenShift cluster on {{site.data.keyword.cloud_notm}} workers nodes, subnets, and VLAN networking. Choose from a variety of virtual, bare metal, GPU, or software-defined storage flavors.</p>
    </div>
    </a>
</div>
  <div class="solutionBox">
   <a href = "#deploy-app">
    <div>
         <h2><img src="images/icon-containers-bw.svg" alt="Container icon" width="15" style="width:15px; border-style: none"/> Deploy and expose an app</h2>
         <p class="bx--type-caption">Deploy a sample `node.js` app as a container from an image that is stored in GitHub. Then, expose it with a router to get an IP address for quick testing of your first app.</p>
     </div>
    </a>
</div>
    </div>

## Creating a classic OpenShift cluster
{: #clusters_gs}

Create a Red Hat OpenShift on IBM Cloud cluster on classic {{site.data.keyword.cloud_notm}} infrastructure in the {{site.data.keyword.cloud_notm}} console. OpenShift clusters run version 3.11, which includes Kubernetes version 1.11. The operating system is Red Hat Enterprise Linux 7.
{: shortdesc}

Want to learn more about customizing your cluster setup with the CLI? Check out [Creating an OpenShift cluster](/docs/openshift?topic=openshift-clusters).
{: tip}

1.  Log in to your [{{site.data.keyword.cloud_notm}} account ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/).
2.  From the **Catalog**, click [**Red Hat OpenShift Cluster** ![External link icon](../icons/launch-glyph.svg "External link icon")]](https://cloud.ibm.com/kubernetes/catalog/openshiftcluster), and then click **Create**.
3.  Choose your cluster setup details and name.
    *   Enter a unique name for your cluster, and select the resource group that you want to assign to your cluster.
    *   Enter tags that you want to add to your cluster. Tags can help you organize and find your clusters more easily in your  {{site.data.keyword.cloud_notm}} account.
    *   For the **Location**, set the **Geography**, and then select any of the six worldwide multizone **Metro** or single zone [locations](/docs/openshift?topic=openshift-regions-and-zones) to use for your **Worker zones**.
    *   For **Default worker pool**, choose an available flavor for your worker nodes. Red Hat OpenShift on IBM Cloud supports OpenShift version 3.11 only, which includes Kubernetes version 1.11. The operating system is Red Hat Enterprise Linux 7.
    *   Set a number of worker nodes to create per zone, such as `3`.
4.  To finish, click **Create cluster**.<p class="note">Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and load-balancing component take about 10 more minutes to deploy and update the cluster domain that you use for the OpenShift web console and other routes. </p>
5.  Verify that your cluster setup is finished before you continue to the next step by checking that the worker nodes on the **Worker Nodes** tab have a **Status** of normal.

Now that your cluster is ready, [deploy an app](#deploy-app).

<br />



## Deploying an app with the OpenShift service catalog
{: #deploy-app}

From the OpenShift console, you can deploy one of the built-in service catalog apps.
{: shortdesc}

1.  From the cluster details page, click **OpenShift web console**.
2.  In the **My Projects** pane, click **Create Project**. Enter a name for your project name, and click **Create**.
3.  Click your project name, then click **Browse Catalog**.
4.  Click an app to deploy. For example, from the **Language** tab, select **JavaScript**, and then click **Node.js**. The Node.js wizard opens.
    1.  In the *Information* tab, click **Next**.
    2.  In the *Configuration* tab, click **Try Sample Repository**, then click **Create**.
    3.  In the *Results* tab, the `nodejs-ex` app is created. Click **Close**.
5.  Wait a few minutes for the pods to deploy. To check the status of the pods, click **Applications > Pods**. You must see one `nodejs-ex-build` pod in a **Completed** state, and one `nodejs-ex` pod in a **Running** state.
6.  When both pods are available, click **Applications > Routes**.
7.  Click the **Hostname** of your `nodejs-ex` app. A new tab in your browser opens with a message similar to the following.
    ```
    Welcome to your Node.js application on OpenShift
    ```
    {: screen}
8.  **Optional**: To clean up the resources that you created, click the project name in the menu bar and then **View All Projects**. Click the **More options icon > Delete project**.

<br />


## What's next?
{: #whats-next}

Complete the [Red Hat OpenShift on IBM Cloud tutorial](/docs/openshift?topic=openshift-openshift_tutorial) to:
* Set up your {{site.data.keyword.cloud_notm}} and OpenShift CLI.
* Deploy an app that uses an {{site.data.keyword.cloud_notm}} service.

<br>
For more information about deploying and routing network traffic to your apps, see the [OpenShift Developer Guide ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/dev_guide/index.html).


