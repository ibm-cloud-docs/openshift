---

copyright:
  years: 2024, 2025
lastupdated: "2025-03-13"


keywords: openshift, version, update, upgrade, 4.16, update openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# 4.16 version information and update actions
{: #cs_versions_416}

Review information about version 4.16 of {{site.data.keyword.openshiftlong_notm}}. This version is based on Kubernetes version {{site.data.keyword.openshift_416_kube_version}}. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [Red Hat {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_versions) and the version [4.16 release notes](https://docs.openshift.com/container-platform/4.16/release_notes/ocp-4-16-release-notes.html#ocp-4-16-release-notes){: external}.
{: tip}


![This badge indicates Kubernetes version 1.29 certification for {{site.data.keyword.openshiftlong_notm}}](images/certified-kubernetes-color.svg){: caption="Kubernetes version 1.29 certification badge" caption-side="bottom"}

{{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.29 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

## Release timeline 
{: #release_timeline_416}

The following table includes the expected release timeline for version 4.16. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Supported | 4.16 / {{site.data.keyword.openshift_416_kube_version}} | {{site.data.keyword.openshift_416_release_date}} | {{site.data.keyword.openshift_416_unsupported_date}}`†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}} version 4.16." caption-side="bottom"}

## Preparing to update
{: #prep-up-416}

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) to version 4.16. This information summarizes updates that are likely to have an impact on deployed apps when you update.
{: shortdesc}


The backup and restore Helm chart is supported on {{site.data.keyword.openshiftlong_notm}} 4.16 clusters. However, only the COS direct endpoints are supported. For example: `s3.direct.us.cloud-object-storage.appdomain.cloud`.
{: note}

VPC worker nodes provisioned for version 4.16 have VPC Instance Metadata Service enabled. For more information, see [About VPC Instance Metadata](/docs/vpc?topic=vpc-imd-about). 
{: note}


### Update before master
{: #416_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

For clusters that run version 4.16 or later, you can use the `oc adm upgrade status` command to check the update status of your cluster master during a master version update. For more information, see [Viewing cluster upgrade status with the `oc adm upgrade status` command](/docs/openshift?topic=openshift-upgrade-status).
{: tip}

| Type | Description |
| --- | --- |
| **Unsupported:** Deprecated and removed OpenShift features | For more information, review the [OpenShift Container Platform version 4.16 deprecated and removed features](https://docs.openshift.com/container-platform/4.16/release_notes/ocp-4-16-release-notes.html#ocp-4-16-deprecated-removed-features_release-notes){: external} and information for [preparing to update to OpenShift Container Platform 4.16](https://docs.openshift.com/container-platform/4.16/updating/preparing_for_updates/updating-cluster-prepare.html){: external} for possible actions required. The etcd backup and version selection upgrade preparation actions do not apply to {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud clusters since both of these actions are handled for you. |
| Known OpenShift issues | For more information, review the [OpenShift Container Platform version 4.16 known issues](https://docs.openshift.com/container-platform/4.16/release_notes/ocp-4-16-release-notes.html#ocp-4-16-known-issues_release-notes){: external} for possible actions required. |
| Upgrade requires OpenShift cluster version currency | A cluster master upgrade is canceled if the OpenShift cluster version status indicates that an update is already in progress. See [Why does OpenShift show the cluster version is not up to date?](/docs/openshift?topic=openshift-ts-cluster-version-downlevel) for more information. |
| Upgrade requires resolution to OpenShift cluster version upgradeable conditions | A cluster master upgrade is canceled if the OpenShift cluster version `Upgradeable` status condition indicates that the cluster is not upgradeable. To determine if the cluster is upgradeable, see [Checking the Upgradeable status of your cluster](/docs/openshift?topic=openshift-cs_versions_416#status-check-416). If the cluster is not in an upgradeable status, follow the relevant steps before upgrading. For more information, see [Providing the administrator acknowledgment](https://docs.openshift.com/container-platform/4.16/updating/preparing_for_updates/updating-cluster-prepare.html#update-preparing-ack_updating-cluster-prepare){: external}. |
| RHEL 9.2 micro-architecture requirement | {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud version 4.16 is now based on the RHEL 9.2 host operating system, which increases the [micro-architecture requirements](https://docs.openshift.com/container-platform/4.16/updating/preparing_for_updates/updating-cluster-prepare.html#rhel-micro-architecture-update-requirements){: external} to x86-64-v2. As a result, host machines for IBM Cloud {{site.data.keyword.satelliteshort}} must support x86-64-v2 architecture for any location that contains a version 4.16 cluster. See [Host system requirements](/docs/satellite?topic=satellite-host-reqs) for more information. In addition, client machines used to run `oc` client version 4.16 must also support x86-64-v2 architecture. Client machines, such as Ubuntu 20, that do not meet this micro-architecture requirement must use a RHEL 8 based `oc` version 4.16 client. Refer to the list of [available `oc` version 4.16 clients](https://mirror.openshift.com/pub/openshift-v4/clients/ocp/stable-4.16/){: external}. |
| Reduced access by unauthenticated users or groups | {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud version 4.16 reduces the permissions given to the `system:anonymous` user and `system:unauthenticated` group. This applies to new clusters only. If you wish to use the more secure defaults then remove the `system:unauthenticated` group from the `self-access-reviewers`, `system:oauth-token-deleters`, `system:scope-impersonation`, and `system:webhooks` cluster role bindings. See [Reduce unauthenticated user or group access](https://www.redhat.com/en/blog/what-you-need-to-know-red-hat-openshift-416){: external} for more information. |
| Legacy service account API token secrets are no longer generated for each service account | {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud version 4.16 no longer automatically generates a legacy service account API token secret for each service account. See [Legacy service account API token secrets are no longer generated for each service account](https://docs.openshift.com/container-platform/4.16/release_notes/ocp-4-16-release-notes.html){: external} for more information. | 
| Calico API server is a managed resource | {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud version 4.16 now manages the installation of and updates to the Calico API server component. If your cluster contains the `calico-apiserver` namespace, then you must uninstall the Calico API server before upgrading. |
| Default OpenShift cluster monitoring configuration | {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud version 4.16 now creates a default OpenShift cluster monitoring configuration if one doesn't exist. This new default configuration sets a 10 GB retention size which may impact the metrics retention for your cluster. See [Built-in {{site.data.keyword.redhat_openshift_notm}} monitoring tools](https://cloud.ibm.com/docs/openshift?topic=openshift-health-monitor#built-in-mon-tools){: external} for instructions on how you can configure the monitoring stack to use persistent storage, change the metrics retention policies, or run Prometheus on dedicated nodes. |
{: caption="Changes to make before you update the master to {{site.data.keyword.redhat_openshift_notm}} 4.16" caption-side="bottom"}

## Update after master
{: #416_after}

| Type | Description |
| --- | --- |
| **Unsupported:** `localhost` `NodePort` services | To further reduce security risks related to [CVE-2020-8558](https://github.com/advisories/GHSA-wqv3-8cm6-h6wg){: external}, `localhost` access to `NodePort` services is disabled. If your apps rely on this behavior, update them to the node private IP address instead. |
{: caption="Changes to make after you update the master to {{site.data.keyword.redhat_openshift_notm}} 4.16" caption-side="bottom"}

## Checking the `Upgradeable` status of your cluster
{: #status-check-416}

Run the following command to check the `Upgradeable` status of your cluster.

```sh
oc get clusterversion version -o json | jq '.status.conditions[] | select(.type == "Upgradeable")'
```
{: pre}

Example output where the `Upgradeable` status is `False`.

```sh
{
  "lastTransitionTime": "2023-10-04T15:55:54Z",
  "message": "Kubernetes 1.29 and therefore OpenShift 4.16 remove several APIs which require admin consideration. Please see the knowledge article  for details and instructions.",
  "reason": "AdminAckRequired",
  "status": "False",
  "type": "Upgradeable"
}
```
{: screen}

If the `Upgradeable` status is `False`, the condition information provides instructions that must be followed before upgrading. For more information, see [Providing the administrator acknowledgment](https://docs.openshift.com/container-platform/4.16/updating/preparing_for_updates/updating-cluster-prepare.html#update-preparing-ack_updating-cluster-prepare){: external}.


## RHEL 9
{: #416_rhel9}

RHEL 9 is available for Classic or VPC clusters that run version 4.16.

You can provision a new cluster with RHEL 9 in the console by specifying the RHEL operating system for your worker node flavor or [in the CLI](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-vpc-gen2) by including the `--operating-system REDHAT_9_64` option when you run the `ibmcloud oc cluster create` command. 

If you upgrade an existing cluster to version 4.16 and want your worker nodes to run RHEL 9, you must [follow the steps to migrate your worker nodes](/docs/openshift?topic=openshift-rhel_migrate).

For more information on RHEL 9, see the [Red Hat OpenShift release notes](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/9.4_release_notes/index){: external}. 
