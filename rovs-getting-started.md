---

copyright:
  years: 2026, 2026
lastupdated: "2026-06-25"

keywords: openshift, virtualization service, rovs, quickstart, console, ui, virtual machines

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Quickstart: Creating a Virtualization Service cluster from the console
{: #rovs-getting-started}

[Virtual Private Cloud]{: tag-vpc}
[4.21 and later]{: tag-red}
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

2. Verify that your VPC infrastructure meets the requirements, or be prepared to create the necessary resources:
   - A VPC in your target region
   - Subnets in at least 3 zones for high availability (256 IP addresses recommended per subnet)
   - Bare metal capacity available in your selected zones (flavors ending in `d` for local NVME storage)

For detailed VPC setup instructions, see [Create or verify your VPC setup](/docs/openshift?topic=openshift-rovs-cluster-create#rovs-create-vpc).

## Create a Virtualization Service cluster
{: #rovs-gs-create}

1. Log in to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/).

2. Navigate to **Infrastructure** > **OpenShift Virtualization**.

3. Click **Create cluster**.

4. Review the pre-configured cluster settings (automatically configured, cannot be changed):
   - **Orchestrator**: Red Hat OpenShift on IBM Cloud
   - **Infrastructure**: VPC
   - **Machine type**: Bare metal
   - **Operating system**: Red Hat CoreOS (RHCOS)
   - **Networking plugin**: Open Virtual Network (OVN-Kubernetes)

5. Select the **OpenShift version** (4.21 or later is automatically selected).

6. Configure **Virtualization integrations**:

   **OpenShift Virtualization operator**
   :   Required. Automatically configured with default settings. Creates and maintains OpenShift Virtualization Deployment.

   **Advanced Cluster Management (ACM)**
   :   Optional. Configure this cluster as the ACM hub cluster to control and monitor other Kubernetes clusters.

   **OpenShift Data Foundation (ODF)**
   :   Recommended. Provides persistent storage for VMs. Configured with default settings.

   **File Storage for VPC**
   :   **Beta**: Alternative to ODF. Provides file storage backed by VPC infrastructure. File Storage for VPC support is available as a beta feature.

   You must select at least one storage option (ODF or File Storage for VPC).
   {: important}

7. Select your **Virtual private cloud** (or create a new one if needed).

8. Configure the **Location**. Choose your worker zones and configure your subnets. Select at least 3 zones for high availability. For each zone, you can edit the automatically selected subnet as needed.

9. Configure the **Worker pool**:
   - **Flavor**: Select a bare metal flavor with local NVME storage (e.g., `bx2d.metal.96x384`)
   - **Worker nodes per zone**: Specify at least 3 for high availability

10. Configure **Networking** (optional):
    - **Network settings**: Choose private & public endpoints (default) or private only
    - **Internal registry**: Select a Cloud Object Storage instance

11. Configure **Security** settings (optional):
    - **Cluster encryption**: Enable KMS for encrypting secrets
    - **Ingress secrets management**: Register Secrets Manager instance
    - **VPC security groups**: Apply custom security groups

12. Configure **Cluster details**:
    - **Cluster name**: Enter a unique name (e.g., `my-vs-cluster`)
    - **Resource group**: Select a resource group
    - **Tags**: Optional - add tags for organization

13. Review the **Integrations** section and verify that the OpenShift Virtualization operator and any selected add-ons are listed.

14. Review the estimated cost and click **Create**.

The cluster typically takes 30-45 minutes to provision. You can monitor the progress in the console.

## Access the OpenShift console
{: #rovs-gs-access}

1. In the {{site.data.keyword.cloud_notm}} console, navigate to **OpenShift** > **Clusters**.

2. Click your cluster name to view details.

3. Wait until the cluster **Status** shows **Normal** and **Master status** shows **Ready**.

4. Click **OpenShift web console** to access the cluster interface.

## Verify pre-configured components
{: #rovs-gs-verify}

1. In the OpenShift web console, navigate to **Ecosystem** > **Installed Operators**.

2. Verify that the **OpenShift Virtualization** operator shows a status of **Succeeded**.

3. Navigate to **Ecosystem** > **Installed Operators**.

4. Verify that the **OpenShift Data Foundation** operator has a status of **Succeeded**. This can take a few minutes to complete.

5. Navigate to **Storage** > **Data Foundation**.

6. Verify that the storage system shows **Resiliency** of **Healthy**.

7. Navigate to **Storage** > **StorageClasses**.

8. Verify that multiple OCS storage classes are available, including **ocs-storagecluster-ceph-rbd-virtualization**, which should be indicated as the default for VirtualMachines.

## Deploy your first virtual machine
{: #rovs-gs-first-vm}

1. In the OpenShift console, click **Virtualization** in the left navigation menu.

2. Click **VirtualMachines**.

3. Click **Create VirtualMachine**.

4. Select **From template** to use a pre-configured template.

5. Choose a template such as **Fedora** or **CentOS Stream**.

6. Configure the VM:
   - **Name**: Enter a name for your VM (e.g., `my-first-vm`)
   - **Storage class**: Select `ocs-storagecluster-ceph-rbd-virtualization`
   - **CPU**: Adjust as needed (default is usually sufficient)
   - **Memory**: Adjust as needed (default is usually sufficient)

7. Click **Create VirtualMachine**.

8. In the VM details page, click **Start** to start the VM.

9. Monitor the VM status until it shows **Running**.

10. Click the **Console** tab to access the VM console.

You now have a running virtual machine on your Virtualization Service cluster!

## Next steps
{: #rovs-gs-next-steps}

- [Managing Virtualization Service clusters](/docs/openshift?topic=openshift-rovs-manage)
- [Understanding limitations](/docs/openshift?topic=openshift-rovs-limitations)
- [Detailed cluster creation tutorial](/docs/openshift?topic=openshift-rovs-cluster-create)
- [Configure virtual machine networking](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/virtualization/virtual-machines#virt-networking){: external}
- [Set up VM snapshots and cloning](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/virtualization/virtual-machines#virt-managing-vms){: external}

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
