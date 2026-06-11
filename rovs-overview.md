---

copyright:
  years: 2026, 2026
lastupdated: "2026-06-11"

keywords: openshift, virtualization service, rovs, virtual machines, vms, bare metal, pre-configured

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Understanding OpenShift Virtualization Service
{: #rovs-overview}

[Virtual Private Cloud]{: tag-vpc}
[4.21 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

OpenShift Virtualization Service (also known as Red Hat OpenShift Virtualization Service or ROVS) is a pre-configured offering that delivers a ready-to-use virtualization platform on {{site.data.keyword.openshiftlong_notm}}, enabling you to run virtual machines with minimal setup.
{: shortdesc}

This service is currently available as a beta release. Access is controlled by an allowlist. During the beta period, only console-based cluster creation is supported.
{: beta}

## What is OpenShift Virtualization Service?
{: #rovs-what-is}

OpenShift Virtualization Service (ROVS) provides a streamlined path to deploying virtualized infrastructure on IBM Cloud. Unlike manual OpenShift Virtualization deployments, Virtualization Service comes with essential components pre-configured and pre-installed, allowing you to start running virtual machines immediately after cluster creation.

Key features include:

- **Automated deployment**: Cluster creation automatically installs and configures OpenShift Virtualization through the `openshift-virtualization` add-on
- **Pre-configured storage**: OpenShift Data Foundation (ODF) is automatically deployed and configured with local NVME storage during cluster creation. VPC Block Storage is not used.
- **Optimized networking**: Open Virtual Network (OVN) is pre-configured with MTU settings for optimal VM performance
- **Cost-effective licensing**: Uses OpenShift Virtualization Engine (OVE) licensing instead of full OpenShift Container Platform (OCP) licensing
- **Simplified management**: Managed add-ons ensure consistent configuration and updates
- **Operator management**: The add-on automatically installs and manages OpenShift Virtualization, NMState, and Node Maintenance operators

## Benefits
{: #rovs-benefits}

Faster time to value
:   Start running virtual machines within minutes of cluster creation, without manual configuration of storage, networking, or operators.

Reduced complexity
:   Eliminate multi-step setup processes and configuration decisions. The platform is optimized for virtualization workloads out of the box.

Cost optimization
:   OVE licensing provides a more cost-effective option for workloads focused primarily on virtualization rather than extensive container orchestration.

Consistent configuration
:   Pre-configured components ensure best practices are followed and reduce the risk of misconfiguration.

Managed updates
:   Core virtualization components are managed as add-ons, simplifying maintenance and updates.

## Virtualization Service vs. Manual Deployment
{: #rovs-comparison}

| Feature | Virtualization Service | Manual Deployment |
|---------|----------------------|-------------------|
| **Setup time** | Minutes | Hours |
| **OpenShift Virtualization** | Pre-installed via add-on | Manual installation required |
| **Storage (ODF)** | Pre-configured | Manual setup required |
| **Networking optimization** | Automatic OVN (MTU 8900/9000) | Manual configuration |
| **Licensing** | OVE license (cost-effective) | Full OCP license |
| **Add-on management** | Patches applied by IBM, version updates applied by user | Patches applied by IBM, version updates applied by user |
| **Operator installation** | Managed by add-on | Install from OperatorHub |
| **Best for** | Virtualization-focused workloads | Custom configurations |
| **Minimum version** | OpenShift 4.21 | OpenShift 4.17 |
{: caption="Comparison of Virtualization Service and manual deployment" caption-side="bottom"}

## Cluster characteristics
{: #rovs-characteristics}

Virtualization Service clusters are deployed with the following characteristics:

- **Infrastructure**: VPC with bare metal worker nodes
- **OpenShift version**: 4.21 or later
- **Operating system**: Red Hat CoreOS (RHCOS)
- **Network**: OVN-Kubernetes CNI with MTU 8900 (OVN) and 9000 (worker nodes)
- **Storage**: OpenShift Data Foundation (ODF) with local NVME storage (pre-configured, VPC Block Storage not used)
- **Licensing**: OpenShift Virtualization Engine (OVE) license

These settings are automatically configured during cluster creation and cannot be changed after deployment.

## Supported bare metal flavors
{: #rovs-flavors}

Virtualization Service supports specific VPC bare metal flavors optimized for virtualization workloads.

For a complete list of supported flavors, see [Worker node flavors](/docs/openshift?topic=openshift-vpc-flavors).

To check bare metal flavor availability in your zone:
```sh
ibmcloud ks flavors --zone <zone> --provider vpc-gen2 | grep metal
```
{: pre}

To verify that a specific flavor supports Virtualization Service, use `ibmcloud ks flavor get --flavor <flavor> --zone <zone> --provider vpc-gen2` and check for the `openshift-vs` tag in the output.

## Limitations
{: #rovs-limitations-ov}

- Virtualization Service is supported only on VPC bare metal worker nodes
- Virtualization Service is licensed for virtualization workloads only. Installing container-based workloads is not supported. For container workloads, use standard {{site.data.keyword.openshiftlong_notm}}.
- Windows VMs require appropriate licensing

For complete limitations, see [OpenShift Virtualization Service limitations](/docs/openshift?topic=openshift-rovs-limitations).

## Pricing
{: #rovs-pricing}

Virtualization Service uses OpenShift Virtualization Engine (OVE) licensing, which is more cost-effective than full OpenShift Container Platform (OCP) licensing for virtualization-focused workloads.

Pricing includes:
- Infrastructure costs (bare metal worker nodes with local NVME storage)
- OVE license charges (per instance-hour, for a worker node of up to 128 vCPUs; larger worker nodes require multiple license instances)
- Storage costs (NVME storage cost is included in the bare metal infrastructure cost)

For detailed pricing information, see the [IBM Cloud Pricing Calculator](https://cloud.ibm.com/estimator).

## Next steps
{: #rovs-next-steps}

- [Getting started with OpenShift Virtualization Service](/docs/openshift?topic=openshift-rovs-getting-started)
- [Tutorial: Creating a Virtualization Service cluster](/docs/openshift?topic=openshift-rovs-cluster-create)
- [Managing Virtualization Service clusters](/docs/openshift?topic=openshift-rovs-manage)
