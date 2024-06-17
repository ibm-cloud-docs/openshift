---

copyright: 
  years: 2022, 2024
lastupdated: "2024-06-14"


keywords: openshift, file storage, storage class reference, eni

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Storage class reference
{: #storage-file-vpc-sc-ref}

The available storage classes correspond to the predefined {{site.data.keyword.filestorage_vpc_short}} profiles. For storage classes with definied IOPs, make sure the IOPs are sufficient for the file share size you want to provision. For more information about the profiles and IOPs tiers, see [{{site.data.keyword.filestorage_vpc_short}} `dp2` profiles](/docs/vpc?topic=vpc-file-storage-profiles&interface=ui#dp2-profile).

The {{site.data.keyword.filestorage_vpc_short}} cluster add-on is available in Beta. 
{: beta} 

For more information about each of the classes view the details from the web console or run the following command.

```sh
oc get sc CLASS
```
{: pre}

- All file shares are provisioned with zonal availability.
- All classes are elastic network interface (ENI) enabled.
- The `metro` classes support cross-zone mounting.



| Name | Description |
| --- | --- |
| ibmc-vpc-file-1000-iops | 1000 IOPs |
| ibmc-vpc-file-3000-iops | 3000 IOPs|
| ibmc-vpc-file-500-iops | 500 IOPs |
| ibmc-vpc-file-eit | 1000 IOPs, `Immediate ` binding, as well as and ElasticNetworkInterface(ENI) and EncryptionInTransit(EIT) enabled. |
| ibmc-vpc-file-metro-1000-iops | 1000 IOPs and `WaitForFirstConsumer` binding. |
| ibmc-vpc-file-metro-3000-iops | 3000 IOPs and `WaitForFirstConsumer` binding. |
| ibmc-vpc-file-metro-500-iops | 500 IOPs `WaitForFirstConsumer` binding. |
| ibmc-vpc-file-metro-retain-1000-iops | 1000 IOPs, `WaitForFirstConsumer` binding, and recliam policy set to `Retain`. |
| ibmc-vpc-file-metro-retain-3000-iops | 3000 IOPs, `WaitForFirstConsumer` binding, and recliam policy set to `Retain`. |
| ibmc-vpc-file-metro-retain-500-iops | 500 IOPs, `WaitForFirstConsumer` binding, and recliam policy set to `Retain`. |
| ibmc-vpc-file-min-iops | Minimum IOPs based on file share size, `Immediate` binding. For more information, see [{{site.data.keyword.filestorage_vpc_short}} profiles](/docs/vpc?topic=vpc-file-storage-profiles&interface=ui#dp2-profile). |
| ibmc-vpc-file-retain-1000-iops | 3000 IOPs, `WaitForFirstConsumer` binding. |
| ibmc-vpc-file-retain-3000-iops | 1000 IOPs, `WaitForFirstConsumer` binding. |
| ibmc-vpc-file-retain-500-iops | 500 IOPs, `WaitForFirstConsumer` binding. |
{: caption="File Storage for VPC storage classes" caption-side="bottom"}


