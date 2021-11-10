---

copyright: 
  years: 2014, 2021
lastupdated: "2021-11-10"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Controlling user access with {{site.data.keyword.cloud_notm}} IAM and Kubernetes RBAC
{: #users}

Set {{site.data.keyword.cloud_notm}} IAM platform access and service access policies in the {{site.data.keyword.cloud_notm}} console or CLI so that users can work with clusters in {{site.data.keyword.openshiftlong_notm}}. IAM service access roles correspond with Kubernetes role-based access control (RBAC) within the cluster.
{: shortdesc}

Before you begin, check out [Understanding access policies and roles](/docs/openshift?topic=openshift-access-overview#access_policies) to review what policies are, whom you can assign policies to, and what resources can be granted policies.
{: shortdesc}

{{site.data.keyword.cloud_notm}} IAM roles can't be assigned to a service account. Instead, you can directly [assign RBAC roles to service accounts](#rbac).
{: note}

## Example cluster use cases and IAM roles
{: #example-iam}

Wondering which access roles to assign to your cluster users? Use the examples in following table to determine which roles and scope to assign. You can find more information about what roles authorize which types of actions on the user access reference page in the table's links.
{: shortdesc}

| Use case | Example roles and scope |
| --- | --- |
| App auditor | [Viewer platform access role for a cluster, region, or resource group](/docs/openshift?topic=openshift-access_reference#iam_platform), [Reader service access role for a cluster, region, or resource group](/docs/openshift?topic=openshift-access_reference#service). |
| App developers | [Editor platform access role for a cluster](/docs/openshift?topic=openshift-access_reference#iam_platform), [Writer service access role scoped to a namespace](/docs/openshift?topic=openshift-access_reference#service), [Cloud Foundry developer space role](/docs/openshift?topic=openshift-access_reference#cloud-foundry). |
| Billing | [Viewer platform access role for a cluster, region, or resource group](/docs/openshift?topic=openshift-access_reference#iam_platform). |
| Create a cluster | See [Permissions to create a cluster](/docs/openshift?topic=openshift-access_reference#cluster_create_permissions).|
| Cluster administrator | [Administrator platform access role for a cluster](/docs/openshift?topic=openshift-access_reference#iam_platform), [Manager service access role not scoped to a namespace (for the whole cluster)](/docs/openshift?topic=openshift-access_reference#service).|
| DevOps operator | [Operator platform access role for a cluster](/docs/openshift?topic=openshift-access_reference#iam_platform), [Writer service access role not scoped to a namespace (for the whole cluster)](/docs/openshift?topic=openshift-access_reference#service), [Cloud Foundry developer space role](/docs/openshift?topic=openshift-access_reference#cloud-foundry).  |
| Operator or site reliability engineer | [Administrator platform access role for a cluster, region, or resource group](/docs/openshift?topic=openshift-access_reference#iam_platform), [Reader service access role for a cluster or region](/docs/openshift?topic=openshift-access_reference#service) or [Manager service access role for all cluster namespaces](/docs/openshift?topic=openshift-access_reference#service) to be able to use `kubectl top nodes,pods` commands. |
{: summary="The first column contains the use case, which is typically the role of a user. The second column is the example role and scope of the role that you assign the user in {{site.data.keyword.cloud_notm}} IAM."}
{: caption="Types of roles you might assign to meet different use cases." caption-side="top"}


## Assigning {{site.data.keyword.cloud_notm}} IAM roles with the console
{: #add_users}

Grant users access to your {{site.data.keyword.openshiftlong_notm}} clusters by assigning {{site.data.keyword.cloud_notm}} IAM platform access and service access roles with the {{site.data.keyword.cloud_notm}} console.
{: shortdesc}

Do not assign platform access roles at the same time as a service access role. You must assign platform and service access roles separately.
{: tip}

Before you begin, verify that you're assigned the **Administrator** platform access role for the {{site.data.keyword.cloud_notm}} account in which you're working.

1. Log in to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external}. From the menu bar, select **Manage > Access (IAM)**.

2. Select users individually or create an access group of users.
    - To assign roles to an individual user
        1. In the left navigation, click the **Users** page, and then click the name of the user that you want to set permissions for. If the user isn't shown, click **Invite users** to add them to the account.
        2. Click the **Access policies** tab, and then click **Assign access**. Now, the breadcrumbs on the page are **Users / Manage User**.
        3. Optional: Add the user to an access group that has access to {{site.data.keyword.openshiftlong_notm}}.
    - To assign roles to multiple users in an access group
        1. In the left navigation, click the **Access groups** page.
        2. Click **Create** and give your group a **Name** and **Description**. Click **Create**.
        3. Click **Add users** to add people to your access group. A list of users that have access to your account is shown.
        4. Check the box next to the users that you want to add to the group. A dialog box displays.
        5. Click **Add to group**.
        6. Click the **Access policies** tab.
        7. Click **Assign access**. Now, the breadcrumbs on the page are **Groups / Manage Group**.

3. Assign an access policy to {{site.data.keyword.openshiftlong_notm}}.
    1. Click the **IAM services** tile.
    2. In the services drop-down list, select **Kubernetes Service**. You can enter text in the drop-down list instead of scrolling through the list.
    3. **Optional**: To scope the access policy to a resource group, select the resource group from the resource group drop-down list. If you want to scope the policy to a Kubernetes namespace, make sure to clear the resource group drop-down list. You cannot scope an access policy to both a Kubernetes namespace and a resource group at the same time.
    4. From the **Region** list, select one or all regions.
    5. From the **Cluster** `string equals` drop-down list, select the cluster that you want to scope the access policy to. To scope the policy to all clusters, clear or leave the field blank.
    6. From the **Namespace** `string equals` field, enter the Kubernetes namespace that you want to scope the access policy to. Note that you cannot scope an access policy to a namespace if you also scope the access policy to a resource group. Additionally, if you scope an access policy to a namespace, you must assign only a **service access** role. Do not assign a **platform access** role at the same time as you assign a service access role. Assign a platform access role separately.
    7. Select roles for the access policy.
        - **Platform access role**: Grants access to {{site.data.keyword.openshiftlong_notm}} so that users can manage infrastructure resources such as clusters, worker nodes, worker pools, Ingress application load balancers, and storage. To find a list of supported actions per role, see [platform access roles reference page](/docs/openshift?topic=openshift-access_reference#iam_platform). Note that if you assign a user the **Administrator** platform access role for only one cluster, you must also assign the user the **Viewer** platform access role for all clusters in that region in the resource group.
        - **Service access role**: Grants access to the Kubernetes API from within a cluster so that users can manage Kubernetes resources such as pods, deployments, services, and namespaces. To find a list of supported actions per role, see [service access roles reference page](/docs/openshift?topic=openshift-access_reference#service). Do not assign a platform access role at the same time as you assign a service access role. If you also want the user to have a platform access role, repeat these steps but leave the namespace field blank and assign only a platform access role (do not assign a service access role again).
    8. Click **Add**.
    9. If you assigned only service access roles to users, the users must perform a one-time `ibmcloud oc cluster config` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_config) and be given the cluster master URL to open the {{site.data.keyword.openshiftshort}} web console from their browser at `https://<master_URL>/console` instead of the {{site.data.keyword.cloud_notm}} console. Otherwise, [give the users the platform **Viewer** role](#add_users_cli_platform).

4. Assign the users **Viewer** access to the resource group so that they can work with clusters in resource groups other than default. Note that users must have access to the resource group to create clusters.
    1. Click the **IAM services** tile.
    2. In the services drop-down list, select **No service access**.
    3. In the next drop-down list, scope the policy to **All resource groups** or to particular resource groups.
    4. Select **Viewer**.
    5. Click **Add**.

5. In the side panel, review the **Access summary** of your changes, and click **Assign**. If you assigned a service access role, the role might take a couple minutes to sync with your cluster's RBAC.


## Assign {{site.data.keyword.cloud_notm}} IAM roles with the CLI
{: #add_users_cli}

Grant users access to your {{site.data.keyword.openshiftlong_notm}} clusters by assigning {{site.data.keyword.cloud_notm}} IAM platform access and service access roles with the CLI.
{: shortdesc}

Before you begin, complete the following steps.

- Verify that you're assigned the `cluster-admin` {{site.data.keyword.cloud_notm}} IAM platform access role for the {{site.data.keyword.cloud_notm}} account in which you're working.
- Verify that the user is added to the account. If the user is not, invite the user to your account by running `ibmcloud account user-invite <user@email.com>`.
- [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
- Decide whether to assign [platform or service access](/docs/openshift?topic=openshift-access-overview#access_policies) roles. The CLI steps vary depending on which access role you want to assign:
    - [Assign platform access roles from the CLI](#add_users_cli_platform)
    - [Assign service access roles from the CLI](#add_users_cli_service)


### Assigning {{site.data.keyword.cloud_notm}} IAM _platform_ roles from the CLI
{: #add_users_cli_platform}

Create an {{site.data.keyword.cloud_notm}} IAM access policy to set permissions for {{site.data.keyword.openshiftlong_notm}} (**`--service-name containers-kubernetes`**). Scope the access policy based on what you want to assign access to with the following options.

User
:   CLI option: N/A
:   You can assign the policy to an individual or group of users. Place this positional argument immediately following the command.

- Individual user: Enter the email address of the user.
- Access group: Enter the name of the access group of users. You can create an access group with the `ibmcloud iam access-group-create` command. To list available access groups, run `ibmcloud iam access-groups`. To add a user to an access group, run `ibmcloud iam access-group-user-add <access_group_name> <user_email>`.

Resource group
:   ClI option: `--resource-group-name`
:   You can grant a policy for a resource group. If you do not specify a resource group or a specific cluster ID, the policy applies to all clusters for all resource groups. To list available resource groups, run `ibmcloud resource groups`.

Cluster
:   ClI option: `--service-instance`
:   You can limit the policy to a single cluster. To list your cluster IDs, run `ibmcloud oc cluster ls`. Note that if you assign a user the **Administrator** platform access role for only one cluster, you must also assign the user the **Viewer** platform access role for all clusters in the region within the resource group.

Region
:   ClI option: `--region`
:   You can scope the policy to apply to clusters within a particular region. If you do not specify a region or specific cluster ID, the policy applies to all clusters for all regions. To list available regions, review the [previous region](/docs/openshift?topic=openshift-regions-and-zones#zones-mz) column in the {{site.data.keyword.openshiftlong_notm}} locations table.



Role
:   ClI option: `--role`
:   Choose the [platform access role](/docs/openshift?topic=openshift-access_reference#iam_platform) that you want to assign. Possible values are: `Administrator`, `Operator`, `Editor`, or `Viewer`. 

1. Assign the platform access for the user.

    * Assign an individual user the **Viewer** platform access role to one cluster in the default resource group and US East region:
        ```sh
        ibmcloud iam user-policy-create user@email.com --resource-group-name default --service-name containers-kubernetes --region us-east --service-instance clusterID-1111aa2b2bb22bb3333c3c4444dd4ee5 --roles Viewer
        ```
        {: pre}
        
    *  Assign an individual user **Administrator** platform access to all clusters in a `HR` resource group:
        ```sh
        ibmcloud iam user-policy-create user@email.com --resource-group-name HR --service-name containers-kubernetes [--region <region>] --roles Administrator
        ```
        {: pre}

    *  Assign an `auditors` group of users the **Viewer** platform access role to all clusters in all resource groups:
        ```sh
        ibmcloud iam access-group-policy-create auditors --service-name containers-kubernetes --roles Viewer
        ```
        {: pre}

2. Assign the users **Viewer** access to the resource group so that they can work with clusters in resource groups other than default. Note that users must have access to the resource group to create clusters. You can find the resource group ID by running `ibmcloud resource group <resource_group_name> --id`.
    * For individual users:
        ```sh
        ibmcloud iam user-policy-create <user@email.com> --resource-type resource-group --resource <resource_group_ID> --roles Viewer
        ```
        {: pre}

    * For access groups:
        ```sh
        ibmcloud iam access-group-policy-create <access_group> --resource-type resource-group --resource <resource_group_ID> --roles Viewer
        ```
        {: pre}

3. Verify that the user or access group has the assigned platform access role.
    * For individual users:
        ```sh
        ibmcloud iam user-policies <user@email.com>
        ```
        {: pre}

    * For access groups:
        ```sh
        ibmcloud iam access-group-policies <access_group>
        ```
        {: pre}


### Assigning {{site.data.keyword.cloud_notm}} IAM _service_ roles from the CLI:**
{: #add_users_cli_service}


You cannot scope {{site.data.keyword.cloud_notm}} IAM service access roles to an IAM access group because the roles are not synced to the RBAC roles within the cluster. If you want to scope RBAC roles to a group of users, you must [manually set up groups of users](https://docs.openshift.com/container-platform/4.7/authentication/understanding-authentication.html){: external} in your cluster instead of using IAM access groups. You can still manage individual users and service accounts with IAM service access roles. You can also still scope IAM platform access roles to IAM access groups to control actions like ordering worker nodes, because platform access roles are never synced to RBAC roles.
{: note}



1. Get the user information for the individual user that you want to assign the service access role to.

    1. Get your **Account ID**.
        ```sh
        ibmcloud account show
        ```
        {: pre}

    2. For individual users, get the user's **`userID`** and **`ibmUniqueId`**.
        ```sh
        ibmcloud account users --account-id <account_ID> --output JSON
        ```
        {: pre}

2. Create a `policy.json` file that scopes the service access role to a Kubernetes namespace in your cluster.

    ```json
    {
        "subjects": [
            {
                "attributes": [
                    {
                        "name": "(iam_id)",
                        "value": "<user_ID>"
                    }
                ]
            }
        ],
        "roles": [
            {
                "role_id": "crn:v1:bluemix:public:iam::::serviceRole:<(Manager|Writer|Reader)>"
            }
        ],
        "resources": [
            {
                "attributes": [
                    {
                        "name": "accountId",
                        "value": "<account_ID>"
                    },
                    {
                        "name": "serviceName",
                        "value": "containers-kubernetes"
                    },
                    {
                        "name": "serviceInstance",
                        "value": "<cluster_ID1,cluster_ID2>"
                    },
                    {
                        "name": "namespace",
                        "value": "<namespace_name>"
                    }
                ]
            }
        ]
    }
    ```
    {: codeblock}
    
    | Component | Description |
    | --- | --- |
    | `subjects.attributes` | Enter the {{site.data.keyword.cloud_notm}} IAM details for the individual user or access group that you previously retrieved. \n * For individual users, set `iam_id` for the `name` field. Enter the previously retrieved `ibmUniqueId` for the `value` field. |
    | `roles.role_id` | Choose the [IAM service access role](/docs/openshift?topic=openshift-access_reference#service) that you want to assign. Possible values are: \n * `crn:v1:bluemix:public:iam::::serviceRole:Manager` \n * `crn:v1:bluemix:public:iam::::serviceRole:Writer` \n * `crn:v1:bluemix:public:iam::::serviceRole:Reader` |
    | `resources.attributes` | Configure the scope of the policy to your account, cluster, and namespace. Leave the `"name"` fields as given in the example, and enter certain `"value"` fields as follows. \n * For `"accountId"`: Enter your {{site.data.keyword.cloud_notm}} account ID that you previously retrieved. \n * For `"serviceName"`: Leave the service name as given: `containers-kubernetes`. \n * For `"serviceInstance"`: Enter your cluster ID. For multiple clusters, separate with a comma. To get your cluster ID, run `ibmcloud oc cluster ls`. \n * For `"namespace"`: Enter a Kubernetes namespace in your cluster. To list the namespaces in your cluster, run `oc get namespaces`.  \n \n To assign the access policy to all namespaces in a cluster, remove the entire `{"name": "namespace", "value": "<namespace_name"}` entry. |
    {: caption="Table 1. Understanding options for service access role policy" caption-side="top"}

3. Apply the {{site.data.keyword.cloud_notm}} IAM policy to an individual user.
    * For individual users
          ```sh
          ibmcloud iam user-policy-create <user@email.com> --file <filepath>/policy.json
          ```
          {: pre}

4. If you assigned only service access roles to users, the users must be given the cluster master URL to open the {{site.data.keyword.openshiftshort}} web console from their browser at `https://<master_URL>/console` instead of the {{site.data.keyword.cloud_notm}} console. Otherwise, [give the users the platform **Viewer** role](#add_users_cli_platform).

5. **Optional**: After a couple minutes, verify that the user is added to the corresponding [RBAC role binding or cluster role binding](#checking-rbac). 



## Understanding RBAC permissions
{: #understand-rbac}

RBAC roles and cluster roles define a set of permissions for how users can interact with Kubernetes resources in your cluster.
{: shortdesc}

With {{site.data.keyword.cloud_notm}} IAM, you can automatically manage RBAC from {{site.data.keyword.cloud_notm}}, by assigning users [service access roles](#add_users). You might want a deeper understanding of RBAC to customize access for resources within your cluster, like service accounts.
{: note}

**What are the types of RBAC roles?**

* A Kubernetes _role_ is scoped to resources within a specific namespace, such as a deployment or service.
* A Kubernetes _cluster role_ is scoped to cluster-wide resources, such as worker nodes, or to namespace-scoped resources that can be found in each namespace, like pods.

**What are RBAC role bindings and cluster role bindings?**

Role bindings apply RBAC roles or cluster roles to a specific namespace. When you use a role binding to apply a role, you give a user access to a specific resource in a specific namespace. When you use a role binding to apply a cluster role, you give a user access to namespace-scoped resources that can be found in each namespace, like pods, but only within a specific namespace.

Cluster role bindings apply RBAC cluster roles to all namespaces in the cluster. When you use a cluster role binding to apply a cluster role, you give a user access to cluster-wide resources, like worker nodes, or to namespace-scoped resources in every namespace, like pods.

**What do these roles look like in my cluster?**

If you want users to be able to interact with Kubernetes resources from within a cluster, you must assign user access to one or more namespaces through [{{site.data.keyword.cloud_notm}} IAM service access roles](#add_users). Every user who is assigned a service access role is automatically assigned a corresponding RBAC cluster role. These RBAC cluster roles are predefined and permit users to interact with Kubernetes resources in your cluster. Additionally, a role binding is created to apply the cluster role to a specific namespace, or a cluster role binding is created to apply the cluster role to all namespaces.

To learn more about the actions permitted by each RBAC role, check out the [{{site.data.keyword.cloud_notm}} IAM service access roles](/docs/openshift?topic=openshift-access_reference#service) reference topic. To see the permissions that are granted by each RBAC role to individual Kubernetes resources, check out [Kubernetes resource permissions per RBAC role](/docs/openshift?topic=openshift-access_reference#rbac_ref).

All users of an {{site.data.keyword.openshiftshort}} cluster are added to the following {{site.data.keyword.openshiftshort}} RBAC groups by cluster version. <img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> Version 3 clusters: `basic-users` and `self-provisioners`. <img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> Version 4 clusters: `basic-users`.
{: note}

**Can I create custom roles or cluster roles?**

The `view`, `edit`, `admin`, and `cluster-admin` cluster roles are predefined roles that are automatically created when you assign a user the corresponding {{site.data.keyword.cloud_notm}} IAM service access role. To grant other Kubernetes permissions, you can [create custom RBAC permissions](#rbac). Custom RBAC roles are in addition to and do not change or override any RBAC roles that you might have assigned with service access roles. Note that to create custom RBAC permissions, you must have the IAM **Manager** service access role that gives you the `cluster-admin` Kubernetes RBAC role. However, the other users do not need an IAM service access role if you manage your own custom Kubernetes RBAC roles.

Making your own custom RBAC policies? Be sure not to edit the existing IBM role bindings that are in the cluster, or name new role bindings with the same name. Any changes to IBM-provided RBAC role bindings are overwritten periodically. Instead, create your own role bindings.
{: tip}

**Can I assign custom RBAC roles to groups of users?**

You can [manually assign users to groups](https://docs.openshift.com/container-platform/4.7/authentication/understanding-authentication.html){: external} in your cluster, and then assign roles to the group. However, a known issue is that you cannot use {{site.data.keyword.cloud_notm}} IAM access groups.


**When do I need to use cluster role bindings and role bindings that are not tied to the {{site.data.keyword.cloud_notm}} IAM permissions that I set?**

You might want to authorize who can create and update pods in your cluster. With [security context constraints (SCCs)](/docs/openshift?topic=openshift-openshift_scc#oc_sccs), you can use existing cluster role bindings that come with your cluster, or create your own.

You might also want to integrate add-ons to your cluster. For example, when you [set up Helm in your cluster](/docs/containers?topic=containers-helm)


## Creating custom RBAC permissions for users, groups, or service accounts
{: #rbac}

The `view`, `edit`, `admin`, and `cluster-admin` cluster roles are automatically created when you assign the corresponding {{site.data.keyword.cloud_notm}} IAM service access role. Do you need your cluster access policies to be more granular than these predefined permissions allow? No problem! You can create custom RBAC roles and cluster roles.
{: shortdesc}

You can assign custom RBAC roles and cluster roles to individual users, groups of users, or service accounts. When a binding is created for a group, it affects any user that is added or removed from that group. When you add users to a group, they get the access rights of the group in addition to any individual access rights that you grant them. If they are removed, their access is revoked. Note that you can't add service accounts to access groups.

If you want to assign access to a process that runs in pods, such as a continuous delivery toolchain, you can use [Kubernetes `ServiceAccounts`](https://kubernetes.io/docs/reference/access-authn-authz/service-accounts-admin/){: external}. To follow a tutorial that demonstrates how to set up service accounts for Travis and Jenkins and to assign custom RBAC roles to the service accounts, see the blog post [Kubernetes `ServiceAccounts` for use in automated systems](https://medium.com/@jakekitchener/kubernetes-serviceaccounts-for-use-in-automated-systems-515297974982){: external}.

To prevent breaking changes, do not change the predefined `view`, `edit`, `admin`, and `cluster-admin` cluster roles. Custom RBAC roles are in addition to and do not change or override any RBAC roles that you might have assigned with {{site.data.keyword.cloud_notm}} IAM service access roles.
{: important}

**Do I create a role or a cluster role? Do I apply it with a role binding or a cluster role binding?**

- **Namespace access**: To allow a user, access group, or service account to access a resource within a specific namespace, choose one of the following combinations:
    - Create a role, and apply it with a role binding. This option is useful for controlling access to a unique resource that exists only in one namespace, like an app deployment.
    - Create a cluster role, and apply it with a role binding. This option is useful for controlling access to general resources in one namespace, like pods.
- **Cluster-wide access**: To allow a user or an access group to access cluster-wide resources or resources in all namespaces, create a cluster role, and apply it with a cluster role binding. This option is useful for controlling access to resources that are not scoped to namespaces, like worker nodes, or resources in all namespaces in your cluster, like pods in each namespace.

**Before you begin**:

- Target the [Kubernetes CLI](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) to your cluster.
- Ensure you that have the [**Manager** {{site.data.keyword.cloud_notm}} IAM service access role](#add_users) for all namespaces.
- To assign access to individual users or users in an access group, ensure that the user or group has been assigned at least one [{{site.data.keyword.cloud_notm}} IAM platform access role](#add_users) at the {{site.data.keyword.openshiftlong_notm}} service level.

To create custom RBAC permissions,

1. Create the role or cluster role with the access that you want to assign.

    1. Create a `.yaml` file to define the role or cluster role.

        ```yaml
        kind: Role
        apiVersion: rbac.authorization.k8s.io/v1
        metadata:
          namespace: default
          name: my_role
        rules:
        - apiGroups: [""]
          resources: ["pods"]
          verbs: ["get", "watch", "list"]
        - apiGroups: ["apps", "extensions"]
          resources: ["daemonsets", "deployments"]
          verbs: ["get", "list", "watch", "create", "update", "patch", "delete"]
        ```
        {: codeblock}
        
        | Parameter | Description |
        | --- | --- |
        | `kind` | Use `Role` to grant access to resources within a specific namespace. Use `ClusterRole` to grant access to cluster-wide resources such as worker nodes, or to namespace-scoped resources such as pods in all namespaces. |
        | `apiVersion` |  * For clusters that run Kubernetes 1.8 or later, use `rbac.authorization.k8s.io/v1`. \n * For earlier versions, use `apiVersion: rbac.authorization.k8s.io/v1beta1`. |
        | `metadata.namespace` | For kind `Role` only: Specify the Kubernetes namespace to which access is granted. |
        | `metadata.name` | Name the role or cluster role. |
        | `rules.apiGroups` | Specify the Kubernetes [API groups](https://kubernetes.io/docs/reference/using-api/api-overview/#api-groups){: external} that you want users to be able to interact with, such as `"apps"`, `"batch"`, or `"extensions"`. For access to the core API group at REST path `api/v1`, leave the group blank: `[""]`. |
        | `rules.resources` | Specify the Kubernetes [resource types](https://kubernetes.io/docs/reference/kubectl/cheatsheet/){: external} to which you want to grant access, such as `"daemonsets"`, `"deployments"`, `"events"`, or `"ingresses"`. If you specify `"nodes"`, then the kind must be `ClusterRole`. |
        | `rules.verbs` | Specify the types of [actions](https://kubectl.docs.kubernetes.io/){: external} that you want users to be able to do, such as `"get"`, `"list"`, `"describe"`, `"create"`, or `"delete"`. |
        {: caption="Table 3. Understanding the YAML parameters" caption-side="top"}

    2. Create the role or cluster role in your cluster.

        ```sh
        oc apply -f my_role.yaml
        ```
        {: pre}

    3. Verify that the role or cluster role is created.
        * Role:
            ```sh
            oc get roles -n <namespace>
            ```
            {: pre}

        * Cluster role:
            ```sh
            oc get clusterroles
            ```
            {: pre}

2. Bind users to the role or cluster role.

    1. Create a `.yaml` file to bind users to your role or cluster role. Note the unique URL to use for each subject's name.

        ```yaml
        kind: RoleBinding
        apiVersion: rbac.authorization.k8s.io/v1
        metadata:
          name: my_role_binding
          namespace: default
        subjects:
        - kind: User
          name: IAM#user1@example.com
          apiGroup: rbac.authorization.k8s.io
        - kind: Group
          name: team1
          apiGroup: rbac.authorization.k8s.io
        - kind: ServiceAccount
          name: <service_account_name>
          namespace: <kubernetes_namespace>
        roleRef:
          kind: Role
          name: my_role
          apiGroup: rbac.authorization.k8s.io
        ```
        {: codeblock}

        | Parameter | Description |
        | --- | --- |
        | `kind` | * Specify `RoleBinding` for a namespace-specific `Role` or `ClusterRole`. \n * Specify `ClusterRoleBinding` for a cluster-wide `ClusterRole`. |
        | `apiVersion` |  * For clusters that run Kubernetes 1.8 or later, use `rbac.authorization.k8s.io/v1`. \n * For earlier versions, use `apiVersion: rbac.authorization.k8s.io/v1beta1`. |
        | `metadata.namespace` | * For kind `RoleBinding`: Specify the Kubernetes namespace to which access is granted. \n * For kind `ClusterRoleBinding`: Don't use the `namespace` field. |
        | `metadata.name` | Name the role binding or cluster role binding. |
        | `subjects.kind` | Specify the kind as one of the following: \n * `User`: Bind the RBAC role or cluster role to an individual user in your account.  \n * `Group`: Bind the RBAC role or cluster role to an [{{site.data.keyword.cloud_notm}} IAM access group](/docs/account?topic=account-groups#groups) in your account. \n * `ServiceAccount`: Bind the RBAC role or cluster role to a service account in a namespace in your cluster. |
        | `subjects.name` | * For `User`: Append the individual user's email address to `IAM#` as follows: `IAM#user@email.com`. \n * For `Group`: Specify the name of the [{{site.data.keyword.cloud_notm}} IAM access group](/docs/account?topic=account-groups#groups) in your account. \n * For `ServiceAccount`: Specify the service account name. |
        | `subjects.apiGroup` | * For `User` or `Group`: Use `rbac.authorization.k8s.io`. \n * For `ServiceAccount`: Don't include this field. |
        | `subjects.namespace` | For `ServiceAccount` only: Specify the name of the Kubernetes namespace that the service account is deployed to. |
        | `roleRef.kind` | Enter the same value as the `kind` in the role `.yaml` file: `Role` or `ClusterRole`. |
        | `roleRef.name` | Enter the name of the role `.yaml` file. |
        | `roleRef.apiGroup` | Use `rbac.authorization.k8s.io`. |
        {: caption="Table 3. Understanding the YAML parameters" caption-side="top"}

    2. Create the role binding or cluster role binding resource in your cluster.

        ```sh
        oc apply -f my_role_binding.yaml
        ```
        {: pre}

    3. Verify that the binding is created.

        ```sh
        oc get rolebinding -n <namespace>
        ```
        {: pre}

3. Optional: To enforce the same level of user access in other namespaces, you can copy the role bindings for those roles or cluster roles to other namespaces.
    1. Copy the role binding from one namespace to another namespace.
        ```sh
        oc get rolebinding <role_binding_name> -o yaml | sed 's/<namespace_1>/<namespace_2>/g' | oc -n <namespace_2> create -f -
        ```
        {: pre}

        For example, copy the `custom-role` role binding from the `default` namespace to the `testns` namespace.
        ```sh
        oc get rolebinding custom-role -o yaml | sed 's/default/testns/g' | oc -n testns create -f -
        ```
        {: pre}

    2. Verify that the role binding is copied. If you added an {{site.data.keyword.cloud_notm}} IAM access group to the role binding, each user in that group is added individually, not as an access group ID.
        ```sh
        oc get rolebinding -n <namespace_2>
        ```
        {: pre}

Now that you created and bound a custom Kubernetes RBAC role or cluster role, follow up with users. Ask them to test an action that they have permission to complete due to the role, such as deleting a pod.


## Extending existing permissions by aggregating cluster roles
{: #rbac_aggregate}

You can extend your users' existing permissions by aggregating, or combining, cluster roles with other cluster roles. When you assign a user an {{site.data.keyword.cloud_notm}} service access role, the user is added to a [corresponding Kubernetes RBAC cluster role](/docs/openshift?topic=openshift-access_reference#service). However, you might want to allow certain users to perform additional operations.
{: shortdesc}

For example, a user with the namespace-scoped `admin` cluster role cannot use the `oc top pods` command to view pod metrics for all the pods in the namespace. You might aggregate a cluster role so that users in the `admin` cluster role are authorized to run the `top pods` command. For more information, [see the Kubernetes docs](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#aggregated-clusterroles){: external}.

**What are some common operations that I might want to extend permissions for a default cluster role?**

Review [the operations that each default RBAC cluster role permits](/docs/openshift?topic=openshift-access_reference#rbac_ref) to get a good idea of what your users can do, and then compare the permitted operations to what you want them to be able to do.

If your users in the same cluster role encounter errors similar to the following for the same type of operation, you might want to extend the cluster role to include this operation.

```sh
Error from server (Forbidden): pods.metrics.k8s.io is forbidden: User "IAM#myname@example.com" cannot list resource "pods" in API group "metrics.k8s.io" in the namespace "mynamespace"
```
{: screen}

**To aggregate cluster roles**:

Before you begin: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Create a cluster role YAML file. In the `labels` section, specify the existing cluster role that you want to aggregate permissions to. The following example extends the predefined `admin` cluster role to allow users to run `oc top pods`. For more examples, [see the Kubernetes docs](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#aggregated-clusterroles){: external}.
    ```yaml
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRole
    metadata:
      name: view-pod-metrics
      labels:
        rbac.authorization.k8s.io/aggregate-to-admin: "true"
    rules:
    - apiGroups:
      - "metrics.k8s.io"
      resources:
      - pods
      verbs:
      - list
    ```
    {: codeblock}

    | Parameter | Description |
    | --- | --- |
    | `metadata.name` | Enter a name for the cluster role. **Do not** use the predefined cluster role names: `view`, `edit`, `admin`, and `cluster-admin`. |
    | `metadata.labels` | Add a label that matches the cluster role that you want to aggregate to in the format `rbac.authorization.k8s.io/aggregate-to-<cluster_role>: "true"`. The labels for the predefined cluster roles are as follows. \n * IAM **Manager** service access role, scoped to a namespace: `rbac.authorization.k8s.io/aggregate-to-admin: "true"` \n * IAM **Writer** service access role: `rbac.authorization.k8s.io/aggregate-to-edit: "true"` \n * IAM **Reader** service access role: `rbac.authorization.k8s.io/aggregate-to-view: "true"` |
    | `rules.apiGroups` | Specify the Kubernetes [API groups](https://kubernetes.io/docs/reference/using-api/api-overview/#api-groups){: external} that you want users to be able to interact with, such as `"apps"`, `"batch"`, or `"extensions"`. For access to the core API group at REST path `api/v1`, leave the group blank: `[""]`. |
    | `rules.resources` | Specify the Kubernetes [resource types](https://kubernetes.io/docs/reference/kubectl/cheatsheet/){: external} to which you want to grant access, such as `"daemonsets"`, `"deployments"`, `"events"`, or `"ingresses"`. |
    | `rules.verbs` | Specify the types of [actions](https://kubectl.docs.kubernetes.io/){: external} that you want users to be able to do, such as `"get"`, `"list"`, `"describe"`, `"create"`, or `"delete"`. |
    {: caption="Table 4. Understanding the YAML parameters" caption-side="top"}

2. Create the cluster role in your cluster. Any users that have a role binding to the `admin` cluster role now have the additional permissions from the `view-pod-metrics` cluster role.
    ```sh
    oc apply -f <cluster_role_file.yaml>
    ```
    {: pre}

3. Follow up with users that have the `admin` cluster role. Ask them to [refresh their cluster configuration](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) and test the action, such as `oc top pods`.


## Checking user permissions
{: #checking-perms}

Before you complete a task, you might want to check that you have the appropriate permissions in {{site.data.keyword.cloud}} Identity and Access Management (IAM).
{: shortdesc}

### Checking IAM platform and service access roles
{: #checking-iam}

Check your access policies that are assigned by IAM platform and service access roles.
{: shortdesc}

#### Checking IAM platform and service access roles from the UI
{: #checking-iam-ui}

1. Log in to the [{{site.data.keyword.cloud_notm}} IAM console](https://cloud.ibm.com/iam){: external}.
2. From the navigation menu, click the **Users** tab.
3. In the table, click the user with the tag `self` for yourself or the user that you want to check.
4. Click the **Access policies** tab.
5. Review the **Resource attributes** column for a short description of the access. Click the number tag to view all the allowed actions for the role.

    Service access roles are synchronized with Kubernetes RBAC roles within your cluster. If you have a service access role, you might want to [verify your RBAC role](#checking-rbac), too.
    {: tip}

6. To review what the roles and allowed actions permit, see the following topics.
    * [IAM roles and actions](/docs/account?topic=account-iam-service-roles-actions)
    * [{{site.data.keyword.openshiftlong_notm}} user access permissions](/docs/containers?topic=containers-access_reference)
    * <img src="images/icon-satellite.svg" alt="{{site.data.keyword.satelliteshort}} infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **Satellite-only**: [{{site.data.keyword.satelliteshort}} IAM platform and service roles](/docs/satellite?topic=satellite-iam#iam-roles)
7. To change or assign new access policies, see [Assigning {{site.data.keyword.openshiftlong_notm}} roles](#add_users) or [Assigning {{site.data.keyword.satelliteshort}} access](/docs/satellite?topic=satellite-iam#iam-assign).


#### Checking IAM platform and service access roles from the CLI
{: #checking-iam-cli}

1. Log in to your {{site.data.keyword.cloud_notm}} account. If you have a federated ID, include the `--sso` flag.
    ```sh
    ibmcloud login -r [--sso]
    ```
    {: pre}

2. Find the **User ID** of the user whose permissions you want to check.
    ```sh
    ibmcloud account users
    ```
    {: pre}

3. Check the IAM access policies of the user.
    ```sh
    ibmcloud iam user-policies <user_id>
    ```
    {: pre}

    Service access roles are synchronized with Kubernetes RBAC roles within your cluster. If you have a service access role, you might want to [verify your RBAC role](#checking-rbac), too.
    {: tip}

4. To review what the roles and allowed actions permit, see the following topics.
    * [IAM roles and actions](/docs/account?topic=account-iam-service-roles-actions)
    * [{{site.data.keyword.openshiftlong_notm}} user access permissions](/docs/containers?topic=containers-access_reference)
    * <img src="images/icon-satellite.svg" alt="{{site.data.keyword.satelliteshort}} infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **Satellite-only**: [{{site.data.keyword.satelliteshort}} IAM platform and service roles](/docs/satellite?topic=satellite-iam#iam-roles)
5. To change or assign new access policies, see [Assigning {{site.data.keyword.openshiftlong_notm}} roles](#add_users_cli) or [Assigning {{site.data.keyword.satelliteshort}} access](/docs/satellite?topic=satellite-iam#iam-assign-cli).

### Checking RBAC roles
{: #checking-rbac}

Verify your custom RBAC or synchronized IAM service access to RBAC roles in your {{site.data.keyword.openshiftlong_notm}} cluster.
{: shortdesc} 

#### Checking RBAC roles from the UI
{: #checking-rbac-ui}

1. Log in to the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}.
2. Click the cluster with the RBAC roles that you want to check.
5. Click the **{{site.data.keyword.openshiftshort}} web console**.

    If you have a private network only cluster, you might not be able to open the dashboard unless you are on a VPN. See [Accessing clusters through the private cloud service endpoint](/docs/openshift?topic=openshift-access_cluster#access_private_se) or for {{site.data.keyword.satelliteshort}}, [Accessing {{site.data.keyword.openshiftshort}} clusters on {{site.data.keyword.satelliteshort}}](/docs/openshift?topic=openshift-access_cluster#access_cluster_sat).
    {: note}

6. From the **Administrator** perspective, click **User Management > Users**.
7. Click the user that you want to check, then click **Role Bindings**.

#### Checking RBAC roles with the CLI
{: #checking-rbac-cli}

1. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
2. Check that the user is added to the RBAC role. Users are not added to a role binding if they have a higher permission. For example, if users have a cluster role and are in a cluster role binding, they are not added to each individual namespace role binding as well.

    You must be a cluster administrator (**Manager** service access role in all namespaces) to check role bindings and cluster role bindings.
    {: note}

    * Reader:
        ```sh
        oc get rolebinding ibm-view -o yaml -n <namespace>
        ```
        {: pre}

    * Writer:
        ```sh
        oc get rolebinding ibm-edit -o yaml -n <namespace>
        ```
        {: pre}

    * Manager, scoped to a namespace:
        ```sh
        oc get rolebinding ibm-operate -o yaml -n <namespace>
        ```
        {: pre}

    * Manager, all namespaces:
        ```sh
        oc get clusterrolebinding ibm-admin -o yaml
        ```
        {: pre}

Example output

If you assign user `user@email.com` and access group `team1` the **Reader** service access role, and then run `oc get rolebinding ibm-view -o yaml -n default`, you get the following example output.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  creationTimestamp: 2018-05-23T14:34:24Z
  name: ibm-view
  namespace: default
  resourceVersion: "8192510"
  selfLink: /apis/rbac.authorization.k8s.io/v1/namespaces/default/rolebindings/ibm-view
  uid: 63f62887-5e96-11e8-8a75-b229c11ba64a
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: view
subjects:
- apiGroup: rbac.authorization.k8s.io
  kind: User
  name: IAM#user@email.com
- apiGroup: rbac.authorization.k8s.io
  kind: group
  name: team1
```
{: screen}

### Checking infrastructure roles
{: #checking-infra}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) Check your {{site.data.keyword.cloud_notm}} classic infrastructure roles. For more information, see [Understanding access to the infrastructure portfolio](/docs/openshift?topic=openshift-access-creds#understand_infra).
{: shortdesc}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC infrastructure permissions are managed with [IAM platform and service access roles](#checking-iam).
{: note}

If you are an administrator for the region and resource group, you might want to [check if the user's credentials are used for infrastructure permissions](#removing_check_infra), especially before removing the user.
{: tip}

#### Checking infrastructure roles from the UI
{: #checking-infra-ui}

1. Log in to the [{{site.data.keyword.cloud_notm}} IAM console](https://cloud.ibm.com/iam){: external}.
2. From the navigation menu, click the **Users** tab.
3. In the table, click the user with the tag `self` for yourself or the user that you want to check.
4. Click the **Classic infrastructure** tab.
5. Review each of the classic infrastructure tabs.
    1. **Permissions**: Expand the categories to review the permissions that the user has.
    2. **Devices**: Review the devices that the user has permissions to. A common issue is when a user has administrator permissions but the `Enable future access` was not checked so whenever a new device is ordered, the user cannot administer the device.
    3. **VPN subnets**: The subnets permission is important if the user must administer the subnets for the cluster.
6. To review what the roles and allowed actions permit, see the following topics.
    * [Account classic infrastructure permissions](/docs/account?topic=account-infrapermission)
    * [{{site.data.keyword.openshiftlong_notm}} classic infrastructure roles](/docs/openshift?topic=openshift-access_reference#infra)
7. To change or assign new access policies, see [Customizing infrastructure permissions](/docs/openshift?topic=openshift-access-creds#infra_access).

#### Checking infrastructure roles with the CLI
{: #checking-infra-cli}

1. Log in to your {{site.data.keyword.cloud_notm}} account. If you have a federated ID, include the `--sso` flag.
    ```sh
    ibmcloud login -r [--sso]
    ```
    {: pre}

2. List the users in your classic infrastructure account and note the **id** of the user whose credentials are set manually or by the API key.
    ```sh
    ibmcloud sl user list
    ```
    {: pre}

3. List the current classic infrastructure permissions that the user has.
    ```sh
    ibmcloud sl user permissions <user_id>
    ```
    {: pre}

4. To review what the roles and allowed actions permit, see the following topics.
    * [Account classic infrastructure permissions](/docs/account?topic=account-infrapermission)
    * [{{site.data.keyword.openshiftlong_notm}} classic infrastructure roles](/docs/openshift?topic=openshift-access_reference#infra)
5. To change or assign new access policies, see [Customizing infrastructure permissions](/docs/openshift?topic=openshift-access-creds#infra_access).



### Checking other cloud infrastructure provider roles
{: #checking-infra-providers}

<img src="images/icon-satellite.svg" alt="{{site.data.keyword.satelliteshort}} infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **Satellite-only**: If your cluster runs in a {{site.data.keyword.satelliteshort}} location, you use infrastructure that comes from other on-prem or cloud providers. Consult their product documentation to make sure that you have the correct permissions to create infrastructure resources.
{: shortdesc}

Also, see the following related topics.

* [Common permissions in other cloud providers](/docs/satellite?topic=satellite-iam#permissions-other-clouds)



## Removing user permissions
{: #removing}

If a user no longer needs specific access permissions, or if the user is leaving your organization, the {{site.data.keyword.cloud_notm}} account owner can remove that user's permissions.
{: shortdesc}

### Checking if the user's credentials are used for infrastructure permissions
{: #removing_check_infra}

Before you remove a user's specific access permissions or remove a user from your account completely, ensure that the user's infrastructure credentials are not used to set the API key or for the `ibmcloud oc credential set` command. Otherwise, the other users in the account might lose access to the IBM Cloud infrastructure portal and infrastructure-related commands might fail.
{: shortdesc}

To avoid this issue for future users, consider using a functional ID user for the API key owner instead of a personal user. In case the person leaves the team, the functional ID user remains the API key owner.
{: tip}

1. Target your CLI context to a region and resource group where you have clusters.
    ```sh
    ibmcloud target -g <resource_group_name> -r <region>
    ```
    {: pre}

2. Check the owner of the API key or infrastructure credentials set for that region and resource group.
    * If you use the [API key to access the IBM Cloud infrastructure portfolio](/docs/openshift?topic=openshift-access-creds#default_account):
        ```sh
        ibmcloud oc api-key info --cluster <cluster_name_or_id>
        ```
        {: pre}

    * If you set [infrastructure credentials to access the IBM Cloud infrastructure portfolio](/docs/openshift?topic=openshift-access-creds#credentials):
        ```sh
        ibmcloud oc credential get --region <region>
        ```
        {: pre}

3. **API key**: If the user's username is returned, use another user's credentials to set the API key.
    1. [Invite a functional ID user](/docs/account?topic=account-iamuserinv) to your {{site.data.keyword.cloud_notm}} account to use to set the API key infrastructure credentials, instead of a personal user. In case a person leaves the team, the functional ID user remains the API key owner.
    2. [Ensure that the functional ID user who sets the API key has the correct permissions](/docs/openshift?topic=openshift-access-creds#owner_permissions).
    3. Log in as the functional ID.
        ```sh
        ibmcloud login
        ```
        {: pre}

    4. Change the infrastructure credentials to the functional ID user.
        ```sh
        ibmcloud oc api-key reset --region <region>
        ```
        {: pre}

    5. Refresh the clusters in the region to pick up on the new API key configuration.
        ```sh
        ibmcloud oc cluster master refresh -c <cluster_name_or_ID>
        ```
        {: pre}

4. **Infrastructure account**: If the user's username is returned as the owner of the infrastructure account, migrate your existing clusters to a different infrastructure account before removing the user. For each cluster that the user created, follow these steps:
    1. Check which infrastructure account the user used to provision the cluster.
        1. In the **Worker Nodes** tab, select a worker node and note its **ID**.
        2. Open the menu ![Menu icon](../icons/icon_hamburger.svg "Menu icon") and click **Classic Infrastructure**.
        3. From the infrastructure navigation pane, click **Devices > Device List**.
        4. Search for the worker node ID that you previously noted.
        5. If you do not find the worker node ID, the worker node is not provisioned into this infrastructure account. Switch to a different infrastructure account and try again.
    2. Determine what happens to the infrastructure account that the user used to provision the clusters after the user leaves.
        * If the user does not own the infrastructure account, then other users have access to this infrastructure account and it persists after the user leaves. You can continue to work with these clusters in your account. Make sure that at least one other user has the [**Administrator** platform access role](#add_users) for the clusters.
        * If the user owns the infrastructure account, then the infrastructure account is deleted when the user leaves. You cannot continue to work with these clusters. To prevent the cluster from becoming orphaned, the user must delete the clusters before the user leaves. If the user has left but the clusters were not deleted, you must use the `ibmcloud oc credential set` command to change your infrastructure credentials to the account that the cluster worker nodes are provisioned in, and delete the cluster. For more information, see [Unable to modify or delete infrastructure in an orphaned cluster](/docs/openshift?topic=openshift-worker_infra_errors#orphaned).
5. Repeat these steps for each combination of resource groups and regions where you have clusters.

### Removing a user from your account
{: #remove_user}

If a user in your account is leaving your organization, you must remove permissions for that user carefully to ensure that you do not orphan clusters or other resources. After you remove permissions, you can remove the user from your {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

1. [Check that the user's infrastructure credentials are not used](#removing_check_infra) for any {{site.data.keyword.openshiftlong_notm}} resources.
2. If you have other service instances in your {{site.data.keyword.cloud_notm}} account that the user might have provisioned, check the documentation for those services for any steps that you must complete before you remove the user from the account.
3. [Remove the user from the {{site.data.keyword.cloud_notm}} account](/docs/account?topic=account-remove). When you remove a user, the user's assigned {{site.data.keyword.cloud_notm}} IAM platform access roles, Cloud Foundry roles, and IBM Cloud infrastructure roles are automatically removed.
4. When {{site.data.keyword.cloud_notm}} IAM platform permissions are removed, the user's permissions are also automatically removed from the associated predefined RBAC roles. However, if you created custom RBAC roles or cluster roles, [remove the user from those RBAC role bindings or cluster role bindings](#remove_custom_rbac).

    The {{site.data.keyword.cloud_notm}} IAM permission removal process is asynchronous and can take some time to complete.
    {: note}

5. Optional: If the user had admin access to your cluster, you can [rotate your cluster's certificate authority (CA) certificates](/docs/openshift?topic=openshift-security#cert-rotate).

### Removing specific permissions
{: #remove_permissions}

If you want to remove specific permissions for a user, you can remove individual access policies that have been assigned to the user.
{: shortdesc}

Before you begin, [check that the user's infrastructure credentials are not used](#removing_check_infra) for any {{site.data.keyword.openshiftlong_notm}} resources. After checking, you can remove the following credentials.
* [a user from an access group](/docs/account?topic=account-assign-access-resources)
* [a user's {{site.data.keyword.cloud_notm}} IAM platform and associated RBAC permissions](#remove_iam_rbac)
* [a user's custom RBAC permissions](#remove_custom_rbac)
* [a user's Cloud Foundry permissions](#remove_cloud_foundry)
* [a user's infrastructure permissions](#remove_infra)

#### Remove {{site.data.keyword.cloud_notm}} IAM platform permissions and the associated pre-defined RBAC permissions
{: #remove_iam_rbac}

1. Log in to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external}. From the menu bar, select **Manage > Access (IAM)**.
2. Click the **Users** page, and then click the name of the user that you want to remove permissions from.
3. In the table entry for the user, click the **Actions menu** ![Action menu icon](../icons/action-menu-icon.svg "Action menu icon") **> Remove user**.
4. When {{site.data.keyword.cloud_notm}} IAM platform permissions are removed, the user's permissions are also automatically removed from the associated predefined RBAC roles. To update the RBAC roles with the changes, run `ibmcloud oc cluster config`. However, if you created [custom RBAC roles or cluster roles](#rbac), you must remove the user from the `.yaml` files for those RBAC role bindings or cluster role bindings. See steps to remove custom RBAC permissions in the next section.

#### Remove custom RBAC permissions
{: #remove_custom_rbac}

If you do not need custom RBAC permissions anymore, you can remove them.
{: shortdesc}

1. Open the `.yaml` file for the role binding or cluster role binding that you created.
2. In the `subjects` section, remove the section for the user.
3. Save the file.
4. Apply the changes in the role binding or cluster role binding resource in your cluster.
    ```sh
    oc apply -f my_role_binding.yaml
    ```
    {: pre}

#### Remove Cloud Foundry permissions
{: #remove_cloud_foundry}

To remove all of a user's Cloud Foundry permissions, you can remove the user's organization roles. If you want to remove only a user's ability, for example, to bind services in a cluster, then remove only the user's space roles.
{: shortdesc}

1. Log in to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/). From the menu bar, select **Manage > Access (IAM)**.
2. Click the **Users** page, and then click the name of the user that you want to remove permissions from.
3. Click the **Cloud Foundry access** tab.
    * To remove the user's space role
        1. Expand the table entry for the organization that the space is in.
        2. In the table entry for the space role, click the actions menu and select **Edit space role**.
        3. Delete a role by clicking the close button.
        4. To remove all space roles, select **No space role** in the drop-down list.
        5. Click **Save role**.
    * To remove the user's organization role
        1. In the table entry for the organization role, click the actions menu and select **Edit organization role**.
        2. Delete a role by clicking the close button.
        3. To remove all organization roles, select **No organization role** in the drop-down list.
        4. Click **Save role**.

#### Remove classic infrastructure permissions
{: #remove_infra}

You can remove IBM Cloud infrastructure permissions for a user by using the {{site.data.keyword.cloud_notm}} console.
{: shortdesc}

Classic infrastructure permissions apply only to classic clusters. For VPC clusters, see [Granting user permissions for VPC resources](/docs/vpc?topic=vpc-managing-user-permissions-for-vpc-resources).
{: note}

1. Log in to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external}. From the menu bar, select **Manage > Access (IAM)**.
2. Click the **Users** page, and then click the name of the user that you want to remove permissions from.
3. Click the **Classic infrastructure** tab, then click the **Permissions, Devices, or VPN subnets** tabs.
4. In each tab, deselect specific permissions.
5. To save your changes, click **Set** and **Save**. Permissions are downgraded after a few minutes.




