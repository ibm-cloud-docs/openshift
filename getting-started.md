---

copyright:
  years: 2023, 2025
lastupdated: "2025-03-05"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes cluster, red hat openshift, openshift container platform, red hat, create openshift cluster, vpc cluster, classic cluster, clusters

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}



# Getting started with {{site.data.keyword.openshiftlong_notm}}
{: #getting-started}

{{site.data.keyword.openshiftlong_notm}} is a managed Kubernetes service to create your own cluster of compute hosts where you can deploy and manage containerized apps on IBM Cloud. Combined with an intuitive user experience, built-in security and isolation, and advanced tools to secure, manage, and monitor your cluster workloads, you can rapidly deliver highly available and secure containerized apps in the public cloud.
{: shortdesc}

Complete the following steps to get familiar with the basics, understand the service components, create your first cluster, and deploy a starter app.

## Review the basics
{: #getting-started-basics}
{: step}

Get an overview of the service by reviewing the concepts, terms, and benefits. For more information, see [Understanding {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-overview).

Already familiar with containers and {{site.data.keyword.openshiftlong_notm}}? Continue to the next step to prepare your account for creating clusters.

## Prepare your account
{: #getting-started-prepare-account}
{: step}

To set up your {{site.data.keyword.cloud_notm}} account so that you can create clusters, see [Preparing your account to create clusters](/docs/openshift?topic=openshift-clusters).

If you've already prepared your account and you're ready to create a cluster, continue to the next step.

## Create a cluster environment strategy
{: #getting-started-strategy}
{: step}

Review the decision points in the [Creating a cluster environment strategy](/docs/openshift?topic=openshift-strategy) doc to begin designing your setup.

Not sure where to start? Try following a tutorial in the next step.
{: tip}


## Create a cluster
{: #getting-started-create}
{: step}

Follow a tutorial, or set up your own custom cluster environment. Review the following table for your deployment options.


| Type | Level | Time | Description |
| --- | --- | --- | --- | 
| Tutorial | Beginner | 30 minutes | Create a small, 2 node cluster to begin testing {{site.data.keyword.openshiftlong_notm}}. For more information, see [Creating a 2 node VPC cluster by using Schematics](/docs/openshift?topic=openshift-tutorial-two-node). | 
| Tutorial | Beginner | 45 minutes | Follow the steps in this tutorial to create your first cluster by using the IBM Cloud CLI. This tutorial uses Classic infrastructure. For more information, see [Creating a classic cluster from the CLI](/docs/openshift?topic=openshift-openshift_tutorial). |
| Tutorial| Beginner | 1 hour | Follow the steps in this tutorial to create your own Virtual Private Cloud (VPC), then create an {{site.data.keyword.openshiftlong_notm}} cluster by using the CLI. For more information, see [Create a cluster in your own Virtual Private Cloud](/docs/openshift?topic=openshift-vpc_rh_tutorial). |
| Deployable architecture: QuickStart variation | Beginner | 1 hour | This deployable architecture creates one VPC cluster with two worker nodes and a public endpoint. Note that the QuickStart variation is not highly available or validated for the IBM Cloud Framework for Financial Services. For more information, see [{{site.data.keyword.openshiftlong_notm}} on VPC landing zone](https://cloud.ibm.com/catalog?search=openshift%20label%3Areference_architecture#search_results){: explore} |
| Deployable architecture: Standard variation | Intermediate | 1-3 hours | This deployable architecture is based on the IBM Cloud for Financial Services reference architecture. The architecture creates secure and compliant clusters on a Virtual Private Cloud (VPC) network. For more information, see [{{site.data.keyword.openshiftlong_notm}} on VPC landing zone](https://cloud.ibm.com/catalog?search=openshift%20label%3Areference_architecture#search_results){: explore}. |
| Deployable architectures: Community Registry | Intermediate | 1-4 hours | There are more deployable architectures available in the Community Registry. Review the options to see if they fit your use case. For more information, see [Catalog](https://cloud.ibm.com/catalog#reference_architecture){: external} and select **Community Registry** from the drop-down menu. |
| Deployable architectures: OpenShift AI on {{site.data.keyword.IBM}} | Intermediate | 1-2 hours | This deployable architecture creates a new OpenShift cluster that runs GPU worker nodes and includes the Red Hat OpenShift AI operator. For more information, see [OpenShift AI on IBM Cloud](https://cloud.ibm.com/catalog/7a4d68b4-cf8b-40cd-a3d1-f49aff526eb3/architecture/roks-rhoai-c24ae512-8b25-43d7-8fb3-4173c7e94472-global){: external} in the Catalog. | 
| Custom deployment | Intermediate | 1-3 hours | [Create a custom cluster on Classic infrastructure](/docs/openshift?topic=openshift-cluster-create-classic). |
| Custom deployment | Intermediate | 1-3 hours | [Create a custom cluster on VPC infrastructure](/docs/openshift?topic=openshift-cluster-create-vpc-gen2). |
{: caption="Options for creating a cluster" caption-side="bottom"}

Already have a cluster? Continue to the next step to deploy a sample app!




## Deploy a sample app
{: #getting-started-deploy-app}
{: step}

After you create your cluster, deploy a sample app from the {{site.data.keyword.redhat_openshift_notm}} console, you can deploy one of the built-in service catalog apps and expose the app with a route.


1. From the navigation menu, change from the **Administrator** perspective to **Developer** perspective.
1. Click **+Add** > **View all samples** > **Go**.
1. Wait a few minutes for the resources to deploy. 
1. Check the status from the **Topology** pane by clicking your **`Go`** app and reviewing the sidebar.
1. When the deployment is complete. Click the **Open URL** button to view your app in a web browser.

    ```txt
    Hello World!
    ```
    {: screen}

1. To clean up the resources that you created, delete your deployment from the **Topology** pane.





## What's next?
{: #getting-started-whats-next}


Check out the curated learning paths
- [Learning path for administrators](/docs/openshift?topic=openshift-learning-path-admin).
- [Learning path for developers](/docs/openshift?topic=openshift-learning-path-dev).
