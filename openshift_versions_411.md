---

copyright:
  years: 2022, 2022
lastupdated: "2022-09-01"

keywords: openshift, version, update, upgrade, 4.11, update openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# 4.11 version information and update actions
{: #cs_versions_411}

Review information about version 4.11 of {{site.data.keyword.openshiftlong_notm}}, released 31 August 2022. This version is based on Kubernetes version 1.24. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [Red Hat OpenShift on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_changelog) and the version [4.11 blog](https://cloud.redhat.com/blog/introducing-red-hat-openshift-4.11){: external}
{: tip}



## Release timeline 
{: #release_timeline_411}

The following table includes the expected release timeline for version 4.11. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Supported | 4.11 / 1.24 | 31 Aug 2022 | Mar 2024`†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}} version 4.11." caption-side="top"}
{: summary="The rows are read from left to right. The first column is the supported status, the second column is OpenShift and Kubernetes version number. The third column is the release date. The fourth column is the unsupported date."}

## Preparing to update
{: #prep-up-411}

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) to version 4.11. This information summarizes updates that are likely to have an impact on deployed apps when you update.
{: shortdesc}

**Before you update**: Review the following list of considerations and limitations before you update your cluster to version 4.11. Some of the following entries are relevant to specific add-ons. To check if you have an add-on enabled in your cluster, run `ibmcloud oc cluster addon ls`. 

RHEL 8 operating system support 
:    RHEL 8 is the only operating system supported for clusters that run version 4.11. If you update an existing cluster to 4.11, you must take steps to [migrate your worker nodes](#rhel-migrate-411) to RHEL 8.

Gateway-enabled clusters
:    Classic clusters created with the `--gateway-enabled` option do not support RHEL 8 worker nodes, and therefore are not supported for version 4.11. Do not update your cluster to version 4.11 if it has the gateway-enabled cluster controller installed. 

Cluster autoscaler add-on
:    The cluster autoscaler add-on does not support {{site.keyword.openshiftshort}} version 4.11. Do not update your cluster to version 4.11 if this add-on is installed.

Portworx
:    Portworx does not support {{site.keyword.openshiftshort}} version 4.11. Do not update your cluster to version 4.11 if you have Portworx installed. To check if you have Portworx installed in your cluster, run `oc get pods -n kube-system | grep 'portworx'`.

OpenShift Data Foundation (ODF)
:    ODF version 4.10 supports {{site.keyword.openshiftshort}} version 4.11 clusters. You may continue to use version 4.10 of the ODF add-on.

Extended update support (EUS)
:    EUS updates are not available at this time for clusters that run version 4.11.

### Update before master
{: #411_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| --- | --- |
| **Unsupported:** Deprecated and removed OpenShift features | For more information, review the [OpenShift version 4.11 deprecated and removed features](https://docs.openshift.com/container-platform/4.11/release_notes/ocp-4-11-release-notes.html#ocp-4-11-deprecated-removed-features){: external}. |
| Known Red Hat OpenShift issues | For more information about possible required actions, review [Red Hat OpenShift version 4.11 known issues](https://docs.openshift.com/container-platform/4.11/release_notes/ocp-4-11-release-notes.html#ocp-4-11-known-issues){: external}. |
| `LegacyServiceAccountTokenNoAutoGeneration` feature gate is enabled | For more information, review possible required actions in the `LegacyServiceAccountTokenNoAutoGeneration is on by default` section of the[OpenShift version 4.11 notable technical changes](https://docs.openshift.com/container-platform/4.11/release_notes/ocp-4-11-release-notes.html#ocp-4-11-notable-technical-changes). |
| Red Hat OpenShift web console redirect changed | Cluster server URL no longer redirects to the Red Hat OpenShift web console. You must add `/console` to the URL for the redirect. | 
{: caption="Changes to make before you update the master to Red Hat OpenShift 4.11" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the type of update. The second column is a description of the update and impacts it might have."}

### Update after master
{: #411_after}

| Type | Description |
| --- | --- |
| **Unsupported:** RHEL 7 worker nodes | Using RHEL 7 worker nodes with Red Hat OpenShift on IBM Cloud version 4.11 clusters is unsupported. After updating the cluster master, the cluster worker pools must be re-created with RHEL 8 worker nodes. For more information about steps to take after you upgrade your cluster to 4.11, see [Migrating your worker nodes from RHEL 7 to RHEL 8](#rhel-migrate-411). |
{: caption="Changes to make after you update the master to Red Hat OpenShift 4.11" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the type of update. The second column is a description of the update and impacts it might have."}




