---

copyright:
  years: 2014, 2021
lastupdated: "2021-10-19"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does pod not build with a permission denied error because of security context constraint (SCC)?
{: #ts-app-scc}
{: troubleshoot}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


A system pod or other pod that uses a security context constraint (SCC) has an operation that keeps retrying but fails with a `permission denied` error. For example, you might log in to the internal `image-registry` pod and try to run `docker push`.
{: tsSymptoms}

Example error message when pushing an image to the internal registry:
```
error: build error: Failed to push image: error copying layers and metadata
```
{: screen}


The pod might use an SCC or belong to a system group that uses an SCC without the correct permission. You might have added a system group to an SCC by running `oc adm policy add-scc-to-group <scc> system:<group>`.
{: tsCauses}

If the pod mounts a volume, the pod's permissions that are authorized by the SCC might no longer allow the pod to read or write data to the volume.

For example, the internal registry mounts a volume to read and write image data to a file storage instance. If the `system:authenticated` group that the internal registry belongs to changes the SCC from `restricted` to `anyuid`, then the pod runs with a different UID. The different UID prevents the internal registry pod from pushing or pulling images from the storage device.


Change the pod's SCC permissions.
{: tsResolve}

1. Describe the pod and check the `openshift.io/scc: <scc>` security context constraint in the **Annotations** section.
    ```sh
    oc describe pod -n <project> <pod>
    ```
    {: pre}

    Example output

    ```sh
    NAME:               image-registry-1234567
    Namespace:          openshift-image-registry
    Priority:           2000000000
    PriorityClassName:  system-cluster-critical
    Node:               10.xxx.xx.xxx/10.xxx.xx.xxx
    Start Time:         Wed, 19 Feb 2020 15:38:53 -0500
    Labels:             docker-registry=default
    Annotations:        openshift.io/scc: anyuid
    ```
    {: screen}

2. Describe the security context constraint and check the user and groups in the **Access** section.
    ```sh
    oc describe scc <scc>
    ```
    {: pre}

    Example output

    ```sh
    NAME:                        anyuid
    Priority:                    <none>
    Access:                        
        Users:                    <none>
        Groups:                    system:authenticated
    ```
    {: screen}

3. If you do not want the user or group to have the permissions of the SCC, remove the user or group from the SCC. For more information, review the default [{{site.data.keyword.openshiftshort}}](/docs/openshift?topic=openshift-openshift_scc#oc_sccs) and [{{site.data.keyword.cloud_notm}}](/docs/openshift?topic=openshift-openshift_scc#ibm_sccs) SCCs that are set in the cluster.
    ```sh
    oc adm policy remove-scc-from-group <scc> <(user|group)>
    ```
    {: pre}

4. Add the user or group to the SCC with the appropriate permissions.
    ```sh
    oc adm policy add-scc-to-group <scc> <(user|group)>
    ```
    {: pre}

5. Delete the pod so that the pod is rescheduled with the new SCC permissions.
    ```sh
    oc delete pod -n <project> <pod>
    ```
    {: pre}






