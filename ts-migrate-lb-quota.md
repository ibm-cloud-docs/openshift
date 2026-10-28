---

copyright:
  years: 2026, 2026
lastupdated: "2026-10-28"

keywords: openshift, classic, vpc, migrate, migration, global resource migration, ingress, ALB, load balancer quota

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my Classic-to-VPC migration stuck in global resource migration?
{: #ts-migrate-lb-quota}
{: troubleshoot}
{: support}

[Classic infrastructure]{: tag-classic-inf}

Your Classic-to-VPC cluster migration does not complete the global resource migration sub-operation.
{: shortdesc}

During global resource migration, the migration service also migrates Ingress controllers for {{site.data.keyword.openshiftlong_notm}} clusters. In the migration wizard (navigate to the navigation menu > **Migration** > **Get started** > **Clusters** > **Eligible clusters** and click **Open wizard** next to the source cluster), on the Phase 1 **Create** step (**Create VPC cluster** page), the migration job does not progress. In the **VPC cluster** card, the **Global resources migration** field remains stuck with statuses such as `Creating ingress subdomains`, `Enabling ingress ALBs`, or `Enabling ingress controllers`.
{: tsSymptoms}

The account reached its VPC load balancer quota in the target region where the VPC cluster is being provisioned. The migration cannot create the VPC load balancers that the Ingress components require.
{: tsCauses}

To resolve the issue, request a VPC load balancer quota increase for your account and region.
{: tsResolve}

1. Review the VPC load balancer quota for your account and region. For more information, see [Quotas and service limits](/docs/vpc?topic=vpc-quotas#alb-quotas){: external}.

2. Open a support case to request a VPC load balancer quota increase for the region.
   1. Go to the [{{site.data.keyword.cloud_notm}} Support Center](https://cloud.ibm.com/unifiedsupport/supportcenter){: external}.
   2. Click **Create a case**.
   3. Select **VPC Infrastructure** as the offering.
   4. In the case description, specify your account, the target region where the VPC cluster is provisioned, your current VPC load balancer quota, and the requested quota increase.

3. After the quota increase is applied, the stuck migration job resumes automatically. You can monitor the migration progress to verify that the global resource migration completes. For more information, see [Monitor global resource migration](/docs/openshift?topic=openshift-vpc-migrate-global-resources).
