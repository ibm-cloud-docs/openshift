---
copyright:
  years: 2021, 2021
lastupdated: "2021-08-13"

keywords: openshift, terraform, create, cluster, iam, access

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}
  

# Assigning cluster access by using Terraform for {{site.data.keyword.openshiftlong_notm}}
{: #terraform-setup}

Terraform on {{site.data.keyword.cloud}} enables predictable and consistent provisioning of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multi-tier cloud environments following Infrastructure as Code (IaC) principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API and SDKs, you can automate the provisioning, update, and deletion of your {{site.data.keyword.openshiftlong_notm}} resources by using HashiCorp Configuration Language (HCL).
{: shortdesc}

Looking for a managed Terraform on {{site.data.keyword.cloud}} solution? Try out [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started). With {{site.data.keyword.bpshort}}, you can use the Terraform scripting language that you are familiar with, but you don't have to worry about setting up and maintaining the Terraform command line or the {{site.data.keyword.cloud}} Provider plug-in. {{site.data.keyword.bpshort}} also provides pre-defined Terraform templates that you can easily install from the {{site.data.keyword.cloud}} catalog.
{: tip}

## Creating a {{site.data.keyword.openshiftshort}} cluster by using Terraform
{: #terraform-cluster-create}

Before you can assign cluster access by using Terraform, follow the steps to create a {{site.data.keyword.openshiftshort}} cluster using Terraform. If you already have a cluster, see [Assigning IAM user access](#terraform-cluster-IAM).
{: shortdesc}

Before you begin, make sure that you have the [required access](/docs/openshift?topic=openshift-access_reference) to create and work with {{site.data.keyword.openshiftlong_notm}} resources. 

1. Follow the [Terraform on {{site.data.keyword.cloud}} getting started tutorial](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started) to install the Terraform CLI and configure the {{site.data.keyword.cloud}} Provider plug-in for Terraform. The plug-in abstracts the {{site.data.keyword.cloud}} APIs that are used to provision, update, or delete {{site.data.keyword.openshiftshort}} service instances and resources. 

2. Follow the tutorial to [create single and multi-zone clusters with Terraform](docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-tutorial-tf-clusters#create-cluster).

3. **Optional**: [Use Terraform to configure IAM user access policies for your {{site.data.keyword.openshiftshort}} cluster](#terraform-cluster-IAM).

## Assigning IAM user access to {{site.data.keyword.openshiftshort}} clusters
{: #terraform-cluster-IAM }

You can use Terraform to assign IAM user access for {{site.data.keyword.openshiftshort}} clusters in an {{site.data.keyword.cloud_notm}} account. For more information on using Terraform with IAM policies, see [the IBM Cloud provider Terraform documentation](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs){: external}.
{: shortdesc}

1. In your Terraform directory, create a configuration file that is named `iam.tf`. In your `iam.tf` file, add the configuration parameters to create an IAM user access policy for a {{site.data.keyword.openshiftshort}} cluster by using the HashiCorp Configuration Language (HCL). The following example configuration contains two blocks. The first block is the `data source` block that specifies the cluster where you want to create an access policy. The second block is the `resource` block that contains the specifications for the IAM access policy that you want to create. For more information, see the [Terraform documentation](https://www.terraform.io/docs/language/index.html){: external}.

    ```
    data "ibm_container_cluster" "cluster" {
    cluster_name_id = "<cluster_name>"
    }

    resource "ibm_iam_user_policy" "cluster" {
    ibm_id = "<ibm_id>"
    roles  = ["<access_role_1>, <access_role_2>"]

    resources {
        service = "containers-kubernetes"
        resource_instance_id  = data.ibm_container_cluster.cluster.name
    }
    }
    ```
    {: codeblock}

    | Data source | Description |
    |---|---|
    | `cluster_name_id` | The name of the cluster that you want to create an IAM access policy for.  |
    {: caption="Configuring IAM access policies with Terraform" caption-side="top"}
    {: summary="The rows are read from left to right. The first column is the data source block parameter. The second column is a brief description of the parameter."}


    | Resource | Description |
    |---|---|
    | `ibm_id` | The IBM Cloud ID or email of the address of the user that you want to create the IAM access policy for. | 
    | `roles` | A comma-separated list of the access roles that you want to assign the user.  |
    | `service` | The type of service that the access policy applies to. Enter `"openshift"` for {{site.data.keyword.openshiftshort}} clusters. For a complete list of applicable service types, run `ibmcloud oc catalog service-marketplace`. |
    | `resource_instance_id` | The ID or name of the cluster. Enter `data.ibm_container_cluster.cluster.id` to automatically reference the ID of the cluster that you specified in the `data source` block. |
    {: caption="Configuring IAM access policies with Terraform" caption-side="top"}
    {: summary="The rows are read from left to right. The first column is the resource source block parameter. The second column is a brief description of the parameter."}

    **Example configuration file**:

    ```
    data "ibm_container_cluster" "cluster" {
        cluster_name_id = "tfcluster"
    }

    resource "ibm_iam_user_policy" "test_policy" {
        ibm_id = "ibm_id@ibm.com"
        roles  = ["Viewer", "Editor", "Administrator"]

        resources {
            service = "containers-kubernetes"
            resource_instance_id  = data.ibm_container_cluster.cluster.name
        }
    }
    ```
    {: codeblock}

1. Initialize the Terraform CLI. 

    ```sh
    terraform init
    ```
    {: pre}

1. Create a Terraform execution plan and review the output. The Terraform execution plan summarizes all of the actions that run to create the {{site.data.keyword.openshiftshort}} cluster in your account. Note the `Plan` section of the output. The example output states `Plan: 1 to add, 0 to change, 0 to destroy` because the configuration file creates one IAM user access policy.

    ```
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
    ibmcloud oc terraform apply
    ```
    {: pre}

    **Example output**:

    ```
    ibm_iam_user_policy.test_policy: Creating...
    ibm_iam_user_policy.test_policy: Creation complete after 2s [id=ibm_id@ibm.com/f81b161f-e1db-4084-8b28-cfcbe88fec72]
    ```
    {: screen}

1. Verify that the IAM access policy was successfully created by running the command and searching for the policy ID you previously noted.

    ```sh
    ibmcloud oc iam user-policies ibm_id@ibm.com
    ```
    {: pre}

    **Example output**:

    ```
    Policy ID:   f81b161f-e1db-4084-8b28-cfcbe88fec72   
    Roles:       Viewer, Editor, Administrator   
    Resources:                        
                Service Name   containers-kubernetes    
    ```
    {: screen} 



