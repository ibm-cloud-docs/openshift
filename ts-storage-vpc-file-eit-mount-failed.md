---

copyright: 
  years: 2024, 2024
lastupdated: "2024-07-16"


keywords: kubernetes, openshift, MountingTargetFailed, encryption in-transit, eit

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Why do I see a `MountingTargetFailed` error for {{site.data.keyword.filestorage_vpc_short}}?
{: #ts-storage-vpc-file-eit-mount-failed}

[Virtual Private Cloud]{: tag-vpc}

Volume mounting fails with an error message similar to the following.
{: tsSymptoms}

```sh
Warning FailedMount 68s kubelet MountVolume.SetUp failed for volume "pvc-c37fe511-ec6d-44c1-8c55-1b5e2c21ec5b" : rpc error: code = DeadlineExceeded desc = context deadline exceeded
Warning FailedMount 65s kubelet Unable to attach or mount volumes: unmounted volumes=[test-persistent-storage], unattached volumes=[], failed to process volumes=[]: timed out waiting for the condition
```
{: screen}

New security group rules were introduced in cluster versions 4.11 and later. These rule changes mean that you must sync your security groups before you can use {{site.data.keyword.filestorage_vpc_short}}. For more information, see [Adding {{site.data.keyword.filestorage_vpc_short}} to apps](/docs/containers?topic=containers-storage-file-vpc-apps).
{: tsCauses}

If your cluster was initially created at a version earlier than 4.11, make sure to sync your security groups by running the [security group sync command](https://cloud.ibm.com/docs/containers?topic=containers-kubernetes-service-cli#security_group_sync).
{: tsResolve}


1. Get the ID of the `kube-<clusterID>` security group.

    ```sh
    ibmcloud is sg kube-<cluster-id>  | grep ID
    ```
    {: pre}


1. Sync your security group settings.

    ```sh
    ibmcloud ks security-group sync -c <cluster ID> --security-group <ID>
    ```
    {: pre}



If your cluster was created at version 4.11 or later, verify that the node on whichever pod is deployed is allowlisted in the [VNI security group](/docs/containers?topic=containers-storage-file-vpc-apps#storage-file-vpc-vni-prereqs).
{: note}


