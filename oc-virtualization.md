---

copyright:
  years: 2025, 2025
lastupdated: "2025-09-17"


keywords: openshift, virtualization, oc virt

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Installing the OpenShift Virtualization Operator on {{site.data.keyword.openshiftlong_notm}} clusters
{: #oc-virtualization}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Red Hat CoreOS only]{: tag-warm-gray}
[Baremetal worker nodes only]{: tag-warm-gray}


You can use the OpenShift Virtualization Operator to manage virtual machine workloads alongside your container workloads.
{: shortdesc}

The OpenShift Virtualization Operator adds Kubernetes custom resources to enable virtualization. You can use these resources for the following tasks.

- Create and manage Linux and Windows virtual machines (VMs).
- Run pod and VM workloads alongside each other in your cluster.
- Clone or import VMs.
- Manage network interface controllers and storage disks attached to your VMs.
- Migrate virtual machines between nodes.


Secondary networks and User defined networks aren't supported. For more information, see [Primary networks](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/multiple_networks/primary-networks){: external}.
{: note}

## Prerequisites
{: #virt-fs-prereq}

Before you begin, make sure that you have the following.

- A {{site.data.keyword.openshiftlong_notm}} cluster at version 4.17 or later
- VPC Baremetal workers
- RHCOS operating system
- Outbound traffic protection disabled
- OpenShift Data Foundation installed

To install ODF, see [Deploying OpenShift Data Foundation on VPC clusters](/docs/openshift?topic=openshift-deploy-odf-vpc&interface=ui).
{: tip}

## Setting up virtualization with {{site.data.keyword.filestorage_vpc_short}}
{: #virt-fs-example}


1. In the `kube-system/addon-vpc-block-csi-driver-configmap` configmap, set the `IsStorageClassDefault` property to `false`.
    ```sh
    oc edit cm -n kube-system addon-vpc-block-csi-driver-configmap
    ```
    {: pre}


1. Install the {{site.data.keyword.filestorage_vpc_short}} add-on from IBM cloud console.

1. Verify the add-on is installed by listing the storage classes.
    ```sh
    oc get storageclass
    ```
    {: pre}


1. Choose a storage class, for example `ibmc-vpc-file-metro-1000-iops` and set it as the default by editing the `kube-system/addon-vpc-file-csi-driver-configmap` and entering it as the `SET_DEFAULT_STORAGE_CLASS` field.
    ```sh
    oc edit cm -n kube-system addon-vpc-file-csi-driver-configmap
    ```
    {: pre}


1. Wait a few minutes for the changes to take effect.

1. [Subscribe to the OpenShift Virtualization catalog by using the CLI](https://docs.openshift.com/container-platform/4.17/virt/install/installing-virt.html#virt-subscribing-cli_installing-virt){: external}.

1. Follow the steps to [Deploy the OpenShift Virtualization Operator by using the CLI](https://docs.openshift.com/container-platform/4.17/virt/install/installing-virt.html#installing-virt-operator-cli_installing-virt){: external}.

1. Wait until `StorageProfile` resources are created for each StorageClass. As CDI does not automatically recognize VPC File storage properties, you need to properly set it up.

1. Edit the `StorageProfile` for the default storage class (`ibmc-vpc-file-metro-1000-iops`) and add the following specs.
    ```yaml
    spec:
      claimPropertySets:
      - accessModes:
        - ReadWriteMany
        volumeMode:
          Filesystem
    ```
    {: codeblock}

1. Check if the resource status is updated with a `claimPropertySets` that represents the new specs.
    ```sh
    oc get storageprofile ibmc-vpc-file-metro-1000-iops -o yaml
    ```
    {: pre}

1. In the OpenShift console, look for a new main menu item called **Virtualization**. You can now use the console to create template VMs from the console.

## Next steps
{: #virt-next-steps}

Review the following Red Hat docs for creating and managing VMs in your cluster.

- [Creating virtual machines from Red Hat images overview](https://docs.openshift.com/container-platform/4.17/virt/virtual_machines/creating_vms_rh/virt-creating-vms-from-rh-images-overview.html){: external}.
- [Creating virtual machines from the command line](https://docs.redhat.com/en/documentation/openshift_container_platform/4.17/html/virtualization/virtual-machines#virt-creating-vms-from-cli){: external}.
- [Connecting to virtual machine consoles](https://docs.openshift.com/container-platform/4.17/virt/virtual_machines/virt-accessing-vm-consoles.html){: external}.
