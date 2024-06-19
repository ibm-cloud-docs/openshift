---

copyright: 
  years: 2022, 2024
lastupdated: "2024-06-19"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, add-on, file

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Enabling the {{site.data.keyword.filestorage_vpc_full_notm}} cluster add-on
{: #storage-file-vpc-install}

[Virtual Private Cloud]{: tag-vpc}

{{site.data.keyword.filestorage_vpc_full_notm}} is persistent, fast, and flexible network-attached, NFS-based {{site.data.keyword.filestorage_vpc_short}} that you can add to your apps by using Kubernetes persistent volumes (PVs). You can choose between predefined storage classes that meet the GB sizes and IOPS that meet the requirements of your workloads. To find out if {{site.data.keyword.filestorage_vpc_short}} is the correct storage option for you, see [Choosing a storage solution](/docs/openshift?topic=openshift-storage-plan). For pricing information, see [Pricing](https://cloud.ibm.com/vpc-ext/provision/fileShare){: external}.
{: shortdesc}

The {{site.data.keyword.filestorage_vpc_short}} cluster add-on is available in Beta. 
{: beta} 


1. Update the `container-service` CLI plug-in.
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
    vpc-file-csi-driver   1.2             >=1.24.0                     >=4.10.0                    -                    -
    vpc-file-csi-driver   2.0 (default)   >=1.30.0                     >=4.15.0                    -                    -
    ```
    {: pre}

1. Enable the add-on and follow the prompts to install any dependencies.
    ```sh
    ibmcloud oc cluster addon enable vpc-file-csi-driver --version VERSION --cluster CLUSTER
    ```
    {: pre}

    Example output.
    ```sh
    Enabling add-on vpc-file-csi-driver(1.0) for cluster devcluster2...
    The add-on might take several minutes to deploy and become ready for use.
    The ibm-storage-operator add-on version 1.0 is required to enable the vpc-file-csi-driver add-on. Enable ibm-storage-operator? [y/N]> y
    ```
    {: screen}


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
- [{{site.data.keyword.filestorage_vpc_short}} storage class reference](/docs/openshift?topic=openshift-storage-file-vpc-sc-ref).

