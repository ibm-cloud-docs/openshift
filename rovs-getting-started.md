---

copyright:
  years: 2026, 2026
lastupdated: "2026-06-01"

keywords: openshift, virtualization service, rovs, quickstart, console, ui, virtual machines

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Quickstart: Creating a Virtualization Service cluster from the console
{: #rovs-getting-started}

[Virtual Private Cloud]{: tag-vpc}
[4.20 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}

Get started quickly with OpenShift Virtualization Service by creating a pre-configured cluster using the {{site.data.keyword.cloud_notm}} console. This quickstart focuses on the fastest path to deploying virtual machines using only the console interface.
{: shortdesc}

This service is currently available as a beta release. Access is controlled by an allowlist. During the beta period, only console-based cluster creation is supported.
{: beta}

## Before you begin
{: #rovs-gs-prereqs}

1. Ensure you have the required permissions:
   - **Operator** role for {{site.data.keyword.containerlong_notm}}
   - **Editor** or **Administrator** role for VPC Infrastructure Services

2. Verify that you have or can create:
   - A VPC in your target region
   - Subnets in the zones where you want to deploy worker nodes
   - Bare metal capacity available in your selected zones

## Create a Virtualization Service cluster
{: #rovs-gs-create}

1. Log in to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/).

2. Navigate to **Infrastructure** > **OpenShift Virtualization Service**.

3. Click **Create cluster**.

4. Configure your cluster details:
   - **Cluster name**: Enter a unique name (e.g., `my-vs-cluster`)
   - **Resource group**: Select a resource group
   - **OpenShift version**: The latest supported version (4.20 or later) is automatically selected

5. Configure the location:
   - **Geography**: Select your region (e.g., `North America`)
   - **Availability**: Choose **Multizone** for high availability
   - **Worker zones**: Select at least 3 zones for production workloads

6. Configure the VPC:
   - **VPC**: Select an existing VPC or create a new one
   - **Subnets**: For each selected zone, choose the corresponding subnet

7. Configure worker nodes:
   - **Flavor**: Select a supported bare metal flavor (e.g., `bx2d.metal.96x384`)
   - **Worker nodes per zone**: Specify at least 3 for high availability

8. Review the pre-configured settings:
   - **Operating system**: Red Hat CoreOS (RHCOS)
   - **Container network interface**: OVN-Kubernetes
   - **OpenShift Virtualization**: Pre-installed
   - **OpenShift Data Foundation**: Pre-configured

9. Review the estimated cost.

10. Click **Create** to provision your cluster.

The cluster typically takes 30-45 minutes to provision. You can monitor the progress in the console.

## Access the OpenShift console
{: #rovs-gs-access}

1. In the {{site.data.keyword.cloud_notm}} console, navigate to **OpenShift** > **Clusters**.

2. Click your cluster name to view details.

3. Wait until the cluster **Status** shows **Normal** and **Master status** shows **Ready**.

4. Click **OpenShift web console** to access the cluster interface.

## Verify pre-configured components
{: #rovs-gs-verify}

1. In the OpenShift web console, navigate to **Operators** > **Installed Operators**.

2. Select the **openshift-cnv** project from the dropdown.

3. Verify that the **OpenShift Virtualization** operator shows a status of **Succeeded**.

4. Click the operator name and navigate to the **HyperConverged** tab.

5. Verify that the HyperConverged resource shows a **Phase** of **Deployed**.

6. Navigate to **Storage** > **Data Foundation**.

7. Verify that the storage system shows a status of **Ready**.

8. Navigate to **Storage** > **StorageClasses**.

9. Verify that multiple OCS storage classes are available, including:
   - `ocs-storagecluster-ceph-rbd`
   - `ocs-storagecluster-cephfs`

## Deploy your first virtual machine
{: #rovs-gs-first-vm}

1. In the OpenShift console, click **Virtualization** in the left navigation menu.

2. Click **VirtualMachines**.

3. Click **Create VirtualMachine**.

4. Select **From template** to use a pre-configured template.

5. Choose a template such as **Fedora** or **CentOS Stream**.

6. Configure the VM:
   - **Name**: Enter a name for your VM (e.g., `my-first-vm`)
   - **Storage class**: Select `ocs-storagecluster-ceph-rbd`
   - **CPU**: Adjust as needed (default is usually sufficient)
   - **Memory**: Adjust as needed (default is usually sufficient)

7. Click **Create VirtualMachine**.

8. In the VM details page, click **Start** to start the VM.

9. Monitor the VM status until it shows **Running**.

10. Click the **Console** tab to access the VM console.

You now have a running virtual machine on your Virtualization Service cluster!

## Next steps
{: #rovs-gs-next-steps}

- [Learn about managing Virtualization Service clusters](/docs/openshift?topic=openshift-rovs-manage)
- [Create a cluster with Advanced Cluster Management](/docs/openshift?topic=openshift-rovs-acm-tutorial)
- [Explore detailed cluster creation options](/docs/openshift?topic=openshift-rovs-cluster-create)
- [Configure virtual machine networking](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/virtualization/virtual-machines#virt-networking){: external}
- [Set up VM snapshots and cloning](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/virtualization/virtual-machines#virt-managing-vms){: external}

## Troubleshooting
{: #rovs-gs-troubleshoot}

**Cluster creation fails**
:   Verify that bare metal capacity is available in your selected zones. Try a different zone or contact IBM Cloud support.

**Cannot access OpenShift console**
:   Wait for the cluster master status to show **Ready**. This can take up to 45 minutes.

**Virtual machine fails to start**
:   - Verify that OpenShift Data Foundation is in **Ready** state
    - Check that you selected a valid storage class
    - Ensure sufficient resources are available in your cluster

For more troubleshooting guidance, see [Troubleshooting OpenShift Virtualization](/docs/openshift?topic=openshift-ts-virt-operator-install-fails).
