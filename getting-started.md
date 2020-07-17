---

copyright:
  years: 2014, 2020
lastupdated: "2020-07-17"

keywords: red hat openshift, red hat openshift on ibm cloud, openshift container platform, red hat, create openshift cluster, openshift vpc cluster, openshift classic cluster, red hat cluster, openshift, containers, clusters, roks, rhoks, rhos

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

# Getting started with Red Hat OpenShift on IBM Cloud
{: #getting-started}

With Red Hat OpenShift on IBM Cloud, you can deploy apps on highly available OpenShift clusters that run the [Red Hat OpenShift on IBM Cloud Container Platform](https://docs.openshift.com/container-platform/4.3/welcome/index.html){: external} software on Red Hat Enterprise Linux machines.
{: shortdesc}

First, create a classic {{site.data.keyword.openshiftlong}} cluster or a cluster on the second generation of compute infrastructure in a Virtual Private Cloud (VPC). Then, deploy and expose a sample app in your cluster.
<br>

To complete the getting started tutorial, use a [Pay-As-You-Go or Subscription {{site.data.keyword.containerlong}} account](/docs/account?topic=account-upgrading-account) where you are the owner or have [full Administrator access](/docs/account?topic=account-assign-access-resources).
{: note}

<div class=solutionBoxContainer>
  <div class="solutionBox">
   <a href = "#clusters_gs">
    <div>
         <p><strong><img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Create a classic cluster</strong></p>
         <p class="bx--type-caption">Create an OpenShift cluster on {{site.data.keyword.cloud_notm}} classic workers nodes, subnets, and VLAN networking. Choose from a variety of virtual, bare metal, or software-defined storage flavors.</p>
    </div>
   </a>
  </div>
  <div class="solutionBox">
    <a href = "#vpc-gen2-gs">
      <div>
         <p><strong><img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Create a VPC cluster</strong></p>
         <p class="bx--type-caption">Create your cluster on the second generation of compute resources in a Virtual Private Cloud (VPC) that gives you the security of a private cloud with the scalability of a public cloud.</p>
      </div>
    </a>
  </div>
  <div class="solutionBox">
   <a href = "#deploy-app">
    <div>
         <p><strong><img src="images/icon-containers-bw.svg" alt="OpenShift Container icon" width="15" style="width:15px; border-style: none"/> Deploy and expose an app</strong></p>
         <p class="bx--type-caption">In your OpenShift cluster, deploy a sample app from a container image that is stored in Docker Hub. Then, expose it with a router to get an IP address for quick testing of your first app.</p>
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
2.  From the **Catalog**, click [**Red Hat OpenShift on IBM Cloud**](https://cloud.ibm.com/kubernetes/catalog/about?platformType=openshift){: external}.
3.  Review the platform version details, **OpenShift 4.3.23**.
4.  If you see the **OCP entitlement** section: Leave the value set to **Purchase additional licenses for this worker pool** because you are not using an {{site.data.keyword.cloud_notm}} Pak for this getting started cluster.
5.  For the **Infrastructure**, select **Classic**.
6.  Configure the **Location** details for your cluster.
    1.  Select the **Resource group** that you want to create your cluster in. You cannot change the resource group later. If you do not select a resource group, your cluster is created in the default resource group.
    2.  Select a **Geography** to create the cluster in, such as **North America**. The geography helps filter the **Availability** and **Data centers** values that you can select.
    3.  Select the **Availability** that you want for your cluster, such as **Single zone**.
    4.  Select the **Data center** to create your cluster in, such as **Dallas 10**.
7.  Configure your **Worker pool** setup.
    1.  If you want a larger size for your worker nodes, click **Change flavor**. Otherwise, leave the default **4 vCPUs / 16 GB** flavor selected.
    2.  Set how many worker nodes to create per zone, such as **3**. Note that you must have at least 2 worker nodes per zone in each worker pool to run the default OpenShift components.
8.  Fill out the **Resource details** to customize the cluster name and any tags that you want to use to organize your {{site.data.keyword.cloud_notm}} resources.
9.  Review the **Summary**, and then click **Create**.<p class="note">Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and load-balancing components take about 10 more minutes to deploy and update the cluster domain that you use for the OpenShift web console and other routes. Wait until the cluster is ready before continuing to the next step by checking that the **Ingress Subdomain** follows a pattern of `<cluster_name>.<globally_unique_account_HASH>-0001.<region>.containers.appdomain.cloud`.</p>
10.  Verify that your cluster setup is finished before you continue to the next step by checking that the worker nodes on the **Worker Nodes** tab have a **Status** of normal.

Now that your cluster is ready, [deploying your first app](#deploy-app)!

<br />




## Creating a VPC Gen 2 compute cluster
{: #vpc-gen2-gs}

Create a VPC Generation 2 compute cluster by using the {{site.data.keyword.cloud_notm}} console. VPC OpenShift clusters run version 4.3, which includes Kubernetes version 1.16. The operating system is Red Hat Enterprise Linux 7.
{: shortdesc}

Want to learn more about customizing your cluster setup with the CLI? Check out [Creating a VPC Gen 2 compute cluster](/docs/openshift?topic=openshift-clusters#clusters_vpcg2).
{: tip}

1. Create a Virtual Private Cloud (VPC) on generation 2 compute.
  1. Navigate to the [VPC create console](https://cloud.ibm.com/vpc/provision/vpc){: external}.
  2. Make sure that the banner at the beginning of the page is set to **Gen 2 compute**. If **Gen 1 compute** is set, click **Switch to Gen 2 compute**.
  3. Give the VPC a name and select a resource group to deploy the VPC into.
  4. Give the VPC subnet a name and select the location where you want to create the cluster.
  5. Attach a public gateway to your subnet so that you can access public endpoints from your cluster. This public gateway is used later on to access default OpenShift components like the web console, OperatorHub, and service catalog.
  6. Click **Create virtual private cloud**.
2. Allow traffic requests to apps that you deploy by modifying the VPC's default security group.
    1. From the [Virtual private cloud dashboard](https://cloud.ibm.com/vpc-ext/network/vpcs){: external}, click the name of the **Default Security Group** for the VPC that you created.
    2. In the **Inbound rules** section, click **New rule**.
    3. Choose the **TCP** protocol, enter `30000` for the **Port min** and `32767` for the **Port max**, and leave the **Any** source type selected.
    4. Click **Save**.
    5. If you require VPC VPN access or classic infrastructure access into this cluster, repeat these steps to add a rule that uses the **UDP** protocol, `30000` for the **Port min**, `32767` for the **Port max**, and the **Any** source type.
3. From the [Red Hat OpenShift on IBM Cloud dashboard](https://cloud.ibm.com/kubernetes/landing?platformType=openshift){: external}, click **Create cluster**.
4. Configure your cluster's VPC environment.
  1.  Review the platform version details, **OpenShift 4.3.23**.
  2.  If you see the **OCP entitlement** section: Leave the value set to **Purchase additional licenses for this worker pool** because you are not using an {{site.data.keyword.cloud_notm}} Pak for this getting started cluster.
  3.  For the **Infrastructure**, select **VPC**.
  4.  From the **Virtual private cloud** drop-down menu, select the VPC that you created earlier.
5.  Configure the **Location** details for your cluster.
    1. Select the **Resource group** that you want to create your cluster in. You cannot change the resource group later. If you do not select a resource group, your cluster is created in the default resource group.
    2. Select the zones to create your cluster in. The zones are filtered based on the VPC that you selected, and include the subnets that you previously created.
5.  Configure your **Worker pool** setup.
    1.  If you want a larger size for your worker nodes, click **Change flavor**. Otherwise, leave the default **4 vCPUs / 16 GB** flavor selected.
    2.  Set how many worker nodes to create per zone, such as **3**. Note that you must have at least 2 worker nodes per zone in each worker pool to run the default OpenShift components.
6.  Fill out the **Resource details** to customize the cluster name and any tags that you want to use to organize your {{site.data.keyword.cloud_notm}} resources.
7.  Review the **Summary**, and then click **Create**.<p class="note">Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and load-balancing components take about 10 more minutes to deploy and update the cluster domain that you use for the OpenShift web console and other routes. Wait until the cluster is ready before continuing to the next step by checking that the **Ingress Subdomain** follows a pattern of `<cluster_name>.<globally_unique_account_HASH>-0001.<region>.containers.appdomain.cloud`.</p>

<br>

The worker node can take a few minutes to provision, but you can see the progress in the **Worker nodes** tab. When the status reaches `Ready`, you can start working with your cluster by [deploying your first app](#deploy-app)!

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

* Complete the [Red Hat OpenShift on IBM Cloud classic cluster tutorial](/docs/openshift?topic=openshift-openshift_tutorial) or the [Red Hat OpenShift on IBM Cloud VPC cluster tutorial](/docs/openshift?topic=openshift-vpc_roks_tutorial) to:
  * Set up your {{site.data.keyword.cloud_notm}} and OpenShift CLI.
  * Deploy an app that uses an {{site.data.keyword.cloud_notm}} service.
* For more information about working with your apps, see the [OpenShift developer activities](https://docs.openshift.com/container-platform/4.3/welcome/index.html#developer-activities){: external} documentation.

Looking for an overview of all your options in Red Hat OpenShift on IBM Cloud? Check out the curated [learning path for administrators](/docs/openshift?topic=openshift-learning-path-admin) or [learning path for developers](/docs/openshift?topic=openshift-learning-path-dev).
{: tip}


