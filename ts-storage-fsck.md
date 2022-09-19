---

copyright: 
  years: 2022, 2022
lastupdated: "2022-09-19"

keywords: openshift, fsck

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does mounting {{site.data.keyword.blockstorageshort}} fail with an `fsck` error?
{: #ts-storage-fsck}
{: troubleshoot}
{: support}

Supported infrastructure providers
:   Classic

When you view pod logs for pods that are using {{site.data.keyword.blockstorageshort}}, you see an error similar to the following example.
{: tsSymptoms}

```sh
UNEXPECTED INCONSISTENCY; RUN fsck MANUALLY.(i.e., without -a or -p 
options)
```
{: screen}

The disk is corrupted.
{: tsCauses}


Run the folling commands to patch the PV that the pod is mounting.
{: tsResolve}


1. Get the details of the pod that is failing and make a note of the PV and PVC it is mounting.
    ```sh
    kubectl get pods
    ```
    {: pre}

1. Patch the PV to add the `"ibm.io/autofix-fsckErr":"true"` annotation.
    ```sh
    kubectl patch pv PVNAME -p '{"metadata": {"annotations":{"ibm.io/autofix-
    fsckErr":"true"}}}'
    ```
    {: pre}
    
1. Delete and recreate your app pod to retry mounting the PV. After deleting and re-creating the pod, Kubernetes retries the mount operation and the {{site.data.keyword.blockstorageshort}} driver pod tries to auto-fix the issue based on the `"ibm.io/autofix-fsckErr":"true"` annotation.

1. After the pod is successfully deployed and running, run the following command to edit the PV.
    ```sh
    kubectl edit pv PVNAME
    ```
    {: pre}

1. Remove the `"ibm.io/autofix-fsckErr: true"` annotation from the PV and save it.

1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.

