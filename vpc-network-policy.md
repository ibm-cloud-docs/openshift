---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-30"

keywords: openshift, firewall, acl, acls, access control list, rules, security group

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Overview of network security options
{: #vpc-network-policy}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) This information is specific to VPC clusters. For network policy information for classic clusters, see [Classic: Controlling traffic with network policies](/docs/containers?topic=containers-network_policies).
{: note}

Control traffic to and from your cluster and traffic between pods in your cluster by creating network rules and policies.
{: shortdesc}

Control traffic to and from your cluster with VPC access control lists (ACLs) and VPC security groups, and control traffic between pods in your cluster with Kubernetes network policies.
{: shortdesc}

## Comparison of network security options
{: #comparison}

The following table describes the basic characteristics of each network security option that you can use for your VPC cluster in {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

|Policy type|Application level|Default behavior|Use case|Limitations|
|-----------|-----------------|----------------|--------|-----------|
|[VPC security groups](/docs/containers?topic=containers-vpc-security-group) (Recommended)|Worker node|Version 4.5 and later: The default security groups for your cluster allow incoming traffic requests to the 30000 - 32767 port range on your worker nodes.</br>Version 4.4 and earlier: The default security group for your VPC denies all incoming traffic requests to your worker nodes.|Control inbound and outbound traffic to and from your worker nodes. Rules allow or deny traffic to or from an IP range with specified protocols and ports. |You can add rules to the default security group that is applied to your worker nodes. However, because your worker nodes exist in a service account and are not listed in the VPC infrastructure dashboard, you can't add more security groups and apply them to your worker nodes.|
|[VPC security groups](/docs/vpc?topic=vpc-alb-integration-with-security-groups)|Load balancer|If you don't specify a security group when you create a load balancer, then the default security group is used.|Allow inbound traffic from all sources to the listener port on a public load balancer.|None|
|[VPC access control lists (ACLs)](/docs/openshift?topic=openshift-vpc-acls) (Not recommended)|VPC subnet|The default ACL for the VPC, `allow-all-network-acl-<VPC_ID>`, allows all traffic to and from your subnets. Changing the default ACL is not recommended; instead, use security groups.|Control inbound and outbound traffic to and from the cluster subnet that you attach the ACL to. Rules allow or deny traffic to or from an IP range with specified protocols and ports.|can't be used to control traffic between the clusters that share the same VPC subnets. Instead, you can [create Calico policies](/docs/openshift?topic=openshift-network_policies#isolate_workers) to isolate your clusters on the private network.|
|[Kubernetes network policies](/docs/containers?topic=containers-vpc-kube-policies)|Worker node host endpoint|None|Control traffic within the cluster at the pod level by using pod and namespace labels. Protect pods from internal network traffic, such as isolating app microservices from each other within a namespace or across namespaces.|None|
{: caption="Network security options for VPC clusters"}

VPC Load Balancer also supports security groups. For more information, see [Integrating an IBM Cloud Application Load Balancer for VPC with security groups](/docs/vpc?topic=vpc-alb-integration-with-security-groups).
{: note}


## Access control lists (ACLs) or security groups?
{: #acl-sg-compare}

Although you can use either VPC ACLs or VPC security groups to control inbound traffic to and outbound traffic from your cluster, security groups are easier to implement. You can simplify your security setup by adding rules to only the default security group for your cluster, and leaving the default ACL for your VPC as-is.
{: shortdesc}

To simplify your VPC security setup, leave your default ACL for the VPC as-is or configure inbound and outbound rules either only at the security group level or only at the ACL level. If you configure rules in both ACLs for your subnets and in the default security group for your worker nodes, you might inadvertently block the subnets and ports that are required for necessary traffic to reach your cluster.
{: tip}

Review the following advantages of security groups over ACLs:
- As opposed to ACLs, security group rules are stateful. When you create a rule to allow traffic in one direction, reverse traffic in response to allowed traffic is automatically permitted without the need for another rule. Fewer rules are required to set up your security group than to set up an ACL.
- An ACL must be created for each subnet that your cluster is attached to, but only one security group must be modified for all worker nodes in your cluster.
- ACLs are applied at the level of the VPC subnet. If one cluster uses multiple subnets, rules are required to ensure that the subnets can communicate with each other. If you create multiple clusters that use the same subnets in one VPC, you can't use ACLs to control traffic between the clusters because they share the same subnets.
- With an ACL, you must explicitly allow traffic in both directions for a connection to succeed.

Regardless of which security option you choose, be sure to follow the instructions for [security groups](/docs/containers?topic=containers-vpc-security-group) or [ACLs](/docs/openshift?topic=openshift-vpc-acls) to allow the subnets and ports that are required for necessary traffic to reach your cluster.




