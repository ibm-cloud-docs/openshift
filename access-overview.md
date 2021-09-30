---

copyright: 
  years: 2014, 2021
lastupdated: "2021-09-30"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---




{{site.data.keyword.attribute-definition-list}}



# Understanding access control for clusters
{: #access-overview}

Learn how you can set up access control for your {{site.data.keyword.openshiftlong}} clusters by using various types of access control, roles, and policies.
{: shortdesc}

## Access control checklist
{: #access-checklist}

Use the following checklist to configure user access to your {{site.data.keyword.openshiftlong_notm}} cluster.
{: shortdesc}

### {{site.data.keyword.cloud_notm}} access control
{: #access-checklist-iam}

Your clusters use {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) as the identity provider to control access to the cluster.
{: shortdesc}

1. [Understand how roles, users, and resources in your account](#access_policies) can be managed.
2. [Set the API key](#api_key) for all the regions and resource groups that you want to create clusters in.
3. Invite users to your account and [assign them {{site.data.keyword.cloud_notm}} IAM roles](/docs/containers?topic=containers-users#checking-perms) for the service (**containers-kubernetes** in the API or CLI, and **Kubernetes Service** in the console).<p class="note">Do not assign {{site.data.keyword.cloud_notm}} IAM platform access roles at the same time as a service access role. You must assign platform and service access roles separately.</p>
4. To allow users to bind services to the cluster or to view logs that are forwarded from cluster logging configurations, [grant users Cloud Foundry roles](/docs/account?topic=account-mngcf) for the org and space that the services are deployed to or where logs are collected.
5. If you use Kubernetes namespaces to isolate resources within the cluster, grant access to namespaces by [assigning users {{site.data.keyword.cloud_notm}} IAM service access roles for the namespaces](/docs/containers?topic=containers-users#checking-perms).
6. For any automation tooling such as in your CI/CD pipeline, set up service accounts and [assign the service accounts Kubernetes RBAC permissions](/docs/containers?topic=containers-users#rbac)).

For more information about setting up your account and resources, try out this tutorial about the [best practices for organizing users, teams, and applications](/docs/solution-tutorials?topic=solution-tutorials-users-teams-applications).
{: tip}

### Other types of access control
{: #access-checklist-other}

Besides {{site.data.keyword.cloud_notm}} IAM access control policies that you set up, you might explore the additional ways to control how your cluster can be accessed.
{: shortdesc}

**Cluster network setup**:
- Cloud service endpoints: You might consider creating a cluster with only a private cloud service endpoint for communication to the cluster's API server. You can also [create an allowlist for the private cloud service endpoint](/docs/containers?topic=containers-access_cluster#private-se-allowlist) to limit access to your cluster from only the allowed subnets. For more information, see the different service architecture setups for [classic](/docs/containers?topic=containers-service-arch#architecture_classic) or [VPC](/docs/containers?topic=containers-service-arch#architecture_vpc) clusters.
- Classic network: See [Network segmentation and privacy for classic clusters](/docs/containers?topic=containers-security#network_segmentation).
- VPC network: See [Network segmentation and privacy for VPC clusters](/docs/containers?topic=containers-security#network_segmentation_vpc).

**Kubernetes resources within the cluster**:
- Pod-to-pod network traffic control: Consider using [Kubernetes network policies and Calico](/docs/containers?topic=containers-network_policies).
- {{site.data.keyword.openshiftshort}} resources for pod-level control: See [Configuring security context constraints (SCCs)](/docs/openshift?topic=openshift-openshift_scc#oc_sccs).


## Understanding IAM access policies and roles
{: #access_policies}
{: help}
{: support}

Access policies determine the level of access that users in your {{site.data.keyword.cloud_notm}} account have to resources across the {{site.data.keyword.cloud_notm}} platform. A policy assigns a user one or more roles that define the scope of access to a single service or to a set of services and resources that are organized together in a resource group. Each service in {{site.data.keyword.cloud_notm}} might require its own set of access policies.
{: shortdesc}

### Pick the right access policy and role for your users
{: #access_roles}

You must define access policies for every user that works with {{site.data.keyword.openshiftlong_notm}}. The scope of an access policy is based on a user's defined role or roles, which determine the actions that the user can perform. Some policies are pre-defined but others can be customized. The same policy is enforced whether the user makes the request from the {{site.data.keyword.cloud_notm}} API, CLI, or UI.
{: shortdesc}

The following image shows the different types of permissions and roles, the actions a role can perform, and how the roles relate to each other.

<img src="images/user_access.png" alt="In {{site.data.keyword.cloud_notm}}, you can assign IAM platform, IAM service, Cloud Foundry, and infrastructure roles." style="border-style: none"/>

To see the specific {{site.data.keyword.openshiftlong_notm}} permissions that can be performed with each role, check out the [User access permissions](/docs/openshift?topic=openshift-access_reference) reference topic.
{: tip}

#### Overview of {{site.data.keyword.cloud_notm}} IAM platform access roles
{: #platform-roles-ov}

Use platform access roles in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) to grant users access to manage cluster resources in {{site.data.keyword.openshiftlong_notm}}. When you configure permissions for {{site.data.keyword.openshiftlong_notm}} in IAM, use the name **containers-kubernetes** for the API or CLI, and **Kubernetes Service** for the console.
{: shortdesc}

**What types of actions do platform access roles permit?**

With platform access roles, users can manage resources like clusters, worker pools, worker nodes, and add-ons. Example actions that are permitted by platform access roles are creating or removing clusters, binding services to a cluster, managing networking and storage resources, or adding extra worker nodes. You can set the policies for these roles by resource group, region, or cluster instance. You cannot scope a platform access role by namespace within a cluster.

For more information, see [{{site.data.keyword.cloud_notm}} IAM platform access roles](/docs/containers?topic=containers-access_reference#iam_platform).

**What types of actions are not permitted by platform access roles?**

No access to Kubernetes resources
: Platform access roles do not grant access to the Kubernetes API to manage resources within the cluster, like Kubernetes pods, namespaces, or services. However, users can still perform the `ibmcloud oc cluster config` command to set the Kubernetes context to the cluster. Then, you can authorize the users to perform select Kubernetes actions by using [custom RBAC policies](/docs/containers?topic=containers-access-overview#role-binding). You might do this if your organization currently uses custom RBAC policies to control Kubernetes access and plans to continue using custom RBAC instead of service access roles.

No access to underlying infrastructure
: Although platform access roles authorize you to perform infrastructure actions on the cluster, they do not grant access to the IBM Cloud infrastructure resources. Access to the IBM Cloud infrastructure resources is determined by the [API key that is set for the region](#api_key).

#### Overview of {{site.data.keyword.cloud_notm}} IAM service access roles
{: #service-roles-ov}

Use service access roles in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) to grant users access to manage Kubernetes resources in {{site.data.keyword.openshiftlong_notm}} clusters. When you configure permissions for {{site.data.keyword.openshiftlong_notm}} in IAM, use the name **containers-kubernetes** for the API or CLI, and **Kubernetes Service** for the console.
{: shortdesc}

**What types of actions do platform access roles permit?**

Service access roles are synchronized with corresponding Kubernetes RBAC policies in a cluster. As such, service access roles grant access to the Kubernetes API, dashboard, and CLI (`oc`). Example actions that are permitted by service access roles include creating app deployments, adding namespaces, or setting up configmaps.

**What can I scope service access policies to?**

You can scope the policy for service access roles by resource group, region, or cluster instance. Further, you can also scope service access roles to Kubernetes namespaces that are in all, individual, or region-wide clusters. When you scope a service access role to a namespace, you cannot apply the policy to a resource group or assign a platform access role at the same time.

If you assigned only service access roles to users, the users must be given the cluster master URL to open the {{site.data.keyword.openshiftshort}} web console from their browser at `https://<master_URL>/console` instead of the {{site.data.keyword.cloud_notm}} console. Otherwise, [give the users the platform **Viewer** role](/docs/containers?topic=containers-users#add_users_cli_platform).

#### Overview of RBAC
{: #role-binding}

In Kubernetes, role-based access control (RBAC) is a way of securing the resources inside your cluster. RBAC roles determine the Kubernetes actions that users can perform on those resources, such as Kubernetes pods, namespaces, or services. Example actions that are permitted by RBAC roles are creating objects such as pods or reading pod logs.
{: shortdesc}

**How can I assign RBAC roles?**

Choose from the following options.

Use {{site.data.keyword.cloud_notm}} IAM
: You can use IAM to automatically create and manage RBAC in your cluster, by assigning [service access roles](#service-roles-ov) to users. Every user who is assigned a service access role is automatically assigned a corresponding RBAC cluster role. This RBAC cluster role is applied either in a specific namespace or in all namespaces, depending on whether you scope the policy to a namespace. Change that you make to the user in IAM, such as updating or removing the service access policy, are automatically synchronized to the RBAC in your cluster. The synchronization of service roles to RBAC might take a couple minutes, depending on the number of users and namespaces in your cluster.

Manage your own RBAC
: See [Assigning RBAC permissions](/docs/containers?topic=containers-access-overview#role-binding).

#### Overview of classic infrastructure
{: #api_key}

Classic infrastructure roles enable access to your classic IBM Cloud infrastructure resources.
{: shortdesc}

Set up a user with **Super User** infrastructure role, and store this user's infrastructure credentials in an API key. Then, set the API key in each region and resource group that you want to create clusters in. After you set up the API key, other users that you grant access to {{site.data.keyword.openshiftlong_notm}} do not need infrastructure roles as the API key is shared for all users within the region. Instead, {{site.data.keyword.cloud_notm}} IAM platform access roles determine the infrastructure actions that users are allowed to perform.

If you don't want to set up the API key with full **Super User** infrastructure permissions or you need to grant specific device access to users, you can [customize infrastructure permissions](/docs/containers?topic=containers-access-creds#infra_access).

Example actions that are permitted by infrastructure roles are viewing the details of cluster worker node machines or editing networking and storage resources.

VPC clusters do not need classic infrastructure permissions. Instead, you assign **Administrator** platform access to the **VPC Infrastructure** service in {{site.data.keyword.cloud_notm}}. Then, these credentials are stored in the API key for each region and resource group that you create clusters in.
{: note}

#### Overview of Cloud Foundry
{: #cf_overview}

Not all {{site.data.keyword.cloud_notm}} services can be managed with IAM. If you use one of these services, you can continue to use Cloud Foundry user roles to control access to those services.
{: shortdesc}

Cloud Foundry roles grant access to organizations and spaces within the account. To see the list of Cloud Foundry-based services in {{site.data.keyword.cloud_notm}}, run `ibmcloud service list`.

Example actions that are permitted by Cloud Foundry roles are creating a new Cloud Foundry service instance or binding a Cloud Foundry service instance to a cluster. To learn more, see the available [org and space roles](/docs/account?topic=account-cfaccess) or the steps for [managing Cloud Foundry access](/docs/account?topic=account-mngcf) in the {{site.data.keyword.cloud_notm}} IAM documentation.

### Assign access roles to individual or groups of users in {{site.data.keyword.cloud_notm}} IAM
{: #iam_individuals_groups}

When you set {{site.data.keyword.cloud_notm}} IAM policies, you can assign roles to an individual user or to a group of users.
{: shortdesc}

Individual users
: You might have a specific user that needs more or less permissions than the rest of your team. You can customize permissions on an individual basis so that each person has the permissions that they need to complete their tasks. You can assign more than one {{site.data.keyword.cloud_notm}} IAM role to each user.

Multiple users in an access group
: You can create a group of users and then assign permissions to that group. For example, you can group all team leaders and assign administrator access to the group. Then, you can group all developers and assign only write access to that group. You can assign more than one {{site.data.keyword.cloud_notm}} IAM role to each access group. When you assign permissions to a group, any user that is added or removed from that group is affected. If you add a user to the group, then they also have the additional access. If they are removed, their access is revoked.
  You cannot scope {{site.data.keyword.cloud_notm}} IAM service access roles to an IAM access group because the roles are not synced to the RBAC roles within the cluster. If you want to scope RBAC roles to a group of users, you must [manually set up groups of users](https://docs.openshift.com/container-platform/4.7/authentication/understanding-authentication.html){: external} in your cluster instead of using IAM access groups. You can still scope IAM platform access roles to IAM access groups to control actions like ordering worker nodes, because platform access roles are never synced to RBAC roles.
  {: note}


{{site.data.keyword.cloud_notm}} IAM roles can't be assigned to a service account. Instead, you can directly [assign RBAC roles to service accounts](/docs/containers?topic=containers-users#rbac).
{: tip}

You must also specify whether users have access to one cluster in a resource group, all clusters in a resource group, or all clusters in all resource groups in your account.


### Scope user access to cluster instances, namespaces, or resource groups
{: #resource_groups}

In {{site.data.keyword.cloud_notm}} IAM, you can assign user access roles to resource instances, Kubernetes namespaces (projects in {{site.data.keyword.openshiftshort}}), or resource groups.
{: shortdesc}

When you create your {{site.data.keyword.cloud_notm}} account, the default resource group is created automatically. If you do not specify a resource group when you create the resource, resource instances (clusters) automatically belong to the default resource group. In {{site.data.keyword.cloud_notm}} IAM, a Kubernetes namespace is a resource type of a resource instance (cluster). If you want to add a resource group in your account, see [Best practices for setting up your account](/docs/account?topic=account-account_setup) and [Setting up your resource groups](/docs/account?topic=account-rgs).

Resource instance
: Each {{site.data.keyword.cloud_notm}} service in your account is a resource that has instances. The instance differs by service. For example, in {{site.data.keyword.openshiftlong_notm}}, the instance is a cluster, but in {{site.data.keyword.cloudcerts_long_notm}}, the instance is a certificate. By default, resources belong to the default resource group in your account. You can assign users an access role to a resource instance to grant permissions as described in the following scenarios.
  - All {{site.data.keyword.cloud_notm}} IAM services in your account, including all clusters in {{site.data.keyword.openshiftlong_notm}} and images in {{site.data.keyword.registrylong_notm}}.
  - All instances within a service, such as all the clusters in {{site.data.keyword.openshiftlong_notm}}.
  - All instances within a region of a service, such as all the clusters in the <strong>US South</strong> region of {{site.data.keyword.openshiftlong_notm}}.
  - To an individual instance, such as one cluster.
  
Kubernetes namespace (projects in {{site.data.keyword.openshiftshort}})
: As part of cluster resource instances in {{site.data.keyword.cloud_notm}} IAM, you can assign users with service access roles to namespaces within your clusters.
  When you assign access to a namespace, the policy applies to all current and future instances of the namespace in all the clusters that you authorize. For example, say that you want a `dev` group of users to be able to deploy Kubernetes resources in a `test` namespace in all your clusters in AP North. If you assign the `dev` access group the **Writer** service access role for the Kubernetes namespace `test` in all clusters in the AP North region within the `default` resource group, the `dev` group can access the `test` namespace in any AP North cluster in the `default` resource group that currently has or eventually has a `test` namespace.
  If you scope a service access role to a namespace, you cannot apply the policy to a resource group or assign a platform access role at the same time.
    
Resource group
: You can organize your account resources in customizable groupings so that you can quickly assign individual or groups of users access to more than one resource at a time. Resource groups can help operators and administrators filter resources to view their current usage, troubleshoot issues, and manage teams.
  A cluster can be created in only one resource group that you can't change afterward. If you create a cluster in the wrong resource group, you must delete the cluster and re-create it in the correct resource group. Furthermore, if you need to use the `ibmcloud oc cluster service bind` command to [integrate with an {{site.data.keyword.cloud_notm}} service](/docs/containers?topic=containers-service-binding#bind-services), that service must be in the same resource group as the cluster. Services that do not use resource groups like {{site.data.keyword.registrylong_notm}} or that do not need service binding like {{site.data.keyword.la_full_notm}} work even if the cluster is in a different resource group.
  {: important}
  Consider giving clusters unique names across resource groups and regions in your account to avoid naming conflicts. You cannot rename a cluster.
  You can assign users an access role to a resource group to grant permissions as described in the following scenarios. Note that unlike resource instances, you cannot grant access to an individual instance within a resource group.
  - All {{site.data.keyword.cloud_notm}} IAM services in the resource group, including all clusters in {{site.data.keyword.openshiftlong_notm}} and images in {{site.data.keyword.registrylong_notm}}.</li>
  - All instances within a service in the resource group, such as all the clusters in {{site.data.keyword.openshiftlong_notm}}.</li>
  - All instances within a region of a service in the resource group, such as all the clusters in the <strong>US South</strong> region of {{site.data.keyword.openshiftlong_notm}}.




