---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-08"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---
{{site.data.keyword.attribute-definition-list}}



# Why can't non-root users access files?
{: #cos_nonroot_access}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


You uploaded files to your {{site.data.keyword.cos_full_notm}} service instance by using the console or the REST API. When you try to access these files with a non-root user that you defined with `runAsUser` in your app deployment, access to the files is denied.
{: tsSymptoms}


In Linux, a file or a directory has three access groups: `Owner`, `Group`, and `Other`. When you upload a file to {{site.data.keyword.cos_full_notm}} by using the console or the REST API, the permissions for the `Owner`, `Group`, and `Other` are removed. The permission of each file looks as follows:
{: tsCauses}

```sh
d--------- 1 root root 0 Jan 1 1970 <file_name>
```
{: screen}

When you upload a file by using the {{site.data.keyword.cos_full_notm}} plug-in, the permissions for the file are preserved and not changed.


To access the file with a non-root user, the non-root user must have read and write permissions for the file. Changing the permission on a file as part of your pod deployment requires a write operation. {{site.data.keyword.cos_full_notm}} is not designed for write workloads.
{: tsResolve}

Updating permissions during the pod deployment might prevent your pod from getting into a `Running` state.

To resolve this issue, before you mount the PVC to your app pod, create another pod to set the correct permission for the non-root user.

1. To check the permissions of your files in your bucket, create a configuration file for your `test-permission` pod and name the file `test-permission.yaml`.
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: test-permission
    spec:
      containers:
      - name: test-permission
         image: nginx
         volumeMounts:
         - name: cos-vol
         mountPath: /test
      volumes:
      - name: cos-vol
         persistentVolumeClaim:
         claimName: <pvc_name>
   ```
   {: codeblock}

2. Create the `test-permission` pod.

    ```sh
    oc apply -f test-permission.yaml
    ```
    {: pre}

3. Log in to your pod.

    ```sh
    oc exec test-permission -it bash
    ```
    {: pre}

4. Navigate to your mount path and list the permissions for your files.

    ```sh
    cd test && ls -al
    ```
    {: pre}

    Example output

    ```sh
    d--------- 1 root root 0 Jan 1 1970 <file_name>
    ```
    {: screen}

5. Delete the pod.

    ```sh
    oc delete pod test-permission
    ```
    {: pre}

6. Create a configuration file for the pod that you use to correct the permissions of your files and name it `fix-permission.yaml`.

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: fix-permission
      namespace: <namespace>
    spec:
      containers:
      - name: fix-permission
        image: busybox
        command: ['sh', '-c']
        args: ['chown -R <nonroot_userID> <mount_path>/*; find <mount_path>/ -type d -print -exec chmod u=+rwx,g=+rx {} \;']
        volumeMounts:
        - mountPath: "<mount_path>"
          name: cos-volume
      volumes:
      - name: cos-volume
        persistentVolumeClaim:
          claimName: <pvc_name>
    ```
    {: codeblock}

3. Create the `fix-permission` pod.

    ```sh
    oc apply -f fix-permission.yaml
    ```
    {: pre}

4. Wait for the pod to go into a `Completed` state. 

    ```sh
    oc get pod fix-permission
    ```
    {: pre}

5. Delete the `fix-permission` pod.

    ```sh
    oc delete pod fix-permission
    ```
    {: pre}

5. Re-create the `test-permission` pod that you used earlier to check the permissions.

    ```sh
    oc apply -f test-permission.yaml
    ```
    {: pre}

## Verifying that the permissions for your files are updated
{: #verifying_file_permission_update}

1. Log in to your pod.

    ```sh
    oc exec test-permission -it bash
    ```
    {: pre}

2. Navigate to your mount path and list the permissions for your files.

    ```sh
    cd test && ls -al
    ```
    {: pre}

    Example output

    ```sh
    -rwxrwx--- 1 <nonroot_userID> root 6193 Aug 21 17:06 <file_name>
    ```
    {: screen}

6. Delete the `test-permission` pod.

    ```sh
    oc delete pod test-permission
    ```
    {: pre}

7. Mount the PVC to the app with the non-root user.


Define the non-root user as `runAsUser` without setting `fsGroup` in your deployment YAML at the same time. Setting `fsGroup` triggers the {{site.data.keyword.cos_full_notm}} plug-in to update the group permissions for all files in a bucket when the pod is deployed. Updating the permissions is a write operation and might prevent your pod from getting into a `Running` state.
{: important}

After you set the correct file permissions in your {{site.data.keyword.cos_full_notm}} service instance, do not upload files by using the console or the REST API. Use the {{site.data.keyword.cos_full_notm}} plug-in to add files to your service instance.
{: tip}






