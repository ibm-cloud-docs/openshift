---

copyright:
  years: 2023, 2024
lastupdated: "2024-10-10"


keywords: openshift, version, update, upgrade, 4.14, update openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# 4.14 version information and update actions
{: #cs_versions_414}

Review information about version 4.14 of {{site.data.keyword.openshiftlong_notm}}. This version is based on Kubernetes version {{site.data.keyword.openshift_414_kube_version}}. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [Red Hat {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_versions) and the version [4.14 blog](https://www.redhat.com/blog/red-hat-openshift-4.14-is-now-available){: external}.
{: tip}

![This badge indicates Kubernetes version 1.27 certification for {{site.data.keyword.openshiftlong_notm}}](images/certified-kubernetes-color.svg){: caption="Kubernetes version 1.27 certification badge" caption-side="bottom"}

{{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.27 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._





## Release timeline 
{: #release_timeline_414}

The following table includes the expected release timeline for version 4.14. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Supported | 4.14 / {{site.data.keyword.openshift_414_kube_version}} | {{site.data.keyword.openshift_414_release_date}} | {{site.data.keyword.openshift_414_unsupported_date}}`†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}} version 4.14." caption-side="bottom"}

## Preparing to update
{: #prep-up-414}

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) to version 4.14. This information summarizes updates that are likely to have an impact on deployed apps when you update.
{: shortdesc}



### Update before master
{: #414_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

Cluster master access for VPC clusters with a private service endpoint changed significantly from version 4.13. Before updating a cluster of this type, review the following information and consider what changes you must make before upgrading your cluster. Also, consider this before creating a new  4.14 cluster with only a private service endpoint.
{: important}

| Type | Description |
| --- | --- |
| **Unsupported:** Deprecated and removed OpenShift features | For more information, review the [OpenShift version 4.14 deprecated and removed features](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-deprecated-removed-features){: external} and [Preparing to update to OpenShift Container Platform 4.14](https://docs.openshift.com/container-platform/4.14/updating/preparing_for_updates/updating-cluster-prepare.html){: external} for possible actions required. |
| Known OpenShift issues | For more information, review the [OpenShift version 4.14 known issues](https://docs.openshift.com/container-platform/4.14/release_notes/ocp-4-14-release-notes.html#ocp-4-14-known-issues){: external} for possible actions required. |
| Upgrade requires OpenShift cluster version currency | A cluster master upgrade will now be cancelled if the OpenShift cluster version status indicates that an update is already in progress.  See [Why does OpenShift show the cluster version is not up to date?](/docs/openshift?topic=openshift-ts-cluster-version-downlevel){: external} for details. |
| Upgrade requires resolution to OpenShift cluster version upgradeable conditions | A cluster master upgrade might be cancelled if the OpenShift cluster version `Upgradeable` status condition indicates that the cluster is not upgradeable. To determine if the cluster is upgradeable, see [Checking the `Upgradeable` status of your cluster](#status-check-414). If the cluster is not in an upgradeable status, the condition information provides instructions that must be followed before upgrading. For more information, see [Providing the administrator acknowledgment](https://docs.openshift.com/container-platform/4.14/updating/preparing_for_updates/updating-cluster-prepare.html#update-preparing-ack_updating-cluster-prepare){: external}. |
| Pod security admission label synchronization changes | Highly privileged namespaces `default`, `kube-public`, and `kube-system` are exempt from pod security admission enforcement. That is, pod security admission label synchronization will ensure that these namespaces enforce `privileged` pod security admission. You can disable pod security admission label synchronization for other namespaces by setting the value of the `security.openshift.io/scc.podSecurityLabelSync` namespace label to `false`. For more information, see [Understanding and managing pod security admission](https://docs.openshift.com/container-platform/4.14/authentication/understanding-and-managing-pod-security-admission.html){: external}. |
| OpenVPN replaced by Konnectivity |	 Konnectivity replaces OpenVPN as the Kubernetes API server network proxy used to secure OpenShift master to worker node communication. If your apps rely on OpenVPN to implement a secure OpenShift master to worker node communication, update your apps to support Konnectivity. |
| Networking changes to VPC clusters | In version 4.13 and earlier, VPC clusters pull images from the IBM Cloud Container Registry through a private cloud service endpoint for the Container Registry. For version 4.14 and later, this network path is updated so that images are pulled through a VPE gateway instead of a private service endpoint. For update actions, see [Networking changes for VPC clusters](#networking_414). |
| [VPC]{: tag-vpc} Cluster access changes for VPC clusters with a private service endpoint only that were introduced in version 4.13 have been reverted. | - **Previously** In VPC clusters with a private service endpoint only, if you wanted to access the cluster through the Openshift Console, run terraform scripts, create a `kubeconfig` file with `oc login` command, or make similar API calls that required oauth to get a token, then you accessed the private service endpoint, which was in the format `https://cX00.private.us-south.containers.cloud.ibm.com:port`. This setup only required access to the IBM Cloud private network `166.8.0.0/14`.  \n - **Changes introduced in version 4.13**: In 4.13, the default behavior for accessing the Red Hat OpenShift console, running `oc login` command, or making similar API calls, was changed to use the VPE gateway in the VPC.  \n - **Now in version 4.14**: The change to VPE has been reverted and the previous default behavior has been restored. The OpenShift console/OAuth now use the private service endpoint (`https://cX00.private.us-south.containers.cloud.ibm.com:port`) by default. You can now set the Oauth access type for your cluster to either the PSE or the VPE. If you want to keep the same behavior as from version 4.13, you can set the access type to use the VPE gateway. For more information, see [Setting the OAuth access type for VPC clusters](/docs/openshift?topic=openshift-setting-oauth-access-type). |
{: caption="Changes to make before you update the master to Red Hat OpenShift 4.14" caption-side="bottom"}

## Checking the `Upgradeable` status of your cluster
{: #status-check-414}

Run the following command to check the `Upgradeable` status of your cluster.

```sh
oc get clusterversion version -o json | jq '.status.conditions[] | select(.type == "Upgradeable")'
```
{: pre}

Example output where the `Upgradeable` status is `False`.

```sh
{
  "lastTransitionTime": "2023-10-04T15:55:54Z",
  "message": "Kubernetes 1.27 and therefore OpenShift 4.14 remove several APIs which require admin consideration. Please see the knowledge article https://access.redhat.com/articles/6958395 for details and instructions.",
  "reason": "AdminAckRequired",
  "status": "False",
  "type": "Upgradeable"
}
```
{: screen}

If the `Upgradeable` status is `False`, the condition information provides instructions that must be followed before upgrading. For more information, see [Providing the administrator acknowledgment](https://docs.openshift.com/container-platform/4.14/updating/preparing_for_updates/updating-cluster-prepare.html#update-preparing-ack_updating-cluster-prepare){: external}.




## Networking changes for VPC clusters
{: #networking_414}

In version 4.13 and earlier, VPC clusters pull images from the IBM Cloud Container Registry through a private cloud service endpoint for the Container Registry. For version 4.14 and later, this network path is updated so that images are pulled through a VPE gateway instead of a private service endpoint. This change affects all clusters in a VPC; when you create or update a single cluster in a VPC to version 4.14, all clusters in that VPC, regardless of their version, have their network path updated. Depending on the setup of your security groups, network ACLs, and network policies, you might need to make changes to ensure that your workers continue to successfully pull container images after updating to version 4.14. 
{: shortdesc}

The following image shows the new network path for version 4.14, which uses a VPE Gateway for Registry instead of the private service endpoint.

![VPE Gateway for Registry](images/registry-vpe-iks.svg){: caption="VPE Gateway for Registry in 4.14 and later clusters."}

With the network path updates, creating or updating a VPC cluster to run at version 4.14 adds a new VPE gateway to your VPC. This VPE gateway is specifically used for pulling images from the IBM Cloud Container Registry and is assigned one IP address for each zone in the VPC that has at least one cluster worker. DNS entries are added to the entire VPC that resolve all `icr.io` domain names to the new VPE gateway IP addresses. Depending on how you have configured your network security components, you might need to act to ensure that connections to the new VPE are allowed. 


### What do I need to do?
{: #networking_steps_oc}

The steps you need to take to ensure that your VPC cluster worker nodes continue pulling images from the Container Registry depend on your network security setup. 
{: shortdesc}

- If you use the default network rules for all security groups, network ACLs, and network policies, you do not need to take any action. 
- If you have a customized network security setup that blocks certain TCP connections within the VPC, you must take additional actions before updating to or creating a new cluster at version 4.14. Make the adjustments in the following sections to ensure that connections to the new VPE Gateway for Registry are allowed.

Regardless of whether you need to take additional steps, if you keep other clusters in the VPC that do not run version 4.14 you must [refresh the cluster master](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_apiserver_refresh) on those clusters. This refresh ensures that the correct updates are applied to the non-4.14 clusters so that traffic to the new VPE is allowed. 
{: important}


### I have custom security groups. What do I change?
{: #networking_steps_sg_oc}

The necessary allow rules are automatically added to the IBM-managed `kube-<cluster_ID>` cluster security group when you update to or create a cluster at version 4.14. However, if you created a VPC cluster that does **NOT** use the `kube-<cluster_ID>` cluster security group rules, you must make sure that the following security group rules are implemented to allow traffic to the VPE gateway for registry. If the rules are not already implemented in your custom setup, [add them](/docs/containers?topic=containers-vpc-security-group-manage&interface=cli#security_groups_cli). Each of these rules must be created for each zone in the VPC and must specify the entire VPC address prefix range for the zone as the destination CIDR. To find the VPC address prefix range for each zone in the VPC, run `ibmcloud is vpc-address-prefixes <vpc_name_or_id>`.

Add the following rules to your custom security group.

| Rule type | Protocol | Destination IP or CIDR | Destination Port |
|---|---|---|---|
| Outbound | TCP | Entire VPC address prefix range | 443 |
{: caption="Outbound security group rules to add for version 4.14" caption-side="bottom"}

To make these rules more restrictive, you can set the destination to the security group used by the VPE Gateway or you can specify the exact VPE Gateway reserved IP address. Note that these IP addresses can change if all cluster workers in a VPC are removed. 

### I have custom ACLs. What do I change?
{: #networking_steps_acl_oc}

If VPC networks ACLs that apply to your cluster workers have been customized to only allow certain egress and ingress traffic, make sure that the following ACL rules, or equivalent rules, are implemented to allow connections to and from the VPE Gateway for Registry. If the rules are not already implemented, [add them](/docs/containers?topic=containers-vpc-acls&interface=ui). Each of these rules must be created for each zone in the VPC and must specify the entire VPC address prefix range for the zone as the source (for outbound rules) or destination (for inbound rules) CIDR. To find the VPC address prefix range for each zone in the VPC, run `ibmcloud is vpc-address-prefixes <vpc_name_or_id>`. The priority for each rule should be higher than any rule that would otherwise deny this traffic, such as a rule that denies all traffic.

Add the following rules to your custom ACLs.

| Rule type | Protocol | Source IP or CIDR | Source Port | Destination IP or CIDR | Destination Port  |
|---|---|---|---|---|---|
| Outbound/Allow | TCP | Entire VPC address prefix range | Any | Entire VPC address prefix range | 443 |
| Inbound/Allow | TCP | Entire VPC address prefix range | 443 | Entire VPC address prefix range | Any |
{: caption="Outbound and inbound ACL rules to add for version 4.14" caption-side="bottom"}


### I have custom network policies. What do I change?
{: #networking_steps_policy_oc}

If you use Calico policies to restrict outbound connections from cluster workers, you must add the following policy rule to allow connections to the VPE Gateway for Registry. This policy must be created for each zone in the VPC and must specify the entire VPC address prefix range for the zone as the destination CIDR. To find the VPC address prefix range for each zone in the VPC, run `ibmcloud is vpc-address-prefixes <vpc_name_or_id>`.

```yaml
apiVersion: projectcalico.org/v3
kind: GlobalNetworkPolicy
metadata:
  name: allow-vpe-gateway-registry
spec:
  egress:
  - action: Allow
    destination:
      nets:
      - <entire-vpc-address-prefix-range> # example: 10.245.0.0/16
      ports:
      - 443
    protocol: TCP
    source: {}
  order: 500
  selector: ibm.role == 'worker_private'
  types:
  - Egress
```
{: codeblock}
