---

copyright: 
  years: 2022, 2024
lastupdated: "2024-10-30"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, snapshot, storage

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}





# Why can't I delete my {{site.data.keyword.block_storage_is_short}} volume snapshot resources?
{: #ts-storage-volumesnapshotdelete}
{: support}

**Infrastructure provider**:
VPC

When you try to remove your `volumesnapshot` and `volumesnapshotcontents` objects, the removal fails, but your volume snapshot object shows a `ReadyToUse` status as `false`.
{: tsSymptoms}

There are [finalizers](https://kubernetes.io/docs/concepts/overview/working-with-objects/finalizers/){: external} preventing the resources from being removed.
{: tsCauses}

Remove the finalizers and continue deleting the resources. Note that stale `volumesnapshot` and `volumesnapshotcontents` objects can cause unnecessary `CreateSnapshot` requests, which can eventually lead to request spamming.
{: tsResolve}

If the `volumesnapshot` and `volumesnapshotcontent` objects are included as a single mapping, follow these steps.

1. Delete the `volumesnapshot` and `volumesnapshotcontent` objects.
    ```sh
    kubectl delete volumesnapshot snapshot-csi-block-3
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

If the `volumesnapshot` object is deleted, but `volumesnapshotcontent` object still exists, follow these steps to remove the `volumesnapshotcontent` object. 

1.  Find `volumesnapshotcontent` object that do not have a `ReadyToUse` status as empty or `false`.
    ```sh
    kubectl get volumesnapshotcontents | egrep -v 'true'
    ```
    {: pre}  

1. Delete the snapshot object.
    ```sh
    kubectl delete volumesnapshotcontent snapcontent-011b11d1-1101-4b11-b1b1-011abcde11db
    ```
    {: pre}

1. Remove the finalizer.
    ```sh
    kubectl patch volumesnapshotcontent/snapcontent-011b11d1-1101-4b11-b1b1-011abcde11db --type json --patch='[ { "op": "remove", "path": "/metadata/finalizers" } ]'
    ```
    {: pre}


If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
