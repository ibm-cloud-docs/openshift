---

copyright: 
  years: 2014, 2021
lastupdated: "2021-09-24"

keywords: block, debug, help

subcollection: openshift
content-type: troubleshoot

---



{{site.data.keyword.attribute-definition-list}}

# Why do I get a `Volume not attached` error when trying to expand a {{site.data.keyword.block_storage_is_short}} volume?
{: #block_not_attached_vpc}

**Infrastructure provider**:
* <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC


When you edit a {{site.data.keyword.block_storage_is_short}} and update the `spec.resources.requests.storage` section to expand your volume, you see the following error:
{: tsSymptoms}

```sh
Volume not attached
```
{: screen}


You tried to expand the volume size of an existing {{site.data.keyword.block_storage_is_short}} PVC that is not mounted by a pod. Only volumes mounted by app pods can be expanded.
{: tsCauses}


Verify that your PVC supports volume expansion, then create an app pod that uses your PVC.
{: tsResolve}

1. Describe your existing PVC. Verify that `allowVolumeExpansion` is set to `true`.
    ```sh
    oc describe pvc <pvc-name>
    ```
    {: pre}

1. Create an app pod that uses your PVC and deploy it to your cluster.

1. Edit the PVC and increase the value in the `spec.resources.requests.storage` field.
    ```sh
    oc edit pvc <pvc-name>
    ```
    {: pre}

1. Get the details of your PVC and make a note of the PV name.
    ```sh
    oc get pvc <pvc-name>
    ```
    {: pre}

1. Describe your PV and make a note of the volume ID
    ```sh
    oc describe PV
    ```
    {: pre}

1. Get the details of your {{site.data.keyword.block_storage_is_short}} volume and verify the capacity.
    ```sh
    ibmcloud is vol <volume-ID>
    ```
    {: pre}







