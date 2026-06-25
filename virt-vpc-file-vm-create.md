---

copyright:
  years: 2026
lastupdated: "2026-06-25"

keywords: openshift virtualization, vpc file storage, virtual machines, data volumes, storage profiles, virtctl

subcollection: openshift

content-type: how-to

---

{{site.data.keyword.attribute-definition-list}}

# Creating virtual machines with VPC File Storage
{: #virt-vpc-file-vm-create}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

Use {{site.data.keyword.filestorage_vpc_short}} to provision persistent storage for virtual machines that run on OpenShift Virtualization.
{: shortdesc}

This topic describes how to verify your environment, create a virtual machine that uses VPC File Storage, and validate that the virtual machine starts successfully.

## Before you begin
{: #virt-vpc-file-vm-create-prereqs}

Before you create a virtual machine with VPC File Storage, complete the following tasks:

1. Create a VPC cluster with bare metal worker nodes that uses Red Hat CoreOS (RHCOS). For more information, see [Creating VPC clusters](/docs/openshift?topic=openshift-cluster-create-vpc-gen2).
1. Review the planning guidance in [Planning your OpenShift Virtualization deployment](/docs/openshift?topic=openshift-virt-plan).
1. Configure VPC File Storage as described in [Setting up storage for OpenShift Virtualization](/docs/openshift?topic=openshift-virt-storage-setup).
1. Install the OpenShift Virtualization Operator as described in [Installing the OpenShift Virtualization Operator](/docs/openshift?topic=openshift-oc-virtualization).
1. Install the `virtctl` CLI. For more information, see [Getting started with OpenShift Virtualization CLI tools](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/virtualization/getting-started#virt-installing-virtctl_virt-getting-started){: external}.

## Verifying your environment
{: #virt-vpc-file-vm-create-verify}

Verify that your cluster is ready before you create a virtual machine.

1. Confirm that the OpenShift Virtualization components are deployed.
   ```sh
   oc get hyperconverged -n openshift-cnv
   oc get pods -n openshift-cnv
   ```
   {: pre}

   Look for the `PHASE` value `Deployed` in the HyperConverged output. In the pod output, verify that the virtualization pods show `Running` or `Completed` status and that they are not stuck in `Pending`, `CrashLoopBackOff`, or `Error`.

1. Confirm that the VPC File CSI driver add-on is installed.
   ```sh
   ibmcloud ks cluster addon ls -c <cluster-name> | grep vpc-file-csi-driver
   ```
   {: pre}

   Look for the `vpc-file-csi-driver` add-on in the output and verify that its health state is `normal` or that the status indicates that the add-on is ready.

1. Verify that a VPC File Storage class is available.
   ```sh
   oc get storageclass | grep vpc-file
   ```
   {: pre}

   Look for storage classes such as `ibmc-vpc-file-1000-iops` or `ibmc-vpc-file-6000-iops`. Note the storage class name that you want to use in the later steps.

1. Verify that the storage profile for your selected VPC File Storage class is configured with `ReadWriteMany` access mode and `Filesystem` volume mode.
   ```sh
   oc get storageprofile <storage-class-name> -o yaml
   ```
   {: pre}

   In the output, look for `claimPropertySets` under `spec`. Verify that `accessModes` includes `ReadWriteMany` and that `volumeMode` is set to `Filesystem`.
   ```yaml
   claimPropertySets:
   - accessModes:
     - ReadWriteMany
     volumeMode: Filesystem
   ```
   {: codeblock}

1. Verify that the selected storage class can provision a persistent volume claim.
   ```yaml
   cat <<EOF | oc apply -f -
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: vpc-file-test-pvc
   spec:
     accessModes:
     - ReadWriteMany
     resources:
       requests:
         storage: 10Gi
     storageClassName: <storage-class-name>
   EOF
   ```
   {: codeblock}

1. Confirm that the test persistent volume claim is bound.
   ```sh
   oc get pvc vpc-file-test-pvc
   ```
   {: pre}

   In the output, look for the `STATUS` column and verify that the persistent volume claim shows `Bound`. If the claim remains in `Pending`, the storage class or storage profile is not configured correctly.

1. Review the persistent volume claim details if the claim does not bind.
   ```sh
   oc describe pvc vpc-file-test-pvc
   ```
   {: pre}

1. Delete the test persistent volume claim.
   ```sh
   oc delete pvc vpc-file-test-pvc
   ```
   {: pre}

## Creating a virtual machine from the web console
{: #virt-vpc-file-vm-create-console}

Use the OpenShift web console to create a virtual machine that stores its disk on VPC File Storage.

1. Log in to the OpenShift web console for your cluster.
1. In the navigation menu, click **Virtualization** > **VirtualMachines**.
1. Click **Create** and select a template or select **From YAML** if you want to define the virtual machine manually.
1. Enter a name for the virtual machine.
1. Select the project where you want to create the virtual machine.
1. In the storage section, select a VPC File Storage class such as `ibmc-vpc-file-1000-iops` or `ibmc-vpc-file-6000-iops`.
1. Set the disk size based on your workload requirements.
1. Review the CPU and memory settings, then update them as needed.
1. Click **Create VirtualMachine**.
1. In the virtual machine details page, review the **Disks**, **Network interfaces**, and **Configuration** tabs to confirm that the virtual machine was created with the expected settings.

After the virtual machine is created, the console creates the associated persistent volume claim and data volume resources.


## Creating a virtual machine from the CLI
{: #virt-vpc-file-vm-create-cli}

Use the CLI if you want to create a virtual machine from a reusable manifest.

1. Create a namespace for your virtual machine workloads if you do not already have one.
   ```sh
   oc create namespace vm-project
   ```
   {: pre}

1. Create a virtual machine manifest that references a VPC File Storage class.
   ```yaml
   cat <<EOF | oc apply -f -
   apiVersion: kubevirt.io/v1
   kind: VirtualMachine
   metadata:
     name: rhel9-vm
     namespace: vm-project
   spec:
     running: false
     template:
       metadata:
         labels:
           kubevirt.io/domain: rhel9-vm
       spec:
         domain:
           cpu:
             cores: 2
           devices:
             disks:
             - disk:
                 bus: virtio
               name: rootdisk
             - disk:
                 bus: virtio
               name: cloudinitdisk
           resources:
             requests:
               memory: 4Gi
         volumes:
         - dataVolume:
             name: rhel9-vm-rootdisk
           name: rootdisk
         - cloudInitNoCloud:
             userData: |
               #cloud-config
               user: cloud-user
               password: changeme
               chpasswd: { expire: false }
           name: cloudinitdisk
     dataVolumeTemplates:
     - metadata:
         name: rhel9-vm-rootdisk
       spec:
         pvc:
           accessModes:
           - ReadWriteMany
           resources:
             requests:
               storage: 40Gi
           storageClassName: <storage-class-name>
           volumeMode: Filesystem
         source:
           blank: {}
   EOF
   ```
   {: codeblock}

1. Verify that the virtual machine and data volume resources were created.
   ```sh
   oc get vm -n vm-project
   oc get dv -n vm-project
   oc get pvc -n vm-project
   ```
   {: pre}

   In the output, verify that the virtual machine `rhel9-vm` is listed, that the data volume `rhel9-vm-rootdisk` exists, and that the persistent volume claim `rhel9-vm-rootdisk` is created. If the persistent volume claim is not yet `Bound`, wait for provisioning to complete before you continue.

1. Review the data volume details if the data volume is not ready.
   ```sh
   oc describe dv rhel9-vm-rootdisk -n vm-project
   oc describe pvc rhel9-vm-rootdisk -n vm-project
   ```
   {: pre}

1. Start the virtual machine.
   ```sh
   virtctl start rhel9-vm -n vm-project
   ```
   {: pre}

1. Verify that the virtual machine instance is running.
   ```sh
   oc get vmi -n vm-project
   ```
   {: pre}

   In the output, look for the virtual machine instance name and verify that its phase is `Running`. If no virtual machine instance is listed, review the virtual machine status.
   ```sh
   oc get vm rhel9-vm -n vm-project -o yaml
   ```
   {: pre}

## Validating the virtual machine
{: #virt-vpc-file-vm-create-validate}

After you create the virtual machine, validate that the storage and compute resources are working as expected.

1. Confirm that the persistent volume claim is bound.
   ```sh
   oc get pvc -n vm-project
   ```
   {: pre}

   In the output, look for the persistent volume claim `rhel9-vm-rootdisk` and verify that the `STATUS` column shows `Bound`.

1. Confirm that the data volume import or provisioning completed successfully.
   ```sh
   oc get dv -n vm-project
   ```
   {: pre}

   In the output, verify that the data volume shows a successful phase such as `Succeeded` or `Ready`, depending on your environment. If the data volume is not ready, review the data volume and persistent volume claim events.
   ```sh
   oc describe dv rhel9-vm-rootdisk -n vm-project
   oc describe pvc rhel9-vm-rootdisk -n vm-project
   ```
   {: pre}

1. Confirm that the virtual machine instance is running.
   ```sh
   oc get vmi -n vm-project
   ```
   {: pre}

1. Review the virtual machine instance details to confirm the node placement, interfaces, and attached volumes.
   ```sh
   oc describe vmi rhel9-vm -n vm-project
   ```
   {: pre}

1. If you configured cloud-init credentials, connect to the virtual machine console.
   ```sh
   virtctl console rhel9-vm -n vm-project
   ```
   {: pre}

1. Review the virtual machine details if the instance does not start.
   ```sh
   oc describe vm rhel9-vm -n vm-project
   oc describe vmi rhel9-vm -n vm-project
   ```
   {: pre}

## Understanding limitations and considerations
{: #virt-vpc-file-vm-create-limitations}

Review the following considerations when you use VPC File Storage for virtual machines:

VPC File Storage performance
:   VPC File Storage is a network-attached storage option. It is generally best suited for development, test, and lower-I/O workloads.

Snapshots and cloning
:   Snapshot and cloning support differs from OpenShift Data Foundation. Review your storage requirements before you standardize on VPC File Storage for production workloads.

Live migration
:   Live migration is supported when the storage profile is configured correctly and the workload meets the OpenShift Virtualization requirements.

Storage profile configuration
:   You must configure the storage profile for the VPC File CSI provisioner so that CDI can use the storage class correctly.

## Troubleshooting
{: #virt-vpc-file-vm-create-troubleshooting}

If the virtual machine does not start or the disk is not provisioned correctly, review the following topics:

- [Setting up storage for OpenShift Virtualization](/docs/openshift?topic=openshift-virt-storage-setup#virt-storage-troubleshoot)
- [Why do my VM disks fail to provision?](/docs/openshift?topic=openshift-ts-virt-vm-disks-fail-to-provision)
- [Why are my PVCs stuck in Pending?](/docs/openshift?topic=openshift-ts-virt-pvcs-pending)
- [Why does my VM fail to start?](/docs/openshift?topic=openshift-ts-virt-vm-fails-to-start)

## Next steps
{: #virt-vpc-file-vm-create-next}

After you create a virtual machine with VPC File Storage:

1. [Manage virtual machines in Virtualization Service clusters](/docs/openshift?topic=openshift-rovs-manage#rovs-manage-vms)
1. [Configure virtual network interfaces](/docs/openshift?topic=openshift-vni-virtualization)
1. [Review the Red Hat OpenShift Virtualization documentation](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/virtualization/index){: external}
