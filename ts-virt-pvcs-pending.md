---

copyright:
  years: 2026, 2026

lastupdated: "2026-04-16"

keywords: openshift virtualization, pvc pending, storage provisioner, odf, vpc file storage

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do persistent volume claims stay in `Pending` for OpenShift Virtualization?
{: #ts-virt-pvcs-pending}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

You create storage for a virtual machine, but the persistent volume claim (PVC) stays in `Pending`.
{: tsSymptoms}

The PVC might reference an unavailable storage class, or the required storage provisioner is not healthy. For OpenShift Virtualization, this issue commonly affects ODF and VPC File Storage configurations.
{: tsCauses}

To resolve the issue,
{: tsResolve}

 review the PVC events, confirm that the storage provisioner is running, and verify that the storage class is available.

1. Check the PVC status and events.
   ```sh
   oc describe pvc <pvc_name> -n <namespace>
   ```
   {: pre}

2. If you use ODF, verify that the storage pods are running.
   ```sh
   oc get pods -n openshift-storage
   ```
   {: pre}

3. If you use VPC File Storage, verify that the CSI driver pods are running.
   ```sh
   oc get pods -n kube-system | grep vpc-file
   ```
   {: pre}

4. If you use ODF, review the provisioner logs.
   ```sh
   oc logs -n openshift-storage -l app=csi-rbdplugin
   ```
   {: pre}

5. If you use VPC File Storage, review the provisioner logs.
   ```sh
   oc logs -n kube-system -l app=ibm-vpc-file-csi-controller
   ```
   {: pre}

6. Verify that the referenced storage class exists.
   ```sh
   oc get storageclass <storage_class_name>
   ```
   {: pre}

7. Review [Setting up storage for OpenShift Virtualization](/docs/openshift?topic=openshift-virt-storage-setup) to confirm that your storage configuration matches the requirements for your chosen backend.
