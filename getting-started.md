---

copyright:
  years: 2023, 2026
lastupdated: "2026-07-09"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes cluster, red hat openshift, openshift container platform, red hat, create openshift cluster, vpc cluster, classic cluster, clusters

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}



# Getting started with {{site.data.keyword.openshiftlong_notm}}
{: #getting-started}

{{site.data.keyword.openshiftlong_notm}} is a managed Kubernetes service to create your own cluster of compute hosts where you can deploy and manage containerized apps on IBM Cloud. Combined with an intuitive user experience, built-in security and isolation, and advanced tools to secure, manage, and monitor your cluster workloads, you can rapidly deliver highly available and secure containerized apps in the public cloud.
{: shortdesc}

## Ready to create your first cluster?
{: #getting-started-quick-start}

If you already have an IBM Cloud account and want to get started immediately:

[Create a cluster now](https://cloud.ibm.com/containers/cluster-management/catalog/create?platformType=openshift){: external}

Don't have an account? [Sign up for IBM Cloud](https://cloud.ibm.com/registration?target=/kubernetes/catalog/create?platformType=openshift){: external}

Use this page to move through the main setup flow: review the service, prepare your account, plan your environment, create a cluster, and deploy a sample app.

## Review the basics
{: #getting-started-basics}

Start with the core concepts, terminology, and benefits. For more information, see [Understanding {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-overview).

If you already know the basics, continue to the next section.

## Prepare your account
{: #getting-started-prepare-account}

Make sure that your {{site.data.keyword.cloud_notm}} account is ready for cluster creation. For setup steps, see [Preparing your account to create clusters](/docs/openshift?topic=openshift-clusters).

You must be logged in to IBM Cloud before you create a cluster. If you don't have an account yet, you can [create one](https://cloud.ibm.com/registration){: external}.

### Pricing considerations
{: #getting-started-pricing}

Pricing varies based on worker node flavor, number of nodes, and infrastructure type. For more information, see [Red Hat OpenShift on IBM Cloud pricing](https://cloud.ibm.com/containers/cluster-management/catalog/about?platformType=openshift#pricing){: external}.

## Choose your infrastructure type
{: #getting-started-infra}

Before you create a cluster, choose the infrastructure type that fits your environment.

[VPC]{: tag-vpc}
:   Worker nodes are provisioned as virtual server instances on VPC infrastructure. VPC is the recommended infrastructure type for new clusters. It provides network isolation by default and supports the latest {{site.data.keyword.openshiftlong_notm}} features, including dedicated hosts and secure by default.

[Classic]{: tag-classic-inf}
:   Worker nodes are provisioned on virtual or bare metal machines on IBM Cloud classic infrastructure. Use Classic if you require bare metal worker nodes, software-defined storage (SDS) flavors, or connections to existing classic infrastructure resources.

[{{site.data.keyword.satelliteshort}}]{: tag-satellite}
:   Worker nodes are provisioned on your own infrastructure, including on-premises hardware or virtual machines in other cloud providers such as AWS, Azure, and GCP. Use {{site.data.keyword.satelliteshort}} when you need to run {{site.data.keyword.cloud_notm}}-managed clusters outside of IBM Cloud data centers.

For a detailed comparison including worker node options and availability, see [Cluster environment strategy](/docs/openshift?topic=openshift-strategy).

## Create a cluster
{: #getting-started-create}

Review your deployment options in the following table.

| Type | Level | Time | Description |
| --- | --- | --- | --- | 
| Quickstart | Beginner | 30 minutes | Create a pre-configured OpenShift Virtualization Service cluster with virtual machine capabilities ready to use. For more information, see [Quickstart: Creating a Virtualization Service cluster](/docs/openshift?topic=openshift-rovs-getting-started). |
| Tutorial | Beginner | 30 minutes | Create a small, 2-node cluster to begin testing {{site.data.keyword.openshiftlong_notm}}. For more information, see [Creating a 2-node VPC cluster by using Schematics](/docs/openshift?topic=openshift-tutorial-two-node). |
| Tutorial | Beginner | 45 minutes | Follow the steps in this tutorial to create your first cluster by using the IBM Cloud CLI. This tutorial uses Classic infrastructure. For more information, see [Creating a classic cluster from the CLI](/docs/openshift?topic=openshift-openshift_tutorial). |
| Tutorial| Beginner | 1 hour | Follow the steps in this tutorial to create your own Virtual Private Cloud (VPC), then create an {{site.data.keyword.openshiftlong_notm}} cluster by using the CLI. For more information, see [Create a cluster in your own Virtual Private Cloud](/docs/openshift?topic=openshift-vpc_rh_tutorial). |
| Deployable architecture: Quickstart variation | Beginner | 1 hour | This deployable architecture creates one VPC cluster with two worker nodes and a public endpoint. Note that the Quickstart variation is not highly available or validated for the IBM Cloud Framework for Financial Services. For more information, see [{{site.data.keyword.openshiftlong_notm}} on VPC landing zone](https://cloud.ibm.com/catalog?search=openshift%20label%3Areference_architecture#search_results){: explore} |
| Deployable architecture: Standard variation | Intermediate | 1-3 hours | This deployable architecture is based on the IBM Cloud for Financial Services reference architecture. The architecture creates secure and compliant clusters on a Virtual Private Cloud (VPC) network. For more information, see [{{site.data.keyword.openshiftlong_notm}} on VPC landing zone](https://cloud.ibm.com/catalog?search=openshift%20label%3Areference_architecture#search_results){: explore}. |
| Deployable architecture: Community Registry | Intermediate | 1-4 hours | There are more deployable architectures available in the Community Registry. Review the options to see if they fit your use case. For more information, see [Catalog](https://cloud.ibm.com/catalog#reference_architecture){: external} and select **Community Registry** from the drop-down menu. |
| Deployable architecture: OpenShift AI on {{site.data.keyword.IBM}} | Intermediate | 1-2 hours | This deployable architecture creates a new OpenShift cluster that runs GPU worker nodes and includes the Red Hat OpenShift AI operator. For more information, see [OpenShift AI on IBM Cloud](https://cloud.ibm.com/catalog/7a4d68b4-cf8b-40cd-a3d1-f49aff526eb3/architecture/roks-rhoai-c24ae512-8b25-43d7-8fb3-4173c7e94472-global){: external} in the Catalog. | 
| Custom deployment | Intermediate | 1-3 hours | [Create a custom cluster on Classic infrastructure](/docs/openshift?topic=openshift-cluster-create-classic). |
| Custom deployment | Intermediate | 1-3 hours | [Create a custom cluster on VPC infrastructure](/docs/openshift?topic=openshift-cluster-create-vpc-gen2). |
{: caption="Options for creating a cluster" caption-side="bottom"}

Already have a cluster? **[Learn how to access it](/docs/openshift?topic=openshift-access_cluster)** and continue to the next step to deploy a sample app.




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





## Quick actions
{: #getting-started-quick-actions}

If you already have a cluster, use these links to continue:

Access your cluster
:   Connect to your cluster and run kubectl commands. For more information, see [Accessing clusters](/docs/openshift?topic=openshift-access_cluster).

Install the CLI
:   Set up your local development environment. For more information, see [Installing the CLI](/docs/openshift?topic=openshift-cli-install).

Deploy your first app
:   Get hands-on with a sample application. For more information, see [Deploying apps](/docs/openshift?topic=openshift-app).

Need to check pricing first? [View Red Hat OpenShift on IBM Cloud pricing](https://cloud.ibm.com/containers/cluster-management/catalog/about?platformType=openshift#pricing){: external}.

## What's next?
{: #getting-started-whats-next}

Continue with one of these curated learning paths:
- [Learning path for administrators](/docs/openshift?topic=openshift-learning-path-admin).
- [Learning path for developers](/docs/openshift?topic=openshift-learning-path-dev).
