---

copyright: 
  years: 2025, 2025
lastupdated: "2025-12-04"


keywords: kubernetes, openshift, {{site.data.keyword.filestorage_vpc_short}}, snapshot, restore

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Why can't I restore my {{site.data.keyword.filestorage_vpc_short}} snapshot to a PVC?
{: #ts-storage-vpc-file-snapshot-delete}
{: support}

[Virtual Private Cloud]{: tag-vpc}

When you try to remove your volumesnapshot and volumesnapshotcontents objects, the removal fails, but your volume snapshot object shows a ReadyToUse status as false.
{: tsSymptoms}


There are finalizers preventing the resources from being removed.
{: tsCauses}


Remove the finalizers and continue deleting the resources. Note that stale volumesnapshot and volumesnapshotcontents objects can cause unnecessary CreateSnapshot requests, which can eventually lead to request spamming.
{: tsResolve}

* If the volumesnapshot and volumesnapshotcontent objects are included as a single mapping, follow these steps.

    1. Delete the volumesnapshot and volumesnapshotcontent objects.
        ```sh
        kubectl delete volumesnapshot snapshot-csi-file-1
        ```
        {: pre}

    1. Remove the finalizers section from the volumesnapshot resource.
        ```sh
        kubectl patch volumesnapshot/VOLUMESNAPSHOT --type json --patch='[ { "op": "remove", "path": "/metadata/finalizers" } ]'
        ```
        {: pre}

    1. Remove the finalizers section from the volumesnapshotcontents resource.
        ```sh
        kubectl patch volumesnapshotcontent/snapcontent-VOLUMESNAPSHOTCONTENT --type json --patch='[ { "op": "remove", "path": "/metadata/finalizers" } ]'
        ```
        {: pre}


* If the volumesnapshot object is deleted, but volumesnapshotcontent object still exists, complete the following steps:

    1. Find the volumesnapshotcontent object that does not have a `ReadyToUse` status as empty or false.
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

    1. If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.


