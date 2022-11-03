---

copyright: 
  years: 2022, 2022
lastupdated: "2022-11-03"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# IAM service access roles
{: #iam-service-access-roles}

Every user who is assigned an {{site.data.keyword.cloud_notm}} IAM service access role is also automatically assigned a corresponding Kubernetes role-based access control (RBAC) role in a specific namespace. To assign service access roles, see [Granting users access to your cluster through {{site.data.keyword.cloud_notm}} IAM](/docs/openshift?topic=openshift-users#checking-perms). Do not assign {{site.data.keyword.cloud_notm}} IAM platform access roles at the same time as a service access role. You must assign platform and service access roles separately.
{: shortdesc}

Looking for which Kubernetes actions each service access role grants through RBAC? See [Kubernetes resource permissions per RBAC role](#rbac_ref). To learn more about RBAC roles, see [Assigning RBAC permissions](/docs/openshift?topic=openshift-access-overview#role-binding) and [Extending existing permissions by aggregating cluster roles](/docs/openshift?topic=openshift-users#rbac_aggregate). For the username details, see [{{site.data.keyword.cloud_notm}} IAM issuer details for RBAC users](#iam_issuer_users).
{: tip}

The following table shows the Kubernetes resource permissions that are granted by each service access role and its corresponding RBAC role.


| Service access role| Corresponding RBAC role, binding, and scope | Kubernetes resource permissions |
| -------- | -------------- | -------------- |
| Reader role | When scoped to one namespace: **`view`** cluster role applied by the **`ibm-view`** role binding in that namespace. \n - When scoped to all namespaces: **`view`** cluster role applied by the **`ibm-view`** role binding in each namespace of the cluster. You can also view the cluster in the {{site.data.keyword.cloud_notm}} console and CLI. | - Read access to resources in a namespace \n - No read access to roles and role bindings or to Kubernetes secrets \n - Access the {{site.data.keyword.redhat_openshift_notm}} dashboard to view resources in a namespace. |
| Writer role | When scoped to one namespace: **`edit`** cluster role applied by the **`ibm-edit`** role binding in that namespace. \n \n When scoped to all namespaces: **`edit`** cluster role applied by the **`ibm-edit`** role binding in each namespace of the cluster | - Read/write access to resources in a namespace \n - No read/write access to roles and role bindings< \n - Access the Kubernetes dashboard to view resources in a namespace. |
| Manager role | When scoped to one namespace: **`admin`** cluster role applied by the **`ibm-operate`** role binding in that namespace \n  \n When scoped to all namespaces: **`cluster-admin`** cluster role applied by the **`ibm-admin`** cluster role binding that applies to all namespaces | When scoped to one namespace: \n - Read/write access to all resources in a namespace but not to resource quota or the namespace itself \n - Create RBAC roles and role bindings in a namespace  \n - Access the Kubernetes dashboard to view all resources in a namespace  \n When scoped to all namespaces: \n - Read/write access to all resources in every namespace \n - Create RBAC roles and role bindings in a namespace or cluster roles and cluster role bindings in all namespaces \n - Access the Kubernetes dashboard \n - Create an Ingress resource that makes apps publicly available \n - Review cluster metrics such as with the `oc top pods`, `oc top nodes`, or `oc get nodes` commands | 
| Any service access role | All users of a {{site.data.keyword.redhat_openshift_notm}} cluster are given the following roles that vary by cluster version. \n - Version 3 clusters: `basic-users` and `self-provisioners`. \n -  Version 4 clusters: `basic-users`. | |  - Get basic information about projects that the user has access to. \n - Create authorized resources in the projects that the user has access to. \n - For more information, see the [{{site.data.keyword.redhat_openshift_notm}} docs](https://docs.openshift.com/container-platform/4.10/authentication/using-rbac.html){: external} |
{: caption="Table 1. Kubernetes resource permissions by service and corresponding RBAC roles" caption-side="bottom"}

## Kubernetes resource permissions per RBAC role
{: #rbac_ref}

Every user who is assigned an {{site.data.keyword.cloud_notm}} IAM service access role is also automatically assigned a corresponding, predefined Kubernetes role-based access control (RBAC) role. If you plan to manage your own custom Kubernetes RBAC roles, see [Creating custom RBAC permissions for users, groups, or service accounts](/docs/openshift?topic=openshift-users#rbac). For the username details, see [{{site.data.keyword.cloud_notm}} IAM issuer details for RBAC users](#iam_issuer_users).
{: shortdesc}

Wondering if you have the correct permissions to run a certain `oc` command on a resource in a namespace? Try the [`oc auth can-i` command](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-can-i-em-){: external}.
{: tip}

The following sections show the permissions that are granted by each RBAC role to individual Kubernetes resources. Permissions are shown as which `verbs` (or actions) a user with that role can complete against the resource, such as "get", "list", "describe", "create", or "delete".


### `bindings`
{: #rbac-bindings}

`view`
:   `get`, `list`, `watch`

`edit`
:   `get`, `list`, `watch`

`admin`
:   `get`, `list`, `watch`

`cluster-admin`
:   `create`, `delete`, `update`


### `configmaps`
{: #rbac-configmaps}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `cronjobs.batch`
{: #rbac-cronjobs}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `daemonsets.apps`
{: #rbac-ds-apps}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `daemonsets.extensions`
{: #rbac-ds-extensions}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `deployments.apps` 
{: #rbac-dep-apps}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch` 

### `deployments.apps/rollback`
{: #rbac-dep-rollback}

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`


### `deployments.apps/scale`
{: #rbac-dep-apps-scale}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `deployments.extensions`
{: #rbac-dep-extensions}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `deployments.extensions/rollback`
{# rbac-dep-extension-rollback}

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `deployments.extensions/scale`
{: #rbac-dep-extensions-scale}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:    `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `endpoints`
{: #rbac-endpoints}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `events`
{: #rbac-events}

`view`
:   `get`, `list`, `watch`

`edit`
:   `get`, `list`, `watch`

`admin` and `cluster-admin`
:   `get`, `list`, `watch`

### `horizontalpodautoscalers.autoscaling`
{: #rbac-hpas}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `ingresses.extensions`
{: #rbac-configmaps}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch` 


`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `jobs.batch`
{: #rbac-jobs-batch}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:    `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `limitranges`
{: #rbac-limitranges}

`view`
:   `get`, `list`, `watch`

`edit`
:   `get`, `list`, `watch`

`admin` and `cluster-admin`
:   `get`, `list`, `watch`

### `localsubjectaccessreviews` 
{: #rbac-localsubjectaccessreviews}

`view`,`edit` 
:   None

`admin` and `cluster-admin`
:   `create`

### `namespaces`
{: #rbac-namespaces}

`view`
:   `get`, `list`, `watch`

`edit`
:   `get`, `list`, `watch` 

`admin` 
:   `get`, `list`, `watch`

`cluster-admin`
:   `get`, `list`, `watch`,`create`, `delete`

### `namespaces/status`
{: #rbac-namespaces-status}

`view`
:   `get`, `list`, `watch`

`edit`
:   `get`, `list`, `watch` | `get`, `list`, `watch` |

### `networkpolicies`
{: #rbac-networkpolicies}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch` 

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `networkpolicies.extensions`
{: #rbac-networkpolicies-extensions}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `node`
{: #rbac-node}

`admin`
:   Scoped to a namespace: None

`cluster-admin`
:   All namespaces: All verbs


### `persistentvolume`
{: #rbac-persistentvolume}

`view`
:   None

`edit`
:   None

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`


### `persistentvolumeclaims`
{: #rbac-persistentvolumeclaims}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `poddisruptionbudgets.policy`
{: #rbac-poddisruptionbudgets-policy}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `pods`
{: #rbac-pods}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `top`, `patch`, `update`, `watch`

### `pods/attach`
{: #rbac-pods-attach}

`view`
:   None

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `pods/exec`
{: #rbac-pods-exec}

`view`
:   None

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `pods/log`
{: #rbac-pods-log}

`view`
:   `get`, `list`, `watch`

`edit`
:   `get`, `list`, `watch`

`admin` and `cluster-admin`
:   `get`, `list`, `watch`

### `pods/portforward`
{: #rbac-pods-portforward}

`view`
:   None

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `pods/proxy`
{: #rbac-pods-proxy}

`view`
:   None

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `pods/status`
{: #rbac-pods-status}

`view`
:   `get`, `list`, `watch`

`edit`
:   `get`, `list`, `watch`

`admin` and `cluster-admin`
:   `get`, `list`, `watch`

### `replicasets.apps`
{: #rbac-replicasets-apps}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `replicasets.apps/scale`
{: #rbac-replicasets-apps-scale}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `replicasets.extensions`
{: #rbac-replicasets-extensions}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `replicasets.extensions/scale`
{: #rbac-replicasets-extensions-scale}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `replicationcontrollers` 
{: #rbac-replicationcontrollers}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `replicationcontrollers/scale`
{: #rbac-replicationcontrollers-scale}

`view`
:   `get`, `list`, `watch` 

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `replicationcontrollers/status`
{: #rbac-replicationcontrollers-status}

`view`
:   `get`, `list`, `watch` 

`edit`
:   `get`, `list`, `watch` 

`admin` and `cluster-admin`
:   `get`, `list`, `watch`

### `replicationcontrollers.extensions/scale`
{: #rbac-replicationcontrollers-extensions-scale}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `resourcequotas`
{: #rbac-resourcequotas}

`view`
:   `get`, `list`, `watch`

`edit`
:   `get`, `list`, `watch`

`admin` and `cluster-admin`
:   `get`, `list`, `watch`

### `resourcequotas/status`
{: #rbac-resourcequotas-status}

`view`
:   `get`, `list`, `watch`

`edit`
:   `get`, `list`, `watch`

`admin` and `cluster-admin`
:   `get`, `list`, `watch`

### `rolebindings`
{: #rbac-rolebindings}

`view`
:   None

`edit`
:   None

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `roles`
{: #rbac-roles}

`view`
:   None

`edit`
:   None

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `secrets`
{: #rbac-secrets}

`view`
:   None

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `serviceaccounts`
{: #rbac-serviceaccounts}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`, `impersonate` 

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`, `impersonate` 

### `services`
{: #rbac-services}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch` 

### `services/proxy`
{: #rbac-services-proxy}

`view`
:   None

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `statefulsets.apps` 
{: #rbac-statefulsets-apps}

`view`
:   `get`, `list`, `watch`

`edit`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:   `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

### `statefulsets.apps/scale`
{: #rbac-statefulsets-apps-scale}

`view`
:   `get`, `list`, `watch`

`edit`
:    `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`

`admin` and `cluster-admin`
:    `create`, `delete`, `deletecollection`, `get`, `list`, `patch`, `update`, `watch`




## {{site.data.keyword.cloud_notm}} IAM issuer details for RBAC users
{: #iam-issuer-users}

Users with a service access role to {{site.data.keyword.openshiftlong_notm}} in IAM are given [corresponding user roles in RBAC](#rbac_ref). The RBAC user details include a unique issuer ID, subject identifier claim, and {{site.data.keyword.redhat_openshift_notm}} username. These details vary with the {{site.data.keyword.redhat_openshift_notm}} version of the cluster. When you update a cluster from a previous version, the details are automatically updated. RBAC usernames are prefixed by `IAM#`, such as in the output of `oc get users`. For more information about how OpenID authentication works, see the [{{site.data.keyword.redhat_openshift_notm}} documentation](https://docs.openshift.com/container-platform/4.10/authentication/identity_providers/configuring-oidc-identity-provider.html){: external}.
{: shortdesc}

You might use this information if you build automation tooling within the cluster that relies on the user details to authenticate with the {{site.data.keyword.redhat_openshift_notm}} API server.

| Version | Issuer | Claim | Casing`*` |
| --- | --- | --- | --- |
| 3.11 or later | `https://iam.cloud.ibm.com/identity` | `sub_<account_ID>` | lowercase |
{: summary="The rows are read from left to right. The first column is the {{site.data.keyword.redhat_openshift_notm}} version of the cluster. The second column is the {{site.data.keyword.cloud_notm}} IAM Issuer ID. The third column is the subject identifier claim. The fourth column is the casing style of the username."}
{: caption="{{site.data.keyword.cloud_notm}} IAM issuer details for RBAC users" caption-side="bottom"}

`*`: An example of lowercase is `user.name@company.com`. An example of camel case is `User.Name@company.com`.
{: note}


