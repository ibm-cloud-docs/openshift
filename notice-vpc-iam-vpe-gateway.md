---

copyright:
  years: 2026

lastupdated: "2026-09-10"

keywords: VPE gateway, IAM, virtual private endpoint, private.iam.cloud.ibm.com, notice, change, VPC

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# IAM VPE Gateway is being added to your VPC
{: #notice-vpc-iam-vpe-gateway}

[Virtual Private Cloud]{: tag-vpc}

Starting in November 2026, {{site.data.keyword.openshiftlong_notm}} automatically creates a Virtual Private Endpoint (VPE) Gateway for {{site.data.keyword.iamshort}} (IAM) in every VPC that contains a {{site.data.keyword.openshiftlong_notm}} cluster. This change might affect applications or network policies that connect to `private.iam.cloud.ibm.com`.
{: shortdesc}

Most environments are not affected. However, you might need to take action before November 2026 if you run workloads outside of a {{site.data.keyword.openshiftlong_notm}} cluster in the same VPC, use custom network ACLs, or have Kubernetes or Calico network policies that restrict egress to the IBM Cloud private service endpoint range (`166.8.0.0/14`).

IBM recommends that you proactively create the gateway yourself and monitor your environment for connectivity issues before the automatic rollout. A script is available to create or verify the gateway with no impact if it already exists.

For detailed information about who is affected, how to check your environment, and how to resolve any connectivity issues, see [Understanding the IAM VPE Gateway for VPC clusters](/docs/openshift?topic=openshift-vpc-iam-vpe-gateway).
