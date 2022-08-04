---

copyright:
  years: 2014, 2022
lastupdated: "2022-08-04"

keywords: openshift, version, update, upgrade

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# 4.8 version information and update actions
{: #cs_versions_48}

Review information about version 4.8 of {{site.data.keyword.openshiftlong_notm}}, released 29 Sep 2021. This version is based on Kubernetes version 1.21. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [Red Hat OpenShift on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_changelog).
{: tip}

![This badge indicates Kubernetes version 1.21 certification for {{site.data.keyword.containerlong_notm}}](images/certified_kubernetes_1x21.svg){: caption="Figure 1. Kubernetes version 1.21 certification badge" caption-side="bottom"}

{{site.data.keyword.containerlong_notm}} is a Certified Kubernetes product for version 1.21 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

## Release timeline 
{: #release_timeline_48}

The following table includes the expected release timeline for version 4.8. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Supported | 4.8 / 1.21 | 29 Sep 2021 | Feb 2023`†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}} version 4.8." caption-side="top"}
{: summary="The rows are read from left to right. The first column is the supported status, the second column is OpenShift and Kubernetes version number. The third column is the release date. The fourth column is the unsupported date."}

## Preparing to update
{: #prep-up-48}

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) to version 4.8. This information summarizes updates that are likely to have and impact on deployed apps when you update.
{: shortdesc}

### Update before master
{: #48_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| ---- | ----------- |
| **Unsupported:** Deprecated and removed OpenShift features | For more information, review [OpenShift version 4.8 deprecated and removed features](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-deprecated-removed-features){: external}. |
| Container runtime default security context capabilities | The container runtime (i.e. CRI-O) default security context capabilities have been changed to match Red Hat OpenShift Container Platform (OCP). `NET_RAW` and `SYS_CHROOT` have been removed. This brings the security behavior of containers in line with OCP. If your app requires either of these capabilities and does not list them in the container or pod `securityContext`, then the app must be changed to include these capabilities. If these changes are not made, your microservices might fail to start and you might see a `permission denied` error. Applications developed for OCP already have the necessary changes.  |
| Strongswan users | If you are using Strongswan in your cluster, then update at least version 2.7.11 of Strongswan before you update your cluster master to {{site.data.keyword.redhat_openshift_notm}} 4.8. In versions of Strongswan earlier than 2.7.11, certain [Strongswan configuration options](/docs/openshift?topic=openshift-vpn#vpn-setup) do not work with the {{site.data.keyword.redhat_openshift_notm}} 4.8 master. |
{: caption="Changes to make before you update the master to {{site.data.keyword.redhat_openshift_notm}} 4.8" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the type of update. The second column is a description of the update and impacts it might have."}


