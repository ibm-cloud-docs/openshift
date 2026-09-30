---

copyright: 
  years: 2014, 2026
lastupdated: "2026-09-30"


keywords: openshift, kubernetes, firewall, acl, acls, access control list, rules, security group

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Controlling traffic with ACLs
{: #vpc-acls}

[Virtual Private Cloud]{: tag-vpc}

With the introduction of Secure by Default networking for VPC clusters, IBM no longer recommends to change the default network ACLs. Network traffic should be managed using VPC security groups.  This information is provided for reference only.  If you do choose to use VPC ACLs you might need to customize what is provided, and are responsible for any problems in your environment caused by these ACLs.
{: important}


For more information about Secure by Default, see the following resources.
- [Understanding Secure by Default](/docs/openshift?topic=openshift-vpc-security-group-reference).
- [Managing outbound traffic protection in VPC clusters](/docs/openshift?topic=openshift-sbd-allow-outbound).

If your cluster was created at version 4.14 or earlier, it has not been switched to use Secure by Default unless you explicitly enabled Secure by Default.  To switch it to Secure by Default see [Enabling secure by default for existing clusters](/docs/openshift?topic=openshift-vpc-sbd-enable-existing).



## Overview of ACLs
{: #acls-overview}

If you create custom ACLs, only network traffic that is specified in the ACL rules is permitted to and from your VPC subnets. All other traffic that is not specified in the ACLs, such as cluster integrations with third-party services, is blocked entering or exiting the given subnet.
{: important}

Level of application
:   Virtual Private Cloud subnet

Default behavior
:   When you create a VPC, a default ACL is created in the format `allow-all-network-acl-<VPC_ID>` for the VPC. The ACL includes an inbound rule and an outbound rule that allow all traffic to and from your subnets. Any subnet that you create in the VPC is attached to this ACL by default. ACL rules are applied in a particular order. When you allow traffic in one direction by creating an inbound or outbound rule, you must also create a rule for responses in the opposite direction because responses are not automatically permitted.

Use case
:   If you want to specify which traffic is permitted to the worker nodes on your VPC subnets, you can create a custom ACL for each subnet in the VPC. For example, you can create the following set of ACL rules to block most inbound and outbound network traffic of a cluster, while allowing communication that is necessary for the cluster to function.

Required traffic for clusters
:   If you use custom ACLs, you must allow at minimum outbound traffic from all subnets to the following endpoints.
:   - [VPC service endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc)
:   - [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
:   - [VPC metadata service IPs](https://cloud.ibm.com/apidocs/vpc-metadata)
:   - All other subnets in the VPC

Limitations
:   If you create multiple clusters that use the same subnets in one VPC, you can't use ACLs to control traffic between the clusters because they share the same subnets.  Secure by Default security groups handle this isolation.
