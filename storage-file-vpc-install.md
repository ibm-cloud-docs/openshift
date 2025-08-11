---

copyright: 
  years: 2022, 2025
lastupdated: "2025-08-11"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, add-on, file

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Enabling the {{site.data.keyword.filestorage_vpc_full_notm}} cluster add-on
{: #storage-file-vpc-install}

[Virtual Private Cloud]{: tag-vpc}

{{site.data.keyword.filestorage_vpc_full_notm}} is persistent, fast, and flexible network-attached, NFS-based {{site.data.keyword.filestorage_vpc_short}} that you can add to your apps by using Kubernetes persistent volumes claims (PVCs).
{: shortdesc}


You can choose between predefined storage classes that meet the GB sizes and IOPS that meet the requirements of your workloads. To find out if {{site.data.keyword.filestorage_vpc_short}} is the correct storage option for you, see [Choosing a storage solution](/docs/openshift?topic=openshift-storage-plan). For pricing information, see [Pricing](https://cloud.ibm.com/infrastructure/provision/fileShare){: external}.


File Storage for VPC is considered to be a Financial Services Validated service only when encryption-in-transit is enabled. For more information, see [what is a Financial Services Validated service](/docs/framework-financial-services?topic=framework-financial-services-faqs-framework#financial-services-validated).
{: important}



## Considerations
{: #file-vpc-addon-considerations}

- It is recommended that your cluster and VPC are part of same resource group. If your cluster and VPC are in separate resource groups, then before you can provision file shares, you must create your own storage class and provide your VPC resource group ID. For more information, see [Creating your own storage class](/docs/openshift?topic=openshift-storage-file-vpc-apps#storage-file-vpc-custom-sc).
- New security group rules were introduced in cluster versions 4.11 and later. These rule changes mean that you must sync your security groups before you can use {{site.data.keyword.filestorage_vpc_short}}. For more information, see [Adding {{site.data.keyword.filestorage_vpc_short}} to apps](/docs/containers?topic=containers-storage-file-vpc-apps).
- New storage classes were added with version 2.0 of the add-on. You can no longer provision new file shares that use the older storage classes. Existing volumes that use the older storage classes continue to function, however you cannot expand the volumes that were created using the older classes. For more information, see the [Migrating to a new storage class](/docs/openshift?topic=openshift-storage-file-vpc-apps#storage-file-expansion-migration).
- The add-on is managed by the `addon-vpc-file-csi-driver-configmap` configmap in the `kube-system` namespace. File storage events are published in the `file-csi-driver-status` configmap in the `kube-system` namespace. For {{site.data.keyword.openshiftlong_notm}} 4.17, these two conifgmaps are retained even when the add-on is disabled. Which means, whenever the add-on is enabled again, the values set by the user in add-on configmap are reapplied.
- Encryption in-transit is enabled by default. You can optionally enable encryption in-transit when you enable the add-on.



Need to update the add-on to a newer version? See [Updating the {{site.data.keyword.filestorage_vpc_short}} add-on](/docs/openshift?topic=openshift-storage-file-vpc-managing#storage-file-vpc-update)
{: tip}

## Enabling the add-on
{: #file-vpc-addon-enable}


1. Update the Cloud CLI and the `container-service` plug-in.
    ```shell
    ibmcloud update && ibmcloud plugin update container-service
    ```
    {: pre}

1. Get a list of the add-on versions and decide which version to install for your cluster version.
    ```sh
    ibmcloud oc cluster addon versions --addon vpc-file-csi-driver
    ```
    {: pre}

    Example output
    ```sh
    Name                  Version         Supported Kubernetes Range   Supported OpenShift Range   Kubernetes Default   OpenShift Default
    vpc-file-csi-driver   2.0 (default)   >=1.30.0                     >=4.15.0                    -                    -
    ```
    {: pre}

1. Enable the add-on and follow the prompts to install any dependencies. Version 2.0 is recommended.
    ```sh
    ibmcloud oc cluster addon enable vpc-file-csi-driver --version 2.0 --cluster CLUSTER
    ```
    {: pre}

    Example output
    ```sh
    Enabling add-on vpc-file-csi-driver(2.0) for cluster devcluster2...
    The add-on might take several minutes to deploy and become ready for use.
    The ibm-storage-operator add-on version 1.0 is required to enable the vpc-file-csi-driver add-on. Enable ibm-storage-operator? [y/N]> y
    ```
    {: screen}

    Example prompt to install dependencies.
    ```sh
    The ibm-storage-operator add-on version 1.0 is required to enable the vpc-file-csi-driver add-on. Enable ibm-storage-operator? [y/N]> y
    ```
    {: pre}


1. Verify that the add-on is enabled.
    ```sh
    ibmcloud oc cluster addon ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output
    ```sh
    Name                   Version   Health State   Health Status
    ibm-storage-operator   1.0       normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)
    vpc-file-csi-driver    2.0       normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)
    ```
    {: pre}


## Next steps
{: #vpc-enable-next-steps}

Review the following links to continue setting up {{site.data.keyword.filestorage_vpc_short}}.

- [Quick start for {{site.data.keyword.filestorage_vpc_short}}](/docs/openshift?topic=openshift-storage-file-vpc-apps#vpc-add-file-dynamic)
- [Adding {{site.data.keyword.filestorage_vpc_short}} to apps](/docs/openshift?topic=openshift-storage-file-vpc-apps).
- [Managing {{site.data.keyword.filestorage_vpc_short}}](/docs/openshift?topic=openshift-storage-file-vpc-managing).
- [Creating your own storage class](/docs/openshift?topic=openshift-storage-file-vpc-apps#storage-file-vpc-custom-sc).
- [{{site.data.keyword.filestorage_vpc_short}} storage class reference](/docs/openshift?topic=openshift-storage-file-vpc-sc-ref).



## Assigning trusted profiles to file storage
{: #file-vpc-trustedprofile}

You can use trusted profiles to grant different IBM Cloud identities access to resources in your account, including your storage solutions. Trusted profiles centralize access control, eliminate the need for long-lived API keys, and allow you to scope permissions to the exact minimum required for a specific task. For more information, see [Configuring a trusted profile for storage components](/docs/containers?topic=containers-configure-trusted-profile&interface=ui).
