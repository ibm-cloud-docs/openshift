---

copyright:
  years: 2026, 2026
lastupdated: "2026-06-10"

keywords: openshift, virtualization service, rovs, limitations, restrictions, constraints

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# OpenShift Virtualization Service limitations
{: #rovs-limitations}

[Virtual Private Cloud]{: tag-vpc}
[4.21 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

Review the limitations and restrictions for OpenShift Virtualization Service clusters on {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

This service is currently available as a beta release. Access is controlled by an allowlist. During the beta period, only console-based cluster creation is supported.
{: beta}

## Infrastructure requirements
{: #rovs-limit-infra}

- VPC infrastructure with bare metal worker nodes only (no Classic or VSI support)
- Bare metal flavors with `openshift-vs` tag (with NVME storage if ODF is required)
- OpenShift 4.21 or later
- Red Hat CoreOS (RHCOS) only
- OVN-Kubernetes CNI only (automatically configured, cannot use Calico)
- MTU settings are pre-configured (OVN: 8900, Worker nodes: 9000) and must not be changed

## Configuration restrictions
{: #rovs-limit-config}

The following components and settings are pre-configured and cannot be disabled or modified:

Add-ons
:   - The `openshift-virtualization` add-on is automatically enabled and cannot be disabled
    - Optional add-ons are chosen from a limited selection suitable for virtualization

Operators
:   - OpenShift Virtualization Operator (installed and managed by the add-on)
    - NMState Operator (installed and managed by the add-on)
    - Node Maintenance Operator (installed and managed by the add-on)
    - Installation of these operators from Red Hat OperatorHub is blocked

Storage
:   - OpenShift Data Foundation (ODF) is pre-configured using bare metal flavors with local NVME storage
    - VPC Block Storage is not deployed or used in ROVS clusters
    - All storage is provided through ODF with local disks

Networking
:   - MTU settings are fixed (OVN: 8900, Worker nodes: 9000)
    - Outbound traffic protection is disabled and cannot be enabled

Installation of OpenShift Virtualization, NMState, and Node Maintenance operators from Red Hat OperatorHub is blocked on ROVS clusters. These operators are managed exclusively by the `openshift-virtualization` add-on.
{: important}

## Storage and networking
{: #rovs-limit-storage-network}

Storage
:   - ODF uses local NVME storage; node failures may cause data unavailability
    - VM snapshots supported but limited by storage capacity

Networking
:   - VM live migration supported within same zone only (cross-zone requires shutdown)
    - Kubernetes network policies supported with some limitations

## Virtual machines
{: #rovs-limit-vms}

- You must provide and manage the licenses for the operating systems and software you install in your VMs, including Windows
- GPU passthrough and vGPU may have limited support
- Nested virtualization not supported
- Migration between different bare metal flavors may have limitations

## Licensing and scaling
{: #rovs-limit-licensing-scaling}

Licensing
:   OVE licensing only (per instance-hour, for a worker node of up to 128 vCPUs; larger worker nodes require multiple license instances). BYOL and Cloud Pak entitlements are not supported. The `entitlement` parameter cannot be specified when creating ROVS clusters or worker pools.

Scaling
:   - All worker pools must use supported bare metal flavors
    - Minimum 3 worker nodes recommended for production

Availability
:   Bare metal capacity may not be available in all zones. Check before creating:
    ```sh
    ibmcloud ks flavors --zone <zone> --provider vpc-gen2 | grep metal
    ```
    {: pre}

## Operations
{: #rovs-limit-ops}

- Worker node maintenance may require VM migration or downtime
- Backup and restore limited to ODF and OpenShift Virtualization features

## When to use standard OpenShift
{: #rovs-limit-alternatives}

Use a standard OpenShift cluster if you need VSI worker nodes, custom storage, full OCP licensing, RHEL support, Calico CNI, or greater add-on flexibility.

## Next steps
{: #rovs-limit-next-steps}

- [Manage Virtualization Service clusters](/docs/openshift?topic=openshift-rovs-manage)
- [Troubleshooting guidance](/docs/openshift?topic=openshift-ts-virt-operator-install-fails)
- [OpenShift Virtualization documentation](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/virtualization){: external}
- [Get support](/docs/get-support)
