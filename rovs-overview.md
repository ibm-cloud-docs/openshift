---

copyright:
  years: 2026, 2026
lastupdated: "2026-06-16"

keywords: openshift, virtualization service, rovs, virtual machines, vms, bare metal, pre-configured

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# OpenShift Virtualization Service overview
{: #rovs-overview}

[Virtual Private Cloud]{: tag-vpc}
[4.21 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

OpenShift Virtualization Service is a pre-configured offering that delivers a ready-to-use virtualization platform on {{site.data.keyword.openshiftlong_notm}}, enabling you to run virtual machines with minimal setup.
{: shortdesc}

This service is currently available as a beta release. Access is controlled by an allowlist. During the beta period, only console-based cluster creation is supported.
{: beta}

## What is OpenShift Virtualization Service?
{: #rovs-what-is}

OpenShift Virtualization Service provides a streamlined path to deploying virtualized infrastructure on IBM Cloud. Unlike manual OpenShift Virtualization deployments, Virtualization Service comes with essential components pre-configured and pre-installed, allowing you to start running virtual machines immediately after cluster creation.

## How does Virtualization Service compare to manual deployment?
{: #rovs-comparison}

Virtualization Service provides a streamlined, pre-configured virtualization platform compared to manual OpenShift Virtualization deployment:

| Feature | Virtualization Service | Manual Deployment |
|---------|----------------------|-------------------|
| **Setup time** | Minutes | Hours |
| **OpenShift Virtualization** | Pre-installed via add-on | Manual installation required |
| **Storage options** | ODF (local NVME) or VPC File Storage | Manual setup required |
| **Networking** | Automatic OVN with MTU 8900/9000 | Manual configuration |
| **Operators** | Auto-installed (Virtualization, NMState, Node Maintenance) | Install from OperatorHub |
| **Licensing** | OVE license (cost-effective) | Full OCP license |
| **Updates** | Managed add-on updates | Self-managed |
| **Best for** | Virtualization-focused workloads | Custom configurations |
| **Minimum version** | OpenShift 4.21 | OpenShift 4.17 |
{: caption="Comparison of Virtualization Service and manual deployment" caption-side="bottom"}

## What are the cluster requirements for Virtualization Service?
{: #rovs-requirements}

Virtualization Service clusters must meet the following requirements:

Infrastructure
:   VPC with bare metal worker nodes only.

OpenShift version
:   4.21 or later.

Operating system
:   Red Hat CoreOS (RHCOS) only.

Network
:   OVN-Kubernetes CNI with MTU 8900 (OVN) and 9000 (worker nodes).

Storage
:   OpenShift Data Foundation (ODF) with local NVME storage or VPC File Storage (one option must be selected during cluster creation).

Licensing
:   OpenShift Virtualization Engine (OVE) license.

These settings are automatically configured during cluster creation and cannot be changed after deployment.

## Which bare metal flavors are supported?
{: #rovs-flavors}

Virtualization Service supports specific VPC bare metal flavors optimized for virtualization workloads. For a complete list of supported flavors, see [Worker node flavors](/docs/openshift?topic=openshift-vpc-flavors).

To check bare metal flavor availability in the CLI:
```sh
ibmcloud ks flavors --zone <zone> --provider vpc-gen2 | grep metal
```
{: pre}

To verify that a specific flavor supports Virtualization Service, use the following command and check for the `openshift-vs` tag in the output:
```sh
ibmcloud ks flavor get --flavor <flavor> --zone <zone> --provider vpc-gen2
```
{: pre}

## Where is Virtualization Service available?
{: #rovs-regions}

Virtualization Service is available in the following regions:
- Dallas (us-south)
- Washington DC (us-east)
- Toronto (ca-tor)
- Montreal (ca-mon)
- Frankfurt (eu-de)

## What are the limitations of Virtualization Service?
{: #rovs-limitations-ov}

Virtualization Service has the following limitations:

- Supported only on VPC bare metal worker nodes
- Available only in specific regions (see [Where is Virtualization Service available?](#rovs-regions))
- Licensed for virtualization workloads only. Installing container-based workloads is not supported. For container workloads, use standard {{site.data.keyword.openshiftlong_notm}}.
- Windows VMs require appropriate licensing

For complete limitations, see [OpenShift Virtualization Service limitations](/docs/openshift?topic=openshift-rovs-limitations).

## How is Virtualization Service priced?
{: #rovs-pricing}

Virtualization Service uses OpenShift Virtualization Engine (OVE) licensing, which is more cost-effective than full OpenShift Container Platform (OCP) licensing for virtualization-focused workloads.

Pricing includes:

Infrastructure costs
:   Bare metal worker nodes with local NVME storage.

OVE license charges
:   Per instance-hour, for a worker node of up to 128 vCPUs. Larger worker nodes require multiple license instances.

Storage costs
:   NVME storage cost is included in the bare metal infrastructure cost.

For detailed pricing information, see the [{{site.data.keyword.cloud_notm}} Pricing Calculator](https://cloud.ibm.com/estimator){: external}.

## Next steps
{: #rovs-next-steps}

- [Getting started with OpenShift Virtualization Service](/docs/openshift?topic=openshift-rovs-getting-started)
- [Tutorial: Creating a Virtualization Service cluster](/docs/openshift?topic=openshift-rovs-cluster-create)
- [Managing Virtualization Service clusters](/docs/openshift?topic=openshift-rovs-manage)
