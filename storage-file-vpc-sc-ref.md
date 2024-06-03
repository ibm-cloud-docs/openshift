---

copyright: 
  years: 2022, 2024
lastupdated: "2024-06-03"


keywords: openshift, file storage, storage class reference, eni

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Storage class reference
{: #storage-file-vpc-sc-ref}

The available storage classes correspond to the predefined {{site.data.keyword.filestorage_vpc_short}} profiles. For more information about the profiles and IOPs tiers, see [{{site.data.keyword.filestorage_vpc_short}} profiles](/docs/vpc?topic=vpc-file-storage-profiles).

By default, all {{site.data.keyword.filestorage_vpc_short}} devices are endurance storage solid-state drives that are billed hourly. For more information about pricing, see [Pricing information](https://cloud.ibm.com/cloud-storage/file/order){: external}.


| Characteristics | Setting |
|:-----------------|:-----------------|
| Name | `ibmc-vpc-file-dp2` |
| IOPS per gigabyte | 5 |
| Size range in gigabytes | 20-12000 Gi |
| `gid` | `0` |
| `encrypted` | `false` |
| `profile` | `dp2` |
| `iops` | `100` |
| `isENIEnabled` | `true` |
| `uid` | `0` |
| `billingType` | `hourly` |
| `reclaimPolicy` | `Delete` |
| `allowVolumeExpansion` | `true` |
| `volumeBindingMode` | `Immediate` |
{: class="simple-tab-table"}
{: caption="ibmc-vpc-file-dp2" caption-side="bottom"}
{: #simpletabtable1-file-vpc-sc-ref}
{: tab-title="dp2"}
{: tab-group="Class"}

  

| Characteristics | Setting|
|:-----------------|:-----------------|
| Name | `ibmc-vpc-file-retain-dp2` |
| IOPS per gigabyte | 5 |
| Size range in gigabytes | 20-12000 Gi |
| `gid` | `0` |
| `encrypted` | `false` |
| `profile` | `dp2` |
| `iops` | `100` |
| `isENIEnabled` | `true` |
| `uid` | `0` |
| `billingType` | `hourly` |
| `reclaimPolicy` | `Retain` |
| `allowVolumeExpansion` | `true` |
| `volumeBindingMode` | `Immediate` |
{: class="simple-tab-table"}
{: caption="ibmc-vpc-file-retain-dp2" caption-side="bottom"}
{: #simpletabtable2-file-vpc-sc-ref}
{: tab-title="dp2 retain"}
{: tab-group="Class"}

| Characteristics | Setting|
|:-----------------|:-----------------|
| Name | `ibmc-vpc-file-metro-dp2` |
| IOPS per gigabyte | 10|
| Size range in gigabytes | 20-4000 Gi|
| `gid` | `0` |
| `encrypted` | `false` |
| `profile` | `dp2` |
| `iops` | `100` |
| `isENIEnabled` | `true` |
| `uid` | `0` |
| `billingType` | `hourly` |
| `reclaimPolicy` | `Delete` |
| `allowVolumeExpansion` | `true` |
| `volumeBindingMode` | `WaitForFirstConsumer` |
{: class="simple-tab-table"}
{: caption="ibmc-vpc-file-metro-dp2 " caption-side="bottom"}
{: #simpletabtable3-file-vpc-sc-ref}
{: tab-title="dp2 metro"}
{: tab-group="Class"}

| Characteristics | Setting|
|:-----------------|:-----------------|
| Name | `ibmc-vpc-file-metro-retain-dp2` |
| IOPS per gigabyte | 10|
| Size range in gigabytes | 20-4000 Gi|
| `gid` | `0` |
| `encrypted` | `false` |
| `profile` | `dp2` |
| `iops` | `100` |
| `isENIEnabled` | `true` |
| `uid` | `0` |
| `billingType` | `hourly` |
| `reclaimPolicy` | `Retain` |
| `allowVolumeExpansion` | `true` |
| `volumeBindingMode` | `Immediate` |
{: class="simple-tab-table"}
{: caption="ibmc-vpc-file-metro-retain-dp2" caption-side="bottom"}
{: #simpletabtable4-file-vpc-sc-ref}
{: tab-title="dp2 metro retain"}
{: tab-group="Class"}

