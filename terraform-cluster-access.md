---

copyright: 
  years: 2023, 2024
lastupdated: "2024-01-03"


keywords: openshift, terraform, create, cluster, access

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Assigning cluster access by using Terraform for {{site.data.keyword.openshiftlong_notm}}
{: #terraform-setup}

Terraform on {{site.data.keyword.cloud}} enables predictable and consistent provisioning of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multitiered cloud environments following Infrastructure as Code (IaC) principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API and SDKs, you can automate the provisioning, update, and deletion of your {{site.data.keyword.openshiftlong_notm}} resources by using HashiCorp Configuration Language (HCL).
{: shortdesc}

Looking for a managed Terraform on {{site.data.keyword.cloud}} solution? Try out [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started). With {{site.data.keyword.bpshort}}, you can use the Terraform scripting language that you are familiar with, but you don't have to worry about setting up and maintaining the Terraform command line or the {{site.data.keyword.cloud}} Provider plug-in. {{site.data.keyword.bpshort}} also provides pre-defined Terraform templates that you can easily install from the {{site.data.keyword.cloud}} catalog.
{: tip}

## Creating a {{site.data.keyword.redhat_openshift_notm}} cluster by using Terraform
{: #terraform-cluster-create}

Before you can assign cluster access by using Terraform, follow the steps to create a {{site.data.keyword.redhat_openshift_notm}} cluster using Terraform. If you already have a cluster, see [Assigning IAM user access](#terraform-cluster-IAM).
{: shortdesc}

Before you begin, make sure that you have the [required access](/docs/openshift?topic=openshift-access_reference) to create and work with {{site.data.keyword.openshiftlong_notm}} resources. 

1. Follow the [Terraform on {{site.data.keyword.cloud}} getting started tutorial](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started) to install the Terraform CLI and configure the {{site.data.keyword.cloud}} Provider plug-in for Terraform. The plug-in abstracts the {{site.data.keyword.cloud}} APIs that are used to provision, update, or delete {{site.data.keyword.redhat_openshift_notm}} service instances and resources. 

2. Follow the tutorial to [create single and multi-zone clusters with Terraform](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-tutorial-tf-clusters#create-cluster).

3. **Optional**: [Use Terraform to configure IAM user access policies for your {{site.data.keyword.redhat_openshift_notm}} cluster](#terraform-cluster-IAM).

## Assigning IAM user access to {{site.data.keyword.redhat_openshift_notm}} clusters
{: #terraform-cluster-IAM}

You can use Terraform to assign IAM user access for {{site.data.keyword.redhat_openshift_notm}} clusters in an {{site.data.keyword.cloud_notm}} account. For more information on using Terraform with IAM policies, see [the IBM Cloud provider Terraform documentation](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs){: external}.
{: shortdesc}

1. In your Terraform directory, create a configuration file that is named `iam.tf`. In your `iam.tf` file, add the configuration parameters to create an IAM user access policy for a {{site.data.keyword.redhat_openshift_notm}} cluster by using the HashiCorp Configuration Language (HCL). The following example configuration creates the `ibm_iam_user_policy` and then assigns the policy to a specified cluster.  For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

    ```terraform
    resource "ibm_iam_user_policy" "cluster" {
    ibm_id = "<ibm_id>"
    roles  = ["<access_role_1>, <access_role_2>"]

    resources {
        service = "containers-kubernetes"
        resource_instance_id  = "<cluster_name>"
    }
    }
    ```
    {: codeblock}

    | Resource | Description |
    |---|---|
    | `ibm_id` | The IBM Cloud ID or email address of the user that you want to create the IAM access policy for. | 
    | `roles` | A comma-separated list of the access roles that you want to assign the user.  |
    | `service` | The type of service that the access policy applies to. Enter `"openshift"` for {{site.data.keyword.redhat_openshift_notm}} clusters. For a complete list of applicable service types, run `ibmcloud oc catalog service-marketplace`. |
    | `resource_instance_id` | The ID or name of the cluster. |
    {: caption="Configuring IAM access policies with Terraform" caption-side="bottom"}

    **Example configuration file**:

    ```terraform
    resource "ibm_iam_user_policy" "test_policy" {
        ibm_id = "ibm_id@ibm.com"
        roles  = ["Viewer", "Editor", "Administrator"]

        resources {
            service = "containers-kubernetes"
            resource_instance_id  = "my-cluster"
        }
    }
    ```
    {: codeblock}

1. Initialize the Terraform CLI. 

    ```sh
    terraform init
    ```
    {: pre}

1. Create a Terraform execution plan and review the output. The Terraform execution plan summarizes all the actions that run to create the {{site.data.keyword.redhat_openshift_notm}} cluster in your account. Note the `Plan` section of the output. The example output states `Plan: 1 to add, 0 to change, 0 to destroy` because the configuration file creates one IAM user access policy.

    ```terraform
    Terraform used the selected providers to generate the following execution plan. Resource actions are
    indicated with the following symbols:
    + create

    Terraform will perform the following actions:

    # ibm_iam_user_policy.test_policy will be created
    + resource "ibm_iam_user_policy" "test_policy" {
        + account_management = false
        + ibm_id             = "ibm_id@ibm.com"
        + id                 = (known after apply)
        + roles              = [
            + "Viewer",
            + "Editor",
            + "Administrator",
            ]

        + resources {
            + service = "containers-kubernetes"
            }
        }

    Plan: 1 to add, 0 to change, 0 to destroy.
    ```
    {: screen}

1. Apply the configuration file to create the access policy. It may take a few seconds to complete. In the output, note the policy ID number after the user's IBM email.

    ```sh
    terraform apply
    ```
    {: pre}

    Example output:

    ```sh
    ibm_iam_user_policy.test_policy: Creating...
    ibm_iam_user_policy.test_policy: Creation complete after 2s [id=ibm_id@ibm.com/f81b161f-e1db-4084-8b28-cfcbe88fec72]
    ```
    {: screen}

1. Verify that the IAM access policy was successfully created by running the command and searching for the policy ID you previously noted.

    ```sh
    ibmcloud iam user-policies ibm_id@ibm.com
    ```
    {: pre}

    Example output:

    ```sh
    Policy ID:   f81b161f-e1db-4084-8b28-cfcbe88fec72   
    Roles:       Viewer, Editor, Administrator   
    Resources:                        
                Service Name       containers-kubernetes   
                Service Instance   my-cluster
    ```
    {: screen} 
    





