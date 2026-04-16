---

copyright:
  years: 2026, 2026

lastupdated: "2026-04-16"

keywords: openshift virtualization, odf install, openshift data foundation, local nvme, storagecluster

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the OpenShift Data Foundation installation fail for OpenShift Virtualization?
{: #ts-virt-odf-installation-fails}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

You try to set up OpenShift Data Foundation (ODF) for OpenShift Virtualization, but the installation does not complete successfully.
{: tsSymptoms}

ODF for virtualization on VPC bare metal workers requires local NVMe storage, enough worker nodes, and a healthy storage cluster deployment. Installation can fail if the worker nodes do not have suitable local disks or if the storage cluster does not become ready.
{: tsCauses}

To resolve the issue,
{: tsResolve}

 verify the worker node storage, confirm the node count, and review the storage cluster status.

1. Verify that your bare metal worker nodes have local NVMe storage.
   ```sh
   oc debug node/<node_name>
   chroot /host
   lsblk
   ```
   {: pre}

2. Ensure that your cluster has at least three worker nodes.
   ```sh
   oc get nodes
   ```
   {: pre}

3. Verify that the disks you plan to use are available.
   ```sh
   oc debug node/<node_name>
   chroot /host
   lsblk
   ```
   {: pre}

4. Review the ODF operator logs.
   ```sh
   oc logs -n openshift-storage -l app=ocs-operator
   ```
   {: pre}

5. Check the storage cluster status.
   ```sh
   oc get storagecluster -n openshift-storage
   oc describe storagecluster -n openshift-storage
   ```
   {: pre}

6. Review [Setting up storage for OpenShift Virtualization](/docs/openshift?topic=openshift-virt-storage-setup#virt-storage-odf) and [Deploying OpenShift Data Foundation on VPC clusters](/docs/openshift?topic=openshift-deploy-odf-vpc) to confirm that your cluster meets the supported ODF requirements.
