---

copyright: 
  years: 2025, 2026
lastupdated: "2026-01-27"


keywords: kubernetes, openshift, {{site.data.keyword.filestorage_vpc_short}}, snapshot, restore

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Why can't I create {{site.data.keyword.filestorage_vpc_short}} snapshots?
{: #ts-storage-vpc-file-snapshot-create}
{: support}


[Virtual Private Cloud]{: tag-vpc}


You are unable to create snapshots and you see error messages similar to the following.
{: tsSymptoms}

```sh
shares_snapshot_operation_not_allowed
```
{: screen}

```sh
shares_access_forbidden
```
{: screen}


There are several reasons why you might not be able to create snapshots. To debug the issue, complete the following steps to gather the required log files before contacting support.
{: tsCauses}

1. Describe your volume snapshot and review the status.
    ```sh
    kubectl describe volumesnapshot VOLUMESNAPSHOT
    ```
    {: pre}

    * If there is a `shares_snapshot_operation_not_allowed` error, make sure you have been allowlisted for regional file share access and contact IBM VPC Support team.

    * If there is a `shares_access_forbidden` error, make sure you have **Share Snapshot Operator** [permissions in IAM](/docs/account?topic=account-iam-service-roles-actions#is.share-roles).

1. If issue still persist then get the logs of the `ibm-vpc-file-csi-controller-XXX` driver and sidecar pod. Replace `ibm-vpc-file-csi-controller-XXX` with the exact pod name from your cluster.

    ```sh
    kubectl logs -n kube-system ibm-vpc-file-csi-controller-XXX -c csi-snapshotter
    ```
    {: pre}

    ```sh
    kubectl logs -n kube-system ibm-vpc-file-csi-controller-xx -c iks-vpc-file-driver
    ```
    {: pre}

1. If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
