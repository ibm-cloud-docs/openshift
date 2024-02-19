---

copyright:
  years: 2023, 2024
lastupdated: "2024-02-19"


keywords: openshift, kubernetes cluster, red hat openshift, openshift container platform, red hat, create openshift cluster, vpc cluster, classic cluster, clusters

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}



# Getting started with {{site.data.keyword.openshiftlong_notm}}
{: #getting-started}

{{site.data.keyword.openshiftlong_notm}} is a managed offering to create your own cluster of compute hosts where you can deploy and manage containerized apps on IBM Cloud. Combined with an intuitive user experience, built-in security and isolation, and advanced tools to secure, manage, and monitor your cluster workloads, you can rapidly deliver highly available and secure containerized apps in the public cloud.
{: shortdesc}

Complete the following steps to get familiar with the basics, understand the service components, create your first cluster, and deploy a starter app.

## Review the basics
{: #getting-started-basics}
{: step}

- Get an overview of the service by reviewing the concepts and terms, and benefits. For more information, see [Understanding {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-overview).

- [Review the FAQs](/docs/openshift?topic=openshift-faqs)

Already familiar with containers and {{site.data.keyword.openshiftlong_notm}}? Continue to the next step to prepare your account for creating clusters.

## Prepare your account
{: #getting-started-prepare-account}
{: step}

To set up your {{site.data.keyword.cloud_notm}} account so that you can create clusters, see [Preparing your account to create clusters](/docs/openshift?topic=openshift-clusters).

If you've already prepared your account and you're ready to create a cluster, continue to the next step.


## Create a cluster
{: #getting-started-create}
{: step}

Follow a tutorial, or set up your own custom cluster environment. Review the following table for your deployment options.


| Type | Level | Time | Deployment method | Description |
| --- | --- | --- | --- | --- |
| [Tutorial]{: tag-green} | Beginner | 30 minutes | Automated via IBM Cloud Schematics | [Creating a 2 node VPC cluster by using Schematics](/docs/openshift?topic=openshift-tutorial-two-node). | 
| [Tutorial]{: tag-green} | Beginner | 45 minutes | CLI | [Creating a classic cluster from the CLI](/docs/openshift?topic=openshift-openshift_tutorial). |
| [Tutorial]{: tag-green} | Beginner | 60 minutes | CLI | [Create a cluster in your own Virtual Private Cloud](/docs/openshift?topic=openshift-vpc_rh_tutorial). | 
| [Custom deployment]{: tag-warm-gray} | Intermediate | UI, CLI, or Terraform | 1-3 hours | [Create a custom cluster on Classic infrastructure](/docs/openshift?topic=openshift-cluster-create-classic). |
| [Custom deployment]{: tag-warm-gray} | Intermediate | UI, CLI, or Terraform | 1-3 hours | [Create a custom cluster on VPC infrastructure](/docs/openshift?topic=openshift-cluster-create-vpc-gen2). |
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


