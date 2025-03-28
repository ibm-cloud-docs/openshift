---

copyright: 
  years: 2014, 2025
lastupdated: "2025-03-28"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, node scaling, ca, autoscaler

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Classic flavors
{: #classic-flavors}

Review the classic worker node flavors by metro.







## Amsterdam (`ams`)
{: #amsterdam-ams}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| mb4c.20x192 | Bare Metal | 20, 192GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | Bare Metal | 20, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | Bare Metal | 32, 768GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | Bare Metal | 48, 1536GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.4x32 | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 2000GB HDD | N/A|
| mb4c.4x32.1.9tb.ssd | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | Bare Metal GPUs | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | Bare Metal GPUs | 48, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Amsterdam." caption-side="bottom"}
{: #ams-physical-table}
{: tab-title="physical"}
{: tab-group="ams-tables"}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| b3c.16x64 | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | Balanced | 32, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | Balanced | 4, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | Balanced | 56, 242GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | Balanced | 8, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x16 | Compute | 16, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | Compute | 16, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | Compute | 32, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | Compute | 32, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.16x128 | Memory | 16, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | Memory | 30, 240GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | Memory | 4, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | Memory | 8, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="VSI flavors in Amsterdam." caption-side="bottom"}
{: #ams-virtual-table}
{: tab-title="virtual"}
{: tab-group="ams-tables"}





## Chennai (`che`)
{: #chennai-che}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| mb4c.20x192 | Bare Metal | 20, 192GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | Bare Metal | 20, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | Bare Metal | 32, 768GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | Bare Metal | 48, 1536GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.4x32 | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 2000GB HDD | N/A|
| mb4c.4x32.1.9tb.ssd | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | Bare Metal GPUs | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | Bare Metal GPUs | 48, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Chennai." caption-side="bottom"}
{: #che-physical-table}
{: tab-title="physical"}
{: tab-group="che-tables"}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| b3c.16x64 | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | Balanced | 32, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | Balanced | 4, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | Balanced | 56, 242GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | Balanced | 8, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x16 | Compute | 16, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | Compute | 16, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | Compute | 32, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | Compute | 32, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.16x128 | Memory | 16, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | Memory | 30, 240GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | Memory | 4, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | Memory | 8, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="VSI flavors in Chennai." caption-side="bottom"}
{: #che-virtual-table}
{: tab-title="virtual"}
{: tab-group="che-tables"}





## Dallas (`dal`)
{: #dallas-dal}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| mb4c.20x192 | Bare Metal | 20, 192GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | Bare Metal | 20, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | Bare Metal | 32, 768GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | Bare Metal | 48, 1536GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.4x32 | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 2000GB HDD | N/A|
| mb4c.4x32.1.9tb.ssd | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | Bare Metal GPUs | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | Bare Metal GPUs | 48, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Dallas." caption-side="bottom"}
{: #dal-physical-table}
{: tab-title="physical"}
{: tab-group="dal-tables"}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| b3c.16x64 | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | Balanced | 32, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | Balanced | 4, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | Balanced | 56, 242GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | Balanced | 8, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x16 | Compute | 16, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | Compute | 16, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | Compute | 32, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | Compute | 32, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.16x128 | Memory | 16, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | Memory | 30, 240GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.48x384 | Memory | 48, 384GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | Memory | 4, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.56x448 | Memory | 56, 448GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.64x512 | Memory | 64, 512GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | Memory | 8, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="VSI flavors in Dallas." caption-side="bottom"}
{: #dal-virtual-table}
{: tab-title="virtual"}
{: tab-group="dal-tables"}





## Frankfurt (`fra`)
{: #frankfurt-fra}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| mb4c.20x192 | Bare Metal | 20, 192GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | Bare Metal | 20, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | Bare Metal | 32, 768GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | Bare Metal | 48, 1536GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.4x32 | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 2000GB HDD | N/A|
| mb4c.4x32.1.9tb.ssd | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | Bare Metal GPUs | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | Bare Metal GPUs | 48, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Frankfurt." caption-side="bottom"}
{: #fra-physical-table}
{: tab-title="physical"}
{: tab-group="fra-tables"}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| b3c.16x64 | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | Balanced | 32, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | Balanced | 4, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | Balanced | 56, 242GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | Balanced | 8, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x16 | Compute | 16, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | Compute | 16, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | Compute | 32, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | Compute | 32, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.16x128 | Memory | 16, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | Memory | 30, 240GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | Memory | 4, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | Memory | 8, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="VSI flavors in Frankfurt." caption-side="bottom"}
{: #fra-virtual-table}
{: tab-title="virtual"}
{: tab-group="fra-tables"}





## London (`lon`)
{: #london-lon}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| mb4c.20x192 | Bare Metal | 20, 192GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | Bare Metal | 20, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | Bare Metal | 32, 768GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | Bare Metal | 48, 1536GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.4x32 | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 2000GB HDD | N/A|
| mb4c.4x32.1.9tb.ssd | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | Bare Metal GPUs | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | Bare Metal GPUs | 48, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in London." caption-side="bottom"}
{: #lon-physical-table}
{: tab-title="physical"}
{: tab-group="lon-tables"}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| b3c.16x64 | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | Balanced | 32, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | Balanced | 4, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | Balanced | 56, 242GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | Balanced | 8, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x16 | Compute | 16, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | Compute | 16, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | Compute | 32, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | Compute | 32, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.16x128 | Memory | 16, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | Memory | 30, 240GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | Memory | 4, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | Memory | 8, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="VSI flavors in London." caption-side="bottom"}
{: #lon-virtual-table}
{: tab-title="virtual"}
{: tab-group="lon-tables"}





## Milan (`mil`)
{: #milan-mil}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| mb4c.20x192 | Bare Metal | 20, 192GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | Bare Metal | 20, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | Bare Metal | 32, 768GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | Bare Metal | 48, 1536GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.4x32 | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 2000GB HDD | N/A|
| mb4c.4x32.1.9tb.ssd | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | Bare Metal GPUs | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | Bare Metal GPUs | 48, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Milan." caption-side="bottom"}
{: #mil-physical-table}
{: tab-title="physical"}
{: tab-group="mil-tables"}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| b3c.16x64 | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | Balanced | 32, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | Balanced | 4, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | Balanced | 56, 242GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | Balanced | 8, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x16 | Compute | 16, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | Compute | 16, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | Compute | 32, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | Compute | 32, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | Memory | 4, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="VSI flavors in Milan." caption-side="bottom"}
{: #mil-virtual-table}
{: tab-title="virtual"}
{: tab-group="mil-tables"}





## Montreal (`mon`)
{: #montreal-mon}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| mb4c.20x192 | Bare Metal | 20, 192GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | Bare Metal | 20, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | Bare Metal | 32, 768GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | Bare Metal | 48, 1536GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.4x32 | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 2000GB HDD | N/A|
| mb4c.4x32.1.9tb.ssd | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | Bare Metal GPUs | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | Bare Metal GPUs | 48, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Montreal." caption-side="bottom"}
{: #mon-physical-table}
{: tab-title="physical"}
{: tab-group="mon-tables"}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| b3c.16x64 | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | Balanced | 32, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | Balanced | 4, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | Balanced | 56, 242GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | Balanced | 8, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x16 | Compute | 16, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | Compute | 16, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | Compute | 32, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | Compute | 32, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.16x128 | Memory | 16, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | Memory | 30, 240GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | Memory | 4, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | Memory | 8, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="VSI flavors in Montreal." caption-side="bottom"}
{: #mon-virtual-table}
{: tab-title="virtual"}
{: tab-group="mon-tables"}





## Osaka (`osa`)
{: #osaka-osa}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| mb4c.20x192 | Bare Metal | 20, 192GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | Bare Metal | 20, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | Bare Metal | 32, 768GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | Bare Metal | 48, 1536GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.4x32 | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 2000GB HDD | N/A|
| mb4c.4x32.1.9tb.ssd | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | Bare Metal GPUs | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | Bare Metal GPUs | 48, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Osaka." caption-side="bottom"}
{: #osa-physical-table}
{: tab-title="physical"}
{: tab-group="osa-tables"}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| b3c.16x64 | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | Balanced | 32, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | Balanced | 4, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | Balanced | 56, 242GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | Balanced | 8, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x16 | Compute | 16, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | Compute | 16, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | Compute | 32, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | Compute | 32, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.16x128 | Memory | 16, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | Memory | 30, 240GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.48x384 | Memory | 48, 384GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | Memory | 4, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.56x448 | Memory | 56, 448GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.64x512 | Memory | 64, 512GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | Memory | 8, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="VSI flavors in Osaka." caption-side="bottom"}
{: #osa-virtual-table}
{: tab-title="virtual"}
{: tab-group="osa-tables"}





## Paris (`par`)
{: #paris-par}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| mb4c.20x192 | Bare Metal | 20, 192GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | Bare Metal | 20, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | Bare Metal | 32, 768GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | Bare Metal | 48, 1536GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.4x32 | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 2000GB HDD | N/A|
| mb4c.4x32.1.9tb.ssd | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | Bare Metal GPUs | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | Bare Metal GPUs | 48, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Paris." caption-side="bottom"}
{: #par-physical-table}
{: tab-title="physical"}
{: tab-group="par-tables"}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| b3c.16x64 | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | Balanced | 32, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | Balanced | 4, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | Balanced | 56, 242GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | Balanced | 8, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x16 | Compute | 16, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | Compute | 16, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | Compute | 32, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | Compute | 32, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.16x128 | Memory | 16, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | Memory | 30, 240GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | Memory | 4, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | Memory | 8, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="VSI flavors in Paris." caption-side="bottom"}
{: #par-virtual-table}
{: tab-title="virtual"}
{: tab-group="par-tables"}





## Sao Paulo (`sao`)
{: #sao-paulo-sao}




| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| b3c.16x64 | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | Balanced | 32, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | Balanced | 4, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | Balanced | 56, 242GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | Balanced | 8, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | Memory | 4, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="VSI flavors in Sao Paulo." caption-side="bottom"}
{: #sao-virtual-table}
{: tab-title="virtual"}
{: tab-group="sao-tables"}





## San Jose (`sjc`)
{: #san-jose-sjc}




| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| b3c.16x64 | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | Balanced | 32, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | Balanced | 4, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | Balanced | 56, 242GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | Balanced | 8, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x16 | Compute | 16, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | Compute | 16, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | Compute | 32, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | Compute | 32, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | Memory | 4, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="VSI flavors in San Jose." caption-side="bottom"}
{: #sjc-virtual-table}
{: tab-title="virtual"}
{: tab-group="sjc-tables"}





## Singapore (`sng`)
{: #singapore-sng}




| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| b3c.16x64 | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 300GB SSD | N/A|
| b3c.4x16 | Balanced | 4, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | Balanced | 8, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x16 | Compute | 16, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | Compute | 16, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.16x128 | Memory | 16, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | Memory | 30, 240GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | Memory | 4, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | Memory | 8, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="VSI flavors in Singapore." caption-side="bottom"}
{: #sng-virtual-table}
{: tab-title="virtual"}
{: tab-group="sng-tables"}





## Sydney (`syd`)
{: #sydney-syd}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| mb4c.20x192 | Bare Metal | 20, 192GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | Bare Metal | 20, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | Bare Metal | 32, 768GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | Bare Metal | 48, 1536GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.4x32 | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 2000GB HDD | N/A|
| mb4c.4x32.1.9tb.ssd | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | Bare Metal GPUs | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | Bare Metal GPUs | 48, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Sydney." caption-side="bottom"}
{: #syd-physical-table}
{: tab-title="physical"}
{: tab-group="syd-tables"}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| b3c.16x64 | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | Balanced | 32, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | Balanced | 4, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | Balanced | 56, 242GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | Balanced | 8, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x16 | Compute | 16, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | Compute | 16, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | Compute | 32, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | Compute | 32, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.16x128 | Memory | 16, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | Memory | 30, 240GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | Memory | 4, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | Memory | 8, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="VSI flavors in Sydney." caption-side="bottom"}
{: #syd-virtual-table}
{: tab-title="virtual"}
{: tab-group="syd-tables"}





## Tokyo (`tok`)
{: #tokyo-tok}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| mb4c.20x192 | Bare Metal | 20, 192GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | Bare Metal | 20, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | Bare Metal | 32, 768GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | Bare Metal | 48, 1536GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.4x32 | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 2000GB HDD | N/A|
| mb4c.4x32.1.9tb.ssd | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | Bare Metal GPUs | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | Bare Metal GPUs | 48, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Tokyo." caption-side="bottom"}
{: #tok-physical-table}
{: tab-title="physical"}
{: tab-group="tok-tables"}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| b3c.16x64 | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | Balanced | 32, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | Balanced | 4, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | Balanced | 56, 242GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | Balanced | 8, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x16 | Compute | 16, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | Compute | 16, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | Compute | 32, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | Compute | 32, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.16x128 | Memory | 16, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | Memory | 30, 240GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | Memory | 4, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | Memory | 8, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="VSI flavors in Tokyo." caption-side="bottom"}
{: #tok-virtual-table}
{: tab-title="virtual"}
{: tab-group="tok-tables"}





## Toronto (`tor`)
{: #toronto-tor}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| mb4c.20x192 | Bare Metal | 20, 192GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | Bare Metal | 20, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | Bare Metal | 32, 768GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | Bare Metal | 48, 1536GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.4x32 | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 2000GB HDD | N/A|
| mb4c.4x32.1.9tb.ssd | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | Bare Metal GPUs | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | Bare Metal GPUs | 48, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Toronto." caption-side="bottom"}
{: #tor-physical-table}
{: tab-title="physical"}
{: tab-group="tor-tables"}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| b3c.16x64 | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | Balanced | 32, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | Balanced | 4, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | Balanced | 56, 242GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | Balanced | 8, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x16 | Compute | 16, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | Compute | 16, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | Compute | 32, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | Compute | 32, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.16x128 | Memory | 16, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | Memory | 30, 240GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | Memory | 4, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | Memory | 8, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="VSI flavors in Toronto." caption-side="bottom"}
{: #tor-virtual-table}
{: tab-title="virtual"}
{: tab-group="tor-tables"}





## Washington DC (`wdc`)
{: #washington-dc-wdc}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| mb4c.20x192 | Bare Metal | 20, 192GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | Bare Metal | 20, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | Bare Metal | 20, 64GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | Bare Metal | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | Bare Metal | 32, 768GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | Bare Metal | 48, 1536GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| mb4c.4x32 | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 2000GB HDD | N/A|
| mb4c.4x32.1.9tb.ssd | Bare Metal | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | Bare Metal Edge | 4, 32GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | Bare Metal GPUs | 32, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | Bare Metal GPUs | 48, 384GB, 10000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Washington DC." caption-side="bottom"}
{: #wdc-physical-table}
{: tab-title="physical"}
{: tab-group="wdc-tables"}



| Name | Family | Cores, Memory, and Network speed | OS | Primary storage | Secondary storage | GPUs |
| ---- | ---- | -------------------------------- | ---- | --------------- | ----------------- | -- |
| b3c.16x64 | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | Balanced | 16, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | Balanced | 32, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | Balanced | 4, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | Balanced | 56, 242GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | Balanced | 8, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x16 | Compute | 16, 16GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | Compute | 16, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | Compute | 32, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | Compute | 32, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.16x128 | Memory | 16, 128GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | Memory | 30, 240GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | Memory | 4, 32GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | Memory | 8, 64GB, 1000Mbps |  REDHAT_7_64, REDHAT_8_64, RHEL_9_64| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="VSI flavors in Washington DC." caption-side="bottom"}
{: #wdc-virtual-table}
{: tab-title="virtual"}
{: tab-group="wdc-tables"}
