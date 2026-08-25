---

copyright: 
  years: 2025, 2026
lastupdated: "2026-08-25"


keywords: openshift, storage, file storage vpc, cluster add-on, add-ons

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is the {{site.data.keyword.filestorage_vpc_short}} add-on in `Critical` state
{: #ts-storage-file-addon-cm}

When you list add-ons or check the {{site.data.keyword.filestorage_vpc_short}} add-on status configmap, you see errors similar to the following.
{: tsSymptoms}


Troubleshoot file storage add-on ConfigMap issues.
{: shortdesc}

```txt
Unable to set 'bmf' as default storage class due to internal error.
event: Change default storage class request
```
{: screen}

```txt
'EnableVPCFileCSIDriver unsuccessful, Error: resource name may not be empty, DriverVersion: v2.0.13'
```
{: screen}


The `addon-vpc-file-csi-driver-configmap` has missing or incorrect values.
{: tsCauses}

Review `file-csi-driver-status` configmap for errors and update any missing or incorrect values in the `addon-vpc-file-csi-driver-configmap` configmap.
{: tsResolve}


1. Review the add-on status.
    ```sh
    ibmcloud ks cluster addon ls --cluster <cluster>
    ```
    {: pre}

1. Review the events in the file status configmap.
    ```sh
    oc get cm file-csi-driver-status -n kube-system -o yaml
    ```
    {: pre}

    Example output
    ```yaml
    apiVersion: v1
    data:
      EIT_ENABLED_WORKER_NODES: ""
      PACKAGE_DEPLOYER_VERSION: ""
      SET_DEFAULT_STORAGE_CLASS: ""
      events: |
        - description: Unable to set 'bmf' as default storage class due to internal error.
          event: Change default storage class request
          timestamp: "2025-06-26 14:07:53"
        - description: 'EnableVPCFileCSIDriver unsuccessful, Error: resource name may not
            be empty, DriverVersion: v2.0.13'
          event: EnableVPCFileCSIDriver
          timestamp: "2025-06-26 14:07:53"
    ```

1. Get the storage operator logs.
    ```sh
    kubectl logs ibm-storage-operator-xxx -n kube-system
    ```
    {: pre}

1. If any property is missing or invalid, edit the value in the configmap.
    ```sh
    kubectl edit cm addon-vpc-file-csi-driver-configmap  -n kube-system -o yaml
    ```
    {: pre}

1. After 5-10 mins check the add-on status.
    ```sh
    ibmcloud ks cluster addon ls --cluster <cluster>
    ```
    {: pre}

1. If the issue persists, contact support. Open a [support case](/docs/support?topic=support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.


