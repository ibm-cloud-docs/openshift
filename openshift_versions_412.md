---

copyright:
  years: 2023, 2023
lastupdated: "2023-04-05"

keywords: openshift, version, update, upgrade, 4.12, update openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}





# 4.12 version information and update actions
{: #cs_versions_412}

Review information about version 4.12 of {{site.data.keyword.openshiftlong_notm}}, released 23 Feb 2023. This version is based on Kubernetes version 1.25. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [Red Hat {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_changelog) and the version [4.12 blog](https://cloud.redhat.com/blog/whats-new-in-red-hat-openshift-4.12-blog){: external}.
{: tip}

![This badge indicates Kubernetes version 1.25 certification for {{site.data.keyword.openshiftlong_notm}}](images/certified-kubernetes-color.svg){: caption="Figure 1. Kubernetes version 1.25 certification badge" caption-side="bottom"}

{{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.25 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

## Release timeline 
{: #release_timeline_412}

The following table includes the expected release timeline for version 4.12. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Supported | 4.12 / 1.25 | 23 Feb 2023 | 26 Feb 2025`†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}} version 4.12." caption-side="bottom"}

## Preparing to update
{: #prep-up-412}

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) to version 4.12. This information summarizes updates that are likely to have an impact on deployed apps when you update.
{: shortdesc}

**Before you update**: Review the following list of considerations and limitations before you update your cluster to version 4.11. Some entries are relevant to specific add-ons. To check if you have an add-on enabled in your cluster, run `ibmcloud oc cluster addon ls`. 

Calico BGP password
:   When you upgrade your cluster to version 4.12, a [BGP password](https://docs.tigera.io/calico/latest/reference/resources/bgppeer#bgppassword){: external} is automatically configured for Calico. This might disrupt pod networking for several seconds while the BGP password configuration is applied. 

CoreOS
:   Red Hat CoreOS-enabled IBM Cloud Satellite locations are not currently supported on clusters that run version 4.12.

### Update before master
{: #412_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| --- | --- |
| **Unsupported:** Deprecated and removed OpenShift features | For more information, review the [OpenShift version 4.12 deprecated and removed features](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-deprecated-removed-features){: external} and [Preparing to update to OpenShift Container Platform 4.12](https://docs.openshift.com/container-platform/4.12/updating/updating-cluster-prepare.html#updating-cluster-prepare){: external} for actions that might be required. |
| Known OpenShift issues | For information on actions that might be required, review the [OpenShift version 4.12 known issues](https://docs.openshift.com/container-platform/4.12/release_notes/ocp-4-12-release-notes.html#ocp-4-12-known-issues){: external}. |
| Pod security admission synchronization | If an Operator is installed in a user-created `openshift-*` namespace, synchronization is turned on by default after a cluster service version (CSV) is created in the namespace. The synchronized label inherits the permissions of the service accounts in the namespace. See [Controlling pod security admission synchronization](https://docs.openshift.com/container-platform/4.12/authentication/understanding-and-managing-pod-security-admission.html#security-context-constraints-psa-opting_understanding-and-managing-pod-security-admission){: external} for actions that might be required. |
| Application updates required for `natPortRange` changes. | If your app requires a larger number of egress network connections from `pod-network` pods to a destination that is external to the cluster, you might need to make updates. This applies if your app has more than 30,000 egress connections open on a single worker node simultaneously, or over 30,000 egress connections open on a single worker node within a few minutes. For more information, see [Why am I running out of SNAT ports for egress connections from pods in my cluster?](/docs/openshift?topic=openshift-ts-network-snat-125). |
{: caption="Changes to make before you update the master to Red Hat OpenShift 4.12" caption-side="bottom"}

