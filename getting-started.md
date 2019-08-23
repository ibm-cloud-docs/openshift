---

copyright:
  years: 2014, 2019
lastupdated: "2019-08-23"

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

# Getting started with Red Hat OpenShift on IBM Cloud
{: #getting-started}

With Red Hat OpenShift on IBM Cloud, you can create {{site.data.keyword.containerlong_notm}} clusters with worker nodes that come installed with the Red Hat OpenShift on IBM Cloud Container Platform orchestration software. You get all the [advantages of managed {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-responsibilities_iks) for your cluster infrastructure environment, while using the [OpenShift tooling and catalog ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/welcome/index.html) that runs on Red Hat Enterprise Linux for your app deployments.
{: shortdesc}

To complete the getting started tutorial, use a Pay-As-You-Go {{site.data.keyword.cloud_notm}} account where you are the owner or have full Administrator privileges. This getting started tutorial focuses on setting up a cluster and sample app quickly by using the {{site.data.keyword.cloud_notm}} console. For more information on how to use the CLI to create your OpenShift cluster and deploy an app, check out this [tutorial](/docs/openshift?topic=openshift-openshift_tutorial).

## Creating an OpenShift cluster
{: #openshift_gs_cluster}

Create a Red Hat OpenShift on IBM Cloud cluster in the {{site.data.keyword.containerlong_notm}} console. OpenShift clusters run version 3.11, which includes Kubernetes version 1.11. The operating system is Red Hat Enterprise Linux 7.
{: shortdesc}

Want to learn more about customizing your cluster setup with the CLI? Check out [Creating an OpenShift cluster](/docs/openshift?topic=openshift-openshift-create-cluster).
{: tip}

1.  Log in to your [{{site.data.keyword.cloud_notm}} account ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/).
2.  From the **Catalog**, click [**Red Hat OpenShift Cluster** ![External link icon](../icons/launch-glyph.svg "External link icon")]](https://cloud.ibm.com/kubernetes/catalog/openshiftcluster), and then click **Create**.
3.  Choose your cluster setup details and name.
    *   Enter a name for your cluster, and select the resource group that you want to assign to your cluster.
    *   Enter tags that you want to add to your cluster. Tags can help you organize and find your clusters more easily in your  {{site.data.keyword.cloud_notm}} account.
    *   For the **Location**, set the **Geography**, and then select any of the six worldwide multizone **Metro** [locations](/docs/openshift?topic=openshift-regions-and-zones) to use for your **Worker zones**.
    *   For **Default worker pool**, choose an available flavor for your worker nodes. Red Hat OpenShift on IBM Cloud supports OpenShift version 3.11 only, which includes Kubernetes version 1.11. The operating system is Red Hat Enterprise Linux 7.
    *   Set a number of worker nodes to create per zone, such as `3`.
4.  To finish, click **Create cluster**.<p class="note">Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and load-balancing component take about 10 more minutes to deploy and update the cluster domain that you use for the OpenShift web console and other routes. </p>
5.  Verify that your cluster setup is finished before you continue to the next step by checking that the **Ingress subdomain** on the cluster details page follows a pattern of `<cluster_name>.<region>.containers.appdomain.cloud`.

<br />


## Deploying an app with the OpenShift catalog
{: #openshift_gs_app}

From the OpenShift console, you can deploy one of the built-in catalog apps.
{: shortdesc}

1.  From the cluster details page, click **OpenShift web console**.
2.  In the **My Projects** pane, click **Create Project**. Enter a name for your project name, and click **Create**. If you already have existing projects, your pane name changes to **My Projects**.
3.  Click your project name, then click **Browse Catalog**.
4.  Click an app to deploy. For example, from the **Language** tab, select **JavaScript**, and then click **Node.js**. The Node.js wizard opens.
    1.  In the *Information* tab, click **Next**.
    2.  In the *Configuration* tab, click **Try Sample Repository**.
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
{: #openshift_gs_next}

Complete the [Red Hat OpenShift on IBM Cloud tutorial](/docs/openshift?topic=openshift-openshift_tutorial) to:
* Set up your {{site.data.keyword.cloud_notm}} and OpenShift CLI.
* Deploy an app that uses an {{site.data.keyword.cloud_notm}} service.

<br>
For more information about working with your apps and routing services, see the [OpenShift Developer Guide ![External link icon](../icons/launch-glyph.svg "External link icon")]](https://docs.openshift.com/container-platform/3.11/dev_guide/index.html).

<br />

