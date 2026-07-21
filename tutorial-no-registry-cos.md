---

copyright:
  years: 2026
lastupdated: "2026-07-21"

keywords: openshift, roks, no cos, no registry, emptydir, image registry, internal registry, icr, fs cloud, financial services

subcollection: openshift

content-type: tutorial
services: openshift, vpc
account-plan: paid
completion-time: 30m

---

{{site.data.keyword.attribute-definition-list}}

# Creating a VPC cluster without an Object Storage bucket
{: #tutorial-no-registry-cos}
{: toc-content-type="tutorial"}
{: toc-services="openshift, vpc"}
{: toc-completion-time="30m"}

[Virtual Private Cloud]{: tag-vpc}



Create an {{site.data.keyword.openshiftlong_notm}} cluster on VPC without a {{site.data.keyword.cos_full_notm}} bucket backing the internal image registry. For environments that must meet [IBM Financial Services Cloud](https://cloud.ibm.com/docs/financial-services-validated-partners?topic=financial-services-validated-partners-about){: external} requirements, you can create the cluster without a {{site.data.keyword.cos_full_notm}} instance and pull container images directly from {{site.data.keyword.registrylong_notm}}. When no {{site.data.keyword.cos_full_notm}} instance is provided at cluster creation, the internal registry uses ephemeral `emptyDir` storage, which ensures the cluster operates consistently with FS Cloud standards that rely on centralized image management rather than the internal registry.
{: shortdesc}

## Audience
{: #tutorial-no-registry-cos-audience}

This tutorial is for cluster administrators who are creating an {{site.data.keyword.openshiftlong_notm}} cluster on VPC infrastructure in environments that must meet IBM Financial Services Cloud requirements. It is intended for teams that need to use {{site.data.keyword.registrylong_notm}} as the primary image registry instead of the cluster-internal registry.
{: shortdesc}

## Objectives
{: #tutorial-no-registry-cos-objectives}

In this tutorial, you create an {{site.data.keyword.openshiftlong_notm}} VPC cluster without configuring a {{site.data.keyword.cos_full_notm}} instance, consistent with IBM Financial Services Cloud standards. The cluster's internal image registry uses ephemeral `emptyDir` storage, and images are managed centrally through {{site.data.keyword.registrylong_notm}}.

## What you'll get
{: #tutorial-no-registry-cos-get}

In this tutorial, you create the following resources. There are optional steps to delete these resources if you do not want to keep them after completing the tutorial.

- An {{site.data.keyword.openshiftlong_notm}} cluster on VPC without a COS-backed internal registry
- Cluster access configured for administrative use

## Before you begin
{: #tutorial-no-registry-cos-prereqs}

Complete the following prerequisite steps before you create your cluster.
{: shortdesc}

Permissions
:   If you are the account owner, you already have the required permissions to create a cluster and can continue to the next step. Otherwise, ask the account owner to [set up the API key and assign you the minimum user permissions in {{site.data.keyword.cloud_notm}} IAM](/docs/openshift?topic=openshift-iam-platform-access-roles).

Command-line tools
:   Set up your local command-line environment by completing the following steps.
    1. [Install the {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`)](/docs/cli?topic=cli-getting-started).
    2. Install the {{site.data.keyword.openshiftlong_notm}} plug-in.
        ```sh
        ibmcloud plugin install kubernetes-service
        ```
        {: pre}

    3. Install the {{site.data.keyword.redhat_openshift_notm}} CLI (`oc`). For instructions, see [Installing the OpenShift CLI](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/cli_tools/openshift-cli-oc#installing-openshift-cli){: external}.

VPC infrastructure
:   Before you create your cluster, you must have an existing VPC and subnet. To create them, see [Creating a VPC and subnet](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console).

## Create the cluster
{: #tutorial-no-registry-cos-create}
{: step}

Create an {{site.data.keyword.openshiftlong_notm}} cluster on VPC without providing a {{site.data.keyword.cos_full_notm}} instance. When no COS instance is specified, the internal image registry is backed by `emptyDir` storage.
{: shortdesc}

When you omit the `--cos-instance` option from the cluster creation command, the internal registry uses `emptyDir` storage instead of {{site.data.keyword.cos_full_notm}}. `emptyDir` storage is ephemeral — data stored in the registry is lost when the image-registry pod restarts or is rescheduled. This setup is not suitable for production use cases that rely on the internal registry. If you need a persistent internal registry in the future, you can configure a {{site.data.keyword.cos_full_notm}} bucket after cluster creation. For more information, see [Backing up your internal image registry to {{site.data.keyword.cos_full_notm}}](/docs/openshift?topic=openshift-registry#cos_image_registry).
{: important}

1. Log in to the {{site.data.keyword.cloud_notm}} account, resource group, and region where you want to create your cluster. If you have a federated ID, include the `--sso` option.
    ```sh
    ibmcloud login -r <region> [-g <resource_group>] [--sso]
    ```
    {: pre}

2. Create the cluster. Replace the placeholder values with your own cluster name, zone, {{site.data.keyword.redhat_openshift_notm}} version, worker node flavor, VPC ID, and subnet ID.
    ```sh
    ibmcloud oc cluster create vpc-gen2 \
      --name <cluster-name> \
      --zone <zone> \
      --version <openshift-version> \
      --flavor <worker-flavor> \
      --workers <number-of-workers> \
      --vpc-id <vpc-id> \
      --subnet-id <subnet-id>
    ```
    {: pre}

    Notice that the command does not include the `--cos-instance` option. Omitting this option is what configures the internal registry to use `emptyDir` storage.
    {: tip}

3. Wait for the cluster to finish provisioning. This process might take 20 - 30 minutes. Monitor the cluster state by running the following command until the **State** field shows `normal`.
    ```sh
    ibmcloud oc cluster get --cluster <cluster-name>
    ```
    {: pre}

## Configure cluster access
{: #tutorial-no-registry-cos-access}
{: step}

After your cluster is running, download the cluster configuration to set up `oc` CLI access.
{: shortdesc}

1. Download the cluster configuration file and set the `KUBECONFIG` environment variable.
    ```sh
    ibmcloud oc cluster config --cluster <cluster-name> --admin
    ```
    {: pre}

2. Verify that you can connect to the cluster.
    ```sh
    oc get nodes
    ```
    {: pre}

    All nodes should show a **STATUS** of `Ready`.

## Verify the image registry configuration
{: #tutorial-no-registry-cos-verify}
{: step}

Confirm that the internal image registry is using `emptyDir` storage as expected.
{: shortdesc}

1. Check the image registry deployment status.
    ```sh
    oc get deployment -n openshift-image-registry
    ```
    {: pre}

2. Confirm the storage type in the image registry configuration. In the output, the `storage` field should show `emptyDir: {}`.
    ```sh
    oc get configs.imageregistry.operator.openshift.io cluster -o yaml
    ```
    {: pre}

## What's next?
{: #tutorial-no-registry-cos-next}

Your cluster is now running with an `emptyDir`-backed internal registry. You can push and pull images by using {{site.data.keyword.registrylong_notm}}.
{: shortdesc}

- [Push images to {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-registry#push-images) and pull them directly into your cluster workloads.
- [Configure an image pull secret](/docs/openshift?topic=openshift-registry#other_registry_accounts) so that your pods can pull images from {{site.data.keyword.registrylong_notm}}.
- [Set up IBM Cloud monitoring](/docs/openshift?topic=openshift-health-monitor) to observe your cluster.
- If you want to add persistent internal registry storage later, see [Backing up your internal image registry to {{site.data.keyword.cos_full_notm}}](/docs/openshift?topic=openshift-registry#cos_image_registry).
- If you see an `E7278` error during cluster creation, see [Why do I get an error about a cloud object storage bucket when I create a cluster?](/docs/openshift?topic=openshift-ts_cos_bucket_cluster_create). If the steps there do not resolve the issue, [contact {{site.data.keyword.cloud_notm}} support](/docs/get-support?topic=get-support-using-avatar).
