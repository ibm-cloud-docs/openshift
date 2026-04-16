---

copyright:
  years: 2026, 2026

lastupdated: "2026-04-16"

keywords: openshift virtualization, vm disks, pvc, storage profile, rwx, vpc file storage

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do VM disks fail to provision?
{: #ts-virt-vm-disks-fail-to-provision}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

You create or start a virtual machine, but the VM disks are not provisioned.
{: tsSymptoms}

OpenShift Virtualization requires storage that supports `ReadWriteMany` (RWX) access mode for VM disks and live migration. Provisioning can fail if no default storage class is set, if the selected storage class does not support RWX, or if the storage profile is not configured correctly.
{: tsCauses}

To resolve the issue,
{: tsResolve}

 review the default storage class, the storage class capabilities, and the storage profile configuration.

1. Verify that a default storage class is configured.
   ```sh
   oc get storageclass | grep "(default)"
   ```
   {: pre}

2. Check whether the storage class supports the required access mode.
   ```sh
   oc describe storageclass <storage_class_name>
   ```
   {: pre}

3. Review the storage profile configuration.
   ```sh
   oc get storageprofile
   oc describe storageprofile <storage_profile_name>
   ```
   {: pre}

4. For VPC File Storage, verify the configured claim property sets.
   ```sh
   oc get storageprofile <storage_profile_name> -o yaml | grep -A 5 claimPropertySets
   ```
   {: pre}

5. If the storage profile is not configured for RWX file system access, patch it.
   ```sh
   oc patch storageprofile <storage_profile_name> --type=merge -p '{
     "spec": {
       "claimPropertySets": [
         {
           "accessModes": ["ReadWriteMany"],
           "volumeMode": "Filesystem"
         }
       ]
     }
   }'
   ```
   {: pre}

6. Review [Setting up storage for OpenShift Virtualization](/docs/openshift?topic=openshift-virt-storage-setup) and make sure that your cluster has one properly configured storage solution before you retry the VM deployment.
