---

copyright:
years: 2025, 2025
lastupdated: "2025-03-05"


keywords:  


subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Add-ons for {{site.data.keyword.openshiftlong_notm}}
{: #addons}

Review the managed add-ons available for {{site.data.keyword.containerlong_notm}}.
{: shortdesc}

|Add-on name | Description | Information and change log |
|---|---|---|
| Autoscaler | Automatically scale the worker pools in your cluster based on the sizing needs of your scheduled workloads. | - [Preparing classic and VPC clusters for autoscaling](/docs/containers?topic=containers-cluster-scaling-classic-vpc)  \n - [Cluster autoscaler add-on change log](/docs/containers?topic=containers-ca_changelog) |
| Back up and restore Helm chart | Create a one-time or scheduled backup for data that is stored in a file storage or block storage persistent volume claim (PVC). | - [Backing up and restoring PVC data for file and block storage](/docs/containers?topic=containers-utilities#ibmcloud-backup-restore)  \n - [Back up and restore Helm chart change log](/containers?topic=containers-backup_restore_changelog) |
| IBM Cloud Object Storage plug-in | Set up pre-defined storage classes for IBM Cloud Object Storage and use these storage classes to create a PVC to provision storage for your apps. | - [Installing the IBM Cloud Object Storage plug-in](/docs/containers?topic=containers-storage_cos_install)  \n - [IBM Cloud Object Storage plug-in change log](/docs/containers?topic=containers-cos_plugin_changelog) |
| IBM Storage Operator |  Manage several storage configmaps and resources in your cluster. This add-on is installed by default in VPC clusters that run version 4.15 or later. | - [Enabling the IBM Storage Operator](/docs/containers?topic=containers-storage-operator)  \n - [IBM Storage Operator add-on version change log](/docs/containers?topic=containers-cl-add-ons-ibm-storage-operator) |
| OpenShift AI add-on | Deploy the OpenShift AI operator to enable data acquisition and preparation, model training and fine-tuning, model serving and model monitoring, and hardware acceleration. | - [About the Red Hat OpenShift AI add-on](/docs/openshift?topic=openshift-ai-addon-about)  \n -[OpenShift AI add-on version change log](/docs/openshift?topic=openshift-cl-add-ons-openshift-ai) |
| OpenShift Data Foundation |  Manage persistent storage for your containerized apps with the highly available OpenShift Data Foundation storage solution. | - [Understanding OpenShift Data Foundation](/docs/openshift?topic=openshift-ocs-storage-prep)  \n - [OpenShift Data Foundation add-on version change log](/docs/openshift?topic=openshift-cl-add-ons-openshift-data-foundation)  |
| Static Route |  Create static routes that allow worker nodes to re-route response packets through a VPN or gateway to an IP address in an on-premises data center. | - [Adding static routes to worker nodes](/docs/containers?topic=containers-static-routes)  \n - [Static Route add-on version change log](/containers?topic=containers-cl-add-ons-static-route) |
| VPC Block CSI Driver | Copy a storage volume's contents at a particular point in time without creating an entirely new volume. | - [Setting up snapshots with the Block Storage for VPC cluster add-on](/docs/containers?topic=containers-vpc-volume-snapshot)  \n - [VPC Block CSI Driver add-on version change log](/docs/containers?topic=containers-cl-add-ons-vpc-block-csi-driver) | 
| VPC File CSI Driver | Create persistent volume claims for fast and flexible network-attached, NFS-based File Storage for VPC. | -[Enabling the IBM Cloud File Storage for VPC cluster add-on](/docs/containers?topic=containers-storage-file-vpc-install)  \n - [VPC File CSI Driver add-on version change log](/docs/containers?topic=containers-cl-add-ons-vpc-file-csi-driver) |
