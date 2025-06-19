---

copyright: 
  years: 2014, 2025
lastupdated: "2025-06-19"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, node scaling, ca, autoscaler

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Classic flavors
{: #classic-flavors}

Review the classic worker node flavors by metro.

The flavors listed here might differ from what is actually available for your cluster. You can find a list of available flavors specific to your clusters by running **`ibmcloud oc flavor ls`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_flavor_ls) or review the list of flavors when creating a cluster in the console.

These conditions might impact cluster flavor availability:
- **Operating system specifications**: Some flavors have specific operating system requirements. When selecting a flavor in the console, make sure you have the correct zone and operating system selections for your needs.



## Amsterdam (`ams`)
{: #amsterdam-ams}

| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| b3c.16x64  \n(Balanced) | ams03 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb  \n(Balanced) | ams03 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 300GB SSD |
| b3c.32x128  \n(Balanced) | ams03 | 32 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.4x16  \n(Balanced) | ams03 | 4 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.56x242  \n(Balanced) | ams03 | 56 cores  \n242GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.8x32  \n(Balanced) | ams03 | 8 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x16  \n(Compute) | ams03 | 16 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x32  \n(Compute) | ams03 | 16 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x32  \n(Compute) | ams03 | 32 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x64  \n(Compute) | ams03 | 32 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.16x128  \n(Memory) | ams03 | 16 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.30x240  \n(Memory) | ams03 | 30 cores  \n240GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.4x32  \n(Memory) | ams03 | 4 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.8x64  \n(Memory) | ams03 | 8 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
{: class="simple-tab-table"}
{: caption="VSI flavors in Amsterdam." caption-side="bottom"}
{: #ams-virtual-table}
{: tab-title="Virtual"}
{: tab-group="ams-tables"}



| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| mb4c.20x192  \n(Bare Metal) | ams03 | 20 cores  \n192GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x384  \n(Bare Metal) | ams03 | 20 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64  \n(Bare Metal) | ams03 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd  \n(Bare Metal) | ams03 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd  \n(Bare Metal) | ams03 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd  \n(Bare Metal) | ams03 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd  \n(Bare Metal) | ams03 | 32 cores  \n768GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.48x1536  \n(Bare Metal) | ams03 | 48 cores  \n1536GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.4x32  \n(Bare Metal) | ams03 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 2000GB HDD |
| mb4c.4x32.1.9tb.ssd  \n(Bare Metal) | ams03 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| me4c.4x32  \n(Bare Metal Edge) | ams03 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd  \n(Bare Metal Edge) | ams03 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100  \n(Bare Metal GPUs) | ams03 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n2 P100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100  \n(Bare Metal GPUs) | ams03 | 48 cores  \n384GB memory  \n10000Mbps network speed  \n2 V100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Amsterdam." caption-side="bottom"}
{: #ams-physical-table}
{: tab-title="Physical"}
{: tab-group="ams-tables"}


## Chennai (`che`)
{: #chennai-che}

| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| b3c.16x64  \n(Balanced) | che01 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb  \n(Balanced) | che01 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 300GB SSD |
| b3c.32x128  \n(Balanced) | che01 | 32 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.4x16  \n(Balanced) | che01 | 4 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.56x242  \n(Balanced) | che01 | 56 cores  \n242GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.8x32  \n(Balanced) | che01 | 8 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x16  \n(Compute) | che01 | 16 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x32  \n(Compute) | che01 | 16 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x32  \n(Compute) | che01 | 32 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x64  \n(Compute) | che01 | 32 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.16x128  \n(Memory) | che01 | 16 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.30x240  \n(Memory) | che01 | 30 cores  \n240GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.4x32  \n(Memory) | che01 | 4 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.8x64  \n(Memory) | che01 | 8 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
{: class="simple-tab-table"}
{: caption="VSI flavors in Chennai." caption-side="bottom"}
{: #che-virtual-table}
{: tab-title="Virtual"}
{: tab-group="che-tables"}



| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| mb4c.20x192  \n(Bare Metal) | che01 | 20 cores  \n192GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x384  \n(Bare Metal) | che01 | 20 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64  \n(Bare Metal) | che01 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd  \n(Bare Metal) | che01 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd  \n(Bare Metal) | che01 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd  \n(Bare Metal) | che01 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd  \n(Bare Metal) | che01 | 32 cores  \n768GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.48x1536  \n(Bare Metal) | che01 | 48 cores  \n1536GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.4x32  \n(Bare Metal) | che01 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 2000GB HDD |
| mb4c.4x32.1.9tb.ssd  \n(Bare Metal) | che01 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| me4c.4x32  \n(Bare Metal Edge) | che01 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd  \n(Bare Metal Edge) | che01 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100  \n(Bare Metal GPUs) | che01 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n2 P100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100  \n(Bare Metal GPUs) | che01 | 48 cores  \n384GB memory  \n10000Mbps network speed  \n2 V100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Chennai." caption-side="bottom"}
{: #che-physical-table}
{: tab-title="Physical"}
{: tab-group="che-tables"}


## Dallas (`dal`)
{: #dallas-dal}

| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| b3c.16x64  \n(Balanced) | dal10  \ndal12  \ndal13 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb  \n(Balanced) | dal10  \ndal12  \ndal13 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 300GB SSD |
| b3c.32x128  \n(Balanced) | dal10  \ndal12  \ndal13 | 32 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.4x16  \n(Balanced) | dal10  \ndal12  \ndal13 | 4 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.56x242  \n(Balanced) | dal10  \ndal12  \ndal13 | 56 cores  \n242GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.8x32  \n(Balanced) | dal10  \ndal12  \ndal13 | 8 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x16  \n(Compute) | dal10  \ndal12  \ndal13 | 16 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x32  \n(Compute) | dal10  \ndal12  \ndal13 | 16 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x32  \n(Compute) | dal10  \ndal12  \ndal13 | 32 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x64  \n(Compute) | dal10  \ndal12  \ndal13 | 32 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.16x128  \n(Memory) | dal10  \ndal12  \ndal13 | 16 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.30x240  \n(Memory) | dal10  \ndal12  \ndal13 | 30 cores  \n240GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.48x384  \n(Memory) | dal10  \ndal12  \ndal13 | 48 cores  \n384GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.4x32  \n(Memory) | dal10  \ndal12  \ndal13 | 4 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.56x448  \n(Memory) | dal10  \ndal12  \ndal13 | 56 cores  \n448GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.64x512  \n(Memory) | dal10  \ndal12  \ndal13 | 64 cores  \n512GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.8x64  \n(Memory) | dal10  \ndal12  \ndal13 | 8 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
{: class="simple-tab-table"}
{: caption="VSI flavors in Dallas." caption-side="bottom"}
{: #dal-virtual-table}
{: tab-title="Virtual"}
{: tab-group="dal-tables"}



| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| mb4c.20x192  \n(Bare Metal) | dal10  \ndal12  \ndal13 | 20 cores  \n192GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x384  \n(Bare Metal) | dal10  \ndal12  \ndal13 | 20 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64  \n(Bare Metal) | dal10  \ndal12  \ndal13 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd  \n(Bare Metal) | dal10  \ndal12  \ndal13 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd  \n(Bare Metal) | dal10  \ndal12  \ndal13 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd  \n(Bare Metal) | dal10  \ndal12  \ndal13 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd  \n(Bare Metal) | dal10  \ndal12  \ndal13 | 32 cores  \n768GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.48x1536  \n(Bare Metal) | dal10  \ndal12  \ndal13 | 48 cores  \n1536GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.4x32  \n(Bare Metal) | dal10  \ndal12  \ndal13 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 2000GB HDD |
| mb4c.4x32.1.9tb.ssd  \n(Bare Metal) | dal10  \ndal12  \ndal13 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| me4c.4x32  \n(Bare Metal Edge) | dal10  \ndal12  \ndal13 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd  \n(Bare Metal Edge) | dal10  \ndal12  \ndal13 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100  \n(Bare Metal GPUs) | dal10  \ndal12  \ndal13 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n2 P100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100  \n(Bare Metal GPUs) | dal10  \ndal12  \ndal13 | 48 cores  \n384GB memory  \n10000Mbps network speed  \n2 V100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Dallas." caption-side="bottom"}
{: #dal-physical-table}
{: tab-title="Physical"}
{: tab-group="dal-tables"}


## Frankfurt (`fra`)
{: #frankfurt-fra}

| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| b3c.16x64  \n(Balanced) | fra02  \nfra04  \nfra05 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb  \n(Balanced) | fra02  \nfra04  \nfra05 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 300GB SSD |
| b3c.32x128  \n(Balanced) | fra02  \nfra04  \nfra05 | 32 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.4x16  \n(Balanced) | fra02  \nfra04  \nfra05 | 4 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.56x242  \n(Balanced) | fra02  \nfra04  \nfra05 | 56 cores  \n242GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.8x32  \n(Balanced) | fra02  \nfra04  \nfra05 | 8 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x16  \n(Compute) | fra02  \nfra04  \nfra05 | 16 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x32  \n(Compute) | fra02  \nfra04  \nfra05 | 16 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x32  \n(Compute) | fra02  \nfra04  \nfra05 | 32 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x64  \n(Compute) | fra02  \nfra04  \nfra05 | 32 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.16x128  \n(Memory) | fra02  \nfra04  \nfra05 | 16 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.30x240  \n(Memory) | fra02  \nfra04  \nfra05 | 30 cores  \n240GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.4x32  \n(Memory) | fra02  \nfra04  \nfra05 | 4 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.8x64  \n(Memory) | fra02  \nfra04  \nfra05 | 8 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
{: class="simple-tab-table"}
{: caption="VSI flavors in Frankfurt." caption-side="bottom"}
{: #fra-virtual-table}
{: tab-title="Virtual"}
{: tab-group="fra-tables"}



| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| mb4c.20x192  \n(Bare Metal) | fra02  \nfra04  \nfra05 | 20 cores  \n192GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x384  \n(Bare Metal) | fra02  \nfra04  \nfra05 | 20 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64  \n(Bare Metal) | fra02  \nfra04  \nfra05 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd  \n(Bare Metal) | fra02  \nfra04  \nfra05 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd  \n(Bare Metal) | fra02  \nfra04  \nfra05 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd  \n(Bare Metal) | fra02  \nfra04  \nfra05 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd  \n(Bare Metal) | fra02  \nfra04  \nfra05 | 32 cores  \n768GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.48x1536  \n(Bare Metal) | fra02  \nfra04  \nfra05 | 48 cores  \n1536GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.4x32  \n(Bare Metal) | fra02  \nfra04  \nfra05 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 2000GB HDD |
| mb4c.4x32.1.9tb.ssd  \n(Bare Metal) | fra02  \nfra04  \nfra05 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| me4c.4x32  \n(Bare Metal Edge) | fra02  \nfra04  \nfra05 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd  \n(Bare Metal Edge) | fra02  \nfra04  \nfra05 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100  \n(Bare Metal GPUs) | fra02  \nfra04  \nfra05 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n2 P100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100  \n(Bare Metal GPUs) | fra02  \nfra04  \nfra05 | 48 cores  \n384GB memory  \n10000Mbps network speed  \n2 V100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Frankfurt." caption-side="bottom"}
{: #fra-physical-table}
{: tab-title="Physical"}
{: tab-group="fra-tables"}


## London (`lon`)
{: #london-lon}

| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| b3c.16x64  \n(Balanced) | lon02  \nlon04  \nlon05  \nlon06 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb  \n(Balanced) | lon02  \nlon04  \nlon05  \nlon06 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 300GB SSD |
| b3c.32x128  \n(Balanced) | lon02  \nlon04  \nlon05  \nlon06 | 32 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.4x16  \n(Balanced) | lon02  \nlon04  \nlon05  \nlon06 | 4 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.56x242  \n(Balanced) | lon02  \nlon04  \nlon05  \nlon06 | 56 cores  \n242GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.8x32  \n(Balanced) | lon02  \nlon04  \nlon05  \nlon06 | 8 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x16  \n(Compute) | lon02  \nlon04  \nlon05  \nlon06 | 16 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x32  \n(Compute) | lon02  \nlon04  \nlon05  \nlon06 | 16 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x32  \n(Compute) | lon02  \nlon04  \nlon05  \nlon06 | 32 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x64  \n(Compute) | lon02  \nlon04  \nlon05  \nlon06 | 32 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.16x128  \n(Memory) | lon02  \nlon04  \nlon05  \nlon06 | 16 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.30x240  \n(Memory) | lon02  \nlon04  \nlon05  \nlon06 | 30 cores  \n240GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.4x32  \n(Memory) | lon02  \nlon04  \nlon05  \nlon06 | 4 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.8x64  \n(Memory) | lon02  \nlon04  \nlon05  \nlon06 | 8 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
{: class="simple-tab-table"}
{: caption="VSI flavors in London." caption-side="bottom"}
{: #lon-virtual-table}
{: tab-title="Virtual"}
{: tab-group="lon-tables"}



| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| mb4c.20x192  \n(Bare Metal) | lon02  \nlon04  \nlon05  \nlon06 | 20 cores  \n192GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x384  \n(Bare Metal) | lon02  \nlon04  \nlon05  \nlon06 | 20 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64  \n(Bare Metal) | lon02  \nlon04  \nlon05  \nlon06 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd  \n(Bare Metal) | lon02  \nlon04  \nlon05  \nlon06 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd  \n(Bare Metal) | lon02  \nlon04  \nlon05  \nlon06 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd  \n(Bare Metal) | lon02  \nlon04  \nlon05  \nlon06 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd  \n(Bare Metal) | lon02  \nlon04  \nlon05  \nlon06 | 32 cores  \n768GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.48x1536  \n(Bare Metal) | lon02  \nlon04  \nlon05  \nlon06 | 48 cores  \n1536GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.4x32  \n(Bare Metal) | lon02  \nlon04  \nlon05  \nlon06 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 2000GB HDD |
| mb4c.4x32.1.9tb.ssd  \n(Bare Metal) | lon02  \nlon04  \nlon05  \nlon06 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| me4c.4x32  \n(Bare Metal Edge) | lon02  \nlon04  \nlon05  \nlon06 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd  \n(Bare Metal Edge) | lon02  \nlon04  \nlon05  \nlon06 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100  \n(Bare Metal GPUs) | lon02  \nlon04  \nlon05  \nlon06 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n2 P100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100  \n(Bare Metal GPUs) | lon02  \nlon04  \nlon05  \nlon06 | 48 cores  \n384GB memory  \n10000Mbps network speed  \n2 V100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in London." caption-side="bottom"}
{: #lon-physical-table}
{: tab-title="Physical"}
{: tab-group="lon-tables"}


## Milan (`mil`)
{: #milan-mil}

| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| b3c.16x64  \n(Balanced) | mil01 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb  \n(Balanced) | mil01 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 300GB SSD |
| b3c.32x128  \n(Balanced) | mil01 | 32 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.4x16  \n(Balanced) | mil01 | 4 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.56x242  \n(Balanced) | mil01 | 56 cores  \n242GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.8x32  \n(Balanced) | mil01 | 8 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x16  \n(Compute) | mil01 | 16 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x32  \n(Compute) | mil01 | 16 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x32  \n(Compute) | mil01 | 32 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x64  \n(Compute) | mil01 | 32 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.4x32  \n(Memory) | mil01 | 4 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
{: class="simple-tab-table"}
{: caption="VSI flavors in Milan." caption-side="bottom"}
{: #mil-virtual-table}
{: tab-title="Virtual"}
{: tab-group="mil-tables"}



| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| mb4c.20x192  \n(Bare Metal) | mil01 | 20 cores  \n192GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x384  \n(Bare Metal) | mil01 | 20 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64  \n(Bare Metal) | mil01 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd  \n(Bare Metal) | mil01 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd  \n(Bare Metal) | mil01 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd  \n(Bare Metal) | mil01 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd  \n(Bare Metal) | mil01 | 32 cores  \n768GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.48x1536  \n(Bare Metal) | mil01 | 48 cores  \n1536GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.4x32  \n(Bare Metal) | mil01 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 2000GB HDD |
| mb4c.4x32.1.9tb.ssd  \n(Bare Metal) | mil01 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| me4c.4x32  \n(Bare Metal Edge) | mil01 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd  \n(Bare Metal Edge) | mil01 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100  \n(Bare Metal GPUs) | mil01 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n2 P100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100  \n(Bare Metal GPUs) | mil01 | 48 cores  \n384GB memory  \n10000Mbps network speed  \n2 V100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Milan." caption-side="bottom"}
{: #mil-physical-table}
{: tab-title="Physical"}
{: tab-group="mil-tables"}


## Montreal (`mon`)
{: #montreal-mon}

| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| b3c.16x64  \n(Balanced) | mon01 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb  \n(Balanced) | mon01 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 300GB SSD |
| b3c.32x128  \n(Balanced) | mon01 | 32 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.4x16  \n(Balanced) | mon01 | 4 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.56x242  \n(Balanced) | mon01 | 56 cores  \n242GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.8x32  \n(Balanced) | mon01 | 8 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x16  \n(Compute) | mon01 | 16 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x32  \n(Compute) | mon01 | 16 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x32  \n(Compute) | mon01 | 32 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x64  \n(Compute) | mon01 | 32 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.16x128  \n(Memory) | mon01 | 16 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.30x240  \n(Memory) | mon01 | 30 cores  \n240GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.4x32  \n(Memory) | mon01 | 4 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.8x64  \n(Memory) | mon01 | 8 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
{: class="simple-tab-table"}
{: caption="VSI flavors in Montreal." caption-side="bottom"}
{: #mon-virtual-table}
{: tab-title="Virtual"}
{: tab-group="mon-tables"}



| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| mb4c.20x192  \n(Bare Metal) | mon01 | 20 cores  \n192GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x384  \n(Bare Metal) | mon01 | 20 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64  \n(Bare Metal) | mon01 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd  \n(Bare Metal) | mon01 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd  \n(Bare Metal) | mon01 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd  \n(Bare Metal) | mon01 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd  \n(Bare Metal) | mon01 | 32 cores  \n768GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.48x1536  \n(Bare Metal) | mon01 | 48 cores  \n1536GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.4x32  \n(Bare Metal) | mon01 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 2000GB HDD |
| mb4c.4x32.1.9tb.ssd  \n(Bare Metal) | mon01 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| me4c.4x32  \n(Bare Metal Edge) | mon01 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd  \n(Bare Metal Edge) | mon01 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100  \n(Bare Metal GPUs) | mon01 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n2 P100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100  \n(Bare Metal GPUs) | mon01 | 48 cores  \n384GB memory  \n10000Mbps network speed  \n2 V100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Montreal." caption-side="bottom"}
{: #mon-physical-table}
{: tab-title="Physical"}
{: tab-group="mon-tables"}


## Osaka (`osa`)
{: #osaka-osa}

| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| b3c.16x64  \n(Balanced) | osa21  \nosa22  \nosa23 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb  \n(Balanced) | osa21  \nosa22  \nosa23 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 300GB SSD |
| b3c.32x128  \n(Balanced) | osa21  \nosa22  \nosa23 | 32 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.4x16  \n(Balanced) | osa21  \nosa22  \nosa23 | 4 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.56x242  \n(Balanced) | osa21  \nosa22  \nosa23 | 56 cores  \n242GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.8x32  \n(Balanced) | osa21  \nosa22  \nosa23 | 8 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x16  \n(Compute) | osa21  \nosa22  \nosa23 | 16 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x32  \n(Compute) | osa21  \nosa22  \nosa23 | 16 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x32  \n(Compute) | osa21  \nosa22  \nosa23 | 32 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x64  \n(Compute) | osa21  \nosa22  \nosa23 | 32 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.16x128  \n(Memory) | osa21  \nosa22  \nosa23 | 16 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.30x240  \n(Memory) | osa21  \nosa22  \nosa23 | 30 cores  \n240GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.48x384  \n(Memory) | osa21  \nosa22  \nosa23 | 48 cores  \n384GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.4x32  \n(Memory) | osa21  \nosa22  \nosa23 | 4 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.56x448  \n(Memory) | osa21  \nosa22  \nosa23 | 56 cores  \n448GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.64x512  \n(Memory) | osa21  \nosa22  \nosa23 | 64 cores  \n512GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.8x64  \n(Memory) | osa21  \nosa22  \nosa23 | 8 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
{: class="simple-tab-table"}
{: caption="VSI flavors in Osaka." caption-side="bottom"}
{: #osa-virtual-table}
{: tab-title="Virtual"}
{: tab-group="osa-tables"}



| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| mb4c.20x192  \n(Bare Metal) | osa21  \nosa22  \nosa23 | 20 cores  \n192GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x384  \n(Bare Metal) | osa21  \nosa22  \nosa23 | 20 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64  \n(Bare Metal) | osa21  \nosa22  \nosa23 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd  \n(Bare Metal) | osa21  \nosa22  \nosa23 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd  \n(Bare Metal) | osa21  \nosa22  \nosa23 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd  \n(Bare Metal) | osa21  \nosa22  \nosa23 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd  \n(Bare Metal) | osa21  \nosa22  \nosa23 | 32 cores  \n768GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.48x1536  \n(Bare Metal) | osa21  \nosa22  \nosa23 | 48 cores  \n1536GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.4x32  \n(Bare Metal) | osa21  \nosa22  \nosa23 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 2000GB HDD |
| mb4c.4x32.1.9tb.ssd  \n(Bare Metal) | osa21  \nosa22  \nosa23 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| me4c.4x32  \n(Bare Metal Edge) | osa21  \nosa22  \nosa23 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd  \n(Bare Metal Edge) | osa21  \nosa22  \nosa23 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100  \n(Bare Metal GPUs) | osa21  \nosa22  \nosa23 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n2 P100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100  \n(Bare Metal GPUs) | osa21  \nosa22  \nosa23 | 48 cores  \n384GB memory  \n10000Mbps network speed  \n2 V100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Osaka." caption-side="bottom"}
{: #osa-physical-table}
{: tab-title="Physical"}
{: tab-group="osa-tables"}



## San Jose (`sjc`)
{: #san-jose-sjc}

| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| b3c.16x64  \n(Balanced) | sjc03  \nsjc04 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb  \n(Balanced) | sjc03  \nsjc04 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 300GB SSD |
| b3c.32x128  \n(Balanced) | sjc03  \nsjc04 | 32 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.4x16  \n(Balanced) | sjc03  \nsjc04 | 4 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.56x242  \n(Balanced) | sjc03  \nsjc04 | 56 cores  \n242GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.8x32  \n(Balanced) | sjc03  \nsjc04 | 8 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x16  \n(Compute) | sjc03  \nsjc04 | 16 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x32  \n(Compute) | sjc03  \nsjc04 | 16 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x32  \n(Compute) | sjc03  \nsjc04 | 32 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x64  \n(Compute) | sjc03  \nsjc04 | 32 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.4x32  \n(Memory) | sjc03  \nsjc04 | 4 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.16x128  \n(Memory) | sjc04 | 16 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.30x240  \n(Memory) | sjc04 | 30 cores  \n240GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.8x64  \n(Memory) | sjc04 | 8 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
{: class="simple-tab-table"}
{: caption="VSI flavors in San Jose." caption-side="bottom"}
{: #sjc-virtual-table}
{: tab-title="Virtual"}
{: tab-group="sjc-tables"}



| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| mb4c.20x192  \n(Bare Metal) | sjc04 | 20 cores  \n192GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x384  \n(Bare Metal) | sjc04 | 20 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64  \n(Bare Metal) | sjc04 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd  \n(Bare Metal) | sjc04 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd  \n(Bare Metal) | sjc04 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd  \n(Bare Metal) | sjc04 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd  \n(Bare Metal) | sjc04 | 32 cores  \n768GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.48x1536  \n(Bare Metal) | sjc04 | 48 cores  \n1536GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.4x32  \n(Bare Metal) | sjc04 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 2000GB HDD |
| mb4c.4x32.1.9tb.ssd  \n(Bare Metal) | sjc04 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| me4c.4x32  \n(Bare Metal Edge) | sjc04 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd  \n(Bare Metal Edge) | sjc04 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100  \n(Bare Metal GPUs) | sjc04 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n2 P100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100  \n(Bare Metal GPUs) | sjc04 | 48 cores  \n384GB memory  \n10000Mbps network speed  \n2 V100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in San Jose." caption-side="bottom"}
{: #sjc-physical-table}
{: tab-title="Physical"}
{: tab-group="sjc-tables"}


## Sao Paulo (`sao`)
{: #sao-paulo-sao}

| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| b3c.16x64  \n(Balanced) | sao01 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb  \n(Balanced) | sao01 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 300GB SSD |
| b3c.32x128  \n(Balanced) | sao01 | 32 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.4x16  \n(Balanced) | sao01 | 4 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.56x242  \n(Balanced) | sao01 | 56 cores  \n242GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.8x32  \n(Balanced) | sao01 | 8 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.4x32  \n(Memory) | sao01 | 4 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
{: class="simple-tab-table"}
{: caption="VSI flavors in Sao Paulo." caption-side="bottom"}
{: #sao-virtual-table}
{: tab-title="Virtual"}
{: tab-group="sao-tables"}



| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
|No flavors available.| N/A | N/A | N/A | N/A | N/A |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Sao Paulo." caption-side="bottom"}
{: #sao-physical-table}
{: tab-title="Physical"}
{: tab-group="sao-tables"}


## Singapore (`sng`)
{: #singapore-sng}

| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| b3c.16x64  \n(Balanced) | sng01 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb  \n(Balanced) | sng01 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 300GB SSD |
| b3c.4x16  \n(Balanced) | sng01 | 4 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.8x32  \n(Balanced) | sng01 | 8 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x16  \n(Compute) | sng01 | 16 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x32  \n(Compute) | sng01 | 16 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.16x128  \n(Memory) | sng01 | 16 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.30x240  \n(Memory) | sng01 | 30 cores  \n240GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.4x32  \n(Memory) | sng01 | 4 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.8x64  \n(Memory) | sng01 | 8 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
{: class="simple-tab-table"}
{: caption="VSI flavors in Singapore." caption-side="bottom"}
{: #sng-virtual-table}
{: tab-title="Virtual"}
{: tab-group="sng-tables"}



| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
|No flavors available.| N/A | N/A | N/A | N/A | N/A |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Singapore." caption-side="bottom"}
{: #sng-physical-table}
{: tab-title="Physical"}
{: tab-group="sng-tables"}


## Sydney (`syd`)
{: #sydney-syd}

| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| b3c.16x64  \n(Balanced) | syd01  \nsyd04  \nsyd05 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb  \n(Balanced) | syd01  \nsyd04  \nsyd05 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 300GB SSD |
| b3c.32x128  \n(Balanced) | syd01  \nsyd04  \nsyd05 | 32 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.4x16  \n(Balanced) | syd01  \nsyd04  \nsyd05 | 4 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.56x242  \n(Balanced) | syd01  \nsyd04  \nsyd05 | 56 cores  \n242GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.8x32  \n(Balanced) | syd01  \nsyd04  \nsyd05 | 8 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x16  \n(Compute) | syd01  \nsyd04  \nsyd05 | 16 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x32  \n(Compute) | syd01  \nsyd04  \nsyd05 | 16 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x32  \n(Compute) | syd01  \nsyd04  \nsyd05 | 32 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x64  \n(Compute) | syd01  \nsyd04  \nsyd05 | 32 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.16x128  \n(Memory) | syd01  \nsyd04  \nsyd05 | 16 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.30x240  \n(Memory) | syd01  \nsyd04  \nsyd05 | 30 cores  \n240GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.4x32  \n(Memory) | syd01  \nsyd04  \nsyd05 | 4 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.8x64  \n(Memory) | syd01  \nsyd04  \nsyd05 | 8 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
{: class="simple-tab-table"}
{: caption="VSI flavors in Sydney." caption-side="bottom"}
{: #syd-virtual-table}
{: tab-title="Virtual"}
{: tab-group="syd-tables"}



| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| mb4c.20x192  \n(Bare Metal) | syd01  \nsyd04  \nsyd05 | 20 cores  \n192GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x384  \n(Bare Metal) | syd01  \nsyd04  \nsyd05 | 20 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64  \n(Bare Metal) | syd01  \nsyd04  \nsyd05 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd  \n(Bare Metal) | syd01  \nsyd04  \nsyd05 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd  \n(Bare Metal) | syd01  \nsyd04  \nsyd05 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd  \n(Bare Metal) | syd01  \nsyd04  \nsyd05 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd  \n(Bare Metal) | syd01  \nsyd04  \nsyd05 | 32 cores  \n768GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.48x1536  \n(Bare Metal) | syd01  \nsyd04  \nsyd05 | 48 cores  \n1536GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.4x32  \n(Bare Metal) | syd01  \nsyd04  \nsyd05 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 2000GB HDD |
| mb4c.4x32.1.9tb.ssd  \n(Bare Metal) | syd01  \nsyd04  \nsyd05 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| me4c.4x32  \n(Bare Metal Edge) | syd01  \nsyd04  \nsyd05 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd  \n(Bare Metal Edge) | syd01  \nsyd04  \nsyd05 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100  \n(Bare Metal GPUs) | syd01  \nsyd04  \nsyd05 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n2 P100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100  \n(Bare Metal GPUs) | syd01  \nsyd04  \nsyd05 | 48 cores  \n384GB memory  \n10000Mbps network speed  \n2 V100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Sydney." caption-side="bottom"}
{: #syd-physical-table}
{: tab-title="Physical"}
{: tab-group="syd-tables"}


## Tokyo (`tok`)
{: #tokyo-tok}

| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| b3c.16x64  \n(Balanced) | tok02  \ntok04  \ntok05 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb  \n(Balanced) | tok02  \ntok04  \ntok05 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 300GB SSD |
| b3c.32x128  \n(Balanced) | tok02  \ntok04  \ntok05 | 32 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.4x16  \n(Balanced) | tok02  \ntok04  \ntok05 | 4 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.56x242  \n(Balanced) | tok02  \ntok04  \ntok05 | 56 cores  \n242GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.8x32  \n(Balanced) | tok02  \ntok04  \ntok05 | 8 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x16  \n(Compute) | tok02  \ntok04  \ntok05 | 16 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x32  \n(Compute) | tok02  \ntok04  \ntok05 | 16 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x32  \n(Compute) | tok02  \ntok04  \ntok05 | 32 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x64  \n(Compute) | tok02  \ntok04  \ntok05 | 32 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.16x128  \n(Memory) | tok02  \ntok04  \ntok05 | 16 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.30x240  \n(Memory) | tok02  \ntok04  \ntok05 | 30 cores  \n240GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.4x32  \n(Memory) | tok02  \ntok04  \ntok05 | 4 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.8x64  \n(Memory) | tok02  \ntok04  \ntok05 | 8 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
{: class="simple-tab-table"}
{: caption="VSI flavors in Tokyo." caption-side="bottom"}
{: #tok-virtual-table}
{: tab-title="Virtual"}
{: tab-group="tok-tables"}



| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| mb4c.20x192  \n(Bare Metal) | tok02  \ntok04  \ntok05 | 20 cores  \n192GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x384  \n(Bare Metal) | tok02  \ntok04  \ntok05 | 20 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64  \n(Bare Metal) | tok02  \ntok04  \ntok05 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd  \n(Bare Metal) | tok02  \ntok04  \ntok05 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd  \n(Bare Metal) | tok02  \ntok04  \ntok05 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd  \n(Bare Metal) | tok02  \ntok04  \ntok05 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd  \n(Bare Metal) | tok02  \ntok04  \ntok05 | 32 cores  \n768GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.48x1536  \n(Bare Metal) | tok02  \ntok04  \ntok05 | 48 cores  \n1536GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.4x32  \n(Bare Metal) | tok02  \ntok04  \ntok05 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 2000GB HDD |
| mb4c.4x32.1.9tb.ssd  \n(Bare Metal) | tok02  \ntok04  \ntok05 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| me4c.4x32  \n(Bare Metal Edge) | tok02  \ntok04  \ntok05 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd  \n(Bare Metal Edge) | tok02  \ntok04  \ntok05 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100  \n(Bare Metal GPUs) | tok02  \ntok04  \ntok05 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n2 P100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100  \n(Bare Metal GPUs) | tok02  \ntok04  \ntok05 | 48 cores  \n384GB memory  \n10000Mbps network speed  \n2 V100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Tokyo." caption-side="bottom"}
{: #tok-physical-table}
{: tab-title="Physical"}
{: tab-group="tok-tables"}


## Toronto (`tor`)
{: #toronto-tor}

| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| b3c.16x64  \n(Balanced) | tor01 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb  \n(Balanced) | tor01 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 300GB SSD |
| b3c.32x128  \n(Balanced) | tor01 | 32 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.4x16  \n(Balanced) | tor01 | 4 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.56x242  \n(Balanced) | tor01 | 56 cores  \n242GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.8x32  \n(Balanced) | tor01 | 8 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x16  \n(Compute) | tor01 | 16 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x32  \n(Compute) | tor01 | 16 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x32  \n(Compute) | tor01 | 32 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x64  \n(Compute) | tor01 | 32 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.16x128  \n(Memory) | tor01 | 16 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.30x240  \n(Memory) | tor01 | 30 cores  \n240GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.4x32  \n(Memory) | tor01 | 4 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.8x64  \n(Memory) | tor01 | 8 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
{: class="simple-tab-table"}
{: caption="VSI flavors in Toronto." caption-side="bottom"}
{: #tor-virtual-table}
{: tab-title="Virtual"}
{: tab-group="tor-tables"}



| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| mb4c.20x192  \n(Bare Metal) | tor01 | 20 cores  \n192GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x384  \n(Bare Metal) | tor01 | 20 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64  \n(Bare Metal) | tor01 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd  \n(Bare Metal) | tor01 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd  \n(Bare Metal) | tor01 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd  \n(Bare Metal) | tor01 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd  \n(Bare Metal) | tor01 | 32 cores  \n768GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.48x1536  \n(Bare Metal) | tor01 | 48 cores  \n1536GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.4x32  \n(Bare Metal) | tor01 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 2000GB HDD |
| mb4c.4x32.1.9tb.ssd  \n(Bare Metal) | tor01 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| me4c.4x32  \n(Bare Metal Edge) | tor01 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd  \n(Bare Metal Edge) | tor01 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100  \n(Bare Metal GPUs) | tor01 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n2 P100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100  \n(Bare Metal GPUs) | tor01 | 48 cores  \n384GB memory  \n10000Mbps network speed  \n2 V100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Toronto." caption-side="bottom"}
{: #tor-physical-table}
{: tab-title="Physical"}
{: tab-group="tor-tables"}


## Washington DC (`wdc`)
{: #washington-dc-wdc}

| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| b3c.16x64  \n(Balanced) | wdc04  \nwdc06  \nwdc07 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb  \n(Balanced) | wdc04  \nwdc06  \nwdc07 | 16 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 300GB SSD |
| b3c.32x128  \n(Balanced) | wdc04  \nwdc06  \nwdc07 | 32 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.4x16  \n(Balanced) | wdc04  \nwdc06  \nwdc07 | 4 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.56x242  \n(Balanced) | wdc04  \nwdc06  \nwdc07 | 56 cores  \n242GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| b3c.8x32  \n(Balanced) | wdc04  \nwdc06  \nwdc07 | 8 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x16  \n(Compute) | wdc04  \nwdc06  \nwdc07 | 16 cores  \n16GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.16x32  \n(Compute) | wdc04  \nwdc06  \nwdc07 | 16 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x32  \n(Compute) | wdc04  \nwdc06  \nwdc07 | 32 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| c3c.32x64  \n(Compute) | wdc04  \nwdc06  \nwdc07 | 32 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.16x128  \n(Memory) | wdc04  \nwdc06  \nwdc07 | 16 cores  \n128GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.30x240  \n(Memory) | wdc04  \nwdc06  \nwdc07 | 30 cores  \n240GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.4x32  \n(Memory) | wdc04  \nwdc06  \nwdc07 | 4 cores  \n32GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
| m3c.8x64  \n(Memory) | wdc04  \nwdc06  \nwdc07 | 8 cores  \n64GB memory  \n1000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 25GB SSD | 100GB SSD |
{: class="simple-tab-table"}
{: caption="VSI flavors in Washington DC." caption-side="bottom"}
{: #wdc-virtual-table}
{: tab-title="Virtual"}
{: tab-group="wdc-tables"}



| Name | Data centers | Resources | OS | Primary storage | Secondary storage |
| ---- | ---- |-------------------------------- | ---- | --------------- | ----------------- |  
| mb4c.20x192  \n(Bare Metal) | wdc04  \nwdc06  \nwdc07 | 20 cores  \n192GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x384  \n(Bare Metal) | wdc04  \nwdc06  \nwdc07 | 20 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64  \n(Bare Metal) | wdc04  \nwdc06  \nwdc07 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd  \n(Bare Metal) | wdc04  \nwdc06  \nwdc07 | 20 cores  \n64GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd  \n(Bare Metal) | wdc04  \nwdc06  \nwdc07 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd  \n(Bare Metal) | wdc04  \nwdc06  \nwdc07 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd  \n(Bare Metal) | wdc04  \nwdc06  \nwdc07 | 32 cores  \n768GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.48x1536  \n(Bare Metal) | wdc04  \nwdc06  \nwdc07 | 48 cores  \n1536GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mb4c.4x32  \n(Bare Metal) | wdc04  \nwdc06  \nwdc07 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 2000GB HDD |
| mb4c.4x32.1.9tb.ssd  \n(Bare Metal) | wdc04  \nwdc06  \nwdc07 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| me4c.4x32  \n(Bare Metal Edge) | wdc04  \nwdc06  \nwdc07 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd  \n(Bare Metal Edge) | wdc04  \nwdc06  \nwdc07 | 4 cores  \n32GB memory  \n10000Mbps network speed  \n No GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100  \n(Bare Metal GPUs) | wdc04  \nwdc06  \nwdc07 | 32 cores  \n384GB memory  \n10000Mbps network speed  \n2 P100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100  \n(Bare Metal GPUs) | wdc04  \nwdc06  \nwdc07 | 48 cores  \n384GB memory  \n10000Mbps network speed  \n2 V100 GPUs |  REDHAT_7_64  \n REDHAT_8_64  \n RHEL_9_64  \n| 2000GB HDD | 960GB SSD |
{: class="simple-tab-table"}
{: caption="Bare metal flavors in Washington DC." caption-side="bottom"}
{: #wdc-physical-table}
{: tab-title="Physical"}
{: tab-group="wdc-tables"}
