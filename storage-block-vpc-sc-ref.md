---

copyright: 
  years: 2024, 2024
lastupdated: "2024-09-23"


keywords: openshift, block storage, deploy apps, storage class reference

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# {{site.data.keyword.block_storage_is_short}} storage class reference
{: #storage-block-vpc-sc-ref}

[Virtual Private Cloud]{: tag-vpc}

Review the following storage class information for {{site.data.keyword.block_storage_is_short}} in {{site.data.keyword.openshiftlong_notm}} clusters.
{: shortdesc}

All storage classes use hourly billing. For more information about pricing, see [Pricing information](https://cloud.ibm.com/infrastructure/provision/vs){: external} and the [corresponding {{site.data.keyword.block_storage_is_short}} tiers](/docs/vpc?topic=vpc-block-storage-profiles#tiers).


| Name | File system | Volume binding mode | Reclaim policy |
| --- | --- | --- | --- |
| `ibmc-vpc-block-10iops-tier` | `ext4` | Immediate | Delete |
| `ibmc-vpc-block-retain-10iops-tier` | `ext4` | Immediate | Retain |
| `ibmc-vpc-block-metro-10iops-tier` | `ext4` | WaitForFirstConsumer | Delete |
| `ibmc-vpc-block-metro-retain-10iops-tier` | `ext4` | WaitForFirstConsumer | Retain |
| `ibmc-vpcblock-odf-10iops` | `ext4` | WaitForFirstConsumer | Delete |
| `ibmc-vpcblock-odf-ret-10iops` | `ext4` | WaitForFirstConsumer | Retain |
| `ibmc-vpc-block-5iops-tier` | `ext4` | Immediate | Delete | 
| `ibmc-vpc-block-retain-5iops-tier` | `ext4` | Immediate | Retain |
| `ibmc-vpc-block-metro-5iops-tier` | `ext4` | WaitforFirstConsumer | Delete | 
| `ibmc-vpc-block-metro-retain-5iops-tier` | `ext4` | WaitForFirstConsumer | Retain |
| `ibmc-vpcblock-odf-5iops` | `ext4` | WaitForFirstConsumer | Delete | 
| `ibmc-vpcblock-odf-ret-5iops created` | `ext4` | WaitForFirstConsumer Retain |
| `ibmc-vpc-block-custom` | `ext4` | Immediate | Delete |
| `ibmc-vpc-block-retain-custom` | `ext4` | Immediate | Retain |
| `ibmc-vpc-block-metro-custom` | `ext4` | WaitforFirstConsumer | Delete |
| `ibmc-vpc-block-metro-retain-custom` | `ext4` | WaitForFirstConsumer | Retain |
| `ibmc-vpcblock-odf-custom` | `ext4` | WaitForFirstConsumer | Delete | 
| `ibmc-vpcblock-odf-ret-custom` | `ext4` | WaitForFirstConsumer | Retain |
| `ibmc-vpc-block-general-purpose` | `ext4` | Immediate | Delete | 
| `ibmc-vpc-block-retain-general-purpose` | `ext4` | Immediate | Retain | 
| `ibmc-vpc-block-metro-general-purpose` | `ext4` | WaitforFirstConsumer | Delete | 
| `ibmc-vpc-block-metro-retain-general-purpose` | `ext4` | WaitforFirstConsumer | Retain | 
| `ibmc-vpcblock-odf-ret-general` | `ext4` | WaitforFirstConsumer | Retain | 
| `ibmc-vpcblock-odf-general` | `ext4` | WaitforFirstConsumer | Delete |
{: caption="Table 1. VPC Block storage class reference" caption-side="bottom"}
