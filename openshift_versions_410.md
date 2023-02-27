---

copyright:
  years: 2022, 2023
lastupdated: "2023-02-27"

keywords: openshift, version, update, upgrade, 4.10

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}





# 4.10 version information and update actions
{: #cs_versions_410}

Review information about version 4.10 of {{site.data.keyword.openshiftlong_notm}}, released 27 April 2022. This version is based on Kubernetes version 1.23. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [the {{site.data.keyword.openshiftlong_notm}} version information](/docs/openshift?topic=openshift-openshift_changelog) and the version [4.10 blog](https://cloud.redhat.com/blog/introducing-red-hat-openshift-4.10){: external}
{: tip}

RHEL 8 is the only operating system for worker nodes created in version 4.10 clusters.
{: important}

If you have Portworx installed, follow the steps to upgrade your installation to use at least image version `2.11.4`. For more information, see [Upgrading Portworx to a specific version](/docs/openshift?topic=openshift-portworx).
{: important}

Gateway-enabled clusters on Classic infrastructure are deprecated and will be unsupported soon. The end of support dates are linked directly to the end of support of {{site.data.keyword.openshiftlong_notm}} version 4.9. Gateway-enabled clusters are not supported on version 4.10 and later. If your cluster is gateway-enabled cluster, plan to create a new cluster before support ends. If you need similar functionality, consider creating a cluster on VPC infrastructure.
{: important} 

[Extended update support (EUS) updates](https://docs.openshift.com/container-platform/4.10/updating/preparing-eus-eus-upgrade.html){: external} are not available at this time for {{site.data.keyword.openshiftlong_notm}} version 4.10 clusters.
{: note}


![This badge indicates Kubernetes version 1.23 certification for {{site.data.keyword.openshiftlong_notm}}](images/certified-kubernetes-color.svg){: caption="Figure 1. Kubernetes version 1.23 certification badge" caption-side="bottom"}

{{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.23 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._



## Release timeline 
{: #release_timeline_410}

The following table includes the expected release timeline for version 4.10. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Supported | 4.10 / 1.23 | 27 April 2022 | October 2023`†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}} version 4.10." caption-side="bottom"}

## Preparing to update
{: #prep-up-410}

If you want to upgrade a 4.9 cluster with RHEL 7 worker nodes to 4.10, [replace your RHEL 7 worker nodes](#410_rhel-migrate) with RHEL 8 worker nodes before you follow the steps to upgrade to version 4.10. 
{: important}

Gateway-enabled clusters
:    Classic clusters created with the `--gateway-enabled` option do not support RHEL 8 worker nodes, and therefore are not supported for version 4.10. You cannot update your cluster to version 4.10 if it has the gateway-enabled cluster controller installed.

### Update before master
{: #410_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}


| Type | Description |
| --- | --- |
| **Unsupported:** Deprecated and removed {{site.data.keyword.redhat_openshift_notm}} features | For more information, review the [{{site.data.keyword.redhat_openshift_notm}} version 4.10 deprecated and removed features](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-deprecated-removed-features){: external}. |
| Kubernetes API server metrics job name changed | Kubernetes API server metrics now use job `kube-apiserver` rather than `cluster-version-operator`. Update any custom metrics and alerts to use the new job name. |
| **Deprecated**: RHEL 7 | RHEL 7 is deprecated in version 4.10. [Migrate your worker nodes to RHEL 8](#410_rhel-migrate). |
{: caption="Changes to make before you update the master to {{site.data.keyword.redhat_openshift_notm}} 4.10" caption-side="bottom"}

## Migrating your worker nodes to RHEL 8
{: #410_rhel-migrate}

With the release of RHEL 8, the use of RHEL 7 worker nodes is deprecated in clusters that run version 4.10. You cannot upgrade RHEL 7 worker nodes to RHEL 8.

Instead, you must provision a new worker pool and then delete the previous worker pool. In versions 4.10 and later, worker nodes in the new worker pool run RHEL 8 by default. See [Migrating to a new Red Hat Enterprise Linux version](/docs/openshift?topic=openshift-rhel_migrate).






