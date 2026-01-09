---

copyright:
  years: 2024, 2026
lastupdated: "2026-01-09"


keywords: openshift, version, update, upgrade, 4.15, update openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# 4.15 version information and update actions
{: #cs_versions_415}



This version is no longer supported. Update your cluster to a [supported version](/docs/openshift?topic=openshift-openshift_versions) as soon as possible.
{: important}



Review information about version 4.15 of {{site.data.keyword.openshiftlong_notm}}. This version is based on Kubernetes version {{site.data.keyword.openshift_415_kube_version}}. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [Red Hat {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_versions) and the version [4.15 release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.15/html/release_notes/ocp-4-15-release-notes){: external}.
{: tip}

![This badge indicates Kubernetes version 1.28 certification for {{site.data.keyword.openshiftlong_notm}}](images/certified-kubernetes-color.svg){: caption="Kubernetes version 1.28 certification badge" caption-side="bottom"}

{{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.28 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._


## Release timeline 
{: #release_timeline_415}

The following table includes the expected release timeline for version 4.15. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Deprecated | 4.15 / {{site.data.keyword.openshift_415_kube_version}} | {{site.data.keyword.openshift_415_release_date}} | {{site.data.keyword.openshift_415_unsupported_date}}`†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}} version 4.15." caption-side="bottom"}

## Preparing to update
{: #prep-up-415}

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) to version 4.15. This information summarizes updates that are likely to have an impact on deployed apps when you update.
{: shortdesc}

The backup and restore Helm chart is supported on {{site.data.keyword.openshiftlong_notm}} 4.15 clusters. However, only the COS direct endpoints are supported. For example: `s3.direct.us.cloud-object-storage.appdomain.cloud`.
{: note}


### Update before master
{: #415_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| --- | --- |
| **Unsupported:** Deprecated and removed OpenShift features | For more information, review the [OpenShift version 4.15 deprecated and removed features](https://docs.redhat.com/en/documentation/openshift_container_platform/4.15/html/release_notes/ocp-4-15-release-notes#ocp-4-15-deprecated-removed-features) and [Preparing to update to OpenShift Container Platform 4.15](https://docs.openshift.com/container-platform/4.15/updating/preparing_for_updates/updating-cluster-prepare.html) for possible actions required. |
| Known OpenShift issues | For more information, review the [OpenShift version 4.15 known issues](https://docs.redhat.com/en/documentation/openshift_container_platform/4.15/html/release_notes/ocp-4-15-release-notes#ocp-4-15-known-issues) for possible actions required. |
| Upgrade requires OpenShift cluster version currency | A cluster master upgrade is canceled when the OpenShift cluster version status indicates that an update is already in progress. See [Why does OpenShift show the cluster version is not up to date](/docs/openshift?topic=openshift-ts-cluster-version-downlevel) for details. |
| Upgrade requires resolution to OpenShift cluster version upgradeable conditions | A cluster master upgrade will now be canceled if the OpenShift cluster version `Upgradeable` status condition indicates that the cluster is not upgradeable. See [Why do I see a `Cannot complete cluster master upgrade` message?](/docs/openshift?topic=openshift-ts-cluster-master-upgrade) for details. |
| VPE gateways changes when creating or updating a VPC cluster to version 4.15 | There are important changes to the VPE gateways used for VPC clusters when creating a 4.15 cluster or updating to 4.15. These changes might require action. To review the changes and determine your required actions, see [VPE gateway creation information](#vpe-gateway-415). |
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

If the `Upgradeable` status is `False`, the condition information provides instructions that must be followed before upgrading. For more information, see [Providing the administrator acknowledgment](https://docs.redhat.com/en/documentation/openshift_container_platform/4.15/html/updating_clusters/preparing-to-update-a-cluster#update-preparing-ack_updating-cluster-prepare){: external}.

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


## VPE gateway creation information
{: #vpe-gateway-415}

When a VPC cluster is created at or updated to version 4.15, the following VPE gateways are created if they do not exist.

| VPE DNS Name(s) | Service | Versions |
| --- | --- | --- |
| `s3.direct.<region>.cloud-object-storage.appdomain.cloud` and `*.s3.direct.<region>.cloud-object-storage.appdomain.cloud` | Cloud Object Storage | Version 4.15 and later |
| `config.direct.cloud-object-storage.cloud.ibm.com` | Cloud Object Storage Configuration | Version 4.15 and later |
| `<region>.private.iaas.cloud.ibm.com` | VPC infrastructure | Version 4.15 and later |
| `icr.io` and `*.icr.io`* | Container Registry | Version 4.14 and later |
| `api.<region>.containers.cloud.ibm.com`* | {{site.data.keyword.openshiftlong_notm}} | Version 4.14 and later |
{: caption="Changes to VPE gateways in version 4.15" caption-side="bottom"}


* For clusters updated to 4.15, these VPE Gateways should already exist since they would have been created when the cluster was at 4.14.

These VPE Gateways are shared by all resources in the VPC, and when they are first created, they change the IP addresses associated with these services as well as restrict access to them.

If any resources in the VPC are using any of these services where the VPE Gateway does not yet exist, you must take the actions described below both before and possibly during the update to ensure the resources still have access.

The steps you take are different depending on if you are creating a new 4.15 cluster, or upgrading the master of an existing 4.14 cluster.
- New 4.15 clusters get the Secure by Default configurations described above.
- Upgraded existing 4.14 clusters continue to use the old security group model.

### VPE gateways created when upgrading to version 4.15
{: #vpe-gateway-415-upgrade}

Three new VPE Gateways for 4.15 are created if they don't already exist in the VPC. Also, one IP address per zone is added to each VPE gateway for each zone that has cluster workers in.
These IP addresses are taken from one of the existing VPC subnets in that zone.

The VPE gateways are put into the existing `kube-<vpcID>` security group, which by default allows all traffic. Unless you have modified this security group, you don't need to add any rules to allow inbound access to these new VPE Gateways.

If you have modified the `kube-<vpcID>` security group, you must make sure all resources in the VPC that use these services are allowed inbound access to this security group. Also, ensure there are no network ACLs on the subnets, security groups on the resources themselves, or custom VPC routes that block access to these new VPE gateways.

### New VPE gateway configuration when creating a new 4.15 cluster
{: #vpe-gateway-415-new}

Five new VPE gateways are created if they don't already exist in the VPC. Also, one IP addresses per zone is added to each VPE Gateway for each zone that has cluster workers in.
These IP addresses are taken from one of the existing VPC subnets in that zone.

The VPE gateways are put into a new `kube-vpegw-<vpcID>` security group, which only allows inbound traffic to these new VPE gateways from the cluster worker security group `kube-<clusterID>`.

Before you create your cluster, for any resources in your VPC that access any of these endpoints, ensure there are no network ACLs on the subnets, security groups on the resources themselves, or custom VPC routes that block access to these new VPE gateways.

As your cluster is being updated, watch for the creation of the `kube-vpegw-<vpcID>` security group. After it is created, add the necessary inbound rules to allow all your resources that are not cluster workers to access the new VPE gateways that are being created. Note that all cluster workers in the VPC can already access these VPE gateways via security group rules that are added automatically as the cluster is created.

For more information about a similar use case, see [VPC application troubleshooting](/docs/openshift?topic=openshift-ts-sbd-other-clusters).


## Common issues and troubleshooting 
{: #sbd-common-ts}

- [After enabling outbound traffic protection on my 4.15 cluster, my app no longer works](/docs/openshift?topic=openshift-ts-sbd-app-not-working).
- [When I try to create version 4.15 cluster, I see a quota error](/docs/openshift?topic=openshift-ts-sbd-cluster-create-quota).
- [When I update my cluster to secure by default, my nodeport app no longer works](/docs/openshift?topic=openshift-ts-sbd-nodeport-not-working).
- [Why do I see DNS failures after adding a custom DNS resolver?](/docs/openshift?topic=openshift-ts-sbd-custom-dns).
- [After creating a version 4.15 cluster, applications running in other clusters in my VPC are failing](/docs/openshift?topic=openshift-ts-sbd-other-clusters).
