---

copyright: 
  years: 2014, 2023
lastupdated: "2023-04-14"

keywords: openshift, node scaling, ca, autoscaler

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Classic flavors
{: #classic-flavors}

Review the classic worker node flavors by metro.





## `ams`
{: #ams}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| b3c.16x64 | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 300GB SSD |
| b3c.32x128 | 128GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.4x16 | 16GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.56x242 | 242GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.8x32 | 32GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x32 | 32GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x64 | 64GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.4x32 | 32GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 192GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 384GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 768GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 1536GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 384GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 4GB | 1000Mbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
{: caption="Table 1. Worker node flavors for Amsterdam." caption-side="bottom"}



## `che`
{: #che}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| b3c.16x64 | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 300GB SSD |
| b3c.32x128 | 128GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.4x16 | 16GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.56x242 | 242GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.8x32 | 32GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x32 | 32GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x64 | 64GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.4x32 | 32GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 192GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 384GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 768GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 1536GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 384GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 4GB | 1000Mbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
{: caption="Table 2. Worker node flavors for Chennai." caption-side="bottom"}



## `dal`
{: #dal}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| b3c.16x64 | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 300GB SSD |
| b3c.32x128 | 128GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.4x16 | 16GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.56x242 | 242GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.8x32 | 32GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x32 | 32GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x64 | 64GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.16x128 | 128GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.30x240 | 240GB | 1000Mbps | 30 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.48x384 | 384GB | 1000Mbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.4x32 | 32GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.56x448 | 448GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.64x512 | 512GB | 1000Mbps | 64 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.8x64 | 64GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 192GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 384GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 768GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 1536GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 384GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 4GB | 1000Mbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
{: caption="Table 3. Worker node flavors for Dallas." caption-side="bottom"}



## `fra`
{: #fra}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| b3c.16x64 | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 300GB SSD |
| b3c.32x128 | 128GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.4x16 | 16GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.56x242 | 242GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.8x32 | 32GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x32 | 32GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x64 | 64GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.16x128 | 128GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.30x240 | 240GB | 1000Mbps | 30 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.4x32 | 32GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.8x64 | 64GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 192GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 384GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 768GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 1536GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 384GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 4GB | 1000Mbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
{: caption="Table 4. Worker node flavors for France." caption-side="bottom"}



## `lon`
{: #lon}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| b3c.16x64 | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 300GB SSD |
| b3c.32x128 | 128GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.4x16 | 16GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.56x242 | 242GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.8x32 | 32GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x32 | 32GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x64 | 64GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.16x128 | 128GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.30x240 | 240GB | 1000Mbps | 30 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.4x32 | 32GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.8x64 | 64GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 192GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 384GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 768GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 1536GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 384GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 4GB | 1000Mbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
{: caption="Table 5. Worker node flavors for London." caption-side="bottom"}



## `mil`
{: #mil}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| b3c.16x64 | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 300GB SSD |
| b3c.32x128 | 128GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.4x16 | 16GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.56x242 | 242GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.8x32 | 32GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x32 | 32GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x64 | 64GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.4x32 | 32GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 192GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 384GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 768GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 1536GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 384GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 4GB | 1000Mbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
{: caption="Table 6. Worker node flavors for Milan." caption-side="bottom"}



## `mon`
{: #mon}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| b3c.16x64 | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 300GB SSD |
| b3c.32x128 | 128GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.4x16 | 16GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.56x242 | 242GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.8x32 | 32GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x32 | 32GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x64 | 64GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.4x32 | 32GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 192GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 384GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 768GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 1536GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 384GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 4GB | 1000Mbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
{: caption="Table 7. Worker node flavors for Montreal." caption-side="bottom"}



## `osa`
{: #osa}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| b3c.16x64 | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 300GB SSD |
| b3c.32x128 | 128GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.4x16 | 16GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.56x242 | 242GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.8x32 | 32GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x32 | 32GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x64 | 64GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.16x128 | 128GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.30x240 | 240GB | 1000Mbps | 30 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.48x384 | 384GB | 1000Mbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.4x32 | 32GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.56x448 | 448GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.64x512 | 512GB | 1000Mbps | 64 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.8x64 | 64GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 192GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 384GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 768GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 1536GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 384GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 4GB | 1000Mbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
{: caption="Table 8. Worker node flavors for Osaka." caption-side="bottom"}



## `par`
{: #par}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| b3c.16x64 | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 300GB SSD |
| b3c.32x128 | 128GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.4x16 | 16GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.56x242 | 242GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.8x32 | 32GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x32 | 32GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x64 | 64GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.16x128 | 128GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.30x240 | 240GB | 1000Mbps | 30 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.4x32 | 32GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.8x64 | 64GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 192GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 384GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 768GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 1536GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 384GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 4GB | 1000Mbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
{: caption="Table 9. Worker node flavors for Paris." caption-side="bottom"}



## `sao`
{: #sao}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| b3c.16x64 | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 300GB SSD |
| b3c.32x128 | 128GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.4x16 | 16GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.56x242 | 242GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.8x32 | 32GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.4x32 | 32GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| u3c.2x4 | 4GB | 1000Mbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
{: caption="Table 10. Worker node flavors for South America." caption-side="bottom"}



## `sjc`
{: #sjc}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| b3c.16x64 | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 300GB SSD |
| b3c.32x128 | 128GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.4x16 | 16GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.56x242 | 242GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.8x32 | 32GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x32 | 32GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x64 | 64GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.4x32 | 32GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| u3c.2x4 | 4GB | 1000Mbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
{: caption="Table 11. Worker node flavors for San Jose." caption-side="bottom"}



## `sng`
{: #sng}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| b3c.16x64 | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 300GB SSD |
| b3c.4x16 | 16GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.8x32 | 32GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x32 | 32GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.4x32 | 32GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| u3c.2x4 | 4GB | 1000Mbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
{: caption="Table 12. Worker node flavors for Singapore." caption-side="bottom"}



## `syd`
{: #syd}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| b3c.16x64 | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 300GB SSD |
| b3c.32x128 | 128GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.4x16 | 16GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.56x242 | 242GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.8x32 | 32GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x32 | 32GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x64 | 64GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.16x128 | 128GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.30x240 | 240GB | 1000Mbps | 30 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.4x32 | 32GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.8x64 | 64GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 192GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 384GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 768GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 1536GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 384GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 4GB | 1000Mbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
{: caption="Table 13. Worker node flavors for Sydney." caption-side="bottom"}



## `tok`
{: #tok}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| b3c.16x64 | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 300GB SSD |
| b3c.32x128 | 128GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.4x16 | 16GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.56x242 | 242GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.8x32 | 32GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x32 | 32GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x64 | 64GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.16x128 | 128GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.30x240 | 240GB | 1000Mbps | 30 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.4x32 | 32GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.8x64 | 64GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 192GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 384GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 768GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 1536GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 384GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 4GB | 1000Mbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
{: caption="Table 14. Worker node flavors for Tokyo." caption-side="bottom"}



## `tor`
{: #tor}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| b3c.16x64 | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 300GB SSD |
| b3c.32x128 | 128GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.4x16 | 16GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.56x242 | 242GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.8x32 | 32GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x32 | 32GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x64 | 64GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.16x128 | 128GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.30x240 | 240GB | 1000Mbps | 30 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.4x32 | 32GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.8x64 | 64GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 192GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 384GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 768GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 1536GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 384GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 4GB | 1000Mbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
{: caption="Table 15. Worker node flavors for Toronto." caption-side="bottom"}



## `wdc`
{: #wdc}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| b3c.16x64 | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 64GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 300GB SSD |
| b3c.32x128 | 128GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.4x16 | 16GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.56x242 | 242GB | 1000Mbps | 56 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| b3c.8x32 | 32GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.16x32 | 32GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| c3c.32x64 | 64GB | 1000Mbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.16x128 | 128GB | 1000Mbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.30x240 | 240GB | 1000Mbps | 30 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.4x32 | 32GB | 1000Mbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| m3c.8x64 | 64GB | 1000Mbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 192GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 384GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 64GB | 10000Mbps | 20 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 768GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 1536GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 32GB | 10000Mbps | 4 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 384GB | 10000Mbps | 32 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 384GB | 10000Mbps | 48 | Physical | **REDHAT_7_64 (default)**, REDHAT_8_64| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 4GB | 1000Mbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 25GB SSD | 100GB SSD |
{: caption="Table 16. Worker node flavors for Washington DC." caption-side="bottom"}






