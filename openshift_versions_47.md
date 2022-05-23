---

copyright:
  years: 2014, 2022
lastupdated: "2022-05-23"

keywords: openshift, version, update, upgrade

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# 4.7 version information and update actions
{: #cs_versions_47}

Review information about version 4.7 of {{site.data.keyword.openshiftlong_notm}}, released 09 Jun 2021. This version is based on Kubernetes version 1.20. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [Red Hat OpenShift on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_changelog).
{: tip}

![This badge indicates Kubernetes version 1.20 certification for {{site.data.keyword.containerlong_notm}}](images/certified_kubernetes_1x20.svg)

{{site.data.keyword.containerlong_notm}} is a Certified Kubernetes product for version 1.20 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

## Release timeline 
{: #release_timeline_47}

The following table includes the expected release timeline for version 4.7. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Supported | 4.7 / 1.20 | 09 Jun 2021 | Dec 2022`†` |
{: caption="Release history for Red Hat OpenShift version 4.7." caption-side="top"}

## Preparing to update
{: #prep-up-47}

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) to version 4.7. This information summarizes updates that are likely to have and impact on deployed apps when you update.
{: shortdesc}


### Update before master
{: #47_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| ---- | ----------- |
| Kubernetes snapshot CRDs | {{site.data.keyword.containerlong_notm}} installs Kubernetes snapshot custom resource definition (CRD) version `v1beta1`. If you use other Kubernetes snapshot CRD versions `v1` or `v1alpha1`, you must change the version to `v1beta1`. To check the currently installed version of your snapshot CRDs, run `grep snapshot.storage.k8s.io <<(kubectl get apiservices)`. Follow the Kubernetes documentation to [Upgrade from v1alpha1 to v1beta1](https://github.com/kubernetes-csi/external-snapshotter#upgrade-from-v1alpha1-to-v1beta1){: external} to make sure that your snapshot CRDs are at the correct `v1beta1` version. The steps to downgrade from version `v1` to `v1beta1` are the same as those to upgrade from `v1alpha1`. Do not follow the instructions to upgrade from version `v1beta1` to version `v1`. |
| **Unsupported:** Deprecated and removed {{site.data.keyword.redhat_openshift_notm}} features | For more information, review the [{{site.data.keyword.redhat_openshift_notm}} version 4.7 deprecated and removed features](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-deprecated-removed-features){: external}. |
{: caption="Changes to make before you update the master to Red Hat OpenShift 4.7" caption-side="top"}



