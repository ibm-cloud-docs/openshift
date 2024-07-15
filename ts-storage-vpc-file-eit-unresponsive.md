---

copyright: 
  years: 2024, 2024
lastupdated: "2024-07-15"


keywords: kubernetes, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Why do I see an `UnresponsiveMountHelperContainerUtility` error for {{site.data.keyword.filestorage_vpc_short}}?
{: #ts-storage-vpc-file-eit-unresponsive}

[Virtual Private Cloud]{: tag-vpc}


Your app that uses encryption in-transit {{site.data.keyword.filestorage_vpc_short}} fails with an `UnresponsiveMountHelperContainerUtility` error.
{: tsSymptoms}

You see an error message similar to the following example.

```sh
Code: UnresponsiveMountHelperContainerUtility, Description: Failed to mount target because unable to make connection to mount helper container service., BackendError: Failed to send EIT based request. Failed with error: Post "http://unix/api/mount": dial unix /var/lib/ibmshare.sock: connect: no such file or directory, Action: Check if EIT is enabled from storage operator. Run command 'kubectl edit configmap addon-vpc-file-csi-driver-configmap -n kube-system' and set 'ENABLE_EIT' flag to 'true'.}
```
{: screen}

Either encryption in-transit (EIT) is not enabled on your worker pools or, if EIT is enabled, your app that uses EIT features is running on a different worker node where EIT is not enabled.
{: tsCauses}

Make sure that your app pod is running in the same worker pool as mentioned in the `EIT_ENABLED_WORKER_POOL` section of the configmap. Also verify that EIT is enabled for the workers on which pod is getting scheduled.
{: tsResolve}

1. Review the `file-csi-driver-status` configmap and verify that EIT is enabled. Make sure that the `ENABLE_EIT` flag is set to `true` and that you have specified the worker pools where you want to run your app.

    ```sh
    oc describe cm file-csi-driver-status -n kube-system
    ```
    {: pre}

1. List your app pods and verify your app is running in the worker pool specified in the `EIT_ENABLED_WORKER_POOL` configmap section.

    ```sh
    oc get pods -A
    ```
    {: pre}

