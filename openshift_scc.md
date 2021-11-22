---

copyright:
  years: 2014, 2021
lastupdated: "2021-11-22"

keywords: openshift, scc, security context constraint, psp

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}

# Configuring security context constraints
{: #openshift_scc}

With security context constraints (SCCs), you can control the actions and access that pods within your {{site.data.keyword.openshiftlong}} cluster can perform. For more information about SCCs, see the [{{site.data.keyword.openshiftshort}} docs](https://docs.openshift.com/container-platform/4.7/authentication/managing-security-context-constraints.html){: external}.
{: shortdesc}

**Why do I set security context constraints?**

As a cluster admin, you want to control what happens in your cluster, especially actions that affect the cluster's security or readiness. Security context constraints can help you control what actions and access the pods in your container have, such as the usage of privileged containers, root namespaces, host networking and ports, volume types, host file systems, Linux permissions such as read-only or group IDs, and more.

**Can I also add users or system groups to SCCs?**

For user access to your cluster resources, don't use SCCs. Instead, see [Assigning cluster access](/docs/openshift?topic=openshift-users) to set {{site.data.keyword.cloud_notm}} IAM and infrastructure permissions.

For system groups such as `system:authenticated`, these groups already are assigned to SCCs. You can see which groups are assigned to an SCC by describing the SCC. If you change the SCC that a system group is assigned to, default components that belong to the system group might experience errors due to the change in permissions.

**Are any SCCs set by default?**

By default, {{site.data.keyword.openshiftlong_notm}} clusters include a standard set of [{{site.data.keyword.openshiftshort}} SCCs](#oc_sccs). Additionally, clusters have [IBM SCCs](#ibm_sccs) that closely resemble the [Kubernetes pod security policies of community Kubernetes clusters in {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-psp#ibm_psp). These IBM SCCs are included for improved portability with {{site.data.keyword.cloud_notm}} Private packages such as Cloud Paks.

**What SCCs are applied to my resources by default?**

If you don't specify a security context, the {{site.data.keyword.openshiftshort}} `restricted` security context constraint is applied by default. To check a pod's security context, describe the pod and look for the SCC annotation, such as in the following example.

```sh
oc describe pod <pod_name>
```
{: pre}

```
Name:               <pod_name>
Namespace:          <project_name>
...
Annotations:        openshift.io/...
                    openshift.io/scc=restricted
...
```
{: screen}

**Can I use Kubernetes pod security policies instead?**

No. [Kubernetes pod security policies](https://kubernetes.io/docs/concepts/policy/pod-security-policy/){: external} (PSPs) are originally based on {{site.data.keyword.openshiftshort}} SCCs. However, {{site.data.keyword.openshiftshort}} supports only SCCs, not PSPs.

The default {{site.data.keyword.openshiftshort}} SCCs are stricter than the default PSPs in community Kubernetes clusters. As such, app deployments that run in community Kubernetes clusters might need to be modified to run in {{site.data.keyword.openshiftshort}}.


## Customizing security context constraints
{: #customize_sccs}

To create, edit, list, delete, and otherwise manage security context constraints, see the [{{site.data.keyword.openshiftshort}} docs](https://docs.openshift.com/container-platform/4.7/authentication/managing-security-context-constraints.html){: external}. You can also add users or groups to the default security context constraints.
{: shortdesc}

Make sure that you use the [`oc` CLI or `kubectl` version 1.12 CLI](/docs/openshift?topic=openshift-openshift-cli#cli_oc) to interact with these resources, such as `oc get scc`. The `kubectl` CLI version 1.11 CLI has a bug that yields an error when you run commands against {{site.data.keyword.openshiftshort}}-specific resources, such as `kubectl get scc`.
{: important}


## Default {{site.data.keyword.openshiftshort}} security context constraints
{: #oc_sccs}

{{site.data.keyword.openshiftlong_notm}} clusters come with the following security context constraints by default.
{: shortdesc}

Do not edit existing {{site.data.keyword.openshiftshort}} or IBM SCCs settings, except for `priority`, `users`, or `groups` fields.
{: note}

|SCC name | Description |
|---------|-------------|
| `anyuid`| Denies access similar to the `restricted` SCC, but allows users to run with any UID and any GID.|
| `hostaccess`| Allows access to all host namespaces, but still requires that pods are run with a UID and SELinux context that are allocated to the namespace. \n  \n **Important**: Grant this SCC for only trusted pods that require host access to namespaces, file systems, and process IDs. |
| `hostmount-anyuid` | Denies access similar to the `restricted` SCC, but allows host mounts and any UID by a pod. This SCC is primarily used by the persistent volume recycler. \n  \n **Important**: Grant this SCC for only pods that require host file system access as any UID, including UID 0. |
| `hostnetwork`| Allows the usage of host networking and host ports, but still requires that pods are run with a UID and SELinux context that are allocated to the namespace. \n  \n **Important**: Grant this SCC for only pods that require host network access. |
| `node-exporter`| Gives the appropriate access for the built-in Prometheus node exporter. |
| `nonroot`| Denies access similar to the `restricted` SCC, but allows users to run with any non-root UID. Either the user or the manifest of the container runtime must specify the UID.|
| `privileged`| Allows access to all privileged and host features and the ability to run as any user, any group, any fsGroup, and with any SELinux context. \n  \n **Important**: Grant this SCC for only cluster administration that requires the most access possible. |
| `restricted`| Denies access to all host features and requires that pods are run with a UID and SELinux context that are allocated to the namespace. This is the most restrictive SCC, and it is used by default for authenticated users.|
{: caption="Default {{site.data.keyword.openshiftshort}} security context constraints" caption-side="top"}


## Default IBM security context constraints
{: #ibm_sccs}

{{site.data.keyword.openshiftlong_notm}} clusters come with the following IBM security context constraints by default.
{: shortdesc}

Do not edit existing {{site.data.keyword.openshiftshort}} or IBM SCCs settings, except for `priority`, `users`, or `groups` fields.
{: note}

|SCC name | Description |
|---------|-------------|
| `ibm-anyuid-hostaccess-scc`| Allows pods to run with any UID and GID, any volume, and full access to the host. \n  \n **Important**: Grant this SCC for only pods that require full access to the host and network. |
| `ibm-anyuid-hostpath-scc`| Allows pods to run with any UID and GID and any volume, including the host path. \n  \n **Important**: Grant this SCC for only pods that require access to `hostPath` volumes. |
| `ibm-anyuid-scc` | Allows pods to run with any UID and GID, but prevents access to the host.|
| `ibm-privileged-scc`| Grants access to all privileged host features, and allows a pod to run with any UID and GID and any volume. \n  \n **Important**: Grant this SCC for only cluster administration that requires the most access possible. |
| `ibm-restricted-scc` | Denies access to all host features and requires that pods are run with a UID and SELinux context that are allocated to the namespace. This SCC is the most restrictive IBM SCC.|
{: caption="Default IBM security context constraints" caption-side="top"}






