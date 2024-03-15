---

copyright: 
  years: 2014, 2024
lastupdated: "2024-03-15"

keywords: openshift, kubernetes, infrastructure, policy, users, permissions, access, roles

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# IAM roles and actions
{: #iam-platform-access-roles}

{{site.data.keyword.openshiftlong_notm}} is configured to use {{site.data.keyword.iamlong}} roles to determine the actions that users can perform on {{site.data.keyword.openshiftlong_notm}} clusters, worker nodes, and Ingress application load balancers (ALBs).
{: shortdesc}

Review the following table for a list of Platform and Service roles and their associated actions.

{{../account/iam-service-roles.md#containers-kubernetes-roles}}

For a list of all IBM services and roles, see [IAM roles and actions](/docs/account?topic=account-iam-service-roles-actions){: tip}

## Required permissions to create a cluster
{: #cluster-create-permissions}


| Service or resource group | Role | Scope | Required? |
| --- | --- | --- | --- |
| {{site.data.keyword.containershort}} | - **Administrator** platform access role  \n - **Writer** or **Manager** service access role | Yes | 
| {{site.data.keyword.registryshort_notm}} | **Administrator** platform access role. | An individual instance or all instances. Do not limit policies for {{site.data.keyword.registrylong_notm}} to the resource group level. | Yes |
| {{site.data.keyword.cos_full_notm}} | **Administrator** platform access role | An individual instance or all instances. |
| {{site.data.keyword.secrets-manager_short}} | **Administrator** or **Editor** platform access role  \n - **Manager** service access role | All resource groups | Required if you plan to use {{site.data.keyword.secrets-manager_short}} for encryption. |
| Resource group permissions | - **Viewer** platform access role  | The resource group where you want to create a cluster. | Yes |
| IAM Identity Service | - **Service ID creator**  \n - **User API key creator** role  \n - **Viewer** platform access role  | Yes |
| {{site.data.keyword.keymanagementserviceshort}}| **Administrator** platform access role. | All instances or the specific instance you want to use. | Required if you plan to use {{site.data.keyword.keymanagementserviceshort}} for encryption. |
| {{site.data.keyword.hscrypto}} | **Administrator** platform access role. | All instances or the specific instance you want to use. | Required if you plan to use {{site.data.keyword.hscrypto}} for encryption. | 
| Classic infrastructure | **Super User** role | N/A | Yes | 
| VPC infrastructure | **Administrator** platform access role for [VPC Infrastructure](/docs/vpc?topic=vpc-iam-getting-started). | All instances or the specific instance you want to use. | Yes |
{: caption="IAM roles needed to create a cluster." caption-side="bottom"}


## Example custom IAM roles
{: #example-iam}

The following table provides some example use cases and the corresponding IAM roles for those cases. You can use these examples or create your own custom roles. For more information, see [Creating custom roles](/docs/account?topic=account-custom-roles&interface=ui).


| Example custom role | Permissions |
| --- | --- |
| App auditor | - [Viewer platform access role for a cluster, region, or resource group](/docs/openshift?topic=openshift-iam-platform-access-roles)  \n - [Reader service access role for a cluster, region, or resource group](/docs/openshift?topic=openshift-iam-platform-access-roles). |
| App developers | - [Editor platform access role for a cluster](/docs/openshift?topic=openshift-iam-platform-access-roles)  \n - [Writer service access role scoped to a namespace](/docs/openshift?topic=openshift-iam-platform-access-roles). |
| Billing | [Viewer platform access role for a cluster, region, or resource group](/docs/openshift?topic=openshift-iam-platform-access-roles). |
| Create a cluster | See [Permissions to create a cluster](/docs/openshift?topic=openshift-iam-platform-access-roles).|
| Cluster administrator | - [Administrator platform access role for a cluster](/docs/openshift?topic=openshift-iam-platform-access-roles)  \n - [Manager service access role not scoped to a namespace (for the whole cluster)](/docs/openshift?topic=openshift-iam-platform-access-roles).|
| DevOps operator | - [Operator platform access role for a cluster](/docs/openshift?topic=openshift-iam-platform-access-roles)  \n - [Writer service access role not scoped to a namespace (for the whole cluster)](/docs/openshift?topic=openshift-iam-platform-access-roles).  |
| Operator or site reliability engineer | - [Administrator platform access role for a cluster, region, or resource group](/docs/openshift?topic=openshift-iam-platform-access-roles)  \n - [Reader service access role for a cluster or region](/docs/openshift?topic=openshift-iam-platform-access-roles)  \n - [Manager service access role for all cluster namespaces](/docs/openshift?topic=openshift-iam-platform-access-roles) to be able to use `kubectl top nodes,pods` commands. |
{: caption="Types of roles you might assign to meet different use cases." caption-side="bottom"}


