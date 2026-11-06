---

copyright:
  years: 2026, 2026
lastupdated: "2026-11-05"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, prepare to update, update checklist, backup before update, update permissions

subcollection: openshift

content-type: howto

---

{{site.data.keyword.attribute-definition-list}}


# Preparing to update your cluster
{: #update-prepare}

Before you update the master or worker nodes, review what changes in the new version, check your add-ons and plug-ins, and confirm your access. Completing these checks once reduces the risk of version skew failures, app downtime, and blocked updates.
{: shortdesc}

Complete these checks before you [update the cluster master](/docs/openshift?topic=openshift-update-master) and again before you update worker nodes if time has passed.

## Before you begin
{: #update-prepare-permissions}

Make sure that you have the [**Operator** or **Administrator** IAM platform access role](/docs/openshift?topic=openshift-iam-platform-access-roles). If you're unsure of your access role, go to **Manage** > **Access (IAM)** > **Users** in the {{site.data.keyword.cloud_notm}} console, or ask your account administrator. The **Operator** role is the minimum role that the `cluster master update`, `worker update`, `worker replace`, and `worker reload` commands require. For classic clusters, infrastructure actions are authorized through your IAM platform access role.

If a certificate authority (CA) certificate rotation is in progress, the master update is blocked until the rotation completes. Check the status of any in-progress [CA certificate rotation](/docs/openshift?topic=openshift-cert-rotate) before you begin.
{: important}

## Reviewing version changes and backing up
{: #update-prepare-steps}

Review the changes that come with the new version and protect data that you can't re-create.
{: shortdesc}

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
2. Review the [{{site.data.keyword.openshiftshort}} version information](/docs/openshift?topic=openshift-openshift_versions) and make any changes that are marked _Update before master_ or _Update after master_ in the [{{site.data.keyword.redhat_openshift_notm}} version preparation guide](/docs/openshift?topic=openshift-openshift_versions).
3. Review any [Kubernetes helpful warnings](https://kubernetes.io/blog/2020/09/03/warnings/){: external}, such as deprecation notices.
4. Back up your app data and any configuration that you can't re-create, including data on [persistent storage](/docs/openshift?topic=openshift-storage-plan). IBM backs up the etcd data for your cluster master, such as your Kubernetes workload configuration files. For more information, see [Your responsibilities with using {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-responsibilities_iks).

You can't roll back a cluster to a previous version after the update process takes place. Use a test cluster to address potential issues before you update your production cluster.
{: important}

## Checking add-ons
{: #update-prepare-addons}

Check that the managed add-ons in your cluster support the version that you are updating to.
{: shortdesc}

1. List the add-ons in the cluster.

    ```sh
    ibmcloud oc cluster addon ls --cluster CLUSTER
    ```
    {: pre}

2. Check the supported {{site.data.keyword.redhat_openshift_notm}} version for each add-on that is installed.

    ```sh
    ibmcloud oc addon-versions
    ```
    {: pre}

3. If an add-on must be updated to run in the {{site.data.keyword.redhat_openshift_notm}} version that you want to update your cluster to, [update the add-on](/docs/openshift?topic=openshift-managed-addons#updating-managed-add-ons).

## Checking plug-ins
{: #update-prepare-plugins}

Check that the plug-ins that you installed from the Helm catalog support the version that you are updating to.
{: shortdesc}

1. In the [Helm catalog](https://cloud.ibm.com/kubernetes/helm){: external}, find the plug-ins that you installed in your cluster.
2. From the side menu, expand the **SOURCES & TAR FILE** section.
3. Download and open the source code.
4. Check the `README.md` or `RELEASENOTES.md` files for supported versions.
5. If a plug-in must be updated to run in the {{site.data.keyword.redhat_openshift_notm}} version that you want to update your cluster to, update the plug-in by following the plug-in instructions.

## Next steps
{: #update-prepare-next}

[Update the cluster master](/docs/openshift?topic=openshift-update-master). When the master update is complete, update your worker nodes.

It is good practice to [rotate your CA certificates](/docs/openshift?topic=openshift-cert-rotate) whenever you update your worker nodes, as the longest step of certificate rotation includes reloading or replacing your worker nodes.
{: tip}

## Related links
{: #update-prepare-related}

* [Updating clusters, worker nodes, and cluster components](/docs/openshift?topic=openshift-update)
* [Your responsibilities with using {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-responsibilities_iks)
