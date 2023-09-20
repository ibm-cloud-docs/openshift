---

copyright:
  years: 2014, 2023
lastupdated: "2023-09-20"

keywords: openshift, scc, security context constraint, psp

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}




# Configuring security context constraints
{: #openshift_scc}

With security context constraints (SCCs), you can control the actions and access that pods within your {{site.data.keyword.openshiftlong}} cluster can perform. For more information about SCCs, see the [{{site.data.keyword.redhat_openshift_notm}} docs](https://docs.openshift.com/container-platform/4.12/authentication/managing-security-context-constraints.html){: external}.
{: shortdesc}

Why do I set security context constraints?
:   As a cluster admin, you want to control what happens in your cluster, especially actions that affect the cluster's security or readiness. Security context constraints can help you control what actions and access the pods in your container have, such as the usage of privileged containers, root namespaces, host networking and ports, volume types, host file systems, Linux permissions such as read-only or group IDs, and more.

Can I also add users or system groups to SCCs?
:   For user access to your cluster resources, don't use SCCs. Instead, see [Assigning cluster access](/docs/openshift?topic=openshift-users) to set {{site.data.keyword.cloud_notm}} IAM and infrastructure permissions.
:   For system groups such as `system:authenticated`, these groups already are assigned to SCCs. You can see which groups are assigned to an SCC by describing the SCC. If you change the SCC that a system group is assigned to, default components that belong to the system group might experience errors due to the change in permissions.

Are any SCCs set by default?
:   By default, {{site.data.keyword.openshiftlong_notm}} clusters include a standard set of [{{site.data.keyword.redhat_openshift_notm}} SCCs](#oc_sccs). Additionally, clusters have [IBM SCCs](#ibm_sccs) that closely resemble the [Kubernetes pod security policies of community Kubernetes clusters in {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-psp#ibm_psp). These IBM SCCs are included for improved portability with {{site.data.keyword.cloud_notm}} Private packages such as Cloud Paks.

What SCCs are applied to my resources by default?
:   If you don't specify a security context, the {{site.data.keyword.redhat_openshift_notm}} `restricted` (or `restricted-v2` in 4.11 and later) security context constraint is applied by default. To check a pod's security context, describe the pod and look for the SCC annotation, such as in the following example.

```sh
oc describe pod <pod_name>
```
{: pre}

```sh
Name:               <pod_name>
Namespace:          <project_name>
...
Annotations:        openshift.io/...
                    openshift.io/scc=restricted
...
```
{: screen}

Can I use Kubernetes pod security policies instead?
:   No. [Kubernetes pod security policies](https://kubernetes.io/docs/concepts/security/pod-security-policy/){: external} (PSPs) are originally based on {{site.data.keyword.redhat_openshift_notm}} SCCs. However, {{site.data.keyword.redhat_openshift_notm}} supports only SCCs, not PSPs.

The default {{site.data.keyword.redhat_openshift_notm}} SCCs are stricter than the default PSPs in community Kubernetes clusters. As such, app deployments that run in community Kubernetes clusters might need to be modified to run in {{site.data.keyword.redhat_openshift_notm}}.


## Customizing security context constraints
{: #customize_sccs}

To create, edit, list, delete, and otherwise manage security context constraints, see the [{{site.data.keyword.redhat_openshift_notm}} docs](https://docs.openshift.com/container-platform/4.12/authentication/managing-security-context-constraints.html){: external}. You can also authorize users or groups to the default security context constraints by using role-based access control such as `clusterroles`, `clusterrolebindings`, `roles`, and `rolebindings`. You can also use the `oc adm policy` subcommands, such as `oc adm policy add-scc-to-user`, to manage these settings. The oc version is the same as that of the cluster being managed.
{: shortdesc}

## Guidelines for assigning access to SCCs
{: #scc-guidelines}

- Authorize specific service accounts to the SCC that is to be used by pods running under that service account.
- If a service account needs access to multiple SCCs, consider creating additional service accounts so that all pods running under a service account are expected to use the same SCC.
- Do not authorize all users or all service accounts to use any SCC other than the `restricted` (4.10 and earlier) or `restricted-v2` (4.11 and later) SCCs.
- Do not change SCC authorization for service accounts in the `openshift-*` namespaces. {{site.data.keyword.redhat_openshift_notm}} components are designed to run under specific SCCs and might not operate properly under a different SCC.


## Default {{site.data.keyword.redhat_openshift_notm}} security context constraints
{: #oc_sccs}

{{site.data.keyword.openshiftlong_notm}} clusters come with the following security context constraints by default.
{: shortdesc}

Do not edit existing {{site.data.keyword.redhat_openshift_notm}} or IBM SCCs settings, except for `priority`, `users`, or `groups` fields.
{: note}

|SCC name | Description |
|---------|-------------|
| `anyuid`| Denies access similar to the `restricted` SCC, but allows users to run with any UID and any GID.|
| `hostaccess`| Allows access to all host namespaces, but still requires that pods are run with a UID and SELinux context that are allocated to the namespace. \n  \n **Important**: Grant this SCC for only trusted pods that require host access to namespaces, file systems, and process IDs. |
| `hostmount-anyuid` | Denies access similar to the `restricted` SCC, but allows host mounts and any UID by a pod. This SCC is primarily used by the persistent volume recycler. \n  \n **Important**: Grant this SCC for only pods that require host file system access as any UID, including UID 0. |
| `hostnetwork`| Allows the usage of host networking and host ports, but still requires that pods are run with a UID and SELinux context that are allocated to the namespace. \n  \n **Important**: Grant this SCC for only pods that require host network access. |
| `node-exporter`| Gives the appropriate access for the built-in Prometheus node exporter. |
| `nonroot`| Denies access similar to the `restricted` SCC, but allows users to run with any non-root UID. Either the user or the manifest of the container runtime must specify the UID.|
| `privileged`| Allows access to all privileged and host features and the ability to run as any user, any group, any `fsGroup` setting, and with any SELinux context. \n  \n **Important**: Grant this SCC for only cluster administration that requires the most access possible. |
| `restricted`| Denies access to all host features and requires that pods are run with a UID and SELinux context that are allocated to the namespace. This is the most restrictive SCC, and it is used by default for authenticated users.|
| `hostnetwork-v2`| Similar to the `hostnetwork` SCC, but modified to minimize differences from the Pod Security Standards `Restricted` profile. |
| `nonroot-v2`| Similar to the `nonroot` SCC, but modified to minimize differences from the Pod Security Standards `Restricted` profile. |
| `restricted-v2`| Similar to the `restricted` SCC, but modified to satisfy the Pod Security Standards `Restricted` profile. |
{: caption="Default {{site.data.keyword.redhat_openshift_notm}} security context constraints" caption-side="bottom"}


## Default IBM security context constraints
{: #ibm_sccs}

{{site.data.keyword.openshiftlong_notm}} clusters come with the following IBM security context constraints by default.
{: shortdesc}

Do not edit existing {{site.data.keyword.redhat_openshift_notm}} or IBM SCCs settings, except for `priority`, `users`, or `groups` fields.
{: note}

|SCC name | Description |
|---------|-------------|
| `ibm-anyuid-hostaccess-scc`| Allows pods to run with any UID and GID, any volume, and full access to the host. \n  \n **Important**: Grant this SCC for only pods that require full access to the host and network. |
| `ibm-anyuid-hostpath-scc`| Allows pods to run with any UID and GID and any volume, including the host path. \n  \n **Important**: Grant this SCC for only pods that require access to `hostPath` volumes. |
| `ibm-anyuid-scc` | Allows pods to run with any UID and GID, but prevents access to the host.|
| `ibm-privileged-scc`| Grants access to all privileged host features, and allows a pod to run with any UID and GID and any volume. \n  \n **Important**: Grant this SCC for only cluster administration that requires the most access possible. |
| `ibm-restricted-scc` | Denies access to all host features and requires that pods are run with a UID and SELinux context that are allocated to the namespace. This SCC is the most restrictive IBM SCC.|
{: caption="Default IBM security context constraints" caption-side="bottom"}






