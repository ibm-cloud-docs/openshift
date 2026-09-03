---

copyright:
  years: 2026

lastupdated: "2026-09-03"

keywords: VPE gateway, IAM, virtual private endpoint, private.iam.cloud.ibm.com, DNS, VPC, gateway, security group, network ACL, Calico

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Understanding the IAM VPE Gateway for VPC clusters
{: #vpc-iam-vpe-gateway}

[Virtual Private Cloud]{: tag-vpc}

Starting in November 2026, {{site.data.keyword.openshiftlong_notm}} automatically creates a Virtual Private Endpoint (VPE) Gateway for {{site.data.keyword.iamshort}} (IAM) in every VPC that contains a {{site.data.keyword.openshiftlong_notm}} cluster. After this gateway is created, `private.iam.cloud.ibm.com` resolves to VPE Gateway IP addresses in your cluster worker subnets instead of the IBM Cloud private service endpoint range. Depending on how your environment is configured, this change might break applications that make IAM calls to `private.iam.cloud.ibm.com`.
{: shortdesc}

## Why is {{site.data.keyword.openshiftlong_notm}} adding an IAM VPE Gateway?
{: #vpc-iam-vpe-why}

VPE Gateways are already created for services that {{site.data.keyword.openshiftlong_notm}} clusters use, such as Container Registry and the Container APIs. Now that IAM supports VPE, a gateway for IAM is being added as well. VPE Gateways route service traffic over the private network using addresses in your VPC's existing subnets, and allow that traffic to be controlled by security groups and network ACLs.

## Who is affected by this change?
{: #vpc-iam-vpe-impact}

Most environments are not affected. You might be affected if any of the following situations apply:

- You run an application on a VSI or other machine in your VPC — outside of a {{site.data.keyword.openshiftlong_notm}} cluster — that makes IAM calls to `private.iam.cloud.ibm.com`. After the gateway is created, traffic from that machine is likely blocked by the default security group rules on the new VPE Gateway.
- You customized network ACLs on any VPC subnets and restrict traffic between subnets. The new VPE Gateway IPs are allocated from your cluster worker subnets, and your ACL rules might block traffic to them.
- You have Kubernetes or Calico network policies that allow egress traffic to the IBM Cloud private service endpoint range (`166.8.0.0/14`) but do not explicitly allow egress to your VPC subnets. Because the VPE Gateway IPs come from your VPC subnets rather than the `166.8.0.0/14` range, those policies block the traffic.

You are not affected if both of the following are true:

- No application outside your clusters connects to `private.iam.cloud.ibm.com`.
- Your network ACLs and Kubernetes and Calico network policies allow all non-public traffic.

## Check whether your environment is affected
{: #vpc-iam-vpe-check}

The safest way to find out whether this change affects you is to create the IAM VPE Gateway yourself using the script provided, and monitor your environment for connectivity problems before IBM creates the gateway automatically. IBM recommends that you run the script in your test environment first.

The script checks whether a VPE Gateway for IAM already exists in your VPC. If the gateway does not exist, the script creates one. If it already exists and is stable, the script exits without making changes.

## Before you begin
{: #vpc-iam-vpe-prereqs}

Make sure the following tools are installed and configured:

- [`ibmcloud` CLI](/docs/cli?topic=cli-getting-started)
- `ibmcloud is` (VPC Infrastructure) plugin: `ibmcloud plugin install vpc-infrastructure`
- `ibmcloud ks` (Kubernetes Service) plugin: `ibmcloud plugin install kubernetes-service`
- [`jq`](https://jqlang.org/download/){: external}

Log in and target the region that contains your VPC cluster.  Unset the resource group so the script can see the clusters in all your resource groups:

```sh
ibmcloud login
ibmcloud target -r <region>
ibmcloud target --unset-resource-group
```
{: pre}

Download the script and make it executable:

```sh
curl -LO https://raw.githubusercontent.com/IBM-Cloud/kube-samples/master/vpe-gateway/create-iam-vpe-gateway.sh
chmod +x create-iam-vpe-gateway.sh
```
{: pre}

## Create the IAM VPE Gateway
{: #vpc-iam-vpe-create}

Run the script to create the gateway. The script automatically discovers the VPC and subnets from your cluster worker nodes. You can also specify them explicitly.

```sh
# Auto-detect the VPC and subnets
./create-iam-vpe-gateway.sh add

# Specify the VPC and subnets explicitly
./create-iam-vpe-gateway.sh add --vpc <vpc-name-or-id> --subnets <subnet-zone1-id>,<subnet-zone2-id>,<subnet-zone3-id>
```
{: pre}

After the script runs, monitor your environment for connectivity issues. If no problems appear, you can leave the gateway in place. {{site.data.keyword.openshiftlong_notm}} recognizes the gateway and manages it automatically when the rollout runs in November 2026.

To remove the gateway and revert to the previous behavior, run the following command:

```sh
./create-iam-vpe-gateway.sh remove --vpc <vpc-name-or-id>
```
{: pre}

## Resolve connectivity issues
{: #vpc-iam-vpe-resolve}

If creating the IAM VPE Gateway breaks connectivity to `private.iam.cloud.ibm.com` in your environment, use the following sections to identify the cause and restore connectivity.

### Update security group rules
{: #vpc-iam-vpe-update-sg-rules}

This applies if the affected application runs on a VSI or system that is outside of a cluster.

The name of the security group that the script attaches to the IAM VPE Gateway depends on your cluster type:

- **Secure-by-default clusters**: `kube-vpegw-<vpcID>`
- **All other clusters**: `kube-<vpcID>`

The script prints the security group name in its output.

To restore connectivity, update the security groups on both the client system and the IAM VPE Gateway:

1. On the security group for the client system, add an outbound rule to allow all traffic to the IAM VPE Gateway security group.
2. On the IAM VPE Gateway security group, add an inbound rule to allow all traffic from the client system's security group.

Do not add rules that specify the IP addresses of the VPE Gateway directly. Those IPs can change if the VPC subnets used by your cluster workers change.
{: important}

### Update custom network ACL rules
{: #vpc-iam-vpe-update-acl-rules}

This applies if you use custom network ACLs on your VPC subnets. Custom network ACLs are [not recommended](/docs/openshift?topic=openshift-vpc-acls) for {{site.data.keyword.openshiftlong_notm}} clusters.

You might need to update ACLs in two places:

- The network ACLs for the subnet where the affected client system runs.
- The network ACLs for all VPC subnets used by workers in any clusters in the VPC, because the VPE Gateway IPs are allocated from those subnets.

Unlike security group rules, network ACLs require both an inbound and an outbound rule to allow a flow. See [About network ACLs](/docs/vpc?topic=vpc-using-acls) for more information.

Network ACL rules are complex to get right. The recommended diagnostic approach is:

1. Create the VPE Gateway for IAM using the script.
2. Add a temporary allow-all inbound and allow-all outbound rule at the top of each network ACL.
3. If that restores connectivity, the cause is the network ACLs. You can then determine the minimal set of rules needed and replace the temporary allow-all rules.

### Update Kubernetes and Calico network policies
{: #vpc-iam-vpe-update-network-policies}

This applies if you have Kubernetes or Calico network policies that allow egress traffic to the IBM Cloud private service endpoint range (`166.8.0.0/14`) but do not explicitly allow egress to your VPC subnets.

Because VPE Gateway IPs are allocated from your VPC worker subnets — not from the `166.8.0.0/14` range — those policies block traffic to the new gateway.

You cannot predict which specific IPs are assigned to VPE Gateways, and those IPs can change. For any network policy that restricts egress from pods or worker nodes, allow egress to all VPC subnets that contain cluster workers. Workers and pods with no egress restrictions do not need to be updated.

## Next steps
{: #vpc-iam-vpe-next}

- If connectivity issues persist after following the steps above, see [Resolving issues with VSI connections to VPE Gateways](/docs/openshift?topic=openshift-ts-sbd-vsi-vpe) for additional troubleshooting steps.
- To learn more about how {{site.data.keyword.openshiftlong_notm}} manages VPE Gateways in your VPC, see [Understanding secure by default cluster VPC networking](/docs/openshift?topic=openshift-vpc-security-group-reference).
