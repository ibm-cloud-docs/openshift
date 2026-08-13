---

copyright:
  years: 2026, 2026
lastupdated: "2026-08-13"


keywords: openshift, virtualization, virtual machines, learning path, vm administrator, rovs, migration, vmware

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Learning path for VM administrators
{: #learning-path-virt}

[Virtual Private Cloud]{: tag-vpc}
[4.21 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}

Follow this curated path to plan, deploy, and manage virtual machines on {{site.data.keyword.openshiftlong_notm}} using OpenShift Virtualization Service.
{: shortdesc}

## Understand the service
{: #virt-path-understand}

Start by learning what OpenShift Virtualization Service is and how it differs from a standard OpenShift cluster.

1. Read the [OpenShift Virtualization Service overview](/docs/openshift?topic=openshift-rovs-overview) to understand the pre-configured components, supported workloads, and deployment model.
2. Review [OpenShift Virtualization on IBM Cloud](/docs/openshift?topic=openshift-virt-overview) to understand the broader virtualization platform.
3. Check the [limitations](/docs/openshift?topic=openshift-rovs-limitations) before you start planning.

## Plan your environment
{: #virt-path-plan}

Design your virtualization environment before creating a cluster.

1. Review the [cluster planning guidance](/docs/openshift?topic=openshift-strategy) for sizing and availability decisions specific to your workload.
2. If you are migrating from VMware, review the [Migration Toolkit for Virtualization](https://docs.redhat.com/en/documentation/migration_toolkit_for_virtualization){: external} to understand the migration path.

## Create a cluster
{: #virt-path-create}

Create a pre-configured Virtualization Service cluster.

1. Use the [quickstart](/docs/openshift?topic=openshift-rovs-getting-started) to create a cluster from the console.
2. Or follow [Creating an OpenShift Virtualization Service cluster](/docs/openshift?topic=openshift-rovs-cluster-create) for CLI and full-configuration options.

## Manage and maintain
{: #virt-path-manage}

Keep your cluster and virtual machines healthy.

1. Learn how to manage cluster components and worker nodes in [Managing Virtualization Service clusters](/docs/openshift?topic=openshift-rovs-manage).
2. Manage the OpenShift Virtualization add-on in [Managing the OpenShift Virtualization add-on](/docs/openshift?topic=openshift-rovs-addon-virtualization).
3. Manage virtual network interfaces for VMs in [Managing virtual network interfaces](/docs/openshift?topic=openshift-vni-virtualization).

## Secure your cluster
{: #virt-path-secure}

Apply security controls appropriate for virtualized workloads.

1. Review the [Security and access](/docs/openshift?topic=openshift-vpc-security-group2) options for VPC clusters, including security groups and ACLs.
2. [Encrypt secrets](/docs/openshift?topic=openshift-encryption-secrets) and [worker node disks](/docs/openshift?topic=openshift-encryption-vpc-worker-disks).
3. Configure [IAM roles and access](/docs/openshift?topic=openshift-iam-platform-access-roles) for your team.

## Monitor and log
{: #virt-path-observe}

Set up observability for your VMs and cluster.

1. [Set up logging](/docs/openshift?topic=openshift-logging) for cluster and VM activity.
2. [Set up monitoring](/docs/openshift?topic=openshift-monitoring) for performance and health metrics.
3. Review [Tuning ODF performance for virtualization](/docs/openshift?topic=openshift-odf-virt-performance) if you are using OpenShift Data Foundation for VM storage.

## Troubleshoot
{: #virt-path-troubleshoot}

Use the troubleshooting guides when something goes wrong.

- [OpenShift Virtualization troubleshooting](/docs/openshift?topic=openshift-ts-virt-operator-install-fails) — start with the operator installation failures guide and navigate to the relevant topic.
