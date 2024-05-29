---

copyright: 
  years: 2014, 2024
lastupdated: "2024-05-29"

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

For a list of all IBM services and their associated roles and actions, see [IAM roles and actions](/docs/account?topic=account-iam-service-roles-actions). For more information about setting up your account and resources, see [best practices for organizing users, teams, and applications](/docs/account?topic=account-account_setup).
{: tip}


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
| {{site.data.keyword.secrets-manager_short}} | - **Administrator** or **Editor** platform access role  \n - **Manager** service access role | All resource groups | Required if you plan to use {{site.data.keyword.secrets-manager_short}} for encryption. |
| Resource group permissions | - **Viewer** platform access role  | The resource group where you want to create a cluster. | Yes |
| IAM Identity Service | - **Service ID creator**  \n - **User API key creator** role  \n - **Viewer** platform access role  | The resource group where you want to create a cluster. | Yes |
| {{site.data.keyword.keymanagementserviceshort}}| **Administrator** platform access role. | All instances or the specific instance you want to use. | Required if you plan to use {{site.data.keyword.keymanagementserviceshort}} for encryption. |
| {{site.data.keyword.hscrypto}} | **Administrator** platform access role. | All instances or the specific instance you want to use. | Required if you plan to use {{site.data.keyword.hscrypto}} for encryption. | 
| Classic infrastructure | **Super User** role. For more information, see [Classic infrastructure roles](#iam-platform-access-roles). | N/A | Yes | 
| VPC infrastructure | **Administrator** platform access role for [VPC Infrastructure](/docs/vpc?topic=vpc-iam-getting-started). | All instances or the specific instance you want to use. | Yes |
{: caption="IAM roles needed to create a cluster." caption-side="bottom"}


Consider saving the permissions outlined in the earlier table as a custom IAM role. This way, you can assign users to the custom role instead of assigning each individual service. For more information, see the following example custom roles or the IAM documentation for [Creating custom roles](/docs/account?topic=account-custom-roles&interface=ui).
{: tip}



## Example custom IAM roles
{: #example-iam}

The following table provides some example use cases and the corresponding IAM roles for those cases. You can use these examples or create your own custom roles. For more information, see [Creating custom roles](/docs/account?topic=account-custom-roles&interface=ui).


| Example custom role | Permissions |
| --- | --- |
| App auditor | - **Viewer** platform access role for a cluster, region, or resource group.  \n - **Reader** service access role for a cluster, region, or resource group. |
| App developers | - Editor platform access role for a cluster. \n - Writer service access role scoped to a namespace. |
| Billing | **Viewer** platform access role for a cluster, region, or resource group. |
| Cluster administrator | - **Administrator** platform access role for a cluster.  \n - **Manager** service access role for the whole cluster (not scoped to a namespace).|
| DevOps operator | - **Operator** platform access role for a cluster.  \n - **Writer** service access role for the whole cluster (not scoped to a namespace).  |
| Operator or site reliability engineer | - **Administrator** platform access role for a cluster, region, or resource group. \n - Reader service access role for a cluster or region.  \n - **Manager** service access role for all cluster namespaces to be able to use `kubectl top nodes,pods` commands. |
{: caption="Types of roles you might assign to meet different use cases." caption-side="bottom"}


## Classic infrastructure roles
{: #classic-roles}

A user with the **Super User** infrastructure access role sets the API key for a region and resource group so that infrastructure actions can be performed.

The infrastructure actions that other users in the account can perform are authorized through {{site.data.keyword.cloud_notm}} IAM platform access roles. 

Use the following table to customize classic infrastructure permissions only when you can't assign **Super User** to the user who sets the API key. For instructions to assign permissions, see [Customizing infrastructure permissions](/docs/openshift?topic=openshift-iam-platform-access-roles).
{: important}




### Required classic infrastructure permissions
{: #required-classic-rbac}

| Permission | Description | IAM Assign Policy Console | CLI |
|:-----------------|:-----------------|:---------------|:----|
| IPMI Remote Management | Manage worker nodes.|
| Add Server | Add worker nodes.   \n   \n  **Note**: For worker nodes that have public IP addresses, you also need the **Add Compute with Public Network Port** permission in the **Network** category. |
| Cancel Server | Delete worker nodes. |
| OS Reloads and Rescue Kernel | Update, reboot, and reload worker nodes. |
| View Virtual Server Details | Required if the cluster has VM worker nodes. List and get details of VM worker nodes. |
| View Hardware Details | Required if the cluster has bare metal worker nodes. List and get details of bare metal worker nodes. |
| Add Support Case | As part of the cluster creation automation, support cases are opened to provision the cluster infrastructure. |
| Edit Support Case | As part of the cluster creation automation, support cases are updated to provision the cluster infrastructure. |
| View Support Case | As part of the cluster creation automation, support cases are used to provision the cluster infrastructure. |
{: caption="Table 1: Required classic infrastructure permissions" caption-side="bottom"}


### Suggested classic infrastructure permissions
{: #classic-rbac-suggested}

| Permission | Description |
| --- | --- |
| Access All Virtual | Access all worker nodes. |
| Access All Hardware | Designate access to all bare metal worker nodes.  Without this permission, a user who creates one cluster might not be able to view the bare metal worker nodes of another cluster even if the user has IAM access to both clusters. |
| Add Compute with Public Network Port | Let worker nodes have a port that can be accessible on the public network. |
| Manage DNS | Set up public load balancer or Ingress networking to expose apps. |
| Edit Hostname/Domain | Set up public load balancer or Ingress networking to expose apps. |
| Add IP Addresses | Add IP addresses to public or private subnets that are used for cluster load balancing. |
| Manage Network Subnet Routes | Manage public and private VLANs and subnets that are used for cluster load balancing. |
| Manage Port Control | Manage ports that are used for app load balancing. |
| Manage Certificates (SSL) | Set up certificates that are used for cluster load balancing. |
| View Certificates (SSL) | Set up certificates that are used for cluster load balancing. |
| Add/Upgrade Storage (Storage Layer) | Create {{site.data.keyword.cloud_notm}} File or Block storage instances to attach as volumes to your apps for persistent storage of data. |
| Storage Manage | Manage {{site.data.keyword.cloud_notm}} File or Block storage instances that are attached as volumes to your apps for persistent storage of data. |
{: caption="Table 2: Suggested classic infrastructure permissions" caption-side="bottom"}

