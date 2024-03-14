---

copyright: 
  years: 2022, 2024
lastupdated: "2024-03-14"


keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}




# IAM service access roles
{: #iam-service-access-roles}

Every user who is assigned an {{site.data.keyword.cloud_notm}} IAM service access role is also automatically assigned a corresponding Kubernetes role-based access control (RBAC) role in a specific namespace. To assign service access roles, see [Granting users access to your cluster through {{site.data.keyword.cloud_notm}} IAM](/docs/openshift?topic=openshift-users#checking-perms). Do not assign {{site.data.keyword.cloud_notm}} IAM platform access roles at the same time as a service access role. You must assign platform and service access roles separately.
{: shortdesc}

Looking for which Kubernetes actions each service access role grants through RBAC? See [Kubernetes resource permissions per RBAC role](#rbac_ref). To learn more about RBAC roles, see [Assigning RBAC permissions](/docs/openshift?topic=openshift-access-overview#role-binding) and [Extending existing permissions by aggregating cluster roles](/docs/openshift?topic=openshift-users#rbac_aggregate). For the username details, see [{{site.data.keyword.cloud_notm}} IAM issuer details for RBAC users](#iam-issuer-users).
{: tip}

See the IAM Policy Management [API reference](https://cloud.ibm.com/apidocs/iam-policy-management#list-roles){: external} for more information on managing IAM roles with the API.
{: tip}


{{../account/iam-service-roles.md#containers-kubernetes-roles}}

## Kubernetes service access roles and corresponding RBAC roles
{: #rbac_service}

The following table shows the Kubernetes resource permissions that are granted by each service access role and its corresponding RBAC role.


| Service access role| Corresponding RBAC role, binding, and scope | Kubernetes resource permissions |
| -------- | -------------- | -------------- |
| Reader role | When scoped to one namespace: **`view`** cluster role applied by the **`ibm-view`** role binding in that namespace. \n - When scoped to all namespaces: **`view`** cluster role applied by the **`ibm-view`** role binding in each namespace of the cluster. You can also view the cluster in the {{site.data.keyword.cloud_notm}} console and CLI. | - Read access to resources in a namespace \n - No read access to roles and role bindings or to Kubernetes secrets \n - Access the {{site.data.keyword.redhat_openshift_notm}} dashboard to view resources in a namespace. |
| Writer role | When scoped to one namespace: **`edit`** cluster role applied by the **`ibm-edit`** role binding in that namespace. \n \n When scoped to all namespaces: **`edit`** cluster role applied by the **`ibm-edit`** role binding in each namespace of the cluster | - Read/write access to resources in a namespace \n - No read/write access to roles and role bindings< \n - Access the Kubernetes dashboard to view resources in a namespace. |
| Manager role | When scoped to one namespace: **`admin`** cluster role applied by the **`ibm-operate`** role binding in that namespace \n  \n When scoped to all namespaces: **`cluster-admin`** cluster role applied by the **`ibm-admin`** cluster role binding that applies to all namespaces | When scoped to one namespace: \n - Read/write access to all resources in a namespace but not to resource quota or the namespace itself \n - Create RBAC roles and role bindings in a namespace  \n - Access the Kubernetes dashboard to view all resources in a namespace  \n When scoped to all namespaces: \n - Read/write access to all resources in every namespace \n - Create RBAC roles and role bindings in a namespace or cluster roles and cluster role bindings in all namespaces \n - Access the Kubernetes dashboard \n - Create an Ingress resource that makes apps publicly available \n - Review cluster metrics such as with the `oc top pods`, `oc top nodes`, or `oc get nodes` commands | 
| Any service access role | All users of a {{site.data.keyword.redhat_openshift_notm}} cluster are given the `basic-users`. | |  - Get basic information about projects that the user has access to. \n - Create authorized resources in the projects that the user has access to. \n - For more information, see the [{{site.data.keyword.redhat_openshift_notm}} docs](https://docs.openshift.com/container-platform/4.14/authentication/using-rbac.html){: external} |
{: caption="Table 1. Kubernetes resource permissions by service and corresponding RBAC roles" caption-side="bottom"}

## Kubernetes resource permissions per RBAC role
{: #rbac_ref}

Every user who is assigned an {{site.data.keyword.cloud_notm}} IAM service access role is also automatically assigned a corresponding, predefined Kubernetes role-based access control (RBAC) role. If you plan to manage your own custom Kubernetes RBAC roles, see [Creating custom RBAC permissions for users, groups, or service accounts](/docs/openshift?topic=openshift-users#rbac). For the username details, see [{{site.data.keyword.cloud_notm}} IAM issuer details for RBAC users](#iam-issuer-users).
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
{: caption="Table 1. Kubernetes resource permissions granted by each predefined RBAC role" caption-side="bottom"}




## {{site.data.keyword.cloud_notm}} IAM issuer details for RBAC users
{: #iam-issuer-users}

Users with a service access role to {{site.data.keyword.openshiftlong_notm}} in IAM are given [corresponding user roles in RBAC](#rbac_ref). The RBAC user details include a unique issuer ID, subject identifier claim, and {{site.data.keyword.redhat_openshift_notm}} username. These details vary with the {{site.data.keyword.redhat_openshift_notm}} version of the cluster. When you update a cluster from a previous version, the details are automatically updated. RBAC usernames are prefixed by `IAM#`, such as in the output of `oc get users`. For more information about how OpenID authentication works, see the [{{site.data.keyword.redhat_openshift_notm}} documentation](https://docs.openshift.com/container-platform/4.14/authentication/identity_providers/configuring-oidc-identity-provider.html){: external}.
{: shortdesc}

You might use this information if you build automation tooling within the cluster that relies on the user details to authenticate with the {{site.data.keyword.redhat_openshift_notm}} API server.

| Version | Issuer | Claim | Casing`*` |
| --- | --- | --- | --- |
| 3.11 or later | `https://iam.cloud.ibm.com/identity` | `sub_<account_ID>` | lowercase |
{: caption="{{site.data.keyword.cloud_notm}} IAM issuer details for RBAC users" caption-side="bottom"}

`*`: An example of lowercase is `user.name@company.com`. An example of camel case is `User.Name@company.com`.
{: note}




