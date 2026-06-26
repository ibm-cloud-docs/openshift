---

copyright:
  years: 2021, 2026
lastupdated: "2026-06-26"


keywords: openshift, storage

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}






# Why are the OpenShift Data Foundation pods stuck at `Pending`?
{: #ts-ocs-pods-pending-status}
{: support}

When you list pods in the `openshift-storage` namespace, the OpenShift Data Foundation pods are stuck at `Pending` status.
{: shortdesc}

When you run `oc get pods -n openshift-storage`, the OpenShift Data Foundation pods show a `Pending` status.
{: tsSymptoms}

To determine why your storage cluster pods are stuck at `Pending`, describe the pods that have the `Pending` status.
{: tsCauses}

```sh 
oc describe pod <pod> -n openshift-storage
```
{: pre}

In the output, check the `Events` section for the following error:
```sh
"Error: 0/3 nodes are available: 1 node(s) didn't match pod affinity/anti-affinity, 2 node(s) had volume node affinity conflict"
```
{: screen}

This error indicates that the classic or VPC cluster where your OpenShift Data Foundation storage cluster is installed is a multizone cluster, but the storage classes specified in the `monStorageClassName` or `osdStorageClassName` fields have a `VolumeBindingMode` parameter set to `Immediate`.

The `VolumeBindingMode` parameter controls when volume binding and dynamic provisioning occur. When set to `Immediate`, volumes are provisioned as soon as the PVC is created. However, multizone OpenShift Data Foundation deployments require storage classes with `VolumeBindingMode` set to `WaitForFirstConsumer`, which delays volume binding until a pod using the PVC is scheduled. This ensures that volumes are created in the same zone as the pod.
{: tsResolve}

1. [Create your own storage class](/docs/openshift?topic=openshift-vpc-block#vpc-customize-storage-class) with the `VolumeBindingMode` set to `WaitForFirstConsumer`, or choose a pre-existing storage class with the same parameters.

2. List the name of your OpenShift Data Foundation storage cluster.
    ```sh
    oc get storagecluster -n openshift-storage
    ```
    {: pre}

    Example output:
    ```sh
    NAME                 AGE
    ocs-storagecluster   71d
    ```
    {: screen}

3. Delete the storage cluster.
    ```sh
    oc delete storagecluster <storage_cluster_name> -n openshift-storage
    ```
    {: pre}

4. Verify that your storage cluster is deleted and is not listed.
    ```sh
    oc get storagecluster -n openshift-storage
    ```
    {: pre}

5. [Re-create the storage cluster](/docs/openshift?topic=openshift-deploy-odf-vpc) with the storage class you chose in step 1. Make sure to specify the correct storage class in the `monStorageClassName` and `osdStorageClassName` fields.
