---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-17"


keywords: openshift, version, update, upgrade, 4.13, update openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}





# 4.13 version information and update actions
{: #cs_versions_413}

Review information about version 4.13 of {{site.data.keyword.openshiftlong_notm}}. This version is based on Kubernetes version {{site.data.keyword.openshift_413_kube_version}}. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [Red Hat {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_versions) and the version [4.13 blog](https://www.redhat.com/blog/red-hat-openshift-413-now-available){: external}.
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



### Update before master
{: #413_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

Cluster master access for VPC clusters with a private service endpoint changed significantly from version 4.12. Before updating a cluster of this type, review the following information and consider what changes you must make before upgrading your cluster. Also, consider this before creating a new  4.13 cluster with only a private service endpoint.
{: important}

| Type | Description |
| --- | --- |
| **Unsupported:** Deprecated and removed OpenShift features | For more information, review the [OpenShift version 4.13 deprecated and removed features](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-deprecated-removed-features) and [Preparing to update to OpenShift Container Platform 4.13](https://docs.openshift.com/container-platform/4.13/updating/updating-cluster-prepare.html#updating-cluster-prepare) for possible actions required. |
| Known OpenShift issues | For more information, review the [OpenShift version 4.13 known issues](https://docs.openshift.com/container-platform/4.13/release_notes/ocp-4-13-release-notes.html#ocp-4-13-known-issues) for possible actions required. |
| Updated worker node metrics configuration | In order for your cluster to maintain pod and node metrics during the update, your cluster master must be at fix pack version [4.12.16_1545_openshift](/docs/openshift?topic=openshift-openshift_changelog_412&interface=ui#41216_1545_openshift_M) or later and your cluster worker nodes must be at fix pack version [4.12.19_1546_openshift](/docs/openshift?topic=openshift-openshift_changelog_412&interface=ui#41219_1546_openshift_W) or later. |
| Access changes for VPC clusters with a private service endpoint only  | - **Previously** In VPC clusters with a private service endpoint only, if you wanted to access the cluster through the Openshift Console, run terraform scripts, create a `kubeconfig` file via `oc login`, or make similar API calls that required oauth to get a token, then you needed to access the private service endpoint, which was in the format `https://cX00.private.us-south.containers.cloud.ibm.com:port`. This setup only required access to the IBM Cloud private network `166.8.0.0/14`.  \n - **Now** In Openshift 4.13 this behavior has changed. In addition to accessing the IBM Cloud private network, the client system also needs access to the VPC's private DNS resolution to be able to connect to IP addresses in the VPC that the cluster is in. This is due to a change to use the VPE gateway DNS name of the form `clusterID.vpe.private.us-south.containers.cloud.ibm.com:port` for access to the apiserver and the oauth server. Now, to access the Red Hat OpenShift console, run `oc login`, or make similar API calls, the client system must be able to resolve the VPE gateway DNS name and reach the VPE gateway in the VPC. You must setup your VPC VPN or other networking solution to be able to access the VPE gateway. For more information, see [Accessing VPC clusters through the VPE gateway](/docs/openshift?topic=openshift-access_cluster#vpc_vpe). It is important to set the IBM Cloud VPC Private DNS server addresses (`161.26.0.7` and `161.26.0.8`) as DNS resolvers and set routing towards IaaS services (`161.26.0.0/16`). |
{: caption="Changes to make before you update the master to Red Hat OpenShift 4.13" caption-side="bottom"}




