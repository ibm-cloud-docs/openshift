---

copyright: 
  years: 2024, 2025
lastupdated: "2025-12-05"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, infrastructure, rbac, policy, role-based access control

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Understanding RBAC permissions
{: #understand-rbac}

IAM service access roles correspond to Kubernetes role-based access control (RBAC) within {{site.data.keyword.openshiftlong_notm}} clusters. RBAC roles and cluster roles define a set of permissions for how users can interact with Kubernetes resources in your cluster.
{: shortdesc}

With {{site.data.keyword.cloud_notm}} IAM, you can automatically manage RBAC from {{site.data.keyword.cloud_notm}}, by assigning users IAM service access roles. You might want a deeper understanding of RBAC to customize access for resources within your cluster, like service accounts.



All users of a {{site.data.keyword.redhat_openshift_notm}} cluster are added to the `basic-users` RBAC group.
{: note}



- {{site.data.keyword.cloud_notm}} IAM roles can't be assigned to a service account. Instead, you can directly [assign RBAC roles to service accounts](#rbac).
- Users must run the `ibmcloud ks cluster config` command for their role changes to take effect.



## What are the types of RBAC roles?
{: #rbac-types}

* A Kubernetes _role_ is scoped to resources within a specific namespace, such as a deployment or service.
* A Kubernetes _cluster role_ is scoped to cluster-wide resources, such as worker nodes, or to namespace-scoped resources that can be found in each namespace, like pods.

## What are RBAC role bindings and cluster role bindings?
{: #what-is-rbac}

Role bindings apply RBAC roles or cluster roles to a specific namespace. When you use a role binding to apply a role, you give a user access to a specific resource in a specific namespace. When you use a role binding to apply a cluster role, you give a user access to namespace-scoped resources that can be found in each namespace, like pods, but only within a specific namespace.

Cluster role bindings apply RBAC cluster roles to all namespaces in the cluster. When you use a cluster role binding to apply a cluster role, you give a user access to cluster-wide resources, like worker nodes, or to namespace-scoped resources in every namespace, like pods.

## What do these roles look like in my cluster?
{: #what-do-roles-look-like}

If you want users to be able to interact with Kubernetes resources from within a cluster, you must assign user access to one or more namespaces through [{{site.data.keyword.cloud_notm}} IAM service access roles](/docs/openshift?topic=openshift-iam-platform-access-roles). Every user who is assigned a service access role is automatically assigned a corresponding RBAC cluster role. These RBAC cluster roles are predefined and permit users to interact with Kubernetes resources in your cluster. Additionally, a role binding is created to apply the cluster role to a specific namespace, or a cluster role binding is created to apply the cluster role to all namespaces.

To learn more about the actions permitted by each RBAC role, check out the {{site.data.keyword.cloud_notm}} IAM service access roles reference topic. To see the permissions that are granted by each RBAC role to individual Kubernetes resources, check out [Kubernetes resource permissions per RBAC role](#rbac_ref).

## Can I create custom roles or cluster roles?
{: #create-custom-rbac-roles}

If you are making your own custom RBAC policies, make sure that you do not edit the existing IBM role bindings that are in the cluster, or create custom role bindings with the same name as the existing IBM bindings. Changes that you make to the IBM-provided RBAC role bindings are not retained on updates.

The `view`, `edit`, `admin`, and `cluster-admin` cluster roles are predefined roles that are automatically created when you assign a user the corresponding {{site.data.keyword.cloud_notm}} IAM service access role. To grant other Kubernetes permissions, you can [create custom RBAC permissions](#rbac). Custom RBAC roles are in addition to and don't change or override any RBAC roles that you might have assigned with service access roles. Note that to create custom RBAC permissions, you must have the IAM **Manager** service access role or the **Administrator** platform role that gives you the `cluster-admin` Kubernetes RBAC role. However, the other users don't need an IAM service access role if you manage your own custom Kubernetes RBAC roles.

## When do I need to use custom cluster role bindings and role bindings?
{: #when-do-i-use-custom-rbac}

You might want to authorize who can create and update pods in your cluster. With [security context constraints (SCCs)](/docs/openshift?topic=openshift-openshift_scc#oc_sccs), you can use existing cluster role bindings that come with your cluster, or create your own.

You might also want to integrate add-ons to your cluster. For example, when you [set up Helm in your cluster](/docs/openshift?topic=openshift-helm)


## Creating custom RBAC permissions for users, groups, or service accounts
{: #rbac}

The `view`, `edit`, `admin`, and `cluster-admin` cluster roles are automatically created when you assign the corresponding {{site.data.keyword.cloud_notm}} IAM service access role. Do you need your cluster access policies to be more granular than these predefined permissions allow? No problem! You can create custom RBAC roles and cluster roles.
{: shortdesc}

You can assign custom RBAC roles and cluster roles to individual users, groups of users, or service accounts. When a binding is created for a group, it affects any user that is added or removed from that group. When you add users to a group, they get the access rights of the group in addition to any individual access rights that you grant them. If they are removed, their access is revoked. Note that you can't add service accounts to access groups.

If you want to assign access to a container process that runs in pods, such as a continuous delivery toolchain, you can use [Kubernetes `ServiceAccounts`](https://kubernetes.io/docs/reference/access-authn-authz/service-accounts-admin/){: external}. To follow a tutorial that demonstrates how to set up service accounts for Travis and Jenkins and to assign custom RBAC roles to the service accounts, see the blog post [Kubernetes `ServiceAccounts` for use in automated systems](https://medium.com/@jakekitchener/kubernetes-serviceaccounts-for-use-in-automated-systems-515297974982){: external}.

To prevent breaking changes, don't change the predefined `view`, `edit`, `admin`, and `cluster-admin` cluster roles. Custom RBAC roles are in addition to and don't change or override any RBAC roles that you might have assigned with {{site.data.keyword.cloud_notm}} IAM service access roles.
{: important}


- **Namespace access**: To allow a user, access group, or service account to access a resource within a specific namespace, choose one of the following combinations:
    - Create a role, and apply it with a role binding. This option is useful for controlling access to a unique resource that exists only in one namespace, like an app deployment.
    - Create a cluster role, and apply it with a role binding. This option is useful for controlling access to general resources in one namespace, like pods.
- **Cluster-wide access**: To allow a user or an access group to access cluster-wide resources or resources in all namespaces, create a cluster role, and apply it with a cluster role binding. This option is useful for controlling access to resources that are not scoped to namespaces, like worker nodes, or resources in all namespaces in your cluster, like pods in each namespace.

- [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)
- Ensure you that have the [**Manager** IAM service access role for all namespaces](/docs/openshift?topic=openshift-iam-platform-access-roles) or the **Administrator** platform role.
- To assign access to individual users or users in an access group, ensure that the user or group has been assigned at least one IAM platform access role at the {{site.data.keyword.openshiftlong_notm}} service level.

To create custom RBAC permissions,

1. Create a `.yaml` file similar to the following to define the `role` or `cluster role`.

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
    | `metadata.namespace` | For kind `Role` only: Specify the Kubernetes namespace to which access is granted. |
    | `rules.apiGroups` | Specify the Kubernetes [API groups](https://kubernetes.io/docs/reference/using-api/#api-groups){: external} that you want users to be able to interact with, such as `"apps"`, `"batch"`, or `"extensions"`. For access to the core API group at REST path `api/v1`, leave the group blank: `[""]`. |
    | `rules.resources` | Specify the Kubernetes [resource types](https://kubernetes.io/docs/reference/kubectl/quick-reference/){: external} to which you want to grant access, such as `"daemonsets"`, `"deployments"`, `"events"`, or `"ingresses"`. If you specify `"nodes"`, then the kind must be `ClusterRole`. |
    | `rules.verbs` | Specify the types of [actions](https://kubectl.docs.kubernetes.io/){: external} that you want users to be able to do, such as `"get"`, `"list"`, `"describe"`, `"create"`, or `"delete"`. |
    {: caption="Understanding the YAML parameters" caption-side="bottom"}

1. Create the role or cluster role in your cluster.

    ```sh
    oc apply -f my_role.yaml
    ```
    {: pre}

1. Verify that the role or cluster role is created.
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

1. Bind users to the role or cluster role by creating a `.yaml` file. Note the unique URL to use for each subject's name.

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
    {: caption="Understanding the YAML parameters" caption-side="bottom"}

1. Create the role binding or cluster role binding resource in your cluster.

    ```sh
    oc apply -f my_role_binding.yaml
    ```
    {: pre}

1. Verify that the binding is created.

    ```sh
    oc get rolebinding -n <namespace>
    ```
    {: pre}

1. Optional: To enforce the same level of user access in other namespaces, you can copy the role bindings for those roles or cluster roles to other namespaces.
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

You can extend your users' existing permissions by aggregating, or combining, cluster roles with other cluster roles. When you assign a user an {{site.data.keyword.cloud_notm}} service access role, the user is added to a [corresponding Kubernetes RBAC cluster role](/docs/openshift?topic=openshift-iam-platform-access-roles). However, you might want to allow certain users to perform additional operations.
{: shortdesc}

For example, a user with the namespace-scoped `admin` cluster role can't use the `oc top pods` command to view pod metrics for all the pods in the namespace. You might aggregate a cluster role so that users in the `admin` cluster role are authorized to run the `top pods` command. For more information, [see the Kubernetes docs](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#aggregated-clusterroles){: external}.

### What are some common operations that I might want to extend permissions for a default cluster role?
{: #common-rbac-operations}

Review [the operations that each default RBAC cluster role permits](#rbac_ref) to get a good idea of what your users can do, and then compare the permitted operations to what you want them to be able to do.

If your users in the same cluster role encounter errors similar to the following for the same type of operation, you might want to extend the cluster role to include this operation.

```sh
Error from server (Forbidden): pods.metrics.k8s.io is forbidden: User "IAM#myname@example.com" can't list resource "pods" in API group "metrics.k8s.io" in the namespace "mynamespace"
```
{: screen}

Before you begin: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

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
    | `metadata.name` | Enter a name for the cluster role. **don't** use the predefined cluster role names: `view`, `edit`, `admin`, and `cluster-admin`. |
    | `metadata.labels` | Add a label that matches the cluster role that you want to aggregate to in the format `rbac.authorization.k8s.io/aggregate-to-<cluster_role>: "true"`. The labels for the predefined cluster roles are as follows. \n * IAM **Manager** service access role, scoped to a namespace: `rbac.authorization.k8s.io/aggregate-to-admin: "true"` \n * IAM **Writer** service access role: `rbac.authorization.k8s.io/aggregate-to-edit: "true"` \n * IAM **Reader** service access role: `rbac.authorization.k8s.io/aggregate-to-view: "true"` |
    | `rules.apiGroups` | Specify the Kubernetes [API groups](https://kubernetes.io/docs/reference/using-api/#api-groups){: external} that you want users to be able to interact with, such as `"apps"`, `"batch"`, or `"extensions"`. For access to the core API group at REST path `api/v1`, leave the group blank: `[""]`. |
    | `rules.resources` | Specify the Kubernetes [resource types](https://kubernetes.io/docs/reference/kubectl/quick-reference/){: external} to which you want to grant access, such as `"daemonsets"`, `"deployments"`, `"events"`, or `"ingresses"`. |
    | `rules.verbs` | Specify the types of [actions](https://kubectl.docs.kubernetes.io/){: external} that you want users to be able to do, such as `"get"`, `"list"`, `"describe"`, `"create"`, or `"delete"`. |
    {: caption="Understanding the YAML parameters" caption-side="bottom"}

2. Create the cluster role in your cluster. Any users that have a role binding to the `admin` cluster role now have the additional permissions from the `view-pod-metrics` cluster role.
    ```sh
    oc apply -f <cluster_role_file.yaml>
    ```
    {: pre}

3. Follow up with users that have the `admin` cluster role. Ask them to [refresh their cluster configuration](/docs/containers?topic=containers-access_cluster) and test the action, such as `oc top pods`.


## Checking RBAC roles
{: #checking-rbac}

Verify your custom RBAC or synchronized IAM service access to RBAC roles in your {{site.data.keyword.openshiftlong_notm}} cluster.
{: shortdesc} 

### Checking RBAC roles from the UI
{: #checking-rbac-ui}

1. Log in to the [console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}.
1. Click the cluster with the RBAC roles that you want to check.
1. Click the **{{site.data.keyword.redhat_openshift_notm}} web console**.

    If you have a private network only cluster, you might not be able to open the dashboard unless you are on a VPN. See [Accessing clusters through the private cloud service endpoint](/docs/openshift?topic=openshift-access_cluster#access_private_se) or for {{site.data.keyword.satelliteshort}}, [Accessing {{site.data.keyword.redhat_openshift_notm}} clusters on {{site.data.keyword.satelliteshort}}](/docs/openshift?topic=openshift-access_cluster#access_cluster_sat).
    {: note}

1. From the **Administrator** perspective, click **User Management > Users**.
1. Click the user that you want to check, then click **Role Bindings**.

### Checking RBAC roles with the CLI
{: #checking-rbac-cli}

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
2. Check that the user is added to the RBAC role. Users are not added to a role binding if they have a higher permission. For example, if users have a cluster role and are in a cluster role binding, they are not added to each individual namespace role binding as well.

    You must be a cluster administrator to check role bindings and cluster role bindings. Cluster administrators have the **Manager** service access role in all namespaces or the **Administrator** platform access role. 
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


## Kubernetes service access roles and corresponding RBAC roles
{: #rbac_service}

The following table shows the Kubernetes resource permissions that are granted by each service access role and its corresponding RBAC role.


| Service access role| Corresponding RBAC role, binding, and scope | Kubernetes resource permissions |
| -------- | -------------- | -------------- |
| Reader role | When scoped to one namespace: **`view`** cluster role applied by the **`ibm-view`** role binding in that namespace. \n - When scoped to all namespaces: **`view`** cluster role applied by the **`ibm-view`** role binding in each namespace of the cluster. You can also view the cluster in the {{site.data.keyword.cloud_notm}} console and CLI. | - Read access to resources in a namespace \n - No read access to roles and role bindings or to Kubernetes secrets \n - Access the {{site.data.keyword.redhat_openshift_notm}} dashboard to view resources in a namespace. |
| Writer role | When scoped to one namespace: **`edit`** cluster role applied by the **`ibm-edit`** role binding in that namespace. \n \n When scoped to all namespaces: **`edit`** cluster role applied by the **`ibm-edit`** role binding in each namespace of the cluster | - Read/write access to resources in a namespace \n - No read/write access to roles and role bindings< \n - Access the Kubernetes dashboard to view resources in a namespace. |
| Manager role | When scoped to one namespace: **`admin`** cluster role applied by the **`ibm-operate`** role binding in that namespace \n  \n When scoped to all namespaces: **`cluster-admin`** cluster role applied by the **`ibm-admin`** cluster role binding that applies to all namespaces | When scoped to one namespace: \n - Read/write access to all resources in a namespace but not to resource quota or the namespace itself \n - Create RBAC roles and role bindings in a namespace  \n - Access the Kubernetes dashboard to view all resources in a namespace  \n When scoped to all namespaces: \n - Read/write access to all resources in every namespace \n - Create RBAC roles and role bindings in a namespace or cluster roles and cluster role bindings in all namespaces \n - Access the Kubernetes dashboard \n - Create an Ingress resource that makes apps publicly available \n - Review cluster metrics such as with the `oc top pods`, `oc top nodes`, or `oc get nodes` commands | 
| Any service access role | All users of a {{site.data.keyword.redhat_openshift_notm}} cluster are given the `basic-users`. | |  - Get basic information about projects that the user has access to. \n - Create authorized resources in the projects that the user has access to. \n - For more information, see the [{{site.data.keyword.redhat_openshift_notm}} docs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/authentication_and_authorization/using-rbac){: external} |
{: caption="Kubernetes resource permissions by service and corresponding RBAC roles" caption-side="bottom"}

### Kubernetes resource permissions per RBAC role
{: #rbac_ref}

Every user who is assigned an {{site.data.keyword.cloud_notm}} IAM service access role is also automatically assigned a corresponding, predefined Kubernetes role-based access control (RBAC) role. If you plan to manage your own custom Kubernetes RBAC roles, see [Creating custom RBAC permissions for users, groups, or service accounts](#rbac). For the username details, see [{{site.data.keyword.cloud_notm}} IAM issuer details for RBAC users](/docs/openshift?topic=openshift-iam-platform-access-roles).
{: shortdesc}

Wondering if you have the correct permissions to run a certain `oc` command on a resource in a namespace? Try the [`oc auth can-i` command](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-can-i-em-){: external}.
{: tip}

The following table shows the permissions that are granted by each RBAC role to individual Kubernetes resources. Permissions are shown as which `verbs` (or actions) a user with that role can complete against the resource, such as "get", "list", "describe", "create", or "delete".


| Kubernetes resource| `view` | `edit`| `admin` and `cluster-admin` |
| -------------- | -------------- | -------------- | -------------- | 
| `bindings` | get, list, watch | get, list, watch | get, list, watch \n **cluster-admin only:** create, delete, update |
| `configmaps` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `cronjobs.batch` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `daemonsets.apps` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `daemonsets.extensions` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `deployments.apps` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `deployments.apps/rollback` | - | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `deployments.apps/scale` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `deployments.extensions` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `deployments.extensions/rollback` | - | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `deployments.extensions/scale` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `endpoints` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `events` | get, list, watch | get, list, watch | get, list, watch |
| `horizontalpodautoscalers.autoscaling` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `ingresses.extensions` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `jobs.batch` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `limitranges` | get, list, watch | get, list, watch | get, list, watch |
| `localsubjectaccessreviews` | - | - | `create` |
| `namespaces` | get, list, watch | get, list, watch | get, list, watch \n **cluster-admin only:** create, delete |
| `namespaces/status` | get, list, watch | get, list, watch | get, list, watch |
| `networkpolicies` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `networkpolicies.extensions` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `node` | None | None | `admin` scoped to a namespace: None \n  \n  `cluster-admin` for all namespaces: All verbs |
| `persistentvolume` | None | None | create, delete, `deletecollection`, get, list, patch, update, watch |
| `persistentvolumeclaims` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `poddisruptionbudgets.policy` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `pods` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, `top`, patch, update, watch |
| `pods/attach` | - | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `pods/exec` | - | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `pods/log` | get, list, watch | get, list, watch | get, list, watch |
| `pods/portforward` | - | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `pods/proxy` | - | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `pods/status` | get, list, watch | get, list, watch | get, list, watch |
| `replicasets.apps` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `replicasets.apps/scale` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `replicasets.extensions` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `replicasets.extensions/scale` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `replicationcontrollers` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `replicationcontrollers/scale` | get, list, watch | cr}eate, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `replicationcontrollers/status` | get, list, watch | get, list, watch | get, list, watch |
| `replicationcontrollers.extensions/scale` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `resourcequotas` | get, list, watch | get, list, watch | get, list, watch |
| `resourcequotas/status` | get, list, watch | get, list, watch | get, list, watch |
| `rolebindings` | - | - | create, delete, `deletecollection`, get, list, patch, update, watch |
| `roles` | - | - | create, delete, `deletecollection`, get, list, patch, update, watch |
| `secrets` | - | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `serviceaccounts` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch, `impersonate` | create, delete, `deletecollection`, get, list, patch, update, watch, `impersonate` |
| `services` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `services/proxy` | - | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `statefulsets.apps` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
| `statefulsets.apps/scale` | get, list, watch | create, delete, `deletecollection`, get, list, patch, update, watch | create, delete, `deletecollection`, get, list, patch, update, watch |
{: caption="Kubernetes resource permissions granted by each predefined RBAC role" caption-side="bottom"}




### {{site.data.keyword.cloud_notm}} IAM issuer details for RBAC users
{: #iam-issuer-users}

Users with a service access role to {{site.data.keyword.openshiftlong_notm}} in IAM are given [corresponding user roles in RBAC](#rbac_ref). The RBAC user details include a unique issuer ID, subject identifier claim, and {{site.data.keyword.redhat_openshift_notm}} username. These details vary with the {{site.data.keyword.redhat_openshift_notm}} version of the cluster. When you update a cluster from a previous version, the details are automatically updated. RBAC usernames are prefixed by `IAM#`, such as in the output of `oc get users`. For more information about how OpenID authentication works, see the [{{site.data.keyword.redhat_openshift_notm}} documentation](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/authentication_and_authorization/external-auth#external-auth-configuring_external-auth){: external}.
{: shortdesc}

You might use this information if you build automation tooling within the cluster that relies on the user details to authenticate with the {{site.data.keyword.redhat_openshift_notm}} API server.

| Version | Issuer | Claim | Casing`*` |
| --- | --- | --- | --- |
| {{site.data.keyword.redhat_openshift_notm}} | `https://iam.cloud.ibm.com/identity` | `sub_<account_ID>` | lowercase |
{: caption="{{site.data.keyword.cloud_notm}} IAM issuer details for RBAC users" caption-side="bottom"}

`*`: An example of lowercase is `user.name@company.com`. An example of camel case is `User.Name@company.com`.
{: note}
