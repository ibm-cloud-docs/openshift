---

copyright:
  years: 2024, 2025
lastupdated: "2025-03-13"


keywords: openshift, version, update, upgrade, 4.17, update openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# 4.17 version information and update actions
{: #cs_versions_417}

Review information about version 4.17 of {{site.data.keyword.openshiftlong_notm}}. This version is based on Kubernetes version {{site.data.keyword.openshift_417_kube_version}}. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [Red Hat {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_versions) and the version [4.17 release notes](https://docs.openshift.com/container-platform/4.17/release_notes/ocp-4-17-release-notes.html#ocp-4-17-release-notes){: external}.
{: tip}


![This badge indicates Kubernetes version 1.30 certification for {{site.data.keyword.openshiftlong_notm}}](images/certified-kubernetes-color.svg){: caption="Kubernetes version 1.30 certification badge" caption-side="bottom"}

{{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.30 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._


## Release timeline 
{: #release_timeline_417}

The following table includes the expected release timeline for version 4.17. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Supported | 4.17 / {{site.data.keyword.openshift_417_kube_version}} | {{site.data.keyword.openshift_417_release_date}} | {{site.data.keyword.openshift_417_unsupported_date}}`†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}} version 4.17." caption-side="bottom"}


## Preparing to update
{: #prep-up-417}

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) to version 4.17. This information summarizes updates that are likely to have an impact on deployed apps when you update.
{: shortdesc}


### Update before master
{: #417_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

For clusters that run version 4.17 or later, you can use the `oc adm upgrade status` command to check the update status of your cluster master during a master version update. For more information, see [Viewing cluster upgrade status with the `oc adm upgrade status` command](/docs/openshift?topic=openshift-upgrade-status).
{: tip}

| Type | Description |
| --- | --- |
| Preparing to update OpenShift | For more information, review the [Preparing to update to OpenShift Container Platform 4.17](https://docs.openshift.com/container-platform/4.17/updating/preparing_for_updates/updating-cluster-prepare.html) for possible actions required. The etcd backup and version selection upgrade preparation actions do not apply to Red Hat OpenShift on IBM Cloud clusters since both of these actions are handled for you. |
| Deprecated and removed OpenShift features | For more information, review the [OpenShift Container Platform version 4.17 deprecated and removed features](https://docs.openshift.com/container-platform/4.17/release_notes/ocp-4-17-release-notes.html#ocp-4-17-deprecated-removed-features_release-notes) for possible actions required. |
| Known OpenShift issues | For more information, review the [OpenShift Container Platform version 4.17 known issues](https://docs.openshift.com/container-platform/4.17/release_notes/ocp-4-17-release-notes.html#ocp-4-17-known-issues_release-notes) for possible actions required. |
| Upgrade requires OpenShift cluster version currency | A cluster master upgrade will be canceled if the OpenShift cluster version status indicates that an update is already in progress. See [Why does OpenShift show the cluster version is not up to date?](/docs/openshift?topic=openshift-ts-cluster-version-downlevel) for details. |
| Upgrade requires resolution to OpenShift cluster version upgradeable conditions | A cluster master upgrade will be canceled if the OpenShift cluster version `Upgradeable` status condition indicates that the cluster is not upgradeable. To determine if the cluster is upgradeable, see [Checking the Upgradeable status of your cluster](/docs/openshift?topic=openshift-cs_versions_417#status-check-417). |
| RHEL 9.2 micro-architecture requirement | Red Hat OpenShift on IBM Cloud version 4.17 is based on the RHEL 9.2 host operating system thus increasing the [micro-architecture requirements](https://docs.openshift.com/container-platform/4.17/updating/preparing_for_updates/updating-cluster-prepare.html#rhel-micro-architecture-update-requirements){: external} to x86-64-v2. As a result, host machines for IBM Cloud Satellite must support x86-64-v2 architecture for any location that contains a Red Hat OpenShift on IBM Cloud version 4.17 cluster. See [Host system requirements](/docs/satellite?topic=satellite-host-reqs) for details. In addition, client machines used to run `oc` client version 4.17 must also support x86-64-v2 architecture. Client machines, such as Ubuntu 20, that do not meet this micro-architecture requirement must use a RHEL 8 based `oc` version 4.17 client. Review the list of available `oc` [version 4.17 clients](https://mirror.openshift.com/pub/openshift-v4/clients/ocp/stable-4.17/){: external} |
| RHEL 9 is the default operating system | RHEL 9 is now the default operating system for Red Hat OpenShift on IBM Cloud version 4.17 Classic or VPC clusters. Upgrading a cluster to version 4.17 does not change the operating system for an existing worker pool. For more information and possible migration actions related to RHEL 9, see [Migrating to a new Red Hat Enterprise Linux version](/docs/openshift?topic=openshift-rhel_migrate). |
| Node label `node-role.kubernetes.io/master` removed | VPC clusters with CoreOS enabled no longer set the `node-role.kubernetes.io/master` node label for version 4.17 worker nodes. If your apps rely on this node label, update them accordingly. |
{: caption="Changes to make before you update the master to {{site.data.keyword.redhat_openshift_notm}} 4.17" caption-side="bottom"}

## Checking the `Upgradeable` status of your cluster
{: #status-check-417}

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


## RHEL 9
{: #417_rhel9}

RHEL 9 is available for Classic or VPC clusters that run version 4.17.

You can provision a new cluster with RHEL 9 in the console by specifying the RHEL operating system for your worker node flavor or [in the CLI](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-vpc-gen2) by including the `--operating-system REDHAT_9_64` option when you run the `ibmcloud oc cluster create` command. 

If you upgrade an existing cluster to version 4.17 and want your worker nodes to run RHEL 9, you must [follow the steps to migrate your worker nodes](/docs/openshift?topic=openshift-rhel_migrate).

For more information on RHEL 9, see the [Red Hat OpenShift release notes](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/9.4_release_notes/index){: external}. 
