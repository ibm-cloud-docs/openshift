---

copyright:
  years: 2023, 2023
lastupdated: "2023-06-27"

keywords: openshift, version, update, upgrade, 4.13, update openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}





# 4.13 version information and update actions
{: #cs_versions_413}

Review information about version 4.13 of {{site.data.keyword.openshiftlong_notm}}, released {{site.data.keyword.openshift_413_release_date}}. This version is based on Kubernetes version {{site.data.keyword.openshift_413_kube_version}}. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [Red Hat {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_versions) and the version [4.13 blog](https://www.redhat.com/en/blog/red-hat-openshift-413-now-available){: external}.
{: tip}



![This badge indicates Kubernetes version 1.26 certification for {{site.data.keyword.openshiftlong_notm}}](images/certified-kubernetes-color.svg){: caption="Figure 1. Kubernetes version 1.26 certification badge" caption-side="bottom"}

{{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.26 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._



## Release timeline 
{: #release_timeline_413}

The following table includes the expected release timeline for version 4.13. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Supported | 4.13 / {{site.data.keyword.openshift_413_kube_version}} | {{site.data.keyword.openshift_413_release_date}} | {{site.data.keyword.openshift_413_unsupported_date}}`†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}} version 4.13." caption-side="bottom"}

## Preparing to update
{: #prep-up-413}

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) to version 4.13. This information summarizes updates that are likely to have an impact on deployed apps when you update.
{: shortdesc}

Portworx
:   [Portworx](/docs/openshift?topic=openshift-storage_portworx_about) does not yet support {{site.data.keyword.openshiftlong_notm}} version 4.13 clusters. Do not update your cluster to version 4.13 if Portworx is installed.



### Update before master
{: #413_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| --- | --- |
| **Unsupported:** Deprecated and removed OpenShift features | For more information, review the [OpenShift version 4.13 deprecated and removed features](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-deprecated-removed-features) and [Preparing to update to OpenShift Container Platform 4.13](https://docs.openshift.com/container-platform/4.13/updating/updating-cluster-prepare.html#updating-cluster-prepare) for possible actions required. |
| Known OpenShift issues | For more information, review the [OpenShift version 4.13 known issues](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-known-issues) for possible actions required. |
| Updated worker node metrics configuration | In order for your cluster to maintain pod and node metrics during the update, your cluster master must be at fix pack version [4.12.16_1545_openshift](/docs/openshift?topic=openshift-openshift_changelog_412&interface=ui#41216_1545_openshift_M) or later and your cluster worker nodes must be at fix pack version [4.12.19_1546_openshift](/docs/openshift?topic=openshift-openshift_changelog_412&interface=ui#41219_1546_openshift_W) or later. |
| OpenShift Console access changes on IBM Cloud VPC | **Previously**, {{site.data.keyword.openshiftlong_notm}} VPC clusters that have disabled their public service endpoint, provided Red Hat OpenShift console access via the private service endpoint URL (for example `https://cX00.private.us-south.containers.cloud.ibm.com:port`) which required the internet browser to reach the IBM Cloud private network with routing to 166.8.0.0/14. **Now**, the Red Hat OpenShift console for such clusters is accessible via the virtual private endpoint (VPE) gateway URL (for example `https://clusterID.vpe.private.us-south.containers.cloud.ibm.com:port`). The VPE gateway is created automatically for the cluster and it exists in the same VPC as the cluster. To access the Red Hat OpenShift console, the internet browser must be able to resolve the VPE gateway URL and reach the VPE gateway in the VPC. To enable the access, setup the VPC VPN or other networking solution to be able to access the VPE gateway. For more information, please see [Accessing VPC clusters through the VPE gateway](/docs/containers?topic=containers-access_cluster#vpc_vpe) documentation. It is important to set the IBM Cloud VPC Private DNS server addresses (`161.26.0.7` and `161.26.0.8`) as DNS resolvers and set routing towards IaaS services (`161.26.0.0/16`). |
{: caption="Changes to make before you update the master to Red Hat OpenShift 4.13" caption-side="bottom"}




