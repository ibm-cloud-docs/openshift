---

copyright:
  years: 2022, 2022
lastupdated: "2022-07-07"

keywords: openshift, version, update, upgrade, 4.10

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# 4.10 version information and update actions
{: #cs_versions_410}

Review information about version 4.10 of {{site.data.keyword.openshiftlong_notm}}, released 27 April 2022. This version is based on Kubernetes version 1.23. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [Red Hat OpenShift on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_changelog) and the version [4.10 blog](https://cloud.redhat.com/blog/introducing-red-hat-openshift-4.10){: external}
{: tip}

RHEL 7 worker nodes with {{site.data.keyword.openshiftlong_notm}} version 4.10 clusters is deprecated and becomes unsupported after support for RHEL 8 is available. After RHEL 8 is available, you must replace your RHEL 7 worker nodes with RHEL 8 worker nodes.
{: important}

[Extended update support (EUS) updates](https://docs.openshift.com/container-platform/4.10/updating/preparing-eus-eus-upgrade.html){: external} are not available at this time for {{site.data.keyword.openshiftlong_notm}} version 4.10 clusters.
{: note}


![This badge indicates Kubernetes version 1.23 certification for {{site.data.keyword.containerlong_notm}}](images/certified_kubernetes_1x23.svg)

{{site.data.keyword.containerlong_notm}} is a Certified Kubernetes product for version 1.23 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._



## Release timeline 
{: #release_timeline_410}

The following table includes the expected release timeline for version 4.10. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Supported | 4.10 / 1.23 | 27 April 2022 | October 2023`†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}} version 4.10." caption-side="top"}
{: summary="The rows are read from left to right. The first column is the supported status, the second column is OpenShift and Kubernetes version number. The third column is the release date. The fourth column is the unsupported date."}

## Preparing to update
{: #prep-up-410}

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) to version 4.10. This information summarizes updates that are likely to have an impact on deployed apps when you update.
{: shortdesc}

### Update before master
{: #410_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}


| Type | Description |
| --- | --- |
| **Unsupported:** Deprecated and removed OpenShift features | For more information, review the [OpenShift version 4.10 deprecated and removed features](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-deprecated-removed-features){: external}. |
| Kubernetes API server metrics job name changed | Kubernetes API server metrics now use job `kube-apiserver` rather than `cluster-version-operator`. Update any custom metrics and alerts to use the new job name. |
{: caption="Changes to make before you update the master to {{site.data.keyword.redhat_openshift_notm}} 4.10" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the type of update. The second column is a description of the update and impacts it might have."}


