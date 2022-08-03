---

copyright: 
  years: 2022, 2022
lastupdated: "2022-08-03"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Storage class reference
{: #storage-file-vpc-sc-ref}

The available storage classes correspond to the predefined {{site.data.keyword.filestorage_vpc_short}} profiles. For more information about the profiles and IOPs tiers, see [{{site.data.keyword.filestorage_vpc_short}} profiles](/docs/vpc?topic=vpc-file-storage-profiles).

By default, all {{site.data.keyword.filestorage_short}} devices are provisioned with an hourly billing type and endurance storage.
If you choose a monthly billing type, when you remove the persistent storage, you still pay the monthly charge for it, even if you used it only for a short amount of time. If you want to keep your data, then choose a `retain` storage class. When you delete the PVC, only the PVC is deleted. The PV, the physical storage device in your IBM Cloud infrastructure account, and your data still exist. To reclaim the storage and use it in your cluster again, you must remove the PV and follow the steps for [using existing {{site.data.keyword.filestorage_short}}](#vpc_add_file). If you want the PV, the data, and your physical {{site.data.keyword.filestorage_short}} device to be deleted when you delete the PVC, choose a storage class without `retain`
{: note}


Storage classes that have `retain` in the title have a reclaim policy of **Retain**. Example: `ibmc-file-retain-bronze`. Storage classes that don't have `retain` in the title have a reclaim policy of **Delete**. Example: `ibmc-file-bronze`.
{: tip}

| Characteristics | Setting|
|:-----------------|:-----------------|
| Name | `ibmc-vpc-file-3iops-tier`  \n `ibmc-vpc-file-retain-3iops-tier ` |
| Type | Endurance storage|
| File system | NFS |
| IOPS per gigabyte | 3 |
| Size range in gigabytes | 20-12000 Gi|
| Hard disk | SSD|
| Reclaim policy | `ibmc-vpc-file-3iops-tier`: Delete  \n `ibmc-vpc-file-retain-3iops-tier`: Retain |

| Billing | Hourly|
| Pricing | [Pricing information](https://www.ibm.com/cloud/file-storage/pricing){: external}|
{: class="simple-tab-table"}
{: caption="3 IOPS" caption-side="top"}
{: #simpletabtable1}
{: tab-title="3 IOPS"}
{: tab-group="Class"}

| Characteristics | Setting|
|:-----------------|:-----------------|
| Name | `ibmc-vpc-file-5iops-tier`  \n `ibmc-vpc-file-retain-5iops-tier` |
| Type | Endurance storage |
| File system | NFS |
| IOPS per gigabyte | 5 |
| Size range in gigabytes | 20-12000 Gi |
| Hard disk | SSD|
| Reclaim policy | `ibmc-vpc-file-5iops-tier`: Delete  \n `ibmc-vpc-file-retain-5iops-tier`: Retain |

| Billing | Hourly|
| Pricing | [Pricing information](https://www.ibm.com/cloud/vpc/pricing){: external} |
{: class="simple-tab-table"}
{: caption="5 IOPS" caption-side="top"}
{: #simpletabtable2}
{: tab-title="5 IOPS"}
{: tab-group="Class"}

| Characteristics | Setting|
|:-----------------|:-----------------|
| Name | `ibmc-vpc-file-10iops-tier`  \n `ibmc-vpc-file-retain-10iops-tier`  \n |
| Type | Endurance storage|
| File system | NFS|
| IOPS per gigabyte | 10|
| Size range in gigabytes | 20-4000 Gi|
| Hard disk | SSD|
| Reclaim policy | `ibmc-vpc-file-10iops-tier`: Delete  \n `ibmc-vpc-file-retain-10iops-tier`: Retain   \n |

| Billing | Hourly|
| Pricing | [Pricing information](https://www.ibm.com/cloud/file-storage/pricing){: external}|
{: class="simple-tab-table"}
{: caption="10 IOPS Tier" caption-side="top"}
{: #simpletabtable3}
{: tab-title="10 IOPS"}
{: tab-group="Class"}

