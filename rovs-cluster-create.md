---

copyright:
  years: 2026, 2026
lastupdated: "2026-06-10"

keywords: openshift, virtualization service, rovs, create cluster, vpc, bare metal, tutorial

subcollection: openshift
content-type: tutorial
services: openshift
account-plan: paid
completion-time: 30m

---

{{site.data.keyword.attribute-definition-list}}

# Creating an OpenShift Virtualization Service cluster
{: #rovs-cluster-create}
{: toc-content-type="tutorial"}
{: toc-services="openshift"}
{: toc-completion-time="30m"}

[Virtual Private Cloud]{: tag-vpc}
[4.21 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

Create an OpenShift Virtualization Service cluster with pre-configured components for running virtual machines on {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

This service is currently available as a beta release. Access is controlled by an allowlist. During the beta period, only console-based cluster creation is supported.
{: beta}

## Objectives
{: #rovs-create-objectives}

In this tutorial, you will:

- Prepare your VPC infrastructure for a Virtualization Service cluster
- Create a Virtualization Service cluster using the console
- Verify that pre-configured components are properly installed
- Access the OpenShift Virtualization interface

## Before you begin
{: #rovs-create-prereqs}

### Required permissions
{: #rovs-create-permissions}

All users need the following permissions regardless of the interface used:
- **Operator** role for {{site.data.keyword.containerlong_notm}}
- **Editor** or **Administrator** role for VPC Infrastructure Services

### Required tools for console users
{: #rovs-create-tools-console}
{: ui}

- Access to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/)
- Optional: [OpenShift CLI (`oc`)](/docs/openshift?topic=openshift-cli-install) for verifying the cluster after creation

### Required tools for CLI users
{: #rovs-create-tools-cli}
{: cli}

- [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli)
- [{{site.data.keyword.containerlong_notm}} CLI plugin](/docs/openshift?topic=openshift-cli-install)
- [OpenShift CLI (`oc`)](/docs/openshift?topic=openshift-cli-install)







### Review supported flavors
{: #rovs-create-review-flavors}

Review [supported bare metal flavors](/docs/openshift?topic=openshift-rovs-overview#rovs-flavors) for Virtualization Service.

## Prepare your VPC infrastructure
{: #rovs-create-vpc}
{: step}

Before creating a Virtualization Service cluster, set up your VPC infrastructure.

### Create or identify a VPC
{: #rovs-create-vpc-setup}

1. Log in to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/).

2. Navigate to **VPC Infrastructure** > **VPCs**.

3. Either select an existing VPC or click **Create** to create a new one.

4. If creating a new VPC:
   - Enter a unique name
   - Select a resource group
   - Choose the region where you want to deploy your cluster
   - Configure address prefixes for your zones

### Create subnets
{: #rovs-create-subnets}

1. In your VPC, navigate to **Subnets**.

2. Create at least one subnet in each zone where you plan to deploy worker nodes:
   - Click **Create**
   - Enter a subnet name
   - Select the zone
   - Configure the IP range (ensure sufficient IP addresses for your worker nodes)
   - Click **Create subnet**

3. Repeat for each zone (minimum 3 zones recommended for high availability).

### Verify bare metal availability
{: #rovs-create-verify-capacity}

You can verify bare metal availability in the console during cluster creation, or use the CLI to check in advance.

Check that bare metal capacity is available in your selected zones:

```sh
ibmcloud ks flavors --zone <zone> --provider vpc-gen2 | grep metal
```
{: pre}

Look for flavors with the `openshift-vs` tag or flavors ending in `d` (indicating local NVME storage).

## Create a Virtualization Service cluster
{: #rovs-create-cluster}
{: step}

You can create a Virtualization Service cluster by using the console.

### Creating a cluster from the console
{: #rovs-create-console}
{: ui}

1. In the {{site.data.keyword.cloud_notm}} console, navigate to **Infrastructure** > **OpenShift Virtualization Service**.

2. Click **Create cluster**.

3. Configure the cluster details:

   **Cluster name**
   :   Enter a unique name for your cluster (e.g., `my-vs-cluster`).

   **Resource group**
   :   Select the resource group where you want to create the cluster.

   **OpenShift version**
   :   The latest supported version (4.21 or later) is automatically selected.

4. Configure the location:

   **Geography**
   :   Select the region (e.g., `North America`).

   **Availability**
   :   Choose **Multizone** for high availability or **Single zone** for development.

   **Worker zones**
   :   Select the zones where you want to deploy worker nodes (minimum 3 zones recommended).

5. Configure the VPC:

   **VPC**
   :   Select the VPC you prepared earlier.

   **Subnets**
   :   For each selected zone, choose the corresponding subnet.

6. Configure worker nodes:

   **Flavor**
   :   Select a supported bare metal flavor (e.g., `bx2d.metal.96x384`).
   
   Only flavors with local NVME storage and the `openshift-vs` tag are available.
   {: note}

   **Worker nodes per zone**
   :   Specify the number of worker nodes per zone (minimum 3 recommended for high availability).

7. Review the pre-configured settings:
   - **Operating system**: Red Hat CoreOS (RHCOS)
   - **Container network interface**: OVN-Kubernetes
   - **OpenShift Virtualization add-on**: Automatically enabled (cannot be disabled)
   - **OpenShift Data Foundation**: Pre-configured with local NVME storage
   - **VPC Block Storage**: Not deployed (ROVS uses ODF for storage)
   - **Outbound traffic protection**: Disabled

8. Review the estimated cost.

9. Click **Create** to provision your cluster.

10. Monitor the cluster creation progress. The cluster typically takes 30-45 minutes to provision.



## Verify the cluster and pre-configured components
{: #rovs-create-verify}
{: step}

After your cluster is created, verify that it's working correctly and that pre-configured components are installed. Use the console-based checks to confirm the cluster and operators are available in the UI.

### Access the cluster from the console
{: #rovs-create-verify-access-console}
{: ui}

1. In the {{site.data.keyword.cloud_notm}} console, navigate to **OpenShift** > **Clusters**.

2. Click your cluster name to view details.

3. Verify that the cluster **State** shows **Normal** and the master status shows **Ready**.

4. Click **OpenShift web console** to access the cluster interface.

5. Optional: To use the CLI, click **Actions** > **Connect via CLI** for instructions.

### Access the cluster from the CLI
{: #rovs-create-verify-access-cli}
{: cli}

1. Configure your CLI to use the cluster:

   ```sh
   ibmcloud ks cluster config --cluster <cluster-name> --admin
   ```
   {: pre}

2. Verify cluster access:

   ```sh
   oc get nodes
   ```
   {: pre}







### Verify OpenShift Virtualization from the console
{: #rovs-create-verify-virt-console}
{: ui}

1. In the OpenShift web console, navigate to **Operators** > **Installed Operators**.

2. Select the **openshift-cnv** project from the dropdown.

3. Verify that the **OpenShift Virtualization** operator shows a status of **Succeeded**.

4. In the left navigation of the OpenShift web console, click **Virtualization**.

5. Verify that the Virtualization pages load without prompts to install additional operators.

6. Click the operator name and navigate to the **HyperConverged** tab.

7. Verify that the HyperConverged resource shows a **Phase** of **Deployed**.

### Verify OpenShift Virtualization from the CLI
{: #rovs-create-verify-virt-cli}
{: cli}

1. Check the OpenShift Virtualization Operator:

   ```sh
   oc get csv -n openshift-cnv
   ```
   {: pre}

   Look for `kubevirt-hyperconverged-operator` with `PHASE: Succeeded`.

2. Verify the HyperConverged resource:

   ```sh
   oc get hyperconverged -n openshift-cnv
   ```
   {: pre}

   The `PHASE` should show `Deployed`.

3. Check virtualization pods:

   ```sh
   oc get pods -n openshift-cnv
   ```
   {: pre}

   All pods should be in `Running` or `Completed` state.









## Access the OpenShift Virtualization interface
{: #rovs-create-access-ui}
{: step}

### Access from the console
{: #rovs-create-access-ui-console}
{: ui}

1. In the {{site.data.keyword.cloud_notm}} console, navigate to **OpenShift** > **Clusters**.

2. Click your cluster name.

3. Click **OpenShift web console** to open the cluster interface.

4. In the left navigation, click **Virtualization** to access the virtual machine management interface.

5. Explore the available options:
   - **Overview**: Dashboard showing VM statistics
   - **VirtualMachines**: List and manage VMs
   - **Templates**: Pre-configured VM templates
   - **InstanceTypes**: VM sizing configurations
   - **Preferences**: VM preference settings

### Access from the CLI
{: #rovs-create-access-ui-cli}
{: cli}

1. Get the OpenShift console URL:
   ```sh
   ibmcloud ks cluster get --cluster $CLUSTER_NAME | grep "Public Service Endpoint URL"
   ```
   {: pre}

2. Log in to the OpenShift web console using your IBM Cloud credentials.

3. In the left navigation, click **Virtualization** to access the virtual machine management interface.

4. Explore the available options:
   - **Overview**: Dashboard showing VM statistics
   - **VirtualMachines**: List and manage VMs
   - **Templates**: Pre-configured VM templates
   - **InstanceTypes**: VM sizing configurations
   - **Preferences**: VM preference settings



## Next steps
{: #rovs-create-next-steps}

Now that your Virtualization Service cluster is ready:

- [Deploy your first virtual machine](/docs/openshift?topic=openshift-rovs-getting-started#rovs-gs-first-vm)
- [Learn about managing Virtualization Service clusters](/docs/openshift?topic=openshift-rovs-manage)
- [Explore VM templates and images](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/virtualization/virtual-machines#virt-creating-vms-from-rh-images-overview){: external}
- [Configure virtual machine networking](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/virtualization/virtual-machines#virt-networking){: external}

## Troubleshooting
{: #rovs-create-troubleshoot}

If you encounter issues during cluster creation:

**Cluster creation fails with capacity error**
:   Bare metal capacity may not be available in your selected zone. Try a different zone or contact IBM Cloud support.

**Worker nodes fail to provision**
:   - Verify that your VPC and subnets are properly configured
    - Check that you have sufficient IP addresses in your subnets
    - Ensure your IAM permissions are correct

**Pre-configured components not installing**
:   - Check cluster logs: `ibmcloud ks cluster get --cluster <cluster-name> --show-resources`
    - Verify add-on status: `ibmcloud ks cluster addon ls --cluster <cluster-name>`
    - Review operator logs in the OpenShift console

For more troubleshooting guidance, see [Troubleshooting OpenShift Virtualization](/docs/openshift?topic=openshift-ts-virt-operator-install-fails).
