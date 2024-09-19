---

copyright:
  years: 2024, 2024
lastupdated: "2024-09-19"


keywords: kubernetes

subcollection: openshift

content-type: tutorial
services: openshift, vpc, schematics
account-plan: paid
completion-time: 30m

---

{{site.data.keyword.attribute-definition-list}}

# Creating a 2 node OpenShift cluster on VPC infrastructure by using Schematics
{: #tutorial-two-node}
{: toc-content-type="tutorial"}
{: toc-services="openshift, vpc, schematics"}
{: toc-completion-time="30m"}

Create an {{site.data.keyword.openshiftlong_notm}} cluster in a Virtual Private Cloud (VPC) by using Schematics.
{: shortdesc}

## Audience
{: #basic-audience}

This tutorial is designed for account administrators who want to learn about {{site.data.keyword.openshiftlong_notm}} and Schematics.

Alternatively, you can use this tutorial to set up a small testing environment for administrators who are already familiar with OpenShift, VPC, and Schematics.

To complete this tutorial, you must have the at least the following permissions in IAM. For more information, see [IAM roles and actions](/docs/account?topic=account-iam-service-roles-actions).

- **Administrator** or **Compliance Management** for IBM Cloud Kubernetes Service.
- **Administrator** or **Editor** for VPC.
- **Manager** for Schematics.
- **Manager** for Cloud Object Storage.

## What you'll get
{: #basic-what-you-get}

In this tutorial, you create the following resources. There are optional steps to delete these resources if you do not want to keep them after completing the tutorial. 

- 1 Virtual Private Cloud (VPC)
- 1 Subnet
- 1 Public gateway
- 1 Cloud Object Storage (COS) bucket
- 1 OpenShift cluster with 2 worker nodes in the same zone.

## Create a Schematics workspaces
{: #basic-create-workspace}
{: step}

1. Navigate to the [Schematics console](https://cloud.ibm.com/schematics/workspaces){: external}.
1. Click **Create workspace**.
1. In the **GitHub, GitLab or Bitbucket repository URL** field, enter the following URL.
    ```txt
    https://github.com/IBM-Cloud/kube-samples/tree/master/ez-ibm-openshift-vpc
    ```
    {: codeblock}

1. Uncheck the **Use Full Repository** box.
1. Make sure the **Branch**, **Folder**, and **Personal Access Token** fields are empty.
1. Use the default Terraform version and click **Next**.
1. In the **Workplace Details** section, give your workspace a name and fill out the remaining fields as desired.
1. Click **Next**, then review the information you entered. 
1. Click **Create**, then wait a few minutes while the Schematics template populates.

## Generate, review, and apply the Schematics plan
{: #basic-generate-plan}
{: step}

1. Click **Generate plan** to create a Terraform execution plan. Generating a plan lets you review the resources that will be deployed in your account and the associated cost estimate.
1. After reviewing the plan details and the cost estimate, click **Apply plan**.
1. Wait a few minutes while Schematics creates the resources in your account.


## Access your OpenShift cluster
{: #basic-access-cluster}
{: step}

1. Navigate to the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}.
1. Select your cluster. The cluster name is `ez-ibm-openshift-vpc-XXX`.
1. Click **OpenShift web console** to access your cluster. For more information, see [Connecting to the cluster from the console](/docs/openshift?topic=openshift-access_cluster&interface=cli#access_oc_console).


## Optional: Clean up the resources
{: #basic-cleanup}
{: step}

1. Navigate to your Schematics workspace.
1. From the **Actions** dropdown menu, click **Destroy resources**.
1. Wait a few minutes while Schematics deletes the resources from your account.
1. From the **Actions menu**, click **Delete workspace**.
