---

copyright:
  years: 2026, 2026
lastupdated: "2026-08-31"

keywords: openshift, classic, cluster, create, restriction, blocked, vpc

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Classic cluster creation restrictions
{: #classic-create-restriction}

[Classic infrastructure]{: tag-classic-inf}

Accounts that do not already have at least one classic cluster in a region can no longer create new classic clusters in that region. This restriction applies when you create a cluster from the console, the CLI, the API, or Terraform.
{: shortdesc}

## Who is affected by this restriction?
{: #classic-create-restriction-affected}

This restriction applies to your account if both of the following conditions are true:

- You are trying to create a classic cluster in a region.
- Your account does not already have an existing classic cluster in that same region.

Accounts that already have at least one classic cluster in a region are not affected and can continue to create classic clusters there.

## Why does this restriction exist?
{: #classic-create-restriction-why}

Classic infrastructure is a legacy compute platform. {{site.data.keyword.containerlong_notm}} is investing in VPC infrastructure as the strategic direction for new workloads. VPC clusters provide improved security, networking flexibility, and a better overall experience. To learn more, see [Overview of Classic and VPC infrastructure](/docs/openshift?topic=openshift-infrastructure_providers).

## What error do I see when classic cluster creation is blocked?
{: #classic-create-restriction-error}

If you try to create a classic cluster in a region where your account has no existing classic clusters, the request is rejected with the following error:

```
E501e: Classic cluster creation is not supported in regions that do not have existing classic clusters.
```
{: screen}

## What are my options if I'm affected?
{: #classic-create-restriction-next}

If your account is affected, consider the following options:

- **Create a VPC cluster.** VPC clusters are the recommended option for new workloads. To get started, see [Creating VPC clusters](/docs/openshift?topic=openshift-cluster-create-vpc-gen2).
- **Use a region where you already have a classic cluster.** If your account has a classic cluster in another region, you can create additional classic clusters in that region.
- **Request an exception.** If you have a specific use case that requires classic infrastructure in a new region and you cannot migrate to VPC, [open a support case](/unifiedsupport/cases/add) and provide your account ID, the target region, and the reason that VPC infrastructure does not meet your requirements.

## How do I check whether my account has existing classic clusters?
{: #classic-create-restriction-check}

To check which regions your account has classic clusters in, run the following command:

```sh
ibmcloud ks clusters --provider classic
```
{: pre}

The output lists all classic clusters and their regions. If the list is empty or does not include the target region, the restriction applies to you for that region.
