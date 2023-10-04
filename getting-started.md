---

copyright:
  years: 2023, 2023
lastupdated: "2023-10-04"

keywords: openshift, kubernetes cluster, red hat openshift, openshift container platform, red hat, create openshift cluster, vpc cluster, classic cluster, clusters

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}



# Getting started with {{site.data.keyword.openshiftlong_notm}}
{: #getting-started}

With {{site.data.keyword.openshiftlong_notm}}, you can deploy apps on highly available clusters.
{: shortdesc}

## Review the basics
{: #getting-started-basics}
{: step}

- Get an overview of the service by reviewing the concepts and terms, and benefits. For moe information, see [Understanding {{site.data.keyword.openshiftlong_notm}}](docs/openshift?topic=openshift-overview).

[Review the FAQs](docs/openshift?topic=openshift-overview)

Already familiar with containers and {{site.data.keyword.openshiftlong_notm}}? Continue to the next step to prepare your account for creating clusters.

## Prepare your account
{: getting-started-prepare-account}
{: step}

To set up your {{site.data.keyword.cloud_notm}} account so that you can create clusters, see [Preparing your account to create clusters](/docs/containers?topic=containers-clusters).

If you've already prepared your account and you're ready to create a cluster, continue to the next step.


## Create a cluster
{: getting-started-create}
{: step}

Follow a tutorial, or set up your own custom cluster environment.


- [Tutorial]{: tag-blue} [Create a classic cluster from the CLI](/docs/openshift?topic=openshift-openshift_tutorial).
- [Tutorial]{: tag-blue} [Create a cluster in your own Virtual Private Cloud](/docs/openshift?topic=openshift-vpc_rh_tutorial).
- [Create a custom cluster on Classic infrastructure](/docs/openshift?topic=openshift-cluster-create-classic).
- [Create a custom cluster on VPC infrastructure](/docs/openshift?topic=openshift-cluster-create-vpc).




Already have a cluster? Continue to the next step to deploy an app!




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
- [Learning path for administrators](/docs/containers?topic=containers-learning-path-admin).
- [Learning path for developers](/docs/containers?topic=containers-learning-path-dev).


