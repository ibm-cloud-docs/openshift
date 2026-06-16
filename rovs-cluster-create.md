---

copyright:
  years: 2026, 2026
lastupdated: "2026-06-16"

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







## Create or verify your VPC setup
{: #rovs-create-vpc}
{: step}

Before creating a Virtualization Service cluster, verify that your VPC infrastructure meets the following requirements. If you don't have the required resources, create them.

### VPC infrastructure requirements
{: #rovs-vpc-requirements}

Your VPC setup must include:

VPC
:   A VPC in one of the supported regions: Dallas (us-south), Washington DC (us-east), Toronto (ca-tor), Montreal (ca-mon), or Frankfurt (eu-de).

Subnets
:   At least one subnet in each zone where you want to deploy worker nodes.
    - For high availability, create subnets in at least 3 zones for a multizone cluster
    - Each subnet must have enough IP addresses (256 recommended)
    - Do not use the following reserved ranges: `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16`

Bare metal capacity
:   Bare metal worker node flavors must be available in your selected zones.
    - Look for flavors ending in `d`, which indicates local NVME storage required for OpenShift Data Foundation
    - Verify that flavors support Virtualization Service by checking for the `openshift-vs` tag

Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
{: important}

If you don't have the required VPC infrastructure, complete the following steps to create it.

### Creating VPC resources from the console
{: #rovs-vpc-console}
{: ui}

If you don't have the required VPC infrastructure, create it from the console.

1. [Create a VPC](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console) in the region where you want to create the cluster.

2. [Create subnets](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console#creating-a-subnet) in each zone where you want to deploy worker nodes.
   - Create subnets in at least 3 zones for high availability
   - [Create VPC subnets with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256

3. Verify bare metal capacity in your selected zones by checking the available flavors when you create your cluster in the next step.

### Creating VPC resources from the CLI
{: #rovs-vpc-cli}
{: cli}

If you don't have the required VPC infrastructure, create it from the CLI.

1. [Create a VPC](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#create-a-vpc-cli) in the region where you want to create the cluster.

2. [Create subnets](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#create-a-subnet-cli) in each zone where you want to deploy worker nodes.
   - Create subnets in at least 3 zones for high availability
   - [Create VPC subnets with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256

3. Verify that bare metal capacity is available in your selected zones.
   ```sh
   ibmcloud ks flavors --zone <zone> --provider vpc-gen2 | grep metal
   ```
   {: pre}

   Look for bare metal flavors ending in `d`, which indicates local NVME storage required for OpenShift Data Foundation. To verify that a specific flavor supports Virtualization Service, run `ibmcloud ks flavor get --flavor <flavor> --zone <zone> --provider vpc-gen2` and check for the `openshift-vs` tag in the output. For a complete list of supported flavors, see [Worker node flavors](/docs/openshift?topic=openshift-vpc-flavors).

## Create a Virtualization Service cluster
{: #rovs-create-cluster}
{: step}

You can create a Virtualization Service cluster by using the console.

### Creating a cluster from the console
{: #rovs-create-console}
{: ui}

1. In the {{site.data.keyword.cloud_notm}} console, navigate to **Infrastructure** > **OpenShift virtualization**.

2. Click **Create cluster**.

3. Review the pre-configured cluster settings:

   The following settings are automatically configured for OpenShift Virtualization Service clusters and cannot be changed:
   
   - **Orchestrator**: Red Hat OpenShift on IBM Cloud
   - **Infrastructure**: VPC
   - **Machine type**: Bare metal
   - **Operating system**: Red Hat CoreOS (RHCOS)
   - **Networking plugin**: Open Virtual Network (OVN-Kubernetes)

4. Select the **OpenShift version**:

   OpenShift Virtualization requires version 4.21 or later. The latest supported version is automatically selected.

5. Configure **Virtualization integrations**:

   Extend your cluster with key virtualization components. These integrations are connected once the cluster provisioning is complete.

   **OpenShift Virtualization operator**
   :   Required. Automatically configured with default settings. Creates and maintains OpenShift Virtualization Deployment.

   **Advanced Cluster Management (ACM)**
   :   Optional. Configure this cluster as the ACM hub cluster to control and monitor other Kubernetes clusters.
   
   - **Plan**: ACM for Virtualization
   - **Managed clusters**: Import later
   - **Disaster recovery**: For disaster recovery, install ODF on a separate managed cluster

   **OpenShift Data Foundation (ODF)**
   :   Recommended. Provides portable and scalable software-defined file, block, and object persistent storage for your container workloads. Configured with default settings.
   
   - **Version**: Latest available
   - **Plan**: Advanced
   - **Storage type**: Local Storage

   **File Storage for VPC**
   :   Alternative to ODF. Provides file storage backed by VPC infrastructure.

   You must select at least one storage option (ODF or File Storage for VPC) to provision a Virtualization Service cluster.
   {: important}

6. Select your **Virtual private cloud**:

   Choose an existing VPC or create a new one. If no VPCs are available, you'll need to create one before proceeding.

7. Configure the **Location**:

   Choose your worker zones and configure your subnets. Select the **Zones** where you want to deploy worker nodes (at least 3 zones for high availability). For each selected zone, you can edit the automatically selected **Subnet** as needed.

8. Configure the **Worker pool**:

   Set up a worker pool with the flavor and number of worker nodes that you want to run your first workload.

   **Flavor**
   :   Select a supported bare metal flavor with local NVME storage (e.g., `bx2d.metal.96x384`).
   
   Only bare metal flavors with the `openshift-vs` tag are available. These flavors include local NVME storage required for OpenShift Data Foundation.
   {: note}

   **Worker nodes per zone**
   :   Specify the number of worker nodes per zone (minimum 3 recommended for high availability).

   **Worker pool encryption**
   :   Optional. Manage the encryption of the worker nodes by enabling a key management service (KMS) provider at the worker pool level.
   
   - Select the root key by Instance
   - Choose a root key CRN for encryption

9. Configure **Networking**:

   **Network plugin**
   :   Open Virtual Network (OVN-Kubernetes) is automatically configured and cannot be changed.
   
   OVN-Kubernetes provides advanced, distributed virtual networking with native support for logical switches, routers, and security policies.
   {: note}

   **Network settings**
   :   Set up network communication to the master.
   
   - **Both private & public endpoints**: Communication to the master is accessible from the internet to your private and public network (default)
   - **Private endpoint only**: Communication is established securely to authorized cluster users in your private network, IBM Cloud services, or through a VPC VPN connection

   **Internal registry**
   :   Store images in the cluster internal registry with IBM Cloud Object Storage. A COS bucket will automatically be created for your cluster's internal registry.
   
   - Select an existing Cloud Object Storage instance or create a new one

10. Configure **Security** settings:

    **Outbound traffic protection**
    :   Optional. Protect network traffic by enabling only the connectivity necessary for the cluster to operate and preventing access to the public Internet.
    
    This setting is disabled by default for Virtualization Service clusters.
    {: note}

    **Cluster encryption**
    :   Optional. Enable a key management service (KMS) provider to encrypt the secrets in your cluster.
    
    - Select the root key by Instance
    - Choose a root key CRN for encryption

    **Ingress secrets management**
    :   Optional. Register an IBM Cloud Secrets Manager instance to the cluster for managing ingress subdomain certificates and secrets.
    
    Service authorization is required to allow OpenShift to communicate with Secrets Manager. Click **Authorize now** to create a policy scoped to all resources in this account, or go to IAM to create a policy with custom scoping.
    {: note}

    **VPC security groups**
    :   Optional. Provide up to four custom security groups to apply to all worker nodes on the VPC cluster instead of the default VPC security group. The default VPC security group will not be applied.
 
 11. Configure **Cluster details**:

    **Cluster name**
    :   Enter a unique name for your cluster (e.g., `my-vs-cluster`).

    **Resource group**
    :   Select the resource group where you want to create the cluster.

    **Tags**
    :   Optional. Add tags to organize and manage your cluster resources.

 12. Review the **Integrations** section:

    Get more from your cluster by connecting integrations. Verify that the OpenShift Virtualization operator and any selected add-ons (ACM, ODF, or File Storage) are listed.
 
 13. Review the **Summary** and estimated cost:

    The summary shows:
    - Number of worker nodes and their configuration
    - Operating system (RHCOS)
    - ROVE license fee
    - Total estimated monthly cost
    
    Additional charges for networking and bandwidth might apply. Estimate does not include usage-based charges.
    {: note}
 
 14. Click **Create** to provision your cluster.
 
 15. Monitor the cluster creation progress in the {{site.data.keyword.cloud_notm}} console. The cluster typically takes 30-45 minutes to provision.



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

1. In the OpenShift web console, navigate to **Ecosystem** > **Installed Operators**.

2. Verify that the **OpenShift Virtualization** operator shows a status of **Succeeded**. You might need to select **Show default projects** to see the **openshift-cnv** project.

3. In the left navigation of the OpenShift web console, click **Virtualization**.

4. Verify that the Virtualization pages load without prompts to install additional operators.

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
:   Bare metal capacity might not be available in your selected zone. Try a different zone or contact IBM Cloud support.

**Worker nodes fail to provision**
:   - Verify that your VPC and subnets are properly configured
    - Check that you have sufficient IP addresses in your subnets
    - Ensure your IAM permissions are correct

**Pre-configured components not installing**
:   - Check cluster logs: `ibmcloud ks cluster get --cluster <cluster-name> --show-resources`
    - Verify add-on status: `ibmcloud ks cluster addon ls --cluster <cluster-name>`
    - Review operator logs in the OpenShift console

For more troubleshooting guidance, see [Troubleshooting OpenShift Virtualization](/docs/openshift?topic=openshift-ts-virt-operator-install-fails).
