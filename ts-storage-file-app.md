---

copyright: 
  years: 2014, 2022
lastupdated: "2022-05-06"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why can't my app access or write to PVCs?
{: #file_app_failures}
{: support}

**Infrastructure provider**: ![Classic](../icons/classic.svg "Classic") Classic

When you mount a PVC to your pod, you might experience errors when accessing or writing to the PVC.
{: shortdesc}

1. List the pods in your cluster and review the status of the pod.
    ```sh
    oc get pods
    ```
    {: pre}

2. Find the root cause for why your app can't access or write to the PVC.
    ```sh
    oc describe pod <pod_name>
    ```
    {: pre}

    ```sh
    oc logs <pod_name>
    ```
    {: pre}

3. Review common errors that can occur when you mount a PVC to a pod.

| Symptom or error message | Description | Steps to resolve |
| --- | --- | --- |
| Your pod is stuck in a `ContainerCreating` state. `MountVolume.SetUp failed for volume ... read-only file system`. | The {{site.data.keyword.cloud_notm}} infrastructure back end experienced network problems. To protect your data and to avoid data corruption, {{site.data.keyword.cloud_notm}} automatically disconnected the file storage server to prevent write operations on NFS file shares. | See [File storage: File systems for worker nodes change to read-only](/docs/containers?topic=containers-readonly_nodes) |
| `write-permission` `don't have required permission` `can't create directory '/bitnami/mariadb/data': Permission denied` | In your deployment, you specified a non-root user to own the NFS file storage mount path. By default, non-root users don't have write permission on the volume mount path for NFS-backed storage. | See [File storage: App fails when a non-root user owns the NFS file storage mount path](/docs/containers?topic=containers-nonroot) |
| After you specified a non-root user to own the NFS file storage mount path or deployed a Helm chart with a non-root user ID specified, the user can't write to the mounted storage. | The deployment or Helm chart configuration specifies the security context for the pod's `fsGroup` (group ID) and `runAsUser` (user ID) | See [File storage: Adding non-root user access to persistent storage fails](/docs/containers?topic=containers-cs_storage_nonroot) |
{: caption="{{site.data.keyword.filestorage_short}} error messages" caption-side="top"}
{: summary="The columns are read from left to right. The first column has the symptom or error message. The second column describes the message. The third column provides steps to resolve the error."}






