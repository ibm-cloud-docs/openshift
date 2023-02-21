---

copyright: 
  years: 2022, 2023
lastupdated: "2023-02-21"

keywords: openshift, storage, snapshot

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}





# Why can't I delete my {{site.data.keyword.block_storage_is_short}} volume snapshot resources?
{: #ts-storage-volumesnapshotdelete}
{: support}

**Infrastructure provider**:
VPC

When you try to remove your `volumesnapshot` and `volumesnapshotcontents` resources, the removal fails
{: tsSymptoms}

There are [finalizers](https://kubernetes.io/docs/concepts/overview/working-with-objects/finalizers/){: external} preventing the resources from being removed.
{: tsCauses}

Remove the finalizers and continue deleting the resources.
{: tsResolve}

1. Edit your `volumesnapshot` or `volumesnapshotcontents` and remove the `finalizers`. Note that the finalizers might be different for each resource.
    ```sh
    kubectl edit volumesnapshot VOLUMESNAPSHOT
    ```
    {: pre}
    
    ```sh
    kubectl edit volumesnapshotcontents VOLUMESNAPSHOTcontents
    ```
    {: pre}
    
1. Remove the `finalizers` section, then save and close the file.
    ```yaml
    finalizers:
           - snapshot.storage.kubernetes.io/volumesnapshot-bound-protection
    ```
    {: screen}
    
1. Try deleting the resources you want to remove again.

1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
