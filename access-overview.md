---

copyright: 
  years: 2014, 2024
lastupdated: "2024-03-29"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, infrastructure, rbac, policy

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

1. [Understand how roles, users, and resources in your account](/docs/openshift?topic=openshift-iam-platform-access-roles) can be managed.
1. Invite users to your account and [assign them {{site.data.keyword.cloud_notm}} IAM roles](/docs/openshift?topic=openshift-iam-platform-access-roles) for the service.

    Do not assign {{site.data.keyword.cloud_notm}} IAM platform access roles at the same time as a service access role. You must assign platform and service access roles separately.
    {: note}

1. If you use Kubernetes namespaces to isolate resources within the cluster, grant access to namespaces by [assigning users {{site.data.keyword.cloud_notm}} IAM service access roles for the namespaces](/docs/openshift?topic=openshift-iam-platform-access-roles).
1. For any automation tooling such as in your CI/CD pipeline, set up service accounts and [assign the service accounts Kubernetes RBAC permissions](/docs/openshift?topic=openshift-understand-rbac).

For more information about setting up your account and resources, see [best practices for organizing users, teams, and applications](/docs/account?topic=account-account_setup).
{: tip}



#### Overview of RBAC
{: #role-binding}

In Kubernetes, role-based access control (RBAC) is a way of securing the resources inside your cluster. RBAC roles determine the Kubernetes actions that users can perform on those resources, such as Kubernetes pods, namespaces, or services. Example actions that are permitted by RBAC roles are creating objects such as pods or reading pod logs.
{: shortdesc}

You can assign RBAC roles through the following methods.

By using {{site.data.keyword.cloud_notm}} IAM
:   You can use IAM to automatically create and manage RBAC in your cluster, by assigning IAM service access roles to users. Every user who is assigned a service access role is automatically assigned a corresponding RBAC cluster role. This RBAC cluster role is applied either in a specific namespace or in all namespaces, depending on whether you scope the policy to a namespace. Change that you make to the user in IAM, such as updating or removing the service access policy, are automatically synchronized to the RBAC in your cluster. The synchronization of service roles to RBAC might take a couple minutes, depending on the number of users and namespaces in your cluster.

Managing your own RBAC
:   See [Assigning RBAC permissions](/docs/openshift?topic=openshift-understand-rbac).



### Assign access roles to individual or groups of users in {{site.data.keyword.cloud_notm}} IAM
{: #iam_individuals_groups}

When you set {{site.data.keyword.cloud_notm}} IAM policies, you can assign roles to an individual user or to a group of users.
{: shortdesc}

Individual users
:   You might have a specific user that needs more or less permissions than the rest of your team. You can customize permissions on an individual basis so that each person has the permissions that they need to complete their tasks. You can assign more than one {{site.data.keyword.cloud_notm}} IAM role to each user.

Multiple users in an access group
:   You can create a group of users and then assign permissions to that group. For example, you can group all team leaders and assign administrator access to the group. Then, you can group all developers and assign only write access to that group. You can assign more than one {{site.data.keyword.cloud_notm}} IAM role to each access group. When you assign permissions to a group, any user that is added or removed from that group is affected. If you add a user to the group, then they also have the additional access. If they are removed, their access is revoked.


{{site.data.keyword.cloud_notm}} IAM roles can't be assigned to a service account. Instead, you can directly [assign RBAC roles to service accounts](/docs/openshift?topic=openshift-understand-rbac).
{: tip}

You must also specify whether users have access to one cluster in a resource group, all clusters in a resource group, or all clusters in all resource groups in your account.


### Scope user access to cluster instances, namespaces, or resource groups
{: #resource_groups}

In {{site.data.keyword.cloud_notm}} IAM, you can assign user access roles to resource instances, Kubernetes namespaces (projects in {{site.data.keyword.redhat_openshift_notm}}), or resource groups.
{: shortdesc}

When you create your {{site.data.keyword.cloud_notm}} account, the default resource group is created automatically. If you don't specify a resource group when you create the resource, resource instances (clusters) automatically belong to the default resource group. In {{site.data.keyword.cloud_notm}} IAM, a Kubernetes namespace is a resource type of a resource instance (cluster). If you want to add a resource group in your account, see [Best practices for setting up your account](/docs/account?topic=account-account_setup) and [Setting up your resource groups](/docs/account?topic=account-rgs).

Resource instance
:   Each {{site.data.keyword.cloud_notm}} service in your account is a resource that has instances. The instance differs by service. For example, in {{site.data.keyword.openshiftlong_notm}}, the instance is a cluster. By default, resources belong to the default resource group in your account. You can assign users an access role to a resource instance to grant permissions as described in the following scenarios.
    - All {{site.data.keyword.cloud_notm}} IAM services in your account, including all clusters in {{site.data.keyword.openshiftlong_notm}} and images in {{site.data.keyword.registrylong_notm}}.
    - All instances within a service, such as all the clusters in {{site.data.keyword.openshiftlong_notm}}.
    - All instances within a region of a service, such as all the clusters in the **US South** region of {{site.data.keyword.openshiftlong_notm}}.
    - To an individual instance, such as one cluster.
  
Kubernetes namespace (projects in {{site.data.keyword.redhat_openshift_notm}})
:   As part of cluster resource instances in {{site.data.keyword.cloud_notm}} IAM, you can assign users with service access roles to namespaces within your clusters.
    When you assign access to a namespace, the policy applies to all current and future instances of the namespace in all the clusters that you authorize. For example, say that you want a `dev` group of users to be able to deploy Kubernetes resources in a `test` namespace in all your clusters in AP North. If you assign the `dev` access group the **Writer** service access role for the Kubernetes namespace `test` in all clusters in the AP North region within the `default` resource group, the `dev` group can access the `test` namespace in any AP North cluster in the `default` resource group that currently has or eventually has a `test` namespace.
    If you scope a service access role to a namespace, you can't apply the policy to a resource group or assign a platform access role at the same time.
    

    




