---

copyright:
  years: 2025, 2026
lastupdated: "2026-03-17"


keywords: loadbalancer, load, balancer, protocol, unmarshalling, discriminator, kubernetes, openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# VPC clusters: Security group protocol error creating or updating a LoadBalancer
{: #vpc_ts_lb_security_group_error}
{: support}

[Virtual Private Cloud]{: tag-vpc}

Creating or updating a `LoadBalancer` service in your VPC cluster fails with cluster event similar to the following.
{: tsSymptoms}


```txt
error unmarshalling property 'security_groups' as []vpcv1.SecurityGroup: error unmarshalling property 'rules' as []vpcv1.SecurityGroupRuleIntf: unrecognized value for discriminator property 'protocol':
```
{: screen}

You can review cluster events by running the following commands.
```sh
kubectl get events -A | grep protocol
```
{: pre}

```sh
kubectl describe svc -A
```
{: pre}


These errors, as well as related problems with Ingress and Load Balancers, are caused by both of the following conditions being true
{: tsCauses}

- The cluster master being at an old patch version prior to the January 2026 patch.
- A security group rule in your account that uses one of the newly introduced protocol options, including the new **Any** protocol option.


To solve this you need to do one of the following
{: tsResolve}

- Patch update your cluster master to at least the January 2026 patch
- Remove any security group rules in your account that use one of the newly introduced protocol options
- Change any rules that use the new protocols back to one of the older `tcp`, `udp`, `icmp`, or the combined `tcp-udp-icmp` protocol options

For more information, see [Updating to the 2025-12-09 version security group and network ACL rules](/docs/vpc?topic=vpc-2025-12-09-migration-security-group-network-acl-rules)
