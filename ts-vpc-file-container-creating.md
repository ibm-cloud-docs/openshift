---

copyright: 
  years: 2024, 2024
lastupdated: "2024-01-26"


keywords: openshift, storage, container creating, file

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

Example command to get the pipelineruns logs.
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

1. Restart the `ibm-vpc-file-csi-node` daemonset.
    ```sh
    kubectl rolloutrestart daemonset ibm-vpc-file-csi-node
    ```
    {: pre}

1. Wait a few minutes for the daemonset to restart.                                                                

1. Retry your app deployment.

1. Reboot the worker node.
    ```sh
    ibmcloud oc worker reboot -c CLUSTER -w WORKER
    ```
    {: pre}

1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.


