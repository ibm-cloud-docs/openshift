---

copyright: 
  years: 2024, 2024
lastupdated: "2024-10-30"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, storage, container creating, file

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}



# Why is my app pod stuck in `Container creating` when trying to mount {{site.data.keyword.filestorage_vpc_short}}?
{: #ts-vpc-file-container-creating}
{: support}


When you try to deploy an app that uses {{site.data.keyword.filestorage_vpc_short}} you see one or more of the following error messages.
{: tsSymptoms}

Example command to get the `ibm-vpc-file-csi` driver logs.
```sh
kubectl logs ibm-vpc-file-csi-node-xxx -n kube-system -c iks-vpc-file-node-driver
```
{: pre}

Example output with error message.
```sh
ibmcsidriver/node.go:94","msg":"CSINodeServer-NodePublishVolume..."
ibmcsidriver/node.go:160","msg":"CSINodeServer-NodeUnpublishVolume..."
```
{: screen}

Example `describe pod` command.

```sh
kubectl describe pod ibm-vpc-file-csi-node-xxx -n kube-system -c iks-vpc-file-node-driver
```
{: pre}

Example output with error message.

```sh
Warning FailedMount 68s kubelet MountVolume.SetUp failed for volume "pvc-c37fe511-ec6d-44c1-8c55-1b5e2c21ec5b" : rpc error: code = DeadlineExceeded desc = context deadline exceeded
Warning FailedMount 65s kubelet Unable to attach or mount volumes: unmounted volumes=[test-persistent-storage], unattached volumes=[], failed to process volumes=[]: timed out waiting for the condition
```
{: screen}

Example command to get the `pipelineruns` logs.
```sh
kubectl logs cat -n pipelineruns
```
{: pre}

Example output with error message.
```sh
Error from server (BadRequest): container "cat" in pod "cat" is waiting to start: ContainerCreating
```
{: screen}

A temporary network outage might cause file shares to be unreachable and unmountable.
{: tsCauses}

Complete the following steps to resolve the issue.
{: tsResolve}

New security group rules were introduced in versions 4.11 and later. These rule changes mean you must sync your security groups before you can use {{site.data.keyword.filestorage_vpc_short}}. If your cluster was initially created at version 4.11 or earlier, run the following commands to sync your security group settings.
{: important}

* If your cluster was initially created at version 4.11 or earlier:

    1. Get the ID of your cluster.
        ```sh
        ibmcloud oc cluster ls
        ```
        {: pre}

    1. Get the ID of the `kube-<clusterID>` security group.
        ```sh
        ibmcloud is sg kube-<cluster-id>  | grep ID
        ```
        {: pre}

    1. Sync the `kube-<clusterID>` security group by using the ID that you retrieved in the previous step.
        ```sh
        ibmcloud ks security-group sync -c <cluster ID> --security-group <ID>
        ```
        {: pre}

* If your cluster was created at version 4.11 and later, verify that the worker node where pod is deployed is allowlisted in the VNI security group.

1. If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
