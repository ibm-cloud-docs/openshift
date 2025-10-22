---

copyright: 
  years: 2022, 2025
lastupdated: "2025-10-22"


keywords: openshift, file storage, storage class reference, eni

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Storage class reference
{: #storage-file-vpc-sc-ref}

The available storage classes correspond to the predefined {{site.data.keyword.filestorage_vpc_short}} profiles. For storage classes with defined IOPs, make sure the IOPs are sufficient for the file share size you want to provision. For more information about the profiles and IOPs tiers, see [{{site.data.keyword.filestorage_vpc_short}} `dp2` profiles](/docs/vpc?topic=vpc-file-storage-profiles&interface=ui#dp2-profile).

- All file shares are provisioned with zonal availability except `regional` classes which have regional availability.
- All classes are elastic network interface (ENI) enabled.
- All classes support cross-zone mounting.

| Name | Description |
| --- | --- |
| ibmc-vpc-file-1000-iops | 1000 IOPs and `Immediate` binding. |
| ibmc-vpc-file-3000-iops | 3000 IOPs and `Immediate` binding. |
| ibmc-vpc-file-500-iops | 500 IOPs `Immediate` binding |
| ibmc-vpc-file-eit | 1000 IOPs, `Immediate` binding., as well as and ElasticNetworkInterface(ENI) and EncryptionInTransit(EIT) enabled. |
| ibmc-vpc-file-metro-1000-iops | 1000 IOPs and `WaitForFirstConsumer` binding. |
| ibmc-vpc-file-metro-3000-iops | 3000 IOPs and `WaitForFirstConsumer` binding. |
| ibmc-vpc-file-metro-500-iops | 500 IOPs `WaitForFirstConsumer` binding. |
| ibmc-vpc-file-metro-retain-1000-iops | 1000 IOPs, `WaitForFirstConsumer` binding, and reclaim policy set to `Retain`. |
| ibmc-vpc-file-metro-retain-3000-iops | 3000 IOPs, `WaitForFirstConsumer` binding, and reclaim policy set to `Retain`. |
| ibmc-vpc-file-metro-retain-500-iops | 500 IOPs, `WaitForFirstConsumer` binding, and reclaim policy set to `Retain`. |
| ibmc-vpc-file-min-iops | Minimum IOPs based on file share size, `Immediate` binding. For more information, see [{{site.data.keyword.filestorage_vpc_short}} profiles](/docs/vpc?topic=vpc-file-storage-profiles&interface=ui#dp2-profile). |
| ibmc-vpc-file-retain-1000-iops | 3000 IOPs and `Retain` reclaim policy. |
| ibmc-vpc-file-retain-3000-iops | 1000 IOPs and `Retain` reclaim policy. |
| ibmc-vpc-file-retain-500-iops | 500 IOPs and `Retain` reclaim policy. |
| ibmc-vpc-file-regional | Regional availability, `Delete` reclaim policy, and `Immediate` binding |
| ibmc-vpc-file-regional-max-bandwidth | Regional availability, `Delete` reclaim policy, and `Immediate` binding |
| ibmc-vpc-file-regional-max-bandwidth-sds | Regional availability, `Delete` reclaim policy, and `WaitForFirstConsumer` biding |
{: caption="File Storage for VPC storage classes" caption-side="bottom"}

For more information about each of the classes view the details from the web console or run the following command.

```sh
oc get sc CLASS
```
{: pre}
