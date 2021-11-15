---

copyright: 
  years: 2014, 2021
lastupdated: "2021-11-15"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does mounting existing block storage to a pod fail with the wrong file system?
{: #block_filesystem}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


When you run `oc describe pod <pod_name>`, you see the following error:
{: tsSymptoms}

```sh
failed to mount the volume as "ext4", it already contains xfs. Mount error: mount failed: exit status 32
```
{: screen}


You have an existing block storage device that is set up with an `XFS` file system. To mount this device to your pod, you [created a PV](/docs/openshift?topic=openshift-block_storage#existing_block) that specified `ext4` as your file system or no file system in the `spec/flexVolume/fsType` section. If no file system is defined, the PV defaults to `ext4`.
{: tsCauses}

The PV was created successfully and was linked to your existing block storage instance. However, when you try to mount the PV to your cluster by using a matching PVC, the volume fails to mount. You cannot mount your `XFS` block storage instance with an `ext4` file system to the pod.


Update the file system in the existing PV from `ext4` to `XFS`.
{: tsResolve}

1. List the existing PVs in your cluster and note the name of the PV that you used for your existing block storage instance.
    ```sh
    oc get pv
    ```
    {: pre}

2. Save the PV YAML on your local machine.
    ```sh
    oc get pv <pv_name> -o yaml > <filepath/xfs_pv.yaml>
    ```
    {: pre}

3. Open the YAML file and change the `fsType` from `ext4` to `xfs`.
4. Replace the PV in your cluster.
    ```sh
    oc replace --force -f <filepath/xfs_pv.yaml>
    ```
    {: pre}

5. Log in to the pod where you mounted the PV.
    ```sh
    oc exec -it <pod_name> sh
    ```
    {: pre}

6. Verify that the file system changed to `XFS`.
    ```sh
    df -Th
    ```
    {: pre}

    **Example output**:
    ```sh
    Filesystem Type Size Used Avail Use% Mounted on /dev/mapper/3600a098031234546d5d4c9876654e35 xfs 20G 33M 20G 1% /myvolumepath
    ```
    {: screen}






