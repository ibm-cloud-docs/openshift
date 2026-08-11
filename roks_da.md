---

copyright:
  years: 2025, 2026
lastupdated: "2026-08-11"

keywords: openshift, deployable architecture

subcollection: openshift

content-type: howto

---

{{site.data.keyword.attribute-definition-list}}

# Creating clusters with deployable architectures
{: #roks_da}

IBM Cloud deployable architectures (DAs) are well-architected automation patterns that create a complete {{site.data.keyword.openshiftlong}} cluster environment for you, including networking, security, and optional integrations.
{: shortdesc}

The following three deployable architectures create a cluster or clusters for you.

- [Red Hat OpenShift Container Platform on VPC Landing Zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-slz-ocp-95fccffc-ae3b-42df-b6d9-80be5914d852-global){: external} — Creates a cluster environment that adheres to the IBM Financial Services Cloud reference architecture. For related infrastructure code, see the [Red Hat OpenShift VPC cluster on IBM Cloud](https://registry.terraform.io/modules/terraform-ibm-modules/base-ocp-vpc/ibm/latest){: external} Terraform module.

- [OpenShift AI on IBM Cloud](https://cloud.ibm.com/catalog/7a4d68b4-cf8b-40cd-a3d1-f49aff526eb3/architecture/roks-rhoai-c24ae512-8b25-43d7-8fb3-4173c7e94472-global){: external} — A Community Registry solution that creates a cluster with GPU-based worker nodes and installs the Red Hat OpenShift AI operator and its dependencies.

- [Red Hat OpenShift on IBM Cloud Starters](https://cloud.ibm.com/catalog/7a4d68b4-cf8b-40cd-a3d1-f49aff526eb3/architecture/roks-tryit-137000f7-e552-464f-866c-a1b5a3bc8d56-global){: external} — A Community Registry solution that creates a simple cluster with or without integrated logging and monitoring.

## Checking your permissions
{: #roks_da_permissions}

Each deployable architecture requires a specific set of IAM permissions. In addition to creating the cluster, a deployable architecture can also create complementary services that integrate with the cluster. A permissions check runs during deployment to verify that you have the necessary access. For details, see [IAM roles and actions](/docs/openshift?topic=openshift-iam-platform-access-roles).

## Creating an API key
{: #roks_da_api_key}

Deployable architectures authenticate using an IBM Cloud API key. After you confirm that you have the required permissions, [create an API key](/docs/iam?topic=iam-userapikey&interface=ui#create_user_key) and save it for use during deployment.

## Creating the deployable architecture
{: #roks_da_creation}

1. In the IBM Cloud catalog, click the deployable architecture tile that meets your needs. If the architecture has variations, review the architecture diagram for each variation before selecting one.

1. Click **Add to Project**. Give your project a name. The configuration name becomes the name of the IBM Cloud Schematics workspace where the Terraform runs. Select the region for the workspace, then click **Create**.

1. In the project, complete the three configuration tabs in the **Configure** section:
   - **Security** — Enter your API key in the **`api_key`** field.
   - **Required** — Complete all required variables.
   - **Optional** — Complete any optional variables.

1. Click **Save**, then click **Validate**. The validation phase runs first.
   - For the VPC Landing Zone deployable architecture, review and resolve any validation errors before proceeding.
   - For the OpenShift AI and Starters deployable architectures, you can override validation results if needed.

1. To continue, either click **Edit Configuration** to resolve validation issues, or provide a comment and click **Override and Approve**.

1. Click **Deploy** to run the Terraform.

After provisioning completes, your cluster appears in the [IBM Cloud console](https://cloud.ibm.com/){: external}.
