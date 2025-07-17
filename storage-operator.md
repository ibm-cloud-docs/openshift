---

copyright: 
  years: 2024, 2025
lastupdated: "2025-07-17"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, add-on, storage operator

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Enabling the IBM Storage Operator cluster add-on
{: #storage-operator}

The `ibm-storage-operator` cluster add-on manages several storage configmaps and resources in your cluster.
{: shortdesc}

The `ibm-storage-operator` is installed by default in VPC clusters beginning with versions 4.15 and later and is a dependency of the {{site.data.keyword.filestorage_vpc_full_notm}} add-on.

1. Update the `container-service` plug-in to the most recent version. You can update the plug-in by running the following command.
    ```shell
    ibmcloud update && ibmcloud plugin update container-service
    ```
    {: pre}

1. Check if the add-on is enabled.
    ```sh
    ibmcloud oc cluster addon ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output
    ```sh
    Name                   Version   Health State   Health Status   
    ibm-storage-operator    1.0.0     normal         Addon Ready
    ```
    {: pre}

1. If the add-on is not enabled, enable it.
    ```sh
    ibmcloud oc cluster addon enable ibm-storage-operator -c CLUSTER --version VERSION
    ```
    {: pre}

## Disabling the `ibm-storage-operator` add-on
{: #storage-operator-disable}

Note that you can't disable the add-on if there are other add-ons are using the `ibm-storage-operator`.
{: note}

1. Run the following command to disable the add-on.

    ```sh
    ibmcloud oc cluster addon disable ibm-storage-operator -c CLUSTER
    ```
    {: pre}

    Example output where dependencies are installed.
    ```sh
    Data and resources that you created for the add-on might be deleted when the add-on is disabled. Continue? [y/N]> y
    Disabling add-on ibm-storage-operator for cluster devcluster2...
    FAILED
    Unable to disable ibm-storage-operator because it is required by the vpc-file-csi-driver add-on(s).
    ```
    {: screen}

1. If you no longer need the dependencies, remove them before continuing.


1. Disable the add-on.

    ```sh
    ibmcloud oc cluster addon disable ibm-storage-operator -c CLUSTER
    ```
    {: pre}
