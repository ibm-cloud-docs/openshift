---

copyright: 
  years: 2025, 2026
lastupdated: "2026-01-27"


keywords: kubernetes, openshift, {{site.data.keyword.filestorage_vpc_short}}, snapshot, restore

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Why can't I restore my {{site.data.keyword.filestorage_vpc_short}} snapshot to a PVC?
{: #ts-storage-vpc-file-snapshot-restore}
{: support}

[Virtual Private Cloud]{: tag-vpc}


You are unable to restore your {{site.data.keyword.filestorage_vpc_short}} snapshot to a PVC.
{: tsSymptoms}

You see provisioning failed errors similar to the following when trying to restore your snapshot.

```sh
Warning ProvisioningFailed  19s        vpc.file.csi.ibm.io_ibm-vpc-file-csi-controller-777bd678bb-zrqsj_7a76f47e-5dba-4a50-8398-2027ff48047c failed to provision volume with StorageClass "ibmc-vpc-file-regional": rpc error: code = InvalidArgument desc = {RequestID: d406e3d3-7d3e-4b1d-abb8-d8d43f2ba901 , BackendError: {Trace Code:, Code:shares_snapshot_not_found, Description:The Share Snapshot ID 'r134-eb2d244b-45f0-4ce6-95f1-a629f4e4717c' for share '' that you are trying to find is either deleted or never existed, RC:404 Not Found.Failed to create file share with the storage provider}, Action: Please provide valid parameters}
```
{: screen}

You might see this error if you have deleted the original PVC that was used to create the snapshot. This results in the removal of all of its respective snapshots. Another possilbe reason is that you manually deleted the snapshot from your VPC resources.
{: tsCauses}


1. Delete the Kubernetes objects like the PVC, volume snapshot and volume snapshot content

	```sh
	kubectl delete pvc PVC
    ```
    {: pre}

1. Delete the volumesnapshot which should automatically delete volumesnapshotcontent.
    ```sh
    kubectl delete volumesnapshot SNAPSHOT
    ```
    {: pre}

**Optional**: If you encounter any other errors while cleaning up your resources, complete the following steps to gather the required log files before contacting support.

1. Describe your pvc and review the status.
    ```sh
    kubectl describe pvc PVC
    ```
    {: pre}

1. Describe your volumesnapshot and review the status.
    ```sh
    kubectl describe volumesnapshot VOLUMESNAPSHOT
    ```
    {: pre}

1. Describe your volumesnapshotcontent and grep the snapshot CRN. Copy string after share-snaphot.
    ```sh
    kubectl describe vsc VOLUMESNAPSHOTCONTENT | grep share-snapshot
    ```
    {: pre}

    Example output
    ```sh
    Snapshot Handle:  crn:v1:staging:public:is:us-south-3:a/77f2bceddaeb577dcaddb4073fe82c1c::share-snapshot:r134-c37715c8-1f32-431d-9a10-72f94cf86f6b/r134-252ad340-5f29-4b27-96bf-1747e0e38eea
    ```
    {: pre}

1. Get the backend snapshot details and review the status.

    ```sh
    ibmcloud is share-snapshot SHARE SNAPSHOT
    ```
    {: pre}

    Example
    ```sh
    ibmcloud is share-snapshot r134-c37715c8-1f32-431d-9a10-72f94cf86f6b r134-252ad340-5f29-4b27-96bf-1747e0e38eea
    ```
    {: pre}

1. Get the logs of the ibm-vpc-file-csi-controller-xxx driver and sidecar.

    ```sh
    kubectl logs -n kube-system ibm-vpc-file-csi-controller-xxx -c csi-snapshotter
    kubectl logs -n kube-system ibm-vpc-file-csi-controller-xx -c iks-vpc-file-driver
    ```
    {: pre}

1. If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
