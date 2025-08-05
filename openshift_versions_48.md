---

copyright:
  years: 2014, 2025
lastupdated: "2025-08-05"


keywords: openshift, version, update, upgrade

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}





# 4.8 version information and update actions
{: #cs_versions_48}



This version is no longer supported. Update your cluster to a [supported version](/docs/openshift?topic=openshift-openshift_versions) as soon as possible.
{: important}



Review information about version 4.8 of {{site.data.keyword.openshiftlong_notm}}, released 29 Sept 2021. This version is based on Kubernetes version 1.21. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [Red Hat OpenShift on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_versions).
{: tip}

![This badge indicates Kubernetes version 1.21 certification for {{site.data.keyword.openshiftlong_notm}}](images/certified-kubernetes-color.svg){: caption="Kubernetes version 1.21 certification badge" caption-side="bottom"}

{{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.21 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

## Release timeline 
{: #release_timeline_48}

The following table includes the expected release timeline for version 4.8. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| No | 4.8 / 1.21 | 29 September 2021 | 27 April 2023`†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}} version 4.8." caption-side="bottom"}


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
| **Unsupported:** Deprecated and removed {{site.data.keyword.redhat_openshift_notm}} features | For more information, review [{{site.data.keyword.redhat_openshift_notm}} version 4.8 deprecated and removed features](https://docs.redhat.com/documentation/openshift_container_platform/4.8/html/release_notes/ocp-4-8-release-notes#ocp-4-8-deprecated-removed-features){: external}. |
| Container runtime default security context capabilities | The container runtime (for example, CRI-O) default security context capabilities have been changed to match Red Hat OpenShift Container Platform (OCP). `NET_RAW` and `SYS_CHROOT` have been removed. This brings the security behavior of containers inline with OCP. If your app requires either of these capabilities and does not list them in the container or pod `securityContext`, then the app must be changed to include these capabilities. If these changes are not made, your microservices might fail to start and you might see a `permission denied` error. Applications developed for OCP already have the necessary changes.  |
| Strongswan users | If you are using Strongswan in your cluster, then update at least version 2.7.11 of Strongswan before you update your cluster master to {{site.data.keyword.redhat_openshift_notm}} 4.8. In versions of Strongswan earlier than 2.7.11, certain [Strongswan configuration options](/docs/openshift?topic=openshift-vpn#vpn-setup) do not work with the {{site.data.keyword.redhat_openshift_notm}} 4.8 master. |
{: caption="Changes to make before you update the master to {{site.data.keyword.redhat_openshift_notm}} 4.8" caption-side="bottom"}
