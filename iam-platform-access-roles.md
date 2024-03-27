---

copyright: 
  years: 2014, 2024
lastupdated: "2024-03-27"

keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, infrastructure, policy, users, permissions, access, roles

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# IAM roles and actions
{: #iam-platform-access-roles}

{{site.data.keyword.openshiftlong_notm}} is configured to use {{site.data.keyword.iamlong}} roles to determine the actions that users can perform on {{site.data.keyword.openshiftlong_notm}} clusters, worker nodes, and Ingress application load balancers (ALBs).
{: shortdesc}

Review the following table for a list of Platform and Service roles and their associated actions.

{{../account/iam-service-roles.md#containers-kubernetes-roles}}

For a list of all IBM services and their associated roles and actions, see [IAM roles and actions](/docs/account?topic=account-iam-service-roles-actions){: tip}


Platform access roles
:   With platform access roles, users can manage resources like clusters, worker pools, worker nodes, and add-ons. Example actions that are permitted by platform access roles are creating or removing clusters, binding services to a cluster, managing networking and storage resources, or adding extra worker nodes. You can set the policies for these roles by resource group, region, or cluster instance. You can't scope a platform access role by namespace within a cluster. Platform access roles don't grant access to the Kubernetes API to manage resources within the cluster, like Kubernetes pods, namespaces, or services.

Service access roles
:   Use service access roles to grant users access to manage Kubernetes resources within {{site.data.keyword.openshiftlong_notm}} clusters. Service access roles are synchronized with corresponding [Kubernetes RBAC policies](/docs/openshift?topic=openshift-understand-rbac) in a cluster. As such, service access roles grant access to the Kubernetes API, dashboard, and CLI (`oc`). Example actions that are permitted by service access roles include creating app deployments, adding namespaces, or setting up configmaps. You can scope the policy for service access roles by resource group, region, or cluster instance. Further, you can also scope service access roles to Kubernetes namespaces that are in all clusters, individual clusters, or clusters in a specific region. 

## Permissions to create a cluster
{: #cluster-create-permissions}

Review the following permissions that you need to create a cluster including the required permissions for other integrations and services that you might use.


| Service or resource group | Role | Scope | Required? |
| --- | --- | --- | --- |
| {{site.data.keyword.containershort}} | - **Administrator** platform access role  \n - **Writer** or **Manager** service access role | The resource group where you want to create a cluster. | Yes |
| {{site.data.keyword.registryshort_notm}} | **Administrator** platform access role. | An individual instance or all instances. Do not limit policies for {{site.data.keyword.registrylong_notm}} to the resource group level. | Yes |
| {{site.data.keyword.cos_full_notm}} | **Administrator** platform access role | An individual instance or all instances. | Yes |
| {{site.data.keyword.secrets-manager_short}} | **Administrator** or **Editor** platform access role  \n - **Manager** service access role | All resource groups | Required if you plan to use {{site.data.keyword.secrets-manager_short}} for encryption. |
| Resource group permissions | - **Viewer** platform access role  | The resource group where you want to create a cluster. | Yes |
| IAM Identity Service | - **Service ID creator**  \n - **User API key creator** role  \n - **Viewer** platform access role  | The resource group where you want to create a cluster. | Yes |
| {{site.data.keyword.keymanagementserviceshort}}| **Administrator** platform access role. | All instances or the specific instance you want to use. | Required if you plan to use {{site.data.keyword.keymanagementserviceshort}} for encryption. |
| {{site.data.keyword.hscrypto}} | **Administrator** platform access role. | All instances or the specific instance you want to use. | Required if you plan to use {{site.data.keyword.hscrypto}} for encryption. | 
| Classic infrastructure | **Super User** role | N/A | Yes | 
| VPC infrastructure | **Administrator** platform access role for [VPC Infrastructure](/docs/vpc?topic=vpc-iam-getting-started). | All instances or the specific instance you want to use. | Yes |
{: caption="IAM roles needed to create a cluster." caption-side="bottom"}


Consider saving the permissions outlined in the previous table as a custom IAM role. This way, you can assign users to the custom role instead of assigning each individual service. For more information, see the following example custom roles or the IAM documentation for [Creating custom roles](/docs/account?topic=account-custom-roles&interface=ui).
{: tip}



## Example custom IAM roles
{: #example-iam}

The following table provides some example use cases and the corresponding IAM roles for those cases. You can use these examples or create your own custom roles. For more information, see [Creating custom roles](/docs/account?topic=account-custom-roles&interface=ui).


| Example custom role | Permissions |
| --- | --- |
| App auditor | - Viewer platform access role for a cluster, region, or resource group.  \n - [Reader service access role for a cluster, region, or resource group. |
| App developers | - Editor platform access role for a cluster. \n - Writer service access role scoped to a namespace. |
| Billing | Viewer platform access role for a cluster, region, or resource group. |
| Cluster administrator | - Administrator platform access role for a cluster.  \n - Manager service access role for the whole cluster (not scoped to a namespace).|
| DevOps operator | - Operator platform access role for a cluster.  \n - Writer service access role for the whole cluster (not scoped to a namespace.  |
| Operator or site reliability engineer | - Administrator platform access role for a cluster, region, or resource group. \n - Reader service access role for a cluster or region.  \n - Manager service access role for all cluster namespaces to be able to use `kubectl top nodes,pods` commands. |
{: caption="Types of roles you might assign to meet different use cases." caption-side="bottom"}


