---

copyright: 
  years: 2022, 2023
lastupdated: "2023-06-19"

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

1. Delete the resources.
    ```sh
    kubectl delete volumesnapshot VOLUMESNAPSHOT
    ```
    {: pre}

1. Remove the `finalizers` section from the `volumesnapshot` resource.
    ```sh
    kubectl patch volumesnapshot/VOLUMESNAPSHOT --type json --patch='[ { "op": "remove", "path": "/metadata/finalizers" } ]'
    ```
    {: pre}
    
1. Remove the `finalizers` section from the `volumesnapshotcontents` resource.
    ```sh
    kubectl patch volumesnapshotcontent/snapcontent-VOLUMESNAPSHOTCONTENT --type json --patch='[ { "op": "remove", "path": "/metadata/finalizers" } ]'
    ```
    {: pre}
    

1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.

