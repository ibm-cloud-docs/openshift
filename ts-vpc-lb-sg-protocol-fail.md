---

copyright:
  years: 2025, 2025
lastupdated: "2025-12-22"


keywords: loadbalancer, load, balancer, protocol, unmarshalling, discriminator, kubernetes, openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# VPC clusters: Security Group Protocol error creating or updating LoadBalancer
{: #vpc_ts_lb_security_group_error}
{: support}

**Infrastructure provider**: VPC

Creating or updating a `LoadBalancer` service in your VPC cluster fails with cluster events similar to: `error unmarshalling property 'security_groups' as []vpcv1.SecurityGroup: error unmarshalling property 'rules' as []vpcv1.SecurityGroupRuleIntf: unrecognized value for discriminator property 'protocol':`
{: tsSymptoms}

These events can be found using something like `kubectl get events -A | grep protocol` or by describing the Load Balancer directly using `kubectl describe svc -A`

These errors, as well as related problems with Ingress and Load Balancers, are caused by adding a security group to your VPC that uses one of the newly introduced protocol options, including the new "any" protocol.
{: tsCauses}

The immediate solution to this, until IBM can fix this issue, is to remove any security group rules you added that use the new protocol options, or to change the protocol of these rules to one of `tcp`, `udp`, `icmp`, or the combined `tcp-udp-icmp` protocol option.  More information can be found here: https://cloud.ibm.com/docs/vpc?topic=vpc-2025-12-09-migration-security-group-network-acl-rules
{: tsResolve}
