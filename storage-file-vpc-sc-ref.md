---

copyright: 
  years: 2022, 2024
lastupdated: "2024-06-21"


keywords: openshift, file storage, storage class reference, eni

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Storage class reference
{: #storage-file-vpc-sc-ref}

The available storage classes correspond to the predefined {{site.data.keyword.filestorage_vpc_short}} profiles. For storage classes with defined IOPs, make sure the IOPs are sufficient for the file share size you want to provision. For more information about the profiles and IOPs tiers, see [{{site.data.keyword.filestorage_vpc_short}} `dp2` profiles](/docs/vpc?topic=vpc-file-storage-profiles&interface=ui#dp2-profile).

- All file shares are provisioned with zonal availability.
- All classes are elastic network interface (ENI) enabled.
- All classes support cross-zone mounting.

The {{site.data.keyword.filestorage_vpc_short}} cluster add-on is available in Beta. 
{: beta}


New storage classes were introduced with version 2.0.0. You can no longer provision new file shares that use the older storage classes. However, existing volumes (PVC/PVs) that use the older storage classes are not impacted and continue to function. For more information, see the [storage class reference](/docs/openshift?topic=openshift-storage-file-vpc-sc-ref).
{: note}


| Name | Description |
| --- | --- |
| ibmc-vpc-file-1000-iops | 1000 IOPs and `Immediate ` binding. |
| ibmc-vpc-file-3000-iops | 3000 IOPs and `Immediate ` binding. |
| ibmc-vpc-file-500-iops | 500 IOPs `Immediate ` binding |
| ibmc-vpc-file-eit | 1000 IOPs, `Immediate ` binding., as well as and ElasticNetworkInterface(ENI) and EncryptionInTransit(EIT) enabled. |
| ibmc-vpc-file-metro-1000-iops | 1000 IOPs and `WaitForFirstConsumer` binding. |
| ibmc-vpc-file-metro-3000-iops | 3000 IOPs and `WaitForFirstConsumer` binding. |
| ibmc-vpc-file-metro-500-iops | 500 IOPs `WaitForFirstConsumer` binding. |
| ibmc-vpc-file-metro-retain-1000-iops | 1000 IOPs, `WaitForFirstConsumer` binding, and recliam policy set to `Retain`. |
| ibmc-vpc-file-metro-retain-3000-iops | 3000 IOPs, `WaitForFirstConsumer` binding, and recliam policy set to `Retain`. |
| ibmc-vpc-file-metro-retain-500-iops | 500 IOPs, `WaitForFirstConsumer` binding, and recliam policy set to `Retain`. |
| ibmc-vpc-file-min-iops | Minimum IOPs based on file share size, `Immediate` binding. For more information, see [{{site.data.keyword.filestorage_vpc_short}} profiles](/docs/vpc?topic=vpc-file-storage-profiles&interface=ui#dp2-profile). |
| ibmc-vpc-file-retain-1000-iops | 3000 IOPs and `Retain` reclaim policy. |
| ibmc-vpc-file-retain-3000-iops | 1000 IOPs and `Retain` reclaim policy. |
| ibmc-vpc-file-retain-500-iops | 500 IOPs and `Retain` reclaim policy. |
{: caption="File Storage for VPC storage classes" caption-side="bottom"}

For more information about each of the classes view the details from the web console or run the following command.

```sh
oc get sc CLASS
```
{: pre}



