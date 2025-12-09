---

copyright: 
  years: 2025, 2025
lastupdated: "2025-12-09"


keywords: deployable architecture, DA

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Creating clusters with deployable architectures
{: #roks_da}

Creating a secure, compliant, and tailored {{site.data.keyword.openshiftlong}} cluster is often challenging and requires expertise. However, with careful planning and appropriate resources, it is feasible to automate most aspects of the deployment process. IBM Cloud provides you with well-architected patterns called deployable architectures (DA) that can help you set up your environment. 
{: shortdesc}

There are three different DAs that create a cluster or clusters for you. They are:

- [Red Hat OpenShift Container Platform on VPC Landing Zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-slz-ocp-95fccffc-ae3b-42df-b6d9-80be5914d852-global){: external} - This DA creates a {{site.data.keyword.openshiftlong}} cluster environment that adheres to the IBM Financial Services Cloud reference architecture. The [Terraform IBM Modules](https://github.com/terraform-ibm-modules/terraform-ibm-base-ocp-vpc?tab=readme-ov-file#red-hat-openshift-vpc-cluster-on-ibm-cloud-module) repository provides related infrastructure code and examples you may find useful.

- [OpenShift AI on IBM Cloud](https://cloud.ibm.com/catalog/7a4d68b4-cf8b-40cd-a3d1-f49aff526eb3/architecture/roks-rhoai-c24ae512-8b25-43d7-8fb3-4173c7e94472-global){: external} - This Community Registry DA will create a cluster for you with GPU-based worker nodes and install the Red Hat OpenShift AI operator and all its dependents. For guidance on Terraform usage refer [Terraform IBM Modules](https://github.com/terraform-ibm-modules/terraform-ibm-ocp-ai?tab=readme-ov-file#red-hat-openshift-ai-on-ibm-cloud).

- [Red Hat OpenShift on IBM Cloud Starters](https://cloud.ibm.com/catalog/7a4d68b4-cf8b-40cd-a3d1-f49aff526eb3/architecture/roks-tryit-137000f7-e552-464f-866c-a1b5a3bc8d56-global){: external} - This Community Registry DA will create a simple cluster for your with or without integrated logging and monitoring.


## Checking your permissions
{: #roks_da_permissions}

Each DA has a set of permissions that the user must have to be successful in executing the DA. A DA cannot only create the cluster for you, but can also create other complementary services that the cluster can use or integrate with. When executing the DA, a permissions check will be done to ensure you have the necessary permissions to create the resources in the DA. See [IAM roles and actions](/docs/openshift?topic=openshift-iam-platform-access-roles) for details on the specific permission needed by related services.

## Creating an API key
{: #roks_da_api_key}

To authenticate yourself with the DA, an IBM Cloud API Key is required. After you have all the necessary permissions, [create an API key](/docs/account?topic=account-userapikey&interface=ui#create_user_key) and save it for use when executing the DA.

## Creating the DA
{: #roks_da_creation}

When you are ready to create a cluster using a DA, click the appropriate DA tile in the catalog. If the DA has different variations, choose the variation that meets your needs. For each variation you should see an architecture diagram that shows what the DA will create.

To begin, click **Add to Project** in the lower right hand corner. Projects are a way to execute DAs and collect the resources created by the DAs. Give your project a name. The configuration name is actually the name of the IBM Cloud Schematics workspace, where the DA terraform will execute. Select the region where you want the Schematics workspace to be created. After providing all the information, click **Create**.

When you open the project, you will see the DA schematics name and version that you previously selected in the **Define Details** section. In the **Configure** section, there are three tabs:

- Security - Enter the API key you created above in the **`api_key`** text box.
- Required - Enter all required variables on the **Required** tab.
- Optional - Enter all optional variables on the **Optional** tab.

After you specify all the variables, click **Save** and then click **Validate**.

The DA will now begin to execute in the Schematics workspace. The first phase is a validation phase. For some DAs, you can skip the results of the validation. The OpenShift AI and Starters DA are focused on getting you a cluster quickly. For the VPC Landing Zone DA you should pay attention to the validation errors if any are shown.

To continue, either fix your validation concerns by clicking **Edit Configuration** or override the validation by providing a comment and clicking **Override and Approve**. Then click **Deploy** to execute the DA terraform. 

After the DA has finished provisioning, you can see your cluster in the [IBM Cloud console](https://cloud.ibm.com/){: external}.
