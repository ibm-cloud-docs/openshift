---
copyright:
  years: 2023, 2023
lastupdated: "2023-11-28"

keywords: openshift, byok, debug, help, vpc, storage, encryption

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why can't I create a VPC cluster with encrypted worker nodes? 
{: #ts-vpc-byok-encrypted-storage}
{: support}

The VPC worker nodes can not be provisioned due to a key error with the KMS provider.
{: tsSymptoms}

```sh
Encrypted storage cannot be configured. Review the customer root key configuration for the worker pool.
```
{: pre}

The KMS instance or root key was deleted between the time the worker pool was created and the time the worker was provisioned.
{: tsCauses}

Verify that the KMS instance or root key still exist. If either one has been deleted, you must re-create the instance and a new worker pool to use encryption. 
{: tsResolve}

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. To check that KMS encryption is enabled, verify that the **Key Management Service** status is set to `enabled`.
    ```sh
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}


    Example output when the master is ready.
    ```sh
    NAME:                   <cluster_name>   
    ID:                     <cluster_ID>   
    ...
    Master Status:          Ready (1 min ago)
    ...
    Key Management Service: enabled   
    ```
    {: screen}

1. Verify that the root key still exists from the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}. 

    1. Log in to the IBM Cloud console.

    1. Go to **Menu** > **Resource list** to view a list of your resources.

    1. From the resource list, select your instance of your KMS provider. 


1. If either instance or the root key has been disabled or deleted, you must recreate them. For more information, see [Setting up a KMS provider](/docs/openshift?topic=openshift-encryption-setup).

1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.





