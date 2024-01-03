---

copyright: 
  years: 2022, 2024
lastupdated: "2024-01-03"


keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}




# Storage class reference
{: #storage-file-vpc-sc-ref}

The available storage classes correspond to the predefined {{site.data.keyword.filestorage_vpc_short}} profiles. For more information about the profiles and IOPs tiers, see [{{site.data.keyword.filestorage_vpc_short}} profiles](/docs/vpc?topic=vpc-file-storage-profiles).

By default, all {{site.data.keyword.filestorage_vpc_short}} devices are provisioned with an hourly billing type and endurance storage.
If you choose a monthly billing type, when you remove the persistent storage, you still pay the monthly charge for it, even if you used it only for a short amount of time. If you want to keep your data, then choose a `retain` storage class. When you delete the PVC, only the PVC is deleted. The PV, the physical storage device in your IBM Cloud infrastructure account, and your data still exist. To reclaim the storage and use it in your cluster again, you must remove the PV and follow the steps for [using existing {{site.data.keyword.filestorage_vpc_short}}](/docs/openshift?topic=openshift-storage-file-vpc-apps). If you want the PV, the data, and your physical {{site.data.keyword.filestorage_vpc_short}} device to be deleted when you delete the PVC, choose a storage class without `retain`
{: note}


| Characteristics | Setting|
|:-----------------|:-----------------|
| IOPS per gigabyte | 5 |
| Size range in gigabytes | 20-12000 Gi |
| Hard disk | SSD|
| Reclaim policy | Delete |
| Volume binding mode | Immediate |
| Billing | Hourly|
| Pricing | [Pricing information](https://cloud.ibm.com/vpc-ext/provision/vs){: external} |
{: class="simple-tab-table"}
{: caption="ibmc-vpc-file-dp2" caption-side="bottom"}
{: #simpletabtable1-file-vpc-sc-ref}
{: tab-title="`ibmc-vpc-file-dp2`"}
{: tab-group="Class"}

| Characteristics | Setting|
|:-----------------|:-----------------|
| IOPS per gigabyte | 5 |
| Size range in gigabytes | 20-12000 Gi |
| Hard disk | SSD|
| Reclaim policy | Retain |
| Volume binding mode | Immediate |
| Billing | Hourly|
| Pricing | [Pricing information](https://cloud.ibm.com/vpc-ext/provision/vs){: external} |
{: class="simple-tab-table"}
{: caption="ibmc-vpc-file-retain-dp2" caption-side="bottom"}
{: #simpletabtable2-file-vpc-sc-ref}
{: tab-title="`ibmc-vpc-file-retain-dp2`"}
{: tab-group="Class"}

| Characteristics | Setting|
|:-----------------|:-----------------|
| IOPS per gigabyte | 10|
| Size range in gigabytes | 20-4000 Gi|
| Hard disk | SSD |
| Reclaim policy | Delete |
| Volume binding mode | WaitForFirstConsumer |
| Billing | Hourly|
| Pricing | [Pricing information](https://cloud.ibm.com/cloud-storage/file/order){: external}|
{: class="simple-tab-table"}
{: caption="ibmc-vpc-file-metro-dp2 " caption-side="bottom"}
{: #simpletabtable3-file-vpc-sc-ref}
{: tab-title="`ibmc-vpc-file-metro-dp2`"}
{: tab-group="Class"}

| Characteristics | Setting|
|:-----------------|:-----------------|
| IOPS per gigabyte | 10|
| Size range in gigabytes | 20-4000 Gi|
| Hard disk | SSD |
| Reclaim policy | Retain |
| Volume binding mode | WaitForFirstConsumer |
| Billing | Hourly|
| Pricing | [Pricing information](https://cloud.ibm.com/cloud-storage/file/order){: external}|
{: class="simple-tab-table"}
{: caption="ibmc-vpc-file-metro-retain-dp2 " caption-side="bottom"}
{: #simpletabtable4-file-vpc-sc-ref}
{: tab-title="`ibmc-vpc-file-metro-retain-dp2`"}
{: tab-group="Class"}

