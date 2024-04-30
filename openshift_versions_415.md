---

copyright:
  years: 2023, 2024
lastupdated: "2024-04-30"


keywords: openshift, version, update, upgrade, 4.15, update openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# 4.15 version information and update actions
{: #cs_versions_415}

Review information about version 4.15 of {{site.data.keyword.openshiftlong_notm}}. This version is based on Kubernetes version {{site.data.keyword.openshift_415_kube_version}}. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [Red Hat {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_versions) and the version [4.15 release notes](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-release-notes){: external}.
{: tip}

![This badge indicates Kubernetes version 1.28 certification for {{site.data.keyword.openshiftlong_notm}}](images/certified-kubernetes-color.svg){: caption="Figure 1. Kubernetes version 1.28 certification badge" caption-side="bottom"}

{{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.28 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._





## Release timeline 
{: #release_timeline_415}

The following table includes the expected release timeline for version 4.15. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Supported | 4.15 / {{site.data.keyword.openshift_415_kube_version}} | {{site.data.keyword.openshift_415_release_date}} | {{site.data.keyword.openshift_415_unsupported_date}}`†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}} version 4.15." caption-side="bottom"}

## Preparing to update
{: #prep-up-415}

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) to version 4.15. This information summarizes updates that are likely to have an impact on deployed apps when you update.
{: shortdesc}

The OpenShift Data Foundation and the cluster-autoscaler add-ons do not support {{site.data.keyword.openshiftlong_notm}} version 4.15 with CoreOS worker nodes.
{: note}

The backup and restore Helm chart is supported on {{site.data.keyword.openshiftlong_notm}} 4.15 clusters. However, only the COS direct endpoints are supported. For example: `s3.direct.us.cloud-object-storage.appdomain.cloud`.
{: note}

[Portworx](https://cloud.ibm.com/docs/openshift?topic=openshift-storage_portworx_about) does not yet support {{site.data.keyword.openshiftlong_notm}} version 4.15 clusters. Do not update your cluster to version 4.15 if Portworx is installed.
{: note}

{{site.data.keyword.openshiftlong_notm}} version 4.15 clusters do not yet support [Rotating CA certificates in your cluster](/docs/openshift?topic=openshift-cert-rotate). Do not update your cluster to version 4.15 if this support is required.
{: note}


### Update before master
{: #415_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| --- | --- |
| **Unsupported:** Deprecated and removed OpenShift features | For more information, review the [OpenShift version 4.15 deprecated and removed features](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-deprecated-removed-features) and [Preparing to update to OpenShift Container Platform 4.15](https://docs.openshift.com/container-platform/4.15/updating/preparing_for_updates/updating-cluster-prepare.html) for possible actions required. |
| Known OpenShift issues | For more information, review the [OpenShift version 4.15 known issues](https://docs.openshift.com/container-platform/4.15/release_notes/ocp-4-15-release-notes.html#ocp-4-15-known-issues) for possible actions required. |
| Upgrade requires OpenShift cluster version currency | A cluster master upgrade is canceled when the OpenShift cluster version status indicates that an update is already in progress. See [Why does OpenShift show the cluster version is down-level?](/docs/openshift?topic=openshift-ts-cluster-version-downlevel) for details. |
| Upgrade requires resolution to OpenShift cluster version upgradeable conditions | A cluster master upgrade will now be cancelled if the OpenShift cluster version `Upgradeable` status condition indicates that the cluster is not upgradeable. See [Why do I see a `Cannot complete cluster master upgrade` message?](/docs/openshift?topic=openshift-ts-cluster-master-upgrade) for details. |
{: caption="Changes to make before you update the master to Red Hat OpenShift 4.15" caption-side="bottom"}

## Checking the `Upgradeable` status of your cluster
{: #status-check-415}

Run the following command to check the `Upgradeable` status of your cluster.

```sh
oc get clusterversion version -o json | jq '.status.conditions[] | select(.type == "Upgradeable")'
```
{: pre}

Example output where the `Upgradeable` status is `False`.

```sh
{
  "lastTransitionTime": "2023-10-04T15:55:54Z",
  "message": "Kubernetes 1.27 and therefore OpenShift 4.15 remove several APIs which require admin consideration. Please see the knowledge article https://access.redhat.com/articles/6958395 for details and instructions.",
  "reason": "AdminAckRequired",
  "status": "False",
  "type": "Upgradeable"
}
```
{: screen}

If the `Upgradeable` status is `False`, the condition information provides instructions that must be followed before upgrading. For more information, see [Providing the administrator acknowledgment](https://docs.openshift.com/container-platform/4.15/updating/preparing_for_updates/updating-cluster-prepare.html#update-preparing-ack_updating-cluster-prepare){: external}.

## Important networking changes for VPC clusters created at version 4.15
{: #understand-sbd}

Beginning with version 4.15, {{site.data.keyword.openshiftlong_notm}} introduced a new security feature for VPC clusters called Secure by Default Cluster VPC Networking.

At a high-level, the security posture for {{site.data.keyword.openshiftlong_notm}} VPC clusters has changed from allowing all outbound traffic then providing users with mechanisms to selectively block traffic as needed to now blocking all traffic that is not crucial to cluster functionality and providing users with mechanisms to selectively allow traffic as needed.

When you provision a new {{site.data.keyword.openshiftlong_notm}} VPC cluster at version 4.15 or later, the default provisioning behavior is to allow only the traffic that is necessary for the cluster to function. All other access is blocked. To implement Secure by Default Networking, there are changes to the default VPC security groups settings as well as new Virtual Private Endpoints (VPEs) for common IBM services.

Some key notes for Secure by Default Networking are:

- Applies to VPC clusters only. Classic clusters are not impacted.

- Does not affect existing clusters. Existing clusters in your VPC will continue to function as they do today.

- Applies only to newly provisioned {{site.data.keyword.openshiftlong_notm}} clusters at version 4.15. The security group configurations for existing {{site.data.keyword.openshiftlong_notm}} clusters that are upgraded to version 4.15, including any customizations you've made, are not changed.

- The default behavior for clusters created at version 4.15 and later is to enable Secure by Default outbound traffic protection. However, new parameters in the UI, CLI, API, and Terraform allow you to disable this feature. You can also enable and disable outbound traffic protection after you create a cluster.

- If your VPC uses a custom DNS resolver, provisioning a new version 4.15 cluster automatically adds rules allowing traffic through the resolver IP addresses on your IKS-managed security group (`kube-<clusterID>`).


For an overview of Secure by Default Cluster VPC networking, including the security groups, rules, and VPEs that are created by default, see [Understanding Secure by Default Cluster VPC Networking](/docs/openshift?topic=openshift-vpc-security-group-reference).



### Which connections are allowed?
{: #sbd-allowed-connections}

In VPC clusters with Secure by Default outbound traffic protection enabled, the following connections are allowed. 

- Accessing the internal IBM `*.icr.io` registries to pull necessary container images via a VPE gateway.
- Accessing the cluster master and {{site.data.keyword.openshiftlong_notm}} APIs via VPE gateways.
- Accessing other essential IBM services such as logging and monitoring over the private IBM network.
- Accessing IBM Cloud DNS.


### Which connections are blocked?
{: #sbd-blocked-connections}

Review the following examples of connections that are blocked by default. Note that you can selectively enable outbound traffic to these or other external sources that your app needs.

- Pulling images from public registries such as quay.io and Docker Hub.
- Accessing the Red Hat Marketplace and OperatorHub.
- Accessing any service over the public network.


### Changes to worker-to-master backup communication
{: #backup-considerations}

VPC cluster workers use the private network to communicate with the cluster master. Previously, for VPC clusters that had the public service endpoint enabled, if the private network was blocked or unavailable, then the cluster workers could fall back to using the public network to communicate with the cluster master.

In clusters with Secure by Default outbound traffic protection, falling back to the public network is not an option because public outbound traffic from the cluster workers is blocked. You might want to disable outbound traffic protection to allow this public network backup option, however, there is a better alternative. Instead, if there a temporary issue with the worker-to-master connection over the private network, then, at that time, you can add a temporary security group rule to the `kube-clusterID` security group to allow outbound traffic to the cluster master `apiserver` port. This way you allow only traffic for the `apiserver` instead of all traffic. Later, when the problem is resolved, you can remove the temporary rule.


## Allowing outbound traffic after creating a 4.15 cluster
{: #sbd-allow-outbound-after}

If you created a version 4.15 cluster with outbound traffic protection enabled, your apps or services might experience downtime due to dependencies that require external network connections. Review the following options for enabling outbound traffic selectively or allowing all outbound traffic.

For more information, see [Managing outbound traffic protection in VPC clusters](/docs/openshift?topic=openshift-sbd-allow-outbound).


## Common issues and troubleshooting 
{: #sbd-common-ts}

- [After enabling outbound traffic protection on my 4.15 cluster, my app no longer works](/docs/openshift?topic=openshift-ts-sbd-app-not-working).
- [When I try to create version 4.15 cluster, I see a quota error](/docs/openshift?topic=openshift-ts-sbd-cluster-create-quota).
- [When I update my cluster to secure by default, my nodeport app no longer works](/docs/openshift?topic=openshift-ts-sbd-nodeport-not-working).
- [Why do I see DNS failures after adding a custom DNS resolver?](/docs/openshift?topic=openshift-ts-sbd-custom-dns).
- [After creating a version 4.15 cluster, applications running in other clusters in my VPC are failing](/docs/openshift?topic=openshift-ts-sbd-other-clusters).

