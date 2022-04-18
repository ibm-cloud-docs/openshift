---

copyright:
  years: 2014, 2022
lastupdated: "2022-04-18"

keywords: openshift, version, update, upgrade

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# 4.9 version information and update actions
{: #cs_versions_49}

Review information about version 4.9 of {{site.data.keyword.openshiftlong_notm}}, released 09 Feb 2022. This version is based on Kubernetes version 1.22. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [Red Hat OpenShift on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_changelog).
{: tip}

![This badge indicates Kubernetes version 1.22 certification for {{site.data.keyword.containerlong_notm}}](images/certified_kubernetes_1x22.svg)

{{site.data.keyword.containerlong_notm}} is a Certified Kubernetes product for version 1.22 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

## Release timeline 
{: #release_timeline_49}

The following table includes the expected release timeline for version 4.9. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Supported | 4.9 / 1.22 | 09 Feb 2022 | May 2023`†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}} version 4.9." caption-side="top"}
{: summary="The rows are read from left to right. The first column is the supported status, the second column is OpenShift and Kubernetes version number. The third column is the release date. The fourth column is the unsupported date."}

## Preparing to update
{: #prep-up-49}

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) to version 4.9. This information summarizes updates that are likely to have and impact on deployed apps when you update.
{: shortdesc}

### Update before master
{: #49_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| ---- | ----------- | 
| **Unsupported:** Deprecated and removed OpenShift features | For more information, review [OpenShift version 4.9 deprecated and removed features](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html#ocp-4-9-deprecated-removed-features){: external}. |
| **Unsupported:**  Beta versions of numerous Kubernetes APIs | For more information, review [Preparing to upgrade to OpenShift Container Platform 4.9](https://access.redhat.com/articles/6329921){: external}, [Kubernetes API and Feature Removals In 1.22: Here’s What You Need To Know](https://kubernetes.io/blog/2021/07/14/upcoming-changes-in-kubernetes-1-22/){: external} and [Deprecated API Migration Guide](https://kubernetes.io/docs/reference/using-api/deprecation-guide/#v1-22){: external}. See [Deprecation Warnings](https://kubernetes.io/blog/2020/09/03/warnings/#deprecation-warnings){: external} for methods to identify use of deprecated APIs. Warnings for components provided by the Red Hat OpenShift on IBM Cloud cluster install can be ignored since they will be handled during the update. Note that {{site.data.keyword.openshiftlong_notm}} cluster administrators do not need to provide a manual acknowledgment before the cluster can be upgraded, as mentioned in this Red Hat [article](https://access.redhat.com/articles/6329921){: external}. |
{: caption="Changes to make before you update the master to {{site.data.keyword.redhat_openshift_notm}} 4.9" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the type of update. The second column is a description of the update and impacts it might have."}


