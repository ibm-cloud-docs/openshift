---

copyright:
  years: 2021, 2021
lastupdated: "2021-10-08"

keywords: openshift, storage

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why are the ODF pods stuck at `Pending`?
{: #ts-ocs-pods-pending-status}


When you list pods in the `openshift-storage` namespace with the `oc get pods -n openshift-storage` command, the ODF pods are stuck at `Pending`.
{: tsSymptoms}


To determine why your storage cluster status is stuck at `Pending`, describe the pods that have the status `Pending`.
{: tsCauses}

```sh 
oc describe pod <pod> -n openshift-storage
```
{: pre}

In the output, check the `Events` section for the following error:
```
"Error: 0/3 nodes are available: 1 node(s) didn't match pod affinity/anti-affinity, 2 node(s) had volume node affinity conflict"
```
{: screen}

This error indicates that that the classic or VPC cluster where your ODF storage cluster is installed is a multizone cluster, but the storage classes specified in the `monStorageClassName` or `osdStorageClassName` fields in your CRD have a `VolumeBindingMode` parameter that is set to `Immediate`. Multizone ODF deployments require storage classes that have the `VolumeBindingMode` parameter set to `WaitForFirstConsumer`.
{: tsResolve}

1. [Create custom storage class](/docs/openshift?topic=openshift-vpc-block#vpc-customize-storage-class) with the `VolumeBindingMode` set to `WaitForFirstConsumer`, or choose a pre-exisiting storage class with the same parameters. 

2. List the name of your ODF storage cluster. 
    ```sh
    oc get ocscluster
    ```
    {: pre}

    **Example output**:
    ```sh
    NAME             AGE
    ocscluster-vpc   71d
    ```
    {: screen}

3. Delete the storage cluster.
    ```sh
    oc delete ocscluster <ocs_cluster_name>
    ```
    {: pre}

4. Verify that your storage cluster is deleted and is not listed.
    ```sh
    oc get ocscluster
    ```
    {: pre}

5. Re-create the CRD with the pre-existing or custom storage class you chose earlier.

6. Re-deploy the storage cluster.








