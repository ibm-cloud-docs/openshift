---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-01"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}


# Why does my app fail with a group ID error for NFS file storage permissions?
{: #root}
{: support}

**Infrastructure provider**: ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic


After you [create](/docs/openshift?topic=openshift-file_storage#add_file) or [add existing](/docs/openshift?topic=openshift-file_storage#existing_file) NFS storage to your cluster, your app's container deployment fails. You see group ID (GID) error messages.
{: tsSymptoms}


When you create a container from an image that does not specify a user and user ID (UID), all instructions in the Dockerfile are run by the root user (UID: 0) inside the container by default.
{: tsCauses}

However, when you want to mount an NFS file share to your container, the user ID `0` inside the container is mapped to the user ID `nobody` on the NFS host system. Therefore, the volume mount path is owned by the user ID `nobody` and not by `root`. This security feature is also known as root squash. Root squash protects the data within NFS by mounting the container without granting the user ID root permissions on the actual NFS host file system.


Use a Kubernetes [`DaemonSet`](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/){: external} to enable root permission to the storage mount path on all your worker nodes for NFSv4 file shares.
{: tsResolve}

To allow root permission on the volume mount path, you must set up a configmap on your worker node. The configmap maps the user ID `nobody` from the NFS host system to the root user ID `0` in your container. This process is also referred to as no root squash. An effective way of updating all your worker nodes is to use a daemon set, which runs a specified pod on every worker node in your cluster. In this case, the pod that is controlled by the daemon set updates each of your worker nodes to enable root permission on the volume mount path.

The deployment is configured to allow the daemon set pod to run in privileged mode, which is necessary to access the host file system. Running a pod in privileged mode does create a security risk, so use this option with caution.

While the daemon set is running, new worker nodes that are added to the cluster are automatically updated.

Before you begin:

* [Create persistent storage](/docs/openshift?topic=openshift-file_storage#add_file).
* [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

Steps:

1. Copy the `norootsquash` daemon set [deployment YAML file](https://github.com/IBM-Cloud/kube-samples/tree/master/daemonset-sample){: external}

2. Create the `norootsquash` daemon set deployment.
    ```sh
    oc apply -f norootsquash.yaml
    ```
    {: pre}

3. Get the name of the pod that your storage volume is mounted to. This pod is not the same as the `norootsquash`  pods.
    ```sh
    oc get pods
    ```
    {: pre}

4. Log in to the pod.
    ```sh
    oc exec -it mypod /bin/bash
    ```
    {: pre}

5. Verify that the permissions to the mount path are `root`.
    ```sh
    root@mypod:/# ls -al /mnt/myvol/
    total 8
    drwxr-xr-x 2 root root 4096 Feb  7 20:49 .
    drwxr-xr-x 1 root root 4096 Feb 20 18:19 .
    ```
    {: pre}

    This output shows that the UID in the first row is now owned by `root` (instead of previously `nobody`).

6. If the UID is owned by `nobody`, exit the pod and reboot your cluster's worker nodes. Wait for the nodes to reboot.
    ```sh
    ibmcloud oc worker reboot --cluster <my_cluster> --worker <my_worker1>,<my_worker2>
    ```
    {: pre}

7. Repeat Steps 4 and 5 to verify the permissions.







