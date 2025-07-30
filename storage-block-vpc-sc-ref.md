---

copyright: 
  years: 2024, 2025
lastupdated: "2025-07-30"


keywords: openshift, block storage, deploy apps, storage class reference

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# {{site.data.keyword.block_storage_is_short}} storage class reference
{: #storage-block-vpc-sc-ref}

[Virtual Private Cloud]{: tag-vpc}

Review the following storage class information for {{site.data.keyword.block_storage_is_short}} in {{site.data.keyword.openshiftlong_notm}} clusters. For more information about {{site.data.keyword.block_storage_is_short}}, see [About {{site.data.keyword.block_storage_is_short}}](/docs/vpc?topic=vpc-block-storage-about).
{: shortdesc}

All storage classes use hourly billing. For more information about pricing, see [Pricing information](https://cloud.ibm.com/infrastructure/provision/vs){: external} and the [corresponding {{site.data.keyword.block_storage_is_short}} tiers](/docs/vpc?topic=vpc-block-storage-profiles#tiers).

The SSD defined performance (`sdp`) profile is a second-generation volume profile that offers more flexibility than the previous custom profile when it comes to specifying capacity and performance. By using the `sdp` profile, you can specify the capacity, and the maximum throughput limit. 
- Volume size can range from 1 - 32,000 GB.
- Volume performance can range of 3000 - 64,000 IOPS.
- Throughput range is 125-1024 MBps (1000-8192 Mbps).

For more information, see [Block Storage capacity and performance](/docs/vpc?topic=vpc-capacity-performance&interface=ui) and [SSD defined performance profile](/docs/vpc?topic=vpc-block-storage-profiles&interface=ui#defined-performance-profile).

SSD defined performance profiles (SDP) are available in Dallas, Frankfurt, London, Madrid, Osaka, Sao Paulo, Sydney, Tokyo, Toronto, and Washington, D.C. Snapshot creation for SSD defined performance profiles is available in Dallas, Frankfurt, Tokyo, and Washington, D.C.
{: note}


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
| `ibmc-vpcblock-odf-ret-5iops` | `ext4` | WaitForFirstConsumer Retain |
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
| `ibmc-vpc-block-sdp` | `ext4` | Immediate | Delete |
| `ibmc-vpc-block-sdp-max-bandwidth` |  `ext4` | Immediate | Delete | 
| `ibmc-vpc-block-sdp-max-bandwidth-sds` |`ext4` | WaitForFirstConsumer | Delete |
{: caption="VPC Block storage class reference" caption-side="bottom"}
