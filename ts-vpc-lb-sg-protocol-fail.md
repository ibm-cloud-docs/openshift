---

copyright:
  years: 2025, 2026
lastupdated: "2026-01-06"


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


These errors, as well as related problems with Ingress and Load Balancers, are caused by adding a security group to your VPC that uses one of the newly introduced protocol options, including the new **Any** protocol option.
{: tsCauses}

Until IBM provides a permanent fix, remove any security group rules that you added that use the new protocol options, or change the protocol of these rules to one of `tcp`, `udp`, `icmp`, or the combined `tcp-udp-icmp` protocol option. For more information, see [Updating to the 2025-12-09 version security group and network ACL rules](/docs/vpc?topic=vpc-2025-12-09-migration-security-group-network-acl-rules)
{: tsResolve}
