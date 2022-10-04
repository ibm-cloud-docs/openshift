---

copyright: 
  years: 2022, 2022
lastupdated: "2022-10-04"

keywords: openshift, storage, snapshot, volumesnapshot

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}



# Why can't I create {{site.data.keyword.block_storage_is_short}} snapshots?
{: #ts-storage-volumesnapshotdelete}
{: support}

**Infrastructure provider**:
VPC

You are unable to create `volumesnapshots`.
{: tsSymptoms}

There are several reasons why you might not be able to create snapshots. To debug the issue, complete the following steps to gather the required log files before contacting support.
{: tsCauses}


1. Describe your `volumesnapshot` and review the status.
    ```sh
    kubectl describe volumesnapshot VOLUMESNAPSHOT
    ```
    {: pre}

1. Get the logs of the `ibm-vpc-block-csi-controller-0` driver and sidecar.
    ```sh
    kubectl logs -n kube-system ibm-vpc-block-csi-controller-0 -c csi-snapshotter
    ```
    {: pre}
    
    ```sh
    kubectl logs -n kube-system ibm-vpc-block-csi-controller-0 -c iks-vpc-block-driver
    ```
    {: pre}

    ```sh
    kubectl logs -n kube-system ibm-vpc-block-csi-controller-0
    ```
    {: pre}
    
1. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
