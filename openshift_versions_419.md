---

copyright:
  years: 2024, 2025
lastupdated: "2025-10-17"


keywords: openshift, version, update, upgrade, 4.19, update openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# 4.19 version information and update actions
{: #cs_versions_419}

Review information about version 4.19 of {{site.data.keyword.openshiftlong_notm}}. This version is based on Kubernetes version {{site.data.keyword.openshift_419_kube_version}}. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [Red Hat {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_versions) and the version [4.19 release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/release_notes/index){: external}.
{: tip}


![This badge indicates Kubernetes version 1.32 certification for {{site.data.keyword.openshiftlong_notm}}](images/certified-kubernetes-color.svg){: caption="Kubernetes version 1.32 certification badge" caption-side="bottom"}

{{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.32 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._



## Release timeline 
{: #release_timeline_419}

The following table includes the expected release timeline for version 4.19. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Supported | 4.19 / {{site.data.keyword.openshift_419_kube_version}} | {{site.data.keyword.openshift_419_release_date}} | {{site.data.keyword.openshift_419_unsupported_date}}`†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}} version 4.19." caption-side="bottom"}


## Preparing to update
{: #prep-up-419}

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) to version 4.19. This information summarizes updates that are likely to have an impact on deployed apps when you update.
{: shortdesc}

For Satellite clusters: The 4.19 RHCOS image is not yet supported in Satellite. To create a CoreOS-enabled Satellite cluster with version 4.19, you must provision an RHCOS host at version 4.18 or earlier and attach the host to your location. Then, assign the host to your 4.19 cluster. After the host is assigned to your cluster, it automatically updates to match the Red Hat OpenShift version of the cluster, including 4.19. 
{: important}

The [Satellite Location Sizing Requirements](/docs/satellite?topic=satellite-location-sizing) for hosting {{site.data.keyword.openshiftlong_notm}} version 4.19 clusters are the same regardless of whether the location is RHEL (non-CoreOS) or CoreOS-enabled. The requirements for location nodes are the same as those for [CoreOS-enabled locations](/docs/satellite?topic=satellite-location-sizing#control-plane-how-many-clusters-rhcos).
{: important}

[Portworx](/docs/containers?topic=containers-storage_portworx_about) does not yet support version 4.19. Do not upgrade your cluster to version 4.19 if your apps use Portworx. For more information, see [Supported OpenShift versions](https://docs.portworx.com/portworx-enterprise/platform/ibm-cloud#supported-openshift-versions){: external}
{: important}


### Update before master
{: #419_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

For clusters that run version 4.19 or later, you can use the `oc adm upgrade status` command to check the update status of your cluster master during a master version update. For more information, see [Viewing cluster upgrade status with the `oc adm upgrade status` command](/docs/openshift?topic=openshift-upgrade-status).
{: tip}

| Type | Description |
| ---- | ---- |
| Preparing to update OpenShift | For more information, review the [Preparing to update to OpenShift Container Platform 4.19](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/updating_clusters/preparing-to-update-a-cluster){: external} for possible actions required. The etcd backup, version selection, and SDN removal upgrade preparation actions do not apply to Red Hat OpenShift on IBM Cloud clusters since etcd backups and version selection actions are handled for you, and Calico is used instead of SDN. |
| Deprecated and removed OpenShift features | For more information, review the [OpenShift Container Platform version 4.19 deprecated and removed features](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/release_notes/ocp-4-19-release-notes#ocp-4-19-deprecated-removed-features_release-notes){: external} for possible actions required. |
| Upgrade requires administrator acknowledgment | After you have evaluated your cluster for any removed APIs and have migrated any removed APIs, you can acknowledge that your cluster is ready to upgrade from OpenShift Container Platform 4.18 to 4.19.. See [Providing the administrator acknowledgment](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/updating_clusters/preparing-to-update-a-cluster#update-preparing-ack_updating-cluster-prepare){: external} for details. |
| Known OpenShift issues | For more information, review the [OpenShift Container Platform version 4.19 known issues](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/release_notes/ocp-4-19-release-notes#ocp-4-19-known-issues_release-notes){: external} for possible actions required. |
| Upgrade requires OpenShift cluster version currency | A cluster master upgrade will be canceled if the OpenShift cluster version status indicates that an update is already in progress. See [Why does OpenShift show the cluster version is not up to date?](/docs/openshift?topic=openshift-ts-cluster-version-downlevel) for details. |
| Upgrade requires resolution to OpenShift cluster version upgradeable conditions | A cluster master upgrade will be canceled if the OpenShift cluster version Upgradeable status condition indicates that the cluster is not upgradeable. To determine if the cluster is upgradeable, see [Checking the Upgradeable status of your cluster](/docs/openshift?topic=openshift-cs_versions_419#status-check-419){: external}. |
{: caption="Changes to make before you update the master to {{site.data.keyword.redhat_openshift_notm}} 4.19" caption-side="bottom"}



## Checking the `Upgradeable` status of your cluster
{: #status-check-419}

Run the following command to check the `Upgradeable` status of your cluster.

```sh
oc get clusterversion version -o json | jq '.status.conditions[] | select(.type == "Upgradeable")'
```
{: pre}

Example output where the `Upgradeable` status is `False`.

```sh
{
  "lastTransitionTime": "2024-11-17T19:29:34Z",
  "message": "Cluster operator operator-lifecycle-manager should not be upgraded between minor versions: ClusterServiceVersions blocking cluster upgrade: default/test is incompatible with OpenShift minor versions greater than 4.16",
  "reason": "IncompatibleOperatorsInstalled",
  "status": "False",
  "type": "Upgradeable"
}
```
{: screen}

If the `Upgradeable` status is `False`, the condition information provides instructions that must be followed before upgrading.
