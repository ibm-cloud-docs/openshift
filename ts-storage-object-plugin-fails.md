---

copyright: 
  years: 2014, 2026
lastupdated: "2026-05-14"


keywords: openshift

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}





# Why does installing the {{site.data.keyword.cos_full_notm}} plug-in fail?
{: #cos_plugin_fails}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

Installing the {{site.data.keyword.cos_full_notm}} plug-in fails due to conflicting resources from previous installations.
{: shortdesc}

When you install the `ibm-object-storage-plugin`, the installation fails.
{: tsSymptoms}

You see an error message similar to the following example:

```sh
Error: rendered manifest contains a resource that already exists. Unable to continue with install. Existing resource conflict: namespace: , name: ibmc-s3fs-smart-cross-region, existing_kind: storageClass, new_kind: storage.k8s.io/v1, Kind=StorageClass
Error: plugin "ibmc" exited with error
```
{: screen}


During the installation, the {{site.data.keyword.cos_full_notm}} plug-in executes many different tasks, such as creating storage classes and cluster role bindings. Some resources might already exist in your cluster from previous {{site.data.keyword.cos_full_notm}} plug-in installations and were not properly removed when you removed or upgraded the plug-in.
{: tsCauses}

## Resolving the issue
{: #cos-plugin-resolve}

Delete the resource that is displayed in the error message and retry the installation.
{: tsResolve}

1. Delete the resource that is displayed in the error message.
    ```sh
    oc delete <resource_kind> <resource_name>
    ```
    {: pre}

    Example for deleting a storage class resource:
    ```sh
    oc delete storageclass <storage_class_name>
    ```
    {: pre}

2. [Retry the installation](/docs/openshift?topic=openshift-storage_cos_install).

3. If you continue to see the same error, identify and remove all conflicting resources from previous installations.

4. Get a list of storage classes that are created by the `ibmcloud-object-storage-plugin`.
    ```sh
    oc get sc --all-namespaces \
            -l app=ibmcloud-object-storage-plugin \
            -o jsonpath='{range .items[*]}{.metadata.name}{"\n"}{end}'
    ```
    {: pre}

5. Get a list of cluster role bindings that are created by the `ibmcloud-object-storage-plugin`.
    ```sh
    oc get ClusterRoleBinding --all-namespaces \
            -l app=ibmcloud-object-storage-plugin \
            -o jsonpath='{range .items[*]}{.metadata.name}{"\n"}{end}'
    ```
    {: pre}

6. Get a list of role bindings that are created by the `ibmcloud-object-storage-driver`.
    ```sh
    oc get RoleBinding --all-namespaces \
        -l app=ibmcloud-object-storage-driver \
        -o jsonpath='{range .items[*]}{.metadata.namespace}{"\t"}{.metadata.name}{"\n"}{end}'
    ```
    {: pre}

7. Get a list of role bindings that are created by the `ibmcloud-object-storage-plugin`.
    ```sh
    oc get RoleBinding --all-namespaces \
            -l app=ibmcloud-object-storage-plugin \
            -o jsonpath='{range .items[*]}{.metadata.namespace}{"\t"}{.metadata.name}{"\n"}{end}'
    ```
    {: pre}

8. Get a list of cluster roles that are created by the `ibmcloud-object-storage-plugin`.
    ```sh
    oc get ClusterRole --all-namespaces \
        -l app=ibmcloud-object-storage-plugin \
        -o jsonpath='{range .items[*]}{.metadata.name}{"\n"}{end}'
    ```
    {: pre}

9. Get a list of deployments that are created by the `ibmcloud-object-storage-plugin`.
    ```sh
    oc get deployments --all-namespaces \
        -l app=ibmcloud-object-storage-plugin \
        -o jsonpath='{range .items[*]}{.metadata.namespace}{"\t"}{.metadata.name}{"\n"}{end}'
    ```
    {: pre}

10. Get a list of the daemon sets that are created by the `ibmcloud-object-storage-driver`.
    ```sh
    oc get DaemonSets --all-namespaces \
        -l app=ibmcloud-object-storage-driver \
        -o jsonpath='{range .items[*]}{.metadata.namespace}{"\t"}{.metadata.name}{"\n"}{end}'
    ```
    {: pre}

11. Get a list of the service accounts that are created by the `ibmcloud-object-storage-driver`.
    ```sh
    oc get ServiceAccount --all-namespaces \
        -l app=ibmcloud-object-storage-driver \
        -o jsonpath='{range .items[*]}{.metadata.namespace}{"\t"}{.metadata.name}{"\n"}{end}'
    ```
    {: pre }

12. Get a list of the service accounts that are created by the `ibmcloud-object-storage-plugin`.
    ```sh
    oc get ServiceAccount --all-namespaces \
        -l app=ibmcloud-object-storage-plugin \
        -o jsonpath='{range .items[*]}{.metadata.namespace}{"\t"}{.metadata.name}{"\n"}{end}'
    ```
    {: pre}

13. Delete the conflicting resources that were identified in the previous steps.

    ```sh
    oc delete <resource_kind> <resource_name>
    ```
    {: pre}

14. After you delete the conflicting resources, [retry the installation](/docs/openshift?topic=openshift-storage_cos_install).

15. Verify the plug-in is installed successfully.

    ```sh
    oc get pods -n kube-system | grep object-storage
    ```
    {: pre}
