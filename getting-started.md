---

copyright:
  years: 2014, 2020
lastupdated: "2020-04-20"

keywords: openshift, containers, clusters, roks, rhoks, rhos

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

With {{site.data.keyword.openshiftlong}}, you can deploy apps on highly available clusters that come installed with the [Red Hat OpenShift on IBM Cloud Container Platform](https://docs.openshift.com/container-platform/4.2/welcome/index.html){: external} software installed on Red Hat Enterprise Linux.
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
         <p class="bx--type-caption">Create an OpenShift cluster on {{site.data.keyword.cloud_notm}} workers nodes, subnets, and VLAN networking. Choose from a variety of virtual, bare metal, or software-defined storage flavors.</p>
    </div>
    </a>
</div>
  <div class="solutionBox">
   <a href = "#deploy-app">
    <div>
         <h2><img src="images/icon-containers-bw.svg" alt="Container icon" width="15" style="width:15px; border-style: none"/> Deploy and expose an app</h2>
         <p class="bx--type-caption">Deploy a sample `websphere-liberty` app from a container image that is stored in Docker Hub. Then, expose it with a router to get an IP address for quick testing of your first app.</p>
     </div>
    </a>
</div>
    </div>

## Creating a classic OpenShift cluster
{: #clusters_gs}

Create a Red Hat OpenShift on IBM Cloud cluster on classic {{site.data.keyword.cloud_notm}} infrastructure in the {{site.data.keyword.cloud_notm}} console. To get started, create a cluster that runs OpenShift Container Platform version 4.3. The operating system is Red Hat Enterprise Linux 7.
{: shortdesc}

Want to learn more about customizing your cluster setup with the CLI? Check out [Creating an OpenShift cluster](/docs/openshift?topic=openshift-clusters).
{: tip}

1.  Log in to your [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/){: external}.
2.  From the **Catalog**, click [**Red Hat OpenShift Cluster**](https://cloud.ibm.com/kubernetes/catalog/openshiftcluster){: external}, and then click **Create**.
3.  Choose your cluster setup details and name.
    *   Enter a unique name for your cluster, and select the resource group that you want to assign to your cluster.
    *   Enter tags that you want to add to your cluster. Tags can help you organize and find your clusters more easily in your  {{site.data.keyword.cloud_notm}} account.
    *   For the **Location**, set the **Geography**, and then select any of the six worldwide multizone **Metro** or single zone [locations](/docs/openshift?topic=openshift-regions-and-zones) to use for your **Worker zones**.
    *   In the **Default worker pool** section, configure your worker pool version and size.
        *  For **OpenShift version**, select 4.3.
        *  For **Flavor**, choose an available flavor for your worker nodes.
        *  For **Worker nodes**, set a number of worker nodes to create in each zone of the worker pool, such as `3`.
4.  To finish, click **Create cluster**.<p class="note">Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and load-balancing components take about 10 more minutes to deploy and update the cluster domain that you use for the OpenShift web console and other routes. Wait until the cluster is ready before continuing to the next step by checking that the **Ingress Subdomain** follows a pattern of `<cluster_name>.<globally_unique_account_HASH>-0001.<region>.containers.appdomain.cloud`.</p>
5.  Verify that your cluster setup is finished before you continue to the next step by checking that the worker nodes on the **Worker Nodes** tab have a **Status** of normal.

Now that your cluster is ready, [deploy an app](#deploy-app).

<br />



## Deploying an app with the OpenShift service catalog
{: #deploy-app}

From the OpenShift console, you can deploy one of the built-in service catalog apps and expose the app with a route.
{: shortdesc}

1.  From the cluster details page, click **OpenShift web console**.
2.  From the side navigation menu in the **Administrator** perspective, click **Home > Projects** and then click **Create Project**. Enter a name for your project, and click **Create**. Now that your project is created by the administrator, you can switch to the Developer perspective to create an app.
3.  From the side navigation menu, select **Developer** from the perspective switcher.
4.  Click **+Add**. From the **Add** pane menu bar, make sure that the **Project** is the one that you just created.
5.  Click **From Catalog**. The **Developer Catalog** opens in the pane.
6.  From the navigation menu in the pane, click **Languages > JavaScript**.
7.  Click **Node.js**, and then click **Create Application**. The **Create Source-to-Image Application** pane opens.
8.  In the **Git** section, click **Try Sample**.
9.  Scroll to confirm that **Deployment** and **Create a route to the application** are selected, and then click **Create**.
8.  Wait a few minutes for the pods to deploy. To check the status of the pods, from the **Topology** pane, click your **nodejs** app and review its sidebar. You must see that the `nodejs` build is complete, and that the `nodejs` pod is in a **Running** state to continue.
9.  When the deployment is complete, click the route location URL, which has a format similar to the following.

    ```
    http://nodejs-<project>.<cluster_name>-<hash>.<region>.containers.appdomain.cloud
    ```
    {: screen}

    A new tab in your browser opens with a message similar to the following.
    ```
    Welcome to your Node.js application on OpenShift
    ```
    {: screen}
10.  **Optional**: To clean up the resources that you created, select **Administrator** from the perspective switcher, navigate to **Home > Projects**, click your project's action menu, and click **Delete Project**.

<br />


## What's next?
{: #whats-next}

Complete the [Red Hat OpenShift on IBM Cloud tutorial](/docs/openshift?topic=openshift-openshift_tutorial) to:
* Set up your {{site.data.keyword.cloud_notm}} and OpenShift CLI.
* Deploy an app that uses an {{site.data.keyword.cloud_notm}} service.

<br>
For more information about working with your apps, see the [OpenShift developer activities](https://docs.openshift.com/container-platform/4.2/welcome/index.html#developer-activities){: external} documentation.

Looking for an overview of all your options in Red Hat OpenShift on IBM Cloud? Check out the curated [learning path for administrators](/docs/openshift?topic=openshift-learning-path-admin) or [learning path for developers](/docs/openshift?topic=openshift-learning-path-dev).
{: tip}


